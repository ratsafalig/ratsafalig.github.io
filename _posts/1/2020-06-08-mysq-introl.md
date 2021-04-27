---
title: MySQL Intro
date: 2020-06-08 00:00:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="MySQL Intro"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-06-08T08:00:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="MySQL Intro" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-08T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="MySQL Intro" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-08T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="MySQL Intro" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-06-08T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="_1">概念</h1>

<h2 id="_2">Mysql结构</h2>

<pre><code class="language-mermaid">graph TD;
    id1(客户端)
    id2(连接/线程处理)
    id3(查询缓存)
    id4(解析器)
    id5(优化器)
    id6(存储引擎)

    id1--&gt;id2
    id2--1.查找--&gt;id3
    id3--2.未找到--&gt;id2
    id2--3.解析--&gt;id4
    id4--4.优化--&gt;id5
    id5--5.查询--&gt;id6
    id4--6.写入--&gt;id3
</code></pre>

<h2 id="_3">锁的种类</h2>

<pre><code class="language-mermaid">graph TD;
    id1(乐观锁)
    id2(悲观锁)
    id3(读锁==共享锁)
    id4(写锁==排他锁)
    id5(表锁)
    id6(行锁)
    id7(MVCC)

    id1--&gt;id7
    id2--&gt;id3
    id2--&gt;id4
    id3--&gt;id5
    id3--&gt;id6
    id4--&gt;id5
    id4--&gt;id6
</code></pre>

<h2 id="_4">隔离级别</h2>

<pre><code class="language-mermaid">graph TD;
    id1(read-uncommitted)
    id2(read-committed)
    id3(repeatable-read)
    id4(serializable)

    id1--&gt;id2
    id2--&gt;id3
    id3--&gt;id4
</code></pre>

<h2 id="_5">MVCC</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>mvcc全称多版本并发控制.说是乐观锁,其实压根不是锁,是一种无阻塞的并发控制.

InnoDB的mvcc是通过在每行数据后面加两个隐藏的列,行的创建时间和行的过期时间,这个时间不是真实的时间,而是版本号.

例如,select操作一行语句的时候,会自动给这条select语句赋予一个版本号,查找的结果只查找过期时间小于或者等于该select语句版本号的结果
</code></pre></div></div>
<pre><code class="language-mermaid">graph TD;
    id0(语句启动,分配语句一个版本号)
    id1(select语句,查找过期时间小于等于当前版本的结果)
    id2(insert语句,插入的每一行数据都是当前insert语句的版本号)
    id3(delete语句,把要删除的语句的过期版本标记成当前语句的版本号)
    id4(update语句,插入一个新的语句,新语句的版本号是update版本号,旧的语句的过期版本号变成update语句版本号)
    id0--&gt;id1
    id0--&gt;id2
    id0--&gt;id3
    id0--&gt;id4
</code></pre>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>MVCC只在repeatable-read和read-committed隔离等级下进行,因为read-uncommitted总是读取新数据,而serializable对所有行加锁
</code></pre></div></div>

<h2 id="_6">引擎差异</h2>

<pre><code class="language-mermaid">graph TD;
    id1(事务)
    id2(聚簇索引)
    id3(行锁)
    id4(表锁)
    id5(全文索引)
    id6(压缩表)
    id7(外键)

    idb(MyISAM)
    ida(InnoDB)

    ida--&gt;id1
    ida--&gt;id2
    ida--&gt;id3
    ida--&gt;id4
    ida--&gt;id7

    idb--&gt;id4
    idb--&gt;id5
    idb--&gt;id6
</code></pre>
<h1 id="_7">优化</h1>

<h2 id="_8">数据类型</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>varchar(xxx) : 变长字符串,字符串最大长度为xxx,数据会保存一个数组长度的变量(如果MyISAM的定长表的时候,这个时候varchar会和char一样)

char(xxx) : 定长字符串,字符串长度为xxx

null : 不必要的情况下不要设置null,因为如果一个列可为null时候需要一个额外字节存储是否为null,并且索引也更难优化.可能导致定长索引变成变长索引

decimal : 因为float采用指数形式存储,数值越大偏差越大,decimal采用的是精准存储小数点和小数的形式

blob/text : 采用二进制存储的数据,如果数据过大,innodb会采用外部存储,只在列位置存一个指针,实际放在别的地方,text数据类型还存在字符集和排序规则,在进行排序的时候,需要指明排序的列的长度,因为Blob和text类型可能非常长,没办法整个列排序

