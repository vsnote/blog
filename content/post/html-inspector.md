---
title: HTML Inspector
author: 陈 三
layout: post
date: 2015-04-20T13:28:20+00:00
url: /html-inspector.html
views:
  - 500
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
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 用法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 定制</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    ​我们写 CSS、写 JavaScript，通常都会用到 CSSLint、JSHint 这类工具，用于辅助​检查我们代码中的错误或糟糕部分。比起人类的粗枝大叶，通常工具要靠谱多了。
  </p>
  
  <p>
    <a href="https://github.com/philipwalton/html-inspector">HTML Inspector</a> 是一个类似的工具，当然，它并不是用来检查我们 HTML 代码书写是否规范、是否标签未关闭这种事情。我们知道，HTML 代码里充斥着各种勾子，CSS 样式化的类名，JavaScript 选择器 ID 等等，HTML Inspector 可以帮忙检查，我们的代码是否符合最佳实践，或者说我们自己定义的最佳实践。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">用法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在要检查的 HTML 页面中 <code>&lt;/body&gt;</code> 前引用 HTML Inspector 代码并立即执行：
  </p>
  
  <pre><code>&lt;script src="//cdnjs.cloudflare.com/ajax/libs/html-inspector/0.8.2/html-inspector.js"&gt;&lt;/script&gt;
&lt;script&gt;
      HTMLInspector.inspect();
&lt;/script&gt;
</code></pre>
  
  <p>
    当然，我也可以使用 npm 或 bower 来安装。
  </p>
  
  <p>
    之后刷新该 HTML 页面，就可以在 console（浏览器控制台）里看到当前 HTML 页面的报告，比如：
  </p>
  
  <blockquote>
    <script> elements should appear right before the closing </body> tag for optimal performance.
  </blockquote>
  
  <p>
    根据这类提示，我们可以对 HTML 代码做诸多改进。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">定制</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    HTML Inspector 允许你自己定制规则，可以想到，一个团队如果有某些代码上的规范，则可以落实到规则中，这样项目成员都可以自行检测代码中不合规范的部分，保证代码风格统一及规范。
  </p>
</div>