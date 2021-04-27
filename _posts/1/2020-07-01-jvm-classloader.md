---
title: ClassLoader
date: 2020-07-01 00:00:00 Z
tags:
- Java
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="ClassLoader"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00">
    <meta itemprop="keywords" content="Java"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="ClassLoader" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="ClassLoader" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="ClassLoader" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-07-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="_0">参考地址</h1>

<p><a href="https://www.cnblogs.com/xrq730/p/4847337.html">参考地址1</a></p>

<h1 id="_1">实例代码</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nl">JDK的ApplicationClassLoader:</span>

<span class="kd">protected</span> <span class="kd">synchronized</span> <span class="nc">Class</span><span class="o">&lt;?&gt;</span> <span class="n">loadClass</span><span class="o">(</span><span class="nc">String</span> <span class="n">name</span><span class="o">,</span> <span class="kt">boolean</span> <span class="n">resolve</span><span class="o">)</span>
    <span class="kd">throws</span> <span class="nc">ClassNotFoundException</span>
    <span class="o">{</span>
        <span class="c1">// First, check if the class has already been loaded</span>
        <span class="nc">Class</span> <span class="n">c</span> <span class="o">=</span> <span class="n">findLoadedClass</span><span class="o">(</span><span class="n">name</span><span class="o">);</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">c</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
            <span class="k">try</span> <span class="o">{</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">parent</span> <span class="o">!=</span> <span class="kc">null</span><span class="o">)</span> <span class="o">{</span>
                <span class="n">c</span> <span class="o">=</span> <span class="n">parent</span><span class="o">.</span><span class="na">loadClass</span><span class="o">(</span><span class="n">name</span><span class="o">,</span> <span class="kc">false</span><span class="o">);</span>
            <span class="o">}</span> <span class="k">else</span> <span class="o">{</span>
                <span class="n">c</span> <span class="o">=</span> <span class="n">findBootstrapClass0</span><span class="o">(</span><span class="n">name</span><span class="o">);</span>
            <span class="o">}</span>
            <span class="o">}</span> <span class="k">catch</span> <span class="o">(</span><span class="nc">ClassNotFoundException</span> <span class="n">e</span><span class="o">)</span> <span class="o">{</span>
                <span class="c1">// If still not found, then invoke findClass in order</span>
                <span class="c1">// to find the class.</span>
                <span class="n">c</span> <span class="o">=</span> <span class="n">findClass</span><span class="o">(</span><span class="n">name</span><span class="o">);</span>
            <span class="o">}</span>
        <span class="o">}</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">resolve</span><span class="o">)</span> <span class="o">{</span>
            <span class="n">resolveClass</span><span class="o">(</span><span class="n">c</span><span class="o">);</span>
        <span class="o">}</span>
        <span class="k">return</span> <span class="n">c</span><span class="o">;</span>
    <span class="o">}</span>
</code></pre></div></div>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>双亲委派模型基本过程:
1. 是否被加载
2. 如果没有,从父类加载
3. 父类加载不了,自己加载

打破双亲委派模型的方法
1. 重写loadClass方法
不想打破双亲委派模型的方法
1. 重写findClass
</code></pre></div></div>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nl">自定义加载器代码:</span>

