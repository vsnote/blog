---
title: Ember.js 在 IE 下渲染问题
author: 陈 三
layout: post
date: 2014-03-25T21:10:25+00:00
excerpt: Ember.js 页面在 IE 浏览器下无法渲染，去除 console.log 恢复正常
url: /ember-js-not-render-in-ie.html
views:
  - 506
categories:
  - 前端开发
tags:
  - ember.js

---
_Note：本文基于 Ember.js 1.4.0_

Google Chrome、Firefox 下，Ember.js 页面均正常渲染，但 IE9 里，却出现页面无法渲染的问题 &#8211; 尤其是在使用国产某所谓极速浏览器下，从 IE9 内核切换到 Chrome 内核，再来回切换几次，就很容易爆出该问题。

根据 Ember.js 最近的一篇博客[^12010.1]说明，IE 浏览器里，它是**支持 IE8 以上**的，

> Despite the imminent End of Life status of Windows XP, we will continue supporting Internet Explorer 8. We know many Ember.js users still need to target enterprise and education customers, who will be on IE8 for some time.

再来看 Fiddler2 的抓包结果，一切请求均正常，没有丢失或请求失败的情形。初时以为代码逻辑有问题，但找来找去都没有结果。后来灵光一现：**IE 低版本里，以前曾碰上过因为代码里带 `console.log()` 引起的问题**。于是把 app.js 中所有 `console.log` 命令全部注释掉，再开 IE9 测试，莫名地恢复正常渲染 &#8211; 但我仍不敢确定，问题是不是真的因 console.log 而起。

[^12010.1]:    
    [Ember.js &#8211; What&#8217;s Coming in Ember in 2014][1]

 [1]: http://emberjs.com/blog/2013/12/17/whats-coming-in-ember-in-2014.html