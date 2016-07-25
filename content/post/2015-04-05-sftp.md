---
title: SFTP 用法
author: 陈 三
layout: post
date: 2015-04-05T14:37:58+00:00
excerpt: 使用 sftp 上传、下载文件
url: /sftp.html
views:
  - 1061
categories:
  - 未分类
tags:
  - sftp

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 连接</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 下载文件</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 上传文件</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-4"><span class="toc_number toc_depth_1">4</span> 更多命令</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    FTP 诸君大概都用过，SFTP 用过的估计比较少。简单说，它就是 ftp 前加个 secure，通过 ssh 通道在本地及远程服务器间进行文件传输，更为安全。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">连接</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    ssh 的连接通常是这样：
  </p>
  
  <pre><code>ssh sam@zfanw.com
</code></pre>
  
  <p>
    然后输入密码。
  </p>
  
  <p>
    sftp 基本就是把 <code>ssh</code> 换作 <code>sftp</code>：
  </p>
  
  <pre><code>sftp sam@zfanw.com
</code></pre>
  
  <p>
    如果配置了 ssh 的 config 文件，使用私钥/公钥的形式连接远程服务器，则更简单了：
  </p>
  
  <pre><code>sftp linode
</code></pre>
  
  <p>
    连接完成后，终端显示：
  </p>
  
  <blockquote>
    <p>
      sftp >
    </p>
  </blockquote>
  
  <h2 class="storycontent-h2">
    <span id="i-2">下载文件</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    ftp 主要的作用就是文件传输，sftp 提供的下载文件命令是 <code>get</code>：
  </p>
  
  <pre><code>get -r picture
</code></pre>
  
  <p>
    这个命令把 picture 目录下载到本地。
  </p>
  
  <pre><code>get sam.png
</code></pre>
  
  <p>
    这个命令把 sam.png 图片下载到本地。
  </p>
  
  <p>
    本地的哪里？？
  </p>
  
  <p>
    我们可以借助 <code>lpwd</code> 命令查看本地的当前工作目录 &#8211; 就是在 <code>pwd</code> 命令前加个 <code>l</code> 表示 local。可以想知，我们同样可以使用 <code>lcd</code> 来切换本地的工作目录。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">上传文件</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    sftp 提供的上传命令是 <code>put</code>。
  </p>
  
  <pre><code>put sam.png
</code></pre>
  
  <p>
    这个命令把本地当前工作目录下的 sam.png 上传到远程服务器的工作目录下。
  </p>
  
  <pre><code>put -r picture
</code></pre>
  
  <p>
    上传整个目录文件。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-4">更多命令</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-4" href="#i-4"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    在 <code>sftp &gt;</code> 终端输入 <code>help</code> 即可以查看 sftp 提供的所有命令：
  </p>
  
  <pre><code>sftp&gt; help 
Available commands:
bye                                Quit sftp
cd path                            Change remote directory to 'path'
chgrp grp path                     Change group of file 'path' to 'grp'
chmod mode path                    Change permissions of file 'path' to 'mode'
chown own path                     Change owner of file 'path' to 'own'
df [-hi] [path]                    Display statistics for current directory or
                                   filesystem containing 'path'
exit                               Quit sftp
get [-Ppr] remote [local]          Download file
help                               Display this help text
lcd path                           Change local directory to 'path'
lls [ls-options [path]]            Display local directory listing
lmkdir path                        Create local directory
ln [-s] oldpath newpath            Link remote file (-s for symlink)
lpwd                               Print local working directory
ls [-1afhlnrSt] [path]             Display remote directory listing
lumask umask                       Set local umask to 'umask'
mkdir path                         Create remote directory
progress                           Toggle display of progress meter
put [-Ppr] local [remote]          Upload file
pwd                                Display remote working directory
quit                               Quit sftp
rename oldpath newpath             Rename remote file
rm path                            Delete remote file
rmdir path                         Remove remote directory
symlink oldpath newpath            Symlink remote file
version                            Show SFTP version
!command                           Execute 'command' in local shell
!                                  Escape to local shell
?                                  Synonym for help
</code></pre>
</div>