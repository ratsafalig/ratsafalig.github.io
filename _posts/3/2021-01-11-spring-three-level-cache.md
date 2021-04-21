---
title: Spring Three Level Cache (Spring 三级缓存)
date: 2021-01-11 00:00:00 Z
tags:
- Java
- Spring
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Spring Three Level Cache (Spring 三级缓存)"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2021-01-11T08:00:00+08:00">
    <meta itemprop="keywords" content="Java,Spring"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Spring Three Level Cache (Spring 三级缓存)" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-01-11T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Spring" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="循环依赖问题">循环依赖问题</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">class</span> <span class="nc">Main</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="kd">static</span> <span class="kt">void</span> <span class="nf">main</span><span class="o">(</span><span class="nc">String</span><span class="o">[]</span> <span class="n">args</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">Exception</span> <span class="o">{</span>
        <span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">.</span><span class="na">println</span><span class="o">(</span><span class="k">new</span> <span class="no">A</span><span class="o">());</span>
    <span class="o">}</span>

<span class="o">}</span>
<span class="kd">class</span> <span class="nc">A</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="nf">A</span><span class="o">()</span> <span class="o">{</span>
        <span class="k">new</span> <span class="nf">B</span><span class="o">();</span>
    <span class="o">}</span>
<span class="o">}</span>
<span class="kd">class</span> <span class="nc">B</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="nf">B</span><span class="o">()</span> <span class="o">{</span>
        <span class="k">new</span> <span class="nf">A</span><span class="o">();</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<p>会出现Stackoverflow</p>

<h1 id="spring-循环依赖问题">Spring 循环依赖问题</h1>

<h2 id="启动时出错">启动时出错</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nd">@Service</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">A</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="nf">A</span><span class="o">(</span><span class="no">B</span> <span class="n">b</span><span class="o">)</span> <span class="o">{</span>
    <span class="o">}</span>
<span class="o">}</span>
<span class="nd">@Service</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">B</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="nf">B</span><span class="o">(</span><span class="no">A</span> <span class="n">a</span><span class="o">)</span> <span class="o">{</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="运行时出错">运行时出错</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">package</span> <span class="nn">com.example.demo</span><span class="o">;</span>


<span class="kn">import</span> <span class="nn">org.springframework.beans.factory.annotation.Autowired</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.springframework.boot.SpringApplication</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.springframework.boot.autoconfigure.SpringBootApplication</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.springframework.context.ApplicationContext</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.springframework.context.annotation.Bean</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.springframework.context.annotation.Configuration</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.springframework.context.annotation.Scope</span><span class="o">;</span>

<span class="kd">class</span> <span class="nc">A</span><span class="o">{</span>
    <span class="kd">static</span> <span class="kt">int</span> <span class="n">count</span> <span class="o">=</span> <span class="mi">1</span><span class="o">;</span>
    <span class="kd">public</span> <span class="nf">A</span><span class="o">(){</span>
        <span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">.</span><span class="na">println</span><span class="o">(</span><span class="s">"A --- "</span> <span class="o">+</span> <span class="n">count</span><span class="o">++);</span>
    <span class="o">}</span>

    <span class="nd">@Autowired</span>
    <span class="no">B</span> <span class="n">b</span><span class="o">;</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">setB</span><span class="o">(</span><span class="no">B</span> <span class="n">b</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">this</span><span class="o">.</span><span class="na">b</span> <span class="o">=</span> <span class="n">b</span><span class="o">;</span>
    <span class="o">}</span>
    <span class="kd">public</span> <span class="no">B</span> <span class="nf">getB</span><span class="o">()</span> <span class="o">{</span>
        <span class="k">return</span> <span class="n">b</span><span class="o">;</span>
    <span class="o">}</span>
<span class="o">}</span>

