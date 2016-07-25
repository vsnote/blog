---
title: react-native 滑动删除
author: 陈 三
layout: post
date: 2016-06-28T10:41:27+00:00
url: /react-native-swipeable-listview.html
views:
  - 200
categories:
  - 前端开发
tags:
  - react-native

---
**说明**：本文基于 react-native 0.29.0-rc.0，仅针对 iOS 平台。

iOS 下的列表，通常都可以往左滑动，显示快捷菜单 &#8211; 比如删除。

只是 react-native 下的 ListView 不具备这种功能。

但实际上，react-native 官方库里，就有一个 [SwipeableListView][1]，只不过是放在 `Experimental` 目录下，表示还不成熟 &#8211; 目前也是没有文档的，只能自己阅读源代码。

其实用法非常简单，大部分跟 ListView 是一致的，只是多了些 prop。

来看一个示例：

```javascript
import React from 'react'
import { ScrollView, View, TouchableHighlight, Text, SwipeableListView } from 'react-native'
import { connect } from 'react-redux'
import styles from './styles'
import formatListViewDataSource from '../../utils/formatListViewDataSource'
class WantHome extends React.Component {
  componentDidMount () {
    this.props.dispatch({
      type: 'USER_ENTERED_WANT_HOME'
    })
  }
  render () {
    let ds = SwipeableListView.getNewDataSource()
    let obj = formatListViewDataSource(this.props.want)
    ds = ds.cloneWithRowsAndSections(...obj)
    if (!this.props.want.length) {
      return (
        <View style={[styles.container, styles.center]}>
          <Text>暂无内容，请点击右上角按钮添加</Text>
        </View>
      )
    } else {
      return (
        <ScrollView style={[styles.body]}>
          <SwipeableListView
            bounceFirstRowOnMount
            maxSwipeDistance={100}
            dataSource={ds}
            renderQuickActions={(rowData, sectionID, rowID) => {
              return (
                <View style={{
                  flex: 1,
                  flexDirection: 'row',
                  justifyContent: 'flex-end',
                  alignItems: 'center'
                }}>
                  <TouchableHighlight
                    onPress={() => {
                      alert(1)
                    }}>
                    <View style={{
                      backgroundColor: 'red',
                      flex: 1,
                      alignItems: 'center',
                      flexDirection: 'row',
                      paddingHorizontal: 10
                    }}>
                      <Text style={{
                        color: 'white',
                        fontSize: 16
                      }}>删除</Text>
                    </View>
                  </TouchableHighlight>
                </View>
              )
            }}
            renderRow={(rowData) => {
              return (
                <View style={{
                  paddingVertical: 10,
                  backgroundColor: '#fff'
                }}>
                  <Text style={{
                    fontSize: 16
                  }}>
                    {rowData.text}
                  </Text>
                </View>
              )
            }}
          />
        </ScrollView>
      )
    }
  }
}
const mapStateToProps = (state) => ({
  want: state.want
})
export default connect(mapStateToProps)(WantHome)
```    

这里有几个需要注意的属性值：

  1. `dataSource` &#8211; 我们要渲染的数据列表。
    
    通常我们会有一个数组，比如 `['咸饭', '粥']`，数据需要处理成 `SwipeableListView` 需要的格式，比如：
    
        {
        's1': '标题',
        'r1': '咸饭',
        'r2': '粥'
        }
        
    
    这也是上面代码中 `formatListViewDataSource` 函数起到的作用：
    
        /**
        * @function formatListViewDataSource format data for ListView of react-native
        * @param {Array} data - data to be formatted
        * @return {Array}
        * @example
        *   let ds = formatListViewDataSource([1, 2, 3])
        *   xxx.cloneWithRowsAndSections(...ds)
        */
        export default function formatListViewDataSource (data) {
        if (!Array.isArray(data)) {
        throw new Error('function only accept Array')
        }
        var dataBlob = {}
        var sectionIDs = ['s1']
        var rowIDs = [[]]
        data.forEach(function (element, index) {
        dataBlob['r' + index] = {id: 'r' + index, text: element}
        rowIDs[0].push('r' + index)
        })
        dataBlob['s1'] = ''
        return [
        dataBlob,
        sectionIDs,
        rowIDs
        ]
        }
        
        

  2. `maxSwipeDistance` &#8211; 表示滑动的最大距离，必须设置，否则默认为 0
  3. `renderQuickActions` &#8211; 这就是我们滑动后显示的快捷动作了

效果如下图：

[<img src="https://www.zfanw.com/blog/wp-content/uploads/2016/06/react-native-swipeablelist.gif" alt="react native swipeableListView" width="372" class="alignnone size-full wp-image-18623" />][2]

 [1]: https://github.com/facebook/react-native/tree/master/Libraries/Experimental/SwipeableRow
 [2]: https://www.zfanw.com/blog/wp-content/uploads/2016/06/react-native-swipeablelist.gif