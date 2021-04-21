---
title: ZooKeeper
date: 2021-01-31 00:00:00 Z
tags:
- Apache
- ZooKeeper
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="ZooKeeper"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2021-01-31T08:00:00+08:00">
    <meta itemprop="keywords" content="Apache,ZooKeeper"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="ZooKeeper" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-01-31T08:00:00+08:00" />
    <meta itemprop="keywords" content="Apache,ZooKeeper" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="overview">Overview</h1>

<p><a href="https://zookeeper.apache.org/doc/r3.6.2/zookeeperOver.html">ZooKeeper: A Distributed Coordination Service for Distributed Applications</a></p>

<p><img src="/assets/3/zookeeper/zkservice.jpg" alt="" /></p>

<p><img src="/assets/3/zookeeper/zknamespace.jpg" alt="" /></p>

<p><img src="/assets/3/zookeeper/QQ截图20210131123056.png" alt="" /></p>

<h2 id="bin">/bin/</h2>

<p><img src="/assets/3/zookeeper/QQ截图20210131123125.png" alt="" /></p>

<h2 id="conf">/conf/</h2>

<p><img src="/assets/3/zookeeper/QQ截图20210131123150.png" alt="" /></p>

<h1 id="配置">配置</h1>

<p><a href="https://zookeeper.apache.org/doc/r3.6.2/zookeeperStarted.html">Getting Started: Coordinating Distributed Applications with ZooKeeper</a></p>

<p>单机配置zookeeper的zoo.cfg:</p>
<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c"># 心跳频率,单位为毫秒</span>
<span class="nv">tickTime</span><span class="o">=</span>2000

<span class="c"># 新加入的follower同步leader的tick数,单位是tickTime,如果在规定时间无法连接到leader,则连接失败</span>
<span class="nv">initLimit</span><span class="o">=</span>10

<span class="c"># follower同步leader的tick数,如果超时则该节点会被抛弃</span>
<span class="nv">syncLimit</span><span class="o">=</span>5

<span class="c"># 存放数据的文件夹</span>
<span class="c"># 该文件夹可以存在 2-3 个文件:</span>
<span class="c"># - myid       : 文件名必须是myid,该文件内部只有一个 ascii 的整数,代表该节点的id</span>
<span class="c"># - initialize : 如果存在该文件,表面该节点刚刚启动,还需要查询 data-tree, 当树形结构构造完毕后,该文件会被删除</span>
<span class="c"># - snapshot   : 存放 data-tree 的快照 </span>
<span class="nv">dataDir</span><span class="o">=</span>/tmp/zookeeper

<span class="c"># 开放给客户端连接的端口</span>
<span class="nv">clientPort</span><span class="o">=</span>2181
<span class="nv">secureClientPort</span><span class="o">=</span>2182

<span class="c"># 除了follower和leader外,还有一种observer节点,这种节点不算在投票,选举里,仅仅是负责连接客户端和同步结果,</span>
<span class="c"># 为了避免observer连接到leader节点造成负载过大,可以将observer的连接到follower上去,这个节点就表明follower(或者leader)的哪个节点监听observer消息</span>
<span class="nv">observerMasterPort</span><span class="o">=</span>2183 

<span class="c"># 选举算法</span>
<span class="nv">electionAlg</span><span class="o">=</span>3 

<span class="c"># 每个集群中的服务器必须知道所有其他的服务器,server.id=host:port:port,第一个port用来连接leader,第二个port用来选举leader</span>
server.1<span class="o">=</span>192.168.0.1:2888:3888 
server.2<span class="o">=</span>192.168.0.2:2888:3888 | 192.168.1.2:2888:3888 
server.3<span class="o">=</span>192.168.0.3:2888:3888

<span class="c"># 如果采用分组的结构,每次选举要多数不同的group选举通过才行</span>
group.1<span class="o">=</span>1 
group.2<span class="o">=</span>2
group.3<span class="o">=</span>3

<span class="c"># 每个服务器的权重</span>
weight.1<span class="o">=</span>1 
weight.2<span class="o">=</span>1
weight.3<span class="o">=</span>1

