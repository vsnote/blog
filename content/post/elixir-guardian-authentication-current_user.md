---
title: Elixir Guardian 库的 current_user
author: 陈 三
layout: post
date: 2016-05-22T04:50:32+00:00
excerpt: guardian 的会话管理如何取得 current_user 值。
url: /elixir-guardian-authentication-current_user.html
views:
  - 222
categories:
  - 后端开发
tags:
  - elixir
  - guaridan
  - phoenix framework

---
如果你用 [Phoenix framework 的 session][1] 管理会话，那么你的登录函数大概是这样写：

      def login(conn, user) do
        conn
        |> assign(:current_user, user)
        |> put_session(:user_id, user.id)
        |> configure_session(renew: true)
      end
    

这里的 `assign(:current_user, user)` 允许我们在模板中直接使用 `@current_user`。

在 [Guardian][2] 下，因为我们把会话管理交给 guardian，所以代码大概是这么写的：

    case IngressRun.Auth.login_by_email_and_pass(conn, email, pass, repo: Repo) do
          {:ok, user} ->
            conn
            |> Guardian.Plug.sign_in(user)
            |> put_flash(:info, "Welcome back!")
            |> redirect(to: page_path(conn, :index))
          {:error, _reason, conn} ->
            conn
            |> put_flash(:error, "Invalid email/password combination")
            |> render("new.html")
    end
    

那么有一个问题，在 guardian 下，我们的模板要怎样取到 `current_user` 的值？

guardian 提供了方法，让我们取得当前的用户资源：

    Guardian.Plug.current_resource(conn)
    

所以要在模板中使用 `@current_user`，我们的 controller 函数大概是这么写：

    defmodule IngressRun.AboutController do
      use IngressRun.Web, :controller
    
      def index(conn, _params) do
        conn
        |> assign(:current_user, Guardian.Plug.current_resource(conn))
        |> render("index.html")
      end
    end
    

guardian 还提供了 Phoenix 助手，所以在 controller 中我们可以把上面的代码改写如下：

    defmodule IngressRun.AboutController do
      use IngressRun.Web, :controller
      use Guardian.Phoenix.Controller
    
      def index(conn, _params, user, _claims) do
        conn
        |> assign(:current_user, user)
        |> render("index.html")
      end
    end
    

但因为这个 `current_user` 每个页面都要用到，则每个 controller 里的每个 action 都要写一遍 `assign(:current_user, user)`，未免太棘手。

这时我们就可以用上 [plug][3] &#8211; 如果你写过 express.js，则这个概念与中间件类似：

    plug :assign_current_user
    # ...
    defp assign_current_user(conn, _opts) do
        assign(conn, :current_user, Guardian.Plug.current_resource(conn))
    end
    

我们可以把这个 plug 定义在 controller 里，但如前面所说的，整个站点都要用到它，则定义在 `pipeline` 里会更合适，如下：

    pipeline :browser_session do
        plug Guardian.Plug.VerifySession
        plug Guardian.Plug.LoadResource
        plug :assign_current_user
    end
    

这样我们就可以继续在模板中使用 `<%= @current_user %>` 了。

 [1]: http://www.phoenixframework.org/docs/sessions
 [2]: https://github.com/ueberauth/guardian
 [3]: https://github.com/elixir-lang/plug#the-plugconn