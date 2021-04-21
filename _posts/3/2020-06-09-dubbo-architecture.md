---
title: Dubbo Architecture
date: 2020-06-09 00:00:00 Z
tags:
- Java
- Apache
- Dubbo
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Dubbo Architecture"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-06-09T08:00:00+08:00">
    <meta itemprop="keywords" content="Java,Apache,Dubbo"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Dubbo Architecture" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-09T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Apache,Dubbo" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Dubbo Architecture" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-09T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Apache,Dubbo" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Dubbo Architecture" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-09T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Apache,Dubbo" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="参考地址">参考地址</h1>

<p><a href="http://dubbo.apache.org/zh-cn/docs/dev/design.html">参考地址</a></p>

<h1 id="架构">架构</h1>

<p><img src="/assets/1/tutorial/dubbo/dubbo-framework.jpg" alt="" /></p>

<p><img src="/assets/1/tutorial/dubbo/dubbo-extension.jpg" alt="" /></p>

<h1 id="应用部分">&gt;应用部分</h1>

<h2 id="关系">关系</h2>

<pre><code class="language-mermaid">graph TD;
    id1(Cluster)
    id2(LoadBalance)
    id3(Router)
    id4(Directory)
    id5(Invoker)

    id4--parameter--&gt;Cluster
    Cluster--call_join_method--&gt;id1
    id1--return_new_invoker--&gt;id5
    id5--&gt;call_invoke_method
    call_invoke_method--use--&gt;Directory
    Directory--list_method_use--&gt;id3
    call_invoke_method--use--&gt;id2
</code></pre>

<h2 id="从服务提供者角度">从服务提供者角度</h2>

<p><img src="/assets/1/tutorial/dubbo/dubbo_rpc_export.jpg" alt="" /></p>

<h2 id="从服务消费者角度">从服务消费者角度</h2>

<p><img src="/assets/1/tutorial/dubbo/dubbo_rpc_refer.jpg" alt="" /></p>

<p><img src="/assets/1/tutorial/dubbo/dubbo-export.jpg" alt="" /></p>

<h2 id="调用过程">调用过程</h2>

<p><img src="/assets/1/tutorial/dubbo/dubbo_rpc_invoke.jpg" alt="" /></p>

<p><img src="/assets/1/tutorial/dubbo/dubbo-refer.jpg" alt="" /></p>

<h2 id="集群容错">集群容错</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>现在应用一般会在多个服务器上配置同一个service的provider,所以要一个机制在所有的provider中选一个,这个类就是Cluster,它根据传入的Directory,Directory保存了所有的provider信息,Cluster首先会调用Directory的list方法返回一个Invoker数组,这个list方法还有可能根据特定的Router在url里进行筛选再返回筛选后的Invoker数组.

Cluster会返回一个选择后的Invoker,通常的逻辑并不是由Cluster去根据Directory选择Invoker,而是创建一个特殊的Invoker,再通过构造函数传入Directory,这个特殊Invoker的invoke方法会加载LoadBalance,根据Directory的Invoker数组和LoadBalance的决策调用特定Invoker的invoke

这些特殊Invoker可以被自定义,dubbo提供了几个,分别是FailbackClusterInvoker,FailoverClusterInvoker,FailsafeClusterInvoker,ForkingClusterInvoker,FailoverClusterInvoker.对应的Cluster分别是FailbackCluster,FailoverCluster......

这些Cluster的区别是:

1. failover : 设定重传次数.每出现错误就选择其他服务器
2. failback : 失败自动恢复,后台记录失败请求,定时重发
3. failfast : 快速失败,只发起一次调用,如果出错就抛出
4. failsafe : 出现异常直接忽略.
5. forking : 并行调用多个provider,有一个成功就成功
6. broadcast : 调用所有provider,有一个错就算错

以上配置可以通过如下配置
</code></pre></div></div>

<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;dubbo:service</span> <span class="na">cluster=</span><span class="s">"failsafe"</span> <span class="nt">/&gt;</span>
<span class="c">&lt;!--或者--&gt;</span>
<span class="nt">&lt;dubbo:reference</span> <span class="na">cluster=</span><span class="s">"failsafe"</span> <span class="nt">/&gt;</span>
</code></pre></div></div>

<h2 id="负载均衡">负载均衡</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>既然要在一堆Directory里选出一个Invoker,那么肯定需要一个策略,Dubbo的方案是直接返回一个代理的Invoker,实际调用的时候由这个代理的Invoker选出Directory的实际Invoker,这个选出Invoker的策略就是LoadBalance.

特点:
1. Random LoadBalance : 按权重随机选取一个,在一个截面上碰撞的概率高,但调用量越大分布越均匀,而且按概率使用权重后也比较均匀,有利于动态调整提供者权重
2. RoundRobin LoadBalance : 轮询,按公约后的权重设置轮询比率,存在慢的提供者累积请求的问题,比如:第二台机器很慢,但没挂,当请求调到第二台时就卡在那,久而久之,所有请求都卡在调到第二台上.
3. LeastActive LoadBalance : 最少活跃调用,相同活跃数的随机,活跃数指调用前后计数差,使慢的提供者收到更少请求,因为越慢的提供者的调用前后计数差会越大.
4. ConsistentHash LoadBalance : 一致性 Hash,相同参数的请求总是发到同一提供者

示例配置:
</code></pre></div></div>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c">&lt;!--服务级别,对一整个类用一个loadbalance--&gt;</span>
<span class="nt">&lt;dubbo:service</span> <span class="na">interface=</span><span class="s">"..."</span> <span class="na">loadbalance=</span><span class="s">"roundrobin"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;dubbo:reference</span> <span class="na">interface=</span><span class="s">"..."</span> <span class="na">loadbalance=</span><span class="s">"roundrobin"</span> <span class="nt">/&gt;</span>

<span class="c">&lt;!--方法级别,对不同方法调用不同的loadbalance--&gt;</span>
<span class="nt">&lt;dubbo:service</span> <span class="na">interface=</span><span class="s">"..."</span><span class="nt">&gt;</span>
    <span class="nt">&lt;dubbo:method</span> <span class="na">name=</span><span class="s">"..."</span> <span class="na">loadbalance=</span><span class="s">"roundrobin"</span><span class="nt">/&gt;</span>
<span class="nt">&lt;/dubbo:service&gt;</span>
<span class="nt">&lt;dubbo:reference</span> <span class="na">interface=</span><span class="s">"..."</span><span class="nt">&gt;</span>
    <span class="nt">&lt;dubbo:method</span> <span class="na">name=</span><span class="s">"..."</span> <span class="na">loadbalance=</span><span class="s">"roundrobin"</span><span class="nt">/&gt;</span>
<span class="nt">&lt;/dubbo:reference&gt;</span>
</code></pre></div></div>

<h2 id="线程模型">线程模型</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>如果一个操作要花费很长的时间,如果采用阻塞的方式将会导致并发性大幅度下降,前一个没完成下一个就无法开始,所以需要一个机制进行多线程处理,一个请求一个线程,这样就可以同时处理多个请求
</code></pre></div></div>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;dubbo:protocol</span> <span class="na">name=</span><span class="s">"dubbo"</span> <span class="na">dispatcher=</span><span class="s">"all"</span> <span class="na">threadpool=</span><span class="s">"fixed"</span> <span class="na">threads=</span><span class="s">"100"</span> <span class="nt">/&gt;</span>
</code></pre></div></div>

<pre><code class="language-mermaid">graph LR;
    id1(Dispatcher)
    id2(all)
    id3(direct)
    id4(message)
    id5(execution)
    id6(connection)
    id1--所有消息都派发到线程池,包括请求,响应,连接事件,断开事件,心跳等--&gt;id2
    id1--所有消息都不派发到线程池,全部在IO线程上直接执行--&gt;id3
    id1--只有请求响应消息派发到线程池,其它连接断开事件,心跳等消息,直接在IO线程上执行--&gt;id4
    id1--只有请求消息派发到线程池,不含响应,响应和其它连接断开事件,心跳等消息,直接在IO线程上执行--&gt;id5
    id1--在IO线程上,将连接断开事件放入队列,有序逐个执行,其它消息派发到线程池--&gt;id6

</code></pre>

<pre><code class="language-mermaid">graph LR;
    id1(ThreadPool)
    id2(fixed)
    id3(cached)
    id4(limited)
    id5(eager)

    id1--固定大小线程池,启动时建立线程,不关闭,一直持有,缺省是fixed--&gt;id2
    id1--缓存线程池,空闲一分钟自动删除,需要时重建--&gt;id3
    id1--可伸缩线程池,但池中的线程数只会增长不会收缩,只增长不收缩的目的是为了避免收缩时突然来了大流量引起的性能问题--&gt;id4
    id1--优先创建Worker线程池.在任务数量大于corePoolSize但是小于maximumPoolSize时.优先创建Worker来处理任务.当任务数量大于maximumPoolSize时,将任务放入阻塞队列中.阻塞队列充满时抛出RejectedExecutionException,相比于cached:cached在任务数量超过maximumPoolSize时直接抛出异常而不是将任务放入阻塞队列--&gt;id5
