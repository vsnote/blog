---
title: redux-saga 回调中执行 put
author: 陈 三
layout: post
date: 2016-06-11T08:05:11+00:00
url: /redux-saga-put-in-callback.html
views:
  - 244
categories:
  - 前端开发
tags:
  - redux
  - redux-saga

---
在 [redux-saga][1] 下，

    postWithLoadingEffect(API.user, user).then(
        (response) => {
          console.log(response)
          // yield put(userActions.setCurrentUser(response.data))
        }
      ).catch(
        (error) => {
          console.error(error)
        }
      )
    

`yield put` 放在回调中是不会执行的，因为回调函数并不是 generator 函数。

但这种需求在实际代码里会经常出现。我们可以绕个圈子实现它：

      try {
        let response = yield call(postWithLoadingEffect, API.user, user)
        if (response) {
          console.log(response)
          window.localStorage.setItem('authToken', response.meta.jwt)
          yield put(userActions.setCurrentUser(response.data))
        }
      } catch (error) {
        console.error(error)
      }
    

[call][2] 是 redux-saga 提供的一个 effect，它会执行传递给它的函数。这样我们就取得了结果，可以正常使用 `yield put`。

但很多时候，我觉得在 saga 中直接使用 `dispatch` 会更方便，只是这样 redux-saga 的好处便又丢了 &#8211; 不如回去写 redux-thunk。

 [1]: https://github.com/yelouafi/redux-saga
 [2]: https://yelouafi.github.io/redux-saga/docs/api/index.html#callfn-args