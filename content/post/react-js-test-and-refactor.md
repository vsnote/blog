---
title: React.js 测试与重构
author: 陈 三
layout: post
date: 2015-09-21T23:07:32+00:00
excerpt: 测试代码帮忙守门
url: /react-js-test-and-refactor.html
views:
  - 722
categories:
  - 前端开发
tags:
  - react.js

---
我有时在给 react.js 组件写测试时，总是想发笑，因为，好像都是在测试些显然的东西，比如：

    expect(loading.type).toBe('div')
    

我说，见鬼了，为什么我要 `expect` 它的 type 是 `div`？其它的就不行吗？比如 `span`？老实说，它到底是 block 元素还是 inline 元素又有什么关系，反正有 CSS 规则可以控制。

但我看 react.js 官方的测试说明里经常出现这样的语句，心想无害，不妨也先写上，也许哪天就突然明白了。

但至今为止，我还是没有明白。

只是这并不妨碍我继续热衷给组件写测试。

因为我发现，组件的代码，与测试的代码，有一种正比关系：如果组件的代码太复杂，那么测试的代码就会非常恶心，比如有一次，我写出这样的测试代码：

    expect(loading.props.children[0].props.children.type).toBe('span')
    

如果再要测试 `click` 事件，则简直想把电脑扔出窗外 &#8211; 22 层。

我马上醒悟，这可能就是所谓的 [code smell][1]，我的 react 组件需要重构了。

我觉得这是 react.js 可爱的地方，它竟然让人生出一种不断解构组件的冲动 &#8211; 有人会说我现在拿 react.js 当锤子，看见什么都当钉子。

我承认，我现在是有这么种倾向。

 [1]: https://en.wikipedia.org/wiki/Code_smell