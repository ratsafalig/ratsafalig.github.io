---
title: VS Code Edge Debugger
date: 2021-02-26 00:00:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="VS Code Edge Debugger"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2021-02-26T08:00:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="VS Code Edge Debugger" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-02-26T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="VS Code Edge Debugger" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2021-02-26T08:00:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><div class="language-json highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="p">{</span><span class="w">
    </span><span class="err">//</span><span class="w"> </span><span class="err">Use</span><span class="w"> </span><span class="err">IntelliSense</span><span class="w"> </span><span class="err">to</span><span class="w"> </span><span class="err">learn</span><span class="w"> </span><span class="err">about</span><span class="w"> </span><span class="err">possible</span><span class="w"> </span><span class="err">attributes.</span><span class="w">
    </span><span class="err">//</span><span class="w"> </span><span class="err">Hover</span><span class="w"> </span><span class="err">to</span><span class="w"> </span><span class="err">view</span><span class="w"> </span><span class="err">descriptions</span><span class="w"> </span><span class="err">of</span><span class="w"> </span><span class="err">existing</span><span class="w"> </span><span class="err">attributes.</span><span class="w">
    </span><span class="err">//</span><span class="w"> </span><span class="err">For</span><span class="w"> </span><span class="err">more</span><span class="w"> </span><span class="err">information</span><span class="p">,</span><span class="w"> </span><span class="err">visit:</span><span class="w"> </span><span class="err">https://go.microsoft.com/fwlink/?linkid=</span><span class="mi">830387</span><span class="w">
    </span><span class="nl">"version"</span><span class="p">:</span><span class="w"> </span><span class="s2">"0.2.0"</span><span class="p">,</span><span class="w">
    </span><span class="nl">"configurations"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="w">
        </span><span class="p">{</span><span class="w">
            </span><span class="nl">"type"</span><span class="p">:</span><span class="w"> </span><span class="s2">"edge"</span><span class="p">,</span><span class="w">
            </span><span class="nl">"request"</span><span class="p">:</span><span class="w"> </span><span class="s2">"launch"</span><span class="p">,</span><span class="w">
            </span><span class="nl">"name"</span><span class="p">:</span><span class="w"> </span><span class="s2">"Edge"</span><span class="p">,</span><span class="w">
            </span><span class="nl">"webRoot"</span><span class="p">:</span><span class="w"> </span><span class="s2">"${workspaceFolder}/src"</span><span class="p">,</span><span class="w">
            </span><span class="nl">"url"</span><span class="p">:</span><span class="w"> </span><span class="s2">"http://localhost:1234"</span><span class="p">,</span><span class="w">
            </span><span class="nl">"version"</span><span class="p">:</span><span class="w"> </span><span class="s2">"dev"</span><span class="w">
        </span><span class="p">}</span><span class="w">
    </span><span class="p">]</span><span class="w">
</span><span class="p">}</span><span class="w">
</span></code></pre></div></div>

<p><img src="/assets/3/vscode-edge-debugger/QQ截图20210226214322.png" alt="" /></p>

<p><img src="/assets/3/vscode-edge-debugger/QQ截图20210226214432.png" alt="" /></p>

<p><img src="/assets/3/vscode-edge-debugger/QQ截图20210226214502.png" alt="" /></p>

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
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2021/02/26/bilibili-danmu.html">Bilibili DanMu 弹幕</a></div><div class="next"><span>下篇</span><a href="/2021/03/02/unity-persistance.html">Unity 持久化</a></div></div></div>

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