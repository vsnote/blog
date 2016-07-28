---
title: 防止布局振荡
author: 陈 三
layout: post
date: 2014-07-05T07:15:00+00:00
url: /prevent-layout-thrashing.html
views:
  - 564
categories:
  - 前端开发
tags:
  - JavaScript
  - 前端性能

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 快速解决办法？</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 现实世界又如何？</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#requestAnimationFrame"><span class="toc_number toc_depth_1">3</span> 来认识requestAnimationFrame</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    原文地址：<a href="http://wilsonpage.co.uk/preventing-layout-thrashing/">Preventing &#8216;layout thrashing&#8217; | Wilson Page</a>
  </p>
  
  <p>
    最近接触页面性能的东西，有很多细微又原始的内容，比如浏览器渲染。资料非常多，所以选一些做节译，备忘。
  </p>
  
  <hr />
  
  <p>
    JavaScript多次写、读DOM就会发生「布局振荡」，引起文档重排<fnref target="13021.2" />(reflow &#8211; the process of constructing a render tree from a DOM tree<fnref target="13021.1" />)。
  </p>
  
  <pre><code>// 读
var h1 = element1.clientHeight;

// 写 (布局作废)
element1.style.height = (h1 * 2) + 'px';

// 读 (触发布局)
var h2 = element2.clientHeight;

// 写 (布局作废)
element2.style.height = (h2 * 2) + 'px';

// 读 (触发布局)
var h3 = element3.clientHeight;

// 写 (布局作废)
element3.style.height = (h3 * 2) + 'px';
</code></pre>
  
  <p>
    DOM被写时，布局就作废了，需要在某个时间点重排。但浏览器很懒，它想等到当前操作(或说帧)结束前再来重排。
  </p>
  
  <p>
    不过，如果我们在当前操作(或说帧)结束前从DOM中读取几何数值，那么我们就强制浏览器提前重排布局，这就是所谓的「强制同步布局」(forced synchonous layout)，它会要了性能的命。
  </p>
  
  <p>
    在现代的桌面浏览器上，布局振荡的副作用可能并不明显；但放到低端移动设备上，问题就很严重了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">快速解决办法？</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在一个理想世界里，我们只要简单地重新排列代码执行顺序，就可以批量读DOM、批量写DOM。这意味着，文档只需一次重排。
  </p>
  
  <pre><code>// 读
var h1 = element1.clientHeight;
var h2 = element2.clientHeight;
var h3 = element3.clientHeight;

// 写 (布局作废)
element1.style.height = (h1 * 2) + 'px';
element2.style.height = (h2 * 2) + 'px';
element3.style.height = (h3 * 2) + 'px';

// 文档在帧末重排
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i-2">现实世界又如何？</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    现实中可就没那么简单。大型程序中，代码散播各处，个个都存在这类危险的DOM。我们没法轻松(显然也不应该)把我们漂亮的、解藕的代码揉合一块，就只是为了控制住执行顺序。那么为了优化性能，我们怎样把读和写做批量处理？
  </p>
  
  <h2 class="storycontent-h2">
    <span id="requestAnimationFrame">来认识requestAnimationFrame</span><a title="标题链接地址" class="u-floatRight hidden" id="heyrequestAnimationFrame" href="#requestAnimationFrame"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <code>window.requestAnimationFrame</code>安排一个函数在下一帧执行，类似于<code>setTimout(fn, 0)</code>。这非常有用，因为我们可以用它来排定所有的DOM写操作在下一帧一同执行，DOM读操作就按现在的顺序同步执行。
  </p>
  
  <pre><code>// 读
var h1 = element1.clientHeight;

// 写
requestAnimationFrame(function() {
  element1.style.height = (h1 * 2) + 'px';
});

// 读
var h2 = element2.clientHeight;

// 写
requestAnimationFrame(function() {
  element2.style.height = (h2 * 2) + 'px';
});
</code></pre>
  
  <p>
    &#8230;&#8230;
  </p>
  
  <footnotes>
    <fn name="13021.2">
      <p>
        注意，重排不要理解成中文的「重新排布」，而是「布局」、「布置」的意思，确切说，reflow是webkit的说法，layout是Gecko的说法。
      </p>
    </fn>
    
    <fn name="13021.1">
      <p>
        <a href="http://gent.ilcore.com/2011/03/how-not-to-trigger-layout-in-webkit.html">Fastersite: How (not) to trigger a layout in WebKit</a>
      </p>
    </fn>
  </footnotes>
</div>