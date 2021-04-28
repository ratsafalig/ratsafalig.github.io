---
title: Tomcat Cluster 集群
date: 2020-06-29 00:00:00 Z
tags:
- Java
- Tomcat
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Cluster 集群"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-06-29T08:00:00+08:00">
    <meta itemprop="keywords" content="Java,Tomcat"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Cluster 集群" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-29T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Cluster 集群" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-29T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Cluster 集群" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-29T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="_0">参考地址</h1>

<p><a href="https://tomcat.apache.org/connectors-doc/">参考地址—tomcat-doc-jk</a></p>

<p><a href="https://tomcat.apache.org/tomcat-9.0-doc/config/cluster.html">参考地址—tomcat-doc-cluster</a></p>

<p><a href="https://access.redhat.com/solutions/900933">参考地址—blog-sticky-session</a></p>

<p><a href="https://stackoverflow.com/questions/10494431/sticky-and-non-sticky-sessions">参考地址—stackoverflow-sticky-session</a></p>

<p><a href="http://tomcat.apache.org/tomcat-9.0-doc/proxy-howto.html">参考地址—tomcat-doc-proxy</a></p>

<h1 id="_0_1">标签结构</h1>

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

<pre><code class="language-mermaid">graph LR;
    id13(Cluster)
    id14(Manager)
    id15(Channel)
    id16(Valve)
    id17(Deployer)
    id18(ClusterListener)

    id13--&gt;id14
    id13--&gt;id15
    id13--&gt;id16
    id13--&gt;id17
    id13--&gt;id18

    id19(Membership)
    id20(Sender)
    id21(Transport)
    id22(Receiver)
    id23(Interceptor)

    id15--&gt;id19
    id15--&gt;id20
    id15--&gt;id22
    id15--&gt;id23
    id20--&gt;id21
</code></pre>

<pre><code class="language-mermaid">graph LR;

    id1(Cluster)
    id2(Manager)
    id3(Chennel)
    id4(Valve)
    id5(Deployer)
    id6(ClusterListener)
    id7(Membership)
    id8(Sender)
    id9(Receiver)
    id10(Interceptor)
    id11(Member)
    id12(LocalMember)

    id1--&gt;id2
    id1--&gt;id3
    id1--&gt;id4
    id1--&gt;id5
    id1--&gt;id6
    id1--&gt;id7
    id1--&gt;id8
    id1--&gt;id9
    id1--&gt;id10
    id7--&gt;id11
    id7--&gt;id12
</code></pre>

<h1 id="_0_2">标签</h1>

<h2 id="_1">Cluster</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nc">Cluster可能在Engine或者Host标签下</span><span class="o">,</span><span class="nl">Cluster拥有如下必选属性:</span>
<span class="mi">1</span><span class="o">.</span> <span class="n">className</span><span class="o">(</span><span class="n">只能填org</span><span class="o">.</span><span class="na">apache</span><span class="o">.</span><span class="na">catalina</span><span class="o">.</span><span class="na">ha</span><span class="o">.</span><span class="na">tcp</span><span class="o">.</span><span class="na">SimpleTcpCluster</span><span class="o">)</span>
<span class="mi">2</span><span class="o">.</span> <span class="n">channelSendOptions</span><span class="o">(</span>
    <span class="n">定义消息如何被发送</span>
    <span class="kt">int</span> <span class="n">options</span> <span class="o">=</span> <span class="nc">Channel</span><span class="o">.</span><span class="na">SEND_OPTIONS_ASYNCHRONOUS</span> <span class="o">|</span>
    <span class="nc">Channel</span><span class="o">.</span><span class="na">SEND_OPTIONS_SYNCHRONIZED_ACK</span> <span class="o">|</span>
    <span class="nc">Channel</span><span class="o">.</span><span class="na">SEND_OPTIONS_USE_ACK</span><span class="o">;)</span>
</code></pre></div></div>

