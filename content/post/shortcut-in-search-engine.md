---
title: 搜索引擎框中的快捷键
author: 陈 三
layout: post
date: 2012-12-02T07:48:07+00:00
url: /shortcut-in-search-engine.html
views:
  - 1603
dsq_thread_id:
  - 954003178
categories:
  - Firefox
  - vimperator
tags:
  - Firefox
  - vimperator

---
搜索引擎框中有许多快捷键可以用，并且与 Bash、Emacs 一类软件相通，如果能熟练使用，可以很好提高效率。

以下分别列出，其中 &#8220;C&#8221; 表示 Ctrl 键。

假设搜索框中的字符串为 &#8220;**Hello vi*mperator on firefox**&#8220;，字符串中的星号表示光标位置。

| 快捷键            | 作用及示例说明                                    |
| -------------- | ------------------------------------------ |
| <kbd>C-a</kbd> | 跳转到搜索框所有字符前（Hello 之前）                      |
| <kbd>C-e</kbd> | 跳转到搜索框所有字符后（firefox 之后）                    |
| <kbd>C-k</kbd> | 从光标位置起，删除所有往后的字符（剩下 Hello vi）              |
| <kbd>C-u</kbd> | 从光标位置起，删除所有往前的字符（剩下 mperator on firefox）   |
| <kbd>C-d</kbd> | 删除光标位置后一个字符（剩下 Hello viperator on firefox） |
| <kbd>C-h</kbd> | 删除光标位置前一个字符（剩下 Hello vmperator on firefox） |
| <kbd>C-z</kbd> | 取消删除                                       |
| <kbd>C-w</kbd> | 删除光标位置前的一个单词（剩下 Hello perator on firefox）  |

在 Bash 中，<kbd>C-f</kbd> 表示向前（右）移动一个字符，<kbd>C-b</kbd> 表示向后（左）移动一个字符，但是在 firefox 下，这两个的作用分别是“查找”与“打开书签侧边栏”。在 vimperator 下我并不需要这两个功能，就可以在 .vimperatorrc 配置文件中将其映射给移动字符的功能：

    inoremap <C-f> <Right>
    inoremap <C-b> <Left>
    

可以从上面的表格里看到，我们可以通过 <C-w> 删除光标位置前一个单词，那么要删除光标位置后一个单词如何？Bash 下是通过 <kbd>A-d</kbd> （A 指 alt 键），firefox 下或 vimperator 下这个键组合是选中导航栏上的网址。当然，我们也可以通过键映射来完成，只是有些复杂：

    inoremap <A-d> <C-t>dwi
    

当 Vimperator 处于插入模式(insert mode)时，按 <kbd>C-t</kbd> 可以进入 textarea mode （文本区域模式），可以把它理解为简单的 vi 模式，像 h l ^ $ 之类的键统统可用，这时按 <kbd>dw</kbd> 可以删除到光标位置后的一个单词，最末的一个 <kbd>i</kbd> 则是从 textarea mode 转回插入模式。

当然，以上快捷键并不仅限于搜索引擎中，凡是网页上的文本框基本都可以使用。另外，某些方法比如删除单词在中文里并不适用，因为中文并不通过空格来分词。