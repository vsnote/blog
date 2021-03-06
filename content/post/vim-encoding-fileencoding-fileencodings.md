---
title: VIM 编码
author: 陈 三
layout: post
date: 2012-03-10T23:59:16+00:00
url: /vim-encoding-fileencoding-fileencodings.html
dsq_thread_id:
  - 606262156
views:
  - 2085
categories:
  - 未分类
tags:
  - encoding
  - fileencoding
  - fileencodings
  - vim

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 乱码</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 测试</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 总结</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#Ubuntu_Gvim_option"><span class="toc_number toc_depth_1">4</span> Ubuntu 下 Gvim 的 option</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <h2 class="storycontent-h2">
    <span id="i">乱码</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Vim 里关于编码有多个 option，比如 encoding、fileencoding、fileencodings、termencoding。用 <kbd>:help xxx</kbd> 分别查看，就会有一个疑问：为什么会有这么多 option 存在？然后你可以自言自语地总结：存在总是有其历史的不正确的原因或者非历史的正确原因。
  </p>
  
  <p>
    但对于普通用户来说，其实无谓多少 option 存在，只要能不乱码，又或者乱了知道怎么处理就够了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">测试</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    Windows 7 下 Gvim 7.3.46 版本，界面为中文，环境变量 $LANG 值为 zh-CN，上面几个 option 的默认值分别为：
  </p>
  
  <ul>
    <li>
      termencoding=
    </li>
    <li>
      encoding=cp936
    </li>
    <li>
      fileencoding=
    </li>
    <li>
      fileencodings=ucs-bom
    </li>
  </ul>
  
  <p>
    按帮助内容说，当 termencoding 值为空时，取值与 encoding 一样，即也为 <a href="http://en.wikipedia.org/wiki/Code_page_936">cp936</a>，cp936 是微软的简体中文字符编码集。
  </p>
  
  <p>
    fileencoding 为空其取值也是与 encoding 一样，也是 cp936。
  </p>
  
  <p>
    针对文件我们可以有两种常见行为，一是创建，一是读取，创建时用一种编码集，读取时又用一种编码集，如果读取时所用的编码集与创建时所用不同，就可能出现乱码。
  </p>
  
  <h3>
    记事本下的不同编码
  </h3>
  
  <p>
    我的测试是打开记事本，并分别另存两个 txt 文件，一个编码为 ANSI ，一个编码为 UTF-8，然后用 Gvim 打开并查看上述各 option 的取值变化。
  </p>
  
  <ul>
    <li>
      ANSI <ul>
        <li>
          termencoding=
        </li>
        <li>
          encoding=cp936
        </li>
        <li>
          fileencoding=
        </li>
        <li>
          fileencodings=ucs-bom
        </li>
      </ul>
    </li>
    
    <li>
      UTF-8 <ul>
        <li>
          termencoding=
        </li>
        <li>
          encoding=cp936
        </li>
        <li>
          fileencoding=utf-8
        </li>
        <li>
          fileencodings=ucs-bom
        </li>
      </ul>
    </li>
  </ul>
  
  <p>
    从结果可以看到，记事本保存的两个不同编码文件在 Vim 中打开并未出现乱码的情况。
  </p>
  
  <h3>
    乱码来了
  </h3>
  
  <p>
    那么来见一下乱码的情形。
  </p>
  
  <p>
    在 Vim 的配置文件 _vimrc 里加上一句 <code>set fileencoding=utf-8</code>，然后从 Vim 中新建一个 vim-utf-8.txt 文件，保存后重新用 Vim 打开，接着乱码就出现了。查看各个 option 值，唯 fileencoding 值与新建时不一样，变成 cp936。
  </p>
  
  <p>
    也就是说，在新建这个文件时所用的编码是 utf-8，到打开时使用的却是 cp936，因为 utf-8 的字符集要大于 cp936，于是就出现乱码。
  </p>
  
  <p>
    所以我们需要 Vim 在读取文件时认得其所用编码，又或者读取所用的字符集包含了创建所用的字符集。
  </p>
  
  <h3>
    解决乱码
  </h3>
  
  <p>
    在 _vimrc 文件中增加一行 <code>set fileencodings=utf-8,&lt;a href="https://zh.wikipedia.org/wiki/位元組順序記號">ucs-bom&lt;/a></code>，这样 Vim 在读取时给要打开的文件应用的编码就按 fileencodings 从从左住右应用第一个找到的可用编码，类似于 CSS 下的 font-family 用法。
  </p>
  
  <p>
    重新打开 vim-utf-8.txt 文件，这时乱码已经消失，查看 fileencoding 值，已经是 utf-8 了。
  </p>
  
  <p>
    另外，上述乱码情况在不更改 fileencodings 的情况下可以使用在 Vim 命令行模式下调用 <kbd>:e ++enc=utf-8</kbd> 强制更改，一如 <a href="http://www.zfanw.com/blog/vim-file-format-problem.html">Vim 文件格式</a> 一篇提到的办法。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">总结</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ul>
    <li>
      创建文件时所用编码据 fileencoding 值
    </li>
    <li>
      读取文件时所应用编码据 fileencodings 值
    </li>
    <li>
      termencoding 与 encoding 值平常用户一般不用管
    </li>
  </ul>
  
  <h2 class="storycontent-h2">
    <span id="Ubuntu_Gvim_option">Ubuntu 下 Gvim 的 option</span><a title="标题链接地址" class="u-floatRight hidden" id="heyUbuntu_Gvim_option" href="#Ubuntu_Gvim_option"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <ul>
    <li>
      $LANG=en.US_UTF-8
    </li>
    <li>
      termencoding=utf-8
    </li>
    <li>
      encoding=utf-8
    </li>
    <li>
      fileencoding=
    </li>
    <li>
      fileencodings=ucs-bom,utf-8,default,latin1
    </li>
  </ul>
</div>