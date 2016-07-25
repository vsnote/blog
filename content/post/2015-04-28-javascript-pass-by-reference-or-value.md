---
title: JavaScript 按值传递还是按引用传递
author: 陈 三
layout: post
date: 2015-04-28T12:00:27+00:00
url: /javascript-pass-by-reference-or-value.html
views:
  - 478
categories:
  - 前端开发
tags:
  - JavaScript

---
​今天下午碰到的一个 JavaScript 问题，着实让我大吃一惊。

    var obj = { age: 5 };
    
    function changeObj(o) {
      o = { age: 6 };
    }
    
    changeObj(obj);
    
    console.log(obj.age);
    

上面 log 出的结果是 **5**。

再看另一段代码：

    var obj = { age: 5 };
    
    function changeObj(o) {
      o.age = 6;
    }
    
    changeObj(obj);
    
    console.log(obj.age);
    

这段代码 log 出来是 **6**。

我们可以确定的一点是，函数的参数如果是原始类型，则它们是按值传递的，比如传递字符串、数值，函数会对它们的值做一个拷贝，函数内部对参数的修改不会影响传递给函数的变量。

但上面两段代码的参数是对象。

JavaScript 权威指南一书里有一段：

> A function can use the reference to modify properties of the object or elements of the array. But if the function overwrites the reference with a reference to a new object or array, that modification is not visible outside of the function.

[StackOverflow][1] 上同样一大段讨论。

跟一个[前同事][2]聊了下，大致可以这样理解：

  1. 第一段代码中，`o` 是函数内的一个变量 &#8211; 确实，我们未曾显式声明，但因为它是函数的参数，所以默认在函数内声明了该变量[^15694.1]。变量 `o` 是函数外对象 `obj` 的一个引用，之后我们在函数内部把 `o` 的引用指向一个新的对象字面量 `{ age: 6 }`，所以函数作用域外的 `obj` 就没有受到影响。

  2. 而第二段代码中，我们对 `obj` 的一个引用直接修改属性，所以就影响到函数作用域外的 `obj` 本身了。

[^15694.1]:    
    [JavaScript 局部变量与参数][3]

 [1]: http://stackoverflow.com/questions/518000/is-javascript-a-pass-by-reference-or-pass-by-value-language
 [2]: http://doller.io/
 [3]: http://stackoverflow.com/questions/3057737/local-variable-vs-parameter