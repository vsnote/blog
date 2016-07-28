---
title: Jasmine.js 简介
author: 陈 三
layout: post
date: 2013-02-16T13:59:17+00:00
url: /jasmine-js.html
views:
  - 642
dsq_thread_id:
  - 1087030333
categories:
  - 前端开发
tags:
  - Unit test

---
这是一个 JavaScript [测试工具][1]。

对我这样基本没机会写上大而复杂的程序的人来说，其实感觉有些多余，但玩玩还是有点意思。

所以，这一篇完全是「新手篇」。因为阅读过[很多][2] jasmine.js 的[文][3][章][4]，多数只是举它所提供的示例文件再阐述一遍。而作为新手，我觉得最重要的弄明白**为什么**，我为什么要用它，用它有什么好处，清楚了目的，再操弄工具的话，就不至于一头雾水而最后觉得根本是屠龙之术要来无用而放弃其实利器的东西。

平常写 js 程序，不可避免地要调试或除错(debug)，目前一般使用 firebug，但其实效率低下，有点暗箱操作的意思。出问题最好，没出问题其实也不是很清除它到底是运行正常了或其实不正常而无法知道。

这是 Jasmine.js 这样的测试工具的意义。

在写程序时，我们会有个预期，比如，一个加法函数，两个数字相加，我可以预计，1 + 1 = 2，1 + 1 ！= 3，当我们的程序通过这样的测试，即搞明白一加一等于多少不等于多少时，我们就可以确认，它是正确的。

写一个简单的加法 js 程序如下：

    function add(a,b){
      return a+b;
    }
    

则 jasmine.js 的测试语句可以这样写：

    describe('add function',function(){
      it('should be 2',function(){
        expect(add(1,1)).toBe(2);
      });
      it ('shouldn not be 3',function(){
        expect(add(1,1)).not.toBe(3);
      });
    });
    

将上述两段代码拷入在线的 Jasmine.js 测试工具 <http://tryjasmine.com/> 里，然后按左上角的 <kbd>try jasmine!</kbd>，可以看到通过测试的说明：

> specs 2 specs, 0 failures in 0.069s (see results)

再来说说它的结构。

`describe` 指示一个测试单元，`it` 则用于描述可能的预期，相当于将具体参数置入，运行程序。它们都是 JavaScript 函数，也因些遵循 JavaScript 的许多规则，比如函数的作用域等。

这样我们就清楚地知道程序运行的情况，而不是任由浏览器去运行，给出个无法确认的结果。

而且，Jasmine.js 跟我们的文件是分离的(不过 describe 与 it 仅仅只是函数，我们甚至可以将整个要测试的代码写入其中 &#8211; jasmine.js 主页上列出的 Matchers 演示即是那样，不过那并不推荐在实际中使用，因为只会让测试代码变得一团糟)，我们只是通过 `script` 标签链接到要测试的 js 文件，然后在 jasmine.js 的框架下编写测试，不需要其他依赖。

 [1]: http://pivotal.github.com/jasmine/
 [2]: https://www.adobe.com/devnet/html5/articles/unit-test-javascript-applications-with-jasmine.html
 [3]: http://ivanjovanovic.com/2011/07/22/introduction-to-javascript-bdd-testing-with-jasmine-library/
 [4]: http://net.tutsplus.com/tutorials/javascript-ajax/testing-your-javascript-with-jasmine/