---
title: Google Apps Script userAppPanel 问题
author: 陈 三
layout: post
date: 2013-03-16T23:36:45+00:00
url: /google-apps-script-userapppanel.html
dsq_thread_id:
  - 1143129950
views:
  - 392
categories:
  - 未分类
tags:
  - Apps Script

---
我在 Google App Scripts 里写了一个脚本，使用 Google 提供的 [UiApp][1] API 来创建一个对话框，并且在 triggers 中设定打开 Google 电子表格时运行函数来显示对话框。

当我把该电子表格分享给别人用时，别人的情况是，脚本并不运行，对话框里的元素也一片空白，只显示了对话框标题，另外，页面还会下载一个叫 userAppPanel 的文件。

同类的问题在 Google 上可以搜寻出不少，去年就有人在 Google code 上报告 [bug][2]，但现在还能碰上这问题，大概是还没有解决。

一个简单的解决办法来自 [stackoverflow][3]，是将要自动运行的函数名写成 onOpen()，而不是通过 triggers 来设定，这样就不会出现 userAppPanel 的问题。

 [1]: https://developers.google.com/apps-script/class_uiapp?hl=en
 [2]: http://code.google.com/p/google-apps-script-issues/issues/detail?id=2215
 [3]: http://stackoverflow.com/questions/12041867/spreadsheet-ui-user-prompted-to-open-or-save-userapppanel-from-docs-google-com