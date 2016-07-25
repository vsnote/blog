---
title: Charles Proxy 的 .desktop 文件
author: 陈 三
layout: post
date: 2015-02-03T14:30:58+00:00
url: /dot-desktop-file-charles-proxy.html
views:
  - 587
categories:
  - openSUSE
tags:
  - Charles Proxy

---
[Charles Proxy 的 Linux 版本][1] 只是一个压缩包，解压到 _/opt_ 目录后，如果希望从 openSUSE 的 kickoff 开始菜单中启动，就需要创建一个 [.desktop][2] 文件。

我的电脑环境：

  1. openSUSE 13.2 32 位
  2. Plasma 5.2 桌面环境

在 _~/.local/share/applications_ 目录下新建一个 **charles.desktop** 文件，添加如下内容：

    [Desktop Entry] 
    Version=3.9.3 
    Type=Application 
    Name=Charles 
    Icon=/opt/charles/icon/charles_icon512.png 
    Exec="/opt/charles/bin/charles" %f 
    Categories=Development;IDE; 
    Terminal=false 
    StartupWMClass=com-xk72-charles-gui-MainWithClassLoader 
    

其中 `StartupWMClass` 可以通过执行 [`xprop`][3] 命令取得。

最终效果如下图：

[resp_image id=&#8217;15134&#8242; caption=&#8221; ]

 [1]: http://www.charlesproxy.com/download/
 [2]: http://standards.freedesktop.org/desktop-entry-spec/latest/
 [3]: http://www.xfree86.org/4.0/xprop.1.html