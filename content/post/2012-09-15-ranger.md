---
title: Ranger 文件管理器
author: 陈 三
layout: post
date: 2012-09-15T11:32:42+00:00
url: /ranger.html
views:
  - 1550
dsq_thread_id:
  - 845156384
categories:
  - openSUSE
  - Ubuntu
tags:
  - file manager

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#_Ranger"><span class="toc_number toc_depth_1">1</span> 安装 Ranger</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_ranger"><span class="toc_number toc_depth_1">2</span> 使用 ranger</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <a href="http://ranger.nongnu.org/index.html">Ranger</a> 是一个终端窗口内的<strong>文件管理器</strong>，使用 VI 键绑定。
  </p>
  
  <p>
    如果你习惯使用键盘，并且熟悉基本的 Vim 键组合，则 Ranger 是个非常不错的选择。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_Ranger">安装 Ranger</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_Ranger" href="#_Ranger"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Ranger 的安装方法有多种。
  </p>
  
  <h3>
    系统安装包
  </h3>
  
  <p>
    某些 Linux 系统有打包好的 ranger 安装包，可直接安装，比如 Ubuntu：
  </p>
  
  <pre><code>$ sudo apt-get install ranger
</code></pre>
  
  <p>
    openSUSE 下：
  </p>
  
  <pre><code>sudo zypper install ranger
</code></pre>
  
  <p>
    但软件源提供的 Ranger 有可能不是最新，那么可以考虑下面一种方法。
  </p>
  
  <h3>
    压缩包
  </h3>
  
  <p>
    从 <a href="http://ranger.nongnu.org/download.html">ranger</a> 网站下载压缩包，然后解压。
  </p>
  
  <p>
    解压后的文件可以直接运行：
  </p>
  
  <pre><code>$ tar xvf ranger-stable.tar.gz 
$ cd ranger-stable 
$ ./ranger.py
</code></pre>
  
  <p>
    也可以安装后运行：
  </p>
  
  <pre><code>$ tar xvf ranger-stable.tar.gz 
$ cd ranger-stable 
$ sudo make install
</code></pre>
  
  <p>
    这个办法同样可用于更新 Ranger，查看 Ranger 的版本命令为终端窗口输入：<code>ranger --version</code>。
  </p>
  
  <h3>
    git 源
  </h3>
  
  <p>
    ranger 源代码通过 git 管理，所以，也可以从源代码库克隆一份，好处是最新的程序更新都能使用到，但稳定性不一定最佳：
  </p>
  
  <pre><code>$ git clone git://git.savannah.nongnu.org/ranger.git 
$ cd ranger
</code></pre>
  
  <p>
    之后按上一步的两个办法操作。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_ranger">使用 ranger</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_ranger" href="#_ranger"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    打开终端窗口，输入:<code>ranger</code> 然后按 <kbd>Enter</kbd> 进入 Ranger 界面。
  </p>
  
  <p>
    Ranger 的界面分为三列，
  </p>
  
  <ol>
    <li>
      中间列 &#8211; 当前目录
    </li>
    <li>
      左列 &#8211; 上一级目录
    </li>
    <li>
      右列 &#8211; 可预览文件的内容，默认仅支持文本文件的预览，但是可以通过设置预览 html，图片，存档文件，pdf 甚至音视频信息。
    </li>
  </ol>
  
  <p>
    <a href="http://www.zfanw.com/blog/wp-content/uploads/2012/09/ranger.png"><img src="http://www.zfanw.com/blog/wp-content/uploads/2012/09/ranger.png" alt="ranger screenshot" title="ranger" width="610" "alignnone size-full wp-image-5552" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/09/ranger.png 810w, https://www.zfanw.com/blog/wp-content/uploads/2012/09/ranger-300x222.png 300w" sizes="(max-width: 810px) 100vw, 810px" /></a>
  </p>
  
  <p>
    因为 ranger 使用 VI 键绑定，所以对 Vim 熟悉的用户可以轻松上手，比如 j 表示光标下移，k 表示光标上移，h 表示返回上一级目录，l 表示进入光标所在的目录或打开光标所在的文件。
  </p>
  
  <p>
    ranger 的键绑定很多，某些不常用的键，一时记不起是正常的，这时可以在 ranger 里按 <kbd>1?</kbd> 打开键绑定的清单，<kbd>2?</kbd> 则是命令清单，<kbd>3?</kbd> 是设置项清单，<kbd>?</kbd> 则是整个使用手册。按 <kbd>q</kbd> 即可退出帮助界面。
  </p>
  
  <p>
    在 ranger 里，可以像 Vim 一样按 <kbd>:</kbd> 进入命令模式，然后调用 ranger 的命令。比如光标位置下的图片，我不想用系统默认的程序打开，则可以按 <kbd>:</kbd> 进入命令模式，然后输入 open_with（可以按 <kbd>r</kbd> 快速打开这个命令），再之后是要打开图片的程序，比如 feh，则整个命令的形式是：
  </p>
  
  <pre><code>:open_with feh
