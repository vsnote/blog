---
title: openSUSE 上的 infinality
author: 陈 三
layout: post
date: 2013-11-22T13:57:23+00:00
url: /opensuse-infinality.html
dsq_thread_id:
  - 2009316390
dsq_needs_sync:
  - 1
views:
  - 1252
categories:
  - openSUSE
tags:
  - infinality
  - openSUSE

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_FreeType"><span class="toc_number toc_depth_1">1</span> 下载 FreeType</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_freetype-infinality"><span class="toc_number toc_depth_1">2</span> 下载 freetype-infinality</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_freetype"><span class="toc_number toc_depth_1">3</span> 给 freetype 文件打补丁</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_fontconfig-infinality"><span class="toc_number toc_depth_1">4</span> 下载 fontconfig-infinality</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">5</span> 问题汇</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <strong>简快版</strong>，仅需要三步：
  </p>
  
  <ol>
    <li>
      安装 <a href="https://build.opensuse.org/package/show/home:opensuse_zh/freetype2">freetype2</a>
    </li>
    <li>
      安装 <a href="https://software.opensuse.org/package/fontconfig-infinality?search_term=fontconfig-infinality">fontconfig infinality</a>
    </li>
    <li>
      <code>cd /etc/fonts/infinality</code>，执行 <code>./infctl.sh setstyle</code>
    </li>
  </ol>
  
  <p>
    以前用 Ubuntu 时，在系统上折腾过 <a href="http://www.zfanw.com/blog/ubuntu-font-render-with-infinality.html">infinality</a>，字体渲染的效果要比系统默认的好很多。最近<a href="http://www.zfanw.com/blog/opensuse-upgrade-12-3-to-13-1.html">升级 openSUSE 到13.1</a>，感觉字体太细，看得不很舒服，就想起 infinality。
  </p>
  
  <p>
    opensuse_zh 中文源上有提供 <a href="https://build.opensuse.org/package/show/home:opensuse_zh/freetype2">freetype2</a>，不过我看它13.1版本下的 build 状态是 failed，所以没有尝试。所以最后仍是根据官网上的<a href="http://www.infinality.net/forum/viewtopic.php?f=2&t=77">说明</a>配置的。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_FreeType">下载 FreeType</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_FreeType" href="#_FreeType"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    从 FreeType 官网下载 <a href="http://download.savannah.gnu.org/releases/freetype/">freetype 2.4.12</a>。FreeType 现在已经出到2.5版本，但出于安全考虑，还是照作者说的做，下载2.4.12版本。
  </p>
  
  <p>
    我在 /home/sam/ 目录下建了个 fonts 目录，将 freetype 压缩包解压到 fonts 目录里。
  </p>
  
  <p>
    现在的 fonts 目录结构如下：
  </p>
  
  <blockquote>
    <p>
      &#45; fonts
    </p>
    
    <p>
      ++ freetype-2.4.12
    </p>
  </blockquote>
  
  <h2 class="storycontent-h2">
    <span id="_freetype-infinality">下载 freetype-infinality</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_freetype-infinality" href="#_freetype-infinality"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    从 infinality <a href="http://www.infinality.net/blog/infinality-freetype-patches/">页面</a> 下载 freetype-infinality-2.4.12-20130514_01-x86_64.tar.bz2 文件，同样解压到 fonts 目录下，fonts 目录结构现在如下：
  </p>
  
  <blockquote>
    <p>
      &#45; fonts
    </p>
    
    <p>
      &#43;+ freetype-2.4.12
    </p>
    
    <p>
      &#43;+ freetype-infinality-2.4.12-20130514_01-x86_64
    </p>
  </blockquote>
  
  <h2 class="storycontent-h2">
    <span id="_freetype">给 freetype 文件打补丁</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_freetype" href="#_freetype"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <pre><code>$ cd /home/sam/fonts/freetype-2.4.12

$ patch -p1 &lt; ../freetype-infinality-2.4.12-20130514_01-x86_64/freetype-entire-infinality-patchset-20130514-01.patch
</code></pre>
  
  <p>
    接下来是 make(以下命令全部来自 infinality 说明)：
  </p>
  
  <pre><code>$ ./configure

$ make

$ sudo mkdir /usr/lib/freetype-infinality/ #64位系统上把 lib 改成 lib64

$ sudo find . -name libfreetype.so.6.10.1 -exec mv {} /usr/lib/freetype-infinality/  \;       

$ cd /usr/lib/freetype-infinality

