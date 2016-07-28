---
title: 加载中
author: 陈 三
layout: post
date: 2016-06-06T01:43:29+00:00
excerpt: 开发时如何应用 loading 动画
url: /loading-indicator.html
views:
  - 204
categories:
  - 前端开发
tags:
  - Web Usability

---
在 app 上，我们经常见到“加载中”的图标。这是站在用户的角度看。如果切换到开发者角度，则会有一个疑惑，这个 loading 图标是即刻出现的吗？

如果 http 响应很快，则一闪而过的 loading 对用户来说，体验并不好。

可是，我们怎么知道一个响应是快还是慢？毕竟，网络的状况并不可控，一个响应在美国也许很快，在中国却异常的慢。

一个更友好的解决办法，可能是这样：

  1. http 请求发起
  2. 100ms 内响应，则不需要调出 loading
  3. 如果 100ms 内还未响应，则调出 loading

在 [nngroup 进度指示条一文里][1] ，作者提到一个参考时间：

> This indicator should be reserved for actions that take between 2-10 seconds. For anything that takes less than 1 second to load, it is distracting to use a looped animation, because users cannot keep up with what happened and might feel anxious about whatever flashed on the screen.
> 
> 如果 1s 内能响应，就不该用循环动画来指示进度，因为用户没法跟上，可能会对屏幕上一闪而过的东西感到焦虑。

所以上面的解决办法可以修改为：

  1. http 请求发起
  2. 10s 内响应，则不需要调出 loading
  3. 如果 10s 内未响应，则调出 loading

只是这里会有一个问题出现，如果 http 请求在 11s 时响应，则 loading 还是一闪而过。 &#8211; 在 web 的复杂环境下，这近于无解。

至于代码实现上，我们通常需要封装一个专用的 API 来处理 http 请求。

 [1]: https://www.nngroup.com/articles/progress-indicators/