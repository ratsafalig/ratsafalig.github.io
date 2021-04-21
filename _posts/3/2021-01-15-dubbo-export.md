---
title: Dubbo Export
date: 2021-01-15 00:00:00 Z
tags:
- Dubbo
- Java
- Apache
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Dubbo Export"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2021-01-15T08:00:00+08:00">
    <meta itemprop="keywords" content="Dubbo,Java,Apache"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Dubbo Export" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-01-15T08:00:00+08:00" />
    <meta itemprop="keywords" content="Dubbo,Java,Apache" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="实例">实例</h1>

<h2 id="api">API</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.config.ApplicationConfig</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.config.RegistryConfig</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.config.ProviderConfig</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.config.ServiceConfig</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">com.xxx.XxxService</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">com.xxx.XxxServiceImpl</span><span class="o">;</span>
 
<span class="c1">// 服务实现</span>
<span class="nc">XxxService</span> <span class="n">xxxService</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">XxxServiceImpl</span><span class="o">();</span>
 
<span class="c1">// 当前应用配置</span>
<span class="nc">ApplicationConfig</span> <span class="n">application</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ApplicationConfig</span><span class="o">();</span>
<span class="n">application</span><span class="o">.</span><span class="na">setName</span><span class="o">(</span><span class="s">"xxx"</span><span class="o">);</span>
 
<span class="c1">// 连接注册中心配置</span>
<span class="nc">RegistryConfig</span> <span class="n">registry</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">RegistryConfig</span><span class="o">();</span>
<span class="n">registry</span><span class="o">.</span><span class="na">setAddress</span><span class="o">(</span><span class="s">"10.20.130.230:9090"</span><span class="o">);</span>
<span class="n">registry</span><span class="o">.</span><span class="na">setUsername</span><span class="o">(</span><span class="s">"aaa"</span><span class="o">);</span>
<span class="n">registry</span><span class="o">.</span><span class="na">setPassword</span><span class="o">(</span><span class="s">"bbb"</span><span class="o">);</span>
 
<span class="c1">// 服务提供者协议配置</span>
<span class="nc">ProtocolConfig</span> <span class="n">protocol</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ProtocolConfig</span><span class="o">();</span>
<span class="n">protocol</span><span class="o">.</span><span class="na">setName</span><span class="o">(</span><span class="s">"dubbo"</span><span class="o">);</span>
<span class="n">protocol</span><span class="o">.</span><span class="na">setPort</span><span class="o">(</span><span class="mi">12345</span><span class="o">);</span>
<span class="n">protocol</span><span class="o">.</span><span class="na">setThreads</span><span class="o">(</span><span class="mi">200</span><span class="o">);</span>
 
<span class="c1">// 注意：ServiceConfig为重对象，内部封装了与注册中心的连接，以及开启服务端口</span>
 
<span class="c1">// 服务提供者暴露服务配置</span>
<span class="nc">ServiceConfig</span><span class="o">&lt;</span><span class="nc">XxxService</span><span class="o">&gt;</span> <span class="n">service</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ServiceConfig</span><span class="o">&lt;</span><span class="nc">XxxService</span><span class="o">&gt;();</span> <span class="c1">// 此实例很重，封装了与注册中心的连接，请自行缓存，否则可能造成内存和连接泄漏</span>
<span class="n">service</span><span class="o">.</span><span class="na">setApplication</span><span class="o">(</span><span class="n">application</span><span class="o">);</span>
<span class="n">service</span><span class="o">.</span><span class="na">setRegistry</span><span class="o">(</span><span class="n">registry</span><span class="o">);</span> <span class="c1">// 多个注册中心可以用setRegistries()</span>
<span class="n">service</span><span class="o">.</span><span class="na">setProtocol</span><span class="o">(</span><span class="n">protocol</span><span class="o">);</span> <span class="c1">// 多个协议可以用setProtocols()</span>
<span class="n">service</span><span class="o">.</span><span class="na">setInterface</span><span class="o">(</span><span class="nc">XxxService</span><span class="o">.</span><span class="na">class</span><span class="o">);</span>
<span class="n">service</span><span class="o">.</span><span class="na">setRef</span><span class="o">(</span><span class="n">xxxService</span><span class="o">);</span>
<span class="n">service</span><span class="o">.</span><span class="na">setVersion</span><span class="o">(</span><span class="s">"1.0.0"</span><span class="o">);</span>
 
<span class="c1">// 暴露及注册服务</span>
<span class="n">service</span><span class="o">.</span><span class="na">export</span><span class="o">();</span>
</code></pre></div></div>

<p>类图关系:</p>

<pre><code class="language-mermaid">classDiagram

ServiceConfig --&gt; ApplicationConfig
ServiceConfig --&gt; RegistryConfig
ServiceConfig --&gt; ProtocolConfig

ApplicationConfig : name

RegistryConfig : address
RegistryConfig : username
RegistryConfig : password

ProtocolConfig : name
ProtocolConfig : port
ProtocolConfig : threads

ServiceConfig : ref
ServiceConfig : version
ServiceConfig : interface

</code></pre>

<h1 id="导出细节">导出细节</h1>

<h2 id="serviceconfigexport">ServiceConfig.export()</h2>

<pre><code class="language-mermaid">graph TD
id1("export()")
id2("doExport()")
    id2_1("doExportUrls()")
        id2_1_1("doExportUrlsFor1Protocol()")
id3("exported()")

id1     --&gt; id2
id2     --&gt; id2_1
id2_1   --&gt; id2_1_1
id2_1_1 --&gt; id3
</code></pre>

<h2 id="serviceconfigdoexport">ServiceConfig.doExport()</h2>

<h2 id="serviceconfigdoexporturls">ServiceConfig.doExportUrls()</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">private</span> <span class="kt">void</span> <span class="nf">doExportUrls</span><span class="o">()</span> <span class="o">{</span>
        <span class="nc">ServiceRepository</span> <span class="n">repository</span> <span class="o">=</span> <span class="nc">ApplicationModel</span><span class="o">.</span><span class="na">getServiceRepository</span><span class="o">();</span>
        <span class="nc">ServiceDescriptor</span> <span class="n">serviceDescriptor</span> <span class="o">=</span> <span class="n">repository</span><span class="o">.</span><span class="na">registerService</span><span class="o">(</span><span class="n">getInterfaceClass</span><span class="o">());</span>
        <span class="n">repository</span><span class="o">.</span><span class="na">registerProvider</span><span class="o">(</span>
                <span class="n">getUniqueServiceName</span><span class="o">(),</span>
                <span class="n">ref</span><span class="o">,</span>
                <span class="n">serviceDescriptor</span><span class="o">,</span>
                <span class="k">this</span><span class="o">,</span>
                <span class="n">serviceMetadata</span>
        <span class="o">);</span>

        <span class="nc">List</span><span class="o">&lt;</span><span class="no">URL</span><span class="o">&gt;</span> <span class="n">registryURLs</span> <span class="o">=</span> <span class="nc">ConfigValidationUtils</span><span class="o">.</span><span class="na">loadRegistries</span><span class="o">(</span><span class="k">this</span><span class="o">,</span> <span class="kc">true</span><span class="o">);</span>

        <span class="k">for</span> <span class="o">(</span><span class="nc">ProtocolConfig</span> <span class="n">protocolConfig</span> <span class="o">:</span> <span class="n">protocols</span><span class="o">)</span> <span class="o">{</span>
            <span class="nc">String</span> <span class="n">pathKey</span> <span class="o">=</span> <span class="no">URL</span><span class="o">.</span><span class="na">buildKey</span><span class="o">(</span><span class="n">getContextPath</span><span class="o">(</span><span class="n">protocolConfig</span><span class="o">)</span>
                    <span class="o">.</span><span class="na">map</span><span class="o">(</span><span class="n">p</span> <span class="o">-&gt;</span> <span class="n">p</span> <span class="o">+</span> <span class="s">"/"</span> <span class="o">+</span> <span class="n">path</span><span class="o">)</span>
                    <span class="o">.</span><span class="na">orElse</span><span class="o">(</span><span class="n">path</span><span class="o">),</span> <span class="n">group</span><span class="o">,</span> <span class="n">version</span><span class="o">);</span>
            <span class="c1">// In case user specified path, register service one more time to map it to path.</span>
            <span class="n">repository</span><span class="o">.</span><span class="na">registerService</span><span class="o">(</span><span class="n">pathKey</span><span class="o">,</span> <span class="n">interfaceClass</span><span class="o">);</span>
            <span class="c1">// TODO, uncomment this line once service key is unified</span>
            <span class="n">serviceMetadata</span><span class="o">.</span><span class="na">setServiceKey</span><span class="o">(</span><span class="n">pathKey</span><span class="o">);</span>
            <span class="n">doExportUrlsFor1Protocol</span><span class="o">(</span><span class="n">protocolConfig</span><span class="o">,</span> <span class="n">registryURLs</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>
</code></pre></div></div>

<p>以上的代码可以看出<code class="language-plaintext highlighter-rouge">ServiceRepository</code>,<code class="language-plaintext highlighter-rouge">ServiceDescriptor</code>之间的类关系</p>

<pre><code class="language-mermaid">classDiagram
ServiceRepository --&gt; ServiceDescriptor
class ServiceRepository{
    ConcurrentMap&lt;String, ProviderModel&gt; providers
    ConcurrentMap&lt;String, ServiceDescriptor&gt; services

    registerProvider(...)
    registerService(...)
}
</code></pre>

<p>缕一缕<code class="language-plaintext highlighter-rouge">doExportUrls()</code>的流程:</p>

<pre><code class="language-mermaid">graph TD
id1("通过ApplicationModel.getServiceRepository()获取一个ServiceRepository")
id2("把providor信息注册到ServiceRepository")
id3("根据配置信息获取到所有的注册中心URL")
id4("如果用户指定了path项,重新注册一次到ServiceRepository")
id5("对每个配置的protocol,都用该协议向所有注册中心导出")

id1 --&gt; id2
id2 --&gt; id3
id3 --&gt; id4
id4 --&gt; id5
</code></pre>

<h2 id="doexporturlsfor1protocol">doExportUrlsFor1Protocol()</h2>

<p><code class="language-plaintext highlighter-rouge">doExportUrlsFor1Protocol()</code>是一个非常长的函数</p>

<blockquote>

  <p>分为两个部分</p>
  <ul>
    <li>配置map</li>
    <li>导出服务</li>
  </ul>
</blockquote>

<pre><code class="language-mermaid">graph TD
id1("使用AbstractConfig.appendParameters把相关参数装载在一个HashMap里")
    subgraph "使用AbstractConfig.appendParameters(Map&lt;String, String&gt; parameters, Object config)"
        id1_1("获取到所有config实例的getter方法")
        id1_2("获取到config实例对应getter的key和value")
        id1_3("把key,value键值对放入map")
        id1_1 --&gt; id1_2
        id1_2 --&gt; id1_3
    end

id2("导出服务")

id1   --&gt; id1_1
id1_3 --&gt; id2
</code></pre>

<h3 id="配置map">配置map</h3>

<p>在说到保存参数到<code class="language-plaintext highlighter-rouge">map</code>的过程之前,有必要解析以下<code class="language-plaintext highlighter-rouge">AbstractConfig.appendParameters(...)</code>这个函数的功能<br />
因为保存到<code class="language-plaintext highlighter-rouge">map</code>的过程大量涉及到这个函数的使用</p>

<h4 id="abstractconfigappendparameters">AbstractConfig.appendParameters(…)</h4>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code>    <span class="kd">public</span> <span class="kd">static</span> <span class="kt">void</span> <span class="nf">appendParameters</span><span class="o">(</span><span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">String</span><span class="o">&gt;</span> <span class="n">parameters</span><span class="o">,</span> <span class="nc">Object</span> <span class="n">config</span><span class="o">)</span> <span class="o">{</span>
        <span class="n">appendParameters</span><span class="o">(</span><span class="n">parameters</span><span class="o">,</span> <span class="n">config</span><span class="o">,</span> <span class="kc">null</span><span class="o">);</span>
    <span class="o">}</span>

    <span class="nd">@SuppressWarnings</span><span class="o">(</span><span class="s">"unchecked"</span><span class="o">)</span>
    <span class="kd">public</span> <span class="kd">static</span> <span class="kt">void</span> <span class="nf">appendParameters</span><span class="o">(</span><span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">String</span><span class="o">&gt;</span> <span class="n">parameters</span><span class="o">,</span> <span class="nc">Object</span> <span class="n">config</span><span class="o">,</span> <span class="nc">String</span> <span class="n">prefix</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">config</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
            <span class="k">return</span><span class="o">;</span>
        <span class="o">}</span>
        <span class="nc">Method</span><span class="o">[]</span> <span class="n">methods</span> <span class="o">=</span> <span class="n">config</span><span class="o">.</span><span class="na">getClass</span><span class="o">().</span><span class="na">getMethods</span><span class="o">();</span>
        <span class="k">for</span> <span class="o">(</span><span class="nc">Method</span> <span class="n">method</span> <span class="o">:</span> <span class="n">methods</span><span class="o">)</span> <span class="o">{</span>
            <span class="k">try</span> <span class="o">{</span>
                <span class="nc">String</span> <span class="n">name</span> <span class="o">=</span> <span class="n">method</span><span class="o">.</span><span class="na">getName</span><span class="o">();</span>
                <span class="k">if</span> <span class="o">(</span><span class="nc">MethodUtils</span><span class="o">.</span><span class="na">isGetter</span><span class="o">(</span><span class="n">method</span><span class="o">))</span> <span class="o">{</span>
                    <span class="nc">Parameter</span> <span class="n">parameter</span> <span class="o">=</span> <span class="n">method</span><span class="o">.</span><span class="na">getAnnotation</span><span class="o">(</span><span class="nc">Parameter</span><span class="o">.</span><span class="na">class</span><span class="o">);</span>
                    <span class="k">if</span> <span class="o">(</span><span class="n">method</span><span class="o">.</span><span class="na">getReturnType</span><span class="o">()</span> <span class="o">==</span> <span class="nc">Object</span><span class="o">.</span><span class="na">class</span> <span class="o">||</span> <span class="n">parameter</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">parameter</span><span class="o">.</span><span class="na">excluded</span><span class="o">())</span> <span class="o">{</span>
                        <span class="k">continue</span><span class="o">;</span>
                    <span class="o">}</span>
                    <span class="nc">String</span> <span class="n">key</span><span class="o">;</span>
                    <span class="k">if</span> <span class="o">(</span><span class="n">parameter</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">parameter</span><span class="o">.</span><span class="na">key</span><span class="o">().</span><span class="na">length</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
                        <span class="n">key</span> <span class="o">=</span> <span class="n">parameter</span><span class="o">.</span><span class="na">key</span><span class="o">();</span>
                    <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
                        <span class="n">key</span> <span class="o">=</span> <span class="n">calculatePropertyFromGetter</span><span class="o">(</span><span class="n">name</span><span class="o">);</span>
                    <span class="o">}</span>
                    <span class="nc">Object</span> <span class="n">value</span> <span class="o">=</span> <span class="n">method</span><span class="o">.</span><span class="na">invoke</span><span class="o">(</span><span class="n">config</span><span class="o">);</span>
                    <span class="nc">String</span> <span class="n">str</span> <span class="o">=</span> <span class="nc">String</span><span class="o">.</span><span class="na">valueOf</span><span class="o">(</span><span class="n">value</span><span class="o">).</span><span class="na">trim</span><span class="o">();</span>
                    <span class="k">if</span> <span class="o">(</span><span class="n">value</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">str</span><span class="o">.</span><span class="na">length</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
                        <span class="k">if</span> <span class="o">(</span><span class="n">parameter</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">parameter</span><span class="o">.</span><span class="na">escaped</span><span class="o">())</span> <span class="o">{</span>
                            <span class="n">str</span> <span class="o">=</span> <span class="no">URL</span><span class="o">.</span><span class="na">encode</span><span class="o">(</span><span class="n">str</span><span class="o">);</span>
                        <span class="o">}</span>
                        <span class="k">if</span> <span class="o">(</span><span class="n">parameter</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">parameter</span><span class="o">.</span><span class="na">append</span><span class="o">())</span> <span class="o">{</span>
                            <span class="nc">String</span> <span class="n">pre</span> <span class="o">=</span> <span class="n">parameters</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">key</span><span class="o">);</span>
                            <span class="k">if</span> <span class="o">(</span><span class="n">pre</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">pre</span><span class="o">.</span><span class="na">length</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
                                <span class="n">str</span> <span class="o">=</span> <span class="n">pre</span> <span class="o">+</span> <span class="s">","</span> <span class="o">+</span> <span class="n">str</span><span class="o">;</span>
                            <span class="o">}</span>
                        <span class="o">}</span>
                        <span class="k">if</span> <span class="o">(</span><span class="n">prefix</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">prefix</span><span class="o">.</span><span class="na">length</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
                            <span class="n">key</span> <span class="o">=</span> <span class="n">prefix</span> <span class="o">+</span> <span class="s">"."</span> <span class="o">+</span> <span class="n">key</span><span class="o">;</span>
                        <span class="o">}</span>
                        <span class="n">parameters</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">key</span><span class="o">,</span> <span class="n">str</span><span class="o">);</span>
                    <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">(</span><span class="n">parameter</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">parameter</span><span class="o">.</span><span class="na">required</span><span class="o">())</span> <span class="o">{</span>
                        <span class="k">throw</span> <span class="k">new</span> <span class="nf">IllegalStateException</span><span class="o">(</span><span class="n">config</span><span class="o">.</span><span class="na">getClass</span><span class="o">().</span><span class="na">getSimpleName</span><span class="o">()</span> <span class="o">+</span> <span class="s">"."</span> <span class="o">+</span> <span class="n">key</span> <span class="o">+</span> <span class="s">" == null"</span><span class="o">);</span>
                    <span class="o">}</span>
                <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">(</span><span class="n">isParametersGetter</span><span class="o">(</span><span class="n">method</span><span class="o">))</span> <span class="o">{</span>
                    <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">String</span><span class="o">&gt;</span> <span class="n">map</span> <span class="o">=</span> <span class="o">(</span><span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">String</span><span class="o">&gt;)</span> <span class="n">method</span><span class="o">.</span><span class="na">invoke</span><span class="o">(</span><span class="n">config</span><span class="o">,</span> <span class="k">new</span> <span class="nc">Object</span><span class="o">[</span><span class="mi">0</span><span class="o">]);</span>
                    <span class="n">parameters</span><span class="o">.</span><span class="na">putAll</span><span class="o">(</span><span class="n">convert</span><span class="o">(</span><span class="n">map</span><span class="o">,</span> <span class="n">prefix</span><span class="o">));</span>
                <span class="o">}</span>
            <span class="o">}</span> <span class="k">catch</span> <span class="o">(</span><span class="nc">Exception</span> <span class="n">e</span><span class="o">)</span> <span class="o">{</span>
                <span class="k">throw</span> <span class="k">new</span> <span class="nf">IllegalStateException</span><span class="o">(</span><span class="n">e</span><span class="o">.</span><span class="na">getMessage</span><span class="o">(),</span> <span class="n">e</span><span class="o">);</span>
            <span class="o">}</span>
        <span class="o">}</span>
    <span class="o">}</span>
</code></pre></div></div>

<p>再更详细的看看<code class="language-plaintext highlighter-rouge">appendParameters(...)</code>函数的原理,大概就执行这么一个逻辑:</p>

<pre><code class="language-mermaid">graph TD
id1("获取到所有的config的getter方法")
id2("调用所有的getter方法,获取到返回的value")
id3("把key和value放到map里")

id4{"map里是否已经含有该key"}
    id5("value用一个逗号和已经存放的value连接起来(pre,curr)")
id6{"prefix是否为空"}
    id7("key用.连接起来(prefix.key)")

