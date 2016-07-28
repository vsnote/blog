---
title: redux.js 的盛行
author: 陈 三
layout: post
date: 2016-06-01T02:35:36+00:00
url: /redux-js-prevail.html
views:
  - 339
categories:
  - 前端开发
tags:
  - react.js
  - redux

---
在 react.js 里，如果把一个组件写在另一个组件的 `render` 方法里，则其它组件要用它的话，我们又要重复一遍代码。所以我们要抽取它，独立成一个组件。可是，这时它的 `state` 应该放在哪里？

如果我们把 `state` 放在组件内部，则父组件有读取子组件数据的需求时，父组件内部就要创建一个变量，还要提供给子组件一个回调，这样，同样的 `state` 我们会在父、子两个地方实现，则不如 `state` 只定义在父组件中，通过 `props` 传递给子组件，这样，子组件的功能就比较单一，便于复用。

但是，又有一个新的问题产生。举一个 Email 组件来说，它可能在登录表单组件里使用，也可能在注册表单组件里使用，这两个父组件的逻辑是不一样的，无法复用，而它们在使用 Email 组件时，却都需要提供给 Email 组件一个变量及一个回调函数 &#8211; 它们在两个父组件中显然又是重复的。

比如我的一个使用 [mobx][1] 的注册组件：

    import React, { Component } from 'react'
    import { observable, action, computed } from 'mobx'
    import Email from '../common/Email'
    
    @observer
    class Register extends Component {
      @observable email = ''
      @computed get emailError () {
        if (this.email.trim() === '') {
          return '请填写邮箱地址'
        }
        if (!emailRegExp.test(this.email.trim())) {
          return '请填写正确的邮箱地址'
        }
        return ''
      }
      render () {
        return (
          <div>
              <Email email={this.email}
                changeEmail={this.changeEmail}
                emailError={this.emailError}
                />
          </div>
      }
    }
    

在登录组件中，几乎一模一样的代码，我又要重复一遍。

Don&#8217;t repeat yourself 说起来当然是简单，但做起来并不容易。就说我们上面所做的演进，目的是满足需求的同时消除重复，但结果我们只是把 repeat 从一个地方迁移到了另一个地方。

[Redux][2] 能解决我们的问题：

  1. 将父组件中重复的变量存储到 store 中
  2. 回调函数拆为 reducer + action

这样，我们就不必在多个父组件里重复变量及回调函数。但是，因为我们把变量存储在 store 里，把回调函数拆为 reducer + action，则我们在使用时，就又多了一个读取过程，在 redux.js 里，这通过 [react-redux][3] 实现。

当然，像 redux 这样提取父组件中重复变量然后复用的做法并不能满足所有需求。很多时候，我们确实需要两份数据，这时，redux [也没有][4]好的[解决办法][5]，因为 action 没法复用，reducer 也没法复用。

在 redux 的定义里，组件有两种：

  1. Container component
  2. Presentational component

上面的例子里，Email 组件是 Presentational component，要做到它的复用十分容易，而登录或注册组件则属于 Container component，它们的复用性就非常低，代码上的重复也很难避免 &#8211; 目前我还没看到较好的解决办法。

如果你有，欢迎留言：）

 [1]: https://github.com/mobxjs/mobx
 [2]: http://redux.js.org/index.html
 [3]: https://github.com/reactjs/react-redux/blob/master/docs/api.md#api
 [4]: https://github.com/reactjs/redux/issues/822#issuecomment-186614362
 [5]: https://github.com/reactjs/redux/issues/897#issuecomment-148233789