---
title: Unity Avatar
date: 2021-01-23 00:00:00 Z
tags:
- Unity
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Unity Avatar"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2021-01-23T08:00:00+08:00">
    <meta itemprop="keywords" content="Unity"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Unity Avatar" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-01-23T08:00:00+08:00" />
    <meta itemprop="keywords" content="Unity" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Unity Avatar" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-01-23T08:00:00+08:00" />
    <meta itemprop="keywords" content="Unity" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="fbx-文件">FBX 文件</h1>

<p><code class="language-plaintext highlighter-rouge">FBX</code> 不仅可以包含:</p>

<blockquote>

  <ul>
    <li>材质</li>
    <li>骨骼动画</li>
    <li>3D模型</li>
    <li>层级结构</li>
    <li>…</li>
  </ul>
</blockquote>

<p>更有可能只导出 骨骼动画 ,而不导出实际的模型</p>

<h1 id="fbx-作为模型">FBX 作为模型</h1>

<p>在 Unity 里,导入的 <code class="language-plaintext highlighter-rouge">.fbx</code> 文件会以 Unity 自己的理解来识别<br />
每一个导入的 <code class="language-plaintext highlighter-rouge">.fbx</code> 都可以在 <code class="language-plaintext highlighter-rouge">Inspector</code> 界面有如下属性:</p>

<p><img src="/assets/3/unity-avatar/QQ截图20210123191201.png" alt="" /></p>

<p>其中在 <code class="language-plaintext highlighter-rouge">Rig</code> 下:</p>

<p><img src="/assets/3/unity-avatar/QQ截图20210123191353.png" alt="" /></p>

<p>如果模型是一个 人形模型 ,可以把 <code class="language-plaintext highlighter-rouge">Animation Type</code> 设置成 <code class="language-plaintext highlighter-rouge">Humanoid</code><br />
设置之后, <code class="language-plaintext highlighter-rouge">Avatar Definition</code></p>

<p><img src="/assets/3/unity-avatar/QQ截图20210123192234.png" alt="" /></p>

<blockquote>

  <ul>
    <li>Create From This Model : 创建一个 Avatar 映射</li>
    <li>Copy From Other Avatar : 使用一个现成映射</li>
  </ul>
</blockquote>

<h2 id="create-from-this-model">Create From This Model</h2>

<p><img src="/assets/3/unity-avatar/QQ截图20210123192547.png" alt="" /></p>

<p><img src="/assets/3/unity-avatar/QQ截图20210123192430.png" alt="" /></p>

<h2 id="copy-from-other-avatar">Copy From Other Avatar</h2>

<p><img src="/assets/3/unity-avatar/QQ截图20210123192608.png" alt="" /></p>

<h1 id="fbx-作为动画">FBX 作为动画</h1>

<p>由于 <code class="language-plaintext highlighter-rouge">.fbx</code> 可以只导出 骨骼动画<br />
所以动画也可以有 <code class="language-plaintext highlighter-rouge">Rig</code> 属性:</p>

<p><img src="/assets/3/unity-avatar/QQ截图20210123194245.png" alt="" /></p>

<p>Unity 的人形动画适配有两个原则:</p>

<blockquote>

  <ul>
    <li>模型必须适配自己的 Avatar</li>
    <li>模型可以使用所有的 Avatar 动画</li>
  </ul>
</blockquote>

<p><img src="/assets/3/unity-avatar/QQ截图20210123195727.png" alt="" /></p>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2021-01-23T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2021/01/22/keras.html">Keras</a></div><div class="next"><span>下篇</span><a href="/2021/01/25/scrapy.html">Scrapy</a></div></div></div>

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