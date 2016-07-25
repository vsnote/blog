---
title: 修订历史
author: 陈 三
layout: page
date: 2015-05-01T04:00:24+00:00
views:
  - 450

---
## 博客修订历史

  * 2013.07.30 根据 BootStrap 3 对博客做修改。
    
    1.1 Single Post 页面，目录右浮动，加 BootStrap Scrollspy、affix 效果；
    
    1.2 页面自适应，页面宽度小于 BootStrap 定义的 large 时，停止浮动，即返回正常页面流中

  * 2013.08.04 Script 现由 LABjs 管理
  * 2014.01.01 去掉评论功能
  * 2014.03.22 加上评论，希望它们能对内容有所扩展、补充
  * 2014.11.01 修了一个移动端上链接无法点击的 bug，因为只设定 .col-lg-xx 类
  * 2015.04.17 关闭评论
  * 2015.04.30 基于 Google Material Design 改版，移除 BootStrap 样式
  * 2015.05.15 移除 CDN 上的整个 bootstrap.js，仅取用 affix.js 与 scrollspy.js 代码
  * 2015.06.10 移除汉堡包菜单，换成左侧可见的全局菜单，移动端上将全局菜单固定定位到屏幕底部
  * 2015.09.04 转 HTTPS

## TODO

  1. [x] 加载大图时加上 loading indicator 标识
  2. [x] 移动端上，单面页的前后文章导航存在高度不一致 &#8212; 使用 `display: flex;` 解决
  3. [x] overlay 在 iOS 上 Safari 点击无法移除 &#8212; 监听 touchend 事件解决
  4. [x] 添加 fastclick
  5. ​优化页面渲染性能
  6. <del>把导航区的 list svg 换成三色的</del>
  7. <del>导航区出来时会导致 toc 位置跳回初始位置 &#8212; won&#8217;t fix</del>
  8. 将 style.css 中 media query 部分分离出来，重新确认下几个响应断点
  9. 检查旧文，把 a 的 title 补上
 10. [ ] 将 blog 的样式表重新整理