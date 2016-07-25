---
title: 错误分类
author: 陈 三
layout: post
date: 2016-06-09T08:41:15+00:00
url: /different-errors.html
views:
  - 157
categories:
  - 前端开发
tags:
  - react.js

---
​如果你在网页上看到错误提示，它们的来源大致有两种，一种来自前端，一种来自后端。

比如说有一个邮箱地址的输入框，用户试图提交空值，我们会报告一个前端上的错误：

> 请填写邮箱地址

在 react.js 里，这个错误是一个 [computed 值][1]（计算值 &#8211; 即依赖其它 state 计算出来的）：

    class Email extends React.Component {
      state = {
        email: ''
      }
      render () {
        const computedError = email.trim() === '' ? '请填写邮箱地址' : ''
        return <div>
          <input type='text' value={this.state.email}/>
          <span>{computedError}</span>
        </div>
    }
    

这是因为，`state` 多了，代码难以管理，所以有些数据我们要尽量从其它数据中推演，而不是新建一个。

但上面的示例里，email 地址提交到服务端，还可能返回一种错误：

> 该邮箱地址已经被人注册

这一种错误，并没办法通过 `email` 数据推演，我的做法是，新建一个 state 用来存储。不过这类表单数据多了，整个组件就会非常庞大，很容易出错。

 [1]: https://facebook.github.io/react/docs/interactivity-and-dynamic-uis.html#what-shouldnt-go-in-state