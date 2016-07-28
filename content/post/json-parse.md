---
title: JSON 解析
author: 陈 三
layout: post
date: 2013-12-24T12:24:54+00:00
url: /json-parse.html
views:
  - 694
categories:
  - 前端开发
tags:
  - jQuery
  - JSON

---
Ajax 请求返回的 JSON 数据，通过 [JSON.parse][1] 或 jQuery 提供的 [parseJSON][2] 解析后，就可以当成 JavaScript 对象处理：

    $.get('http://www.example.com/json', function(data) {
        var response = JSON.parse(data);
        console.log(response.result);
    });
    

当然，事情要比上面这种说法复杂一些，这是由 HTTP 响应头的 Content-Type 值决定的。

比如我们的响应头里 Content-Type 如下：

    Content-Type: text/plain; charset=utf-8
    

那么，JSON.parse 或 jQuery.parseJSON 都可以并且应该使用，因为返回的是一个 JSON 字符串。

但当 Content-Type 是 `application/json;charset=utf-8` 时，情况就不一样了，因为返回值本身就是 JavaScript 对象，可以直接访问，这时如果使用 JSON.parse 解析反而是错误的。

还有一种常见的情况，返回的是 JSON 字符串，但 Content-Type 却是 text/html，需要预先使用 `eval` 将其转化为 JavaScript 对象：

    var response = eval("(" + data + ")");
    console.log(response.result);

 [1]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse
 [2]: http://api.jquery.com/jQuery.parseJSON/