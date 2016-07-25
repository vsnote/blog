---
title: CSS 最糟实践之复杂标签
author: 陈 三
layout: post
date: 2015-05-18T12:06:51+00:00
url: /css-worst-practice-complex-tag-selectors.html
views:
  - 733
categories:
  - 前端开发
tags:
  - css
  - 最佳实践

---
我开始学 CSS 时，写过很多现在来看非常糟糕的 CSS。这是我想写这一个系列的直接原因：也许我们不知道要怎么做，但知道了什么不该做，就约略知道要怎么做了。

这篇是 CSS 最糟实践系列的第一集，**复杂标签选择器**。

假设 A 君写了这么一条规则：

    header ul li a { color: white; background: #333; text-decoration: none; }
    

设置 `header` 元素里的 `ul` 下的 `li` 的 `a` 链接前景色为白色，背景色为 `#333`，无下划线。

我们在未来可能碰上以下问题：

  1. HTML 结构变了，这条规则失效，需要修改。但是没人敢动这条规则，因为谁也不敢确认，这条规则有没有什么地方用到，所以我们为减少意外，又根据变化后的 HTML 结构加了一条 CSS 规则 &#8211; CSS 文件越来越大。
  2. 其他人写了一条特异性更高的规则，比如 `header .menu-item { color: blue; }` &#8211; 我们无法阻止这样的副作用发生，换句话说，我们的 CSS 规则变得不可预测 &#8211; 它可能是前景白、背景黑，也可能压根不是这个样子，对，我们写的不是 CSS，是薛定锷的猫。

而如果我们这样写：

    .link {
      text-decoration: none;
    }
    .link--standout { color: white; background: #333; }
    

然后在 HTML 中应用：

    <header>
      <ul>
        <li><a class='link link--standout'>陈三的博客</a></li>
      </ul>
    </header>
    

我们就解决了前面的规则可能引起的问题：

  1. HTML 结构变化现在对我们的 CSS 规则没什么影响
  2. 因为样式是通过 CSS 类应用的，所以我们根本不担心其他人的规则无端渗入

是的，CSS 的全称叫层叠样式表，但实际上，层叠的样式只是灾难 &#8211; 除非你写的页面像我[首页][1]这么简单。

 [1]: http://www.zfanw.com