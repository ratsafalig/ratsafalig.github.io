---
title: Linux 动态链接 Dynamic Linking
date: 2020-10-18 00:00:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Linux 动态链接 Dynamic Linking"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-10-18T08:00:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Linux 动态链接 Dynamic Linking" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-18T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Linux 动态链接 Dynamic Linking" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-18T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Linux 动态链接 Dynamic Linking" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-10-18T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="编译过程">编译过程</h1>

<pre><code class="language-mermaid">graph TD
id1(".c")
id1 --预处理--&gt; id2(".i")
id2 --编译--&gt; id3(".s")
id3 --可重定位目标文件--&gt; id4(".o")
id5(".o")
id6(".a")
id6_1(".so")
id6_2(".so")
    id4 --链接--&gt; id7("链接器")
    id5 --链接--&gt; id7
    id6 --连接--&gt; id7
    id6_1 --链接--&gt; id7
    id6_2 --连接--&gt; id7 
        id7 --&gt; id8("可执行文件")
            id8 --&gt; id9("加载器")
                id10(".so")
                id11(".so")
                    id9 --动态链接--&gt; id12("动态连接器")
                    id10 --动态链接--&gt; id12
                    id11 --动态链接--&gt; id12
</code></pre>

<h1 id="elf格式">ELF格式</h1>

<p>现代<code class="language-plaintext highlighter-rouge">*unix</code>系统采用<code class="language-plaintext highlighter-rouge">ELF</code>文件格式作为可执行文件的格式<br />
<code class="language-plaintext highlighter-rouge">ELF</code>(<code class="language-plaintext highlighter-rouge">Executable and Linkable Format</code>)格式由以下几个部分组成</p>

<table>
  <tbody>
    <tr>
      <td>ELF头</td>
      <td> </td>
    </tr>
    <tr>
      <td>.text</td>
      <td>已经编译程序的机器代码</td>
    </tr>
    <tr>
      <td>.rodata</td>
      <td>只读数据</td>
    </tr>
    <tr>
      <td>.data</td>
      <td>已经初始化的全局变量和静态C变量</td>
    </tr>
    <tr>
      <td>.bss</td>
      <td>未初始化的全局和静态C变量</td>
    </tr>
    <tr>
      <td>.symtab</td>
      <td>一个符号表</td>
    </tr>
    <tr>
      <td>.rel.text</td>
      <td>一个.text节中位置的列表</td>
    </tr>
    <tr>
      <td>.rel.data</td>
      <td>被模块引用或定义的所有全局变量的重定位信息</td>
    </tr>
    <tr>
      <td>.debug</td>
      <td>一个符号调试表</td>
    </tr>
    <tr>
      <td>.line</td>
      <td>原始C源程序中的行号和.text节中机器指令之间的映射</td>
    </tr>
    <tr>
      <td>.strtab</td>
      <td>一个字符串表</td>
    </tr>
    <tr>
      <td>节头部表</td>
      <td> </td>
    </tr>
  </tbody>
</table>

<h1 id="符号解析">符号解析</h1>

<p>符号表的条目在<code class="language-plaintext highlighter-rouge">.symtab</code>节中<br />
符号表的定义如下</p>

<div class="language-c highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">typedef</span> <span class="k">struct</span><span class="p">{</span>
    <span class="kt">int</span> <span class="n">name</span><span class="p">;</span>
    <span class="kt">int</span> <span class="n">value</span><span class="p">;</span>
    <span class="kt">int</span> <span class="n">size</span><span class="p">;</span>
    <span class="kt">char</span> <span class="n">type</span><span class="o">:</span><span class="mi">4</span><span class="p">,</span>
            <span class="nl">binding:</span><span class="mi">4</span><span class="p">;</span>
    <span class="kt">char</span> <span class="n">reserved</span><span class="p">;</span>
    <span class="kt">char</span> <span class="n">section</span><span class="p">;</span>
<span class="p">}</span><span class="n">Elf_Symbol</span><span class="p">;</span>
</code></pre></div></div>

