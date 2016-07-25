---
title: Vimfiler
author: 陈 三
layout: post
date: 2012-09-02T09:19:12+00:00
url: /vimfiler.html
views:
  - 1589
dsq_thread_id:
  - 827715789
categories:
  - 未分类
tags:
  - vim
  - vimfiler

---
我在 Ubuntu 上使用 [ranger][1] 文件管理器，通过 terminal emulator 打开，全键盘操作，键绑定类于 Vim，相当方便。而这个 [vimfiler][2] 则直接在 Vim 中进行文件管理，许多键绑定也是 Vim 一类的，相比 Vim 默认的文件管理器 netrw 功能更为强大，另外，它是用 Vim scripts 写的。

本篇略做介绍。

首先是安装 vimfiler，可以按 [Vundle 管理 Vim 插件][3]一篇介绍的方法来安装，不过因为 vimfiler 依赖于 [unite.vim][4]，所以在之前需要安装 unite.vim，这两个都是同一个作者 [Shougo][5] 的作品。

安装完 vimfiler 后打开 Vim，命令行里输入：

    :VimFiler
    

即可在 Vim 中打开 vimfiler 文件管理器，默认显示当前目录下的内容。

如前面所说的，Vim 本身是带有一个 netrw 文件管理，可以通以下命令打开：

    :e .
    

可以通过在 .vimrc 文件中添加命令开关将这个默认文件管理器更改成 vimfiler:

    let g:vimfiler_as_default_explorer = 1
    

这样 `:e .` 命令打开的就是 vimfiler 而不是 netrw 了。

要退出 vimfiler 也很简单，按 `Q` 键即可退出 vimfiler 回到 Vim 界面，如果是按小写的 `q`，则是隐藏 vimfiler，下次再进入时目录位置仍是上次的目录。

Vim 最常见的几个移动键在 vimfiler 下的作用如下：

  * j &#8211; 向下移动
  * k &#8211; 向上移动
  * gg &#8211; 跳转光标到最上面一个文件或文件夹
  * G &#8211; 跳转光标到最下面一个文件或文件夹
  * h &#8211; 返回上一个文件夹
  * l/Enter &#8211; 进入选中的文件夹或用相关的程序执行文件

刚安装好 vimfiler 然后按 l 键 vimfiler 可能会显示：

    [vimfiler/execute] Associated programs are not found.
    

vimfiler 关联的程序没有找到。这是因为我们还没有对 vimfiler 里的文件类型进行关联。我们可以通过命令来关联，比如我们要将 php 文件用 eclipse 打开：

    call vimfiler#set_execute_file('php', 'eclipse')
    

将上述语句添加到 .vimrc 文件后，我们就可以按 l 键来调用 eclipse 打开 php 文件。

如果需要关联多个打开方式：

    call vimfiler#set_execute_file('php',['eclipse','gvim'])
    

按 l 键后会新开一个 vim 面板窗口，让你选择是用 eclipse 还是 gvim 打开 php 文件。

使用 l 的好处是我们可以自定义很多内容，那如果是想使用默认的打开方式呢？

vimfiler 里提供 `x` 键调用系统默认关联的程序来打开光标位置下的文件。

另外几个相关的编辑按键如下：

  * e &#8211; 使用 Vim 编辑光标位置下的文件，如果是 Vim 无法识别的文件比如图片、视频，打开的会是一片乱码，这里可以 vim 命令行输入 `:e .` 返回到 vimfiler 界面
  * E &#8211; 在 Vim 中分割出一个窗口来编辑光标位置下的文件

以上讲的方法是固定下来的，如果仅是临时想使用其他程序打开内容呢？比如有一个 AVI 格式视频，系统默认使用 Gnome-mplayer 打开，但我这次想用 Mplayer 打开：

  1. 按空格键标记该 AVI 视频，vimfiler 会在文件名前加个星号表示已经标记
  2. 按 `!` 打开 shell 命令输入口
  3. 输入命令 `mplayer`，回车即可

当然，也可以直接按 `!` 调出 shell 命令输入口键入命令 `mplayer abc.avi`，不过据我测试文件名称并没有自动补齐，所以会比较麻烦。

其他如删除、重命名等功能均有提供，不过需要关闭安全模式：

    let g:vimfiler_safe_mode_by_default = 0
    

将上述语句加入 .vimrc 文件即可关闭安全模式，之后就可以进行以下操作：

  * r &#8211; 重命名光标位置下的文件或文件夹名称
  * N &#8211; 新建文件
  * K &#8211; 新建文件夹
  * dd &#8211; 删除光标位置下的文件或文件夹
  * cc &#8211; 复制文件或文件夹，会要求输入目标位置
  * mm &#8211; 移动文件或文件夹，要求输入目标位置

注意，上面 dd/cc/mm 是按了两次，第一次表示选中，第二次才真是是操作命令，也可以先按空格键选中，再按一次 d/c/m 即可。

再来讲讲文件夹或说目录。

  * . &#8211; 显示/隐藏隐藏文件
  * ~ &#8211; 跳转到主目录
  * \ &#8211; 跳转到根目录
  * t &#8211; 展开当前目录下的子文件，包括子文件夹
  * T &#8211; 递归展开当前目录下的文件，包括深层目录里的。如果目录很大，轻易不要用 `T` 来展开。
  * S &#8211; 对目录文件进行排序，排序根据可以选择

如果要在一个目录下查找内容？

  * / &#8211; 如你所料，这个一如继往地可以用，小写的 n 用于跳转到下一个符合项
  * gf &#8211; 执行系统 find 命令
  * gr &#8211; 执行系统 grep 命令

不过，在使用这两个命令前，还需要安装 [vimproc][6]，否则会出现错误提示：No such action: find。 vimfiler 文档里并没有明确说明这个依赖，仍是到 twitter 上问作者才知道的。

这样，一个文件管理器该有的操作都有了。如果还需要了解更多，可以按 `?` 查看帮助，或者 `:help vimfiler`。这个比起 Ubuntu 自带的那个文件管理器可不会差吧。

 [1]: http://ranger.nongnu.org/
 [2]: https://github.com/Shougo/vimfiler
 [3]: http://www.zfanw.com/blog/vundle-vim-plugin-management.html
 [4]: https://github.com/Shougo/unite.vim
 [5]: https://twitter.com/ShougoMatsu
 [6]: https://github.com/Shougo/vimproc