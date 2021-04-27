---
title: Tomcat JNDI
date: 2020-06-15 00:00:00 Z
tags:
- Tomcat
- Java
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat JNDI"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-06-15T08:00:00+08:00">
    <meta itemprop="keywords" content="Tomcat,Java"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat JNDI" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-15T08:00:00+08:00" />
    <meta itemprop="keywords" content="Tomcat,Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat JNDI" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-15T08:00:00+08:00" />
    <meta itemprop="keywords" content="Tomcat,Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_1">参考地址</h1>

<p><a href="https://tomcat.apache.org/tomcat-9.0-doc/config/sessionidgenerator.html">参考地址—tomcat-doc-sessionidgenerator</a></p>

<p><a href="http://tomcat.apache.org/tomcat-9.0-doc/deployer-howto.html">参考地址—tomcat-doc-deploy</a></p>

<p><a href="http://tomcat.apache.org/tomcat-9.0-doc/jndi-datasource-examples-howto.html">参考地址—tomcat-doc-jndi-datasource-howto</a></p>

<p><a href="http://tomcat.apache.org/tomcat-9.0-doc/jndi-resources-howto.html">参考地址—tomcat-doc-jndi-resources-howto</a></p>

<p><a href="http://tomcat.apache.org/tomcat-9.0-doc/jdbc-pool.html">参考地址—tomcat-doc-jdbc-pool</a></p>

<h1 id="_2">标签原理</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="mi">1</span><span class="o">.</span> <span class="n">server</span><span class="o">.</span><span class="na">xml的父tag和子tag的关系大概是have</span><span class="o">-</span><span class="n">a关系的</span><span class="o">,</span>
<span class="n">可以在父tag里头配置子tag的相关配置</span><span class="o">.</span><span class="na">比如Cluster元素have</span><span class="o">-</span><span class="n">a</span> <span class="nc">Manager元素</span><span class="o">,</span><span class="n">于是它可以定制自己的Cluster</span> <span class="nc">Manager</span>
<span class="mi">2</span><span class="o">.</span> <span class="n">通常可以看见各种应用直接用一个new</span> <span class="nc">InitialContext就简单的创建一个上下文</span><span class="o">.</span><span class="na">但是读取的文件又是不同类型的</span><span class="o">,</span><span class="nl">这主要通过以下实现:</span>
<span class="nc">System</span><span class="o">.</span><span class="na">setProperty</span><span class="o">(</span><span class="n">javax</span><span class="o">.</span><span class="na">naming</span><span class="o">.</span><span class="na">Context</span><span class="o">.</span><span class="na">INITIAL_CONTEXT_FACTORY</span><span class="o">,</span><span class="s">"org.apache.naming.java.javaURLContextFactory"</span><span class="o">);</span>
</code></pre></div></div>

<h1 id="_3">JNDI</h1>

<h2 id="_3_1">Environment env-entry</h2>

<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;Environment&gt;</span>代表环境变量,可以通过java:comp/env前缀的jndi进行查看

<span class="nt">&lt;Context&gt;</span>
  <span class="nt">&lt;Environment</span> <span class="na">name=</span><span class="s">"maxExemptions"</span> <span class="na">value=</span><span class="s">"10"</span>
         <span class="na">type=</span><span class="s">"java.lang.Integer"</span> <span class="na">override=</span><span class="s">"false"</span><span class="nt">/&gt;</span>
<span class="nt">&lt;/Context&gt;</span>
<span class="c">&lt;!--.............................................--&gt;</span>
<span class="nt">&lt;env-entry&gt;</span>
  <span class="nt">&lt;env-entry-name&gt;</span>maxExemptions<span class="nt">&lt;/env-entry-name&gt;</span>
  <span class="nt">&lt;env-entry-value&gt;</span>10<span class="nt">&lt;/env-entry-value&gt;</span>
  <span class="nt">&lt;env-entry-type&gt;</span>java.lang.Integer<span class="nt">&lt;/env-entry-type&gt;</span>
<span class="nt">&lt;/env-entry&gt;</span>
</code></pre></div></div>

<h2 id="_3_2">Listener</h2>

<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;Listener&gt;</span>标签不多说,简单的观察者模式

