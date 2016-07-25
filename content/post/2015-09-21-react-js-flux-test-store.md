---
title: react.js 里测试 flux 架构的 store
author: 陈 三
layout: post
date: 2015-09-21T12:55:26+00:00
url: /react-js-flux-test-store.html
views:
  - 895
categories:
  - 前端开发
tags:
  - flux
  - react.js

---
在 [flux 架构][1]​的 react.js 项目里，我写过 component 的测试，略为无趣；但 store 的测试则相对有趣多了。

​想想，一个 action 分发后，store 就会相应做出变化，就好像你跟喜欢的人​​表白，保证能得到 yes 的回应似的 &#8211; 让人欣喜。

我们要用到的测试框架不是 [Mocha][2]，不是 [Jasmine][3]，而是 facebook 出品的基于 Jasmine 的 [jest][4]，据 react.js 官方说，他们都用这个测试，不过我敢保证，你一定会遇上各种问题。

且把这些担忧放到一边，来看一个简单的 [react.js 项目][5]，源码托管在 [github][6]。

它只有一个输入框，

  1. 输入内容并回车
  2. 触发一个 action
  3. 这个 action 继而触发了 store 里的回调
  4. 回调修改了 store 中的 model 数据
  5. store 射出事件
  6. 监听 store 的 view 重新读取 store 中的数据、设置 state、重新 render 组件

这是 flux 原始实现的整个流程。

因为 store 中的操作都是同步的，所以测试就非常便捷了。

但使用 jest 有几个注意事项：

  1. 最好使用 node.js 4.x.x
  2. 如果你要用 es6 写法，需要使用 [babel-jest][7] 一类预处理器
  3. 如果用 es6 写法，要测试的 store 不能使用 `import`，而必须使用 `require`，因为 `import` [会被置前][8]，导致 `jest.dontMock` 失效

来看测试代码：

    jest.dontMock('object-assign')
    jest.dontMock('../src/stores/Todo')
    
    describe('TodoStore', () => {
      let AppDispatcher
      let TodoStore
      let callback
    
      // mock actions
      let actionNewTodo = {
        type: 'NEW_TODO',
        todo: 'hello world'
      }
    
      beforeEach(() => {
        AppDispatcher = require('../src/dispatcher/AppDispatcher')
        TodoStore = require('../src/stores/Todo')
        callback = AppDispatcher.register.mock.calls[0][0]
      })
    
      it('registers a callback with the dispatcher', () => {
        expect(AppDispatcher.register.mock.calls.length).toBe(1)
      })
    
      it('初始化时为空', () => {
        expect(TodoStore.getTodos()).toEqual([])
      })
    
      it('创建一个新的 todo', () => {
        callback(actionNewTodo)
        expect(TodoStore.getTodos().length).toBe(1)
        expect(TodoStore.getTodos()[0]).toEqual('hello world')
      })
    })
    

`callback = AppDispatcher.register.mock.calls[0][0]` 是一个黑魔法，它能够执行我们的 action，而 store 将会相应地变化，就如上面的代码中：

  1. 初始化时 `TodoStore.getTodos()` 返回一个空数组
  2. 在执行 `callback(actionNewTodo)` 后，TodoStore 里插入了 `'hello world'`，我们就能预计它的长度为 1，且第一条数据是 `'hello world'`

在命令行下跑 `npm test`，就能看到 &#8220;1 test passed&#8221; 的字眼了。

真是让人感动：我们前端终于有机会写单元测试，并且还十分轻松。

## 扩展阅读

[Flux | Application Architecture for Building User Interfaces][9]

 [1]: https://facebook.github.io/flux/
 [2]: http://mochajs.org/
 [3]: http://jasmine.github.io/
 [4]: https://github.com/facebook/jest
 [5]: https://www.zfanw.com/react/demo-store-test/
 [6]: https://github.com/chenxsan/demo-jest-test-flux-store/blob/master/__tests__/TodoStore.test.js
 [7]: https://github.com/babel/babel-jest
 [8]: https://github.com/babel/babel-jest/issues/16#issuecomment-104063719
 [9]: https://facebook.github.io/flux/docs/testing-flux-applications.html