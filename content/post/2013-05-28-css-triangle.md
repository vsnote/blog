---
title: CSS 画三角形
author: 陈 三
layout: post
date: 2013-05-28T05:05:07+00:00
url: /css-triangle.html
dsq_thread_id:
  - 1329007273
views:
  - 993
categories:
  - 前端开发
tags:
  - css

---
使用 CSS 画三角形？第一感觉不太可能。但那是对 border 有一点误会。

来看一个示例：

<div style="width:100px;
    height:100px;
    background-color:black;
    border-top:50px solid red;
    border-right:50px solid green;
    border-bottom:50px solid blue;
    border-left:50px solid orange;">
</div>

它的 HTML 代码如下：

    <div style="width:100px;
        height:100px;
        background-color:black;
        border-top:50px solid red;
        border-right:50px solid green;
        border-bottom:50px solid blue;
        border-left:50px solid orange;">
    </div>
    

我们需要注意，**边框相接的地方**，**即相邻边框的样式**。因为我们平时使用边框，一般只几像素宽，所以可以不注意它们相接的样式，但当边框达到50像素宽，就可以清楚看到，它们在相接时是如何处理的 &#8211; 这是 CSS 实现三角形的原理。

可以想像到，把 div 块的宽、高设为0将是如下样子：

<div style="width:0;
    height:0;
    background-color:black;
    border-top:50px solid red;
    border-right:50px solid green;
    border-bottom:50px solid blue;
    border-left:50px solid orange;">
</div>

这时，CSS 画三角形的做法就非常清楚。

比如，我要用 CSS 实现倒三角形，只要将下边框设为无，左、右边框颜色设为透明：

<div style="width:0;
    height:0;
    background-color:none;
    border-left:50px solid transparent;
    border-right:50px solid transparent;
    border-bottom:none;
    border-top:50px solid red;">
</div>

代码如下：

    <div style="width:0;
        height:0;
        background-color:none;
        border-left:50px solid transparent;
        border-right:50px solid transparent;
        border-bottom:none;
        border-top:50px solid red;">
    </div>
    

其他方向的三角形同理可以实现。