---
title: SSH 远程端口转发
author: 陈 三
layout: post
date: 2016-03-07T06:28:37+00:00
url: /ssh-remote-forwarding.html
views:
  - 415
categories:
  - 前端开发
tags:
  - ssh

---
我在[开发 Telegram bot][1] 时，是先在本地写好代码，上传到服务器再测试的。因为 telegram 的 [setWebhook][2] 指定的网址是线上的。这一点，与微信公众号开发时的[接入服务器配置][3]是一样的。

当然，这样谈不上什么开发效率。

网上有些端口映射的工具，比如 ngrok，但 SSH 本身就带了这样一个工具。

假设我 telegram webhook 地址是 https://www.zfanw.com/telegram，服务器运行在 3344 端口，本地的开发环境运行在 localhost:3344 地址上，则运行如下命令：

    ssh -R 3344:localhost:3344 admin@zfanw.com
    

就可以完成远程端口转发到本地。这样，telegram 往 https://www.zfanw.com/telegram 地址 POST 的数据都会被转发到我本地上的 localhost:3344。

等等，要怎么断掉转发？首先，SSH 连接并不稳定，很容易就断掉。如果万幸不掉，则输入

    exit
    

回车即可退出。

当然，我们也可以按 <kbd>CTRL - C</kbd> 强制退出。

 [1]: https://www.zfanw.com/blog/telegram-bot-with-nodejs.html "使用 hapi.js 开发 telegram 机器人"
 [2]: https://core.telegram.org/bots/api#setwebhook
 [3]: https://mp.weixin.qq.com/wiki/8/f9a0b8382e0b77d87b3bcc1ce6fbc104.html#.E7.AC.AC.E4.B8.80.E6.AD.A5.EF.BC.9A.E5.A1.AB.E5.86.99.E6.9C.8D.E5.8A.A1.E5.99.A8.E9.85.8D.E7.BD.AE "微信开发者文档"