<span class="c"># 设置了这个参数的节点被标识为observer</span>
<span class="nv">peerType</span><span class="o">=</span>observer

<span class="c"># 要声明成observer,还要在每个集群的节点的配置文件里标识出本节点是observer,如下</span>
server.4.192.168.0.4:2888:3888:observer
</code></pre></div></div>

<ul>
  <li>服务器启动 : <code class="language-plaintext highlighter-rouge">bin/zkServer.sh start</code></li>
  <li>客户端启动 : <code class="language-plaintext highlighter-rouge">bin/zkCli.sh -server 127.0.0.1:2181</code></li>
</ul>

<h1 id="programmers-guide">Programmer’s Guide</h1>

<p><a href="https://zookeeper.apache.org/doc/r3.6.2/zookeeperProgrammers.html">ZooKeeper Programmer’s Guide</a></p>

<h2 id="znodes">ZNodes</h2>

<h3 id="watches">Watches</h3>

<p><a href="https://zookeeper.apache.org/doc/r3.6.2/zookeeperProgrammers.html#ch_zkWatches">ZooKeeper Watches</a></p>

<p>一个 observer 模式,对一个 znode 进行监听 (watch) 可以接收到 znode 的变动通知<br />
zookeeper 的 watch 有如下特性:</p>

<ul>
  <li>watch 只触发一次 : 如果对一个节点监听 更改 事件,对该节点的更改行为会发布到 watcher 上,而后该 watcher 就会失效</li>
  <li>由于 watch 是异步发送给客户端的,这就导致了网络延迟可能导致对一个节点的删除之后再收到了对该节点的更改 watch 事件
zookeeper保证如果一个客户端对一个节点的施加 watch,那么所有对节点的更改只有接收到 watch 事件之后才会对用户可见</li>
  <li>创建一个子节点将会递归的触发 当前节点的相关 watch, 父 / 祖先 节点的相关 watch</li>
</ul>

<h3 id="data-access">Data Access</h3>

<p>访问控制机制</p>

<h3 id="ephemeral-nodes">Ephemeral Nodes</h3>

<p>只存在于当前会话 (session) 的节点,如果会话结束,则节点马上被删除</p>

<h3 id="sequence-nodes">Sequence Nodes</h3>

<p>序列节点</p>

<h3 id="container-nodes">Container Nodes</h3>

<p>容器节点,当容器节点的所有子节点被删除之后,该节点也会被 zookeeper 提上删除的日程,将会在后续被删除</p>

<h3 id="ttl-nodes">TTL Nodes</h3>

<p>定时节点,时间到期后删除</p>

<h2 id="time-in-zookeeper">Time in ZooKeeper</h2>

<p><a href="https://zookeeper.apache.org/doc/r3.6.2/zookeeperProgrammers.html#sc_timeInZk">Time in ZooKeeper</a></p>

<ul>
  <li>Zxid : (ZooKeeper Transaction Id), zxid1 小于 zxid2 ,所以 zxid1 在 zxid2 之前发生</li>
  <li>Version Number : 每一次对节点的修改都会增加节点的 Version Number , Version Number 分为三类:
    <ul>
      <li>version : number of changes to the data of a znode</li>
      <li>cversion : number of changes to the children of a znode</li>
      <li>aversion : number of changes to the ACL of a znode (ACL 即 ccess Control List)</li>
    </ul>
  </li>
  <li>Ticks</li>
  <li>Real time</li>
</ul>

<h1 id="administrators-guide">Administrator’s Guide</h1>

<p><a href="https://zookeeper.apache.org/doc/r3.6.2/zookeeperAdmin.html">ZooKeeper Administrator’s Guide</a></p>

<h1 id="zookeeper-internals">ZooKeeper Internals</h1>

<p><a href="https://zookeeper.apache.org/doc/r3.6.2/zookeeperInternals.html">ZooKeeper Internals</a></p>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2021-01-31T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2021/01/31/redis.html">Redis</a></div><div class="next"><span>下篇</span><a href="/2021/02/03/cpp-dllexport-dllimport.html">C++ __declspec(dllexport) __declspec(dllimport)</a></div></div></div>

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