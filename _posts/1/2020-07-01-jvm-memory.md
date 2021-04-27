---
title: JVM 内存
date: 2020-07-01 00:00:00 Z
tags:
- Java
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="JVM 内存"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00">
    <meta itemprop="keywords" content="Java"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="JVM 内存" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="JVM 内存" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_1">JVM Memory Model</h1>

<pre><code class="language-mermaid">graph LR;
    id1(方法区)
    id2(堆)
    id3(虚拟机栈)
    id4(本地方法栈)
    id5(young)
    id6(survival)
    id7(old)
    id8(运行时常量池)
    id9(直接内存)
    id10(栈)
    id1--&gt;id8
    id2--&gt;id5
    id2--&gt;id6
    id2--&gt;id7
    id10--&gt;id3
    id10--&gt;id4
</code></pre>

<h1 id="_2">对象</h1>

<pre><code class="language-mermaid">graph LR;
    id1(对象头)
    id2(Mark-Word)
    id3(类型指针)
    id4(hash)
    id5(gc年龄)
    id6(偏向信息)
    id7(实例信息)

    id1--&gt;id2
    id2--&gt;id4
    id2--&gt;id5
    id2--&gt;id6
</code></pre>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-07-01T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/07/01/jvm-gc.html">JVM GC</a></div><div class="next"><span>下篇</span><a href="/2020/07/03/java-juc.html">Java JUC</a></div></div></div>

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