---
title: ShaderLab
tags:
- Unity
- Game
- GL
categories:
- Unity
- Game
- GL
---

```
Shader "<name>"
{
    <optional: Material properties>
    <One or more SubShader definitions>
    <optional: custom editor>
    <optional: fallback>
} 
```

```
Signature	Function
SubShader
{
    <optional: LOD>
    <optional: tags>
    <optional: commands>
    <One or more Pass definitions>
}
```

# Built-in Render Pipeline

```
Shader "Examples/SinglePass"
{
    SubShader
    {
        Tags { "ExampleSubShaderTagKey" = "ExampleSubShaderTagValue" }
        LOD 100

         // ShaderLab commands that apply to the whole SubShader go here. 

        Pass
        {                
              Name "ExamplePassName"
              Tags { "ExamplePassTagKey" = "ExamplePassTagValue" }

              // ShaderLab commands that apply to this Pass go here.

              // HLSL code goes here.
        }
    }
}
```

# URP