---
title: JavaScript 里判断 null 与 undefined
author: 陈 三
layout: post
date: 2015-01-02T00:21:00+00:00
url: /javascript-reflect-null-undefined.html
views:
  - 582
categories:
  - 前端开发
tags:
  - JavaScript
  - 'null'
  - undefined

---
这里所说的判断，是指判断变量的值是否就是 null 或 undefined。

如[区别 null 与 undefined 一文][1]中所讲的，null 与 undefined 是它们所属类型的唯一一个值。所以判断方法非常方便，只要我们使用恒等比较（===）。

  * a 即 undefined
    
        var a;
        a === undefined;
        
    
    上面的代码将输出 `true`，即 a 为 `undefined`。

  * a 为 null
    
        var a = null;
        a === null;
        
    
    上面的代码将输出 `true`，即 a 是 `null`。

当然，恒等比较有一个前提，就是变量已经存在，如果变量尚未声明，引用未声明的变量会抛出错误。

    i === undefined;
    

以上代码执行后会抛出错误：

> ReferenceError: i is not defined

所以使用 `typeof` 来检查变量是否为 undefined 会更安全：

    typeof i === 'undefined'; // 如果 i 未声明，或 i 已声明但未赋值，结果为 true
    

但 `typeof` 检查变量值是否为 null 时，输出结果是 &#8220;object&#8221;，这个结论并不准确。以下方法才是对的且安全的：

    var a = null;
    Object.prototype.toString.call(a).slice(8, -1);
    

它会输出 `Null`，表示变量 a 的值是 `null`。

 [1]: http://www.zfanw.com/blog/javascript-difference-between-null-undefined.html