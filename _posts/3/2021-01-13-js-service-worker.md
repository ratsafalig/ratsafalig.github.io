---
title: JS Service Worker
date: 2021-01-13 00:00:00 Z
tags:
- JS
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="JS Service Worker"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2021-01-13T08:00:00+08:00">
    <meta itemprop="keywords" content="JS"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="JS Service Worker" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-01-13T08:00:00+08:00" />
    <meta itemprop="keywords" content="JS" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><p><a href="https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorker">MDN-ServiceWorker</a></p>

<p><a href="https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API">MDN-Service_Worker_API</a></p>

<p><a href="https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers">MDN-Using_Service_Workers</a></p>

<p><a href="https://stackoverflow.com/questions/35780397/understanding-service-worker-scope">StackOverflow-Understanding-Service-Worker-scope</a></p>

<h1 id="生命周期">生命周期</h1>

<p><img src="/assets/3/js-service-worker/sw-lifecycle.png" alt="" /></p>

<p><img src="/assets/3/js-service-worker/sw-events.png" alt="" /></p>

<p><code class="language-plaintext highlighter-rouge">ServiceWorker</code>(以下简称SW),是一个缓存机制,通过注册一个作用域,和一个执行脚本,让所有作用域内页面的网络请求都会代理到执行脚本上去:</p>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nb">navigator</span><span class="p">.</span><span class="nx">serviceWorker</span><span class="p">.</span><span class="nx">register</span><span class="p">(</span><span class="dl">"</span><span class="s2">script.js</span><span class="dl">"</span><span class="p">,</span> <span class="p">{</span><span class="na">scope</span><span class="p">:</span> <span class="dl">"</span><span class="s2">...</span><span class="dl">"</span><span class="p">}).</span><span class="nx">then</span><span class="p">(</span><span class="kd">function</span><span class="p">(</span><span class="nx">reg</span><span class="p">){...})</span>
</code></pre></div></div>

<p>而script.js脚本执行环境是不同于普通脚本空间的,也就无法通过windows对象获取到浏览器界面<br />
script.js的执行空间闭包在一个<code class="language-plaintext highlighter-rouge">ServiceWorkerGlobalScope</code></p>

<p>每当头一回请求一个界面时都会触发<code class="language-plaintext highlighter-rouge">install</code>和<code class="language-plaintext highlighter-rouge">activate</code>事件,区别在于<code class="language-plaintext highlighter-rouge">activate</code>事件在前台已经有其他SW的时候暂时不会触发<br />
这段话的意思是,设想你有一个index.html:</p>

<div class="language-html highlighter-rouge"><div class="highlight"><pre class="highlight"><code>...
<span class="nt">&lt;script&gt;</span>
<span class="nb">navigator</span><span class="p">.</span><span class="nx">serviceWorker</span><span class="p">.</span><span class="nx">register</span><span class="p">(</span><span class="dl">"</span><span class="s2">a.js</span><span class="dl">"</span><span class="p">)...</span>
<span class="nt">&lt;/script&gt;</span>
...
</code></pre></div></div>

<p>理所当然第一次执行的时候会加载<code class="language-plaintext highlighter-rouge">a.js</code>的<code class="language-plaintext highlighter-rouge">install</code>和<code class="language-plaintext highlighter-rouge">activate</code><br />
但是如果服务器更改了index.html:</p>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nb">navigator</span><span class="p">.</span><span class="nx">serviceWorker</span><span class="p">.</span><span class="nx">register</span><span class="p">(</span><span class="dl">"</span><span class="s2">b.js</span><span class="dl">"</span><span class="p">)...</span>
</code></pre></div></div>

<p>那么这个时候只会执行<code class="language-plaintext highlighter-rouge">b.js</code>的<code class="language-plaintext highlighter-rouge">install</code><br />
它的<code class="language-plaintext highlighter-rouge">activate</code>会在前台的<code class="language-plaintext highlighter-rouge">a.js</code>过期后执行<br />
同样也可以通过函数强制触发更新</p>

