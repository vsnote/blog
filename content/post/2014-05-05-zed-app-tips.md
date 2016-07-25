---
title: Zed使用小贴士
author: 陈 三
layout: post
date: 2014-05-05T11:14:50+00:00
url: /zed-app-tips.html
views:
  - 428
categories:
  - 未分类
tags:
  - Zed
  - 编辑器

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 创建新文件</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 打开文件</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    Zed文档里，有一些细节没有写出来，最后往往会在Github issues上，以问题的形式出现。答案均出自Zed作者，因为我也碰到过，所以略作整理。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">创建新文件</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    按<kbd>Ctrl-e</kbd>调出goto UI后，输入一个当前项目下不存在的文件名即可创建一个新文件。但是，这个新文件的位置是<strong>项目根目录</strong>。
  </p>
  
  <p>
    而大部分时候，我们是想在当前编辑的文件同一级目录下创建新文件。
  </p>
  
  <p>
    有一个快速输入当前编辑的文件的路径的方法：
  </p>
  
  <ol>
    <li>
      <kbd>Ctrl-e</kbd>调出goto UI
    </li>
    <li>
      按空格键自动补全当前编辑文件的路径
    </li>
  </ol>
  
  <h2 class="storycontent-h2">
    <span id="i-2">打开文件</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <kbd>Ctrl-e</kbd>调出goto UI后，输入你要编辑的文件名称。但这里有一个细节，即goto UI只会在文件名称里查找，不会在文件夹名称里查找。
  </p>
  
  <p>
    如果你打算编辑 wp-content/themes/zfanw/index.php 文件，却只输入<code>zfanw index</code>是不行的。文件夹部分，需要在后面跟上 “/”，比如 <code>zfanw/index</code> 这样，才能正确定位到该文件。
  </p>
</div>