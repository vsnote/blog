---
title: iOS Safari 点击事件无效
author: 陈 三
layout: post
date: 2015-05-01T12:36:40+00:00
url: /ios-safari-click-not-working.html
views:
  - 1603
categories:
  - 前端开发
tags:
  - iOS
  - Safari

---
我久远的记忆中，自己曾经碰上过这一问题，只是后来没再怎么接触移动端的 Web，就又忘了干净。

这一次是这样的，我的 blog 点击左上图标，会从左侧拉出一块导航，并且会有个 overlay 层覆盖住，点击 overlay 层的话，导航会收回去。

但 iOS 上的 Safari 里，点击 overlay 层是没有反应的。

JavaScript 代码如下：

    $(document).on('click', '.overlay', function() {
        $('html').toggleClass('cs-app--open');
    });
    

一个简单粗暴的解决办法是，把事件同样绑定给 `touchstart` 或 `touchend` 事件：

    $(document).on('click touchstart', '.overlay', function() {
        $('html').toggleClass('cs-app--open');
    });
    

但这样如果页面要滚动就没办法了。

另外一个办法，由 iOS Developer library 提供：

    <div class = 'overlay' onclick = 'void(0)'></div>
    

通过增加一个空的 `onclick` 事件处理器，我们让该 div 块可以点击了。

最后还有一个办法，是给 `.overlay` 声明一个 CSS 规则：

    .overlay { cursor: pointer; }
    

相比之下，我显然倾向最后一个方法。

再来说原因。

iOS 上，屏幕是触碰的，所以页面元素默认会有 `touch` 一类事件，而不是 `click`。也就是说，我点击上面的 `.overlay` 元素时，iOS 上的 Safari 冒泡的是 `touch` 一类事件，而不是 `click`。只有两类元素，链接与 input 输入域才有 `click` 事件，但通过 `cursor: pointer` 及 `onclick=` 代码我们又可以给其它元素变得可点击。这是 iPhone 上的 Safari 有别与其它浏览器的地方。

## 扩展阅读

  1. [Click event delegation on the iPhone][1]
  2. [Making Elements Clickable][2]

附：如果你有在页面上使用 [FastClick][3]，则上面的问题已经顺带解决，不需要我们操心。

 [1]: http://www.quirksmode.org/blog/archives/2010/09/click_event_del.html
 [2]: https://developer.apple.com/library/ios/documentation/AppleApplications/Reference/SafariWebContent/HandlingEvents/HandlingEvents.html#//apple_ref/doc/uid/TP40006511-SW6
 [3]: http://ftlabs.github.io/fastclick/