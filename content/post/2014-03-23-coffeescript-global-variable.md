---
title: CoffeeScript 全局变量
author: 陈 三
layout: post
date: 2014-03-23T14:11:08+00:00
url: /coffeescript-global-variable.html
views:
  - 876
categories:
  - 前端开发
tags:
  - CoffeeScript

---
CoffeeScript 下，没有全局变量，所有的代码封装到一个即时运行函数中，比如以下简单的一段代码：

    a = 5
    b = ->
      return 5
    

编译出来的 JavaScript 代码：

    (function() {
      var a, b;
    
      a = 5;
    
      b = function() {
        return 5;
      };
    }).call(this); // <- 定义一个匿名函数，并传入 `this` 这个上下文随即执行，a、b 都是局域变量
    

但我们可能有定义全局变量的需要，所以 CoffeeScript 还是提供了声明的方法，没有灭绝全局变量：

> If you&#8217;d like to create top-level variables for other scripts to use, attach them as properties on window, or on the exports object in CommonJS. The existential operator (covered below), gives you a reliable way to figure out where to add them; if you&#8217;re targeting both CommonJS and the browser: exports ? this

在浏览器环境下，你可以这样定义：

    window.foo = 'baz'
    

在 Node.js 环境下，你可以这样定义：

    exports.foo = 'baz'
    

为增强代码健壮性，两头都适用，你可以这样写：

    root = exports ? this
    root.foo = 'baz'
    

还有一种比较脏的写法，是用一对 \` 符号包起来的代码：

    `foo = 'baz'`
    

编译后的代码：

    (function() {
      foo = 'baz'; // <- foo 是全局变量
    }).call(this);
    

不过这种是我们尽量应该避免的，因为连 `var` 都没有加。