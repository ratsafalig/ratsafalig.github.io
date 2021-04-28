---
title: Bilibili DanMu 弹幕
date: 2021-02-26 00:00:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Bilibili DanMu 弹幕"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2021-02-26T08:00:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Bilibili DanMu 弹幕" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-02-26T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Bilibili DanMu 弹幕" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-02-26T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><p><img src="/assets/3/bilibili-danmu/QQ截图20210226215605.png" alt="" /></p>

<p><img src="/assets/3/bilibili-danmu/QQ截图20210226215638.png" alt="" /></p>

<p>弹幕的前 16 个字节为 元信息 ,记载诸如长度之类的数据<br />
弹幕通过 convertToObject 转换成 json</p>

<p><img src="/assets/3/bilibili-danmu/QQ截图20210226215821.png" alt="" /></p>

<div class="language-js highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nx">e</span><span class="p">.</span><span class="nx">prototype</span><span class="p">.</span><span class="nx">convertToObject</span> <span class="o">=</span> <span class="kd">function</span><span class="p">(</span><span class="nx">e</span><span class="p">)</span> <span class="p">{</span>
    <span class="kd">var</span> <span class="nx">t</span> <span class="o">=</span> <span class="k">new</span> <span class="nb">DataView</span><span class="p">(</span><span class="nx">e</span><span class="p">)</span>
        <span class="p">,</span> <span class="nx">n</span> <span class="o">=</span> <span class="p">{</span>
        <span class="na">body</span><span class="p">:</span> <span class="p">[]</span>
    <span class="p">};</span>
    <span class="k">if</span> <span class="p">(</span>
        <span class="cm">/* 逗号分隔开的 if 字段内容,表示不做判断,仅仅执行 */</span>
        <span class="nx">n</span><span class="p">.</span><span class="nx">packetLen</span> <span class="o">=</span> <span class="nx">t</span><span class="p">.</span><span class="nx">getInt32</span><span class="p">(</span><span class="nx">i</span><span class="p">.</span><span class="nx">a</span><span class="p">.</span><span class="nx">WS_PACKAGE_OFFSET</span><span class="p">),</span>
        <span class="k">this</span><span class="p">.</span><span class="nx">wsBinaryHeaderList</span><span class="p">.</span><span class="nx">forEach</span><span class="p">((</span><span class="kd">function</span><span class="p">(</span><span class="nx">e</span><span class="p">)</span> <span class="p">{</span>
                <span class="mi">4</span> <span class="o">===</span> <span class="nx">e</span><span class="p">.</span><span class="nx">bytes</span> <span class="p">?</span> <span class="nx">n</span><span class="p">[</span><span class="nx">e</span><span class="p">.</span><span class="nx">key</span><span class="p">]</span> <span class="o">=</span> <span class="nx">t</span><span class="p">.</span><span class="nx">getInt32</span><span class="p">(</span><span class="nx">e</span><span class="p">.</span><span class="nx">offset</span><span class="p">)</span> <span class="p">:</span> <span class="mi">2</span> <span class="o">===</span> <span class="nx">e</span><span class="p">.</span><span class="nx">bytes</span> <span class="o">&amp;&amp;</span> <span class="p">(</span><span class="nx">n</span><span class="p">[</span><span class="nx">e</span><span class="p">.</span><span class="nx">key</span><span class="p">]</span> <span class="o">=</span> <span class="nx">t</span><span class="p">.</span><span class="nx">getInt16</span><span class="p">(</span><span class="nx">e</span><span class="p">.</span><span class="nx">offset</span><span class="p">))</span>
            <span class="p">}</span>
        <span class="p">)),</span>    
        <span class="nx">n</span><span class="p">.</span><span class="nx">packetLen</span> <span class="o">&lt;</span> <span class="nx">e</span><span class="p">.</span><span class="nx">byteLength</span> <span class="o">&amp;&amp;</span> <span class="k">this</span><span class="p">.</span><span class="nx">convertToObject</span><span class="p">(</span><span class="nx">e</span><span class="p">.</span><span class="nx">slice</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="nx">n</span><span class="p">.</span><span class="nx">packetLen</span><span class="p">)),</span>
        <span class="k">this</span><span class="p">.</span><span class="nx">decoder</span> <span class="o">||</span> <span class="p">(</span><span class="k">this</span><span class="p">.</span><span class="nx">decoder</span> <span class="o">=</span> <span class="nx">o</span><span class="p">.</span><span class="nx">a</span><span class="p">.</span><span class="nx">getDecoder</span><span class="p">()),</span>
        <span class="cm">/* 真正的 if 判断字段 */</span>
        <span class="o">!</span><span class="nx">n</span><span class="p">.</span><span class="nx">op</span> <span class="o">||</span> <span class="nx">i</span><span class="p">.</span><span class="nx">a</span><span class="p">.</span><span class="nx">WS_OP_MESSAGE</span> <span class="o">!==</span> <span class="nx">n</span><span class="p">.</span><span class="nx">op</span> <span class="o">&amp;&amp;</span> <span class="nx">n</span><span class="p">.</span><span class="nx">op</span> <span class="o">!==</span> <span class="nx">i</span><span class="p">.</span><span class="nx">a</span><span class="p">.</span><span class="nx">WS_OP_CONNECT_SUCCESS</span><span class="p">)</span>
            <span class="nx">n</span><span class="p">.</span><span class="nx">op</span> <span class="o">&amp;&amp;</span> <span class="nx">i</span><span class="p">.</span><span class="nx">a</span><span class="p">.</span><span class="nx">WS_OP_HEARTBEAT_REPLY</span> <span class="o">===</span> <span class="nx">n</span><span class="p">.</span><span class="nx">op</span> <span class="o">&amp;&amp;</span> <span class="p">(</span><span class="nx">n</span><span class="p">.</span><span class="nx">body</span> <span class="o">=</span> <span class="p">{</span>
                <span class="na">count</span><span class="p">:</span> <span class="nx">t</span><span class="p">.</span><span class="nx">getInt32</span><span class="p">(</span><span class="nx">i</span><span class="p">.</span><span class="nx">a</span><span class="p">.</span><span class="nx">WS_PACKAGE_HEADER_TOTAL_LENGTH</span><span class="p">)</span>
            <span class="p">});</span>
    <span class="k">else</span>
        <span class="k">for</span> <span class="p">(</span><span class="kd">var</span> <span class="nx">r</span> <span class="o">=</span> <span class="nx">i</span><span class="p">.</span><span class="nx">a</span><span class="p">.</span><span class="nx">WS_PACKAGE_OFFSET</span><span class="p">,</span> <span class="nx">s</span> <span class="o">=</span> <span class="nx">n</span><span class="p">.</span><span class="nx">packetLen</span><span class="p">,</span> <span class="nx">l</span> <span class="o">=</span> <span class="dl">""</span><span class="p">,</span> <span class="nx">c</span> <span class="o">=</span> <span class="dl">""</span><span class="p">;</span> <span class="nx">r</span> <span class="o">&lt;</span> <span class="nx">e</span><span class="p">.</span><span class="nx">byteLength</span><span class="p">;</span> <span class="nx">r</span> <span class="o">+=</span> <span class="nx">s</span><span class="p">)</span> <span class="p">{</span>
            <span class="nx">s</span> <span class="o">=</span> <span class="nx">t</span><span class="p">.</span><span class="nx">getInt32</span><span class="p">(</span><span class="nx">r</span><span class="p">),</span>
            <span class="nx">l</span> <span class="o">=</span> <span class="nx">t</span><span class="p">.</span><span class="nx">getInt16</span><span class="p">(</span><span class="nx">r</span> <span class="o">+</span> <span class="nx">i</span><span class="p">.</span><span class="nx">a</span><span class="p">.</span><span class="nx">WS_HEADER_OFFSET</span><span class="p">);</span>
            <span class="k">try</span> <span class="p">{</span>
                <span class="k">if</span> <span class="p">(</span><span class="nx">n</span><span class="p">.</span><span class="nx">ver</span> <span class="o">===</span> <span class="nx">i</span><span class="p">.</span><span class="nx">a</span><span class="p">.</span><span class="nx">WS_BODY_PROTOCOL_VERSION_DEFLATE</span><span class="p">)</span> <span class="p">{</span>
                    <span class="kd">var</span> <span class="nx">u</span> <span class="o">=</span> <span class="nx">e</span><span class="p">.</span><span class="nx">slice</span><span class="p">(</span><span class="nx">r</span> <span class="o">+</span> <span class="nx">l</span><span class="p">,</span> <span class="nx">r</span> <span class="o">+</span> <span class="nx">s</span><span class="p">)</span>
                        <span class="cm">/* 这个不起眼的字段非常重要,作用为把字段解压 */</span>
                        <span class="p">,</span> <span class="nx">d</span> <span class="o">=</span> <span class="nx">a</span><span class="p">(</span><span class="k">new</span> <span class="nb">Uint8Array</span><span class="p">(</span><span class="nx">u</span><span class="p">));</span>
                    <span class="nx">c</span> <span class="o">=</span> <span class="k">this</span><span class="p">.</span><span class="nx">convertToObject</span><span class="p">(</span><span class="nx">d</span><span class="p">.</span><span class="nx">buffer</span><span class="p">).</span><span class="nx">body</span>
                <span class="p">}</span> <span class="k">else</span> <span class="p">{</span>
                    <span class="kd">var</span> <span class="nx">h</span> <span class="o">=</span> <span class="k">this</span><span class="p">.</span><span class="nx">decoder</span><span class="p">.</span><span class="nx">decode</span><span class="p">(</span><span class="nx">e</span><span class="p">.</span><span class="nx">slice</span><span class="p">(</span><span class="nx">r</span> <span class="o">+</span> <span class="nx">l</span><span class="p">,</span> <span class="nx">r</span> <span class="o">+</span> <span class="nx">s</span><span class="p">));</span>
                    <span class="nx">c</span> <span class="o">=</span> <span class="mi">0</span> <span class="o">!==</span> <span class="nx">h</span><span class="p">.</span><span class="nx">length</span> <span class="p">?</span> <span class="nx">JSON</span><span class="p">.</span><span class="nx">parse</span><span class="p">(</span><span class="nx">h</span><span class="p">)</span> <span class="p">:</span> <span class="kc">null</span>
                <span class="p">}</span>
                <span class="nx">c</span> <span class="o">&amp;&amp;</span> <span class="nx">n</span><span class="p">.</span><span class="nx">body</span><span class="p">.</span><span class="nx">push</span><span class="p">(</span><span class="nx">c</span><span class="p">)</span>
            <span class="p">}</span> <span class="k">catch</span> <span class="p">(</span><span class="nx">t</span><span class="p">)</span> <span class="p">{</span>
                <span class="nx">console</span><span class="p">.</span><span class="nx">error</span><span class="p">(</span><span class="dl">"</span><span class="s2">decode body error:</span><span class="dl">"</span><span class="p">,</span> <span class="k">new</span> <span class="nb">Uint8Array</span><span class="p">(</span><span class="nx">e</span><span class="p">),</span> <span class="nx">n</span><span class="p">,</span> <span class="nx">t</span><span class="p">)</span>
            <span class="p">}</span>
        <span class="p">}</span>
    <span class="k">return</span> <span class="nx">n</span>
