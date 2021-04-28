---
title: 汇编
date: 2020-08-10 00:00:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="汇编"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-08-10T08:00:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="汇编" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-10T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="汇编" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-10T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="汇编" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-08-10T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="_1">指令</h1>

<div class="language-cpp highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="err">加载有效地址</span><span class="o">:</span>
<span class="n">leal</span> <span class="o">%</span><span class="n">eax</span><span class="p">,</span> <span class="o">%</span><span class="n">ebx</span> <span class="c1">//movl的变形,例如leal 7(%eax, %ebx, 4), %ebx,设eax是x,ebx是y,则该指令把ebx填充成4y+x+7</span>

<span class="err">单目运算</span><span class="o">:</span>
<span class="n">inc</span> <span class="o">%</span><span class="n">eax</span> 
<span class="n">dec</span> <span class="o">%</span><span class="n">eax</span>
<span class="n">neg</span> <span class="o">%</span><span class="n">eax</span>
<span class="n">not</span> <span class="o">%</span><span class="n">eax</span>

<span class="err">双目运算</span><span class="o">:</span>
<span class="n">add</span> <span class="o">%</span><span class="n">eax</span><span class="p">,</span> <span class="o">%</span><span class="n">ebx</span>
<span class="n">sub</span> <span class="o">%</span><span class="n">eax</span><span class="p">,</span> <span class="o">%</span><span class="n">ebx</span>
<span class="n">imul</span> <span class="o">%</span><span class="n">eax</span><span class="p">,</span> <span class="o">%</span><span class="n">ebx</span>
<span class="n">xor</span> <span class="o">%</span><span class="n">eax</span><span class="p">,</span> <span class="o">%</span><span class="n">ebx</span>
<span class="n">or</span> <span class="o">%</span><span class="n">eax</span><span class="p">,</span> <span class="o">%</span><span class="n">ebx</span>
<span class="n">and</span> <span class="o">%</span><span class="n">eax</span><span class="p">,</span> <span class="o">%</span><span class="n">ebx</span>

<span class="err">位移</span><span class="o">:</span>
<span class="n">sal</span> <span class="n">k</span><span class="p">,</span> <span class="o">%</span><span class="n">eax</span> <span class="c1">//左移</span>
<span class="n">shl</span> <span class="n">k</span><span class="p">,</span> <span class="o">%</span><span class="n">eax</span> <span class="c1">//等同于sal</span>
<span class="n">sar</span> <span class="n">k</span><span class="p">,</span> <span class="o">%</span><span class="n">eax</span> <span class="c1">//算数右移,最高位填充符号位例如:1000&gt;&gt;1==1100</span>
<span class="n">shr</span> <span class="n">k</span><span class="p">,</span> <span class="o">%</span><span class="n">eax</span> <span class="c1">//逻辑右移,最高位填充0</span>

<span class="cm">/**
 * CPU维护了几个条件码用来实现条件跳转等操作:
 * CF:进位标识
 * ZF:零标识
 * SF:符号标识
 * OF:溢出标识
 */</span>
<span class="err">条件</span><span class="o">:</span>
<span class="n">cmp</span> <span class="o">%</span><span class="n">eax</span><span class="p">,</span> <span class="o">%</span><span class="n">ebx</span>
<span class="n">test</span> <span class="o">%</span><span class="n">eax</span><span class="p">,</span> <span class="o">%</span><span class="n">ebx</span>
<span class="n">setxx</span> <span class="o">%</span><span class="n">eax</span> <span class="c1">//根据xx的具体值,把当前条件码的状态设置到%eax</span>
<span class="n">jmp</span> <span class="n">label</span> <span class="c1">//无条件跳转</span>
<span class="n">jxx</span> <span class="n">label</span> <span class="c1">//根据具体的xx和条件码,选择性跳转</span>

