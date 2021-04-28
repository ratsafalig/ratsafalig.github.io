---
title: Tomcat Deploy 部署
date: 2020-07-07 00:00:00 Z
tags:
- Java
- Tomcat
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Deploy 部署"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-07-07T08:00:00+08:00">
    <meta itemprop="keywords" content="Java,Tomcat"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Deploy 部署" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-07T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Deploy 部署" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-07T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Deploy 部署" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-07T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="_0">参考地址</h1>

<h1 id="_1">Host</h1>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>假设一下一个文件结构:
</code></pre></div></div>
<pre><code class="language-mermaid">graph TD;
    id0(webapp/)
    id1(foo.xml)
    id2(bar.xml)
    id3(baz/)
    id4(qux.war)
    id5(index.html)
    id6(index.html)
    id7(foo/)
    id8(bar/)
    id3--&gt;id5
    id4--&gt;id6
    id0--&gt;id1
    id0--&gt;id2
    id0--&gt;id3
    id0--&gt;id4
    id0--&gt;id7
    id0--&gt;id8
</code></pre>

<h2 id="_2">Host标签的deployOnStartup</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>如果启用了deployOnStartup,则context.xml不一定在webapp1/META-INF/context.xml下,而是可能在appBase下,
例如foo.xml对应/foo的context.xml,foo#bar.xml对应/foo/bar的context.xml

部署的顺序是:

1. foo.xml,foo#bar.xml
2. foo/,bar/
3. baz/
4. qux.war

官方给出的顺序是:
1. .xml将会首先被部署(包括.xml对应的webapp)
2. 没有.xml对应的文件夹结构webapp被部署
3. .war被部署
</code></pre></div></div>

<h2 id="_3">Host标签的autoDeploy</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>如果启用了autoDeploy,则部署tomcat会在每次配置变动的时候重新加载配置,
配置顺序如下:
1. appBase下的.war
2. appBase下的文件夹webapp
3. 如果.war更改,重新部署并解压(如果unpackWar="false",则不解压)
4. 如果web.xml或者其他server.xml里的WatchedResource被更改,重新部署应用
5. 如果context.xml或者等价的.xml被更改,重新部署应用
6. 如果host或者全局context.xml被更改,重新部署应用
7. 如果对应的$CATALINA_BASE/conf/[enginename]/[hostname]/添加了context.xml,重新部署应用
8. 如果.war或者文件夹结构webapp被删除,则取消部署一个应用
</code></pre></div></div>

<h1 id="_3_1">Context</h1>

<h2 id="_4">Context标签的docBase</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>这个文档只能在当Context元素是在server.xml或者docBase不在webBase里的时候才能指定,
但是我还发现如果使用autoDeploy或者deployOnStartup的时候,不会识别这个信息,
也就是说前两个属性其一之一被设置为true的时候,
所有的webapp都只能在appBase里,但是我只在windows环境下试过,所以还不确定这个特性是否是真的
</code></pre></div></div>

<h2 id="_5">Context标签的path</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>path属性表明前置url,比如path="/bar",所有url为/bar的才会匹配这个webapp
由于tomcat会自动推断,所以只有在:
1. Context在server.xml里
2. deployOnStartup设置为false
3. autoDeploy设置为false
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-07-07T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/07/07/java-servlet.html">Servlet</a></div><div class="next"><span>下篇</span><a href="/2020/07/11/io-java-io.html">Java IO</a></div></div></div>

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