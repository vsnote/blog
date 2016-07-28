---
title: BackWPup 更新至3.0.4
author: 陈 三
layout: post
date: 2013-03-04T23:39:22+00:00
url: /backwpup-3-0-4.html
views:
  - 517
dsq_thread_id:
  - 1120346797
categories:
  - WordPress
tags:
  - Dropbox
  - Wordpress

---
BackWPup 是我用的一个免费 WordPress 插件，用于定期将网站数据库、文件备份至 Dropbox，但从版本3开始后，在备份数据库过程出现如下错误：

> ERROR: No MySQLi extension found. Please install it.

因为 BackWPup 自版本3起使用 MySQLi 扩展备份数据库，服务器不曾安装 MySQLi，数据库的备份只能失败并抛出错误。

而且，看作者的意思，是不打算做任何 fallback 的。

所以，解决办法是，在服务器上安装 MySQLi 这个 PHP 扩展，或者继续使用 BackWPup 2.xx 版本。

附：[它的版本变化说明][1]。

**更新**：

2014.4.9 目前 BackWpup 已经更新至3.1.2版本，并且我的情况可正常备份，不知道是作者想不开又继续支持 MySQL 还是主机商安装 MySQLi 了。

 [1]: http://wordpress.org/extend/plugins/backwpup/changelog/