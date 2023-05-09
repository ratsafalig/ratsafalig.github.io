---
title: Deferred Shading
tags:
- GL
- Game
categories:
- AI
- Game
---

Deferred shading和Forward shading是两种3D图形渲染技术。

在Forward shading中，所有物体都将进行逐像素着色，所以它直接使用几何中的信息。每个像素都被处理，以确定它是最终图像中的颜色。Forward shading的主要优点是它在实时渲染方面的速度非常快，但缺点是它在真正大型场景中的效率可能会下降。

相比而言，Deferred shading只需要对每个像素一个基本的几何信息。这个g-buffer包含了几何信息如深度、法线和材质信息，后续的lighting和shading处理是针对每个像素的各种属性，而不是基本几何信息。Deferred shading可以实现大型场景下实时渲染，并且因为不需要对每个物体都进行逐像素着色，因此它可以使用非常大的照明数据集，而且不会影响性能。不过，Deferred shading需要比Forward shading更多的内存，并有需要创建额外Render pass的额外开销。

以下是示例（出自Unity官方文档）：

在Deferred Shading中，几何渲染到GBuffer中，然后照明和材质计算在延迟阶段进行：

```
Geometry Pass:
Render scene geometry to GBuffer
-Depth
-Normal
-Albedo
-Specular/Metallic (packed into Alpha)

Lighting Pass:
For each light:
-Render light geometry to the stencil buffer (where the light is)
-Add light contribution to light accumulation buffer (with stencil mask)
```

在Forward Shading中，对于每个像素，直接使用自身的几何信息，对其进行光照和材质渲染。

```
Per-pixel Rendering
For each light:
-Render scene geometry
-Compute diffuse and specular light contribution for each light 
-Combine light contribution within shader
```

# Geometry Pass

```glsl
#version 330 core
layout (location = 0) in vec3 aPos;
layout (location = 1) in vec3 aNormal;
layout (location = 2) in vec2 aTexCoords;

out vec3 FragPos;
out vec2 TexCoords;
out vec3 Normal;

uniform mat4 model;
uniform mat4 view;
uniform mat4 projection;

void main()
{
    vec4 worldPos = model * vec4(aPos, 1.0);
    FragPos = worldPos.xyz; 
    TexCoords = aTexCoords;
    
    mat3 normalMatrix = transpose(inverse(mat3(model)));
    Normal = normalMatrix * aNormal;

    gl_Position = projection * view * worldPos;
}
```

```glsl
#version 330 core
layout (location = 0) out vec3 gPosition;
layout (location = 1) out vec3 gNormal;
layout (location = 2) out vec4 gAlbedoSpec;

in vec2 TexCoords;
in vec3 FragPos;
in vec3 Normal;

uniform sampler2D texture_diffuse1;
uniform sampler2D texture_specular1;

void main()
{    
    // store the fragment position vector in the first gbuffer texture
    gPosition = FragPos;
    // also store the per-fragment normals into the gbuffer
    gNormal = normalize(Normal);
    // and the diffuse per-fragment color
    gAlbedoSpec.rgb = texture(texture_diffuse1, TexCoords).rgb;
    // store specular intensity in gAlbedoSpec's alpha component
    gAlbedoSpec.a = texture(texture_specular1, TexCoords).r;
}
```

# Lighting Pass

```glsl
#version 330 core
layout (location = 0) in vec3 aPos;
layout (location = 1) in vec2 aTexCoords;

out vec2 TexCoords;

void main()
{
    TexCoords = aTexCoords;
    gl_Position = vec4(aPos, 1.0);
}
```

```glsl
#version 330 core
out vec4 FragColor;

in vec2 TexCoords;

uniform sampler2D gPosition;
uniform sampler2D gNormal;
uniform sampler2D gAlbedoSpec;

struct Light {
    vec3 Position;
    vec3 Color;
    
    float Linear;
    float Quadratic;
};
const int NR_LIGHTS = 32;
uniform Light lights[NR_LIGHTS];
uniform vec3 viewPos;

void main()
{             
    // retrieve data from gbuffer
    vec3 FragPos = texture(gPosition, TexCoords).rgb;
    vec3 Normal = texture(gNormal, TexCoords).rgb;
    vec3 Diffuse = texture(gAlbedoSpec, TexCoords).rgb;
    float Specular = texture(gAlbedoSpec, TexCoords).a;
    
    // then calculate lighting as usual
    vec3 lighting  = Diffuse * 0.1; // hard-coded ambient component
    vec3 viewDir  = normalize(viewPos - FragPos);
    for(int i = 0; i < NR_LIGHTS; ++i)
    {
        // diffuse
        vec3 lightDir = normalize(lights[i].Position - FragPos);
        vec3 diffuse = max(dot(Normal, lightDir), 0.0) * Diffuse * lights[i].Color;
        // specular
        vec3 halfwayDir = normalize(lightDir + viewDir);  
        float spec = pow(max(dot(Normal, halfwayDir), 0.0), 16.0);
        vec3 specular = lights[i].Color * spec * Specular;
        // attenuation
        float distance = length(lights[i].Position - FragPos);
        float attenuation = 1.0 / (1.0 + lights[i].Linear * distance + lights[i].Quadratic * distance * distance);
        diffuse *= attenuation;
        specular *= attenuation;
        lighting += diffuse + specular;        
    }
    FragColor = vec4(lighting, 1.0);
}

```