<span class="p">}</span>
<span class="cm">/**********************************************************************************************************/</span>
<span class="nx">e</span><span class="p">.</span><span class="nx">getDecoder</span> <span class="o">=</span> <span class="kd">function</span><span class="p">()</span> <span class="p">{</span>
    <span class="k">return</span> <span class="nb">window</span><span class="p">.</span><span class="nx">TextDecoder</span> <span class="p">?</span> <span class="k">new</span> <span class="nb">window</span><span class="p">.</span><span class="nx">TextDecoder</span> <span class="p">:</span> <span class="p">{</span>
        <span class="na">decode</span><span class="p">:</span> <span class="kd">function</span><span class="p">(</span><span class="nx">e</span><span class="p">)</span> <span class="p">{</span>
            <span class="k">return</span> <span class="nb">decodeURIComponent</span><span class="p">(</span><span class="nb">window</span><span class="p">.</span><span class="nx">escape</span><span class="p">(</span><span class="nb">String</span><span class="p">.</span><span class="nx">fromCharCode</span><span class="p">.</span><span class="nx">apply</span><span class="p">(</span><span class="nb">String</span><span class="p">,</span> <span class="k">new</span> <span class="nb">Uint8Array</span><span class="p">(</span><span class="nx">e</span><span class="p">))))</span>
        <span class="p">}</span>
    <span class="p">}</span>
<span class="p">}</span>
<span class="cm">/**********************************************************************************************************/</span>
<span class="cm">/* r 函数为 convertToObject 的 a 函数实际结构 */</span>
<span class="kd">function</span> <span class="nx">r</span><span class="p">(</span><span class="nx">e</span><span class="p">,</span> <span class="nx">t</span><span class="p">)</span> <span class="p">{</span>
    <span class="cm">/* 注意不是方法返回值,而是返回一个对象 */</span>
    <span class="kd">var</span> <span class="nx">n</span> <span class="o">=</span> <span class="k">new</span> <span class="nx">i</span><span class="p">(</span><span class="nx">t</span><span class="p">);</span>
    <span class="k">if</span> <span class="p">(</span><span class="nx">n</span><span class="p">.</span><span class="nx">push</span><span class="p">(</span><span class="nx">e</span><span class="p">,</span> <span class="o">!</span><span class="mi">0</span><span class="p">),</span>
    <span class="nx">n</span><span class="p">.</span><span class="nx">err</span><span class="p">)</span>
        <span class="k">throw</span> <span class="nx">n</span><span class="p">.</span><span class="nx">msg</span> <span class="o">||</span> <span class="nx">c</span><span class="p">[</span><span class="nx">n</span><span class="p">.</span><span class="nx">err</span><span class="p">];</span>
    <span class="k">return</span> <span class="nx">n</span><span class="p">.</span><span class="nx">result</span>
<span class="p">}</span>
<span class="cm">/**********************************************************************************************************/</span>
<span class="kd">function</span> <span class="nx">i</span><span class="p">(</span><span class="nx">e</span><span class="p">)</span> <span class="p">{</span>
    <span class="k">if</span> <span class="p">(</span><span class="o">!</span><span class="p">(</span><span class="k">this</span> <span class="k">instanceof</span> <span class="nx">i</span><span class="p">))</span>
        <span class="k">return</span> <span class="k">new</span> <span class="nx">i</span><span class="p">(</span><span class="nx">e</span><span class="p">);</span>
    <span class="k">this</span><span class="p">.</span><span class="nx">options</span> <span class="o">=</span> <span class="nx">a</span><span class="p">.</span><span class="nx">assign</span><span class="p">({</span>
        <span class="na">chunkSize</span><span class="p">:</span> <span class="mi">16384</span><span class="p">,</span>
        <span class="na">windowBits</span><span class="p">:</span> <span class="mi">0</span><span class="p">,</span>
        <span class="na">to</span><span class="p">:</span> <span class="dl">""</span>
    <span class="p">},</span> <span class="nx">e</span> <span class="o">||</span> <span class="p">{});</span>
    <span class="kd">var</span> <span class="nx">t</span> <span class="o">=</span> <span class="k">this</span><span class="p">.</span><span class="nx">options</span><span class="p">;</span>
    <span class="cm">/* 语句分段 */</span>
    <span class="nx">t</span><span class="p">.</span><span class="nx">raw</span> <span class="o">&amp;&amp;</span> 
    <span class="mi">0</span> <span class="o">&lt;=</span> <span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span> <span class="o">&amp;&amp;</span> 
    <span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span> <span class="o">&lt;</span> <span class="mi">16</span> <span class="o">&amp;&amp;</span> 
    <span class="p">(</span><span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span> <span class="o">=</span> <span class="o">-</span><span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span><span class="p">,</span><span class="mi">0</span> <span class="o">===</span> <span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span> <span class="o">&amp;&amp;</span> <span class="p">(</span><span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span> <span class="o">=</span> <span class="o">-</span><span class="mi">15</span><span class="p">)),</span>
    <span class="cm">/* 语句分段 */</span>
    <span class="o">!</span><span class="p">(</span><span class="mi">0</span> <span class="o">&lt;=</span> <span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span> <span class="o">&amp;&amp;</span> <span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span> <span class="o">&lt;</span> <span class="mi">16</span><span class="p">)</span> <span class="o">||</span> 
    <span class="nx">e</span> <span class="o">&amp;&amp;</span> 
    <span class="nx">e</span><span class="p">.</span><span class="nx">windowBits</span> <span class="o">||</span> 
    <span class="p">(</span><span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span> <span class="o">+=</span> <span class="mi">32</span><span class="p">),</span>
    <span class="cm">/* 语句分段 */</span>
    <span class="mi">15</span> <span class="o">&lt;</span> <span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span> <span class="o">&amp;&amp;</span>
    <span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span> <span class="o">&lt;</span> <span class="mi">48</span> <span class="o">&amp;&amp;</span>
    <span class="mi">0</span> <span class="o">==</span> <span class="p">(</span><span class="mi">15</span> <span class="o">&amp;</span> <span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span><span class="p">)</span> <span class="o">&amp;&amp;</span> 
    <span class="p">(</span><span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span> <span class="o">|=</span> <span class="mi">15</span><span class="p">),</span>
    <span class="cm">/* 语句分段 */</span>
    <span class="k">this</span><span class="p">.</span><span class="nx">err</span> <span class="o">=</span> <span class="mi">0</span><span class="p">,</span>
    <span class="k">this</span><span class="p">.</span><span class="nx">msg</span> <span class="o">=</span> <span class="dl">""</span><span class="p">,</span>
    <span class="k">this</span><span class="p">.</span><span class="nx">ended</span> <span class="o">=</span> <span class="o">!</span><span class="mi">1</span><span class="p">,</span>
    <span class="k">this</span><span class="p">.</span><span class="nx">chunks</span> <span class="o">=</span> <span class="p">[],</span>
    <span class="k">this</span><span class="p">.</span><span class="nx">strm</span> <span class="o">=</span> <span class="k">new</span> <span class="nx">u</span><span class="p">,</span>
    <span class="k">this</span><span class="p">.</span><span class="nx">strm</span><span class="p">.</span><span class="nx">avail_out</span> <span class="o">=</span> <span class="mi">0</span><span class="p">;</span>
    <span class="cm">/* inflate 压缩相关 */</span>
    <span class="kd">var</span> <span class="nx">n</span> <span class="o">=</span> <span class="nx">o</span><span class="p">.</span><span class="nx">inflateInit2</span><span class="p">(</span><span class="k">this</span><span class="p">.</span><span class="nx">strm</span><span class="p">,</span> <span class="nx">t</span><span class="p">.</span><span class="nx">windowBits</span><span class="p">);</span>
    <span class="k">if</span> <span class="p">(</span><span class="nx">n</span> <span class="o">!==</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_OK</span><span class="p">)</span>
        <span class="k">throw</span> <span class="k">new</span> <span class="nb">Error</span><span class="p">(</span><span class="nx">c</span><span class="p">[</span><span class="nx">n</span><span class="p">]);</span>
    <span class="k">if</span> <span class="p">(</span>
        <span class="k">this</span><span class="p">.</span><span class="nx">header</span> <span class="o">=</span> <span class="k">new</span> <span class="nx">d</span><span class="p">,</span>
        <span class="cm">/* inflate 压缩相关 */</span>
        <span class="nx">o</span><span class="p">.</span><span class="nx">inflateGetHeader</span><span class="p">(</span><span class="k">this</span><span class="p">.</span><span class="nx">strm</span><span class="p">,</span> <span class="k">this</span><span class="p">.</span><span class="nx">header</span><span class="p">),</span>
        <span class="nx">t</span><span class="p">.</span><span class="nx">dictionary</span> <span class="o">&amp;&amp;</span>
        <span class="p">(</span><span class="dl">"</span><span class="s2">string</span><span class="dl">"</span> <span class="o">==</span> <span class="k">typeof</span> <span class="nx">t</span><span class="p">.</span><span class="nx">dictionary</span> <span class="p">?</span> <span class="nx">t</span><span class="p">.</span><span class="nx">dictionary</span> <span class="o">=</span> <span class="nx">s</span><span class="p">.</span><span class="nx">string2buf</span><span class="p">(</span><span class="nx">t</span><span class="p">.</span><span class="nx">dictionary</span><span class="p">)</span> <span class="p">:</span> <span class="dl">"</span><span class="s2">[object ArrayBuffer]</span><span class="dl">"</span> <span class="o">===</span> <span class="nx">h</span><span class="p">.</span><span class="nx">call</span><span class="p">(</span><span class="nx">t</span><span class="p">.</span><span class="nx">dictionary</span><span class="p">)</span> <span class="o">&amp;&amp;</span> <span class="p">(</span><span class="nx">t</span><span class="p">.</span><span class="nx">dictionary</span> <span class="o">=</span> <span class="k">new</span> <span class="nb">Uint8Array</span><span class="p">(</span><span class="nx">t</span><span class="p">.</span><span class="nx">dictionary</span><span class="p">)),</span><span class="nx">t</span><span class="p">.</span><span class="nx">raw</span> <span class="o">&amp;&amp;</span> <span class="p">(</span><span class="nx">n</span> <span class="o">=</span> <span class="nx">o</span><span class="p">.</span><span class="nx">inflateSetDictionary</span><span class="p">(</span><span class="k">this</span><span class="p">.</span><span class="nx">strm</span><span class="p">,</span> <span class="nx">t</span><span class="p">.</span><span class="nx">dictionary</span><span class="p">))</span> <span class="o">!==</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_OK</span><span class="p">))</span>
            <span class="k">throw</span> <span class="k">new</span> <span class="nb">Error</span><span class="p">(</span><span class="nx">c</span><span class="p">[</span><span class="nx">n</span><span class="p">])</span>
<span class="p">}</span>
<span class="cm">/**********************************************************************************************************/</span>
<span class="cm">/* 解压的关键,解压之后变成正常函数 */</span>
<span class="nx">i</span><span class="p">.</span><span class="nx">prototype</span><span class="p">.</span><span class="nx">push</span> <span class="o">=</span> <span class="kd">function</span><span class="p">(</span><span class="nx">e</span><span class="p">,</span> <span class="nx">t</span><span class="p">)</span> <span class="p">{</span>
    <span class="kd">var</span> <span class="nx">n</span><span class="p">,</span> <span class="nx">i</span><span class="p">,</span> <span class="nx">r</span><span class="p">,</span> <span class="nx">c</span><span class="p">,</span> <span class="nx">u</span><span class="p">,</span> <span class="nx">d</span> <span class="o">=</span> <span class="k">this</span><span class="p">.</span><span class="nx">strm</span><span class="p">,</span> <span class="nx">f</span> <span class="o">=</span> <span class="k">this</span><span class="p">.</span><span class="nx">options</span><span class="p">.</span><span class="nx">chunkSize</span><span class="p">,</span> <span class="nx">p</span> <span class="o">=</span> <span class="k">this</span><span class="p">.</span><span class="nx">options</span><span class="p">.</span><span class="nx">dictionary</span><span class="p">,</span> <span class="nx">v</span> <span class="o">=</span> <span class="o">!</span><span class="mi">1</span><span class="p">;</span>
    <span class="k">if</span> <span class="p">(</span><span class="k">this</span><span class="p">.</span><span class="nx">ended</span><span class="p">)</span>
        <span class="k">return</span> <span class="o">!</span><span class="mi">1</span><span class="p">;</span>
    <span class="nx">i</span> <span class="o">=</span> <span class="nx">t</span> <span class="o">===</span> <span class="o">~~</span><span class="nx">t</span> <span class="p">?</span> <span class="nx">t</span> <span class="p">:</span> <span class="o">!</span><span class="mi">0</span> <span class="o">===</span> <span class="nx">t</span> <span class="p">?</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_FINISH</span> <span class="p">:</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_NO_FLUSH</span><span class="p">,</span>
    <span class="dl">"</span><span class="s2">string</span><span class="dl">"</span> <span class="o">==</span> <span class="k">typeof</span> <span class="nx">e</span> <span class="p">?</span> <span class="nx">d</span><span class="p">.</span><span class="nx">input</span> <span class="o">=</span> <span class="nx">s</span><span class="p">.</span><span class="nx">binstring2buf</span><span class="p">(</span><span class="nx">e</span><span class="p">)</span> <span class="p">:</span> <span class="dl">"</span><span class="s2">[object ArrayBuffer]</span><span class="dl">"</span> <span class="o">===</span> <span class="nx">h</span><span class="p">.</span><span class="nx">call</span><span class="p">(</span><span class="nx">e</span><span class="p">)</span> <span class="p">?</span> <span class="nx">d</span><span class="p">.</span><span class="nx">input</span> <span class="o">=</span> <span class="k">new</span> <span class="nb">Uint8Array</span><span class="p">(</span><span class="nx">e</span><span class="p">)</span> <span class="p">:</span> <span class="nx">d</span><span class="p">.</span><span class="nx">input</span> <span class="o">=</span> <span class="nx">e</span><span class="p">,</span>
    <span class="nx">d</span><span class="p">.</span><span class="nx">next_in</span> <span class="o">=</span> <span class="mi">0</span><span class="p">,</span>
    <span class="nx">d</span><span class="p">.</span><span class="nx">avail_in</span> <span class="o">=</span> <span class="nx">d</span><span class="p">.</span><span class="nx">input</span><span class="p">.</span><span class="nx">length</span><span class="p">;</span>
    <span class="k">do</span> <span class="p">{</span>
        <span class="k">if</span> <span class="p">(</span>
            <span class="mi">0</span> <span class="o">===</span> <span class="nx">d</span><span class="p">.</span><span class="nx">avail_out</span> <span class="o">&amp;&amp;</span> <span class="p">(</span><span class="nx">d</span><span class="p">.</span><span class="nx">output</span> <span class="o">=</span> <span class="k">new</span> <span class="nx">a</span><span class="p">.</span><span class="nx">Buf8</span><span class="p">(</span><span class="nx">f</span><span class="p">),</span>
            <span class="nx">d</span><span class="p">.</span><span class="nx">next_out</span> <span class="o">=</span> <span class="mi">0</span><span class="p">,</span>
            <span class="nx">d</span><span class="p">.</span><span class="nx">avail_out</span> <span class="o">=</span> <span class="nx">f</span><span class="p">),</span>
            <span class="p">(</span><span class="nx">n</span> <span class="o">=</span> <span class="nx">o</span><span class="p">.</span><span class="nx">inflate</span><span class="p">(</span><span class="nx">d</span><span class="p">,</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_NO_FLUSH</span><span class="p">))</span> <span class="o">===</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_NEED_DICT</span> <span class="o">&amp;&amp;</span> <span class="nx">p</span> <span class="o">&amp;&amp;</span> <span class="p">(</span><span class="nx">n</span> <span class="o">=</span> <span class="nx">o</span><span class="p">.</span><span class="nx">inflateSetDictionary</span><span class="p">(</span><span class="k">this</span><span class="p">.</span><span class="nx">strm</span><span class="p">,</span> <span class="nx">p</span><span class="p">)),</span>
            <span class="nx">n</span> <span class="o">===</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_BUF_ERROR</span> <span class="o">&amp;&amp;</span> 
            <span class="o">!</span><span class="mi">0</span> <span class="o">===</span> <span class="nx">v</span> <span class="o">&amp;&amp;</span> 
            <span class="p">(</span><span class="nx">n</span> <span class="o">=</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_OK</span><span class="p">,</span><span class="nx">v</span> <span class="o">=</span> <span class="o">!</span><span class="mi">1</span><span class="p">),</span>
            <span class="nx">n</span> <span class="o">!==</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_STREAM_END</span> <span class="o">&amp;&amp;</span> 
            <span class="nx">n</span> <span class="o">!==</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_OK</span><span class="p">)</span>
                <span class="k">return</span> <span class="k">this</span><span class="p">.</span><span class="nx">onEnd</span><span class="p">(</span><span class="nx">n</span><span class="p">),</span><span class="o">!</span><span class="p">(</span><span class="k">this</span><span class="p">.</span><span class="nx">ended</span> <span class="o">=</span> <span class="o">!</span><span class="mi">0</span><span class="p">);</span>
        <span class="nx">d</span><span class="p">.</span><span class="nx">next_out</span> <span class="o">&amp;&amp;</span> <span class="p">(</span><span class="mi">0</span> <span class="o">!==</span> <span class="nx">d</span><span class="p">.</span><span class="nx">avail_out</span> <span class="o">&amp;&amp;</span> <span class="nx">n</span> <span class="o">!==</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_STREAM_END</span> <span class="o">&amp;&amp;</span> <span class="p">(</span><span class="mi">0</span> <span class="o">!==</span> <span class="nx">d</span><span class="p">.</span><span class="nx">avail_in</span> <span class="o">||</span> <span class="nx">i</span> <span class="o">!==</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_FINISH</span> <span class="o">&amp;&amp;</span> <span class="nx">i</span> <span class="o">!==</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_SYNC_FLUSH</span><span class="p">)</span> <span class="o">||</span> <span class="p">(</span><span class="dl">"</span><span class="s2">string</span><span class="dl">"</span> <span class="o">===</span> <span class="k">this</span><span class="p">.</span><span class="nx">options</span><span class="p">.</span><span class="nx">to</span> <span class="p">?</span> <span class="p">(</span><span class="nx">r</span> <span class="o">=</span> <span class="nx">s</span><span class="p">.</span><span class="nx">utf8border</span><span class="p">(</span><span class="nx">d</span><span class="p">.</span><span class="nx">output</span><span class="p">,</span> <span class="nx">d</span><span class="p">.</span><span class="nx">next_out</span><span class="p">),</span>
        <span class="nx">c</span> <span class="o">=</span> <span class="nx">d</span><span class="p">.</span><span class="nx">next_out</span> <span class="o">-</span> <span class="nx">r</span><span class="p">,</span>
        <span class="nx">u</span> <span class="o">=</span> <span class="nx">s</span><span class="p">.</span><span class="nx">buf2string</span><span class="p">(</span><span class="nx">d</span><span class="p">.</span><span class="nx">output</span><span class="p">,</span> <span class="nx">r</span><span class="p">),</span>
        <span class="nx">d</span><span class="p">.</span><span class="nx">next_out</span> <span class="o">=</span> <span class="nx">c</span><span class="p">,</span>
        <span class="nx">d</span><span class="p">.</span><span class="nx">avail_out</span> <span class="o">=</span> <span class="nx">f</span> <span class="o">-</span> <span class="nx">c</span><span class="p">,</span>
        <span class="nx">c</span> <span class="o">&amp;&amp;</span> <span class="nx">a</span><span class="p">.</span><span class="nx">arraySet</span><span class="p">(</span><span class="nx">d</span><span class="p">.</span><span class="nx">output</span><span class="p">,</span> <span class="nx">d</span><span class="p">.</span><span class="nx">output</span><span class="p">,</span> <span class="nx">r</span><span class="p">,</span> <span class="nx">c</span><span class="p">,</span> <span class="mi">0</span><span class="p">),</span>
        <span class="k">this</span><span class="p">.</span><span class="nx">onData</span><span class="p">(</span><span class="nx">u</span><span class="p">))</span> <span class="p">:</span> <span class="k">this</span><span class="p">.</span><span class="nx">onData</span><span class="p">(</span><span class="nx">a</span><span class="p">.</span><span class="nx">shrinkBuf</span><span class="p">(</span><span class="nx">d</span><span class="p">.</span><span class="nx">output</span><span class="p">,</span> <span class="nx">d</span><span class="p">.</span><span class="nx">next_out</span><span class="p">)))),</span>
        <span class="mi">0</span> <span class="o">===</span> <span class="nx">d</span><span class="p">.</span><span class="nx">avail_in</span> <span class="o">&amp;&amp;</span> <span class="mi">0</span> <span class="o">===</span> <span class="nx">d</span><span class="p">.</span><span class="nx">avail_out</span> <span class="o">&amp;&amp;</span> <span class="p">(</span><span class="nx">v</span> <span class="o">=</span> <span class="o">!</span><span class="mi">0</span><span class="p">)</span>
    <span class="p">}</span> <span class="k">while</span> <span class="p">((</span><span class="mi">0</span> <span class="o">&lt;</span> <span class="nx">d</span><span class="p">.</span><span class="nx">avail_in</span> <span class="o">||</span> <span class="mi">0</span> <span class="o">===</span> <span class="nx">d</span><span class="p">.</span><span class="nx">avail_out</span><span class="p">)</span> <span class="o">&amp;&amp;</span> <span class="nx">n</span> <span class="o">!==</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_STREAM_END</span><span class="p">);</span>
    <span class="k">return</span> <span class="nx">n</span> <span class="o">===</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_STREAM_END</span> <span class="o">&amp;&amp;</span> <span class="p">(</span><span class="nx">i</span> <span class="o">=</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_FINISH</span><span class="p">),</span>
    <span class="nx">i</span> <span class="o">===</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_FINISH</span> <span class="p">?</span> <span class="p">(</span><span class="nx">n</span> <span class="o">=</span> <span class="nx">o</span><span class="p">.</span><span class="nx">inflateEnd</span><span class="p">(</span><span class="k">this</span><span class="p">.</span><span class="nx">strm</span><span class="p">),</span>
    <span class="k">this</span><span class="p">.</span><span class="nx">onEnd</span><span class="p">(</span><span class="nx">n</span><span class="p">),</span>
    <span class="k">this</span><span class="p">.</span><span class="nx">ended</span> <span class="o">=</span> <span class="o">!</span><span class="mi">0</span><span class="p">,</span>
    <span class="nx">n</span> <span class="o">===</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_OK</span><span class="p">)</span> <span class="p">:</span> <span class="nx">i</span> <span class="o">!==</span> <span class="nx">l</span><span class="p">.</span><span class="nx">Z_SYNC_FLUSH</span> <span class="o">||</span> <span class="p">(</span><span class="k">this</span><span class="p">.</span><span class="nx">onEnd</span><span class="p">(</span><span class="nx">l</span><span class="p">.</span><span class="nx">Z_OK</span><span class="p">),</span>
    <span class="o">!</span><span class="p">(</span><span class="nx">d</span><span class="p">.</span><span class="nx">avail_out</span> <span class="o">=</span> <span class="mi">0</span><span class="p">))</span>
<span class="p">}</span>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2021-02-26T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2021/02/13/c.html">C#</a></div><div class="next"><span>下篇</span><a href="/2021/02/26/vscode-edge-debugger.html">VS Code Edge Debugger</a></div></div></div>

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