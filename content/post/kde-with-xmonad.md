---
title: KDE 与 Xmonad
author: 陈 三
layout: post
date: 2014-12-06T03:23:11+00:00
excerpt: KDE 桌面环境中使用 xmonad 窗口管理器
url: /kde-with-xmonad.html
views:
  - 1011
categories:
  - openSUSE
tags:
  - KDE
  - xmonad

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_Xmonad"><span class="toc_number toc_depth_1">1</span> 安装 Xmonad</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_xmonadhs"><span class="toc_number toc_depth_1">2</span> 配置 xmonad.hs</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 设置窗口管理器</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">4</span> 附录</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    之前我写过一篇博客 <a href="http://www.zfanw.com/blog/opensuse-xmonad.html">openSUSE 下的 xmonad</a>，讲的是完整的 xmonad 环境，这篇讲 <strong>KDE 下如何使用 xmonad</strong>，好处是 KDE 的许多功能都可以使用，只是窗口管理器换成 xmonad。
  </p>
  
  <blockquote>
    <p>
      系统环境：openSUSE 13.2
    </p>
  </blockquote>
  
  <h2 class="storycontent-h2">
    <span id="_Xmonad">安装 Xmonad</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Xmonad" href="#_Xmonad"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    参照<a href="http://www.zfanw.com/blog/opensuse-xmonad.html">前一篇说明</a>，使用 <code>cabal</code> 安装 xmonad。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_xmonadhs">配置 xmonad.hs</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_xmonadhs" href="#_xmonadhs"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    打开 <code>~/.xmonad/xmonad.hs</code> 文件，将内容改为如下<fnref target="14705.1" />：
  </p>
  
  <pre><code>import System.IO

import XMonad
import XMonad.Config.Kde
import XMonad.Hooks.SetWMName
import XMonad.Util.WindowProperties (getProp32s)

main = do
  xmonad kde4Config {
    terminal = "konsole"
  , modMask = mod4Mask
  , startupHook = setWMName "LG3D"
  , manageHook = ((className =? "krunner") &gt;&gt;= return . not --&gt; manageHook kde4Config)
      &lt;+&gt; (kdeOverride --&gt; doFloat)
}

kdeOverride :: Query Bool
kdeOverride = ask &gt;&gt;= \w -&gt; liftX $ do
    override &lt;- getAtom "_KDE_NET_WM_WINDOW_TYPE_OVERRIDE"
    wt &lt;- getProp32s "_NET_WM_WINDOW_TYPE" w
    return $ maybe False (elem $ fromIntegral override) wt
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="i">设置窗口管理器</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    先用 <code>which</code> 命令查看 xmonad 路径：
  </p>
  
  <pre><code>sam@linux-qo4p:~|master⚡⇒  which xmonad 
/home/sam/.cabal/bin/xmonad
</code></pre>
  
  <p>
    在 <em>~/.kde4/env</em> 目录（<strong>如果是 <a href="https://www.kde.org/announcements/plasma5.0/" title="plasma 5, kde 5">Plasma5</a> 的话则是在 ~/.config/plasma-workspace/env **）下创建 **set_window_manager.sh</strong> 文件，添加如下内容：
  </p>
  
  <pre><code>export KDEWM=/home/sam/.cabal/bin/xmonad
</code></pre>
  
  <p>
    修改文件权限，允许文件执行：
  </p>
  
  <pre><code>$ chmod 755 set_window_manager.sh
</code></pre>
  
  <p>
    注销 KDE 会话，然后再登录进去，KDE 的窗口管理器已经从 kwin 换成 Xmonad 了<fnref target="14705.2" />，如下图：
  </p>
  
  <p>
    [resp_image id=&#8217;14769&#8242; caption=&#8221; ]
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">附录</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="https://github.com/chenxsan/rc-files/blob/master/.xmonad/xmonad.hs">存放在 Github 上的我的 xmonad.hs 配置文件</a>
    </li>
  </ol>
  
  <footnotes>
    <fn name="14705.1">
      <p>
        <a href="https://code.google.com/p/xmonad/issues/attachmentText?id=430&aid=-7752565881665183817&name=xmonad.hs&token=ABZ6GAfGlZ9LEhxXYjzpcH9ZO25qwQmc0w%3A1417834536394">Google Code 上的一个 xmonad.hs 配置文件（英文）</a>
      </p>
    </fn>
    
    <fn name="14705.2">
      <p>
        <a href="https://www.haskell.org/haskellwiki/Xmonad/Using_xmonad_in_KDE">HaskellWiki 教你如何在 KDE 下使用 Xmonad（英文）</a>
      </p>
    </fn>
  </footnotes>
</div>