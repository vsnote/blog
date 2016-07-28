---
title: Github 最佳实践
author: 陈 三
layout: post
date: 2014-09-16T22:44:55+00:00
url: /best-practice-contribute-on-github.html
views:
  - 2252
categories:
  - 前端开发
tags:
  - Git
  - Github

---
标题写的是「最佳实践」，但其实是我自己的标准，并非绝对意义。

另外，这个「最佳实践」限定在 Github 上贡献代码。

**长话短说版本**（以下内容假定你熟悉 Git 的各种基本命令）：

  1. fork 开源库 [A][1] 到自己的 github，假设为库 [B][2]
  2. 从库 B clone 一份到本地，假设目录为 fundamentals
  {{< highlight bash >}}
$ git clone git@github.com:chenxsan/WebFundamentals.git fundamentals
  {{< /highlight >}}
  3. 给本地库配置上游
  {{< highlight bash >}}$ git remote add upstream https://github.com/google/WebFundamentals.git{{< /highlight >}}  
  4. 从本地 master 分支分出一个 dev 分支
  {{< highlight bash >}}
  $ git checkout -b dev
  {{< /highlight >}}
  5. 在 dev 分支上出力
  {{< highlight bash >}}
  $ git add -u
  $ git commit -m 'fix bug'
  {{< /highlight >}}
  6. 将 dev 分支 `push` 到 github
  {{< highlight bash >}}
  $ git push origin dev:dev
  {{< /highlight >}}  
    
    **注意：** `:` 前是本地的分支名，`:` 后是远程的分支名。远程的分支名任你取。

  7. 从 github 上的 dev 分支提交 pull request 给上游库 A
  8. 不幸被拒绝，上游库所有者要求你再补点东西；然后上游库有新的 commit
  9. 本地 master 分支更新上游库 A 的代码
  {{< highlight bash >}}
$ git stash
$ git checkout master
$ git pull --rebase upstream master
  {{< /highlight >}}
 10. 本地 dev 分支重新基于 master 来过
 {{< highlight bash >}}
$ git checkout dev
$ git rebase master
$ git stash pop
 {{< /highlight >}}   
    
    **（如果你的 dev 分支是公开且有人使用，请谨慎使用 `rebase`，因为它会改变公开的历史）**

 11. 继续修改 dev 分支，改完后重复上面的 commit 动作，然后 push 到 github 上再提交 pull request
 {{< highlight bash >}}
$ git push --force origin dev
 {{< /highlight >}}   
    
    之所以要加 `--force`，是因为 github 上的 dev 分支已经跟本地的 dev 有过分歧。git 会提示你先 pull 然后 merge，但那样会一片混乱，所以粗暴点用上 `--force`。当然，更好的建议是，没事别乱推送到 Github，等确定要提 pull request 时再推送。

 12. 在 pull request 被合并后，删除本地、远程的 dev 分支
{{< highlight bash >}}
$ git push origin --delete dev # 删除远程 dev 分支
$ git branch -D dev # 删除本地 dev 分支
{{< /highlight >}}   
    
    因为 dev 分支只是出于一时目的使用，所以在 pull request 被合并后，就可以通过命令删除它。也可以在被合并的 pull request 页面上删除，Github 提供有删除按钮。

 13. 将本地 master 分支与上游库同步
 {{< highlight bash >}}
$ git pull --rebase upstream master
$ git push
 {{< /highlight >}}   

这里有几个重点。

**一个**是保持 master 分支干净，不在 master 分支上 commit。这一条建议来自 jQuery[^13490.1]。目的是给自己方便：

> This is really only for your own convenience: it&#8217;s easy for the maintainer of a project to accept your pull request from your master branch, but it&#8217;s problematic for your fork when you want to pull the changes back and your master branch has diverged from upstream.
> 
> 这纯是为了你自己方便：对项目维护者来说，接受来自你 master 分支的 pull request 是很简单的事，但对你的分支来说，这会是个问题，比如你要从上游分支拉回修改，但是你的 master 分支却已经分道扬镳。

整个过程中，我们 fork 的 master 分支只是为同步上游库的内容而存在。

**另一个**是保持 commit 历史干净[^13490.2]。所以上面的流程中，拉回上游库的修改用了 `--rebase`，而不是先 fetch 再 merge。更多请看文末的链接2。

[^13490.1]:    
    [Commits and Pull Requests | Contribute to jQuery][3]

[^13490.2]:    
    [Git and Github: keeping a feature branch updated with upstream?][4]

 [1]: https://github.com/google/WebFundamentals.git
 [2]: https://github.com/chenxsan/WebFundamentals
 [3]: http://contribute.jquery.org/commits-and-pull-requests/#never-commit-on-master
 [4]: http://ginsys.eu/git-and-github-keeping-a-feature-branch-updated-with-upstream/