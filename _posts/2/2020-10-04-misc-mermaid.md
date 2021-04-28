---
title: Mermaid 语法
date: 2020-10-04 00:00:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Mermaid 语法"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-10-04T08:00:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Mermaid 语法" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-04T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Mermaid 语法" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-04T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Mermaid 语法" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-04T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="参考地址">参考地址</h1>

<p><a href="https://github.com/mermaidjs/mermaid-gitbook/tree/master/content">mermaid-gitbook</a></p>

<h1 id="流程图">流程图</h1>

<ul>
  <li>流程图的基本框架是<code class="language-plaintext highlighter-rouge">A --&gt; B</code>来表示一个流程到另一个流程的转换</li>
  <li>流程图允许用户定义图像是横着显示还是竖着显示
    <ul>
      <li><code class="language-plaintext highlighter-rouge">graph LR</code>横着</li>
      <li><code class="language-plaintext highlighter-rouge">graph TD</code>竖着</li>
    </ul>
  </li>
  <li>流程图允许用户定义每个流程的形状,例如:<code class="language-plaintext highlighter-rouge">["A"] --&gt; {"B"}</code>
    <ul>
      <li><code class="language-plaintext highlighter-rouge">[]</code>正方形</li>
      <li><code class="language-plaintext highlighter-rouge">(())</code>圆形</li>
      <li><code class="language-plaintext highlighter-rouge">()</code>圆角矩形</li>
      <li><code class="language-plaintext highlighter-rouge">{}</code>菱形</li>
    </ul>
  </li>
  <li>流程图允许用户定义每个流程的别名,例如:<code class="language-plaintext highlighter-rouge">A["123"] --&gt; B{"456"}</code></li>
  <li>流程图允许用户定义流程之间转换的注释,例如:<code class="language-plaintext highlighter-rouge">A["123"] --&gt;|456|B{"789"}</code>
    <ul>
      <li><code class="language-plaintext highlighter-rouge">A[123] --&gt;|456|B{789}</code></li>
      <li><code class="language-plaintext highlighter-rouge">A[123] --456--&gt; B{789}</code></li>
    </ul>
  </li>
  <li>流程图允许用户定义连接的线类型(虚线,实线):<code class="language-plaintext highlighter-rouge">A["123"] -.--&gt; B{"456"}</code>
    <ul>
      <li><code class="language-plaintext highlighter-rouge">--&gt;</code>实线</li>
      <li><code class="language-plaintext highlighter-rouge">.-&gt;</code>虚线</li>
      <li><code class="language-plaintext highlighter-rouge">--</code>无箭头实线</li>
      <li><code class="language-plaintext highlighter-rouge">.-</code>无箭头虚线</li>
    </ul>
  </li>
  <li>流程图允许定义子图
    <div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>  subgraph 123
      ...
  end
</code></pre></div>    </div>
  </li>
</ul>

<pre><code class="language-mermaid">graph TD
    id1("123")
    id2{"456"}
    id3(("789"))

    id1 --&gt;|123| id2
    id2 .-&gt;|123| id3
</code></pre>

<h1 id="时序图">时序图</h1>

