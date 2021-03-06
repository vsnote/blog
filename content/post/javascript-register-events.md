---
title: JavaScript 事件注册方法
author: 陈 三
layout: post
date: 2013-01-06T03:42:53+00:00
url: /javascript-register-events.html
views:
  - 694
dsq_thread_id:
  - 1010668934
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
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 行内方法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 传统注册方法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 现代注册方法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">4</span> 参考</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    出于一些历史遗留原因，JavaScript 的事件注册(绑定)方法有多种。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">行内方法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    这是最古老的方法，由 Netscape 引入，因为当时 Netscape 在浏览器市场的影响很大，IE 只能跟随，也因此这个方法最为通用，基本没有浏览器兼容性的问题。
  </p>
  
  <p>
    它在 HTML 元素的事件属性中直接绑定：
  </p>
  
  <pre><code>&lt;a href="http://www.zfanw.com/blog/" onclick="alert('hey it's me.');"&gt;....&lt;/a&gt;
</code></pre>
  
  <p>
    这种方法的好处是没有浏览器不兼容问题，但是我们将 JavaScript 代码混入了 HTML 中，这不合「行为与结构分离」的原则，会给我们带来很多麻烦。所以一般不会推荐这种用法。
  </p>
  
  <p>
    在上例中，如果点击链接，则会有两个动作发生，一个是弹出对话框，一个是在当前标签页/窗口打开链接，两个动作的发生顺序也是由当时的 Netscape 决定的：
  </p>
  
  <ol>
    <li>
      绑定的事件函数将先执行，在本例子中，会先弹出对话框；
    </li>
    <li>
      打开链接，即 a 元素的默认动作
    </li>
  </ol>
  
  <p>
    如果要阻止默认动作，则是在绑定的 JavaScript 事件处理函数中返回一个 false 值，
  </p>
  
  <pre><code>    &lt;a href="http://www.zfanw.com/blog/" onclick="alert('hey it's me.');return false"&gt;....&lt;/a&gt;
</code></pre>
  
  <p>
    这样点击链接就只会弹出窗口，而不打开链接。
  </p>
  
  <p>
    但显然不是所有的默认动作都允许 JavaScript 阻止，比如用户关闭页面而触发的 unload 动作，如果能被阻止，用户就连页面都关不掉，JavaScript 不会有这种蠢问题。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">传统注册方法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    所谓传统，是相对于现代浏览器的方法而言的。这种方法仍是由 Netscape 引入，IE 被迫跟随。
  </p>
  
  <p>
    比如：
  </p>
  
  <pre><code>window.onload = doSomething;
</code></pre>
  
  <p>
    但这种方法有个问题，就是同一个元素的同一个事件只能注册一个函数，如果你再为之注册一个函数，则后面的会覆盖掉前面一个。
  </p>
  
  <p>
    另外，这种注册方法只支持事件冒泡，不支持捕获 &#8211; 这是事件执行顺序的两种阶段，具体可以看参考6中 W3 上的详述。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">现代注册方法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    W3C 很认真地推出新的事件注册方法想解决传统方法的问题。不可避免的是，Microsoft 又横出一脚，有自己的新的注册方法 &#8211; 直到 IE9 它才支持 W3C 的方法。于是这里要分为两种方法。
  </p>
  
  <h3>
    W3C DOM 事件注册方法
  </h3>
  
  <p>
    语法为：
  </p>
  
  <pre><code>target.addEventListener(type, listener[, useCapture]);
</code></pre>
  
  <p>
    target 为绑定事件的对象，type 为事件的类型，比如 click、dbclick 等，listener 即绑定的事件处理函数，useCapture 为一个布尔值，指定事件处理是在哪个阶段发生，其默认值为 false，事件注册在冒泡阶段。
  </p>
  
  <p>
    如果要绑定多个事件处理函数，则重复调用 addEventListener 方法则可，不会出现后来定义的覆盖前面的问题。
  </p>
  
  <h3>
    Microsoft 事件注册方法
  </h3>
  
  <p>
    在 IE9 之前，需要使用 IE 自有的事件注册方法 attachEvent，
  </p>
  
  <pre><code>object.attachEvent(event, pDisp) 
</code></pre>
  
  <p>
    其中 event 为事件类型，类似于 W3C 定义的方法里 type 的意思，但是又有所区别，它是带有 「on」 的，比如 「onclick」，而 W3C 定义里是没有的。pDisp 指绑定的事件处理函数。
  </p>
  
  <p>
    另外，attachEvent 方法有一个缺陷，它把 <code>this</code> 绑定到 window 对象上，而非调用它的对象上。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">参考</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://www.quirksmode.org/js/events_early.html">Early events handler</a>
    </li>
    <li>
      <a href="http://www.quirksmode.org/js/events_tradmod.html">Javascript &#8211; Traditional event registration model</a>
    </li>
    <li>
      <a href="http://www.quirksmode.org/js/events_advanced.html">Javascript &#8211; Advanced event registration models</a>
    </li>
    <li>
      <a href="https://developer.mozilla.org/en-US/docs/DOM/element.addEventListener">element.addEventListener &#8211; Document Object Model (DOM) | MDN</a>
    </li>
    <li>
      <a href="https://en.wikipedia.org/wiki/DOM_events">DOM events &#8211; Wikipedia, the free encyclopedia</a>
    </li>
    <li>
      <a href="http://www.w3.org/TR/DOM-Level-3-Events/#dom-event-architecture">Document Object Model (DOM) Level 3 Events Specification</a>
    </li>
  </ol>
</div>