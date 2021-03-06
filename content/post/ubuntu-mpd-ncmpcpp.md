---
title: Ubuntu 下使用 MPD 与 Ncmpcpp
author: 陈 三
layout: post
date: 2012-09-11T02:28:21+00:00
url: /ubuntu-mpd-ncmpcpp.html
views:
  - 1610
dsq_thread_id:
  - 839133237
categories:
  - Ubuntu
tags:
  - MPD
  - music
  - ncmpcpp
  - Ubuntu

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_MPD_Ncmpcpp"><span class="toc_number toc_depth_1">1</span> 安装 MPD 与 Ncmpcpp</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_MPD"><span class="toc_number toc_depth_1">2</span> 配置 MPD</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_ncmpcpp"><span class="toc_number toc_depth_1">3</span> 使用 ncmpcpp</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">4</span> 鸣谢</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    先说个我作为新手使用 MPD 的一个经历，在启用 ncmpcpp 客户端播放《虫师》的音乐后，我退出 ncmpcpp，音乐仍在播放，我决定 log out 当前用户看看，它仍在播放，我心里大笑，想着说重启你总不会再播放了吧，关机那时显然是没了声音，等重启进入登录界面时，音乐继续。那个时候我觉得时光美好。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_MPD_Ncmpcpp">安装 MPD 与 Ncmpcpp</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_MPD_Ncmpcpp" href="#_MPD_Ncmpcpp"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    我的 Ubuntu 版本为 12.04,
  </p>
  
  <pre><code>$ sudo apt-get install mpd ncmpcpp
</code></pre>
  
  <h2 class="storycontent-h2">
    <span id="_MPD">配置 MPD</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_MPD" href="#_MPD"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    打开 /etc/mpd.conf 文件，
  </p>
  
  <pre><code>$ sudo gvim /etc/mpd.conf
</code></pre>
  
  <p>
    修改 music_directory 内容：
  </p>
  
  <pre><code>music_directory     "/home/sam/music"
</code></pre>
  
  <p>
    将其指向音乐文件夹即可。
  </p>
  
  <p>
    并且注释掉以下内容：
  </p>
  
  <pre><code>#audio_output {
#  type    "alsa"
#  name    "Sound Card"
#  device    "hw:0,0"  # optional
#  format    "44100:16:2"  # optional
#  mixer_device  "default" # optional
#  mixer_control "PCM"   # optional
#  mixer_index "0"   # optional
#}
</code></pre>
  
  <p>
    增加如下内容：
  </p>
  
  <pre><code>audio_output {
  type    "pulse"
  name    "MPD"
}
</code></pre>
  
  <p>
    如果声音会有问题，将下一行的注释#符号去掉，没问题则忽略：
  </p>
  
  <pre><code>#mixer_type "software"
</code></pre>
  
  <p>
    保存 mpd.conf 文件并重启 mpd:
  </p>
  
  <pre><code>$ sudo /etc/init.d/mpd restart
</code></pre>
  
  <p>
    又因为默认情况下 MPD 可能没有权限访问 PulseAudio，如下命令用于将它加入拥有访问权限的组中：
  </p>
  
  <pre><code>$ sudo usermod -aG pulse,pulse-access mpd
</code></pre>
  
  <p>
    这样，MPD 就以系统服务的形式在系统后台运行。
  </p>
  
  <p>
    另外，如果要使用 tag editor，需要拷贝一份 config 文件到 ~/.ncmpcpp/ 下：
  </p>
  
  <pre><code>$ cd ~/.ncmpcpp
