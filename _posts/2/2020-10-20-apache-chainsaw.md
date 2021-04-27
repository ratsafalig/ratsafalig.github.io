---
title: Apache Chainsaw
date: 2020-10-20 00:00:00 Z
tags:
- Java
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Apache Chainsaw"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-10-20T08:00:00+08:00">
    <meta itemprop="keywords" content="Java"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Apache Chainsaw" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Apache Chainsaw" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Apache Chainsaw" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="chainsaw是什么">Chainsaw是什么</h1>

<p><code class="language-plaintext highlighter-rouge">Chainsaw</code>是一个<code class="language-plaintext highlighter-rouge">Log4j</code>的配套软件,可以提供可视化,远程的日志查看功能(见过<code class="language-plaintext highlighter-rouge">wireshark</code>吗,差不多就是这么个软件)</p>

<p><img src="/assets/2/chainsaw-1.jpg" alt="" /></p>

<h1 id="chainsaw能干嘛">Chainsaw能干嘛</h1>

<blockquote>

  <ul>
    <li>查看远程事件
      <blockquote>
        <p>远程的事件使用<code class="language-plaintext highlighter-rouge">log4j 1.3</code>新提供的<code class="language-plaintext highlighter-rouge">Receiver</code>概念被<code class="language-plaintext highlighter-rouge">Chainsaw</code>接收</p>
      </blockquote>
    </li>
    <li>自定义配置保存
      <blockquote>
        <p>可以自由定义多种配置的<code class="language-plaintext highlighter-rouge">Chainsaw</code>,并且在下次打开的时候会自动加载该配置</p>
      </blockquote>
    </li>
    <li>响应
      <blockquote>
        <p>自定义事件刷新频率</p>
      </blockquote>
    </li>
    <li>标签
      <blockquote>
        <p>为每个远程主机/应用分配一个标签,并且可以把每个应用的标签和主窗口分离,实现监控多个应用</p>
      </blockquote>
    </li>
    <li>颜色
      <blockquote>
        <p>和<code class="language-plaintext highlighter-rouge">wireshark</code>差不多,对不同的消息类型定义不同的显示颜色</p>
      </blockquote>
    </li>
    <li>过滤
      <blockquote>
        <p>可以过滤,让窗口只显示想输出的事件</p>
      </blockquote>
    </li>
    <li>循环显示
      <blockquote>
        <p>意思就是窗口可以一直跳动显示所有新来的消息</p>
      </blockquote>
    </li>
    <li>文档
      <blockquote>
        <p>提供完整的<code class="language-plaintext highlighter-rouge">html</code>文档</p>
      </blockquote>
    </li>
  </ul>
</blockquote>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-10-20T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/10/18/misc-linux-dynamic-linking.html">Linux 动态链接 Dynamic Linking</a></div><div class="next"><span>下篇</span><a href="/2021/01/07/com.html">COM Component Object Model</a></div></div></div>

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