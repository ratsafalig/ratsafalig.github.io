---
title: Unity Shader
date: 2021-03-04 00:00:00 Z
tags:
- Unity
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Unity Shader"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2021-03-04T08:00:00+08:00">
    <meta itemprop="keywords" content="Unity"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Unity Shader" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-03-04T08:00:00+08:00" />
    <meta itemprop="keywords" content="Unity" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Unity Shader" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-03-04T08:00:00+08:00" />
    <meta itemprop="keywords" content="Unity" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="shaderlab">ShaderLab</h1>

<div class="language-c# highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">Shader</span> <span class="s">"..."</span><span class="p">{</span>
    <span class="n">Properties</span><span class="p">{</span>

    <span class="p">}</span>
    <span class="n">SubShader</span><span class="p">{</span>
        <span class="n">Tag</span><span class="p">{</span>

        <span class="p">}</span>
        <span class="n">Pass</span><span class="p">{</span>
            <span class="n">Tag</span><span class="p">{</span>
                
            <span class="p">}</span>
            <span class="cm">/**
             * HLSL 程序要闭包在 CGPROGRAM 和 ENDCG 内部
             */</span>
            <span class="n">CGPROGRAM</span>
            <span class="err">#</span><span class="n">pragma</span> <span class="n">vertex</span> <span class="p">...</span>
            <span class="err">#</span><span class="n">pragma</span> <span class="n">fragment</span> <span class="p">...</span>
            <span class="n">ENDCG</span>
        <span class="p">}</span>
    <span class="p">}</span>
    <span class="n">Fallback</span> <span class="s">"..."</span>
<span class="p">}</span>
</code></pre></div></div>

<h1 id="surface-shader">Surface Shader</h1>

<p><a href="https://docs.unity3d.com/Manual/SL-SurfaceShaderExamples.html">Surface Shader examples</a></p>

<p><a href="https://docs.unity3d.com/Manual/SL-VertexFragmentShaderExamples.html">Vertex and fragment shader examples</a></p>

<div class="language-c# highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="cm">/**
 * 输入结构
 *
 * shader 函数由用户自己定义一个 Input 结构  
 * Input 结构的内容可以包含如下选项,所有的命名都必须按照规定
 * 例如 : uv_MyTexture...
 */</span>
<span class="k">struct</span> <span class="nc">Input</span>
<span class="p">{</span>
    <span class="n">float2</span> <span class="n">uv_MyTexture</span><span class="p">;</span>
    <span class="n">float2</span> <span class="n">uv2_MyTexture2</span><span class="p">;</span>
    <span class="n">float3</span> <span class="n">viewDir</span><span class="p">;</span>
    <span class="n">float4</span> <span class="n">color</span> <span class="p">:</span> <span class="n">COLOR</span><span class="p">;</span>
    <span class="n">float4</span> <span class="n">screenPos</span><span class="p">;</span>
    <span class="n">float3</span> <span class="n">worldPos</span><span class="p">;</span>
    <span class="n">float3</span> <span class="n">worldRefl</span><span class="p">;</span>
    <span class="n">float3</span> <span class="n">worldNormal</span><span class="p">;</span>
    <span class="n">float3</span> <span class="n">worldRefl</span><span class="p">;</span>
    <span class="n">float3</span> <span class="n">worldNormal</span><span class="p">;</span>
<span class="p">}</span>


<span class="cm">/**
 * 输出结构
 */</span>
