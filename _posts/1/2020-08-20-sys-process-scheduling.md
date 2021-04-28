---
title: 进程调度
date: 2020-08-20 00:00:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="进程调度"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-08-20T08:00:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="进程调度" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="进程调度" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="进程调度" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="_1">批处理系统</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">批处理系统关心的是CPU利用率</span><span class="o">,</span><span class="n">因为这些CPU密集型任务大都可以预测出执行大致需要的时间</span><span class="o">,</span>
<span class="n">所以对应的它的调度算法就有如下几种</span>

<span class="mi">1</span><span class="o">.</span> <span class="no">FIFO</span>
<span class="mi">2</span><span class="o">.</span> <span class="n">最短作业优先</span>
<span class="mi">3</span><span class="o">.</span> <span class="n">最短剩余时间优先</span>
</code></pre></div></div>

<h1 id="_2">交互式系统</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">因为交互式系统要和用户交互</span><span class="o">,</span><span class="n">所以不可能采取长时间暂停的方法进行调度</span><span class="o">,</span>

<span class="mi">1</span><span class="o">.</span> <span class="nl">轮转调度:</span>
    <span class="n">划分时间片</span><span class="o">,</span><span class="n">按照时间片轮转各个进程的调度</span>
<span class="mi">2</span><span class="o">.</span> <span class="nl">优先级调度:</span>
    <span class="n">轮转调度的改进版本</span><span class="o">,</span><span class="n">加上了优先级的概念</span><span class="o">.</span><span class="na">然优先级高的进程优先得到调度</span>
<span class="mi">3</span><span class="o">.</span> <span class="nl">多级队列:</span>
    <span class="n">优先级调度的又一次改进</span><span class="o">,</span><span class="n">多级队列让优先级高的进程每轮转一次就降一个优先级</span><span class="o">,</span>
    <span class="n">同时优先级低的每次分配的时间片就更多</span><span class="o">,</span><span class="n">这样就可以实现优先级高但是需要时间短的任务被优先执行</span>
    <span class="n">随着执行时间的不断增大</span><span class="o">,</span><span class="n">它被调用到的概率也越来越低</span><span class="o">,</span><span class="n">这就保证了优先级的同时又保证了交互性</span>
<span class="mi">4</span><span class="o">.</span> <span class="nl">最短进程优先:</span>
    <span class="n">和批处理系统不同</span><span class="o">,</span><span class="n">交互式系统往往不能直到任务需要的确切时间</span><span class="o">,</span><span class="n">所以这里采用老化算法估计</span><span class="o">,</span><span class="n">数值最小的可以猜测为需要的剩余时间更少</span><span class="o">,</span>
    <span class="n">于时优先调度最短进程</span>
<span class="mi">5</span><span class="o">.</span> <span class="nl">保证调度:</span>
    <span class="n">保证调度确保每个进程有相同的概率被调度到</span>
<span class="mi">6</span><span class="o">.</span> <span class="nl">彩票调度:</span>
    <span class="n">保证调度的改进</span><span class="o">,</span><span class="n">给每个进程分配不同的权重</span><span class="o">,</span><span class="n">权重高的进程有更高的概率被调度到</span>
</code></pre></div></div>

<h1 id="_3">实时系统</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">实时系统的调度没有太多可说</span><span class="o">,</span><span class="n">只要保证在规定时间内可以完成所有交给的任务就行了</span><span class="o">(</span><span class="n">类似背包问题</span><span class="o">)</span>
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
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/08/20/sys-dead-lock.html">死锁</a></div><div class="next"><span>下篇</span><a href="/2020/08/20/sys-thread-process-communication.html">进程通信 线程通信</a></div></div></div>

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