<h2 id="_2">Manager</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nl">内置了两种Manager使用:</span>
<span class="mi">1</span><span class="o">.</span> <span class="n">org</span><span class="o">.</span><span class="na">apache</span><span class="o">.</span><span class="na">catalina</span><span class="o">.</span><span class="na">ha</span><span class="o">.</span><span class="na">session</span><span class="o">.</span><span class="na">DeltaManager</span> <span class="o">(</span><span class="n">复制session到所有备份服务器</span><span class="o">,</span><span class="n">即使它并没有跑当前应用</span><span class="o">,</span><span class="n">one</span><span class="o">-</span><span class="n">to</span><span class="o">-</span><span class="n">all</span><span class="o">)</span>
<span class="mi">2</span><span class="o">.</span> <span class="n">org</span><span class="o">.</span><span class="na">apache</span><span class="o">.</span><span class="na">catalina</span><span class="o">.</span><span class="na">ha</span><span class="o">.</span><span class="na">session</span><span class="o">.</span><span class="na">BackupManager</span> <span class="o">(</span><span class="n">挑选一个跑当前应用的备份服务器备份</span><span class="o">,</span><span class="n">one</span><span class="o">-</span><span class="n">to</span><span class="o">-</span><span class="n">one</span><span class="o">)</span>

<span class="nl">拥有如下必选配置:</span>

<span class="mi">1</span><span class="o">.</span> <span class="n">className</span>
<span class="mi">2</span><span class="o">.</span> <span class="n">name</span><span class="o">(</span><span class="n">用来区分一个集群node上的一个Manager</span><span class="o">,</span><span class="n">注意这个值可能被服务器修改</span><span class="o">)</span>
</code></pre></div></div>

<h2 id="_3">Channel</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nc">Channel抽象了一个管道</span><span class="o">,</span><span class="n">和别的节点通信的通道</span><span class="o">.</span>
<span class="nl">有如下必选属性:</span>

<span class="mi">1</span><span class="o">.</span> <span class="n">className</span><span class="o">(</span><span class="n">默认org</span><span class="o">.</span><span class="na">apache</span><span class="o">.</span><span class="na">catalina</span><span class="o">.</span><span class="na">tribes</span><span class="o">.</span><span class="na">group</span><span class="o">.</span><span class="na">GroupChannel</span><span class="o">)</span>
</code></pre></div></div>

<h2 id="_4">Membership</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">定义一个成员组</span><span class="o">,</span><span class="nl">必选属性有:</span>
<span class="mi">1</span><span class="o">.</span> <span class="n">className</span><span class="o">(</span>
    <span class="nl">可选:</span>
    <span class="mi">1</span><span class="o">.</span> <span class="n">org</span><span class="o">.</span><span class="na">apache</span><span class="o">.</span><span class="na">catalina</span><span class="o">.</span><span class="na">tribes</span><span class="o">.</span><span class="na">membership</span><span class="o">.</span><span class="na">McastService</span><span class="o">(</span><span class="n">广播方式发送消息</span><span class="o">)</span>
    <span class="mi">2</span><span class="o">.</span> <span class="n">org</span><span class="o">.</span><span class="na">apache</span><span class="o">.</span><span class="na">catalina</span><span class="o">.</span><span class="na">tribes</span><span class="o">.</span><span class="na">membership</span><span class="o">.</span><span class="na">StaticMembershipService</span><span class="o">(</span><span class="n">静态定义成员</span><span class="o">))</span>

</code></pre></div></div>

<h2 id="_5">LocalMember Member</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">如果采用了static</span> <span class="n">membership</span> <span class="n">service</span><span class="o">,</span><span class="n">那么还需要定义member或者local</span> <span class="n">member</span>
<span class="n">local</span> <span class="nl">member的必选属性有:</span>

<span class="mi">1</span><span class="o">.</span> <span class="n">className</span>
<span class="mi">2</span><span class="o">.</span> <span class="n">uniqueId</span>

<span class="nl">member的必选属性有:</span>

<span class="mi">1</span><span class="o">.</span> <span class="n">className</span>
<span class="mi">2</span><span class="o">.</span> <span class="n">port</span>
<span class="mi">3</span><span class="o">.</span> <span class="n">host</span>
<span class="mi">4</span><span class="o">.</span> <span class="n">uniqueId</span>
</code></pre></div></div>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code>示例配置:
<span class="nt">&lt;Membership</span> <span class="na">className=</span><span class="s">"org.apache.catalina.tribes.membership.StaticMembershipService"</span><span class="nt">&gt;</span>
<span class="nt">&lt;LocalMember</span> <span class="na">className=</span><span class="s">"org.apache.catalina.tribes.membership.StaticMember"</span>
            <span class="na">uniqueId=</span><span class="s">"{0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15}"</span><span class="nt">/&gt;</span>
