---
title: 再谈浏览器缓存
author: 陈 三
layout: post
date: 2016-07-08T05:32:04+00:00
url: /browser-cache.html
views:
  - 111
categories:
  - 前端开发

---
一个页面上的资源，可以简单分为两种：

  1. url 可变，比如这个页面上的 css 文件，这次可能是 app.fe5a24f8ae.css，下次可能是 app.613e5f58f1.css
  2. url 不可能变，比如这个页面的 url

针对它们，我们的缓存方式可以不同。

比如第一种，我们可以这样设置响应头：

> Cache-Control max-age=31536000, must-revalidate

表示这个资源一年内都有效，过期的话才要到服务器上验证。

那么，我们如何保证资源修改后能及时更新到用户端？修改 url 即可。

而针对第二种，因为 url 无法改变，我们就需要另外的方式。

比如：

> Cache-Control no-cache

`no-cache` 不是表示不能缓存，而是说每次浏览器都要跟服务器做个确认 &#8211; 通过 `ETag` 或 `Last-Modified`，这样就会多出一个请求 。

## 扩展阅读

  1. [Caching best practices & max-age gotchas &#8211; JakeArchibald.com][1]

 [1]: https://jakearchibald.com/2016/caching-best-practices/