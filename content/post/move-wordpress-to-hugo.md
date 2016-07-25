+++
date = "2016-07-25T18:28:49+08:00"
title = "从 WordPress 到 Hugo"
url = "/move-wordpress-to-hugo.html"
+++

我还记得，我是在 2009 年的五四青年节注册的这个域名。当初的目的，并不是写 blog，只是后来只有 blog 活了下来。

当时 WordPress 风头正劲，我虽然不懂 PHP，也还是靠着文档，把这个 blog 搭了起来。也感谢 WordPress，否则我现在对 Linux/Unix 环境可能还是一无所知。

说说迁移的理由：

1. 现在的[静态内容生成工具很多](https://www.staticgen.com/)，易用性不输 WordPress；另外前端开发环境变化很大，比如 AutoPrefixer 这样的工具，要集成到 WordPress 里其实很难
2. PHP 太脆弱了，如果我在线修改 WordPress 的主题，很可能整个站点都要挂掉，最后只能 ssh 到 vps 上直接改源文件
2. 最重要的，WordPress 的评论系统没什么用处。我曾经关过评论 - 因为垃圾评论太多，而真正的评论太少。而今我后台的 200 多条评论，大约找得出两条值得迁移的：

    ![phoenixframework comment](img/elixir-phoenix-framework-comment.png)

    ![babel 6](img/babel-6-comment.png)

当然，WP 也有擅长的，比如 4.4 里推出的[响应式图片](https://make.wordpress.org/core/2015/11/10/responsive-images-in-wordpress-4-4/)，目前在 [Hugo](https://gohugo.io/) 下我还不知道如何弄。但这是后话 - 迁了再说。

至于为什么用 Hugo - 它是基于 golang 搭建的，而不是用 Hexo 这些基于 Node.js 搭建的，大概要说是缘份，因为曾在 twitter 上看过我 follow 的一个人用了 Hugo - 就这样。

不过，目前使用 [wordpress to hugo exporter 做的迁移](https://github.com/SchumacherFM/wordpress-to-hugo-exporter)并不完整，还有许多要手动处理的。

## TODO

1. 代码高亮 - 多数需要修订
2. 图片的显示问题
  1. 限定最大宽度 [x]
  2. 响应式 [ ]
  3. 点击查看大图 [ ]
3. 评论系统？
4. service worker
5. AutoPrefixer
6. fix rss

