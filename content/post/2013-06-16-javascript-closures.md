---
title: JavaScript 闭包
author: 陈 三
layout: post
date: 2013-06-16T14:49:35+00:00
url: /javascript-closures.html
dsq_thread_id:
  - 1405423021
views:
  - 934
categories:
  - 前端开发
tags:
  - JavaScript

---
JavaScript 中，变量 foo 的解析流程是这样：

  1. 检查当前函数作用域，是否有局域变量 foo；没有，下一步;
  2. 检查当前函数作用域，是否传入参数 foo；没有，下一步；
  3. 检查函数名称是否是 foo，如果不是，下一步；
  4. 到上一级函数作用域中，重复 1 &#8211; 4 步骤，一直到全局环境；
  5. 如果全局环境也没有变量 foo，则抛出错误 &#8220;ReferenceError: foo is not defined&#8221;。

You Don&#8217;t Know JS 里[比喻][1]说：

> 你现在站在大楼大堂，要找到一个叫 foo 的人，你得每一层每一个房间找过去，直到最顶层。

这跟闭包有什么关系？

有，简单说，闭包就是变量解析的一种看似特殊的情况。

举个例子：

    var a = 5
    function foo () {
      var a = 6
      console.log(a)
    }
    foo() // => 输出了 6
    

这个结果并不意外，因为 foo 本身是一个函数，函数天然是一个作用域，所以在解析 `a` 变量里，我们先从 foo 的作用域开始：里面有定义一个局域变量 a，并且值是 6。

来看个闭包的例子：

    var a = 5
    var foo = (function () {
      var a = 6
      return function () {
        console.log(a)
      }
    })()
    foo() // => 输出了 ??
    

如果对这个例子有疑惑，那就对了。我们在这里碰上了闭包。

上面的例子中，一个立即执行函数([IIFE][2])中返回了一个函数并赋给 foo，所以在我们执行 `foo()` 时，该立即执行函数已经结束，我们可能会认为 `var a = 6` 已经随着立即执行函数的结束而结束。

实际上，并没有。

Why?

JavaScript 虽然不是静态编译语言，但它在真正执行代码前，同样有一个编译的过程，只不过这个过程极为短暂。

而在这个编译过程中，它就提取代码中的所有声明，构建好所有的作用域。

拿上面的例子说，我们有三个作用域：

  1. 全局的作用域
    
      * 变量 a
      * 变量 foo

  2. 立即执行函数的作用域
    
      * 变量 a

  3. 立即执行函数中的匿名函数作用域
    
      * 无

这三个作用域的相互关系是：1 包含 2，2 包含 3。

变量 `foo` 指向的是立即执行函数中的匿名函数，因为有这个引用在，所以作用域 2 并没有被回收，于是解析变量 `a` 的顺序是：3 -> 2 -> 1。

因为我们在作用域 2 中找到了变量 a，所以 js 引擎就不再继续检索了。

结果是 6。

## 扩展阅读

  1. [Closures &#8211; JavaScript | MDN][3]
  2. [Why use &#8220;closure&#8221;? &#8211; How To Node &#8211; NodeJS][4]

 [1]: https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20&%20closures/ch1.md#building-on-metaphors
 [2]: https://en.wikipedia.org/wiki/Immediately-invoked_function_expression
 [3]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Closures
 [4]: http://howtonode.org/why-use-closure