<span class="nt">&lt;Member</span> <span class="na">className=</span><span class="s">"org.apache.catalina.tribes.membership.StaticMember"</span>
            <span class="na">port=</span><span class="s">"4004"</span>
            <span class="na">host=</span><span class="s">"tomcat02.mydomain.com"</span>
            <span class="na">uniqueId=</span><span class="s">"{1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,1}"</span><span class="nt">/&gt;</span>
<span class="nt">&lt;/Membership&gt;</span>
<span class="c">&lt;!--................................................................................--&gt;</span>
<span class="nt">&lt;Membership</span> <span class="na">className=</span><span class="s">"org.apache.catalina.tribes.membership.StaticMembershipService"</span><span class="nt">&gt;</span>
<span class="nt">&lt;Member</span> <span class="na">className=</span><span class="s">"org.apache.catalina.tribes.membership.StaticMember"</span>
            <span class="na">port=</span><span class="s">"4004"</span>
            <span class="na">host=</span><span class="s">"tomcat01.mydomain.com"</span>
            <span class="na">uniqueId=</span><span class="s">"{0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15}"</span><span class="nt">/&gt;</span>
<span class="nt">&lt;Member</span> <span class="na">className=</span><span class="s">"org.apache.catalina.tribes.membership.StaticMember"</span>
            <span class="na">port=</span><span class="s">"4004"</span>
            <span class="na">host=</span><span class="s">"tomcat02.mydomain.com"</span>
            <span class="na">uniqueId=</span><span class="s">"{1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,1}"</span><span class="nt">/&gt;</span>
<span class="nt">&lt;/Membership&gt;</span>
</code></pre></div></div>

<h2 id="_6">Sender</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nc">Sender抽象了一个发送器</span><span class="o">,</span><span class="nl">必选属性有:</span>
<span class="mi">1</span><span class="o">.</span> <span class="n">className</span><span class="o">(</span><span class="n">只支持org</span><span class="o">.</span><span class="na">apache</span><span class="o">.</span><span class="na">catalina</span><span class="o">.</span><span class="na">tribes</span><span class="o">.</span><span class="na">transport</span><span class="o">.</span><span class="na">ReplicationTransmitter</span><span class="o">)</span>
</code></pre></div></div>

<h2 id="_6_1">Transport</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">配置传输层参数</span><span class="o">,</span><span class="nl">必选属性有:</span>
<span class="mi">1</span><span class="o">.</span> <span class="n">className</span><span class="o">(</span>
    <span class="nl">内置:</span>
    <span class="mi">1</span><span class="o">.</span> <span class="n">org</span><span class="o">.</span><span class="na">apache</span><span class="o">.</span><span class="na">catalina</span><span class="o">.</span><span class="na">tribes</span><span class="o">.</span><span class="na">transport</span><span class="o">.</span><span class="na">nio</span><span class="o">.</span><span class="na">PooledParallelSender</span><span class="o">(</span><span class="n">非阻塞</span><span class="o">)</span>
    <span class="mi">2</span><span class="o">.</span> <span class="n">org</span><span class="o">.</span><span class="na">apache</span><span class="o">.</span><span class="na">catalina</span><span class="o">.</span><span class="na">tribes</span><span class="o">.</span><span class="na">transport</span><span class="o">.</span><span class="na">bio</span><span class="o">.</span><span class="na">PooledMultiSender</span><span class="o">(</span><span class="n">阻塞</span><span class="o">))</span>

</code></pre></div></div>

<h2 id="_7">Receiver</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">接收器</span><span class="o">,</span><span class="nl">必选属性:</span>
<span class="mi">1</span><span class="o">.</span> <span class="n">className</span><span class="o">(</span>
    <span class="nl">支持两种实现:</span>
    <span class="mi">1</span><span class="o">.</span> <span class="n">org</span><span class="o">.</span><span class="na">apache</span><span class="o">.</span><span class="na">catalina</span><span class="o">.</span><span class="na">tribes</span><span class="o">.</span><span class="na">transport</span><span class="o">.</span><span class="na">nio</span><span class="o">.</span><span class="na">NioReceiver</span><span class="o">(</span><span class="n">非阻塞</span><span class="o">)</span>
    <span class="mi">2</span><span class="o">.</span> <span class="n">org</span><span class="o">.</span><span class="na">apache</span><span class="o">.</span><span class="na">catalina</span><span class="o">.</span><span class="na">tribes</span><span class="o">.</span><span class="na">transport</span><span class="o">.</span><span class="na">bio</span><span class="o">.</span><span class="na">BioReceiver</span><span class="o">(</span><span class="n">阻塞</span><span class="o">))</span>
