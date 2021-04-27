---
title: Ant Design
date: 0000-01-01 00:00:00 Z
tags:
- JS
- CSS
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Ant Design"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="0000-01-01T08:00:00+08:00">
    <meta itemprop="keywords" content="JS,CSS"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Ant Design" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="0000-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="JS,CSS" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Ant Design" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="0000-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="JS,CSS" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><p>使用 create-react-app 来创建一个实验项目:</p>

<ul>
  <li></li>
</ul>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>npm <span class="nb">install </span>create-react-app
</code></pre></div></div>

<ul>
  <li>在 package.json 里修改:</li>
</ul>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="o">{</span>
  <span class="s2">"scripts"</span>: <span class="o">{</span>
    <span class="s2">"create-react-app"</span> : <span class="s2">"create-react-app"</span>
  <span class="o">}</span>,
  ...
<span class="o">}</span>
</code></pre></div></div>

<ul>
  <li>
    <p><code class="language-plaintext highlighter-rouge">npm run create-react-app my-app</code></p>
  </li>
  <li>
    <p><code class="language-plaintext highlighter-rouge">npm install antd</code></p>
  </li>
</ul>

<p>通过上述步骤之后,文件夹结构为:</p>

<p><img src="/assets/3/ant-design/QQ截图20210202120926.png" alt="" /></p>

<p><img src="/assets/3/ant-design/QQ截图20210202120950.png" alt="" /></p>

<p><img src="/assets/3/ant-design/QQ截图20210202121006.png" alt="" /></p>

<h1 id="hello-world">Hello World</h1>

<ul>
  <li>更改 index.html : <code class="language-plaintext highlighter-rouge">&lt;div id="root"&gt;&lt;/div&gt;</code></li>
  <li>更改 index.css :</li>
</ul>

<div class="language-css highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nc">.App</span> <span class="p">{</span>
  <span class="nl">padding</span><span class="p">:</span> <span class="m">20px</span><span class="p">;</span>
<span class="p">}</span>
</code></pre></div></div>

<ul>
  <li>更改 index.js :</li>
</ul>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">import</span> <span class="nx">React</span> <span class="k">from</span> <span class="dl">"</span><span class="s2">react</span><span class="dl">"</span><span class="p">;</span>
<span class="k">import</span> <span class="nx">ReactDOM</span> <span class="k">from</span> <span class="dl">"</span><span class="s2">react-dom</span><span class="dl">"</span><span class="p">;</span>
<span class="k">import</span> <span class="p">{</span> <span class="nx">Button</span><span class="p">,</span> <span class="nx">DatePicker</span><span class="p">,</span> <span class="nx">version</span> <span class="p">}</span> <span class="k">from</span> <span class="dl">"</span><span class="s2">antd</span><span class="dl">"</span><span class="p">;</span>
<span class="k">import</span> <span class="dl">"</span><span class="s2">antd/dist/antd.css</span><span class="dl">"</span><span class="p">;</span>
<span class="k">import</span> <span class="dl">"</span><span class="s2">./index.css</span><span class="dl">"</span><span class="p">;</span>

<span class="nx">ReactDOM</span><span class="p">.</span><span class="nx">render</span><span class="p">(</span>
  <span class="o">&lt;</span><span class="nx">div</span> <span class="nx">className</span><span class="o">=</span><span class="dl">"</span><span class="s2">App</span><span class="dl">"</span><span class="o">&gt;</span>
    <span class="o">&lt;</span><span class="nx">h1</span><span class="o">&gt;</span><span class="nx">antd</span> <span class="nx">version</span><span class="p">:</span> <span class="p">{</span><span class="nx">version</span><span class="p">}</span><span class="o">&lt;</span><span class="sr">/h1</span><span class="err">&gt;
</span>    <span class="o">&lt;</span><span class="nx">DatePicker</span> <span class="o">/&gt;</span>
    <span class="o">&lt;</span><span class="nx">Button</span> <span class="nx">type</span><span class="o">=</span><span class="dl">"</span><span class="s2">primary</span><span class="dl">"</span> <span class="nx">style</span><span class="o">=</span><span class="p">{</span> <span class="na">marginLeft</span><span class="p">:</span> <span class="mi">8</span> <span class="p">}</span><span class="o">&gt;</span>
      <span class="nx">Primary</span> <span class="nx">Button</span>
    <span class="o">&lt;</span><span class="sr">/Button</span><span class="err">&gt;
</span>  <span class="o">&lt;</span><span class="sr">/div&gt;</span><span class="err">,
</span>  <span class="nb">document</span><span class="p">.</span><span class="nx">getElementById</span><span class="p">(</span><span class="dl">"</span><span class="s2">root</span><span class="dl">"</span><span class="p">)</span>
<span class="p">);</span>
</code></pre></div></div>

<ul>
  <li>
    <p><code class="language-plaintext highlighter-rouge">npm run start</code></p>
  </li>
  <li>
    <p>输出 :</p>
  </li>
</ul>

<p><img src="/assets/3/ant-design/QQ截图20210202121649.png" alt="" /></p>

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
<div class="article__section-navigator clearfix"><div class="next"><span>下篇</span><a href="/0000/01/01/douyu.html">Douyu</a></div></div></div>

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