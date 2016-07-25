---
title: AngularJS 转换 RGBA、ARGB
author: 陈 三
layout: post
date: 2013-08-16T12:49:00+00:00
url: /angularjs-rgba-argb-converter.html
dsq_thread_id:
  - 1747474424
views:
  - 468
categories:
  - 前端开发
tags:
  - Angularjs

---
在 [IE6/7/8 实现 RGBA][1] 一篇，我写了个[工具][2]，用来转换 RGBA、ARGB。

当时用 jQuery 实现，写了不少事件函数；后来换 AngularJS 实现，代码相对简洁，如下：

<div ng-app>
  <div ng-controller="helloAngularjs">
    <pre ng-style="bg()">
.bg-transparent{
  background:transparent; /* fallback */
  background:{{rgba||"rgba(0,0,0,.5)"}}; /* 现代浏览器 */
}
.lt-ie9 .bg-transparent{
  -ms-filter: "progid:DXImageTransform.Microsoft.gradient(GradientType=1, StartColorStr='{{argb||"#7F000000"}}', EndColorStr='{{argb||"#7F000000"}}')"; /* IE8 */ 
}
.lt-ie8 .bg-transparent{
  filter: progid:DXImageTransform.Microsoft.Gradient(GradientType = 1, StartColorStr = '{{argb||"#7F000000"}}', EndColorStr = '{{argb||"#7F000000"}}'); /* IE6、7 */ 
  zoom: 1; /* 针对 IE6、IE7 的 hack */
}
</pre> 将上面生成的代码块拷入 CSS 文件即可使用。
  </div>
</div>

<div class='timeline'>
  <h2>
    修订历史
  </h2>
  
  <ol>
    <li>
      <span itemprop='dateModified'>2015-06-26</span>：修改样式
    </li>
  </ol>
</div>

 [1]: http://www.zfanw.com/blog/ie6-ie7-ie8-rgba.html
 [2]: http://www.zfanw.com/tools/argb-rgba.html