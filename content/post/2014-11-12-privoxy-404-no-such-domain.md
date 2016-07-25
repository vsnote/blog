---
title: 解决 Privoxy 404 No Such Domain 问题
author: 陈 三
layout: post
date: 2014-11-11T22:23:48+00:00
url: /privoxy-404-no-such-domain.html
views:
  - 762
categories:
  - Firefox
  - openSUSE
tags:
  - Firefox
  - Privoxy

---
_404 No Such Domain_ 错误，在 Privoxy 的 [FAQ][1] 中有提及，但作者只是提到可能原因，没有提供解决办法。

在我的 openSUSE 13.1 系统上，这个错误，大致可以按以下步骤重现（作者你神经病）：

  1. 按 [Privoxy 转发到 SOCKS 服务器][2]一文的说明配置使用 SOCKS 代理
  2. 删除 _config_ 文件中 `forward-socks5 / 127.0.0.1:9999` 一句
  3. 未断掉 SSH 连接的情况下重启 openSUSE 系统
  4. 打开 Firefox

之后 Firefox 打开的所有网址都会返回 404 No Such Domain 错误，除了 Privoxy 的配置地址 http://p.p。

而如果我禁止 Firefox 走 Privoxy 代理，则一切均正常。但这没达到我的目的。重启系统也不能解决问题。

最后找到的解决办法简单得跌破眼镜，就是重启 Privoxy。openSUSE 下执行命令：

    $ sudo rcprivoxy restart
    

当然，openSUSE 下可视化的 **Services Manager** 里重启 Privoxy 也是可以的。

 [1]: http://www.privoxy.org/faq/trouble.html#DNSERRORS
 [2]: http://www.zfanw.com/blog/privoxy-forward-ssh.html