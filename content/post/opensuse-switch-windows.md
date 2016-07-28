---
title: openSUSE 下快速切换打开的窗口
author: 陈 三
layout: post
date: 2013-11-02T16:43:29+00:00
url: /opensuse-switch-windows.html
views:
  - 445
categories:
  - openSUSE
tags:
  - openSUSE

---
我一直认为，Alt + Tab 这样的切换运行任务的方式非常低效。这也是我在 Windows 系统下使用 [iSwitchw][1] 脚本的原因。

openSUSE 有类似功能，不过颇隐蔽。

按 <kbd>Alt - F1</kbd>，打开桌面左下的主菜单，然后点击 Configure Desktop(配置桌面)，进入界面后，打开 Shortcuts and Gestures，定位到 Global Keyboard Shortcuts，KDE component 下拉菜单中选择 Run Command Interface，然后配置下方的 「Runner &#8220;Windows&#8221; only」：

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2013/11/opensuse-run-command-windows.png" alt="opensuse 切换运行中的窗口" width="623" height="593" class="alignnone size-full wp-image-10900" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/11/opensuse-run-command-windows.png 623w, https://www.zfanw.com/blog/wp-content/uploads/2013/11/opensuse-run-command-windows-300x285.png 300w" sizes="(max-width: 623px) 100vw, 623px" />][2]

我的习惯，是使用 <kbd>Win + W</kbd> 键。

调出小窗口后，输入要定位的窗口标题，然后回车即可。

## 补充

KDE 下其实还有一个预览当前所有打开窗口的方法，只要把光标移动到桌面左上角，或者按<kbd>Ctrl-F9</kbd>(预览当前桌面所有打开窗口)、<kbd>Ctrl-F10</kbd>(预览所有桌面的所有打开窗口)。之后在预览里输入标题信息即可自动过滤。

 [1]: http://www.zfanw.com/blog/windows-switch-opened-application.html
 [2]: http://www.zfanw.com/blog/wp-content/uploads/2013/11/opensuse-run-command-windows.png