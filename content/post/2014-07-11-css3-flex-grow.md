---
title: CSS3 flex-grow
author: 陈 三
layout: post
date: 2014-07-11T05:59:19+00:00
url: /css3-flex-grow.html
views:
  - 528
categories:
  - 前端开发
tags:
  - css3
  - 弹性盒模型

---
CSS3弹性盒模型中，有两类元素：

  1. flex container
  2. flex item

如下图[^13063.1]：

![css3 flexible box model][1]

flex container通过声明元素的`display`属性为`flex`或`inline-flex`定义，flex container的子元素无需声明，直接就是flex item。

`flex-grow`是flex item的CSS属性，默认值为0。

简单说，它是flex item分配flex container剩余空间的规则。

如下例：

[CSS3 flex-grow属性][2]{.jsbin-embed}

未设置`flex-grow`前，红色部分文字宽度是403px，蓝色部分文字宽度是27px，包含块宽度是630px。所以包含块还剩下200px空间可以给它的flex item分配。

因为红色部分的`flex-grow`值为1，蓝色部分的`flex-grow`值为2，所以200px分三份，红色占一份，即66.6666666667px，蓝色占两份，即133.333333333px。

最后计算结果，红色的长度为403+66.6666666667=470px，绿色的长度为27+133.333333333=160px。

而如果flex container没有空间剩余，则`flex-grow`值不管设置成什么都不会有影响。

[^13063.1]:    
    图片来自[W3][3]

 [1]: https://dev.w3.org/csswg/css-flexbox/images/flex-direction-terms.svg
 [2]: http://jsbin.com/wiluco/2/embed?output
 [3]: http://dev.w3.org/csswg/css-flexbox/#box-model