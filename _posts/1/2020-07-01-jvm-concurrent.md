---
title: JVM 高效并发
date: 2020-07-01 00:00:00 Z
tags:
- Java
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="JVM 高效并发"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00">
    <meta itemprop="keywords" content="Java"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="JVM 高效并发" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="JVM 高效并发" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="JVM 高效并发" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_1">Java内存模型(Java Memory Model)</h1>

<p><img src="/assets/1/jvm/concurrent1.jpg" alt="1" /></p>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>Java内存模型是一种&lt;概念&gt;,
每个线程自己的内存叫做&lt;工作内存(worker-memory)&gt;,
共享的内存叫做&lt;主内存(main-memory)&gt;,
1. 所有的变量都是存放在&lt;主内存&gt;中,
2. 所有赋值,加载操作都是在&lt;工作内存&gt;里完成
3. &lt;工作内存&gt;存放了&lt;主内存&gt;变量的备份

这也是volatile关键字的意义,并发情况下,
一个线程对一个变量的写回并不一定马上体现在另一个线程对同一个变量的读取:
1. 线程A写回x
2. 线程B读取x
这个时候B读取的有可能是缓存在自己内存的x,如果变量定义为volatile,
Java保证每次读取都是从主内存读取
</code></pre></div></div>

<h1 id="_2">线程</h1>

<h2>线程种类</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>@. 内核线程
</code></pre></div></div>
<p><img src="/assets/1/jvm/thread1.jpg" alt="t1" /></p>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>@. 用户线程
</code></pre></div></div>
<p><img src="/assets/1/jvm/thread2.jpg" alt="t2" /></p>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>@. 混合线程
</code></pre></div></div>
<p><img src="/assets/1/jvm/thread3.jpg" alt="t3" /></p>

<h2 id="_3">调度方案</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>1. 协同式调度
    线程自己执行完让出去,由线程支配
2. 抢占式调度
    操作系统支配,操作系统让谁执行谁就执行
</code></pre></div></div>
<p><img src="/assets/1/jvm/thread4.jpg" alt="t4" /></p>

<h1 id="_5">同步</h1>

<h2 id="_6">同步方案</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>@. 同步互斥(锁)
@. 非阻塞同步(CAS操作等等)
</code></pre></div></div>
<div class="language-javascript highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">//CAS示例</span>
<span class="kd">function</span> <span class="nx">cas</span><span class="p">(</span><span class="nx">p</span> <span class="p">:</span> <span class="nx">pointer</span> <span class="nx">to</span> <span class="nx">int</span><span class="p">,</span> <span class="nx">old</span> <span class="p">:</span> <span class="nx">int</span><span class="p">,</span> <span class="k">new</span> <span class="p">:</span> <span class="nx">int</span><span class="p">)</span> <span class="nx">returns</span> <span class="nx">bool</span> <span class="p">{</span>
    <span class="k">if</span> <span class="o">*</span><span class="nx">p</span> <span class="err">≠</span> <span class="nx">old</span> <span class="p">{</span>
        <span class="k">return</span> <span class="kc">false</span>
    <span class="p">}</span>
    <span class="o">*</span><span class="nx">p</span> <span class="err">←</span> <span class="k">new</span>
    <span class="k">return</span> <span class="kc">true</span>
<span class="p">}</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>@. 无同步方案
</code></pre></div></div>

<h2 id="_7" style="color:green">优化方案</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>@. 锁消除
    JVM发现某个地方你用了同步,实际上压根不需要同步的地方的锁给他删了
@. 锁粗化
    一连串连续的同步可以被改写成一个大的同步块
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">synchronized</span><span class="o">(</span><span class="n">a</span><span class="o">){</span>
    <span class="kd">synchronized</span><span class="o">(</span><span class="n">b</span><span class="o">){</span>
    <span class="o">}</span>
<span class="o">}</span>
<span class="c1">//改写成</span>
<span class="kd">synchronized</span><span class="o">(</span><span class="n">a和b的并集</span><span class="o">){</span>
<span class="o">}</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>@. 自旋锁
    大多数锁需要等待的时间非常短,自旋锁的意思就是干等着,等待一定的周期(比如100个cpu周期)
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>@. 轻量级锁
</code></pre></div></div>
<p><img src="/assets/1/jvm/markword1.jpg" alt="mw" />
<img src="/assets/1/jvm/lock1.jpg" alt="lock1" /></p>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>在栈上维护一个mark-word,同时使用cas操作更新对象的mark-word(这个mark-word和栈上的一样),把对象的mark-word改成指向栈上这个mark-word副本的指针,如果成功,则对象拥有该锁
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>@. 偏向锁
</code></pre></div></div>
<p><img src="/assets/1/jvm/lock2.jpg" alt="lock2" /></p>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>和轻量锁差不多,不同的地方是偏向锁使用CAS把mark-word改成线程获取锁的线程的id
下一次持有该锁的线程进来的时候直接不用获取锁(CAS都不用,直接test一下就行)
</code></pre></div></div>

<h2 id="_8">轻量锁 偏向锁 重量锁</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>重量锁包含了所有等待这个锁的线程:比如A线程持有x,B和C都等待x,
那么x的锁就包含了如下信息:
1. A持有
2. B和C在等待
以便后续实施notify等操作.总而言之,多线程竞争情况下,锁需要所有竞争者的标识

但是在很多情况下.并不会出现竞争,只是偶尔出现一两次,这个时候既不能简单把锁去掉(因为可能出现竞争),
就引出了偏向锁和轻量锁的概念,如果只是一个线程在使用,直接一次CAS就可以完成偏向,
而且直接在mark-word就可以记录到底是谁持有,这种情况在另一个线程同时要竞争的时候就失效了,
因为mark-word无法储存竞争者的信息,所以就要膨胀成轻量锁,后续过程就一样了,轻量锁解决不了就继续膨胀成最终形态
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
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/07/01/jvm-classloader.html">ClassLoader</a></div><div class="next"><span>下篇</span><a href="/2020/07/01/jvm-gc.html">JVM GC</a></div></div></div>

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