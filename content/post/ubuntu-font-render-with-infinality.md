---
title: Ubuntu 字体设置与 infinality
author: 陈 三
layout: post
date: 2012-10-11T05:36:31+00:00
url: /ubuntu-font-render-with-infinality.html
views:
  - 2676
dsq_thread_id:
  - 880647356
categories:
  - Ubuntu
tags:
  - infinality
  - Ubuntu
  - 字体设置

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_fontconfig-infinality"><span class="toc_number toc_depth_1">1</span> 安装 fontconfig-infinality 配置文件</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_freetype"><span class="toc_number toc_depth_1">2</span> 给 freetype 源文件打补丁</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 其他设置内容</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">4</span> 效果图</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">5</span> 鸣谢</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <strong>说明 2013.11.28</strong>：本文写于2012年，内容与最新的 infinality 可能不一样，如有出入，请以官网说明为准。
  </p>
  
  <p>
    我眼神不大好。见着别人说操作系统的字体可以渲染得怎样清晰和好看，但身边没有样例，就只好发挥自己的想象力。可惜实在想不出来，就找相关图片看了下，确实要比 Ubuntu 默认下的清晰、好看。
  </p>
  
  <p>
    于是想尝试一下，就找来 infinality &#8211; 这是因为在推上见<a href="https://twitter.com/doublechou">玛丽苏</a>提过。结果先是不小心把 /etc/fonts/conf.d 文件夹给删了，当时还没想着处理，只一味担心重启系统后会出问题，结果发现，Ubuntu 竟然还能启动，还能打出中文，只是字体变了样子，与原来见的不一样，如下：
  </p>
  
  <p>
    <a href="http://www.zfanw.com/blog/wp-content/uploads/2012/10/Screenshot-from-2012-10-09-233813.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/Screenshot-from-2012-10-09-233813.png" alt="删除 /etc/fonts/conf.d 后的字体" title="Screenshot from 2012-10-09 23:38:13" width="617"  class="alignnone size-full wp-image-6154" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/Screenshot-from-2012-10-09-233813.png 617w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/Screenshot-from-2012-10-09-233813-300x70.png 300w" sizes="(max-width: 617px) 100vw, 617px" /></a>
  </p>
  
  <p>
    接着找了些资料，心里约摸觉得把 fontconfig-config 包重装一下就好：
  </p>
  
  <pre><code>$ sudo apt-get --reinstall install fontconfig-config
</code></pre>
  
  <p>
    切换到 etc/fonts/ 目录下，果然出来 conf.d 文件夹，重启系统，字体如下图：
  </p>
  
  <p>
    <a href="http://www.zfanw.com/blog/wp-content/uploads/2012/10/Screenshot-from-2012-10-09-234606.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/Screenshot-from-2012-10-09-234606.png" alt="ubuntu字体设置" title="Screenshot from 2012-10-09 23:46:06" width="542"  class="alignnone size-full wp-image-6155" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/Screenshot-from-2012-10-09-234606.png 542w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/Screenshot-from-2012-10-09-234606-300x153.png 300w" sizes="(max-width: 542px) 100vw, 542px" /></a>
  </p>
  
  <p>
    你可能要问：有区别吗？抱歉，这真是难到我了。
  </p>
  
  <p>
    在我来看，这两张 GVIM 截图并没什么区别，大概是 GVIM 渲染方法不同，又或者我选择的字型的问题。不过在网页里，前后的区别倒一眼就能看出。不过不曾截图。
  </p>
  
  <p>
    以下进入正题，<strong>Ubuntu</strong> 下如何使用 <strong>infinality</strong> 美化字体。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_fontconfig-infinality">安装 fontconfig-infinality 配置文件</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_fontconfig-infinality" href="#_fontconfig-infinality"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    首先，到 infinality 网站下载两个压缩包：
  </p>
  
  <ol>
    <li>
      <a href="http://www.infinality.net/fedora/linux/zips/freetype-infinality-2.4.10-20120616_01-x86_64.tar.bz2">freetype-infinality-2.4.10-20120616_01-x86_64.tar.bz2</a>
    </li>
    <li>
      <a href="http://www.infinality.net/fedora/linux/zips/fontconfig-infinality-1-20120615_1.tar.bz2">fontconfig-infinality-1-20120615_1.tar.bz2</a>
    </li>
  </ol>
  
  <p>
    譬如都下载到 ~/Downloads 目录下，将 fontconfig-infinality 压缩包解压到 /etc/fonts/ 目录下：
  </p>
  
  <pre><code>$ cd ~/Downloads
$ tar -jfxv fontconfig-infinality-1-20120615_1.tar.bz2 -C /etc/fonts/
</code></pre>
  
  <p>
    这样，/etc/fonts/ 目录下会出现一个子目录 infinality。
  </p>
  
  <p>
    根据 infinality 目录下 README 的说明，需要为 /etc/fonts/conf.d/ 下的 52-infinality-conf 创建一个软链接(symlink)指向 /etc/fonts/infinality/ 下的 infinality.conf：
  </p>
  
  <pre><code>$ cd /etc/fonts/conf.d/
$ sudo ln -sf ../infinality/infinality.conf 52-infinality-conf
</code></pre>
  
  <p>
    接着是调整 /etc/fonts/infinality/infinality.conf 文件配置，这是一个 XML 文件，可以手动修改，也可以通过运行 infinality 目录下的 infctl.sh 来设置：
  </p>
  
  <pre><code>$ cd /etc/fonts/infinality
