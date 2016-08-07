+++
date = "2016-08-06T21:02:39+08:00"
title = "App Store export compliance 填写"
url = "app-store-export-compliance.html"
+++

一个猜想，不一定对：中国的开发者多数是法盲。

这是我提交 app 到苹果的 App Store 时，碰上 export compliance 一词的想法。

`ITSAppUsesNonExemptEncryption` 值该是 true 还是 false？

作为一名前端开发，我显然不知道这是什么东西。我查了点资料，似乎跟美国的[加密算法的出口管制](https://developer.apple.com/library/ios/documentation/LanguagesUtilities/Conceptual/iTunesConnect_Guide/Chapters/SubmittingTheApp.html#//apple_ref/doc/uid/TP40011225-CH33-SW6)有关：

> U.S. export laws require that products containing encryption be properly authorized for export. 

翻译过来大致是：美国的出口法律要求包含加密的产品经审批方能出口。

我开发的这个 app，没有用户系统，只是使用了 twitter 的 [Sign in with Twitter](https://dev.twitter.com/web/sign-in) 功能，当然，API 接口是 https 加密的，而据 [stackoverflow](http://stackoverflow.com/questions/35739361/itsappusesnonexemptencryption-export-compliance-while-internal-testing) 的一个说法，用 https，也是要把 `ITSAppUsesNonExemptEncryption` 设置为 `true` 的。

但一旦设置为 `true`，我可能要跟以下这类文档打交道：

1. Encryption Registration approval from BIS
2. CCATS approval from BIS
3. French import declaration

我想了想，这三样我肯定是一样都拿不出，那还是选 `false` 吧。