<span class="nt">&lt;Context&gt;</span>
  <span class="nt">&lt;Listener</span> <span class="na">className=</span><span class="s">"com.mycompany.mypackage.MyListener"</span> <span class="err">...</span> <span class="nt">&gt;</span>
<span class="nt">&lt;/Context&gt;</span>
</code></pre></div></div>

<h2 id="_3_3">Resource resource-ref</h2>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;Resource&gt;</span>相当于spring的bean.可以通过java:comp/env前缀的jndi查看

<span class="nt">&lt;Context&gt;</span>
  <span class="nt">&lt;Resource</span> <span class="na">name=</span><span class="s">"jdbc/EmployeeDB"</span> <span class="na">auth=</span><span class="s">"Container"</span>
            <span class="na">type=</span><span class="s">"javax.sql.DataSource"</span>
     <span class="na">description=</span><span class="s">"Employees Database for HR Applications"</span><span class="nt">/&gt;</span>
<span class="nt">&lt;/Context&gt;</span>
<span class="c">&lt;!--....................................................--&gt;</span>
<span class="nt">&lt;resource-ref&gt;</span>
  <span class="nt">&lt;description&gt;</span>Employees Database for HR Applications<span class="nt">&lt;/description&gt;</span>
  <span class="nt">&lt;res-ref-name&gt;</span>jdbc/EmployeeDB<span class="nt">&lt;/res-ref-name&gt;</span>
  <span class="nt">&lt;res-ref-type&gt;</span>javax.sql.DataSource<span class="nt">&lt;/res-ref-type&gt;</span>
  <span class="nt">&lt;res-auth&gt;</span>Container<span class="nt">&lt;/res-auth&gt;</span>
<span class="nt">&lt;/resource-ref&gt;</span>
</code></pre></div></div>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code>可以在 <span class="nt">&lt;resource-ref&gt;</span> 里头配置大部分,但是一旦涉及到setter,就只能在<span class="nt">&lt;Resource&gt;</span>里配置,比如JDBC,
这种情况下,要在context.xml里的 <span class="nt">&lt;Resource&gt;</span> 里配置:
<span class="nt">&lt;Context&gt;</span>
  <span class="nt">&lt;Resource</span> <span class="na">name=</span><span class="s">"jdbc/EmployeeDB"</span>
            <span class="na">auth=</span><span class="s">"Container"</span>
            <span class="na">type=</span><span class="s">"javax.sql.DataSource"</span>
            <span class="na">username=</span><span class="s">"dbusername"</span>
            <span class="na">password=</span><span class="s">"dbpassword"</span>
            <span class="na">driverClassName=</span><span class="s">"org.hsql.jdbcDriver"</span>
            <span class="na">url=</span><span class="s">"jdbc:HypersonicSQL:database"</span>
            <span class="na">maxTotal=</span><span class="s">"8"</span>
            <span class="na">maxIdle=</span><span class="s">"4"</span><span class="nt">/&gt;</span>
<span class="nt">&lt;/Context&gt;</span>
</code></pre></div></div>

<h1 id="_4">Connector</h1>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>connector如名字所示,主要是支持http协议的功能.
它的主要配置项也是关于协议层面的配置:监听端口之类的
connector没有classname属性,所以它的特性通过protocol体现,tomcat内置协议:HTTP/1.1,HTTP/2,AJP
当设置HTTP/1.1时候,可以是以下几种protocol之一:

1. HTTP/1.1(默认)
2. org.apache.coyote.http11.Http11NioProtocol 
3. org.apache.coyote.http11.Http11Nio2Protocol
4. org.apache.coyote.http11.Http11AprProtocol
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>当设置为HTTP\/2时候,需要在connector里头嵌套一个&lt;UpgradeProtocol&gt;并进行设置
如果要使用AJP协议,protocol如下:
1. AJP/1.3
2. org.apache.coyote.ajp.AjpNioProtocol
3. org.apache.coyote.ajp.AjpNio2Protocol
4. org.apache.coyote.ajp.AjpAprProtocol
</code></pre></div></div>

</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-06-15T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/06/09/dubbo-architecture.html">Dubbo Architecture</a></div><div class="next"><span>下篇</span><a href="/2020/06/29/js-ts.html">TypeScript 入门</a></div></div></div>

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