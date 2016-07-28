---
title: CoffeeScript 里 setTimeout 写法
author: 陈 三
layout: post
date: 2014-04-05T17:27:39+00:00
url: /coffeescript-settimeout.html
views:
  - 572
categories:
  - 前端开发
tags:
  - CoffeeScript

---
CoffeeScript 中，要给一个函数传递参数并执行，可以用括号，也可以省略括号：

    run = (a, b) -> # 定义 run 函数
      // code hear
    
    run 1, 2 # 传递参数1、2给 run 函数并执行，省略了括号
    
    run(1, 2) # 传递参数1、2给 run 函数并执行，带括号
    

当然，你还可以将参数换行写，比如：

    run 1,
    2
    
    run 1
    , 2
    
    run(1,
    2)
    
    run(1
    , 2)
    

只要有带上逗号，你想怎么写都可以，CoffeeScript 的编译器都会识别出你的用意。

假如要在 CoffeeScript 定义一个 `setTimeout` 函数，可以这么写：

    setTimeout  ->
      console.log a, b
    , 1000
    

编译出的结果是：

    setTimeout(function() {
      return console.log(a, b);
    }, 1000);
    

还有一种可行的写法，是把第一个参数用括号包起来：

    setTimeout  (->
      console.log a, b
    ), 1000
    

这种写法要更明白。

不过最明白的，肯定是把函数定义在其他地方，然后给 setTimeout 传递函数名：

    func = ->
      console.log 'code'
    setTimeout(func, 1000)