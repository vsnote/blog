---
title: NPM 安装目录问题
author: 陈 三
layout: post
date: 2013-01-04T10:00:08+00:00
url: /npm-install-current-location.html
views:
  - 940
dsq_thread_id:
  - 1007686506
categories:
  - 前端开发
tags:
  - Node
  - NPM

---
因为要安装 [Grunt-contrib-less][1] 用于 less 自动 compile 成 CSS，按其说明：

    npm install grunt-contrib-less
    

然后再到 grunt.js 文件中添加相应配置，然后在命令行运行命令，问题来了：

> Local Npm module &#8220;grunt-contrib-less&#8221; not found. Is it installed?

运行 `npm ls`，可以看到，grunt-contrib-less 安装到用户目录 /home/sam/ 下。而按 NPM 上的说明，如果不曾加参数 『-g』，是应该安装在当前目录下的。

`npm config ls` 查看其配置：

        ; cli configs
        registry = "https://registry.npmjs.org/"
    
        ; userconfig /home/sam/.npmrc
        https-proxy = "http://127.0.0.1:8118/"
        proxy = "http://127.0.0.1:8118/"
    
        ; node bin location = /usr/bin/nodejs
        ; cwd = /home/sam/tmp/
        ; HOME = /home/sam
        ; 'npm config ls -l' to show all defaults.
    

并无不妥的地方。

而且，无论我切换到哪个目录下按装 NPM 包，除非带上参数 『-g』，否则全部都安装后 「/home/sam/node_modules」 目录下。

解决办法是，在当前目录下创建一个 node_modules 目录：

    mkdir node_modules
    npm install grunt-contrib-less
    

然后就可以安装到当前目录下而非用户主目录下。

 [1]: https://npmjs.org/package/grunt-contrib-less