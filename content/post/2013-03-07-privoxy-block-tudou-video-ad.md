---
title: 使用 Privoxy 屏蔽土豆网视频广告
author: 陈 三
layout: post
date: 2013-03-07T12:07:22+00:00
url: /privoxy-block-tudou-video-ad.html
views:
  - 823
dsq_thread_id:
  - 1123766393
categories:
  - 未分类
tags:
  - Privoxy

---
之前写过一篇[利用 Privoxy 屏蔽网页广告的介绍文][1]，稍稍介绍怎样应用它来屏蔽网页中的图片及不需要的内容。这里，再举个实例介绍下屏蔽土豆网视频播放前的广告。

首先，需要查找出视频广告的地址，土豆网的视频广告是 .flv 扩展名，firefox 下，可以借助 firebug 来查看这些广告的网址，Google Chrome 则使用它的开发者工具查看，这些广告的大小约摸大于500K：

[<img src="http://www.zfanw.com/blog/wp-content/uploads/2013/03/Screenshot-from-2013-03-06-2200162.png" alt="firebug 检查网站流媒体" width="659" height="106" class="alignnone size-full wp-image-8340" srcset="https://www.zfanw.com/blog/wp-content/uploads/2013/03/Screenshot-from-2013-03-06-2200162.png 659w, https://www.zfanw.com/blog/wp-content/uploads/2013/03/Screenshot-from-2013-03-06-2200162-300x48.png 300w" sizes="(max-width: 659px) 100vw, 659px" />][2]

找出广告的地址后，就是通过 Privoxy 的 user.action 文件来屏蔽了：

    {+block{土豆网视频广告}}
    27.221.18.172/youku/*
    27.221.18.173/youku/*
    27.221.18.174/youku/*
    27.221.18.179/youku/*
    27.221.18.182/youku/*
    27.221.18.185/youku/*
    60.217.245.11/youku/*
    60.217.245.12/youku/*
    60.217.245.13/youku/*
    60.217.245.14/youku/*
    60.217.245.16/youku/*
    60.217.246.13/youku/*
    60.217.250.11/youku/*
    60.217.250.12/youku/*
    60.217.250.13/youku/*
    60.217.250.15/youku/*
    60.217.251.15/youku/*
    60.217.251.16/youku/*
    60.217.253.11/youku/*
    60.217.253.13/youku/*
    60.217.253.14/youku/*
    119.167.129.11/youku/*
    119.167.129.12/youku/*
    119.167.129.13/youku/*
    119.167.129.14/youku/*
    119.167.129.16/youku/*
    119.167.129.23/youku/*
    119.167.129.24/youku/*
    119.167.129.17/youku/*
    119.167.129.19/youku/*
    119.167.152.41/youku/*
    119.167.152.43/youku/*
    119.167.152.44/youku/*
    119.167.152.49/youku/*
    119.167.152.50/youku/*
    119.167.152.53/youku/*
    119.167.152.54/youku/*
    119.167.152.55/youku/*
    119.188.0.201/youku/*
    119.188.0.202/youku/*
    182.118.6.72/youku/*
    182.118.6.73/youku/*
    182.118.6.74/youku/*
    182.118.6.78/youku/*
    182.118.6.83/youku/*
    182.118.6.85/youku/*
    

列表有点长，但我想这可能还只是一部分，因此以后可能继续更新该列表，具体见 [Github 上的库][3]。如果你也有 github，可以考虑克隆一份，用于维护自己的 Privoxy 配置文件。

 [1]: http://www.zfanw.com/blog/block-webpage-ad-with-privoxy.html
 [2]: http://www.zfanw.com/blog/wp-content/uploads/2013/03/Screenshot-from-2013-03-06-2200162.png
 [3]: https://github.com/chenxsan/Privoxy