$ cp /usr/share/doc/ncmpcpp/examples/config.gz .
$ gunzip config.gz
</code></pre>
  
  <p>
    打开 config 文件，将 mpd_music_dir 一行注释取消，并将值改为 /home/sam/music，即你的音乐文件夹。如果不做这一步，试图编辑音乐文件的 tag 时会出现错误：configuration variable mpd_music_dir is not set。
  </p>
  
  <p>
    然后重启 mpd，进入 ncmpcpp 后按数字 7 即可以进入 tag editor。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_ncmpcpp">使用 ncmpcpp</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_ncmpcpp" href="#_ncmpcpp"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Ncmpcpp 全称为 NCurses Music Player Client (Plus Plus)，界面与 Ncmpc 相近，但提供更多新特性，这也是加两个 Plus 的意思。另外，Ncmpcpp 只是 MPD 许多客户端中的一个，更多请见 <a href="http://mpd.wikia.com/wiki/Clients">http://mpd.wikia.com/wiki/Clients</a>。
  </p>
  
  <p>
    我们可以通过命令行输入 <code>ncmpcpp</code> 启用它。
  </p>
  
  <h3>
    更新数据库
  </h3>
  
  <p>
    上面我们虽然为 MPD 配置了音乐文件夹位置，但数据库内并没有更新文件内容，这需要通过客户端来完成，在进入 ncmpcpp 后，我们可以按 u 键来更新数据库：
  </p>
  
  <p>
    <kbd>u</kbd> &#8211; 更新音乐数据库
  </p>
  
  <p>
    网络上还能看到 <code>mpd --create-db</code> 这个命令，但这个命令在 MPD 最近版本中显然已经被取消。
  </p>
  
  <h3>
    Ncmpcpp 常用快捷键
  </h3>
  
  <ul>
    <li>
      <kbd>j</kbd> &#8211; 向下移动
    </li>
    <li>
      <kbd>k</kbd> &#8211; 向上移动
    </li>
    <li>
      <kbd>1</kbd> &#8211; 这是数字 1，打开帮助，可以查看各种快捷键的用法
    </li>
    <li>
      <kbd>3</kbd> &#8211; Browser，可以查看音乐文件夹下的内容，在 Browser 里，可以按空格将文件加入播放列表，也可以按 Enter 键将文件加入播放列表并开始播放；如果要添加全部文件到播放列表，先按 a 键，然后 / 键，接着回车。
    </li>
    <li>
      <kbd>2</kbd> &#8211; Playlist，播放列表，在播放列表中按 c 可以清空列表，按 d 可以删除条目，按 S 可以保存列表，小写 s 则是停止播放，P 是暂停播放，再按一次 P 继续播放
    </li>
    <li>
      <kbd>l</kbd> &#8211; 这是字母，小写的 L，表示 lyric，取得歌词
    </li>
    <li>
      <kbd>q</kbd> &#8211; 退出 ncmpcpp
    </li>
  </ul>
  
  <p>
    其实 Vim 里的许多快捷键都可以在 Ncmpcpp 中使用。
  </p>
  
  <p>
    另外，Ncmpcpp 有几个让人郁结的地方，比如按 S 保存播放列表，输入几个字母后你改变主意不想保存了，想取消这个动作，抱歉，没有快捷键，只能按 <kbd>Ctrl-c</kbd> 退出 ncmpcpp。
  </p>
  
  <p>
    更多快捷键按 1 键进入帮助查看，更多配置可以参见以下链接。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">鸣谢</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="https://help.ubuntu.com/community/MPD">https://help.ubuntu.com/community/MPD</a>
    </li>
    <li>
      <a href="https://wiki.archlinux.org/index.php/Ncmpcpp">https://wiki.archlinux.org/index.php/Ncmpcpp</a>
    </li>
    <li>
      <a href="http://ncmpcpp.rybczak.net/">http://ncmpcpp.rybczak.net/</a>
    </li>
    <li>
      <a href="https://bbs.archlinux.org/viewtopic.php?pid=1033566">https://bbs.archlinux.org/viewtopic.php?pid=1033566</a>
    </li>
    <li>
      <a href="http://manpages.ubuntu.com/manpages/lucid/man1/ncmpcpp.1.html">http://manpages.ubuntu.com/manpages/lucid/man1/ncmpcpp.1.html</a>
    </li>
  </ol>
</div>