<p>其中<code class="language-plaintext highlighter-rouge">name</code>为<code class="language-plaintext highlighter-rouge">.strtab</code>的偏移量<br />
<code class="language-plaintext highlighter-rouge">value</code>为节偏移,代表这个符号在它所在的节的偏移量<br />
<code class="language-plaintext highlighter-rouge">type</code>表明是变量还是函数<br />
在代码中,难免会引用到其他文件写好的函数或者变量,但是编译的时候解析到当前文件的时候并不知道引用的函数的信息<br />
所以会在<code class="language-plaintext highlighter-rouge">.rel.text</code>和<code class="language-plaintext highlighter-rouge">.rel.data</code>生成重定位条目</p>

<div class="language-c highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">typedef</span> <span class="k">struct</span><span class="p">{</span>
    <span class="kt">long</span> <span class="n">offset</span><span class="p">;</span>
    <span class="kt">long</span> <span class="n">type</span><span class="o">:</span><span class="mi">32</span><span class="p">,</span>
         <span class="nl">symbol:</span><span class="mi">32</span><span class="p">;</span>
    <span class="kt">long</span> <span class="n">addend</span><span class="p">;</span>
<span class="p">}</span><span class="n">Elf64_Rela</span><span class="p">;</span>
</code></pre></div></div>

<p>其中<code class="language-plaintext highlighter-rouge">offset</code>和<code class="language-plaintext highlighter-rouge">type</code>指明了被重定位的符号在哪里<br />
<code class="language-plaintext highlighter-rouge">symbol</code>指向<code class="language-plaintext highlighter-rouge">.symtab</code>的偏移<br />
编译过程中编译器会把所有的源文件整合成一整个<code class="language-plaintext highlighter-rouge">ELF</code><br />
并且为所有的函数,变量分配一个确定的运行时地址<br />
解析符号的过程中会根据<code class="language-plaintext highlighter-rouge">Elf64_Rela</code>把不确定的符号引用解析成相对引用或者绝对引用</p>

<h1 id="动态链接">动态链接</h1>

<p>本篇不对静态链接作解释,因为静态链接无非就是把所有的代码编到同一个可执行文件里,所以没啥好说<br />
假设一台电脑上有很多代码只有一行的文件,但是这些文件都引用了一个非常大的库,这样的话虽然代码就一行  <br />
但是由于引用了库,还是会导致编译过后的文件非常大,为了避免这种情况,引入了动态链接的概念<br />
所谓动态链接就是用一种机制来实现代码的共享,动态链接的共享体现在两个方面</p>

<ul>
  <li>硬盘内的共享,无需把所有的库都编译都编译到一个可执行文件,节省硬盘空间</li>
  <li>内存内的共享,无需把所有加载该库的进程都在内存里分配一个该库的拷贝,节省内存空间</li>
</ul>

<h2 id="链接时动态链接">链接时动态链接</h2>

<h3 id="硬盘内的共享">硬盘内的共享</h3>

<p><code class="language-plaintext highlighter-rouge">ELF</code>文件中实际上在动态链接时会引入一个<code class="language-plaintext highlighter-rouge">.interp</code>节<br />
在<a href="#编译过程">编译过程</a>的流程图里的将<code class="language-plaintext highlighter-rouge">.so</code>,<code class="language-plaintext highlighter-rouge">.a</code>,<code class="language-plaintext highlighter-rouge">.o</code>编译成可执行文件的过程中</p>

<p class="info">会在<code class="language-plaintext highlighter-rouge">.interp</code>存入系统的动态连接器信息,同时存进去一些信息(例如动态连接库的名称信息等等,注意不是存整个<code class="language-plaintext highlighter-rouge">.so</code>,而是存标识符之类的东西),这一过程就节省了硬盘空间</p>
<p>这里注意动态连接器本身也是一个<code class="language-plaintext highlighter-rouge">.so</code>文件(<code class="language-plaintext highlighter-rouge">linux-lb.so</code>),而且这个库没有引用任何其他库</p>

<h3 id="内存内的共享">内存内的共享</h3>

<p>在编译完的可执行文件运行的时候,会调用操作系统的加载器<br />
加载器根据<code class="language-plaintext highlighter-rouge">.interp</code>节的信息加载所有的<code class="language-plaintext highlighter-rouge">.so</code>,然后进行重定位等等操作</p>

