---
title: V6 SuperCharger 操作流程
author: 陈 三
layout: post
date: 2012-10-19T13:13:36+00:00
url: /v6-supercharger.html
views:
  - 1769
dsq_thread_id:
  - 891663082
dsq_needs_sync:
  - 1
categories:
  - 未分类
tags:
  - Android

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_8211_SManager"><span class="toc_number toc_depth_1">1</span> 安装本管理工具 &#8211; SManager</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_SuperCharger_Starter_Kit"><span class="toc_number toc_depth_1">2</span> 安装 SuperCharger Starter Kit</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_servicesjar"><span class="toc_number toc_depth_1">3</span> 给 services.jar 打补丁</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_SuperCharger"><span class="toc_number toc_depth_1">4</span> 运行 SuperCharger 脚本</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    我其实并不经常折腾手机。
  </p>
  
  <p>
    就说最近，只偶尔<a href="http://www.zfanw.com/blog/defy-flash-cm10.html">刷刷 CM10 Nightly 版本</a>。所以对 SuperCharger 的存在一直都不知道，直到昨天看到 <a href="http://wingofikaros.tumblr.com/post/33709025688/android-android-v6-supercharge">[不折腾会死]系列之 Android最强优化脚本V6 Supercharge简单流程</a> ，才知道还有这玩意儿。
  </p>
  
  <p>
    看下它的介绍：
  </p>
  
  <blockquote>
    <p>
      SuperCharger = Speed + Multitasking!
    </p>
    
    <p>
      No more lag! No more launcher redraws! Smooth & Snappy!
    </p>
    
    <p>
      It&#8217;s the ONLY Complete Memory Management Fix!
    </p>
    
    <p>
      There is NOTHING ELSE LIKE IT!
    </p>
    
    <p>
      It Runs Like A&#8230;
    </p>
  </blockquote>
  
  <p>
    这段文字后是一张配图，一幅地狱场景，一个人骑在摩托车上，因为车速太快，整个身体向后跌去，表示你一定要牢牢抓住。
  </p>
  
  <p>
    这样我们就大概知道 SuperCharger 是干什么的。
  </p>
  
  <p>
    不过它的教程真的是看着头疼，就好像一个人开了 Word 软件，然后到处加粗字体，突出颜色，链接来来去去不知多少趟。
  </p>
  
  <p>
    所以，这是一篇再再（再的应该是不折腾会死系列）整理的内容，在我的 Motorola Defy 即 ME525 手机上操作。请先阅读不折腾会死的那一篇，对整个操作的必要条件等作个了解。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_8211_SManager">安装本管理工具 &#8211; SManager</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_8211_SManager" href="#_8211_SManager"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    从 <a href="https://play.google.com/store/apps/details?id=os.tools.scriptmanager">Google Play 上下载 SManager</a> 并安装，这个应用用于运行脚本，如果更喜欢命令行工具的话，很多 ROM 里都提供有终端模拟器，可以通过它来运行脚本。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_SuperCharger_Starter_Kit">安装 SuperCharger Starter Kit</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_SuperCharger_Starter_Kit" href="#_SuperCharger_Starter_Kit"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    这个工具包是为后面作准备，它会给系统安装 fixed su binary，zipalign binary，sqlite3 binary 和 busybox v1.19.4，如果系统上已经有了（比如 CM10 就没必要），就直接跳过。
  </p>
  
  <p>
    安装方法是从 <a href="http://forum.xda-developers.com/showpost.php?p=18703418&postcount=5021">XDA 论坛上下载</a>最新的 SuperCharger_Starter_Kit_RCXX.zip 压缩包，解压并上传到 SD 卡根目录下。
  </p>
  
  <p>
    然后通过 SManager 工具运行解压出的 SuperCharger_Starter_Kit 目录下的 StartMeUp.sh 脚本，它会自动安装以上列出的一切。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_servicesjar">给 services.jar 打补丁</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_servicesjar" href="#_servicesjar"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    作用不多提，总之是种种好 &#8211; 按作者的说法。
  </p>
  
  <p>
    过程还是根据 <a href="http://forum.xda-developers.com/showpost.php?p=16635544&postcount=2">XDA 上面的教程</a>。
  </p>
  
  <p>
    首先打开 ”<a href="http://forum.xda-developers.com/showthread.php?t=1914159">Ultimate Jar Power Tools</a>“ 页面，在该页面查找 ”Attached Files“，当下时间该附件名称为 ”ALL_ROMS_Ultimate_Jar_Power_Tools-Smali_Patcher_Test_RC1.sh.txt“，另存到电脑上，把 .txt 扩展名去掉，还原它的脚本扩展名 .sh。
  </p>
  
  <p>
    到 <a href="http://hotfile.com/dl/121586687/ae510fb/jar_file_decompile_and_compiler_with_tutor.zip.html">hotfile 链接下载</a> jar_file_decompile_and_compiler_with_tutor.zip 文件，解压到 C:\super 文件夹下（操作系统为 Windows xp）。
  </p>
  
  <p>
    从 <a href="http://code.google.com/p/smali/downloads/list">Google code</a> 网站上下载两个最新版的 jar 文件，分别重命名为 smali.jar 和 baksmali.jar，放入 C:\super 文件夹，覆盖掉原有的两个同名文件。
  </p>
  
  <p>
    进入手机 /system/framework/ 目录，复制一份 services.jar 文件放入 C:\super 文件夹。（<strong>注意备份一个 services.jar 文件</strong>）
  </p>
  
  <p>
    打开 Windows 系统的 cmd 窗口：
  </p>
  
  <pre><code>$ cd c:\super
