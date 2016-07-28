---
title: Chrome 开发者工具之 Collect JavaScript CPU Profile
author: 陈 三
layout: post
date: 2015-10-24T09:46:53+00:00
excerpt: 介绍 Chrome 开发者工具下的 Collect JavaScript CPU Profile 用法
url: /chrome-devtools-collect-javascript-cpu-profile.html
views:
  - 889
categories:
  - 前端开发
tags:
  - Chrome
  - devtools

---
如果你想了解 JavaScript 程序的运行情况，Chrome 开发者工具下的 [Collect JavaScript CPU Profile][1] 是个好帮手。

可是它们的文档更新速度常常跟不上它们版本的更新速度。比如 Collect JavaScript CPU Profile 下的 Chart 视图，Chrome 46 以后版本的火焰图（flame chart）已经跟文档上的配图不一样了，是倒过来的。

好在重要的名词没有倒过来。

在 Collect JavaScript CPU Profile 中，我们主要关心**函数**，比如：

  1. 函数执行了多长时间
  2. 函数调用了哪些函数

Chrome 提供了三种查阅方式：

  1. Heavy (Bottom Up)
  2. Tree (Top Down)
  3. Chart

这三种视图，我比较喜欢 Chart。

<a href="https://www.zfanw.com/blog/wp-content/uploads/2015/10/flame-chart-chrome1.png" rel="attachment wp-att-17616"><img src="https://www.zfanw.com/blog/wp-content/uploads/2015/10/flame-chart-chrome1.png" alt="chrome devtools cpu profile flame chart" width="1278" class="alignnone size-full wp-image-17616" srcset="https://www.zfanw.com/blog/wp-content/uploads/2015/10/flame-chart-chrome1.png 1278w, https://www.zfanw.com/blog/wp-content/uploads/2015/10/flame-chart-chrome1-300x237.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2015/10/flame-chart-chrome1-1024x808.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2015/10/flame-chart-chrome1-100x79.png 100w, https://www.zfanw.com/blog/wp-content/uploads/2015/10/flame-chart-chrome1-768x606.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2015/10/flame-chart-chrome1-520x411.png 520w" sizes="(max-width: 1278px) 100vw, 1278px" /></a>

如前面说过的，我们主要关心**函数是否执行时间过长**。

在火焰图上，水平方向表示我们录制的时间轴，垂直方向表示函数的 call stack，即函数调用了其它函数的情形。因为一个色块表示一个函数的执行情况，所以，假如某个色块在水平方向上很宽，则说明它执行的时间太长了，极可能有优化的空间，需要我们注意；至于垂直方向，按 Chrome devtools 文档的说法：so a tall flame is not necessarily significant，其实并不十分重要。

再来说明一下上面的截图中的几个名词：

  1. Name &#8211; 表示函数的名称
  2. Self time &#8211; 函数自身语句执行的时长，不包含调用其它函数
  3. Total time &#8211; 函数整个 call stack 执行的时长
  4. Aggregated self time &#8211; 在我们录制的整个时间段内，函数自身语句总共执行了多久
  5. Aggregated total time &#8211; 在我们录制的整个时间段内，函数所有 call stack 执行了多久

以截图中具体函数来说：

  1. 函数的 name 是 `e.extend._hitTest`
  2. 函数语句本身执行的时长是 0，当然，只是无限接近 0
  3. `e.extend._hitTest` 的 call stack 执行时间 2.5ms
  4. 在我录制的 4s 多时间内，函数自身语句总共执行了 0 秒
  5. 在我录制的 4s 多时间内，函数的 call stack 总共执行了 3.90ms

情况并不算坏。

 [1]: https://developers.google.com/web/tools/chrome-devtools/profile/rendering-tools/js-execution