---
title: 单页应用与前端路由库设计原理
categories: 前端进击笔记
toc: true
date: 2021/7/18
---

## 什么是单页应用

单页应用就是只有一个 HTML 页面的应用，页面 URL 的变化只是通过浏览器 API 修改，浏览器不会向服务器请求新的 HTML 的，而是通过 JS 控制不同的 URL 渲染相应的内容。

单页应用相比传统的 JSP、PHP 多页应用，在切换页面时无需刷新，只需进行局部更新，加载内容快，页面的数据状态和用户数据依然保留。但是，因为单页应用返回的是一个 body 空白的 HTML 文件，HTML 内容由 JS 生成，搜索引擎无法获取到，可能影响搜索引擎排名。

<!-- more -->

## 前端路由库设计原理

单页应用可以实现内容的局部更新，例如页面的导航栏和底部保持不变，页面主体发生改变。为了保持页面刷新时，依然能够展现当前的内容，所以单页应用根据不同的 URL 渲染不同的页面，前端路由库应运而生。

前端路由库一般有两种模式，一种是 History 模式，一种是 Hash 模式。

- History 模式  
  History 模式下不同的 pathname 渲染渲染相应的内容，依赖浏览器 History API（IE 10+），以及服务器配置，如下。

```
location / {
  try_files $uri $uri/ /index.html;
}
```

History 方法 [在线实例](https://kerita.me/fe-attack-demo/12-spa/history.html)：
1.history.go():参数为 0 时，刷新页面；参数超出界限时，不会有任何效果也不会报错。
2.history.back:相当于 history.go(-1)，返回上一页，触发 popstate event。
3.history.forward:相当于 history.go(1)，进入下一页，触发 popstate event。  
4.history.pushState()：向当前浏览器会话的历史堆栈添加一个状态，不会触发 popstate event。  
5.history.replaceState():修改当前浏览器会话的历史堆栈最新的状态，不会触发 popstate event。

History 模式下维护了当前的路由 state，根据不同的路由 state 渲染不同的组件，history.back 和 history.forward 相当于浏览器的后退和前进，可以通过触发 popstate 改变当前的路由 state，路由库通过提供 push 方法，由 pushState 改变浏览器 URL，并自行更改路由 state。因而，在单页应用中使用 window.history.pushState 改变 URL，是无法实现内容的切换的，需要使用路由库提供的 push 方法。

- Hash 模式  
  Hash 模式依赖 location.hash 获取和改变 hash，通过监听 hashchange event 知道 URL 改变。

## vue-router 的三种路由模式

vue-router 三种路由模式分别是 History,Hash 和 Abstract，History 和 Hash 与前面所讲一致，Abstract 是 vue-router 特有的一种模式。

Abstract 支持所有 JavaScript 运行环境，如 Node.js 服务器端。如果发现没有浏览器的 API，路由会自动强制进入这个模式。使用 Abstract 模式，可以在已存在的路由页面中内嵌其他的路由页面，而保持在浏览器当中依旧显示当前页面的路由。

## 总结

- history 模式依赖 popstate 事件
  - 使用 window.history.back 和 window.history.forward 改变 URL，触发 popstate 事件，可以实现单页应用的路由切换
  - 使用 window.history.pushState 和 window.history.replaceState 无法触发事件，因而无法实现单页应用路由切换
- hash 模式依赖 hashchange 事件，使用 window.location.hash 修改和获取路由

## 参考资料

[浅析 vue-router 的三种模式](https://segmentfault.com/a/1190000039692879)
[Vue Router history 模式的配置方法及其原理](https://segmentfault.com/a/1190000019391139)
[History -- MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/History)
[「源码解析 」这一次彻底弄懂 react-router 路由原理](https://juejin.cn/post/6886290490640039943#heading-14)
[vue 基于 abstract 路由模式 实现页面内嵌](https://zhuanlan.zhihu.com/p/336767145)
