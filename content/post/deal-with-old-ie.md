---
title: 我对 IE6、7的态度
author: 陈 三
layout: post
date: 2013-08-07T13:46:14+00:00
url: /deal-with-old-ie.html
views:
  - 687
categories:
  - 前端开发
tags:
  - ie6

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 现实</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#IE67"><span class="toc_number toc_depth_1">2</span> IE6、7背后的逻辑</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <h2 class="storycontent-h2">
    <span id="i">现实</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    现实是，因为某种原因，IE6、7在中国浏览器市场上，还<a href="http://www.ie6countdown.com/">占有不少份额</a>。没有几家互联网行业公司可以绕开它们，我们从事前端开发的，也就必须面对它们。
  </p>
  
  <p>
    我看过不少人在他们的博客分享 IE6、7的问题或解决办法，评论里就有人说，IE6 这么古老的东西，早该放弃，不必要纠结。我猜想这些人大概不做前端开发，又或者他们的公司不要求兼容低版本 IE 浏览器。这是幸事，但也不必要因此说责他人。我想没几个前端开发人员喜欢调试 IE6、7，大概是工作需要，所以不得已要面对。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="IE67">IE6、7背后的逻辑</span><a title="标题链接地址" class="u-floatRight hidden" id="heyIE67" href="#IE67"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    浮动时双边距是什么逻辑？IE6 自动扩展包含块又是什么逻辑？&#8230;&#8230;
  </p>
  
  <p>
    在我开始接触这些所谓 IE 浏览器 Bug 时，我很努力想了解它们背后的逻辑。因为我私以为，了解它们背后的逻辑，才能更好地解决问题。但后来我发现，自己错了。这些非标准背后，也许有其逻辑，但它的逻辑相对于标准来说，只能是“非逻辑”。谁来告诉我，IE6、7下，margin 与 padding 为什么会存在消失或合并的问题？也许 IE 的开发者们知道，但他们不曾解释。
  </p>
  
  <p>
    我现在改变想法，不再试图了解 IE6、7 Bug 背后的逻辑。我觉得我要做的，是利用各种已知或试验可行的 hack 技术，保证页面与标准的相近 &#8211; 这就够了。
  </p>
</div>