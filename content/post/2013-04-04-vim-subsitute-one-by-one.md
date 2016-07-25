---
title: Vim 批量依次替换链接
author: 陈 三
layout: post
date: 2013-04-04T14:46:36+00:00
url: /vim-subsitute-one-by-one.html
dsq_thread_id:
  - 1186542451
views:
  - 1006
categories:
  - 未分类
tags:
  - vim

---
以前写过一篇[利用 Vim 进行批量替换的内容][1]，但可操作性不高，或者说写得有点稀里糊涂，因此补一篇。

**应用情景**：淘宝页面。

大部分人在上传淘宝图片的流程应该是如下：

设计 -》 切图 -》 图片加许多热点 -》 每个热点上添加链接 -》 上传图片到淘宝空间 -》将本地图片地址替换成淘宝空间的图片地址 -》 拷贝完成的代码到淘宝上 -》 保存发布页面

这里，有两个过程是重复枯燥且容易出错的，一个是图片热点上添加链接，一个是替换图片地址。

图片上添加热点的工作，很多人是在 Dreamweaver 里完成的，生成的代码一般是如下：

    <img src="img/hello-vim.jpg" usemap="#Map" border="0">
    <map name="Map">
        <area shape="rect" target="_blank" coords="1,0,178,261" href="#"> 
        <area shape="rect" target="_blank" coords="193,1,373,263" href="#"> 
        <area shape="rect" target="_blank" coords="386,-3,563,263" href="#"> 
        <area shape="rect" target="_blank" coords="577,-2,758,260" href="#"> 
        <area shape="rect" target="_blank" coords="771,4,961,264" href="#"> 
    </map>
    

这里，要将每个 # 替换成链接。

从我的理解看，找一个链接然后切换到 Dreamweaver 可视化界面或者是代码界面替换掉 # 然后再重复同样动作，这种效率极差，因为有个切换过程，并且同时在做多件事，精力分散了。

所以，一个改进的流程是，先按顺序把所有热点链接找出，如下面的列表1：

  * http://www.example.com/1.html
  * http://www.example.com/2.html
  * http://www.example.com/3.html
  * http://www.example.com/4.html
  * http://www.example.com/5.html

然后依次将其替入热点图代码中的 #。

再来看我以前写的 Vim 函数：

    function Cclist()
    "注，下面一行用于删除文件中的空行(更新：2011.8.11 10：31)
       g/^$/d
       let lastline=line('$')
       let g:imglist=[]
       for line in getline(1,lastline)
          call add(g:imglist,line)
       endfor
       return g:imglist
    endfunction
    

将其拷入 .vimrc 文件中，任何启动的 Vim 都将带有这个 Cclist 函数 &#8211; 当然，这个名称可以随你取，只要函数名首字母大写。

函数的作用在于从列表1生成一个全局变量，这个 Vim 全局变量在打开的 Vim 窗口中可以调用到。

函数的用法是用 Vim 打开列表1文件，然后按 <kbd>:</kbd> 进入 Vim 的命令行模式，运行 `call Cclist()<CR>`(注:`<CR>` 指按确定键)，之后就生成 imglist 这个变量。

因为我基本不用 <kbd>F6</kbd> 键，所以在 .vimrc 中我把它映射给运行 Cclist() 函数的功能：

    map <F6> :call Cclist()<CR>
    

之后在 Gvim 窗口按 <kbd>F6</kbd> 即可生成 imglist 变量。

接着用同一个 Vim 窗口(测试过不同 Vim 窗口下检测不到 imglist 变量)打开 Dreamweaver 中生成的热点图片代码，进入命令行模式，运行如下命令：

    let i=0<CR>
    g/href="#"/s//\='href="'.imglist[i].'"'/g | let i+=1<CR>
    

注意，它们是两行命令。`\=` 形式的替换比较少见，可以参见 [vimdoc][2] 的说明。

然后我们就可以看到 Vim 提示替换了几行内容。

图片地址从本地替换成淘宝空间上的地址时也可以如法炮制：

    let i=0
    g/src="images\/.*\.jpg"/s//\='src="'.imglist[i].'"'/g | let i+=1
    

因为 Vim 可以轻松进行键映射，所以上述命令的输入完全可以通过键映射来简化：

    function SubsituteLinks(imglist)
      let imglist=a:imglist
      let i=0
      g/href="#"/s//\='href="'.imglist[i].'"'/g | let i+=1
    endfunction
    map <F6> :call Cclist()<CR><C-w><C-w>:call SubsituteLinks(g:imglist)<CR>:w<CR>
    

这样，在链接的窗口中只要按一下<kbd>F6</kbd> 键，即可以完成**切换到下一个窗口中替换所有链接并且保存修改到文件中**的工作。

整合一下所有的代码如下：

    function Cclist()
    "注，下面一行用于删除文件中的空行(更新：2011.8.11 10：31)
       g/^$/d
       let lastline=line('$')
       let g:imglist=[]
       for line in getline(1,lastline)
          call add(g:imglist,line)
       endfor
       return g:imglist
    endfunction
    "定义替换链接的函数
    function SubsituteLinks(imglist)
      let imglist=a:imglist
      let i=0
      g/href="#"/s//\='href="'.imglist[i].'"'/g | let i+=1
    endfunction
    "定义替换图片地址的函数
    function SubsituteImages(imglist)
      let imglist=a:imglist
      let i=0
      g/src="images\/.*\.jpg"/s//\='src="'.imglist[i].'"'/g | let i+=1
    endfunction
    "键映射相应的动作，F6 键替换链接地址，F7 键替换图片地址
    map <F6> :call Cclist()<CR><C-w><C-w>:call SubsituteLinks(g:imglist)<CR>:w<CR>
    map <F7> :call Cclist()<CR><C-w><C-w>:call SubsituteImages(g:imglist)<CR>:w<CR>
    

将上述代码拷入 .vimrc 文件中，然后准备好材料，即可一键完成图片或链接的替换工作。

 [1]: http://www.zfanw.com/blog/vim-substitute-script-function.html
 [2]: http://vimdoc.sourceforge.net/htmldoc/change.html#sub-replace-expression