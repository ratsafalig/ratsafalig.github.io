---
title: Java NIO
date: 2020-07-11 00:00:00 Z
tags:
- Java
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Java NIO"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-07-11T08:00:00+08:00">
    <meta itemprop="keywords" content="Java"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Java NIO" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-11T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Java NIO" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-11T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_0">参考地址</h1>

<p><a href="https://www.tutorialspoint.com/java_nio/java_nio_vs_io.htm">tutorialspoint-nio</a></p>

<p><a href="https://blog.csdn.net/u013857458/article/details/82424104">csdn-nio</a></p>

<h1 id="_1">Channel</h1>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>NIO的Channel相当于BIO的Stream,只不过一个Channel同时包含了InputStream和OutputStream的操作.
主要有几下几种Channel:

1. FileChannel :
    读写文件
2. DatagramChannel : 
    UDP的数据报
3. SocketChannel :
    客户端Socket读写
4. ServerSocketChannel :
    服务端Socket
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">import</span> <span class="nn">java.io.IOException</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.io.RandomAccessFile</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.ByteBuffer</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.channels.FileChannel</span><span class="o">;</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">ChannelDemo</span> <span class="o">{</span>
   <span class="kd">public</span> <span class="kd">static</span> <span class="kt">void</span> <span class="nf">main</span><span class="o">(</span><span class="nc">String</span> <span class="n">args</span><span class="o">[])</span> <span class="kd">throws</span> <span class="nc">IOException</span> <span class="o">{</span>
      <span class="nc">RandomAccessFile</span> <span class="n">file</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">RandomAccessFile</span><span class="o">(</span><span class="s">"C:/Test/temp.txt"</span><span class="o">,</span> <span class="s">"r"</span><span class="o">);</span>
      <span class="nc">FileChannel</span> <span class="n">fileChannel</span> <span class="o">=</span> <span class="n">file</span><span class="o">.</span><span class="na">getChannel</span><span class="o">();</span>
      <span class="nc">ByteBuffer</span> <span class="n">byteBuffer</span> <span class="o">=</span> <span class="nc">ByteBuffer</span><span class="o">.</span><span class="na">allocate</span><span class="o">(</span><span class="mi">512</span><span class="o">);</span>
      <span class="k">while</span> <span class="o">(</span><span class="n">fileChannel</span><span class="o">.</span><span class="na">read</span><span class="o">(</span><span class="n">byteBuffer</span><span class="o">)</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
         <span class="n">byteBuffer</span><span class="o">.</span><span class="na">flip</span><span class="o">();</span>
         <span class="k">while</span> <span class="o">(</span><span class="n">byteBuffer</span><span class="o">.</span><span class="na">hasRemaining</span><span class="o">())</span> <span class="o">{</span>
            <span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">.</span><span class="na">print</span><span class="o">((</span><span class="kt">char</span><span class="o">)</span> <span class="n">byteBuffer</span><span class="o">.</span><span class="na">get</span><span class="o">());</span>
         <span class="o">}</span>
      <span class="o">}</span>
      <span class="n">file</span><span class="o">.</span><span class="na">close</span><span class="o">();</span>
   <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="_2">ServerSocketChannel</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>服务端:
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">import</span> <span class="nn">java.io.IOException</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.net.InetSocketAddress</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.ByteBuffer</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.channels.FileChannel</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.channels.ServerSocketChannel</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.channels.SocketChannel</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.file.Path</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.file.Paths</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.file.StandardOpenOption</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.util.EnumSet</span><span class="o">;</span>

<span class="kd">public</span> <span class="kd">class</span> <span class="nc">SocketChannelServer</span> <span class="o">{</span>
   <span class="kd">public</span> <span class="kd">static</span> <span class="kt">void</span> <span class="nf">main</span><span class="o">(</span><span class="nc">String</span><span class="o">[]</span> <span class="n">args</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">IOException</span> <span class="o">{</span>
      <span class="nc">ServerSocketChannel</span> <span class="n">serverSocket</span> <span class="o">=</span> <span class="kc">null</span><span class="o">;</span>
      <span class="nc">SocketChannel</span> <span class="n">client</span> <span class="o">=</span> <span class="kc">null</span><span class="o">;</span>
      <span class="n">serverSocket</span> <span class="o">=</span> <span class="nc">ServerSocketChannel</span><span class="o">.</span><span class="na">open</span><span class="o">();</span>
      <span class="n">serverSocket</span><span class="o">.</span><span class="na">socket</span><span class="o">().</span><span class="na">bind</span><span class="o">(</span><span class="k">new</span> <span class="nc">InetSocketAddress</span><span class="o">(</span><span class="mi">9000</span><span class="o">));</span>
      <span class="n">client</span> <span class="o">=</span> <span class="n">serverSocket</span><span class="o">.</span><span class="na">accept</span><span class="o">();</span>
      <span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">.</span><span class="na">println</span><span class="o">(</span><span class="s">"Connection Set:  "</span> <span class="o">+</span> <span class="n">client</span><span class="o">.</span><span class="na">getRemoteAddress</span><span class="o">());</span>
      <span class="nc">Path</span> <span class="n">path</span> <span class="o">=</span> <span class="nc">Paths</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="s">"C:/Test/temp1.txt"</span><span class="o">);</span>
      <span class="nc">FileChannel</span> <span class="n">fileChannel</span> <span class="o">=</span> <span class="nc">FileChannel</span><span class="o">.</span><span class="na">open</span><span class="o">(</span><span class="n">path</span><span class="o">,</span> 
         <span class="nc">EnumSet</span><span class="o">.</span><span class="na">of</span><span class="o">(</span><span class="nc">StandardOpenOption</span><span class="o">.</span><span class="na">CREATE</span><span class="o">,</span> 
            <span class="nc">StandardOpenOption</span><span class="o">.</span><span class="na">TRUNCATE_EXISTING</span><span class="o">,</span>
            <span class="nc">StandardOpenOption</span><span class="o">.</span><span class="na">WRITE</span><span class="o">)</span>
         <span class="o">);</span>      
      <span class="nc">ByteBuffer</span> <span class="n">buffer</span> <span class="o">=</span> <span class="nc">ByteBuffer</span><span class="o">.</span><span class="na">allocate</span><span class="o">(</span><span class="mi">1024</span><span class="o">);</span>
      <span class="k">while</span><span class="o">(</span><span class="n">client</span><span class="o">.</span><span class="na">read</span><span class="o">(</span><span class="n">buffer</span><span class="o">)</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
         <span class="n">buffer</span><span class="o">.</span><span class="na">flip</span><span class="o">();</span>
         <span class="n">fileChannel</span><span class="o">.</span><span class="na">write</span><span class="o">(</span><span class="n">buffer</span><span class="o">);</span>
         <span class="n">buffer</span><span class="o">.</span><span class="na">clear</span><span class="o">();</span>
      <span class="o">}</span>
      <span class="n">fileChannel</span><span class="o">.</span><span class="na">close</span><span class="o">();</span>
      <span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">.</span><span class="na">println</span><span class="o">(</span><span class="s">"File Received"</span><span class="o">);</span>
      <span class="n">client</span><span class="o">.</span><span class="na">close</span><span class="o">();</span>
   <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>客户端:
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">import</span> <span class="nn">java.io.IOException</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.net.InetSocketAddress</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.net.SocketAddress</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.ByteBuffer</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.channels.FileChannel</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.channels.SocketChannel</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.file.Path</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.file.Paths</span><span class="o">;</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">SocketChannelClient</span> <span class="o">{</span>
   <span class="kd">public</span> <span class="kd">static</span> <span class="kt">void</span> <span class="nf">main</span><span class="o">(</span><span class="nc">String</span><span class="o">[]</span> <span class="n">args</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">IOException</span> <span class="o">{</span>
      <span class="nc">SocketChannel</span> <span class="n">server</span> <span class="o">=</span> <span class="nc">SocketChannel</span><span class="o">.</span><span class="na">open</span><span class="o">();</span>
      <span class="nc">SocketAddress</span> <span class="n">socketAddr</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">InetSocketAddress</span><span class="o">(</span><span class="s">"localhost"</span><span class="o">,</span> <span class="mi">9000</span><span class="o">);</span>
      <span class="n">server</span><span class="o">.</span><span class="na">connect</span><span class="o">(</span><span class="n">socketAddr</span><span class="o">);</span>
      <span class="nc">Path</span> <span class="n">path</span> <span class="o">=</span> <span class="nc">Paths</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="s">"C:/Test/temp.txt"</span><span class="o">);</span>
      <span class="nc">FileChannel</span> <span class="n">fileChannel</span> <span class="o">=</span> <span class="nc">FileChannel</span><span class="o">.</span><span class="na">open</span><span class="o">(</span><span class="n">path</span><span class="o">);</span>
      <span class="nc">ByteBuffer</span> <span class="n">buffer</span> <span class="o">=</span> <span class="nc">ByteBuffer</span><span class="o">.</span><span class="na">allocate</span><span class="o">(</span><span class="mi">1024</span><span class="o">);</span>
      <span class="k">while</span><span class="o">(</span><span class="n">fileChannel</span><span class="o">.</span><span class="na">read</span><span class="o">(</span><span class="n">buffer</span><span class="o">)</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
         <span class="n">buffer</span><span class="o">.</span><span class="na">flip</span><span class="o">();</span>
         <span class="n">server</span><span class="o">.</span><span class="na">write</span><span class="o">(</span><span class="n">buffer</span><span class="o">);</span>
         <span class="n">buffer</span><span class="o">.</span><span class="na">clear</span><span class="o">();</span>
      <span class="o">}</span>
      <span class="n">fileChannel</span><span class="o">.</span><span class="na">close</span><span class="o">();</span>
      <span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">.</span><span class="na">println</span><span class="o">(</span><span class="s">"File Sent"</span><span class="o">);</span>
      <span class="n">server</span><span class="o">.</span><span class="na">close</span><span class="o">();</span>
   <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h1 id="_3">Selector</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">import</span> <span class="nn">java.io.FileInputStream</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.io.IOException</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.net.InetSocketAddress</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.ByteBuffer</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.channels.FileChannel</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.channels.SelectionKey</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.channels.Selector</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.channels.ServerSocketChannel</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.nio.channels.SocketChannel</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.util.Iterator</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">java.util.Set</span><span class="o">;</span>

<span class="kd">public</span> <span class="kd">class</span> <span class="nc">SelectorDemo</span> <span class="o">{</span>
   <span class="kd">public</span> <span class="kd">static</span> <span class="kt">void</span> <span class="nf">main</span><span class="o">(</span><span class="nc">String</span><span class="o">[]</span> <span class="n">args</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">IOException</span> <span class="o">{</span>
      <span class="nc">String</span> <span class="n">demo_text</span> <span class="o">=</span> <span class="s">"This is a demo String"</span><span class="o">;</span>	
      <span class="nc">Selector</span> <span class="n">selector</span> <span class="o">=</span> <span class="nc">Selector</span><span class="o">.</span><span class="na">open</span><span class="o">();</span>
      <span class="nc">ServerSocketChannel</span> <span class="n">serverSocket</span> <span class="o">=</span> <span class="nc">ServerSocketChannel</span><span class="o">.</span><span class="na">open</span><span class="o">();</span>
      <span class="n">serverSocket</span><span class="o">.</span><span class="na">bind</span><span class="o">(</span><span class="k">new</span> <span class="nc">InetSocketAddress</span><span class="o">(</span><span class="s">"localhost"</span><span class="o">,</span> <span class="mi">5454</span><span class="o">));</span>
      <span class="n">serverSocket</span><span class="o">.</span><span class="na">configureBlocking</span><span class="o">(</span><span class="kc">false</span><span class="o">);</span>
      <span class="n">serverSocket</span><span class="o">.</span><span class="na">register</span><span class="o">(</span><span class="n">selector</span><span class="o">,</span> <span class="nc">SelectionKey</span><span class="o">.</span><span class="na">OP_ACCEPT</span><span class="o">);</span>
      <span class="nc">ByteBuffer</span> <span class="n">buffer</span> <span class="o">=</span> <span class="nc">ByteBuffer</span><span class="o">.</span><span class="na">allocate</span><span class="o">(</span><span class="mi">256</span><span class="o">);</span>
      <span class="k">while</span> <span class="o">(</span><span class="kc">true</span><span class="o">)</span> <span class="o">{</span>
         <span class="n">selector</span><span class="o">.</span><span class="na">select</span><span class="o">();</span>
         <span class="nc">Set</span><span class="o">&lt;</span><span class="nc">SelectionKey</span><span class="o">&gt;</span> <span class="n">selectedKeys</span> <span class="o">=</span> <span class="n">selector</span><span class="o">.</span><span class="na">selectedKeys</span><span class="o">();</span>
         <span class="nc">Iterator</span><span class="o">&lt;</span><span class="nc">SelectionKey</span><span class="o">&gt;</span> <span class="n">iter</span> <span class="o">=</span> <span class="n">selectedKeys</span><span class="o">.</span><span class="na">iterator</span><span class="o">();</span>
         <span class="k">while</span> <span class="o">(</span><span class="n">iter</span><span class="o">.</span><span class="na">hasNext</span><span class="o">())</span> <span class="o">{</span>
            <span class="nc">SelectionKey</span> <span class="n">key</span> <span class="o">=</span> <span class="n">iter</span><span class="o">.</span><span class="na">next</span><span class="o">();</span>
            <span class="kt">int</span> <span class="n">interestOps</span> <span class="o">=</span> <span class="n">key</span><span class="o">.</span><span class="na">interestOps</span><span class="o">();</span>
            <span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">.</span><span class="na">println</span><span class="o">(</span><span class="n">interestOps</span><span class="o">);</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">key</span><span class="o">.</span><span class="na">isAcceptable</span><span class="o">())</span> <span class="o">{</span>
               <span class="nc">SocketChannel</span> <span class="n">client</span> <span class="o">=</span> <span class="n">serverSocket</span><span class="o">.</span><span class="na">accept</span><span class="o">();</span>
               <span class="n">client</span><span class="o">.</span><span class="na">configureBlocking</span><span class="o">(</span><span class="kc">false</span><span class="o">);</span>
               <span class="n">client</span><span class="o">.</span><span class="na">register</span><span class="o">(</span><span class="n">selector</span><span class="o">,</span> <span class="nc">SelectionKey</span><span class="o">.</span><span class="na">OP_READ</span><span class="o">);</span>
            <span class="o">}</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">key</span><span class="o">.</span><span class="na">isReadable</span><span class="o">())</span> <span class="o">{</span>
               <span class="nc">SocketChannel</span> <span class="n">client</span> <span class="o">=</span> <span class="o">(</span><span class="nc">SocketChannel</span><span class="o">)</span> <span class="n">key</span><span class="o">.</span><span class="na">channel</span><span class="o">();</span>
               <span class="n">client</span><span class="o">.</span><span class="na">read</span><span class="o">(</span><span class="n">buffer</span><span class="o">);</span>
               <span class="k">if</span> <span class="o">(</span><span class="k">new</span> <span class="nc">String</span><span class="o">(</span><span class="n">buffer</span><span class="o">.</span><span class="na">array</span><span class="o">()).</span><span class="na">trim</span><span class="o">().</span><span class="na">equals</span><span class="o">(</span><span class="n">demo_text</span><span class="o">))</span> <span class="o">{</span>
                  <span class="n">client</span><span class="o">.</span><span class="na">close</span><span class="o">();</span>
                  <span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">.</span><span class="na">println</span><span class="o">(</span><span class="s">"Not accepting client messages anymore"</span><span class="o">);</span>
               <span class="o">}</span>
               <span class="n">buffer</span><span class="o">.</span><span class="na">flip</span><span class="o">();</span>
               <span class="n">client</span><span class="o">.</span><span class="na">write</span><span class="o">(</span><span class="n">buffer</span><span class="o">);</span>
               <span class="n">buffer</span><span class="o">.</span><span class="na">clear</span><span class="o">();</span>
            <span class="o">}</span>
            <span class="n">iter</span><span class="o">.</span><span class="na">remove</span><span class="o">();</span>
         <span class="o">}</span>
      <span class="o">}</span>
   <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-07-11T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/07/11/io-java-io.html">Java IO</a></div><div class="next"><span>下篇</span><a href="/2020/07/11/tcp.html">TCP</a></div></div></div>

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