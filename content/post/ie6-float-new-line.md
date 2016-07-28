---
title: IE6 下的浮动换行问题
author: 陈 三
layout: post
date: 2013-05-12T04:13:44+00:00
url: /ie6-float-new-line.html
dsq_thread_id:
  - 1282032521
views:
  - 396
categories:
  - 前端开发
tags:
  - css
  - html
  - ie6

---
如下 HTML 代码：

    <p>
    <a href="#">普通的行内元素</a>
    <a href="#">普通的行内元素</a>
    <a href="#" class="fl-r">普通的行内元素 - 右浮动</a>
    </p>
    

CSS 样式如下：

    .fl-r{float:right;}
    

在现代浏览器下，它会显示成一行，但 IE6 下，右浮动的元素显示在新一行，这样 `p` 元素的高度就增加了，如下图：

<div id="attachment_8911" style="width: 563px" class="wp-caption alignnone">
  <a href="http://www.zfanw.com/blog/wp-content/uploads/2013/05/ie6-float-new-line.jpg"><img src="http://www.zfanw.com/blog/wp-content/uploads/2013/05/ie6-float-new-line.jpg" alt="ie6 浮动换行" width="553" height="55" class="size-full wp-image-8911" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/05/ie6-float-new-line.jpg 553w, https://www.zfanw.com/blog/wp-content/uploads/2013/05/ie6-float-new-line-300x29.jpg 300w" sizes="(max-width: 553px) 100vw, 553px" /></a>
  
  <p class="wp-caption-text">
    ie6 浮动换行
  </p>
</div>

解决办法有多个，比如：

  1. 将前两个 a 元素左浮动
  2. 将 p 元素相对定位 `position:relative`，并且将最后一个 a 绝对定位

但这两种办法多少都有些过头，最简单的方法，将右浮动的元素提到最前：

    <p>
    <a href="#" class="fl-r">普通的行内元素 - 右浮动</a>
    <a href="#">普通的行内元素</a>
    <a href="#">普通的行内元素</a>
    </p>
    

这样 IE6 下它们就显示在同一行。