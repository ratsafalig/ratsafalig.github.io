---
title: HashMap And ConcurrentHashMap
date: 2020-01-16 00:00:00 Z
tags:
- Java
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="HashMap And ConcurrentHashMap"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-01-16T08:00:00+08:00">
    <meta itemprop="keywords" content="Java"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="HashMap And ConcurrentHashMap" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-01-16T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="HashMap And ConcurrentHashMap" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-01-16T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="HashMap And ConcurrentHashMap" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-01-16T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><p><a href="https://crossoverjie.top/2018/07/23/java-senior/ConcurrentHashMap/">HashMap? ConcurrentHashMap? 相信看完这篇没人能难住你！</a></p>

<p><a href="https://dzone.com/articles/how-concurrenthashmap-works-internally-in-java">How ConcurrentHashMap Works Internally in Java</a></p>

<p><img src="/assets/3/java-hashmap-and-concurrenthashmap/HashMap.png" alt="" /></p>

<p><img src="/assets/3/java-hashmap-and-concurrenthashmap/LinkedList.png" alt="" /></p>

<h1 id="hashmap">HashMap</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">class</span> <span class="nc">HashMap</span><span class="o">{</span>
    <span class="kd">static</span> <span class="kd">final</span> <span class="kt">int</span> <span class="no">MAXIMUM_CAPACITY</span> <span class="o">=</span> <span class="mi">1</span> <span class="o">&lt;&lt;</span> <span class="mi">30</span><span class="o">;</span>
    <span class="o">...</span>
    <span class="kd">public</span> <span class="nf">HashMap</span><span class="o">(</span><span class="kt">int</span> <span class="n">initialCapacity</span><span class="o">,</span> <span class="kt">float</span> <span class="n">loadFactor</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">initialCapacity</span> <span class="o">&gt;</span> <span class="no">MAXIMUM_CAPACITY</span><span class="o">)</span>
            <span class="n">initialCapacity</span> <span class="o">=</span> <span class="no">MAXIMUM_CAPACITY</span><span class="o">;</span>
        <span class="k">this</span><span class="o">.</span><span class="na">loadFactor</span> <span class="o">=</span> <span class="n">loadFactor</span><span class="o">;</span>
        <span class="k">this</span><span class="o">.</span><span class="na">threshold</span> <span class="o">=</span> <span class="n">tableSizeFor</span><span class="o">(</span><span class="n">initialCapacity</span><span class="o">);</span>
    <span class="o">}</span>
    <span class="o">...</span>
    <span class="kd">static</span> <span class="kd">final</span> <span class="kt">int</span> <span class="nf">tableSizeFor</span><span class="o">(</span><span class="kt">int</span> <span class="n">cap</span><span class="o">)</span> <span class="o">{</span>
        <span class="kt">int</span> <span class="n">n</span> <span class="o">=</span> <span class="o">-</span><span class="mi">1</span> <span class="o">&gt;&gt;&gt;</span> <span class="nc">Integer</span><span class="o">.</span><span class="na">numberOfLeadingZeros</span><span class="o">(</span><span class="n">cap</span> <span class="o">-</span> <span class="mi">1</span><span class="o">);</span> <span class="c1">// &gt;&gt;不会位移符号位,&gt;&gt;&gt;会位移符号位</span>
        <span class="k">return</span> <span class="o">(</span><span class="n">n</span> <span class="o">&lt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">?</span> <span class="mi">1</span> <span class="o">:</span> <span class="o">(</span><span class="n">n</span> <span class="o">&gt;=</span> <span class="no">MAXIMUM_CAPACITY</span><span class="o">)</span> <span class="o">?</span> <span class="no">MAXIMUM_CAPACITY</span> <span class="o">:</span> <span class="n">n</span> <span class="o">+</span> <span class="mi">1</span><span class="o">;</span> <span class="c1">// 如果 n &lt; 0 返回 1, 如果 n &gt;= MAXINUM__CAPACITY 返回 MAXIUM_CAPACITY, 否则返回正常的 n + 1</span>
    <span class="o">}</span>
    <span class="o">...</span>

    <span class="kd">final</span> <span class="no">V</span> <span class="nf">putVal</span><span class="o">(</span><span class="kt">int</span> <span class="n">hash</span><span class="o">,</span> <span class="no">K</span> <span class="n">key</span><span class="o">,</span> <span class="no">V</span> <span class="n">value</span><span class="o">,</span> <span class="kt">boolean</span> <span class="n">onlyIfAbsent</span><span class="o">,</span> <span class="kt">boolean</span> <span class="n">evict</span><span class="o">)</span> <span class="o">{</span>
        <span class="o">...</span>
        <span class="k">if</span><span class="o">(++</span><span class="n">size</span> <span class="o">&gt;</span> <span class="n">threshold</span><span class="o">){</span>
            <span class="n">resize</span><span class="o">();</span>
        <span class="o">}</span>
        <span class="o">...</span>
    <span class="o">}</span>

    <span class="kd">final</span> <span class="nc">Node</span><span class="o">&lt;</span><span class="no">K</span><span class="o">,</span><span class="no">V</span><span class="o">&gt;[]</span> <span class="nf">resize</span><span class="o">()</span> <span class="o">{</span>
        <span class="n">threshold</span> <span class="o">=</span> <span class="o">...;</span>
        <span class="n">capacity</span> <span class="o">=</span> <span class="o">...;</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<blockquote>

  <p>hashmap的关键参数有:</p>
  <ul>
    <li>size       : 当前map里有多少个元素</li>
    <li>capacity   : 当前map的全部可用空间</li>
    <li>loadFactor : 衡量map满的程度, size / capacity,默认为0.75</li>
    <li>threshold  : 当size大于threshold的时候,进行resize,通常情况下threshold = capacity * loadFactor</li>
  </ul>
</blockquote>

<h2 id="死锁">死锁</h2>

<p><a href="https://www.cnblogs.com/andy-zhou/p/5402984.html">HashMap多线程并发问题分析</a></p>

<p><img src="/assets/3/java-hashmap-and-concurrenthashmap/142929_Vawr_120166.jpg" alt="" /></p>

<h1 id="concurrenthashmap">ConcurrentHashMap</h1>

<p><a href="https://www.cnblogs.com/huangjuncong/p/9478505.html">Java并发编程笔记之ConcurrentHashMap原理探究</a></p>

<p><img src="/assets/3/java-hashmap-and-concurrenthashmap/1202638-20180814213921035-778397290.png" alt="" /></p>

<p><code class="language-plaintext highlighter-rouge">ConcurrentHashMap</code>和<code class="language-plaintext highlighter-rouge">HashMap</code>的改进在于,<code class="language-plaintext highlighter-rouge">CHM</code>(<code class="language-plaintext highlighter-rouge">ConcurrentHashMap</code>)的结构是二层的:</p>
<blockquote>

  <ul>
    <li>HashMap:
      <ul>
        <li>表
          <ul>
            <li>链
              <ul>
                <li>点(key : val)</li>
              </ul>
            </li>
          </ul>
        </li>
      </ul>
    </li>
    <li>ConcurrentHashMap:
      <ul>
        <li>段
          <ul>
            <li>表
              <ul>
                <li>链
                  <ul>
                    <li>点(key : val)</li>
                  </ul>
                </li>
              </ul>
            </li>
          </ul>
        </li>
      </ul>
    </li>
  </ul>
</blockquote>

<p>CHM维护了多个段(实际上就是维护多个<code class="language-plaintext highlighter-rouge">HashMap</code>),每当对一个值插入时<br />
会先计算hash值存到一个Segment,再次计算hash计算该存到该Segment的什么位置<br />
当需要resize的时候,仅仅对该Segment加锁(ReentrantLock)</p>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-01-16T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/01/01/issue-ts-module-resolution.html">Issue TS Module Resolution</a></div><div class="next"><span>下篇</span><a href="/2020/02/05/misc-uri-standard.html">URI 标准</a></div></div></div>

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