---
title: Unity URP 定制渲染管线
tag:
- Unity
- Game
- GL
categories:
- Unity
- Game
- GL
mermaid: true
image:
    path: /assets/img/2023-05-24-custom-urp/example.gif
---

本意是想做一个渲染效果, 几个 camera 始终在同一个 transform, 各自渲染到各自的 render-texture, 然后把每一个 camera 的 render-texture 做一个融合.  
然后按照各自的 depth-texture 决定哪个像素点显示在上面  

因为我一直用 URP ( 因为 shader graph ), 所以要达到这样的效果必须定制管线了  

## 例子

### 例子0

对卡车做像素化, 场景里的其他GameObject保持不变

![](/assets/img/2023-05-24-custom-urp/example.gif)

### 例子1

红绿方块在不同的 camera 的不同 render-texture 里, 让它在主相机里用 depth 做融合

![](/assets/img/2023-05-24-custom-urp/urp.gif)

## 思路

为每一个 camera 准备两个 render-texture, color-rt 和 depth-rt,  
每一个 camera 渲染结束之后都把 camera 的 color-target 和 depth-target 存放到对应的 rt 里.  

等到 main-camera 渲染的时候, 把所有 camera 的 color 和 depth, 用 CommandBuffer.SetGlobalTexture 填到里头  

然后对 main-camera 做一次 self Blit, 把所有的 color 和 depth 做融合   

## 注意

- Blit camera 的 depth-texture 的时候要 * 255 !!
- pass 的 event 要设置成 Before Rendering Post Processing !!

## Shader

### BlitColor

```
Shader "Hidden/BlitColor"
{
    Properties
    {
    }

    SubShader
    {
        Pass{
            Tags { 
                // "LightMode" = ""
            }

            CGPROGRAM

            #pragma vertex vert
            #pragma fragment frag

            #pragma target 3.0

            #include "UnityCG.cginc"

            sampler2D _CameraColorAttachment;
            sampler2D _CameraColorAttachmentA;
            sampler2D _CameraDepthTexture;
            sampler2D _SourceTex;
            sampler2D _MainTex;

            struct appdata {
                float4 vertex : POSITION;
                float2 uv : TEXCOORD0;
                float3 normal : NORMAL;
            };

            struct v2f {
                float4 position : SV_POSITION;
                float2 uv : TEXCOORD0;
            };

            v2f vert (appdata IN) {
                v2f OUT;
                
                OUT.position = UnityObjectToClipPos(IN.vertex);

                OUT.uv = IN.uv;

                return OUT;
            }

            fixed4 frag (v2f IN) : SV_TARGET {
                float4 color = tex2D(_SourceTex, IN.uv);
                return color;
            }

            ENDCG
        }
    }
}
```

### BlitDepth

```glsl
Shader "Hidden/BlitDepth"
{
    Properties
    {
    }

    SubShader
    {
        Pass{
            Tags { 
                // "LightMode" = ""
            }

            CGPROGRAM

            #pragma vertex vert
            #pragma fragment frag

            #pragma target 3.0

            #include "UnityCG.cginc"
            
            sampler2D _CameraColorAttachment;
            sampler2D _CameraColorAttachmentA;
            sampler2D _CameraDepthTexture;
            sampler2D _SourceTex;
            sampler2D _MainTex;

            struct appdata {
                float4 vertex : POSITION;
                float2 uv : TEXCOORD0;
                float3 normal : NORMAL;
            };

            struct v2f {
                float4 position : SV_POSITION;
                float2 uv : TEXCOORD0;
            };

            v2f vert (appdata IN) {
                v2f OUT;
                
                OUT.position = UnityObjectToClipPos(IN.vertex);

                OUT.uv = IN.uv;

                return OUT;
            }

            float frag (v2f IN) : SV_TARGET {
                float depth = tex2D(_CameraDepthTexture, IN.uv);

                depth = depth * 255;

                // if(depth == 0){
                //     return 0;
                // }else{
                //     return 1;
                // }

                return depth;
            }

            ENDCG
        }
    }
}
```

