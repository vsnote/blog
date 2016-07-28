---
title: JavaScript 里区别 null 与 undefined
author: 陈 三
layout: post
date: 2015-01-01T13:51:45+00:00
excerpt: JavaScript 代码中简单区分 null 和 undefined 两种类型
url: /javascript-difference-between-null-undefined.html
views:
  - 473
categories:
  - 前端开发
tags:
  - JavaScript
  - 'null'
  - undefined

---
`null` 与 `undefined` 是 JavaScript 的两个类型，类型的值如下：

| 类型        | 值               |
| --------- | --------------- |
| null      | 只有一个值 null      |
| undefined | 只有一个值 undefined |

`null` 表示变量取值为 `null` &#8211; 换句话说，取值即不是字符串也不是数字也不是真假值也不是对象。

`undefined` 表示变量已经声明，但未赋值，或赋值 `undefined`。

比如：

    var a; // 变量已声明，未赋值
    var b = undefined; // 变量已声明，则赋值 undefined
    a === b;
    

`a === b` 的输出结果是 `true`。

所以我们可以简单地区别它们：

  * undefined 表示没找到变量的值 &#8211; 找不到值
  * null 表示找到变量的值是 `null` &#8211; 找得到值