---
title: 图片居中
author: 陈 三
layout: post
date: 2013-03-15T14:14:03+00:00
url: /center-image.html
views:
  - 602
dsq_thread_id:
  - 1139139497
categories:
  - 前端开发
tags:
  - css
  - 图片

---
如果是一个不确定宽度的块，要让一张已知宽度的图片在其中居中，最好的办法应该是利用 CSS 把图片设置为块的背景图片，然后利用背景图片位置功能将其居中。如下：

    div {
        background:url('example.jpg') no-repeat center top;
    }
    

这种办法在处理图片宽度超出包含块的情况下尤其有效。但是，这个办法会导致图片超出部分被隐藏。

老实说，以上用法已经背离结构与样式分离的通则，为了让图片居中，我们把本该位于 HTML 中 IMG 标签里的图片变成样式中没有语义的背景图片。不过，目的第一。

如果知道包含块的宽度比图片宽度要大，则也可以设置包含块的 `text-align` 为 `center`，这是因为 `text-align` 对包含的行内元素起作用：

    div { text-align:center; }
    

还有一种办法，是将 IMG 声明为 block，然后利用左右 margin 的 auto 值自动平均来居中：

    img{ display:block; margin:0 auto;}
    

至于已知包含块的宽度与图片大小的情况就更简单，除了以上办法外，还可以利用绝对定位来居中。

当你希望图片居中，并且能根据设备分辨率自动做出大小调整时，事情开始变得复杂。

在现代的浏览器上，自适应(或称响应式)可以使用媒体查询，比如要让背景图片自适应设备宽度：

    @media screen and (max-width:980px) {
        div {
          background-size:100% auto;
          }
    }
    

而在早期浏览器上，只能考虑放弃，或者使用 JavaScript。

简单示例见 [jsfiddle][1]。

 [1]: http://jsfiddle.net/chenxsan/RDQLb/