### Merge

```glsl
Shader "Hidden/Merge"
{
    Properties
    {
    }

    SubShader
    {
        Pass{
            Tags { 
                // "LightMode" = ""
            }

            CGPROGRAM

            #pragma vertex vert
            #pragma fragment frag

            #pragma target 3.0

            #include "UnityCG.cginc"

            sampler2D MainCameraColor;
            sampler2D TestCameraColor;

            sampler2D MainCameraDepth;
            sampler2D TestCameraDepth;

            struct appdata {
                float4 vertex : POSITION;
                float2 uv : TEXCOORD0;
                float3 normal : NORMAL;
            };

            struct v2f {
                float4 position : SV_POSITION;
                float2 uv : TEXCOORD0;
            };

            v2f vert (appdata IN) {
                v2f OUT;
                
                OUT.position = UnityObjectToClipPos(IN.vertex);

                OUT.uv = IN.uv;

                return OUT;
            }

            float4 frag (v2f IN) : SV_TARGET {
                float depthMain = tex2D(MainCameraDepth, IN.uv);
                float depthTest = tex2D(TestCameraDepth, IN.uv);

                float4 colorMain = tex2D(MainCameraColor, IN.uv);
                float4 colorTest = tex2D(TestCameraColor, IN.uv);

                // return 0;

                if(depthMain > depthTest){
                    return colorMain;
                }else{
                    return colorTest;
                }
            }

            ENDCG
        }
    }
}
```

## CS脚本

### MergeRenderPass

