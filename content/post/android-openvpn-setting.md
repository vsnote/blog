---
title: 'Android  OpenVPN 设置'
author: 陈 三
layout: post
date: 2012-10-12T09:41:27+00:00
url: /android-openvpn-setting.html
views:
  - 4386
dsq_thread_id:
  - 882072252
categories:
  - 未分类
tags:
  - Android
  - OpenVPN

---
Android 自 ICS 4.0 版本起，在手机上使用 VPN 会强制要求启用 PIN 码或者密码。对我来说，这非常麻烦，于是很长一段时间，我都懒得在手机上开 VPN。

直到有一天，在 twitter 时间线上发现 [OpenVPN for Android][1]。

OpenVPN for Android 是一个 **OpenVPN 客户端**，无需 root 系统就能使用，另外，也是最重要的，我无需启用 PIN 码或密码了。而且设置简便，只要系统版本 4.0 以上即可。

首先，你需要一个 OpenVPN 账户，免费的、收费的均可。登录你的账户，根据你 VPN 提供商的说明下载 ca 文件，保存为 openvpn.crt，然后传输到手机上备用。

在手机上安装好 OpenVPN for Android，打开，如下图：

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-1.jpg" alt="选择 vpn 列表" title="openvpn-1" width="480"  class="alignnone size-full wp-image-6125" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-1.jpg 480w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-1-300x90.jpg 300w" sizes="(max-width: 480px) 100vw, 480px" />][2]

如上图所示，点击 “VPN 列表”进入下一个界面

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-2.jpg" alt="添加 vpn 配置" title="openvpn-2" width="480"  class="alignnone size-full wp-image-6126" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-2.jpg 480w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-2-300x57.jpg 300w" sizes="(max-width: 480px) 100vw, 480px" />][3]

选择上图中右上方的加号图标，添加配置文件，名称任取。

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-3.jpg" alt="基本配置内容" title="openvpn-3" width="480"  class="alignnone size-full wp-image-6127" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-3.jpg 480w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-3-300x84.jpg 300w" sizes="(max-width: 480px) 100vw, 480px" />][4]

设置界面有许多内容，据我经验，只要设置”基本“即可。

点击”基本“后将进入具体设置内容，如下图：

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn1.jpg" alt="openvpn 具体设置内容" title="openvpn" width="480"  class="alignnone size-full wp-image-6116" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn1.jpg 480w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn1-202x300.jpg 202w" sizes="(max-width: 480px) 100vw, 480px" />][5]

将已有的资料填入上图，比如 VPN 地址、端口、用户名、密码，其中 **VPN 类型**选择**用户名/密码**，CA 证书选择之前下载并上传到手机的 openvpn.crt。后退即自动保存信息。

之后连接。而且据我的使用经历，OpenVPN 要比 PPTP/L2TP 稳定多了。<div class=timeline> 

## 修订历史

  1. 2012-11-15：[OpenVPN Connect][6]，比 OpenVPN for Android 的使用更简单，直接从服务器上下载 ovpn 配置文件，然后在 OpenVPN Connect 中导入该文件即可连接。
  2. <span itemprop='dateModified'>2013-04-30</span>：我的 VPN 商认为，OpenVPN 彻底歇菜，于是他的后台里 OpenVPN 也没影了。</div>

 [1]: https://play.google.com/store/apps/details?id=de.blinkt.openvpn&hl=en
 [2]: http://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-1.jpg
 [3]: http://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-2.jpg
 [4]: http://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn-3.jpg
 [5]: http://www.zfanw.com/blog/wp-content/uploads/2012/10/openvpn1.jpg
 [6]: https://play.google.com/store/apps/details?id=net.openvpn.openvpn&hl=en