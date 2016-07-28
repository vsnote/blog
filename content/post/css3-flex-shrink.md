---
title: CSS3 flex-shrink
author: 陈 三
layout: post
date: 2014-07-15T12:02:26+00:00
url: /css3-flex-shrink.html
views:
  - 634
categories:
  - 前端开发
tags:
  - css3
  - 弹性盒模型

---
`flex-grow`控制flex container有多余空间的时候怎么分配，默认值为0，即所有的flex items都不分配。

`flex-shrink`[^13081.1]则控制flex container空间不足以包含flex items时，flex items怎样缩小所占空间，来防止溢出container。其默认值为1，flex items们根据自身的`flex-basis`值做相应调整。

看一个示例：

    <div class='example-Grid'>
      <div class='example-first'>汇成一道道光的流河</div>
      <div class='example-last'>我曾在天上见过地的繁华</div>
    </div>
    <style>
    .example-Grid{
      display: flex;
      border: 2px solid black;
      width: 250px;
    }
    .example-first{
      background: red;
      flex-basis: 150px;
      flex-shrink: 1;
    }
    .example-last{
      background:orange;
      flex-basis: 200px;
      flex-shrink:1;
    }
    </style>
    

<div class='example-Grid'>
  <div class='example-first'>
    汇成一道道光的流河
  </div>
  
  <div class='example-last'>
    我曾在天上见过地的繁华
  </div>
</div>



在上面的代码中，flex container宽度为250px，而两个flex item宽度加起来有350px，所以要腾100px空间出来。

计算的方式是，每个flex item的`flex-basis`值乘以`flex-shrink`值求积，求和所有flex items的乘积，然后求占比，再乘以要腾出的空间。

> .example-first: (150 \* 1) / ((200 \* 1) + (150 \* 1)) \* 100 = 42.8571428571
> 
> .exampel-last: (200 \* 1) / ((200 \* 1) + (150 \* 1)) \* 100 = 57.1428571429

所以.example-first的宽度为150 &#8211; 42.8571428571 = 107px，.example-last的宽度为200 &#8211; 57.1428571429 = 143px。

[^13081.1]:    
    [flex-shrink &#8211; CSS | MDN][1]

 [1]: https://developer.mozilla.org/en-US/docs/Web/CSS/flex-shrink