<h1 id="api">API</h1>

<h2 id="serviceworkercontainer">ServiceWorkerContainer</h2>

<p><a href="https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerContainer">ServiceWorkerContainer</a></p>

<p>ServiceWorkerContainer是正常页面里的对象:</p>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">if</span> <span class="p">(</span><span class="dl">'</span><span class="s1">serviceWorker</span><span class="dl">'</span> <span class="k">in</span> <span class="nb">navigator</span><span class="p">)</span> <span class="p">{</span>
  <span class="nb">navigator</span><span class="p">.</span><span class="nx">serviceWorker</span><span class="p">.</span><span class="nx">register</span><span class="p">(</span><span class="dl">'</span><span class="s1">./sw-test/sw.js</span><span class="dl">'</span><span class="p">,</span> <span class="p">{</span><span class="na">scope</span><span class="p">:</span> <span class="dl">'</span><span class="s1">./sw-test/</span><span class="dl">'</span><span class="p">})</span>
  <span class="p">...</span>
<span class="p">}</span>
</code></pre></div></div>

<p>通过<code class="language-plaintext highlighter-rouge">navigator.serviceWorker</code>调用该对象</p>

<blockquote>

  <p>ServiceWorkerContainer:</p>
  <ul>
    <li>controller : 只读属性</li>
    <li>ready      : 只读属性</li>
    <li>register(…)</li>
    <li>getRegistration(…)</li>
    <li>getRegistrations(…)</li>
    <li>startMessages(…)</li>
  </ul>
</blockquote>

<blockquote>

  <p>可以处理的事件:</p>
  <ul>
    <li>controllerchange</li>
    <li>error</li>
    <li>message</li>
  </ul>
</blockquote>

<h2 id="serviceworkerglobalscope">ServiceWorkerGlobalScope</h2>

<p><a href="https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope">ServiceWorkerGlobalScope</a></p>

<p>通过<code class="language-plaintext highlighter-rouge">navigator.serviceWorker.register(...)</code>注册的js脚本所运行的环境全是在<code class="language-plaintext highlighter-rouge">ServiceWorkerGlobalScope</code>下的,也就是说该js脚本可以直接调用<code class="language-plaintext highlighter-rouge">ServiceWorkerGlobalScope</code>里的方法/函数/事件</p>

<blockquote>

  <p>ServiceWorkerGlobalScope :</p>
  <ul>
    <li>caches : 只读属性</li>
    <li>clients : 只读属性</li>
    <li>registration : 只读属性</li>
    <li>skipWaiting()</li>
    <li>fetch()</li>
  </ul>
</blockquote>

<blockquote>

  <p>可以处理的事件:</p>
  <ul>
    <li>activate</li>
    <li>contentdelete</li>
    <li>fetch</li>
    <li>install</li>
    <li>message</li>
    <li>notificationclick</li>
    <li>notificationclose</li>
    <li>push</li>
    <li>pushsubscriptionchange</li>
    <li>sync</li>
  </ul>
</blockquote>

<p>可以通过<code class="language-plaintext highlighter-rouge">addEventListener(...)</code>来把一个事件处理器注册,每次事件发生就会执行<code class="language-plaintext highlighter-rouge">EventHandler</code><br />
不仅可以通过<code class="language-plaintext highlighter-rouge">addEventListener(...)</code>也可以直接通过<code class="language-plaintext highlighter-rouge">onxxx</code>直接添加<code class="language-plaintext highlighter-rouge">EventHandler</code>:</p>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nx">onactivate</span> <span class="o">=</span> <span class="p">(</span><span class="nx">event</span><span class="p">)</span><span class="o">=&gt;</span><span class="p">{...}</span>
<span class="nx">oncontentdelete</span> <span class="o">=</span> <span class="p">(</span><span class="nx">event</span><span class="p">)</span><span class="o">=&gt;</span><span class="p">{...}</span>
<span class="p">...</span>
</code></pre></div></div>

