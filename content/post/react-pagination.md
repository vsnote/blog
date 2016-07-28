---
title: 翻页组件
author: 陈 三
layout: post
date: 2015-10-07T12:26:28+00:00
url: /react-pagination.html
views:
  - 606
categories:
  - 前端开发

---
放假期间，在用 react.js 写一个[翻页组件][1]，于是就考察了些网站，看它们的翻页组件是怎么做的。

  1. Google
    
    [resp_image id=&#8217;17545&#8242; caption=&#8221; ]

  2. Bing
    
    [resp_image id=&#8217;17547&#8242; caption=&#8221; ]

  3. nngroup
    
    [resp_image id=&#8217;17548&#8242; caption=&#8221; ]

我怀疑它们是商量好了。

最早，我仿照它们做了一个，后来，又加上显示总页数的功能：

[resp_image id=&#8217;17551&#8242; caption=&#8221; ]

但我又在揣测，为什么它们不显示总页数？

是否是因为数字太大已然失去了意义？比如 Google 中搜索 `hello`，能找到约 841,000,000 条结果，如果一页显示 10 条，则按我的设计，页码最末会显示 2 / 84100000。这么大的数字，对用户已经失去意义，所以不如剔除。界面上还显得干净，易于布局。

 [1]: https://github.com/chenxsan/pager