---
title: Java Security Architecture
date: 0000-01-01 00:00:00 Z
tags:
- Java
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Java Security Architecture"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="0000-01-01T08:00:00+08:00">
    <meta itemprop="keywords" content="Java"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Java Security Architecture" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="0000-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Java Security Architecture" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="0000-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<<<<<<< HEAD
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Java Security Architecture" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="0000-01-01T08:00:00+08:00" />
    <meta itemprop="keywords" content="Java" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
=======
>>>>>>> 3aaf6be6636648b1ab4c90bee56e9c7e29e3ede1
<div class="article__content" itemprop="articleBody"><h1 id="java-security-architecture">Java Security Architecture</h1>

<p><a href="https://zhuanlan.zhihu.com/p/36832100">X.509 数字证书的基本原理及应用</a></p>

<p>Java Security 是 Java 语言内核层级的特性<br />
只要通过 <code class="language-plaintext highlighter-rouge">java -Djava.security.manager </code> 启动安全管理,便可以自动的对所有运行代码进行安全检查<br />
类之间大致的组合关系大致如下:</p>

<blockquote>

  <ul>
    <li>LoginContext
      <ul>
        <li>AccessController</li>
        <li>SecurityManager (deprecated)</li>
        <li>Subject
          <ul>
            <li>Principal</li>
          </ul>
        </li>
      </ul>
    </li>
    <li>SecurityManager （deprecated)
      <ul>
        <li>AccessController
          <ul>
            <li>AccessControlContext
              <ul>
                <li>ProtectionDomain
                  <ul>
                    <li>CodeSource</li>
                    <li>Principal</li>
                    <li>Permission</li>
                  </ul>
                </li>
              </ul>
            </li>
          </ul>
        </li>
      </ul>
    </li>
    <li>AccessController
      <ul>
        <li>AccessControlContext
          <ul>
            <li>ProtectionDomain
              <ul>
                <li>CodeSource</li>
                <li>Principal</li>
                <li>Permission</li>
              </ul>
            </li>
          </ul>
        </li>
      </ul>
    </li>
  </ul>
</blockquote>

<h1 id="配置">配置</h1>

<p>只要设置了 <code class="language-plaintext highlighter-rouge">java -Djava.security.manager</code> 就表明启用了安全机制,<code class="language-plaintext highlighter-rouge">java -Djava.security.manager=A.B.MySecurityManager</code> 还可以指定自己的安全管理器实现<br />
默认情况下,jvm会读取 <code class="language-plaintext highlighter-rouge">${java.home}/conf/security/java.policy</code>, <code class="language-plaintext highlighter-rouge">${user.home}/.java.policy</code> 和 <code class="language-plaintext highlighter-rouge">${java.home}/conf/security/java.security</code> 
其中对于 <code class="language-plaintext highlighter-rouge">.policy</code> 文件,可以通过 <code class="language-plaintext highlighter-rouge">java -Djava.security.policy=myUrl</code> 或者在 <code class="language-plaintext highlighter-rouge">.security</code> 文件里指定自己的 <code class="language-plaintext highlighter-rouge">.policy</code></p>

<h2 id="javasecurity">java.security</h2>

<p><code class="language-plaintext highlighter-rouge">java.security</code>:</p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c"># 默认为 sun.security.provider.PolicyFile</span>
policy.provider<span class="o">=</span>A.B.MyPolicyProvider 

<span class="c"># policy.url.2 的文件会覆盖 policy.url.1 的配置</span>
policy.url.1 <span class="o">=</span> ...
policy.url.2 <span class="o">=</span> ...

<span class="c"># keystore 文件的格式</span>
keystore.type <span class="o">=</span> ...

<span class="c"># 使用全限定类名加载</span>
<span class="c"># 必须实现 Provider 接口</span>
security.provider.1 <span class="o">=</span> A.B.MyProvider1

<span class="c"># 使用 SPI 加载实现</span>
security.provider.2 <span class="o">=</span> MyProvider2

<span class="c"># 该值确定哪个序号的 provider 被启用,即 security.provider.n 的 n</span>
jdk.security.provider.preferred <span class="o">=</span> ...
...

</code></pre></div></div>

<h2 id="javapolicy">java.policy</h2>

<p><code class="language-plaintext highlighter-rouge">java.policy</code>:</p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c"># java.policy 包含:</span>
<span class="c"># 0-1 个 keystore</span>
<span class="c"># 0-1 个 keystorePasswordURL</span>
<span class="c"># 0-n 个 grant </span>

