---
title: Vim 文件格式
author: 陈 三
layout: post
date: 2012-03-07T04:05:11+00:00
url: /vim-file-format-problem.html
dsq_thread_id:
  - 601529812
views:
  - 2249
categories:
  - 未分类
tags:
  - vim

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 新建文件</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 特殊字符</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_unix_dos"><span class="toc_number toc_depth_1">3</span> 从 unix 转 dos</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#_M"><span class="toc_number toc_depth_1">4</span> 清空 ^M</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">5</span> 参考资料</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    因为经常要在 Windows XP 上用 Vim 编辑从 Apache 服务器上下载的文件，于是行末就会经常出现 &#8220;^M&#8221; 这样的非正常行结束符。
  </p>
  
  <p>
    首先，Vim 能够识别三个操作系统下的文件格式，包括 Unix，Dos 与 Mac。在创建文件或写入时，这三种文件格式分别决定了行末要添加什么特殊字符，而在读入文件时，又分别决定了要从行末移去什么特殊字符。
  </p>
  
  <p>
    这样，就可以列出下面一个表格：
  </p>
  
  <table class="table table-condensed">
    <caption> Vim File Format </caption> <tr>
      <th>
      </th>
      
      <th>
        Unix
      </th>
      
      <th>
        Dos
      </th>
      
      <th>
        Mac OS X
      </th>
    </tr>
    
    <tr>
      <td>
        写入
      </td>
      
      <td>
        +LF
      </td>
      
      <td>
        +CRLF
      </td>
      
      <td>
        +LF
      </td>
    </tr>
    
    <tr>
      <td>
        读取
      </td>
      
      <td>
        -LF
      </td>
      
      <td>
        -CRLF
      </td>
      
      <td>
        -LF
      </td>
    </tr>
  </table>
  
  <p>
    注:
  </p>
  
  <blockquote>
    <p>
      CR is carriage return (return cursor to left margin), which is Ctrl-M or ^M or hex 0D.
    </p>
    
    <p>
      LF is linefeed (move cursor down), which is Ctrl-J or ^J or hex 0A. Sometimes, LF is written as NL (newline).
    </p>
  </blockquote>
  
  <h2 class="storycontent-h2">
    <span id="i">新建文件</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    从 Vim 新建的文件，文件的 file format 值是由 Vim <code>fileformats</code> 这个选项值决定。fileformats 是全局选项，决定了操作系统新建或打开文件时应用到文件上的 file format 值。
  </p>
  
  <p>
    比如我现在所用系统为 Windows XP，在 Vim 命令模式下使用 <kbd>:set ffs?</kbd> 可以查看到，fileformats 值是 &#8220;dos,unix&#8221;。则我从 Vim 中新建并保存的一个 ffs.txt 文件，用 <kbd>:set ff?</kbd> 查看的话，其显示值为 &#8220;fileformat=dos&#8221;。
  </p>
  
  <p>
    根据上面表格说明，则 Vim 在保存过程中，在行末添加了 &#8220;^M^J&#8221; 字符，只是在打开时又移除了，所以我们看不见。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">特殊字符</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    用 Vim 打开上面那个 fileformat 值为 dos 的 ffs.txt 文件，然后在命令模式下键入 <kbd>:e ++ff=unix</kbd>，这个命令用于将当前文件的 fileformat 值更改为 unix，根据上表，这样就需要从行末移除 &#8220;LF&#8221;，即 &#8220;^J&#8221; 字符，因为 fileformat=dos 时在行末添加的是 &#8220;^M^J&#8221;，而 fileformat=unix 仅仅移除了 &#8220;^J&#8221;，于是 &#8220;^M&#8221; 这个特殊字符就可见了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_unix_dos">从 unix 转 dos</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_unix_dos" href="#_unix_dos"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    新建一个 ffunix.txt 文件，保存时将它的 fileformat 设置为 unix，这样就会在行末加入 &#8220;^J&#8221; 字符，那么再用 <kbd>:e ++ff=dos</kbd> 转换文件格式为 dos。在 Vim 下方显示文件名称的右侧会出现 <code>[CR missing]</code> 的提示。Vim 试图从 &#8220;^J&#8221; 中移除 &#8220;^M^J&#8221;，于是就出现上面的错误提示了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="_M">清空 ^M</span><a title="标题链接地址" class="u-floatRight hidden" id="hey_M" href="#_M"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    今天试图从 ftp上 直接打开 php 文件，Vim 显示两个 &#8220;^M&#8221; 字符，真够让人傻眼的。上面介绍的转换文件格式的方法显然不能用，则另有个办法，用 Vim 下的替换功能，将特殊字符 &#8220;^M^M&#8221; 替换为空。
  </p>
  
  <p>
    在 Vim 的命令模式下键入 <kbd>:%s/\r//g</kbd>，就可以清空无关的 &#8220;^M&#8221; 字符。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">参考资料</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ol>
    <li>
      <a href="http://vim.wikia.com/wiki/File_format">file format</a>
    </li>
  </ol>
</div>