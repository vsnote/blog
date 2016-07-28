---
title: 自定义input radio的样式
author: 陈 三
layout: post
date: 2014-08-12T12:15:07+00:00
url: /input-radio-style.html
views:
  - 1513
categories:
  - 前端开发
tags:
  - css

---
HTML的radio单选按钮，代码如下：

    <input type="radio" value="河西" name='flow'>河西
    <input type="radio" value="河东" name='flow'>河东
    

样式大抵如下：

<input type="radio" value="河西" name='flow' />河西 <input type="radio" value="河东" name='flow' />河东

桌面端上不同浏览器看，上面的样式可能不一样；换到移动端上，通常也会有差异。

那么我们如果想自定义radio的样式如何？

比如下面（请在webkit内核下的浏览器下查看）这样：

<div class='example'>
  <input type="radio" value="河西" name='flow' />河西 <input type="radio" value="河东" name='flow' />河东
</div>



这里用到一个非标准的CSS属性`-webkit-appearance`[^13303.1]，将其值设为`none`，预先移除浏览器默认的样式，接着添加自定义样式，具体代码如下：

    input[type="radio"]{
      -webkit-appearance: none;
      background: red;
      width: 16px;
      height: 16px;
      border-radius: 50%;
    }
    input[type=radio]:checked{
      background: orange;
    }
    

因为`appearance`是非标准的属性，所以各个浏览器的实现并不一样，有些浏览器则根本没有该属性。不过如果只是兼容iOS与Android手机上的webkit内核浏览器，倒是无妨用上。

[^13303.1]:    
    [Can I use&#8230; Support tables for HTML5, CSS3, etc][1]

 [1]: http://caniuse.com/#feat=css-appearance