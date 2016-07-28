---
title: WordPress 图片上传问题
author: 陈 三
layout: post
date: 2014-11-05T11:24:34+00:00
url: /wordpress-upload-image-problem.html
views:
  - 559
categories:
  - WordPress
tags:
  - apache
  - openSUSE

---
博客从虚拟主机迁到 VPS 后，开始水土不服，曝各种问题 &#8211; 当然，水土不服是屁话，WordPress 运行环境不一样，各种配置需要做调整才是真的。

比如这 WordPress 后台上传图片的问题：

> There are no HTTP transports available which can complete the requested request.

有人说是缺少 _php5-curl_ 模块的缘故，我服务器系统跑的是 openSUSE 13.1 64位，检查 _php5-curl_ 的情况：

    zypper info php5-curl
    

输出结果如下：

    Information for package php5-curl:
    ----------------------------------
    Repository: openSUSE-13.1-Update
    Name: php5-curl
    Version: 5.4.20-30.1
    Arch: i586
    Vendor: openSUSE
    Installed: No
    Status: not installed
    Installed Size: 70.2 KiB
    Summary: PHP5 Extension Module
    Description: 
    PHP interface to libcurl that allows you to connect to and communicate
    with servers of many different types, using protocols of many different
    types.
    

请注意 **Installed: No**，确实未曾安装。

且安装一下：

    sudo zypper install php5-curl
    

然后重启服务器上的 Apache：

    sudo /usr/sbin/rcapache2 restart
    

之后图片就可以上传，不再报错。有些人说要改 php.ini 文件配置，我的情况则不需要。