<span class="err">过程相关</span><span class="o">:</span>
<span class="n">push</span> <span class="o">%</span><span class="n">eax</span>
<span class="n">pop</span> <span class="o">%</span><span class="n">eax</span>
<span class="n">call</span> <span class="n">label</span>
<span class="n">leave</span>
<span class="n">ret</span>
</code></pre></div></div>

<h1 id="_2">call</h1>

<div class="language-cpp highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="err">执行</span><span class="n">call</span><span class="err">前</span>
    <span class="o">%</span><span class="n">eip</span> <span class="o">:</span> <span class="mh">0x080483dc</span>
    <span class="o">%</span><span class="n">esp</span> <span class="o">:</span> <span class="mh">0xff9bc960</span>
<span class="err">执行</span><span class="n">call</span><span class="err">后</span>
    <span class="o">%</span><span class="n">eip</span> <span class="o">:</span> <span class="mh">0x08048394</span> <span class="c1">//跳转目的地地址</span>
    <span class="o">%</span><span class="n">esp</span> <span class="o">:</span> <span class="mh">0xff9bc95c</span>  
    <span class="p">(</span><span class="o">%</span><span class="n">esp</span><span class="p">)</span> <span class="o">:</span> <span class="mh">0x080483e1</span> <span class="c1">//执行call前的后一条指令 </span>
<span class="err">执行</span><span class="n">ret</span><span class="err">后</span>
    <span class="o">%</span><span class="n">eip</span> <span class="o">:</span> <span class="mh">0x080483e1</span> <span class="c1">//返回原执行点的下一条</span>
    <span class="o">%</span><span class="n">esp</span> <span class="o">:</span> <span class="mh">0xff9bc960</span> <span class="c1">//返回地址释放</span>
</code></pre></div></div>

<h1 id="_3">leave</h1>

<div class="language-cpp highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">leave</span><span class="err">用来执行调用</span><span class="n">ret</span><span class="err">之前的准备工作</span><span class="p">,</span><span class="err">有时候编译器会采用一个或者多个</span><span class="n">pop</span><span class="err">来代替</span><span class="n">leave</span>
<span class="n">leave</span> <span class="o">==</span> <span class="n">movl</span> <span class="o">%</span><span class="n">ebp</span><span class="p">,</span><span class="o">%</span><span class="n">esp</span> <span class="c1">//把帧起点设为栈顶</span>
         <span class="n">popl</span> <span class="o">%</span><span class="n">ebp</span> <span class="c1">//把上一个帧的地址放入ebp</span>
</code></pre></div></div>

<h1 id="_4">寄存器使用惯例</h1>

<div class="language-cpp highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="err">调用者保存寄存器</span><span class="p">(</span><span class="o">%</span><span class="n">eax</span><span class="p">,</span><span class="o">%</span><span class="n">edx</span><span class="p">,</span><span class="o">%</span><span class="n">ecx</span><span class="p">)</span> <span class="o">==</span> <span class="err">调用者负责保管数据</span><span class="p">,</span><span class="err">在被调用者覆盖之前自己先存起来</span>
<span class="err">被调用者保存</span><span class="p">(</span><span class="o">%</span><span class="n">ebx</span><span class="p">,</span><span class="o">%</span><span class="n">esi</span><span class="p">,</span><span class="o">%</span><span class="n">edi</span><span class="p">)</span> <span class="o">==</span> <span class="err">被调用者覆盖这些数据之前</span><span class="p">,</span><span class="err">先存到栈上</span><span class="p">,</span><span class="err">要返回的时候恢复到寄存器中还给调用者</span>
</code></pre></div></div>

<h1 id="_5">缓冲区溢出攻击</h1>

