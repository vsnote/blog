---
title: JavaScript 同源策略
author: 陈 三
layout: post
date: 2013-11-01T11:52:58+00:00
url: /javascript-same-origin-policy.html
dsq_thread_id:
  - 2008874624
views:
  - 1209
categories:
  - 前端开发
tags:
  - ajax
  - JavaScript
  - XMLHttpRequest

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 同源的定义</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 同源策略的内容</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    最近大量用 ajax，自然要面对跨域问题。什么是跨域？先来定义同源。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">同源的定义</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    同源指两个网页，它们的协议（protocal）、端口（port）和主机（host）一致。
  </p>
  
  <p>
    比如下面这两个网页：
  </p>
  
  <ol>
    <li>
      http://www.example.com/sam.html
    </li>
    <li>
      https://www.example.com/sam.html
    </li>
  </ol>
  
  <p>
    它们的协议不一，一个是 <code>http</code>，一个是 <code>https</code>，所以不同源。同理可推端口、主机。
  </p>
  
  <p>
    <strong>不同源，即跨域。</strong>
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">同源策略的内容</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    同源策略是出于安全考虑设计的，那么，它具体指什么？
  </p>
  
  <p>
    MDN 上是<a href="https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy">这样说的</a>：
  </p>
  
  <blockquote>
    <p>
      The same-origin policy restricts how a document or script loaded from one origin can interact with a resource from another origin.
    </p>
  </blockquote>
  
  <p>
    “同源策略限制了一个域的文档或脚本如何与另一个域的资源交互”。
  </p>
  
  <p>
    啥？我们可以分几种情况说明。
  </p>
  
  <h3>
    读取资源
  </h3>
  
  <p>
    我们通常说的跨域，多是针对 XMLHttpRequest &#8211; ajax 技术的基础之一。
  </p>
  
  <p>
    假设我在本地搭建了一个服务器环境，网址是 <code>http://localhost/</code>，主页 <code>index.html</code> 中有一段 JavaScript 代码如下：
  </p>
  
  <pre><code>$(function(){
   $.get('sam.html',function(data){
       $('body').html(data)
   })
})
</code></pre>
  
  <p>
    <code>sam.html</code> 文件位于 <code>index.html</code> 同一文件夹下。结果显示，我们成功 <code>GET</code> 到 <code>sam.html</code> 文件的内容。
  </p>
  
  <p>
    那么再尝试一下，从本地 GET 远程文件如何。这里代码中加入一个对照组：
  </p>
  
  <pre><code>$(function(){
   $.get('http://www.zfanw.com/?12132313232',function(data){
       $('body').html(data);
   });
    $.get('sam.html',function(data){
        console.log(data);
    })
});
</code></pre>
  
  <p>
    我们看看 Google Chrome 30.0.1599.114 控制台下的情况：
  </p>
  
  <p>
    <a href="https://www.zfanw.com/blog/wp-content/uploads/2013/10/google-chrome-console-log.png"><img src="https://www.zfanw.com/blog/wp-content/uploads/2013/10/google-chrome-console-log.png" alt="google chrome 控制台信息" width="493" height="48" class="alignnone size-full wp-image-10878" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/10/google-chrome-console-log.png 493w, https://www.zfanw.com/blog/wp-content/uploads/2013/10/google-chrome-console-log-300x29.png 300w" sizes="(max-width: 493px) 100vw, 493px" /></a>
  </p>
  
  <p>
    Google Chrome 控制台报错了：
  </p>
  
  <blockquote>
    <p>
      XMLHttpRequest cannot load http://www.zfanw.com/?12132313232. Origin http://127.0.0.1 is not allowed by Access-Control-Allow-Origin.
    </p>
  </blockquote>
  
  <p>
    因为 <code>http://localhost</code> 与 <code>http://www.zfanw.com</code> 不同源，所以浏览器会禁止来自 localhost 的脚本访问跨域资源。
  </p>
  
  <p>
    这很容易理解，你家里当然不会允许陌生人随便进去，要进，得要你邀请了才行。Chrome 控制台中提到的 <code>Access-Control-Allow-Origin</code>，正是我们邀请其它域的脚本访问的方法，具体用法请看 <a href="http://enable-cors.org/">enable cross-origin resource sharing 网站的说明</a>。
  </p>
  
  <h3>
    写入
  </h3>
  
  <p>
    跨域写入的情况可以参照读取部分的说明，这也是时下非常常见的，比如我有一个 API 服务器部署在另一个域名下，但我依然可以通过 ajax 请求将数据存储到 API 服务器中，只要我们在 <code>Access-Control-Allow-Origin</code> 中许可了来自其它源的请求。
  </p>
  
  <h3>
    执行
  </h3>
  
  <p>
    出于安全考虑，同源策略默认不允许源 A 的脚本读取源 B 的资源，但却允许执行源 B 的资源。
  </p>
  
  <p>
    这个概念也有些拗⼝。
  </p>
  
  <p>
    简单说，我这个博客，调用了 Google CDN 提供的 jQuery，它的源显然与我的博客不同，但我却可以用它来操作我的博客页面 DOM，它也可以读取我的 cookie、localStorage 等。
  </p>
  
  <p>
    假设一个场景，Google CDN 上的 jQuery 被注入了恶意代码，或者被劫持，指向另一个带有恶意代码的 jQuery，则引用它的网站就很危险了，因为这恶意 jQuery 现在可以读取我们网站的内容，并且向其它地方写入。
  </p>
</div>