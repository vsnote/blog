---
title: 滚动网页到某一位置后固定
author: 陈 三
layout: post
date: 2012-09-21T12:12:19+00:00
url: /jquery-scroll-fixed-position.html
views:
  - 1615
dsq_thread_id:
  - 853221326
categories:
  - 前端开发
tags:
  - jQuery
  - scrollTop

---
现在网页常见这一种用法，一个导航条在 Logo 部分下面，网页往下滚动，当到达导航条位置时，导航条即固定在页面顶部。比如 我这篇[Firefox OS 内容][1]右侧目录块。

技术上实现很简单，首先，将该目录内容用 CSS 固定，

    #toc_container{position:fixed;top:100px;}
    

这样，页面载入时 #toc_container 块就固定在视窗范围内，离顶部距离 100 像素的位置。

接下来是 jQuery 语句：

    $(window).scroll(function(){
        $("#toc_container").css("top",Math.max(0,100-$(this).scrollTop()));
    });
    

scrollTop() 是 一个 jQuery 函数，用于取得 jQuery 对象滚动出可视窗口顶部边界外的距离：

> The vertical scroll position is the same as the number of pixels that are hidden from view above the scrollable area. If the scroll bar is at the very top, or if the element is not scrollable, this number will be 0.
Math.max 函数用于取得最大值，在目录滚动出窗口顶部之前，100-$(this).scrollTop() 的结果大于 0，于是 top 取它的值，因为 top 值一直在减小，所以虽然该目录 position 为 fixed，视觉上就好像该目录并不固定在页面上，直到 Math.max 取值为 0，这时目录内容的 top 值固定为 0。

## 鸣谢

  1. <http://stackoverflow.com/questions/5902822/stopping-fixed-position-scrolling-at-a-certain-point>
  2. <http://api.jquery.com/scrollTop/>
  3. <https://developer.mozilla.org/en-US/docs/DOM/element.scrollTop>

 [1]: http://www.zfanw.com/blog/firefox-os.html