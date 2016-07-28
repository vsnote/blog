---
title: Babun – Windows系统下的Linux环境
author: 陈 三
layout: post
date: 2014-05-15T04:31:53+00:00
url: /babun-linux-environment-in-windows.html
views:
  - 1883
categories:
  - 未分类
tags:
  - Windows

---
我还记得我在windows系统下安装cygwin[^12744.1]的过程，并不是件让人开心的事。安装完后，似乎又为中文显示乱码的事折腾许久。再后来，换了Git bash[^12744.2]，才稍稍感觉好点。又因为Git bash没有tmux[^12744.3]或GNU Screen[^12744.4]的多标签页功能，一旦窗口开多了，管理也麻烦。于是又找了conemu[^12744.5]，标签页是有，但切换的效率还是太低。

但现在可以试试[Babun][1]。

简单说，这是个配置好的Cygwin，并增加了一些特性，比如：

  1. pact &#8211; 软件包管理器
  2. 集成oh-my-zsh
  3. 配置好的git和shell
  4. 自动升级

举软件包管理器来说，我要安装tmux：

    $ pact find tmux
    $ pact install tmux
    

如果你用过apt-get或zypper，就会非常熟悉这一套。

Babun的安装也非常简单，从它的主页下载压缩包，解压，双击执行install.bat。

只是它的压缩包有点大，总共200多M，可是相比折腾Cygwin的痛苦，下载久一点根本没什么。

[^12744.1]:    
    [Cygwin][2]

[^12744.2]:    
    [Git for Windows][3]

[^12744.3]:    
    [tmux][4]

[^12744.4]:    
    [GNU Screen &#8211; GNU Project &#8211; Free Software Foundation][5]

[^12744.5]:    
    [conemu-maximus5 &#8211; Windows Console Emulator, Far Manager plugins &#8211; Google Project Hosting][6]

 [1]: http://babun.github.io/
 [2]: http://www.cygwin.com/
 [3]: http://msysgit.github.io/
 [4]: http://tmux.sourceforge.net/
 [5]: http://www.gnu.org/software/screen/
 [6]: https://code.google.com/p/conemu-maximus5/