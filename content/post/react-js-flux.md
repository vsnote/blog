---
title: React.js Flux 概念
author: 陈 三
layout: post
date: 2015-08-15T11:04:50+00:00
url: /react-js-flux.html
views:
  - 783
categories:
  - 前端开发
tags:
  - react.js

---
假设一个最简单的 todo 应用，它只有添加 todo 的功能：<div class=demo> <div id=main></div> </div> 

则应用 [flux 架构][1]的话，整个过程可以做如下描述：

  1. Todo 组件首先从 store 中读入所有的 todos 数据，并赋给 `state`，`render` 方法根据 `state` 的值渲染组件
  2. Todo 组件在 `componentDidMount` 中监听 store 中的数据变化，并传入一个回调，回调执行时，会重新设置组件的 `state`；另外我们还在 `componentWillUnmount` 中解除监听
  3. Todo 组件中，`新增` 按键触发了 `ADD_TODO` 的动作（action）
  4. store 中，监听 `ADD_TODO` 动作的回调接收到 `ADD_TODO` 的动作而执行，改变了 store 中 todos 数据，并 emit 出 `CHANGE` 事件
  5. Todo 组件监听到 store 数据变化，于是执行了重新设置组件 `state` 值的回调。因为 `state` 变化，于是组件又重新渲染

在 flux 的设计中，数据是单向流转的。从我们人脑角度说，非常容易理解。

 [1]: https://facebook.github.io/flux/docs/overview.html