---
title: Tomcat Connector调优
date: 2020-07-20 00:00:00 Z
tags:
- Java
- Tomcat
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Connector调优"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-07-20T08:00:00+08:00">
    <meta itemprop="keywords" content="Java,Tomcat"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Connector调优" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Connector调优" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Tomcat Connector调优" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-20T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Tomcat" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="_0">参考地址</h1>

<p><a href="https://tomcat.apache.org/tomcat-9.0-doc/config/http.html">tomcat-doc</a></p>

<h1 id="_1">Common Attributes</h1>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>maxHeaderCount : http请求中头部的最大个数,0表示无限制,默认100
maxParameterCount : URL的最大参数个数,默认1000
maxPostSize : 上传的最大文件大小,可以设置为负数来取消这一限制,默认为2MB
maxSavePostSize :  
ayncTimeout : 异步请求的最大超时时间,默认3000毫秒
port : 监听的端口
protocol : 使用的协议,可选ajp,http/1.1,http/2,每种协议都有nio,nio2,apr三种实现
</code></pre></div></div>

<h1 id="_2">Standard Implementation</h1>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>acceptCount : 当所有线程都被使用的时候,新来的accept请求都会被入队列,这个队列的最大大小就是acceptCount,再超过就会被拒绝
acceptThreadPriority : 用来处理accept请求的线程的优先值
address : 监听的地址,0:0:0:0表示所有地址

compressibleMimeType : 允许压缩的mime-type
compression : 可选on,off,force
compressMinSize : 超出这个大小的数据会被压缩,默认2048Byte

connectionLinger : socket关闭之后残存的时间,-1表示立即消除
connectionTimeout : accept之后最大的等待URL/数据的时间
connectionUploadTimeout : 上传的超时时间
disableUploadTimeout : 不解释

executor : 指向一个&lt;Executor&gt;元素,代表一个共享线程池,如果设置了这个属性,所有有关线程的配置都会被忽略,而采用executor里的配置
executorTerminationTimeoutMillis : 私有的内部的executor在等待executor里的线程终止的时间.等待完毕之后就会启动该executor的终止过程,默认5000(5秒)

keepAliveTimeout : 不解释,一个http请求的持续时间,-1表示无限等待

maxConnections : 最大处理的连接个数.达到这个值之后,新的连接会被阻塞,直到到达acceptCount的值,NIO,NIO2的协议实现下可以设置为-1(不限制)
maxCookieCount : 默认200,最大cookie
maxExtensionSize : http如果是chunk形式的话,最大的chunk个数
maxHttpHeaderSize : 默认8KB
maxKeepAliveRequests : 默认100,最大的长连接http个数
maxSwallowSize : 超过这个大小的http的body会被丢弃
maxThreads : 如果没用共享线程池,最大的线程数
maxTrailerSize : 
minSpareThreads : 最少要有这么多线程处在running状态

tcpNoDelay : 是否启用Nagle算法(捎带应答)

useAsyncIO : 除非使用APR实现,否则默认true
</code></pre></div></div>

<h1 id="_3">Java TCP socket attributes</h1>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>都是socket开头,例如socket.rxBufSize,socket.txBufSize...
socket.rxBufSize : 接收缓冲区大小
socket.txBufSize : 发送缓冲区大小
socket.tcpNoDelay : 是否启用Nagle算法
socket.soKeepAlive : 是否启用长连接

socket.ooBInline : 
socket.soReuseAddress : 
socket.onLingerOn
socket.onLingerTime

socket.soTimeout : 等价于connectionTimeout

socket.performanceConnectionTime
socket.performanceLantency
socket.performanceBandwidth
socket.unlockTimout
</code></pre></div></div>

<h1 id="_4">NIO specific configuration</h1>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>NIO是基于IO多路复用的非阻塞同步IO机制,需要一个线程轮询selector.
pollerThreadPriority ：selector线程的优先级
selectorTimeout : select(x),select的时间
useSendfile

socket.directBuffer : 是否使用直接内存,即java.nio.ByteBuffer.allocate()或者java.nio.ByteBuffer.allocateDirect(),确保jdk设置正常
socket.directSslBuffer : 

socket.appReadBufSize : 读取的缓冲区大小
socket.appWriteBufSize : 写缓存大小
socket.bufferPool : 每个socket都对应了一个channel(类似io的strean),这个数值代表缓存的多少个channel
socket.bufferPoolSize : 缓冲的channel的大小, buf_size = read_buf_size + write_buf_size

...
selectorPool.maxSelectors : 最大的selector个数
selectorPool.maxSpareSelectors : 最大空闲selector
selectorPool.shared : 是否采用selector共享机制(类似executor),如果false,则上述的selectorPool.maxSelectors和selectorPool.maxSpareSelectors才会起作用
 
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-07-20T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/07/20/misc-aba.html">CAS 的 ABA 问题</a></div><div class="next"><span>下篇</span><a href="/2020/08/10/sys-assembler.html">汇编</a></div></div></div>

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