<span class="c"># keystore 文件相对 policy.url.n 的位置</span>
keystore <span class="o">=</span> ...

<span class="c"># keystore是一个加密文件</span>
<span class="c"># 该项指明了 keystore 的密码文件所在 url</span>
keystorePasswordURL <span class="o">=</span> ...

<span class="c"># signedBy, codeBase principal 都是可以省略的</span>
<span class="c"># 首先,一个 grant 字段代表一个 domain</span>
<span class="c">#</span>
<span class="c"># signedBy  : 表示该 domain 被某个 private key 签名(涉及非对称加密,涉及 jdk 的 jarsigner.exe)</span>
<span class="c"># codeBase  : 表示该 domain 的地址(文件系统的地址或者 url 地址)</span>
<span class="c"># principal : 表示一个执行主体,当 domain 以该主体执行时通过</span>
grant signedBy <span class="s2">""</span>, codeBase <span class="s2">""</span>, principal A.B.MyPrincipal1 <span class="s2">""</span>, principal A.B.MyPrincipal2 <span class="s2">""</span><span class="o">{</span>
    <span class="c"># 允许使用诸如 ${java.home}, ${user.home} 等属性</span>
    permission A.B.MyPermission1 <span class="s2">"target_name"</span>, <span class="s2">"action_name"</span><span class="p">;</span>
    permission A.B.MyPermission2 <span class="s2">"target_name"</span>, <span class="s2">"action_name"</span>, signedBy <span class="s2">""</span><span class="p">;</span>
<span class="o">}</span>
</code></pre></div></div>

<h1 id="keystore">KeyStore</h1>

<p><a href="https://www.baeldung.com/java-keystore">Java KeyStore API</a></p>

<p><a href="https://docs.oracle.com/cd/E19509-01/820-3503/ggbgc/index.html">Public Keys, Private Keys, and Certificates</a></p>

<p>使用 <code class="language-plaintext highlighter-rouge">keytool</code> 工具,可以生成一个 <code class="language-plaintext highlighter-rouge">.keystore</code> 文件,该文件实际上是一个证书的简易数据库<br />
而这个 <code class="language-plaintext highlighter-rouge">.keystore</code> 在 Java 环境下的格式就是 <code class="language-plaintext highlighter-rouge">class KeyStore{...}</code><br />
该数据库可以存放几种大类的数据:</p>

<ul>
  <li>对称加密密钥 (Secret Key)</li>
</ul>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nc">KeyStore</span><span class="o">.</span><span class="na">SecretKeyEntry</span> <span class="n">secret</span>
<span class="o">=</span> <span class="k">new</span> <span class="nc">KeyStore</span><span class="o">.</span><span class="na">SecretKeyEntry</span><span class="o">(</span><span class="n">secretKey</span><span class="o">);</span>
<span class="nc">KeyStore</span><span class="o">.</span><span class="na">ProtectionParameter</span> <span class="n">password</span>
<span class="o">=</span> <span class="k">new</span> <span class="nc">KeyStore</span><span class="o">.</span><span class="na">PasswordProtection</span><span class="o">(</span><span class="n">pwdArray</span><span class="o">);</span>
<span class="n">ks</span><span class="o">.</span><span class="na">setEntry</span><span class="o">(</span><span class="s">"db-encryption-secret"</span><span class="o">,</span> <span class="n">secret</span><span class="o">,</span> <span class="n">password</span><span class="o">);</span>
</code></pre></div></div>

<ul>
  <li>非对称加密密钥 (Public Key, Private Key)</li>
</ul>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="nc">X509Certificate</span><span class="o">[]</span> <span class="n">certificateChain</span> <span class="o">=</span> <span class="k">new</span> <span class="nc">X509Certificate</span><span class="o">[</span><span class="mi">2</span><span class="o">];</span>
<span class="n">chain</span><span class="o">[</span><span class="mi">0</span><span class="o">]</span> <span class="o">=</span> <span class="n">clientCert</span><span class="o">;</span>
<span class="n">chain</span><span class="o">[</span><span class="mi">1</span><span class="o">]</span> <span class="o">=</span> <span class="n">caCert</span><span class="o">;</span>
<span class="cm">/**
 * 会自动的生成 public key
 */</span>
<span class="n">ks</span><span class="o">.</span><span class="na">setKeyEntry</span><span class="o">(</span><span class="s">"sso-signing-key"</span><span class="o">,</span> <span class="n">privateKey</span><span class="o">,</span> <span class="n">pwdArray</span><span class="o">,</span> <span class="n">certificateChain</span><span class="o">);</span>
</code></pre></div></div>