<span class="kd">class</span> <span class="nc">B</span><span class="o">{</span>
	<span class="kd">static</span> <span class="kt">int</span> <span class="n">count</span> <span class="o">=</span> <span class="mi">1</span><span class="o">;</span>
	<span class="kd">public</span> <span class="nf">B</span><span class="o">(){</span>
		<span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">.</span><span class="na">println</span><span class="o">(</span><span class="s">"B --- "</span> <span class="o">+</span> <span class="n">count</span><span class="o">++);</span>
	<span class="o">}</span>

	<span class="nd">@Autowired</span>
	<span class="no">A</span> <span class="n">a</span><span class="o">;</span>

	<span class="kd">public</span> <span class="kt">void</span> <span class="nf">setA</span><span class="o">(</span><span class="no">A</span> <span class="n">a</span><span class="o">)</span> <span class="o">{</span>
		<span class="k">this</span><span class="o">.</span><span class="na">a</span> <span class="o">=</span> <span class="n">a</span><span class="o">;</span>
	<span class="o">}</span>
	<span class="kd">public</span> <span class="no">A</span> <span class="nf">getA</span><span class="o">()</span> <span class="o">{</span>
		<span class="k">return</span> <span class="n">a</span><span class="o">;</span>
	<span class="o">}</span>
<span class="o">}</span>

<span class="nd">@Configuration</span>
<span class="kd">class</span> <span class="nc">Config</span><span class="o">{</span>
	<span class="nd">@Bean</span>
	<span class="nd">@Scope</span><span class="o">(</span><span class="n">scopeName</span> <span class="o">=</span> <span class="s">"prototype"</span><span class="o">)</span>
	<span class="no">A</span> <span class="nf">createA</span><span class="o">(){</span>
		<span class="no">A</span> <span class="n">a</span> <span class="o">=</span> <span class="k">new</span> <span class="no">A</span><span class="o">();</span>
		<span class="n">a</span><span class="o">.</span><span class="na">setB</span><span class="o">(</span><span class="n">createB</span><span class="o">());</span>
		<span class="k">return</span> <span class="n">a</span><span class="o">;</span>
	<span class="o">}</span>
	<span class="nd">@Bean</span>
	<span class="nd">@Scope</span><span class="o">(</span><span class="n">scopeName</span> <span class="o">=</span> <span class="s">"prototype"</span><span class="o">)</span>
	<span class="no">B</span> <span class="nf">createB</span><span class="o">(){</span>
		<span class="no">B</span> <span class="n">b</span> <span class="o">=</span> <span class="k">new</span> <span class="no">B</span><span class="o">();</span>
		<span class="n">b</span><span class="o">.</span><span class="na">setA</span><span class="o">(</span><span class="n">createA</span><span class="o">());</span>
		<span class="k">return</span> <span class="n">b</span><span class="o">;</span>
	<span class="o">}</span>
<span class="o">}</span>

<span class="nd">@SpringBootApplication</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">DemoApplication</span> <span class="o">{</span>
	<span class="kd">public</span> <span class="kd">static</span> <span class="kt">void</span> <span class="nf">main</span><span class="o">(</span><span class="nc">String</span><span class="o">[]</span> <span class="n">args</span><span class="o">)</span> <span class="o">{</span>
		<span class="nc">ApplicationContext</span> <span class="n">ac</span> <span class="o">=</span> <span class="nc">SpringApplication</span><span class="o">.</span><span class="na">run</span><span class="o">(</span><span class="nc">DemoApplication</span><span class="o">.</span><span class="na">class</span><span class="o">,</span> <span class="n">args</span><span class="o">);</span>
		<span class="no">A</span> <span class="n">a</span> <span class="o">=</span> <span class="o">(</span><span class="no">A</span><span class="o">)</span><span class="n">ac</span><span class="o">.</span><span class="na">getBean</span><span class="o">(</span><span class="s">"createA"</span><span class="o">);</span>
	<span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="不会出错">不会出错</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nd">@Service</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">A</span> <span class="o">{</span>
    <span class="nd">@Autowired</span>
    <span class="kd">private</span> <span class="no">B</span> <span class="n">b</span><span class="o">;</span>
<span class="o">}</span>

<span class="nd">@Service</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">B</span> <span class="o">{</span>
    <span class="nd">@Autowired</span>
    <span class="kd">private</span> <span class="no">A</span> <span class="n">a</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>

<h1 id="原因">原因</h1>

<p><img src="/assets/3/spring-three-level-cache/cache1.png" alt="" /></p>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2021-01-11T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2021/01/11/spring-mvc.html">SpringMvc</a></div><div class="next"><span>下篇</span><a href="/2021/01/11/spring.html">Spring</a></div></div></div>

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