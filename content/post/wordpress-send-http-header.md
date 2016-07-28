---
title: WordPress 设置 HTTP 响应头
author: 陈 三
layout: post
date: 2014-04-05T07:36:15+00:00
excerpt: 在 WordPress 中通过 send_headers 勾子给页面设置 HTTP 响应头。
url: /wordpress-send-http-header.html
views:
  - 595
categories:
  - WordPress

---
如果要给 WordPress 设置一个 HTTP 响应头(header)，却在搜索引擎中搜索 「WordPress header 设置」，结果可能会让你失望。因为 WordPress 有一个文件叫 header.php，搜索引擎很容易误会你的意图。

当然，这一篇说的是设置 HTTP 响应头，与 header.php 文件无关。

譬如你要给 WordPress 加一个 _X-Frame-Options_ [^12062.1]响应头，防止其他网站使用 iframe 嵌入你的网站，则可以通过 WordPress 的 _send_headers_ [^12062.2]勾子。

打开 **functions.php** 文件，加入如下代码：

    add_action( 'send_headers', 'avoid_clickjacking_attacks' );
    function avoid_clickjacking_attacks() {
        header( 'X-Frame-Options: SAMEORIGIN' ); 
    }
    

非同源的站点如果使用 iframe 嵌入你的网站，浏览器会拒绝渲染。Firefox 控制台会提示错误如下：

> Load denied by X-Frame-Options: http://www.zfanw.com/blog/ember-js-template-add-html5-attribute.html does not permit cross-origin framing.

## 示例

以下是两个 iframe，左边一个 src 指向 Vice，右边一个 src 指向 Google 首页。因为 Google 定义了 X-Frame-Options 响应头，所以右边一个 iframe 内容无法渲染，显示一片空白：

[^12062.1]:    
    [The X-Frame-Options response header &#8211; HTTP | MDN][1]

[^12062.2]:    
    [Plugin API/Action Reference/send headers « WordPress Codex][2]

 [1]: https://developer.mozilla.org/en-US/docs/HTTP/X-Frame-Options
 [2]: https://codex.wordpress.org/Plugin_API/Action_Reference/send_headers