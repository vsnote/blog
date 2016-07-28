---
title: Mongoose populate 预填充字段
author: 陈 三
layout: post
date: 2016-05-10T12:14:00+00:00
url: /mongoose-populate.html
views:
  - 286
categories:
  - 后端开发
tags:
  - mongoose.js

---
举这个博客说，它有两个模型（model），`User` 和 `Post`。

一个 User 可以有多篇 Post，创建 Post 的时候，我们要存一个作者信息，假定是 `author` 字段，它的值指向用户的 `_id`。

    var mongoose = require('mongoose')
      , Schema = mongoose.Schema
    var userSchema = Schema({
      name: String
    })
    var postSchema = Schema({
      title: String,
      content: String,
      author: String
    })
    var User = mongoose.model('User', userSchema)
    var Post = mongoose.model('Post', postSchema)
    

以上是我还不知道 `populate` 时的写法，`Post` 模型里，`author` 指向了用户的 `_id`，这样，每次查询 post 都需要查询两个模型：

    Post.findOne({title: 'mongoose populate'}).then((doc) => {
      User.findOne({_id: doc.author}).then((user) => {
        return Object.assign({}, doc, {author: user})
      })
    })
    

但 mongoose 提供了 `populate` 方法，可以在查询时，预先填充字段：

    var mongoose = require('mongoose')
      , Schema = mongoose.Schema
    var userSchema = Schema({
      name: String
    })
    // 这里，我们给 author 定义了一个 `ref` 指向了 User 模型
    var postSchema = Schema({
      title: String,
      content: String,
      author: {
        type: mongoose.Schema.Types.ObjectId,
        ref: 'User'
      }
    })
    // `findOne` 勾子，在使用 `findOne` 时，mongoose 会预填充 `author` 字段的数据
    postSchema.pre('findOne', function (next) {
      this.populate('author', 'name')
      next()
    })
    var User = mongoose.model('User', userSchema)
    var Post = mongoose.model('Post', postSchema)
    

我们的查询 post 语句可以写成这样：

    Post.findOne({title: 'mongoose populate'}).then((doc) => {
      return doc
    })
    

其中 `doc` 里的 `author` 是一个对象，包含一个 `_id` 和一个 `name`，非常便捷、简洁。

## 参考

  1. [Mongoose Query Population v4.4.16][1]

 [1]: http://mongoosejs.com/docs/populate.html