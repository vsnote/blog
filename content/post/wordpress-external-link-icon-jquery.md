---
title: 给 WordPress 博客外部链接添加小图标
author: 陈 三
layout: post
date: 2012-09-04T03:58:09+00:00
url: /wordpress-external-link-icon-jquery.html
views:
  - 1090
dsq_thread_id:
  - 829983904
categories:
  - WordPress
  - 前端开发
tags:
  - the_content
  - Wordpress

---
我的博客里，凡外部链接，它的右侧都有个小图标，用于标示出站链接，比如 [WordPress][1]。

最早打算使用 CSS 属性选择器，如下：

    .storycontent a{
        text-decoration:none;
        color:#000;
        padding-right:16px;
        background:url(http://www.zfanw.com/blog/wp-content/uploads/2012/08/icon_external.png)
            right center no-repeat;
    }
    .storycontent a[href^="http://www.zfanw.com/blog"],
    .storycontent a[href^="#"]{
        background:none;
        padding-right:0;
    }
    

但这有个不足，IE6 不支持属性选择符(时至2013-10-25，你还要支持 IE6 吗，我真同情你)。

另外一个办法，就是给外部链接加 class，比如 .external，然后赋予类某种样式，就没有浏览器兼容性问题。

这个方法要用到 WordPress 的 filter，the_content。

首先，在 functions.php 文件里创建一个函数 addExternalClass，用于过滤页面内容，之后再添加过滤勾子，这样内容在输出到屏幕前会按照我们的设定进行预处理：

    function addExternalClass($content) {
        $content = str_replace('<a href=', '<a class="external" href=', $content);
        //首先将页面里所有链接都加上 .external 类
        $content = str_replace('<a class="external" href="http://www.zfanw.com', '<a href="http://www.zfanw.com', $content);
        //将带本站 url 地址 http://www.zfanw.com 的链接的类 .external 移除。
        $content = str_replace('<a class="external" href="#', '<a href="#', $content);
        //将锚链接的 .external 类移除
        return $content;
        //返回处理过的内容
    }
    add_filter('the_content', 'addExternalClass');
    

再之后，就是到 style.css 里给类 .external 写个规则：

    .external{
        text-decoration:none;
        border-bottom:1px dashed #333;
        color:#000;
        padding-right:16px;
        background:url(http://www.zfanw.com/blog/wp-content/uploads/2012/08/icon_external.png)
            right center no-repeat;
    }
    

如果要让外部链接在新窗口打开，过滤函数里加个 &#8220;target=&#8217;_blank'&#8221; 就可以。

第三种办法，通过 jQuery filter 函数选择所有外部链接并添加 .external 类：

    jQuery('a').filter(function() {
       return this.hostname && this.hostname !== location.hostname;
    }).addClass("external");
    

## 鸣谢

  1. [http://codex.wordpress.org/Plugin\_API/Filter\_Reference/the_content][2]
  2. <http://api.jquery.com/filter/>
  3. <http://css-tricks.com/snippets/jquery/target-only-external-links/>

 [1]: http://wordpress.org/
 [2]: http://codex.wordpress.org/Plugin_API/Filter_Reference/the_content