enum : 实际列中存放的是索引值,然后根据索引值在文件的一个位置去寻找索引对应的字符串

set : enum只能选一个值,set可以选好几个
</code></pre></div></div>

<h2 id="_9">索引类型</h2>

<pre><code class="language-mermaid">graph TD;
    id1(B+Tree)
    id2(Hash)
    id3(全文索引)
    id4(左前匹配)
    id5(列前匹配)
    id6(范围匹配)
    id7(精确匹配)
    id8(只访问索引的查询优化...using_index)
    id9(相关性匹配)

    id1--&gt;id3
    id1--&gt;id4
    id1--&gt;id5
    id1--&gt;id6
    id1--&gt;id7
    id1--&gt;id8
    id2--&gt;id7
    id3--&gt;id9
</code></pre>

<h2 id="_10">特点</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>聚簇索引 : 相比MyISAM索引使用B+Tree进行建立,然后表的顺序不一定规则摆放,InnoDB直接将实际的表内的数据按B+Tree根据主键索引的规则摆放.这么做的好处首先就是减少磁盘IO次数.

坏处也很明显,维护一个聚簇索引的数据意味着经常要将底层的数据复制来复制去,同时索引查询比非聚簇索引的引擎慢,因为聚簇索引的引擎的索引的叶子节点存放的是主键的值,然后再根据主键的值去根据聚簇去查找.
</code></pre></div></div>

<h2 id="_11">优化设计</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>1. 缓存表 : 比如一个网站要统计实时消息数,通常做法可以是每次一个新消息来的时候都update一个数据并+1消息数,这样难免效率低下,
替代方案可以是每一个小时进行一次count(*),然后直接一个Select就可以得知消息数

2. 计数器表 : 假设一个表只有一个项目
</code></pre></div></div>
<div class="language-sql highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">create</span> <span class="k">table</span> <span class="n">a</span><span class="p">(</span>
    <span class="n">b</span> <span class="nb">int</span>
<span class="p">)</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>如果实时对这个表进行更新,比如进常需要执行
</code></pre></div></div>
<div class="language-sql highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">update</span> <span class="n">a</span> <span class="k">set</span> <span class="n">b</span> <span class="o">=</span> <span class="n">b</span> <span class="o">+</span> <span class="mi">1</span> <span class="k">where</span> <span class="n">b</span> <span class="o">=</span> <span class="n">xxx</span><span class="p">;</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>这个时候由于写入过程要对表加锁,会导致所有的更新都会被阻塞在这一行,造成效率非常低下,
这个时候可以采用一个新表替代
</code></pre></div></div>
<div class="language-sql highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">create</span> <span class="k">table</span> <span class="n">a</span><span class="p">(</span>
    <span class="n">b1</span> <span class="nb">int</span><span class="p">,</span>
    <span class="n">b2</span> <span class="nb">int</span><span class="p">,</span>
    <span class="n">b3</span> <span class="nb">int</span>
<span class="p">)</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>然后随机选择update b1 b2 b3中的一个,这个时候由于innodb的行锁不会锁整个表,就可以提供三个插槽给更新操作,避免一个插槽位置造成的阻塞
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>3. 切分查询 : 删除大部分数据时候,如果一次性删除的话,会造成锁住很多数据,所以这个时候为了提高并发性能,拆成多个子删除是可能的.通常一次性删除1W行是比较合适的数值

4. 分解关联查询 : 过多的关联查询可以分解成一个个的单查询,在应用层实现分解,这样做的好处可能有:
    1. 更好的应用数据库的缓存,因为一行一行的查询可能早已经被数据库缓存完了
    2. 减少冗余查询,在mysql里执行关联,同一部分的数据可能要被访问多次,所以应用层进行关联可能会减少查询量
    3. 分解查询后,减少了锁的数量,增加并发性能

5. 必要的时候加上limit,减少查询的消息数

6. 正确的索引 : 将选择性高的列放在前头,因为索引的作用可以达到左前匹配,所以如果选择性低的列在前,比如说一个列只有一个可能值,那么这个索引匹配了和没匹配一样,还是需要全表查
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-06-08T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/05/31/java-jta.html">JTA</a></div><div class="next"><span>下篇</span><a href="/2020/06/09/dubbo-architecture.html">Dubbo Architecture</a></div></div></div>

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