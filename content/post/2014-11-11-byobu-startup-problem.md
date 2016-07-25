---
title: Byobu 的启动问题
author: 陈 三
layout: post
date: 2014-11-10T19:59:59+00:00
url: /byobu-startup-problem.html
views:
  - 505
categories:
  - openSUSE
tags:
  - bash
  - Byobu

---
在我的 openSUSE 13.1 上启动 Byobu 后：

> Have a lot of fun&#8230;
> 
> /usr/lib/byobu/include/common:27: command not found: command -v

检查该路径下的 _common_ 文件第 27 行：

        for BYOBU_TEST in "command -v" "type" "which"; do
            $BYOBU_TEST >/dev/null && break || true
        done
    

虽然我不懂 Bash 编程，但大致明白，这是在检查三个 bash 内建的命令 `command -v`、`type`、`which`。

比如我们可以输入：

    which command
    

显示的结果是：

> command: shell built-in command

所以问题是出在 `command -v` 这一条，Byobu 在启动过程中，未检查到该命令。

**快速解决办法**是，修改 `command -v` 为 `command`，据我的使用，并没有什么问题。

当然，放任这个错误信息的话，也不影响使用。