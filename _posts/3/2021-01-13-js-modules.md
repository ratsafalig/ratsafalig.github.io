---
title: JS CJS AMD UMD ESM JavaScript Modules
date: 2021-01-13 00:00:00 Z
tags:
- JS
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="JS CJS AMD UMD ESM JavaScript Modules"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2021-01-13T08:00:00+08:00">
    <meta itemprop="keywords" content="JS"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="JS CJS AMD UMD ESM JavaScript Modules" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-01-13T08:00:00+08:00" />
    <meta itemprop="keywords" content="JS" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><p><a href="https://dev.to/iggredible/what-the-heck-are-cjs-amd-umd-and-esm-ikm">what-the-heck-are-cjs-amd-umd-and-esm-ikm</a></p>

<h1 id="cjs">CJS</h1>

<p>使用在<code class="language-plaintext highlighter-rouge">node</code>环境下:</p>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">//importing </span>
<span class="kd">const</span> <span class="nx">doSomething</span> <span class="o">=</span> <span class="nx">require</span><span class="p">(</span><span class="dl">'</span><span class="s1">./doSomething.js</span><span class="dl">'</span><span class="p">);</span> 

<span class="c1">//exporting</span>
<span class="nx">module</span><span class="p">.</span><span class="nx">exports</span> <span class="o">=</span> <span class="kd">function</span> <span class="nx">doSomething</span><span class="p">(</span><span class="nx">n</span><span class="p">)</span> <span class="p">{</span>
  <span class="c1">// do something</span>
<span class="p">}</span>
</code></pre></div></div>

<h1 id="amd">AMD</h1>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nx">define</span><span class="p">([</span><span class="dl">'</span><span class="s1">dep1</span><span class="dl">'</span><span class="p">,</span> <span class="dl">'</span><span class="s1">dep2</span><span class="dl">'</span><span class="p">],</span> <span class="kd">function</span> <span class="p">(</span><span class="nx">dep1</span><span class="p">,</span> <span class="nx">dep2</span><span class="p">)</span> <span class="p">{</span>
    <span class="c1">//Define the module value by returning a value.</span>
    <span class="k">return</span> <span class="kd">function</span> <span class="p">()</span> <span class="p">{};</span>
<span class="p">});</span>
</code></pre></div></div>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">// "simplified CommonJS wrapping" https://requirejs.org/docs/whyamd.html</span>
<span class="nx">define</span><span class="p">(</span><span class="kd">function</span> <span class="p">(</span><span class="nx">require</span><span class="p">)</span> <span class="p">{</span>
    <span class="kd">var</span> <span class="nx">dep1</span> <span class="o">=</span> <span class="nx">require</span><span class="p">(</span><span class="dl">'</span><span class="s1">dep1</span><span class="dl">'</span><span class="p">),</span>
        <span class="nx">dep2</span> <span class="o">=</span> <span class="nx">require</span><span class="p">(</span><span class="dl">'</span><span class="s1">dep2</span><span class="dl">'</span><span class="p">);</span>
    <span class="k">return</span> <span class="kd">function</span> <span class="p">()</span> <span class="p">{};</span>
<span class="p">});</span>
</code></pre></div></div>

<h1 id="umd">UMD</h1>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="p">(</span><span class="kd">function</span> <span class="p">(</span><span class="nx">root</span><span class="p">,</span> <span class="nx">factory</span><span class="p">)</span> <span class="p">{</span>
    <span class="k">if</span> <span class="p">(</span><span class="k">typeof</span> <span class="nx">define</span> <span class="o">===</span> <span class="dl">"</span><span class="s2">function</span><span class="dl">"</span> <span class="o">&amp;&amp;</span> <span class="nx">define</span><span class="p">.</span><span class="nx">amd</span><span class="p">)</span> <span class="p">{</span>
        <span class="nx">define</span><span class="p">([</span><span class="dl">"</span><span class="s2">jquery</span><span class="dl">"</span><span class="p">,</span> <span class="dl">"</span><span class="s2">underscore</span><span class="dl">"</span><span class="p">],</span> <span class="nx">factory</span><span class="p">);</span>
    <span class="p">}</span> <span class="k">else</span> <span class="k">if</span> <span class="p">(</span><span class="k">typeof</span> <span class="nx">exports</span> <span class="o">===</span> <span class="dl">"</span><span class="s2">object</span><span class="dl">"</span><span class="p">)</span> <span class="p">{</span>
        <span class="nx">module</span><span class="p">.</span><span class="nx">exports</span> <span class="o">=</span> <span class="nx">factory</span><span class="p">(</span><span class="nx">require</span><span class="p">(</span><span class="dl">"</span><span class="s2">jquery</span><span class="dl">"</span><span class="p">),</span> <span class="nx">require</span><span class="p">(</span><span class="dl">"</span><span class="s2">underscore</span><span class="dl">"</span><span class="p">));</span>
    <span class="p">}</span> <span class="k">else</span> <span class="p">{</span>
        <span class="nx">root</span><span class="p">.</span><span class="nx">Requester</span> <span class="o">=</span> <span class="nx">factory</span><span class="p">(</span><span class="nx">root</span><span class="p">.</span><span class="nx">$</span><span class="p">,</span> <span class="nx">root</span><span class="p">.</span><span class="nx">_</span><span class="p">);</span>
    <span class="p">}</span>
<span class="p">}(</span><span class="k">this</span><span class="p">,</span> <span class="kd">function</span> <span class="p">(</span><span class="nx">$</span><span class="p">,</span> <span class="nx">_</span><span class="p">)</span> <span class="p">{</span>
    <span class="c1">// this is where I defined my module implementation</span>

    <span class="kd">var</span> <span class="nx">Requester</span> <span class="o">=</span> <span class="p">{</span> <span class="c1">// ... };</span>

    <span class="k">return</span> <span class="nx">Requester</span><span class="p">;</span>
<span class="p">}));</span>
</code></pre></div></div>

<h1 id="esm">ESM</h1>

<p>常用在TS里:</p>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">import</span> <span class="nx">React</span> <span class="k">from</span> <span class="dl">'</span><span class="s1">react</span><span class="dl">'</span><span class="p">;</span>
<span class="k">import</span> <span class="p">{</span><span class="nx">foo</span><span class="p">,</span> <span class="nx">bar</span><span class="p">}</span> <span class="k">from</span> <span class="dl">'</span><span class="s1">./myLib</span><span class="dl">'</span><span class="p">;</span>

<span class="p">...</span>

<span class="k">export</span> <span class="k">default</span> <span class="kd">function</span><span class="p">()</span> <span class="p">{</span>
  <span class="c1">// your Function</span>
<span class="p">};</span>
<span class="k">export</span> <span class="kd">const</span> <span class="nx">function1</span><span class="p">()</span> <span class="p">{...};</span>
<span class="k">export</span> <span class="kd">const</span> <span class="nx">function2</span><span class="p">()</span> <span class="p">{...};</span>
</code></pre></div></div>

<div class="language-html highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;script </span><span class="na">type=</span><span class="s">"module"</span><span class="nt">&gt;</span>
  <span class="k">import</span> <span class="p">{</span><span class="nx">func1</span><span class="p">}</span> <span class="k">from</span> <span class="dl">'</span><span class="s1">my-lib</span><span class="dl">'</span><span class="p">;</span>

  <span class="nx">func1</span><span class="p">();</span>
<span class="nt">&lt;/script&gt;</span>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2021-01-13T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2021/01/13/css.html">CSS</a></div><div class="next"><span>下篇</span><a href="/2021/01/13/js-service-worker.html">JS Service Worker</a></div></div></div>

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