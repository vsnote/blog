---
title: Adobe Brackets 与 CSS DRY 原则
author: 陈 三
layout: post
date: 2013-09-08T11:17:28+00:00
excerpt: 如何利用 Adobe Brackets 快速编辑工具有效组织我们的 CSS 代码
url: /adobe-brackets-css-dont-repeat-youself.html
dsq_thread_id:
  - 1744972212
views:
  - 460
categories:
  - 前端开发
tags:
  - Adobe Brackets
  - css

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 快速编辑</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 妙用</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    在后端程序里，随处可见强调 <a href="http://zh.wikipedia.org/wiki/一次且仅一次">DRY</a>(don&#8217;t repeat youself) 原则，我想前端开发中也不应该例外。
  </p>
  
  <p>
    一个样式类，在 CSS 文件中多处出现，就会造成后期修改的困难。谁也不能保证，我多处都做好修改。但如果我们只定义一次，就很容易确信，我们已经修改好了。
  </p>
  
  <p>
    那么，我们又如何确定自己只定义了一次？
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">快速编辑</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Adobe Brackets 的 <a href="https://github.com/adobe/brackets/wiki/How-to-Use-Brackets#quick-edit">Quick Edit</a>(<strong>快速编辑</strong>样式) 工具可以很好地帮助解决这个问题。
  </p>
  
  <p>
    在 Brackets 中，打开 HTML 文件，光标定位到类名位置，然后按 <kbd>Ctrl-E</kbd> 快捷键，就会在当前 HTML 编辑窗口内调出快速样式编辑面板：
  </p>
  
  <p>
    <img src="http://www.zfanw.com/blog/wp-content/uploads/2013/09/adobe-brackets-quick-edit.jpg" alt="adobe brackets 快速编辑" width="700" height="114" class="alignnone size-full wp-image-10399" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/09/adobe-brackets-quick-edit.jpg 700w, https://www.zfanw.com/blog/wp-content/uploads/2013/09/adobe-brackets-quick-edit-300x48.jpg 300w" sizes="(max-width: 700px) 100vw, 700px" />
  </p>
  
  <p>
    面板分左右两列，左列显示样式规则，右列显示所有定义有该样式的 CSS 文件名称、代码位置。
  </p>
  
  <p>
    比如上图中，我定义了一个 <code>.rom-comment-num</code> 的类，该类出现在 main.css 样式文件中，并且出现了两次。当类出现在许多样式文件中，或者在一个样式文件中出现多处，我们就要认真考虑一下，我们是否正在违背 DRY 原则，正在给我们的后期维护制造困难。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">妙用</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    上面我们已经知道快速编辑样式怎么用，这样，从中就能延展出一个不错的用处。
  </p>
  
  <p>
    当我们给 CSS 类命名时，即便有一定的规范在，我们也会担心，这个命名是不是已经被定义过了？毕竟，页面一多，参与开发的人一多，谁也不好保证这种问题。这时按快捷键 <kbd>Ctrl-E</kbd>，如果没能调出快速编辑面板，则该类名还没有被用过，我们可以放心使用。当然，Firebug 之类的网页调试工具也可以达到这种功能，但毕竟不如在编辑器中确认来得方便。
  </p>
</div>