```cs
using UnityEngine;
using UnityEngine.Rendering;
using UnityEngine.Rendering.Universal;
using UnityEngine.Experimental.Rendering;
using System.Collections;
using System.Collections.Generic;

[System.Serializable]
public class MergeRenderPass : ScriptableRenderPass
{
    [SerializeField]
    private MergeRenderPassFeatureSettings settings;

    CommandBuffer cmd;

    Dictionary<string, RenderTexture> name2ColorRT;
    Dictionary<string, RenderTexture> name2DepthRT;

    Material BlitColor;
    Material BlitDepth;
    Material Merge;
    Material MergeDepth;

    public MergeRenderPass(MergeRenderPassFeatureSettings settings){
        this.settings = settings;

        cmd = new CommandBuffer();
        cmd.name = "Merge";

        if(settings.name2ColorRT != null){
            settings.name2ColorRT.Clear();
        }
        if(settings.name2DepthRT != null){
            settings.name2DepthRT.Clear();
        }
    }

    private Camera main;
    private Camera camera;
    private string cameraName;
    private RenderTargetIdentifier cameraColorTarget;
    private RenderTargetIdentifier cameraDepthTarget;

    private List<string> allCameraNames = new List<string>();

    private int width, height;

    public override void Configure(CommandBuffer cmd, RenderTextureDescriptor cameraTextureDescriptor){

    }

    public override void OnCameraSetup(CommandBuffer cmd, ref RenderingData renderingData){
        this.cameraColorTarget = renderingData.cameraData.renderer.cameraColorTarget;
        this.cameraDepthTarget = renderingData.cameraData.renderer.cameraDepthTarget;

        this.camera = renderingData.cameraData.camera;
        this.cameraName = this.camera.name.Replace(" ", "_");

        this.renderPassEvent = settings.renderPassEvent;

        this.BlitColor = settings.BlitColor;
        this.BlitDepth = settings.BlitDepth;
        this.Merge = settings.Merge;

        if(settings.name2ColorRT == null){
            settings.name2ColorRT = new Dictionary<string, RenderTexture>();
        }
        if(settings.name2DepthRT == null){
            settings.name2DepthRT = new Dictionary<string, RenderTexture>();
        }

        this.name2ColorRT = settings.name2ColorRT;
        this.name2DepthRT = settings.name2DepthRT;

        if(this.width != Screen.width || this.height != Screen.height){
            
            foreach(var key in name2ColorRT.Keys){
                var rt = name2ColorRT[key];
                rt.Release();
                rt.width = Screen.width;
                rt.height = Screen.height;
                rt.Create();
            } 

            foreach(var key in name2DepthRT.Keys){
                var rt = name2DepthRT[key];
                rt.Release();
                rt.width = Screen.width;
                rt.height = Screen.height;
                rt.Create();
            }
        }

        this.width = Screen.width;
        this.height = Screen.height;
    }

    public override void Execute(ScriptableRenderContext context, ref RenderingData renderingData)
    {
        string colorRTName = cameraName + "Color";
        string depthRTName = cameraName + "Depth";

        RenderTexture colorTexture = GetColorTexture(colorRTName);
        RenderTexture depthTexture = GetDepthTexture(depthRTName);
        
        cmd.SetGlobalTexture(colorRTName, colorTexture);
        cmd.SetGlobalTexture(depthRTName, depthTexture);

        ExecuteCmd(context);

        Blit(cmd, cameraDepthTarget, depthTexture, this.BlitDepth);
        Blit(cmd, cameraColorTarget, colorTexture);

        ExecuteCmd(context);

        context.Submit();

        if(camera == Camera.main){     
            MergeRT();
            ExecuteCmd(context);
        }
    }

    public void ExecuteCmd(ScriptableRenderContext context){
        context.ExecuteCommandBuffer(cmd);
        
        cmd.Clear();
    }

    RenderTexture GetColorTexture(string name){
        RenderTexture rt;
        if(name2ColorRT.ContainsKey(name)){
            return name2ColorRT[name];
        }
        rt = new RenderTexture(this.width, this.height, 0, RenderTextureFormat.ARGB32);
        rt.name = name;
        name2ColorRT[name] = rt;
        return rt;
    }

    RenderTexture GetDepthTexture(string name){
        RenderTexture rt;
        if(name2DepthRT.ContainsKey(name)){
            return name2DepthRT[name];
        }
        rt = new RenderTexture(this.width, this.height, 0, RenderTextureFormat.R8);
        rt.name = name;
        name2DepthRT[name] = rt;
        return rt;
    }

    void MergeRT(){
        Debug.Log("MergeRT");

        cmd.Blit(cameraColorTarget, cameraColorTarget, this.Merge);
    }
}
```

### MergeRenderPassFeatureSettings

```cs
using UnityEngine;
using UnityEngine.Rendering;
using UnityEngine.Rendering.Universal;
using System.Collections;
using System.Collections.Generic;

[System.Serializable]
public class MergeRenderPassFeatureSettings {
    [SerializeField]
    public Dictionary<string, RenderTexture> name2ColorRT;
    [SerializeField]
    public Dictionary<string, RenderTexture> name2DepthRT;
    [SerializeField]
    public Material BlitColor;
    [SerializeField]
    public Material BlitDepth;
    [SerializeField]
    public Material Merge;

    [SerializeField]
    public RenderPassEvent renderPassEvent;
}
```

### MergeRenderPassFeature

```cs
using UnityEngine;
using UnityEngine.Rendering;
using UnityEngine.Rendering.Universal;
using System.Collections;
using System.Collections.Generic;

public class MergeRenderPassFeature : ScriptableRendererFeature
{
    MergeRenderPass m_ScriptablePass;
    [SerializeField]
    MergeRenderPassFeatureSettings settings;

    /// <inheritdoc/>
    public override void Create()
    {
        m_ScriptablePass = new MergeRenderPass(settings);
    }

    // Here you can inject one or multiple render passes in the renderer.
    // This method is called when setting up the renderer once per-camera.
    public override void AddRenderPasses(ScriptableRenderer renderer, ref RenderingData renderingData)
    {
        renderer.EnqueuePass(m_ScriptablePass);
    }
}
```