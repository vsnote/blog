---
title: PhoneGap打包错误
author: 陈 三
layout: post
date: 2014-07-22T22:31:52+00:00
excerpt: 打包PhoneGap目录碰上exit code 8错误的一种解决办法
url: /phonegap-error-exit-code-8.html
views:
  - 905
categories:
  - 前端开发
tags:
  - PhoneGap

---
在我安装、配置好PhoneGap项目的所有依赖后，试图执行

    $ cordova run android
    

命令时，出现过如下错误。

`cordova build android`或`cordova emulate android`的结果也是一样。

但其实真正的问题在上面几行：

这是因为项目下有多个node_modules目录，被重复打包而引发的`Command failed with exit code 8`问题。

解决办法是修改`platforms/android/build.xml`：

    <property name="aapt.ignore.assets" value="&lt;dir&gt;node_*" />
    

将node_modules目录排除掉，就可以正常执行`cordova`命令。