id1 --&gt; id2
id2 --&gt; id4
id4 --是--&gt; id5
    id5 --&gt; id6
id4 --否--&gt; id6
id6 --否--&gt; id7
    id7 --&gt; id3
id6 --是--&gt; id3
</code></pre>

<p>说完了工具函数<code class="language-plaintext highlighter-rouge">appendParameters(...)</code>,接下来就是<code class="language-plaintext highlighter-rouge">doExportUrlsFor1Protocol(...)</code>的正式过程<br />
以下将对<code class="language-plaintext highlighter-rouge">doExportUrlsFor1Protocol(...)</code>的代码逐段分析</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code>    <span class="kd">private</span> <span class="kt">void</span> <span class="nf">doExportUrlsFor1Protocol</span><span class="o">(</span><span class="nc">ProtocolConfig</span> <span class="n">protocolConfig</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="no">URL</span><span class="o">&gt;</span> <span class="n">registryURLs</span><span class="o">)</span> <span class="o">{</span>
        <span class="nc">String</span> <span class="n">name</span> <span class="o">=</span> <span class="n">protocolConfig</span><span class="o">.</span><span class="na">getName</span><span class="o">();</span>
        <span class="k">if</span> <span class="o">(</span><span class="nc">StringUtils</span><span class="o">.</span><span class="na">isEmpty</span><span class="o">(</span><span class="n">name</span><span class="o">))</span> <span class="o">{</span>
            <span class="n">name</span> <span class="o">=</span> <span class="no">DUBBO</span><span class="o">;</span>
        <span class="o">}</span>

        <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">String</span><span class="o">&gt;</span> <span class="n">map</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">HashMap</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">String</span><span class="o">&gt;();</span>
        <span class="n">map</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="no">SIDE_KEY</span><span class="o">,</span> <span class="no">PROVIDER_SIDE</span><span class="o">);</span>

        <span class="nc">ServiceConfig</span><span class="o">.</span><span class="na">appendRuntimeParameters</span><span class="o">(</span><span class="n">map</span><span class="o">);</span>
        <span class="nc">AbstractConfig</span><span class="o">.</span><span class="na">appendParameters</span><span class="o">(</span><span class="n">map</span><span class="o">,</span> <span class="n">getMetrics</span><span class="o">());</span>
        <span class="nc">AbstractConfig</span><span class="o">.</span><span class="na">appendParameters</span><span class="o">(</span><span class="n">map</span><span class="o">,</span> <span class="n">getApplication</span><span class="o">());</span>
        <span class="nc">AbstractConfig</span><span class="o">.</span><span class="na">appendParameters</span><span class="o">(</span><span class="n">map</span><span class="o">,</span> <span class="n">getModule</span><span class="o">());</span>
        <span class="c1">// remove 'default.' prefix for configs from ProviderConfig</span>
        <span class="c1">// appendParameters(map, provider, Constants.DEFAULT_KEY);</span>
        <span class="nc">AbstractConfig</span><span class="o">.</span><span class="na">appendParameters</span><span class="o">(</span><span class="n">map</span><span class="o">,</span> <span class="n">provider</span><span class="o">);</span>
        <span class="nc">AbstractConfig</span><span class="o">.</span><span class="na">appendParameters</span><span class="o">(</span><span class="n">map</span><span class="o">,</span> <span class="n">protocolConfig</span><span class="o">);</span>
        <span class="nc">AbstractConfig</span><span class="o">.</span><span class="na">appendParameters</span><span class="o">(</span><span class="n">map</span><span class="o">,</span> <span class="k">this</span><span class="o">);</span>
        <span class="nc">MetadataReportConfig</span> <span class="n">metadataReportConfig</span> <span class="o">=</span> <span class="n">getMetadataReportConfig</span><span class="o">();</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">metadataReportConfig</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">metadataReportConfig</span><span class="o">.</span><span class="na">isValid</span><span class="o">())</span> <span class="o">{</span>
            <span class="n">map</span><span class="o">.</span><span class="na">putIfAbsent</span><span class="o">(</span><span class="no">METADATA_KEY</span><span class="o">,</span> <span class="no">REMOTE_METADATA_STORAGE_TYPE</span><span class="o">);</span>
        <span class="o">}</span>
        <span class="c1">//...</span>
</code></pre></div></div>

<p>以上这一段代码把<code class="language-plaintext highlighter-rouge">MetricsConfig</code>,<code class="language-plaintext highlighter-rouge">ApplicationConfig</code>,<code class="language-plaintext highlighter-rouge">ModuleConfig</code>,<code class="language-plaintext highlighter-rouge">ProviderConfig</code>,<code class="language-plaintext highlighter-rouge">ProtocolConfig</code>,<code class="language-plaintext highlighter-rouge">ServiceConfig</code>,的相关参数通过<code class="language-plaintext highlighter-rouge">AbstractConfig.appendParameters</code>保存到<code class="language-plaintext highlighter-rouge">map</code>里</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">if</span> <span class="o">(</span><span class="nc">CollectionUtils</span><span class="o">.</span><span class="na">isNotEmpty</span><span class="o">(</span><span class="n">getMethods</span><span class="o">()))</span> <span class="o">{</span>
            <span class="k">for</span> <span class="o">(</span><span class="nc">MethodConfig</span> <span class="n">method</span> <span class="o">:</span> <span class="n">getMethods</span><span class="o">())</span> <span class="o">{</span>
                <span class="nc">AbstractConfig</span><span class="o">.</span><span class="na">appendParameters</span><span class="o">(</span><span class="n">map</span><span class="o">,</span> <span class="n">method</span><span class="o">,</span> <span class="n">method</span><span class="o">.</span><span class="na">getName</span><span class="o">());</span>
                <span class="nc">String</span> <span class="n">retryKey</span> <span class="o">=</span> <span class="n">method</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">".retry"</span><span class="o">;</span>
                <span class="k">if</span> <span class="o">(</span><span class="n">map</span><span class="o">.</span><span class="na">containsKey</span><span class="o">(</span><span class="n">retryKey</span><span class="o">))</span> <span class="o">{</span>
                    <span class="nc">String</span> <span class="n">retryValue</span> <span class="o">=</span> <span class="n">map</span><span class="o">.</span><span class="na">remove</span><span class="o">(</span><span class="n">retryKey</span><span class="o">);</span>
                    <span class="k">if</span> <span class="o">(</span><span class="s">"false"</span><span class="o">.</span><span class="na">equals</span><span class="o">(</span><span class="n">retryValue</span><span class="o">))</span> <span class="o">{</span>
                        <span class="n">map</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">method</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">".retries"</span><span class="o">,</span> <span class="s">"0"</span><span class="o">);</span>
                    <span class="o">}</span>
                <span class="o">}</span>
</code></pre></div></div>

<p>把所有配置的<code class="language-plaintext highlighter-rouge">MethodConfig</code>的相关参数存放到<code class="language-plaintext highlighter-rouge">map</code>里</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code>                <span class="nc">List</span><span class="o">&lt;</span><span class="nc">ArgumentConfig</span><span class="o">&gt;</span> <span class="n">arguments</span> <span class="o">=</span> <span class="n">method</span><span class="o">.</span><span class="na">getArguments</span><span class="o">();</span>
                <span class="k">if</span> <span class="o">(</span><span class="nc">CollectionUtils</span><span class="o">.</span><span class="na">isNotEmpty</span><span class="o">(</span><span class="n">arguments</span><span class="o">))</span> <span class="o">{</span>
                    <span class="k">for</span> <span class="o">(</span><span class="nc">ArgumentConfig</span> <span class="n">argument</span> <span class="o">:</span> <span class="n">arguments</span><span class="o">)</span> <span class="o">{</span>
                        <span class="c1">// convert argument type</span>
                        <span class="k">if</span> <span class="o">(</span><span class="n">argument</span><span class="o">.</span><span class="na">getType</span><span class="o">()</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">argument</span><span class="o">.</span><span class="na">getType</span><span class="o">().</span><span class="na">length</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
                            <span class="nc">Method</span><span class="o">[]</span> <span class="n">methods</span> <span class="o">=</span> <span class="n">interfaceClass</span><span class="o">.</span><span class="na">getMethods</span><span class="o">();</span>
                            <span class="c1">// visit all methods</span>
                            <span class="k">if</span> <span class="o">(</span><span class="n">methods</span><span class="o">.</span><span class="na">length</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
                                <span class="k">for</span> <span class="o">(</span><span class="kt">int</span> <span class="n">i</span> <span class="o">=</span> <span class="mi">0</span><span class="o">;</span> <span class="n">i</span> <span class="o">&lt;</span> <span class="n">methods</span><span class="o">.</span><span class="na">length</span><span class="o">;</span> <span class="n">i</span><span class="o">++)</span> <span class="o">{</span>
                                    <span class="nc">String</span> <span class="n">methodName</span> <span class="o">=</span> <span class="n">methods</span><span class="o">[</span><span class="n">i</span><span class="o">].</span><span class="na">getName</span><span class="o">();</span>
                                    <span class="c1">// target the method, and get its signature</span>
                                    <span class="k">if</span> <span class="o">(</span><span class="n">methodName</span><span class="o">.</span><span class="na">equals</span><span class="o">(</span><span class="n">method</span><span class="o">.</span><span class="na">getName</span><span class="o">()))</span> <span class="o">{</span>
                                        <span class="nc">Class</span><span class="o">&lt;?&gt;[]</span> <span class="n">argtypes</span> <span class="o">=</span> <span class="n">methods</span><span class="o">[</span><span class="n">i</span><span class="o">].</span><span class="na">getParameterTypes</span><span class="o">();</span>
                                        <span class="c1">// one callback in the method</span>
                                        <span class="k">if</span> <span class="o">(</span><span class="n">argument</span><span class="o">.</span><span class="na">getIndex</span><span class="o">()</span> <span class="o">!=</span> <span class="o">-</span><span class="mi">1</span><span class="o">)</span> <span class="o">{</span>
                                            <span class="k">if</span> <span class="o">(</span><span class="n">argtypes</span><span class="o">[</span><span class="n">argument</span><span class="o">.</span><span class="na">getIndex</span><span class="o">()].</span><span class="na">getName</span><span class="o">().</span><span class="na">equals</span><span class="o">(</span><span class="n">argument</span><span class="o">.</span><span class="na">getType</span><span class="o">()))</span> <span class="o">{</span>
                                                <span class="nc">AbstractConfig</span><span class="o">.</span><span class="na">appendParameters</span><span class="o">(</span><span class="n">map</span><span class="o">,</span> <span class="n">argument</span><span class="o">,</span> <span class="n">method</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">"."</span> <span class="o">+</span> <span class="n">argument</span><span class="o">.</span><span class="na">getIndex</span><span class="o">());</span>
                                            <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
                                                <span class="k">throw</span> <span class="k">new</span> <span class="nf">IllegalArgumentException</span><span class="o">(</span><span class="s">"Argument config error : the index attribute and type attribute not match :index :"</span> <span class="o">+</span> <span class="n">argument</span><span class="o">.</span><span class="na">getIndex</span><span class="o">()</span> <span class="o">+</span> <span class="s">", type:"</span> <span class="o">+</span> <span class="n">argument</span><span class="o">.</span><span class="na">getType</span><span class="o">());</span>
                                            <span class="o">}</span>
                                        <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
                                            <span class="c1">// multiple callbacks in the method</span>
                                            <span class="k">for</span> <span class="o">(</span><span class="kt">int</span> <span class="n">j</span> <span class="o">=</span> <span class="mi">0</span><span class="o">;</span> <span class="n">j</span> <span class="o">&lt;</span> <span class="n">argtypes</span><span class="o">.</span><span class="na">length</span><span class="o">;</span> <span class="n">j</span><span class="o">++)</span> <span class="o">{</span>
                                                <span class="nc">Class</span><span class="o">&lt;?&gt;</span> <span class="n">argclazz</span> <span class="o">=</span> <span class="n">argtypes</span><span class="o">[</span><span class="n">j</span><span class="o">];</span>
                                                <span class="k">if</span> <span class="o">(</span><span class="n">argclazz</span><span class="o">.</span><span class="na">getName</span><span class="o">().</span><span class="na">equals</span><span class="o">(</span><span class="n">argument</span><span class="o">.</span><span class="na">getType</span><span class="o">()))</span> <span class="o">{</span>
                                                    <span class="nc">AbstractConfig</span><span class="o">.</span><span class="na">appendParameters</span><span class="o">(</span><span class="n">map</span><span class="o">,</span> <span class="n">argument</span><span class="o">,</span> <span class="n">method</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">"."</span> <span class="o">+</span> <span class="n">j</span><span class="o">);</span>
                                                    <span class="k">if</span> <span class="o">(</span><span class="n">argument</span><span class="o">.</span><span class="na">getIndex</span><span class="o">()</span> <span class="o">!=</span> <span class="o">-</span><span class="mi">1</span> <span class="o">&amp;&amp;</span> <span class="n">argument</span><span class="o">.</span><span class="na">getIndex</span><span class="o">()</span> <span class="o">!=</span> <span class="n">j</span><span class="o">)</span> <span class="o">{</span>
                                                        <span class="k">throw</span> <span class="k">new</span> <span class="nf">IllegalArgumentException</span><span class="o">(</span><span class="s">"Argument config error : the index attribute and type attribute not match :index :"</span> <span class="o">+</span> <span class="n">argument</span><span class="o">.</span><span class="na">getIndex</span><span class="o">()</span> <span class="o">+</span> <span class="s">", type:"</span> <span class="o">+</span> <span class="n">argument</span><span class="o">.</span><span class="na">getType</span><span class="o">());</span>
                                                    <span class="o">}</span>
                                                <span class="o">}</span>
                                            <span class="o">}</span>
                                        <span class="o">}</span>
                                    <span class="o">}</span>
                                <span class="o">}</span>
                            <span class="o">}</span>
                        <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">(</span><span class="n">argument</span><span class="o">.</span><span class="na">getIndex</span><span class="o">()</span> <span class="o">!=</span> <span class="o">-</span><span class="mi">1</span><span class="o">)</span> <span class="o">{</span>
                            <span class="nc">AbstractConfig</span><span class="o">.</span><span class="na">appendParameters</span><span class="o">(</span><span class="n">map</span><span class="o">,</span> <span class="n">argument</span><span class="o">,</span> <span class="n">method</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">"."</span> <span class="o">+</span> <span class="n">argument</span><span class="o">.</span><span class="na">getIndex</span><span class="o">());</span>
                        <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
                            <span class="k">throw</span> <span class="k">new</span> <span class="nf">IllegalArgumentException</span><span class="o">(</span><span class="s">"Argument config must set index or type attribute.eg: &lt;dubbo:argument index='0' .../&gt; or &lt;dubbo:argument type=xxx .../&gt;"</span><span class="o">);</span>
                        <span class="o">}</span>

                    <span class="o">}</span>
                <span class="o">}</span>
            <span class="o">}</span> <span class="c1">// end of methods for</span>
        <span class="o">}</span>
</code></pre></div></div>

<p>以上的代码由于<code class="language-plaintext highlighter-rouge">if</code>和<code class="language-plaintext highlighter-rouge">for</code>的嵌套复杂,直接用流程图画出来如下</p>

<pre><code class="language-mermaid">graph TD
id1("获取MethodConfig的所有实参")
id2("获取配置的interfaceClass的所有方法")
id3("找到MethodConfig与interfaceClass对应的方法")
id4("验证MethodConfig的参数列表和interfaceClass的参数列表是否匹配")
    id5("抛出异常")
id6("把MethodConfig配置的ArgumentConfig(实参)再次通过appendParameters存放到map")

id1 --&gt; id2
id2 --&gt; id3
id3 --&gt; id4
id4 --不匹配--&gt; id5
id4 --匹配  --&gt; id6
</code></pre>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code>        <span class="k">if</span> <span class="o">(</span><span class="nc">ProtocolUtils</span><span class="o">.</span><span class="na">isGeneric</span><span class="o">(</span><span class="n">generic</span><span class="o">))</span> <span class="o">{</span>
            <span class="n">map</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="no">GENERIC_KEY</span><span class="o">,</span> <span class="n">generic</span><span class="o">);</span>
            <span class="n">map</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="no">METHODS_KEY</span><span class="o">,</span> <span class="no">ANY_VALUE</span><span class="o">);</span>
        <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
            <span class="nc">String</span> <span class="n">revision</span> <span class="o">=</span> <span class="nc">Version</span><span class="o">.</span><span class="na">getVersion</span><span class="o">(</span><span class="n">interfaceClass</span><span class="o">,</span> <span class="n">version</span><span class="o">);</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">revision</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">revision</span><span class="o">.</span><span class="na">length</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
                <span class="n">map</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="no">REVISION_KEY</span><span class="o">,</span> <span class="n">revision</span><span class="o">);</span>
            <span class="o">}</span>

            <span class="nc">String</span><span class="o">[]</span> <span class="n">methods</span> <span class="o">=</span> <span class="nc">Wrapper</span><span class="o">.</span><span class="na">getWrapper</span><span class="o">(</span><span class="n">interfaceClass</span><span class="o">).</span><span class="na">getMethodNames</span><span class="o">();</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">methods</span><span class="o">.</span><span class="na">length</span> <span class="o">==</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
                <span class="n">logger</span><span class="o">.</span><span class="na">warn</span><span class="o">(</span><span class="s">"No method found in service interface "</span> <span class="o">+</span> <span class="n">interfaceClass</span><span class="o">.</span><span class="na">getName</span><span class="o">());</span>
                <span class="n">map</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="no">METHODS_KEY</span><span class="o">,</span> <span class="no">ANY_VALUE</span><span class="o">);</span>
            <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
                <span class="n">map</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="no">METHODS_KEY</span><span class="o">,</span> <span class="nc">StringUtils</span><span class="o">.</span><span class="na">join</span><span class="o">(</span><span class="k">new</span> <span class="nc">HashSet</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;(</span><span class="nc">Arrays</span><span class="o">.</span><span class="na">asList</span><span class="o">(</span><span class="n">methods</span><span class="o">)),</span> <span class="s">","</span><span class="o">));</span>
            <span class="o">}</span>
        <span class="o">}</span>

        <span class="cm">/**
         * Here the token value configured by the provider is used to assign the value to ServiceConfig#token
         */</span>
        <span class="k">if</span><span class="o">(</span><span class="nc">ConfigUtils</span><span class="o">.</span><span class="na">isEmpty</span><span class="o">(</span><span class="n">token</span><span class="o">)</span> <span class="o">&amp;&amp;</span> <span class="n">provider</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
            <span class="n">token</span> <span class="o">=</span> <span class="n">provider</span><span class="o">.</span><span class="na">getToken</span><span class="o">();</span>
        <span class="o">}</span>

        <span class="k">if</span> <span class="o">(!</span><span class="nc">ConfigUtils</span><span class="o">.</span><span class="na">isEmpty</span><span class="o">(</span><span class="n">token</span><span class="o">))</span> <span class="o">{</span>
            <span class="k">if</span> <span class="o">(</span><span class="nc">ConfigUtils</span><span class="o">.</span><span class="na">isDefault</span><span class="o">(</span><span class="n">token</span><span class="o">))</span> <span class="o">{</span>
                <span class="n">map</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="no">TOKEN_KEY</span><span class="o">,</span> <span class="no">UUID</span><span class="o">.</span><span class="na">randomUUID</span><span class="o">().</span><span class="na">toString</span><span class="o">());</span>
            <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
                <span class="n">map</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="no">TOKEN_KEY</span><span class="o">,</span> <span class="n">token</span><span class="o">);</span>
            <span class="o">}</span>
        <span class="o">}</span>
</code></pre></div></div>