<span class="kd">public</span> <span class="kd">class</span> <span class="nc">MyClassLoader</span> <span class="kd">extends</span> <span class="nc">ClassLoader</span>
<span class="o">{</span>
    <span class="kd">public</span> <span class="nf">MyClassLoader</span><span class="o">()</span>
    <span class="o">{</span>        
    <span class="o">}</span>
    
    <span class="kd">public</span> <span class="nf">MyClassLoader</span><span class="o">(</span><span class="nc">ClassLoader</span> <span class="n">parent</span><span class="o">)</span>
    <span class="o">{</span>
        <span class="kd">super</span><span class="o">(</span><span class="n">parent</span><span class="o">);</span>
    <span class="o">}</span>
    
    <span class="kd">protected</span> <span class="nc">Class</span><span class="o">&lt;?&gt;</span> <span class="n">findClass</span><span class="o">(</span><span class="nc">String</span> <span class="n">name</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">ClassNotFoundException</span>
    <span class="o">{</span>
        <span class="nc">File</span> <span class="n">file</span> <span class="o">=</span> <span class="n">getClassFile</span><span class="o">(</span><span class="n">name</span><span class="o">);</span>
        <span class="k">try</span>
        <span class="o">{</span>
            <span class="kt">byte</span><span class="o">[]</span> <span class="n">bytes</span> <span class="o">=</span> <span class="n">getClassBytes</span><span class="o">(</span><span class="n">file</span><span class="o">);</span>
            <span class="nc">Class</span><span class="o">&lt;?&gt;</span> <span class="n">c</span> <span class="o">=</span> <span class="k">this</span><span class="o">.</span><span class="na">defineClass</span><span class="o">(</span><span class="n">name</span><span class="o">,</span> <span class="n">bytes</span><span class="o">,</span> <span class="mi">0</span><span class="o">,</span> <span class="n">bytes</span><span class="o">.</span><span class="na">length</span><span class="o">);</span>
            <span class="k">return</span> <span class="n">c</span><span class="o">;</span>
        <span class="o">}</span> 
        <span class="k">catch</span> <span class="o">(</span><span class="nc">Exception</span> <span class="n">e</span><span class="o">)</span>
        <span class="o">{</span>
            <span class="n">e</span><span class="o">.</span><span class="na">printStackTrace</span><span class="o">();</span>
        <span class="o">}</span>
        
        <span class="k">return</span> <span class="kd">super</span><span class="o">.</span><span class="na">findClass</span><span class="o">(</span><span class="n">name</span><span class="o">);</span>
    <span class="o">}</span>
    
    <span class="kd">private</span> <span class="nc">File</span> <span class="nf">getClassFile</span><span class="o">(</span><span class="nc">String</span> <span class="n">name</span><span class="o">)</span>
    <span class="o">{</span>
        <span class="nc">File</span> <span class="n">file</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">File</span><span class="o">(</span><span class="s">"D:/Person.class"</span><span class="o">);</span>
        <span class="k">return</span> <span class="n">file</span><span class="o">;</span>
    <span class="o">}</span>
    
    <span class="kd">private</span> <span class="kt">byte</span><span class="o">[]</span> <span class="nf">getClassBytes</span><span class="o">(</span><span class="nc">File</span> <span class="n">file</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">Exception</span>
    <span class="o">{</span>
        <span class="c1">// 这里要读入.class的字节，因此要使用字节流</span>
        <span class="nc">FileInputStream</span> <span class="n">fis</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">FileInputStream</span><span class="o">(</span><span class="n">file</span><span class="o">);</span>
        <span class="nc">FileChannel</span> <span class="n">fc</span> <span class="o">=</span> <span class="n">fis</span><span class="o">.</span><span class="na">getChannel</span><span class="o">();</span>
        <span class="nc">ByteArrayOutputStream</span> <span class="n">baos</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">ByteArrayOutputStream</span><span class="o">();</span>
        <span class="nc">WritableByteChannel</span> <span class="n">wbc</span> <span class="o">=</span> <span class="nc">Channels</span><span class="o">.</span><span class="na">newChannel</span><span class="o">(</span><span class="n">baos</span><span class="o">);</span>
        <span class="nc">ByteBuffer</span> <span class="n">by</span> <span class="o">=</span> <span class="nc">ByteBuffer</span><span class="o">.</span><span class="na">allocate</span><span class="o">(</span><span class="mi">1024</span><span class="o">);</span>                                                                                
        <span class="k">while</span> <span class="o">(</span><span class="kc">true</span><span class="o">)</span>
        <span class="o">{</span>
            <span class="kt">int</span> <span class="n">i</span> <span class="o">=</span> <span class="n">fc</span><span class="o">.</span><span class="na">read</span><span class="o">(</span><span class="n">by</span><span class="o">);</span>
            <span class="k">if</span> <span class="o">(</span><span class="n">i</span> <span class="o">==</span> <span class="mi">0</span> <span class="o">||</span> <span class="n">i</span> <span class="o">==</span> <span class="o">-</span><span class="mi">1</span><span class="o">)</span>
                <span class="k">break</span><span class="o">;</span>
            <span class="n">by</span><span class="o">.</span><span class="na">flip</span><span class="o">();</span>
            <span class="n">wbc</span><span class="o">.</span><span class="na">write</span><span class="o">(</span><span class="n">by</span><span class="o">);</span>
            <span class="n">by</span><span class="o">.</span><span class="na">clear</span><span class="o">();</span>
        <span class="o">}</span>        
        <span class="n">fis</span><span class="o">.</span><span class="na">close</span><span class="o">();</span>        
        <span class="k">return</span> <span class="n">baos</span><span class="o">.</span><span class="na">toByteArray</span><span class="o">();</span>
    <span class="o">}</span>
<span class="o">}</span>

<span class="kd">public</span> <span class="kd">class</span> <span class="nc">TestMyClassLoader</span>
<span class="o">{</span>
    <span class="kd">public</span> <span class="kd">static</span> <span class="kt">void</span> <span class="nf">main</span><span class="o">(</span><span class="nc">String</span><span class="o">[]</span> <span class="n">args</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">Exception</span>
    <span class="o">{</span>
        <span class="nc">MyClassLoader</span> <span class="n">mcl</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">MyClassLoader</span><span class="o">();</span>
        <span class="nc">Class</span><span class="o">&lt;?&gt;</span> <span class="n">c1</span> <span class="o">=</span> <span class="nc">Class</span><span class="o">.</span><span class="na">forName</span><span class="o">(</span><span class="s">"com.xrq.classloader.Person"</span><span class="o">,</span> <span class="kc">true</span><span class="o">,</span> <span class="n">mcl</span><span class="o">);</span>
        <span class="nc">Object</span> <span class="n">obj</span> <span class="o">=</span> <span class="n">c1</span><span class="o">.</span><span class="na">newInstance</span><span class="o">();</span>
        <span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">.</span><span class="na">println</span><span class="o">(</span><span class="n">obj</span><span class="o">);</span>
        <span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">.</span><span class="na">println</span><span class="o">(</span><span class="n">obj</span><span class="o">.</span><span class="na">getClass</span><span class="o">().</span><span class="na">getClassLoader</span><span class="o">());</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<h1 id="_3">类生命周期</h1>

<p><img src="/assets/1/jvm/classloader1.jpg" alt="类生命周期" /></p>

<h1 id="_4">时机</h1>

<h2 id="_5">什么时候类加载</h2>

<p>一般就是引用一个类,解符号引用解析不到的时候,就会触发一个类加载过程</p>

<h2 id="_6">加载过程</h2>

<h3 id="_7">加载</h3>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>1. 通过一个类的全限定名来获取定义此类的二进制字节流。
2. 将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构。
3. 在内存中生成一个代表这个类的java.lang.Class对象，作为方法区这个类的各种数据
的访问入口。
</code></pre></div></div>

<h3 id="_8">验证</h3>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>1. 文件格式验证
2. 元数据验证(是否有父类,是否继承了不该继承的final类...)
3. 字节码验证(保证跳转指令不会跳转到方法体以外的部分...)
4. 符号引用验证(是否可以找到指定的类)
</code></pre></div></div>

<h3 id="_9">初始化</h3>

<h2 id="_10">什么时候初始化</h2>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>1. &lt;a style="color:green"&gt;**遇到new,getstatic,putstatic,invokestatic指令的时候,如果类没有进行过初始化**
2. **java.lang.reflect进行反射调用的时候,如果没有进行初始化**
3. **初始化一个类的时候,如果它的父类没有初始化,则先初始化父类**&lt;/a&gt;
4. 当虚拟机启动时，用户需要指定一个要执行的主类（包含main（）方法的那个
类），虚拟机会先初始化这个主类
5. 当使用JDK 1.7的动态语言支持时，如果一个java.lang.invoke.MethodHandle实例最后的解析结果REF_getStatic、 REF_putStatic、 REF_invokeStatic的方法句柄，并且这个方法句柄
所对应的类没有进行过初始化，则需要先触发其初始化。
</code></pre></div></div>

<h2 id="_11">过程</h2>

<p><img src="/assets/1/jvm/classloader2.jpg" alt="classloader2" /></p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>1. 首先jvm加载bootstrap-classloader
2. 读取源文件准备开始执行
3. 发现缺少platform-specific-jar
4. 委托给extension-classloader加载ext/lib下的jar
5. 发现缺少应用的各自类
6. application-classloader开始加载
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-07-01T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/07/01/java-collection.html">Java Collection</a></div><div class="next"><span>下篇</span><a href="/2020/07/01/jvm-concurrent.html">JVM 高效并发</a></div></div></div>

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