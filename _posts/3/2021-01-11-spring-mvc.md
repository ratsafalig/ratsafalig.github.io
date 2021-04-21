---
title: SpringMvc
date: 2021-01-11 00:00:00 Z
tags:
- Java
- Spring
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="SpringMvc"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2021-01-11T08:00:00+08:00">
    <meta itemprop="keywords" content="Java,Spring"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="SpringMvc" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-01-11T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java,Spring" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="servlet">Servlet</h1>

<p><a href="https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-servlet">官方文档-DispatcherServlet</a></p>

<p>Servlet3.0会在应用启动时加载SPI: <code class="language-plaintext highlighter-rouge">/META-INF/services/javax.servlet.ServletContainerInitializer</code><br />
并且调用其的<code class="language-plaintext highlighter-rouge">onStartup</code>:</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">interface</span> <span class="nc">ServletContainerInitializer</span> <span class="o">{</span>
    <span class="kt">void</span> <span class="nf">onStartup</span><span class="o">(</span><span class="nc">Set</span><span class="o">&lt;</span><span class="nc">Class</span><span class="o">&lt;?&gt;&gt;</span> <span class="n">c</span><span class="o">,</span> <span class="nc">ServletContext</span> <span class="n">ctx</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">ServletException</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>

<p>以下例子可以用来在Spring(非Boot)环境下配置SpringMvc:</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">class</span> <span class="nc">MyWebApplicationInitializer</span> <span class="kd">implements</span> <span class="nc">WebApplicationInitializer</span> <span class="o">{</span>
    <span class="nd">@Override</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">onStartup</span><span class="o">(</span><span class="nc">ServletContext</span> <span class="n">servletContext</span><span class="o">)</span> <span class="o">{</span>
        <span class="c1">// Load Spring web application configuration</span>
        <span class="nc">AnnotationConfigWebApplicationContext</span> <span class="n">context</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">AnnotationConfigWebApplicationContext</span><span class="o">();</span>
        <span class="n">context</span><span class="o">.</span><span class="na">register</span><span class="o">(</span><span class="nc">AppConfig</span><span class="o">.</span><span class="na">class</span><span class="o">);</span>
        <span class="c1">// Create and register the DispatcherServlet</span>
        <span class="nc">DispatcherServlet</span> <span class="n">servlet</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">DispatcherServlet</span><span class="o">(</span><span class="n">context</span><span class="o">);</span>
        <span class="nc">ServletRegistration</span><span class="o">.</span><span class="na">Dynamic</span> <span class="n">registration</span> <span class="o">=</span> <span class="n">servletContext</span><span class="o">.</span><span class="na">addServlet</span><span class="o">(</span><span class="s">"app"</span><span class="o">,</span> <span class="n">servlet</span><span class="o">);</span>
        <span class="n">registration</span><span class="o">.</span><span class="na">setLoadOnStartup</span><span class="o">(</span><span class="mi">1</span><span class="o">);</span>
        <span class="n">registration</span><span class="o">.</span><span class="na">addMapping</span><span class="o">(</span><span class="s">"/app/*"</span><span class="o">);</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<div class="language-xml highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nt">&lt;web-app&gt;</span>
    <span class="nt">&lt;listener&gt;</span>
        <span class="nt">&lt;listener-class&gt;</span>org.springframework.web.context.ContextLoaderListener<span class="nt">&lt;/listener-class&gt;</span>
    <span class="nt">&lt;/listener&gt;</span>
    <span class="nt">&lt;context-param&gt;</span>
        <span class="nt">&lt;param-name&gt;</span>contextConfigLocation<span class="nt">&lt;/param-name&gt;</span>
        <span class="nt">&lt;param-value&gt;</span>/WEB-INF/app-context.xml<span class="nt">&lt;/param-value&gt;</span>
    <span class="nt">&lt;/context-param&gt;</span>
    <span class="nt">&lt;servlet&gt;</span>
        <span class="nt">&lt;servlet-name&gt;</span>app<span class="nt">&lt;/servlet-name&gt;</span>
        <span class="nt">&lt;servlet-class&gt;</span>org.springframework.web.servlet.DispatcherServlet<span class="nt">&lt;/servlet-class&gt;</span>
        <span class="nt">&lt;init-param&gt;</span>
            <span class="nt">&lt;param-name&gt;</span>contextConfigLocation<span class="nt">&lt;/param-name&gt;</span>
            <span class="nt">&lt;param-value&gt;&lt;/param-value&gt;</span>
        <span class="nt">&lt;/init-param&gt;</span>
        <span class="nt">&lt;load-on-startup&gt;</span>1<span class="nt">&lt;/load-on-startup&gt;</span>
    <span class="nt">&lt;/servlet&gt;</span>
    <span class="nt">&lt;servlet-mapping&gt;</span>
        <span class="nt">&lt;servlet-name&gt;</span>app<span class="nt">&lt;/servlet-name&gt;</span>
        <span class="nt">&lt;url-pattern&gt;</span>/app/*<span class="nt">&lt;/url-pattern&gt;</span>
    <span class="nt">&lt;/servlet-mapping&gt;</span>
<span class="nt">&lt;/web-app&gt;</span>
</code></pre></div></div>

<p>要使用<code class="language-plaintext highlighter-rouge">ApplicationContext</code>里提供的<code class="language-plaintext highlighter-rouge">HierarchicalBeanFactory</code>提供的功能,可以使用如下:</p>

<p><img src="/assets/3/spring-mvc/mvc-context-hierarchy.png" alt="" /></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">class</span> <span class="nc">MyWebAppInitializer</span> <span class="kd">extends</span> <span class="nc">AbstractAnnotationConfigDispatcherServletInitializer</span> <span class="o">{</span>
    <span class="nd">@Override</span>
    <span class="kd">protected</span> <span class="nc">Class</span><span class="o">&lt;?&gt;[]</span> <span class="n">getRootConfigClasses</span><span class="o">()</span> <span class="o">{</span>
        <span class="k">return</span> <span class="k">new</span> <span class="nc">Class</span><span class="o">&lt;?&gt;[]</span> <span class="o">{</span> <span class="nc">RootConfig</span><span class="o">.</span><span class="na">class</span> <span class="o">};</span>
    <span class="o">}</span>
    <span class="nd">@Override</span>
    <span class="kd">protected</span> <span class="nc">Class</span><span class="o">&lt;?&gt;[]</span> <span class="n">getServletConfigClasses</span><span class="o">()</span> <span class="o">{</span>
        <span class="k">return</span> <span class="k">new</span> <span class="nc">Class</span><span class="o">&lt;?&gt;[]</span> <span class="o">{</span> <span class="nc">App1Config</span><span class="o">.</span><span class="na">class</span> <span class="o">};</span>
    <span class="o">}</span>
    <span class="nd">@Override</span>
    <span class="kd">protected</span> <span class="nc">String</span><span class="o">[]</span> <span class="nf">getServletMappings</span><span class="o">()</span> <span class="o">{</span>
        <span class="k">return</span> <span class="k">new</span> <span class="nc">String</span><span class="o">[]</span> <span class="o">{</span> <span class="s">"/app1/*"</span> <span class="o">};</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<p>可以通过一系列<code class="language-plaintext highlighter-rouge">XxxInitialzer</code>自由的添加<code class="language-plaintext highlighter-rouge">Servlet</code>,<code class="language-plaintext highlighter-rouge">Filter</code>,<code class="language-plaintext highlighter-rouge">Listener</code>等等</p>

<h1 id="实现细节">实现细节</h1>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">interface</span> <span class="nc">HandlerMapping</span> <span class="o">{</span>
    <span class="o">...</span>
	<span class="nd">@Nullable</span>
	<span class="nc">HandlerExecutionChain</span> <span class="nf">getHandler</span><span class="o">(</span><span class="nc">HttpServletRequest</span> <span class="n">request</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">Exception</span><span class="o">;</span>
<span class="o">}</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">HandlerExecutionChain</span><span class="o">{</span>
    <span class="o">...</span>
    <span class="kd">public</span> <span class="nf">HandlerExecutionChain</span><span class="o">(</span><span class="nc">Object</span> <span class="n">handler</span><span class="o">){...}</span>
    <span class="kd">public</span> <span class="nc">Object</span> <span class="nf">getHandler</span><span class="o">(){...}</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">addInteceptor</span><span class="o">(</span><span class="nc">HandlerInterceptor</span> <span class="n">interceptor</span><span class="o">){...}</span>
    <span class="kt">void</span> <span class="nf">applyPreHandle</span><span class="o">(</span><span class="nc">HttpServletRequest</span> <span class="n">req</span><span class="o">,</span> <span class="nc">HttpServletResponse</span> <span class="n">res</span><span class="o">){...}</span>
    <span class="kt">void</span> <span class="nf">applyPostHandle</span><span class="o">(</span><span class="nc">HttpServletRequest</span> <span class="n">req</span><span class="o">,</span> <span class="nc">HttpServletResponse</span> <span class="n">res</span><span class="o">){...}</span>
    <span class="kt">void</span> <span class="nf">triggerAfterCompletion</span><span class="o">(</span><span class="nc">HttpServletRequest</span> <span class="n">request</span><span class="o">,</span> <span class="nc">HttpServletResponse</span> <span class="n">response</span><span class="o">,</span> <span class="nc">Exception</span> <span class="n">ex</span><span class="o">){...}</span>
    <span class="kt">void</span> <span class="nf">applyAfterConcurrentHandlingStarted</span><span class="o">(</span><span class="nc">HttpServletRequest</span> <span class="n">request</span><span class="o">,</span> <span class="nc">HttpServletResponse</span> <span class="n">response</span><span class="o">){...}</span>
<span class="o">}</span>
<span class="kd">public</span> <span class="kd">interface</span> <span class="nc">HandlerInterceptor</span><span class="o">{</span>
    <span class="kt">boolean</span> <span class="nf">preHandle</span><span class="o">(</span><span class="nc">HttpServletRequest</span> <span class="n">request</span><span class="o">,</span> <span class="nc">HttpServletResponse</span> <span class="n">response</span><span class="o">,</span> <span class="nc">Object</span> <span class="n">handler</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">Exception</span><span class="o">;</span>
    <span class="kt">void</span> <span class="nf">postHandle</span><span class="o">(</span><span class="nc">HttpServletRequest</span> <span class="n">request</span><span class="o">,</span> <span class="nc">HttpServletResponse</span> <span class="n">response</span><span class="o">,</span> <span class="nc">Object</span> <span class="n">handler</span><span class="o">,</span> <span class="nc">ModelAndView</span> <span class="n">modelAndView</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">Exception</span><span class="o">;</span>
    <span class="kt">void</span> <span class="nf">afterCompletion</span><span class="o">(</span><span class="nc">HttpServletRequest</span> <span class="n">request</span><span class="o">,</span> <span class="nc">HttpServletResponse</span> <span class="n">response</span><span class="o">,</span> <span class="nc">Object</span> <span class="n">handler</span><span class="o">,</span> <span class="nc">Exception</span> <span class="n">ex</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">Exception</span><span class="o">;</span>
<span class="o">}</span>
<span class="kd">public</span> <span class="kd">interface</span> <span class="nc">HandlerAdapter</span><span class="o">{</span>
    <span class="kt">boolean</span> <span class="nf">supports</span><span class="o">(</span><span class="nc">Object</span> <span class="n">handler</span><span class="o">);</span>
    <span class="nc">ModelAndView</span> <span class="nf">handle</span><span class="o">(</span><span class="nc">HttpServletRequest</span> <span class="n">request</span><span class="o">,</span> <span class="nc">HttpServletResponse</span> <span class="n">response</span><span class="o">,</span> <span class="nc">Object</span> <span class="n">handler</span><span class="o">)</span> <span class="kd">throws</span> <span class="nc">Exception</span><span class="o">;</span>
    <span class="kt">long</span> <span class="nf">getLastModified</span><span class="o">(</span><span class="nc">HttpServletRequest</span> <span class="n">request</span><span class="o">,</span> <span class="nc">Object</span> <span class="n">handler</span><span class="o">);</span>
<span class="o">}</span>
</code></pre></div></div>

<h1 id="执行过程">执行过程</h1>

<p><img src="/assets/3/spring-mvc/1.jpg" alt="" /></p>

<p><img src="https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-servlet-sequence" alt="官方文档-Processing" /></p>

<blockquote>

  <ul>
    <li>DispatcherServlet接收HttpServletRequest</li>
    <li>DispatcherServlet查找绑定的ApplicationContext:
      <div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">class</span> <span class="nc">MyWebAppInitializer</span> <span class="kd">extends</span> <span class="nc">AbstractDispatcherServletInitializer</span> <span class="o">{</span>
  <span class="nd">@Override</span>
  <span class="kd">protected</span> <span class="nc">WebApplicationContext</span> <span class="nf">createServletApplicationContext</span><span class="o">()</span> <span class="o">{</span>
      <span class="nc">XmlWebApplicationContext</span> <span class="n">cxt</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">XmlWebApplicationContext</span><span class="o">();</span>
      <span class="n">cxt</span><span class="o">.</span><span class="na">setConfigLocation</span><span class="o">(</span><span class="s">"/WEB-INF/spring/dispatcher-config.xml"</span><span class="o">);</span>
      <span class="k">return</span> <span class="n">cxt</span><span class="o">;</span>
  <span class="o">}</span>  
  <span class="o">...</span>
<span class="o">}</span>
</code></pre></div>      </div>
    </li>
    <li>如果ApplicationContext绑定了LocaleResolver,查找绑定的LocaleResolver</li>
    <li>如果ApplicationContext绑定了ThemeResolver,查找绑定的ThemeResolver</li>
    <li>如果request是multipart,把HttpServletRequest封装成MultipartHttpServletRequest</li>
    <li>ApplicationContext查找绑定的HandlerMapping</li>
    <li>ApplicationContext查找绑定的HandlerAdapter</li>
    <li>如果返回model,调用渲染并返回客户端</li>
  </ul>
</blockquote>

<h2 id="细节">细节</h2>

<blockquote>

  <ul>
    <li>HandlerExecutionChain hec = DispatcherServlet::getHandler(HttpServletReuqest);</li>
    <li>HandlerAdapter ha = DispatcherServlet::getHandlerAdapter(Object);</li>
    <li>boolean res = HandlerExecutionChain.applyPreHandle(HttpServletRequest,HttpServletResponse);</li>
    <li>ModelAndView mav = HandlerAdapter.handle();</li>
    <li>HandlerExecutionChain.applyPostHandle(HttpServletRequest,HttpServletResponse,ModelAndView)</li>
    <li>DispatcherServlet –» doDispatch –» processDispatchResult –» render(ModelAndView, HttpServletRequest, HttpServletResponse);</li>
  </ul>
</blockquote>

<h1 id="使用">使用</h1>

<h2 id="requestmapping">RequestMapping</h2>

<p><a href="https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-requestmapping">RequestMapping</a></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nd">@RestController</span>
<span class="nd">@RequestMapping</span><span class="o">(</span><span class="s">"/persons"</span><span class="o">)</span>
<span class="kd">class</span> <span class="nc">PersonController</span> <span class="o">{</span>
    <span class="nd">@GetMapping</span><span class="o">(</span><span class="s">"/{id}"</span><span class="o">)</span>
    <span class="kd">public</span> <span class="nc">Person</span> <span class="nf">getPerson</span><span class="o">(</span><span class="nd">@PathVariable</span> <span class="nc">Long</span> <span class="n">id</span><span class="o">)</span> <span class="o">{</span>
    <span class="o">}</span>
    <span class="nd">@PostMapping</span>
    <span class="nd">@ResponseStatus</span><span class="o">(</span><span class="nc">HttpStatus</span><span class="o">.</span><span class="na">CREATED</span><span class="o">)</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">add</span><span class="o">(</span><span class="nd">@RequestBody</span> <span class="nc">Person</span> <span class="n">person</span><span class="o">)</span> <span class="o">{</span>
    <span class="o">}</span>
<span class="o">}</span>
<span class="cm">/***************************************************************************************/</span>
<span class="nd">@GetMapping</span>
<span class="nd">@PostMapping</span>
<span class="nd">@PutMapping</span>
<span class="nd">@DeleteMing</span>
<span class="nd">@PatchMapping</span>
</code></pre></div></div>

<p><code class="language-plaintext highlighter-rouge">@RequestMapping</code>注解的方法签名有特殊意义:</p>

<p><a href="https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-arguments">MethodArguments</a></p>

<p><a href="https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-return-types">ReturnValues</a></p>

<p><a href="https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-typeconversion">TypeConversion</a></p>

<h2 id="handlermethod">HandlerMethod</h2>

<p><a href="https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-methods">HandlerMethod</a></p>

<h2 id="databinder">DataBinder</h2>

<p><a href="https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-initbinder">DataBinder</a></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nd">@Controller</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">FormController</span> <span class="o">{</span>
    <span class="nd">@InitBinder</span> 
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">initBinder</span><span class="o">(</span><span class="nc">WebDataBinder</span> <span class="n">binder</span><span class="o">)</span> <span class="o">{</span>
        <span class="nc">SimpleDateFormat</span> <span class="n">dateFormat</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">SimpleDateFormat</span><span class="o">(</span><span class="s">"yyyy-MM-dd"</span><span class="o">);</span>
        <span class="n">dateFormat</span><span class="o">.</span><span class="na">setLenient</span><span class="o">(</span><span class="kc">false</span><span class="o">);</span>
        <span class="n">binder</span><span class="o">.</span><span class="na">registerCustomEditor</span><span class="o">(</span><span class="nc">Date</span><span class="o">.</span><span class="na">class</span><span class="o">,</span> <span class="k">new</span> <span class="nc">CustomDateEditor</span><span class="o">(</span><span class="n">dateFormat</span><span class="o">,</span> <span class="kc">false</span><span class="o">));</span>
    <span class="o">}</span>
<span class="o">}</span>
<span class="cm">/***************************************************************************************/</span>
<span class="nd">@Controller</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">FormController</span> <span class="o">{</span>
    <span class="nd">@InitBinder</span> 
    <span class="kd">protected</span> <span class="kt">void</span> <span class="nf">initBinder</span><span class="o">(</span><span class="nc">WebDataBinder</span> <span class="n">binder</span><span class="o">)</span> <span class="o">{</span>
        <span class="n">binder</span><span class="o">.</span><span class="na">addCustomFormatter</span><span class="o">(</span><span class="k">new</span> <span class="nc">DateFormatter</span><span class="o">(</span><span class="s">"yyyy-MM-dd"</span><span class="o">));</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>

<p><code class="language-plaintext highlighter-rouge">DataBinder</code>提供了类似<code class="language-plaintext highlighter-rouge">Validator</code>,<code class="language-plaintext highlighter-rouge">PropertyEditor</code>等等功能,验证结果等等可以通过<code class="language-plaintext highlighter-rouge">Controller</code>的方法签名接收</p>

<p><a href="https://stackoverflow.com/questions/5211323/what-is-the-purpose-of-init-binder-in-spring-mvc">StackOverflow-What-Is-The-Purpose-Of-Init-Binder-In-Spring-Mvc</a></p>

<p><a href="https://hibernate.org/validator/">Hibernate-Validator</a></p>

<h2 id="httpmessageconverter">HttpMessageConverter</h2>

<p>SpringMvc对<code class="language-plaintext highlighter-rouge">HttpServletResponse</code>和<code class="language-plaintext highlighter-rouge">HttpServletRequest</code>进行了封装:</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">interface</span> <span class="nc">HttpInputMessage</span> <span class="kd">extends</span> <span class="nc">HttpMessage</span> <span class="o">{</span>
	<span class="nc">InputStream</span> <span class="nf">getBody</span><span class="o">()</span> <span class="kd">throws</span> <span class="nc">IOException</span><span class="o">;</span>
<span class="o">}</span>
<span class="cm">/***************************************************************************************/</span>
<span class="kd">public</span> <span class="kd">interface</span> <span class="nc">HttpOutputMessage</span> <span class="kd">extends</span> <span class="nc">HttpMessage</span> <span class="o">{</span>
	<span class="nc">OutputStream</span> <span class="nf">getBody</span><span class="o">()</span> <span class="kd">throws</span> <span class="nc">IOException</span><span class="o">;</span>
<span class="o">}</span>
</code></pre></div></div>