<p>上面这一段本质上和前文的代码没有什么太大区别,也是一个把一些信息放进<code class="language-plaintext highlighter-rouge">map</code>的过程</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code>        <span class="c1">//init serviceMetadata attachments</span>
        <span class="n">serviceMetadata</span><span class="o">.</span><span class="na">getAttachments</span><span class="o">().</span><span class="na">putAll</span><span class="o">(</span><span class="n">map</span><span class="o">);</span>

        <span class="c1">// export service</span>
        <span class="nc">String</span> <span class="n">host</span> <span class="o">=</span> <span class="n">findConfigedHosts</span><span class="o">(</span><span class="n">protocolConfig</span><span class="o">,</span> <span class="n">registryURLs</span><span class="o">,</span> <span class="n">map</span><span class="o">);</span>
        <span class="nc">Integer</span> <span class="n">port</span> <span class="o">=</span> <span class="n">findConfigedPorts</span><span class="o">(</span><span class="n">protocolConfig</span><span class="o">,</span> <span class="n">name</span><span class="o">,</span> <span class="n">map</span><span class="o">);</span>
        <span class="no">URL</span> <span class="n">url</span> <span class="o">=</span> <span class="k">new</span> <span class="no">URL</span><span class="o">(</span><span class="n">name</span><span class="o">,</span> <span class="n">host</span><span class="o">,</span> <span class="n">port</span><span class="o">,</span> <span class="n">getContextPath</span><span class="o">(</span><span class="n">protocolConfig</span><span class="o">).</span><span class="na">map</span><span class="o">(</span><span class="n">p</span> <span class="o">-&gt;</span> <span class="n">p</span> <span class="o">+</span> <span class="s">"/"</span> <span class="o">+</span> <span class="n">path</span><span class="o">).</span><span class="na">orElse</span><span class="o">(</span><span class="n">path</span><span class="o">),</span> <span class="n">map</span><span class="o">);</span>

        <span class="c1">// You can customize Configurator to append extra parameters</span>
        <span class="k">if</span> <span class="o">(</span><span class="nc">ExtensionLoader</span><span class="o">.</span><span class="na">getExtensionLoader</span><span class="o">(</span><span class="nc">ConfiguratorFactory</span><span class="o">.</span><span class="na">class</span><span class="o">)</span>
                <span class="o">.</span><span class="na">hasExtension</span><span class="o">(</span><span class="n">url</span><span class="o">.</span><span class="na">getProtocol</span><span class="o">()))</span> <span class="o">{</span>
            <span class="n">url</span> <span class="o">=</span> <span class="nc">ExtensionLoader</span><span class="o">.</span><span class="na">getExtensionLoader</span><span class="o">(</span><span class="nc">ConfiguratorFactory</span><span class="o">.</span><span class="na">class</span><span class="o">)</span>
                    <span class="o">.</span><span class="na">getExtension</span><span class="o">(</span><span class="n">url</span><span class="o">.</span><span class="na">getProtocol</span><span class="o">()).</span><span class="na">getConfigurator</span><span class="o">(</span><span class="n">url</span><span class="o">).</span><span class="na">configure</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
        <span class="o">}</span>
</code></pre></div></div>

<p>以上代码是进行正式导出前的最后准备工作,主要是组装<code class="language-plaintext highlighter-rouge">URL</code></p>

<pre><code class="language-mermaid">graph TD
id1("把map转存到serviceMetadata里")
id2("获取要导出的地址,端口")
id3("根据要导出的协议,地址,端口,以及上文一直提到的map组装成一个URL")
id4("通过动态SPI加载用户自定义的ConfiguratorFactory扩展,然后调用其configure方法对URL进行自定义修改")

id1 --&gt; id2
id2 --&gt; id3
id3 --&gt; id4
</code></pre>

<h3 id="导出服务">导出服务</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code>        <span class="nc">String</span> <span class="n">scope</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="no">SCOPE_KEY</span><span class="o">);</span>
        <span class="c1">// don't export when none is configured</span>
        <span class="k">if</span> <span class="o">(!</span><span class="no">SCOPE_NONE</span><span class="o">.</span><span class="na">equalsIgnoreCase</span><span class="o">(</span><span class="n">scope</span><span class="o">))</span> <span class="o">{</span>

            <span class="c1">// export to local if the config is not remote (export to remote only when config is remote)</span>
            <span class="k">if</span> <span class="o">(!</span><span class="no">SCOPE_REMOTE</span><span class="o">.</span><span class="na">equalsIgnoreCase</span><span class="o">(</span><span class="n">scope</span><span class="o">))</span> <span class="o">{</span>
                <span class="n">exportLocal</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
            <span class="o">}</span>
            <span class="c1">// export to remote if the config is not local (export to local only when config is local)</span>
            <span class="k">if</span> <span class="o">(!</span><span class="no">SCOPE_LOCAL</span><span class="o">.</span><span class="na">equalsIgnoreCase</span><span class="o">(</span><span class="n">scope</span><span class="o">))</span> <span class="o">{</span>
                <span class="k">if</span> <span class="o">(</span><span class="nc">CollectionUtils</span><span class="o">.</span><span class="na">isNotEmpty</span><span class="o">(</span><span class="n">registryURLs</span><span class="o">))</span> <span class="o">{</span>
                    <span class="k">for</span> <span class="o">(</span><span class="no">URL</span> <span class="n">registryURL</span> <span class="o">:</span> <span class="n">registryURLs</span><span class="o">)</span> <span class="o">{</span>
                        <span class="c1">//if protocol is only injvm ,not register</span>
                        <span class="k">if</span> <span class="o">(</span><span class="no">LOCAL_PROTOCOL</span><span class="o">.</span><span class="na">equalsIgnoreCase</span><span class="o">(</span><span class="n">url</span><span class="o">.</span><span class="na">getProtocol</span><span class="o">()))</span> <span class="o">{</span>
                            <span class="k">continue</span><span class="o">;</span>
                        <span class="o">}</span>
                        <span class="n">url</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">addParameterIfAbsent</span><span class="o">(</span><span class="no">DYNAMIC_KEY</span><span class="o">,</span> <span class="n">registryURL</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="no">DYNAMIC_KEY</span><span class="o">));</span>
                        <span class="no">URL</span> <span class="n">monitorUrl</span> <span class="o">=</span> <span class="nc">ConfigValidationUtils</span><span class="o">.</span><span class="na">loadMonitor</span><span class="o">(</span><span class="k">this</span><span class="o">,</span> <span class="n">registryURL</span><span class="o">);</span>
                        <span class="k">if</span> <span class="o">(</span><span class="n">monitorUrl</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
                            <span class="n">url</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">addParameterAndEncoded</span><span class="o">(</span><span class="no">MONITOR_KEY</span><span class="o">,</span> <span class="n">monitorUrl</span><span class="o">.</span><span class="na">toFullString</span><span class="o">());</span>
                        <span class="o">}</span>
                        <span class="k">if</span> <span class="o">(</span><span class="n">logger</span><span class="o">.</span><span class="na">isInfoEnabled</span><span class="o">())</span> <span class="o">{</span>
                            <span class="k">if</span> <span class="o">(</span><span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="no">REGISTER_KEY</span><span class="o">,</span> <span class="kc">true</span><span class="o">))</span> <span class="o">{</span>
                                <span class="n">logger</span><span class="o">.</span><span class="na">info</span><span class="o">(</span><span class="s">"Register dubbo service "</span> <span class="o">+</span> <span class="n">interfaceClass</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">" url "</span> <span class="o">+</span> <span class="n">url</span> <span class="o">+</span> <span class="s">" to registry "</span> <span class="o">+</span> <span class="n">registryURL</span><span class="o">);</span>
                            <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
                                <span class="n">logger</span><span class="o">.</span><span class="na">info</span><span class="o">(</span><span class="s">"Export dubbo service "</span> <span class="o">+</span> <span class="n">interfaceClass</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">" to url "</span> <span class="o">+</span> <span class="n">url</span><span class="o">);</span>
                            <span class="o">}</span>
                        <span class="o">}</span>

                        <span class="c1">// For providers, this is used to enable custom proxy to generate invoker</span>
                        <span class="nc">String</span> <span class="n">proxy</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="no">PROXY_KEY</span><span class="o">);</span>
                        <span class="k">if</span> <span class="o">(</span><span class="nc">StringUtils</span><span class="o">.</span><span class="na">isNotEmpty</span><span class="o">(</span><span class="n">proxy</span><span class="o">))</span> <span class="o">{</span>
                            <span class="n">registryURL</span> <span class="o">=</span> <span class="n">registryURL</span><span class="o">.</span><span class="na">addParameter</span><span class="o">(</span><span class="no">PROXY_KEY</span><span class="o">,</span> <span class="n">proxy</span><span class="o">);</span>
                        <span class="o">}</span>

                        <span class="nc">Invoker</span><span class="o">&lt;?&gt;</span> <span class="n">invoker</span> <span class="o">=</span> <span class="no">PROXY_FACTORY</span><span class="o">.</span><span class="na">getInvoker</span><span class="o">(</span><span class="n">ref</span><span class="o">,</span> <span class="o">(</span><span class="nc">Class</span><span class="o">)</span> <span class="n">interfaceClass</span><span class="o">,</span> <span class="n">registryURL</span><span class="o">.</span><span class="na">addParameterAndEncoded</span><span class="o">(</span><span class="no">EXPORT_KEY</span><span class="o">,</span> <span class="n">url</span><span class="o">.</span><span class="na">toFullString</span><span class="o">()));</span>
                        <span class="nc">DelegateProviderMetaDataInvoker</span> <span class="n">wrapperInvoker</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">DelegateProviderMetaDataInvoker</span><span class="o">(</span><span class="n">invoker</span><span class="o">,</span> <span class="k">this</span><span class="o">);</span>

                        <span class="nc">Exporter</span><span class="o">&lt;?&gt;</span> <span class="n">exporter</span> <span class="o">=</span> <span class="no">PROTOCOL</span><span class="o">.</span><span class="na">export</span><span class="o">(</span><span class="n">wrapperInvoker</span><span class="o">);</span>
                        <span class="n">exporters</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">exporter</span><span class="o">);</span>
                    <span class="o">}</span>
                <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
                    <span class="k">if</span> <span class="o">(</span><span class="n">logger</span><span class="o">.</span><span class="na">isInfoEnabled</span><span class="o">())</span> <span class="o">{</span>
                        <span class="n">logger</span><span class="o">.</span><span class="na">info</span><span class="o">(</span><span class="s">"Export dubbo service "</span> <span class="o">+</span> <span class="n">interfaceClass</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">" to url "</span> <span class="o">+</span> <span class="n">url</span><span class="o">);</span>
                    <span class="o">}</span>
                    <span class="nc">Invoker</span><span class="o">&lt;?&gt;</span> <span class="n">invoker</span> <span class="o">=</span> <span class="no">PROXY_FACTORY</span><span class="o">.</span><span class="na">getInvoker</span><span class="o">(</span><span class="n">ref</span><span class="o">,</span> <span class="o">(</span><span class="nc">Class</span><span class="o">)</span> <span class="n">interfaceClass</span><span class="o">,</span> <span class="n">url</span><span class="o">);</span>
                    <span class="nc">DelegateProviderMetaDataInvoker</span> <span class="n">wrapperInvoker</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">DelegateProviderMetaDataInvoker</span><span class="o">(</span><span class="n">invoker</span><span class="o">,</span> <span class="k">this</span><span class="o">);</span>

                    <span class="nc">Exporter</span><span class="o">&lt;?&gt;</span> <span class="n">exporter</span> <span class="o">=</span> <span class="no">PROTOCOL</span><span class="o">.</span><span class="na">export</span><span class="o">(</span><span class="n">wrapperInvoker</span><span class="o">);</span>
                    <span class="n">exporters</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">exporter</span><span class="o">);</span>
                <span class="o">}</span>
                <span class="cm">/**
                 * @since 2.7.0
                 * ServiceData Store
                 */</span>
                <span class="nc">WritableMetadataService</span> <span class="n">metadataService</span> <span class="o">=</span> <span class="nc">WritableMetadataService</span><span class="o">.</span><span class="na">getExtension</span><span class="o">(</span><span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="no">METADATA_KEY</span><span class="o">,</span> <span class="no">DEFAULT_METADATA_STORAGE_TYPE</span><span class="o">));</span>
                <span class="k">if</span> <span class="o">(</span><span class="n">metadataService</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
                    <span class="n">metadataService</span><span class="o">.</span><span class="na">publishServiceDefinition</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
                <span class="o">}</span>
            <span class="o">}</span>
        <span class="o">}</span>
        <span class="k">this</span><span class="o">.</span><span class="na">urls</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
    <span class="o">}</span>
</code></pre></div></div>

<p>正式导出的过程代码倒是不多,用流程图画出来如下</p>

<pre><code class="language-mermaid">graph TD
id1("通过URL获取导出的作用域")
id2{"作用域是否为NONE_SCOPE,也就是不导出"}
id3{"作用域是否为SCOPE_LOCAL"}
    id4("调用exportLocal()向本地导出")
id5("向远程导出")
id6("registryURLs是否为空(也就是注册中心URL)")    
    id7{"对每个注册中心URL,判断是不是LOCAL_PROTOCOL"}
        id8(往url里添加dynamic和monitorUrl的参数)
        id9("日志系统记录一些东西")
        id10{"url是否包含PROXY_KEY参数"}
            id11("往注册中心URL添加PROXY_KEY参数")
        id12("调用PROXY_FACTORY.getInvoker(...)\n并根据配置的接口以及实现以及注册中心URL和导出URL组装一个Invoker")
        id13("根据该Invoker和当前的ServiceConfig生成一个DelegateProviderMetaDataInvoker")
        id14("调用自适应Protocol的export(Invoker)生成Exporter并添加到ServiceConfig的exporters列表中")
id15("把导出的url添加到ServiceConfig的urls列表")        

id1 --&gt; id2
id2 --否--&gt; id3
id2 --是--&gt; id15

id3 --是--&gt; id4
id3 --否--&gt; id5

id5 --&gt; id6
id6 --&gt; id7
id7 --否--&gt; id8
id8 --&gt; id9
id9 --&gt; id10
id10 --是--&gt; id11
    id11 --&gt; id12
id10 --否--&gt; id12
id12 --&gt; id13
id13 --&gt; id14
id14 --&gt; id15

</code></pre>

<h1 id="导出服务-1">导出服务</h1>

<p>视角转移到<code class="language-plaintext highlighter-rouge">doExportUrlFor1Protocol</code>的最后一段逻辑:</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">if</span> <span class="o">(!</span><span class="no">SCOPE_NONE</span><span class="o">.</span><span class="na">equalsIgnoreCase</span><span class="o">(</span><span class="n">scope</span><span class="o">))</span> <span class="o">{</span> <span class="c1">//如果是SCOPE_NONE,则没必要导出                                                                                       </span>
<span class="cm">/*****************************************************************************************************************************************************************/</span>
<span class="cm">/**/</span><span class="k">if</span> <span class="o">(!</span><span class="no">SCOPE_REMOTE</span><span class="o">.</span><span class="na">equalsIgnoreCase</span><span class="o">(</span><span class="n">scope</span><span class="o">))</span> <span class="o">{</span> <span class="c1">//如果不是SCOPE_REMOTE,则使用exportLocal(url)逻辑                                                               /**/</span>
<span class="cm">/**/</span>    <span class="n">exportLocal</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>                                                                                                                                      <span class="cm">/**/</span>
<span class="cm">/**/</span><span class="o">}</span>                                                                                                                                                          <span class="cm">/**/</span>
<span class="cm">/*****************************************************************************************************************************************************************/</span>
    <span class="k">if</span> <span class="o">(!</span><span class="no">SCOPE_LOCAL</span><span class="o">.</span><span class="na">equalsIgnoreCase</span><span class="o">(</span><span class="n">scope</span><span class="o">))</span> <span class="o">{</span> <span class="c1">// 如果不是导出到本地,则使用导出到远程逻辑</span>
        <span class="k">if</span> <span class="o">(</span><span class="nc">CollectionUtils</span><span class="o">.</span><span class="na">isNotEmpty</span><span class="o">(</span><span class="n">registryURLs</span><span class="o">))</span> <span class="o">{</span>
            <span class="k">for</span> <span class="o">(</span><span class="no">URL</span> <span class="n">registryURL</span> <span class="o">:</span> <span class="n">registryURLs</span><span class="o">)</span> <span class="o">{</span>
                <span class="k">if</span> <span class="o">(</span><span class="no">LOCAL_PROTOCOL</span><span class="o">.</span><span class="na">equalsIgnoreCase</span><span class="o">(</span><span class="n">url</span><span class="o">.</span><span class="na">getProtocol</span><span class="o">()))</span> <span class="o">{</span>
                    <span class="k">continue</span><span class="o">;</span>
                <span class="o">}</span>
                <span class="n">url</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">addParameterIfAbsent</span><span class="o">(</span><span class="no">DYNAMIC_KEY</span><span class="o">,</span> <span class="n">registryURL</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="no">DYNAMIC_KEY</span><span class="o">));</span>
                <span class="no">URL</span> <span class="n">monitorUrl</span> <span class="o">=</span> <span class="nc">ConfigValidationUtils</span><span class="o">.</span><span class="na">loadMonitor</span><span class="o">(</span><span class="k">this</span><span class="o">,</span> <span class="n">registryURL</span><span class="o">);</span>
                <span class="k">if</span> <span class="o">(</span><span class="n">monitorUrl</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
                    <span class="n">url</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">addParameterAndEncoded</span><span class="o">(</span><span class="no">MONITOR_KEY</span><span class="o">,</span> <span class="n">monitorUrl</span><span class="o">.</span><span class="na">toFullString</span><span class="o">());</span>
                <span class="o">}</span>
                <span class="k">if</span> <span class="o">(</span><span class="n">logger</span><span class="o">.</span><span class="na">isInfoEnabled</span><span class="o">())</span> <span class="o">{</span>
                    <span class="k">if</span> <span class="o">(</span><span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="no">REGISTER_KEY</span><span class="o">,</span> <span class="kc">true</span><span class="o">))</span> <span class="o">{</span>
                        <span class="n">logger</span><span class="o">.</span><span class="na">info</span><span class="o">(</span><span class="s">"Register dubbo service "</span> <span class="o">+</span> <span class="n">interfaceClass</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">" url "</span> <span class="o">+</span> <span class="n">url</span> <span class="o">+</span> <span class="s">" to registry "</span> <span class="o">+</span> <span class="n">registryURL</span><span class="o">);</span>
                    <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
                        <span class="n">logger</span><span class="o">.</span><span class="na">info</span><span class="o">(</span><span class="s">"Export dubbo service "</span> <span class="o">+</span> <span class="n">interfaceClass</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">" to url "</span> <span class="o">+</span> <span class="n">url</span><span class="o">);</span>
                    <span class="o">}</span>
                <span class="o">}</span>

                <span class="c1">// For providers, this is used to enable custom proxy to generate invoker</span>
                <span class="nc">String</span> <span class="n">proxy</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="no">PROXY_KEY</span><span class="o">);</span>
                <span class="k">if</span> <span class="o">(</span><span class="nc">StringUtils</span><span class="o">.</span><span class="na">isNotEmpty</span><span class="o">(</span><span class="n">proxy</span><span class="o">))</span> <span class="o">{</span>
                    <span class="n">registryURL</span> <span class="o">=</span> <span class="n">registryURL</span><span class="o">.</span><span class="na">addParameter</span><span class="o">(</span><span class="no">PROXY_KEY</span><span class="o">,</span> <span class="n">proxy</span><span class="o">);</span>
                <span class="o">}</span>
<span class="cm">/*****************************************************************************************************************************************************************/</span>
<span class="cm">/**/</span>            <span class="nc">Invoker</span><span class="o">&lt;?&gt;</span> <span class="n">invoker</span> <span class="o">=</span> <span class="no">PROXY_FACTORY</span><span class="o">.</span><span class="na">getInvoker</span><span class="o">(</span><span class="n">ref</span><span class="o">,</span> <span class="o">(</span><span class="nc">Class</span><span class="o">)</span> <span class="n">interfaceClass</span><span class="o">,</span> <span class="n">registryURL</span><span class="o">.</span><span class="na">addParameterAndEncoded</span><span class="o">(</span><span class="no">EXPORT_KEY</span><span class="o">,</span> <span class="n">url</span><span class="o">.</span><span class="na">toFullString</span><span class="o">()));</span><span class="cm">/**/</span>
<span class="cm">/**/</span>            <span class="nc">DelegateProviderMetaDataInvoker</span> <span class="n">wrapperInvoker</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">DelegateProviderMetaDataInvoker</span><span class="o">(</span><span class="n">invoker</span><span class="o">,</span> <span class="k">this</span><span class="o">);</span>                                           <span class="cm">/**/</span>
<span class="cm">/**/</span>            <span class="nc">Exporter</span><span class="o">&lt;?&gt;</span> <span class="n">exporter</span> <span class="o">=</span> <span class="no">PROTOCOL</span><span class="o">.</span><span class="na">export</span><span class="o">(</span><span class="n">wrapperInvoker</span><span class="o">);</span>                                                                                        <span class="cm">/**/</span>
<span class="cm">/**/</span>            <span class="n">exporters</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">exporter</span><span class="o">);</span>                                                                                                                       <span class="cm">/**/</span>
<span class="cm">/*****************************************************************************************************************************************************************/</span>
            <span class="o">}</span>
        <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">logger</span><span class="o">.</span><span class="na">isInfoEnabled</span><span class="o">())</span> <span class="o">{</span>
                <span class="n">logger</span><span class="o">.</span><span class="na">info</span><span class="o">(</span><span class="s">"Export dubbo service "</span> <span class="o">+</span> <span class="n">interfaceClass</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">" to url "</span> <span class="o">+</span> <span class="n">url</span><span class="o">);</span>
            <span class="o">}</span>
<span class="cm">/*****************************************************************************************************************************************************************/</span>
<span class="cm">/**/</span>        <span class="nc">Invoker</span><span class="o">&lt;?&gt;</span> <span class="n">invoker</span> <span class="o">=</span> <span class="no">PROXY_FACTORY</span><span class="o">.</span><span class="na">getInvoker</span><span class="o">(</span><span class="n">ref</span><span class="o">,</span> <span class="o">(</span><span class="nc">Class</span><span class="o">)</span> <span class="n">interfaceClass</span><span class="o">,</span> <span class="n">url</span><span class="o">);</span>                                                                   <span class="cm">/**/</span>
<span class="cm">/**/</span>        <span class="nc">DelegateProviderMetaDataInvoker</span> <span class="n">wrapperInvoker</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">DelegateProviderMetaDataInvoker</span><span class="o">(</span><span class="n">invoker</span><span class="o">,</span> <span class="k">this</span><span class="o">);</span>                                               <span class="cm">/**/</span>
<span class="cm">/**/</span>        <span class="nc">Exporter</span><span class="o">&lt;?&gt;</span> <span class="n">exporter</span> <span class="o">=</span> <span class="no">PROTOCOL</span><span class="o">.</span><span class="na">export</span><span class="o">(</span><span class="n">wrapperInvoker</span><span class="o">);</span>                                                                                            <span class="cm">/**/</span>
<span class="cm">/**/</span>        <span class="n">exporters</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">exporter</span><span class="o">);</span>                                                                                                                           <span class="cm">/**/</span>
<span class="cm">/*****************************************************************************************************************************************************************/</span>
        <span class="o">}</span>
        <span class="o">...</span>
    <span class="o">}</span>
    <span class="o">...</span>
