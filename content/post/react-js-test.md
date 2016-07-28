---
title: React.js 测试
author: 陈 三
layout: post
date: 2015-07-30T14:40:30+00:00
excerpt: 使用 Shallow rendering 测试 react.js 组件
url: /react-js-test.html
views:
  - 976
categories:
  - 前端开发
tags:
  - react.js

---
你写了一个 React.js 的组件，现在打算给组件写测试代码，怎么写？

react.js 官方提供了一个 [Test Utilities][1]，有两种用法：

  1. 渲染到 DOM 后再测试 &#8211; `renderIntoDocument`
  2. 只是生成组件的一个实例，然后对测试该实践 &#8211; 即文档中所说的 Shallow rendering

这里介绍第二种用法，全部测试代码见我 [github 上的 react 日期组件库][2]。

用到的工具有：

  1. [mocha][3] &#8211; 测试框架
  2. [Chai][4] &#8211; 断言库
  3. [babeljs][5] &#8211; 用于编译 jsx 文件

以下测试代码经常简化，并加上注释说明：

    // 导入 React，这个 React 附带 addons
    import React from 'react/addons'; 
    
    // 从 `chai` 包中导入 `expect`
    import {expect} from 'chai'; 
    
    // 导入要测试的 react 组件
    import Week from '../src/week'; 
    
    describe('Week component', function() {
        let {TestUtils} = React.addons; // ES6 写法
        let shallowRenderer = TestUtils.createRenderer();
    
        // 使用 react 的 测试方法渲染 react 组件
        shallowRenderer.render(<Week days={[undefined, undefined, 1, 2, 3, 4, 5]} selectDay={function(){}} highlight={true} day={1}/>);
        let week;
        before('return Week component', () => {
    
            // 从渲染的组件中返回结果
            week = shallowRenderer.getRenderOutput();
    
            // 你可以通过 console.log(week) 来查看 week 对象的结构
        });
    
        // 以下是测试
        it('should have tr as container', () => {
            expect(week.type).to.equal('tr');
        });
        it('should have 7 td children', () => {
            expect(week.props.children.length).to.equal(7);
        });
        // ...
    });
    

如果你对写测试的必要性不敢确定 &#8211; 我知道绝大部分前端开发都不写测试的，可以看看这一篇[单元测试的十二个理由][6]。

 [1]: https://facebook.github.io/react/docs/test-utils.html
 [2]: https://github.com/chenxsan/react-date-picker-cs/blob/master/test/week.js "打开 github 库"
 [3]: http://mochajs.org/ "打开 mocha 首页"
 [4]: http://chaijs.com/ "打开 chaijs 首页"
 [5]: https://babeljs.io/docs/setup/#mocha "如何在 mocha 框架中使用 babelJS"
 [6]: http://www.onjava.com/pub/a/onjava/2003/04/02/javaxpckbk.html