</code></pre>
  
  <p>
    当然，这种常用的操作 ranger 默认配备了一个 <kbd>r</kbd> 快捷键。
  </p>
  
  <p>
    又或者想删除文件，可以按空格键先做标记，或者将光标移动至要删除的文件上，然后进入命令模式，输入 delete 命令，回车，按 y 确定删除。要以 root 的身份启动程序也非常容易，在 open_with 后跟一个 &#8220;r&#8221; 标记(flag)，然后就会要求输入 root 用户密码。
  </p>
  
  <p>
    复制文件按 yy，剪切按 dd，粘贴按 pp，E 编辑当前文件，重命名可以通过命令行 <code>:rename 新名字</code>，ranger 还支持 midnight commander 的一些键用法，比如 f3 是显示文件，f4 是编辑文件，f5 是复制文件，f6 剪切文件。<a href="http://www.gnu.org/software/mc/">midnight commander</a> 也是一个基于文本操作的文件管理器，双面板。与 Windows 系统下的 total commander 有相似之处。
  </p>
  
  <p>
    显然，键绑定是可以修改的，首先，需要一个 rc.conf 配置文件（ranger 1.5 版本后）：
  </p>
  
  <pre><code>$ ranger --copy-config=rc
</code></pre>
  
  <p>
    这样会在 ～/.config/ranger/ 下生成一个 rc.conf 文件，里面可以看到许多 map，类似 Vim 的键映射，可以根据需要进行修改。
  </p>
  
  <p>
    文件的打开程序列表也可以通过配置文件修改：
  </p>
  
  <pre><code>$ ranger --copy-config=rifle
</code></pre>
  
  <p>
    以上命令在复制了一份 rifle.conf 到 ~/.config/ranger/ 目录，打开即可以编辑。
  </p>
  
  <p>
    作为文件管理器，Ranger 可以快捷访问某些目录，比如 gh 访问主目录，gm 访问 /media 目录，实际上，当你按下 g 时，ranger 会在底部弹出一个辅助栏，提示可以通过 g（go to 的意思）访问到的目录。另外，目录也可以以书签形式组织，譬如当前目录可以按 <kbd>ma</kbd> 加入书签中，然后 <kbd>`a</kbd> 或者 <kbd>'a</kbd> 访问到该目录，这在 Vim 下是 quickmark 的操作，也很像 totalcommander 的 ctrl-d + 字符的操作。另外还可以在进入命令模式后按 tab 键自动补齐书签中的目录，不过前一个方法显然要更快捷。
  </p>
  
  <p>
    以上略作介绍，更多内容请见 <a href="http://ranger.nongnu.org/ranger.1.html">ranger 使用手册</a>，即 ranger 中按 <kbd>?</kbd> 的结果。
  </p>
</div>