---
title: react-native Navigation Experimental 怎么用
author: 陈 三
layout: post
date: 2016-06-22T06:50:48+00:00
url: /react-native-navigator-experimental-usage.html
views:
  - 237
categories:
  - 前端开发

---
**说明**：本文基于 react-native 0.29.0-rc.0，仅针对 iOS 平台。

react-native 的 navigation experimental 是 [navigator][1] 的继任，但因为还在开发中，目前没什么文档，API 也经常变动，示例没跟上，就让人看不懂。

在 navigation experimental 下，[路由只是些对象][2]：

  ```javascript
  function createAppNavigationState(): Object {
    return  {
      // Three tabs.
      tabs: {
        index: 0,
        routes: [
          {key: 'apple'},
          {key: 'banana'},
          {key: 'orange'},
        ],
      },
      // Scenes for the `apple` tab.
      apple: {
        index: 0,
        routes: [{key: 'Apple Home'}],
      },
      // Scenes for the `banana` tab.
      banana: {
        index: 0,
        routes: [{key: 'Banana Home'}],
      },
      // Scenes for the `orange` tab.
      orange: {
        index: 0,
        routes: [{key: 'Orange Home'}],
      },
    };
  }
  ```
    

上面的路由表示 app 有三个标签页，每个标签页各有各的子路由。

我们不妨把路由想成一个族谱（family tree），循着每个树枝，我们能抵达到各个页面。而 `index` 就是我们的指路牌。我们的页面间的切换，就是[一个 action 修改 navigation state 的副作用][3]。

有了路由数据，就可以渲染对应的 scene 了，怎么做？

我们来写一个简单页面，它的路由数据是这样：
  ```javascript
    {
      index: 0,
      routes: [{
        key: 'Want Home'
      }]
    }
  ```   

我们只有一个页面，`index` 值表示这个页面处于激活状态中。

页面组件如下：

  ```javascript

    'use strict'
    import React from 'react'
    import { View, Text, NavigationExperimental } from 'react-native'
    const {
      CardStack: NavigationCardStack,
      Header: NavigationHeader,
      PropTypes: NavigationPropTypes,
      StateUtils: NavigationStateUtils,
    } = NavigationExperimental
    class Want extends React.Component {
      renderScene = (sceneProps) => {
        return (
          <View style={{flex: 1, marginTop: 64}}>
            <Text>haha</Text>
          </View>
        )
      }
      render () {
        return (
          <NavigationCardStack
            direction='vertical'
            navigationState={{
              index: 0,
              routes: [{
                key: 'Want Home'
              }]
            }}
            renderScene={this.renderScene}
            />
        )
      }
    }
    export default Want
  ```   
    

刷新 Simulator，我们能看到 `haha` 文本，如果你用的是 react-native 0.28 版本，还会看到如下的错误：

> ExceptionsManager.js:70 Warning: Failed propType: Required prop `onNavigate` was not specified in `NavigationCardStack`. Check the render method of `Want`.

而在 0.29 中，`onNavigate` [被移除了][4]，更换为 `onNavigateBack`。

如果想给页面定义个 navigationBar，我们可以添加一个 `renderOverlay`：

  ```javascript
      renderOverlay = (sceneProps) => {
        return (
          <NavigationHeader
            {...sceneProps}
            renderTitleComponent={() => (
              <NavigationHeader.Title>
                想吃
              </NavigationHeader.Title>
            )}
            />
        )
      }
      render () {
        return (
          <NavigationCardStack
            direction='vertical'
            navigationState={{
              index: 0,
              routes: [{
                key: 'Want Home'
              }]
            }}
            renderScene={this.renderScene}
            renderOverlay={this.renderOverlay}
            />
        )
      }
   ```   

刷新 simulator，我们能看到这样的界面：

[<img src="https://www.zfanw.com/blog/wp-content/uploads/2016/06/Screen-Shot-2016-06-21-at-23.10.14.png" alt="react native navigator experimental" width="760" class="alignnone size-full wp-image-18582" srcset="https://www.zfanw.com/blog/wp-content/uploads/2016/06/Screen-Shot-2016-06-21-at-23.10.14.png 760w, https://www.zfanw.com/blog/wp-content/uploads/2016/06/Screen-Shot-2016-06-21-at-23.10.14-300x105.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2016/06/Screen-Shot-2016-06-21-at-23.10.14-100x35.png 100w" sizes="(max-width: 760px) 100vw, 760px" />][5]

目前我们还只有一个页面，没有路由切换，也没有动画效果。

假定我们点击了 haha 文本会进入详情页面。

在点击发生时，我们需要调整路由数据。

我们要用到 [redux][6]。

先创建一个 `navigation.js` 的 reducer 文件，把上面的路由数据迁移过来：

  ```javascript
    import { PUSH_ROUTE, POP_ROUTE } from '../actionTypes'
    import { NavigationExperimental } from 'react-native'
    const {StateUtils: NavigationStateUtils} = NavigationExperimental
    
    const initialState = {
      index: 0,
      routes: [{
        key: 'Want Home'
      }]
    }
    
    function navigationState (state = initialState, action) {
      switch (action.type) {
        case PUSH_ROUTE:
          if (state.routes[state.index].key === (action.route && action.route.key)) return state
          return NavigationStateUtils.push(state, action.route)
    
        case POP_ROUTE:
          if (state.index === 0 || state.routes.length === 1) return state
          return NavigationStateUtils.pop(state)
    
        default:
          return state
    
      }
    }
    
    export default navigationState
   ```   
    

