---
title: 安装 Plasma 5 的错误 plasmashell closed unexpected
author: 陈 三
layout: post
date: 2015-01-23T17:45:35+00:00
url: /plasma-5-plasmashell-closed-unexpected.html
views:
  - 750
categories:
  - openSUSE
tags:
  - KDE
  - Plasma 5

---
最近盯上 [Plasma 5][1]，于是就在我的 openSUSE 13.2 上安装。

  1. 先是按照 [openSUSE 说明][2]添加两个库：
    
      * `$ sudo zypper ar -f http://download.opensuse.org/repositories/KDE:/Frameworks5/openSUSE_13.2/ Frameworks5`
      * `$ sudo zypper ar -f http://download.opensuse.org/repositories/KDE:/Qt5/openSUSE_13.2/ qt5`

  2. 接着安装 Plasma 5：
    
    `$ sudo zypper in plasma5-session`
    
    安装 plasma 5 过程中会卸载掉许多 KDE 4 相关的内容，别怕，如果有冲突，通常选 1 然后回车确认就对了。

  3. 重启系统。

进入系统后，随即有个窗口报错：

> We are sorry, plasmashell closed unexpectedly. You cannot report this error, because plasmashell does not provide a bug reporting address.
> 
> Detais:
> 
> Executable: plasmashell PID: 1536 Signal: Aborted (6) Time: 1/23/15 14:31:50

也可以[点击看图片][3]。

注意，图中的窗口关掉后桌面只是一片空白。但因为我的 KDE 的窗口管理器用的是 xmonad，所以仍然可以调用出 konsole，通过命令行操作、打开 Firefox、连接网络等。

找了许多材料，没什么效果，最后跑 [KDE 论坛发贴][4]，但整天下来都没人回复，只好自己再接再厉。最后运气女神终于同情了我。

## 解决办法

  1. 查看上面添加的两个库的对应 ID：
    
    `$ zypper lr`
    
    我的结果如下：
    
    <pre>sam@orchid:~|master⚡⇒  zypper lr
#  | Alias                                  | Name                                   | Enabled | Refresh
---+----------------------------------------+----------------------------------------+---------+--------
 1 | Firefox                                | Firefox                                | Yes     | Yes    
 2 | Framewordks5                           | Frameworks5                            | Yes     | Yes    
 3 | Java:packages                          | Java:packages                          | Yes     | Yes    
 4 | M17N                                   | M17N                                   | Yes     | Yes    
 5 | MargueriteSu                           | MargueriteSu                           | Yes     | Yes    
 6 | Mozilla                                | Mozilla                                | Yes     | Yes    
 7 | Node.js                                | Node.js                                | Yes     | Yes    
 8 | PackMan_Essentials                     | PackMan_Essentials                     | Yes     | Yes    
 9 | X11:Bumblebee                          | X11:Bumblebee                          | Yes     | Yes    
10 | X11_WindowManagers                     | X11_WindowManagers                     | Yes     | Yes    
11 | devel:languages:nodejs                 | devel:languages:nodejs                 | Yes     | Yes    
12 | dvd                                    | dvd                                    | Yes     | Yes    
13 | games:tools                            | games:tools                            | Yes     | Yes    
14 | google-chrome                          | google-chrome                          | Yes     | Yes    
15 | google-webdesigner                     | google-webdesigner                     | Yes     | Yes    
16 | home:Mailaender:branches:Java:packages | home:Mailaender:branches:Java:packages | Yes     | Yes    
17 | home:opensuse_zh                       | home:opensuse_zh                       | Yes     | Yes    
18 | home:ralflangb1:composer2distribution  | home:ralflangb1:composer2distribution  | No      | Yes    
19 | home:ruiabreuferreira                  | home:ruiabreuferreira                  | Yes     | Yes    
20 | home:ykoba                             | home:ykoba                             | Yes     | Yes    
21 | libdvdcss                              | libdvdcss                              | Yes     | Yes    
22 | mono-project                           | mono-project                           | Yes     | Yes    
23 | openSUSE:13.2:NON-OSS                  | openSUSE:13.2:NON-OSS                  | Yes     | Yes    
24 | openSUSE:13.2:OSS                      | openSUSE:13.2:OSS                      | Yes     | Yes    
25 | qt5                                    | qt5                                    | Yes     | Yes    
26 | repo-source                            | openSUSE-13.2-Source                   | Yes     | Yes    
27 | repo-update                            | openSUSE-13.2-Update                   | Yes     | Yes    
28 | repo-update-non-oss                    | openSUSE-13.2-Update-Non-Oss           | Yes     | Yes    
29 | security                               | security                               | Yes     | Yes    
30 | utilities                              | utilities                              | Yes     | Yes    
31 | zh                                     | zh   
</pre>

  2. 更新软件
    
    `$ sudo zypper dup --from 2 --from 25`
    
    这里，我强制要求软件从 ID 为 2 和 25 的库升级。</ol> 
    
    最后重启系统，能正常进入 Plasma 5 了。
    
    当然，以上仅是我个人情况，如果你也碰上，并恰巧通过搜索引擎来到这一篇，请仅做参考。如果你因此搞坏了系统，本人不打算心怀歉意。

 [1]: https://www.kde.org/announcements/plasma5.0/
 [2]: https://en.opensuse.org/SDB:KDE_repositories#KDE_Frameworks_5_.26_Plasma_5
 [3]: http://drp.io/myk
 [4]: https://forum.kde.org/viewtopic.php?f=289&t=124595