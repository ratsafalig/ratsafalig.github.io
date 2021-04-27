---
title: Tomcat 类加载以及运行时序
date: 2020-07-06 00:00:00 Z
tags:
- Java
- Tomcat
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat 类加载以及运行时序"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-07-06T08:00:00+08:00">
    <meta itemprop="keywords" content="Java,Tomcat"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat 类加载以及运行时序" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-06T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat 类加载以及运行时序" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-06T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_0">参考地址</h1>

<p><a href="https://github.com/apache/tomcat/blob/master/java/org/apache/catalina/startup/Bootstrap.java">tomcat-git-hub</a></p>

<p><a href="http://tomcat.apache.org/tomcat-10.0-doc/architecture/startup/serverStartup.pdf">tomcat-doc-startup</a></p>

<p><a href="http://tomcat.apache.org/tomcat-10.0-doc/architecture/requestProcess/request-process.png">tomcat-doc-request-process</a></p>

<p><a href="http://tomcat.apache.org/tomcat-10.0-doc/architecture/requestProcess/authentication-process.png">tomcat-doc-authentication</a></p>

<h1 id="_0_1">ClassLoader</h1>

<h2 id="_0_2">双亲代理</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">java采用双亲代理的模型加载类</span><span class="o">,</span><span class="n">而且类加载器采用组合设计模式</span><span class="o">,</span><span class="n">并不是继承形式定义父类加载器</span><span class="o">.</span>
<span class="n">父类加载器是以属性的方式集成到ClassLoader的</span><span class="o">,</span><span class="n">类加载的方式是从parent</span><span class="o">.</span><span class="na">loadClass</span><span class="o">(),</span>
<span class="n">如果父类返回不为null</span><span class="o">,</span><span class="n">则采用父类加载器加载的类</span><span class="o">,</span>
<span class="n">只有所有的父类加载器加载失败才用当前类加载器加载</span><span class="o">.</span>
<span class="n">而且加载完一个类再遇到未加载的类的时候默认使用当前类加载器加载</span><span class="o">.</span>
</code></pre></div></div>
<h2 id="_0_3">Tomcat类加载</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>tomcat采用不同的解决方法去加载类,加载顺序如下:

