---
title: no matching action clause to process request
author: 陈 三
layout: post
date: 2016-06-08T03:15:58+00:00
excerpt: Phoenix framework 下如何过滤资源
url: /no-matching-action-clause-to-process-request.html
views:
  - 243
categories:
  - 后端开发
tags:
  - phoenix framework

---
本文基于 phoenix framework 1.1.4。

我在 phoenix 项目里，定义了这样一个函数，用来过滤用户：

      def index(conn, %{"email" => email, "codename" => codename}) do
        # ... get the user with the filters
      end
    

访问以下两个路径：

  1. http://localhost:4000/api/users?codename=Plator
  2. http://localhost:4000/api/users?email=chenxsan@example.com

均会报告以下错误：

> Phoenix.ActionClauseError at GET /api/users
> 
> bad request to IngressRun.UserController.index, no matching action clause to process request

但如果访问

    http://localhost:4000/api/users?email=chenxsan@example.com&codename=Plator
    

却是能正常响应的。

看[这篇][1]的意思，我有多少个过滤条件，过滤条件组合一下，我就要定义多少个 action &#8211; 并不现实，也很傻。

比较靠谱的做法是[这一篇][2]。不过它的示例里：

    Post
    |> where(^filters)
    |> Repo.all
    

在我的测试中，会报一个编译错误：

> cannot use ^filters outside of match clauses

换成以下形式就没问题：

    from(p in Post, where: ^filters) |> Repo.all
    

另外我好奇的是，为什么这种过滤资源的常用功能，许多框架都不集成，phoenix 里我没见到，express.js 里也没有。

 [1]: http://elixirforum.com/t/am-i-doing-this-right-pattern-matching-in-controller-methods/249/2
 [2]: https://medium.com/@kaisersly/filtering-from-params-in-phoenix-27b85b6b1354#.oebhg9kbm