---
title: Node.js 开发 Telegram bot
author: 陈 三
layout: post
date: 2016-02-27T14:16:36+00:00
url: /telegram-bot-with-nodejs.html
views:
  - 759
categories:
  - 前端开发
tags:
  - node.js
  - telegram

---
昨天 Ingress 厦门的 telegram 群里大家在逗机器人，于是自己也想开发一个玩。

首先，在 telegram 里找 [@BotFather][1] ，跟它对话，让它创建一个 bot，并且讨要一个 token，token 大概长这样：

    123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11
    

接下来，我们与 bot 对话，或是在带了 bot 玩的群里说话，bot 都能够读取到，它相当于中间的传话者，服务器与 bot 对话的方式有两种：

  1. [getUpdates][2] &#8211; 我们的服务器主动读取
    
    拿上面那个假 token 说，GET `https://api.telegram.org/bot123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11/getUpdates` 就可以得到数据。

  2. [setWebhook][3] &#8211; telegram bot 在得到消息后，会主动往我们通过 setWebhook 接口设定的服务器 url POST 数据。
    
    `setWebhook` 的用法是，在浏览器中访问 `https://api.telegram.org/bot123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11/setWebhook?url=https://example.org`，页面会返回结果：
    
    > {&#8220;ok&#8221;:true,&#8221;result&#8221;:true,&#8221;description&#8221;:&#8221;Webhook was set&#8221;}
    
    返回结果表示 Webhook 设定成功，之后 telegram 就会往 https://example.org 地址 POST 新数据。
    
    webhook 的地址必需是 https 的，telegram 文档中有提到证书 &#8211; 除非你的网站是自己签名的，否则可以不理会该参数。

另外，`getUpdates` 方法与 `setWebhook` 只能二选一，不能同时使用。

我用的 node.js 框架是 [hapi.js][4]，整个代码大致如下：

    const Hapi = require('hapi')
    const ajax = require('request')
    
    // Create a server with a host and port
    const server = new Hapi.Server()
    const token = require('./token')
    const api = `https://api.telegram.org/bot${token}/`
    
    server.connection({
      host: 'localhost',
      port: 8888
    })
    
    // Add the route
    server.route({
      method: 'GET',
      path: '/',
      handler: function (request, reply) {
        return reply('hello world')
      }
    })
    server.route({
      method: 'POST',
      path: '/' + token,
      handler: function (req, reply) {
        reply('done')
        const message = req.payload.message
        const chat_id = message.from.id
        ajax.post(api + 'sendMessage',
              {
                form: {chat_id: chat_id, text: message.text}
              }, (err, response, body) => {
                if (err) console.log(err)
                console.log('everything is ok: ', body)
              })
      }
    })
    
    // Start the server
    server.start((err) => {
      if (err) {
        throw err
      }
      console.log('Server running at:', server.info.uri)
    })
    

把代码上传到 vps 上，通过 [pm2][5] 启动，并配置 Apache，将[指定路由的流量全部转发给 node.js 服务器上][6]。

 [1]: https://telegram.me/botfather
 [2]: https://core.telegram.org/bots/api#getupdates
 [3]: https://core.telegram.org/bots/api#setwebhook
 [4]: http://hapijs.com/
 [5]: http://pm2.keymetrics.io/docs/usage/quick-start/
 [6]: https://www.zfanw.com/blog/apache-proxy-node-js.html