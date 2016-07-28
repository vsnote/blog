---
title: 垂直居中对齐浮动的元素
author: 陈 三
layout: post
date: 2013-05-23T15:03:31+00:00
url: /vertical-center-float-element.html
dsq_thread_id:
  - 1310484214
views:
  - 1041
categories:
  - 前端开发
tags:
  - css
  - html

---
类似如下的 HTML 代码非常常见：

    <h1>你好标题一<span><a href="#" title="查看更多">查看更多</a></span></h1>
    

这里，`span` 部分是右浮动的，字体也比较小，我们需要它与其他文本在垂直方向上对齐。

有几个办法很容易想到的办法：

  1. 给右浮动的 span 元素设置 padding-top 或 margin-top 值；
  2. 绝对定位右浮动的 span 元素

但这两种办法在我来看，动作都有些大。一个我认为清爽的做法是，给 span 元素设置 line-height 值。

假定如下 h1 样式：

    h1{
        font-size:18px;
        line-height:1.5;
    }
    

我们可以计算出，h1 的行框高度为 18*1.5=27px，这样，我们将 span 元素的 line-height 设置为27px，CSS 会扣除 span 的 font-size 值，并对半开后分别添加到 span 上/下空间里，

    span{
        float:right;
        font-size:12px;
        line-height:27px;
    }
    

这样就很轻松达到垂直方向上对齐文本的效果。

附：[jsfiddle 示例][1]

 [1]: http://jsfiddle.net/chenxsan/MebhE/2/