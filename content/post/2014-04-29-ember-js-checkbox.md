---
title: Ember.js复选框
author: 陈 三
layout: post
date: 2014-04-28T22:30:49+00:00
url: /ember-js-checkbox.html
views:
  - 562
categories:
  - 前端开发
tags:
  - ember.js

---
Ember.js提供的内建的视图(view)里包括了复选框(checkbox)[^12510.1]。我们可以按照它的教程中的示例使用：

    <label>
      {{view Ember.Checkbox checked=model.isDone}}
      {{model.title}}
    </label>
    

但还有一种写法：

    {{input type="checkbox" checked=isDone}}
    

但不管哪种用法，checked 的值都与控制器属性或模型属性做了双向绑定，所以，根据复选框的勾选情况，isDone 的取值有两个：

  1. true
  2. false

取值结果可以通过`get`方法取得：

    this.get('isDone');
    

结果的类型是布尔值。但经由HTTP请求传递后，PHP后端取得的数据类型会变成字符串型，这点需要稍加注意。

[^12510.1]:    
    [Ember.js &#8211; Views: Built-in Views][1]

 [1]: http://emberjs.com/guides/views/built-in-views/