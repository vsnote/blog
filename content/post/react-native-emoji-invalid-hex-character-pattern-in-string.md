---
title: React Native 下使用 emoji 的 Invalid hex-character pattern in string 问题
author: 陈 三
layout: post
date: 2016-05-07T08:32:23+00:00
url: /react-native-emoji-invalid-hex-character-pattern-in-string.html
views:
  - 279
categories:
  - 前端开发
tags:
  - react-native

---
我在 react native 项目里用到了 emoji，比如笑脸 😁，当然，我不是直接使用表情，而是使用了 unicode。😁 的 unicode 值是 `U+1F601`，在 react native 项目里，代码写成了：

    <Text>{"\u{1F601}"}</Text>
    

项目在模拟器下，或 `Debug` 模式下的设备上跑，都不会有问题，但是在 `Release` 模式下跑设备上，就会出现问题：

    Sat, 07 May 2016 07:02:29 GMT ReactNativePackager:SocketServer server got ipc message { type: 'createSocketServer',
      data: 
       { sockPath: '/var/folders/xk/y5j8r_dd0qg9ckymx96qd81c0000gn/T/react-packager-e36f208f7a835e0174b01026652af058',
         options: 
          { projectRoots: [Object],
            assetRoots: [Object],
            blacklistRE: [Object],
            transformModulePath: '/Users/sam/Documents/job/fz-app/node_modules/react-native/packager/transformer.js' } } }
    [3:02:30 PM] <START> Building Dependency Graph
    [3:02:30 PM] <START> Crawling File System
    Sat, 07 May 2016 07:02:30 GMT ReactNativePackager:SocketServer Process 45912 listening on socket path /var/folders/xk/y5j8r_dd0qg9ckymx96qd81c0000gn/T/react-packager-e36f208f7a835e0174b01026652af058 for server with options {"projectRoots":["/Users/sam/Documents/job/fz-app"],"assetRoots":["/Users/sam/Documents/job/fz-app"],"blacklistRE":{},"transformModulePath":"/Users/sam/Documents/job/fz-app/node_modules/react-native/packager/transformer.js","nonPersistent":true}
    Sat, 07 May 2016 07:02:30 GMT ReactNativePackager:SocketServer succesfully created server
    Sat, 07 May 2016 07:02:30 GMT ReactNativePackager:SocketServer connection to server 45912
    Sat, 07 May 2016 07:02:30 GMT ReactNativePackager:SocketServer got request { type: 'buildBundle',
      data: 
       { entryFile: 'index.ios.js',
         dev: false,
         minify: true,
         platform: 'ios' },
      id: 'xru0e36' }
    [3:02:30 PM] <START> find dependencies
    [3:02:36 PM] <END>   Crawling File System (6361ms)
    [3:02:36 PM] <START> Building in-memory fs for JavaScript
    [3:02:37 PM] <END>   Building in-memory fs for JavaScript (290ms)
    [3:02:37 PM] <START> Building in-memory fs for Assets
    [3:02:37 PM] <END>   Building in-memory fs for Assets (204ms)
    [3:02:37 PM] <START> Building Haste Map
    [3:02:37 PM] <START> Building (deprecated) Asset Map
    [3:02:37 PM] <END>   Building (deprecated) Asset Map (105ms)
    [3:02:37 PM] <END>   Building Haste Map (229ms)
    [3:02:37 PM] <END>   Building Dependency Graph (7105ms)
    [3:02:38 PM] <END>   find dependencies (7604ms)
    Sat, 07 May 2016 07:02:45 GMT ReactNativePackager:SocketServer request error { message: 'Invalid hex-character pattern in string',
      filename: 0,
      line: 39,
      col: 1,
      pos: 1704,
      stack: 'Error\n    at new JS_Parse_Error (eval at <anonymous> (/Users/sam/Documents/job/fz-app/node_modules/uglify-js/tools/node.js:22:1), <anonymous>:1526:18)\n    at js_error (eval at <anonymous> (/Users/sam/Documents/job/fz-app/node_modules/uglify-js/tools/node.js:22:1), <anonymous>:1534:11)\n    at parse_error (eval at <anonymous> (/Users/sam/Documents/job/fz-app/node_modules/uglify-js/tools/node.js:22:1), <anonymous>:1647:9)\n    at hex_bytes (eval at <anonymous> (/Users/sam/Documents/job/fz-app/node_modules/uglify-js/tools/node.js:22:1), <anonymous>:1704:17)\n    at read_escaped_char (eval at <anonymous> (/Users/sam/Documents/job/fz-app/node_modules/uglify-js/tools/node.js:22:1), <anonymous>:1688:49)\n    at eval (eval at <anonymous> (/Users/sam/Documents/job/fz-app/node_modules/uglify-js/tools/node.js:22:1), <anonymous>:1730:27)\n    at eval (eval at <anonymous> (/Users/sam/Documents/job/fz-app/node_modules/uglify-js/tools/node.js:22:1), <anonymous>:1870:24)\n    at Object.next_token [as input] (eval at <anonymous> (/Users/sam/Documents/job/fz-app/node_modules/uglify-js/tools/node.js:22:1), <anonymous>:1897:36)\n    at next (eval at <anonymous> (/Users/sam/Documents/job/fz-app/node_modules/uglify-js/tools/node.js:22:1), <anonymous>:2012:25)\n    at expect_token (eval at <anonymous> (/Users/sam/Documents/job/fz-app/node_modules/uglify-js/tools/node.js:22:1), <anonymous>:2045:20)' }
    Sat, 07 May 2016 07:02:45 GMT ReactNativePackager:SocketServer request finished error
    Worker Farm: Received message for unknown index for existing child. This should not happen!
    Sat, 07 May 2016 07:03:16 GMT ReactNativePackager:SocketServer server dying 45912
    Sat, 07 May 2016 07:03:16 GMT ReactNativePackager:SocketServer exit code: 0
    

重点在这一句：

    Sat, 07 May 2016 07:02:45 GMT ReactNativePackager:SocketServer request error { message: 'Invalid hex-character pattern in string',
    

为什么 `Debug` 模式下没有问题？这是因为 `Release` 模式下，会使用 uglifyjs 压缩代码，碰上 `\u{1F601}` 导致的。

解法有两个：

  1. 直接使用表情字符 😁
  2. 或者使用 [react-native-emoji][1] 这样的第三方库。

 [1]: https://github.com/jorilallo/react-native-emoji