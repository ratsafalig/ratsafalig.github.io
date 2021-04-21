---
title: V2 Dubbo 服务引入
date: 2020-10-08 00:00:00 Z
tags:
- Java
- Dubbo
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="V2 Dubbo 服务引入"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-10-08T08:00:00+08:00">
    <meta itemprop="keywords" content="Java,Dubbo"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="V2 Dubbo 服务引入" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-08T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Dubbo" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="V2 Dubbo 服务引入" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-08T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Dubbo" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="V2 Dubbo 服务引入" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-08T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Dubbo" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="服务引入">服务引入</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">interface</span> <span class="nc">A</span><span class="o">{}</span>

<span class="kd">public</span> <span class="kd">class</span> <span class="nc">DemoApplication</span> <span class="o">{</span>
	<span class="kd">public</span> <span class="kd">static</span> <span class="kt">void</span> <span class="nf">main</span><span class="o">(</span><span class="nc">String</span><span class="o">[]</span> <span class="n">args</span><span class="o">)</span><span class="kd">throws</span> <span class="nc">Exception</span><span class="o">{</span>
        <span class="nc">ApplicationConfig</span> <span class="n">applicationConfig</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ApplicationConfig</span><span class="o">();</span>
        <span class="n">applicationConfig</span><span class="o">.</span><span class="na">setName</span><span class="o">(</span><span class="s">"MyApp"</span><span class="o">);</span>

        <span class="nc">RegistryConfig</span>  <span class="n">registryConfig</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">RegistryConfig</span><span class="o">();</span>
        <span class="n">registryConfig</span><span class="o">.</span><span class="na">setAddress</span><span class="o">(</span><span class="s">"10.20.130.230:9090"</span><span class="o">);</span>

        <span class="nc">ReferenceConfig</span><span class="o">&lt;</span><span class="no">A</span><span class="o">&gt;</span> <span class="n">referenceConfig</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ReferenceConfig</span><span class="o">&lt;&gt;();</span>
        <span class="n">referenceConfig</span><span class="o">.</span><span class="na">setApplication</span><span class="o">(</span><span class="n">applicationConfig</span><span class="o">);</span>
        <span class="n">referenceConfig</span><span class="o">.</span><span class="na">setRegistry</span><span class="o">(</span><span class="n">registryConfig</span><span class="o">);</span>
        <span class="n">referenceConfig</span><span class="o">.</span><span class="na">setInterface</span><span class="o">(</span><span class="no">A</span><span class="o">.</span><span class="na">class</span><span class="o">);</span>

        <span class="n">referenceConfig</span><span class="o">.</span><span class="na">get</span><span class="o">();</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-10-08T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/10/04/misc-mermaid.html">Mermaid 语法</a></div><div class="next"><span>下篇</span><a href="/2020/10/15/misc-auto-hot-key.html">AutoHotKey</a></div></div></div>

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