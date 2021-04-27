---
title: Java Collection
date: 2020-07-01 00:00:00 Z
tags:
- Java
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Java Collection"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00">
    <meta itemprop="keywords" content="Java"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Java Collection" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Java Collection" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Java Collection" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="_1">继承图</h1>

<p><img src="/assets/1/collection/collections-framework-overview.png" alt="" /></p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>List接口继承图
</code></pre></div></div>
<p><img src="/assets/1/collection/list.jpg" alt="" /></p>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>Map接口继承图
</code></pre></div></div>
<p><img src="/assets/1/collection/map.jpg" alt="" /></p>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>Set接口继承图
</code></pre></div></div>
<p><img src="/assets/1/collection/set.jpg" alt="" /></p>

<h1 id="_2">HashMap</h1>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>HashMap可能是非并发的集合类里最难的一个,

主要过程如下:

1. HashMap的数据结构是一个数组,数组的元素是一个&lt;链表/树&gt;的&lt;头/根&gt;节点
2. 插入一个元素的时候,根据key的hash-code计算出hash值,然后存放在数组的指定位置
3. 如果hash-code位置已经有值了,就调用object.equal判断是否是同一个,如果是同一个就替换,否则用链表的方式接在后面
4. 如果链表过长,则转换为红黑树,反之红黑树过小也会转回为链表
5. 如果当前存的数据太多了,就会调用resize()扩容

主要有以下几个关键参数

1. threshold
    threshold&lt;loadFactor*size的时候,调用resize扩容
2. loadFactor
    加载因子,用来计算扩容的时机
3. initialCapacity
    2的initialCapacity次方为hash-map的初始大小
4. TREEIFY_THRESHOLD
    当链表到达这个长度的时候,转换成红黑树
5. UNTREEIFY_THRESHOLD
    当链表小于这个长度的时候,转换成链表
</code></pre></div></div>

<h1 id="_3">LinkedHashMap0</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">通过hashMap</span><span class="o">.</span><span class="na">entrySet</span><span class="o">()</span><span class="n">获取到的set是无序的</span><span class="o">,</span>
<span class="n">而linkedHashMap</span><span class="o">.</span><span class="na">entrySet</span><span class="o">()</span><span class="n">获取到的set拿去迭代是按照插入的顺序</span>
<span class="nc">LinkedHashMap通过维护一个双向链表来达到这个操作</span><span class="o">,</span><span class="n">每插入一个数据</span><span class="o">,</span><span class="nc">Entry</span><span class="o">&lt;</span><span class="no">K</span><span class="o">,</span><span class="no">V</span><span class="o">&gt;,</span>
<span class="n">内部就给Entry包装上一层</span><span class="o">,</span><span class="n">给包装后的Entity提供了before</span><span class="o">,</span><span class="n">after指针</span><span class="o">,</span>
<span class="n">第一次插入数据的时候赋值给内部的head</span><span class="o">,</span>
<span class="n">接下来entrySet就根据包装后的Entry的before</span><span class="o">,</span><span class="n">after的逻辑去遍历</span>
</code></pre></div></div>
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
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/07/01/cpp-virtual-table.html">C++ 虚表</a></div><div class="next"><span>下篇</span><a href="/2020/07/01/jvm-classloader.html">ClassLoader</a></div></div></div>

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