再添加一个 `navigation.js` 的 action 文件：

  ```javascript
    import { PUSH_ROUTE, POP_ROUTE } from '../actionTypes'
    
    export function push (route) {
      return {
        type: PUSH_ROUTE,
        route: route
      }
    }
    
    export function pop () {
      return {
        type: POP_ROUTE
      }
    }
  ```    

在 `Want` 组件中，我们通过 react-redux 提供的 `connect` 绑定 store 里的数据：

  ```javascript
    'use strict'
    import React from 'react'
    import { View, Text, NavigationExperimental, TouchableHighlight } from 'react-native'
    import { connect } from 'react-redux'
    import { push, pop } from '../actions/navigation'
    const {
      CardStack: NavigationCardStack,
      Header: NavigationHeader,
      PropTypes: NavigationPropTypes,
      StateUtils: NavigationStateUtils,
    } = NavigationExperimental
    class Want extends React.Component {
      goDetail = () => {
        this.props.dispatch(push({
          key: 'Want Detail'
        }))
      }
      renderScene = (sceneProps) => {
        // 我们在这里通过 key 渲染不同组件，这里只是简单展示同一个组件
        return (
          <View style={{flex: 1, marginTop: 64}}>
            <TouchableHighlight onPress={this.goDetail}
              ><Text>haha</Text>
            </TouchableHighlight>
          </View>
        )
      }
      renderOverlay = (sceneProps) => {
        return (
          <NavigationHeader
            {...sceneProps}
            renderTitleComponent={() => (
              <NavigationHeader.Title>
                想吃
              </NavigationHeader.Title>
            )}
            />
        )
      }
      render () {
        return (
          <NavigationCardStack
            direction='vertical'
            navigationState={this.props.navigation}
            renderScene={this.renderScene}
            renderOverlay={this.renderOverlay}
            />
        )
      }
    }
    const mapStateToProps = (state) => ({
      navigation: state.navigation
    })
    export default connect(mapStateToProps)(Want)
   ```   
    

这样，我们就有了一个简陋的页面切换：

[<img src="https://www.zfanw.com/blog/wp-content/uploads/2016/06/react-native-navigator.gif" alt="react-native-navigator" width="372" class="alignnone size-full wp-image-18588" />][7]

Chrome 控制台中的 log 如下：

[<img src="https://www.zfanw.com/blog/wp-content/uploads/2016/06/Screen-Shot-2016-06-22-at-11.16.27.png" alt="Screen Shot 2016-06-22 at 11.16.27" width="1400" class="alignnone size-full wp-image-18590" srcset="https://www.zfanw.com/blog/wp-content/uploads/2016/06/Screen-Shot-2016-06-22-at-11.16.27.png 1400w, https://www.zfanw.com/blog/wp-content/uploads/2016/06/Screen-Shot-2016-06-22-at-11.16.27-300x196.png 300w, https://www.zfanw.com/blog/wp-content/uploads/2016/06/Screen-Shot-2016-06-22-at-11.16.27-768x502.png 768w, https://www.zfanw.com/blog/wp-content/uploads/2016/06/Screen-Shot-2016-06-22-at-11.16.27-1024x670.png 1024w, https://www.zfanw.com/blog/wp-content/uploads/2016/06/Screen-Shot-2016-06-22-at-11.16.27-100x65.png 100w" sizes="(max-width: 1400px) 100vw, 1400px" />][8]

上面的动画里可以看到，虽然我们没有给 `Want Detail` 添加返回键，它默认却是已经有了。但是我们如果点击返回键，是没有效果的。

我们需要给 `NavigationHeader` 添加一个 `onNavigateBack`，它定义了用户点击返回键时的效果：

  ```javascript
<NavigationHeader
  {...sceneProps}
  onNavigateBack={
    () => this.props.dispatch(pop())
  }
  renderTitleComponent={() => (
    <NavigationHeader.Title>
      想吃
    </NavigationHeader.Title>
  )}
  />
  ```  

结果如下图：

[<img src="https://www.zfanw.com/blog/wp-content/uploads/2016/06/react-native-navigator-with-back.gif" alt="react-native-navigator-with-back" width="372" class="alignnone size-full wp-image-18595" />][9]

 [1]: https://facebook.github.io/react-native/docs/navigator.html
 [2]: https://github.com/facebook/react-native/blob/master/Examples/UIExplorer/NavigationExperimental/NavigationCardStack-NavigationHeader-Tabs-example.js#L53
 [3]: https://github.com/facebook/react-native/blob/master/Examples/UIExplorer/NavigationExperimental/NavigationCardStack-NavigationHeader-Tabs-example.js#L84
 [4]: https://github.com/facebook/react-native/commit/fb0007d85323909ab652bf97166744fa7e17daab
 [5]: https://www.zfanw.com/blog/wp-content/uploads/2016/06/Screen-Shot-2016-06-21-at-23.10.14.png
 [6]: https://github.com/reactjs/redux
 [7]: https://www.zfanw.com/blog/wp-content/uploads/2016/06/react-native-navigator.gif
 [8]: https://www.zfanw.com/blog/wp-content/uploads/2016/06/Screen-Shot-2016-06-22-at-11.16.27.png
 [9]: https://www.zfanw.com/blog/wp-content/uploads/2016/06/react-native-navigator-with-back.gif