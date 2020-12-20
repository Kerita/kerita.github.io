---
title: Awards 项目总结
categories: 前端
tag: 项目
toc: true
date: 2017/09/24
---

本周二（19号）彻底完成公司 Awards 项目的需求和需求修改并上线，趁热打铁写下完成项目过程的一些思考。

<!-- more -->

## 项目介绍
[Awards 项目](https://awards.insta360.com/about?locale=zh) 是 Insta360 针对全景作品进行有奖征集一个项目，项目工作量主要在前端（故所说项目都指前端部分项目—— fe-awards），完成整个项目大概花了四天时间（指完成第一版需求的功能，不包括后来改需求时间）。

## React+mobx 架构
整个项目采用 React+mobx 的架构， React 完成项目 View 层面的呈现，mobx 负责一些项目数据的管理。

- React
1. Vue、 React、 Angular
以 Vue、 React、 Angular 为代表的 mvvm 框架取代 jQuery 成为当下前端圈最热门的框架，解决的最大痛点就是让前端工程师从繁琐的 DOM 操作解脱。

2. 实例
以隐藏一个 div 为例，jQuery 需要获取该 div，再设置display 为 none, 或者从该 div 的父元素利用 DOM 操作移除该元素；而 React 的只需要在该 div 的 style属性中给 display 属性绑定一个三元条件判断,将组件 state 中的某个变量作为判断条件，当 state 的变量值发生改变时，界面 div 是否显示也会随着改变。

3. Vue&React
 在使用 React 前也用过 Vue，使用过程最大的感受就是 Vue 提供了很多语法糖，写的时候很顺畅，随心所欲； React 则没有那么多语法糖，甚至连需要学习的新语法也很少。

 很多人都说 Vue 比 React 容易上手，其实如果掌握了 mvvm 这种思想，React 比 Vue 更容易上手，因为除了 JSX 这种混合 JS 和 HTML 的语法、几个生态周期函数、setState()，React 就基本没有东西了，而 Vue 则还有需要掌握一些语法。但如上面所说， React 写起来就是没有 Vue 顺畅。

- mobx
使用 mobx 而不是常见的 Redux，是为了解决 React 单向数据流的不方便，实现数据双向绑定自动更新，特别是那些存储于数据管理框架中给各组件共享的数据。

下面介绍 mobx 的一些特性，具体内容查看 [mobx 文档](http://cn.mobx.js.org/)
1. 数据双向绑定自动更新
项目中的 mobx 存储了一个变量 locale，指明当前页面使用的是哪种语言，当调用 mobx 中定义的方法改变 locale 时，所有组件引用这个 locale 的地方都会自动更新，对页面重新渲染。

2. 数据自动持久化
还是 locale 这个值，在 mobx 声明时利用 @persist 修饰符指明需要持久化，当 locale 发生改变时便会自动存储在 localstorge 中，下次加载也会自动读取这个值。

3. 计算属性
声明计算属性，根据其他值，该属性设置不同的值。当 locale 为 zh 时，加载中文语言包，当 locale 为 en 时，加载英文语言包。

## 统计代码追踪
在项目中加了 growingIO、百度统计、ga、fb pixel等统计代码，对访问数据进行记录。

同时加了一些 meta 信息，使得在 facebook 分享这个项目时，可以显示我们想要的预览图。

这个地方基本没什么问题，就是 ga 上与其他项目使用同个 id 追踪时，这个项目无法利用过滤器中的主机名（awards.insta360.com）筛选出来，但相同情况下的 blog.insta360.com 就筛选出来了。

## 移动端适配方案
我对整个项目进行分割—— header,footer,banner,about,instruction,terms。

- 对于 header,footer,banner 这三个PC端和移动端 UI 上差异比较大的，我分开来写，根据不同屏幕加载不同组件。

- 对于 about,instruction,terms UI 差别不大，利用媒体查询 @media(max-width: 768px) 对移动端做了适配。

## 遇到的问题
- 修改 Antd 组件样式
  项目使用 React 经典组件库 Antd 进行开发，无论是在布局还是表单组件上都很方便，但是有些地方例如 单选、多选，因为各个公司设计不同，不能直接使用，想要使用 antd Form 组件各种方便的 api，如验证数据有效性、required 、初始值，就只能痛苦地修改 Antd 组件的样式。而且只能写在 App.css 中才能控制到 Antd 的样式，代码有些丑了。

  如果有时间针对表单组件，联合公司设计师写一套适合公司 UI 风格的 React 组件，接下来会很大方便开发。

- Insta360 Air app 语言参数不生效
  因为项目有多语言，而且要求首次加载的时候就能指定语言，所以会获取 url 的 locale 参数值（zh或en），没有的取 localstorage 的值, localstorage 也没有的话默认为 en。

  但是这个参数在 Insta360 Air app 的 webview 中无法生效，一开始以为是webview 禁止取参数，测试发现是可以的。摸索了一些，发现是 mobx 持久化函数的回调没法生效，所以只要把 取参数设置 locale 这段代码 移到其他就行了。

  但有个奇怪的地方，就是只在 Insta360 Air app 的 webview 有这个问题，难道这个 app 的 webview 加了什么特技？

## 小结
- 不足之处
1. 组件化程度不够高
一开始觉得这个项目数据流动不多，所以没有抽出很多小组件，导致组件化程度不够高，有些组件代码比较多，对应的 CSS 代码也多。所以即使数据不多的情况下，抽组件依然有好处

2. 代码质量
无论是 JSX、 json、 还是 CSS，都尽可能写得好看漂亮，不仅有利于之后维护，写的时候也清晰。 