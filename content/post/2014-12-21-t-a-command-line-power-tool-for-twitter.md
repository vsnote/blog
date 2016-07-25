---
title: t – twitter 的命令行界面客户端
author: 陈 三
layout: post
date: 2014-12-20T16:02:37+00:00
excerpt: twitter 的命令行界面客户端 t 的安装使用
url: /t-a-command-line-power-tool-for-twitter.html
views:
  - 621
categories:
  - openSUSE
tags:
  - t
  - Twitter

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_t"><span class="toc_number toc_depth_1">1</span> 安装 t</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_t-2"><span class="toc_number toc_depth_1">2</span> 认证 t</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_Twitter_App"><span class="toc_number toc_depth_1">3</span> 创建 Twitter App</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    这篇讲 Twitter 的 CLI（command-line interface） 应用 <strong>t</strong>，是我安装使用中碰上的问题总结。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_t">安装 t</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_t" href="#_t"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    t<fnref target="14785.1" /> 是一个 gem 包，所以你需要事先安装 Ruby 和 RubyGems。准备就绪后：
  </p>
  
  <pre><code>$ sudo gem install t
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="_t-2">认证 t</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_t-2" href="#_t-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <pre><code>$ t authorize -d
</code></pre>
  
  <h3>
    问题
  </h3>
  
  <ul>
    <li>
      <p>
        <code>t: command not found</code>
      </p>
      
      <p>
        因为 gem 安装路径的问题，你可能碰上 t 命令找不到的情况。可以使用 <code>gem env</code> 查看 gem 安装路径，然后直接切换到 t 的路径执行 <code>./t authorize</code>。
      </p>
    </li>
    
    <li>
      <p>
        关于 <code>-d</code> 参数
      </p>
      
      <p>
        上面使用了 <code>-d</code> 参数，这是因为我的 openSUSE 13.2　里，t 在命令行下无法打开浏览器网页的缘故，它会报一个错<fnref target="14785.2" />：
      </p>
      
      <blockquote>
        <p>
          xprop: unable to open display &#8221;
        </p>
      </blockquote>
      
      <p>
        使用 <code>-d</code> 参数可以在终端里生成 URL 地址，以便拷贝到浏览器中。
      </p>
    </li>
  </ul>
  
  <h2 class="storycontent-h2">
    <span id="_Twitter_App">创建 Twitter App</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Twitter_App" href="#_Twitter_App"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    你需要根据提示，在 Twitter Application Management<fnref target="14785.3" /> 创建一个 app，生成 t 需要的 API Key 及 API Secret。
  </p>
  
  <p>
    验证后期，还会需要一个 PIN 码。正常情况下，t 会打开一个 twitter 网址，非正常情况，就需要你手动拷贝那个认证 URL 到浏览器，生成一个 PIN 码，然后根据 t 的要求填入，即可完成认证。
  </p>
  
  <footnotes>
    <fn name="14785.1">
      <p>
        <a href="https://github.com/sferik/t">sferik/t 源代码</a>
      </p>
    </fn>
    
    <fn name="14785.2">
      <p>
        <a href="https://github.com/sferik/t/issues/216">认证时无法打开浏览器 · Issue #216 · sferik/t</a>
      </p>
    </fn>
    
    <fn name="14785.3">
      <p>
        <a href="https://apps.twitter.com">Twitter Application Management</a>
      </p>
    </fn>
  </footnotes>
</div>