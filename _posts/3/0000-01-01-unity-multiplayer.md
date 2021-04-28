---
title: Unity Multiplayer
date: 0000-01-01 00:00:00 Z
tags:
- Unity
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Unity Multiplayer"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="0000-01-01T08:00:00+08:00">
    <meta itemprop="keywords" content="Unity"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Unity Multiplayer" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="0000-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Unity" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Unity Multiplayer" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="0000-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Unity" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Unity Multiplayer" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="0000-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Unity" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="network-manager">Network Manager</h1>

<p><img src="/assets/3/unity-multiplayer/QQ截图20210213205437.png" alt="" /></p>

<ul>
  <li>Player Prefab : 玩家操控的角色</li>
  <li>Registered Spawnable Prefabs : 其他可以通过网络来生成的物体</li>
</ul>

<p>生成的物体如果有 <code class="language-plaintext highlighter-rouge">Network Start Position</code> 组件,则物体的 <code class="language-plaintext highlighter-rouge">Position</code> 会被设置成生成物体的位置</p>

<p><img src="/assets/3/unity-multiplayer/QQ截图20210213210533.png" alt="" /></p>

<h1 id="network-manager-hud">Network Manager HUD</h1>

<p><img src="/assets/3/unity-multiplayer/QQ截图20210213205547.png" alt="" /></p>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="0000-01-01T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/0000/01/01/stl.html">STL</a></div><div class="next"><span>下篇</span><a href="/0000/01/01/xml.html">XML</a></div></div></div>

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