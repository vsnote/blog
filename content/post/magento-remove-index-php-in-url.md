---
title: Magento 移除 URL 中的 index.php
author: 陈 三
layout: post
date: 2013-07-16T14:08:20+00:00
url: /magento-remove-index-php-in-url.html
dsq_thread_id:
  - 1504322340
views:
  - 664
categories:
  - 未分类
tags:
  - Magento

---
默认情况下，Magento 搭建的网站，分类的 URL 范式是：

    http://www.example.com/index.php/category.html
    

URL 中的 `index.php` 会导致网址过长，移除它也没什么坏处，所以最好还是移除掉。

方法如下：

  1. 进入管理后台
  2. 打开 System -> Configuration 菜单项
  3. 左侧菜单树中找到 Web 选项卡，右侧子菜单中有 `Search Engine Optimization`，把 `Use Web Server Rewrites` 值从 no 改成 yes，保存。

注：本方法在 Magento 1.7.0.2 下测试有效。