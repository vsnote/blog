---
title: URL 末尾的 ／
author: 陈 三
layout: post
date: 2013-02-04T16:07:10+00:00
url: /slash-in-url-end.html
views:
  - 691
dsq_thread_id:
  - 1064841313
categories:
  - 未分类
tags:
  - 301

---
我的博客是放在服务器主目录 blog 文件夹下，即 /blog/ 这样的文件结构。以前我的概念里，是以为博客 URL 为 zfanw.com/blog 的，后来发现还有一个 zfanw.com/blog/，即 URL 末尾多了一个斜杠，虽然我所访问的内容并没有差异，但这两者还是有一点区别。

传统用法中，URL 末的斜杠指示一个目录，没有斜杠则表示文件。但并没有强制说一定要这样，以 zfanw.com/blog 来说，服务器找不到 blog 文件，只找到 blog 目录，则会根据服务器配置来返回目录里的默认页，比如 index.html。

但这样多了一道不必要的判断，而且，两个不同的网址返回相同的内容，对于搜索引擎来说，这就是重复内容。所以，如果内容相同，就做一个跳转，或301跳转或302跳转，统一使用一个网址。

不过 WordPress 后台中设置 ”WordPress Address“ 时，末尾的 / 会被强制去掉。也就是说，它认可的是 zfanw.com/blog 这个网址，而非 zfanw.com/blog/ 这个网址。所以我只能强制进行跳转。

再来看看实践方面，打开 Google 搜索 [inurl:&#8221;.com/blog&#8221; intext:&#8221;powered by wordpress][1]，可以看到很多由 WordPress 架设的，类似我博客网址的网站，通过下列命令查看 HTTP 头：

    curl -I xxx.com/blog
    

可以看到，基本上都有做过301跳转到 /blog/ 上。当然，这实践是别人的，你跳不跳转还是取决于你。

## 扩展阅读

  1. [Official Google Webmaster Central Blog: To slash or not to slash][2]

 [1]: https://www.google.com/search?num=50&hl=en&safe=off&q=inurl%3A%22.com%2Fblog%22+intext%3A%22powered+by+wordpress%22&oq=inurl%3A%22.com%2Fblog%22+intext%3A%22powered+by+wordpress%22"
 [2]: http://googlewebmastercentral.blogspot.jp/2010/04/to-slash-or-not-to-slash.html