<ul>
  <li>证书(Certificate)_</li>
</ul>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">ks</span><span class="o">.</span><span class="na">setCertificateEntry</span><span class="o">(</span><span class="s">"google.com"</span><span class="o">,</span> <span class="n">trustedCertificate</span><span class="o">);</span>
</code></pre></div></div>

<p>Certificate 和 Public Key / Private Key 的区别在于, Public Key / Private Key 为服务器自己的公私密钥<br />
而 Certificate 是权威机构的 Info + Public Key</p>

<h1 id="codesource">CodeSource</h1>

<p><a href="https://docs.oracle.com/javase/7/docs/technotes/guides/security/spec/security-spec.doc3.htm">Permissions and Security Policy</a></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">class</span> <span class="nc">CodeSource</span> <span class="kd">implements</span> <span class="n">java</span><span class="o">.</span><span class="na">io</span><span class="o">.</span><span class="na">Serializable</span> <span class="o">{</span>
    <span class="o">...</span>
    <span class="kd">private</span> <span class="kd">transient</span> <span class="nc">CodeSigner</span><span class="o">[]</span> <span class="n">signers</span> <span class="o">=</span> <span class="o">...;</span>
    
    <span class="kd">public</span> <span class="kd">final</span> <span class="kd">class</span> <span class="nc">CodeSigner</span> <span class="kd">implements</span> <span class="n">java</span><span class="o">.</span><span class="na">io</span><span class="o">.</span><span class="na">Serializable</span><span class="o">{</span>
        <span class="o">...</span>
    <span class="o">}</span>
<span class="o">}</span>
<span class="cm">/****************************************************************************************************************************/</span>
<span class="kd">public</span> <span class="kd">abstract</span> <span class="kd">class</span> <span class="nc">CertPath</span> <span class="kd">implements</span> <span class="nc">Serializable</span> <span class="o">{</span>
    <span class="o">...</span>
    <span class="kd">public</span> <span class="kd">abstract</span> <span class="nc">List</span><span class="o">&lt;?</span> <span class="kd">extends</span> <span class="nc">Certificate</span><span class="o">&gt;</span> <span class="nf">getCertificates</span><span class="o">();</span>
<span class="o">}</span>
<span class="cm">/****************************************************************************************************************************/</span>
<span class="kd">public</span> <span class="kd">abstract</span> <span class="kd">class</span> <span class="nc">Certificate</span> <span class="kd">implements</span> <span class="n">java</span><span class="o">.</span><span class="na">io</span><span class="o">.</span><span class="na">Serializable</span> <span class="o">{</span>
    <span class="o">...</span>
    <span class="kd">public</span> <span class="kd">abstract</span> <span class="kt">void</span> <span class="nf">verify</span><span class="o">(</span><span class="nc">PublicKey</span> <span class="n">key</span><span class="o">)</span> <span class="kd">throws</span> <span class="o">...;</span>
    <span class="kd">public</span> <span class="kd">abstract</span> <span class="kt">void</span> <span class="nf">verify</span><span class="o">(</span><span class="nc">PublicKey</span> <span class="n">key</span><span class="o">,</span> <span class="nc">String</span> <span class="n">sigProvider</span><span class="o">)</span> <span class="kd">throws</span> <span class="o">...;</span>
    <span class="kd">public</span> <span class="kt">void</span> <span class="nf">verify</span><span class="o">(</span><span class="nc">PublicKey</span> <span class="n">key</span><span class="o">,</span> <span class="nc">Provider</span> <span class="n">sigProvider</span><span class="o">)</span> <span class="kd">throws</span> <span class="o">...;</span>

    <span class="kd">public</span> <span class="kd">abstract</span> <span class="nc">PublicKey</span> <span class="nf">getPublicKey</span><span class="o">();</span>
<span class="o">}</span>
</code></pre></div></div>

<p>可以看到 <code class="language-plaintext highlighter-rouge">signedBy</code> 功能是通过 <code class="language-plaintext highlighter-rouge">CodeSource</code> 进行验证的</p>

<h1 id="principal">Principal</h1>