<h2 id="serviceworkerscoperegistration">ServiceWorkerScopeRegistration</h2>

<p><a href="https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerRegistration">ServiceWorkerScopeRegistration</a></p>

<p>该对象可以通过如下获取:</p>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">if</span> <span class="p">(</span><span class="dl">'</span><span class="s1">serviceWorker</span><span class="dl">'</span> <span class="k">in</span> <span class="nb">navigator</span><span class="p">)</span> <span class="p">{</span>
  <span class="nb">navigator</span><span class="p">.</span><span class="nx">serviceWorker</span><span class="p">.</span><span class="nx">register</span><span class="p">(...).</span><span class="nx">then</span><span class="p">(</span><span class="kd">function</span><span class="p">(</span><span class="nx">registration</span><span class="p">){</span>
    <span class="p">...</span>
  <span class="p">})</span>
<span class="p">}</span>
<span class="cm">/******************************************************************/</span>
<span class="cm">/**
 * 在ServiceWorkerGlobalScope环境下
 */</span>
<span class="nb">self</span><span class="p">.</span><span class="nx">registration</span>
</code></pre></div></div>

<blockquote>

  <p>ServiceWorkerScopeRegistration只读属性</p>
  <ul>
    <li>scope</li>
    <li>installing</li>
    <li>waiting</li>
    <li>active</li>
    <li>navigationPreload</li>
    <li>pushManager</li>
    <li>sync</li>
    <li>index</li>
  </ul>
</blockquote>

<blockquote>

  <p>ServiceWorkerScopeRegistration事件处理器:</p>
  <ul>
    <li>onupdatefound</li>
  </ul>
</blockquote>

<blockquote>

  <p>ServiceWorkerScopeRegistration方法:</p>
  <ul>
    <li>getNotification(…)</li>
    <li>showNotification(…)</li>
    <li>update(…)</li>
    <li>unregister(…)</li>
  </ul>
</blockquote>

<h2 id="serviceworker">ServiceWorker</h2>

<p><a href="https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorker">ServiceWorker</a></p>

<p><a href="https://developer.mozilla.org/en-US/docs/Web/API/Worker">Worker</a></p>

<p>可以通过如下获取ServiceWorker对象(尤其注意active和activate的区别):</p>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">if</span> <span class="p">(</span><span class="dl">'</span><span class="s1">serviceWorker</span><span class="dl">'</span> <span class="k">in</span> <span class="nb">navigator</span><span class="p">)</span> <span class="p">{</span>
  <span class="nb">navigator</span><span class="p">.</span><span class="nx">serviceWorker</span><span class="p">.</span><span class="nx">register</span><span class="p">(</span><span class="dl">'</span><span class="s1">./sw-test/sw.js</span><span class="dl">'</span><span class="p">,</span> <span class="p">{</span><span class="na">scope</span><span class="p">:</span> <span class="dl">'</span><span class="s1">./sw-test/</span><span class="dl">'</span><span class="p">})</span>
  <span class="p">.</span><span class="nx">then</span><span class="p">((</span><span class="nx">reg</span><span class="p">)</span> <span class="o">=&gt;</span> <span class="p">{</span>
    <span class="kd">var</span> <span class="nx">serviceWorker</span> <span class="o">=</span> <span class="nx">reg</span><span class="p">.</span><span class="nx">active</span><span class="p">;</span>
  <span class="p">});</span>
<span class="p">}</span>

<span class="k">if</span> <span class="p">(</span><span class="dl">'</span><span class="s1">serviceWorker</span><span class="dl">'</span> <span class="k">in</span> <span class="nb">navigator</span><span class="p">)</span> <span class="p">{</span>
  <span class="kd">var</span> <span class="nx">serviceWorker</span> <span class="o">=</span> <span class="nb">navigator</span><span class="p">.</span><span class="nx">serviceWorker</span><span class="p">.</span><span class="nx">controller</span><span class="p">;</span>
<span class="p">}</span>
<span class="cm">/**************************************************************************/</span>
<span class="cm">/**
 * 在ServiceWorkerGlobalScope环境下:
 */</span>