<div class="language-cpp highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="err">来看一段过程调用的代码</span><span class="o">:</span>
    <span class="n">caller</span><span class="o">:</span>
        <span class="n">pushl</span> <span class="o">%</span><span class="n">ebp</span>
        <span class="n">movl</span> <span class="o">%</span><span class="n">esp</span><span class="p">,</span><span class="o">%</span><span class="n">ebp</span>
        <span class="n">subl</span> <span class="err">$</span><span class="mi">24</span><span class="p">,</span><span class="o">%</span><span class="n">esp</span>
        <span class="n">movl</span> <span class="err">$</span><span class="mi">534</span><span class="p">,</span><span class="o">-</span><span class="mi">4</span><span class="p">(</span><span class="o">%</span><span class="n">ebp</span><span class="p">)</span>
        <span class="n">movl</span> <span class="err">$</span><span class="mi">1057</span><span class="p">,</span><span class="o">-</span><span class="mi">8</span><span class="p">(</span><span class="o">%</span><span class="n">ebp</span><span class="p">)</span>
        <span class="n">leal</span> <span class="o">-</span><span class="mi">8</span><span class="p">(</span><span class="o">%</span><span class="n">ebp</span><span class="p">),</span><span class="o">%</span><span class="n">eax</span>
        <span class="n">movl</span> <span class="o">%</span><span class="n">eax</span><span class="p">,</span><span class="mi">4</span><span class="p">(</span><span class="o">%</span><span class="n">esp</span><span class="p">)</span>
        <span class="n">leal</span> <span class="o">-</span><span class="mi">4</span><span class="p">(</span><span class="o">%</span><span class="n">ebp</span><span class="p">),</span><span class="o">%</span><span class="n">eax</span>
        <span class="n">movl</span> <span class="n">swap_add</span>
        <span class="n">movl</span> <span class="o">-</span><span class="mi">4</span><span class="p">(</span><span class="o">%</span><span class="n">ebp</span><span class="p">),</span><span class="o">%</span><span class="n">edx</span>
        <span class="n">subl</span> <span class="o">-</span><span class="mi">8</span><span class="p">(</span><span class="o">%</span><span class="n">ebp</span><span class="p">),</span><span class="o">%</span><span class="n">edx</span>
        <span class="n">imull</span> <span class="o">%</span><span class="n">edx</span><span class="p">,</span><span class="o">%</span><span class="n">eax</span>
        <span class="n">leave</span>
        <span class="n">ret</span>
    <span class="n">swap_add</span><span class="o">:</span>
        <span class="n">pushl</span> <span class="o">%</span><span class="n">ebp</span>
        <span class="n">movl</span> <span class="o">%</span><span class="n">esp</span><span class="p">,</span><span class="o">%</span><span class="n">ebp</span>
        <span class="n">pushl</span> <span class="o">%</span><span class="n">edx</span> <span class="c1">//被调用者保存寄存器,使用前先保存到栈上,返回前复原</span>
        <span class="n">movl</span> <span class="mi">8</span><span class="p">(</span><span class="o">%</span><span class="n">ebp</span><span class="p">),</span><span class="o">%</span><span class="n">edx</span> <span class="c1">//Get xp</span>
        <span class="n">movl</span> <span class="mi">12</span><span class="p">(</span><span class="o">%</span><span class="n">ebp</span><span class="p">),</span><span class="o">%</span><span class="n">ecx</span> <span class="c1">//Get yp</span>
        <span class="n">movl</span> <span class="p">(</span><span class="o">%</span><span class="n">edx</span><span class="p">),</span><span class="o">%</span><span class="n">ebx</span> <span class="c1">//Get x</span>
        <span class="n">movl</span> <span class="p">(</span><span class="o">%</span><span class="n">ecx</span><span class="p">),</span><span class="o">%</span><span class="n">eax</span> <span class="c1">//Get y</span>
        <span class="n">movl</span> <span class="o">%</span><span class="n">eax</span><span class="p">,(</span><span class="o">%</span><span class="n">edx</span><span class="p">)</span> <span class="c1">//Store y at yp</span>
        <span class="n">movl</span> <span class="o">%</span><span class="n">ebx</span><span class="p">,(</span><span class="o">%</span><span class="n">ecx</span><span class="p">)</span> <span class="c1">//Store x at xp</span>
        <span class="n">addl</span> <span class="o">%</span><span class="n">ebx</span><span class="p">,</span><span class="o">%</span><span class="n">eax</span> <span class="c1">//Return value = x + y,加法结果存放到默认寄存器</span>
        <span class="n">popl</span> <span class="o">%</span><span class="n">ebx</span> <span class="c1">//复原寄存器 </span>
        <span class="n">popl</span> <span class="o">%</span><span class="n">ebp</span> 
        <span class="n">ret</span>
