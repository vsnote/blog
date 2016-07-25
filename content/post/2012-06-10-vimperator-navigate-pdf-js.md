---
title: Vimperator 下使用 pdf.js
author: 陈 三
layout: post
date: 2012-06-10T14:34:55+00:00
url: /vimperator-navigate-pdf-js.html
views:
  - 1604
dsq_thread_id:
  - 720085459
categories:
  - vimperator
tags:
  - pdf.js
  - vimperator

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_pdfjs"><span class="toc_number toc_depth_1">1</span> 安装 pdf.js</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_pdfjsjs"><span class="toc_number toc_depth_1">2</span> 安装 pdf.js.js</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 使用方法</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    在 twitter 上看到 <a href="https://twitter.com/#!/anekos">@anekos</a> さん发的 <a href="http://vimperator.g.hatena.ne.jp/nokturnalmortum/20120610/1339333950">pdf.js.js 推文链接</a>，不巧以前就对 pdf.js 在 Vimperator 下的导航有些不满，就安装试用了下 pdf.js.js，功能简洁方便，略作介绍。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_pdfjs">安装 pdf.js</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_pdfjs" href="#_pdfjs"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    下载地址：<a href="https://addons.mozilla.org/ja/firefox/addon/pdfjs/">https://addons.mozilla.org/ja/firefox/addon/pdfjs/</a>
  </p>
  
  <p>
    pdf.js 是 Firefox 插件，可以让你直接在 Firefox 中打开 pdf 文件，省去安装其他 pdf 阅读软件的麻烦。据称 Firefox 14 版本中将内建它的功能。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_pdfjsjs">安装 pdf.js.js</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_pdfjsjs" href="#_pdfjsjs"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    下载地址：<a href="https://github.com/vimpr/vimperator-plugins/blob/master/PDF.js.js">https://github.com/vimpr/vimperator-plugins/blob/master/PDF.js.js</a>
  </p>
  
  <p>
    将其放到 vimperator/plugin 文件夹下，重启 Firefox 即可。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">使用方法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <kbd>j</kbd> &#8211; 向下滚动页面
  </p>
  
  <p>
    <kbd>k</kbd> &#8211; 向上滚动页面
  </p>
  
  <p>
    <kbd>n</kbd> &#8211; 翻到下一页
  </p>
  
  <p>
    <kbd>p</kbd> &#8211; 翻到上一页
  </p>
  
  <p>
    <kbd>gg</kbd> &#8211; 翻到第一页
  </p>
  
  <p>
    <kbd>count gg</kbd> &#8211; 第 count 页
  </p>
  
  <p>
    还有一个命令 <code>:pdfjs</code> 可以在 Vimperator 的命令行模式中使用。
  </p>
  
  <p>
    它有两个参数，index 与 zoom，index 跳转到某一页面，zoom 用于设置页面缩放。
  </p>
  
  <p>
    于是，pdf.js 提供的功能都可以通过命令完成。
  </p>
</div>