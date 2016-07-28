---
title: Mustache 嵌套数组
author: 陈 三
layout: post
date: 2014-08-15T05:09:16+00:00
url: /mustache-nested-array.html
views:
  - 1081
categories:
  - 前端开发
tags:
  - Mustache.js

---
如果观察Mustache[^13336.1]模板的填充数据，会发现最深层的通常是一个对象，对象的`key`在mustache模板中占位，`value`值则显示在key所占的位置。

如下模板：

     * {{name}}
     * {{age}}
     * {{place}}
     * {{{place}}}
    

数据：

    {
      "name": "陈三",
      "place": "<b>福州平潭</b>"
    }
    

渲染结果：

     * 陈三
     *
     * &lt;b&gt;福州平潭&lt;/b&gt;
     * <b>福州平潭</b>
    

以上示例十分直观。但碰到value是数组时，Mustache模板就显得委婉。

它引入一个Section(块)的概念，从`{{#key}}`开始，以`{{/key}}`结尾。Section会根据value值的情况渲染出一个或多个Section中包含的代码。

如下模板：

    {{#person}}
      <p>{{name}}</p>
    {{/person}}
    

数据：

    {
      person: [
        "name": "陈三",
        "name": "陈四"
      ]
    }
    

渲染的结果会是：

    <p>陈三</p>
    <p>陈四</p>
    

但我们常常是根据数据来写模板的。

比如：

    {
      person: [
        "陈三",
        "陈四"
      ]
    }
    

这个数据里，value值是一个数组，数组中的单个组成并没有显式的`key`存在。这时，模板是这样写的：

    {{#person}}
      <p>{{.}}</p>
    {{/person}}
    

如果你用过Linux系统，会十分清楚，`.`号表示当前目录。模板中的`.`则表示数据的当前上下文环境，因为value是一个数组，所以Mustache模板在解析时会自动循环输出。

渲染的结果是：

    <p>陈三</p>
    <p>陈四</p>
    

再来看一组有嵌套的数据：

    {
      person: [
        {'lastName': '陈', firstName: ['三', '四']},
        {'lastName': '王', firstName: ['二']}
      ]
    }
    

我希望渲染的结果如下：

    <ul>
     <li>陈
       <ul>
         <li>三</li>
         <li>四</li>
       </ul>
     </li>
     <li>王
       <ul>
         <li>二</li>
       </ul>
     </li>
    <ul>
    

这个模板的写法如下：

    <ul>
    {{#person}}
      <li>{{lastName}}
        <ul>
          {{#firstName}}
            <li>{{.}}</li>
          {{/firstName}}
        </ul>
      </li>  
    {{/person}}
    </ul>
    

模板写成这样，我个人觉得，已经颇为失败。因为直观度降了很多，初学者不认真琢磨，恐怕不能一眼看明白。

另外，如果你想输出数组的索引(index)值，Mustache语法并不支持，Ractive.js[^13336.2]对其做了扩展，甚至支持输出`key`本身的值。

[^13336.1]:    
    [mustache.js][1]

[^13336.2]:    
    [Mustaches | Docs | Ractive.js][2]

 [1]: https://github.com/janl/mustache.js
 [2]: http://docs.ractivejs.org/latest/mustaches#index-references