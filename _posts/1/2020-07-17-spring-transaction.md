---
title: Spring Transaction
date: 2020-07-17 00:00:00 Z
tags:
- Spring
- Java
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Spring Transaction"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-07-17T08:00:00+08:00">
    <meta itemprop="keywords" content="Spring,Java"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Spring Transaction" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-17T08:00:00+08:00" />
    <meta itemprop="keywords" content="Spring,Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Spring Transaction" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-17T08:00:00+08:00" />
    <meta itemprop="keywords" content="Spring,Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Spring Transaction" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-17T08:00:00+08:00" />
    <meta itemprop="keywords" content="Spring,Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_0">参考地址</h1>

<p><a href="https://docs.spring.io/spring/docs/5.2.7.RELEASE/spring-framework-reference/data-access.html#spring-data-tier">spring-doc-dao</a></p>

<h1 id="_1">接口</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">interface</span> <span class="nc">PlatformTransactionManager</span> <span class="kd">extends</span> <span class="nc">TransactionManager</span> <span class="o">{</span>

    <span class="nc">TransactionStatus</span> <span class="nf">getTransaction</span><span class="o">(</span><span class="nc">TransactionDefinition</span> <span class="n">definition</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">TransactionException</span><span class="o">;</span>

    <span class="kt">void</span> <span class="nf">commit</span><span class="o">(</span><span class="nc">TransactionStatus</span> <span class="n">status</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">TransactionException</span><span class="o">;</span>

    <span class="kt">void</span> <span class="nf">rollback</span><span class="o">(</span><span class="nc">TransactionStatus</span> <span class="n">status</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">TransactionException</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">interface</span> <span class="nc">ReactiveTransactionManager</span> <span class="kd">extends</span> <span class="nc">TransactionManager</span> <span class="o">{</span>

    <span class="nc">Mono</span><span class="o">&lt;</span><span class="nc">ReactiveTransaction</span><span class="o">&gt;</span> <span class="nf">getReactiveTransaction</span><span class="o">(</span><span class="nc">TransactionDefinition</span> <span class="n">definition</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">TransactionException</span><span class="o">;</span>

    <span class="nc">Mono</span><span class="o">&lt;</span><span class="nc">Void</span><span class="o">&gt;</span> <span class="nf">commit</span><span class="o">(</span><span class="nc">ReactiveTransaction</span> <span class="n">status</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">TransactionException</span><span class="o">;</span>

    <span class="nc">Mono</span><span class="o">&lt;</span><span class="nc">Void</span><span class="o">&gt;</span> <span class="nf">rollback</span><span class="o">(</span><span class="nc">ReactiveTransaction</span> <span class="n">status</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">TransactionException</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>所谓TransactionDefinition就是字面意思.事务的定义:
1. 传播机制
2. 隔离等级
3. Timeout
4. 是否是只读事务(如果是只读,Spring会做出相应优化)
返回的TransactionStatus就代表事务的状态(状态实体):
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">interface</span> <span class="nc">TransactionStatus</span> <span class="kd">extends</span> <span class="nc">TransactionExecution</span><span class="o">,</span> <span class="nc">SavepointManager</span><span class="o">,</span> <span class="nc">Flushable</span> <span class="o">{</span>

    <span class="nd">@Override</span>
    <span class="kt">boolean</span> <span class="nf">isNewTransaction</span><span class="o">();</span>

    <span class="kt">boolean</span> <span class="nf">hasSavepoint</span><span class="o">();</span>

    <span class="nd">@Override</span>
    <span class="kt">void</span> <span class="nf">setRollbackOnly</span><span class="o">();</span>

    <span class="nd">@Override</span>
    <span class="kt">boolean</span> <span class="nf">isRollbackOnly</span><span class="o">();</span>

    <span class="kt">void</span> <span class="nf">flush</span><span class="o">();</span>

    <span class="nd">@Override</span>
    <span class="kt">boolean</span> <span class="nf">isCompleted</span><span class="o">();</span>
<span class="o">}</span>
</code></pre></div></div>
<h1 id="_2">传播机制</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="mi">1</span><span class="o">.</span> <span class="no">PROPAGATION_REQUIRED</span> <span class="o">:</span> 
    <span class="n">如果存在一个事务就加入</span><span class="o">,</span><span class="n">否则开启新事务</span>
<span class="mi">2</span><span class="o">.</span> <span class="no">PROPAGATION_REQUIRES_NEW</span> <span class="o">:</span> 
    <span class="n">总是开启一个新事务</span><span class="o">,</span><span class="n">挂起旧事务</span>
<span class="mi">3</span><span class="o">.</span> <span class="no">PROPAGATION_NESTED</span> <span class="o">:</span> 
    <span class="n">如果存在一个事务</span><span class="o">,</span><span class="n">则嵌套在这个事务中运行</span><span class="o">(</span><span class="n">子事务的奔溃不影响父事务</span><span class="o">)</span>
<span class="mi">4</span><span class="o">.</span> <span class="no">PROPAGATION_SUPPORTS</span> <span class="o">:</span> 
    <span class="n">如果没事务</span><span class="o">,</span><span class="n">则非事务的执行</span><span class="o">,</span><span class="n">如果存在事务</span><span class="o">,</span><span class="n">则加入这个事务</span>
<span class="mi">5</span><span class="o">.</span> <span class="no">PROPAGATION_NOT_SUPPORTED</span> <span class="o">:</span> 
    <span class="n">挂起所有其他事务</span><span class="o">,</span><span class="n">而且以非事务方式执行当前</span>
<span class="mi">6</span><span class="o">.</span> <span class="no">PROPAGATION_MANDATORY</span> <span class="o">:</span> 
    <span class="n">如果已经存在一个事务</span><span class="o">,</span><span class="n">加入这个事务</span><span class="o">,</span><span class="n">如果不存在</span><span class="o">,</span><span class="n">抛出异常</span><span class="o">(</span><span class="nc">NEVER的反面</span><span class="o">)</span>
<span class="mi">7</span><span class="o">.</span> <span class="no">PROPAGATION_NEVER</span> <span class="o">:</span> 
    <span class="n">如果存在一个事务</span><span class="o">,</span><span class="n">抛出异常</span><span class="o">,</span><span class="n">如果不存在一个事务</span><span class="o">,</span><span class="n">执行</span><span class="o">(</span><span class="nc">MANDATORY的反面</span><span class="o">)</span>
    
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">什么情况下会出现嵌套事务</span><span class="o">?</span><span class="nl">例如:</span>
<span class="kt">void</span> <span class="nf">a</span><span class="o">(){</span>
    <span class="n">b</span><span class="o">();</span>
<span class="o">}</span>
<span class="kt">void</span> <span class="nf">b</span><span class="o">(){</span>
<span class="o">}</span>
<span class="n">嵌套事务如何实现</span><span class="o">(</span><span class="n">nested</span><span class="o">)?</span>
<span class="n">在每次进入子事务的时候</span><span class="o">,</span><span class="n">会创建一个safe</span><span class="o">-</span><span class="n">point</span><span class="o">,</span><span class="n">一旦子事务出现异常</span><span class="o">,</span><span class="n">会回滚到safe</span><span class="o">-</span><span class="n">point</span>
</code></pre></div></div>

<h1 id="_3">Xml示例</h1>

<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code>Spring事务管理器通过AOP的方式.
<span class="nt">&lt;beans&gt;</span>
    ...
    <span class="nt">&lt;tx:advice</span> <span class="na">id=</span><span class="s">"txAdvice"</span> <span class="na">transaction-manager=</span><span class="s">"txManager"</span><span class="nt">&gt;</span>
        <span class="nt">&lt;tx:attributes&gt;</span>
            <span class="nt">&lt;tx:method</span> <span class="na">name=</span><span class="s">"get*"</span> <span class="na">read-only=</span><span class="s">"true"</span><span class="nt">/&gt;</span>
            <span class="nt">&lt;tx:method</span> <span class="na">name=</span><span class="s">"*"</span><span class="nt">/&gt;</span>
        <span class="nt">&lt;/tx:attributes&gt;</span>
    <span class="nt">&lt;/tx:advice&gt;</span>
    ...
    <span class="nt">&lt;aop:config&gt;</span>
        <span class="nt">&lt;aop:pointcut</span> <span class="na">id=</span><span class="s">"fooServiceOperation"</span> <span class="na">expression=</span><span class="s">"execution(* x.y.service.FooService.*(..))"</span><span class="nt">/&gt;</span>
        <span class="nt">&lt;aop:advisor</span> <span class="na">advice-ref=</span><span class="s">"txAdvice"</span> <span class="na">pointcut-ref=</span><span class="s">"fooServiceOperation"</span><span class="nt">/&gt;</span>
    <span class="nt">&lt;/aop:config&gt;</span>
    ...
    <span class="nt">&lt;bean</span> <span class="na">id=</span><span class="s">"dataSource"</span> <span class="na">class=</span><span class="s">"org.apache.commons.dbcp.BasicDataSource"</span> <span class="na">destroy-method=</span><span class="s">"close"</span><span class="nt">&gt;</span>
        <span class="nt">&lt;property</span> <span class="na">name=</span><span class="s">"driverClassName"</span> <span class="na">value=</span><span class="s">"oracle.jdbc.driver.OracleDriver"</span><span class="nt">/&gt;</span>
        <span class="nt">&lt;property</span> <span class="na">name=</span><span class="s">"url"</span> <span class="na">value=</span><span class="s">"jdbc:oracle:thin:@rj-t42:1521:elvis"</span><span class="nt">/&gt;</span>
        <span class="nt">&lt;property</span> <span class="na">name=</span><span class="s">"username"</span> <span class="na">value=</span><span class="s">"scott"</span><span class="nt">/&gt;</span>
        <span class="nt">&lt;property</span> <span class="na">name=</span><span class="s">"password"</span> <span class="na">value=</span><span class="s">"tiger"</span><span class="nt">/&gt;</span>
    <span class="nt">&lt;/bean&gt;</span>
    ...
    <span class="nt">&lt;bean</span> <span class="na">id=</span><span class="s">"txManager"</span> <span class="na">class=</span><span class="s">"org.springframework.jdbc.datasource.DataSourceTransactionManager"</span><span class="nt">&gt;</span>
        <span class="nt">&lt;property</span> <span class="na">name=</span><span class="s">"dataSource"</span> <span class="na">ref=</span><span class="s">"dataSource"</span><span class="nt">/&gt;</span>
    <span class="nt">&lt;/bean&gt;</span>
    ...
<span class="nt">&lt;/beans&gt;</span>

以上这段配置声明实现了以下机制:
在执行FooService的方法的时候会被AOP拦截,然后交给id为txManger的bean接管,
同时告诉事务管理器,在执行getter的时候是只读的事务

特别注意如果是使用JtaTransactionManager,则压根不需要把DataSource注入到JtaTransactionManager里,
只需要将DataSource配置到jndi里就行.
<span class="nt">&lt;beans&gt;</span>
    ...
    <span class="nt">&lt;jee:jndi-lookup</span> <span class="na">id=</span><span class="s">"dataSource"</span> <span class="na">jndi-name=</span><span class="s">"jdbc/jpetstore"</span><span class="nt">/&gt;</span>
    <span class="nt">&lt;bean</span> <span class="na">id=</span><span class="s">"txManager"</span> <span class="na">class=</span><span class="s">"org.springframework.transaction.jta.JtaTransactionManager"</span> <span class="nt">/&gt;</span>
    ...
<span class="nt">&lt;/beans&gt;</span>

事务管理器的全部配置
<span class="nt">&lt;tx:advice</span> <span class="na">id=</span><span class="s">"..."</span> <span class="na">transaction-manager=</span><span class="s">"..."</span><span class="nt">&gt;</span>
    <span class="nt">&lt;tx:attributes&gt;</span>
        <span class="nt">&lt;tx:method</span> <span class="na">name=</span><span class="s">"get*"</span> <span class="na">rollback-for=</span><span class="s">"XxxException"</span> <span class="na">no-rollback-for=</span><span class="s">"YyyException"</span> <span class="na">read-only=</span><span class="s">"true"</span> <span class="na">timeout=</span><span class="s">"-1"</span> <span class="na">isolation=</span><span class="s">"DEFAULT"</span> <span class="na">propagation=</span><span class="s">"REQUIRE"</span><span class="nt">/&gt;</span>
        <span class="c">&lt;!--在抛出XxxException时自动rollback,默认情况下所有的runtime-exception都会被rollback, no-rollback-for的意思和rollback-for相反--&gt;</span>
    <span class="nt">&lt;/tx:attributes&gt;</span>
<span class="nt">&lt;/tx:advice&gt;</span>
</code></pre></div></div>

<h1 id="_3">Annotation实例</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nd">@Transactional</span>
<span class="kd">class</span> <span class="nc">A</span><span class="o">{</span>
    <span class="no">B</span> <span class="nf">getB</span><span class="o">(){...}</span>
<span class="o">}</span>
<span class="n">为了使用</span><span class="nd">@Transactional注解</span><span class="o">,</span><span class="n">必须在Spring上下文类里加上</span><span class="nd">@EnableTransactionManagement或者xml里加上</span><span class="o">&lt;</span><span class="nl">tx:</span><span class="n">annotation</span><span class="o">-</span><span class="n">driven</span><span class="o">/&gt;.</span>
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="o">...</span>
<span class="nd">@Import</span><span class="o">(</span><span class="nc">TransactionManagementConfigurationSelector</span><span class="o">.</span><span class="na">class</span><span class="o">)</span>
<span class="kd">public</span> <span class="nd">@interface</span> <span class="nc">EnableTransactionManagement</span> <span class="o">{</span>
	<span class="kt">boolean</span> <span class="nf">proxyTargetClass</span><span class="o">()</span> <span class="k">default</span> <span class="kc">false</span><span class="o">;</span>
	<span class="nc">AdviceMode</span> <span class="nf">mode</span><span class="o">()</span> <span class="k">default</span> <span class="nc">AdviceMode</span><span class="o">.</span><span class="na">PROXY</span><span class="o">;</span>
	<span class="kt">int</span> <span class="nf">order</span><span class="o">()</span> <span class="k">default</span> <span class="nc">Ordered</span><span class="o">.</span><span class="na">LOWEST_PRECEDENCE</span><span class="o">;</span>
<span class="o">}</span>
<span class="nl">简而言之就是EnableTransactionManagment和tx:</span><span class="n">annotation</span><span class="o">-</span><span class="n">driven一样提供了proxy</span><span class="o">-</span><span class="n">target</span><span class="o">-</span><span class="n">class等等配置</span>
<span class="n">但是缺没有提供transaction</span><span class="o">-</span><span class="n">manager</span><span class="o">,</span><span class="n">因为transaction</span><span class="o">-</span><span class="n">manager的定义是通过TransactionManagementConfigurer来实现的</span>
<span class="nc">TransactionManagementConfigurer是一个实现了Configuration和EnableTransactionManager的注解类</span><span class="o">.</span>
<span class="nl">所以可以如下配置:</span>
<span class="nd">@TransactionManagerConfigurer</span>
<span class="kd">class</span> <span class="nc">Config</span><span class="o">{</span>
     <span class="nd">@Bean</span>
    <span class="kd">public</span> <span class="nc">PlatformTransactionManager</span> <span class="nf">txManager</span><span class="o">()</span> <span class="o">{</span>
        <span class="o">...</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>
<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;beans&gt;</span>
    ...
    <span class="nt">&lt;tx:annotation-driven</span> <span class="na">transaction-manager=</span><span class="s">"XxxManager"</span> <span class="na">mode=</span><span class="s">"proxy"</span> <span class="na">proxy-target-class=</span><span class="s">"true"</span> <span class="na">order=</span><span class="s">"Ordered.LOWEST_PRECEDENCE"</span><span class="nt">&gt;</span>
    <span class="c">&lt;!--mode表示是否是SpringAOP的Proxy代理方式,因为可选的有AspectJ方式--&gt;</span>
    <span class="c">&lt;!--proxy-target-class表示是否是JDK代理还是CGLIB--&gt;</span>
    <span class="c">&lt;!--order表示分配给这个TransactionManager的Advice的Order是多少,因为一个切点可以有多个Advice,Order可以自定义执行顺序--&gt;</span>
    ...
<span class="nt">&lt;/beans&gt;</span>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-07-17T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/07/15/cpp-const.html">Cpp Const</a></div><div class="next"><span>下篇</span><a href="/2020/07/20/misc-aba.html">CAS 的 ABA 问题</a></div></div></div>

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