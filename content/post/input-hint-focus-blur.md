---
title: jQuery 插件 – 显示/隐藏输入框提示
author: 陈 三
layout: post
date: 2013-08-08T13:09:18+00:00
excerpt: 一个简单的 jQuery 插件，用于输入框、文本域等提示文字的显示与隐藏。
url: /input-hint-focus-blur.html
dsq_thread_id:
  - 2009237582
views:
  - 871
categories:
  - 前端开发
tags:
  - jQuery
  - jQuery Plugin

---
目前，浏览器对 [`placeholder`][1] 支持还不普遍，所以输入框中要设置提示信息时，多数还是通过 JavaScript 方法，给 `focus`、`blur` 绑定事件。

我见过很多人是这样写的：

    <input type="text" onblur="if(this.value==''){this.value='请输入搜索信息...';}" onfocus="if(this.value=='请输入搜索信息...'){this.value='';}" value="请输入搜索信息..." name="q">
    

页面中需要设置提示信息的地方经常不止一个，如果每个都这样写，就会重复许多代码，并且容易出错。

以下是我写的一个简单 jQuery 插件，用于输入框中提示信息的显示/隐藏：

    /*===================================
    Module Name: hint
    聚焦时提示消息隐藏；
    blur 时显示隐藏信息;
    Author: 陈三
    Blog: http:www.zfanw.com/blog/
    Time: 2013.7.26
    version: 1.0
    Dependency: jQuery
    ==================================*/
    
    ;(function ($) {
    $.fn.hint = function () {
        this.each(function () {
            var el, old_txt;
            el = $(this);
            old_txt = el.val();
            el.on('focus', function () { //聚焦函数
                if (el.val() === old_txt) {
                    el.val('');
                }
                el.css('color','#000');//聚焦时设置文字颜色为黑
            });
            el.on('blur', function () { //blur 函数
                if (el.val() === '') {
                    el.val(old_txt);
                    el.css('color','');//blur时颜色恢复原有
                }
            });
        });
    return this;
    };
    }(jQuery));
    

在页面引入上述 jQuery 插件后，给每个要设置提示信息的元素添加 CSS 类，比如 `.js-hint`，

    <input class="js-hint" value="请输入提示信息">
    

<input class="js-hint" value="请输入提示信息" />

然后执行上述函数即可：

    $(function(){$('.js-hint').hint();});
    

随后要添加任何近似的元素均可，只要给元素添加 CSS 类 `.js-hint`：

    <textarea class="js-hint">请在这里输入文字...</textarea>
    

<textarea class="js-hint">请在这里输入文字&#8230;</textarea>

 [1]: http://www.w3.org/html/wg/drafts/html/master/forms.html#the-placeholder-attribute