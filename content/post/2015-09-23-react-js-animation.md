---
title: React.js 动画
author: 陈 三
layout: post
date: 2015-09-23T14:24:19+00:00
url: /react-js-animation.html
views:
  - 1521
categories:
  - 前端开发
tags:
  - react.js

---
我猜你看过 [React.js 动画][1]的文档，并且不下三遍。

我看了不下十遍，还是觉得 [ReactCSSTransitionGroup][2] 这 high-level API 跟魔法似的，另外，[奇奇怪怪的 bug][3] 还不少。

最后我决定试试更底层的 [TransitionGroup][4]。

TransitionGroup 定义了动画组件的六个生命周期：

  1. componentWillAppear(callback)
  2. componentDidAppear()
  3. componentWillEnter(callback)
  4. componentDidEnter()
  5. componentWillLeave(callback)
  6. componentDidLeave()

如果你了解 componentDidMount 等，则这六个生命周期的概念是相近的，只不过，它们是动画组件才会有的。

简单说，一个 TransitionGroup 容器中的组件，在它：

  1. 加入容器
  2. 或是从容器中移除

就会经历以上 6 个生命周期。

我们操纵它在这些生命周期中的样式，也就产生了动画。

来看一个简单模样：

      render () {
        let todos = this.state.todos.map((todo, index) => {
          return (
             <Animation key={index}><li>{todo}</li></Animation>
          )
        })
        return (
            <ReactTransitionGroup component='ul'>
              {todos}
            </ReactTransitionGroup>
        )
      }
    
    

ReactTransitionGroup 是容器，Animation 是容器中的元素。

之所以要有一个 Animation 组件包装真正的元素，只是我为了便于代码复用。

Animation 组件中，componentWillEnter 周期中的代码是这样的（**注意，这是我理想中的版本**，具体情况见文末链接）：

      componentWillEnter (cb) {
        let el = React.findDOMNode(this)
        el.classList.add(styles.enter)
        requestAnimationFrame(() => {
          el.classList.add(styles.active)
        })
        el.addEventListener('transitionend', () => {
          if (cb) cb()
        el.classList.remove(styles.enter)
        el.classList.remove(styles.active)
        })
      }
    

我们在 **componentWillEnter** 里给 Animation 组件添加了 styles.enter 样式类，然后在浏览器下一个 tick 加入 styles.active 样式类 &#8211; 这里使用了 requestAnimationFrame，也可以使用 setTimeout，另外我们还监听 &#8216;transitionend&#8217; 事件，transitionend 事件发生时执行回调 cb 并移除 styles.enter 与 styles.active 两个样式类（如果不了解这一种样式用法，请参见 [CSS 模块化][5]）。

相应的 CSS 文件：

    .enter {
      opacity: 0;
    }
    .enter.active {
      opacity: 1;
      transition: opacity 0.5s ease-in;
    }
    
    

当然，现实比较刺人，transitionend 事件并不稳定、时有时没有，所以我写的真实的代码其实是[这样][6]，它基于 khan Academy 的 [timeout-transition-group][7] 组件做了改造，最后的动画效果请点击[示例][8]查看。

不过据说，我们有望在 react.js 0.14 中用上可靠的 [ReactCSSTransitionGroup][9] &#8211; 现在是 react.js 0.14 rc 1。

谢天谢地。<div class=timeline> 

## P.S

  1. 2015-10-02 可以尝试 twitter fabric 团队出的 [velocity-react][10]
  2. 2015-10-11 [react.js 0.14 正式版本][11]已经发布，其中动画部分说明如下：
    
    > To improve reliability, CSSTransitionGroup will no longer listen to transition events. Instead, you should specify transition durations manually using props such as transitionEnterTimeout={500}.</div>

 [1]: https://facebook.github.io/react/docs/animation.html
 [2]: https://github.com/facebook/react/blob/master/src/addons/transitions/ReactCSSTransitionGroupChild.js "源代码"
 [3]: https://github.com/facebook/react/search?q=ReactCSSTransitionGroup&type=Issues&utf8=✓
 [4]: https://facebook.github.io/react/docs/animation.html#low-level-api-reacttransitiongroup
 [5]: https://www.zfanw.com/blog/css-modularize.html
 [6]: https://github.com/chenxsan/demo-jest-test-flux-store/blob/master/src/animation/Animation.js "访问 github"
 [7]: https://github.com/Khan/react-components/blob/master/js/timeout-transition-group.jsx
 [8]: https://www.zfanw.com/react/demo-store-test/
 [9]: https://github.com/facebook/react/pull/4561
 [10]: https://github.com/twitter-fabric/velocity-react
 [11]: http://facebook.github.io/react/blog/2015/10/07/react-v0.14.html