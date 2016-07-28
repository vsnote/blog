---
title: 博客迁移到 https
author: 陈 三
layout: post
date: 2015-09-04T13:43:41+00:00
excerpt: 从 http 迁移到 https 的详细步骤
url: /set-up-https.html
views:
  - 735
categories:
  - 未分类

---
**更新：** 2015-11-10 目前使用了 [letsencrypt][1] 颁发的证书。

http 协议的页面，经过互联网上的路由器、代理服务器时，常常会被人插入广告内容。所以我们常常能看到人们骂电信流氓、骂联通流氓。它们流氓是不必说，但内容提供者们可以提供 https 防止它们的一些流氓行为。

首先，你需要一个以自有域名结尾的邮箱地址，用于验证域名的所有权，比如 webmaster@zfanw.com 这样。你可以自建邮件服务器 &#8211; 比较复杂，也可以使用 [Google Apps for Work][2] 这类收费服务。

接着，我们需要一个 ssl 证书，[comodo][3] 提供有免费 90 天可用的证书。

简单步骤如下：

  1. 点击页面上的 Download Free SSL，会打开一个新页面，页面上有个表单需要填写

  2. 根据它的网站上的[说明][4]生成一个 csr 文件
    
    注意，说明里要求 Common Name 使用 fully qualified domain name，这是不对的。比如我的网站的 FQDN 是 orchid.zfanw.com，按它的说明填入的话，ssl 证书就会授权给 orchid.zfanw.com，而不是 zfanw.com，**所以 Common Name 一项应该填写 &#8220;zfanw.com&#8221; 这样**

  3. 打开生成的 csr 文件，将内容拷入第 1 步中打开的表单中，完成其它选项，将点击 Next

  4. 按它的说明操作完成后，它会发送一个 zip 包到邮箱中，里面有相应的证书文件，按[网站提供的操作说明][5]在服务器上配置并重启 Apache。

  5. 最后，使用 <https://www.digicert.com/help/> 工具验证证书的安装情况，或者直接点击浏览器的地址栏图标。

如果想把 http 全部重定向到 https 的路径，可以使用 [RedirectSSL(Apache 服务器)][6]。

 [1]: https://letsencrypt.org/
 [2]: https://www.google.com/work/apps/business/
 [3]: https://www.comodo.com/e-commerce/ssl-certificates/free-ssl-certificate.php
 [4]: https://support.comodo.com/index.php?/Default/Knowledgebase/Article/View/1/19/
 [5]: https://support.comodo.com/index.php?/Default/Knowledgebase/Article/View/637/37/
 [6]: https://wiki.apache.org/httpd/RedirectSSL