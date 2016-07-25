---
title: JavaScript 正则规则的匹配
author: 陈 三
layout: post
date: 2012-12-22T05:32:27+00:00
url: /javascript-string-match-regexp-exec.html
views:
  - 743
dsq_thread_id:
  - 987008591
categories:
  - 前端开发
tags:
  - JavaScript
  - 正则表达式

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#String_match"><span class="toc_number toc_depth_1">1</span> String 对象的 match 方法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#RegExp_exec"><span class="toc_number toc_depth_1">2</span> RegExp 对象的 exec 方法</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">3</span> 两种特殊情况</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    上一篇 <a href="http://www.zfanw.com/blog/javascript-match-all-strings.html">JavaScript 取得所有匹配字符串</a>中颇多遗漏，所以补一篇。
  </p>
  
  <p>
    在 JavaScript 中，取得匹配字符串主要有两种方法，一种是利用 String 对象的 match() 方法，一种是 RegExp 对象的 exec() 方法。
  </p>
  
  <p>
    预设一个文本变量 str:
  </p>
  
  <pre><code>var str = "this is a long story. And we are so sorry.";
</code></pre>
  
  <p>
    要取得 「story」 与 「sorry」。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="String_match">String 对象的 match 方法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyString_match" href="#String_match"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    代码如下，match 方法会返回一个数组，数组的每个元素都是匹配项，有 g 的话，会进行全局匹配，<code>alert</code> 命令显示 「story」 和 「sorry」；没有 g 的话，就只显示 「story」，即数组中只有一个元素。
  </p>
  
  <pre><code>//********代码1
var str = "this is a long story. And we are so sorry.";
var re = /s[^\s]+y/g;
var ss = str.match(re);
var i = 0;
while (i &lt; ss.length){
    alert(ss[i]);
    i++;
}
</code></pre>
  
  <p>
    但是，在没有全局匹配 g 这个 flag 的情况下，还有一种特殊情况，就是正则表达式中包括了用一对括号 () 括起来的子规则 &#8211; 更常见的说法可能是「<strong>分组</strong>」，
  </p>
  
  <pre><code>//********代码2
var str = "this is a long story. And we are so sorry.";
var re = /s([^\s]+)y/;//这个正则表达式中有一对括号
var ss = str.match(re);
var i = 0;
while (i &lt; ss.length){
    alert(ss[i]);
    i++;
}
</code></pre>
  
  <p>
    这里，<code>alert</code> 命令显示的结果是 「story」 与 「tor」，即 match 返回的数组中包含两个元素，一个是匹配的第一个字符串，一个是正则规则中括号中的子规则匹配的部分字符串。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="RegExp_exec">RegExp 对象的 exec 方法</span><a title="标题链接地址" class="u-floatRight hidden" id="heyRegExp_exec" href="#RegExp_exec"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    exec() 方法跟 String 对象的 match() 方法颇为接近，先来说正则规则中不带括号的情况：
  </p>
  
  <pre><code>//********代码3
var str = "this is a long story. And we are so sorry.";
var re = /s[^\s]+y/;
var ss = re.exec(str);//与 match() 方法对比，主要是改了这一行
var i = 0;
while (i &lt; ss.length){
    alert(ss[i]);
    i++;
}
</code></pre>
  
  <p>
    上述代码只显示 「story」。这很容易理解。
  </p>
  
  <p>
    但是，正则规则里即使使用全局匹配的标志 g，结果也是一样，浏览器里只弹出 「story」。这是与 String 对象的 match() 方法不同的地方。
  </p>
  
  <p>
    不过 g flag 也不是什么都没做，它会将正则对象 re 的 lastIndex 属性值设置为匹配字符串后一位位置值。比如上述代码匹配了 「story」，这个单词后一个字符为「.」，其在文本 str 中的位置为20，这样当 re 正则对象第二次被调用时，它将从 lastIndex 所指示的位置开始查找，如果没有找到匹配的字符串，就将 lastIndex 值设置为0 &#8211; 因为代码3中直接书写 <code>var ss = re.exec(str);</code>，这就导致正则对象只调用了一次 exec() 方法，也就取不到所有的匹配项。除非使用上一篇提到的办法：
  </p>
  
  <pre><code>//********代码4
var str = "this is a long story. And we are so sorry.";
var re = /s[^\s]+y/g;
var ss;
while ((ss = re.exec(str)) !== null){
    alert(ss[0]);
}
</code></pre>
  
  <p>
    这样，我们就捕捉到所有匹配的字符串 &#8211; 包括 「story」 和 「sorry」。
  </p>
  
  <p>
    对比两类方法，如果是匹配全部的字符串的话，String 对象的 match 方法显然要比 RegExp 对象的 exec 方法简便易懂多了。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">两种特殊情况</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    不管是 String 对象的 match 方法还是 RegExp 对象的 exec 方法，在没有 g 标志的情况下，正则表达式中如果使用括号 &#8211; 即含有子规则，它们的处理方法是一样的：都是一个数组，数组中第一个元素是匹配到的第一个字符串，然后是子规则匹配到的字符串。
  </p>
  
  <p>
    但如果全局匹配的情况下兼又含有子规则，则情况又有些不同。
  </p>
  
  <p>
    先说 RegExp 对象的 exec 方法：
  </p>
  
  <pre><code>//********代码5
var str = "this is a long story. And we are so sorry.";
var re = /s([^\s]+)y/g;
var ss;
while ((ss = re.exec(str)) !== null){
    alert(ss[0]);
    alert(ss[1]);
}
</code></pre>
  
  <p>
    上述代码会在浏览器窗口中弹出四个对话框，对话框内容分别是 「story」、「tor」、「sorry」、「orr」。即是说，每次执行 exec 方法时，都会返回一个带有两个元素的数组，一个为匹配的字符串，一个为子规则匹配的字符串。
  </p>
  
  <p>
    String 对象的 match 方法颇有点不同：
  </p>
  
  <pre><code>//********代码6
var str = "this is a long story. And we are so sorry.";
var re = /s([^\s]+)y/g;//这个正则表达式中有一对括号
var ss = str.match(re);
alert(ss.join("-"));
</code></pre>
  
  <p>
    因为我不知道 ss 这个返回的数组里到底是什么东西，就用数组的 join() 方法将其联合起来，结果是 「story-sorry」，没有任何 「tor」、「orr」 的东西，这里，括号所指示的子规则作用被忽视。
  </p>
</div>