---
title: 空密码登录被禁止 (参见 允许空密码)
author: 陈 三
layout: post
date: 2014-04-19T16:44:14+00:00
excerpt: openSUSE下处理phpMyAdmin空密码登录被禁止的错误
url: /login-without-a-password-is-forbidden-by-configuration.html
views:
  - 873
categories:
  - openSUSE
tags:
  - MySQL

---
在openSUSE上，我是通过命令安装的phpMyAdmin：

    sudo zypper in phpMyAdmin
    

因为是在本机上开发，所以偷懒，没给MySQL数据库root用户设置密码。

通过<http://127.0.0.1/phpMyAdmin/>登录时会出现错误：

> 空密码登录被禁止 (参见 允许空密码)

phpMyAdmin的文档[^12391.2]说需要修改配置文件config.inc.php里的配置项$cfg\[&#8216;Servers&#8217;\]\[$i\][&#8216;AllowNoPassword&#8217;]。

打开命令行工具：

    cd /etc
    su
    cd phpMyAdmin
    vi config.inc.php
    

查找$cfg\[&#8216;Servers&#8217;\]\[$i\][&#8216;AllowNoPassword&#8217;]，将它的值false改成true，保存。

当然，你也可以用其他文本编辑工具。

这里之所以要用su命令，是因为我的情况下，sudo的权限还不够进入该目录。

之后再用空密码登录，就可以正常进入phpMyAdmin的管理界面。

如果在phpMyAdmin界面操作时会出现如下错误：

> Table &#8216;phpmyadmin.pma_\_table\_uiprefs&#8217; doesn&#8217;t exist

则请打开config.inc.php配置文件，把$cfg\[&#8216;Servers&#8217;\]\[$i\][&#8216;table_uiprefs&#8217;]的值修改为空值：

    $cfg['Servers'][$i]['table_uiprefs']       = '';
    

之后的操作就正常了。

[^12391.2]:    
    [Configuration — phpMyAdmin 4.2.0-beta1 documentation][1]

 [1]: http://docs.phpmyadmin.net/en/latest/config.html#cfg_Servers_AllowNoPassword