<p><a href="https://www.baeldung.com/security-context-basics">Security Context Basics: User, Subject and Principal</a></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">interface</span> <span class="nc">Principal</span><span class="o">{</span>
    <span class="o">...</span>
    <span class="kd">public</span> <span class="k">default</span> <span class="kt">boolean</span> <span class="nf">implies</span><span class="o">(</span><span class="nc">Subject</span> <span class="n">subject</span><span class="o">)</span> <span class="o">{</span>
        <span class="k">if</span> <span class="o">(</span><span class="n">subject</span> <span class="o">==</span> <span class="kc">null</span><span class="o">)</span>
            <span class="k">return</span> <span class="kc">false</span><span class="o">;</span>
        <span class="k">return</span> <span class="n">subject</span><span class="o">.</span><span class="na">getPrincipals</span><span class="o">().</span><span class="na">contains</span><span class="o">(</span><span class="k">this</span><span class="o">);</span>
    <span class="o">}</span>
<span class="o">}</span>
<span class="cm">/****************************************************************************************************************************/</span>
<span class="kd">public</span> <span class="kd">final</span> <span class="kd">class</span> <span class="nc">Subject</span> <span class="kd">implements</span> <span class="n">java</span><span class="o">.</span><span class="na">io</span><span class="o">.</span><span class="na">Serializable</span> <span class="o">{</span>
    <span class="o">...</span>
    <span class="nc">Set</span><span class="o">&lt;</span><span class="nc">Principal</span><span class="o">&gt;</span> <span class="n">principals</span>
<span class="o">}</span>
</code></pre></div></div>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>grant principal A.B.C.MyPrincipal <span class="s2">""</span> <span class="o">{</span>
    ...
<span class="o">}</span>
</code></pre></div></div>

<h1 id="protectiondomain">ProtectionDomain</h1>

<p>一个 <code class="language-plaintext highlighter-rouge">ProtectionDomain</code> 即一个 <code class="language-plaintext highlighter-rouge">grant</code> 闭包的部分<br />
组合关系:</p>

<ul>
  <li>ProtectionDomain
    <ul>
      <li>CodeSource</li>
      <li>Principal</li>
    </ul>
  </li>
</ul>

<h1 id="permission">Permission</h1>

<p><a href="https://docs.oracle.com/javase/7/docs/technotes/guides/security/spec/security-spec.doc3.htm">Permissions and Security Policy</a></p>

<p>Permission 相关类的组合关系如下:</p>

<ul>
  <li>Permissions
    <ul>
      <li>PermissionCollection
        <ul>
          <li>Permission</li>
        </ul>
      </li>
    </ul>
  </li>
</ul>

<p>其中 Permission 常见有:</p>

<ul>
  <li>FilePermission</li>
  <li>SocketPermission</li>
  <li>BasicPermission</li>
  <li>PropertyPermission</li>
  <li>RuntimePermission</li>
  <li>AWTPermission</li>
  <li>NetPermission</li>
  <li>ReflectPermission</li>
  <li>SerializablePermission</li>
  <li>SecurityPermission</li>
  <li>AllPermission</li>
  <li>AuthPermsision</li>
</ul>

<p>上面所有的 Permission 都有一个接收两个 String 的构造函数,第一个 String 作为 target_name,第二个 String 作为 action_name</p>

<h1 id="policy">Policy</h1>

<p><a href="https://docs.oracle.com/javase/7/docs/technotes/guides/security/spec/security-spec.doc3.htm">Permissions and Security Policy</a></p>

<p><a href="https://docs.oracle.com/javase/7/docs/api/java/security/Policy.html#getInstance(java.lang.String,%20java.security.Policy.Parameters)">Class Policy</a></p>

<p><a href="https://docs.oracle.com/javase/7/docs/technotes/guides/security/PolicyFiles.html">Default Policy Implementation and Policy File Syntax</a></p>

<p><a href="https://github.com/frohoff/jdk8u-jdk/blob/master/src/share/classes/sun/security/provider/PolicyFile.java">sun.security.provider.PolicyFile</a></p>

<p><a href="https://docs.oracle.com/javase/8/docs/api/java/security/Provider.html">java.security.Provider</a></p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">abstract</span> <span class="kd">class</span> <span class="nc">Policy</span><span class="o">{</span>
    <span class="cm">/**
     * Policy.getInstance(...) 使用 SPI 加载实现
     * 以下均对于使用默认实现的 Policy : sun.security.provider.PolicyFile (在 .security 里使用 policy.provider = ... 指定)
     *
     * @param type     : 只能是 JavaPolicy, 也就是调用 sun.security.provider.PolicyFile
     * @param params   : 参数
     * @param provider : 和 .security 里的 security.provider=... 一样
     */</span>
    <span class="kd">public</span> <span class="kd">static</span> <span class="nc">Policy</span> <span class="nf">getInstance</span><span class="o">(</span><span class="nc">String</span> <span class="n">type</span><span class="o">,</span> <span class="nc">Policy</span><span class="o">.</span><span class="na">Parameters</span> <span class="n">params</span><span class="o">,</span> <span class="nc">Provider</span> <span class="n">provider</span><span class="o">){...}</span>
