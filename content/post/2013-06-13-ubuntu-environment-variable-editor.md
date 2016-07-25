---
title: Ubuntu 环境变量 EDITOR 设置
author: 陈 三
layout: post
date: 2013-06-13T05:21:37+00:00
url: /ubuntu-environment-variable-editor.html
dsq_thread_id:
  - 1396928853
views:
  - 634
categories:
  - Ubuntu

---
Ranger 文件管理器中，按 <kbd>E</kbd> 默认使用 nano 编辑当前文件。据它的文档说明，

> EDITOR
> 
> > Defines the editor to be used for the &#8220;E&#8221; key. Defaults to &#8220;nano&#8221;.

我不懂 nano，想换成 Vim，则要改环境变量 `EDITOR` 的值。

理所当然，我会把 `EDITOR` 值设置为 gvim 路径：

    export EDITOR="usr/bin/gvim"
    

但这样在 Ranger 中按 <kbd>E</kbd> 会报错：

<p class="text-error">
  /bin/sh: 1: usr/bin/gvim: not found
</p>

解决办法是，把 `EDITOR` 直接设置为 `gvim`:

    export EDITOR="gvim"
    

使用 `printenv EDITOR` 或 `echo $EDITOR` 可以检查 `EDITOR` 现在的值。

因为我想把 `EDITOR` 值固定下来，就把它写入 .bashrc 文件中：

    EDITOR="gvim"
    

## 参考

  1. [Ubuntu Environment Variables][1]

 [1]: https://help.ubuntu.com/community/EnvironmentVariables