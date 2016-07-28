---
title: CSS 隐藏文本
author: 陈 三
layout: post
date: 2013-08-09T22:20:00+00:00
url: /css-image-replacement.html
dsq_thread_id:
  - 1754468130
views:
  - 401
categories:
  - 前端开发
tags:
  - css

---
一个元素，需要背景图片替代文字，但又想在 HTML 中保留文字，最常见的解决方法是：

    p{text-indent:-9999px;}
    

但据说这种办法可能被[搜索引擎判断为作弊行为][1]。

可我是前端开发，不是搜索引擎优化人员，这种后果暂时就不去想了。

[HTML5Boilerplate][2] 里隐藏文本用的方法如下：

    /*
    * Image replacement
    */
    
    .ir {
        background-color: transparent;
        border: 0;
        overflow: hidden;
        /* IE 6/7 fallback */
        *text-indent: -9999px;
    }
    
    .ir:before {
        content: "";
        display: block;
        width: 0;
        height: 150%;
    }
    

这个方法使用 :before 伪类，在元素前插入空内容块，并设置其高度为元素高度的150%，这样，真实文本超出包含块高度 &#8211; 因为设置 `overflow:hidden;`，也隐藏了文本。

`*` 是针对 [IE6、7浏览器][3]的，可以改造如下：

    .ir {
        background-color: transparent;
        border: 0;
        overflow: hidden;
    }
    .lt-ie8 .ir{
        text-indent:-9999px;
    }
    .ir:before {
        content: "";
        display: block;
        width: 0;
        height: 150%;
    }
    

这样就符合 CSS 规范了。

 [1]: http://luigimontanez.com/2010/stop-using-text-indent-css-trick/
 [2]: https://github.com/h5bp/html5-boilerplate/blob/master/css/main.css
 [3]: http://en.wikipedia.org/wiki/CSS_filter#Star_hack