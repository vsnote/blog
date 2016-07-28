---
title: Theseus – JavaScript 调试工具
author: 陈 三
layout: post
date: 2013-10-23T14:58:23+00:00
url: /theseus-javascript-debugger.html
views:
  - 929
categories:
  - 前端开发
tags:
  - Adobe Brackets
  - JavaScript
  - Theseus

---
我现在用 [Adobe Brackets][1]做前端开发，它有一个扩展 [Theseus][2]，用于 JavaScript 调试。跟浏览器自带的调试工具不太一样，所以小小介绍下。

在浏览器中实时预览 HTML 文件时，Theseus 会用标示 JavaScript 各个函数运行的次数，未曾运行的函数以灰色背景突出显示：

![Theseus Real-time code coverage][3]

<small>注：如没有特殊说明，本篇图片均引用自 Theseus 库。</small>

如果我们点击**次数**，Theseus 会在 Brackets 窗口底部调出一个面板，显示函数的输入/输出值以及异常：

![监控函数的输入/输出值、异常][4]

如果我们点击多个**次数**，函数间有依赖关系，则面板中也会表示出来：

![函数的关系][5]

那么我们常用的 console.log 命令呢？类似的，Theseus 会在窗口底部显示 Events:console.log 字样，点击它就会调出一个面板：

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2013/10/theseus-console-log.png" alt="Theseus 使用 console.log 命令" width="700" class="alignnone size-full wp-image-10728" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/10/theseus-console-log.png 813w, https://www.zfanw.com/blog/wp-content/uploads/2013/10/theseus-console-log-300x163.png 300w" sizes="(max-width: 813px) 100vw, 813px" />][6]

面板中显示了 console.log 命令在 JavaScript 文件中的行位置，命令的运行时间、输出内容等。

你可能要好奇，这东西没有提供断点工具吗？答案是没有。我觉得结合上面提到的方法，完全可以流畅地完成(我目前的) JavaScript 调试工作了。

 [1]: http://www.brackets.io/
 [2]: https://github.com/adobe-research/theseus
 [3]: https://raw.github.com/adobe-research/theseus/gh-pages/call-counts.png
 [4]: https://raw.github.com/adobe-research/theseus/gh-pages/log1.png
 [5]: https://raw.github.com/adobe-research/theseus/gh-pages/log2.png
 [6]: http://www.zfanw.com/blog/wp-content/uploads/2013/10/theseus-console-log.png