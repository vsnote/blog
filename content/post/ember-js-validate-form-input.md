---
title: Ember.js 表单验证
author: 陈 三
layout: post
date: 2014-03-02T04:22:50+00:00
excerpt: Ember.js 框架里怎么对表单元素提交的内容进行验证
url: /ember-js-validate-form-input.html
views:
  - 936
categories:
  - 前端开发
tags:
  - ember.js

---
_Note：本文基于 Ember.js 1.4.0_

Ember.js 里，一件事常常有多种做法。虽说灵活，但对新手来说，我认为反是件坏事，因为选择太多。

比如一个表单元素 input 输入框，用于用户注册时填写用户名，则据我了解到的资料，至少可有以下几种写法：

  * handlebars.js 模板[^11691.1]
    
        {{input type='text' placeholder="请输入用户名" value=username}}
        

  * Ember.TextField
    
    Ember.TextField 是 Ember.js 内建的一个 View 类[^11691.2]，
    
        //template
        {{view Ember.TextField valueBinding="username" placeholder="请输入用户名"}}
        

  * 扩展 Ember.TextField 类
    
        // js
        App.UsernameTextField = Ember.TextField.extend({}); 
        
        // template
        {{view App.UsernameTextField valueBinding="value" placeholder="请输入用户名"}}
        

**我的需求**很简单，对 input 里填写的用户名，发起 ajax 请求到服务器，验证该用户名是否可用。

**触发验证的时机**我选在输入框失焦时。在 Ember.js 里，该事件为 foucusOut。

一个最快的解决办法是，直接把事件绑定给 View 类的属性(下面一段代码基于上面的第三种写法)[^11691.3]：

    App.UsernameTextField = Ember.TextField.extend({
      focusOut: function(evt){
        var username = this.get('value'); // 注意，上面的模板中之所以写成 valueBinding='value' 是因为写成其他的话，本类中会无法取得 username 的值
        console.log(username);
        //这里我用 jQuery 发起 ajax 请求远程服务器进行表单验证
        $.post('http://www.example.com/api/user', {username: username}, function(response) {
          console.log(response);
        });
      }
    });
    

因为我们在模板里对 `value` 做了双向绑定[^11691.4]，所以 View 里可以通过 `this.get('value')` 取得当前输入框的值。这样，在输入框失去焦点后，就可以将取得的用户名通过 ajax 发送到服务器要求验证。

但我的实践里，上面这种做法虽快，但不方便。一个更灵活的方法是把表单验证过程写在控制器里(Controller)，这样可以直接在控制器修改程序状态值(Application state)，而不必在 View 里通过 `this.get('controller').send()` 这种方式。

模板部分如下[^11691.5]，样式基于 Twitter Bootstrap：

    <label for="username" class="col-sm-2 control-label">用户名</label>
    <div {{bind-attr class=":col-sm-10 usernameExist:has-error" }}>
      {{view Ember.TextField name='username' value=username type='text' class='form-control' title='请填写用户名' focus-out="validateUsername"}} <!-- 输入框失去焦点时触发 validateUsername 动作，动作定义在控制器中 -->
      <p {{bind-attr class=":text-muted usernameExist:hidden" }}>用来登录网站</p>
      <p {{bind-attr class=':text-error usernameExist::hidden' }}>该用户名已被人注册</p>
    </div>
    

控制器部分代码如下：

    App.RegisterController = Ember.Controller.extend({ // 注册页面 controller
        username: '',
        usernameExist: false,
        actions: {
            validateUsername: function() {
                var username = this.get('username'),
                    self = this;// 这个 this 指 controller
                if (username !== '') { // 如果输入框中内容不为空，则发起 POST 请求
                     $.post('http://www.example.com/user/register', {username: username}, function(response) {
                        var response = JSON.parse(response);
                        if ('feedback_negative' in response) { // feedback_negative 键名表示该用户名已经被注册
                            self.set('usernameExist', true); // 修改 usernameExist 值来影响模板中 CSS 类的显示与隐藏
                        }
                    });
                }
            }
        }
    });
    

这种方法里，我可以很方便地给 input 绑定各种事件[^11691.6]，并且模板代码十分直观 &#8211; 一眼就能看出某事件绑定了什么事件处理器。

[^11691.1]:    
    [Ember.js &#8211; Templates: Input Helpers][1]

[^11691.2]:    
    [Ember.js &#8211; Views: Built-in Views][2]

[^11691.3]:    
    [Ember.js 表单验证 &#8211; Demo][3]

[^11691.4]:    
    [Ember.js &#8211; Ember.Binding][4]

[^11691.5]:    
    [Ember.js &#8211; Templates: Binding Element Class Names][5]

[^11691.6]:    
    [Ember.js &#8211; Ember.View 事件名称清单][6]

 [1]: http://emberjs.com/guides/templates/input-helpers/
 [2]: http://emberjs.com/guides/views/built-in-views/
 [3]: http://jsbin.com/pahiwote
 [4]: http://emberjs.com/api/classes/Ember.Binding.html
 [5]: http://emberjs.com/guides/templates/binding-element-class-names/
 [6]: http://emberjs.com/api/classes/Ember.View.html#toc_event-names