---
title: Vimperator 打开多个链接
author: 陈 三
layout: post
date: 2012-11-30T05:28:14+00:00
url: /vimperator-multi-links.html
views:
  - 2259
dsq_thread_id:
  - 950870344
categories:
  - Firefox
  - vimperator
tags:
  - vimperator

---
Vimperator 按 <kbd>f</kbd> 或 <kbd>F</kbd> 键进入 hint 模式，就可以通过键盘打开页面内的链接。但是，这种方法只能打个一个链接，总有些人想同时打开多个链接的，比如我。

这个方法使用 Vimperator 的插件 [multi-hints.js][1]。

  1. 下载 multi-hints.js 到 .vimperator/plugin 目录下
  2. 在 vimperator 命令行运行 `:loadplugins`，又或者重启 firefox
  3. 在 vimperator 命令行运行 `:multihints follow`，然后按确定键
  4. 输入要打开的链接的 hint 数字/字母，不同链接的 hint 值用空格分开，比如下图：
    
    [<img src="http://www.zfanw.com/blog/wp-content/uploads/2012/11/vimperator-multi-links.png" alt="vimperator 打开多链接" title="vimperator-multi-links" width="518" height="106" class="alignnone size-full wp-image-7097" srcset="https://www.zfanw.com/blog/wp-content/uploads/2012/11/vimperator-multi-links.png 518w, https://www.zfanw.com/blog/wp-content/uploads/2012/11/vimperator-multi-links-300x61.png 300w" sizes="(max-width: 518px) 100vw, 518px" />][2]
    
    在命令行输入 ll la ls ld 后按确定键，firefox 将在新标签页中打开四个链接

  5. 每次都输入命令行肯定也不方便，就 map 一个快捷键给命令，在vimperator 配置文件中加下以下命令：
    
        :nnoremap <C-A-m> :multihints follow<CR>
        

  6. 重启 firefox 或者 `:source ~/.vimperatorrc`

  7. 之后就可以通过按 <kbd>Ctrl-Alt-m</kbd> 来启用 multihints 打开多个链接

**Update** &#8211; 2012.12.14

「老杨」在评论里提到 Vimperator 扩展 hint 模式下 <kbd>;F</kbd> 用于打开多个链接，这个在我前文中并没有提到，感谢提醒。

对比我所描述的方法，这两者有一个小小差别：<kbd>;F</kbd> 是「一个一个打开多个链接」，multi-hints.js 则是「一下子打开多个链接」。

从我的体验上说，后者要比前者更流畅。当然，也如回复老杨的评论中我所强调的，之所以我用这个方法，是根据我个人的偏门需求定制的 &#8211; 这是 Vimperator 最大的好处，可定制性。

 [1]: https://github.com/caisui/vimperator/blob/master/plugin/multi-hints.js
 [2]: http://www.zfanw.com/blog/wp-content/uploads/2012/11/vimperator-multi-links.png