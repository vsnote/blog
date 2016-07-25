---
title: Apache 代理 Node.js 服务器
author: 陈 三
layout: post
date: 2016-02-07T04:05:35+00:00
url: /apache-proxy-node-js.html
views:
  - 638
categories:
  - 前端开发
tags:
  - apache
  - node.js

---
我在[安装 Ghost 博客][1]时，需要转发 Apache 请求给 node.js 服务器，当时为了快速搞定，找了些资料，拷了些配置，看它可以运行，也就没再搭理。

说来，我根本不知道为什么要加个 `ProxyPassReverse`。

前些天写的 blog [React.js 服务端渲染][2]里，同样需要让示例在服务器上运行。与安装 Ghost 时唯一的区别是，我的 blog 现在已经换成了 https。

所以配置过程是这样的：

  1. 打开 `/etc/httpd/conf.d/vhost.conf` 文件，这是 CentOS 系统下 Apache2 的配置文件路径，添加以下内容：
    
        <VirtualHost *:443>
         # 其它内容，这里不显示
          <Location /react/server-render>
            ProxyPass http://localhost:2222
            ProxyPassReverse http://localhost:2222
         </Location>
        </VirtualHost>
        
    
    `/react/react-render` 是我存放项目的路径，3000 端口是 node.js 运行的服务器端口 &#8211; 我使用了 [PM2][3] 来管理生产环境中的 node.js 项目。

  2. `sudo service httpd restart` 重启 Apache 服务器。

所以 `ProxyPassReverse` 做什么用的？还是看[官方文档][4]吧。

 [1]: https://www.zfanw.com/blog/linode-vps-install-ghost.html#_Apache_Ghost
 [2]: https://www.zfanw.com/blog/react-js-server-render.html
 [3]: https://github.com/Unitech/pm2
 [4]: https://httpd.apache.org/docs/2.4/mod/mod_proxy.html#proxypassreverse