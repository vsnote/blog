---
title: Firefox flash 崩溃
author: 陈 三
layout: post
date: 2014-12-04T15:46:35+00:00
excerpt: 解决 Firefox 下 flash 崩溃的问题
url: /firefox-flash-crash.html
views:
  - 996
categories:
  - openSUSE
tags:
  - Firefox
  - flash

---
这一篇介绍 openSUSE 系统下 flash 崩溃的一种解决办法。

**环境**：

  * 操作系统：openSUSE 13.2 32 位
  * 浏览器：Firefox 34 版本

**病症**：使用 flash 的页面均出现 **Adobe Flash 插件已崩溃**。

尝试了 Chrome 浏览器，同样存在问题：

> Shockwave Flash has crashed.

排查如下：

  1. 打开 Firefox 附加组件页面，检查 flash 相关插件的安装情况，如下图：
    
    [resp_image id=&#8217;14778&#8242;]
    
    我们能看到两个版本的 flash 插件：
    
      * Shockwave Flash 15.0.0.239
      * Shockwave Flash 11.2.202.411
    
    两个插件的情况是：
    
      1. 两个都设置为 active，则 Flash 肯定崩溃
      2. 只设置一个为 active，则页面总是提示要开启 Flash
    
    怀疑是两个版本冲突的问题[^14669.1]。

  2. 使用 `zypper search` 命令检查系统下安装的 flash 相关软件：
    
        $ zypper search flash
        
    
    输出结果如下：
    
    其中 **chromium-pepper-flash** 比较可疑。

  3. 移除 chromium-pepper-flash：
    
        $ sudo zypper rm chromium-pepper-flash 
        
    
    弹出提示如下：
    
    > The following 2 packages are going to be REMOVED: chromium-pepper-flash freshplayerplugin
    > 
    > The following package is going to be upgraded: flash-player
    > 
    > 1 package to upgrade, 2 to remove. Overall download size: 11.6 MiB. Already cached: 0 B After the operation, 13.9 MiB will be freed. Continue? \[y/n/p/? shows all options\] (y): y (Use arrows or pgUp/pgDown keys to scroll the text by lines or pages.)
    
    提示说，chromium-pepper-flash 和 freshplayerplugin 将被移除，并且升级 flash-player。

移除后，重启 Firefox，Flash 可正常使用。

P.S. 图片由 Luna 提供。

[^14669.1]:    
    [How do I totally remove Shockwave Flash 15.0.0152 from my Addons in Ubuntu 12.04? | Firefox Support Forum | Mozilla Support][1]

 [1]: https://support.mozilla.org/en-US/questions/1024170