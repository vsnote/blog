---
title: Bootstrap ScrollSpy 用法
author: 陈 三
layout: post
date: 2012-09-01T12:49:59+00:00
url: /bootstrap-scrollspy.html
views:
  - 3811
dsq_thread_id:
  - 826723116
categories:
  - 前端开发
tags:
  - bootstrap
  - jQuery
  - scrollspy

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 用法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 调试</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <h2 class="storycontent-h2">
    <span id="i">用法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Twitter Bootstrap 的 <a href="http://getbootstrap.com/javascript/#scrollspy">ScrollSpy 插件有两种用法</a>：
  </p>
  
  <ol>
    <li>
      <p>
        通过 data 属性
      </p>
      
      <p>
        根据情况，给需要监视的页面元素添加 <code>data-spy="scroll"</code> &#8211; 一般是 body 元素，并且通过 <code>data-target</code> 属性指定目标：
      </p>
      
      <pre><code>&lt;body data-spy="scroll" data-target=".navbar"&gt;...&lt;/body&gt;
</code></pre>
    </li>
    
    <li>
      <p>
        通过 Javascript 语句
      </p>
      
      <pre><code>$('#navbar').scrollspy()
</code></pre>
    </li>
  </ol>
  
  <p>
    举一个例子，如下：
  </p>
  
  <p>
    监控的导航部分 HTML 代码：
  </p>
  
  <pre><code>&lt;div class="bs-docs-sidebar"&gt;
    &lt;ul class="nav"&gt;
        &lt;li&gt;&lt;a href="#one"&gt;hello Bootstrp 3&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href="#two"&gt;hello jQuery&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href="#three"&gt;hello ScrollSpy&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
&lt;/div&gt;
</code></pre>
  
  <p>
    导航相对应的内容部分代码：
  </p>
  
  <pre><code>&lt;div&gt;
    &lt;h2 id="one"&gt;This is one.&lt;/h2&gt;
    &lt;p&gt;......&lt;/p&gt;
    &lt;h2 id="two"&gt;This is two.&lt;/h2&gt;
    &lt;p&gt;......&lt;/p&gt;
    &lt;h2 id="three"&gt;This is three.&lt;/h2&gt;
    &lt;p&gt;......&lt;/p&gt;
&lt;/div&gt;
</code></pre>
  
  <p>
    上述代码里，我们点击导航部分的锚链接可以直接跳转到相应的内容部分，这是这最基本的 HTML 结构。
  </p>
  
  <p>
    最重要的，导航代码中 <code>ul</code> 含有一个 CSS 类 <code>.nav</code>，它是必需的，没有的话就会导致插件无效果。
  </p>
  
  <p>
    应用第一个方法，在 body 元素添加相关属性：
  </p>
  
  <pre><code>&lt;body data-spy="scroll" data-target=".bs-docs-sidebar"&gt;
</code></pre>
  
  <p>
    <code>data-target</code> 属性指向的是 class 为 <code>bs-docs-sidebar</code> 的 <code>div</code> 块。
  </p>
  
  <p>
    第二种办法，使用 JavaScript：
  </p>
  
  <pre><code>$(function(){
    $('.bs-docs-sidebar').scrollspy();
})
</code></pre>
  
  <p>
    Bootstrap 文档推荐第一种方法，因为不用任何的 JavaScript 语句即可实现 ScrollSpy 效果。
  </p>
  
  <p>
    附：<a href="http://jsfiddle.net/chenxsan/ZgPbZ/">jsfiddle 示例</a>
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">调试</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    如果你的 ScrollSpy 不起作用，则有一个简单的调试办法，利用 <a href="https://addons.mozilla.org/en-us/firefox/addon/firequery/">fireQuery</a>：
  </p>
  
  <p>
    <a href="http://www.zfanw.com/blog/wp-content/uploads/2012/09/Screenshot-from-2013-06-07-010738.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2012/09/Screenshot-from-2013-06-07-010738.png" alt="fireQuery" width="505" height="57" class="alignnone size-full wp-image-9063" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/09/Screenshot-from-2013-06-07-010738.png 505w, https://www.zfanw.com/blog/wp-content/uploads/2012/09/Screenshot-from-2013-06-07-010738-300x33.png 300w" sizes="(max-width: 505px) 100vw, 505px" /></a>
  </p>
  
  <p>
    上图是安装 fireQuery 后打开 firebug 面板 HTML 标签页里的截图，因为 fireQuery 会将 jQuery 事件等附加在 HTML 代码中，所以我们可以清楚地看到如下一条规则，
  </p>
  
  <pre><code>selector=".bs-docs-sidebar .nav li &gt; a"
</code></pre>
  
  <p>
    如果你的导航部分 HTML 结构与它不一样，则说明 jQuery 找不到它要的元素，也就没法生成效果，解决办法是调整代码结构。
  </p>
</div>