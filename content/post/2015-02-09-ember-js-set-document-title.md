---
title: Ember.js 设置页面标题
author: 陈 三
layout: post
date: 2015-02-09T12:34:43+00:00
url: /ember-js-set-document-title.html
views:
  - 495
categories:
  - 前端开发
tags:
  - ember.js

---
ember.js 原生代码中，没有根据路由[设置页面标题][1]的方法，但可以扩展。

使用 [ember-cli][2] 安装 [ember.js 原生代码中，没有根据路由[设置页面标题][1]的方法，但可以扩展。

使用 [ember-cli][2] 安装][3] ：

    $ ember install:npm ember-document-title
    

之后在代码中使用 `title` 即可：

    App.ApplicationRoute = Ember.Route.extend({
      title: "我的应用"
    });
    
    App.UsersRoute.extend({
      title: "用户"
    });
    

这样路由切换时，页面的标题就会自动变换。

 [1]: https://github.com/emberjs/ember.js/pull/3689
 [2]: http://www.ember-cli.com/
 [3]: https://github.com/paddle8/ember-document-title