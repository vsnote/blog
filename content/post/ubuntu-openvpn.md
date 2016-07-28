---
title: 'Ubuntu  OpenVPN 设置'
author: 陈 三
layout: post
date: 2012-10-18T06:35:15+00:00
url: /ubuntu-openvpn.html
views:
  - 1381
dsq_thread_id:
  - 889929859
categories:
  - Ubuntu
tags:
  - OpenVPN
  - Ubuntu

---
Ubuntu 下的 OpenVPN 设置与 [Android OpenVPN 设置][1]很相近。

首先是在 Ubuntu 系统安装 OpenVPN:

    $ sudo apt-get install openvpn network-manager-openvpn
    

接着打开网络设置，Gnome 下叫 network connections，如下：

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/ubuntu-openvpn-set.png" alt="ubuntu vpn 设置" title="ubuntu vpn 设置" width="507" class="alignnone size-full wp-image-6294" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/ubuntu-openvpn-set.png 507w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/ubuntu-openvpn-set-300x191.png 300w" sizes="(max-width: 507px) 100vw, 507px" />][2]

选择 &#8220;VPN&#8221; 标签 -> Add

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/ubuntu-choose-openvpn.png" alt="ubuntu 选择 vpn 连接类型" title="ubuntu 选择 vpn 连接类型" width="565" class="alignnone size-full wp-image-6293" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/ubuntu-choose-openvpn.png 565w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/ubuntu-choose-openvpn-300x146.png 300w" sizes="(max-width: 565px) 100vw, 565px" />][3]

列表项中选择 OpenVPN，

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-setting.png" alt="openvpn 具体设置" title="openvpn-setting" width="727" class="alignnone size-full wp-image-6292" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-setting.png 727w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-setting-300x242.png 300w" sizes="(max-width: 727px) 100vw, 727px" />][4]

填入需要的信息，Authentication 选择 password，CA 文件选择从 VPN 服务器下载的 crt 文件，接着点击 Advanced 进入高级设置：

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-advance-set.png" alt="openvpn 高级设置" title="openvpn-advance-set" width="570" class="alignnone size-full wp-image-6291" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-advance-set.png 570w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-advance-set-300x88.png 300w" sizes="(max-width: 570px) 100vw, 570px" />][5]

将 General 标签页如上图所示的两个选项勾起来，第一个填入相应的端口。

然后保存。接下来连接这个 OpenVPN 就可以。

 [1]: http://www.zfanw.com/blog/android-openvpn-setting.html
 [2]: http://www.zfanw.com/blog/wp-content/uploads/2012/10/ubuntu-openvpn-set.png
 [3]: http://www.zfanw.com/blog/wp-content/uploads/2012/10/ubuntu-choose-openvpn.png
 [4]: http://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-setting.png
 [5]: http://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-advance-set.png