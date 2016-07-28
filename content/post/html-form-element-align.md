---
title: HTML 表单元素对齐
author: 陈 三
layout: post
date: 2015-05-04T05:14:58+00:00
url: /html-form-element-align.html
views:
  - 1073
categories:
  - 前端开发
tags:
  - css
  - form

---
网页里，常见如下的表单代码：

    <div>
      <label for='email'>邮箱地址：</label>
      <input name='email' type='text'/>
    </div>
    <div>
      <label for='password'>密码：</label>
      <input name='password' type='text'/>
    </div>
    

通常，我们想达到下面这种排版效果：

<div class='u-textRight'>
  <label for='email'>邮箱地址：</label> <input name='email' type='text' />
</div>

<div class='u-textRight'>
  <label for='password'>密码：</label> <input name='password' type='text' />
</div>

Bootstrap 里是这么写[^15858.1]：

    <form class="form-horizontal">
      <div class="form-group">
        <label for="inputEmail3" class="col-sm-2 control-label">Email</label>
        <div class="col-sm-10">
          <input type="email" class="form-control" id="inputEmail3" placeholder="Email">
        </div>
      </div>
      <div class="form-group">
        <label for="inputPassword3" class="col-sm-2 control-label">Password</label>
        <div class="col-sm-10">
          <input type="password" class="form-control" id="inputPassword3" placeholder="Password">
        </div>
      </div>
    </form>
    

代码中用到了 grid，然后两个 `label` 设定同样的宽度，并且 `label` 内的文本右对齐。

但如果不考虑移动端的情况的话，我觉得可以这样写：

    <style>.u-textRight { text-align: right !important; }</style>
    
    <div class='u-textRight'>
      <label for='email'>邮箱地址：</label>
      <input name='email' type='text'/>
    </div>
    <div class='u-textRight'>
      <label for='password'>密码：</label>
      <input name='password' type='text'/>
    </div>
    

`label` 与 `input` 都是 inline 元素，我在它们的包含块上设定右对齐，这样不需要给 label 指定宽度，代码也更简洁。

效果如下：

<div class='u-textRight'>
  <label for='email'>邮箱地址：</label> <input name='email' type='text' />
</div>

<div class='u-textRight'>
  <label for='password'>密码：</label> <input name='password' type='text' />
</div>

[^15858.1]:    
    [Bootstrap horizontal form][1]

 [1]: http://getbootstrap.com/css/#forms-horizontal