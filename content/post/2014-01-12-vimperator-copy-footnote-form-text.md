---
title: Vimperator 拷贝当前网页标题与URL成脚注形式文本
author: 陈 三
layout: post
date: 2014-01-12T10:11:53+00:00
url: /vimperator-copy-footnote-form-text.html
views:
  - 1024
categories:
  - vimperator
tags:
  - vimperator

---
这一篇标题有点长，这一篇的需求比较奇葩。

如脚注一篇所说的[^11372.1]，我经常有在 WordPress 里插入脚注的习惯。PHP Markdown Extra 里，脚注是这样的形式：

    [^1]: [WordPress 脚注 – 陈三](http://www.zfanw.com/blog/wordpress-footnote.html)
    

输入次数多了让人反胃。虽然有 Vimperator 的 copy.js [^11372.2]助阵，还是会觉得麻烦。

我理想的用法，应该是输入 `[count]YY` 就可以拷贝出 `[^[count]]: [标题](url)` 这样的形式。

不巧，今天翻译 Vimperator 中文帮助的进度指向 JavaScript 一章，于是就倒腾出如下命令：

    :javascript util.copyToClipboard('[^' + gBrowser.tabContainer.selectedIndex + ']: ['+ buffer.title + '](' + buffer.URL + ')')<CR>
    

这个命令可以拷贝当前网页的标题与 URL 成以下形式：

    [^8]: [Vimperator 拷贝脚注文本 – 陈三](http://www.zfanw.com/blog/?p=11372)
    

数字8是指当前标签页的 index 值，即它的左边还有8个标签页。如果还有其他标签页群组，则数字也许会不一样。

虽然这个结果离我的理想还有点距离，但 [count] 的传递暂时还想不出怎么解决，就只好先接受，再观察。

[^11372.1]:    
    [WordPress 脚注 – 陈三][1]

[^11372.2]:    
    [拷贝 Markdown 语法链接 – 陈三][2]

 [1]: http://www.zfanw.com/blog/wordpress-footnote.html
 [2]: http://www.zfanw.com/blog/copy-link-as-markdown-format.html