<span class="o">}</span>
</code></pre></div></div>

<h1 id="accesscontroller--securitymanager">AccessController / SecurityManager</h1>

<p><a href="https://docs.oracle.com/javase/7/docs/technotes/guides/security/spec/security-spec.doc4.htm">Access Control Mechanisms and Algorithms</a></p>

<p><a href="https://docs.oracle.com/javase/7/docs/technotes/guides/security/spec/security-spec.doc6.html">Security Management</a></p>

<p>当前版本基本上 SecurityManager 已经不用,但是仍然被支持,对 SecurityManager 的操作大部分会被代理到 AccessController 上</p>

<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kd">public</span> <span class="kd">final</span> <span class="kd">class</span> <span class="nc">AccessController</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="kd">static</span> <span class="kd">native</span> <span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="no">T</span> <span class="nf">doPrivileged</span><span class="o">(</span><span class="nc">PrivilegedAction</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">action</span><span class="o">);</span>
    <span class="kd">public</span> <span class="kd">static</span> <span class="kd">native</span> <span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="no">T</span> <span class="nf">doPrivileged</span><span class="o">(</span><span class="nc">PrivilegedAction</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="n">action</span><span class="o">,</span> <span class="nc">AccessControlContext</span> <span class="n">context</span><span class="o">);</span>
    <span class="o">...</span>
<span class="o">}</span>
<span class="cm">/****************************************************************************************************************************/</span>
<span class="kd">public</span> <span class="kd">interface</span> <span class="nc">PrivilegedAction</span><span class="o">&lt;</span><span class="no">T</span><span class="o">&gt;</span> <span class="o">{</span>
    <span class="no">T</span> <span class="nf">run</span><span class="o">();</span>
<span class="o">}</span>

</code></pre></div></div>

<p><code class="language-plaintext highlighter-rouge">doPrivileged(...)</code> 接收一个 <code class="language-plaintext highlighter-rouge">PrivilegedAction</code><br />
<code class="language-plaintext highlighter-rouge">AccessController</code> 会自动的调用 <code class="language-plaintext highlighter-rouge">PrivilegedAction.run()</code></p>

<p><code class="language-plaintext highlighter-rouge">doPrivileged</code> 的作用在用于,会让 <code class="language-plaintext highlighter-rouge">PrivilegedAction.run()</code> 内的代码赋予当前调用 <code class="language-plaintext highlighter-rouge">doPrivileged</code> 的环境下的权限</p>

<h1 id="accesscontrolcontext">AccessControlContext</h1>

<p><a href="https://docs.oracle.com/javase/7/docs/technotes/guides/security/spec/security-spec.doc4.html">Access Control Mechanisms and Algorithms</a></p>

<p>当调用 <code class="language-plaintext highlighter-rouge">AccessController.checkPermission(...)</code> 的时候,检查的内容即是 <code class="language-plaintext highlighter-rouge">AccessControlContext</code> 的内容<br />
当新线程创建的时候,原有的线程里的 AccessControlContext 不会被继承</p>

<h1 id="keytool">keytool</h1>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c"># 以下两个命令完全一样,其中 -gencert 仅作为历史原因保留 </span>
keytool <span class="nt">-genkeypair</span> 
keytool <span class="nt">-gencert</span>
</code></pre></div></div>

<h1 id="jarsigner">jarsigner</h1>

<p><a href="https://docs.oracle.com/javase/7/docs/technotes/tools/windows/jarsigner.html">jarsigner</a></p>

<div class="language-shell highlighter-rouge"><div class="highlight"><pre class="highlight"><code>jarsigner <span class="nt">-keystore</span> &lt;keystore path&gt; <span class="nt">-storepass</span> &lt;keystore password&gt; <span class="nt">-keypass</span> &lt;private key password&gt; MyJar.jar
</code></pre></div></div>

<p>被签名的 jar 和原来的 jar 内容上完全一样,除了多了一个文件: <code class="language-plaintext highlighter-rouge">META-INF/MANIFEST.MF</code></p>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="0000-01-01T08:00:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/0000/01/01/douyu.html">Douyu</a></div><div class="next"><span>下篇</span><a href="/0000/01/01/jdk.html">JDK</a></div></div></div>

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