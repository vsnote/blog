---
title: NPM 安装包
author: 陈 三
layout: post
date: 2012-12-26T12:38:57+00:00
url: /npm-install-package.html
views:
  - 1186
dsq_thread_id:
  - 993203492
categories:
  - Ubuntu
  - 前端开发
tags:
  - Nodejs
  - NPM

---
打算安装个 [Bower][1] 用于一些库文件的管理，Nodejs、NPM 安装完后，运行命令：

    npm install -g bower
    

命令卡住很久，然后出错了,大抵是 『tunnel&#8230;socket&#8230;unknown protocol』 之类。

网络是处于完全畅通状态。

有人说是 proxy 的问题，我的系统下安装有 [privoxy][2]，启用了 http 与 https 代理为 『127.0.0.1：8118』。

在 Zsh 下输入：

    echo $http_proxy
    

显示为 『http://127.0.0.1:8118/』，调用 `unset $http_proxy`，再安装 bower，仍然失败。可能因为这个环境变量不是通过 `export` 命令设置的。

且不说其成功与否，光是为了用 NPM 安装包文件就要取消这系统代理，不免不合理。

再找资料，则知道可以通过 `npm config` 命令来配置其环境：

    npm config set proxy http://127.0.0.1:8118
    npm config set https-proxy http://127.0.0.1:8118
    

之后再运行 `npm install` 就完全正常 &#8211; 因为安装中使用 /usr/lib/ 目录，所以可能需要管理员权限，在 Ubuntu 下是运行 `sudo npm install...`。

安装完 bower 后，就可以安装 JavaScript 库：

    bower install jquery
    

## 参考

  1. [How to setup Node.js and Npm behind a corporate web proxy][3]
  2. [Manage the npm configuration file][4]

 [1]: http://twitter.github.com/bower/
 [2]: http://www.privoxy.org/
 [3]: http://jjasonclark.com/how-to-setup-node-behind-web-proxy
 [4]: https://npmjs.org/doc/config.html