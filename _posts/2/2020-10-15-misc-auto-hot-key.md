---
title: AutoHotKey
date: 2020-10-15 00:00:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="AutoHotKey"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-10-15T08:00:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="AutoHotKey" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-15T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="AutoHotKey" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-15T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="autohotkey">AutoHotKey</h1>

<p>AHK(AutoHotKey)是一种DSL(Domain Specific Language),同时也是一种脚本语言,专注于各种自动化执行脚本(比如绑定各种快捷键操作等等)<br />
AHK脚本文件以<code class="language-plaintext highlighter-rouge">.ahk</code>结尾,在Windows下直接点击脚本文件便可以自动调用<code class="language-plaintext highlighter-rouge">AutoHotKey.exe</code>执行</p>

<h2 id="变量">变量</h2>

<p>AHK定义变量的方式和Python差不多,直接声明就能使用(<code class="language-plaintext highlighter-rouge">x := 123</code>或者<code class="language-plaintext highlighter-rouge">x := "123"</code>等等)</p>

<h3 id="string">String</h3>

<p><code class="language-plaintext highlighter-rouge">x = "123"</code></p>

<h3 id="number">Number</h3>

<p>允许好几种定义数字数据类型的变量</p>

<ul>
  <li><code class="language-plaintext highlighter-rouge">x := 123</code></li>
  <li><code class="language-plaintext highlighter-rouge">x := 00123</code></li>
  <li><code class="language-plaintext highlighter-rouge">x := -1</code></li>
  <li><code class="language-plaintext highlighter-rouge">x := 0X123B</code></li>
  <li><code class="language-plaintext highlighter-rouge">x := 0x123B</code></li>
  <li><code class="language-plaintext highlighter-rouge">x := -0x123B</code></li>
  <li><code class="language-plaintext highlighter-rouge">x := 3.14</code></li>
</ul>

<h3 id="boolean">Boolean</h3>

<p><code class="language-plaintext highlighter-rouge">x := True</code></p>

<h3 id="nothing">Nothing</h3>

<p>在AHK里也存在类似<code class="language-plaintext highlighter-rouge">null</code>的值,例如<code class="language-plaintext highlighter-rouge">x</code>,这个时候<code class="language-plaintext highlighter-rouge">x</code>的默认值为<code class="language-plaintext highlighter-rouge">""</code>(空字符串)</p>

<h3 id="object">Object</h3>

<p>和面向对象语言一样,也支持对象类型</p>

<h2 id="面向对象">面向对象</h2>

<h3 id="属性">属性</h3>

<p>Object的属性访问(<code class="language-plaintext highlighter-rouge">getter</code>和<code class="language-plaintext highlighter-rouge">setter</code>)有几种方式</p>

<ul>
  <li><code class="language-plaintext highlighter-rouge">obj.name</code>调用<code class="language-plaintext highlighter-rouge">name</code>属性</li>
  <li><code class="language-plaintext highlighter-rouge">obj[name]</code>和上述一样,只不过这里的<code class="language-plaintext highlighter-rouge">name</code>可以是表达式</li>
  <li><code class="language-plaintext highlighter-rouge">obj[arg1, arg2, ..., argN]</code>,由于AHK的属性有可能是可以接收参数的,所以还提供了带参数的属性访问方式</li>
  <li><code class="language-plaintext highlighter-rouge">obj.name[arg2, ..., argN]</code>,和上面差不多,只不过这里显示指定出了属性的名字</li>
</ul>

