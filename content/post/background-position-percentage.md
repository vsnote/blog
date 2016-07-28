---
title: background-position 的百分比
author: 陈 三
layout: post
date: 2014-06-02T11:52:17+00:00
url: /background-position-percentage.html
views:
  - 548
categories:
  - 前端开发
tags:
  - css

---
平常使用 `background-position`，一般是用固定值，比如：

    .hello {
      background-position: 50px 50px; // 背景图片左上角离包含块左上角距离为水平方向 50px，竖直方向 50px
    }
    

示意如下：

<div class="hello">
  <p>
    50&#215;50的色块
  </p>
</div>



居中背景图片的话，则常常用百分比：

    .hello {
      background-position:50% 50%;
    }
    

这似乎理所当然。

那如果上面的固定值 50px，我坚持要写成百分比如何？

已知背景图片大小为 150&#215;150，包含块大小为 200&#215;200。

答案是：

    .hello {
      background-position: 100% 100%;
    }
    

这个值是这样计算的：

    50/(200-150)*100% = 100%
    

这是因为 `background-position` 在使用百分比时，概念跟固定取值并不一样。

举上面的示例说，如果设置 `background-postion:10% 30%;`，则是背景图片水平方向 10% 位置的点与包含块水平方向 10% 位置的点重合。换算成固定取值的话：

    (200-50)*10% = 5
    

示意如下：

<div class="hello2">
  <p>
  </p>
</div>



但如果我们使用负的百分比，则浏览器的处理方式又跟绝对值一样了，比如：

    .test {
      background-position: -10%, -50%;
    }
    

就是让背景图片起点定位到包含块 (-10%, -50%) 的位置。

这个概念不十分直观，所以没细究的话，很容易误解。

附：[background-position &#8211; CSS | MDN][1]

 [1]: https://developer.mozilla.org/en-US/docs/Web/CSS/background-position