+++
date = "2016-08-12T20:23:35+08:00"
title = "React Native AsyncStorage promise done"
draft = false
+++

React Native 的 `AsyncStorage` [模块有三种用法](http://facebook.github.io/react-native/docs/asyncstorage.html)：

1. 回调
2. Promise
3. `await`

但文档里目前仅提及 1 与 3，Promise 的用法还得看[代码](https://github.com/rmcvey/react-native/blob/07ee6c75baf0d802c0e5440f0f4678b86cba0acc/Examples/UIExplorer/AsyncStorageExample.js)。只不过，代码中有一个 `done()`，颇让人费解：

{{< highlight javascript >}}
AsyncStorage.setItem(STORAGE_KEY, selectedValue)
  .then(() => this._appendMessage('Saved selection to disk: ' + selectedValue))
  .catch((error) => this._appendMessage('AsyncStorage error: ' + error.message))
  .done();
{{< /highlight >}}

如果写过 jQuery，就会知道，jQuery 下的 ajax 有类似写法：

{{< highlight javascript >}}
var jqxhr = $.ajax( "example.php" )
  .done(function() {
    alert( "success" );
  })
  .fail(function() {
    alert( "error" );
  })
  .always(function() {
    alert( "complete" );
  });
{{< /highlight >}}

但此处的 `done` 与前面的 `done` 明显并不一致。

一个更合适的解释，是来自 [Q.js](https://github.com/kriskowal/q/wiki/API-Reference#promisedoneonfulfilled-onrejected-onprogress)：

> The Golden Rule of done vs. then usage is: either return your promise to someone else, or if the chain ends with you, call done to terminate it. Terminating with catch is not sufficient because the catch handler may itself throw an error.

`catch` 收尾的问题是，`catch` 内部还可能抛出错误。

但是要注意的是，按 [Promisejs](https://www.promisejs.org/#done) 上的说法：

> Note that `promise.done` (used in the examples in this section) has not been standardised. It is supported by most major promise libraries though, and is useful both as a teaching aid and in production code.

`promise.done` 目前尚未标准化，只不过各大 promise 库都已经支持罢了。