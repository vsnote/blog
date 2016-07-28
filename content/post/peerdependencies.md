---
title: peerDependencies
author: 陈 三
layout: post
date: 2016-06-30T06:32:13+00:00
url: /peerdependencies.html
views:
  - 160
categories:
  - 前端开发
tags:
  - node.js
  - NPM

---
写 npm package 时，接触最多的，当属 [dependencies 与 devDependencies][1]。

如果一个包定义了 `dependencies` 与 `devDependencies`，则我们在安装这个包时，会连着它的依赖们一同安装。

比如一个 react-native 的包，它依赖于 `react` 与 `react-native`，如果我们把 `react` 及 `react-native` 定义在 `dependencies` 下，则安装完这个包后，它的目录结构是这样：

  1. ProjectRoot/node\_modules/package\_name/node_modules/react
  2. ProjectRoot/node\_modules/package\_name/node_modules/react-native

我们又下载了一遍 react 与 react-native，这显得多余，可能还会导致冲突问题。

这时我们就可以使用 [`peerDependencies`][2]，通过它，我们能够声明第三方包正常运行的环境 &#8211; 要安装我，你的环境该是如何，否则将无法运行。当然，没人会无聊到在一个 ember.js 项目中安装一个 react-native 的第三方包。

 [1]: https://www.zfanw.com/blog/difference-between-dependencies-and-devdependencies.html
 [2]: https://nodejs.org/en/blog/npm/peer-dependencies/