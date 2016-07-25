---
title: LABjs
author: 陈 三
layout: post
date: 2013-08-04T10:04:24+00:00
excerpt: LABjs 方便我们管理 JavaScript 脚本间的依赖关系，不阻塞页面其他内容的下载，合理利用现代浏览器并行下载能力，提高页面访问速度。
url: /labjs.html
dsq_thread_id:
  - 1750656651
views:
  - 584
categories:
  - 前端开发
tags:
  - JavaScript
  - LABjs

---
我的博客前台页面中引用了如下 JavaScript：

  1. jQuery 1.10.2
  2. bootstrap.min.js
  3. highlight.min.js

另有两段 JavaScript 是写在页面 <script> 标签中：

    <script>
        hljs.initHighlightingOnLoad();//依赖于 highlight.min.js
    </script>
    
    <script>
       $('.menu-item--search').hover(//依赖于 jQuery
    
       function () {
           $(this).addClass('hover');
       },
    
       function () {
           $(this).removeClass('hover');
       });
    </script>
    

传统写法中，我至少需要四个 <script> 标签，并且要根据依赖关系安排它们的顺序。

LABjs 下的写法如下：

    <script src="js/LAB.min.js"></script>
    <script>
       $LAB.script("//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js")
           .wait(function () {// 函数依赖 jQuery，所以通过 .wait() 先执行 jQuery
           $('.menu-item--search').hover(
    
           function () {
               $(this).addClass('hover');
           },
    
           function () {
               $(this).removeClass('hover');
           });
       })
           .script("//netdna.bootstrapcdn.com/bootstrap/3.0.0-rc1/js/bootstrap.min.js");
    
       $LAB.script("http://yandex.st/highlightjs/7.3/highlight.min.js")
           .wait(function () {
           hljs.initHighlightingOnLoad();
       });
    </script>
    

这里，我用了两个 $LAB 链，每一条链表明一串依赖关系 &#8211; 因为 highlight.min.js 并不依赖 jQuery，所以把它单独出来，成一条链。

相比传统的脚本引入写法，通过 LABjs 加载 JavaScript 的好处有：

  1. 不阻塞页面其内容的下载，尽可能地利用浏览器并行下载能力，页面访问速度更快
  2. 清晰明确脚本间的依赖关系

## 参考

  1. [LABjs Script Loader :: Documentation][1]

 [1]: http://labjs.com/documentation.php