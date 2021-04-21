---
title: 进程通信 线程通信
date: 2020-08-20 00:00:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="进程通信 线程通信"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-08-20T08:00:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="进程通信 线程通信" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="进程通信 线程通信" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_0">参考地址</h1>

<p><a href="https://www.cnblogs.com/zgq0/p/8780893.html">参考地址—csdn</a></p>

<h1 id="_1">进程通信</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="mi">1</span><span class="o">.</span> <span class="nl">无名管道:</span>
    <span class="n">半双工</span><span class="o">,</span><span class="n">相关函数int</span> <span class="n">pipe</span><span class="o">(</span><span class="kt">int</span> <span class="n">fd</span><span class="o">[</span><span class="mi">2</span><span class="o">]),</span><span class="n">其中fd</span><span class="o">[</span><span class="mi">0</span><span class="o">]</span><span class="n">拿来读</span><span class="o">,</span><span class="n">fd</span><span class="o">[</span><span class="mi">1</span><span class="o">]</span><span class="n">拿来写</span>
<span class="mi">2</span><span class="o">.</span> <span class="nl">命名管道:</span>
    <span class="n">又叫fifo</span><span class="o">,</span><span class="n">相关函数mkfifo</span><span class="o">(</span><span class="kd">const</span> <span class="kt">char</span> <span class="o">*</span> <span class="n">pathname</span><span class="o">,</span> <span class="n">mode_t</span> <span class="n">mode</span><span class="o">);</span>
<span class="mi">3</span><span class="o">.</span> <span class="nl">消息队列:</span>
    <span class="n">面向记录的消息列表</span><span class="o">,</span><span class="n">由内核维护</span><span class="o">,</span><span class="n">即使进程终止也会继续存在</span>
<span class="mi">4</span><span class="o">.</span> <span class="nl">信号量:</span>
<span class="mi">5</span><span class="o">.</span> <span class="nl">共享内存:</span>
    <span class="n">因为虚拟地址空间的实现</span><span class="o">,</span><span class="n">所以可以通过把物理地址映射到不同进程的虚拟地址空间内达到共享的目的</span>
</code></pre></div></div>

<h1 id="_2">线程通信</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">线程通信通常指的是线程间的同步机制</span><span class="o">,</span><span class="n">主要分为一下几类</span>
<span class="mi">1</span><span class="o">.</span> <span class="nc">JUC库里的一大堆</span>
<span class="mi">2</span><span class="o">.</span> <span class="kd">volatile</span>
<span class="mi">3</span><span class="o">.</span> <span class="nc">ThreadLocal</span>
<span class="mi">4</span><span class="o">.</span> <span class="n">join</span><span class="o">,</span><span class="n">sleep</span><span class="o">,</span><span class="n">wait</span><span class="o">,</span><span class="n">notify</span><span class="o">,</span><span class="n">notifyAll</span>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-08-20T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/08/20/sys-process-scheduling.html">进程调度</a></div><div class="next"><span>下篇</span><a href="/2020/09/01/jvm-class.html">Java Class</a></div></div></div>

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