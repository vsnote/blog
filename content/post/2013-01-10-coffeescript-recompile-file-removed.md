---
title: CoffeeScript Recompile 问题
author: 陈 三
layout: post
date: 2013-01-10T15:14:18+00:00
url: /coffeescript-recompile-file-removed.html
views:
  - 568
dsq_thread_id:
  - 1018320320
categories:
  - 前端开发
tags:
  - CoffeeScript

---
CoffeeScript 提供了一个命令行参数 `--watch` 用来监视 .coffee 文件的变化，如果该类文件有更新，将自动将其 compile 成 JavaScript 文件。

但如果在 vim 下编辑 .coffee 文件，并且调用 coffee 命令监视：

    coffee -w -c xx.coffee
    

在 vim 中保存更新后，会出现如下错误：

> removed xx.coffee

按 [stackoverflow][1] 上的说明，则应该是：

> is that some programs save changes not by writing directly to the existing file, but rather by writing to a temporary file and then mv-ing that file on top of the existing one. From fs.watch&#8217;s perspective, this means that the watched file has been deleted, and changes to the new file will be ignored.

vim 的机制是先创建一个临时文件，然后在 `:w` 命令时将该临时文件移动或复制一份并覆盖原有的文件，在 fs.watch 看来，该原文件就是被删除。于是就出现上述问题。

一个解决办法是使用第三方工具，比如 [jitter][2]，又或者第二个办法，通过 vim 的自动命令功能：

    autocmd BufWritePost,FileWritePost *.coffee silent !coffee -c <afile>
    

第二个方法的不好之处是出错了看不到，第一个则可以随时显示编译的情况。

 [1]: http://stackoverflow.com/questions/8280915/coffeescript-1-1-3-watch-only-works-once
 [2]: https://github.com/TrevorBurnham/jitter