---
title: Byobu 快捷键
author: 陈 三
layout: post
date: 2014-11-06T21:38:11+00:00
excerpt: 修改 Byobu 的快捷键
url: /byobu-keybindings.html
views:
  - 1012
categories:
  - openSUSE
tags:
  - Byobu
  - tmux

---
如果你用过 [GNU Screen][1] 或 [tmux][2]，并且针对它们写过大量配置，那么可以把 [Byobu][3] 当作一个开箱即用的 Screen 或 tmux。许多配置已经写好，并且做了诸多改进。

虽说它最初是针对 Ubuntu 服务器版本的，但现在各大 Linux 发行版基本都可以使用它。

比如 openSUSE 下安装 Byobu：

    sudo zypper in byobu
    

我一直以来都在用 tmux，所以对它的启动键（prefix key）要更为熟悉，而且我的习惯，<kbd>Ctrl - b</kbd> 要比 GNU Screen 默认的 <kbd>Ctrl - a</kbd> 方便按。但 openSUSE 下 Byobu 默认的启动键偏偏是 <kbd>Ctrl -a</kbd>。

## 修改快捷键

不过修改也很简单，打开 _~/.byobu/keybindings.tmux_ 文件，修改以下两行

    set -g prefix ^A
    set -g prefix2 ^A
    

为

    set -g prefix ^B
    set -g prefix2 ^B
    

保存后按 <kbd>F5</kbd> 刷新重载 Byobu 的配置文件，这时启动快捷键已经变成 <kbd>Ctrl - b</kbd> 了。

 [1]: http://www.gnu.org/software/screen/
 [2]: http://tmux.sourceforge.net/
 [3]: http://byobu.co/