</code></pre>

<h2 id="直连提供者">直连提供者</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>可以通过一定配置让指定reference绕过配置的注册中心,直接从指定url获取
</code></pre></div></div>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;dubbo:reference</span> <span class="na">id=</span><span class="s">"xxxService"</span> <span class="na">interface=</span><span class="s">"com.alibaba.xxx.XxxService"</span> <span class="na">url=</span><span class="s">"dubbo://localhost:20890"</span> <span class="nt">/&gt;</span>
</code></pre></div></div>

<h2 id="只订阅">只订阅</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>当在开发一个新的provider时候,要引用其他的provider,但是不想让当前开发未完成的东西注册到注册中心,可以如下配置
</code></pre></div></div>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;dubbo:registry</span> <span class="na">address=</span><span class="s">"10.20.153.10:9090"</span> <span class="na">register=</span><span class="s">"false"</span> <span class="nt">/&gt;</span>
</code></pre></div></div>

<h2 id="只注册">只注册</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>dubbo同样允许provider将服务注册到注册中心,而不让consumer从那个注册中心订阅服务
</code></pre></div></div>

<h2 id="多协议">多协议</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>不同服务不同协议
</code></pre></div></div>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;beans</span> <span class="na">xmlns=</span><span class="s">"http://www.springframework.org/schema/beans"</span>
    <span class="na">xmlns:xsi=</span><span class="s">"http://www.w3.org/2001/XMLSchema-instance"</span>
    <span class="na">xmlns:dubbo=</span><span class="s">"http://dubbo.apache.org/schema/dubbo"</span>
    <span class="na">xsi:schemaLocation=</span><span class="s">"http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd"</span><span class="nt">&gt;</span> 
    <span class="nt">&lt;dubbo:application</span> <span class="na">name=</span><span class="s">"world"</span>  <span class="nt">/&gt;</span>
    <span class="nt">&lt;dubbo:registry</span> <span class="na">id=</span><span class="s">"registry"</span> <span class="na">address=</span><span class="s">"10.20.141.150:9090"</span> <span class="na">username=</span><span class="s">"admin"</span> <span class="na">password=</span><span class="s">"hello1234"</span> <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 多协议配置 --&gt;</span>
    <span class="nt">&lt;dubbo:protocol</span> <span class="na">name=</span><span class="s">"dubbo"</span> <span class="na">port=</span><span class="s">"20880"</span> <span class="nt">/&gt;</span>
    <span class="nt">&lt;dubbo:protocol</span> <span class="na">name=</span><span class="s">"rmi"</span> <span class="na">port=</span><span class="s">"1099"</span> <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 使用dubbo协议暴露服务 --&gt;</span>
    <span class="nt">&lt;dubbo:service</span> <span class="na">interface=</span><span class="s">"com.alibaba.hello.api.HelloService"</span> <span class="na">version=</span><span class="s">"1.0.0"</span> <span class="na">ref=</span><span class="s">"helloService"</span> <span class="na">protocol=</span><span class="s">"dubbo"</span> <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 使用rmi协议暴露服务 --&gt;</span>
    <span class="nt">&lt;dubbo:service</span> <span class="na">interface=</span><span class="s">"com.alibaba.hello.api.DemoService"</span> <span class="na">version=</span><span class="s">"1.0.0"</span> <span class="na">ref=</span><span class="s">"demoService"</span> <span class="na">protocol=</span><span class="s">"rmi"</span> <span class="nt">/&gt;</span> 
<span class="nt">&lt;/beans&gt;</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>多协议暴露服务
</code></pre></div></div>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;beans</span> <span class="na">xmlns=</span><span class="s">"http://www.springframework.org/schema/beans"</span>
    <span class="na">xmlns:xsi=</span><span class="s">"http://www.w3.org/2001/XMLSchema-instance"</span>
    <span class="na">xmlns:dubbo=</span><span class="s">"http://dubbo.apache.org/schema/dubbo"</span>
    <span class="na">xsi:schemaLocation=</span><span class="s">"http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd"</span><span class="nt">&gt;</span>
    <span class="nt">&lt;dubbo:application</span> <span class="na">name=</span><span class="s">"world"</span>  <span class="nt">/&gt;</span>
    <span class="nt">&lt;dubbo:registry</span> <span class="na">id=</span><span class="s">"registry"</span> <span class="na">address=</span><span class="s">"10.20.141.150:9090"</span> <span class="na">username=</span><span class="s">"admin"</span> <span class="na">password=</span><span class="s">"hello1234"</span> <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 多协议配置 --&gt;</span>
    <span class="nt">&lt;dubbo:protocol</span> <span class="na">name=</span><span class="s">"dubbo"</span> <span class="na">port=</span><span class="s">"20880"</span> <span class="nt">/&gt;</span>
    <span class="nt">&lt;dubbo:protocol</span> <span class="na">name=</span><span class="s">"hessian"</span> <span class="na">port=</span><span class="s">"8080"</span> <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 使用多个协议暴露服务 --&gt;</span>
    <span class="nt">&lt;dubbo:service</span> <span class="na">id=</span><span class="s">"helloService"</span> <span class="na">interface=</span><span class="s">"com.alibaba.hello.api.HelloService"</span> <span class="na">version=</span><span class="s">"1.0.0"</span> <span class="na">protocol=</span><span class="s">"dubbo,hessian"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/beans&gt;</span>
</code></pre></div></div>

<h2 id="多注册中心">多注册中心</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>多注册中心注册
</code></pre></div></div>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="cp">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span>
<span class="nt">&lt;beans</span> <span class="na">xmlns=</span><span class="s">"http://www.springframework.org/schema/beans"</span>
    <span class="na">xmlns:xsi=</span><span class="s">"http://www.w3.org/2001/XMLSchema-instance"</span>
    <span class="na">xmlns:dubbo=</span><span class="s">"http://dubbo.apache.org/schema/dubbo"</span>
    <span class="na">xsi:schemaLocation=</span><span class="s">"http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd"</span><span class="nt">&gt;</span>
    <span class="nt">&lt;dubbo:application</span> <span class="na">name=</span><span class="s">"world"</span>  <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 多注册中心配置 --&gt;</span>
    <span class="nt">&lt;dubbo:registry</span> <span class="na">id=</span><span class="s">"hangzhouRegistry"</span> <span class="na">address=</span><span class="s">"10.20.141.150:9090"</span> <span class="nt">/&gt;</span>
    <span class="nt">&lt;dubbo:registry</span> <span class="na">id=</span><span class="s">"qingdaoRegistry"</span> <span class="na">address=</span><span class="s">"10.20.141.151:9010"</span> <span class="na">default=</span><span class="s">"false"</span> <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 向多个注册中心注册 --&gt;</span>
    <span class="nt">&lt;dubbo:service</span> <span class="na">interface=</span><span class="s">"com.alibaba.hello.api.HelloService"</span> <span class="na">version=</span><span class="s">"1.0.0"</span> <span class="na">ref=</span><span class="s">"helloService"</span> <span class="na">registry=</span><span class="s">"hangzhouRegistry,qingdaoRegistry"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/beans&gt;</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>不同服务不同注册中心
</code></pre></div></div>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="cp">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span>
<span class="nt">&lt;beans</span> <span class="na">xmlns=</span><span class="s">"http://www.springframework.org/schema/beans"</span>
    <span class="na">xmlns:xsi=</span><span class="s">"http://www.w3.org/2001/XMLSchema-instance"</span>
    <span class="na">xmlns:dubbo=</span><span class="s">"http://dubbo.apache.org/schema/dubbo"</span>
    <span class="na">xsi:schemaLocation=</span><span class="s">"http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd"</span><span class="nt">&gt;</span>
    <span class="nt">&lt;dubbo:application</span> <span class="na">name=</span><span class="s">"world"</span>  <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 多注册中心配置 --&gt;</span>
    <span class="nt">&lt;dubbo:registry</span> <span class="na">id=</span><span class="s">"chinaRegistry"</span> <span class="na">address=</span><span class="s">"10.20.141.150:9090"</span> <span class="nt">/&gt;</span>
    <span class="nt">&lt;dubbo:registry</span> <span class="na">id=</span><span class="s">"intlRegistry"</span> <span class="na">address=</span><span class="s">"10.20.154.177:9010"</span> <span class="na">default=</span><span class="s">"false"</span> <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 向中文站注册中心注册 --&gt;</span>
    <span class="nt">&lt;dubbo:service</span> <span class="na">interface=</span><span class="s">"com.alibaba.hello.api.HelloService"</span> <span class="na">version=</span><span class="s">"1.0.0"</span> <span class="na">ref=</span><span class="s">"helloService"</span> <span class="na">registry=</span><span class="s">"chinaRegistry"</span> <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 向国际站注册中心注册 --&gt;</span>
    <span class="nt">&lt;dubbo:service</span> <span class="na">interface=</span><span class="s">"com.alibaba.hello.api.DemoService"</span> <span class="na">version=</span><span class="s">"1.0.0"</span> <span class="na">ref=</span><span class="s">"demoService"</span> <span class="na">registry=</span><span class="s">"intlRegistry"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/beans&gt;</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>多注册中心引用
