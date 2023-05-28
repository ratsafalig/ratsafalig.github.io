---
title: 像素化 Shader ( Pixelation Shader )
categories:
- Shader
author: 航
tags:
- Shader
image:
    path: /assets/img/2023-05-01-pixelation-shader/pixelation.gif
---


## 局部像素化 ( Local Pixelation )

### Canvas 叠加实现

如果要实现，某个物体是像素化的，其他物体是正常渲染的，可以使用局部像素化的技术：  

![](/assets/img/2023-05-01-pixelation-shader/pixelation.gif)

实现方法如下：  

1. 给想要像素化的 GameObject 打上 tag，比如 pixel tag
2. 创建三个 Camera，一个渲染 pixel tag 的 GameObject （ pixel camera ），一个渲染 pixel tag 的深度 （ depth camera ），一个渲染最终游戏画面 （ main camera ）
    - pixel camera 和 depth camera 的 culling mask 设置城 pixel tag，并把结果分别渲染到 pixel texture 和 depth texture
    ![](/assets/img/2023-05-01-pixelation-shader/pixel-camera.png)
    ![](/assets/img/2023-05-01-pixelation-shader/depth-camera.png)
    - main camera 的 culling mask 设置成除了 pixel tag 外的所有 Game Object
    ![](/assets/img/2023-05-01-pixelation-shader/main-camera.png)
3. 在 main camera 前加一个 canvas，在上面把 depth texture 当作深度测试，把 pixel texture 画出来
![](/assets/img/2023-05-01-pixelation-shader/canvas.png)

### 定制渲染管线实现

自定义渲染管线, 在另一篇 Blog 里实现了 [custom-urp](/posts/custom-urp)

## 全局像素化 ( Global Pixelation )

借助 on-render-image, 可以简单的实现场景的全局像素风格化  

像素化前：

![raw](/assets/img/2023-05-01-pixelation-shader/raw.png)

像素化后：

![dst](/assets/img/2023-05-01-pixelation-shader/dst.png)

```glsl
Shader "Custom/PostProcessing"
{
    Properties
    {
        _MainTex ("MainTex", 2D) = "white" {}
        _pw("Pixel Width", float) = 64
        _ph("Pixel Height", float) = 64
    }
    SubShader
    {
        Tags { "RenderType"="Opaque" }

        LOD 200

        Cull Off ZWrite Off ZTest Always

        Pass{
            CGPROGRAM

            #pragma vertex vert
            #pragma fragment frag

            #pragma target 3.0

            #include "UnityCG.cginc"

            sampler2D _MainTex;

            float _pw;
            float _ph;

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

                float _dx;
                float _dy;

                _dx = _pw * ( 1 / _ScreenParams.x );
                _dy = _ph * ( 1 / _ScreenParams.y );
                
                float2 coord = float2(_dx * round(IN.uv.x / _dx), _dy * round(IN.uv.y / _dy));

                fixed4 color = tex2D(_MainTex, coord);

                return color;
            }

            ENDCG
        }
    }
    FallBack "Diffuse"
}
```

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[ExecuteAlways]
public class Pixelation : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        
    }

    public Material material;

    void OnRenderImage(RenderTexture source,RenderTexture destination){
        RenderTexture src = RenderTexture.GetTemporary(source.width, source.height);
        material.SetTexture("_MainTex", source);
        Graphics.Blit(source,src,material,0);
        Graphics.Blit(src,destination,material,0);
        RenderTexture.ReleaseTemporary(src);
    }
}
```