---
title: 拷贝 Markdown 语法链接
author: 陈 三
layout: post
date: 2014-01-07T11:36:23+00:00
url: /copy-link-as-markdown-format.html
views:
  - 742
categories:
  - vimperator
tags:
  - vimperator

---
我现在的博客内容，都是用 Markdown [^11224.1]写的。有很多内容是关于前端技术的，经常会引用其他网址。在 Markdown 下，链接是这样写：

    [wordpress Markdown 插件](http://www.zfanw.com/blog/wordpress-markdown.html)
    

如果是平常浏览器用法，则首先，我要拷网页标题，然后是网页 URL，然后再插入一对方括号和一对大括号。这个过程偏无聊，如果链接还多，这个过程就太无聊。

不巧，我用 Vimperator[^11224.2]，我还用 Vimperator 插件[^11224.3]，Vimperator 插件中有个 copy.js，在它的基础上略做增补[^11224.4]，就可以轻易构建出 Markdown 需要的链接形式。

我的做法，是增加一个 `markdownLink` 的选项，之后 Vimperator 命令行下执行 `:copy markdownLink` 即可。

如果嫌命令行里输命令太麻烦，可在普通模式下做个映射：

    :nnoremap YY :copy markdownLink<CR>
    

之后按 YY 即可拷贝。

[^11224.1]:    
    [Daring Fireball: Markdown Syntax Documentation][1]

[^11224.2]:    
    [vimperator][2]

[^11224.3]:    
    [vimperator plugin][3]

[^11224.4]:    
    [copy.js][4]

 [1]: http://daringfireball.net/projects/markdown/syntax
 [2]: http://www.vimperator.org/vimperator
 [3]: https://github.com/vimpr/vimperator-plugins
 [4]: https://github.com/chenxsan/vimperator-plugins/blob/3.6/copy.js