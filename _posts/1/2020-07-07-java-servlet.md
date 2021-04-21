---
title: Servlet
date: 2020-07-07 00:00:00 Z
tags:
- Java
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Servlet"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-07-07T08:00:00+08:00">
    <meta itemprop="keywords" content="Java"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Servlet" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-07T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Servlet" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-07T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_0">参考地址</h1>

<p><a href="https://www.runoob.com/servlet/servlet-intro.html">runoob</a></p>

<p><a href="http://tomcat.apache.org/tomcat-9.0-doc/config/context.html">tomcat-doc-context</a></p>

<h1 id="_1">web.xml</h1>

<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="cp">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span>
<span class="c">&lt;!--
 Licensed to the Apache Software Foundation (ASF) under one or more
  contributor license agreements.  See the NOTICE file distributed with
  this work for additional information regarding copyright ownership.
  The ASF licenses this file to You under the Apache License, Version 2.0
  (the "License"); you may not use this file except in compliance with
  the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
--&gt;</span>
<span class="nt">&lt;web-app</span> <span class="na">xmlns=</span><span class="s">"http://xmlns.jcp.org/xml/ns/javaee"</span>
  <span class="na">xmlns:xsi=</span><span class="s">"http://www.w3.org/2001/XMLSchema-instance"</span>
  <span class="na">xsi:schemaLocation=</span><span class="s">"http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"</span>
  <span class="na">version=</span><span class="s">"4.0"</span>
  <span class="na">metadata-complete=</span><span class="s">"true"</span><span class="nt">&gt;</span>

  <span class="nt">&lt;display-name&gt;&lt;/display-name&gt;</span>
  <span class="nt">&lt;description&gt;</span>
  <span class="nt">&lt;/description&gt;</span>

  <span class="nt">&lt;request-character-encoding&gt;</span>UTF-8<span class="nt">&lt;/request-character-encoding&gt;</span>

  <span class="nt">&lt;servlet&gt;</span>
    <span class="nt">&lt;servlet-name&gt;</span>my-servlet<span class="nt">&lt;/servlet-name&gt;</span>
    <span class="nt">&lt;servlet-class&gt;</span>a.b.c.MyServlet<span class="nt">&lt;/servlet-class&gt;</span>

    <span class="nt">&lt;init-param&gt;</span>
      <span class="nt">&lt;param-name&gt;</span>debug<span class="nt">&lt;/param-name&gt;</span>
      <span class="nt">&lt;param-value&gt;</span>0<span class="nt">&lt;/param-value&gt;</span>
    <span class="nt">&lt;/init-param&gt;</span>

    <span class="nt">&lt;multipart-config&gt;</span>
      <span class="c">&lt;!-- 50MB max --&gt;</span>
      <span class="nt">&lt;max-file-size&gt;</span>52428800<span class="nt">&lt;/max-file-size&gt;</span>
      <span class="nt">&lt;max-request-size&gt;</span>52428800<span class="nt">&lt;/max-request-size&gt;</span>
      <span class="nt">&lt;file-size-threshold&gt;</span>0<span class="nt">&lt;/file-size-threshold&gt;</span>
    <span class="nt">&lt;/multipart-config&gt;</span>
  <span class="nt">&lt;/servlet&gt;</span>

  <span class="nt">&lt;servlet-mapping&gt;</span>
    <span class="nt">&lt;servlet-name&gt;</span>my-servlet<span class="nt">&lt;/servlet-name&gt;</span>
    <span class="nt">&lt;url-pattern&gt;</span>/*<span class="nt">&lt;/url-pattern&gt;</span>

    <span class="nt">&lt;init-param&gt;</span>
      <span class="nt">&lt;param-name&gt;</span>debug<span class="nt">&lt;/param-name&gt;</span>
      <span class="nt">&lt;param-value&gt;</span>0<span class="nt">&lt;/param-value&gt;</span>
    <span class="nt">&lt;/init-param&gt;</span>
  <span class="nt">&lt;/servlet-mapping&gt;</span>

  <span class="nt">&lt;filter&gt;</span>
    <span class="nt">&lt;filter-name&gt;</span>my-filter<span class="nt">&lt;/filter-name&gt;</span>
    <span class="nt">&lt;filter-class&gt;</span>a.b.c.MyFilter<span class="nt">&lt;/filter-class&gt;</span>

    <span class="nt">&lt;init-param&gt;</span>
      <span class="nt">&lt;param-name&gt;</span>my-param-key<span class="nt">&lt;/param-name&gt;</span>
      <span class="nt">&lt;param-value&gt;</span>my-param-val<span class="nt">&lt;/param-value&gt;</span>
    <span class="nt">&lt;/init-param&gt;</span>
  <span class="nt">&lt;/filter&gt;</span>

  <span class="nt">&lt;filter-mapping&gt;</span>
    <span class="nt">&lt;filter-name&gt;</span>my-filter<span class="nt">&lt;/filter-name&gt;</span>
    <span class="nt">&lt;servlet-name&gt;</span>my-servlet<span class="nt">&lt;/servlet-name&gt;</span>
  <span class="nt">&lt;/filter-mapping&gt;</span>

  <span class="nt">&lt;security-constraint&gt;</span>

    <span class="nt">&lt;web-resource-collection&gt;</span>
      <span class="nt">&lt;web-resource-name&gt;</span>my-web-res-name<span class="nt">&lt;/web-resource-name&gt;</span>
      <span class="nt">&lt;url-pattern&gt;</span>/*<span class="nt">&lt;/url-pattern&gt;</span>
    <span class="nt">&lt;/web-resource-collection&gt;</span>

    <span class="nt">&lt;auth-constraint&gt;</span>
       <span class="nt">&lt;role-name&gt;</span>my-role<span class="nt">&lt;/role-name&gt;</span>
    <span class="nt">&lt;/auth-constraint&gt;</span>

  <span class="nt">&lt;/security-constraint&gt;</span>

  <span class="nt">&lt;login-config&gt;</span>
    <span class="nt">&lt;auth-method&gt;</span>DIGEST<span class="nt">&lt;/auth-method&gt;</span>
    <span class="nt">&lt;realm-name&gt;</span>my-name<span class="nt">&lt;/realm-name&gt;</span>
  <span class="nt">&lt;/login-config&gt;</span>

  <span class="nt">&lt;security-role&gt;</span>
    <span class="nt">&lt;description&gt;</span>
    <span class="nt">&lt;/description&gt;</span>
    <span class="nt">&lt;role-name&gt;</span>my-role<span class="nt">&lt;/role-name&gt;</span>
  <span class="nt">&lt;/security-role&gt;</span>

  <span class="nt">&lt;error-page&gt;</span>
    <span class="nt">&lt;error-code&gt;</span>404<span class="nt">&lt;/error-code&gt;</span>
    <span class="nt">&lt;location&gt;</span>/WEB-INF/jsp/404.jsp<span class="nt">&lt;/location&gt;</span>
  <span class="nt">&lt;/error-page&gt;</span>

  <span class="nt">&lt;resource-ref&gt;</span>
    <span class="nt">&lt;description&gt;</span>Employees Database for HR Applications<span class="nt">&lt;/description&gt;</span>
    <span class="nt">&lt;res-ref-name&gt;</span>jdbc/EmployeeDB<span class="nt">&lt;/res-ref-name&gt;</span>
    <span class="nt">&lt;res-ref-type&gt;</span>javax.sql.DataSource<span class="nt">&lt;/res-ref-type&gt;</span>
    <span class="nt">&lt;res-auth&gt;</span>Container<span class="nt">&lt;/res-auth&gt;</span>
  <span class="nt">&lt;/resource-ref&gt;</span>

  <span class="nt">&lt;env-entry&gt;</span>
    <span class="nt">&lt;env-entry-name&gt;</span>maxExemptions<span class="nt">&lt;/env-entry-name&gt;</span>
    <span class="nt">&lt;env-entry-value&gt;</span>10<span class="nt">&lt;/env-entry-value&gt;</span>
    <span class="nt">&lt;env-entry-type&gt;</span>java.lang.Integer<span class="nt">&lt;/env-entry-type&gt;</span>
  <span class="nt">&lt;/env-entry&gt;</span>

  <span class="nt">&lt;context-param&gt;</span>
    <span class="nt">&lt;param-name&gt;</span>companyName<span class="nt">&lt;/param-name&gt;</span>
    <span class="nt">&lt;param-value&gt;</span>My Company, Incorporated<span class="nt">&lt;/param-value&gt;</span>
  <span class="nt">&lt;/context-param&gt;</span>

<span class="nt">&lt;/web-app&gt;</span>

</code></pre></div></div>

<h1 id="_2">HttpServlet</h1>

<h2 id="_3">上下文参数</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="o">&lt;</span><span class="n">context</span><span class="o">-</span><span class="n">param</span><span class="o">&gt;</span><span class="n">标签在整个webapp中共享</span><span class="o">,</span>
<span class="o">&lt;</span><span class="n">servlet</span><span class="o">&gt;&lt;</span><span class="n">init</span><span class="o">-</span><span class="n">param</span><span class="o">&gt;&lt;/</span><span class="n">servlet</span><span class="o">&gt;</span><span class="n">只能在当前servlet中使用</span><span class="o">,</span>

<span class="nl">使用方法是:</span>
<span class="nc">HttpServlet</span> <span class="n">httpServlet</span><span class="o">;</span>
<span class="n">httpServlet</span><span class="o">.</span><span class="na">getInitParameter</span><span class="o">(</span><span class="s">"key"</span><span class="o">);</span>

<span class="n">注意一个host可以配置多个webapp</span><span class="o">,</span><span class="nl">可以通过当前的Servlet获取同一个host下的其他webapp的context:</span>
<span class="nc">ServletContext</span> <span class="n">servletContext</span> <span class="o">=</span> <span class="n">httpServlet</span><span class="o">.</span><span class="na">getServletContext</span><span class="o">().</span><span class="na">getContext</span><span class="o">(</span><span class="s">"/foo"</span><span class="o">);</span>

<span class="n">实际上获取init</span><span class="o">-</span><span class="n">param等的是通过ServletConfig获取的</span><span class="o">,</span><span class="nl">过程如下:</span>
<span class="n">httpServlet</span><span class="o">.</span><span class="na">getServletConfig</span><span class="o">().</span><span class="na">getInitParameter</span><span class="o">(</span><span class="s">"key"</span><span class="o">);</span>
<span class="n">httpServlet</span><span class="o">.</span><span class="na">getServletConfig</span><span class="o">().</span><span class="na">getContext</span><span class="o">(</span><span class="s">"/foo"</span><span class="o">);</span>
</code></pre></div></div>

<h2 id="_4">生命周期</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nl">Servlet接口定义如下:</span>
<span class="kd">public</span> <span class="kd">interface</span> <span class="nc">Servlet</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">init</span><span class="o">(</span><span class="nc">ServletConfig</span> <span class="n">config</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">ServletException</span><span class="o">;</span>
    <span class="kd">public</span> <span class="nc">ServletConfig</span> <span class="nf">getServletConfig</span><span class="o">();</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">service</span><span class="o">(</span><span class="nc">ServletRequest</span> <span class="n">req</span><span class="o">,</span> <span class="nc">ServletResponse</span> <span class="n">res</span><span class="o">)</span>
            <span class="kd">throws</span> <span class="nc">ServletException</span><span class="o">,</span> <span class="nc">IOException</span><span class="o">;</span>
    <span class="kd">public</span> <span class="nc">String</span> <span class="nf">getServletInfo</span><span class="o">();</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">destroy</span><span class="o">();</span>
<span class="o">}</span>
<span class="n">servlet容器启动的时候</span><span class="o">,</span><span class="n">init被调用</span><span class="o">,</span><span class="n">同时传进来ServletConfig</span><span class="o">,</span><span class="n">然后销毁的时候调用destroy</span><span class="o">,</span>
<span class="n">每次有http消息进来的时候</span><span class="o">,</span><span class="n">会调用service</span><span class="o">.</span>

<span class="nl">HttpServlet是实现Servlet接口的抽象类:</span>
<span class="kd">public</span> <span class="kd">abstract</span> <span class="kd">class</span> <span class="nc">HttpServlet</span> <span class="kd">extends</span> <span class="nc">GenericServlet</span>
<span class="n">对service进行了基础封装</span><span class="o">,</span><span class="nl">增加了抽象方法:</span>
<span class="mi">1</span><span class="o">.</span> <span class="n">doGet</span><span class="o">(...)</span>
<span class="mi">2</span><span class="o">.</span> <span class="n">doPost</span><span class="o">(...)</span>
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
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/07/06/tomcat-classloader-and-sequence-diagram.html">Tomcat 类加载以及运行时序</a></div><div class="next"><span>下篇</span><a href="/2020/07/07/tomcat-deploy.html">Tomcat Deploy 部署</a></div></div></div>

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