$ java -jar baksmali.jar -x services.jar -o classout
</code></pre>
  
  <p>
    将 services.jar 文件反编译到 classout 文件夹，可以看到 C:\super 文件夹下多出来 classout 文件夹。
  </p>
  
  <p>
    进入文件夹 C:\super\classout\com\android\server\am，找到 ActivityManagerService.smali 与 ProcessList.smali 文件(ICS 与 Jelly Bean 需要这两个文件，其他版本有所不同)，将这两个文件并上面下载的 ALL_ROMS_Ultimate_Jar_Power_Tools-Smali_Patcher_Test_RC1.sh 文件一同存入 SD 卡某一目录，假设为 ultimate 目录。
  </p>
  
  <p>
    打开手机上的 SManager，定位到 ultimate 目录，运行 ALL_ROMS_Ultimate_Jar_Power_Tools-Smali_Patcher_Test_RC1.sh 脚本。
  </p>
  
  <p>
    基本上就是一路 yes 下去，完成后 ultimate 目录后的两个 smali 文件拷回 C:\super\classout\com\android\server\am，覆盖。
  </p>
  
  <p>
    回到 cmd 窗口，仍是在 C:\super 目录下：
  </p>
  
  <pre><code>$ java -Xmx512M -jar smali.jar classout -o classes.dex
</code></pre>
  
  <p>
    在 C:\super 目录下生成一个 classes.dex 文件。
  </p>
  
  <p>
    使用压缩软件打开 C:\super 目录下的 services.jar 文件，然后将 C:\super 目录下新生成的 classes.dex 拖入，覆盖旧的 classes.dex，这样就生成一个新的 services.jar 文件。
  </p>
  
  <p>
    (<strong>以上办法纯手工操作，非常麻烦，所以 XDA 上还提供了一个在 <a href="http://forum.xda-developers.com/showthread.php?t=1869663">Windows 系统下的简便方法</a></strong>) &#8211; 推荐使用这个办法，非常容易操作。
  </p>
  
  <p>
    将新的 services.jar 文件上传到手机 SD 卡上，然后设置 /system 目录可读写，将其拷入 /system/framework 覆盖掉原来的 services.jar &#8211; SManager 就可以完成这样的操作。
  </p>
  
  <p>
    打开终端模拟器：
  </p>
  
  <pre><code>$ cd /system/framework
$ su
$ chown 0.0 services.jar //将文件所有者/组更改为 root，注意是数字 0，不是字母 o，0.0 表示 root.root
$ chmod 644 services.jar //设置文件读写权限
</code></pre>
  
  <p>
    （<del>分享一下我<a href="http://d.pr/f/sIoM">打过补丁的 services.jar</a>，请谨慎使用，出问题一概不负责</del>）
  </p>
  
  <p>
    然后重启，进入恢复模式，清空 Dalvik Cache，
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_SuperCharger">运行 SuperCharger 脚本</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_SuperCharger" href="#_SuperCharger"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    <a href="http://forum.xda-developers.com/showthread.php?p=16635544#post16635544">具体步骤 XDA 上</a>都有，打开该页面，搜索 “Installing/Using” 就可以看到。其实过程非常简单。
  </p>
  
  <p>
    ICS/Jelly Bean 在运行 SuperCharger 前必须先给 services.jar 打过补丁。
  </p>
  
  <p>
    <a href="http://forum.xda-developers.com/showpost.php?p=18703418&postcount=5021">下载最新版 SuperCharger</a>，比如当下时间 ”V6_SuperCharger_for_Android-Update9_RC10.sh.pdf “，另存到电脑，去掉 .pdf 扩展名。上传到手机 SD 卡根目录。
  </p>
  
  <p>
    打开 SManger，定位到 SD 卡根目录，运行 V6_SuperCharger_for_Android-Update9_RC10.sh 脚本，根据提示操作，直到最后。这个过程所花的时间不短，所以请在电量很足的情况下操作。
  </p>
  
  <p>
    运行结束后，系统要求重启，进入系统后显示正在优化应用&#8230;&#8230;
  </p>
  
  <p>
    以上。
  </p>
</div>