<p class="info">而且,如果加载器发现内存中已经有其他的进程也使用了这些共享库并且已经被加载到内存中<br />
就直接把共享库的物理地址映射到当前进程的虚拟空间就行,节省了内存空间</p>

<p>但是这里有一个点,<code class="language-plaintext highlighter-rouge">.so</code>的加载是在编译之后的,也就是说代码已经被写死了<br />
而且在代码的编译时并不知道加载的<code class="language-plaintext highlighter-rouge">.so</code>会被分配到哪个具体的实际虚拟地址,那么对这种代码怎么编译呢</p>

<p>这个问题通过<code class="language-plaintext highlighter-rouge">GOT(Global Offset Table)全局偏移表</code>和<code class="language-plaintext highlighter-rouge">PLT(Procedure Linkage Table)过程连接表</code>实现</p>

<h3 id="got">GOT</h3>

<p>介绍<code class="language-plaintext highlighter-rouge">GOT</code>首先要介绍<code class="language-plaintext highlighter-rouge">PIC(Position Independent Code)位置无关代码</code><br />
也就是说代码的生成和具体的位置无关(其实并不是真的无关,只是<code class="language-plaintext highlighter-rouge">.text</code>段的符号引用代码的生成和符号在<code class="language-plaintext highlighter-rouge">.text</code>段的位置无关)<br />
首先说一下不管在任何情况下,<code class="language-plaintext highlighter-rouge">.text</code>的虚拟地址段和<code class="language-plaintext highlighter-rouge">.data</code>的虚拟地址段都是固定的<br />
这样也就造成了<code class="language-plaintext highlighter-rouge">.text</code>和<code class="language-plaintext highlighter-rouge">.data</code>的地址的间隔也是固定的<br />
如果我们在<code class="language-plaintext highlighter-rouge">.text</code>段出现的变量都分配在<code class="language-plaintext highlighter-rouge">.data</code>的固定位置,而且两个位置的差总是等于<code class="language-plaintext highlighter-rouge">.text</code>和<code class="language-plaintext highlighter-rouge">.data</code>的间隔<br />
就可以根据<code class="language-plaintext highlighter-rouge">.text</code>中的变量引用位置马上计算出<code class="language-plaintext highlighter-rouge">.data</code>的变量位置,这个机制其实就是<code class="language-plaintext highlighter-rouge">GOT</code></p>

<h3 id="plt">PLT</h3>

<p>由于动态链接的特性,直到运行时才会直到<code class="language-plaintext highlighter-rouge">.so</code>加载的位置,也就是说即使是利用<code class="language-plaintext highlighter-rouge">GOT</code>是不能解决问题的(如果知道<code class="language-plaintext highlighter-rouge">.so</code>要被分配对应的到<code class="language-plaintext highlighter-rouge">GOT</code>的位置,那么根本就不需要<code class="language-plaintext highlighter-rouge">GOT</code>机制,直接写死就行)<br />
所以为了利用这个机制,提供了<code class="language-plaintext highlighter-rouge">PLT</code>机制<br />
编译器给每个未解析的共享库符号都分配一个<code class="language-plaintext highlighter-rouge">PLT</code>的条目,头一次调用的时候,将会将控制流跳转到该符号对应的<code class="language-plaintext highlighter-rouge">PLT</code>处(例如<code class="language-plaintext highlighter-rouge">call sym</code>,将会跳转到<code class="language-plaintext highlighter-rouge">sym</code>对应的<code class="language-plaintext highlighter-rouge">PLT</code>条目)<br />
该<code class="language-plaintext highlighter-rouge">PLT</code>条目的存的第一跳代码是跳转到<code class="language-plaintext info highlighter-rouge">PLT条目对应的GOT条目</code><br />
第一次调用的时候,<code class="language-plaintext highlighter-rouge">GOT</code>条目又会跳转回<code class="language-plaintext highlighter-rouge">PLT</code>条目的下一条指令(刚才跳转到<code class="language-plaintext highlighter-rouge">GOT</code>的下一条)<br />
然后<code class="language-plaintext highlighter-rouge">PLT</code>执行自己的流程,将控制流转到动态连接器,动态连接器覆盖<code class="language-plaintext info highlighter-rouge">该符号的PLT条目对应的GOT条目</code><br />
下一次调用的时候,过程就会短很多</p>
<ol>
  <li>跳转到<code class="language-plaintext highlighter-rouge">PLT</code></li>
  <li>跳转到<code class="language-plaintext highlighter-rouge">GOT</code>(由于这个时候<code class="language-plaintext highlighter-rouge">GOT</code>已经被覆盖成符号的运行时地址,所以无需再次调用动态链接器)</li>
