---
title: Magento复制站点
author: 陈 三
layout: post
date: 2014-08-26T14:34:22+00:00
url: /magento-clone-site.html
views:
  - 565
categories:
  - 未分类
tags:
  - Magento

---
Magento 的模板配置十分麻烦，所以有人贪图省事，就直接复制已有的站点，方法如底部链接所示[^13420.1]。

但不幸的是，我碰上一个问题：新域名会被强制 302 跳转到老的域名。我十分仔细地确认了数据库里的 `core_config_data` 表里的两个 URL 配置：

  1. web/unsecure/base_url
  2. web/secure/base_url

均已指向新域名，没有问题。

新域名的管理后台网址倒是可以访问到，但查看源代码的话，js、css 等的链接全是旧域名的。

注意，我对 `core_config_data` 表做的两个修改是通过 phpMyAdmin 界面完成的。

问题就在这里。

通过 phpMyAdmin 左侧的 `filter` 功能过滤出来的 `core_config_data` 表格其实有两个，而我改了不是我真正应该改的表格。

最后还是 SQL 语句靠谱点：

    SELECT * FROM `database_name`.`core_config_data` 
    

[^13420.1]:    
    [How to copy a Magento installation to a new domain | ITworld][1]

 [1]: http://www.itworld.com/it-management/360898/how-copy-magento-installation-new-domain