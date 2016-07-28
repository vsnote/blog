---
title: jQuery 动画 Promise
author: 陈 三
layout: post
date: 2015-04-06T05:17:25+00:00
excerpt: 用 Promise 接口写 jQuery 的动画代码
url: /jquery-animate-promise.html
views:
  - 643
categories:
  - 前端开发
tags:
  - jQuery
  - Promise

---
jQuery 的 `show`、`hide` 方法大家都好熟悉的，也知道它可以接受一个回调函数，用于动画完成后执行。比如：

    $('.js-sam').hide('slow', function() {
        alert('你刚刚隐藏了 sam');
    });
    

但是，jQuery 1.8 以后版本还提供了另一种书写风格，即 Promise &#8211; 这个中文翻译好难，目前看到有叫**承诺**的 &#8211; 我还是继续用 Promise 的叫法。譬如上面的示例代码，我们可以改成这样：

    var promiseMeHideSam = $('.js-sam').hide('slow').promise();
    
    function whenDone() {
        alert('你刚刚隐藏了 sam');
    }
    
    promiseMeHideSam.done(whenDone);
    

这里，`promise()` 方法未传递参数，则默认为 `fx`，表示动画效果。

[Promise][1] 比起回调（callback），有非常多好处，最明显的一个，我们可以把动画完成后要执行的所有回调动作解构。因为给 `hide` 函数传递回调的话，我们只能把所有动作写入该回调中，比如：

    $('.js-sam').hide('slow', function() {
    
      // 触发一
    
      // 触发二
    
      // 触发三
    
    });
    

但如果是 Promise 的写法：

    func1() {}
    func2() {}
    func3() {}
    promiseMehideSam.done(func1);
    promiseMehideSam.done(func2);
    promiseMehideSam.done(func3);
    

我们可以把三个触发结果分解到三个函数中，而不必写入一个庞大的回调函数里，一来不便维护代码，二来也不易阅读。

另外一种常见情形，比如我们要在动画 A 与动画 B 都结束后执行某个回调。如果照第一种传递回调函数的方法 &#8211; 就我所知，没法写。但 Promise 就可以：

    var animate1 = $('.js-sam').hide().promise();
    var animate2 = $('.js-hi').show().promise();
    
    function whenBothEnd() {
    
      // animate1 与 animate2 结束后执行
      console.log('动画全部结束');
    }
    
    $.when(animate1, animate2).done(whenBothEnd);
    

非常优雅。

 [1]: https://promisesaplus.com/