---
title: Mosh 安装使用
author: 陈 三
layout: post
date: 2012-11-02T13:50:15+00:00
url: /mosh.html
views:
  - 1787
dsq_thread_id:
  - 911169492
categories:
  - Ubuntu
tags:
  - mosh
  - ssh

---
如果用过 ssh 连接远程电脑，就会发现，无论是哪个系统，Ubuntu，或者 Windows，输入都会有很大的延迟。你输入了好多文字，它却要缓上好一会儿才显示得出来。

这是折腾 [Mosh][1](Mobile shell) 的初衷。

首先，要使用 Mosh，需要在客户端及服务器端都安装它，或者在服务器端至少安装 mosh-server。Ubuntu 下可以通过 ppa 安装的：

    $ sudo apt-get install python-software-properties
    $ sudo add-apt-repository ppa:keithw/mosh
    $ sudo apt-get update
    $ sudo apt-get install mosh
    

因为 Mosh 使用的是 UDP 端口，所以服务器上需要打开某 UDP 端口。

假设 Mosh 使用 60001 UDP 端口，则在服务器上运行：

    $ sudo iptables -I INPUT -p udp --dport 60001 -j ACCEPT
    

这样就在服务器上打开 60001 UDP 端口。当然，最好是把上一条命令写入服务器 firewall 的规则中，这样不必要每次都手动打开这个端口。

接下来就是从客户端连接：

    $ mosh -p 60001 sam@zfanw.com
    

`p` 参数用于指定 UDP 端口。

假如你的 [SSH 连接][2] 设置公钥/私钥连接，比如 `ssh zfanw` 即可直接连接服务器而无需输入密码，则 mosh 命令也可以以 `mosh zfanw` 的形式连接，基本上，可以把它当作 ssh 命令的替换，只不过 ssh 开的是 TCP 口，mosh 开的是 UDP 口。

效果如何？开两个窗口，一个直接 ssh 登录，一个通过 mosh 登录，对比输入一下就知道了 &#8211; 当然是 mosh 的输入流畅。

Mosh 有很多强于 ssh 的特性，比如连接不会掉，你可以盖上笔记本电脑让它休眠，然后再打开，mosh 的连接还在，而如果是 ssh 的话，直接就断掉。

不过折腾过程中真是碰上不少问题，比如 locale 问题，后来莫名地就折腾好了 &#8211; 本来还想写一篇关于 Locale 的内容，现在省了。

 [1]: http://mosh.mit.edu/
 [2]: http://www.zfanw.com/blog/ssh-usage.html