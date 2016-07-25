---
title: webpack 与资源缓存
author: 陈 三
layout: post
date: 2015-09-11T16:11:23+00:00
url: /webpack-assets-cache.html
views:
  - 1190
categories:
  - 前端开发
tags:
  - webpack

---
你现在看到的这个网页，至少有三个 js 文件、一个 CSS 文件，还有一张图片。如果你是第一次访问这个页面，则至少要下载 200KB 大小的文件，耗时 6 秒多。

你的时间非常值钱。

所以浏览器提供了缓存功能，如果你是第二次访问这个页面，则很可能，你的浏览器只发送一个请求读取 HTML 页面，其它 js 文件、CSS 及图片都从本地的浏览器缓存中读取。缓存帮你节省了时间，也替你访问的网站节省流量。

简单说，浏览器缓存大概是这样的：

  1. 你第一次访问页面
  2. 页面的 HTTP 响应头中带有 **Cache-Control**，其中设定了资源（JS、CSS、图片等）的有效时间
  3. 有效期内，浏览器会直接从本地缓存中读取文件
  4. 资源失效
  5. 浏览器从远程服务器重新下载资源？？等等，如果远程服务器上的资源跟本地缓存中的还是一样，那我们完全没必要又下载一份一模一样的。其实，第 2 步中的响应头中其实还有一个 **ETag**，它表示资源的一个指纹。浏览器在资源失效后，会携带这个 Etag 去验证服务器上的资源情况，如果没有变化，则本地的资源有效时间重新设过，我们不必要重新下载一份；如果 Etag 变化了，浏览器才会下载一份新的资源缓存到本地
  6. 假如，缓存在浏览器本地的资源尚未过期，但远程服务器上，资源确实改变了，怎么办？
  7. 修改资源的路径，浏览器会重新读取、缓存资源

这第 7 步，正是 webpack 中可以轻易做到的。

我们在开发 React.js 时，有许多第三方库的代码，基本不会修改，比如 react、react-router 或 jQuery，这些代码，在部署的时候，可以打包成一个 vendor.[chunkhash].js 文件，这样用户第一次访问需要下载，第二次访问就可以读取浏览器缓存。

且看 webpack 的[缓存配置用法][1]：

    var path = require( 'path' )
    var webpack = require( 'webpack' )
    
    module.exports = {
      entry: {
        app: [
          './script/app'
        ],
        vendor: ['react', 'react-router', 'jquery']
      },
      output: {
        path: path.join( __dirname, '/dist' ),
        filename: '[name].[chunkhash].js'
      },
      plugins: [ new webpack.optimize.CommonChunkPlugin({ name: 'vendor' }) ]
    }
    

这样，运行 `webpack` 命令打包后，会生成 **vendors.46b0ed9caf9a53733d60.js** 这样的文件名，只要文件内容不变，chunkhash 部分就不会变，而文件内容一旦变化，chunkhash 就会变化。于是我们合理利用了浏览器的缓存功能，同时也保证缓存能够及时更新。

## 扩展阅读

  1. [HTTP caching — Web Fundamentals][2]

 [1]: http://webpack.github.io/docs/long-term-caching.html
 [2]: https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching?hl=en