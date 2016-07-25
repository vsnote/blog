---
title: 屏蔽百度推广广告
author: 陈 三
layout: post
date: 2012-04-17T23:20:40+00:00
url: /how-to-block-ads-on-baidu.html
dsq_thread_id:
  - 653749382
views:
  - 2065
categories:
  - 未分类
tags:
  - 屏蔽广告

---
<div class='timeline'>
  <h2>
    修订历史
  </h2>
  
  <ol>
    <li>
      <span itemprop='dateModified'>2015-06-04</span>：如果只是屏蔽 HTTP 页面的广告，推荐使用 Privoxy 软件，<a href="http://www.zfanw.com/blog/block-webpage-ad-with-privoxy.html" title="我的博客上 Privoxy 的教程">更多可以看我博客上的 Privoxy 教程</a>。
    </li>
  </ol>
</div>

百度推广广告也只是 HTML 中的代码，所以屏蔽百度推广广告，其实就是在浏览器展示页面前，先对页面做处理。

这个方法使用的浏览器是 Firefox，配合 [Scriptish][1] 扩展，这是 Greasemonkey 的一个分支。

分析百度推广广告代码可以看到，在 `div#container` 块内, `table#1` 元素前全部是百度竞价排名广告，包括正常排名前经常多达十个的广告，还有右侧的悬浮广告。所以只要移除 `table#1` 前的 HTML 代码即可.

`$("#container table#1").prevAll().remove();`

调用 jQuery 的方法 `prevAll()` 取得 `table#1` 前所有的兄弟元素然后移除。

<del>具体 <a href="http://userscripts.org/scripts/show/131190" title="屏蔽百度推广广告脚本">userscript 安装地址</a></del>「**说明**：userscript 已死」

 [1]: https://addons.mozilla.org/en-US/firefox/addon/scriptish/