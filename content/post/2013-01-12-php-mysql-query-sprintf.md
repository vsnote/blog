---
title: PHP 中构建查询语句
author: 陈 三
layout: post
date: 2013-01-12T04:05:34+00:00
url: /php-mysql-query-sprintf.html
views:
  - 738
dsq_thread_id:
  - 1021252960
categories:
  - 未分类
tags:
  - MySQL
  - php
  - sprintf

---
如果是很直白的一条 SQL 查询语句：

    SELECT * FROM `SAM`;
    

这就没什么好说的。但是，更多时候需要从用户返回的变量中构建查询语句。比如，一个表单，提交给服务器上的 PHP 文件 `$_POST['when']`，`$_POST['why']` 两个变量。常见的构建查询语句方法如下：

    $sql = "SELECT * FROM `SAM` WHERE Reason ='" . $_POST['why'] . "' AND WHERE Time = '". $_POST['when'] . "'";
    

如果是上述写法，则不仅易出错，而且让人头大，也很难看出它表达了什么。

更快捷、直观的方法，是使用 sprintf() 函数：

    $sql = sprintf("SELECT * FROM `SAM` WHERE Reason = '%s' AND WHERE Time = '%s'",%_POST['why'],%_POST['when'];
    

这样我们就将变量从中区别开来，传递给 sprintf 函数的第一个参数即我们的 SQL 语句，只是用类似占位符的东西替代变量，这样的句子接近自然语言，很容易知道它是做什么，之后我们再将变量传入，函数将其替代后再返回字符串。

换一个角度说，其实许多模板语言比如 Smarty 也是接近这样的思路，把变量与结构区别开来，一来有助于理解，二来也便于修改。