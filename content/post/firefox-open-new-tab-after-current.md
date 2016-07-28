---
title: Firefox 打开新标签
author: 陈 三
layout: post
date: 2012-06-11T03:43:04+00:00
url: /firefox-open-new-tab-after-current.html
views:
  - 1124
dsq_thread_id:
  - 720713320
categories:
  - Firefox
tags:
  - Firefox
  - firefox tips

---
Firefox 有两种形式的新标签页，一种全新打开的，比如按 ctrl-t，一种从页面链接打开的，全新打开的标签页是插入到标签栏最右侧，而如果是当前页面链接打开的新标签页，则有两种可选方式：

  1. 插入到标签栏最右边
  2. 插入到当前标签页右边

这个可以通过 about:config 中的选项调整：

  1. 在地址栏打开 about:config
  2. 搜索 browser.tabs.insertRelatedAfterCurrent
  3. 双击该设置项，值在 true/false 间切换，true 表示插入到当前页右边，false 表示插入到标签栏最后。

一般来说，我会更喜欢插入到当前分页后，这也是 Firefox 自 3.6 版本起的默认设置。