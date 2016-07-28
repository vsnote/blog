---
title: Windows 系统快速切换运行中的任务窗口
author: 陈 三
layout: post
date: 2013-04-06T13:43:13+00:00
url: /windows-switch-opened-application.html
dsq_thread_id:
  - 1191091502
views:
  - 817
categories:
  - 未分类
tags:
  - Switcher
  - Windows

---
如果用用 Windows XP 系统，我可以按 <kbd>Alt+Tab</kbd> 切换运行中的任务窗口，又或者 <kbd>Alt+Esc</kbd>。

Windows 7 中增加快捷键 <kbd>WIN+Tab</kbd>，视觉上有立体效果，见下图（图片来自 Microsoft 网站），

![Aero Flip 3D ][1]

但我之所以用它，只是因为好看。

总体来说，它们的定位效率都太低。

我的电脑上安装 Enlightenment 17 桌面系统，它有个功能，通过打开窗口的标题来快速切换任务。比如我系统里运行着 firefox、Google Chrome、Sublime Text 2、Tmux，则启动该功能后，键入 fi 后按 <kbd>Enter</kbd> 就可以切换到 firefox 窗口。因为知道自己要打开哪个窗口，所以大概地知道窗口标题不是件难事。

Windows 下要增加这种功能，可以借助 [AutoHotkey][2] [脚本][3]。

  1. 首先安装 [AutoHotkey][2]
  2. 然后新建一个 .ahk 文件
  3. 将脚本内容拷入，保存
  4. 运行 ahk 文件。

脚本默认使用 <kbd>CapsLock</kbd> 键来触发，触发后桌面会弹出一个窗口，键入窗口标题就可以快速切换，如下图：

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2013/04/autohotkey-switcher.jpg" alt="autohotkey 运行窗口快速切换" width="719" height="207" class="alignnone size-full wp-image-8643" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/04/autohotkey-switcher.jpg 719w, https://www.zfanw.com/blog/wp-content/uploads/2013/04/autohotkey-switcher-300x86.jpg 300w" sizes="(max-width: 719px) 100vw, 719px" />][4]

但我们可以根据自己的习惯配置触发键，比如我更倾向使用 <kbd>Win + Space</kbd>，因为方便按到。在脚本中查找 `CapsLock::`，把它替换成 `#Space::` &#8211; `#` 在 AutoHotkey 里表示 Win 键。

**附**：[下载 ahk 文件][5]

 [1]: http://res1.windows.microsoft.com/resbox/en/windows%207/main/c7507caf-e2f4-48c9-9e68-eb124737de9d_52.jpg
 [2]: http://www.autohotkey.com/
 [3]: http://www.autohotkey.com/board/topic/30487-iswitchw-cosmetically-enhanced-edition/
 [4]: http://www.zfanw.com/blog/wp-content/uploads/2013/04/autohotkey-switcher.jpg
 [5]: http://d.pr/f/x01s