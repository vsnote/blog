---
title: JavaScript with 语句
author: 陈 三
layout: post
date: 2015-04-12T13:56:12+00:00
url: /javascript-with-statement.html
views:
  - 678
categories:
  - 前端开发
tags:
  - JavaScript

---
​[ECMAScript 5 里已经不推荐][1]使用 `with` 语句，一个主要原因是，它会产生莫名的副作用，比如：

    var obj = { a: 3 };
    
    with (obj) {
      a = 7;
      b = 5;
    }
    

这里，我们创建了一个全局变量 `b`。但一般我们会认为 `b` 是 `obj` 对象的属性 &#8211; 可惜不是，我们确实创建了一个全局变量。

我们知道全局变量是魔鬼，尤其是莫名产生的全局变量。所以 ECMAScript 5 里引入 `'use strict';`，解决这类问题。

如果我们在代码前加入 `'use strict';`：

    'use strict';
    var obj = { a: 3 };
    
    with (obj) {
      b = 5;
    }
    

运行后会报告这样的错误：

> SyntaxError: strict mode code may not contain &#8216;with&#8217; statements

严格模式下不允许使用 `with`。那就不用吧。

另一个不用 `with` 的原因是，它会[拖慢代码的运行速度][2]。通常，JavaScript 引擎会对要运行的 JavaScript 代码做许多优化，但 `with`（以及 `eval`）的引入会变成《海伯利安》这样的变数，导致引擎无法优化代码。

简单说，JavaScript 里不要用 `with` 了，现在，以后，都没什么必要。

 [1]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/with
 [2]: https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20&%20closures/ch2.md#performance