<span class="kd">var</span> <span class="nx">serviceWorker</span> <span class="o">=</span> <span class="nb">self</span><span class="p">.</span><span class="nx">registration</span><span class="p">.</span><span class="nx">active</span><span class="p">;</span>
</code></pre></div></div>

<blockquote>

  <p>ServiceWorker</p>
  <ul>
    <li>scriptURL     : 只读属性</li>
    <li>state         : 只读属性</li>
    <li>onstatechange : EventListener,每次statechange事件触发时会被执行</li>
    <li>所有继承子Worker的函数</li>
  </ul>
</blockquote>

<blockquote>

  <p>Worker属性:</p>
  <ul>
    <li>所有继承自EventTarget的属性</li>
  </ul>
</blockquote>

<blockquote>

  <p>Worker事件处理器:</p>
  <ul>
    <li>onerror</li>
    <li>onmessage</li>
    <li>onmessageerror</li>
    <li>onrejectionhandled</li>
    <li>onunhandledrejection</li>
  </ul>
</blockquote>

<blockquote>

  <p>Worker方法</p>
  <ul>
    <li>postMessage(…)</li>
    <li>terminate(…)</li>
  </ul>
</blockquote>

<h2 id="clients--client">Clients / Client</h2>

<p><a href="https://developer.mozilla.org/en-US/docs/Web/API/Clients">Clients</a></p>

<p>在<code class="language-plaintext highlighter-rouge">ServiceWorkerGlobalScope</code>环境下:</p>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nb">self</span><span class="p">.</span><span class="nx">clients</span> <span class="c1">//获取clients对象,注意client并非简单的client数组,而是做了一些封装</span>
</code></pre></div></div>

<blockquote>

  <p>Clients:</p>
  <ul>
    <li>get(…)</li>
    <li>matchAll(…)</li>
    <li>openWindow(…)</li>
    <li>claim(…)</li>
  </ul>
</blockquote>

<blockquote>

  <p>Client:</p>
  <ul>
    <li>postMessages(…)</li>
    <li>id</li>
    <li>type</li>
    <li>url</li>
  </ul>
</blockquote>

<p>Client代表了一个请求者,请求者可以是:</p>

<blockquote>

  <ul>
    <li>其他Worker</li>
    <li>SharedWorker</li>
    <li>Window(默认的JS执行环境)</li>
  </ul>
</blockquote>

<p>可以通过方法<code class="language-plaintext highlighter-rouge">postMessage</code>应答请求<br />
实际上所有的应答都是通过这个API进行应答的,例如<code class="language-plaintext highlighter-rouge">event.responseWith(...)</code>…</p>

<h1 id="实例">实例</h1>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">if</span> <span class="p">(</span><span class="dl">'</span><span class="s1">serviceWorker</span><span class="dl">'</span> <span class="k">in</span> <span class="nb">navigator</span><span class="p">)</span> <span class="p">{</span>
  <span class="nb">navigator</span><span class="p">.</span><span class="nx">serviceWorker</span><span class="p">.</span><span class="nx">register</span><span class="p">(</span><span class="dl">'</span><span class="s1">./sw-test/sw.js</span><span class="dl">'</span><span class="p">,</span> <span class="p">{</span><span class="na">scope</span><span class="p">:</span> <span class="dl">'</span><span class="s1">./sw-test/</span><span class="dl">'</span><span class="p">})</span>
  <span class="p">.</span><span class="nx">then</span><span class="p">((</span><span class="nx">reg</span><span class="p">)</span> <span class="o">=&gt;</span> <span class="p">{</span>
    <span class="c1">// registration worked</span>
    <span class="nx">console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="dl">'</span><span class="s1">Registration succeeded. Scope is </span><span class="dl">'</span> <span class="o">+</span> <span class="nx">reg</span><span class="p">.</span><span class="nx">scope</span><span class="p">);</span>
  <span class="p">}).</span><span class="k">catch</span><span class="p">((</span><span class="nx">error</span><span class="p">)</span> <span class="o">=&gt;</span> <span class="p">{</span>
    <span class="c1">// registration failed</span>
    <span class="nx">console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="dl">'</span><span class="s1">Registration failed with </span><span class="dl">'</span> <span class="o">+</span> <span class="nx">error</span><span class="p">);</span>
  <span class="p">});</span>
