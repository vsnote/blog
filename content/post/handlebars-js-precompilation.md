---
title: Handlebars.js 预编译
author: 陈 三
layout: post
date: 2014-01-10T14:10:14+00:00
url: /handlebars-js-precompilation.html
views:
  - 2109
categories:
  - 前端开发
tags:
  - grunt.js
  - Handlebars.js

---
Handlebars.js 官网上对预编译[^11247.1]是这样说的：

  1. 你需要安装 Node.js
  2. 你需要在全局环境中，通过 Npm 安装 handlebars 包

然后你就可以通过命令预编译你的 handlebars 模板文件：

    $ handlebars <input> --output <output>
    

假设我有一个模板文件，名称为 person.handlebars，内容很简单，如下：

    <table>
        <tr>
            <td>This is {{firstname}} {{lastname}}</td>
        </tr>
    </table>
    

假定编译后输出文件的名称为 person.js[^11247.2]，检查 person.js 文件内容，可以看到，一个 Handlebars.templates 对象下增加了一个 `person` 属性名：

    var template = Handlebars.template, templates = Handlebars.templates = Handlebars.templates || {};
    templates['person'] = template(function (Handlebars,depth0,helpers,partials,data) {
        ......
    

之后，我们只要在页面 HTML 页面引用 handlebars.runtime.js、person.js 文件，并且通过 js 传入数据：

    <!doctype html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Handlebar.js 模板</title>
    </head>
    <body>
        <div id="person"></div>
        <script src="js/handlebars.runtime.js"></script>
        <script src="js/person.js"></script>
        <script>
            var compiledTemplate = Handlebars.templates['person'],
            html = compiledTemplate({"firstname": "三", "lastname": "陈"});
            document.getElementById('person').innerHTML = html;
        </script>
    </body>
    </html>
    

在浏览器打开 HTML 页面，可以看到最终结果：This is 三 陈。

OK，看完 Handlebars.js 官网提供的纯手工预编译模板的方法后，再来看看 Grunt.js 是怎样全自动预编译模板的。

## grunt-contrib-handlebars[^11247.3]

因为是基于 Grunt.js，所以假定环境中已经安装好 Node.js、Npm，`grunt` 命令也能正常运行。

首先，需要在工作目录下需要安装 `grunt-contrib-handlebars` 模块：

    $ cd myJob
    $ npm install grunt-contrib-handlebars --save-dev
    

安装完 grunt-contrib-handlebars 模块后，我们需要在 Gruntfile.js 文件中加载它：

    grunt.loadNpmTasks('grunt-contrib-handlebars');
    

然后，还是在 Gruntfile.js 文件中，配置预编译任务：

    handlebars: { //定义预编译任务
        compile: {
            options: {
                namespace: "JST" //命名空间，这个很重要，后面会提到
            },
            files: [{
                expand: true,
                cwd: 'js/src/handlebars',
                src: '**/*.handlebars', //模板文件
                dest: 'js/dest/handlebars/', //编译后的文件存放位置
                ext: '.js' //编译后的文件格式          
            }]
            //如果要把所有模板文件编译到一个 .js 文件，则可以写成：
            //files: {"js/dest/template.js": ['js/src/handlebars/**/*.handlebars']}
        }
    }
    watch: { //监控文件变化并自动执行预编译任务
        precompile: {
            files: 'js/src/handlebars/**/*.handlebars',
            tasks: ['handlebars']
        }
    }
    

这里，如果等不及 `grunt watch`，可以先执行 `grunt handlebars` 命令预编译，得到的 person.js [^11247.4]文件如下：

    this["JST"] = this["JST"] || {};
    
    this["JST"]["js/person.handlebars"] = Handlebars.template(function (Handlebars,depth0,helpers,partials,data) {
    this.compilerInfo = [4,'>= 1.0.0'];
    ......
    

这个版本跟手工生成的可不太一样。当然，如果想生成与手工一样的结果也很简单，只要把选项中的 `namespace` 设置为 `false`。

好了，现在我们的 `person` 存放的位置变了，不再是之前的 `templates['person']`，而是 `this["JST"]["js/person.handlebars"]`[^11247.5]，那么，在 HTML 里，我们的 `compiledTemplate` 是怎么获取？很简单：

    var compiledTemplate = JST["js/person.handlebars"],
    

这是因为，在 grunt-contrib-handlebars 自动预编译的文件中，`this` 在浏览器环境下指向 window 对象，所以我们不过是把模板对象存放到一个新的命名空间 JST 下的 &#8220;js/person.handlebars&#8221; 属性名里，结果是，代码冲突的可能性更小了。

[^11247.1]:    
    [Handlebars.js: Minimal Templating on Steroids][1]

[^11247.2]:    
    [Handlebars.js 预编译的结果][2]

[^11247.3]:    
    [gruntjs/grunt-contrib-handlebars][3]

[^11247.4]:    
    [Grunt 自动编译的 Handlebars.js 模板][4]

[^11247.5]:    
    [Pre-compile your Handlebars templates][5]

 [1]: http://handlebarsjs.com/precompilation.html
 [2]: https://gist.github.com/chenxsan/8351314#file-person-js
 [3]: https://github.com/gruntjs/grunt-contrib-handlebars
 [4]: https://gist.github.com/chenxsan/8352178
 [5]: http://danburzo.ro/grunt/chapters/handlebars/