---
title: 链接过程
date: 2020-08-10 00:00:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="链接过程"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-08-10T08:00:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="链接过程" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-10T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="链接过程" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-10T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="链接过程" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-10T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="_1_0">文件结构</h1>

<div class="language-cpp highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="err">可重定位目标文件的结构如下</span><span class="o">:</span>
<span class="p">...</span>
<span class="p">.</span><span class="n">text</span>
<span class="p">.</span><span class="n">rodata</span>
<span class="p">.</span><span class="n">data</span>
<span class="p">.</span><span class="n">bss</span>
<span class="p">.</span><span class="n">symtab</span>
<span class="p">.</span><span class="n">rel</span><span class="p">.</span><span class="n">text</span>
<span class="p">.</span><span class="n">rel</span><span class="p">.</span><span class="n">data</span>
<span class="p">...</span>
<span class="p">.</span><span class="n">strtab</span>
<span class="p">...</span>

<span class="err">其中</span><span class="p">.</span><span class="n">text</span><span class="err">存放代码</span><span class="p">,.</span><span class="n">data</span><span class="err">和</span><span class="p">.</span><span class="n">bss</span><span class="err">存放全局变量</span><span class="p">,</span>
<span class="err">所有的字符量</span><span class="p">(</span><span class="err">函数名</span><span class="p">,</span><span class="err">变量名</span><span class="p">),</span><span class="err">存放在</span><span class="n">strtab</span><span class="err">里</span><span class="p">,</span>
<span class="p">.</span><span class="n">symtab</span><span class="err">存放符号表</span><span class="o">:</span>
<span class="k">typedef</span> <span class="k">struct</span><span class="p">{</span>
        <span class="kt">int</span> <span class="n">name</span><span class="p">;</span>
        <span class="kt">int</span> <span class="n">value</span><span class="p">;</span>
        <span class="kt">int</span> <span class="n">size</span><span class="p">;</span>
        <span class="kt">char</span> <span class="n">type</span><span class="o">:</span><span class="mi">4</span><span class="p">,</span>
             <span class="nl">binding:</span><span class="mi">4</span><span class="p">;</span>
        <span class="kt">char</span> <span class="n">reserved</span><span class="p">;</span>
        <span class="kt">char</span> <span class="n">section</span><span class="p">;</span>
<span class="p">}</span><span class="n">Elf_Symbol</span><span class="p">;</span>
<span class="p">.</span><span class="n">rel</span><span class="p">.</span><span class="n">text</span><span class="err">和</span><span class="p">.</span><span class="n">rel</span><span class="p">.</span><span class="n">data</span><span class="err">存放重定位条目</span><span class="p">,</span><span class="err">所谓重定位条目就是在解析完文件之后没有在当前文件发现的符号都会在</span><span class="p">.</span><span class="n">rel</span><span class="p">.</span><span class="n">xxx</span><span class="err">里创建一个重定位条目</span><span class="o">:</span>
<span class="k">typedef</span> <span class="k">struct</span><span class="p">{</span>
        <span class="kt">int</span> <span class="n">offset</span><span class="p">;</span>
        <span class="kt">int</span> <span class="n">symble</span><span class="o">:</span><span class="mi">24</span><span class="p">,</span>
            <span class="nl">type:</span><span class="mi">8</span><span class="p">;</span>
<span class="p">}</span><span class="n">Elf32_Ref</span><span class="p">;</span>
</code></pre></div></div>

<h1 id="_1">链接</h1>

<div class="language-cpp highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="err">从</span><span class="p">.</span><span class="n">c</span><span class="err">文件到最后的可执行文件</span><span class="p">,</span><span class="err">一共经历几个过程</span><span class="o">:</span>
<span class="p">.</span><span class="n">c</span><span class="o">--&gt;</span><span class="p">.</span><span class="n">i</span> <span class="c1">//预处理</span>
<span class="p">.</span><span class="n">i</span><span class="o">--&gt;</span><span class="p">.</span><span class="n">s</span> <span class="c1">//转汇编</span>
<span class="p">.</span><span class="n">s</span><span class="o">--&gt;</span><span class="p">.</span><span class="n">o</span> <span class="c1">//可重定位目标文件</span>
<span class="err">多个</span><span class="p">.</span><span class="n">o</span><span class="err">通过链接器最终链接成可执行文件</span><span class="p">.</span>

