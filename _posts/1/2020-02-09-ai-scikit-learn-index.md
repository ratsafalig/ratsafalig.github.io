---
title: Scikit Learn 索引
date: 2020-02-09 10:50:00 Z
tags:
- Misc
layout: article
---

<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Scikit Learn 索引"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-02-09T18:50:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_0">参考地址</h1>

<p><a href="https://scikit-learn.org/stable/user_guide.html">sklearn官方文档</a></p>

<p><a href="https://blog.csdn.net/antkillerfarm/article/details/80880221">参考地址(LDA推导)</a></p>

<p><a href="https://www.cnblogs.com/maybe2030/p/4946256.html">参考地址2(拉格朗日乘数法)</a></p>

<p><a href="https://zhuanlan.zhihu.com/p/56562456">参考地址(机器之心)</a></p>

<p><a href="https://blog.csdn.net/qq_20195745/article/details/82721666">参考地址2</a></p>

<p><a href="http://www.gaussianprocess.org/gpml/chapters/RW2.pdf">参考地址3(谷歌学术)</a></p>

<p><a href="http://www.gaussianprocess.org/">参考地址4(高斯过程大全)</a></p>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-02-09T18:50:00+08:00"><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/02/08/io-iocp.html">IOCP</a></div><div class="next"><span>下篇</span><a href="/2020/02/09/sys-ram.html">不同种类的RAM</a></div></div></div>

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