</code></pre></div></div>

<h2 id="_8">Interceptor</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>拦截器,拦截发送和收到消息,必选属性有:
1. className
</code></pre></div></div>

<h1 id="_9">部署</h1>

<h2 id="_10">要求</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="mi">1</span><span class="o">.</span> <span class="o">*</span> <span class="n">session</span><span class="o">-</span><span class="n">attribute必须实现java</span><span class="o">.</span><span class="na">io</span><span class="o">.</span><span class="na">Serializable</span><span class="o">(</span>
    <span class="nc">HttpSession</span><span class="o">.</span><span class="na">setAttribute</span><span class="o">(</span><span class="nc">String</span><span class="o">,</span><span class="nc">Object</span><span class="o">)</span><span class="n">的Object</span><span class="o">))</span>
<span class="mi">2</span><span class="o">.</span> <span class="o">*</span> <span class="n">server</span><span class="o">.</span><span class="na">xml必须有</span><span class="o">&lt;</span><span class="nc">Cluster</span><span class="o">&gt;</span>
<span class="mi">3</span><span class="o">.</span> <span class="o">*</span> <span class="n">如果自定义了</span><span class="o">&lt;</span><span class="nc">Valve</span><span class="o">&gt;,</span><span class="n">请保证至少存在</span><span class="o">&lt;</span><span class="nc">ReplicationValve</span><span class="o">&gt;</span>
<span class="mi">4</span><span class="o">.</span> <span class="o">*</span> <span class="n">如果多个tomcat跑在同一台机器</span><span class="o">,</span><span class="n">确保Receiver</span><span class="o">.</span><span class="na">port不同</span>
<span class="mi">5</span><span class="o">.</span> <span class="o">*</span> <span class="n">web</span><span class="o">.</span><span class="na">xml里一定要有</span><span class="o">&lt;</span><span class="n">distributable</span><span class="o">/&gt;</span>
<span class="mi">6</span><span class="o">.</span> <span class="o">*</span> <span class="o">&lt;</span><span class="nc">Engine</span> <span class="n">name</span><span class="o">=</span><span class="s">"Catalina"</span> <span class="n">jvmRoute</span><span class="o">=</span><span class="s">"xxx"</span><span class="o">&gt;,</span><span class="n">其中xxx对应workers</span><span class="o">.</span><span class="na">properties的id</span>
<span class="mi">7</span><span class="o">.</span> <span class="o">*</span> <span class="n">所有的节点要和NTP同步</span>
<span class="mi">8</span><span class="o">.</span> <span class="o">*</span> <span class="n">loadbalancer配置成sticky</span><span class="o">-</span><span class="n">session模式</span>
</code></pre></div></div>

