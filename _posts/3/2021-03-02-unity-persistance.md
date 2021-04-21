---
title: Unity 持久化
date: 2021-03-02 00:00:00 Z
tags:
- Unity
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Unity 持久化"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2021-03-02T08:00:00+08:00">
    <meta itemprop="keywords" content="Unity"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Unity 持久化" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-03-02T08:00:00+08:00" />
    <meta itemprop="keywords" content="Unity" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><p><a href="https://blog.csdn.net/qq_35711014/article/details/89891139">Unity实现动态资源加载的4种方式</a></p>

<h1 id="assetbundle">AssetBundle</h1>

<p>AssetBundle 是最推荐的方式</p>

<div class="language-c# highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">using</span> <span class="nn">System.Collections</span><span class="p">;</span>
<span class="k">using</span> <span class="nn">UnityEngine</span><span class="p">;</span>
<span class="k">using</span> <span class="nn">UnityEngine.Networking</span><span class="p">;</span>

<span class="k">public</span> <span class="k">class</span> <span class="nc">SampleBehaviour</span> <span class="p">:</span> <span class="n">MonoBehaviour</span>
<span class="p">{</span>
    <span class="n">IEnumerator</span> <span class="nf">Start</span><span class="p">()</span>
    <span class="p">{</span>
        <span class="kt">var</span> <span class="n">uwr</span> <span class="p">=</span> <span class="n">UnityWebRequestAssetBundle</span><span class="p">.</span><span class="nf">GetAssetBundle</span><span class="p">(</span><span class="s">"http://myserver/myBundle.unity3d"</span><span class="p">);</span>
        <span class="k">yield</span> <span class="k">return</span> <span class="n">uwr</span><span class="p">.</span><span class="nf">SendWebRequest</span><span class="p">();</span>

        <span class="c1">// Get an asset from the bundle and instantiate it.</span>
        <span class="n">AssetBundle</span> <span class="n">bundle</span> <span class="p">=</span> <span class="n">DownloadHandlerAssetBundle</span><span class="p">.</span><span class="nf">GetContent</span><span class="p">(</span><span class="n">uwr</span><span class="p">);</span>
        <span class="kt">var</span> <span class="n">loadAsset</span> <span class="p">=</span> <span class="n">bundle</span><span class="p">.</span><span class="n">LoadAssetAsync</span><span class="p">&lt;</span><span class="n">GameObject</span><span class="p">&gt;(</span><span class="s">"Assets/Players/MainPlayer.prefab"</span><span class="p">);</span>
        <span class="k">yield</span> <span class="k">return</span> <span class="n">loadAsset</span><span class="p">;</span>

        <span class="nf">Instantiate</span><span class="p">(</span><span class="n">loadAsset</span><span class="p">.</span><span class="n">asset</span><span class="p">);</span>
    <span class="p">}</span>
<span class="p">}</span>
<span class="cm">/**********************************************************************************************/</span>
<span class="k">public</span> <span class="k">static</span> <span class="n">Networking</span><span class="p">.</span><span class="n">UnityWebRequest</span> <span class="nf">GetAssetBundle</span><span class="p">(</span><span class="kt">string</span> <span class="n">uri</span><span class="p">);</span>
<span class="cm">/**********************************************************************************************/</span>
<span class="k">public</span> <span class="k">static</span> <span class="kt">bool</span> <span class="nf">BuildAssetBundle</span><span class="p">(</span><span class="n">Object</span> <span class="n">mainAsset</span><span class="p">,</span> <span class="n">Object</span><span class="p">[]</span> <span class="n">assets</span><span class="p">,</span> <span class="kt">string</span> <span class="n">pathName</span><span class="p">,</span> <span class="n">BuildAssetBundleOptions</span> <span class="n">assetBundleOptions</span><span class="p">,</span> <span class="n">BuildTarget</span> <span class="n">targetPlatform</span><span class="p">);</span>
</code></pre></div></div>

<h1 id="assetdatabase">AssetDatabase</h1>