<span class="err">有时候一个</span><span class="p">.</span><span class="n">o</span><span class="err">文件包含了在其他文件里定义的函数</span><span class="p">(</span><span class="err">例如</span><span class="n">printf</span><span class="p">),</span><span class="err">这个时候就要通过链接器链接包含</span><span class="n">printf</span><span class="err">函数的文件</span><span class="p">,</span>
<span class="err">而链接的方式有三种</span><span class="o">:</span>
<span class="err">编译时链接</span>
<span class="err">加载时链接</span>
<span class="err">运行时链接</span>

<span class="err">所有的链接方式都要执行两个阶段</span>
<span class="mf">1.</span> <span class="err">符号解析</span>
<span class="mf">2.</span> <span class="err">重定位</span>

<span class="err">所谓符号解析说起来就是把所有的未识别的符号都放在</span><span class="p">.</span><span class="n">rel</span><span class="p">.</span><span class="n">text</span><span class="err">和</span><span class="p">.</span><span class="n">rel</span><span class="p">.</span><span class="n">data</span><span class="err">中</span><span class="p">.</span>
<span class="err">然后再下一个</span><span class="p">.</span><span class="n">o</span><span class="err">文件里去寻找符号</span><span class="p">.</span>
<span class="err">所谓重定位就是把当前</span><span class="p">.</span><span class="n">o</span><span class="err">文件里对未识别符号的</span><span class="n">call</span><span class="err">操作绑定到实际的运行时地址</span>
<span class="p">(</span><span class="err">因为链接器在整合过程中会为把所有的相关文件的</span><span class="p">.</span><span class="n">data</span><span class="err">合并成一个节</span><span class="p">,</span><span class="err">也意味着所有的符号都被赋予了一个运行时的地址</span><span class="p">)</span>

<span class="err">现在想象一个文件需要</span><span class="n">C</span><span class="err">语言某个标准库函数</span><span class="p">,</span><span class="err">最原始的做法是把所有的</span><span class="n">C</span><span class="err">语言函数封装成一个</span><span class="p">.</span><span class="n">o</span><span class="err">然后去链接这个</span><span class="p">.</span><span class="n">o</span><span class="p">,</span>
<span class="err">但是如果只需要一个</span><span class="n">printf</span><span class="p">,</span><span class="err">链接一整个</span><span class="p">.</span><span class="n">o</span><span class="err">未免太狠</span><span class="p">,</span><span class="err">所以提供了一种</span><span class="p">.</span><span class="n">a</span><span class="err">库的机制</span><span class="p">(</span><span class="err">也就是</span><span class="p">.</span><span class="n">lib</span><span class="p">),</span><span class="err">这个时候进行链接的时候只会从</span><span class="p">.</span><span class="n">a</span><span class="err">里取出需要的那部分函数</span><span class="p">.</span>

<span class="err">接下来说三种链接的区别</span>
<span class="mf">1.</span><span class="err">静态链接最简单</span><span class="p">,</span><span class="err">直接暴力在编译阶段串在一起</span>
<span class="mf">2.</span><span class="err">加载时链接类似</span><span class="n">windows</span><span class="err">上的</span><span class="p">.</span><span class="n">dll</span><span class="o">+</span><span class="p">.</span><span class="n">lib</span><span class="err">链接</span><span class="p">,</span><span class="err">但是</span><span class="n">linux</span><span class="err">上又有不同</span><span class="p">,</span><span class="n">linux</span><span class="err">的共享库以</span><span class="p">.</span><span class="n">so</span><span class="err">结尾</span><span class="p">,</span><span class="err">链接的时候链接器会把</span><span class="p">.</span><span class="n">so</span><span class="err">的符号变量复制一部分存到自己内部</span><span class="p">,</span><span class="err">然后把动态链接器的信息存到</span><span class="p">.</span><span class="n">o</span><span class="err">的</span><span class="p">.</span><span class="n">interp</span><span class="err">节里</span><span class="p">,</span>
<span class="err">然后执行的时候根据</span><span class="p">.</span><span class="n">interp</span><span class="err">找到动态链接器</span><span class="p">,</span><span class="err">再根据动态链接器寻找符号表</span><span class="p">,</span><span class="err">加载动态库</span>
<span class="mf">3.</span><span class="err">运行时链接和加载时链接的不同是运行时链接只在代码显示的执行加载系统调用的时候加载动态库</span>

</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-08-10T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/08/10/sys-assembler.html">汇编</a></div><div class="next"><span>下篇</span><a href="/2020/08/20/sys-dead-lock.html">死锁</a></div></div></div>

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