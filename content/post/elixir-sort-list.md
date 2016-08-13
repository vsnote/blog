+++
date = "2016-08-13T10:17:55+08:00"
title = "elixir 列表排序"
url = "elixir-sort-list.html"
+++

在 elixir 里，我有个列表，大概是这样：

{{< highlight elixir >}}
  [
    %{id: 1, retweet_count: 10, favorite_count: 20},
    %{id: 2, retweet_count: 20, favorite_count: 1},
    %{id: 3, retweet_count: 15, favorite_count: 50},
  ]
{{< /highlight >}}

现在想按 `retweet_count` 与 `favorite_count` 的总数降序排列。

在 JavaScript 里，这非常简单：

{{< highlight JavaScript >}}
  list.sort(function (a, b) {
    if (a.retweet_count + a.favorite_count > b.retweet_count + b.favorite_count) {
      return -1
    } else if (a.retweet_count + a.favorite_count < b.retweet_count + b.favorite_count) {
      return 1
    }
    return 0
  })
{{< /highlight >}}

Elixir 有个类似的[方法 sort_by](http://elixir-lang.org/docs/stable/elixir/Enum.html#sort/2)：

> sort(enumerable, fun)

于是我们的降序排列规则写成如下：

{{< highlight elixir >}}
 Enum.sort [
    %{id: 1, retweet_count: 10, favorite_count: 20},
    %{id: 2, retweet_count: 20, favorite_count: 1},
    %{id: 3, retweet_count: 15, favorite_count: 50},
  ], &(Map.get(&1, :retweet_count) + Map.get(&1, :favorite_count) >= Map.get(&2, :retweet_count) + Map.get(&2, :favorite_count))
{{< /highlight >}}
