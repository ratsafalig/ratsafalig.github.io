---
title: Numpy AMin Amax
date: 2020-02-07 15:34:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Numpy AMin Amax"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-02-07T23:34:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Numpy AMin Amax" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-02-07T23:34:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Numpy AMin Amax" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-02-07T23:34:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Numpy AMin Amax" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-02-07T23:34:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_1">Numpy的amin函数和amax函数中的维度</h1>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>1. amin(x,n),x为数据,n为维度
2. amin计算n维度下两个数组的最小值
3. 假设x是4*5*9三维数组,
4. amin(x,0)把x剥离一层,看成4个5*9数组,比较对应的数组位置,返回一个5*9数组
5. amin(x,1)把x剥离两层,看成4次5个9*1数组的比较,返回4*9数组&lt;br&gt;
6. amin(x,2)剥离三层,看成4次5次9个元素比较,返回4*5数组&lt;br&gt;
</code></pre></div></div>

<h1 id="_2">代码</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="n">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="n">plt</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="n">pd</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="n">sns</span>

<span class="n">a</span> <span class="o">=</span> <span class="n">np</span><span class="p">.</span><span class="n">array</span><span class="p">(</span>
    <span class="p">[</span>
        <span class="p">[</span>
            <span class="p">[</span><span class="mi">1</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">4</span><span class="p">],</span>
            <span class="p">[</span><span class="mi">5</span><span class="p">,</span><span class="mi">6</span><span class="p">,</span><span class="mi">7</span><span class="p">,</span><span class="mi">8</span><span class="p">],</span>
            <span class="p">[</span><span class="mi">9</span><span class="p">,</span><span class="mi">10</span><span class="p">,</span><span class="mi">11</span><span class="p">,</span><span class="mi">12</span><span class="p">]</span>
        <span class="p">],</span>
        <span class="p">[</span>
            <span class="p">[</span><span class="mi">13</span><span class="p">,</span><span class="mi">14</span><span class="p">,</span><span class="mi">15</span><span class="p">,</span><span class="mi">16</span><span class="p">],</span>
            <span class="p">[</span><span class="mi">17</span><span class="p">,</span><span class="mi">18</span><span class="p">,</span><span class="mi">19</span><span class="p">,</span><span class="mi">20</span><span class="p">],</span>
            <span class="p">[</span><span class="mi">21</span><span class="p">,</span><span class="mi">22</span><span class="p">,</span><span class="mi">23</span><span class="p">,</span><span class="mi">24</span><span class="p">]</span>
        <span class="p">]</span>
    <span class="p">])</span>
<span class="n">a</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>array([[[ 1,  2,  3,  4],
        [ 5,  6,  7,  8],
        [ 9, 10, 11, 12]],

       [[13, 14, 15, 16],
        [17, 18, 19, 20],
        [21, 22, 23, 24]]])
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">np</span><span class="p">.</span><span class="n">amin</span><span class="p">(</span><span class="n">a</span><span class="p">,</span><span class="mi">0</span><span class="p">)</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>array([[ 1,  2,  3,  4],
       [ 5,  6,  7,  8],
       [ 9, 10, 11, 12]])
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">np</span><span class="p">.</span><span class="n">amin</span><span class="p">(</span><span class="n">a</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>array([[ 1,  2,  3,  4],
       [13, 14, 15, 16]])
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">np</span><span class="p">.</span><span class="n">amin</span><span class="p">(</span><span class="n">a</span><span class="p">,</span><span class="mi">2</span><span class="p">)</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>array([[ 1,  5,  9],
       [13, 17, 21]])
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-02-07T23:34:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/02/07/ai-pandas-idx.html">Pandas Index</a></div><div class="next"><span>下篇</span><a href="/2020/02/08/env-config-centos-with-lamp.html">LAMP</a></div></div></div>

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