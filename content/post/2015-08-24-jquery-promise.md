---
title: jQuery 的 Promise 实现
author: 陈 三
layout: post
date: 2015-08-24T13:06:13+00:00
excerpt: jQuery 在 3.0 版本中实现 Promises/A+ 定义的规范。
url: /jquery-promise.html
views:
  - 689
categories:
  - 前端开发
tags:
  - jQuery

---
早几年，我就看到 Promises/A 的作者在[咆哮][1]，说 jQuery 实现的 Promise 完全是狗屁。但当时的我，能写出

    $.post(url, {}, null, 'json').then(function(data) {}, function(err) {});
    

这样的语句就十分满意了，才不管 jQuery 的 then 里究竟能不能[处理错误][2]。

但 jQuery 终于要在 [3.0 版本中支持 Promises/A+ 了][3]，对我来说，就是代码里不再需要用 Q.js

    Q($.post()).then(func, func)
    

包装 jQuery 的 ajax 请求了。

 [1]: https://blog.domenic.me/youre-missing-the-point-of-promises/
 [2]: https://github.com/kriskowal/q/wiki/Coming-from-jQuery
 [3]: http://blog.jquery.com/2015/07/13/jquery-3-0-and-jquery-compat-3-0-alpha-versions-released/