$ sudo ./infctl.sh setstyle
</code></pre>
  
  <p>
    这时会弹出 8 个预设值供你选择: 1) debug 2) infinality 3) linux 4) osx 5) osx2 6) win7 7) win98 8) winxp
  </p>
  
  <p>
    比如我选择 2，然后按 Enter 确认，会出现一个结果信息：
  </p>
  
  <pre><code>conf.d -&gt; styles.conf.avail/infinality
</code></pre>
  
  <p>
    这是修改了一个软链接指向。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_freetype">给 freetype 源文件打补丁</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_freetype" href="#_freetype"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    从 <a href="http://download.savannah.gnu.org/releases/freetype/">freetype 网站</a> 下载 freetype 2.4.10 最新版，假设压缩包名称为 freetype-2.4.10.tar.gz，下载到 ~/Downloads 目录下。将其解压到 ~ 目录下：
  </p>
  
  <pre><code>$ cd 
$ tar -xvzf ~/Downloads/freetype-2.4.10.tar.gz -C .
</code></pre>
  
  <p>
    解压出来的新目录名为 freetype-2.4.10。
  </p>
  
  <p>
    接着解压 freetype-infinality-2.4.10-20120616_01-x86_64.tar.bz2 压缩包到 ~/bin/ 目录下，当然，要解压到其他地方也无所谓，如果目录不存在，请先建立一个：
  </p>
  
  <pre><code>$ cd ~
$ mkdir bin
$ cd bin
$ tar -xvjf ~/Downloads/freetype-infinality-2.4.10-20120616_01-x86_64.tar.bz2 -C .
</code></pre>
  
  <p>
    现在文件都已经备齐，接下来就是开始打补丁：
  </p>
  
  <pre><code>$ cd ~/freetype-2.4.10
$ patch -p1 &lt; ~/bin/freetype-add-subpixel-hinting-infinality-20120616-01.patch 
$ patch -p1 &lt; ~/bin/freetype-enable-subpixel-hinting-infinality-20120615-01.patch 
$ patch -p1 &lt; ~/bin/freetype-entire-infinality-patchset-20120615-01.patch 
</code></pre>
  
  <p>
    这样，就给 freetype 源文件打好 finality 的补丁。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">其他设置内容</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    接下来，还要进行一些设置，仍是在 freetype-2.4.10 目录下操作：
  </p>
  
  <pre><code>$ ./configure
$ make
$ sudo mkdir /usr/lib/freetype-infinality/        # 如果跑 64 位系统就把 lib 改成 lib64
$ sudo find . -name libfreetype.so.6.9.0 -exec mv {} /usr/lib/freetype-infinality/ \;
$ cd /usr/lib/freetype-infinality
$ sudo ln -s libfreetype.so.6.9.0 libfreetype.so.6
</code></pre>
  
  <p>
    在 ~/bin/ 目录下有两个文件，根据建议需要拷贝到 /etc/profile.d/ 目录下：
  </p>
  
  <pre><code>$ cd ~/bin
$ sudo cp infinality-settings.sh freetype-infinality.sh /etc/profile.d/
</code></pre>
  
  <p>
    /etc/profile.d/infinality-settings.sh 这个文件里可以做很多设置，具体根据个人需要进行修改。
  </p>
  
  <p>
    接着，登出系统再登入，最好是重启系统。
  </p>
  
  <p>
    不过根据我的经历，将这两个文件拷入 /etc/profilde.d/ 目录后重启系统，差一点都登录不进来，输入密码后迅速地闪了一下屏幕，就又回到登录界面 。后来切换到 tty 下移除这两个文件，这才算进来了，目测没这两个文件 infinality 也起作用，另外，如果只拷贝 infinality-settings.sh 到 /etc/profile.d/ 目录下是没问题的。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">效果图</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <a href="http://www.zfanw.com/blog/wp-content/uploads/2012/10/Screenshot-from-2012-10-10-024510.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2012/10/Screenshot-from-2012-10-10-024510.png" alt="ubuntu 字体设置 infinality" title="ubuntu 字体设置效果" width="541"  class="alignnone size-full wp-image-6182" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/10/Screenshot-from-2012-10-10-024510.png 541w, https://www.zfanw.com/blog/wp-content/uploads/2012/10/Screenshot-from-2012-10-10-024510-300x87.png 300w" sizes="(max-width: 541px) 100vw, 541px" /></a>
  </p>
  
  <p>
    在其他不曾设置过的屏幕上，将上图与图片上下的文字显示效果对比一下就知道，这字体设置是否成功。最明显的，是字的锯齿不那么了然，每个字像是一笔一划写出来的，而不是点点点组成。这也就是 infinality 的目的之一：<q>freely provide the nicest font rendering of any operating system.</q>
  </p>
  
  <p>
    这样，我们就完成 Ubuntu 系统下的字体设置，即字体渲染的方法的调整，接下来可以针对不同程序进行字型(font)的选择，这就根据个人喜好，没什么规则可言。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">鸣谢</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://www.infinality.net/forum/viewtopic.php?f=2&t=77#p794">infinality.net 上的安装说明</a>
    </li>
    <li>
      <a href="http://forums.opensuse.org/ae-ae-chinese/aes-aeoe-e-e-ae-zae-aeoe/c-ae-zae-aeoe/470464-opensuse-c-aeoe-oec-zcs-ae-ae-az-e-c-i-oec-ae-mactype.html">openSUSE 论坛的相关内容</a>
    </li>
  </ol>
</div>