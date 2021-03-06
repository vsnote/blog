---
title: 使用 YUI3 网格的注意事项
author: 陈 三
layout: post
date: 2013-07-23T11:44:23+00:00
url: /yui3-css-grid.html
dsq_thread_id:
  - 1522940145
views:
  - 572
categories:
  - 前端开发
tags:
  - ie6
  - ie7
  - inline-block
  - YUI3

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#letter-spacing"><span class="toc_number toc_depth_1">1</span> letter-spacing 取值</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#IE67"><span class="toc_number toc_depth_1">2</span> IE6、7次像素问题</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 参考</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <h2 class="storycontent-h2">
    <span id="letter-spacing">letter-spacing 取值</span><a title="标题链接地址" class="u-floatRight hidden" id="heyletter-spacing" href="#letter-spacing"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <a href="http://yui.yahooapis.com/3.10.3/build/cssgrids/cssgrids.css">YUI3 网格</a> 使用 <code>display:inline-block;</code> 布局网页。
  </p>
  
  <p>
    inline-block 元素间存在间隙，这间隙由空白符引起，而空白符的宽度又由字体集决定，YUI3 使用 <code>letter-spacing</code>、<code>word-spacing</code> 消除间隙：
  </p>
  
  <pre><code>.yui3-g {
    letter-spacing: -0.31em; /* Webkit: collapse white-space between units */
    *letter-spacing: normal; /* reset IE &lt; 8 */
    *word-spacing: -0.43em; /* IE &lt; 8: collapse white-space between units */
    text-rendering: optimizespeed; /* Webkit: fixes text-rendering: optimizeLegibility */
}

/* Opera as of 12 on Windows needs word-spacing.
   The ".opera-only" selector is used to prevent actual prefocus styling
   and is not required in markup.
*/
.opera-only :-o-prefocus,
.yui3-g {
    word-spacing: -0.43em;
}

.yui3-u {
    display: inline-block;
    zoom: 1; *display: inline; /* IE &lt; 8: fake inline-block */
    letter-spacing: normal;
    word-spacing: normal;
    vertical-align: top;
    text-rendering: auto;
}
</code></pre>
  
  <p>
    但 YUI3 中，<code>letter-spacing</code>、<code>word-spaceing</code> 取值基于字体集 Arial，这就有一种可能：一旦类定义的字体集被覆写，有可能破坏布局。
  </p>
  
  <p>
    比如：
  </p>
  
  <pre><code>&lt;div class="yui3-g main"&gt;
    &lt;div class="yui3-u-1-2 bgc-r"&gt;red background&lt;/div&gt;
    &lt;div class="yui3-u-1-2 bgc-g"&gt;green background&lt;/div&gt;
&lt;/div&gt;
&lt;div class="yui3-g main-mirror"&gt;
    &lt;div class="yui3-u-1-2 bgc-r"&gt;red background&lt;/div&gt;
    &lt;div class="yui3-u-1-2 bgc-g"&gt;green background&lt;/div&gt;
&lt;/div&gt;
&lt;style&gt;
    .bgc-r {
        background:red;
    }
    .bgc-g {
        background:green;
    }
    .main-mirror {
        font-family:Courier;
    }
&lt;/style&gt;
</code></pre>
  
  <p>
    因为 <code>.yui3-g</code> 的 <code>font-family</code> 被 <code>.main-mirror</code> 覆写，本该并列的第二列却脱落到下一行：
  </p>
  
  <p>
    我们显然无法保证自己或他人不会覆写 <code>.yui3-g</code> 的字体集，这种不可预测性，会造成麻烦。
  </p>
  
  <p>
    目前，在这个问题上，还没有银子弹存在。
  </p>
  
  <p>
    一个妥协办法，是强制声明 <code>.yui3-g</code> 字体集为默认。
  </p>
  
  <pre><code>.yui3-g{font-family: Arial;}
</code></pre>
  
  <p>
    然后在 <code>yui3-u</code> 及 <code>yui3-u-*-*</code> 中声明我们要使用的字体：
  </p>
  
  <pre><code>.yui3-u,
.yui3-u-1,
.yui3-u-1-2,
.yui3-u-1-3,
.yui3-u-2-3,
.yui3-u-1-4,
.yui3-u-3-4,
.yui3-u-1-5,
.yui3-u-2-5,
.yui3-u-3-5,
.yui3-u-4-5,
.yui3-u-1-6,
.yui3-u-5-6,
.yui3-u-1-8,
.yui3-u-3-8,
.yui3-u-5-8,
.yui3-u-7-8,
.yui3-u-1-12,
.yui3-u-5-12,
.yui3-u-7-12,
.yui3-u-11-12,
.yui3-u-1-24,
.yui3-u-5-24,
.yui3-u-7-24,
.yui3-u-11-24,
.yui3-u-13-24,
.yui3-u-17-24,
.yui3-u-19-24,
.yui3-u-23-24 {
  font-family: 宋体,Arial;
}
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="IE67">IE6、7次像素问题</span><a title="标题链接地址" class="u-floatRight hidden" id="heyIE67" href="#IE67"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    IE6、7浏览器下，0.5~1的像素会四舍五入成1像素，破坏流式布局。
  </p>
  
  <p>
    举个例子，301宽度的块，定义两个子块，类名为 <code>.yui3-u-1-2</code>，在 IE6、7下，右侧子块会掉落，而不是并排:
  </p>
  
  <p>
    解决办法见<a href="http://tylertate.com/blog/2012/01/05/subpixel-rounding.html">这个链接</a>。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">参考</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="https://github.com/yui/pure/issues/41">grids spacing wrong without Arial on pure-g, pure-g-r</a>
    </li>
    <li>
      <a href="http://yuilibrary.com/projects/yui3/ticket/2533215">CSS Grid 2 column layout, columns not appearing side by side.</a>
    </li>
    <li>
      <a href="https://github.com/csswizardry/inuit.css/issues/170">Inline-block and white space in the grid</a>
    </li>
    <li>
      <a href="http://yuilibrary.com/yui/environments/">YUI 支持的浏览器</a>
    </li>
  </ol>
</div>