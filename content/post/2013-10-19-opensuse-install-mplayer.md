---
title: openSUSE 安装 MPlayer
author: 陈 三
layout: post
date: 2013-10-19T04:10:32+00:00
url: /opensuse-install-mplayer.html
dsq_thread_id:
  - 2008572411
views:
  - 766
categories:
  - openSUSE
tags:
  - mplayer
  - openSUSE

---
在 Ubuntu 上，我一直都用 MPlayer 播放视频，简单的几个快捷键就可以控制快进、音量等，非常方便。

这次切换系统到 openSUSE 12.3 上也不想例外。

安装方法如下。

首先是添加 PackMan 源：

    sudo zypper ar http://mirror.pcbeta.com/packman/suse/openSUSE_12.3/Essentials/ packman-essentials
    

附：<small>更多 <a href="http://packman.links2linux.org/mirrors">PackMan 源链接</a></small>

然后就可以使用 zypper 命令安装 MPlayer 了：

    sudo zypper install mplayer
    

命令行里输入：

    mplayer
    

如果有显示相关信息，则说明安装成功。