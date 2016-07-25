---
title: JavaScript 倒计时
author: 陈 三
layout: post
date: 2013-02-01T14:32:29+00:00
url: /javascript-countdown.html
views:
  - 660
dsq_thread_id:
  - 1059186041
categories:
  - 前端开发
tags:
  - JavaScript

---
最近经常用 JavaScript 写倒计时程序，略为整理：

    function countdown(){// 先定义函数 countdown
        var endTime = (new Date(2013,1,10)).getTime();
        //使用 getTime 函数取得2013.2.10的时间数值，JavaScript 中的时间数值是以1970.1.1当天起算的，以毫秒为单位。另外需要特别注意的是，传递给 Date 的月份是从0开始算起的，0表示1月份，11表示12月份
        var now = (new Date()).getTime();//取得当前时间
        var dhms = endTime - now;
        var dd = Math.floor(dhms/3600/24/1000);// 计算天数
        var hms = dhms-(dd*24*3600*1000);// 扣除天数后所剩下的时间，单位毫秒
        var hh = Math.floor(hms/3600/1000);// 计算小时数
        var ms = hms-(hh*3600*1000);// 扣除天数、小时后剩下的时间，单位毫秒
        var mm = Math.floor(ms/60/1000);// 计算分钟数
        var s = ms-(mm*60*1000);// 扣除天数、小时、分钟后剩下的时间，单位毫秒
        var ss = Math.floor(s/1000);// 计算秒数
        if (hh < 10){hh = "0" + hh;} // 如果小时数小于10,在左侧补充一个 "0"，保证两位数，下同
        if (mm < 10){mm = "0" + mm;}
        if (ss < 10){ss = "0" + ss;}
        var output = "倒计时：" + dd + "天" + hh +"小时" + mm +"分钟" + ss + "秒";
        document.getElementById('countdown').innerHTML = output; // 将文档中 ID 为 "countdown" 的元素内容替换成 output
        setTimeout(function(){countdown();},1000);// 1秒后调用自己
    }
    

在定义函数后，就可以在脚本中调用：

        countdown();
    

见 [jsfiddle][1] 的效果。

另一种更简单的，比如从当下开始倒计时：

    function countDown(t){ // t 为秒数
     if (t > 0) {
        $('.js-countDown').text(t);
        setTimeout(function(){countDown(t-1);}, 1000);
      }
    }
    countDown(10); // 倒数10秒
    

## 扩展阅读

  1. [getTime][2] 
  2. [Date][3]

 [1]: http://jsfiddle.net/chenxsan/sUrLj/1
 [2]: https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Date/getTime
 [3]: https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Date