<h3 id="getter-setter">getter setter</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">class</span> <span class="nc">A</span><span class="o">{</span>
    <span class="no">B</span><span class="o">[]{</span>
        <span class="n">get</span><span class="o">{</span>
            <span class="k">return</span> <span class="o">...</span>
        <span class="o">}</span>   
        <span class="n">set</span><span class="o">{</span>
            <span class="k">return</span> <span class="o">...:=</span><span class="n">val</span>
        <span class="o">}</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<p>以上例子给出了一个<code class="language-plaintext highlighter-rouge">getter</code>,<code class="language-plaintext highlighter-rouge">setter</code>的使用方法,其中<code class="language-plaintext highlighter-rouge">B</code>被定义为<code class="language-plaintext highlighter-rouge">A</code>的一个属性<br />
在使用<code class="language-plaintext highlighter-rouge">A.B</code>对<code class="language-plaintext highlighter-rouge">A</code>的<code class="language-plaintext highlighter-rouge">B</code>属性进行读取的时候会被拦截,转而调用<code class="language-plaintext highlighter-rouge">B</code>属性的<code class="language-plaintext highlighter-rouge">get</code>方法<br />
某种程度也是一种元编程技术</p>

<h3 id="方法">方法</h3>

<ul>
  <li><code class="language-plaintext highlighter-rouge">obj.name(arg2, ..., argN)</code></li>
  <li><code class="language-plaintext highlighter-rouge">obj.name[arg2, ..., argN]</code>和上述一样,只不过换成方括号方式调用</li>
  <li><code class="language-plaintext highlighter-rouge">obj[name](arg2, ..., argN)</code>和上述一样,只不过这里的<code class="language-plaintext highlighter-rouge">name</code>可以是表达式</li>
</ul>

<h3 id="内存释放">内存释放</h3>

<p>AHK采用引用计数方式,对一个对象的所有引用都失效之后会自动释放内存,类似C++的<code class="language-plaintext highlighter-rouge">shared_ptr&lt;&gt;()</code></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">obj</span> <span class="o">:=</span> <span class="o">{}</span>
<span class="n">obj</span> <span class="o">:=</span> <span class="s">""</span>
</code></pre></div></div>

<p>如上述例子,在把<code class="language-plaintext highlighter-rouge">obj</code>赋值给<code class="language-plaintext highlighter-rouge">""</code>之后,<code class="language-plaintext highlighter-rouge">{}</code>就会自动被释放</p>

<h3 id="地址转换">地址转换</h3>

<p>可以通过<code class="language-plaintext highlighter-rouge">addr := &amp;obj</code>把对象的地址赋值给<code class="language-plaintext highlighter-rouge">addr</code><br />
因为AHK通过引用计数方式管理内存释放,可以通过<code class="language-plaintext highlighter-rouge">ObjAddRef(addr)</code>对对象增加一个引用计数(因为可以通过<code class="language-plaintext highlighter-rouge">addr</code>调用到对象,所以这是必要的)<br />
<code class="language-plaintext highlighter-rouge">addr</code>可以通过<code class="language-plaintext highlighter-rouge">obj := Object(addr)</code>函数得到对象<br />
通过<code class="language-plaintext highlighter-rouge">Object(obj)</code>创建的对象必须手动调用<code class="language-plaintext highlighter-rouge">ObjRelease(addr)</code>释放<br />
反之通过赋值运算符的就不需要手动调用<code class="language-plaintext highlighter-rouge">ObjRelease(addr)</code><br />
例如</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">ref1</span> <span class="o">:=</span> <span class="nc">Object</span><span class="o">()</span>
<span class="n">ref2</span> <span class="o">:=</span> <span class="n">ref1</span>
<span class="n">ref1</span> <span class="o">:=</span> <span class="s">""</span>
<span class="n">ref2</span> <span class="o">:=</span> <span class="s">""</span>
</code></pre></div></div>

<h3 id="元编程">元编程</h3>

<p>和<code class="language-plaintext highlighter-rouge">Python</code>命名规范差不多,AHK的构造也是<code class="language-plaintext highlighter-rouge">__New(...)</code>这种类型</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">m1</span> <span class="o">:=</span> <span class="k">new</span> <span class="nc">GMem</span><span class="o">(</span><span class="mi">0</span><span class="o">,</span> <span class="mi">20</span><span class="o">)</span>
<span class="n">m2</span> <span class="o">:=</span> <span class="o">{</span><span class="nl">base:</span> <span class="nc">GMem</span><span class="o">}.</span><span class="na">__New</span><span class="o">(</span><span class="mi">0</span><span class="o">,</span> <span class="mi">30</span><span class="o">)</span>

<span class="kd">class</span> <span class="nc">GMem</span>
<span class="o">{</span>
    <span class="n">__New</span><span class="o">(</span><span class="n">aFlags</span><span class="o">,</span> <span class="n">aSize</span><span class="o">)</span>
    <span class="o">{</span>
        <span class="k">this</span><span class="o">.</span><span class="na">ptr</span> <span class="o">:=</span> <span class="nc">DllCall</span><span class="o">(</span><span class="s">"GlobalAlloc"</span><span class="o">,</span> <span class="s">"UInt"</span><span class="o">,</span> <span class="n">aFlags</span><span class="o">,</span> <span class="s">"Ptr"</span><span class="o">,</span> <span class="n">aSize</span><span class="o">,</span> <span class="s">"Ptr"</span><span class="o">)</span>
        <span class="k">if</span> <span class="o">!</span><span class="k">this</span><span class="o">.</span><span class="na">ptr</span>
            <span class="k">return</span> <span class="s">""</span>
        <span class="nc">MsgBox</span> <span class="o">%</span> <span class="s">"New GMem of "</span> <span class="n">aSize</span> <span class="s">" bytes at address "</span> <span class="k">this</span><span class="o">.</span><span class="na">ptr</span> <span class="s">"."</span>
        <span class="k">return</span> <span class="k">this</span>  <span class="o">;</span> <span class="nc">This</span> <span class="n">line</span> <span class="n">can</span> <span class="n">be</span> <span class="n">omitted</span> <span class="n">when</span> <span class="n">using</span> <span class="n">the</span> <span class="err">'</span><span class="k">new</span><span class="err">'</span> <span class="n">operator</span><span class="o">.</span>
    <span class="o">}</span>

    <span class="n">__Delete</span><span class="o">()</span>
    <span class="o">{</span>
        <span class="nc">MsgBox</span> <span class="o">%</span> <span class="s">"Delete GMem at address "</span> <span class="k">this</span><span class="o">.</span><span class="na">ptr</span> <span class="s">"."</span>
        <span class="nc">DllCall</span><span class="o">(</span><span class="s">"GlobalFree"</span><span class="o">,</span> <span class="s">"Ptr"</span><span class="o">,</span> <span class="k">this</span><span class="o">.</span><span class="na">ptr</span><span class="o">)</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<p>更多的元编程函数见官方文档</p>

<h3 id="数组">数组</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">obj</span> <span class="o">:=</span> <span class="o">[</span><span class="mi">1</span><span class="o">,</span><span class="mi">2</span><span class="o">,</span><span class="mi">3</span><span class="o">]</span>
</code></pre></div></div>

<h3 id="关联数组">关联数组</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">obj</span> <span class="o">:=</span> <span class="o">{</span><span class="n">a</span> <span class="o">:</span> <span class="mi">123</span><span class="o">,</span> <span class="n">b</span> <span class="o">:</span> <span class="mi">123</span><span class="o">}</span>
</code></pre></div></div>

<p>以上代码就自动对<code class="language-plaintext highlighter-rouge">Object()</code>创建的对象自动调用引用的增加和减少,所以在执行完<code class="language-plaintext highlighter-rouge">ref2 := ""</code>之后<code class="language-plaintext highlighter-rouge">Object()</code>就会被释放</p>

<h3 id="自定义对象">自定义对象</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">class</span> <span class="nc">baseObject</span> <span class="o">{</span>
    <span class="kd">static</span> <span class="n">foo</span> <span class="o">:=</span> <span class="s">"bar"</span>
<span class="o">}</span>

<span class="c1">//也可以采用如下方式定义对象,效果和上述声明相同</span>
<span class="c1">//baseObject := {foo: "bar"}</span>

<span class="n">obj1</span> <span class="o">:=</span> <span class="nc">Object</span><span class="o">(),</span> <span class="n">obj1</span><span class="o">.</span><span class="na">base</span> <span class="o">:=</span> <span class="n">baseObject</span>
<span class="n">obj2</span> <span class="o">:=</span> <span class="o">{</span><span class="nl">base:</span> <span class="n">baseObject</span><span class="o">}</span>
<span class="n">obj3</span> <span class="o">:=</span> <span class="k">new</span> <span class="n">baseObject</span>
<span class="nc">MsgBox</span> <span class="o">%</span> <span class="n">obj1</span><span class="o">.</span><span class="na">foo</span> <span class="s">" "</span> <span class="n">obj2</span><span class="o">.</span><span class="na">foo</span> <span class="s">" "</span> <span class="n">obj3</span><span class="o">.</span><span class="na">foo</span>
</code></pre></div></div>

<p>通过定义在每个对象的默认的<code class="language-plaintext highlighter-rouge">base</code>属性<br />
在执行的时候子对象可以如果在当前类找不到合适的方法会转而在<code class="language-plaintext highlighter-rouge">base</code>属性的对象里去寻找<br />
这个机制其实有点像继承,区别的是它不提供多态机制</p>

<h3 id="继承">继承</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">class</span> <span class="nc">ClassName</span> <span class="kd">extends</span> <span class="nc">BaseClassName</span>
<span class="o">{</span>
    <span class="nc">InstanceVar</span> <span class="o">:=</span> <span class="nc">Expression</span>
    <span class="kd">static</span> <span class="nc">ClassVar</span> <span class="o">:=</span> <span class="nc">Expression</span>

    <span class="kd">class</span> <span class="nc">NestedClass</span>
    <span class="o">{</span>
        <span class="o">...</span>
    <span class="o">}</span>

    <span class="nc">Method</span><span class="o">()</span>
    <span class="o">{</span>
        <span class="o">...</span>
    <span class="o">}</span>

    <span class="nc">Property</span><span class="o">[]</span>  <span class="o">;</span> <span class="nc">Brackets</span> <span class="n">are</span> <span class="n">optional</span>
    <span class="o">{</span>
        <span class="n">get</span> <span class="o">{</span>
            <span class="k">return</span> <span class="o">...</span>
        <span class="o">}</span>
        <span class="n">set</span> <span class="o">{</span>
            <span class="k">return</span> <span class="o">...</span> <span class="o">:=</span> <span class="n">value</span>
        <span class="o">}</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h2 id="过程">过程</h2>

<h3 id="命令">命令</h3>

<p>命令其实是老版本AHK遗留下来的垃圾语法,例如<code class="language-plaintext highlighter-rouge">MsgBox hello world</code><br />
其实就是函数调用,只不过没有括号,而且后面跟上的参数会被解析成字面常量<br />
但是要引用变量也不是不行,例如<code class="language-plaintext highlighter-rouge">MsgBox %x%</code>就会传入<code class="language-plaintext highlighter-rouge">x</code>参数的值<br />
也可以传入表达式,例如<code class="language-plaintext highlighter-rouge">MsgBox % 1 + 2</code>就会计算<code class="language-plaintext highlighter-rouge">1 + 2</code>返回<code class="language-plaintext highlighter-rouge">3</code>再传入参数</p>

<h3 id="函数">函数</h3>

<p>区别于其他编程语言,AHK的函数不需要显示指定返回值<br />
<code class="language-plaintext highlighter-rouge">func(Arg1, Arg2 := False){return True;}</code><br />
函数的调用差不多一样,<code class="language-plaintext highlighter-rouge">func(123)</code><br />
这里有一个细节,可以把函数通过内置<code class="language-plaintext highlighter-rouge">Func</code>函数转换成变量<code class="language-plaintext highlighter-rouge">x := Func("funcName")</code></p>

<h2 id="控制流">控制流</h2>

<h3 id="if">If</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nc">If</span> <span class="o">(</span><span class="n">intValue</span> <span class="o">=</span> <span class="mi">1</span> <span class="o">&amp;&amp;</span> <span class="n">intValue</span> <span class="o">=</span> <span class="mi">2</span><span class="o">){</span>
    <span class="c1">//...</span>
<span class="o">}</span>
<span class="nc">Else</span> <span class="nf">If</span><span class="o">(</span><span class="n">not</span> <span class="n">boolValue</span><span class="o">){</span>
    <span class="c1">//...</span>
<span class="o">}</span>
</code></pre></div></div>

<h3 id="loop">Loop</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nc">Loop</span><span class="o">,</span> <span class="mi">3</span><span class="o">{</span>
    <span class="c1">//...</span>
<span class="o">}</span>

<span class="nc">Loop</span> <span class="o">{</span>
    <span class="nc">If</span><span class="o">(</span><span class="cm">/**/</span><span class="o">){</span>
        <span class="nc">Break</span><span class="o">;</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h3 id="goto">Goto</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nl">Flag:</span>

<span class="nc">Gosub</span><span class="o">,</span> <span class="nc">Flag</span>
</code></pre></div></div>

<h2 id="标签">标签</h2>

<h3 id="普通标签">普通标签</h3>

<p>普通标签通过<code class="language-plaintext highlighter-rouge">Goto</code>等等命令进行跳转</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nl">Flag:</span>

<span class="nc">Goto</span><span class="o">,</span> <span class="nc">Flag</span>
</code></pre></div></div>

<h3 id="hotkey标签">Hotkey标签</h3>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="err">#</span><span class="nl">n:</span><span class="o">:</span>
<span class="nc">Run</span> <span class="nc">Notepad</span>
<span class="k">return</span>
</code></pre></div></div>

<p>Hotkey标签通过按键进行跳转(<code class="language-plaintext highlighter-rouge">#</code>代表<code class="language-plaintext highlighter-rouge">Win</code>键),所以以上的代码意义为每次按下<code class="language-plaintext highlighter-rouge">Win</code> + <code class="language-plaintext highlighter-rouge">n</code>键就会跳转到该标签</p>

<h3 id="hotstring标签">Hotstring标签</h3>

<p>Hotstring标签的意义就是提供一些缩写的机制</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="o">::</span><span class="nl">btw:</span><span class="o">:</span><span class="n">by</span> <span class="n">the</span> <span class="n">way</span>
</code></pre></div></div>

<p>以上代码在敲入<code class="language-plaintext highlighter-rouge">btw</code> + <code class="language-plaintext highlighter-rouge">enter</code>之后就会自动扩写成<code class="language-plaintext highlighter-rouge">by the way</code><br />
要免去<code class="language-plaintext highlighter-rouge">enter</code>的话可以加上选项</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="o">:*:</span><span class="nl">btw:</span><span class="o">:</span><span class="n">by</span> <span class="n">the</span> <span class="n">way</span>
</code></pre></div></div>

<p>也可以定义长段落的缩写</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="o">:*:</span><span class="nl">x:</span><span class="o">:</span>
<span class="o">(</span>
    <span class="n">hello</span>
    <span class="n">world</span>
<span class="o">)</span>
</code></pre></div></div>

<h2 id="键位重映射">键位重映射</h2>

<p><code class="language-plaintext highlighter-rouge">a::b</code>把<code class="language-plaintext highlighter-rouge">a</code>键映射成<code class="language-plaintext highlighter-rouge">b</code></p>

<h2 id="指令">指令</h2>

<h3 id="include">#Include</h3>

<p><code class="language-plaintext highlighter-rouge">#Include abc.ahk</code>导入一个文件,并使在其中定义的函数在此文件可以被调用</p>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-10-15T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/10/08/v2-dubbo-reference.html">V2 Dubbo 服务引入</a></div><div class="next"><span>下篇</span><a href="/2020/10/18/misc-linux-dynamic-linking.html">Linux 动态链接 Dynamic Linking</a></div></div></div>

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