<ul>
  <li>时序图的基本语法是<code class="language-plaintext highlighter-rouge">Alica-&gt;&gt;Bob : 123</code></li>
  <li>允许定义循环
    <div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>  loop hello 
      Bob -&gt;&gt; Bob : 123`
  end
</code></pre></div>    </div>
  </li>
  <li>允许定义线类型
    <ul>
      <li><code class="language-plaintext highlighter-rouge">-&gt;&gt;</code>实线</li>
      <li><code class="language-plaintext highlighter-rouge">--&gt;&gt;</code>虚线</li>
    </ul>
  </li>
  <li>允许定义别名<code class="language-plaintext highlighter-rouge">participant A as Alice</code></li>
  <li>允许在一个过程中嵌套另一个过程(图2.2)
    <div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>  Alice -&gt;&gt; +Bob
  Alice -&gt;&gt; +Bob
  Bob -&gt;&gt; -Alice
  Bob -&gt;&gt; -Alice
</code></pre></div>    </div>
  </li>
  <li>允许定义分支(alt,opt)</li>
</ul>

<pre><code class="language-mermaid">sequenceDiagram
Alice -&gt;&gt; Bob : 123
Bob --&gt;&gt; Alice : 123
loop 123
    Bob -&gt;&gt; Alice : 123
end
</code></pre>

<p><strong>图2.1</strong></p>

<pre><code class="language-mermaid">sequenceDiagram
    Alice-&gt;&gt;+John: Hello John, how are you?
    Alice-&gt;&gt;+John: John, can you hear me?
    John--&gt;&gt;-Alice: Hi Alice, I can hear you!
    John--&gt;&gt;-Alice: I feel great!
</code></pre>

<p><strong>图2.2</strong></p>

<pre><code class="language-mermaid">sequenceDiagram
    Alice-&gt;&gt;Bob: Hello Bob, how are you?
    alt is sick
        Bob-&gt;&gt;Alice: Not so good :(
    else is well
        Bob-&gt;&gt;Alice: Feeling fresh like a daisy
    end
    opt Extra response
        Bob-&gt;&gt;Alice: Thanks for asking
    end
</code></pre>

<p><strong>图2.3</strong></p>

<h1 id="甘特图">甘特图</h1>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>gantt
section Section
Completed :done,    des1, 2014-01-06,2014-01-08
Active        :active,  des2, 2014-01-07, 3d
Parallel 1   :         des3, after des1, 1d
Parallel 2   :         des4, after des1, 1d
Parallel 3   :         des5, after des3, 1d
Parallel 4   :         des6, after des4, 1d
</code></pre></div></div>

<pre><code class="language-mermaid">gantt
section Section
Completed :done,    des1, 2014-01-06,2014-01-08
Active        :active,  des2, 2014-01-07, 3d
Parallel 1   :         des3, after des1, 1d
Parallel 2   :         des4, after des1, 1d
Parallel 3   :         des5, after des3, 1d
Parallel 4   :         des6, after des4, 1d
</code></pre>

<h1 id="类图">类图</h1>

<ul>
  <li>类图基本语法<code class="language-plaintext highlighter-rouge">ABC &lt;|-- DEF</code></li>
  <li>允许定义类之间的关系
    <ul>
      <li>继承<code class="language-plaintext highlighter-rouge">&lt;|--</code></li>
      <li>实现 <code class="language-plaintext highlighter-rouge">&lt;|..</code></li>
      <li>聚合 <code class="language-plaintext highlighter-rouge">o--</code>,<code class="language-plaintext highlighter-rouge">o--&gt;</code></li>
      <li>组合 <code class="language-plaintext highlighter-rouge">*--</code>,<code class="language-plaintext highlighter-rouge">*--&gt;</code></li>
      <li>关联 <code class="language-plaintext highlighter-rouge">--</code>,<code class="language-plaintext highlighter-rouge">--&gt;</code></li>
      <li>依赖 <code class="language-plaintext highlighter-rouge">..</code>,<code class="language-plaintext highlighter-rouge">..&gt;</code></li>
    </ul>
  </li>
  <li>允许定义类属性,方法<code class="language-plaintext highlighter-rouge">A : a()</code>,<code class="language-plaintext highlighter-rouge">A : 'a'</code>,<code class="language-plaintext highlighter-rouge">class A{...}</code></li>
  <li>允许定义接口<code class="language-plaintext highlighter-rouge">&lt;&lt;interface&gt;&gt; A</code></li>
</ul>

<pre><code class="language-mermaid">classDiagram
A &lt;|-- B
C ..|&gt; D
E o-- F
G o--&gt; H
I *-- J
K *--&gt; L
M &lt;--&gt; N
O &lt;..&gt; P
</code></pre>

<pre><code class="language-mermaid">classDiagram
Class01 &lt;|-- AveryLongClass : Cool
&lt;&lt;interface&gt;&gt; Class01
Class09 --&gt; C2 : Where am i?
Class09 --* C3
Class09 --|&gt; Class07
Class07 : equals()
Class07 : Object[] elementData
Class01 : size()
Class01 : int chimp
Class01 : int gorilla
class Class10 {
  &lt;&lt;service&gt;&gt;
  int id
  size()
}
</code></pre>

<h1 id="状态转换图">状态转换图</h1>

<ul>
  <li>基本语法<code class="language-plaintext highlighter-rouge">A --&gt; B</code></li>
  <li>允许定义开始状态和结束状态<code class="language-plaintext highlighter-rouge">[*] --&gt; A</code>,<code class="language-plaintext highlighter-rouge">A --&gt; [*]</code></li>
</ul>

<pre><code class="language-mermaid">stateDiagram
[*] --&gt; Still
Still --&gt; [*]
Still --&gt; Moving
Moving --&gt; Still
Moving --&gt; Crash
Crash --&gt; [*]
</code></pre>

<h1 id="饼状图">饼状图</h1>

<p>基本语法</p>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>pie
"Dogs" : 386
"Cats" : 85
"Rats" : 15
</code></pre></div></div>

<pre><code class="language-mermaid">pie
"Dogs" : 386
"Cats" : 85
"Rats" : 15
</code></pre>

<h1 id="user-journey">User Journey</h1>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>journey
title My working day
section Go to work
    Make tea: 5: Me
    Go upstairs: 3: Me
    Do work: 1: Me, Cat
section Go home
    Go downstairs: 5: Me
    Sit down: 3: Me
</code></pre></div></div>

<pre><code class="language-mermaid">journey
title My working day
section Go to work
    Make tea: 5: Me
    Go upstairs: 3: Me
    Do work: 1: Me, Cat
section Go home
    Go downstairs: 5: Me
    Sit down: 3: Me
</code></pre>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-10-04T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/09/30/misc-jekyll-text-markdown.html">Markdown 以及 Jekyll TeXt内置格式</a></div><div class="next"><span>下篇</span><a href="/2020/10/08/v2-dubbo-reference.html">V2 Dubbo 服务引入</a></div></div></div>

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