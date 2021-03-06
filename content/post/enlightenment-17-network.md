---
title: Enlightenment 17 网络管理
author: 陈 三
layout: post
date: 2012-12-24T23:57:11+00:00
url: /enlightenment-17-network.html
views:
  - 752
dsq_thread_id:
  - 990920369
categories:
  - Ubuntu
tags:
  - Enlightenment
  - Ubuntu

---
[Enlightenment][1] 新近推出 17，即 0.1.7 版本。

对我来说，用哪个桌面环境区别不大，只要能让我自定义快捷键。所以很快我就从 Gnome 3.6 切换到 Enlightenment 17 版本。

Enlightenment 有几个让我惊讶的用法，按它官方的说法，则也是有别于其他桌面环境的特色内容。

比如当光标放在屏幕右侧时，这时调用 Enlightenment 的菜单，菜单里的子菜单会出现在屏幕外面 &#8211; 这样我们就点击不到子菜单了。常见的软件处理方式是将子菜单自动往左侧展开，但 Enlightenment 不是，你只要将光标继续往右侧子菜单位置上移动时，父菜单会往左移动，然后子菜单从屏幕外退出来。这样的好处是，鼠标不需要再移到左侧去点击，需要移动的距离也短了。

另外一个是关于虚拟桌面。当光标位于屏幕边缘时，默认情况下会切换到旁边一个虚拟桌面。比如，我把光标往右侧屏幕外移动，Enlightenment 会自动帮我切换到右侧一个虚拟桌面。我可以预见的是，这时的光标位置应该是在右侧的虚拟桌面的屏幕右侧，但恰恰相反，它是在左侧。你要做的是继续往右移。也就是说，这些虚拟桌面是连成一片的。

以上两种用法算是对我惯常用法的一种颠覆。

然后再来说网络管理。

根据 [Arch Linux 上的说明][2]，则 E17 倾向于使用网络管理工具 ConnMan &#8211; 虽然也可以使用 NetworkManager。

但是，从 E17 加载的 Modules 来看，其中 Connection Manager 调用的是 EconnMan，于是为了在 E17 的 shelf 上使用网络管理功能，需要[安装 EconnMan][3]，否则 E17 的 Shelf 上会显示一个白色感叹号，点击它的设置时会显示错误 「This module wants to execute an external application EConnMan that does not exist.Please install EConnMan application.」 &#8211; 而况据开发者的说明，它目前并没有管理 VPN 的功能。

只好另找方法。

E17 的 Modules 中有个 Systray，类似 Windows 平台下的系统托盘概念，可以用于显示输入法、网络连接等等。

这里，通过命令行：

    nm-applet
    

就可以调用网络连接出来，让它显示在 systray 中。

为了让 E17 每次启动都自动启用它，打开 E17 菜单：

Settings -> Settings Panel -> Apps -> Startup Applications -> System -> Network

然后重启系统，systray 里已经有网络管理，接下来我们就可以像 Gnome 或 Windows 7 里那样通过点击该图标进行网络连接的管理。

 [1]: http://enlightenment.org/
 [2]: https://wiki.archlinux.org/index.php/E17#Configuring_the_Network
 [3]: http://blog.gustavobarbieri.com.br/2012/08/12/econnman-1-released/