<div class="language-c# highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="cm">/**
 * Creates a new asset at path.
 * You must ensure that the path uses a supported extension ('.mat' for materials, '.cubemap' for cubemaps, '.GUISkin' for skins, '.anim' for animations and '.asset' for arbitrary other assets.)
 * You can add more assets to the file using AssetDatabase.AddObjectToAsset after the asset has been created. If an asset already exists at path it will be deleted prior to creating a new asset. All paths are relative to the project folder, * 
 * for example: "Assets/MyStuff/hello.mat".
 * Be aware that if adding multiple objects to an asset, the order in which the objects are added does not really matter. In other words, asset will not be special within the asset and not be any form of "root" to objects added later. The  
 * object displayed as the asset's main object in the project view is the one that is considered most important (decided based on type) within the collection of objects.
 *
 * 可以看到 AssetDatabase 可以用来创建 .mat .cubemap .GUISkin .anim .asset 文件
 */</span>
<span class="k">public</span> <span class="k">static</span> <span class="k">void</span> <span class="n">AssetDatabase</span><span class="p">.</span><span class="nf">CreateAsset</span><span class="p">(</span><span class="n">Object</span> <span class="n">asset</span><span class="p">,</span> <span class="kt">string</span> <span class="n">path</span><span class="p">);</span>
<span class="cm">/**********************************************************************************************/</span>
<span class="k">using</span> <span class="nn">UnityEngine</span><span class="p">;</span>
<span class="k">using</span> <span class="nn">UnityEditor</span><span class="p">;</span>

<span class="k">public</span> <span class="k">class</span> <span class="nc">CreateMaterialExample</span> <span class="p">:</span> <span class="n">MonoBehaviour</span>
<span class="p">{</span>
    <span class="p">[</span><span class="nf">MenuItem</span><span class="p">(</span><span class="s">"GameObject/Create Material"</span><span class="p">)]</span>
    <span class="k">static</span> <span class="k">void</span> <span class="nf">CreateMaterial</span><span class="p">()</span>
    <span class="p">{</span>
        <span class="c1">// Create a simple material asset</span>

        <span class="n">Material</span> <span class="n">material</span> <span class="p">=</span> <span class="k">new</span> <span class="nf">Material</span><span class="p">(</span><span class="n">Shader</span><span class="p">.</span><span class="nf">Find</span><span class="p">(</span><span class="s">"Specular"</span><span class="p">));</span>
        <span class="n">AssetDatabase</span><span class="p">.</span><span class="nf">CreateAsset</span><span class="p">(</span><span class="n">material</span><span class="p">,</span> <span class="s">"Assets/MyMaterial.mat"</span><span class="p">);</span>

        <span class="c1">// Print the path of the created asset</span>
        <span class="n">Debug</span><span class="p">.</span><span class="nf">Log</span><span class="p">(</span><span class="n">AssetDatabase</span><span class="p">.</span><span class="nf">GetAssetPath</span><span class="p">(</span><span class="n">material</span><span class="p">));</span>
    <span class="p">}</span>
<span class="p">}</span>
</code></pre></div></div>

<h1 id="resources">Resources</h1>

<div class="language-c# highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="cm">/**********************************************************************************************/</span>
<span class="cm">/**
 * Resources 用来加载 Assets / * / Resources 文件夹里的数据
 * 所有名为 Resources 里的数据都可以通过 Resources.Load(...) 加载
 */</span>
<span class="k">using</span> <span class="nn">UnityEngine</span><span class="p">;</span>
<span class="k">using</span> <span class="nn">System.Collections</span><span class="p">;</span>

<span class="k">public</span> <span class="k">class</span> <span class="nc">ExampleClass</span> <span class="p">:</span> <span class="n">MonoBehaviour</span>
<span class="p">{</span>
    <span class="k">void</span> <span class="nf">Start</span><span class="p">()</span>
    <span class="p">{</span>
        <span class="n">GameObject</span> <span class="n">go</span> <span class="p">=</span> <span class="n">GameObject</span><span class="p">.</span><span class="nf">CreatePrimitive</span><span class="p">(</span><span class="n">PrimitiveType</span><span class="p">.</span><span class="n">Plane</span><span class="p">);</span>
        <span class="n">Renderer</span> <span class="n">rend</span> <span class="p">=</span> <span class="n">go</span><span class="p">.</span><span class="n">GetComponent</span><span class="p">&lt;</span><span class="n">Renderer</span><span class="p">&gt;();</span>
        <span class="n">rend</span><span class="p">.</span><span class="n">material</span><span class="p">.</span><span class="n">mainTexture</span> <span class="p">=</span> <span class="n">Resources</span><span class="p">.</span><span class="nf">Load</span><span class="p">(</span><span class="s">"glass"</span><span class="p">)</span> <span class="k">as</span> <span class="n">Texture</span><span class="p">;</span>
    <span class="p">}</span>
<span class="p">}</span>
</code></pre></div></div>

