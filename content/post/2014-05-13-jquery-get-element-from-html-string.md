---
title: jQuery 解析 HTML 源代码
author: 陈 三
layout: post
date: 2014-05-13T11:32:03+00:00
url: /jquery-get-element-from-html-string.html
views:
  - 535
categories:
  - 前端开发
tags:
  - jQuery

---
因为工作需要，经常需要从 Ajax 请求回来的页面 HTML 代码中解析某些数据。

比如要取得网站的 title，我可以用正则表达式匹配，比如：

    <title>[\s\S]*<\/title>
    

但因为各种页面 HTML 代码花样太多，正则规则可能要不断调整，所以通常我更喜欢用 jQuery ，写法如下：

    $.get('http://www.zfanw.com/blog/', function(data) {
      var title = $(data).filter('title').text();
      $('demo').html('陈三的博客的 title 为：' + title);
    });
    

代码执行结果如下：

<div id='demo' class='text-info'>
</div>

这好像理所当然。

但我碰到过的一个情况，HTML 代码结构不合规范，比如有「多余的结束标签&#8221;div&#8221;」(stray end tag &#8220;div&#8221;) 这类错误，就会导致 `$(data)` 解析出问题。

仍以上面的例子说明，则是 `$(data).filter('title')` 的 length 值为 0，也就取不到 title 内容。把多余的结束标签剔除后，就可以正常取到。网上能找到的资料中都没有提过这一点，所以在这里做一补充。