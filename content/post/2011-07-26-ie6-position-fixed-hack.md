---
title: IE6 的固定定位
author: 陈 三
layout: post
date: 2011-07-26T08:09:26+00:00
url: /ie6-position-fixed-hack.html
dsq_thread_id:
  - 458449192
views:
  - 1484
categories:
  - 前端开发
tags:
  - css
  - ie6

---
IE6 不支持**固定定位**，它会把 `position:fixed` 理解成 `position:static`，本该固定定位的块仍处于正常流中。

解决办法是通过 `position:absolute`。

     html.lt-ie7,
    .lt-ie7 body{
        background-image:url(about:blank);
        background-attachment:fixed;
    }
    .lt-ie7 .fixMeTopPlease{
        position:absolute;
        left:0;
        top:expression(eval(document.documentElement.scrollTop));
    }
    

这样，我们就可以在 IE6 下模仿出固定定位效果。

## 附录

  1. [ie6 fixed position gist][1]

 [1]: https://gist.github.com/subtleGradient/158243