<h1 id="www">WWW</h1>

<p>‘www已经被弃用’</p>

<div class="language-c# highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">// Get the latest webcam shot from outside "Friday's" in Times Square</span>
<span class="k">using</span> <span class="nn">UnityEngine</span><span class="p">;</span>
<span class="k">using</span> <span class="nn">System.Collections</span><span class="p">;</span>

<span class="k">public</span> <span class="k">class</span> <span class="nc">ExampleClass</span> <span class="p">:</span> <span class="n">MonoBehaviour</span>
<span class="p">{</span>
    <span class="k">public</span> <span class="kt">string</span> <span class="n">url</span> <span class="p">=</span> <span class="s">"http://images.earthcam.com/ec_metros/ourcams/fridays.jpg"</span><span class="p">;</span>
    <span class="n">IEnumerator</span> <span class="nf">Start</span><span class="p">()</span>
    <span class="p">{</span>
        <span class="k">using</span> <span class="p">(</span><span class="n">WWW</span> <span class="n">www</span> <span class="p">=</span> <span class="k">new</span> <span class="nf">WWW</span><span class="p">(</span><span class="n">url</span><span class="p">))</span>
        <span class="p">{</span>
            <span class="k">yield</span> <span class="k">return</span> <span class="n">www</span><span class="p">;</span>
            <span class="n">Renderer</span> <span class="n">renderer</span> <span class="p">=</span> <span class="n">GetComponent</span><span class="p">&lt;</span><span class="n">Renderer</span><span class="p">&gt;();</span>
            <span class="n">renderer</span><span class="p">.</span><span class="n">material</span><span class="p">.</span><span class="n">mainTexture</span> <span class="p">=</span> <span class="n">www</span><span class="p">.</span><span class="n">texture</span><span class="p">;</span>
        <span class="p">}</span>
    <span class="p">}</span>
<span class="p">}</span>
</code></pre></div></div>

<h1 id="unitywebrequest">UnityWebRequest</h1>

<p>UnityWebRequest 集成了对 AssetBundle 的加载功能</p>

<div class="language-c# highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">using</span> <span class="nn">UnityEngine</span><span class="p">;</span>
<span class="k">using</span> <span class="nn">UnityEngine.Networking</span><span class="p">;</span>
<span class="k">using</span> <span class="nn">System.Collections</span><span class="p">;</span>

<span class="c1">// UnityWebRequest.Get example</span>

<span class="c1">// Access a website and use UnityWebRequest.Get to download a page.</span>
<span class="c1">// Also try to download a non-existing page. Display the error.</span>