1. Bootstrap class of your JVM
2. /WEB-INF/classes 
3. /WEB-INF/lib/*.jar 
4. System class loader classes(JVM默认App-ClassLoader)
5. Common class loader classes(Tomcat定义一个ClassLoader为Common)

但是如果设置&lt;Loader delegate="true"/&gt;(标签在&lt;Context&gt;内),就会采用双亲代理模型加载:

1. Bootstrap classes of your JVM
2. System class loader classes (described above)
3. Common class loader classes (described above)
4. /WEB-INF/classes of your web application
5. /WEB-INF/lib/*.jar of your web application
</code></pre></div></div>

<h3 id="_1">实现</h3>

<p><img src="/assets/1/tomcat/serverStartup.jpg" alt="" /></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="mi">1</span><span class="o">.</span> <span class="nc">Bootstrap调用init</span><span class="o">()</span><span class="nl">方法:</span>
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kt">void</span> <span class="nf">init</span><span class="o">()</span> <span class="kd">throws</span> <span class="nc">Exception</span> <span class="o">{</span>
        <span class="n">initClassLoaders</span><span class="o">();</span>
        <span class="nc">Thread</span><span class="o">.</span><span class="na">currentThread</span><span class="o">().</span><span class="na">setContextClassLoader</span><span class="o">(</span><span class="n">catalinaLoader</span><span class="o">);</span>
        <span class="nc">SecurityClassLoad</span><span class="o">.</span><span class="na">securityClassLoad</span><span class="o">(</span><span class="n">catalinaLoader</span><span class="o">);</span>
        <span class="c1">// Load our startup class and call its process() method</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">log</span><span class="o">.</span><span class="na">isDebugEnabled</span><span class="o">())</span>
            <span class="n">log</span><span class="o">.</span><span class="na">debug</span><span class="o">(</span><span class="s">"Loading startup class"</span><span class="o">);</span>
        <span class="nc">Class</span><span class="o">&lt;?&gt;</span> <span class="n">startupClass</span> <span class="o">=</span> <span class="n">catalinaLoader</span><span class="o">.</span><span class="na">loadClass</span><span class="o">(</span><span class="s">"org.apache.catalina.startup.Catalina"</span><span class="o">);</span>
        <span class="nc">Object</span> <span class="n">startupInstance</span> <span class="o">=</span> <span class="n">startupClass</span><span class="o">.</span><span class="na">getConstructor</span><span class="o">().</span><span class="na">newInstance</span><span class="o">();</span>
        <span class="c1">// Set the shared extensions class loader</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">log</span><span class="o">.</span><span class="na">isDebugEnabled</span><span class="o">())</span>
            <span class="n">log</span><span class="o">.</span><span class="na">debug</span><span class="o">(</span><span class="s">"Setting startup class properties"</span><span class="o">);</span>
        <span class="nc">String</span> <span class="n">methodName</span> <span class="o">=</span> <span class="s">"setParentClassLoader"</span><span class="o">;</span>
        <span class="nc">Class</span><span class="o">&lt;?&gt;</span> <span class="n">paramTypes</span><span class="o">[]</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">Class</span><span class="o">[</span><span class="mi">1</span><span class="o">];</span>
        <span class="n">paramTypes</span><span class="o">[</span><span class="mi">0</span><span class="o">]</span> <span class="o">=</span> <span class="nc">Class</span><span class="o">.</span><span class="na">forName</span><span class="o">(</span><span class="s">"java.lang.ClassLoader"</span><span class="o">);</span>
        <span class="nc">Object</span> <span class="n">paramValues</span><span class="o">[]</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">Object</span><span class="o">[</span><span class="mi">1</span><span class="o">];</span>
        <span class="n">paramValues</span><span class="o">[</span><span class="mi">0</span><span class="o">]</span> <span class="o">=</span> <span class="n">sharedLoader</span><span class="o">;</span>
        <span class="nc">Method</span> <span class="n">method</span> <span class="o">=</span>
            <span class="n">startupInstance</span><span class="o">.</span><span class="na">getClass</span><span class="o">().</span><span class="na">getMethod</span><span class="o">(</span><span class="n">methodName</span><span class="o">,</span> <span class="n">paramTypes</span><span class="o">);</span>
        <span class="n">method</span><span class="o">.</span><span class="na">invoke</span><span class="o">(</span><span class="n">startupInstance</span><span class="o">,</span> <span class="n">paramValues</span><span class="o">);</span>
        <span class="n">catalinaDaemon</span> <span class="o">=</span> <span class="n">startupInstance</span><span class="o">;</span>
    <span class="o">}</span>
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="mi">2</span><span class="o">.</span> <span class="nl">initClassLoader方法内部:</span>
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">private</span> <span class="kt">void</span> <span class="nf">initClassLoaders</span><span class="o">()</span> <span class="o">{</span>
        <span class="k">try</span> <span class="o">{</span>
            <span class="n">commonLoader</span> <span class="o">=</span> <span class="n">createClassLoader</span><span class="o">(</span><span class="s">"common"</span><span class="o">,</span> <span class="kc">null</span><span class="o">);</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">commonLoader</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
                <span class="c1">// no config file, default to this loader - we might be in a 'single' env.</span>
                <span class="n">commonLoader</span> <span class="o">=</span> <span class="k">this</span><span class="o">.</span><span class="na">getClass</span><span class="o">().</span><span class="na">getClassLoader</span><span class="o">();</span>
            <span class="o">}</span>
            <span class="n">catalinaLoader</span> <span class="o">=</span> <span class="n">createClassLoader</span><span class="o">(</span><span class="s">"server"</span><span class="o">,</span> <span class="n">commonLoader</span><span class="o">);</span>
            <span class="n">sharedLoader</span> <span class="o">=</span> <span class="n">createClassLoader</span><span class="o">(</span><span class="s">"shared"</span><span class="o">,</span> <span class="n">commonLoader</span><span class="o">);</span>
        <span class="o">}</span> <span class="k">catch</span> <span class="o">(</span><span class="nc">Throwable</span> <span class="n">t</span><span class="o">)</span> <span class="o">{</span>
            <span class="n">handleThrowable</span><span class="o">(</span><span class="n">t</span><span class="o">);</span>
            <span class="n">log</span><span class="o">.</span><span class="na">error</span><span class="o">(</span><span class="s">"Class loader creation threw exception"</span><span class="o">,</span> <span class="n">t</span><span class="o">);</span>
            <span class="nc">System</span><span class="o">.</span><span class="na">exit</span><span class="o">(</span><span class="mi">1</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>从上面两段代码可以看出Tomcat的类加载器结构:
 Bootstrap
      |
    System
      |
    Common
     /  \
Server  Shared
         /  \
   Webapp1  Webapp2 ...

其中Common是加载Bootstrap的类加载器,可以通过this.getClass().getClassLoader()提取,
Server是加载catalina实例的类加载器,
shared是应用共享的类加载器,通过设置给catalina实例的形式Catalina.setParentClassLoader()
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-07-06T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/07/03/java-juc.html">Java JUC</a></div><div class="next"><span>下篇</span><a href="/2020/07/07/java-servlet.html">Servlet</a></div></div></div>

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