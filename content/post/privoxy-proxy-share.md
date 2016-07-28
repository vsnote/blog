---
title: Privoxy 共享代理
author: 陈 三
layout: post
date: 2015-07-31T16:41:20+00:00
excerpt: 通过 Privoxy 把代理共享给多个设备使用
url: /privoxy-proxy-share.html
views:
  - 1816
categories:
  - Mac OSX
tags:
  - Privoxy

---
Privoxy 在启动后，会在电脑上创建一个代理服务器，默认监听端口 8118。它的这个行为定义在它的 `config` 配置文件中：

    listen-address 127.0.0.1:8118
    

我用 Privoxy，主要目的是去除广告，当然，它也可以转发流量，所以绕过 gfw 也是十分容易。

比如你的代理地址是 `127.0.0.1:11111`，则在 Privoxy 的 `config` 文件中加一行：

    forward / 127.0.0.1:11111
    

就可以把 Privoxy 代理的流量全然转发给代理。

说来，这年头，谁家没几台设备呢？

比如我主要用 MacBook，配了代理，早先退下来的 openSUSE，偶尔也用，但又不想重复操作 &#8211; 再配一次互联网代理。那么，MacBook 上的互联网代理有没有办法共享出来给同一个 wifi 环境下的其它设备使用？比如我的 openSUSE、或手机？

答案是，有的。

## 添加新的监听地址

如上所说，Privoxy 在 `config` 配置中有一行 `listen-address 127.0.0.1:8118`，这一行允许本机软件使用 Privoxy 的代理服务器，如果我们要让该 Privoxy 代理在同一 wifi 环境下其它设备也可用，则需要再添加一个监听地址，比如：

    listen-address 192.168.1.110:8118
    

`192.168.1.110` 是电脑的 ip 地址。

然后在其它设备上，比如我的 openSUSE 下的 firefox 里，将代理指向 192.168.1.110:8118 即可。

这个办法会有一个问题，比如换个网络，路由分配的 ip 地址变了，会导致 Privoxy 启动失败。也就是说，每次电脑的 ip 变化，都需要修改 `config` 中的 `listen-address`，比较麻烦。