<p>和<code class="language-plaintext highlighter-rouge">DataBinder</code>的功能有所不同,<code class="language-plaintext highlighter-rouge">HttpXxxMessage</code>所在的层面相对更远离业务,因为它直接写<code class="language-plaintext highlighter-rouge">HttpServletXxx</code><br />
同理,<code class="language-plaintext highlighter-rouge">HttpMessageConverter</code>也是直接写<code class="language-plaintext highlighter-rouge">HttpServletXxx</code>的,一些框架例如<code class="language-plaintext highlighter-rouge">fastjson</code>就是直接定义一个<code class="language-plaintext highlighter-rouge">HttpMessageConverter</code>实现的<br />
相对来说<code class="language-plaintext highlighter-rouge">HttpMessageConverter</code>更像一个<code class="language-plaintext highlighter-rouge">Filter</code>,对所有进入和出去的<code class="language-plaintext highlighter-rouge">HttpServletXxx</code>进行第一层和最后一层的CRUD</p>

<p>而<code class="language-plaintext highlighter-rouge">DataBinder</code>提供的<code class="language-plaintext highlighter-rouge">Converter</code>和<code class="language-plaintext highlighter-rouge">Validator</code>更倾向于业务层面的验证等等,业务层面的代码更应该写在这里</p>

