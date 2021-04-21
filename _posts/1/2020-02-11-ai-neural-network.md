---
title: V1 Neural Network 神经网络
date: 2020-02-11 00:00:01 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="V1 Neural Network 神经网络"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-02-11T08:00:01+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="V1 Neural Network 神经网络" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-02-11T08:00:01+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="V1 Neural Network 神经网络" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-02-11T08:00:01+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="V1 Neural Network 神经网络" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-02-11T08:00:01+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_1">下标</h1>

<ol>
  <li><a style="color:red">(w_ij)^l</a> : 第l-1层的第j个神经元指向第l层的第i个神经元的权重</li>
  <li><a style="color:red">(a_i)^l</a> : 第l层的第i个神经元的输出值</li>
  <li><a style="color:red">(z_i)^l</a> : 第l层的第i个神经元的输入值</li>
  <li><a style="color:red">(b_i)^l</a> : 第l层的第i个神经元的偏置值</li>
  <li><a style="color:red">C</a> : 代价函数</li>
</ol>

<h1 id="_2">BP公式</h1>

<p><img src="/assets/1/img/posts/neural-network/BP4.jpg" alt="BP4" /></p>

<h1 id="_3">交叉熵代价函数</h1>

<p><img src="/assets/1/img/posts/neural-network/cross.jpg" alt="交叉熵代价函数" /></p>

<h1 id="_4">柔性最大值(softmax)</h1>

<p><img src="/assets/1/img/posts/neural-network/softmax.jpg" alt="softmax" /></p>

<h1 id="_5">柔性最大值和对数似然的反向传播</h1>

<p><img src="/assets/1/img/posts/neural-network/softmax_bp.jpg" alt="柔性最大值和对数似然的反向传播" /></p>

<h1 id="_6">正则化</h1>

<p><img src="/assets/1/img/posts/neural-network/r.jpg" alt="正则化" /></p>

<p><img src="/assets/1/img/posts/neural-network/r2.jpg" alt="正则化2" /></p>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-02-11T08:00:01+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/02/09/sys-ram.html">不同种类的RAM</a></div><div class="next"><span>下篇</span><a href="/2020/02/25/ai-pandas-excel-example.html">Pandas Excel 示例</a></div></div></div>

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