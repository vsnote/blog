---
title: PhoenixFramework 部署注意事项
author: 陈 三
layout: post
date: 2016-07-13T03:00:06+00:00
url: /phoenixframework-deploy.html
views:
  - 66
categories:
  - 后端开发
tags:
  - elixir
  - PhoenixFramework

---
  1. 编译环境与生产环境[应该一致][1]，
    
    > We need to be sure that the architectures for both our build and hosting environments are the same, e.g. 64-bit Linux -> 64-bit Linux. If the architectures don&#8217;t match, our application might not run when deployed.
    
    比如我在 macOS 上编译的，放到 CentOS 7 上，就跑不起来了。最好在本地弄个与生产环境接近的虚拟机用于编译。

  2. 生产环境中一样需要安装 [Erlang][2] 与 [elixir][3]，
    
    用 [exrm][4] 编译不代表万事俱备，生产环境下，Erlang 与 elixir 都需要装一遍。但 PhoenixFramework 就不需要在生产环境中安装了，它只是开发使用。

 [1]: http://www.phoenixframework.org/docs/advanced-deployment
 [2]: https://www.erlang-solutions.com/resources/download.html
 [3]: http://elixir-lang.org/install.html
 [4]: https://hexdocs.pm/exrm/getting-started.html