<h2 id="_10_1">sticky-session</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">尽管所有的session都会被集群化</span><span class="o">,</span><span class="n">但是难免有的情况下会出现一些错误</span><span class="o">,</span><span class="n">所以引出sticky</span><span class="o">-</span><span class="nl">session的概念:</span>
<span class="n">在session生命周期内</span><span class="o">,</span><span class="n">所有交互都会被负载均衡到同一个tomcat</span><span class="o">.</span>
<span class="n">session通过在request里加一个id</span><span class="o">(</span><span class="n">worker的id</span><span class="o">),</span><span class="n">来告诉负载均衡到底是哪台tomcat负责这个session</span><span class="o">,</span><span class="n">但是如果这台worker正好坏了</span>
<span class="n">这下重新的请求就会因为找不到worker而被负载均衡到随机的节点</span><span class="o">,</span><span class="n">为了解决这个办法</span><span class="o">.</span><span class="na">引入了JvmRouteBinderValve</span>
<span class="n">这个valve重写了id到当前tomcat的id</span><span class="o">,</span><span class="n">这样再下一次请求又会一直指向当前服务器</span><span class="o">.</span>
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">简单说</span><span class="o">,</span><span class="nl">就是如下逻辑:</span>
<span class="mi">1</span><span class="o">.</span> <span class="nc">TomcatA</span> <span class="n">starts</span> <span class="n">up</span>
<span class="mi">2</span><span class="o">.</span> <span class="nc">TomcatB</span> <span class="n">starts</span> <span class="nf">up</span> <span class="o">(</span><span class="nc">Wait</span> <span class="n">the</span> <span class="nc">TomcatA</span> <span class="n">start</span> <span class="n">is</span> <span class="n">complete</span><span class="o">)</span>
<span class="mi">3</span><span class="o">.</span> <span class="nc">TomcatA</span> <span class="n">receives</span> <span class="n">a</span> <span class="n">request</span><span class="o">,</span> <span class="n">a</span> <span class="n">session</span> <span class="no">S1</span> <span class="n">is</span> <span class="n">created</span><span class="o">.</span>
<span class="mi">4</span><span class="o">.</span> <span class="nc">TomcatA</span> <span class="n">crashes</span>
<span class="mi">5</span><span class="o">.</span> <span class="nc">TomcatB</span> <span class="n">receives</span> <span class="n">a</span> <span class="n">request</span> <span class="k">for</span> <span class="n">session</span> <span class="no">S1</span>
<span class="mi">6</span><span class="o">.</span> <span class="nc">TomcatA</span> <span class="n">starts</span> <span class="n">up</span>
<span class="mi">7</span><span class="o">.</span> <span class="nc">TomcatA</span> <span class="n">receives</span> <span class="n">a</span> <span class="n">request</span><span class="o">,</span> <span class="n">invalidate</span> <span class="n">is</span> <span class="n">called</span> <span class="n">on</span> <span class="n">the</span> <span class="nf">session</span> <span class="o">(</span><span class="no">S1</span><span class="o">)</span>
<span class="mi">8</span><span class="o">.</span> <span class="nc">TomcatB</span> <span class="n">receives</span> <span class="n">a</span> <span class="n">request</span><span class="o">,</span> <span class="k">for</span> <span class="n">a</span> <span class="k">new</span> <span class="nf">session</span> <span class="o">(</span><span class="no">S2</span><span class="o">)</span>
<span class="mi">9</span><span class="o">.</span> <span class="nc">TomcatA</span> <span class="nc">The</span> <span class="n">session</span> <span class="no">S2</span> <span class="n">expires</span> <span class="n">due</span> <span class="n">to</span> <span class="n">inactivity</span><span class="o">.</span>
</code></pre></div></div>

<h2 id="_11">代理</h2>

<h3 id="_12">mod_proxy</h3>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>过程如下
1. LoadModule proxy_module  {path-to-modules}/mod_proxy.so
2. ProxyPass         /myapp  http://localhost:8081/myapp (正向代理配置)
3. ProxyPassReverse  /myapp  http://localhost:8081/myapp (反向代理配置,改写重定向的服务器)

4. &lt;Connector port="8081" ...
              proxyName="www.mycompany.com"
              proxyPort="80"/&gt;
</code></pre></div></div>

<h3 id="_13">mod_jk</h3>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>Connector的AJP协议允许服务器之间进行通信,于时可以可以通过如下方式配置集群:
1. apache-http当作表面的服务器
2. 一大堆tomcat当作真实服务器

为了让apache-http支持ajp,需要安装模块mod_jk(多个服务器都支持ajp拓展,iis的 ISAPI redirector等等)

mod_jk安装之后,要进行配置,主要通过两个文件夹(实际上只要一个也行):
1. workers.properties
2. uriworkermap.properties
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>workers.properties:
1. worker.list=a,b,c
2. worker.&lt;worker name&gt;.&lt;directive&gt;=&lt;value&gt;
3. worker.a.type=ajp13
   worker.b.type=lb
   worker.c.type=status
4. worker.b.balance_workers=a
5. worker.a.host=
   worker.a.port
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
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/06/29/js-ts.html">TypeScript 入门</a></div><div class="next"><span>下篇</span><a href="/2020/06/29/tomcat-realm-valve.html">Tomcat Realm Valve</a></div></div></div>

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