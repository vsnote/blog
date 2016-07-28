---
title: jQuery postJSON
author: 陈 三
layout: post
date: 2014-09-14T14:12:16+00:00
url: /jquery-postjson.html
views:
  - 801
categories:
  - 前端开发
tags:
  - jQuery

---
jQuery API 提供有 `getJSON` [^13473.1]方法，用于从服务端取回 JSON 数据，其实它只是 `ajax` 的封装：

    $.ajax({
      dataType: "json",
      url: url,
      data: data,
      success: success
    });
    

因为有 `getJSON` 存在，就让人好奇，是不是也有 `postJSON` 存在？结论是没有。

当然你可以模拟 `getJSON` 自己封装一个，但必要性不大。

通常，`getJSON` 是这样写的：

    var gettingBlogs = $.getJSON(url);
    gettingBlogs.done(function(data) {});
    

`POST` [^13473.2]可以写出类似的：

    var gettingBlogs = $.post(url, {page: 1, limit: 5}, null, 'json');
    gettingBlogs.done(function(data) {});
    

其中 `null` 位置本来是传一个 `success` 回调函数。因为我使用 `done` 这种 `promise` 的回调处理形式，所以传了 `null` 值。同时，我还传了 `'json'`，表示返回的数据格式是 json，这样的好处是回调函数中不需要再写：

    data = $.parseJSON(data);
    

这样的东西。语句本身不见得谁好谁坏，所以怎么写只是个人喜好。

[^13473.1]:    
    [jQuery.getJSON() | jQuery API Documentation][1]

[^13473.2]:    
    [jQuery.post() | jQuery API Documentation][2]

 [1]: http://api.jquery.com/jquery.getjson/
 [2]: http://api.jquery.com/jQuery.post/