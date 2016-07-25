---
title: jQuery 自定义事件
author: 陈 三
layout: post
date: 2014-01-24T16:08:15+00:00
excerpt: 使用 jQuery 自定义事件增加代码语义
url: /jquery-custom-event.html
views:
  - 1134
categories:
  - 前端开发
tags:
  - jQuery

---
在 jQuery 中，事件通常使用 `on` 来绑定：

    $('.js-submit').on('click', function() {
      // some code here
    });
    

除了 `click` 事件，我们还有其它可以绑定的事件，比如 `dblclick`、`blur`、`change`，等等。

但使用这些事件会有一个问题：语义不明。`click` 表示什么？它表示我单击了一个元素。但它也仅仅只是表示，一个**点击**事件在页面上发生，至于事件引发什么结果，就需要我们自己定义。

举一个例子。一个输入框，用于输入用户名，一个按钮，用于提交用户名给服务器：

    <input type='text' value='' id='username'>
    <input type='button' value='提交' class='js-submit'>
    

这里，我们假设有三种情况：

  1. 用户提交空值
  2. 用户提交的用户名不存在
  3. 用户提交的用户名存在

经典的 JavaScript 写法是这样的：

    $('.js-submit').on('click', function() {
      var username = $('#username').val();
      username = $.trim(username);
      if (username === '') {
        console.log('请不要留空');
      }
      $.post(url, {username: username}, function(data) {
        var res = data;
        if (res.retcode === -1) {
          console.log('用户名不存在');
        } else if (res.retcode === 0) {
          console.log('用户名存在');
        }
      });
    });
    

誰能说这段代码有问题呢？它可用，也很直观。

但是，如果我们要判断的情况增多了，则上面的写法就会变得非常丑陋。

jQuery 提供的自定义事件可以在代码中引入语义，辅助我们阅读。

以上面的例子说，我们假设有三种情况，在 jQuery 里，我们将它们定义为三种事件：

    $('.js-submit').on('click', function() {
      var username = $('#username').val();
      username = $.trim(username);
      if (username === '') {
        $(document).trigger('blank.username'); // 如果 username 为空值，则触发 blank.username 事件
      }
      $.post(url, {username: username}, function(data) {
        var res = data;
        if (res.retcode === -1) {
          $(document).trigger('notExist.username'); // 如果用户不存在，则触发 notExist.username 事件
        } else if (res.retcode === 0) {
          $(document).trigger('success.username'); // 如果用户存在，则触发 sucess.username 事件
        }
      });
    });
    
    //定义自定义事件
    $(document).on('blank.username', function() {
      console.log('请不要留空');
    });
    $(document).on('notExist.username', function() {
      console.log('用户名不存在');
    });
    $(document).on('success.username', function() {
      console.log('用户名存在');
    });