</code></pre></div></div>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="cp">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span>
<span class="nt">&lt;beans</span> <span class="na">xmlns=</span><span class="s">"http://www.springframework.org/schema/beans"</span>
    <span class="na">xmlns:xsi=</span><span class="s">"http://www.w3.org/2001/XMLSchema-instance"</span>
    <span class="na">xmlns:dubbo=</span><span class="s">"http://dubbo.apache.org/schema/dubbo"</span>
    <span class="na">xsi:schemaLocation=</span><span class="s">"http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd"</span><span class="nt">&gt;</span>
    <span class="nt">&lt;dubbo:application</span> <span class="na">name=</span><span class="s">"world"</span>  <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 多注册中心配置 --&gt;</span>
    <span class="nt">&lt;dubbo:registry</span> <span class="na">id=</span><span class="s">"chinaRegistry"</span> <span class="na">address=</span><span class="s">"10.20.141.150:9090"</span> <span class="nt">/&gt;</span>
    <span class="nt">&lt;dubbo:registry</span> <span class="na">id=</span><span class="s">"intlRegistry"</span> <span class="na">address=</span><span class="s">"10.20.154.177:9010"</span> <span class="na">default=</span><span class="s">"false"</span> <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 引用中文站服务 --&gt;</span>
    <span class="nt">&lt;dubbo:reference</span> <span class="na">id=</span><span class="s">"chinaHelloService"</span> <span class="na">interface=</span><span class="s">"com.alibaba.hello.api.HelloService"</span> <span class="na">version=</span><span class="s">"1.0.0"</span> <span class="na">registry=</span><span class="s">"chinaRegistry"</span> <span class="nt">/&gt;</span>
    <span class="c">&lt;!-- 引用国际站站服务 --&gt;</span>
    <span class="nt">&lt;dubbo:reference</span> <span class="na">id=</span><span class="s">"intlHelloService"</span> <span class="na">interface=</span><span class="s">"com.alibaba.hello.api.HelloService"</span> <span class="na">version=</span><span class="s">"1.0.0"</span> <span class="na">registry=</span><span class="s">"intlRegistry"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/beans&gt;</span>
</code></pre></div></div>

<h2 id="服务分组">服务分组</h2>

<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c">&lt;!--provider--&gt;</span>
<span class="nt">&lt;dubbo:service</span> <span class="na">group=</span><span class="s">"feedback"</span> <span class="na">interface=</span><span class="s">"com.xxx.IndexService"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;dubbo:service</span> <span class="na">group=</span><span class="s">"member"</span> <span class="na">interface=</span><span class="s">"com.xxx.IndexService"</span> <span class="nt">/&gt;</span>
<span class="c">&lt;!--consumer--&gt;</span>
<span class="nt">&lt;dubbo:reference</span> <span class="na">id=</span><span class="s">"feedbackIndexService"</span> <span class="na">group=</span><span class="s">"feedback"</span> <span class="na">interface=</span><span class="s">"com.xxx.IndexService"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;dubbo:reference</span> <span class="na">id=</span><span class="s">"memberIndexService"</span> <span class="na">group=</span><span class="s">"member"</span> <span class="na">interface=</span><span class="s">"com.xxx.IndexService"</span> <span class="nt">/&gt;</span>
<span class="c">&lt;!--任意组--&gt;</span>
<span class="nt">&lt;dubbo:reference</span> <span class="na">id=</span><span class="s">"barService"</span> <span class="na">interface=</span><span class="s">"com.foo.BarService"</span> <span class="na">group=</span><span class="s">"*"</span> <span class="nt">/&gt;</span>
</code></pre></div></div>

<h2 id="多版本">多版本</h2>

<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;dubbo:service</span> <span class="na">interface=</span><span class="s">"com.foo.BarService"</span> <span class="na">version=</span><span class="s">"1.0.0"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;dubbo:service</span> <span class="na">interface=</span><span class="s">"com.foo.BarService"</span> <span class="na">version=</span><span class="s">"2.0.0"</span> <span class="nt">/&gt;</span>

<span class="c">&lt;!--consumer--&gt;</span>
<span class="nt">&lt;dubbo:reference</span> <span class="na">id=</span><span class="s">"barService"</span> <span class="na">interface=</span><span class="s">"com.foo.BarService"</span> <span class="na">version=</span><span class="s">"1.0.0"</span> <span class="nt">/&gt;</span>
<span class="c">&lt;!--任意版本--&gt;</span>
<span class="nt">&lt;dubbo:reference</span> <span class="na">id=</span><span class="s">"barService"</span> <span class="na">interface=</span><span class="s">"com.foo.BarService"</span> <span class="na">version=</span><span class="s">"*"</span> <span class="nt">/&gt;</span>
</code></pre></div></div>

<h2 id="dubbo-spi">Dubbo SPI</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">class</span> <span class="nc">DubboSPITest</span> <span class="o">{</span>
    <span class="nd">@Test</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">sayHello</span><span class="o">()</span> <span class="kd">throws</span> <span class="nc">Exception</span> <span class="o">{</span>
        <span class="nc">ExtensionLoader</span><span class="o">&lt;</span><span class="nc">Robot</span><span class="o">&gt;</span> <span class="n">extensionLoader</span> <span class="o">=</span> 
            <span class="nc">ExtensionLoader</span><span class="o">.</span><span class="na">getExtensionLoader</span><span class="o">(</span><span class="nc">Robot</span><span class="o">.</span><span class="na">class</span><span class="o">);</span>
        <span class="nc">Robot</span> <span class="n">optimusPrime</span> <span class="o">=</span> <span class="n">extensionLoader</span><span class="o">.</span><span class="na">getExtension</span><span class="o">(</span><span class="s">"optimusPrime"</span><span class="o">);</span>
        <span class="n">optimusPrime</span><span class="o">.</span><span class="na">sayHello</span><span class="o">();</span>
        <span class="nc">Robot</span> <span class="n">bumblebee</span> <span class="o">=</span> <span class="n">extensionLoader</span><span class="o">.</span><span class="na">getExtension</span><span class="o">(</span><span class="s">"bumblebee"</span><span class="o">);</span>
        <span class="n">bumblebee</span><span class="o">.</span><span class="na">sayHello</span><span class="o">();</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>调用链
</code></pre></div></div>
<pre><code class="language-mermaid">graph TD;
    id1(getExtension)
    id2(createExtension)
    id3(getExtensionClasses)
    id4(loadExtensionClasses)
    id5(loadDirectory)
    id6(loadResource)
    id7(loadClass)

    id1--cacheInstances缓存未命中--&gt;id2
    id2--&gt;id3
    id3--cachedClasses缓存未命中--&gt;id4
    id4--&gt;id5
    id5--&gt;id6
    id6--&gt;id7
</code></pre>

<h1 id="主要类">主要类</h1>

