---
title: Issue Git Bash Authority
date: 2020-01-01 00:00:00 Z
tags:
- Issue
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Issue Git Bash Authority"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-01-01T08:00:00+08:00">
    <meta itemprop="keywords" content="Issue"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Issue Git Bash Authority" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Issue" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Issue Git Bash Authority" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Issue" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="issue">Issue</h1>

<p>使用<code class="language-plaintext highlighter-rouge">git bash</code>运行:</p>
<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>bundle <span class="nb">exec </span>jekyll serve
</code></pre></div></div>
<p>出现</p>
<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nv">$ </span>bundle <span class="nb">exec </span>jekyll serve
Configuration file: C:/Users/ratsafalig/desktop/blog/_config.yml
            Source: C:/Users/ratsafalig/desktop/blog
       Destination: C:/Users/ratsafalig/desktop/blog/_site
 Incremental build: disabled. Enable with <span class="nt">--incremental</span>
      Generating...
       Jekyll Feed: Generating feed <span class="k">for </span>posts
  Conversion error: Jekyll::Converters::Scss encountered an error <span class="k">while </span>converting <span class="s1">'assets/0/css/main.scss'</span>:
                    File to import not found or unreadable: devlog. Load path: D:/Ruby/Ruby26-x64/lib/ruby/gems/2.6.0/gems/jekyll-theme-primer-0.5.4/_sass on line 3
jekyll 3.8.5 | Error:  File to import not found or unreadable: devlog.
Load path: D:/Ruby/Ruby26-x64/lib/ruby/gems/2.6.0/gems/jekyll-theme-primer-0.5.4/_sass on line 3
</code></pre></div></div>

<h1 id="原因">原因</h1>

<p><code class="language-plaintext highlighter-rouge">git bash</code>中运行部分命令有权限问题,换为cmd执行</p>
<div class="language-bash highlighter-rouge"><div class="highlight"><pre class="highlight"><code>bundle <span class="nb">exec </span>jekyll serve
</code></pre></div></div>
<p>问题不再出现</p>
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
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/0000/01/23/unity.html">Unity</a></div><div class="next"><span>下篇</span><a href="/2020/01/01/issue-ts-module-resolution.html">Issue TS Module Resolution</a></div></div></div>

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