<span class="o">}</span>
<span class="o">...</span>
</code></pre></div></div>

<h2 id="导出服务到本地">导出服务到本地</h2>

<p>如果没有使用<code class="language-plaintext highlighter-rouge">serviceConfig.setScope("remote")</code>,会启用导出到本地的逻辑</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">interface</span> <span class="nc">A</span><span class="o">{</span>

<span class="o">}</span>

<span class="kd">class</span> <span class="nc">B</span> <span class="kd">implements</span> <span class="no">A</span><span class="o">{</span>

<span class="o">}</span>

<span class="kd">public</span> <span class="kd">class</span> <span class="nc">DemoApplication</span> <span class="o">{</span>
	<span class="kd">public</span> <span class="kd">static</span> <span class="kt">void</span> <span class="nf">main</span><span class="o">(</span><span class="nc">String</span><span class="o">[]</span> <span class="n">args</span><span class="o">)</span><span class="kd">throws</span> <span class="nc">Exception</span><span class="o">{</span>
        <span class="no">B</span> <span class="n">b</span> <span class="o">=</span> <span class="k">new</span> <span class="no">B</span><span class="o">();</span>

        <span class="nc">ApplicationConfig</span> <span class="n">applicationConfig</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ApplicationConfig</span><span class="o">();</span>
        <span class="n">applicationConfig</span><span class="o">.</span><span class="na">setName</span><span class="o">(</span><span class="s">"MyApp"</span><span class="o">);</span>

        <span class="nc">RegistryConfig</span> <span class="n">registryConfig</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">RegistryConfig</span><span class="o">();</span>
        <span class="n">registryConfig</span><span class="o">.</span><span class="na">setAddress</span><span class="o">(</span><span class="s">"10.20.130.230:9090"</span><span class="o">);</span>

        <span class="nc">ProtocolConfig</span> <span class="n">protocolConfig</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ProtocolConfig</span><span class="o">();</span>
        <span class="n">protocolConfig</span><span class="o">.</span><span class="na">setName</span><span class="o">(</span><span class="s">"dubbo"</span><span class="o">);</span>
        <span class="n">protocolConfig</span><span class="o">.</span><span class="na">setPort</span><span class="o">(</span><span class="mi">123</span><span class="o">);</span>
        <span class="n">protocolConfig</span><span class="o">.</span><span class="na">setThreads</span><span class="o">(</span><span class="mi">123</span><span class="o">);</span>

        <span class="nc">ServiceConfig</span> <span class="n">serviceConfig</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ServiceConfig</span><span class="o">();</span>
        <span class="n">serviceConfig</span><span class="o">.</span><span class="na">setRef</span><span class="o">(</span><span class="n">b</span><span class="o">);</span>
        <span class="n">serviceConfig</span><span class="o">.</span><span class="na">setInterface</span><span class="o">(</span><span class="no">A</span><span class="o">.</span><span class="na">class</span><span class="o">);</span>
        <span class="c1">//serviceConfig.setScope("remote");</span>
        
        <span class="n">serviceConfig</span><span class="o">.</span><span class="na">setRegistry</span><span class="o">(</span><span class="n">registryConfig</span><span class="o">);</span>
        <span class="n">serviceConfig</span><span class="o">.</span><span class="na">setApplication</span><span class="o">(</span><span class="n">applicationConfig</span><span class="o">);</span>
        <span class="n">serviceConfig</span><span class="o">.</span><span class="na">setProtocol</span><span class="o">(</span><span class="n">protocolConfig</span><span class="o">);</span>
        
        <span class="n">serviceConfig</span><span class="o">.</span><span class="na">export</span><span class="o">();</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<p>最终到达<code class="language-plaintext highlighter-rouge">doExportUrlFor1Protocol()</code>时候会达到下面的分支:</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">if</span> <span class="o">(!</span><span class="no">SCOPE_REMOTE</span><span class="o">.</span><span class="na">equalsIgnoreCase</span><span class="o">(</span><span class="n">scope</span><span class="o">))</span> <span class="o">{</span> <span class="c1">//如果不是SCOPE_REMOTE,则使用exportLocal(url)逻辑</span>
    <span class="n">exportLocal</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
<span class="o">}</span>
</code></pre></div></div>

<p>在<code class="language-plaintext highlighter-rouge">exportLocal()</code>设置一个断点,运行到此时的<code class="language-plaintext highlighter-rouge">URL</code>为:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>dubbo://169.254.161.27:123/com.example.demo.A?anyhost=true&amp;application=MyApp&amp;bind.ip=169.254.161.27&amp;bind.port=123&amp;deprecated=false&amp;dubbo=2.0.2&amp;dynamic=true&amp;generic=false&amp;interface=com.example.demo.A&amp;methods=*&amp;pid=10224&amp;release=2.7.8&amp;side=provider&amp;threads=123&amp;timestamp=1602140887001
</code></pre></div></div>

<p>可以看到这个时候导出的格式还是<code class="language-plaintext highlighter-rouge">dubbo</code>协议,深入到<code class="language-plaintext highlighter-rouge">exportLocal()</code>函数内部</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">private</span> <span class="kt">void</span> <span class="nf">exportLocal</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">)</span> <span class="o">{</span>
    <span class="no">URL</span> <span class="n">local</span> <span class="o">=</span> <span class="nc">URLBuilder</span><span class="o">.</span><span class="na">from</span><span class="o">(</span><span class="n">url</span><span class="o">)</span>
            <span class="o">.</span><span class="na">setProtocol</span><span class="o">(</span><span class="no">LOCAL_PROTOCOL</span><span class="o">)</span>
            <span class="o">.</span><span class="na">setHost</span><span class="o">(</span><span class="no">LOCALHOST_VALUE</span><span class="o">)</span>
            <span class="o">.</span><span class="na">setPort</span><span class="o">(</span><span class="mi">0</span><span class="o">)</span>
            <span class="o">.</span><span class="na">build</span><span class="o">();</span>
    <span class="nc">Exporter</span><span class="o">&lt;?&gt;</span> <span class="n">exporter</span> <span class="o">=</span> <span class="no">PROTOCOL</span><span class="o">.</span><span class="na">export</span><span class="o">(</span>
            <span class="no">PROXY_FACTORY</span><span class="o">.</span><span class="na">getInvoker</span><span class="o">(</span><span class="n">ref</span><span class="o">,</span> <span class="o">(</span><span class="nc">Class</span><span class="o">)</span> <span class="n">interfaceClass</span><span class="o">,</span> <span class="n">local</span><span class="o">));</span>
    <span class="n">exporters</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">exporter</span><span class="o">);</span>
    <span class="n">logger</span><span class="o">.</span><span class="na">info</span><span class="o">(</span><span class="s">"Export dubbo service "</span> <span class="o">+</span> <span class="n">interfaceClass</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">" to local registry url : "</span> <span class="o">+</span> <span class="n">local</span><span class="o">);</span>
<span class="o">}</span>
</code></pre></div></div>

<p>在这个时候<code class="language-plaintext highlighter-rouge">local</code>变量就变成了:</p>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>injvm://127.0.0.1/com.example.demo.A?anyhost=true&amp;application=MyApp&amp;bind.ip=169.254.161.27&amp;bind.port=123&amp;deprecated=false&amp;dubbo=2.0.2&amp;dynamic=true&amp;generic=false&amp;interface=com.example.demo.A&amp;methods=*&amp;pid=10224&amp;release=2.7.8&amp;side=provider&amp;threads=123&amp;timestamp=1602140887001
</code></pre></div></div>
<p>这个时候就导出协议就变成了<code class="language-plaintext highlighter-rouge">injvm</code>协议,将会调用<code class="language-plaintext highlighter-rouge">InjvmProtocol</code>进行导出</p>

<h3 id="protocolexport">PROTOCOL.export(…)</h3>

<h2 id="导出服务到远程">导出服务到远程</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">serviceConfig</span><span class="o">.</span><span class="na">setScope</span><span class="o">(</span><span class="s">"remote"</span><span class="o">)</span>
</code></pre></div></div>

<h3 id="proxy_factorygetinvoker">PROXY_FACTORY.getInvoker(…)</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">private</span> <span class="kd">static</span> <span class="kd">final</span> <span class="nc">ProxyFactory</span> <span class="no">PROXY_FACTORY</span> <span class="o">=</span> <span class="nc">ExtensionLoader</span><span class="o">.</span><span class="na">getExtensionLoader</span><span class="o">(</span><span class="nc">ProxyFactory</span><span class="o">.</span><span class="na">class</span><span class="o">).</span><span class="na">getAdaptiveExtension</span><span class="o">();</span>
<span class="cm">/***************************************************************/</span>
<span class="nd">@SPI</span><span class="o">(</span><span class="s">"javassist"</span><span class="o">)</span>
<span class="kd">public</span> <span class="kd">interface</span> <span class="nc">ProxyFactory</span> <span class="o">{...}</span>
</code></pre></div></div>
<p>可以看出Dubbo默认的<code class="language-plaintext highlighter-rouge">PROXY_FACTORY</code>是<code class="language-plaintext highlighter-rouge">JavassistProxyFactory</code></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">class</span> <span class="nc">JavassistProxyFactory</span> <span class="kd">extends</span> <span class="nc">AbstractProxyFactory</span> <span class="o">{</span>

    <span class="nd">@Override</span>
    <span class="nd">@SuppressWarnings</span><span class="o">(</span><span class="s">"unchecked"</span><span class="o">)</span>
    <span class="kd">public</span> <span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="no">T</span> <span class="nf">getProxy</span><span class="o">(</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">invoker</span><span class="o">,</span> <span class="nc">Class</span><span class="o">&lt;?&gt;[]</span> <span class="n">interfaces</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">return</span> <span class="o">(</span><span class="no">T</span><span class="o">)</span> <span class="nc">Proxy</span><span class="o">.</span><span class="na">getProxy</span><span class="o">(</span><span class="n">interfaces</span><span class="o">).</span><span class="na">newInstance</span><span class="o">(</span><span class="k">new</span> <span class="nc">InvokerInvocationHandler</span><span class="o">(</span><span class="n">invoker</span><span class="o">));</span>
    <span class="o">}</span>

    <span class="nd">@Override</span>
    <span class="kd">public</span> <span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nf">getInvoker</span><span class="o">(</span><span class="no">T</span> <span class="n">proxy</span><span class="o">,</span> <span class="nc">Class</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">type</span><span class="o">,</span> <span class="no">URL</span> <span class="n">url</span><span class="o">)</span> <span class="o">{</span>
        <span class="c1">// TODO Wrapper cannot handle this scenario correctly: the classname contains '$'</span>
        <span class="kd">final</span> <span class="nc">Wrapper</span> <span class="n">wrapper</span> <span class="o">=</span> <span class="nc">Wrapper</span><span class="o">.</span><span class="na">getWrapper</span><span class="o">(</span><span class="n">proxy</span><span class="o">.</span><span class="na">getClass</span><span class="o">().</span><span class="na">getName</span><span class="o">().</span><span class="na">indexOf</span><span class="o">(</span><span class="sc">'$'</span><span class="o">)</span> <span class="o">&lt;</span> <span class="mi">0</span> <span class="o">?</span> <span class="n">proxy</span><span class="o">.</span><span class="na">getClass</span><span class="o">()</span> <span class="o">:</span> <span class="n">type</span><span class="o">);</span>
        <span class="k">return</span> <span class="k">new</span> <span class="nc">AbstractProxyInvoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;(</span><span class="n">proxy</span><span class="o">,</span> <span class="n">type</span><span class="o">,</span> <span class="n">url</span><span class="o">)</span> <span class="o">{</span>
            <span class="nd">@Override</span>
            <span class="kd">protected</span> <span class="nc">Object</span> <span class="nf">doInvoke</span><span class="o">(</span><span class="no">T</span> <span class="n">proxy</span><span class="o">,</span> <span class="nc">String</span> <span class="n">methodName</span><span class="o">,</span>
                                      <span class="nc">Class</span><span class="o">&lt;?&gt;[]</span> <span class="n">parameterTypes</span><span class="o">,</span>
                                      <span class="nc">Object</span><span class="o">[]</span> <span class="n">arguments</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">Throwable</span> <span class="o">{</span>
                <span class="k">return</span> <span class="n">wrapper</span><span class="o">.</span><span class="na">invokeMethod</span><span class="o">(</span><span class="n">proxy</span><span class="o">,</span> <span class="n">methodName</span><span class="o">,</span> <span class="n">parameterTypes</span><span class="o">,</span> <span class="n">arguments</span><span class="o">);</span>
            <span class="o">}</span>
        <span class="o">};</span>
    <span class="o">}</span>

<span class="o">}</span>
</code></pre></div></div>

<blockquote>

  <p>从<code class="language-plaintext highlighter-rouge">JavassistProxyFactory.getInvoker(...)</code>的实现可以看出其逻辑:</p>
  <ul>
    <li>创建一个代理类<code class="language-plaintext highlighter-rouge">Wrapper</code></li>
    <li>根据<code class="language-plaintext highlighter-rouge">Wrapper</code>创建<code class="language-plaintext highlighter-rouge">Invoker</code></li>
  </ul>
</blockquote>

<h3 id="wrappergetwrapper">Wrapper.getWrapper(…)</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code> <span class="kd">public</span> <span class="kd">static</span> <span class="nc">Wrapper</span> <span class="nf">getWrapper</span><span class="o">(</span><span class="nc">Class</span><span class="o">&lt;?&gt;</span> <span class="n">c</span><span class="o">)</span> <span class="o">{</span>	
    <span class="k">while</span> <span class="o">(</span><span class="nc">ClassGenerator</span><span class="o">.</span><span class="na">isDynamicClass</span><span class="o">(</span><span class="n">c</span><span class="o">))</span>
        <span class="n">c</span> <span class="o">=</span> <span class="n">c</span><span class="o">.</span><span class="na">getSuperclass</span><span class="o">();</span>

    <span class="k">if</span> <span class="o">(</span><span class="n">c</span> <span class="o">==</span> <span class="nc">Object</span><span class="o">.</span><span class="na">class</span><span class="o">)</span>
        <span class="k">return</span> <span class="no">OBJECT_WRAPPER</span><span class="o">;</span>

    <span class="c1">// 从缓存中获取 Wrapper 实例</span>
    <span class="nc">Wrapper</span> <span class="n">ret</span> <span class="o">=</span> <span class="no">WRAPPER_MAP</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">c</span><span class="o">);</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">ret</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
        <span class="c1">// 缓存未命中，创建 Wrapper</span>
        <span class="n">ret</span> <span class="o">=</span> <span class="n">makeWrapper</span><span class="o">(</span><span class="n">c</span><span class="o">);</span>
        <span class="c1">// 写入缓存</span>
        <span class="no">WRAPPER_MAP</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">c</span><span class="o">,</span> <span class="n">ret</span><span class="o">);</span>
    <span class="o">}</span>
    <span class="k">return</span> <span class="n">ret</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>

<p>这一段的逻辑很简单,一个简单的缓存检查,如果没有则调用<code class="language-plaintext highlighter-rouge">makeWrapper(...)</code>创建<code class="language-plaintext highlighter-rouge">Wrapper</code><br />
又把思路引到了<code class="language-plaintext highlighter-rouge">makeWrapper</code>上<br />
但是由于<code class="language-plaintext highlighter-rouge">makeWrapper(...)</code>的函数也很长,这里也分段分析</p>

