---
title: JavaScript debounce
author: 陈 三
layout: post
date: 2013-11-28T22:05:50+00:00
excerpt: 防止 JavaScript 事件频繁、重复触发
url: /javascript-debounce.html
dsq_thread_id:
  - 2008560165
views:
  - 1232
categories:
  - 前端开发
tags:
  - JavaScript

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 点击后禁用按钮</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Debounce"><span class="toc_number toc_depth_1">2</span> Debounce</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#throttle"><span class="toc_number toc_depth_1">3</span> throttle</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">4</span> 扩展阅读</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    页面有一个按钮，点击一次可以触发一个 ajax 请求。如果不做特殊处理，那么，快速点击时就会触发大量多余 ajax 请求。
  </p>
  
  <p>
    处理方法有多种。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">点击后禁用按钮</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    简单粗暴，在用户第一次点击后即禁用按钮。在处理完 ajax 请求后，再启用该按钮。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="Debounce">Debounce</span><a title="标题链接地址" class="u-floatRight hidden" id="heyDebounce" href="#Debounce"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    维基上 debounce 译成<a href="http://zh.wiktionary.org/wiki/debounce">去除抖動</a>。我们可以把用户迅速点击造成的大量事件触发看成「信号的抖动」 &#8211; 这时信号还不稳定。
  </p>
  
  <p>
    debounce 的原理是，事件触发时，事件处理器延迟执行(setTimeout)，比如 100 毫秒，如果 100 毫秒内没有再触发事件，则可以认为信号稳定，事件处理器可以在预计的 100 毫秒【当然，这个时间并不准确，有兴趣可以看 <a href="http://www.zfanw.com/blog/javascript-async-single-thread-queue.html">JavaScript 异步一篇的说明</a>】内执行，但如果 100 毫秒内，比如等到 99 毫秒，又进来一个同样的事件，则上一个事件处理器被取消，新的事件处理器替补进来，并且重新开始延迟计时。
  </p>
  
  <p>
    举一个点击按钮提交 ajax 请求的例子<fnref target="11100.1" />：
  </p>
  
  <pre><code>$('#fav').on('click',function () {
    var timer = null;
    return function () {
        clearTimeout(timer); // 新进入的事件处理器清除上一个定时的事件处理器
        timer = setTimeout(function () { // 启动新的延时
            $.ajax({...});
        }, 100);
    }
});
</code></pre>
  
  <p>
    这个方法有一个明显的缺陷，就是用户正常点击时，事件的处理也被无例外地推迟 100 毫秒。
  </p>
  
  <p>
    不过，<a href="http://underscorejs.org/docs/underscore.html#section-83">underscore</a> 等类库提供了另一种 debounce 方式：第一个事件发生时，马上执行我们要执行的函数，第二次函数要想执行，则必须在上一个事件发生 x 秒之后。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="throttle">throttle</span><a title="标题链接地址" class="u-floatRight hidden" id="heythrottle" href="#throttle"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <a href="https://www.google.com/search?q=define+throttle&ie=utf-8&oe=utf-8&aq=t&rls=org.mozilla:en-US:official&client=firefox-a">throttle</a> 的定义是：
  </p>
  
  <blockquote>
    <p>
      a device controlling the flow of fuel or power to an engine.
    </p>
  </blockquote>
  
  <p>
    在这里，可以简单理解成一个控制函数发生频率的机制。
  </p>
  
  <p>
    与 debounce 不同的是，throttle 方法不会延迟第一次事件的处理。它即时处理第一次事件，并记录时间，之后再发生事件，它再计算一个时间值，这个时间值表示，离第一次事件发生过去了多久，如果这个时间值小于设定的时间阀(threshold)，则利用 setTimeout 推迟事件处理，一旦到达时间阀，则即时触发事件处理。
  </p>
  
  <p>
    这样，throttle 就控制住密集事件可触发事件处理器的频率，比如每 200 秒仅触发一个事件函数。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">扩展阅读</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <footnotes>
    <fn name="11100.1">
      <p>
        <a href="https://css-tricks.com/debouncing-throttling-explained-examples/">Debouncing and Throttling Explained Through Examples | CSS-Tricks</a>
      </p>
    </fn>
  </footnotes>
</div>