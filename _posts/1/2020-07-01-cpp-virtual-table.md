---
title: C++ 虚表
date: 2020-07-01 00:00:00 Z
tags:
- Cpp
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="C++ 虚表"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00">
    <meta itemprop="keywords" content="Cpp"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="C++ 虚表" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Cpp" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="C++ 虚表" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Cpp" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="C++ 虚表" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Cpp" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_0">参考地址</h1>

<p><a href="https://blog.twofei.com/496/">参考地址—blog</a></p>

<h1 id="_1">多态性</h1>

<div class="language-cpp highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">class</span> <span class="nc">A</span><span class="p">{</span>
    <span class="k">virtual</span> <span class="kt">void</span> <span class="n">_1</span><span class="p">(){</span>
        <span class="c1">//A</span>
    <span class="p">}</span>
<span class="p">}</span>
<span class="k">class</span> <span class="nc">B</span> <span class="o">:</span> <span class="k">public</span> <span class="n">A</span><span class="p">{</span>
    <span class="k">virtual</span> <span class="kt">void</span> <span class="n">_1</span><span class="p">(){</span>
        <span class="c1">//B</span>
    <span class="p">}</span>
<span class="p">}</span>
<span class="n">A</span> <span class="o">*</span> <span class="n">a</span> <span class="o">=</span> <span class="k">new</span> <span class="nf">B</span><span class="p">();</span>
<span class="n">a</span><span class="o">-&gt;</span><span class="n">_1</span><span class="p">();</span>

<span class="err">这种情况下调用的是</span><span class="n">B</span><span class="err">的</span><span class="n">_1</span><span class="p">(),</span><span class="err">这种动态绑定的机制叫做多态性</span>
</code></pre></div></div>

<h1 id="_2">虚表</h1>

<div class="language-cpp highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">C</span><span class="o">++</span><span class="err">的多态</span><span class="p">(</span><span class="err">包括</span><span class="n">java</span><span class="err">也类似</span><span class="p">),</span><span class="err">是通过虚表的机制实现的</span>

<span class="mf">1.</span> <span class="err">对于每个带有</span><span class="k">virtual</span><span class="err">函数的</span><span class="o">&lt;</span><span class="k">class</span><span class="o">&gt;</span><span class="p">(</span><span class="err">包括继承而来的</span><span class="p">),</span><span class="n">C</span><span class="o">++</span><span class="err">都自动为每个</span><span class="o">&lt;</span><span class="k">class</span><span class="o">&gt;</span><span class="err">创建了一个虚表</span>
<span class="mf">2.</span> <span class="err">如果自类覆盖了父类的</span><span class="k">virtual</span><span class="err">方法</span><span class="p">,</span><span class="err">就在虚表里重写成自类的函数地址</span><span class="p">.</span>

<span class="err">在每个拥有</span><span class="k">virtual</span><span class="err">函数的</span><span class="n">class</span><span class="err">的实例对象中</span><span class="p">,</span><span class="err">实例数据的头总是存放一个名为</span><span class="n">_vptr</span><span class="err">的指针</span><span class="p">,</span>
<span class="err">这个</span><span class="n">_vptr</span><span class="err">指向了一个指针数组的</span><span class="p">,</span><span class="err">其中数组中的每个元素都是一个函数</span><span class="p">.</span>

<span class="err">例如</span><span class="o">:</span>

<span class="k">class</span> <span class="nc">A</span><span class="p">{</span>
    <span class="k">virtual</span> <span class="kt">void</span> <span class="n">_1</span><span class="p">(){}</span>
    <span class="k">virtual</span> <span class="kt">void</span> <span class="n">_2</span><span class="p">(){}</span>
<span class="p">}</span>
<span class="k">class</span> <span class="nc">B</span><span class="p">{</span>
    <span class="k">virtual</span> <span class="kt">void</span> <span class="n">_1</span><span class="p">(){}</span>
    <span class="kt">void</span> <span class="n">_3</span><span class="p">(){}</span>
<span class="p">}</span>
<span class="n">A</span> <span class="o">*</span> <span class="n">a</span> <span class="o">=</span> <span class="k">new</span> <span class="nf">B</span><span class="p">();</span>

<span class="err">这里</span><span class="o">*</span><span class="n">a</span><span class="err">的第一个信息是</span><span class="n">_vptr</span><span class="p">,</span><span class="err">如描述所示</span><span class="p">,</span><span class="err">这个</span><span class="n">vptr</span><span class="err">就是一个指针数组</span><span class="p">,</span>

<span class="err">第一个元素是</span><span class="n">B</span><span class="o">::</span><span class="n">_1</span><span class="p">()</span>
<span class="err">第二个元素是</span><span class="n">A</span><span class="o">::</span><span class="n">_2</span><span class="p">()</span>

<span class="err">对象的布局是这样的</span>

<span class="mf">1.</span> <span class="err">虚表指针</span>
<span class="mf">2.</span> <span class="err">父类数据</span>
<span class="mf">3.</span> <span class="err">本类数据</span>

<span class="err">所以把子类赋值给父类的过程实际上是截断了一部分</span><span class="p">,</span><span class="err">也就是把本类的数据扔掉</span><span class="p">.</span>
<span class="err">但是由于虚表指针始终是在对象的开头部分</span><span class="p">,</span><span class="err">所以多态性得以保留</span><span class="p">,</span><span class="err">因为虚表是每个类型唯一的</span>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-07-01T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/06/29/tomcat-realm-valve.html">Tomcat Realm Valve</a></div><div class="next"><span>下篇</span><a href="/2020/07/01/java-collection.html">Java Collection</a></div></div></div>

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