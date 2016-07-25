---
title: Jekyll 目录树
author: 陈 三
layout: post
date: 2014-11-13T00:22:24+00:00
excerpt: Jekyll 生成目录树
url: /jekyll-table-of-content.html
views:
  - 1139
categories:
  - 前端开发
tags:
  - Jekyll

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_kramdown"><span class="toc_number toc_depth_1">1</span> 启用 kramdown</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_TOC"><span class="toc_number toc_depth_1">2</span> 生成 TOC</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    如你所见，我的这个博客里，稍长点的文章，都会生成目录树（Table of Content），并且配合有 Bootstrap 的 <a href="http://www.zfanw.com/blog/twitter-bootstrap-affix-js.html">affix</a>、<a href="http://www.zfanw.com/blog/bootstrap-scrollspy.html">ScrollSpy</a> 效果。同样地，在 Jekyll 构建的静态博客上，我一样想生成目录树。
  </p>
  
  <p>
    Jekyll 的 Plugins 页面中有提到一个插件 <a href="https://github.com/dafi/jekyll-toc-generator">jekyll-toc-generator</a>，但其实没有必要使用插件，因为 Jekyll 的 Markdown 渲染器 <a href="http://kramdown.gettalong.org/converter/html.html#toc">kramdown</a> 已经具备这个功能。我们只需要启用它即可。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_kramdown">启用 kramdown</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_kramdown" href="#_kramdown"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    打开 _config.yml 文件，确保以下一行存在：
  </p>
  
  <pre><code>markdown: kramdown
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="_TOC">生成 TOC</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_TOC" href="#_TOC"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    接下来是在文章中标识 toc 的生成位置：
  </p>
  
  <pre><code>* 目录
{:toc}

# 陈三

## 陈三的博客
</code></pre>
  
  <ol>
    <li>
      请注意，<em>* 目录</em>这一行是必需的，它表示目录树列表，至于星号后面写什么请随意
    </li>
    <li>
      如果要把某标题从目录树中排除，则在该标题的下一行写上 <code>{:.no_toc}</code>
    </li>
    <li>
      目录深度可以通过 <em>config.yml</em> 文件中添加 <em>toc_levels</em> 选项来定制，默认为 <code>1..6</code>，表示标题一至标题六全部渲染
    </li>
    <li>
      <code>{:toc}</code> 默认生成的目录列表会添加 id 值 <em>markdown-toc</em>，我们可以自定义 id 值，比如 <code>{:toc #chenxsan}</code>，生成的目录列表添加的 id 将会是 <em>chenxsan</em>。
    </li>
  </ol>
  
  <p>
    最后生成的 <a href="http://www.linuxcoo.com/2014/11/20/check-linux-release-distribution.html">toc 样式</a>。
  </p>
</div>