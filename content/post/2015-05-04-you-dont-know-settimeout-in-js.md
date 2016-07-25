---
title: 你不知道 setTimeout 是怎么回事
author: 陈 三
layout: post
date: 2015-05-04T11:54:52+00:00
url: /you-dont-know-settimeout-in-js.html
views:
  - 667
categories:
  - 前端开发
tags:
  - JavaScript
  - setTimeout

---
在我查找 JavaScript setTimeout 相关资料时，看到这一段测试代码[^15831.1]：

    setTimeout(function(){console.log('a');},5);
    var then = (new Date()).getTime(), now;
    do { now = (new Date()).getTime(); } while (now < (then + 5));
    setTimeout(function(){console.log('b');},0);
    

如果照 JavaScript 单线程的思路看，则 log 的顺序应该是：

  1. a
  2. b

在 Safari 8.0.5（Mac） 与 Google Chrome 42.0.2311.135 (64-bit)（Mac）上确实如此。

但让人吃惊的是，Firefox 37.0.2 上 log 出的顺序却是相反的：

[resp_image id=&#8217;15892&#8242; caption=&#8221; ]

测试过 IE11 上的表现是跟 Firefox 一样的。

[^15831.1]:    
    [Bringing setTimeout to ECMAScript][1]

 [1]: https://mail.mozilla.org/pipermail/es-discuss/2011-March/013276.html