<h2 id="exceptions">Exceptions</h2>

<p><a href="https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-exceptionhandler">Exceptions</a></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nd">@Controller</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">SimpleController</span> <span class="o">{</span>
    <span class="nd">@ExceptionHandler</span>
    <span class="kd">public</span> <span class="nc">ResponseEntity</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;</span> <span class="nf">handle</span><span class="o">(</span><span class="nc">IOException</span> <span class="n">ex</span><span class="o">)</span> <span class="o">{</span>
    <span class="o">}</span>
<span class="o">}</span>
<span class="cm">/***************************************************************************************/</span>
<span class="nd">@ExceptionHandler</span><span class="o">({</span><span class="nc">FileSystemException</span><span class="o">.</span><span class="na">class</span><span class="o">,</span> <span class="nc">RemoteException</span><span class="o">.</span><span class="na">class</span><span class="o">})</span>
<span class="kd">public</span> <span class="nc">ResponseEntity</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;</span> <span class="nf">handle</span><span class="o">(</span><span class="nc">IOException</span> <span class="n">ex</span><span class="o">)</span> <span class="o">{</span>
<span class="o">}</span>
<span class="cm">/***************************************************************************************/</span>
<span class="nd">@ExceptionHandler</span><span class="o">({</span><span class="nc">FileSystemException</span><span class="o">.</span><span class="na">class</span><span class="o">,</span> <span class="nc">RemoteException</span><span class="o">.</span><span class="na">class</span><span class="o">})</span>
<span class="kd">public</span> <span class="nc">ResponseEntity</span><span class="o">&lt;</span><span class="nc">String</span><span class="o">&gt;</span> <span class="nf">handle</span><span class="o">(</span><span class="nc">Exception</span> <span class="n">ex</span><span class="o">)</span> <span class="o">{</span>
<span class="o">}</span>
</code></pre></div></div>

