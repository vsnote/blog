+++
date = "2016-08-01T22:39:56+08:00"
title = "CentOS 7 上安装 Elixir"
url = "/install-elixir-on-centos-7"
+++

这里介绍两种方式。

## 发行版仓库

执行 `yum info elixir`，我们得到：

{{< highlight bash >}}
  Available Packages
  Name        : elixir
  Arch        : noarch
  Version     : 0.12.5
  Release     : 2.el7
  Size        : 2.7 M
  Repo        : epel/x86_64
  Summary     : A modern approach to programming for the Erlang VM
  URL         : http://elixir-lang.org/
  License     : ASL 2.0 and ERPL
  Description : Elixir is a programming language built on top of the Erlang VM.
              : As Erlang, it is a functional language built to support distributed,
              : fault-tolerant, non-stop applications with hot code swapping.
{{< /highlight >}}

从上面的数据我们可以看到，epel/x86_64 仓库中 elixir 版本是 0.12.5，而目前（2016-08-01)官网上显示 elixir 版本是 1.3.2。所以这个方法可以放弃。

## 预编译包

Elixir 在 github 上有提供[预编译包](https://github.com/elixir-lang/elixir/releases/)，我们可以下载然后自己安装 - 记得要先安装 erlang。

{{< highlight bash >}}$ cd{{< /highlight >}}
{{< highlight bash >}}$ wget https://github.com/elixir-lang/elixir/archive/v1.3.2.zip{{< /highlight >}}
{{< highlight bash >}}$ unzip v1.3.2.zip -d .{{< /highlight >}}
{{< highlight bash >}}$ cd elixir-1.3.2{{< /highlight >}}
{{< highlight bash >}}$ make{{< /highlight >}}

成功后，把 elixir 的路径加入环境变量中即可：

{{< highlight bash >}}
  export PATH="$PATH:/home/sam/elixir-1.3.2/bin"
{{< /highlight >}}

命令行下敲入：

{{< highlight bash >}}
  $ elixir -v
{{< /highlight >}}

即可查看 elixir 是否安装成功，及成功安装的版本。

这里，我把 elixir 安装在用户主目录下。

此后要升级 elixir，也是按照一样的步骤操作。

## 资料

1. [elixir 官网的安装说明](http://elixir-lang.org/install.html)