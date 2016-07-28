---
title: Emmet-vim CSS 写法
author: 陈 三
layout: post
date: 2011-07-22T01:46:44+00:00
url: /zencoding-vim-html-css.html
dsq_thread_id:
  - 461554854
views:
  - 2598
categories:
  - 前端开发
tags:
  - css
  - emmet
  - html
  - vim
  - zencoding
  - zencoding.vim

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 附录</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 修订历史</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    Emmet（原来叫 Zen Coding） 通过按键触发来展开缩写词。
  </p>
  
  <p>
    在 Vim 下，使用 <a href="https://github.com/mattn/emmet-vim" title="emmet for vim 代码库">Emmet-vim</a> 编辑 CSS 文件，首先需要检查文件类型，
  </p>
  
  <pre><code>:set ft?
</code></pre>
  
  <p>
    如果显示结果不是 <code>filetype=css</code>，则需要先设定文件类型：
  </p>
  
  <pre><code>:set ft=css
</code></pre>
  
  <p>
    然后你就可以开始写 CSS 规则。
  </p>
  
  <p>
    比如要给 <code>body</code> 写一个 <code>margin-right:10px;</code>，则可以在 Vim 输入：
  </p>
  
  <pre><code>mr10
</code></pre>
  
  <p>
    然后按触发键，默认为 <kbd>Ctrl+y,</kbd>。
  </p>
  
  <p>
    又或者要给 <code>div</code> 块加一个 <code>position:absolute;</code>，则可以输入：
  </p>
  
  <pre><code>pos:a
</code></pre>
  
  <p>
    然后按触发键。
  </p>
  
  <p>
    接下来要给 <code>div</code> 增加 <code>top:20px;right:10px;</code>，
  </p>
  
  <pre><code>t20+r10
</code></pre>
  
  <p>
    然后按触发键。
  </p>
  
  <p>
    很简单吧。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">附录</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      Zen Coding 站上的 <a href="https://zen-coding.googlecode.com/files/ZenCodingCheatSheet.pdf">Cheatsheet</a> 提供有更多缩略词列表
    </li>
    <li>
      <a href="http://docs.emmet.io/css-abbreviations/">Emmet 上关于 CSS 扩展的说明</a>
    </li>
  </ol>
  
  <div class='timeline'>
    <h2 class="storycontent-h2">
      <span id="i-2">修订历史</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
    </h2>
    
    <ol>
      <li>
        <span itemprop='dateModified'>2015-06-17</span>：修改 zencoding.vim 为 emmet-vim。
      </li>
    </ol>
  </div>
</div>