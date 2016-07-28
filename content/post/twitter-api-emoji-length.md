+++
date = "2016-07-28T11:00:23+08:00"
title = "twitter api 中 emoji 长度的计量"
url = "/twitter-api-emoji-indices.html"
+++

来看一条 tweet：

<blockquote class="twitter-tweet" data-lang="en"><p lang="zh" dir="ltr">🐷🐷🐷 测试 twitter 字符长度计量 <a href="https://twitter.com/hashtag/testEmoji?src=hash">#testEmoji</a></p>&mdash; 陈三 (@chenxsan) <a href="https://twitter.com/chenxsan/status/758496532593192960">July 28, 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

它的 api 返回数据有一部分是这样：

{{< highlight json >}}
{
  "created_at": "Thu Jul 28 02:57:20 +0000 2016",
  "id": 758496532593193000,
  "id_str": "758496532593192960",
  "text": "🐷🐷🐷 测试 twitter 字符长度计量 #testEmoji",
  "truncated": false,
  "entities": {
    "hashtags": [
      {
        "text": "testEmoji",
        "indices": [
          22,
          32
        ]
      }
    ],
    "symbols": [],
    "user_mentions": [],
    "urls": []
  },
}
{{< /highlight >}}

我们看 `hashtags` 里的 `indices` 数据，[22， 32]，它表示这个 hashtag 在文本中的起始与终点位置，拷贝下 `text` 字段的值，然后放到浏览器控制台下执行：

{{< highlight bash >}}
  "🐷🐷🐷 测试 twitter 字符长度计量 #testEmoji".slice(22, 32)
{{< /highlight >}}

我们得到的是 `"计量 #testEm"`，很遗憾，这是错的。

在浏览器的控制台下，我们可以看到 "🐷🐷🐷" 的长度是 6，但 twitter 返回的数据里表明，twitter 是把它算成 3 个长度值。

我们可以考虑将 `"🐷🐷🐷 测试 twitter 字符长度计量 #testEmoji"` 用 `split` 方法切割成数组后再组装：

{{< highlight console >}}
  > "🐷🐷🐷 测试 twitter 字符长度计量 #testEmoji".split('')
  > ["�", "�", "�", "�", "�", "�", " ", "测", "试", " ", "t", "w", "i", "t", "t", "e", "r", " ", "字", "符", "长", "度", "计", "量", " ", "#", "t", "e", "s", "t", "E", "m", "o", "j", "i"]
{{< /highlight >}}

很遗憾，这个结果是错的。

我找到的一个 npm 库 [spliddit](https://www.npmjs.com/package/spliddit)，它可以正确地切割 emoji：

{{< highlight javascript >}}
  var spliddit = require("spliddit")
  spliddit("🐷🐷🐷 测试 twitter 字符长度计量 #testEmoji")
{{< /highlight >}}

我们会得到如下数据：

{{< highlight javascript >}}
  ["🐷", "🐷", "🐷", " ", "测", "试", " ", "t", "w", "i", "t", "t", "e", "r", " ", "字", "符", "长", "度", "计", "量", " ", "#", "t", "e", "s", "t", "E", "m", "o", "j", "i"]
{{< /highlight >}}

也就是说，我们的文本先经 `spliddit` 切割，再 `slice`，再 `join`，就能根据 `indices` 数据得到正确的 hashtag 了：

{{< highlight console >}}
  > spliddit("🐷🐷🐷 测试 twitter 字符长度计量 #testEmoji").slice(22, 32).join('')
  > "#testEmoji"
{{< /highlight >}}