---
title: Ember.js 模板预编译
author: 陈 三
layout: post
date: 2014-03-19T22:07:25+00:00
url: /ember-js-template-precompile.html
views:
  - 798
categories:
  - 前端开发
tags:
  - ember.js

---
_Note：本文基于 Ember.js 1.4.0_

Ember.js 里，如果把模板直接写在 index.html 文件里，你可以这样写：

    <script type="text/x-handlebars" data-template-name="application"> // 最顶级的模板
    ...
    {{outlet}} 
    </script>
    
    <script type="text/x-handlebars" data-template-name="index">
    ...
    </script>
    
    <script type="text/x-handlebars" data-template-name="user">
    ...
    {{outlet}}
    </script>
    
    <script type="text/x-handlebars" data-template-name="user/index">
    ...
    </script>
    

打开 index.html 网页时，Handlebars.js 会即时编译[^11923.16]模板内容。但你希望提高应用响应速度，则可以把模板文件分离出去，然后预编译。

我们建一个 templates 目录，专门放置 handlebars 模板。以上面的代码说，模板从主页面分离如下：

  1. application.hbs
  2. index.hbs
  3. user.hbs
  4. user/index.hbs 

需要注意！！，第四个 index.hbs 是放在 user 子目录下，.hbs 文件中也不需要 `<script>...</script>` 这样的标签，只需把 script 标签对之间的内容拷入 .hbs 文件。

预编译的工作可以交给 [grunt ember templates][1] ，相应的 Gruntfile.js 配置部分如下：

    emberTemplates: {
      compile: {
        options: {
          templateBasePath: 'app/templates/'
        },
        files: {
          'app/scripts/templates.js': 'app/templates/**/*.hbs' // 将 tempaltes 目录下所有的 hbs 文件一同编译到 scripts/templates.js 文件中
        }
      }
    },
    watch: {
      emberTemplates: {
        files: 'app/templates/**/*.hbs',
        tasks: ['emberTemplates']
      }
    }
    

命令行下运行 `grunt emberTemplates` 就可以预编译，之后在 index.html 文件中引用 templates.js 文件：

    <script type="text/javascript" src="scripts/templates.js"></script>
    

[^11923.16]:    
    [Handlebars.js 预编译][2]

 [1]: https://github.com/dgeb/grunt-ember-templates
 [2]: http://www.zfanw.com/blog/handlebars-js-precompilation.html