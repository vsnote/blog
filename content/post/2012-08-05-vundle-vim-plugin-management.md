---
title: Vundle 管理 Vim 插件
author: 陈 三
layout: post
date: 2012-08-05T04:35:20+00:00
url: /vundle-vim-plugin-management.html
views:
  - 3462
dsq_thread_id:
  - 793263119
categories:
  - 未分类
tags:
  - vim
  - vim script
  - vundle

---
如果用 [pathogen][1] 管理 vim 插件，bundle 文件夹下 vim 插件的更新很麻烦，你需要针对每个插件分别升级。如果你还有不同电脑，那么不同电脑上 vim 插件保持一致也成问题。

Vundle 可以解决上述问题。

首先，你的操作系统需要事先安装 git，然后利用 `git clone` 命令从 github 上下载 Vundle：

    $ git clone https://github.com/gmarik/vundle.git ~/.vim/bundle/vundle
    

打开 .vimrc 配置文件（Windows 系统上为 _vimrc)，配置要安装的 vim 插件：

<pre lang="vim"><code>
 set nocompatible               " 设置 vim 为不兼容 vi 模式
 filetype off                   " 必须的

 set rtp+=~/.vim/bundle/vundle/
 "Windows系统下上一语句修改为
 "set rtp+=$VIM/vimfiles/bundle/vundle/
 call vundle#rc()

 " 让 Vundle 管理 Vundle
 " 此条必须有
 Bundle 'gmarik/vundle'

 " 比如我的 vim 插件
 "
 " 代码源在 github 上的
 Bundle 'mattn/zencoding-vim'
 Bundle 'Lokaltog/vim-powerline'
 Bundle 'kien/ctrlp.vim'

 " 代码存放在 vim script 上
 Bundle 'FuzzyFinder'

 " 代码存放在其他地方
 Bundle 'git://git.wincent.com/command-t.git'
 " ...

 filetype plugin indent on     " 必须有
 "
 " Brief help
 " :BundleList          - list configured bundles
 " :BundleInstall(!)    - install(update) bundles
 " :BundleSearch(!) foo - search(or refresh cache first) for foo
 " :BundleClean(!)      - confirm(or auto-approve) removal of unused bundles
 "
 " see :h vundle for more details or wiki for FAQ
 " NOTE: comments after Bundle command are not allowed..
</code>
</pre>

接下来，vim 中运行命令 `:BundleInstall` 就可以自动安装上述配置文件中的 vim 插件，而如果要更新插件，运行命令 `:BundleInstall!`。

如果要删除插件，则从 .vimrc 文件中删除或注释掉相应行，然后运行 `:BundleClean` 即可。

之后，只要在不同电脑上同步 .vimrc 文件就可以保证不同电脑上的 vim 插件一致。

## 参考

  1. <http://www.charlietanksley.net/philtex/sane-vim-plugin-management/>
  2. <https://github.com/gmarik/vundle>

 [1]: https://github.com/tpope/vim-pathogen