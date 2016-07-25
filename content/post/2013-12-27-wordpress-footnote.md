---
title: WordPress 脚注
author: 陈 三
layout: post
date: 2013-12-26T23:03:47+00:00
url: /wordpress-footnote.html
views:
  - 763
categories:
  - WordPress
tags:
  - Markdown
  - Wordpress

---
至今为止，我的博客末尾，都是一个「扩展阅读」的外部链接。很多时候，其实想以脚注[^11153.1]的形式展现，但 WordPress 并没有便捷的工具；写 HTML 代码的话，又嫌冗繁，也就没弄。

前些日子在某个 feed 里看到 Bigfoot [^11153.2]这个 jQuery 脚注插件，便收藏起来，想着有空试试。今天一试，还是要写不少 HTML 代码，而我在 WordPress 里是用 Markdown  [^11153.3]写的。要在 Markdown 简洁的语法中混入 HTML 代码，于我实在不忍心。想着又要放弃，结果莫名地又查了遍 PHP Markdown Extra [^11153.4]的文档，赫然发现有脚注的用法。

用法非常简单。

首先，在要插入脚注的位置插入 `[^1]` 这样的内容。

然后在底部插入 `[^1]: 这里是脚注的内容`。

Markdown Extra 插件会自动生成相应的 HTML 代码。需要注意，如果有多个脚注内容，它们之间要换行隔开，比如：

    [^1]: 我是脚注内容1
    
    [^2]: 我是脚注内容2
    

最终效果见文末。

[^11153.1]:    
    [脚注的概念][1]

[^11153.2]:    
    [Bigfoot][2]

[^11153.3]:    
    [WordPress 的 Markdown 用法][3]

[^11153.4]:    
    [PHP Markdown Extra 文档][4]

 [1]: http://zh.wikipedia.org/wiki/Help:脚注
 [2]: http://cmsauve.com/labs/bigfoot/
 [3]: http://www.zfanw.com/blog/wordpress-markdown.html
 [4]: http://michelf.ca/projects/php-markdown/extra/#footnotes