</ol>

<p>借用一张csapp第三版的图说明</p>

<p><img src="/assets/2/QQ截图20201019164656.jpg" alt="" class="rounded shadow border" /></p>

<h2 id="运行时动态链接">运行时动态链接</h2>

<p>以上提到的都是在编译时把所有的可以用到的<code class="language-plaintext highlighter-rouge">.so</code>的存根都保存到<code class="language-plaintext highlighter-rouge">.interp</code>里,然后程序执行时自动装载<code class="language-plaintext highlighter-rouge">.so</code>的内容到虚拟地址空间<br />
同时Linux也提供了运行时动态的装载<code class="language-plaintext highlighter-rouge">.so</code>的机制<br />
该机制只有到程序运行到了加载<code class="language-plaintext highlighter-rouge">.so</code>的代码的时候才会加载<code class="language-plaintext highlighter-rouge">.so</code>到地址空间<br />
加载<code class="language-plaintext highlighter-rouge">.so</code>相关的函数有</p>

<ul>
  <li>
    <div class="language-c highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kt">void</span> <span class="o">*</span> <span class="nf">dlopen</span><span class="p">(</span><span class="k">const</span> <span class="kt">char</span> <span class="o">*</span> <span class="n">filename</span><span class="p">,</span> <span class="kt">int</span> <span class="n">flag</span><span class="p">);</span>
</code></pre></div>    </div>
  </li>
  <li>
    <div class="language-c highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kt">void</span> <span class="o">*</span> <span class="nf">dlsym</span><span class="p">(</span><span class="kt">void</span> <span class="o">*</span> <span class="n">handle</span><span class="p">,</span> <span class="kt">char</span> <span class="o">*</span> <span class="n">symbol</span><span class="p">);</span>
</code></pre></div>    </div>
  </li>
  <li>
    <div class="language-c highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kt">int</span> <span class="nf">dlclose</span><span class="p">(</span><span class="kt">void</span> <span class="o">*</span> <span class="n">handle</span><span class="p">);</span>
</code></pre></div>    </div>
  </li>
  <li>
    <div class="language-c highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">const</span> <span class="kt">char</span> <span class="o">*</span>    <span class="nf">dlerror</span><span class="p">(</span><span class="kt">void</span><span class="p">);</span>
</code></pre></div>    </div>
  </li>
</ul>

<p>那么为什么动态加载的时候不需要像链接时动态链接一样把存根信息保存到<code class="language-plaintext highlighter-rouge">.interp</code>呢?<br />
这是因为在动态加载<code class="language-plaintext highlighter-rouge">.so</code>的时候,加载返回指仅仅是一个<code class="language-plaintext highlighter-rouge">void*</code>指针,实际的调用函数需要自己定义<br />
例如定义一个函数指针类型,然后把动态加载的指针去强制类型转换<br />
由于这个过程根本不会涉及<code class="language-plaintext highlighter-rouge">PIC</code>代码的生成,因为所有的过程调用都是绝对地址的调用<br />
也就不需要像上述链接时动态链接一样依赖<code class="language-plaintext highlighter-rouge">GOT</code>,<code class="language-plaintext highlighter-rouge">PLT</code>等等结构,自然也就不需要<code class="language-plaintext highlighter-rouge">.interp</code>里的<code class="language-plaintext highlighter-rouge">.so</code>存根</p>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-10-18T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/10/15/misc-auto-hot-key.html">AutoHotKey</a></div><div class="next"><span>下篇</span><a href="/2020/10/20/apache-chainsaw.html">Apache Chainsaw</a></div></div></div>

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