<span class="p">}</span>
<span class="cm">/**************************************************************************/</span>
<span class="nb">self</span><span class="p">.</span><span class="nx">addEventListener</span><span class="p">(</span><span class="dl">'</span><span class="s1">install</span><span class="dl">'</span><span class="p">,</span> <span class="p">(</span><span class="nx">event</span><span class="p">)</span> <span class="o">=&gt;</span> <span class="p">{</span>
  <span class="nx">event</span><span class="p">.</span><span class="nx">waitUntil</span><span class="p">(</span>
    <span class="nx">caches</span><span class="p">.</span><span class="nx">open</span><span class="p">(</span><span class="dl">'</span><span class="s1">v1</span><span class="dl">'</span><span class="p">).</span><span class="nx">then</span><span class="p">((</span><span class="nx">cache</span><span class="p">)</span> <span class="o">=&gt;</span> <span class="p">{</span>
      <span class="k">return</span> <span class="nx">cache</span><span class="p">.</span><span class="nx">addAll</span><span class="p">([</span>
        <span class="dl">'</span><span class="s1">./sw-test/</span><span class="dl">'</span><span class="p">,</span>
        <span class="dl">'</span><span class="s1">./sw-test/index.html</span><span class="dl">'</span><span class="p">,</span>
        <span class="dl">'</span><span class="s1">./sw-test/style.css</span><span class="dl">'</span><span class="p">,</span>
        <span class="dl">'</span><span class="s1">./sw-test/app.js</span><span class="dl">'</span><span class="p">,</span>
        <span class="dl">'</span><span class="s1">./sw-test/image-list.js</span><span class="dl">'</span><span class="p">,</span>
        <span class="dl">'</span><span class="s1">./sw-test/star-wars-logo.jpg</span><span class="dl">'</span><span class="p">,</span>
        <span class="dl">'</span><span class="s1">./sw-test/gallery/</span><span class="dl">'</span><span class="p">,</span>
        <span class="dl">'</span><span class="s1">./sw-test/gallery/bountyHunters.jpg</span><span class="dl">'</span><span class="p">,</span>
        <span class="dl">'</span><span class="s1">./sw-test/gallery/myLittleVader.jpg</span><span class="dl">'</span><span class="p">,</span>
        <span class="dl">'</span><span class="s1">./sw-test/gallery/snowTroopers.jpg</span><span class="dl">'</span>
      <span class="p">]);</span>
    <span class="p">})</span>
  <span class="p">);</span>
<span class="p">});</span>
<span class="cm">/**************************************************************************/</span>
<span class="nb">self</span><span class="p">.</span><span class="nx">addEventListener</span><span class="p">(</span><span class="dl">'</span><span class="s1">fetch</span><span class="dl">'</span><span class="p">,</span> <span class="p">(</span><span class="nx">event</span><span class="p">)</span> <span class="o">=&gt;</span> <span class="p">{</span>
  <span class="nx">event</span><span class="p">.</span><span class="nx">respondWith</span><span class="p">(</span>
    <span class="nx">caches</span><span class="p">.</span><span class="nx">match</span><span class="p">(</span><span class="nx">event</span><span class="p">.</span><span class="nx">request</span><span class="p">).</span><span class="nx">then</span><span class="p">((</span><span class="nx">resp</span><span class="p">)</span> <span class="o">=&gt;</span> <span class="p">{</span>
      <span class="k">return</span> <span class="nx">resp</span> <span class="o">||</span> <span class="nx">fetch</span><span class="p">(</span><span class="nx">event</span><span class="p">.</span><span class="nx">request</span><span class="p">).</span><span class="nx">then</span><span class="p">((</span><span class="nx">response</span><span class="p">)</span> <span class="o">=&gt;</span> <span class="p">{</span>
        <span class="kd">let</span> <span class="nx">responseClone</span> <span class="o">=</span> <span class="nx">response</span><span class="p">.</span><span class="nx">clone</span><span class="p">();</span>
        <span class="nx">caches</span><span class="p">.</span><span class="nx">open</span><span class="p">(</span><span class="dl">'</span><span class="s1">v1</span><span class="dl">'</span><span class="p">).</span><span class="nx">then</span><span class="p">((</span><span class="nx">cache</span><span class="p">)</span> <span class="o">=&gt;</span> <span class="p">{</span>
          <span class="nx">cache</span><span class="p">.</span><span class="nx">put</span><span class="p">(</span><span class="nx">event</span><span class="p">.</span><span class="nx">request</span><span class="p">,</span> <span class="nx">responseClone</span><span class="p">);</span>
        <span class="p">});</span>
        <span class="k">return</span> <span class="nx">response</span><span class="p">;</span>
      <span class="p">}).</span><span class="k">catch</span><span class="p">(()</span> <span class="o">=&gt;</span> <span class="p">{</span>
        <span class="k">return</span> <span class="nx">caches</span><span class="p">.</span><span class="nx">match</span><span class="p">(</span><span class="dl">'</span><span class="s1">./sw-test/gallery/myLittleVader.jpg</span><span class="dl">'</span><span class="p">);</span>
      <span class="p">})</span>
    <span class="p">});</span>
  <span class="p">);</span>
<span class="p">});</span>
<span class="cm">/**************************************************************************/</span>
<span class="nb">self</span><span class="p">.</span><span class="nx">addEventListener</span><span class="p">(</span><span class="dl">'</span><span class="s1">activate</span><span class="dl">'</span><span class="p">,</span> <span class="p">(</span><span class="nx">event</span><span class="p">)</span> <span class="o">=&gt;</span> <span class="p">{</span>
  <span class="kd">var</span> <span class="nx">cacheKeeplist</span> <span class="o">=</span> <span class="p">[</span><span class="dl">'</span><span class="s1">v2</span><span class="dl">'</span><span class="p">];</span>

  <span class="nx">event</span><span class="p">.</span><span class="nx">waitUntil</span><span class="p">(</span>
    <span class="nx">caches</span><span class="p">.</span><span class="nx">keys</span><span class="p">().</span><span class="nx">then</span><span class="p">((</span><span class="nx">keyList</span><span class="p">)</span> <span class="o">=&gt;</span> <span class="p">{</span>
      <span class="k">return</span> <span class="nb">Promise</span><span class="p">.</span><span class="nx">all</span><span class="p">(</span><span class="nx">keyList</span><span class="p">.</span><span class="nx">map</span><span class="p">((</span><span class="nx">key</span><span class="p">)</span> <span class="o">=&gt;</span> <span class="p">{</span>
        <span class="k">if</span> <span class="p">(</span><span class="nx">cacheKeeplist</span><span class="p">.</span><span class="nx">indexOf</span><span class="p">(</span><span class="nx">key</span><span class="p">)</span> <span class="o">===</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span> <span class="p">{</span>
          <span class="k">return</span> <span class="nx">caches</span><span class="p">.</span><span class="k">delete</span><span class="p">(</span><span class="nx">key</span><span class="p">);</span>
        <span class="p">}</span>
      <span class="p">}));</span>
    <span class="p">})</span>
  <span class="p">);</span>
<span class="p">});</span>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2021-01-13T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2021/01/13/js-modules.html">JS CJS AMD UMD ESM JavaScript Modules</a></div><div class="next"><span>下篇</span><a href="/2021/01/13/npm.html">NPM</a></div></div></div>

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