<h3 id="wrappermakewrapper">Wrapper.makeWrapper(…)</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">private</span> <span class="kd">static</span> <span class="nc">Wrapper</span> <span class="nf">makeWrapper</span><span class="o">(</span><span class="nc">Class</span><span class="o">&lt;?&gt;</span> <span class="n">c</span><span class="o">)</span> <span class="o">{</span>
    <span class="c1">// 检测 c 是否为基本类型，若是则抛出异常</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">c</span><span class="o">.</span><span class="na">isPrimitive</span><span class="o">())</span>
        <span class="k">throw</span> <span class="k">new</span> <span class="nf">IllegalArgumentException</span><span class="o">(</span><span class="s">"Can not create wrapper for primitive type: "</span> <span class="o">+</span> <span class="n">c</span><span class="o">);</span>

    <span class="nc">String</span> <span class="n">name</span> <span class="o">=</span> <span class="n">c</span><span class="o">.</span><span class="na">getName</span><span class="o">();</span>
    <span class="nc">ClassLoader</span> <span class="n">cl</span> <span class="o">=</span> <span class="nc">ClassHelper</span><span class="o">.</span><span class="na">getClassLoader</span><span class="o">(</span><span class="n">c</span><span class="o">);</span>

    <span class="c1">// c1 用于存储 setPropertyValue 方法代码</span>
    <span class="nc">StringBuilder</span> <span class="n">c1</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">StringBuilder</span><span class="o">(</span><span class="s">"public void setPropertyValue(Object o, String n, Object v){ "</span><span class="o">);</span>
    <span class="c1">// c2 用于存储 getPropertyValue 方法代码</span>
    <span class="nc">StringBuilder</span> <span class="n">c2</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">StringBuilder</span><span class="o">(</span><span class="s">"public Object getPropertyValue(Object o, String n){ "</span><span class="o">);</span>
    <span class="c1">// c3 用于存储 invokeMethod 方法代码</span>
    <span class="nc">StringBuilder</span> <span class="n">c3</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">StringBuilder</span><span class="o">(</span><span class="s">"public Object invokeMethod(Object o, String n, Class[] p, Object[] v) throws "</span> <span class="o">+</span> <span class="nc">InvocationTargetException</span><span class="o">.</span><span class="na">class</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">"{ "</span><span class="o">);</span>

    <span class="c1">// 生成类型转换代码及异常捕捉代码，比如：</span>
    <span class="c1">//   DemoService w; try { w = ((DemoServcie) $1); }}catch(Throwable e){ throw new IllegalArgumentException(e); }</span>
    <span class="n">c1</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="n">name</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">" w; try{ w = (("</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">name</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">")$1); }catch(Throwable e){ throw new IllegalArgumentException(e); }"</span><span class="o">);</span>
    <span class="n">c2</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="n">name</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">" w; try{ w = (("</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">name</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">")$1); }catch(Throwable e){ throw new IllegalArgumentException(e); }"</span><span class="o">);</span>
    <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="n">name</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">" w; try{ w = (("</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">name</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">")$1); }catch(Throwable e){ throw new IllegalArgumentException(e); }"</span><span class="o">);</span>

    <span class="c1">// pts 用于存储成员变量名和类型</span>
    <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Class</span><span class="o">&lt;?&gt;&gt;</span> <span class="n">pts</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">HashMap</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Class</span><span class="o">&lt;?&gt;&gt;();</span>
    <span class="c1">// ms 用于存储方法描述信息（可理解为方法签名）及 Method 实例</span>
    <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Method</span><span class="o">&gt;</span> <span class="n">ms</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">LinkedHashMap</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Method</span><span class="o">&gt;();</span>
    <span class="c1">// mns 为方法名列表</span>
    <span class="nc">List</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;</span> <span class="n">mns</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ArrayList</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;();</span>
    <span class="c1">// dmns 用于存储“定义在当前类中的方法”的名称</span>
    <span class="nc">List</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;</span> <span class="n">dmns</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ArrayList</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;();</span>

    <span class="c1">// --------------------------------✨ 分割线1 ✨-------------------------------------</span>

    <span class="c1">// 获取 public 访问级别的字段，并为所有字段生成条件判断语句</span>
    <span class="k">for</span> <span class="o">(</span><span class="nc">Field</span> <span class="n">f</span> <span class="o">:</span> <span class="n">c</span><span class="o">.</span><span class="na">getFields</span><span class="o">())</span> <span class="o">{</span>
        <span class="nc">String</span> <span class="n">fn</span> <span class="o">=</span> <span class="n">f</span><span class="o">.</span><span class="na">getName</span><span class="o">();</span>
        <span class="nc">Class</span><span class="o">&lt;?&gt;</span> <span class="n">ft</span> <span class="o">=</span> <span class="n">f</span><span class="o">.</span><span class="na">getType</span><span class="o">();</span>
        <span class="k">if</span> <span class="o">(</span><span class="nc">Modifier</span><span class="o">.</span><span class="na">isStatic</span><span class="o">(</span><span class="n">f</span><span class="o">.</span><span class="na">getModifiers</span><span class="o">())</span> <span class="o">||</span> <span class="nc">Modifier</span><span class="o">.</span><span class="na">isTransient</span><span class="o">(</span><span class="n">f</span><span class="o">.</span><span class="na">getModifiers</span><span class="o">()))</span>
            <span class="c1">// 忽略关键字 static 或 transient 修饰的变量</span>
            <span class="k">continue</span><span class="o">;</span>

        <span class="c1">// 生成条件判断及赋值语句，比如：</span>
        <span class="c1">// if( $2.equals("name") ) { w.name = (java.lang.String) $3; return;}</span>
        <span class="c1">// if( $2.equals("age") ) { w.age = ((Number) $3).intValue(); return;}</span>
        <span class="n">c1</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" if( $2.equals(\""</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">fn</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">"\") ){ w."</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">fn</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">"="</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">arg</span><span class="o">(</span><span class="n">ft</span><span class="o">,</span> <span class="s">"$3"</span><span class="o">)).</span><span class="na">append</span><span class="o">(</span><span class="s">"; return; }"</span><span class="o">);</span>

        <span class="c1">// 生成条件判断及返回语句，比如：</span>
        <span class="c1">// if( $2.equals("name") ) { return ($w)w.name; }</span>
        <span class="n">c2</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" if( $2.equals(\""</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">fn</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">"\") ){ return ($w)w."</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">fn</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">"; }"</span><span class="o">);</span>

        <span class="c1">// 存储 &lt;字段名, 字段类型&gt; 键值对到 pts 中</span>
        <span class="n">pts</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">fn</span><span class="o">,</span> <span class="n">ft</span><span class="o">);</span>
    <span class="o">}</span>

    <span class="c1">// --------------------------------✨ 分割线2 ✨-------------------------------------</span>

    <span class="nc">Method</span><span class="o">[]</span> <span class="n">methods</span> <span class="o">=</span> <span class="n">c</span><span class="o">.</span><span class="na">getMethods</span><span class="o">();</span>
    <span class="c1">// 检测 c 中是否包含在当前类中声明的方法</span>
    <span class="kt">boolean</span> <span class="n">hasMethod</span> <span class="o">=</span> <span class="n">hasMethods</span><span class="o">(</span><span class="n">methods</span><span class="o">);</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">hasMethod</span><span class="o">)</span> <span class="o">{</span>
        <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" try{"</span><span class="o">);</span>
    <span class="o">}</span>
    <span class="k">for</span> <span class="o">(</span><span class="nc">Method</span> <span class="n">m</span> <span class="o">:</span> <span class="n">methods</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">m</span><span class="o">.</span><span class="na">getDeclaringClass</span><span class="o">()</span> <span class="o">==</span> <span class="nc">Object</span><span class="o">.</span><span class="na">class</span><span class="o">)</span>
            <span class="c1">// 忽略 Object 中定义的方法</span>
            <span class="k">continue</span><span class="o">;</span>

        <span class="nc">String</span> <span class="n">mn</span> <span class="o">=</span> <span class="n">m</span><span class="o">.</span><span class="na">getName</span><span class="o">();</span>
        <span class="c1">// 生成方法名判断语句，比如：</span>
        <span class="c1">// if ( "sayHello".equals( $2 )</span>
        <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" if( \""</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">mn</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">"\".equals( $2 ) "</span><span class="o">);</span>
        <span class="kt">int</span> <span class="n">len</span> <span class="o">=</span> <span class="n">m</span><span class="o">.</span><span class="na">getParameterTypes</span><span class="o">().</span><span class="na">length</span><span class="o">;</span>
        <span class="c1">// 生成“运行时传入的参数数量与方法参数列表长度”判断语句，比如：</span>
        <span class="c1">// &amp;&amp; $3.length == 2</span>
        <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" &amp;&amp; "</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">" $3.length == "</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">len</span><span class="o">);</span>

        <span class="kt">boolean</span> <span class="n">override</span> <span class="o">=</span> <span class="kc">false</span><span class="o">;</span>
        <span class="k">for</span> <span class="o">(</span><span class="nc">Method</span> <span class="n">m2</span> <span class="o">:</span> <span class="n">methods</span><span class="o">)</span> <span class="o">{</span>
            <span class="c1">// 检测方法是否存在重载情况，条件为：方法对象不同 &amp;&amp; 方法名相同</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">m</span> <span class="o">!=</span> <span class="n">m2</span> <span class="o">&amp;&amp;</span> <span class="n">m</span><span class="o">.</span><span class="na">getName</span><span class="o">().</span><span class="na">equals</span><span class="o">(</span><span class="n">m2</span><span class="o">.</span><span class="na">getName</span><span class="o">()))</span> <span class="o">{</span>
                <span class="n">override</span> <span class="o">=</span> <span class="kc">true</span><span class="o">;</span>
                <span class="k">break</span><span class="o">;</span>
            <span class="o">}</span>
        <span class="o">}</span>
        <span class="c1">// 对重载方法进行处理，考虑下面的方法：</span>
        <span class="c1">//    1. void sayHello(Integer, String)</span>
        <span class="c1">//    2. void sayHello(Integer, Integer)</span>
        <span class="c1">// 方法名相同，参数列表长度也相同，因此不能仅通过这两项判断两个方法是否相等。</span>
        <span class="c1">// 需要进一步判断方法的参数类型</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">override</span><span class="o">)</span> <span class="o">{</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">len</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
                <span class="k">for</span> <span class="o">(</span><span class="kt">int</span> <span class="n">l</span> <span class="o">=</span> <span class="mi">0</span><span class="o">;</span> <span class="n">l</span> <span class="o">&lt;</span> <span class="n">len</span><span class="o">;</span> <span class="n">l</span><span class="o">++)</span> <span class="o">{</span>
                    <span class="c1">// 生成参数类型进行检测代码，比如：</span>
                    <span class="c1">// &amp;&amp; $3[0].getName().equals("java.lang.Integer") </span>
                    <span class="c1">//    &amp;&amp; $3[1].getName().equals("java.lang.String")</span>
                    <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" &amp;&amp; "</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">" $3["</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">l</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">"].getName().equals(\""</span><span class="o">)</span>
                            <span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="n">m</span><span class="o">.</span><span class="na">getParameterTypes</span><span class="o">()[</span><span class="n">l</span><span class="o">].</span><span class="na">getName</span><span class="o">()).</span><span class="na">append</span><span class="o">(</span><span class="s">"\")"</span><span class="o">);</span>
                <span class="o">}</span>
            <span class="o">}</span>
        <span class="o">}</span>

        <span class="c1">// 添加 ) {，完成方法判断语句，此时生成的代码可能如下（已格式化）：</span>
        <span class="c1">// if ("sayHello".equals($2) </span>
        <span class="c1">//     &amp;&amp; $3.length == 2</span>
        <span class="c1">//     &amp;&amp; $3[0].getName().equals("java.lang.Integer") </span>
        <span class="c1">//     &amp;&amp; $3[1].getName().equals("java.lang.String")) {</span>
        <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" ) { "</span><span class="o">);</span>

        <span class="c1">// 根据返回值类型生成目标方法调用语句</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">m</span><span class="o">.</span><span class="na">getReturnType</span><span class="o">()</span> <span class="o">==</span> <span class="nc">Void</span><span class="o">.</span><span class="na">TYPE</span><span class="o">)</span>
            <span class="c1">// w.sayHello((java.lang.Integer)$4[0], (java.lang.String)$4[1]); return null;</span>
            <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" w."</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">mn</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="sc">'('</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">args</span><span class="o">(</span><span class="n">m</span><span class="o">.</span><span class="na">getParameterTypes</span><span class="o">(),</span> <span class="s">"$4"</span><span class="o">)).</span><span class="na">append</span><span class="o">(</span><span class="s">");"</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">" return null;"</span><span class="o">);</span>
        <span class="k">else</span>
            <span class="c1">// return w.sayHello((java.lang.Integer)$4[0], (java.lang.String)$4[1]);</span>
            <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" return ($w)w."</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">mn</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="sc">'('</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">args</span><span class="o">(</span><span class="n">m</span><span class="o">.</span><span class="na">getParameterTypes</span><span class="o">(),</span> <span class="s">"$4"</span><span class="o">)).</span><span class="na">append</span><span class="o">(</span><span class="s">");"</span><span class="o">);</span>

        <span class="c1">// 添加 }, 生成的代码形如（已格式化）：</span>
        <span class="c1">// if ("sayHello".equals($2) </span>
        <span class="c1">//     &amp;&amp; $3.length == 2</span>
        <span class="c1">//     &amp;&amp; $3[0].getName().equals("java.lang.Integer") </span>
        <span class="c1">//     &amp;&amp; $3[1].getName().equals("java.lang.String")) {</span>
        <span class="c1">//</span>
        <span class="c1">//     w.sayHello((java.lang.Integer)$4[0], (java.lang.String)$4[1]); </span>
        <span class="c1">//     return null;</span>
        <span class="c1">// }</span>
        <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" }"</span><span class="o">);</span>

        <span class="c1">// 添加方法名到 mns 集合中</span>
        <span class="n">mns</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">mn</span><span class="o">);</span>
        <span class="c1">// 检测当前方法是否在 c 中被声明的</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">m</span><span class="o">.</span><span class="na">getDeclaringClass</span><span class="o">()</span> <span class="o">==</span> <span class="n">c</span><span class="o">)</span>
            <span class="c1">// 若是，则将当前方法名添加到 dmns 中</span>
            <span class="n">dmns</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">mn</span><span class="o">);</span>
        <span class="n">ms</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="nc">ReflectUtils</span><span class="o">.</span><span class="na">getDesc</span><span class="o">(</span><span class="n">m</span><span class="o">),</span> <span class="n">m</span><span class="o">);</span>
    <span class="o">}</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">hasMethod</span><span class="o">)</span> <span class="o">{</span>
        <span class="c1">// 添加异常捕捉语句</span>
        <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" } catch(Throwable e) { "</span><span class="o">);</span>
        <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">"     throw new java.lang.reflect.InvocationTargetException(e); "</span><span class="o">);</span>
        <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" }"</span><span class="o">);</span>
    <span class="o">}</span>

    <span class="c1">// 添加 NoSuchMethodException 异常抛出代码</span>
    <span class="n">c3</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" throw new "</span> <span class="o">+</span> <span class="nc">NoSuchMethodException</span><span class="o">.</span><span class="na">class</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">"(\"Not found method \\\"\"+$2+\"\\\" in class "</span> <span class="o">+</span> <span class="n">c</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">".\"); }"</span><span class="o">);</span>

    <span class="c1">// --------------------------------✨ 分割线3 ✨-------------------------------------</span>

    <span class="nc">Matcher</span> <span class="n">matcher</span><span class="o">;</span>
    <span class="c1">// 处理 get/set 方法</span>
    <span class="k">for</span> <span class="o">(</span><span class="nc">Map</span><span class="o">.</span><span class="na">Entry</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Method</span><span class="o">&gt;</span> <span class="n">entry</span> <span class="o">:</span> <span class="n">ms</span><span class="o">.</span><span class="na">entrySet</span><span class="o">())</span> <span class="o">{</span>
        <span class="nc">String</span> <span class="n">md</span> <span class="o">=</span> <span class="n">entry</span><span class="o">.</span><span class="na">getKey</span><span class="o">();</span>
        <span class="nc">Method</span> <span class="n">method</span> <span class="o">=</span> <span class="o">(</span><span class="nc">Method</span><span class="o">)</span> <span class="n">entry</span><span class="o">.</span><span class="na">getValue</span><span class="o">();</span>
        <span class="c1">// 匹配以 get 开头的方法</span>
        <span class="k">if</span> <span class="o">((</span><span class="n">matcher</span> <span class="o">=</span> <span class="nc">ReflectUtils</span><span class="o">.</span><span class="na">GETTER_METHOD_DESC_PATTERN</span><span class="o">.</span><span class="na">matcher</span><span class="o">(</span><span class="n">md</span><span class="o">)).</span><span class="na">matches</span><span class="o">())</span> <span class="o">{</span>
            <span class="c1">// 获取属性名</span>
            <span class="nc">String</span> <span class="n">pn</span> <span class="o">=</span> <span class="n">propertyName</span><span class="o">(</span><span class="n">matcher</span><span class="o">.</span><span class="na">group</span><span class="o">(</span><span class="mi">1</span><span class="o">));</span>
            <span class="c1">// 生成属性判断以及返回语句，示例如下：</span>
            <span class="c1">// if( $2.equals("name") ) { return ($w).w.getName(); }</span>
            <span class="n">c2</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" if( $2.equals(\""</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">pn</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">"\") ){ return ($w)w."</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">method</span><span class="o">.</span><span class="na">getName</span><span class="o">()).</span><span class="na">append</span><span class="o">(</span><span class="s">"(); }"</span><span class="o">);</span>
            <span class="n">pts</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">pn</span><span class="o">,</span> <span class="n">method</span><span class="o">.</span><span class="na">getReturnType</span><span class="o">());</span>

        <span class="c1">// 匹配以 is/has/can 开头的方法</span>
        <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">((</span><span class="n">matcher</span> <span class="o">=</span> <span class="nc">ReflectUtils</span><span class="o">.</span><span class="na">IS_HAS_CAN_METHOD_DESC_PATTERN</span><span class="o">.</span><span class="na">matcher</span><span class="o">(</span><span class="n">md</span><span class="o">)).</span><span class="na">matches</span><span class="o">())</span> <span class="o">{</span>
            <span class="nc">String</span> <span class="n">pn</span> <span class="o">=</span> <span class="n">propertyName</span><span class="o">(</span><span class="n">matcher</span><span class="o">.</span><span class="na">group</span><span class="o">(</span><span class="mi">1</span><span class="o">));</span>
            <span class="c1">// 生成属性判断以及返回语句，示例如下：</span>
            <span class="c1">// if( $2.equals("dream") ) { return ($w).w.hasDream(); }</span>
            <span class="n">c2</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" if( $2.equals(\""</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">pn</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">"\") ){ return ($w)w."</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">method</span><span class="o">.</span><span class="na">getName</span><span class="o">()).</span><span class="na">append</span><span class="o">(</span><span class="s">"(); }"</span><span class="o">);</span>
            <span class="n">pts</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">pn</span><span class="o">,</span> <span class="n">method</span><span class="o">.</span><span class="na">getReturnType</span><span class="o">());</span>

        <span class="c1">// 匹配以 set 开头的方法</span>
        <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">((</span><span class="n">matcher</span> <span class="o">=</span> <span class="nc">ReflectUtils</span><span class="o">.</span><span class="na">SETTER_METHOD_DESC_PATTERN</span><span class="o">.</span><span class="na">matcher</span><span class="o">(</span><span class="n">md</span><span class="o">)).</span><span class="na">matches</span><span class="o">())</span> <span class="o">{</span>
            <span class="nc">Class</span><span class="o">&lt;?&gt;</span> <span class="n">pt</span> <span class="o">=</span> <span class="n">method</span><span class="o">.</span><span class="na">getParameterTypes</span><span class="o">()[</span><span class="mi">0</span><span class="o">];</span>
            <span class="nc">String</span> <span class="n">pn</span> <span class="o">=</span> <span class="n">propertyName</span><span class="o">(</span><span class="n">matcher</span><span class="o">.</span><span class="na">group</span><span class="o">(</span><span class="mi">1</span><span class="o">));</span>
            <span class="c1">// 生成属性判断以及 setter 调用语句，示例如下：</span>
            <span class="c1">// if( $2.equals("name") ) { w.setName((java.lang.String)$3); return; }</span>
            <span class="n">c1</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" if( $2.equals(\""</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">pn</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="s">"\") ){ w."</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">method</span><span class="o">.</span><span class="na">getName</span><span class="o">()).</span><span class="na">append</span><span class="o">(</span><span class="s">"("</span><span class="o">).</span><span class="na">append</span><span class="o">(</span><span class="n">arg</span><span class="o">(</span><span class="n">pt</span><span class="o">,</span> <span class="s">"$3"</span><span class="o">)).</span><span class="na">append</span><span class="o">(</span><span class="s">"); return; }"</span><span class="o">);</span>
            <span class="n">pts</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">pn</span><span class="o">,</span> <span class="n">pt</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>

    <span class="c1">// 添加 NoSuchPropertyException 异常抛出代码</span>
    <span class="n">c1</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" throw new "</span> <span class="o">+</span> <span class="nc">NoSuchPropertyException</span><span class="o">.</span><span class="na">class</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">"(\"Not found property \\\"\"+$2+\"\\\" filed or setter method in class "</span> <span class="o">+</span> <span class="n">c</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">".\"); }"</span><span class="o">);</span>
    <span class="n">c2</span><span class="o">.</span><span class="na">append</span><span class="o">(</span><span class="s">" throw new "</span> <span class="o">+</span> <span class="nc">NoSuchPropertyException</span><span class="o">.</span><span class="na">class</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">"(\"Not found property \\\"\"+$2+\"\\\" filed or setter method in class "</span> <span class="o">+</span> <span class="n">c</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">".\"); }"</span><span class="o">);</span>

    <span class="c1">// --------------------------------✨ 分割线4 ✨-------------------------------------</span>

    <span class="kt">long</span> <span class="n">id</span> <span class="o">=</span> <span class="no">WRAPPER_CLASS_COUNTER</span><span class="o">.</span><span class="na">getAndIncrement</span><span class="o">();</span>
    <span class="c1">// 创建类生成器</span>
    <span class="nc">ClassGenerator</span> <span class="n">cc</span> <span class="o">=</span> <span class="nc">ClassGenerator</span><span class="o">.</span><span class="na">newInstance</span><span class="o">(</span><span class="n">cl</span><span class="o">);</span>
    <span class="c1">// 设置类名及超类</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">setClassName</span><span class="o">((</span><span class="nc">Modifier</span><span class="o">.</span><span class="na">isPublic</span><span class="o">(</span><span class="n">c</span><span class="o">.</span><span class="na">getModifiers</span><span class="o">())</span> <span class="o">?</span> <span class="nc">Wrapper</span><span class="o">.</span><span class="na">class</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">:</span> <span class="n">c</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">"$sw"</span><span class="o">)</span> <span class="o">+</span> <span class="n">id</span><span class="o">);</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">setSuperClass</span><span class="o">(</span><span class="nc">Wrapper</span><span class="o">.</span><span class="na">class</span><span class="o">);</span>

    <span class="c1">// 添加默认构造方法</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addDefaultConstructor</span><span class="o">();</span>

    <span class="c1">// 添加字段</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addField</span><span class="o">(</span><span class="s">"public static String[] pns;"</span><span class="o">);</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addField</span><span class="o">(</span><span class="s">"public static "</span> <span class="o">+</span> <span class="nc">Map</span><span class="o">.</span><span class="na">class</span><span class="o">.</span><span class="na">getName</span><span class="o">()</span> <span class="o">+</span> <span class="s">" pts;"</span><span class="o">);</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addField</span><span class="o">(</span><span class="s">"public static String[] mns;"</span><span class="o">);</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addField</span><span class="o">(</span><span class="s">"public static String[] dmns;"</span><span class="o">);</span>
    <span class="k">for</span> <span class="o">(</span><span class="kt">int</span> <span class="n">i</span> <span class="o">=</span> <span class="mi">0</span><span class="o">,</span> <span class="n">len</span> <span class="o">=</span> <span class="n">ms</span><span class="o">.</span><span class="na">size</span><span class="o">();</span> <span class="n">i</span> <span class="o">&lt;</span> <span class="n">len</span><span class="o">;</span> <span class="n">i</span><span class="o">++)</span>
        <span class="n">cc</span><span class="o">.</span><span class="na">addField</span><span class="o">(</span><span class="s">"public static Class[] mts"</span> <span class="o">+</span> <span class="n">i</span> <span class="o">+</span> <span class="s">";"</span><span class="o">);</span>

    <span class="c1">// 添加方法代码</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addMethod</span><span class="o">(</span><span class="s">"public String[] getPropertyNames(){ return pns; }"</span><span class="o">);</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addMethod</span><span class="o">(</span><span class="s">"public boolean hasProperty(String n){ return pts.containsKey($1); }"</span><span class="o">);</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addMethod</span><span class="o">(</span><span class="s">"public Class getPropertyType(String n){ return (Class)pts.get($1); }"</span><span class="o">);</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addMethod</span><span class="o">(</span><span class="s">"public String[] getMethodNames(){ return mns; }"</span><span class="o">);</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addMethod</span><span class="o">(</span><span class="s">"public String[] getDeclaredMethodNames(){ return dmns; }"</span><span class="o">);</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addMethod</span><span class="o">(</span><span class="n">c1</span><span class="o">.</span><span class="na">toString</span><span class="o">());</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addMethod</span><span class="o">(</span><span class="n">c2</span><span class="o">.</span><span class="na">toString</span><span class="o">());</span>
    <span class="n">cc</span><span class="o">.</span><span class="na">addMethod</span><span class="o">(</span><span class="n">c3</span><span class="o">.</span><span class="na">toString</span><span class="o">());</span>

    <span class="k">try</span> <span class="o">{</span>
        <span class="c1">// 生成类</span>
        <span class="nc">Class</span><span class="o">&lt;?&gt;</span> <span class="n">wc</span> <span class="o">=</span> <span class="n">cc</span><span class="o">.</span><span class="na">toClass</span><span class="o">();</span>
        
        <span class="c1">// 设置字段值</span>
        <span class="n">wc</span><span class="o">.</span><span class="na">getField</span><span class="o">(</span><span class="s">"pts"</span><span class="o">).</span><span class="na">set</span><span class="o">(</span><span class="kc">null</span><span class="o">,</span> <span class="n">pts</span><span class="o">);</span>
        <span class="n">wc</span><span class="o">.</span><span class="na">getField</span><span class="o">(</span><span class="s">"pns"</span><span class="o">).</span><span class="na">set</span><span class="o">(</span><span class="kc">null</span><span class="o">,</span> <span class="n">pts</span><span class="o">.</span><span class="na">keySet</span><span class="o">().</span><span class="na">toArray</span><span class="o">(</span><span class="k">new</span> <span class="nc">String</span><span class="o">[</span><span class="mi">0</span><span class="o">]));</span>
        <span class="n">wc</span><span class="o">.</span><span class="na">getField</span><span class="o">(</span><span class="s">"mns"</span><span class="o">).</span><span class="na">set</span><span class="o">(</span><span class="kc">null</span><span class="o">,</span> <span class="n">mns</span><span class="o">.</span><span class="na">toArray</span><span class="o">(</span><span class="k">new</span> <span class="nc">String</span><span class="o">[</span><span class="mi">0</span><span class="o">]));</span>
        <span class="n">wc</span><span class="o">.</span><span class="na">getField</span><span class="o">(</span><span class="s">"dmns"</span><span class="o">).</span><span class="na">set</span><span class="o">(</span><span class="kc">null</span><span class="o">,</span> <span class="n">dmns</span><span class="o">.</span><span class="na">toArray</span><span class="o">(</span><span class="k">new</span> <span class="nc">String</span><span class="o">[</span><span class="mi">0</span><span class="o">]));</span>
        <span class="kt">int</span> <span class="n">ix</span> <span class="o">=</span> <span class="mi">0</span><span class="o">;</span>
        <span class="k">for</span> <span class="o">(</span><span class="nc">Method</span> <span class="n">m</span> <span class="o">:</span> <span class="n">ms</span><span class="o">.</span><span class="na">values</span><span class="o">())</span>
            <span class="n">wc</span><span class="o">.</span><span class="na">getField</span><span class="o">(</span><span class="s">"mts"</span> <span class="o">+</span> <span class="n">ix</span><span class="o">++).</span><span class="na">set</span><span class="o">(</span><span class="kc">null</span><span class="o">,</span> <span class="n">m</span><span class="o">.</span><span class="na">getParameterTypes</span><span class="o">());</span>

        <span class="c1">// 创建 Wrapper 实例</span>
        <span class="k">return</span> <span class="o">(</span><span class="nc">Wrapper</span><span class="o">)</span> <span class="n">wc</span><span class="o">.</span><span class="na">newInstance</span><span class="o">();</span>
    <span class="o">}</span> <span class="k">catch</span> <span class="o">(</span><span class="nc">RuntimeException</span> <span class="n">e</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">throw</span> <span class="n">e</span><span class="o">;</span>
    <span class="o">}</span> <span class="k">catch</span> <span class="o">(</span><span class="nc">Throwable</span> <span class="n">e</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">throw</span> <span class="k">new</span> <span class="nf">RuntimeException</span><span class="o">(</span><span class="n">e</span><span class="o">.</span><span class="na">getMessage</span><span class="o">(),</span> <span class="n">e</span><span class="o">);</span>
    <span class="o">}</span> <span class="k">finally</span> <span class="o">{</span>
        <span class="n">cc</span><span class="o">.</span><span class="na">release</span><span class="o">();</span>
        <span class="n">ms</span><span class="o">.</span><span class="na">clear</span><span class="o">();</span>
        <span class="n">mns</span><span class="o">.</span><span class="na">clear</span><span class="o">();</span>
        <span class="n">dmns</span><span class="o">.</span><span class="na">clear</span><span class="o">();</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h3 id="protocolexport-1">PROTOCOL.export(…)</h3>

<p>经由<code class="language-plaintext highlighter-rouge">PROXY_FACTORY.getInvoker(...)</code>之后的<code class="language-plaintext highlighter-rouge">Invoker</code>是特殊处理过的,如果这时候<code class="language-plaintext highlighter-rouge">Invoker.getUrl()</code>:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>registry://10.20.130.230:9090/org.apache.dubbo.registry.RegistryService?application=MyApp&amp;dubbo=2.0.2&amp;export=dubbo%3A%2F%2F169.254.161.27%3A123%2Fcom.example.demo.A%3Fanyhost%3Dtrue%26application%3DMyApp%26bind.ip%3D169.254.161.27%26bind.port%3D123%26deprecated%3Dfalse%26dubbo%3D2.0.2%26dynamic%3Dtrue%26generic%3Dfalse%26interface%3Dcom.example.demo.A%26methods%3D*%26pid%3D4636%26release%3D2.7.8%26scope%3Dremote%26side%3Dprovider%26threads%3D123%26timestamp%3D1602141183774&amp;pid=4636&amp;registry=dubbo&amp;release=2.7.8&amp;timestamp=1602141183763
</code></pre></div></div>

<p>很清晰可以看到协议变成了<code class="language-plaintext highlighter-rouge">registry://</code>,原因是<code class="language-plaintext highlighter-rouge">getInvoker(...)</code>在导出为远程时,实参为:</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nc">Invoker</span><span class="o">&lt;?&gt;</span> <span class="n">invoker</span> <span class="o">=</span> <span class="no">PROXY_FACTORY</span><span class="o">.</span><span class="na">getInvoker</span><span class="o">(</span><span class="n">ref</span><span class="o">,</span> <span class="o">(</span><span class="nc">Class</span><span class="o">)</span> <span class="n">interfaceClass</span><span class="o">,</span> <span class="n">registryURL</span><span class="o">.</span><span class="na">addParameterAndEncoded</span><span class="o">(</span><span class="no">EXPORT_KEY</span><span class="o">,</span> <span class="n">url</span><span class="o">.</span><span class="na">toFullString</span><span class="o">()));</span>
</code></pre></div></div>

<p>这个时候已经把<code class="language-plaintext highlighter-rouge">Invoker</code>的url进行了一次封装,这一后面的<code class="language-plaintext highlighter-rouge">PROTOCOL.export(...)</code>由于自适应SPI,就会自动的调用<code class="language-plaintext highlighter-rouge">RegistryProtocol</code></p>

<h1 id="protocolexport-2">PROTOCOL.export(…)</h1>

<h2 id="registryprotocolexport">RegistryProtocol.export(…)</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nc">Exporter</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nf">export</span><span class="o">(</span><span class="kd">final</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">originInvoker</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span> <span class="o">{</span>
    <span class="c1">// 导出服务</span>
    <span class="kd">final</span> <span class="nc">ExporterChangeableWrapper</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">exporter</span> <span class="o">=</span> <span class="n">doLocalExport</span><span class="o">(</span><span class="n">originInvoker</span><span class="o">);</span>

    <span class="c1">// 获取注册中心 URL，以 zookeeper 注册中心为例，得到的示例 URL 如下：</span>
    <span class="c1">// zookeeper://127.0.0.1:2181/com.alibaba.dubbo.registry.RegistryService?application=demo-provider&amp;dubbo=2.0.2&amp;export=dubbo%3A%2F%2F172.17.48.52%3A20880%2Fcom.alibaba.dubbo.demo.DemoService%3Fanyhost%3Dtrue%26application%3Ddemo-provider</span>
    <span class="no">URL</span> <span class="n">registryUrl</span> <span class="o">=</span> <span class="n">getRegistryUrl</span><span class="o">(</span><span class="n">originInvoker</span><span class="o">);</span>

    <span class="c1">// 根据 URL 加载 Registry 实现类，比如 ZookeeperRegistry</span>
    <span class="kd">final</span> <span class="nc">Registry</span> <span class="n">registry</span> <span class="o">=</span> <span class="n">getRegistry</span><span class="o">(</span><span class="n">originInvoker</span><span class="o">);</span>
    
    <span class="c1">// 获取已注册的服务提供者 URL，比如：</span>
    <span class="c1">// dubbo://172.17.48.52:20880/com.alibaba.dubbo.demo.DemoService?anyhost=true&amp;application=demo-provider&amp;dubbo=2.0.2&amp;generic=false&amp;interface=com.alibaba.dubbo.demo.DemoService&amp;methods=sayHello</span>
    <span class="kd">final</span> <span class="no">URL</span> <span class="n">registeredProviderUrl</span> <span class="o">=</span> <span class="n">getRegisteredProviderUrl</span><span class="o">(</span><span class="n">originInvoker</span><span class="o">);</span>

    <span class="c1">// 获取 register 参数</span>
    <span class="kt">boolean</span> <span class="n">register</span> <span class="o">=</span> <span class="n">registeredProviderUrl</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="s">"register"</span><span class="o">,</span> <span class="kc">true</span><span class="o">);</span>

    <span class="c1">// 向服务提供者与消费者注册表中注册服务提供者</span>
    <span class="nc">ProviderConsumerRegTable</span><span class="o">.</span><span class="na">registerProvider</span><span class="o">(</span><span class="n">originInvoker</span><span class="o">,</span> <span class="n">registryUrl</span><span class="o">,</span> <span class="n">registeredProviderUrl</span><span class="o">);</span>

    <span class="c1">// 根据 register 的值决定是否注册服务</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">register</span><span class="o">)</span> <span class="o">{</span>
        <span class="c1">// 向注册中心注册服务</span>
<span class="cm">/**************************************************************************************************************************************************************************************************/</span>
<span class="cm">/**/</span>    <span class="n">register</span><span class="o">(</span><span class="n">registryUrl</span><span class="o">,</span> <span class="n">registeredProviderUrl</span><span class="o">);</span>
<span class="cm">/**/</span>    <span class="nc">ProviderConsumerRegTable</span><span class="o">.</span><span class="na">getProviderWrapper</span><span class="o">(</span><span class="n">originInvoker</span><span class="o">).</span><span class="na">setReg</span><span class="o">(</span><span class="kc">true</span><span class="o">);</span>
<span class="cm">/**/</span><span class="o">}</span>
<span class="cm">/**************************************************************************************************************************************************************************************************/</span>
    <span class="c1">// 获取订阅 URL，比如：</span>
    <span class="c1">// provider://172.17.48.52:20880/com.alibaba.dubbo.demo.DemoService?category=configurators&amp;check=false&amp;anyhost=true&amp;application=demo-provider&amp;dubbo=2.0.2&amp;generic=false&amp;interface=com.alibaba.dubbo.demo.DemoService&amp;methods=sayHello</span>
    <span class="kd">final</span> <span class="no">URL</span> <span class="n">overrideSubscribeUrl</span> <span class="o">=</span> <span class="n">getSubscribedOverrideUrl</span><span class="o">(</span><span class="n">registeredProviderUrl</span><span class="o">);</span>
    <span class="c1">// 创建监听器</span>
    <span class="kd">final</span> <span class="nc">OverrideListener</span> <span class="n">overrideSubscribeListener</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">OverrideListener</span><span class="o">(</span><span class="n">overrideSubscribeUrl</span><span class="o">,</span> <span class="n">originInvoker</span><span class="o">);</span>
    <span class="n">overrideListeners</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">overrideSubscribeUrl</span><span class="o">,</span> <span class="n">overrideSubscribeListener</span><span class="o">);</span>
    <span class="c1">// 向注册中心进行订阅 override 数据</span>
    <span class="n">registry</span><span class="o">.</span><span class="na">subscribe</span><span class="o">(</span><span class="n">overrideSubscribeUrl</span><span class="o">,</span> <span class="n">overrideSubscribeListener</span><span class="o">);</span>
    <span class="c1">// 创建并返回 DestroyableExporter</span>
    <span class="k">return</span> <span class="k">new</span> <span class="nc">DestroyableExporter</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;(</span><span class="n">exporter</span><span class="o">,</span> <span class="n">originInvoker</span><span class="o">,</span> <span class="n">overrideSubscribeUrl</span><span class="o">,</span> <span class="n">registeredProviderUrl</span><span class="o">);</span>
<span class="o">}</span>
</code></pre></div></div>