<span class="k">struct</span> <span class="nc">SurfaceOutput</span>
<span class="p">{</span>
    <span class="n">fixed3</span> <span class="n">Albedo</span><span class="p">;</span>  <span class="c1">// diffuse color</span>
    <span class="n">fixed3</span> <span class="n">Normal</span><span class="p">;</span>  <span class="c1">// tangent space normal, if written</span>
    <span class="n">fixed3</span> <span class="n">Emission</span><span class="p">;</span>
    <span class="n">half</span> <span class="n">Specular</span><span class="p">;</span>  <span class="c1">// specular power in 0..1 range</span>
    <span class="k">fixed</span> <span class="n">Gloss</span><span class="p">;</span>    <span class="c1">// specular intensity</span>
    <span class="k">fixed</span> <span class="n">Alpha</span><span class="p">;</span>    <span class="c1">// alpha for transparencies</span>
<span class="p">};</span>
<span class="k">struct</span> <span class="nc">SurfaceOutputStandard</span>
<span class="p">{</span>
    <span class="n">fixed3</span> <span class="n">Albedo</span><span class="p">;</span>      <span class="c1">// base (diffuse or specular) color</span>
    <span class="n">fixed3</span> <span class="n">Normal</span><span class="p">;</span>      <span class="c1">// tangent space normal, if written</span>
    <span class="n">half3</span> <span class="n">Emission</span><span class="p">;</span>
    <span class="n">half</span> <span class="n">Metallic</span><span class="p">;</span>      <span class="c1">// 0=non-metal, 1=metal</span>
    <span class="n">half</span> <span class="n">Smoothness</span><span class="p">;</span>    <span class="c1">// 0=rough, 1=smooth</span>
    <span class="n">half</span> <span class="n">Occlusion</span><span class="p">;</span>     <span class="c1">// occlusion (default 1)</span>
    <span class="k">fixed</span> <span class="n">Alpha</span><span class="p">;</span>        <span class="c1">// alpha for transparencies</span>
<span class="p">};</span>
<span class="k">struct</span> <span class="nc">SurfaceOutputStandardSpecular</span>
<span class="p">{</span>
    <span class="n">fixed3</span> <span class="n">Albedo</span><span class="p">;</span>      <span class="c1">// diffuse color</span>
    <span class="n">fixed3</span> <span class="n">Specular</span><span class="p">;</span>    <span class="c1">// specular color</span>
    <span class="n">fixed3</span> <span class="n">Normal</span><span class="p">;</span>      <span class="c1">// tangent space normal, if written</span>
    <span class="n">half3</span> <span class="n">Emission</span><span class="p">;</span>
    <span class="n">half</span> <span class="n">Smoothness</span><span class="p">;</span>    <span class="c1">// 0=rough, 1=smooth</span>
    <span class="n">half</span> <span class="n">Occlusion</span><span class="p">;</span>     <span class="c1">// occlusion (default 1)</span>
    <span class="k">fixed</span> <span class="n">Alpha</span><span class="p">;</span>        <span class="c1">// alpha for transparencies</span>
<span class="p">};</span>

<span class="cm">/**
 * 编译指令
 *
 * https://docs.unity3d.com/Manual/SL-SurfaceShaders.html
 * 
 * @param surfaceFunction : 表面着色器函数名,函数必须为签名 : void surf (Input IN, inout SurfaceOutput o)
 * @param lightModel : 光照模型
 *                   - Standard : 使用 Standard 则使用 SurfaceOutputStandard 
 *                   - StandardSpecular : 使用 SurfaceOutputStandardSpecular 
 *                   - Lambert, BlinnPhong : 不基于物理的光照, 其中 Lambert 使用漫反射, BlinnPhong 使用镜面反射
 *                   - 自定义的光照模型, 例如 MyLightModel, 这个时候会启用名为 LightingMyLightModel 的函数(或者名字类似的函数,取决于渲染管线)
 * @param optionalparams : 
 *                       - https://docs.unity3d.com/Manual/SL-SurfaceShaders.html
 */</span>
<span class="cp">#pragma surface surfaceFunction lightModel [optionalparams]
</span>
<span class="cm">/**
 * https://docs.unity3d.com/Manual/SL-ShaderPrograms.html
 *
 * 声明 vertex / fragment shader
 * vertex shader (顶点着色器)
 * fragment shader (像素着色器)
 */</span>

<span class="cp">#pragma vertex vert
#pragma fragment frag
</span>
<span class="cm">/**
 * https://docs.microsoft.com/en-us/windows/win32/direct3dhlsl/dx-graphics-hlsl-semantics
 * 
 * vertex shader / fragment shader 的输入输出结构体必须遵守一定的语义
 * https://docs.microsoft.com/en-us/windows/win32/direct3dhlsl/dx-graphics-hlsl-semantics
 */</span>

<span class="k">struct</span> <span class="nc">appdata</span>
<span class="p">{</span>
    <span class="cm">/**
     * object space 的坐标,即本地坐标(非世界坐标,也非齐次裁剪空间),
     * 如果需要在 Unity 的 shader 内转换到齐次裁剪空间(照相机的近平面远平面之间的空间),
     * 需要使用函数 float4 UnityObjectToClipPos(float4)
     * https://docs.unity3d.com/Manual/SL-BuiltinFunctions.html
     */</span>
    <span class="n">float4</span> <span class="n">vertex</span> <span class="p">:</span> <span class="n">POSITION</span>
<span class="p">}</span>
</code></pre></div></div>

