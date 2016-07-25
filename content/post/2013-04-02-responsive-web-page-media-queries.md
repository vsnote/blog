---
title: 自适应网页
author: 陈 三
layout: post
date: 2013-04-01T16:44:55+00:00
url: /responsive-web-page-media-queries.html
dsq_thread_id:
  - 1179866433
views:
  - 513
categories:
  - 前端开发

---
CSS3 引入的[媒体查询][1]功能在设计自适应网页时非常方便。但是很可惜，IE6-8 并不支持这个功能。

不过解决办法还是有的：[Respond.js][2]。

用法很简单，只要在所有的 CSS 规则后引用 respond.js 文件即可，这样 `@media...` 书写的 CSS 规则将同样对 IE6-8 生效。

在 [html5boilerplate][3] 中，也提供有这个方法的[自由选配][4]。

 [1]: https://developer.mozilla.org/en-US/docs/CSS/Media_queries "媒体查询"
 [2]: https://github.com/scottjehl/Respond "respond.js"
 [3]: http://html5boilerplate.com/
 [4]: http://www.initializr.com/ "通过 initializr 自由定制 html5 样板"