---
title: Tomcat Realm Valve
date: 2020-06-29 00:00:00 Z
tags:
- Java
- Tomcat
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Realm Valve"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-06-29T08:00:00+08:00">
    <meta itemprop="keywords" content="Java,Tomcat"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Realm Valve" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-29T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Realm Valve" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-29T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Realm Valve" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-29T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="_0">参考地址</h1>

<p><a href="https://tomcat.apache.org/tomcat-9.0-doc/realm-howto.html">参考地址—tomcat-doc-realm-howto</a></p>

<p><a href="https://tomcat.apache.org/tomcat-9.0-doc/config/realm.html">参考地址—tomcat-doc-realm</a></p>

<p><a href="https://tomcat.apache.org/tomcat-9.0-doc/manager-howto.html">参考地址—tomcat-doc-manager-howto</a></p>

<p><a href="">参考地址—tomcat-doc-valve</a></p>

<h1 id="_0_1">Tomcat标签结构</h1>

<pre><code class="language-mermaid">graph LR;
    id1(Server)
    id2(Service)
    id3(Engine)
    id4(Host)
    id5(Context)

    id6(CookieProcesser)
    id7(Loader)
    id8(Manager)
    id9(Realm)
    id10(Resources)
    id11(WatchedResources)
    id12(JarScanner)

    id13(GlobalNamingResources)
    id14(Connector)
    id15(Executor)
    
    id16(JarScanFilter)

    id1--&gt;id13
    id2--&gt;id14
    id2--&gt;id15
    id5--&gt;id16

    id1--&gt;id2
    id2--&gt;id3
    id3--&gt;id4
    id3--&gt;t_id1(Realm)
    id3--&gt;t_id3(Cluster)
    id3--&gt;t_id5(Valve)
    id4--&gt;id5
    id4--&gt;t_id2(Realm)
    id4--&gt;t_id4(Cluster)
    id4--&gt;t_id6(Valve)
    id5--&gt;id6
    id5--&gt;id7
    id5--&gt;id8
    id5--&gt;id9
    id5--&gt;id10
    id5--&gt;id11
    id5--&gt;id12
    id5--&gt;t_id7(Valve)

    id1--&gt;t_id8(Listener)
    id3--&gt;t_id9(Listener)
    id4--&gt;t_id10(Listener)
    id5--&gt;t_id11(Listener)
</code></pre>

<h1 id="_1">Realm</h1>

<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code>如果一个用户登陆:
http://localhost/123/
而我们需要对登陆/123/的url的用户进行过滤(只有输入了密码的用户才能进入,就需要用到realm)

可以在web.xml里声明一个角色,和角色的作用域:

<span class="nt">&lt;security-constraint&gt;</span>
<span class="nt">&lt;web-resource-collection&gt;</span>
    <span class="nt">&lt;web-resource-name&gt;</span>xxx<span class="nt">&lt;/web-resource-name&gt;</span>
    <span class="nt">&lt;url-pattern&gt;</span>/123<span class="nt">&lt;/url-pattern&gt;</span>
<span class="nt">&lt;/web-resource-collection&gt;</span>
<span class="nt">&lt;auth-constraint&gt;</span>
    <span class="nt">&lt;role-name&gt;</span>manager-123<span class="nt">&lt;/role-name&gt;</span>
<span class="nt">&lt;/auth-constraint&gt;</span>
<span class="nt">&lt;/security-constraint&gt;</span>

<span class="c">&lt;!--........................................--&gt;</span>

<span class="nt">&lt;security-role&gt;</span>
<span class="nt">&lt;description&gt;</span>
    xxx
<span class="nt">&lt;/description&gt;</span>
<span class="nt">&lt;role-name&gt;</span>manager-123<span class="nt">&lt;/role-name&gt;</span>
<span class="nt">&lt;/security-role&gt;</span>

以上配置声明了一个manager-123的角色名(role-name)和manager123的作用域(url-pattern)

接下来可以通过web.xml里的login-config定义验证方式:

<span class="nt">&lt;login-config&gt;</span>
<span class="nt">&lt;auth-method&gt;</span>DIGEST<span class="nt">&lt;/auth-method&gt;</span>
<span class="nt">&lt;realm-name&gt;</span>aaa<span class="nt">&lt;/realm-name&gt;</span>
<span class="nt">&lt;/login-config&gt;</span>

这个DIGEST代表不是明文比对,而是比对hash之后的码.
real-name则是自定义的,用来输入hash函数的东西

用户的信息是通过server.xml的<span class="nt">&lt;Realm&gt;</span>标签定义(Engine,Host,Context,Realm下都有可能存在Realm标签
    其中Engine,Host,Context都只能有一个Realm,并且有如下规则:
    1. 下层的标签自动继承上层的Realm,例如Context自动继承Engine的Realm,除非它自己定义一个
    2. 如果<span class="nt">&lt;Realm&gt;</span>包含多个子<span class="nt">&lt;Realm&gt;</span>,那么取第一个成功匹配的realm):

如果采用的Realm是UserDatabaseRealm,则自动查找$CATALINA_BASE/conf/tomcat-users.xml里的定义信息,查看对应的:

<span class="nt">&lt;user</span> <span class="na">username=</span><span class="s">""</span> <span class="na">password=</span><span class="s">""</span> <span class="na">roles=</span><span class="s">""</span><span class="nt">/&gt;</span>

查看对应的username,password是否匹配,如果匹配,检查roles是否符合要进入的url是否满足
</code></pre></div></div>

<h1 id="_2">Valve</h1>

<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code>Valve如名字所示,是一个阀门,过滤一些东西
比如采用了Remote Address Valve(<span class="nt">&lt;Valuve</span> <span class="err">的classname</span><span class="nt">&gt;</span>),就可以如下配置:
    
<span class="nt">&lt;Context&gt;</span>
  ...
  <span class="nt">&lt;Valve</span> <span class="na">className=</span><span class="s">"org.apache.catalina.valves.RemoteAddrValve"</span>
         <span class="na">addConnectorPort=</span><span class="s">"true"</span>
         <span class="na">invalidAuthenticationWhenDeny=</span><span class="s">"true"</span>
         <span class="na">allow=</span><span class="s">".*;8009"</span><span class="nt">/&gt;</span>
  <span class="nt">&lt;Valve</span> <span class="na">className=</span><span class="s">"org.apache.catalina.authenticator.BasicAuthenticator"</span> <span class="nt">/&gt;</span>
  ...
<span class="nt">&lt;/Context&gt;</span>
</code></pre></div></div>

</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-06-29T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/06/29/tomcat-cluster.html">Tomcat Cluster 集群</a></div><div class="next"><span>下篇</span><a href="/2020/07/01/cpp-virtual-table.html">C++ 虚表</a></div></div></div>

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