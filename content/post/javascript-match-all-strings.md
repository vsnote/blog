---
title: JavaScript 取得所有匹配字符串
author: 陈 三
layout: post
date: 2012-12-12T04:31:04+00:00
url: /javascript-match-all-strings.html
views:
  - 1015
dsq_thread_id:
  - 970075328
categories:
  - 前端开发
tags:
  - JavaScript

---
在 JavaScript 中，一段文本，如果要从中取得**所有匹配**某**正则**表达式的**字符串**，可以用正则对象(RegExp)的 exec 方法。

假设如下文本，将其赋值给变量 `str`：

    var str = "this is a long story. And we are so sorry.";
    

我们打算取得文本中所有以 s 开头 y 结尾的单词，即 story 与 sorry。

首先，写出能匹配这两个字符串的正则规则，`g` 表示将进行全局匹配：

    var re = /s[^\s]*y/g;
    

写[正则表达式的辅助工具][1]很多，目前我使用的是 <http://gskinner.com/RegExr/>。

然后执行 RegExp 对象的 exec 方法：

    var allStr = re.exec(str);
    

该表达式将在 `str` 文本中查找匹配 `re` 正则规则的所有字符串，并将其赋值给数组 `allStr`。

这个时候，如果检测 `allStr` 的长度值(length)，将会是1，也就是说 allStr[0] 有值，allStr[1] 的值却是 undefined。

而从我直观上理解，在执行 RegExp 对象的 exec 方法时，**JavaScript 应该取得所有匹配正则规则的字符串，并将其赋值给数组变量**。假如匹配字符串有两个，则数组变量 allStr 的长度值应该是2，而不是1。

可惜程序并不是按我这种直观运行。

要取得匹配的所有字符串，需要使用 while 循环，比如下列语句，将在浏览器窗口中显示所有匹配字符串：

        var str = "this is a long story. And we are so sorry.";
        var re = /s[^\s]*y/g;
        var allStr;
        while ((allStr = re.exec(str)) !== null){
            alert(allStr[0]);
         }
    

这里还有个小误区，也是我一直陷于其中的问题，就是我会在 while 循环外直接将正则的执行结果赋值给变量：

        ....
        ....
        var allStr=re.exec(str);
        while (allStr !== null) {
            alert(allStr[0]);
        }
    

这里，因为 allStr 的值不为 null，就造成判断语句 `allStr !== null` 一直为真，于是死循环，一直显示 「story」。而上一段代码是在每次循环中先赋值再判断。

## 参考

  1. [EXEC &#8211; JavaScript | MDN][2]

 [1]: http://www.dmoz.org/Computers/Programming/Languages/Regular_Expressions/Tools/
 [2]: https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/RegExp/exec