---
title: C++ __declspec(dllexport) __declspec(dllimport)
date: 2021-02-03 00:00:00 Z
tags:
- Cpp
- Windows
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="C++ __declspec(dllexport) __declspec(dllimport)"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2021-02-03T08:00:00+08:00">
    <meta itemprop="keywords" content="Cpp,Windows"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="C++ __declspec(dllexport) __declspec(dllimport)" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-02-03T08:00:00+08:00" />
    <meta itemprop="keywords" content="Cpp,Windows" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="C++ __declspec(dllexport) __declspec(dllimport)" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-02-03T08:00:00+08:00" />
    <meta itemprop="keywords" content="Cpp,Windows" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><p><a href="https://stackoverflow.com/questions/2288293/windows-c-extern-declspecdllimport/2288355">Stack Overflow - Windows &amp; C++: extern &amp; __declspec(dllimport)</a></p>

<p><a href="https://docs.microsoft.com/en-gb/cpp/cpp/dllexport-dllimport?view=msvc-160">MSDN - dllexport, dllimport</a></p>

<p><a href="https://www.it1352.com/1554286.html">在Visual Studio中dllimport的用例(Use case of dllimport in VisualStudio)</a></p>

<p>首先需要说明 __declspec 是一个 microsoft-specific 的东西.</p>

<h1 id="实例">实例</h1>

<h2 id="jnidll">JNI.dll</h2>

<ul>
  <li>创建一个 JNI.dll 和 JNI.lib</li>
</ul>

<div class="language-cpp highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">// dllmain.cpp</span>
<span class="cp">#include "stdafx.h"
#include "iostream"
</span>
<span class="n">BOOL</span> <span class="n">APIENTRY</span> <span class="nf">DllMain</span><span class="p">(</span> <span class="n">HMODULE</span> <span class="n">hModule</span><span class="p">,</span>
                       <span class="n">DWORD</span>  <span class="n">ul_reason_for_call</span><span class="p">,</span>
                       <span class="n">LPVOID</span> <span class="n">lpReserved</span>
                     <span class="p">)</span>
<span class="p">{</span>
	<span class="n">std</span><span class="o">::</span><span class="n">cout</span> <span class="o">&lt;&lt;</span> <span class="s">"hello DllMain"</span> <span class="o">&lt;&lt;</span> <span class="n">std</span><span class="o">::</span><span class="n">endl</span><span class="p">;</span>
    <span class="k">switch</span> <span class="p">(</span><span class="n">ul_reason_for_call</span><span class="p">)</span>
    <span class="p">{</span>
    <span class="k">case</span> <span class="n">DLL_PROCESS_ATTACH</span><span class="p">:</span>
    <span class="k">case</span> <span class="n">DLL_THREAD_ATTACH</span><span class="p">:</span>
    <span class="k">case</span> <span class="n">DLL_THREAD_DETACH</span><span class="p">:</span>
    <span class="k">case</span> <span class="n">DLL_PROCESS_DETACH</span><span class="p">:</span>
        <span class="k">break</span><span class="p">;</span>
    <span class="p">}</span>
    <span class="k">return</span> <span class="n">TRUE</span><span class="p">;</span>
<span class="p">}</span>
<span class="c1">// A.cpp</span>
<span class="cp">#include "stdafx.h"
#include "A.h"
#include "iostream"
</span>
<span class="kt">void</span> <span class="nf">A</span><span class="p">()</span> <span class="p">{</span>
	<span class="n">std</span><span class="o">::</span><span class="n">cout</span> <span class="o">&lt;&lt;</span> <span class="s">"hello A"</span> <span class="o">&lt;&lt;</span> <span class="n">std</span><span class="o">::</span><span class="n">endl</span><span class="p">;</span>
<span class="p">}</span>
<span class="c1">// A.h</span>
<span class="cp">#pragma once
</span><span class="kr">__declspec</span><span class="p">(</span><span class="n">dllexport</span><span class="p">)</span>
<span class="kt">void</span> <span class="nf">A</span><span class="p">();</span>
</code></pre></div></div>

<h2 id="consoleapplication">ConsoleApplication</h2>

<ul>
  <li>创建一个 ConsoleApplication1 :</li>
</ul>

<div class="language-cpp highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">// ConsoleApplication1.cpp</span>
<span class="cp">#include "stdafx.h"
#include "iostream"
</span><span class="c1">// 如果使用 LoadLibrary 进行导入,必须使用 windows.h ,同时注意运行时链接不能直接调用函数,需要使用 GetProcAddress</span>
<span class="c1">// #include "windows.h" </span>
<span class="cp">#include "A.h"
</span>
<span class="c1">// 取决于要怎么样导入,如果使用 visual studio 提供的图形界面则不需要以下操作</span>
<span class="c1">// #pragma comment(lib, "JNI.lib")</span>

<span class="kt">int</span> <span class="nf">main</span><span class="p">()</span> <span class="p">{</span>
	<span class="n">A</span><span class="p">();</span>
<span class="p">}</span>
<span class="c1">// a.h</span>
<span class="cp">#pragma once
</span>
<span class="c1">// 实际上,使不使用 dllimport 都是可以运行的,从网络了解到, dllimport 更像是一种优化</span>
<span class="c1">// 因为如果不加 dllimport ,程序会首先尝试从自己的地址空间查找函数,如果没找到则从 dll 里找</span>
<span class="c1">// 但是必须说明个人还未验证这一说法</span>
<span class="c1">// __declspec(dllimport) </span>
<span class="kt">void</span> <span class="nf">A</span><span class="p">();</span>
</code></pre></div></div>

<h2 id="配置">配置</h2>

<ul>
  <li>配置,以下三种选一即可:</li>
</ul>

<p><code class="language-plaintext info highlighter-rouge">1</code> 使用 visual studio 的 gui 配置 linker
<img src="/assets/3/cpp-dllexport-dllimport/QQ截图20210203234155.png" alt="" /><br />
设置 lib 的目录<br />
<img src="/assets/3/cpp-dllexport-dllimport/QQ截图20210203234303.png" alt="" /></p>

<p><img src="/assets/3/cpp-dllexport-dllimport/QQ截图20210203234346.png" alt="" /></p>

<p>设置配置的作用域</p>

<p><img src="/assets/3/cpp-dllexport-dllimport/QQ截图20210203234410.png" alt="" /></p>

<p><code class="language-plaintext info highlighter-rouge">2</code> 使用 visual studio 直接加入 lib 文件</p>

<p><img src="/assets/3/cpp-dllexport-dllimport/QQ截图20210203234522.png" alt="" /></p>

<p>添加后的效果如下</p>

<p><img src="/assets/3/cpp-dllexport-dllimport/QQ截图20210203234546.png" alt="" /></p>

<p><code class="language-plaintext info highlighter-rouge">3</code> 使用预处理器指令 : <code class="language-plaintext highlighter-rouge">#pragma comment(lib, "JNI.lib)"</code></p>

</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2021-02-03T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2021/01/31/zookeeper.html">ZooKeeper</a></div><div class="next"><span>下篇</span><a href="/2021/02/13/c.html">C#</a></div></div></div>

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