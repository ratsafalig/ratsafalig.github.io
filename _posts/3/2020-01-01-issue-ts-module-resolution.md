---
title: Issue TS Module Resolution
date: 2020-01-01 00:00:00 Z
tags:
- Issue
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Issue TS Module Resolution"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-01-01T08:00:00+08:00">
    <meta itemprop="keywords" content="Issue"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Issue TS Module Resolution" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Issue" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Issue TS Module Resolution" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Issue" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Issue TS Module Resolution" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Issue" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="issue">Issue</h1>

<p>在vscode里在<code class="language-plaintext highlighter-rouge">tsconfig.json</code>里加上:</p>

<div class="language-json highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="p">{</span><span class="w">
    </span><span class="err">...</span><span class="w">
    </span><span class="err">module-resolution</span><span class="w"> </span><span class="err">=</span><span class="w"> </span><span class="s2">"classic"</span><span class="w">
</span><span class="p">}</span><span class="w">
</span></code></pre></div></div>

<p>直接在vscode里运行会发现即使使用<code class="language-plaintext highlighter-rouge">import ./xxx.ts</code>形式的导入,也无法找到根目录的文件<code class="language-plaintext highlighter-rouge">xxx.ts</code><br />
必须把<code class="language-plaintext highlighter-rouge">xxx.ts</code>放入<code class="language-plaintext highlighter-rouge">node-modules</code>目录下</p>

<h1 id="解决方法">解决方法</h1>

<p>直接用cmd进行编译<code class="language-plaintext highlighter-rouge">ts</code>:</p>
<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>tsc compile <span class="nt">--module-resolution</span> <span class="o">=</span> classic
</code></pre></div></div>
<p>就可以成功找到在./目录下的模块</p>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-01-01T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/01/01/issue-git-bash-authority.html">Issue Git Bash Authority</a></div><div class="next"><span>下篇</span><a href="/2020/01/16/java-hashmap-and-concurrenthashmap.html">HashMap And ConcurrentHashMap</a></div></div></div>

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