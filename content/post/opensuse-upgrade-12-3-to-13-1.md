---
title: openSUSE 升级 12.3 到 13.1
author: 陈 三
layout: post
date: 2013-11-19T22:53:14+00:00
url: /opensuse-upgrade-12-3-to-13-1.html
dsq_needs_sync:
  - 1
views:
  - 729
categories:
  - openSUSE
tags:
  - openSUSE

---
因为是初次跨版本升级 openSUSE，虽说碰上几个问题，但总算安稳度过。

升级的方法参照了两个：

  * [官网说明][1]
  * [Marguerite Su 提供的][2]

我碰上的问题有：

  * 控制台里乱码，许多文字显示成方块
    
    我的解决办法是控制台里登录root账户。
    
    Marguerite Su 提供的方法是：
    
    > tty 显示不了中文，请先 export LANG=en_US.UTF-8

  * 下载过程卡住
    
    我的情况，总共2074个文件要下载，但下载到第99个文件时，卡了好几个小时不曾动。后来实在忍不住，就冒险按了两次<kbd>Ctrl-C</kbd>中止过程，重新启动 `zypper dup`，却是恢复正常了。后来想想，也许先让系统把所有要更新的文件下载下来会比较合适：
    
           # zypper dup --download "in-advance"

 [1]: http://en.opensuse.org/SDB:System_upgrade
 [2]: https://forum.suse.org.cn/viewtopic.php?f=2&t=173