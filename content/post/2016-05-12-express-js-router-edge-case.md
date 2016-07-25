---
title: Express 路由
author: 陈 三
layout: post
date: 2016-05-12T12:06:15+00:00
url: /express-js-router-edge-case.html
views:
  - 290
categories:
  - 后端开发
tags:
  - express.js

---
如果你的网站很小，又或者你不介意一个文件有成千上万行的代码，那大可以不必深入理解 express.js 的路由，只要知道 `app.get` 一类的简单用法就行：

    import express from 'express'
    const app = express()
    /**
     * @api {get} / 读取 xx
     */
    app.get('/', (req, res, next) => {})
    
    /**
     * @api {post} / 创建 xx
     */
    app.post('/', (req, res, next) => {})
    
    /**
     * @api {delete} /:id 删除 xx
     */
    app.delete('/:id', (req, res, next) => {})
    

只是事情远没那么简单。

比如上面的 `post` 与 `delete`，需要用户登录后才能执行，则你就需要一个检查用户是否已登录的方法，如果已经登录，则继续执行，否则重定向到登录页。

    /**
     * @function restrict 验证 session 中 token 是否存在
     */
    function restrict (req, res, next) {
      if (!req.session.token) {
        return res.redirect('/login')
      } else {
        next()
      }
    }
    app.post('/', restrict, (req, res, next) => {})
    

[app.METHOD][1] 的用法是这样的：

    app.METHOD(path, callback [, callback ...])
    

恰如前面的例子中所看到的，我们可以给 `app.post` 传递多个 callback，callback 会按顺序执行，除非前头排队执行的不调 `next()`。譬如上面的 `restrict`，在检查到 `token` 不存在后，它就直接 `return` 了，没有 `next()`，再后面的 callback 函数就不再执行。而在 `token` 存在的情况下，它执行了 `next()`，即继续下一个 callback。

在 [RESTful][2] 的规范里，我们的操作是围绕着资源（resources）的，比如这个博客，它有 posts 这个资源，针对它的增删改查（CRUD）在路由中体现为：

    /**
     * @api {get} /posts 读取所有博客
     */
    app.get('/posts', callback)
    
    /**
     * @api {post} /posts 创建博客
     */
    app.post('/posts', callback)
    
    /**
     * @api {get} /posts/:postID 读取 id 为 postID 值的博客
     */
    app.get('/posts/:postID', callback)
    
    /**
     * @api {patch} /posts/:postID 修改 id 为 postID 值的博客
     */
    app.patch('/posts/:postID', callback)
    
    /**
     * @api {delete} /posts/:postID 删除 id 为 postID 值的博客
     */
    app.delete('/posts/:postID', callback)
    

我们为什么要把 `/posts/:postID` 写上三遍甚至多遍？假如后期 URL 想做一点调整，我们就要改三次了。

我们可以使用 [app.route][3] 对上面的代码做一点改进：

    app.route('/posts')
      .get(callback)
      .post(callback)
    
    app.route('/posts/:postID')
      .get(callback)
      .patch(callback)
      .delete(callback)
    

但我的博客上并不仅仅 posts 这类资源，还有 comments 资源，还有 users 资源，于是，我们的路由会慢慢变成这样：

    app.route('/users')
      .all(restrict)
      .get(callback)
      .post(callback)
    
    app.route('/posts')
      .get(callback)
      .post(callback)
    
    app.route('/posts/:postID')
      .get(callback)
      .patch(callback)
      .delete(callback)
    
    app.route('/posts/:postID/comments')
      .get(callback)
      .post(callback)
    
    app.route('/posts/:postID/comments/:commentID')
      .get(callback)
      .patch(callback)
      .delete(callback)
    

想像一下，每个 `callback` 乐观点，假设能用 20 行代码解决，我们的这个路由文件也至少要上 500 行。假如再加上注释，则这个文件估计要有上千行。rMBP 下，14 号大小，编辑器一屏能显示 37 行。

分家的时候到了。

怎么分？

如果 `app.route` 肯接收第二个参数就好了，比如：

    app.route('/posts', callback)
    

这样我们就可以在单独的文件中定义 `/posts` 路径下所有处理逻辑，然后 `import` 进来给 `app.route` 调用。

但 `app.route` 只接收一个 `path` 参数。

这里，我们有两个问题要解决：

  1. 如何把 `app.route(path)` 后所附的各种逻辑独立到一个文件中
  2. 如何将独立文件中的处理逻辑与 url 匹配起来

第一个问题的解决办法是使用 [Router][4]，

    let router = express.Router()
    

这样我们就创建了一个 Router 对象，Router 是一个 mini 的 app，所以我们前面所写的 `app.METHOD` 的代码，Router 都可以同样使用：

    let router = express.Router()
    router.route('/')
      .all(restrict)
      .get(callback)
      .post(callback)
    export default router
    

这样我们就可以将某个 url 下对应的各种处理逻辑独立到一个文件里。

接下来解决第二个问题。

我们要用到 `app.use`，它的用法与我们想像的 `app.route` 的近似：

    app.use([path,] function [, function...])
    

我们首先将独立文件 `import` 进来，然后使用 `app.use` 将它与 url 匹配起来：

    import userRouter from './userRouter'
    app.use('/users', userRouter)
    

这样，app 里所有 `/users/*` 的请求都会进入 `userRouter` 这个 mini app 中处理。

但是我们要注意，`app.use('/users', userRouter)` 这样的写法下，userRouter 中要匹配 `/users` 路径，并不是下面这种写法：

    router.route('/users')
    

而是：

    router.route('/')
    

是的，我们的 url 路径现在分散了，一部分在入口文件中，一部分在 Router 文件中，如果我们切割得很厉害，则一个完整的 API 路径，会分散在多个文件中。假如代码不写注释，也不生成文档，则查阅 API 路径会非常麻烦。就我目前的经验，并没有一个很好的解决办法 &#8211; 除了文档中标注。

**说明**：以上代码均指 express.js 4.x 的 API。

 [1]: http://expressjs.com/en/api.html#app.METHOD
 [2]: https://en.wikipedia.org/wiki/Representational_state_transfer
 [3]: http://expressjs.com/en/api.html#app.route
 [4]: http://expressjs.com/en/api.html#router