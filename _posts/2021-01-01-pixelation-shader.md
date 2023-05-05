---
title: 像素化 Shader ( Pixelation Shader )
categories: [ Shader ]
author: 航
tags:
- Shader
layout: post
toc: true
---

# 全局像素化 ( Global Pixelation )

借助 on-render-image, 可以简单的实现场景的全局像素风格化  
成品如下  
代码如下  

![raw](/assets/img/2021-01-01-pixelation-shader/raw.png)
![dst](/assets/img/2021-01-01-pixelation-shader/dst.png)

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

# 局部像素化 ( Local Pixelation )
