---
title: Ubuntu 安装 Firefox.tar.bz2
author: 陈 三
layout: post
date: 2012-07-16T03:00:36+00:00
url: /ubuntu-firefox-tar-bz2.html
views:
  - 3327
dsq_thread_id:
  - 766947906
categories:
  - Firefox
tags:
  - Firefox
  - Ubuntu

---
**2013.5.8 更新** firefox 现在版本已经持后台自动更新，所以本篇介绍的仅限在 Ubuntu 上初次安装 firefox。

  1. 到 Mozilla 网站[下载 firefox][1]，假设保存到 ~/Downloads 目录。

  2. 将 Downloads 下的 firefox-13.0.1.tar.bz2 拷贝到 /opt 文件夹（这个安装位置可选），然后解压：
    
        % cd ~/Downloads
        % sudo cp firefox-13.0.1.tar.bz2 /opt
        % cd /opt
        % sudo tar -xvjf firefox-13.0.1.tar.bz2
        

解压后，/opt 下会出现一个 firefox 文件夹，在 /usr/bin/ 下重建软链接(soft link)

    % sudo ln -sf /opt/firefox/firefox /usr/bin/firefox
    

其中 -f 表示强制覆盖原有的软链接。

之后，就可以在命令行中使用 &#8220;firefox&#8221; 调用浏览器，如果使用 Unity 桌面系统，按 Alt-F2 输入 &#8220;firefox&#8221; 调用。

 [1]: http://www.mozilla.org/en-US/firefox/new/