---
title: 'ERROR:  While executing gem … (Gem::RemoteFetcher::FetchError)'
author: 陈 三
layout: post
date: 2015-05-19T14:11:02+00:00
url: /error-while-executing-gem-gem-remote-fetch-error.html
views:
  - 2622
categories:
  - 前端开发
tags:
  - Gem
  - ruby

---
我对命令行下安装 gem 包或是 npm 包有很大的心理阴影，因为出现无法​安装的概率实在太大了 &#8211; 每次都要破口大骂 gfw。

这一回是在更新 gem 时：

    gem update --system
    

返回的错误如下：

> ERROR: While executing gem &#8230; (Gem::RemoteFetcher::FetchError)
> 
> Errno::ETIMEDOUT: Operation timed out &#8211; connect(2) for &#8220;s3.amazonaws.com&#8221; port 443 (https://api.rubygems.org/specs.4.8.gz)

出现 s3 的地址是因为此前 https://rubygems.org 源地址不行，所以执行了 `gem source` 添加源库：

    gem source --add https://s3.amazonaws.com/production.s3.rubygems.org/
    

如你所见，还是报错。

查了资料，不巧 [StackOverflow 上这个问题提到了 Proxy][1]，我国的国情，不挂代理简直混不下去 IT 业，所以我的 Mac OSX 的代理环境是这样的：

    privoxy(http://localhost:8118) -> sslEdge(http://localhost:100010)全局
    

Privoxy 我是用来去除一些广告。且把死马当活马医吧：

    export http_proxy=http://localhost:8118
    export https_proxy=http://localhost:8118 
    gem update --system
    

然后目瞪口呆：

    Updating rubygems-update
    Fetching: rubygems-update-2.4.7.gem (100%)
    Successfully installed rubygems-update-2.4.7
    Parsing documentation for rubygems-update-2.4.7
    Installing ri documentation for rubygems-update-2.4.7
    Installing darkfish documentation for rubygems-update-2.4.7
    Done installing documentation for rubygems-update after 2 seconds
    Installing RubyGems 2.4.7
    RubyGems 2.4.7 installed
    Parsing documentation for rubygems-2.4.7
    Installing ri documentation for rubygems-2.4.7
    

竟然真是代理的问题。所以我猜想是 iterm2 不支持 socks 代理，因此全局并未生效。而通过 Privoxy 的 HTTP 代理做一次转发，就正常了 &#8211; 所以，还是 gfw 的问题。

 [1]: http://stackoverflow.com/a/11128293