<p><code class="language-plaintext highlighter-rouge">RegistryProtocol</code>的过程主要由几个部分组成:</p>

<pre><code class="language-mermaid">graph TD
id1("调用doLocalExport(...)向本地导出")
id2("调用register(...)向注册中心注册")
id3("调用registry.subscribe(...)向注册中心订阅")
id4("创建并返回Exporter")

id1 --&gt; id2
id2 --&gt; id3
id3 --&gt; id4
</code></pre>

<h3 id="dolocalexport">doLocalExport(…)</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">private</span> <span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nc">ExporterChangeableWrapper</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nf">doLocalExport</span><span class="o">(</span><span class="kd">final</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">originInvoker</span><span class="o">)</span> <span class="o">{</span>
    <span class="nc">String</span> <span class="n">key</span> <span class="o">=</span> <span class="n">getCacheKey</span><span class="o">(</span><span class="n">originInvoker</span><span class="o">);</span>
    <span class="c1">// 访问缓存</span>
    <span class="nc">ExporterChangeableWrapper</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">exporter</span> <span class="o">=</span> <span class="o">(</span><span class="nc">ExporterChangeableWrapper</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;)</span> <span class="n">bounds</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">key</span><span class="o">);</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">exporter</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
        <span class="kd">synchronized</span> <span class="o">(</span><span class="n">bounds</span><span class="o">)</span> <span class="o">{</span>
            <span class="n">exporter</span> <span class="o">=</span> <span class="o">(</span><span class="nc">ExporterChangeableWrapper</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;)</span> <span class="n">bounds</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">key</span><span class="o">);</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">exporter</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
                <span class="c1">// 创建 Invoker 为委托类对象</span>
                <span class="kd">final</span> <span class="nc">Invoker</span><span class="o">&lt;?&gt;</span> <span class="n">invokerDelegete</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">InvokerDelegete</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;(</span><span class="n">originInvoker</span><span class="o">,</span> <span class="n">getProviderUrl</span><span class="o">(</span><span class="n">originInvoker</span><span class="o">));</span>
                <span class="c1">// 调用 protocol 的 export 方法导出服务</span>
                <span class="n">exporter</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ExporterChangeableWrapper</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;((</span><span class="nc">Exporter</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;)</span> <span class="n">protocol</span><span class="o">.</span><span class="na">export</span><span class="o">(</span><span class="n">invokerDelegete</span><span class="o">),</span> <span class="n">originInvoker</span><span class="o">);</span>
                
                <span class="c1">// 写缓存</span>
                <span class="n">bounds</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">key</span><span class="o">,</span> <span class="n">exporter</span><span class="o">);</span>
            <span class="o">}</span>
        <span class="o">}</span>
    <span class="o">}</span>
    <span class="k">return</span> <span class="n">exporter</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>