<span class="k">public</span> <span class="k">class</span> <span class="nc">Example</span> <span class="p">:</span> <span class="n">MonoBehaviour</span>
<span class="p">{</span>
    <span class="k">void</span> <span class="nf">Start</span><span class="p">()</span>
    <span class="p">{</span>
        <span class="c1">// A correct website page.</span>
        <span class="nf">StartCoroutine</span><span class="p">(</span><span class="nf">GetRequest</span><span class="p">(</span><span class="s">"https://www.example.com"</span><span class="p">));</span>

        <span class="c1">// A non-existing page.</span>
        <span class="nf">StartCoroutine</span><span class="p">(</span><span class="nf">GetRequest</span><span class="p">(</span><span class="s">"https://error.html"</span><span class="p">));</span>
    <span class="p">}</span>

    <span class="n">IEnumerator</span> <span class="nf">GetRequest</span><span class="p">(</span><span class="kt">string</span> <span class="n">uri</span><span class="p">)</span>
    <span class="p">{</span>
        <span class="k">using</span> <span class="p">(</span><span class="n">UnityWebRequest</span> <span class="n">webRequest</span> <span class="p">=</span> <span class="n">UnityWebRequest</span><span class="p">.</span><span class="nf">Get</span><span class="p">(</span><span class="n">uri</span><span class="p">))</span>
        <span class="p">{</span>
            <span class="c1">// Request and wait for the desired page.</span>
            <span class="k">yield</span> <span class="k">return</span> <span class="n">webRequest</span><span class="p">.</span><span class="nf">SendWebRequest</span><span class="p">();</span>

            <span class="kt">string</span><span class="p">[]</span> <span class="n">pages</span> <span class="p">=</span> <span class="n">uri</span><span class="p">.</span><span class="nf">Split</span><span class="p">(</span><span class="sc">'/'</span><span class="p">);</span>
            <span class="kt">int</span> <span class="n">page</span> <span class="p">=</span> <span class="n">pages</span><span class="p">.</span><span class="n">Length</span> <span class="p">-</span> <span class="m">1</span><span class="p">;</span>

            <span class="k">switch</span> <span class="p">(</span><span class="n">webRequest</span><span class="p">.</span><span class="n">result</span><span class="p">)</span>
            <span class="p">{</span>
                <span class="k">case</span> <span class="n">UnityWebRequest</span><span class="p">.</span><span class="n">Result</span><span class="p">.</span><span class="n">ConnectionError</span><span class="p">:</span>
                <span class="k">case</span> <span class="n">UnityWebRequest</span><span class="p">.</span><span class="n">Result</span><span class="p">.</span><span class="n">DataProcessingError</span><span class="p">:</span>
                    <span class="n">Debug</span><span class="p">.</span><span class="nf">LogError</span><span class="p">(</span><span class="n">pages</span><span class="p">[</span><span class="n">page</span><span class="p">]</span> <span class="p">+</span> <span class="s">": Error: "</span> <span class="p">+</span> <span class="n">webRequest</span><span class="p">.</span><span class="n">error</span><span class="p">);</span>
                    <span class="k">break</span><span class="p">;</span>
                <span class="k">case</span> <span class="n">UnityWebRequest</span><span class="p">.</span><span class="n">Result</span><span class="p">.</span><span class="n">ProtocolError</span><span class="p">:</span>
                    <span class="n">Debug</span><span class="p">.</span><span class="nf">LogError</span><span class="p">(</span><span class="n">pages</span><span class="p">[</span><span class="n">page</span><span class="p">]</span> <span class="p">+</span> <span class="s">": HTTP Error: "</span> <span class="p">+</span> <span class="n">webRequest</span><span class="p">.</span><span class="n">error</span><span class="p">);</span>
                    <span class="k">break</span><span class="p">;</span>
                <span class="k">case</span> <span class="n">UnityWebRequest</span><span class="p">.</span><span class="n">Result</span><span class="p">.</span><span class="n">Success</span><span class="p">:</span>
                    <span class="n">Debug</span><span class="p">.</span><span class="nf">Log</span><span class="p">(</span><span class="n">pages</span><span class="p">[</span><span class="n">page</span><span class="p">]</span> <span class="p">+</span> <span class="s">":\nReceived: "</span> <span class="p">+</span> <span class="n">webRequest</span><span class="p">.</span><span class="n">downloadHandler</span><span class="p">.</span><span class="n">text</span><span class="p">);</span>
                    <span class="k">break</span><span class="p">;</span>
            <span class="p">}</span>
        <span class="p">}</span>
    <span class="p">}</span>
<span class="p">}</span>
</code></pre></div></div>

<h1 id="package-manager">Package Manager</h1>

<p>Package Manager 仅仅作用于开发中,作为一个类似 NPM 之类的 Package Manager<br />
从 Package Manager 下载来的项目保留所有原有的文件夹结构,而不像 AssetBundle 那样仅仅是一个二进制格式</p>

<p>一个 Package 的目录结构有 :</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>- /Runtime/...
- /Editor/...
- Editor.meta
- Runtime.meta
- package.json
</code></pre></div></div>

<ul>
  <li>Runtime 文件夹存放所有 MonoBehavior 等等运行时使用的工具</li>
  <li>Editor 存放所有 Custom Editor 之类的工具</li>
  <li>package.json 存放包的元信息</li>
</ul>

<p><a href="https://docs.unity3d.com/Manual/upm-manifestPkg.html">package.json</a> :</p>

<div class="language-json highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="p">{</span><span class="w">
    </span><span class="nl">"name"</span><span class="w"> </span><span class="p">:</span><span class="w"> </span><span class="s2">"..."</span><span class="p">,</span><span class="w">
    </span><span class="nl">"version"</span><span class="w"> </span><span class="p">:</span><span class="w"> </span><span class="s2">"..."</span><span class="w">
</span><span class="p">}</span><span class="w">
</span></code></pre></div></div>

<h1 id="scriptableobject">ScriptableObject</h1>

</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2021-03-02T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2021/02/26/vscode-edge-debugger.html">VS Code Edge Debugger</a></div><div class="next"><span>下篇</span><a href="/2021/03/04/unity-shader.html">Unity Shader</a></div></div></div>

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