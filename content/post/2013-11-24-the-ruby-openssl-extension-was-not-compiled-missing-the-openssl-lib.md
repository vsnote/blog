---
title: The Ruby openssl extension was not compiled. Missing the OpenSSL lib?
author: 陈 三
layout: post
date: 2013-11-24T11:47:50+00:00
url: /the-ruby-openssl-extension-was-not-compiled-missing-the-openssl-lib.html
views:
  - 741
categories:
  - openSUSE
tags:
  - openSUSE
  - ruby

---
我试图通过 [rbenv][1] 安装 Ruby，但失败了，错误如标题所示。

[Ruby-build][2] 上有人报告类似的错误，作者也在 wiki 上给出相应的[环境要求][3]说明。但里面并没有提到 openSUSE 系统。

依他们的思路，我查找了 openSUSE 下的相应 openssl 包：

    $ zypper se openssl
    

找到的有 libopenssl-devel 等，

    $ sudo zypper in libopenssl-devel
    

之后再通过 rbenv 安装：

    $ rben install 2.0.0-p353
    

结果是：

> Installed ruby-2.0.0-p353 to /home/sam/.rbenv/versions/2.0.0-p353

不再报错，成功安装 Ruby 2.0.0-p353。

 [1]: https://github.com/sstephenson/rbenv
 [2]: https://github.com/sstephenson/ruby-build/issues/377
 [3]: https://github.com/sstephenson/ruby-build/wiki#suggested-build-environment