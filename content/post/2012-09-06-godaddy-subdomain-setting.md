---
title: Godaddy 二级域名设置
author: 陈 三
layout: post
date: 2012-09-06T03:48:18+00:00
url: /godaddy-subdomain-setting.html
views:
  - 1853
dsq_thread_id:
  - 832687199
dsq_needs_sync:
  - 1
categories:
  - 未分类
tags:
  - Godaddy
  - 二级域名

---
我的主域名托管在 Godaddy 上，空间则是其他地方，带 Cpanel 管理界面。

要设置一个 **Godaddy 二级域名**，比如 fav.zfanw.com，首先到 Godaddy 域名管理 -> DNS 解析部分，将二级域名 fav.zfanw.com 解析到空间 ip 地址。A 记录情况如下：

  * @ xxx.xxx.xxx.xxx
  * www xxx.xxx.xxx.xxx
  * fav xxx.xxx.xxx.xxx

注意，二级域名所解析的空间 ip 地址与主域名（带 wwww 及不带 www）的均一样。

之后是到空间里设置。

打开 Cpanel -> Domains -> Subdomains，然后创建一个二级域名，并指向空间的相应目录，

  * Subdomains:fav.zfanw.com
  * Document Root:/fav

这样，当输入 fav.zfanw.com 二级域名时，DNS 就会将其解析到空间 ip 地址，到达空间后通过上面的 cpanel 设置结果将其引导至相应文件夹，于是就完成了二级域名的访问。