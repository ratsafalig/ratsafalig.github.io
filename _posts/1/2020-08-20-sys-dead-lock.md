---
title: 死锁
date: 2020-08-20 00:00:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="死锁"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-08-20T08:00:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="死锁" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="死锁" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_1">死锁条件</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">死锁的必要条件</span>

<span class="mi">1</span><span class="o">.</span> <span class="nl">互斥等待:</span>
    <span class="n">一个资源只能分配给一个进程</span>
<span class="mi">2</span><span class="o">.</span> <span class="nl">占有和等待条件:</span>
    <span class="n">已经得到资源的进程可以申请新资源</span>
<span class="mi">3</span><span class="o">.</span> <span class="nl">不可抢占:</span>
    <span class="n">已经分配给一个进程的资源不能被抢占</span><span class="o">,</span><span class="n">只能由它自己释放</span>
<span class="mi">4</span><span class="o">.</span> <span class="nl">环路等待:</span>
</code></pre></div></div>

<h1 id="_2">死锁检测</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">只有一种类型的资源情况下</span><span class="o">,</span><span class="n">可以画出几个节点代表进程</span><span class="o">.</span>
<span class="n">然后从所有的节点使用DFS遍历</span><span class="o">,</span><span class="n">如果存在环路</span><span class="o">,</span><span class="n">则说明出现环路等待</span>

<span class="n">有多种类型的资源的情况下</span><span class="o">,</span><span class="n">就是简单的将上述情况扩展成n维</span>
</code></pre></div></div>

<h1 id="_3">死锁恢复</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="mi">1</span><span class="o">.</span> <span class="nl">利用抢占恢复:</span>
    <span class="n">人工干预</span><span class="o">,</span><span class="n">将某个资源暂时移交给另一个进程来避免环路等待</span><span class="o">.</span>
<span class="mi">2</span><span class="o">.</span> <span class="nl">利用回滚恢复:</span>
    <span class="n">字面意思</span><span class="o">,</span><span class="n">先保存所有的状态</span><span class="o">(</span><span class="n">已经获得的资源数</span><span class="o">,</span><span class="n">寄存器等等</span><span class="o">),</span><span class="n">然后每隔一段时间进行死锁检测</span><span class="o">,</span>
    <span class="n">如果出现死锁</span><span class="o">,</span><span class="n">回滚到安全点</span>
<span class="mi">3</span><span class="o">.</span> <span class="nl">通过杀死进程恢复:</span>
    <span class="n">回滚的无脑法</span>
</code></pre></div></div>

<h1 id="_4">死锁避免</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">上文中的死锁检测是在已经发生情况下检测是否出现环路等待</span><span class="o">,</span>
<span class="n">而死锁避免探讨的是下一个状态是否会出现死锁</span><span class="o">(</span><span class="n">进入不安全状态</span><span class="o">),</span>
<span class="n">如果一个分配是不安全的</span><span class="o">,</span><span class="n">就不执行这个分配</span><span class="o">.</span>

<span class="n">假设这样一种情况</span><span class="o">,</span><span class="n">所有的进程都同一时间请求需要的最大资源数</span><span class="o">,</span>
<span class="nl">例如:</span>
<span class="n">进程A</span><span class="o">(</span><span class="n">已经得到3资源</span><span class="o">,</span><span class="n">总共需要6资源</span><span class="o">)</span>
<span class="n">进程B</span><span class="o">(</span><span class="n">已经获得4资源</span><span class="o">,</span><span class="n">总共需要9资源</span><span class="o">)</span>
<span class="n">那么这个时候就假设出现进程A申请3资源</span><span class="o">,</span><span class="n">进程B申请5资源</span><span class="o">.</span>
<span class="n">假设有一种方法可以在所有进程同时请求最大资源的时候还能完成分配的策略</span><span class="o">,</span>
<span class="n">则这种状态是安全的</span><span class="o">.</span>

<span class="n">死锁避免就是不断检测下一个状态是否是安全的</span><span class="o">,</span><span class="n">如果是安全的就不执行分配</span><span class="o">,</span>
<span class="n">通过不断迭代这一过程来达到避免死锁的目的</span><span class="o">(</span><span class="n">银行家算法</span><span class="o">)</span>
</code></pre></div></div>

<h1 id="_5">死锁预防</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">死锁避免</span><span class="o">,</span><span class="n">死锁检测的目的都是防止死锁的存在</span><span class="o">,</span><span class="n">死锁预防关心的是如何从根源上破坏死锁出现的必要条件</span><span class="o">.</span>
<span class="mi">1</span><span class="o">.</span> <span class="nl">破坏互斥条件:</span>
    <span class="n">虚拟化技术</span><span class="o">,</span><span class="n">如果两个进程都抢占一个打印机</span><span class="o">,</span><span class="n">可以给每个进程都新建一个虚拟打印机</span><span class="o">,</span><span class="n">由打印机自己调度请求</span>
<span class="mi">2</span><span class="o">.</span> <span class="nl">破坏占有和等待:</span>
    <span class="n">禁止已经持有资源的进程再请求更多的资源</span>
<span class="mi">3</span><span class="o">.</span> <span class="nl">破坏不可抢占:</span>
    <span class="n">同样可以用虚拟化技术</span>
<span class="mi">4</span><span class="o">.</span> <span class="nl">破坏环路等待条件:</span>
    <span class="n">给每个资源编号</span><span class="o">,</span><span class="n">比如资源ABCDE对应12345</span>
    <span class="n">如果一个进程申请了资源3</span><span class="o">,</span><span class="n">那么后续只能申请资源12</span><span class="o">,</span><span class="n">而不能申请45</span>
    <span class="n">这样可以保证永远不会出现环路</span>
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
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/08/10/sys-linking.html">链接过程</a></div><div class="next"><span>下篇</span><a href="/2020/08/20/sys-process-scheduling.html">进程调度</a></div></div></div>

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