---
title: FOUC
author: 陈 三
layout: post
date: 2013-08-29T23:33:32+00:00
url: /flash-of-unstyled-content.html
views:
  - 511
categories:
  - 前端开发
tags:
  - FOUC
  - FUBC

---
FOUC 全称 [Flash of unstyled content][1]，是指 HTML 页面在打开过程中，内容先于样式展示，导致页面样式在瞬间出现剧变，并且人眼可见。

维基上有一张截屏，如下：

![fouc][2]

在大量使用 JavaScript 调整样式的今天，类似情况也很常见。我们的页面内容、样式已经渲染完毕，JavaScript 中对样式调整，于是页面加载过程中，样式又在瞬间出现剧变 &#8211; LABjs 作者把它称做 [FUBC &#8211; flash of un-behaviored content][3]。一个最简单的解决办法是，把 JavaScript 文件放置在 `</head>` 标签前，这样可以阻塞页面其它元素的下载、渲染。但显然不现实，前端优化中，为加快页面下载速度，往往会把 JavaScript 文件放置在页面底部，即 `</body>` 标签前 &#8211; 于是 FUBC 现象无可避免。

当然，我们可以把页面加载完毕时暂不显示的内容用 CSS 隐藏，比如我的 [jQuery Tab 插件][4] 中的处理方式，是简单地添加一个 `.is-hide` 类隐藏某些内容。但这会导致一个问题：页面的可访问性变差。如果用户禁用 JavaScript，则这部分内容将不可见。

解决办法是，利用 [Modernizr][5] 的附加功能。

使用 Modernizr 库的页面，`<html>` 标签中带有 `.no-js` 类，在页面执行 Modernizr 后，它会移除 `.no-js` 类，添加 `.js` 类，那么我可以定义一个规则：

    .is-hide{display:none;}
    .no-js .is-hide{display:block;}
    

这样，即使用户禁用浏览器的 JavaScript，他们也可以看到页面的所有内容。

 [1]: http://en.wikipedia.org/wiki/Flash_of_unstyled_content
 [2]: http://upload.wikimedia.org/wikipedia/commons/thumb/b/b0/Wikipedia_FOUC.png/640px-Wikipedia_FOUC.png
 [3]: http://blog.getify.com/labjs-new-hotness-for-script-loading/
 [4]: http://www.zfanw.com/blog/jquery-plugin-tab.html
 [5]: http://www.zfanw.com/blog/modernizr.html