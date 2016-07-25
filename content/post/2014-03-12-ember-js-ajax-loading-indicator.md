---
title: Ember.js ajax 加载中效果
author: 陈 三
layout: post
date: 2014-03-11T22:16:46+00:00
excerpt: Ember.js 里如何给 「ajax 加载中」的状态添加视觉反馈
url: /ember-js-ajax-loading-indicator.html
views:
  - 511
categories:
  - 前端开发
tags:
  - ember.js

---
_Note：本文基于 Ember.js 1.4.0_

Ember.js 里，需要大量处理 ajax 请求，又因为是单页面应用，「ajax 正在加载」就更需要视觉上的反馈 &#8211; 否则用户会简单地认为他点击了却没有反应。

譬如我有这样一个页面：

    App.Router.map(function() {
      this.resource('user', function() {
        this.route('info');
      };
    };
    

从 `/user/index` 路由(点击链接)到 `/user/info`，info 页面需要处理大量 ajax 请求，请求由 `UserInfoRoute` 的 `model` 勾子发出，在 ajax 返回前，`user/info` 模板不会渲染，从视觉上说，就好像点击了链接却没有反应 &#8211; 但其实 ajax 正在加载中。

为了给用户视觉反馈，Ember.js 提供了 `loading` [^11794.1]事件勾子：

    App.UserInfoRoute = Ember.Route.extend({
      model: function() {
        //some promise here
        //return $.get('http://www.zfanw.com/blog/');
      },
      actions: {
        loading: function(transition, originRoute) {
          // 在这里，我可以提供一种 ajax 正在加载中的指示
        }
      }
    });
    

就我个人来说，我不十分喜欢上面的处理方法，因为每个你要进入的路由，需要视觉反馈的话，都要定义一个 `loading` 事件勾子。

Ember.js 还提供一个方法，默认的 `loading`。譬如上面的路由定义里，其实默认允许以下 `loading` 路由：

  1. user.loading
  2. loading

我只需要定义一个统一的 `user/loading` 模板：

    <script type='text/x-handlebars' data-template-name='user/loading'>
    // 把 ajax 加载中的效果样式定义在这里
    </script>
    

之后从 `/user/index` 路由到 `/user/info` 里，如果后者需要处理大量 ajax 数据而未能马上返回，Ember.js 会帮我们暂时切换到 `/user/loading` 中 &#8211; 这里就是我们定义的视觉反馈。ajax 请求数据返回后，我们就自动进入 `/user/info`。

[^11794.1]:    
    [Ember.js &#8211; Routing: Loading / Error Substates][1]

 [1]: http://emberjs.com/guides/routing/loading-and-error-substates/