$ sudo ln -s libfreetype.so.6.10.1 libfreetype.so.10
</code></pre>
  
  <p>
    我的系统下，在 <code>./configure</code> 一步就报错：
  </p>
  
  <blockquote>
    <p>
      configure: error: no acceptable C compiler found in $PATH
    </p>
    
    <p>
      See &#8216;config.log&#8217; for more details
    </p>
  </blockquote>
  
  <p>
    不过很可惜，我在该目录下并没找到 config.log 文件。照错误的字面意思，大概是说通过 $PATH 没能找到可用的 C compiler。
  </p>
  
  <p>
    看了些资料，说要安装下 <a href="http://software.opensuse.org/package/gcc">GCC</a>。
  </p>
  
  <p>
    安装完 GCC 后再跑一趟 <code>./configure</code>，这回正常，之后 <code>make</code>。
  </p>
  
  <p>
    <code>find</code> 一句的意思是，在当前目录，查找名称为 libfreetype.so.6.10.1 的文件，然后将它们移动到 /usr/lib/freetype-infinality/ 目录。<code>{}</code> 类似占位符，<a href="http://en.wikipedia.org/wiki/Find#Search_files_by_name_and_size">find</a> 命令会将找到的文件代入其中，<code>;</code> 指示命令结束，之所以加转义符号 \ 是防止 Bash 把它理解成命令分隔符。
  </p>
  
  <p>
    在完成以上操作后，我们可以切换到 /usr/lib/freetype-infinality 目录查看，现在有一个 libfreetype.so.6.10.1 文件 &#8211; 是的，以上所有的操作是仅为了这个文件的。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_fontconfig-infinality">下载 fontconfig-infinality</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_fontconfig-infinality" href="#_fontconfig-infinality"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    仍是从 <a href="http://www.infinality.net/blog/infinality-freetype-patches/">infinality 网站</a> 下载 fontconfig-infinality-1-20130104_1.tar.bz2，这回是解压到 /etc/fonts/ 目录下：
  </p>
  
  <pre><code>$ sudo tar jfxv fontconfig-infinality-1-20130104_1.tar.bz2 -C /etc/fonts/
</code></pre>
  
  <p>
    /etc/fonts/ 目录下共多出三个文件夹：
  </p>
  
  <ol>
    <li>
      conf.avail
    </li>
    <li>
      conf.d
    </li>
    <li>
      infinality
    </li>
  </ol>
  
  <p>
    根据 /etc/fonts/infinality/README 文件说明，需要确保 /etc/fonts/conf.d 目录下的 52-infinality.conf 有软链接(symlink)指向 /etc/fonts/infinality/ 下的 infinality.conf：
  </p>
  
  <pre><code>$ cd /etc/fonts/conf.d/
$ sudo ln -sf ../infinality/infinality.conf 52-infinality.conf
</code></pre>
  
  <p>
    infinality 的配置说明提到 /home/用户名 目录下的 .fonts.conf 文件，不过我的系统上又没有。于是我就创建一个：
  </p>
  
  <pre><code>$ cd /home/sam/
$ su #以 root 身份
$ vim .fonts.conf
</code></pre>
  
  <p>
    在 .fonts.conf 文件中添加如下内容：
  </p>
  
  <pre><code>&lt;?xml version='1.0'?&gt;
&lt;!DOCTYPE fontconfig SYSTEM 'fonts.dtd'&gt;
&lt;fontconfig&gt;
&lt;/fontconfig&gt;
</code></pre>
  
  <p>
    保存后执行 <code>chattr +i .fonts.conf</code> 命令，使得 .fonts.conf 不受更改或破坏。
  </p>
  
  <p>
    然后添加以下内容到 /etc/X11/Xresources 及 ~/.Xresources(不存在的话创建一个) 文件里：
  </p>
  
  <pre><code>Xft.autohint: 0
Xft.lcdfilter:  lcddefault
Xft.hintstyle:  hintfull
Xft.hinting: 1
Xft.antialias: 1
Xft.dpi: 96
Xft.rgba: rgb
</code></pre>
  
  <p>
    <small>注：infinality 上提到 /etc/profile.d/infinality-settings.sh 文件可以自动配置 /etc/X11/Xresources 及 ~/.Xresources 文件，但我的情况，/etc/ 目录下是没有 profile.d 文件夹的。</small>
  </p>
  
  <p>
    接着重启系统。
  </p>
  
  <p>
    如果需要修改字体渲染的配置文件，可以进入 /etc/fonts/infinality 目录：
  </p>
  
  <pre><code>$ ./infctl.sh setstyle
</code></pre>
  
  <p>
    运行后会提示几个可用的字体渲染配置方法，选择数字然后按确定即可。
  </p>
  
  <p>
    至此，openSUSE 上的配置 infinality 算是完成。
  </p>
  
  <p>
    至于效果，上图看看：
  </p>
  
  <p>
    <a href="http://www.zfanw.com/blog/wp-content/uploads/2013/11/opensuse-fonts-infinality.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2013/11/opensuse-fonts-infinality.png" alt="opensuse 字体美化 渲染 infinality" width="448" height="292" class="alignnone size-full wp-image-11080" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/11/opensuse-fonts-infinality.png 448w, https://www.zfanw.com/blog/wp-content/uploads/2013/11/opensuse-fonts-infinality-300x195.png 300w" sizes="(max-width: 448px) 100vw, 448px" /></a>
  </p>
  
  <p>
    <em>另外，在我的系统里，Firefox在某些页面里，中文渲染的情况非常糟糕，有发虚的现象。后来安装了<a href="http://wenq.org/wqy2/index.cgi?MicroHei">文泉驿微米黑</a>，才算正常。</em>
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">问题汇</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      在我从命令窗口开启 Kaffeine 时，错误提示：
    </li>
  </ol>
  
  <blockquote>
    <p>
      Fontconfig warning: &#8220;/etc/fonts/conf.d/56-user.conf&#8221;, line 14: reading configurations from ~/.fonts.conf is deprecated. please move it to /home/sam/config/fontconfig/fonts.conf manually
    </p>
  </blockquote>
  
  <p>
    查看 /etc/fonts/conf.d/56-user.conf 文件，是一个指向 /usr/share/fontconf/conf.avail/50-user.conf 的软链接，里面的内容表示以上错误提示在将来会被移除。
  </p>
</div>