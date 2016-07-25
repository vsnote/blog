---
title: JavaScript 与 HTML 元素状态
author: 陈 三
layout: post
date: 2013-08-31T15:56:40+00:00
excerpt: HTML 元素的状态不应该全然依赖 JavaScript。
url: /javascript-and-html-element-state.html
views:
  - 428
categories:
  - 前端开发
tags:
  - css
  - jQuery

---
如果把 HTML 元素状态简单分为两种，显示和隐藏，那么，我们常常需要通过 JavaScript 控制它们。

举 [jQuery 选项卡插件][1] 来说，初始化时，我们只显示第一个选项卡对应内容块，隐藏其余内容块，这可以通过 JavaScript 实现：

    $(this).children('div:not(:first)').hide();
    

但我的插件中，添加了 `.is-hide` 类来隐藏元素。之所以不用 JavaScript 控制，是因为我觉得，CSS 类应该在 HTML 代码中起到辅助语义的作用。在我们只阅读 HTML 代码时，看到一个叫 `.is-hide` 的 CSS 类，马上可以明白，这一段元素是隐藏状态的。但如果用 JavaScript 来控制，情况就不一样。我们看 HTML 代码，元素应该是显示的，再看 CSS，元素应该是显示的，但前台却没显示，那只能认为是 JavaScript 干的 &#8211; 这让事情变得不可预测。

<del>像上面我使用的 HTML 结构，可能后端开发看了会说，你这段代码结构怎么能有一个特例？这样我无法遍历输出呀。刻薄点说，我是不是也可以对设计人员说，你这些设计怎么能有一个特例，我无法抽象 CSS 模块类呀。</del>

我用过许多 jQuery 插件，它们都包揽太多工作。比如幻灯片插件，我们只要提供一个 HTML 基础骨架，它就能打包生成 Prev/Next 按钮，pager 等，我觉得这很糟糕，完全的黑箱操作，确实，这样能减少前端人员的一些工作，但对 CSS 结构或者 HTML 的可阅读性并没有帮助。所以我很欣赏 Bootstrap [Carousel][2] 插件的 HTML 结构，要求用户自己写，也就给了我们很大操作空间 &#8211; 写得好还是坏，就是我们的问题。

 [1]: http://www.zfanw.com/blog/jquery-plugin-tab.html
 [2]: http://getbootstrap.com/javascript/#carousel