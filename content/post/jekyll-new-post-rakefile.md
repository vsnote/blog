---
title: Jekyll 创建新文章
author: 陈 三
layout: post
date: 2014-11-12T13:54:21+00:00
url: /jekyll-new-post-rakefile.html
views:
  - 859
categories:
  - 前端开发
tags:
  - Jekyll

---
我的[静态博客][1]，托管在 Github 上，用 [Jekyll][2] 搭建。但翻遍 Jekyll 的文档，都没找出一个可以方便创建新文章的方法。

依它的意思，我大概要这样创建文章：

    vi _post/2014-11-12-sam-chen.md
    

打开文件后，我还得输入一遍 **date**、**title** 等信息。太过低效。

网上可以找到不少便捷的 Rakefile，比如 [octopress 提供的][3]，不过跟我的设想并不一样，所以最后整理了一份[自己的 Rakefile][4]。

  1. 保存 Rakefile 到 Jekyll 创建的站点根目录下
  2. 执行 `rake new` 命令 
      * 输入 URL，比如要创建 2014-11-12-sam-chen.md 文件，我们只需要输入 _sam chen_，当然，你也可以输入中文，但通常不建议
      * 输入文章标题，即 .md 文件中 front matter 里的 _title_ 的值
      * 输入文章的分类，如果有多个分类，以空格分隔，比如 _Jekyll zfanw_ 这样
      * 最后，Rake 会启动 vi，打开新创建的 md 文件，当然，你也可以配置其他编辑器

打开的文件里，大致的内容如下：

    ---
    layout: post
    title: 陈三的静态博客
    date: 2014-11-12 21:23:09 +0800
    categories: blog
    ---
    

这样，就创建好新文章了。

 [1]: http://chenxsan.github.io/
 [2]: http://jekyllrb.com/
 [3]: https://github.com/imathis/octopress/blob/master/Rakefile
 [4]: https://github.com/chenxsan/chenxsan.github.io/blob/master/Rakefile