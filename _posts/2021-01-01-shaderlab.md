---
title: ShaderLab
tags:
- Unity
- Game
- GL
- Shader
categories:
- Unity
- Game
- GL
- Shader
---

## ShaderLab Syntax

```
// colored vertex lighting
Shader "Simple colored lighting"
{
    // a single color property
    Properties {
        _Color ("Main Color", Color) = (1,.5,.5,1)
    }
    // define one subshader
    SubShader
    {
        // a single pass in our subshader
        Pass
        {
            // use fixed function per-vertex lighting
            Material
            {
                Diffuse [_Color]
            }
            Lighting On
        }
    }
}
```

### Properties

```
Properties { Property [Property ...] }

---

name ("display name", Range (min, max)) = number
name ("display name", Float) = number
name ("display name", Int) = number

---

name ("display name", Color) = (number,number,number,number)
name ("display name", Vector) = (number,number,number,number)
```

Example

```
// properties for a water shader
Properties
{
    _WaveScale ("Wave scale", Range (0.02,0.15)) = 0.07 // sliders
    _ReflDistort ("Reflection distort", Range (0,1.5)) = 0.5
    _RefrDistort ("Refraction distort", Range (0,1.5)) = 0.4
    _RefrColor ("Refraction color", Color) = (.34, .85, .92, 1) // color
    _ReflectionTex ("Environment Reflection", 2D) = "" {} // textures
    _RefractionTex ("Environment Refraction", 2D) = "" {}
    _Fresnel ("Fresnel (A) ", 2D) = "" {}
    _BumpMap ("Bumpmap (RGB) ", 2D) = "" {}
}
```

### ShaderLab: SubShader

```
Subshader { [Tags] [CommonState] Passdef [Passdef ...] }
```

Example

```
// ...
SubShader {
    Pass {
        Lighting Off
        SetTexture [_MainTex] {}
    }
}
// ...
```

### ShaderLab: Pass

```
Pass { [Name and Tags] [RenderSetup] }

---

Cull Back | Front | Off

ZTest (Less | Greater | LEqual | GEqual | Equal | NotEqual | Always)

ZWrite On | Off

Offset OffsetFactor, OffsetUnits

Blend sourceBlendMode destBlendMode
Blend sourceBlendMode destBlendMode, alphaSourceBlendMode alphaDestBlendMode
BlendOp colorOp
BlendOp colorOp, alphaOp
AlphaToMask On | Off

ColorMask RGB | A | 0 | any combination of R, G, B, A

Lighting On | Off
Material { Material Block }
SeparateSpecular On | Off
Color Color-value
ColorMaterial AmbientAndDiffuse | Emission

Fog { Fog Block }

AlphaTest (Less | Greater | LEqual | GEqual | Equal | NotEqual | Always) CutoffValue

SetTexture textureProperty { combine options }
```

### ShaderLab: Fallback

```
Fallback "name"

Fallback Off

Shader "example" {
    // properties and subshaders here...
    Fallback "otherexample"
}
```

### ShaderLab: CustomEditor

```
CustomEditor "name"

Shader "example" {
    // properties and subshaders here...
    CustomEditor "MyCustomEditor"
}
```

## Link

[SL-Shader](https://docs.unity3d.com/2018.1/Documentation/Manual/SL-Shader.html)