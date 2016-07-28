---
title: openSUSE 安装最新版 Firefox
author: 陈 三
layout: post
date: 2014-12-02T12:30:08+00:00
url: /opensuse-install-latest-firefox.html
views:
  - 698
categories:
  - openSUSE
tags:
  - Firefox

---
openSUSE 官方提供的 Firefox [^14654.1]版本通常要低于最新发布的 Firefox。比如现在，Firefox 最新版本是 34，但 openSUSE 源上提供的还是 Firefox 33。所以，如果你要在 Firefox 最新版本发布后尽快使用到，则最好使用 Mozilla 提供的第三方软件源[^14654.2]。

操作步骤如下（下面我以 openSUSE 13.2 操作系统为例）：

  1. 添加 Mozilla 软件源
    
        $ sudo zypper ar -f http://download.opensuse.org/repositories/mozilla/openSUSE_13.2/ Mozilla
        

  2. 更新软件源
    
        $ sudo zypper ref
        

  3. 安装 Mozilla 软件源下的 Firefox
    
        $ sudo zypper in Mozilla:MozillaFirefox
        
    
    其中 `Mozilla` 即第一步中设置的软件源的别名（alias）。

安装 Firefox 时，可能会有依赖冲突的提示，按 openSUSE 系统的建议操作即可。

[^14654.1]:    
    [openSUSE 官方源中的 Firefox][1]

[^14654.2]:    
    [Mozilla 提供的第三方软件源][2]

 [1]: http://software.opensuse.org/package/MozillaFirefox
 [2]: https://en.opensuse.org/Additional_package_repositories#Mozilla