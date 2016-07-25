---
title: CSS 贴图定位
author: 陈 三
layout: post
date: 2013-08-11T23:00:01+00:00
url: /css-sprite.html
views:
  - 559
categories:
  - 前端开发
tags:
  - css

---
CSS 贴图定位是我在 Google PageSpeed 看到的叫法，更常见的，应该是 CSS 精灵(sprite)。

CSS 贴图定位的好处，又或制作方法，很多地方都有介绍，所以这篇并不说那些，而是介绍一个 CSS (最|更)佳实践。

假设一张 png 透明图片 sprite.png，则 CSS 规则中会出现如下：

    .icon-arrow-right{background:transparent url(../img/sprite.png) no-repeat -48px -30px;}
    ......
    .slide-heading{background:transparent url(../img/sprite.png) no-repeat 0 -130px;}
    ......
    

上面的代码重复部分很多，一个更简洁，而且富有语义的用法，应该是抽象出一个类：

    .sprite{background-image:url(../img/sprite.png);background-repeat:no-repeat;margin:0;padding:0;}
    

然后针对各元素设定贴图的位置：

    .icon-arrow-right{background-position:-48px -30px;}
    ......
    

在 HTML 代码中，要使用 CSS 贴图定位的元素，一概添加 `.sprite` 类，

    <span class="sprite icon-arrow-right">Hello CSS sprite</span>
    

这样，HTML 代码就可以告诉我们，哪些元素是 CSS 贴图定位完成的效果，非常直观。