---
title: JavaScript setTimeout 居然立即执行了
author: 陈 三
layout: post
date: 2015-05-06T04:15:33+00:00
url: /javascript-settimeout-fire-immediately.html
views:
  - 976
categories:
  - 前端开发
tags:
  - JavaScript
  - setTimeout

---
在我的经历里，有过类似以下的一段代码：

    setTimeout(function() { console.log('sam chen'); }, 2591700000);
    

Ooooooops，立即执行了。而不是我们所预想的，会在至少 2591700000ms 后触发。

原因是这样的[^15918.1]：

> Timeout values too big to fit into a signed 32-bit integer may cause overflow in FF, Safari, and Chrome, resulting in the timeout being scheduled immediately. It makes more sense simply not to schedule these timeouts, since 24.8 days is beyond a reasonable expectation for the browser to stay open.

`setTimeout` 的第二个参数 timeout 的最大值是 2147483647[^15918.2]，我们的设定值超过它，回调函数就会立即执行。

[^15918.1]:    
    [closure timer.js &#8211; code.google.com][1]

[^15918.2]:    
    [最大/最小延迟值 &#8211; MDN][2]

 [1]: https://code.google.com/p/closure-library/source/browse/closure/goog/timer/timer.js?r=7205c0d2f9ef6e079ba626e3c83d93dddf65de67#79
 [2]: https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setTimeout#Minimum.2Fmaximum_delay_and_timeout_nesting