---
title: jQuery 事件委托中的被委托者
author: 陈 三
layout: post
date: 2014-07-04T16:46:11+00:00
url: /jquery-delegate-event-delegatetarget.html
views:
  - 819
categories:
  - 前端开发
tags:
  - jQuery

---
jQuery 的事件委托[^13011.1]是个很有用的特性，适用动态插入的元素。

举个例子：

    $(document).on('click', '#tab > li', function(e){
      console.log($(this)); 
    });
    

上面的代码中，`this` 指向当前点击的 li 元素。

但偶尔，会有需要取得被委托者的必要，比如：

    $('#tab').on('click', '> li', function(e){
      // some code here
    });
    

用户单击 li 元素的时候，我想取得被委托者 `#tab` 对象的引用，这样我可以对它进行些样式上的处理。

以上代码中，可以很明显地取得，

    var delegated = $(this).parent('#tab');
    

但 jQuery 本身提供了一个语义化的对象，event.delegateTarget[^13011.2]，它指向事件绑定(被委托)的元素。

于是取得被委托者的代码可以这样写：

    var delegated = e.delegateTarget;
    

[^13011.1]:    
    [.delegate() | jQuery API Documentation][1]

[^13011.2]:    
    [event.delegateTarget | jQuery API Documentation][2]

 [1]: http://api.jquery.com/delegate/
 [2]: http://api.jquery.com/event.delegateTarget/