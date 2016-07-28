---
title: Emmet-vim 使用错误
author: 陈 三
layout: post
date: 2012-07-04T05:12:26+00:00
url: /zencoding-vim-error.html
views:
  - 1645
dsq_thread_id:
  - 750525256
dsq_needs_sync:
  - 1
categories:
  - 未分类
tags:
  - emmet
  - zencoding.vim

---
估计是我运气不好，经常在使用 Emmet-vim 中出现各种小错误。

这次是在 Ubuntu 系统使用 `git pull` 更新 Emmet-vim，因为我使用 pathogen.vim 管理 vim 插件，所以只是在 .vim/bundle 目录下更新了源，没有其他动作。

接着启动 vim 键入 &#8216;html:5&#8217;，然后按触发键 <kbd><c-y>,</kbd>，结果出现错误：

> Not enough arguments for function:zencoding#expandAbbr

换到 Windows 7 系统，同样更新了源，却没有上述错误出现。

后来想想 Emmet-vim 会在 .vimrc 配置文件里生成内容，比如键的映射等，试着将其清除掉后，再次启动 vim，没有任何错误出现，一切正常使用。

鸣谢：这次还是有跑 twitter 上咨询作者 [@mattn_jp][1]。

<div class='timeline'>
  <h2>
    修订历史
  </h2>
  
  <ol>
    <li>
      <span itemprop='dateModified'>2015-06-17</span>：修改 zencoding.vim 为 emmet-vim。
    </li>
  </ol>
</div>

 [1]: https://twitter.com/#!/mattn_jp