<h2 id="directory">Directory</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">interface</span> <span class="nc">Directory</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="kd">extends</span> <span class="nc">Node</span> <span class="o">{</span>
    <span class="nc">Class</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nf">getInterface</span><span class="o">();</span>
    <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="nf">list</span><span class="o">(</span><span class="nc">Invocation</span> <span class="n">invocation</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>RegistryDirectory
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="nf">doList</span><span class="o">(</span><span class="nc">Invocation</span> <span class="n">invocation</span><span class="o">)</span> <span class="o">{</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">forbidden</span><span class="o">)</span> <span class="o">{</span>
        <span class="c1">// 服务提供者关闭或禁用了服务，此时抛出 No provider 异常</span>
        <span class="k">throw</span> <span class="k">new</span> <span class="nf">RpcException</span><span class="o">(</span><span class="nc">RpcException</span><span class="o">.</span><span class="na">FORBIDDEN_EXCEPTION</span><span class="o">,</span>
            <span class="s">"No provider available from registry ..."</span><span class="o">);</span>
    <span class="o">}</span>
    <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">invokers</span> <span class="o">=</span> <span class="kc">null</span><span class="o">;</span>
    <span class="c1">// 获取 Invoker 本地缓存</span>
    <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;</span> <span class="n">localMethodInvokerMap</span> <span class="o">=</span> <span class="k">this</span><span class="o">.</span><span class="na">methodInvokerMap</span><span class="o">;</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">localMethodInvokerMap</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">localMethodInvokerMap</span><span class="o">.</span><span class="na">size</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
        <span class="c1">// 获取方法名和参数列表</span>
        <span class="nc">String</span> <span class="n">methodName</span> <span class="o">=</span> <span class="nc">RpcUtils</span><span class="o">.</span><span class="na">getMethodName</span><span class="o">(</span><span class="n">invocation</span><span class="o">);</span>
        <span class="nc">Object</span><span class="o">[]</span> <span class="n">args</span> <span class="o">=</span> <span class="nc">RpcUtils</span><span class="o">.</span><span class="na">getArguments</span><span class="o">(</span><span class="n">invocation</span><span class="o">);</span>
        <span class="c1">// 检测参数列表的第一个参数是否为 String 或 enum 类型</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">args</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">args</span><span class="o">.</span><span class="na">length</span> <span class="o">&gt;</span> <span class="mi">0</span> <span class="o">&amp;&amp;</span> <span class="n">args</span><span class="o">[</span><span class="mi">0</span><span class="o">]</span> <span class="o">!=</span> <span class="kc">null</span>
                <span class="o">&amp;&amp;</span> <span class="o">(</span><span class="n">args</span><span class="o">[</span><span class="mi">0</span><span class="o">]</span> <span class="k">instanceof</span> <span class="nc">String</span> <span class="o">||</span> <span class="n">args</span><span class="o">[</span><span class="mi">0</span><span class="o">].</span><span class="na">getClass</span><span class="o">().</span><span class="na">isEnum</span><span class="o">()))</span> <span class="o">{</span>
            <span class="c1">// 通过 方法名 + 第一个参数名称 查询 Invoker 列表，具体的使用场景暂时没想到</span>
            <span class="n">invokers</span> <span class="o">=</span> <span class="n">localMethodInvokerMap</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">methodName</span> <span class="o">+</span> <span class="s">"."</span> <span class="o">+</span> <span class="n">args</span><span class="o">[</span><span class="mi">0</span><span class="o">]);</span>
        <span class="o">}</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">invokers</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
            <span class="c1">// 通过方法名获取 Invoker 列表</span>
            <span class="n">invokers</span> <span class="o">=</span> <span class="n">localMethodInvokerMap</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">methodName</span><span class="o">);</span>
        <span class="o">}</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">invokers</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
            <span class="c1">// 通过星号 * 获取 Invoker 列表</span>
            <span class="n">invokers</span> <span class="o">=</span> <span class="n">localMethodInvokerMap</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">ANY_VALUE</span><span class="o">);</span>
        <span class="o">}</span>
        
        <span class="c1">// 冗余逻辑，pull request #2861 移除了下面的 if 分支代码</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">invokers</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
            <span class="nc">Iterator</span><span class="o">&lt;</span><span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;</span> <span class="n">iterator</span> <span class="o">=</span> <span class="n">localMethodInvokerMap</span><span class="o">.</span><span class="na">values</span><span class="o">().</span><span class="na">iterator</span><span class="o">();</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">iterator</span><span class="o">.</span><span class="na">hasNext</span><span class="o">())</span> <span class="o">{</span>
                <span class="n">invokers</span> <span class="o">=</span> <span class="n">iterator</span><span class="o">.</span><span class="na">next</span><span class="o">();</span>
            <span class="o">}</span>
        <span class="o">}</span>
    <span class="o">}</span>

	<span class="c1">// 返回 Invoker 列表</span>
    <span class="k">return</span> <span class="n">invokers</span> <span class="o">==</span> <span class="kc">null</span> <span class="o">?</span> <span class="k">new</span> <span class="nc">ArrayList</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;(</span><span class="mi">0</span><span class="o">)</span> <span class="o">:</span> <span class="n">invokers</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>因为它实现了NotifyListener接口,所以每次注册中心发送变化都会执行notify
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">synchronized</span> <span class="kt">void</span> <span class="nf">notify</span><span class="o">(</span><span class="nc">List</span><span class="o">&lt;</span><span class="no">URL</span><span class="o">&gt;</span> <span class="n">urls</span><span class="o">)</span> <span class="o">{</span>
    <span class="c1">// 定义三个集合，分别用于存放服务提供者 url，路由 url，配置器 url</span>
    <span class="nc">List</span><span class="o">&lt;</span><span class="no">URL</span><span class="o">&gt;</span> <span class="n">invokerUrls</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ArrayList</span><span class="o">&lt;</span><span class="no">URL</span><span class="o">&gt;();</span>
    <span class="nc">List</span><span class="o">&lt;</span><span class="no">URL</span><span class="o">&gt;</span> <span class="n">routerUrls</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ArrayList</span><span class="o">&lt;</span><span class="no">URL</span><span class="o">&gt;();</span>
    <span class="nc">List</span><span class="o">&lt;</span><span class="no">URL</span><span class="o">&gt;</span> <span class="n">configuratorUrls</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ArrayList</span><span class="o">&lt;</span><span class="no">URL</span><span class="o">&gt;();</span>
    <span class="k">for</span> <span class="o">(</span><span class="no">URL</span> <span class="n">url</span> <span class="o">:</span> <span class="n">urls</span><span class="o">)</span> <span class="o">{</span>
        <span class="nc">String</span> <span class="n">protocol</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getProtocol</span><span class="o">();</span>
        <span class="c1">// 获取 category 参数</span>
        <span class="nc">String</span> <span class="n">category</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">CATEGORY_KEY</span><span class="o">,</span> <span class="nc">Constants</span><span class="o">.</span><span class="na">DEFAULT_CATEGORY</span><span class="o">);</span>
        <span class="c1">// 根据 category 参数将 url 分别放到不同的列表中</span>
        <span class="k">if</span> <span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">ROUTERS_CATEGORY</span><span class="o">.</span><span class="na">equals</span><span class="o">(</span><span class="n">category</span><span class="o">)</span>
                <span class="o">||</span> <span class="nc">Constants</span><span class="o">.</span><span class="na">ROUTE_PROTOCOL</span><span class="o">.</span><span class="na">equals</span><span class="o">(</span><span class="n">protocol</span><span class="o">))</span> <span class="o">{</span>
            <span class="c1">// 添加路由器 url</span>
            <span class="n">routerUrls</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
        <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">CONFIGURATORS_CATEGORY</span><span class="o">.</span><span class="na">equals</span><span class="o">(</span><span class="n">category</span><span class="o">)</span>
                <span class="o">||</span> <span class="nc">Constants</span><span class="o">.</span><span class="na">OVERRIDE_PROTOCOL</span><span class="o">.</span><span class="na">equals</span><span class="o">(</span><span class="n">protocol</span><span class="o">))</span> <span class="o">{</span>
            <span class="c1">// 添加配置器 url</span>
            <span class="n">configuratorUrls</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
        <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">PROVIDERS_CATEGORY</span><span class="o">.</span><span class="na">equals</span><span class="o">(</span><span class="n">category</span><span class="o">))</span> <span class="o">{</span>
            <span class="c1">// 添加服务提供者 url</span>
            <span class="n">invokerUrls</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
        <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
            <span class="c1">// 忽略不支持的 category</span>
            <span class="n">logger</span><span class="o">.</span><span class="na">warn</span><span class="o">(</span><span class="s">"Unsupported category ..."</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">configuratorUrls</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="o">!</span><span class="n">configuratorUrls</span><span class="o">.</span><span class="na">isEmpty</span><span class="o">())</span> <span class="o">{</span>
        <span class="c1">// 将 url 转成 Configurator</span>
        <span class="k">this</span><span class="o">.</span><span class="na">configurators</span> <span class="o">=</span> <span class="n">toConfigurators</span><span class="o">(</span><span class="n">configuratorUrls</span><span class="o">);</span>
    <span class="o">}</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">routerUrls</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="o">!</span><span class="n">routerUrls</span><span class="o">.</span><span class="na">isEmpty</span><span class="o">())</span> <span class="o">{</span>
        <span class="c1">// 将 url 转成 Router</span>
        <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Router</span><span class="o">&gt;</span> <span class="n">routers</span> <span class="o">=</span> <span class="n">toRouters</span><span class="o">(</span><span class="n">routerUrls</span><span class="o">);</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">routers</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
            <span class="n">setRouters</span><span class="o">(</span><span class="n">routers</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>
    <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Configurator</span><span class="o">&gt;</span> <span class="n">localConfigurators</span> <span class="o">=</span> <span class="k">this</span><span class="o">.</span><span class="na">configurators</span><span class="o">;</span>
    <span class="k">this</span><span class="o">.</span><span class="na">overrideDirectoryUrl</span> <span class="o">=</span> <span class="n">directoryUrl</span><span class="o">;</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">localConfigurators</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="o">!</span><span class="n">localConfigurators</span><span class="o">.</span><span class="na">isEmpty</span><span class="o">())</span> <span class="o">{</span>
        <span class="k">for</span> <span class="o">(</span><span class="nc">Configurator</span> <span class="n">configurator</span> <span class="o">:</span> <span class="n">localConfigurators</span><span class="o">)</span> <span class="o">{</span>
            <span class="c1">// 配置 overrideDirectoryUrl</span>
            <span class="k">this</span><span class="o">.</span><span class="na">overrideDirectoryUrl</span> <span class="o">=</span> <span class="n">configurator</span><span class="o">.</span><span class="na">configure</span><span class="o">(</span><span class="n">overrideDirectoryUrl</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>

    <span class="c1">// 刷新 Invoker 列表</span>
    <span class="n">refreshInvoker</span><span class="o">(</span><span class="n">invokerUrls</span><span class="o">);</span>
<span class="o">}</span>
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">private</span> <span class="kt">void</span> <span class="nf">refreshInvoker</span><span class="o">(</span><span class="nc">List</span><span class="o">&lt;</span><span class="no">URL</span><span class="o">&gt;</span> <span class="n">invokerUrls</span><span class="o">)</span> <span class="o">{</span>
    <span class="c1">// invokerUrls 仅有一个元素，且 url 协议头为 empty，此时表示禁用所有服务</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">invokerUrls</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">invokerUrls</span><span class="o">.</span><span class="na">size</span><span class="o">()</span> <span class="o">==</span> <span class="mi">1</span> <span class="o">&amp;&amp;</span> <span class="n">invokerUrls</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="mi">0</span><span class="o">)</span> <span class="o">!=</span> <span class="kc">null</span>
            <span class="o">&amp;&amp;</span> <span class="nc">Constants</span><span class="o">.</span><span class="na">EMPTY_PROTOCOL</span><span class="o">.</span><span class="na">equals</span><span class="o">(</span><span class="n">invokerUrls</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="mi">0</span><span class="o">).</span><span class="na">getProtocol</span><span class="o">()))</span> <span class="o">{</span>
        <span class="c1">// 设置 forbidden 为 true</span>
        <span class="k">this</span><span class="o">.</span><span class="na">forbidden</span> <span class="o">=</span> <span class="kc">true</span><span class="o">;</span>
        <span class="k">this</span><span class="o">.</span><span class="na">methodInvokerMap</span> <span class="o">=</span> <span class="kc">null</span><span class="o">;</span>
        <span class="c1">// 销毁所有 Invoker</span>
        <span class="n">destroyAllInvokers</span><span class="o">();</span>
    <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
        <span class="k">this</span><span class="o">.</span><span class="na">forbidden</span> <span class="o">=</span> <span class="kc">false</span><span class="o">;</span>
        <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">oldUrlInvokerMap</span> <span class="o">=</span> <span class="k">this</span><span class="o">.</span><span class="na">urlInvokerMap</span><span class="o">;</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">invokerUrls</span><span class="o">.</span><span class="na">isEmpty</span><span class="o">()</span> <span class="o">&amp;&amp;</span> <span class="k">this</span><span class="o">.</span><span class="na">cachedInvokerUrls</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
            <span class="c1">// 添加缓存 url 到 invokerUrls 中</span>
            <span class="n">invokerUrls</span><span class="o">.</span><span class="na">addAll</span><span class="o">(</span><span class="k">this</span><span class="o">.</span><span class="na">cachedInvokerUrls</span><span class="o">);</span>
        <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
            <span class="k">this</span><span class="o">.</span><span class="na">cachedInvokerUrls</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">HashSet</span><span class="o">&lt;</span><span class="no">URL</span><span class="o">&gt;();</span>
            <span class="c1">// 缓存 invokerUrls</span>
            <span class="k">this</span><span class="o">.</span><span class="na">cachedInvokerUrls</span><span class="o">.</span><span class="na">addAll</span><span class="o">(</span><span class="n">invokerUrls</span><span class="o">);</span>
        <span class="o">}</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">invokerUrls</span><span class="o">.</span><span class="na">isEmpty</span><span class="o">())</span> <span class="o">{</span>
            <span class="k">return</span><span class="o">;</span>
        <span class="o">}</span>
        <span class="c1">// 将 url 转成 Invoker</span>
        <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">newUrlInvokerMap</span> <span class="o">=</span> <span class="n">toInvokers</span><span class="o">(</span><span class="n">invokerUrls</span><span class="o">);</span>
        <span class="c1">// 将 newUrlInvokerMap 转成方法名到 Invoker 列表的映射</span>
        <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;</span> <span class="n">newMethodInvokerMap</span> <span class="o">=</span> <span class="n">toMethodInvokers</span><span class="o">(</span><span class="n">newUrlInvokerMap</span><span class="o">);</span>
        <span class="c1">// 转换出错，直接打印异常，并返回</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">newUrlInvokerMap</span> <span class="o">==</span> <span class="kc">null</span> <span class="o">||</span> <span class="n">newUrlInvokerMap</span><span class="o">.</span><span class="na">size</span><span class="o">()</span> <span class="o">==</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
            <span class="n">logger</span><span class="o">.</span><span class="na">error</span><span class="o">(</span><span class="k">new</span> <span class="nc">IllegalStateException</span><span class="o">(</span><span class="s">"urls to invokers error ..."</span><span class="o">));</span>
            <span class="k">return</span><span class="o">;</span>
        <span class="o">}</span>
        <span class="c1">// 合并多个组的 Invoker</span>
        <span class="k">this</span><span class="o">.</span><span class="na">methodInvokerMap</span> <span class="o">=</span> <span class="n">multiGroup</span> <span class="o">?</span> <span class="n">toMergeMethodInvokerMap</span><span class="o">(</span><span class="n">newMethodInvokerMap</span><span class="o">)</span> <span class="o">:</span> <span class="n">newMethodInvokerMap</span><span class="o">;</span>
        <span class="k">this</span><span class="o">.</span><span class="na">urlInvokerMap</span> <span class="o">=</span> <span class="n">newUrlInvokerMap</span><span class="o">;</span>
        <span class="k">try</span> <span class="o">{</span>
            <span class="c1">// 销毁无用 Invoker</span>
            <span class="n">destroyUnusedInvokers</span><span class="o">(</span><span class="n">oldUrlInvokerMap</span><span class="o">,</span> <span class="n">newUrlInvokerMap</span><span class="o">);</span>
        <span class="o">}</span> <span class="k">catch</span> <span class="o">(</span><span class="nc">Exception</span> <span class="n">e</span><span class="o">)</span> <span class="o">{</span>
            <span class="n">logger</span><span class="o">.</span><span class="na">warn</span><span class="o">(</span><span class="s">"destroyUnusedInvokers error. "</span><span class="o">,</span> <span class="n">e</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">private</span> <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="nf">toInvokers</span><span class="o">(</span><span class="nc">List</span><span class="o">&lt;</span><span class="no">URL</span><span class="o">&gt;</span> <span class="n">urls</span><span class="o">)</span> <span class="o">{</span>
    <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">newUrlInvokerMap</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">HashMap</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;();</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">urls</span> <span class="o">==</span> <span class="kc">null</span> <span class="o">||</span> <span class="n">urls</span><span class="o">.</span><span class="na">isEmpty</span><span class="o">())</span> <span class="o">{</span>
        <span class="k">return</span> <span class="n">newUrlInvokerMap</span><span class="o">;</span>
    <span class="o">}</span>
    <span class="nc">Set</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;</span> <span class="n">keys</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">HashSet</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;();</span>
    <span class="c1">// 获取服务消费端配置的协议</span>
    <span class="nc">String</span> <span class="n">queryProtocols</span> <span class="o">=</span> <span class="k">this</span><span class="o">.</span><span class="na">queryMap</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">PROTOCOL_KEY</span><span class="o">);</span>
    <span class="k">for</span> <span class="o">(</span><span class="no">URL</span> <span class="n">providerUrl</span> <span class="o">:</span> <span class="n">urls</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">queryProtocols</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">queryProtocols</span><span class="o">.</span><span class="na">length</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
            <span class="kt">boolean</span> <span class="n">accept</span> <span class="o">=</span> <span class="kc">false</span><span class="o">;</span>
            <span class="nc">String</span><span class="o">[]</span> <span class="n">acceptProtocols</span> <span class="o">=</span> <span class="n">queryProtocols</span><span class="o">.</span><span class="na">split</span><span class="o">(</span><span class="s">","</span><span class="o">);</span>
            <span class="c1">// 检测服务提供者协议是否被服务消费者所支持</span>
            <span class="k">for</span> <span class="o">(</span><span class="nc">String</span> <span class="n">acceptProtocol</span> <span class="o">:</span> <span class="n">acceptProtocols</span><span class="o">)</span> <span class="o">{</span>
                <span class="k">if</span> <span class="o">(</span><span class="n">providerUrl</span><span class="o">.</span><span class="na">getProtocol</span><span class="o">().</span><span class="na">equals</span><span class="o">(</span><span class="n">acceptProtocol</span><span class="o">))</span> <span class="o">{</span>
                    <span class="n">accept</span> <span class="o">=</span> <span class="kc">true</span><span class="o">;</span>
                    <span class="k">break</span><span class="o">;</span>
                <span class="o">}</span>
            <span class="o">}</span>
            <span class="k">if</span> <span class="o">(!</span><span class="n">accept</span><span class="o">)</span> <span class="o">{</span>
                <span class="c1">// 若服务消费者协议头不被消费者所支持，则忽略当前 providerUrl</span>
                <span class="k">continue</span><span class="o">;</span>
            <span class="o">}</span>
        <span class="o">}</span>
        <span class="c1">// 忽略 empty 协议</span>
        <span class="k">if</span> <span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">EMPTY_PROTOCOL</span><span class="o">.</span><span class="na">equals</span><span class="o">(</span><span class="n">providerUrl</span><span class="o">.</span><span class="na">getProtocol</span><span class="o">()))</span> <span class="o">{</span>
            <span class="k">continue</span><span class="o">;</span>
        <span class="o">}</span>
        <span class="c1">// 通过 SPI 检测服务端协议是否被消费端支持，不支持则抛出异常</span>
        <span class="k">if</span> <span class="o">(!</span><span class="nc">ExtensionLoader</span><span class="o">.</span><span class="na">getExtensionLoader</span><span class="o">(</span><span class="nc">Protocol</span><span class="o">.</span><span class="na">class</span><span class="o">).</span><span class="na">hasExtension</span><span class="o">(</span><span class="n">providerUrl</span><span class="o">.</span><span class="na">getProtocol</span><span class="o">()))</span> <span class="o">{</span>
            <span class="n">logger</span><span class="o">.</span><span class="na">error</span><span class="o">(</span><span class="k">new</span> <span class="nc">IllegalStateException</span><span class="o">(</span><span class="s">"Unsupported protocol..."</span><span class="o">));</span>
            <span class="k">continue</span><span class="o">;</span>
        <span class="o">}</span>
        
        <span class="c1">// 合并 url</span>
        <span class="no">URL</span> <span class="n">url</span> <span class="o">=</span> <span class="n">mergeUrl</span><span class="o">(</span><span class="n">providerUrl</span><span class="o">);</span>

        <span class="nc">String</span> <span class="n">key</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">toFullString</span><span class="o">();</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">keys</span><span class="o">.</span><span class="na">contains</span><span class="o">(</span><span class="n">key</span><span class="o">))</span> <span class="o">{</span>
            <span class="c1">// 忽略重复 url</span>
            <span class="k">continue</span><span class="o">;</span>
        <span class="o">}</span>
        <span class="n">keys</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">key</span><span class="o">);</span>
        <span class="c1">// 将本地 Invoker 缓存赋值给 localUrlInvokerMap</span>
        <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">localUrlInvokerMap</span> <span class="o">=</span> <span class="k">this</span><span class="o">.</span><span class="na">urlInvokerMap</span><span class="o">;</span>
        <span class="c1">// 获取与 url 对应的 Invoker</span>
        <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">invoker</span> <span class="o">=</span> <span class="n">localUrlInvokerMap</span> <span class="o">==</span> <span class="kc">null</span> <span class="o">?</span> <span class="kc">null</span> <span class="o">:</span> <span class="n">localUrlInvokerMap</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">key</span><span class="o">);</span>
        <span class="c1">// 缓存未命中</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">invoker</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
            <span class="k">try</span> <span class="o">{</span>
                <span class="kt">boolean</span> <span class="n">enabled</span> <span class="o">=</span> <span class="kc">true</span><span class="o">;</span>
                <span class="k">if</span> <span class="o">(</span><span class="n">url</span><span class="o">.</span><span class="na">hasParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">DISABLED_KEY</span><span class="o">))</span> <span class="o">{</span>
                    <span class="c1">// 获取 disable 配置，取反，然后赋值给 enable 变量</span>
                    <span class="n">enabled</span> <span class="o">=</span> <span class="o">!</span><span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">DISABLED_KEY</span><span class="o">,</span> <span class="kc">false</span><span class="o">);</span>
                <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
                    <span class="c1">// 获取 enable 配置，并赋值给 enable 变量</span>
                    <span class="n">enabled</span> <span class="o">=</span> <span class="n">url</span><span class="o">.</span><span class="na">getParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">ENABLED_KEY</span><span class="o">,</span> <span class="kc">true</span><span class="o">);</span>
                <span class="o">}</span>
                <span class="k">if</span> <span class="o">(</span><span class="n">enabled</span><span class="o">)</span> <span class="o">{</span>
                    <span class="c1">// 调用 refer 获取 Invoker</span>
                    <span class="n">invoker</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">InvokerDelegate</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;(</span><span class="n">protocol</span><span class="o">.</span><span class="na">refer</span><span class="o">(</span><span class="n">serviceType</span><span class="o">,</span> <span class="n">url</span><span class="o">),</span> <span class="n">url</span><span class="o">,</span> <span class="n">providerUrl</span><span class="o">);</span>
                <span class="o">}</span>
            <span class="o">}</span> <span class="k">catch</span> <span class="o">(</span><span class="nc">Throwable</span> <span class="n">t</span><span class="o">)</span> <span class="o">{</span>
                <span class="n">logger</span><span class="o">.</span><span class="na">error</span><span class="o">(</span><span class="s">"Failed to refer invoker for interface..."</span><span class="o">);</span>
            <span class="o">}</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">invoker</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
                <span class="c1">// 缓存 Invoker 实例</span>
                <span class="n">newUrlInvokerMap</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">key</span><span class="o">,</span> <span class="n">invoker</span><span class="o">);</span>
            <span class="o">}</span>
            
        <span class="c1">// 缓存命中</span>
        <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
            <span class="c1">// 将 invoker 存储到 newUrlInvokerMap 中</span>
            <span class="n">newUrlInvokerMap</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">key</span><span class="o">,</span> <span class="n">invoker</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>
    <span class="n">keys</span><span class="o">.</span><span class="na">clear</span><span class="o">();</span>
    <span class="k">return</span> <span class="n">newUrlInvokerMap</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">private</span> <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;</span> <span class="nf">toMethodInvokers</span><span class="o">(</span><span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">invokersMap</span><span class="o">)</span> <span class="o">{</span>
    <span class="c1">// 方法名 -&gt; Invoker 列表</span>
    <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;</span> <span class="n">newMethodInvokerMap</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">HashMap</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;();</span>
    <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">invokersList</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ArrayList</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;();</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">invokersMap</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">invokersMap</span><span class="o">.</span><span class="na">size</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">for</span> <span class="o">(</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">invoker</span> <span class="o">:</span> <span class="n">invokersMap</span><span class="o">.</span><span class="na">values</span><span class="o">())</span> <span class="o">{</span>
            <span class="c1">// 获取 methods 参数</span>
            <span class="nc">String</span> <span class="n">parameter</span> <span class="o">=</span> <span class="n">invoker</span><span class="o">.</span><span class="na">getUrl</span><span class="o">().</span><span class="na">getParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">METHODS_KEY</span><span class="o">);</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">parameter</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">parameter</span><span class="o">.</span><span class="na">length</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
                <span class="c1">// 切分 methods 参数值，得到方法名数组</span>
                <span class="nc">String</span><span class="o">[]</span> <span class="n">methods</span> <span class="o">=</span> <span class="nc">Constants</span><span class="o">.</span><span class="na">COMMA_SPLIT_PATTERN</span><span class="o">.</span><span class="na">split</span><span class="o">(</span><span class="n">parameter</span><span class="o">);</span>
                <span class="k">if</span> <span class="o">(</span><span class="n">methods</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">methods</span><span class="o">.</span><span class="na">length</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
                    <span class="k">for</span> <span class="o">(</span><span class="nc">String</span> <span class="n">method</span> <span class="o">:</span> <span class="n">methods</span><span class="o">)</span> <span class="o">{</span>
                        <span class="c1">// 方法名不为 *</span>
                        <span class="k">if</span> <span class="o">(</span><span class="n">method</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">method</span><span class="o">.</span><span class="na">length</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">0</span>
                                <span class="o">&amp;&amp;</span> <span class="o">!</span><span class="nc">Constants</span><span class="o">.</span><span class="na">ANY_VALUE</span><span class="o">.</span><span class="na">equals</span><span class="o">(</span><span class="n">method</span><span class="o">))</span> <span class="o">{</span>
                            <span class="c1">// 根据方法名获取 Invoker 列表</span>
                            <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">methodInvokers</span> <span class="o">=</span> <span class="n">newMethodInvokerMap</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">method</span><span class="o">);</span>
                            <span class="k">if</span> <span class="o">(</span><span class="n">methodInvokers</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
                                <span class="n">methodInvokers</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ArrayList</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;();</span>
                                <span class="n">newMethodInvokerMap</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">method</span><span class="o">,</span> <span class="n">methodInvokers</span><span class="o">);</span>
                            <span class="o">}</span>
                            <span class="c1">// 存储 Invoker 到列表中</span>
                            <span class="n">methodInvokers</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">invoker</span><span class="o">);</span>
                        <span class="o">}</span>
                    <span class="o">}</span>
                <span class="o">}</span>
            <span class="o">}</span>
            <span class="n">invokersList</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">invoker</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>
    
    <span class="c1">// 进行服务级别路由，参考 pull request #749</span>
    <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">newInvokersList</span> <span class="o">=</span> <span class="n">route</span><span class="o">(</span><span class="n">invokersList</span><span class="o">,</span> <span class="kc">null</span><span class="o">);</span>
    <span class="c1">// 存储 &lt;*, newInvokersList&gt; 映射关系</span>
    <span class="n">newMethodInvokerMap</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">ANY_VALUE</span><span class="o">,</span> <span class="n">newInvokersList</span><span class="o">);</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">serviceMethods</span> <span class="o">!=</span> <span class="kc">null</span> <span class="o">&amp;&amp;</span> <span class="n">serviceMethods</span><span class="o">.</span><span class="na">length</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">for</span> <span class="o">(</span><span class="nc">String</span> <span class="n">method</span> <span class="o">:</span> <span class="n">serviceMethods</span><span class="o">)</span> <span class="o">{</span>
            <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">methodInvokers</span> <span class="o">=</span> <span class="n">newMethodInvokerMap</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">method</span><span class="o">);</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">methodInvokers</span> <span class="o">==</span> <span class="kc">null</span> <span class="o">||</span> <span class="n">methodInvokers</span><span class="o">.</span><span class="na">isEmpty</span><span class="o">())</span> <span class="o">{</span>
                <span class="n">methodInvokers</span> <span class="o">=</span> <span class="n">newInvokersList</span><span class="o">;</span>
            <span class="o">}</span>
            <span class="c1">// 进行方法级别路由</span>
            <span class="n">newMethodInvokerMap</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">method</span><span class="o">,</span> <span class="n">route</span><span class="o">(</span><span class="n">methodInvokers</span><span class="o">,</span> <span class="n">method</span><span class="o">));</span>
        <span class="o">}</span>
    <span class="o">}</span>
    <span class="c1">// 排序，转成不可变列表</span>
    <span class="k">for</span> <span class="o">(</span><span class="nc">String</span> <span class="n">method</span> <span class="o">:</span> <span class="k">new</span> <span class="nc">HashSet</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;(</span><span class="n">newMethodInvokerMap</span><span class="o">.</span><span class="na">keySet</span><span class="o">()))</span> <span class="o">{</span>
        <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">methodInvokers</span> <span class="o">=</span> <span class="n">newMethodInvokerMap</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">method</span><span class="o">);</span>
        <span class="nc">Collections</span><span class="o">.</span><span class="na">sort</span><span class="o">(</span><span class="n">methodInvokers</span><span class="o">,</span> <span class="nc">InvokerComparator</span><span class="o">.</span><span class="na">getComparator</span><span class="o">());</span>
        <span class="n">newMethodInvokerMap</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">method</span><span class="o">,</span> <span class="nc">Collections</span><span class="o">.</span><span class="na">unmodifiableList</span><span class="o">(</span><span class="n">methodInvokers</span><span class="o">));</span>
    <span class="o">}</span>
    <span class="k">return</span> <span class="nc">Collections</span><span class="o">.</span><span class="na">unmodifiableMap</span><span class="o">(</span><span class="n">newMethodInvokerMap</span><span class="o">);</span>
