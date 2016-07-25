---
title: JavaScript 事件发生顺序
author: 陈 三
layout: post
date: 2013-01-14T11:08:38+00:00
url: /javascript-event-order.html
views:
  - 570
dsq_thread_id:
  - 1025055374
categories:
  - 前端开发
tags:
  - JavaScript

---
如下一段 HTML 代码：

    <!DOCTYPE HTML>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <p><a href="http://www.zfanw.com/blog/">陈三</a></p>
    </body>
    </html>
    

如果点击链接，click 事件不仅仅发生在 a 元素上，p 元素也有，document 这个根元素也有，如果给它们都绑定了 click 事件处理函数，谁会先发生？

给它们分别绑定事件处理函数，如下：

    <!DOCTYPE HTML>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body onclick="alert('hey you just click a body element')">
        <p onclick="alert('hey you just click a p element')"><a href="http://www.zfanw.com/blog/" onclick="alert('hey you just click on a element');return false">陈三</a></p>
    </body>
    </html>
    

见 [jsfiddle][1]：

在 firefox 17 下，点击链接的话，a 的事件最早触发，然后是 p，然后是 body。

在 IE6 下，点击的情况也是一样。

即它们都采取了冒泡(bubble)方式。Netscape 中采取的是捕获(capture)方式，不过 Netscape 浏览器已经死了，所以可以认为，**目前的浏览器默认都采用冒泡方式**。

但 W3C 定义的事件注册方法 addEventListener 允许通过一个布尔参数来修改：

    target.addEventListener(type, listener[, useCapture]);
    

如果 useCapture 默认为 true，则采用捕获方式。

来看一个[例子][2]，在支持 W3C 事件注册方法的浏览器下，点击链接会先显示 p 元素被点击，然后是 a，然后是 body。

这是因为 W3C 事件注册方法同时支持事件处理的捕获与冒泡阶段。而通过 `useCapture` 值设置为真将 p 元素的单击事件捆绑到捕获阶段，在 W3C DOM 事件规定中，捕获阶段先于冒泡发生，即 body -> p -> a -> p -> body 这样的顺序。于是 p 的单击事件最早发生，随后是 a，最后冒泡到 body。

当然，冒泡也是可以取消的。方法仍有两种，一是 IE，一是 W3C:

  1. W3C &#8211; event.stopPropagation();
  2. IE &#8211; window.event.cancelBubble = true;

## 参考

  1. [Events order][3]

 [1]: http://jsfiddle.net/chenxsan/R4cyq/
 [2]: http://jsfiddle.net/chenxsan/TX8CW/
 [3]: http://www.quirksmode.org/js/events_order.html