<h2 id="custom-lighting-models-in-surface-shaders">Custom lighting models in Surface Shaders</h2>

<div class="language-c# highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="cm">/**
 * surface shader + custom lighting == vertex shader + fragment shader
 */</span>
</code></pre></div></div>

<p><a href="https://docs.unity3d.com/Manual/SL-SurfaceShaderLighting.html">Custom lighting models in Surface Shaders</a></p>

<p><a href="https://docs.unity3d.com/Manual/SL-SurfaceShaderLightingExamples.html">Surface Shader lighting examples</a></p>

<div class="language-c# highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="cm">/**
 * 光照函数必须以 Lighting 开头, 例如 LightingXxx
 */</span>
<span class="n">half4</span> <span class="nf">LightingXxx</span><span class="p">(</span><span class="n">SurfaceOutput</span> <span class="n">s</span><span class="p">,</span> <span class="n">UnityGI</span> <span class="n">gi</span><span class="p">);</span>
<span class="n">half4</span> <span class="nf">LightingXxx</span><span class="p">(</span><span class="n">SurfaceOutput</span> <span class="n">s</span><span class="p">,</span> <span class="n">half3</span> <span class="n">viewDIr</span><span class="p">,</span> <span class="n">UnityGI</span> <span class="n">gi</span><span class="p">);</span>
<span class="cm">/**
 * 不仅以 Lighting 开头, 还以 _Deferred 结尾
 */</span>
<span class="n">half4</span> <span class="nf">LightingXxx_Deferred</span> <span class="p">(</span><span class="n">SurfaceOutput</span> <span class="n">s</span><span class="p">,</span> <span class="n">UnityGI</span> <span class="n">gi</span><span class="p">,</span> <span class="k">out</span> <span class="n">half4</span> <span class="n">outDiffuseOcclusion</span><span class="p">,</span> <span class="k">out</span> <span class="n">half4</span> <span class="n">outSpecSmoothness</span><span class="p">,</span> <span class="k">out</span> <span class="n">half4</span> <span class="n">outNormal</span><span class="p">);</span> 
<span class="cm">/**
 * 不仅以 Lighting 开头, 还以 _PrePass 结尾
 */</span>
<span class="n">half4</span> <span class="nf">LightingXxx_PrePass</span> <span class="p">(</span><span class="n">SurfaceOutput</span> <span class="n">s</span><span class="p">,</span> <span class="n">half4</span> <span class="n">light</span><span class="p">);</span>
<span class="cm">/**
 * 不仅以 Lighting 开头, 还以 _GI 结尾
 */</span>
<span class="n">half4</span> <span class="nf">LightingXxx_GI</span> <span class="p">(</span><span class="n">SurfaceOutput</span> <span class="n">s</span><span class="p">,</span> <span class="n">UnityGIInput</span> <span class="n">data</span><span class="p">,</span> <span class="n">inout</span> <span class="n">UnityGI</span> <span class="n">gi</span><span class="p">);</span>
</code></pre></div></div>

<h1 id="fragment-shader--pixel-shader">Fragment Shader / Pixel Shader</h1>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2021-03-04T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2021/03/02/unity-persistance.html">Unity 持久化</a></div><div class="next"><span>下篇</span><a href="/2021/04/11/jekyll.html">Jekyll</a></div></div></div>

</div>

<script>(function() {
  var SOURCES = window.TEXT_VARIABLES.sources;
  window.Lazyload.js(SOURCES.jquery, function() {
    $(function() {
      var $this ,$scroll;
      var $articleContent = $('.js-article-content');
      var hasSidebar = $('.js-page-root').hasClass('layout--page--sidebar');
      var scroll = hasSidebar ? '.js-page-main' : 'html, body';
      $scroll = $(scroll);

      $articleContent.find('.highlight').each(function() {
        $this = $(this);
        $this.attr('data-lang', $this.find('code').attr('data-lang'));
      });
      $articleContent.find('h1[id], h2[id], h3[id], h4[id], h5[id], h6[id]').each(function() {
        $this = $(this);
        $this.append($('<a class="anchor d-print-none" aria-hidden="true"></a>').html('<i class="fas fa-anchor"></i>'));
      });
      $articleContent.on('click', '.anchor', function() {
        $scroll.scrollToAnchor('#' + $(this).parent().attr('id'), 400);
      });
    });
  });
})();
</script>
</div></article>