<span class="err">可以观察到</span><span class="n">echo</span><span class="err">提前在栈上分配数组的长度</span><span class="p">,</span><span class="err">然后将数组的头指针地址通过参数形式传递给</span><span class="n">gets</span><span class="p">(</span><span class="kt">char</span><span class="o">*</span><span class="p">),</span><span class="err">紧接着把返回地址压入栈</span><span class="p">,</span><span class="err">进行</span><span class="n">gets</span><span class="p">(</span><span class="kt">char</span><span class="o">*</span><span class="p">)</span><span class="err">调用</span>
<span class="err">如果</span><span class="n">gets</span><span class="p">(</span><span class="kt">char</span><span class="o">*</span><span class="p">)</span><span class="err">函数对数组的填写超过分配的长度</span>
<span class="err">那么有可能覆盖掉数组后面的返回地址</span><span class="p">,</span><span class="err">从而达到执行用户无法预测的代码的目的</span>
<span class="err">针对缓冲区溢出的防御</span><span class="o">:</span>
<span class="mf">1.</span> <span class="err">栈随机化</span><span class="o">:</span>
<span class="err">为了实施溢出攻击</span><span class="p">,</span><span class="err">攻击者需要覆盖返回地址为自己的目标代码地址</span><span class="p">,</span><span class="err">也就是要知道自己要执行的代码在什么位置</span>
<span class="err">栈随机化的思想就是每次执行代码</span><span class="p">,</span><span class="err">程序所在的虚拟地址都不同</span><span class="p">,</span><span class="err">这样攻击者无法判断攻击代码的位置</span><span class="p">,</span><span class="err">也就无法覆盖为代码地址</span>
<span class="err">但是</span><span class="p">,</span><span class="err">攻击者可以通过在攻击代码前插入大量'雪橇'代码片</span><span class="p">,</span><span class="err">这些代码片唯一干的就是传递到下一个地址的指令</span><span class="p">,</span><span class="err">这样可以达到地址空间中很大一部分被雪橇覆盖</span>
<span class="err">也就是说这样覆盖掉缓冲区后面的地址随便写一个就有很大可能命中雪橇这片区域</span><span class="p">,</span><span class="err">从而不断滑向真正的攻击代码</span>
<span class="mf">2.</span> <span class="err">栈破坏检测</span><span class="o">:</span>
<span class="err">在缓冲区分配之后</span><span class="p">,</span><span class="err">返回地址之前设置一个哨兵值</span><span class="p">,</span><span class="err">这个值和磁盘或者其他储存器的一个验证值相等</span><span class="p">,</span><span class="err">修改编译结果</span><span class="p">,</span><span class="err">把编译结果改成返回之前比对哨兵值和验证值是否相等</span><span class="p">,</span><span class="err">如果不相等</span><span class="p">,</span><span class="err">说明出现攻击者</span>
<span class="mf">3.</span> <span class="err">限制可执行代码区域</span><span class="o">:</span>
<span class="err">攻击的本质是插入可执行代码</span><span class="p">,</span><span class="err">如果限制只有编译器产生的代码是可执行的就可以避免攻击</span><span class="p">,</span><span class="err">因为虚拟内存是以页组织的</span><span class="p">,</span><span class="err">只要把编译器生成的页设置为可执行</span><span class="p">,</span><span class="err">其他页不能执行就可以</span><span class="p">,</span><span class="err">但是这会带来严重性能损失</span>
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
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/07/20/tomcat-connector.html">Tomcat Connector调优</a></div><div class="next"><span>下篇</span><a href="/2020/08/10/sys-linking.html">链接过程</a></div></div></div>

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