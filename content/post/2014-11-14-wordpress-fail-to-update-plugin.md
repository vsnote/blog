---
title: WordPress 插件更新失败
author: 陈 三
layout: post
date: 2014-11-14T05:24:37+00:00
url: /wordpress-fail-to-update-plugin.html
views:
  - 715
categories:
  - openSUSE
  - WordPress
tags:
  - apache

---
在我升级 WordPress 插件时，碰到如下错误：

> Downloading update from https://downloads.wordpress.org/plugin/akismet.3.0.3.zip…
> 
> Unpacking the update…
> 
> Could not create directory.

原因是 WordPress 没有权限创建新文件夹。

## 解决办法

  1. 终端窗口执行 `ls -l` 命令
    
    查看 _wp-content_ 目录当前所有者（owner）与所属的组（group），结果是 _sam : users_。

  2. 查看 Apache 服务的所有者（owner）：
    
        $ ps aux | grep apache
        
    
    我的 openSUSE 13.2 上显示 **wwwrun**，与第一步得到的用户不一样。我们**需要修改 wp-content 的所有者与组**。

  3. 执行如下命令查看 wwwrun 用户所属的组：
    
        $ groups wwwrun
        
    
    用户 wwwrun 属于 www 组。

  4. 修改 wp-content 目录的所有者与组：
    
        $ sudo chown -R wwwrun:www wp-content
        

接下来就能成功更新插件。