+++
date = "2016-08-09T12:56:31+08:00"
title = "CentOS 7 常用 PostgreSQL 命令"
url = "centos-7-postgresql-command.html"
+++

## 登录用户

CentOS 7 上安装完 PostgreSQL 后，会默认创建一个 `postgres` 的用户。要使用 PostgreSQL，我们需要先切换到该用户：

{{< highlight bash >}}
  $ sudo -i -u postgres
{{< /highlight >}}

接着输入：

{{< highlight bash >}}
  $ psql
{{< /highlight >}}

就可以进入 PostgreSQL 命令行。此时的命令行提示不再显示 `$`，而是 `postgres=#`。

这里，你可以执行各种 SQL 语句。

## 退出 PostgreSQL 命令行

{{< highlight bash >}}
  postgres=# \q
{{< /highlight >}}

## 查看所有数据库

{{< highlight bash >}}
  postgres=# \l
{{< /highlight >}}

## 连接数据库

{{< highlight bash >}}
  postgres=# \c test
{{< /highlight >}}

## 查看表

在连接上数据库后，可以查看数据库下的所有数据表：

{{< highlight bash >}}
  postgres=# \d
{{< /highlight >}}

`\d` 会罗列出所有的数据表，包括 PostgreSQL 自动创建的自增长字段的表。如果只想查看用户创建的，

{{< highlight bash >}}
  postgres=# \dt
{{< /highlight >}}

如果想查看单个数据表的结构，则在命令后指定表名：

{{< highlight bash >}}
  postgres=# \d test
{{< /highlight >}}

## 参考资料

1. [PostgreSQL Meta Commands](https://www.postgresql.org/docs/9.4/static/app-psql.html#APP-PSQL-META-COMMANDS)