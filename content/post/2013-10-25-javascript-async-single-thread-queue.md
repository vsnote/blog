---
title: JavaScript 的异步、单线程和队列
author: 陈 三
layout: post
date: 2013-10-25T12:55:50+00:00
url: /javascript-async-single-thread-queue.html
dsq_thread_id:
  - 2008890923
views:
  - 1280
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
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 异步计时函数</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_IO"><span class="toc_number toc_depth_1">2</span> 异步 I/O 函数</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">3</span> 扩展阅读</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    这是我第一次明白 JavaScript 的异步、单线程、队列这几个概念，感谢 <a href="http://pragprog.com/book/tbajs/async-javascript">Async JavaScript</a> 一书。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">异步计时函数</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    首先从异步计时函数 setTimeout 说起：
  </p>
  
  <pre><code>var begin = new Date();//代码开始
setTimeout(function(){
    var end = new Date();
    alert('陈三你好，这个程序已经运行了' + (end - begin) + '毫秒');
},1000);//1秒后弹出对话框
while ((new Date() - begin) &lt; 2000) {}//循环代码持续2秒
</code></pre>
  
  <p>
    在 firefox 下，按 <kbd>Shift + F4</kbd> 调出代码片段速记器，将以上代码拷入，然后 <kbd>Ctrl - R</kbd> 运行。
  </p>
  
  <p>
    我的某次数值是 2019。
  </p>
  
  <p>
    这个数值让我大吃一惊，不是说好 1 秒后弹对话框的吗？
  </p>
  
  <p>
    如果我们是在多线程程序语言下，那我们的期望是对的。但 JavaScript 是单线程，这就与我们的期望有出入。
  </p>
  
  <p>
    单线程是什么意思？
  </p>
  
  <p>
    JavaScript 从 <code>var begin = new Date();</code> 执行起，然后解析 setTimout 函数。setTimout 一段代码表示，嘿，请在 1 秒后，把我加入事件队列里。之后回调函数排队等候。
  </p>
  
  <p>
    JavaScript 继续运行下一句 &#8211; 在这个例子中是 while 循环。这个循环要持续2秒。这期间，回调函数继续在排队。
  </p>
  
  <p>
    这就是单线程设计下的 JavaScript。队列里的回调函数不会主动发问，它只是被动等待。等 JavaScript 忙完最后一句代码，JavaScript 虚拟机就会朝队列喊话：下一个。
  </p>
  
  <p>
    这时，我们的 <code>alert</code> 终于可以运行了 &#8211; 但时间已经过去 2019 毫秒。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_IO">异步 I/O 函数</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_IO" href="#_IO"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    现代常用的 Ajax 操作属于异步 I/O 类型，比如 GET、POST。
  </p>
  
  <pre><code>$.get('http://www.zfanw.com/blog/',function(data){//因为 JavaScript 的同源策略，本地执行本语句其实会失败，仅做示例
        alert(data);
    });
while (true) {}
</code></pre>
  
  <p>
    JavaScript 在执行到 get 语句时，发起 HTTP 请求，要求返回 http://www.zfanw.com/blog/ 页面，并且定义一个回调函数，将回调加入事件队列，以便 HTTP 响应成功时接收数据，然后 JavaScript 继续执行下一句，即 while，因为 while 条件一直为真，所以程序将永远运行下去，此前定义的回调函数一直在排队，页面呈假死状态。
  </p>
  
  <p>
    当然，这个例子有点极端，举一个轻松点的，本地服务器上架设的例子：
  </p>
  
  <pre><code>$.get('index.html',function(data){
        alert(data);
    });
alert('hey Chen');
</code></pre>
  
  <p>
    代码执行到 &#8216;hey Chen&#8217; 一句，浏览器弹出对话框窗口。
  </p>
  
  <p>
    且慢关掉对话框窗口，打开 Google Chrome 开发者工具查看 Network 选项卡，get 语句的 <a href="http://www.w3.org/TR/XMLHttpRequest/#the-statustext-attribute">Status Text</a> 字段正处在 Pending 状态中。<a href="https://developers.google.com/chrome-developer-tools/">chrome 开发者工具帮助上并没有说明这个词的意思</a>，但我们可以借助 <a href="http://www.wireshark.org/">WireShark</a> 或 <a href="http://fiddler2.com/">Fiddler2</a> 检查 HTTP 请求的状况：
  </p>
  
  <p>
    <a href="http://www.zfanw.com/blog/wp-content/uploads/2013/10/wireshark-log-http.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2013/10/wireshark-log-http.png" alt="wireshark 抓取 http 数据" width="631" height="256" class="alignnone size-full wp-image-10799" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/10/wireshark-log-http.png 631w, https://www.zfanw.com/blog/wp-content/uploads/2013/10/wireshark-log-http-300x121.png 300w" sizes="(max-width: 631px) 100vw, 631px" /></a>
  </p>
  
  <p>
    上图中可以看到，请求 &#8211; 响应过程是成功的，只是 get 定义的回调未能执行，所以 Chrome 下显示成 Pending 状态。现在我们按下对话框窗口的确定按钮，又或关掉对话框，回调函数就执行了。
  </p>
  
  <p>
    以上是 Google Chrome 30.0.1599.114 版本下的情况，即 alert 方法会阻止事件循环，导致回调无法接收数据。
  </p>
  
  <p>
    Firefox 24 下的情况略有不同，示例3中的 alert 并不能阻止事件循环，两个 ajax 请求全部执行并且回调也执行了，这样页面上会有三个弹出对话框。
  </p>
  
  <p>
    WireShark 抓取的 Firefox 下 HTTP 数据如图：
  </p>
  
  <p>
    <a href="http://www.zfanw.com/blog/wp-content/uploads/2013/10/wireshark-log-http-firefox.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2013/10/wireshark-log-http-firefox.png" alt="wireshark log firefox http" width="534" height="106" class="alignnone size-full wp-image-10800" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/10/wireshark-log-http-firefox.png 534w, https://www.zfanw.com/blog/wp-content/uploads/2013/10/wireshark-log-http-firefox-300x59.png 300w" sizes="(max-width: 534px) 100vw, 534px" /></a>
  </p>
  
  <p>
    当然，浏览器的处理方法不同这种事情实在不值得我大惊小怪，毕竟，我是从 IE6 混战里活过来的(笑。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">扩展阅读</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://msdn.microsoft.com/en-us/hh549259">Introduction to HTML5 Web Workers</a>
    </li>
    <li>
      <a href="http://stackoverflow.com/questions/7104474/how-does-asynchronous-javascript-execution-happen-and-when-not-to-use-return-st">How does Asynchronous Javascript Execution happen</a>
    </li>
  </ol>
</div>