<p>对于有<code class="language-plaintext highlighter-rouge">@ExceptionHandler</code>注解的方法,方法的签名(参数和返回值)都有特殊意义:</p>

<p><a href="https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-exceptionhandler-args">MethodArguments</a></p>

<p><a href="https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-exceptionhandler-return-values">ReturnValues</a></p>

<h1 id="webmvcconfigurer">WebMvcConfigurer</h1>

<p>SpringMvc的自动配置类为: <code class="language-plaintext highlighter-rouge">WebMvcAutoConfiguration</code>:</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="o">...</span>
<span class="nd">@ConditionalOnClass</span><span class="o">({</span> <span class="nc">Servlet</span><span class="o">.</span><span class="na">class</span><span class="o">,</span> <span class="nc">DispatcherServlet</span><span class="o">.</span><span class="na">class</span><span class="o">,</span> <span class="nc">WebMvcConfigurer</span><span class="o">.</span><span class="na">class</span> <span class="o">})</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">WebMvcAutoConfiguration</span><span class="o">{</span>
    <span class="o">...</span>
<span class="o">}</span>
<span class="cm">/***************************************************************************************/</span>
<span class="kd">interface</span> <span class="nc">WebMvcConfigurer</span><span class="o">{</span>
    <span class="o">...</span>
    <span class="kt">void</span> <span class="nf">addFormatters</span><span class="o">(</span><span class="nc">FormatterRegistry</span> <span class="n">fr</span><span class="o">);</span>
    <span class="kt">void</span> <span class="nf">addInterceptor</span><span class="o">(</span><span class="nc">InterceptorRegistry</span> <span class="n">ir</span><span class="o">);</span>
    <span class="kt">void</span> <span class="nf">addResourceHandlers</span><span class="o">(</span><span class="nc">ResourceHandlerRegistry</span> <span class="n">rr</span><span class="o">);</span>
    <span class="kt">void</span> <span class="nf">addCorsMappings</span><span class="o">(</span><span class="nc">CorsRegistry</span> <span class="n">cr</span><span class="o">);</span>
    <span class="kt">void</span> <span class="nf">addViewControllers</span><span class="o">(</span><span class="nc">ViewControllerRegistry</span> <span class="n">vr</span><span class="o">);</span>
    <span class="kt">void</span> <span class="nf">addArgumentResolvers</span><span class="o">(</span><span class="nc">List</span><span class="o">&lt;</span><span class="nc">HandlerMethodArgumentResolver</span><span class="o">&gt;</span> <span class="n">lhmar</span><span class="o">);</span>
    <span class="kt">void</span> <span class="nf">addReturnValueHandlers</span><span class="o">(</span><span class="nc">List</span><span class="o">&lt;</span><span class="nc">HandlerMethodReturnValueHandler</span><span class="o">&gt;</span> <span class="n">lhmrvh</span><span class="o">);</span>
    <span class="o">...</span>
    <span class="kt">void</span> <span class="nf">configurePathMatch</span><span class="o">(</span><span class="nc">PathMatchConfigurer</span> <span class="n">configurer</span><span class="o">);</span>
    <span class="kt">void</span> <span class="nf">configureContentNegotiation</span><span class="o">(</span><span class="nc">ContentNegotiationConfigurer</span> <span class="n">configurer</span><span class="o">);</span>
    <span class="kt">void</span> <span class="nf">configureAsyncSupport</span><span class="o">(</span><span class="nc">AsyncSupportConfigurer</span> <span class="n">configurer</span><span class="o">);</span>
    <span class="kt">void</span> <span class="nf">configureDefaultServletHandling</span><span class="o">(</span><span class="nc">DefaultServletHandlerConfigurer</span> <span class="n">configurer</span><span class="o">);</span>
    <span class="kt">void</span> <span class="nf">configureViewResolvers</span><span class="o">(</span><span class="nc">ViewResolverRegistry</span> <span class="n">registry</span><span class="o">);</span>
    <span class="kt">void</span> <span class="nf">configureMessageConverters</span><span class="o">(</span><span class="nc">List</span><span class="o">&lt;</span><span class="nc">HttpMessageConverter</span><span class="o">&lt;?&gt;&gt;</span> <span class="n">converters</span><span class="o">);</span>
    <span class="kt">void</span> <span class="nf">configureHandlerExceptionResolvers</span><span class="o">(</span><span class="nc">List</span><span class="o">&lt;</span><span class="nc">HandlerExceptionResolver</span><span class="o">&gt;</span> <span class="n">resolvers</span><span class="o">);</span>
<span class="o">}</span>
<span class="cm">/***************************************************************************************/</span>
<span class="nd">@Configuration</span>
<span class="nd">@EnableWebMvc</span>
<span class="kd">public</span> <span class="kd">class</span> <span class="nc">WebConfig</span> <span class="kd">implements</span> <span class="nc">WebMvcConfigurer</span> <span class="o">{</span>
    <span class="nd">@Override</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">addFormatters</span><span class="o">(</span><span class="nc">FormatterRegistry</span> <span class="n">registry</span><span class="o">)</span> <span class="o">{</span>
        <span class="nc">DateTimeFormatterRegistrar</span> <span class="n">registrar</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">DateTimeFormatterRegistrar</span><span class="o">();</span>
        <span class="n">registrar</span><span class="o">.</span><span class="na">setUseIsoFormat</span><span class="o">(</span><span class="kc">true</span><span class="o">);</span>
        <span class="n">registrar</span><span class="o">.</span><span class="na">registerFormatters</span><span class="o">(</span><span class="n">registry</span><span class="o">);</span>
    <span class="o">}</span>
<span class="o">}</span>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2021-01-11T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2021/01/11/gradle.html">Gradle</a></div><div class="next"><span>下篇</span><a href="/2021/01/11/spring-three-level-cache.html">Spring Three Level Cache (Spring 三级缓存)</a></div></div></div>

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