---
title: openSUSE 安装使用 xmonad
author: 陈 三
layout: post
date: 2014-11-03T21:45:42+00:00
url: /opensuse-xmonad.html
views:
  - 640
categories:
  - openSUSE
tags:
  - xmonad

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 安装</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 启动与配置</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    在我用 Ubuntu 的时候，尝试过 <a href="http://xmonad.org/">xmonad</a>，颇喜欢。但奇怪的是，openSUSE 软件库中没有它，需要自行安装。好在 Haskell 本身提供有包管理工具 <a href="https://www.haskell.org/cabal/">cabal</a>，十分便利。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">安装</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    首先安装 <em>cabal-install</em> 工具：
  </p>
  
  <pre><code>$ sudo zypper install cabal-install
</code></pre>
  
  <p>
    安装完 <em>cabal</em> 后，检查其安装情况：
  </p>
  
  <pre><code>$ cabal --version
</code></pre>
  
  <p>
    通常会输出 <em>using version 1.16.0 of the Cabal library</em> 这样的内容。
  </p>
  
  <p>
    不过通常 openSUSE 库上的软件并非最新，可能需要升级 <em>cabal-install</em>：
  </p>
  
  <pre><code>$ cabal install cabal-install
</code></pre>
  
  <p>
    另外，我们还需要安装 GHC Haskell compiler，openSUSE 下安装方法：
  </p>
  
  <pre><code>$ sudo zypper install ghc
</code></pre>
  
  <p>
    紧接着更新 cabal 库：
  </p>
  
  <pre><code>$ cabal update
</code></pre>
  
  <p>
    然后安装 xmonad<fnref target="14144.1" />：
  </p>
  
  <pre><code>$ cabal install http://code.haskell.org/xmonad/xmonad.tar.gz
$ cabal install http://code.haskell.org/XMonadContrib/xmc.tar.gz
</code></pre>
  
  <p>
    安装完成后可以通过以下命令检查安装的情况：
  </p>
  
  <pre><code>$ xmonad --version
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i-2">启动与配置</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p class='text-danger'>
    如果你打算继续使用 KDE 提供的各种功能，而非完全的 xmonad，请访问我的另一篇博客 <a href="http://www.zfanw.com/blog/kde-with-xmonad.html" title="KDE 与 Xmonad">KDE 与 Xmonad</a>，忽略以下内容。
  </p>
  
  <p>
    接下来即是启动 xmonad。我原来的桌面环境是 KDE<fnref target="14144.2" />，需要做些配置。
  </p>
  
  <p>
    首先，在主目录下创建一个 <em>.xsession</em> 文件，并加入如下内容：
  </p>
  
  <pre><code>xmonad
</code></pre>
  
  <p>
    为了让登录时 xmonad 可选，在 <em>/usr/share/xsessions/</em> 目录下添加 <em>xmonad.desktop</em> 文件。
  </p>
  
  <pre><code>$ sudo vi /usr/share/xsessions/xmonad.desktop
</code></pre>
  
  <p>
    然后文件中添加如下内容：
  </p>
  
  <pre><code>   [Desktop Entry]
   Encoding=UTF-8
   Name=xmonad
   Comment=This session starts xmonad
   Exec=/home/sam/.cabal/bin/xmonad
   Type=Application
</code></pre>
  
  <p>
    注意，xmonad 可执行文件路径是 <em>/home/sam/.cabal/bin/xmonad</em>，需要将其加入 $PATH 环境变量中：
  </p>
  
  <pre><code>$ cd ~
$ vi .bashrc
</code></pre>
  
  <p>
    添加：
  </p>
  
  <pre><code>export PATH=$PATH:~/.cabal/bin
</code></pre>
  
  <p>
    登出 KDE，选择 xmond，再登录系统 &#8211; 哈，一片空白。
  </p>
  
  <p>
    别慌，这就是 xmonad，你可以按 <kbd>Alt + Shift + Enter</kbd> 调出终端窗口，如果玩了一会儿感觉不佳，可以按 <kbd>Alt + Shift + Q</kbd> 退出登陆，重新选择 KDE。
  </p>
  
  <footnotes>
    <fn name="14144.1">
      <p>
        <a href="http://xmonad.org/intro.html">xmonad : building and installation</a>
      </p>
    </fn>
    
    <fn name="14144.2">
      <p>
        <a href="https://www.haskell.org/haskellwiki/Xmonad/Frequently_asked_questions#How_can_I_use_xmonad_with_a_display_manager.3F_.28xdm.2C_kdm.2C_gdm.29">Xmonad/Frequently asked questions &#8211; HaskellWiki</a>
      </p>
    </fn>
  </footnotes>
</div>