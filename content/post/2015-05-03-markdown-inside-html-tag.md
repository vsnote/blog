---
title: Markdown – HTML 标签中的 Markdown 语法
author: 陈 三
layout: post
date: 2015-05-03T01:06:41+00:00
url: /markdown-inside-html-tag.html
views:
  - 698
categories:
  - 未分类
tags:
  - Markdown

---
Markdown 官方文档[^15813.1]有一句：

> Note that Markdown formatting syntax is not processed within block-level HTML tags. E.g., you can’t use Markdown-style _emphasis_ inside an HTML block.

markdown 不能写在块级 HTML 标签内，就是说，我们下面这样写是不行的：

    <div>
    **加粗我**
    </div>
    

`**` 不会解析为 `<strong></strong>`。

但我在 WordPress 后台用的 Markdown 插件 PHP Markdown Extra [^15813.2]扩展了该功能，可以这样写：

    <div markdown="1">
    **加粗我**
    </div>
    

下面是输出结果：

    <div>
    
    <p><strong>加粗我</strong></p>
    
    </div>
    

我之所以要用这个功能，是为了添加 Microdata [^15813.3]的缘故。拿我的[读书][1]页面说，现在 Markdown 部分是这样写的：

    时间|书名|作者
    ---|---|---
    2013.1.27|无中生有|莎士比亚
    2013.1.28|道连·格雷的画像|王尔德
    

添加 microdata 的 HTML 如下：

    <div itemscope itemtype="http://schema.org/Table">
      <h2 itemprop="about">我喜欢的书</h2>
      <!-- 表格内容在这 -->
    </div>
    

借助 PHP Markdown Extra，可以在 div 块中嵌入 markdown 写法：

    <div itemscope itemtype="http://schema.org/Table" markdown="1">
      <h2 itemprop="about">我喜欢的书</h2>
      <!-- markdown 表格在这 -->
    </div>
    

这样，我就给我的表格加入 Microdata 了。

[^15813.1]:    
    [Markdown 文档][2]

[^15813.2]:    
    [PHP Markdown Extra][3]

[^15813.3]:    
    [Microdata Table][4]

 [1]: http://www.zfanw.com/blog/read
 [2]: http://daringfireball.net/projects/markdown/syntax#html
 [3]: https://michelf.ca/projects/php-markdown/extra/#markdown-attr
 [4]: https://schema.org/Table