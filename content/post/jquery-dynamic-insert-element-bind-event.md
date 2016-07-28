---
title: jQuery 给动态插入的元素绑定事件
author: 陈 三
layout: post
date: 2013-01-08T06:17:15+00:00
url: /jquery-dynamic-insert-element-bind-event.html
views:
  - 1555
dsq_thread_id:
  - 1013857410
categories:
  - 前端开发
tags:
  - jQuery

---
这个误会可能有点深。

一般情况下，给 HTML 元素绑定事件方法如下：

    $('#sam').hover(
        function(){
            alert("hey it's sam.");
        }
    );
    

附：[jsfiddle][1]

这样当鼠标移动到文本上时，浏览器会弹出一个对话框。

但是，以上绑定的方法只能适用页面内已有的元素，如果 ID 为 sam 的 DIV 块是动态生成的，比如利用 `$().append()` 方法，则上面的绑定方法不会有结果。

必须把它绑定给 document 元素，并指向目标元素：

    $(document).on('mouseenter','#sam',function(){
        alert("hey it's sam.");
        });
    

这样，才能达到我们预期的效果。

另一个办法是使用 jQuery 提供的 delegate API &#8211; 这其实跟上述方法是同样的道理，将事件委托给父元素，然后由父元素绑定给子元素，

> $(&#8220;table&#8221;).delegate(&#8220;td&#8221;, &#8220;click&#8221;, function() { $(this).toggleClass(&#8220;chosen&#8221;); });

这样的好处是，我们不必要给每个子元素都注册事件，那样非常浪费，而且对动态插入的子元素也有效果。

又或者，在动态插入时就进行绑定。但这种办法并不优雅。

## 参考

  1. [api hover][2]
  2. [.on() | jQuery API Documentation][3]
  3. [.delegate()][4]

 [1]: http://jsfiddle.net/chenxsan/xtS8R/
 [2]: http://api.jquery.com/hover/
 [3]: http://api.jquery.com/on/
 [4]: http://api.jquery.com/delegate/