<p>一段典型的并发双重检查,检查缓存池是否有<code class="language-plaintext highlighter-rouge">ExporterChangeableWrapper</code>,如果没有则创建<code class="language-plaintext highlighter-rouge">Exporter</code><br />
这里的<code class="language-plaintext highlighter-rouge">protocol.export(...)</code>就是调用的<code class="language-plaintext highlighter-rouge">DubboProtocol</code></p>

<h2 id="dubboprotocol">DubboProtocol</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nc">Exporter</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nf">export</span><span class="o">(</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">invoker</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span> <span class="o">{</span>
    <span class="no">URL</span> <span class="n">url</span> <span class="o">=</span> <span class="n">invoker</span><span class="o">.</span><span class="na">getUrl</span><span class="o">();</span>

    <span class="c1">// 获取服务标识，理解成服务坐标也行。由服务组名，服务名，服务版本号以及端口组成。比如：</span>
    <span class="c1">// demoGroup/com.alibaba.dubbo.demo.DemoService:1.0.1:20880</span>
    <span class="nc">String</span> <span class="n">key</span> <span class="o">=</span> <span class="n">serviceKey</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
    <span class="c1">// 创建 DubboExporter</span>
    <span class="nc">DubboExporter</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">exporter</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">DubboExporter</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;(</span><span class="n">invoker</span><span class="o">,</span> <span class="n">key</span><span class="o">,</span> <span class="n">exporterMap</span><span class="o">);</span>
    <span class="c1">// 将 &lt;key, exporter&gt; 键值对放入缓存中</span>
    <span class="n">exporterMap</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">key</span><span class="o">,</span> <span class="n">exporter</span><span class="o">);</span>

    <span class="c1">// 本地存根相关代码</span>
    <span class="nc">Boolean</span> <span class="n">isStubSupportEvent</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">STUB_EVENT_KEY</span><span class="o">,</span> <span class="nc">Constants</span><span class="o">.</span><span class="na">DEFAULT_STUB_EVENT</span><span class="o">);</span>
    <span class="nc">Boolean</span> <span class="n">isCallbackservice</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">IS_CALLBACK_SERVICE</span><span class="o">,</span> <span class="kc">false</span><span class="o">);</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">isStubSupportEvent</span> <span class="o">&amp;&amp;</span> <span class="o">!</span><span class="n">isCallbackservice</span><span class="o">)</span> <span class="o">{</span>
        <span class="nc">String</span> <span class="n">stubServiceMethods</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">STUB_EVENT_METHODS_KEY</span><span class="o">);</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">stubServiceMethods</span> <span class="o">==</span> <span class="kc">null</span> <span class="o">||</span> <span class="n">stubServiceMethods</span><span class="o">.</span><span class="na">length</span><span class="o">()</span> <span class="o">==</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
            <span class="c1">// 省略日志打印代码</span>
        <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
            <span class="n">stubServiceMethodsMap</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">url</span><span class="o">.</span><span class="na">getServiceKey</span><span class="o">(),</span> <span class="n">stubServiceMethods</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>

    <span class="c1">// 启动服务器</span>
    <span class="n">openServer</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
    <span class="c1">// 优化序列化</span>
    <span class="n">optimizeSerialization</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
    <span class="k">return</span> <span class="n">exporter</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>

<p>有必要提一下<code class="language-plaintext highlighter-rouge">DubboProtocol</code>所持有的一些属性:</p>

<pre><code class="language-mermaid">classDiagram

class AbstractProtocol{
    Map&lt;String, Exporter&lt;?&gt;&gt; exporterMap 
    Map&lt;String, ProtocolServer&gt; serverMap
    Set&lt;Invoker&lt;?&gt;&gt; invokers
}

class DubboProtocol{
    ExchangeHandler requestHandler
}

Protocol &lt;|.. AbstractProtocol
AbstractProtocol &lt;|--DubboProtocol
</code></pre>

<p>单单<code class="language-plaintext highlighter-rouge">DubboProtocol.export(...)</code>函数的作用就是把<code class="language-plaintext highlighter-rouge">exporterMap</code>的缓存更新(<code class="language-plaintext highlighter-rouge">exporterMap.put(key, exporter);</code>)<br />
需要特别注意这里的<code class="language-plaintext highlighter-rouge">requestHandler</code>是匿名内部类,所以这个类共享<code class="language-plaintext highlighter-rouge">DubboProtocol</code>所有的方法和属性<br />
由于<code class="language-plaintext highlighter-rouge">DubboProtocol</code>持有<code class="language-plaintext highlighter-rouge">exporterMap</code>,<code class="language-plaintext highlighter-rouge">serverMap</code>,所以可以根据把底层<code class="language-plaintext highlighter-rouge">NettyServer</code>的事件传递到上层<code class="language-plaintext highlighter-rouge">Protocol</code>层</p>

<h3 id="openserver">openServer(…)</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">private</span> <span class="kt">void</span> <span class="nf">openServer</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">)</span> <span class="o">{</span>
    <span class="c1">// 获取 host:port，并将其作为服务器实例的 key，用于标识当前的服务器实例</span>
    <span class="nc">String</span> <span class="n">key</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getAddress</span><span class="o">();</span>
    <span class="kt">boolean</span> <span class="n">isServer</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">IS_SERVER_KEY</span><span class="o">,</span> <span class="kc">true</span><span class="o">);</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">isServer</span><span class="o">)</span> <span class="o">{</span>
        <span class="c1">// 访问缓存</span>
        <span class="nc">ExchangeServer</span> <span class="n">server</span> <span class="o">=</span> <span class="n">serverMap</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">key</span><span class="o">);</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">server</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
            <span class="c1">// 创建服务器实例</span>
            <span class="n">serverMap</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">key</span><span class="o">,</span> <span class="n">createServer</span><span class="o">(</span><span class="n">url</span><span class="o">));</span>
        <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
            <span class="c1">// 服务器已创建，则根据 url 中的配置重置服务器</span>
            <span class="n">server</span><span class="o">.</span><span class="na">reset</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<p>再次检查<code class="language-plaintext highlighter-rouge">serverMap</code>是否有<code class="language-plaintext highlighter-rouge">ExchangeServer</code>缓存,如果没有则创建</p>

<h3 id="createserver">createServer(…)</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">private</span> <span class="nc">ExchangeServer</span> <span class="nf">createServer</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">)</span> <span class="o">{</span>
    <span class="n">url</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">addParameterIfAbsent</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">CHANNEL_READONLYEVENT_SENT_KEY</span><span class="o">,</span>
    <span class="c1">// 添加心跳检测配置到 url 中</span>
    <span class="n">url</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">addParameterIfAbsent</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">HEARTBEAT_KEY</span><span class="o">,</span> <span class="nc">String</span><span class="o">.</span><span class="na">valueOf</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">DEFAULT_HEARTBEAT</span><span class="o">));</span>
	<span class="c1">// 获取 server 参数，默认为 netty</span>
    <span class="nc">String</span> <span class="n">str</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">SERVER_KEY</span><span class="o">,</span> <span class="nc">Constants</span><span class="o">.</span><span class="na">DEFAULT_REMOTING_SERVER</span><span class="o">);</span>

	<span class="c1">// 通过 SPI 检测是否存在 server 参数所代表的 Transporter 拓展，不存在则抛出异常</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">str</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">str</span><span class="o">.</span><span class="na">length</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span> <span class="o">&amp;&amp;</span> <span class="o">!</span><span class="nc">ExtensionLoader</span><span class="o">.</span><span class="na">getExtensionLoader</span><span class="o">(</span><span class="nc">Transporter</span><span class="o">.</span><span class="na">class</span><span class="o">).</span><span class="na">hasExtension</span><span class="o">(</span><span class="n">str</span><span class="o">))</span>
        <span class="k">throw</span> <span class="k">new</span> <span class="nf">RpcException</span><span class="o">(</span><span class="s">"Unsupported server type: "</span> <span class="o">+</span> <span class="n">str</span> <span class="o">+</span> <span class="s">", url: "</span> <span class="o">+</span> <span class="n">url</span><span class="o">);</span>

    <span class="c1">// 添加编码解码器参数</span>
    <span class="n">url</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">addParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">CODEC_KEY</span><span class="o">,</span> <span class="nc">DubboCodec</span><span class="o">.</span><span class="na">NAME</span><span class="o">);</span>
    <span class="nc">ExchangeServer</span> <span class="n">server</span><span class="o">;</span>
    <span class="k">try</span> <span class="o">{</span>
        <span class="c1">// 创建 ExchangeServer</span>
        <span class="n">server</span> <span class="o">=</span> <span class="nc">Exchangers</span><span class="o">.</span><span class="na">bind</span><span class="o">(</span><span class="n">url</span><span class="o">,</span> <span class="n">requestHandler</span><span class="o">);</span>
    <span class="o">}</span> <span class="k">catch</span> <span class="o">(</span><span class="nc">RemotingException</span> <span class="n">e</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">throw</span> <span class="k">new</span> <span class="nf">RpcException</span><span class="o">(</span><span class="s">"Fail to start server..."</span><span class="o">);</span>
    <span class="o">}</span>
                                   
	<span class="c1">// 获取 client 参数，可指定 netty，mina</span>
    <span class="n">str</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">CLIENT_KEY</span><span class="o">);</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">str</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">str</span><span class="o">.</span><span class="na">length</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
        <span class="c1">// 获取所有的 Transporter 实现类名称集合，比如 supportedTypes = [netty, mina]</span>
        <span class="nc">Set</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;</span> <span class="n">supportedTypes</span> <span class="o">=</span> <span class="nc">ExtensionLoader</span><span class="o">.</span><span class="na">getExtensionLoader</span><span class="o">(</span><span class="nc">Transporter</span><span class="o">.</span><span class="na">class</span><span class="o">).</span><span class="na">getSupportedExtensions</span><span class="o">();</span>
        <span class="c1">// 检测当前 Dubbo 所支持的 Transporter 实现类名称列表中，</span>
        <span class="c1">// 是否包含 client 所表示的 Transporter，若不包含，则抛出异常</span>
        <span class="k">if</span> <span class="o">(!</span><span class="n">supportedTypes</span><span class="o">.</span><span class="na">contains</span><span class="o">(</span><span class="n">str</span><span class="o">))</span> <span class="o">{</span>
            <span class="k">throw</span> <span class="k">new</span> <span class="nf">RpcException</span><span class="o">(</span><span class="s">"Unsupported client type..."</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>
    <span class="k">return</span> <span class="n">server</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="exchangersbind">Exchangers.bind(…)</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">class</span> <span class="nc">Exchangers</span><span class="o">{</span>
    <span class="kd">public</span> <span class="kd">static</span> <span class="nc">ExchangeServer</span> <span class="nf">bind</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">,</span> <span class="nc">ExchangeHandler</span> <span class="n">handler</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RemotingException</span> <span class="o">{</span>
        <span class="c1">//...</span>
        <span class="k">return</span> <span class="nf">getExchanger</span><span class="o">(</span><span class="n">url</span><span class="o">).</span><span class="na">bind</span><span class="o">(</span><span class="n">url</span><span class="o">,</span> <span class="n">handler</span><span class="o">);</span>
    <span class="o">}</span>
    <span class="kd">public</span> <span class="kd">static</span> <span class="nc">Exchanger</span> <span class="nf">getExchanger</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">)</span> <span class="o">{</span>
        <span class="nc">String</span> <span class="n">type</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">EXCHANGER_KEY</span><span class="o">,</span> <span class="nc">Constants</span><span class="o">.</span><span class="na">DEFAULT_EXCHANGER</span><span class="o">);</span>
        <span class="k">return</span> <span class="nf">getExchanger</span><span class="o">(</span><span class="n">type</span><span class="o">);</span>
    <span class="o">}</span>
    <span class="kd">public</span> <span class="kd">static</span> <span class="nc">Exchanger</span> <span class="nf">getExchanger</span><span class="o">(</span><span class="nc">String</span> <span class="n">type</span><span class="o">)</span> <span class="o">{</span>
        <span class="c1">//...</span>
        <span class="k">return</span> <span class="nc">ExtensionLoader</span><span class="o">.</span><span class="na">getExtensionLoader</span><span class="o">(</span><span class="nc">Exchanger</span><span class="o">.</span><span class="na">class</span><span class="o">).</span><span class="na">getExtension</span><span class="o">(</span><span class="n">type</span><span class="o">);</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="exchangerbind">Exchanger.bind()</h2>

<p>主要过程就是调用了<code class="language-plaintext highlighter-rouge">Exchangers.bind(url,requestHandler);</code>,其中<code class="language-plaintext highlighter-rouge">requestHandler</code>是<code class="language-plaintext highlighter-rouge">DubboProtocol</code>的内部匿名类<br />
这一段过程的详细源码如下</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nd">@SPI</span><span class="o">(</span><span class="nc">HeaderExchanger</span><span class="o">.</span><span class="na">NAME</span><span class="o">)</span>
<span class="kd">public</span> <span class="kd">interface</span> <span class="nc">Exchanger</span> <span class="o">{</span>
    <span class="nd">@Adaptive</span><span class="o">({</span><span class="nc">Constants</span><span class="o">.</span><span class="na">EXCHANGER_KEY</span><span class="o">})</span>
    <span class="nc">ExchangeServer</span> <span class="nf">bind</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">,</span> <span class="nc">ExchangeHandler</span> <span class="n">handler</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RemotingException</span><span class="o">;</span>
    <span class="nd">@Adaptive</span><span class="o">({</span><span class="nc">Constants</span><span class="o">.</span><span class="na">EXCHANGER_KEY</span><span class="o">})</span>
    <span class="nc">ExchangeClient</span> <span class="nf">connect</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">,</span> <span class="nc">ExchangeHandler</span> <span class="n">handler</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RemotingException</span><span class="o">;</span>
<span class="o">}</span>
<span class="cm">/*****************************************************************************************************/</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">HeaderExchanger</span> <span class="kd">implements</span> <span class="nc">Exchanger</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="kd">static</span> <span class="kd">final</span> <span class="nc">String</span> <span class="no">NAME</span> <span class="o">=</span> <span class="s">"header"</span><span class="o">;</span>
    <span class="nd">@Override</span>
    <span class="kd">public</span> <span class="nc">ExchangeServer</span> <span class="nf">bind</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">,</span> <span class="nc">ExchangeHandler</span> <span class="n">handler</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RemotingException</span> <span class="o">{</span>
        <span class="k">return</span> <span class="k">new</span> <span class="nf">HeaderExchangeServer</span><span class="o">(</span><span class="nc">Transporters</span><span class="o">.</span><span class="na">bind</span><span class="o">(</span><span class="n">url</span><span class="o">,</span> <span class="k">new</span> <span class="nc">DecodeHandler</span><span class="o">(</span><span class="k">new</span> <span class="nc">HeaderExchangeHandler</span><span class="o">(</span><span class="n">handler</span><span class="o">))));</span>
    <span class="o">}</span>
    <span class="nd">@Override</span>
    <span class="kd">public</span> <span class="nc">ExchangeClient</span> <span class="nf">connect</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">,</span> <span class="nc">ExchangeHandler</span> <span class="n">handler</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RemotingException</span> <span class="o">{</span>
        <span class="k">return</span> <span class="k">new</span> <span class="nf">HeaderExchangeClient</span><span class="o">(</span><span class="nc">Transporters</span><span class="o">.</span><span class="na">connect</span><span class="o">(</span><span class="n">url</span><span class="o">,</span> <span class="k">new</span> <span class="nc">DecodeHandler</span><span class="o">(</span><span class="k">new</span> <span class="nc">HeaderExchangeHandler</span><span class="o">(</span><span class="n">handler</span><span class="o">))),</span> <span class="kc">true</span><span class="o">);</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="transportersbind">Transporters.bind(…)</h2>

<p>可以看到这里就深入到<code class="language-plaintext highlighter-rouge">Dubbo</code>架构的下一层<code class="language-plaintext highlighter-rouge">Transporter</code>层了<br />
同样调用<code class="language-plaintext highlighter-rouge">Transporters.bind(...)</code><br />
看到<code class="language-plaintext highlighter-rouge">Transporter</code>接口的定义</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nd">@SPI</span><span class="o">(</span><span class="s">"netty"</span><span class="o">)</span>
<span class="kd">public</span> <span class="kd">interface</span> <span class="nc">Transporter</span> <span class="o">{</span>
    <span class="c1">//...</span>
<span class="o">}</span>
</code></pre></div></div>

<p>可以看到默认实现是<code class="language-plaintext highlighter-rouge">NettyTransporter</code></p>

<h2 id="transporterbind">Transporter.bind(…)</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">class</span> <span class="nc">NettyTransporter</span> <span class="kd">implements</span> <span class="nc">Transporter</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="kd">static</span> <span class="kd">final</span> <span class="nc">String</span> <span class="no">NAME</span> <span class="o">=</span> <span class="s">"netty3"</span><span class="o">;</span>
    <span class="nd">@Override</span>
    <span class="kd">public</span> <span class="nc">RemotingServer</span> <span class="nf">bind</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">,</span> <span class="nc">ChannelHandler</span> <span class="n">handler</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RemotingException</span> <span class="o">{</span>
        <span class="k">return</span> <span class="k">new</span> <span class="nf">NettyServer</span><span class="o">(</span><span class="n">url</span><span class="o">,</span> <span class="n">handler</span><span class="o">);</span>
    <span class="o">}</span>
    <span class="nd">@Override</span>
    <span class="kd">public</span> <span class="nc">Client</span> <span class="nf">connect</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">,</span> <span class="nc">ChannelHandler</span> <span class="n">handler</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RemotingException</span> <span class="o">{</span>
        <span class="k">return</span> <span class="k">new</span> <span class="nf">NettyClient</span><span class="o">(</span><span class="n">url</span><span class="o">,</span> <span class="n">handler</span><span class="o">);</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="nettyserver">NettyServer</h2>

<pre><code class="language-mermaid">classDiagram

AbstractServer &lt;|-- NettyServer
RemotingServer &lt;|.. NettyServer

class NettyServer{
    doOpen()
    doClose()
}
</code></pre>

<h2 id="registryprotocolregister">RegistryProtocol.register(…)</h2>

<p>从 <a href="#registryprotocol">RegistryProtocol</a> 可以看到在调用<code class="language-plaintext highlighter-rouge">doLocalExport(...)</code>之后还要通过调用<code class="language-plaintext highlighter-rouge">RegistryProtocol.register(...)</code>向注册中心注册服务</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kt">void</span> <span class="nf">register</span><span class="o">(</span><span class="no">URL</span> <span class="n">registryUrl</span><span class="o">,</span> <span class="no">URL</span> <span class="n">registedProviderUrl</span><span class="o">)</span> <span class="o">{</span>
    <span class="c1">// 获取 Registry</span>
    <span class="nc">Registry</span> <span class="n">registry</span> <span class="o">=</span> <span class="n">registryFactory</span><span class="o">.</span><span class="na">getRegistry</span><span class="o">(</span><span class="n">registryUrl</span><span class="o">);</span>
    <span class="c1">// 注册服务</span>
    <span class="n">registry</span><span class="o">.</span><span class="na">register</span><span class="o">(</span><span class="n">registedProviderUrl</span><span class="o">);</span>
<span class="o">}</span>
</code></pre></div></div>

