---
title: Ember.js 里配置 BootStrap 的当前菜单
author: 陈 三
layout: post
date: 2015-02-09T14:23:49+00:00
url: /ember-js-bootstrap-navbar-current.html
views:
  - 620
categories:
  - 前端开发
tags:
  - ember.js

---
如果在 ember.js 里使用 bootstrap 的导航菜单（navbar），`.hbs` 的模板代码通常是这样的：

    <ul class="nav navbar-nav">
      <li>{{#link-to 'index' title='首页'}}首页{{/link-to}}</li>
      <li>{{#link-to 'login' title='登录'}}登录{{/link-to}}</li>
      <li>{{#link-to 'signup' title='注册'}}注册{{/link-to}}</li>
    </ul>
    

ember.js 1.10 里生成的 HTML 代码如下：

    <ul class="nav navbar-nav">
      <li><a title="首页" href="/" class="ember-view" id="ember313">首页</a></li>
      <li><a title="登录" href="/login" class="ember-view" id="ember314">登录</a></li>
      <li><a title="注册" href="/signup" class="ember-view active" id="ember315">注册</a></li>
    </ul>
    

如果我们点击`首页`，则 ember.js 会给该链接增加一个 `active` 类：

    <li><a title="首页" href="/" class="ember-view active" id="ember313">首页</a></li>
    

但是，bootstrap 的当前菜单的 `active` 类是添加在 `li` 元素上的，而不是 `a` 元素。

解决办法非常简单，直接把 `{{#link-to}}` 写到 `li` 上：

    {{#link-to 'index' tagName='li'}}
      <a title='首页' href='#'>首页</a>
    {{/link-to}}
    {{#link-to 'login' tagName='li'}}
      <a title='登录' href='#'>登录</a>
    {{/link-to}}
    {{#link-to 'signup' tagName='li'}}
      <a title='注册' href='#'>注册</a>
    {{/link-to}}
    

这样生成了 HTML 代码后，点击时 `active` 类会添加到 `li` 元素上，只是说 `a` 元素的 `href` 属性变成没有意义的 &#8216;#&#8217; 了。