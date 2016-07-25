---
title: 媒体查询与图片
author: 陈 三
layout: post
date: 2012-11-15T10:35:57+00:00
url: /media-queries-image-resize.html
views:
  - 724
dsq_thread_id:
  - 929151659
categories:
  - 前端开发
tags:
  - css3
  - 媒体查询，CSS

---
[Media Queries][1]（**媒体查询**） 是 CSS3 中加入的模块，可以用于设计[自适应设备的网页][2]，这样页面会根据设备屏幕的大小自动调整页面布局，而无需针对每个屏幕大小分别设计页面布局。

在优化页面速度时，[Google PageSpeed][3] 有这样一条关于[明确图片大小的建议][4]：

> Specifying a width and height for all images allows for faster rendering by eliminating the need for unnecessary reflows and repaints.
> 
> To prevent reflows, specify the width and height of all images, either in the HTML <img> tag, or in CSS.

大概的意思是，建议给图片明确大小，无论是通过 img 属性还是 CSS 代码，这样可以减少页面渲染过程中不必要的重排。比如这样的 HTML 语句：

    <img src="......" width="500" height="500"/>
    

因为图片的宽高值被固定下来，就需要我们在设计自适应页面时，对图片进行某种处理，否则会导致图片在小屏幕上超出屏幕范围。

如下 CSS 语句可以让图片大小（宽高）根据屏幕大小自动调整：

    @media only screen and (max-width: 480px){
        img { 
                    width: 100%;
                    height:auto;
               }
    }
    

当然，还要记得在 head 部分加入类似如下的语句，否则上述的 CSS 不能起作用：

    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
    

## 参考

  1. [An introduction to meta viewport][5]

 [1]: http://www.w3.org/standards/history/css3-mediaqueries
 [2]: http://en.wikipedia.org/wiki/Responsive_Web_Design
 [3]: https://developers.google.com/speed/pagespeed/insights
 [4]: https://developers.google.com/speed/docs/best-practices/rendering#SpecifyImageDimensions
 [5]: http://dev.opera.com/articles/view/an-introduction-to-meta-viewport-and-viewport/