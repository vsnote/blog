---
title: Avgrund Modal
author: 陈 三
layout: post
date: 2013-01-24T17:06:27+00:00
url: /avgrund-modal.html
views:
  - 657
dsq_thread_id:
  - 1044607865
categories:
  - 前端开发
tags:
  - jQuery

---
在 jQuery 系插件所提供的对话框中，jQuery UI 中提供的 [Dialog][1] 算是比较丑的，虽然功能比较齐全。

[Avgrund Modal][2] 从视觉上说，则胜出 jQuery UI 的 Dialog 许多，因为它使用 CSS3 的 `transform:scale()` 功能，在弹出对话框的同时，原页面缩小，视觉上有立体变化，而非像 jQuery UI 的 Dialog 那样平淡的弹出一个对话框。

它的用法也非常简单，

    $('element').avgrund();
    

你可以将其绑定给各种事件，比如单击、鼠标移过、移出等等。

也可以传递数据对象给 avgrund() 函数来自定义某些行为或表现：

    $('element').avgrund({          
        width: 380, // 最宽 640px
        height: 280, // 最高 350px
        showClose: false, // 设置为 true 可以启用 Close 按钮 
        showCloseText: '', // 关闭按键的文字
        closeByEscape: true, // 按 Esc 键关闭对话框
        closeByDocument: true, // 点击文档本身来关闭对话框
        holderClass: '', // lets you name custom class for popin holder..
        overlayClass: '', // ..and overlay block
        enableStackAnimation: false, // another animation type
        onBlurContainer: '', // enables blur filter for specified block
        openOnEvent: true, // set to 'false' to init on load
        setEvent: 'click', // use your event like 'mouseover', 'touchmove', etc.
        onLoad: function () { ... }, // set custom call before popin is inited..
        onUnload: function () { ... }, // ..and after it was closed 
        template: '对话框的内容写在这儿...' // or function() { ... }
    });
    

参数说明中提到它对弹出的对话框大小有限制，最宽640px，最高350px，但这个限制可以通过 avgrund.js 文件修改。

 [1]: http://api.jqueryui.com/dialog/
 [2]: http://labs.voronianski.com/jquery.avgrund.js/