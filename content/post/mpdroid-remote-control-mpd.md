---
title: Android 手机上 MPDroid 遥控 MPD
author: 陈 三
layout: post
date: 2012-10-08T04:15:14+00:00
url: /mpdroid-remote-control-mpd.html
views:
  - 1616
dsq_thread_id:
  - 875968593
categories:
  - Ubuntu
tags:
  - MPD
  - MPDroid
  - Ubuntu

---
[MPDroid][1] 是一个 MPD 客户端，从它的名称里的 &#8220;Droid&#8221; 可以看出，它是个 Android 应用软件。既然它是个 MPD 客户端，我们也就可以通过它控制 MPD 服务器里的音乐，还可以 streaming MPD 服务器上的音乐到手机即客户端。

首先是安装 MPD，我曾经写过一篇简单介绍 [MPD 与 Ncmpcpp 安装使用][2]的内容，也可以查阅 [Wikia 上 MPD 相关资料][3] 进行安装配置。

安装完 MPD 后是修改 mpd.conf 文件：

    $ sudo gvim /etc/mpd.conf
    

查找下列内容并修改结果如下：

    #bind_to_address     "localhost"
    
    bind_to_address    "0.0.0.0"  #这一行是新增加的内容
    
    port    6600
    
    audio_output {
        type        "httpd"
        name        "My HTTP Stream"        # 这个名称可任意修改
        encoder     "vorbis"        # optional, vorbis or lame
        port        "8000"
    #   quality     "5.0"           # do not define if bitrate is defined
        bitrate     "128"           # do not define if quality is defined
        format      "44100:16:1"
    }
    

保存 mpd.conf 文件后需要重启 MPD:

    $ sudo /etc/init.d/mpd restart
    

接着，从 Google Play 上下载 [MPDroid 应用][1]到手机，安装好打开，初始界面如下：

<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/mpdroid-setting-168x300.jpg" alt="mpdroid 初始界面" title="mpdroid 初始设置界面" width="168"  class="alignnone size-medium wp-image-6017" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/mpdroid-setting-168x300.jpg 168w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/mpdroid-setting.jpg 480w" sizes="(max-width: 168px) 100vw, 168px" />

选择 &#8220;Default connection settings&#8221;，另外一个是 &#8220;Wlan based connection&#8221;，可以针对不同的无线网络设置不同 ip：

<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/mpdroid-wlan-setting-168x300.jpg" alt="mpdroid 无线局域网设置" title="mpdroid 设置无线局域网连接" width="168"  class="alignnone size-medium wp-image-6019" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/mpdroid-wlan-setting-168x300.jpg 168w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/mpdroid-wlan-setting.jpg 480w" sizes="(max-width: 168px) 100vw, 168px" />

填写 &#8220;Host&#8221; 与 &#8220;Streaming Host&#8221;，这是 MPD 服务器所在的电脑的 ip 地址，比如我的电脑在局域网的 ip 为 192.168.1.101，Ubuntu 上可以通过以下命令查看：

    $ ifconfig
    

因为 MPDroid 上使用 MPD 服务器所在电脑的 ip 地址来连接，所以电脑的 ip 最好手动分配，DHCP 分配的话每次的 ip 不同，就需要 MPDroid 设置里每次都做修改。

设置完成后，通过按 Android 手机的 Menu 键打开 MPDroid 的 ”Main Menu&#8221;，点击进入音乐控制的主界面：

<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/mpdroid-playing1.jpg" alt="mpdroid 播放音乐中" title="mpdroid 控制播放音乐" width="480"  class="alignnone size-full wp-image-6028" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/mpdroid-playing1.jpg 480w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/mpdroid-playing1-168x300.jpg 168w" sizes="(max-width: 480px) 100vw, 480px" />

一目了然的界面。

要将 MPD 服务器上的音乐 streaming 到手机，即通过手机播放 MPD 服务器上的音乐，如下图所示，可以通过 Android 手机的 Menu 按键调用该菜单，勾选 streaming 就可以开始播放，如果没有声音，请点击上一张图片的**音响**图标进入查看 OUTPUTS 是否勾选了名称为 &#8220;My HTTP Stream&#8221; 的声音输出。

<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/mpdroid-playing-streaming.jpg" alt="mpdroid streaming 播放中" title="mpdroid-playing-streaming" width="168"  class="alignnone size-full wp-image-6024" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/mpdroid-playing-streaming.jpg 480w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/mpdroid-playing-streaming-168x300.jpg 168w" sizes="(max-width: 480px) 100vw, 480px" />

这样，我就可以把手机当成电脑上音乐播放的遥控器；如果无聊，也可以同时在电脑和手机上播放音乐，不过如果在电脑/手机上同时播放时，因为 MPDroid 在手机上 streaming 会有缓冲，于是会慢电脑上几秒，结果就演成“二重唱”了。

 [1]: https://play.google.com/store/apps/details?id=com.namelessdev.mpdroid&hl=en
 [2]: http://www.zfanw.com/blog/ubuntu-mpd-ncmpcpp.html
 [3]: http://mpd.wikia.com/wiki/Music_Player_Daemon_Wiki