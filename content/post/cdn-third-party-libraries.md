---
title: CDN 提供的第三方库
author: 陈 三
layout: post
date: 2013-04-23T02:27:42+00:00
url: /cdn-third-party-libraries.html
dsq_thread_id:
  - 1229792163
views:
  - 574
categories:
  - 前端开发
tags:
  - CDN
  - jQuery

---
我博客上使用的 jQuery 是托管在 [Google CDN][1] 上的所谓第三方库。好处？老实说，以我博客这种流量，即是有好处，大概能感受到的也微乎其微。但从技术上说，确实有好处，我就不妨用上。

[html5boilerplate][2] 提供的模板里，调用 Google CDN 上的 jQuery 库语句是这样写的：

    <script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
    <script>window.jQuery || document.write('<script src="js/vendor/jquery-1.9.1.min.js"><\/script>')</script>
    

先说第一个语句。

第一个语句中，没有 `http:`，这是因为你的页面还可能是加密的(SSL)，`//ajax.googleapis....` 这样的形式可以在 http/https 页面通用，在 http 页面加载 http 版本的 jQuery，https 页面加载 https 版本的 jQuery，无须我们再做额外调整。

但使用 `//` 有一个问题，就是开发时如果使用 file:// 路径则第三方库将无法加载。

第二个语句是为 fallback，在无法加载 CDN 上的 jQuery 时，页面就不存在 window.jQuery 对象，这时页面自动到你的网站服务器上读取文件。

但使用第三方库有个安全问题，一旦第三方库的托管服务器被人侵入，你的网站就非常危险了。所以最好不要随便使用不知名站点托管的第三方库。

 [1]: https://developers.google.com/speed/libraries/devguide
 [2]: http://html5boilerplate.com/