<p>这里的<code class="language-plaintext highlighter-rouge">registryFactory.getRegistry(...)</code>的实现又是通过自适应拓展加载的</p>

<h3 id="registryfactorygetregistry">RegistryFactory.getRegistry(…)</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nd">@SPI</span><span class="o">(</span><span class="s">"dubbo"</span><span class="o">)</span>
<span class="kd">public</span> <span class="kd">interface</span> <span class="nc">RegistryFactory</span> <span class="o">{</span>
    <span class="nd">@Adaptive</span><span class="o">({</span><span class="s">"protocol"</span><span class="o">})</span>
    <span class="nc">Registry</span> <span class="nf">getRegistry</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">);</span>
<span class="o">}</span>
</code></pre></div></div>

<p>好了,又是默认加载<code class="language-plaintext highlighter-rouge">DubboRegistryFactory</code>,但是这里实际上是会先根据<code class="language-plaintext highlighter-rouge">protocol</code>参数选择<code class="language-plaintext highlighter-rouge">RegistryFactory</code><br />
如果通过<code class="language-plaintext highlighter-rouge">zookeeper</code>协议导出到注册中心的话加载的就是<code class="language-plaintext highlighter-rouge">ZookeeperRegistryFactory</code><br />
只考虑通过<code class="language-plaintext highlighter-rouge">zookeeper</code>的协议导出的情况,这种情况下<code class="language-plaintext highlighter-rouge">registryFactory.getRegistry(...)</code>返回的就是<code class="language-plaintext highlighter-rouge">ZookeeperRegistry</code>实例<br />
看看<code class="language-plaintext highlighter-rouge">ZookeeperRegistryFactory.getRegistry(...)</code>实现</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="nc">Registry</span> <span class="nf">getRegistry</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">)</span> <span class="o">{</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">destroyed</span><span class="o">.</span><span class="na">get</span><span class="o">())</span> <span class="o">{</span>
        <span class="no">LOGGER</span><span class="o">.</span><span class="na">warn</span><span class="o">(</span><span class="s">"All registry instances have been destroyed, failed to fetch any instance. "</span> <span class="o">+</span>
                <span class="s">"Usually, this means no need to try to do unnecessary redundant resource clearance, all registries has been taken care of."</span><span class="o">);</span>
        <span class="k">return</span> <span class="no">DEFAULT_NOP_REGISTRY</span><span class="o">;</span>
    <span class="o">}</span>

    <span class="n">url</span> <span class="o">=</span> <span class="nc">URLBuilder</span><span class="o">.</span><span class="na">from</span><span class="o">(</span><span class="n">url</span><span class="o">)</span>
            <span class="o">.</span><span class="na">setPath</span><span class="o">(</span><span class="nc">RegistryService</span><span class="o">.</span><span class="na">class</span><span class="o">.</span><span class="na">getName</span><span class="o">())</span>
            <span class="o">.</span><span class="na">addParameter</span><span class="o">(</span><span class="no">INTERFACE_KEY</span><span class="o">,</span> <span class="nc">RegistryService</span><span class="o">.</span><span class="na">class</span><span class="o">.</span><span class="na">getName</span><span class="o">())</span>
            <span class="o">.</span><span class="na">removeParameters</span><span class="o">(</span><span class="no">EXPORT_KEY</span><span class="o">,</span> <span class="no">REFER_KEY</span><span class="o">)</span>
            <span class="o">.</span><span class="na">build</span><span class="o">();</span>
    <span class="nc">String</span> <span class="n">key</span> <span class="o">=</span> <span class="n">createRegistryCacheKey</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
    <span class="c1">// Lock the registry access process to ensure a single instance of the registry</span>
    <span class="no">LOCK</span><span class="o">.</span><span class="na">lock</span><span class="o">();</span>
    <span class="k">try</span> <span class="o">{</span>
        <span class="nc">Registry</span> <span class="n">registry</span> <span class="o">=</span> <span class="no">REGISTRIES</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">key</span><span class="o">);</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">registry</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
            <span class="k">return</span> <span class="n">registry</span><span class="o">;</span>
        <span class="o">}</span>
        <span class="c1">//create registry by spi/ioc</span>
        <span class="n">registry</span> <span class="o">=</span> <span class="n">createRegistry</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">registry</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
            <span class="k">throw</span> <span class="k">new</span> <span class="nf">IllegalStateException</span><span class="o">(</span><span class="s">"Can not create registry "</span> <span class="o">+</span> <span class="n">url</span><span class="o">);</span>
        <span class="o">}</span>
        <span class="no">REGISTRIES</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">key</span><span class="o">,</span> <span class="n">registry</span><span class="o">);</span>
        <span class="k">return</span> <span class="n">registry</span><span class="o">;</span>
    <span class="o">}</span> <span class="k">finally</span> <span class="o">{</span>
        <span class="c1">// Release the lock</span>
        <span class="no">LOCK</span><span class="o">.</span><span class="na">unlock</span><span class="o">();</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<p>大部分过程都很好理解,唯独<code class="language-plaintext highlighter-rouge">createRegistry(url)</code>这一行</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">class</span> <span class="nc">ZookeeperRegistryFactory</span> <span class="kd">extends</span> <span class="nc">AbstractRegistryFactory</span> <span class="o">{</span>
    <span class="kd">private</span> <span class="nc">ZookeeperTransporter</span> <span class="n">zookeeperTransporter</span><span class="o">;</span>
    <span class="cm">/**
     * Invisible injection of zookeeper client via IOC/SPI
     * @param zookeeperTransporter
     */</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">setZookeeperTransporter</span><span class="o">(</span><span class="nc">ZookeeperTransporter</span> <span class="n">zookeeperTransporter</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">this</span><span class="o">.</span><span class="na">zookeeperTransporter</span> <span class="o">=</span> <span class="n">zookeeperTransporter</span><span class="o">;</span>
    <span class="o">}</span>
    <span class="nd">@Override</span>
    <span class="kd">public</span> <span class="nc">Registry</span> <span class="nf">createRegistry</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">return</span> <span class="k">new</span> <span class="nf">ZookeeperRegistry</span><span class="o">(</span><span class="n">url</span><span class="o">,</span> <span class="n">zookeeperTransporter</span><span class="o">);</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="registry">Registry</h2>

<p>就一行,创建一个<code class="language-plaintext highlighter-rouge">ZookeeperRegistry</code>实例,看一看<code class="language-plaintext highlighter-rouge">ZookeeperRegistry</code>的构造函数
但是这里要注意<code class="language-plaintext highlighter-rouge">ZookeeperTransporter</code>不是通过自适应加载,而是通过Dubbo的SPI提供的IOC实现的<br />
这里加载的是<code class="language-plaintext highlighter-rouge">CuratorZookeeperTransporter</code></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="nf">ZookeeperRegistry</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">,</span> <span class="nc">ZookeeperTransporter</span> <span class="n">zookeeperTransporter</span><span class="o">)</span> <span class="o">{</span>
    <span class="kd">super</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">url</span><span class="o">.</span><span class="na">isAnyHost</span><span class="o">())</span> <span class="o">{</span>
        <span class="k">throw</span> <span class="k">new</span> <span class="nf">IllegalStateException</span><span class="o">(</span><span class="s">"registry address == null"</span><span class="o">);</span>
    <span class="o">}</span>
    <span class="nc">String</span> <span class="n">group</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="no">GROUP_KEY</span><span class="o">,</span> <span class="no">DEFAULT_ROOT</span><span class="o">);</span>
    <span class="k">if</span> <span class="o">(!</span><span class="n">group</span><span class="o">.</span><span class="na">startsWith</span><span class="o">(</span><span class="no">PATH_SEPARATOR</span><span class="o">))</span> <span class="o">{</span>
        <span class="n">group</span> <span class="o">=</span> <span class="no">PATH_SEPARATOR</span> <span class="o">+</span> <span class="n">group</span><span class="o">;</span>
    <span class="o">}</span>
    <span class="k">this</span><span class="o">.</span><span class="na">root</span> <span class="o">=</span> <span class="n">group</span><span class="o">;</span>
    <span class="n">zkClient</span> <span class="o">=</span> <span class="n">zookeeperTransporter</span><span class="o">.</span><span class="na">connect</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
    <span class="n">zkClient</span><span class="o">.</span><span class="na">addStateListener</span><span class="o">((</span><span class="n">state</span><span class="o">)</span> <span class="o">-&gt;</span> <span class="o">{</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">state</span> <span class="o">==</span> <span class="nc">StateListener</span><span class="o">.</span><span class="na">RECONNECTED</span><span class="o">)</span> <span class="o">{</span>
            <span class="n">logger</span><span class="o">.</span><span class="na">warn</span><span class="o">(</span><span class="s">"Trying to fetch the latest urls, in case there're provider changes during connection loss.\n"</span> <span class="o">+</span>
                    <span class="s">" Since ephemeral ZNode will not get deleted for a connection lose, "</span> <span class="o">+</span>
                    <span class="s">"there's no need to re-register url of this instance."</span><span class="o">);</span>
            <span class="nc">ZookeeperRegistry</span><span class="o">.</span><span class="na">this</span><span class="o">.</span><span class="na">fetchLatestAddresses</span><span class="o">();</span>
        <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">(</span><span class="n">state</span> <span class="o">==</span> <span class="nc">StateListener</span><span class="o">.</span><span class="na">NEW_SESSION_CREATED</span><span class="o">)</span> <span class="o">{</span>
            <span class="n">logger</span><span class="o">.</span><span class="na">warn</span><span class="o">(</span><span class="s">"Trying to re-register urls and re-subscribe listeners of this instance to registry..."</span><span class="o">);</span>
            <span class="k">try</span> <span class="o">{</span>
                <span class="nc">ZookeeperRegistry</span><span class="o">.</span><span class="na">this</span><span class="o">.</span><span class="na">recover</span><span class="o">();</span>
            <span class="o">}</span> <span class="k">catch</span> <span class="o">(</span><span class="nc">Exception</span> <span class="n">e</span><span class="o">)</span> <span class="o">{</span>
                <span class="n">logger</span><span class="o">.</span><span class="na">error</span><span class="o">(</span><span class="n">e</span><span class="o">.</span><span class="na">getMessage</span><span class="o">(),</span> <span class="n">e</span><span class="o">);</span>
            <span class="o">}</span>
        <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">(</span><span class="n">state</span> <span class="o">==</span> <span class="nc">StateListener</span><span class="o">.</span><span class="na">SESSION_LOST</span><span class="o">)</span> <span class="o">{</span>
            <span class="n">logger</span><span class="o">.</span><span class="na">warn</span><span class="o">(</span><span class="s">"Url of this instance will be deleted from registry soon. "</span> <span class="o">+</span>
                    <span class="s">"Dubbo client will try to re-register once a new session is created."</span><span class="o">);</span>
        <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">(</span><span class="n">state</span> <span class="o">==</span> <span class="nc">StateListener</span><span class="o">.</span><span class="na">SUSPENDED</span><span class="o">)</span> <span class="o">{</span>

        <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">(</span><span class="n">state</span> <span class="o">==</span> <span class="nc">StateListener</span><span class="o">.</span><span class="na">CONNECTED</span><span class="o">)</span> <span class="o">{</span>

        <span class="o">}</span>
    <span class="o">});</span>
<span class="o">}</span>
</code></pre></div></div>

<p>这里分为<code class="language-plaintext highlighter-rouge">zookeeperTransporter.connect(url)</code>和<code class="language-plaintext highlighter-rouge">zkClient.addStateListener(...)</code>两部分<br />
深入到<code class="language-plaintext highlighter-rouge">CuratorZookeeperTransporter.connect(url)</code></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="nc">ZookeeperClient</span> <span class="nf">connect</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">)</span> <span class="o">{</span>
    <span class="c1">// 创建 CuratorZookeeperClient</span>
    <span class="k">return</span> <span class="k">new</span> <span class="nf">CuratorZookeeperClient</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
<span class="o">}</span>
</code></pre></div></div>

<p>继续深入到<code class="language-plaintext highlighter-rouge">new CuratorZookeeperClient(url)</code></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">class</span> <span class="nc">CuratorZookeeperClient</span> <span class="kd">extends</span> <span class="nc">AbstractZookeeperClient</span><span class="o">&lt;</span><span class="nc">CuratorWatcher</span><span class="o">&gt;</span> <span class="o">{</span>

    <span class="kd">private</span> <span class="kd">final</span> <span class="nc">CuratorFramework</span> <span class="n">client</span><span class="o">;</span>
    
    <span class="kd">public</span> <span class="nf">CuratorZookeeperClient</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">)</span> <span class="o">{</span>
        <span class="kd">super</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
        <span class="k">try</span> <span class="o">{</span>
            <span class="c1">// 创建 CuratorFramework 构造器</span>
            <span class="nc">CuratorFrameworkFactory</span><span class="o">.</span><span class="na">Builder</span> <span class="n">builder</span> <span class="o">=</span> <span class="nc">CuratorFrameworkFactory</span><span class="o">.</span><span class="na">builder</span><span class="o">()</span>
                    <span class="o">.</span><span class="na">connectString</span><span class="o">(</span><span class="n">url</span><span class="o">.</span><span class="na">getBackupAddress</span><span class="o">())</span>
                    <span class="o">.</span><span class="na">retryPolicy</span><span class="o">(</span><span class="k">new</span> <span class="nc">RetryNTimes</span><span class="o">(</span><span class="mi">1</span><span class="o">,</span> <span class="mi">1000</span><span class="o">))</span>
                    <span class="o">.</span><span class="na">connectionTimeoutMs</span><span class="o">(</span><span class="mi">5000</span><span class="o">);</span>
            <span class="nc">String</span> <span class="n">authority</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getAuthority</span><span class="o">();</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">authority</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">authority</span><span class="o">.</span><span class="na">length</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
                <span class="n">builder</span> <span class="o">=</span> <span class="n">builder</span><span class="o">.</span><span class="na">authorization</span><span class="o">(</span><span class="s">"digest"</span><span class="o">,</span> <span class="n">authority</span><span class="o">.</span><span class="na">getBytes</span><span class="o">());</span>
            <span class="o">}</span>
            <span class="c1">// 构建 CuratorFramework 实例</span>
            <span class="n">client</span> <span class="o">=</span> <span class="n">builder</span><span class="o">.</span><span class="na">build</span><span class="o">();</span>
            <span class="c1">// 添加监听器</span>
            <span class="n">client</span><span class="o">.</span><span class="na">getConnectionStateListenable</span><span class="o">().</span><span class="na">addListener</span><span class="o">(</span><span class="k">new</span> <span class="nc">ConnectionStateListener</span><span class="o">()</span> <span class="o">{</span>
                <span class="nd">@Override</span>
                <span class="kd">public</span> <span class="kt">void</span> <span class="nf">stateChanged</span><span class="o">(</span><span class="nc">CuratorFramework</span> <span class="n">client</span><span class="o">,</span> <span class="nc">ConnectionState</span> <span class="n">state</span><span class="o">)</span> <span class="o">{</span>
                    <span class="k">if</span> <span class="o">(</span><span class="n">state</span> <span class="o">==</span> <span class="nc">ConnectionState</span><span class="o">.</span><span class="na">LOST</span><span class="o">)</span> <span class="o">{</span>
                        <span class="nc">CuratorZookeeperClient</span><span class="o">.</span><span class="na">this</span><span class="o">.</span><span class="na">stateChanged</span><span class="o">(</span><span class="nc">StateListener</span><span class="o">.</span><span class="na">DISCONNECTED</span><span class="o">);</span>
                    <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">(</span><span class="n">state</span> <span class="o">==</span> <span class="nc">ConnectionState</span><span class="o">.</span><span class="na">CONNECTED</span><span class="o">)</span> <span class="o">{</span>
                        <span class="nc">CuratorZookeeperClient</span><span class="o">.</span><span class="na">this</span><span class="o">.</span><span class="na">stateChanged</span><span class="o">(</span><span class="nc">StateListener</span><span class="o">.</span><span class="na">CONNECTED</span><span class="o">);</span>
                    <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">(</span><span class="n">state</span> <span class="o">==</span> <span class="nc">ConnectionState</span><span class="o">.</span><span class="na">RECONNECTED</span><span class="o">)</span> <span class="o">{</span>
                        <span class="nc">CuratorZookeeperClient</span><span class="o">.</span><span class="na">this</span><span class="o">.</span><span class="na">stateChanged</span><span class="o">(</span><span class="nc">StateListener</span><span class="o">.</span><span class="na">RECONNECTED</span><span class="o">);</span>
                    <span class="o">}</span>
                <span class="o">}</span>
            <span class="o">});</span>
            
            <span class="c1">// 启动客户端</span>
            <span class="n">client</span><span class="o">.</span><span class="na">start</span><span class="o">();</span>
        <span class="o">}</span> <span class="k">catch</span> <span class="o">(</span><span class="nc">Exception</span> <span class="n">e</span><span class="o">)</span> <span class="o">{</span>
            <span class="k">throw</span> <span class="k">new</span> <span class="nf">IllegalStateException</span><span class="o">(</span><span class="n">e</span><span class="o">.</span><span class="na">getMessage</span><span class="o">(),</span> <span class="n">e</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<p>看到这里可以知道<code class="language-plaintext highlighter-rouge">ZookeeperRegistry</code>大概是个什么玩意<br />
回到 <a href="#服务注册">服务注册</a>, 接下来的调用<code class="language-plaintext highlighter-rouge">Registry.register(...)</code>实际上就是调用的<code class="language-plaintext highlighter-rouge">ZookeeperRegistry.register(...)</code><br />
<code class="language-plaintext highlighter-rouge">ZookeeperRegistry.register(...)</code>的主要功能写在<code class="language-plaintext highlighter-rouge">ZookeeperRegistry.doRegistry(...)</code></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nd">@Override</span>
<span class="kd">public</span> <span class="kt">void</span> <span class="nf">doRegister</span><span class="o">(</span><span class="no">URL</span> <span class="n">url</span><span class="o">)</span> <span class="o">{</span>
    <span class="k">try</span> <span class="o">{</span>
        <span class="n">zkClient</span><span class="o">.</span><span class="na">create</span><span class="o">(</span><span class="n">toUrlPath</span><span class="o">(</span><span class="n">url</span><span class="o">),</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="no">DYNAMIC_KEY</span><span class="o">,</span> <span class="kc">true</span><span class="o">));</span>
    <span class="o">}</span> <span class="k">catch</span> <span class="o">(</span><span class="nc">Throwable</span> <span class="n">e</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">throw</span> <span class="k">new</span> <span class="nf">RpcException</span><span class="o">(</span><span class="s">"Failed to register "</span> <span class="o">+</span> <span class="n">url</span> <span class="o">+</span> <span class="s">" to zookeeper "</span> <span class="o">+</span> <span class="n">getUrl</span><span class="o">()</span> <span class="o">+</span> <span class="s">", cause: "</span> <span class="o">+</span> <span class="n">e</span><span class="o">.</span><span class="na">getMessage</span><span class="o">(),</span> <span class="n">e</span><span class="o">);</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<p>明了了,注册的本质就是在<code class="language-plaintext highlighter-rouge">zookeeper</code>上创建一个名称为<code class="language-plaintext highlighter-rouge">url</code>的节点<br />
借用一张Dubbo官方文档的图</p>

<p><img src="/assets/3/dubbo-export/service-registry.png" alt="" /></p>

<p>注册的本质就是在<code class="language-plaintext highlighter-rouge">/dubbo/com.alibaba.dubbo.demo.DemoService/providers/</code>下注册一个节点,节点的内容就是<code class="language-plaintext highlighter-rouge">url</code>的内容</p>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2021-01-15T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2021/01/13/webpack.html">Webpack</a></div><div class="next"><span>下篇</span><a href="/2021/01/15/dubbo-spi.html">Dubbo SPI</a></div></div></div>

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