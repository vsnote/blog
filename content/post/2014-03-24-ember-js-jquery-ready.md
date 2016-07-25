---
title: 'Ember.js 实现  jQuery ready 事件'
author: 陈 三
layout: post
date: 2014-03-24T12:24:09+00:00
excerpt: jQuery Ready 事件在 Ember.js 下怎么写
url: /ember-js-jquery-ready.html
views:
  - 641
categories:
  - 前端开发
tags:
  - ember.js

---
_Note：本文基于 Ember.js 1.4.0_

jQuery 下，要在 DOM 准备就绪后绑定事件，可以写在 ready [^11987.1]里：

    $( document ).ready(function() {
      // 事件绑定代码写在这里
    });
    

但 Ember.js 里我们不那么写，因为 jQuery 定义的 ready 触发时，也许 Ember.js 视图还没渲染完成，那个时候要给元素绑定事件，元素可能还不存在；你可能考虑用事件委托，但其实不必，因为 Ember.js 提供了一个更方便的事件：didInsertElement[^11987.2]。

> Called when the element of the view has been inserted into the DOM or after the view was re-rendered. Override this function to do any set up that requires an element in the document body.

「在视图层的元素插入 DOM 或视图重新渲染后触发」。

假定我们有一个模板，名称为 `user`：

    <script type="text/x-handlebars" data-template-name="user">
      <button class="js-submit">提交</button>
    </script>
    

我们希望在点击`提交`按钮后 alert 一个消息，则这样写：

    App.UserView = Ember.View.extend({
      didInsertElement: function(){
        $('.js-submit').on('click', function(){
          alert('我点击了提交按钮');
        });
      }
    });
    

这下我们就不需要担心绑定时 `.js-submit` 元素是不是存在 DOM 中。

[^11987.1]:    
    [.ready() | jQuery API Documentation][1]

[^11987.2]:    
    [Ember.js &#8211; Ember.View][2]

 [1]: http://api.jquery.com/ready/
 [2]: http://emberjs.com/api/classes/Ember.View.html#event_didInsertElement