<span class="o">}</span>
<span class="kd">private</span> <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;</span> <span class="nf">toMergeMethodInvokerMap</span><span class="o">(</span><span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;</span> <span class="n">methodMap</span><span class="o">)</span> <span class="o">{</span>
    <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;</span> <span class="n">result</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">HashMap</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;();</span>
    <span class="c1">// 遍历入参</span>
    <span class="k">for</span> <span class="o">(</span><span class="nc">Map</span><span class="o">.</span><span class="na">Entry</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;</span> <span class="n">entry</span> <span class="o">:</span> <span class="n">methodMap</span><span class="o">.</span><span class="na">entrySet</span><span class="o">())</span> <span class="o">{</span>
        <span class="nc">String</span> <span class="n">method</span> <span class="o">=</span> <span class="n">entry</span><span class="o">.</span><span class="na">getKey</span><span class="o">();</span>
        <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">invokers</span> <span class="o">=</span> <span class="n">entry</span><span class="o">.</span><span class="na">getValue</span><span class="o">();</span>
        <span class="c1">// group -&gt; Invoker 列表</span>
        <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;</span> <span class="n">groupMap</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">HashMap</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;&gt;();</span>
        <span class="c1">// 遍历 Invoker 列表</span>
        <span class="k">for</span> <span class="o">(</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">invoker</span> <span class="o">:</span> <span class="n">invokers</span><span class="o">)</span> <span class="o">{</span>
            <span class="c1">// 获取分组配置</span>
            <span class="nc">String</span> <span class="n">group</span> <span class="o">=</span> <span class="n">invoker</span><span class="o">.</span><span class="na">getUrl</span><span class="o">().</span><span class="na">getParameter</span><span class="o">(</span><span class="nc">Constants</span><span class="o">.</span><span class="na">GROUP_KEY</span><span class="o">,</span> <span class="s">""</span><span class="o">);</span>
            <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">groupInvokers</span> <span class="o">=</span> <span class="n">groupMap</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="n">group</span><span class="o">);</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">groupInvokers</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
                <span class="n">groupInvokers</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ArrayList</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;();</span>
                <span class="c1">// 缓存 &lt;group, List&lt;Invoker&gt;&gt; 到 groupMap 中</span>
                <span class="n">groupMap</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">group</span><span class="o">,</span> <span class="n">groupInvokers</span><span class="o">);</span>
            <span class="o">}</span>
            <span class="c1">// 存储 invoker 到 groupInvokers</span>
            <span class="n">groupInvokers</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">invoker</span><span class="o">);</span>
        <span class="o">}</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">groupMap</span><span class="o">.</span><span class="na">size</span><span class="o">()</span> <span class="o">==</span> <span class="mi">1</span><span class="o">)</span> <span class="o">{</span>
            <span class="c1">// 如果 groupMap 中仅包含一组键值对，此时直接取出该键值对的值即可</span>
            <span class="n">result</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">method</span><span class="o">,</span> <span class="n">groupMap</span><span class="o">.</span><span class="na">values</span><span class="o">().</span><span class="na">iterator</span><span class="o">().</span><span class="na">next</span><span class="o">());</span>
        
        <span class="c1">// groupMap.size() &gt; 1 成立，表示 groupMap 中包含多组键值对，比如：</span>
        <span class="c1">// {</span>
        <span class="c1">//     "dubbo": [invoker1, invoker2, invoker3, ...],</span>
        <span class="c1">//     "hello": [invoker4, invoker5, invoker6, ...]</span>
        <span class="c1">// }</span>
        <span class="o">}</span> <span class="k">else</span> <span class="k">if</span> <span class="o">(</span><span class="n">groupMap</span><span class="o">.</span><span class="na">size</span><span class="o">()</span> <span class="o">&gt;</span> <span class="mi">1</span><span class="o">)</span> <span class="o">{</span>
            <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">groupInvokers</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ArrayList</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;();</span>
            <span class="k">for</span> <span class="o">(</span><span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">groupList</span> <span class="o">:</span> <span class="n">groupMap</span><span class="o">.</span><span class="na">values</span><span class="o">())</span> <span class="o">{</span>
                <span class="c1">// 通过集群类合并每个分组对应的 Invoker 列表</span>
                <span class="n">groupInvokers</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">cluster</span><span class="o">.</span><span class="na">join</span><span class="o">(</span><span class="k">new</span> <span class="nc">StaticDirectory</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;(</span><span class="n">groupList</span><span class="o">)));</span>
            <span class="o">}</span>
            <span class="c1">// 缓存结果</span>
            <span class="n">result</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">method</span><span class="o">,</span> <span class="n">groupInvokers</span><span class="o">);</span>
        <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
            <span class="n">result</span><span class="o">.</span><span class="na">put</span><span class="o">(</span><span class="n">method</span><span class="o">,</span> <span class="n">invokers</span><span class="o">);</span>
        <span class="o">}</span>
    <span class="o">}</span>
    <span class="k">return</span> <span class="n">result</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">private</span> <span class="kt">void</span> <span class="nf">destroyUnusedInvokers</span><span class="o">(</span><span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">oldUrlInvokerMap</span><span class="o">,</span> <span class="nc">Map</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">newUrlInvokerMap</span><span class="o">)</span> <span class="o">{</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">newUrlInvokerMap</span> <span class="o">==</span> <span class="kc">null</span> <span class="o">||</span> <span class="n">newUrlInvokerMap</span><span class="o">.</span><span class="na">size</span><span class="o">()</span> <span class="o">==</span> <span class="mi">0</span><span class="o">)</span> <span class="o">{</span>
        <span class="n">destroyAllInvokers</span><span class="o">();</span>
        <span class="k">return</span><span class="o">;</span>
    <span class="o">}</span>
   
    <span class="nc">List</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;</span> <span class="n">deleted</span> <span class="o">=</span> <span class="kc">null</span><span class="o">;</span>
    <span class="k">if</span> <span class="o">(</span><span class="n">oldUrlInvokerMap</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
        <span class="c1">// 获取新生成的 Invoker 列表</span>
        <span class="nc">Collection</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">newInvokers</span> <span class="o">=</span> <span class="n">newUrlInvokerMap</span><span class="o">.</span><span class="na">values</span><span class="o">();</span>
        <span class="c1">// 遍历老的 &lt;url, Invoker&gt; 映射表</span>
        <span class="k">for</span> <span class="o">(</span><span class="nc">Map</span><span class="o">.</span><span class="na">Entry</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">,</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">entry</span> <span class="o">:</span> <span class="n">oldUrlInvokerMap</span><span class="o">.</span><span class="na">entrySet</span><span class="o">())</span> <span class="o">{</span>
            <span class="c1">// 检测 newInvokers 中是否包含老的 Invoker</span>
            <span class="k">if</span> <span class="o">(!</span><span class="n">newInvokers</span><span class="o">.</span><span class="na">contains</span><span class="o">(</span><span class="n">entry</span><span class="o">.</span><span class="na">getValue</span><span class="o">()))</span> <span class="o">{</span>
                <span class="k">if</span> <span class="o">(</span><span class="n">deleted</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
                    <span class="n">deleted</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ArrayList</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;();</span>
                <span class="o">}</span>
                <span class="c1">// 若不包含，则将老的 Invoker 对应的 url 存入 deleted 列表中</span>
                <span class="n">deleted</span><span class="o">.</span><span class="na">add</span><span class="o">(</span><span class="n">entry</span><span class="o">.</span><span class="na">getKey</span><span class="o">());</span>
            <span class="o">}</span>
        <span class="o">}</span>
    <span class="o">}</span>

    <span class="k">if</span> <span class="o">(</span><span class="n">deleted</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
        <span class="c1">// 遍历 deleted 集合，并到老的 &lt;url, Invoker&gt; 映射关系表查出 Invoker，销毁之</span>
        <span class="k">for</span> <span class="o">(</span><span class="nc">String</span> <span class="n">url</span> <span class="o">:</span> <span class="n">deleted</span><span class="o">)</span> <span class="o">{</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">url</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
                <span class="c1">// 从 oldUrlInvokerMap 中移除 url 对应的 Invoker</span>
                <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">invoker</span> <span class="o">=</span> <span class="n">oldUrlInvokerMap</span><span class="o">.</span><span class="na">remove</span><span class="o">(</span><span class="n">url</span><span class="o">);</span>
                <span class="k">if</span> <span class="o">(</span><span class="n">invoker</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
                    <span class="k">try</span> <span class="o">{</span>
                        <span class="c1">// 销毁 Invoker</span>
                        <span class="n">invoker</span><span class="o">.</span><span class="na">destroy</span><span class="o">();</span>
                    <span class="o">}</span> <span class="k">catch</span> <span class="o">(</span><span class="nc">Exception</span> <span class="n">e</span><span class="o">)</span> <span class="o">{</span>
                        <span class="n">logger</span><span class="o">.</span><span class="na">warn</span><span class="o">(</span><span class="s">"destroy invoker..."</span><span class="o">);</span>
                    <span class="o">}</span>
                <span class="o">}</span>
            <span class="o">}</span>
        <span class="o">}</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="router">Router</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">interface</span> <span class="nc">Router</span> <span class="kd">extends</span> <span class="nc">Comparable</span><span class="o">&lt;</span><span class="nc">Router</span><span class="o">&gt;{</span>
    <span class="no">URL</span> <span class="nf">getUrl</span><span class="o">();</span>
    <span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="nf">route</span><span class="o">(</span><span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">invokers</span><span class="o">,</span> <span class="no">URL</span> <span class="n">url</span><span class="o">,</span> <span class="nc">Invocation</span> <span class="n">invocation</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span><span class="o">;</span>
    <span class="kt">int</span> <span class="nf">getPriority</span><span class="o">();</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="loadbalance">LoadBalance</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">interface</span> <span class="nc">LoadBalance</span> <span class="o">{</span>
    <span class="nd">@Adaptive</span><span class="o">(</span><span class="s">"loadbalance"</span><span class="o">)</span>
    <span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nf">select</span><span class="o">(</span><span class="nc">List</span><span class="o">&lt;</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;&gt;</span> <span class="n">invokers</span><span class="o">,</span> <span class="no">URL</span> <span class="n">url</span><span class="o">,</span> <span class="nc">Invocation</span> <span class="n">invocation</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="cluster">Cluster</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">interface</span> <span class="nc">Cluster</span> <span class="o">{</span>
    <span class="nd">@Adaptive</span>
    <span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nf">join</span><span class="o">(</span><span class="nc">Directory</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">directory</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="protocol">Protocol</h2>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">interface</span> <span class="nc">Protocol</span> <span class="o">{</span>
    <span class="cm">/**
     * 暴露远程服务：&lt;br&gt;
     * 1. 协议在接收请求时，应记录请求来源方地址信息：RpcContext.getContext().setRemoteAddress();&lt;br&gt;
     * 2. export()必须是幂等的，也就是暴露同一个URL的Invoker两次，和暴露一次没有区别。&lt;br&gt;
     * 3. export()传入的Invoker由框架实现并传入，协议不需要关心。&lt;br&gt;
     * 
     * @param &lt;T&gt; 服务的类型
     * @param invoker 服务的执行体
     * @return exporter 暴露服务的引用，用于取消暴露
     * @throws RpcException 当暴露服务出错时抛出，比如端口已占用
     */</span>
    <span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nc">Exporter</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nf">export</span><span class="o">(</span><span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">invoker</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span><span class="o">;</span>
 
    <span class="cm">/**
     * 引用远程服务：&lt;br&gt;
     * 1. 当用户调用refer()所返回的Invoker对象的invoke()方法时，协议需相应执行同URL远端export()传入的Invoker对象的invoke()方法。&lt;br&gt;
     * 2. refer()返回的Invoker由协议实现，协议通常需要在此Invoker中发送远程请求。&lt;br&gt;
     * 3. 当url中有设置check=false时，连接失败不能抛出异常，需内部自动恢复。&lt;br&gt;
     * 
     * @param &lt;T&gt; 服务的类型
     * @param type 服务的类型
     * @param url 远程服务的URL地址
     * @return invoker 服务的本地代理
     * @throws RpcException 当连接服务提供方失败时抛出
     */</span>
    <span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nc">Invoker</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="nf">refer</span><span class="o">(</span><span class="nc">Class</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">type</span><span class="o">,</span> <span class="no">URL</span> <span class="n">url</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span><span class="o">;</span>
 
<span class="o">}</span>
</code></pre></div></div>

<h2 id="filter">Filter</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>每个方法在调用被集群筛选之后,调用之前首先会经过Filter
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">package</span> <span class="nn">com.xxx</span><span class="o">;</span>
 
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.Filter</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.Invoker</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.Invocation</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.Result</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.RpcException</span><span class="o">;</span>
 
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">XxxFilter</span> <span class="kd">implements</span> <span class="nc">Filter</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="nc">Result</span> <span class="nf">invoke</span><span class="o">(</span><span class="nc">Invoker</span><span class="o">&lt;?&gt;</span> <span class="n">invoker</span><span class="o">,</span> <span class="nc">Invocation</span> <span class="n">invocation</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span> <span class="o">{</span>
        <span class="c1">// before filter ...</span>
        <span class="nc">Result</span> <span class="n">result</span> <span class="o">=</span> <span class="n">invoker</span><span class="o">.</span><span class="na">invoke</span><span class="o">(</span><span class="n">invocation</span><span class="o">);</span>
        <span class="c1">// after filter ...</span>
        <span class="k">return</span> <span class="n">result</span><span class="o">;</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="listener">Listener</h2>

<h3 id="invokerlistener">InvokerListener</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">package</span> <span class="nn">com.xxx</span><span class="o">;</span>
 
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.InvokerListener</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.Invoker</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.RpcException</span><span class="o">;</span>
 
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">XxxInvokerListener</span> <span class="kd">implements</span> <span class="nc">InvokerListener</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">referred</span><span class="o">(</span><span class="nc">Invoker</span><span class="o">&lt;?&gt;</span> <span class="n">invoker</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span> <span class="o">{</span>
        <span class="c1">// ...</span>
    <span class="o">}</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">destroyed</span><span class="o">(</span><span class="nc">Invoker</span><span class="o">&lt;?&gt;</span> <span class="n">invoker</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span> <span class="o">{</span>
        <span class="c1">// ...</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h3 id="exporterlistener">ExporterListener</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">package</span> <span class="nn">com.xxx</span><span class="o">;</span>
 
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.ExporterListener</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.Exporter</span><span class="o">;</span>
<span class="kn">import</span> <span class="nn">org.apache.dubbo.rpc.RpcException</span><span class="o">;</span>
 
 
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">XxxExporterListener</span> <span class="kd">implements</span> <span class="nc">ExporterListener</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">exported</span><span class="o">(</span><span class="nc">Exporter</span><span class="o">&lt;?&gt;</span> <span class="n">exporter</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span> <span class="o">{</span>
        <span class="c1">// ...</span>
    <span class="o">}</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">unexported</span><span class="o">(</span><span class="nc">Exporter</span><span class="o">&lt;?&gt;</span> <span class="n">exporter</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">RpcException</span> <span class="o">{</span>
        <span class="c1">// ...</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-06-09T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/06/08/mysq-introl.html">MySQL Intro</a></div><div class="next"><span>下篇</span><a href="/2020/06/15/tomcat-jndi.html">Tomcat JNDI</a></div></div></div>

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