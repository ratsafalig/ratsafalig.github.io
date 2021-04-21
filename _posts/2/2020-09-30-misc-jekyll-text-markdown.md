---
title: Markdown 以及 Jekyll TeXt内置格式
date: 2020-09-30 00:00:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Markdown 以及 Jekyll TeXt内置格式"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-09-30T08:00:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Markdown 以及 Jekyll TeXt内置格式" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-09-30T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Markdown 以及 Jekyll TeXt内置格式" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-09-30T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Markdown 以及 Jekyll TeXt内置格式" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-09-30T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="makrdown-语法">Makrdown 语法</h1>

<h2 id="标题">标题</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code># 一级标题

## 二级标题

...

###### 六级标题
</code></pre></div></div>

<h2 id="段落">段落</h2>

<h3 id="字体">字体</h3>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>*abc* 斜体

_abc_ 斜体

**abc** 粗体

__abc__ 粗体

***abc*** 粗斜体

___abc___ 粗斜体
</code></pre></div></div>

<h3 id="分割线">分割线</h3>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>*** 

* * *

- - -
</code></pre></div></div>

<p>每行三个以上的减号或者星号</p>

<h3 id="删除线">删除线</h3>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>~~abc~~
</code></pre></div></div>

<h3 id="下划线">下划线</h3>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>&lt;u&gt;abc&lt;/u&gt;
</code></pre></div></div>

<h3 id="脚注">脚注</h3>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>abc[^def]

[^def]: 注脚内容
</code></pre></div></div>

<h2 id="列表">列表</h2>

<p>有序列表</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>* a
* b
* c
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>+ a
+ b
+ c
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>- a
- b
- c
</code></pre></div></div>

<p>有序列表</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>1. a
2. b
3. c
</code></pre></div></div>

<h2 id="区块">区块</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>&gt; a
&gt; b
&gt; c

&gt; a
&gt;&gt; b
</code></pre></div></div>

<blockquote>
  <p>a</p>
  <blockquote>
    <p>b</p>
    <blockquote>
      <p>c</p>
    </blockquote>
  </blockquote>
</blockquote>

<h2 id="表格">表格</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>| 左对齐 | 右对齐 | 居中对齐 |
| :-----| ----: | :----: |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |
</code></pre></div></div>

<table>
  <thead>
    <tr>
      <th style="text-align: left">左对齐</th>
      <th style="text-align: right">右对齐</th>
      <th style="text-align: center">居中对齐</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: left">单元格</td>
      <td style="text-align: right">单元格</td>
      <td style="text-align: center">单元格</td>
    </tr>
    <tr>
      <td style="text-align: left">单元格</td>
      <td style="text-align: right">单元格</td>
      <td style="text-align: center">单元格</td>
    </tr>
  </tbody>
</table>

<h1 id="jekyll-text-markdown">Jekyll TeXt Markdown</h1>

<h2 id="提示">提示</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>Success Text
{:.success}

Info Text
{:.info}

Warning Text
{:.warning}

Error Text
{:.error}
</code></pre></div></div>

<p class="success">Success Text</p>

<p class="info">Info Text</p>

<p class="warning">Warning Text</p>

<p class="error">Error Text</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>`success`{:.success}

`warning`{:.warning}

`info`{:.info}

`error`{:.error}
</code></pre></div></div>

<p><code class="language-plaintext success highlighter-rouge">success</code></p>

<p><code class="language-plaintext warning highlighter-rouge">warning</code></p>

<p><code class="language-plaintext info highlighter-rouge">info</code></p>

<p><code class="language-plaintext error highlighter-rouge">error</code></p>

<h2 id="图片">图片</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>![Image](path-to-image){:.border}

![Image](path-to-image){:.shadow}

![Image](path-to-image){:.rounded}

![Image](path-to-image){:.circle}

![Image](path-to-image){:.border.rounded}

![Image](path-to-image){:.circle.shadow}

![Image](path-to-image){:.circle.border.shadow}
</code></pre></div></div>

<h1 id="markdown加强">Markdown加强</h1>

<p><a href="https://tianqi.name/jekyll-TeXt-theme/post/2017/07/07/mathjax.html">Jekyll TeXt MathJax</a></p>

<p><a href="https://tianqi.name/jekyll-TeXt-theme/post/2017/06/06/mermaid.html">Jekyll TeXt Mermaid</a></p>

<p><a href="https://tianqi.name/jekyll-TeXt-theme/post/2017/05/05/chart.html">Jekyll TeXt Chart</a></p>

</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-09-30T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/09/01/jvm-class.html">Java Class</a></div><div class="next"><span>下篇</span><a href="/2020/10/04/misc-mermaid.html">Mermaid 语法</a></div></div></div>

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