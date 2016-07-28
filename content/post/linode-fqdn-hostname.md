---
title: Linode FQDN 设置
author: 陈 三
layout: post
date: 2012-11-01T13:41:51+00:00
url: /linode-fqdn-hostname.html
views:
  - 1609
dsq_thread_id:
  - 909806746
categories:
  - Ubuntu
tags:
  - Linode
  - Ubuntu

---
[FQDN][1] 全称叫 Fully qualified domain name，举个例子：

    www.zfanw.com
    

其中 www 是主机名即英文的 [hostname][2]，表示域名指向的是 World-Wide Web 服务器，简单地说，可以把它理解成计算机的名称。比如我 Ubuntu 的计算机名称叫 Sam，登录的用户名为 sam，则打开 terminal emulator，命令行上能看到 `sam@Sam`，表示 Sam 计算机上的 sam 用户目前正在使用中。如果是 Windows 系统，则可以通过系统属性查看“完整的计算机名”，如果你有打开过 Windows 网上邻居，经常能看到各种五花八门的计算机名，这些就是所谓的 hostname。

zfanw 是二级域名([Second-Level domain][3])，.com 是顶级域名([Top-Level domain][4])，类似的顶级域名还有 .org、.net 等。

至于平时常见的 http，它是个互联网协议，类似的还有 ftp 等，这个与 FQDN 倒是无关。

在 Linode VPS 文档中，有一节写的是[设置 hostname][2]。因为这个设置与后期安装 Apache 有关，所以有此一篇说明。

Linode 的这节文档中给出的设置 /etc/hosts 文件的参考例子是：

    127.0.0.1        localhost.localdomain    localhost
    12.34.56.78      plato.example.com        plato
    

其中 plato 是主机名，plato.example.com 正是所谓的 FQDN，这需要你先通过 DNS 设置绑定一个子域名到你的 Linode 服务器 ip 上。

比如我可以到我的域名商 DNS 面板做一个 A 记录，解析 plato.zfanw.com 到 xxx.xxx.xxx.xx 这个 ip 地址，即 Linode 服务器的 ip 上。

然后到 /etc/hosts 文件中增加如下一行：

    xxx.xxx.xxx.xxx plato.zfanw.com plato
    

参考例子中，localhost 应该是个特殊的主机名，如果你是第一次通过 ssh 登录到 Linode 服务器，可以看到 shell prompt 显示的是 `root@localhost`，按我粗浅的理解，localdomain 应该也是个特殊域名。不过这两个我们可以不用管，默认即可。

保存 /etc/hosts 文件后 logout 出服务器，再登录可以看到，shell prompt 已经变成 root@plato 而非 root@localhost。

使用命令 `hostname --fqdn` 显示的结果是 &#8220;plato.zfanw.com&#8221;。

这样，就完成了 Linode FQDN 的设置。如果光设置 hostname 且更新 /etc/hosts 内容而不曾解析二级域名，后期在安装完 Apache 后重启会出现如下错误：

> apache2: apr\_sockaddr\_info_get() failed for plato
> 
> apache2: Could not reliably determine the server&#8217;s fully qualified domain name, using 127.0.0.1 for ServerName

对的，我折腾这一篇纯是因为这个错误，不然我实在懒得再开 DNS 解析一个二级域名。因为 Linode 明明已经有个 FQDN，[lixxx-y.members.linode.com 这样的格式][5]。

<del>最后附一个我的 <a href="https://www.linode.com/?r=c1160d4e51485f11b9ae6b4cf286ebf455f87613">Linode Referal URL</a>，作用是如果你通过这个 URL 购买了 Linode 服务器并且使用达 3 个月以上，我就可以收到 Linode 返还的 $20 美金，相当于 Linode 512 套餐一个月的价格，如果吃快餐的话，可以吃上 10 顿左右，下馆子大概一次搞定 &#8211; 当然，如果你在厦门，我不介意一起下馆子，反正，花的是 Linode 的钱。</del>

 [1]: http://en.wikipedia.org/wiki/Fully_qualified_domain_name
 [2]: http://library.linode.com/getting-started#sph_setting-the-hostname
 [3]: http://en.wikipedia.org/wiki/Second-level_domain
 [4]: http://en.wikipedia.org/wiki/Top-level_domain
 [5]: http://forum.linode.com/viewtopic.php?f=19&t=8378