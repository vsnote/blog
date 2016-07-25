---
title: zencart 插件 Google base(froogle) feeder 的安装使用
author: 陈 三
layout: post
date: 2012-01-04T07:46:48+00:00
url: /zencart-addon-google-base-froogle-feeder.html
dsq_thread_id:
  - 526196100
views:
  - 800
categories:
  - 未分类
tags:
  - zencart

---
最近帮同学整一个外贸网站的优化，因此接触了 [zencart][1] 程序，后台管理还算清晰，只是生成的 HTML 比较老旧，用的 table 布局，层叠十几层的都有，我花了不少时间改成 div + css。

因为网站主要针对 Google 优化，所以注意到 [Google 有个 shopping 产品][2] ，就打算将网站加入 Google 的产品索引库。提交页面为<http://www.google.com/intl/en_us/products/submit.html>，用 Google 帐户登录后，需要我们提交 data feeds 文件。

如果网站产品很多，则手动生成这样一个文件就比较要命，zencart 有 Google base(froogle) feeder 插件可以帮助生成。

  1. 从 [Google base(froogle) feeder 链接][3]下载 zip 文件，里面有个 catalog 文件夹，将文件夹下的文件全部上传到 zen cart 站点根目录，其实就是将 catalog 文件夹下的文件合并进去。

  2. 上传完成后，登录后台管理，Tools -> Install SQL Patches（工具 ->安装 SQL 脚本），将上述的 zip 文件里的 install.sql 文件内容拷入，然后运行。

  3. 再接着是 Configuration -> Google Merchant Center Configuration（商店设置 -> Google Merchant Center Configuration）,将该设置的内容设置下。

  4. 接着到 Tools -> Google Merchant Center Feeder 生成 xml 文件，假如上一步设置过 Google Merchant Center ftp 用户名与密码，就可以在此界面下上传 xml 到 Google Merchant Center，不过据我的经历，比较慢，不如直接上传。

  5. 其他若有问题可以查看 zip 文件下的 readme.html 帮助文件。

 [1]: http://www.zen-cart.com/ "zencart 官网"
 [2]: http://www.google.com/prdhp?hl=en&tab=wf
 [3]: http://www.zen-cart.com/index.php?main_page=product_contrib_info&products_id=473