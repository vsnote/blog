---
title: 一个 react-native 下使用 redux 的错误
author: 陈 三
layout: post
date: 2016-06-17T08:15:47+00:00
url: /react-native-redux-expected-a-component-class-got-object-object.html
views:
  - 324
categories:
  - 前端开发
tags:
  - react-native
  - redux

---
我在 react-native 项目里写的 `index.ios.js` 文件如下：

    import React from 'react'
    import { AppRegistry } from 'react-native'
    import rn from './src/app'
    import { Provider } from 'react-redux'
    import configureStore from './src/store/configureStore'
    const store = configureStore()
    const App = () => {
      return (
        <Provider store={store}>
          <rn />
        </Provider>
        )
    }
    AppRegistry.registerComponent('rn', () => App)
    
    

运行时一直报告这个错误：

> Expected a component class, got [object Object].

`App` 当然是一个 Component，问题出在哪？

问题出在 `AppRegistry.registerComponent` 注册的组件名也叫 `rn`，而我在前头 `import` 了同样的一个 `rn`。

修改如下：

    import React from 'react'
    import { AppRegistry } from 'react-native'
    import Root from './src/app'
    import { Provider } from 'react-redux'
    import configureStore from './src/store/configureStore'
    const store = configureStore()
    const App = () => {
      return (
        <Provider store={store}>
          <Root />
        </Provider>
        )
    }
    AppRegistry.registerComponent('rn', () => App)
    

就不再有问题了。

一个非常简单却很容易忽略的错误。