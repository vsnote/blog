---
title: 搭建前端开发环境
author: 陈 三
layout: post
date: 2014-06-21T05:30:44+00:00
url: /front-end-development-env.html
views:
  - 876
categories:
  - 前端开发
tags:
  - grunt.js
  - node.js

---
如果用[Yeoman][1]创建前端的开发目录，运行:

    $ grunt serve
    

就可以通过`http://localhost:10000`这样的网址访问到开发根目录，

如果系统有Python 2.x，也可以搭建个简易的服务器。切换到开发目录，执行以下命令：

    $ python -m SimpleHTTPServer 10000
    

Python 3.x的命令如下：

    python -m http.server
    

之后，我们同样可以通过`http://localhost:10000`网址访问到开发根目录。

因为跟后端的开发不同步，所以后端数据通常需要在自己的电脑上模拟。

Node.js的框架[express.js][2]是个很方便的工具。

在安装完express.js后，创建一个目录，目录里新建`app.js`：

    var express = require('express');
    var app = express();
    
    app.use(function(req, res, next) { // 解决请求跨域
      res.setHeader('Access-Control-Allow-Origin', '*');
      next();
    });
    
    app.get('/', function(req, res) {
      res.send('hello express');
    });
    
    app.post('/login', function(req, res) {
      res.json({
        state: 1,
        info: null
      });
    });
    
    app.listen(3000);
    

然后运行`node app.js`，后端数据就可以通过`localhost:3000`接口访问到。代码中`app.use`部分用于解决端口不同造成的跨域禁止访问的问题。

 [1]: http://yeoman.io/
 [2]: http://expressjs.com