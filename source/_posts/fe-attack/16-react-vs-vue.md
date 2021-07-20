---
title: React 和 Vue 有什么异同
categories:前端进击笔记
date:2021-07-21
---

React 和 Vue 是当下最流行的两大前端框架，今天我们来对比下他们有什么异同。

<!-- more -->

## 相同点：

- 使用虚拟 DOM
  React 和 Vue 都使用虚拟 DOM 提高页面更新时的渲染性能，虚拟 DOM 的工作流程主要分为 3 步。  
  1.使用 JavaScript 对象描述页面的 DOM 树；  
  2.当页面数据发生变化时，生成新的 DOM 树，对比新旧 DOM 树的差异；  
  3.将虚拟 DOM 的差异应用在真实 DOM 树上，对 DOM 树进行增删改。
- 用于构建用户界面的 JavaScript 库
  不像 Angular 一样大而全，React 和 Vue 可以说小而美，都专注于构建用户界面。针对构建应用需要的脚手架、路由、状态管理等功能，通过社区或者单独的库进行支持。

## 不同点：

- React 比 Vue 更灵活
  React 使用 JSX 作为模板，使用原生的 if、for 等语法实现模板中的常见语法。Vue 则提供了 v-if、v-for、v-model 等语法。对于 import 进入的方法或者组件，React 可以直接使用，Vue 则需要在 Vue 实例中声明一次。

- 针对虚拟 DOM 的优化不同
  页面数据更新时，React 使用递归重新生成虚拟 DOM，如果页面 DOM 节点很多，递归生成的虚拟 DOM 时间就会很长。浏览器中 JavaScript 执行线程和 UI 线程执行顺序是互斥，此时页面就会出现假死状态，影响体验。

  React 16 针对虚拟 DOM 采用 Fiber 进行任务的执行。利用浏览器提供的 requestIdleCallback API，将更新任务拆分成小任务，一个个放在 requestIdleCallback 中执行。requestIdleCallback 中任务的执行优先级比较低，因而不会阻塞页面的操作和渲染。

  Vue 没有采用类似 React Fiber 的时间分片机制，在 Vue 3.0 中采用动静结合的策略，在编译的时候就将模板中用到指令的地方记录下来，页面数据更新时，只需要遍历这些用到指令的地方，遍历的区域大大缩小。

- React 是单向数据流，Vue 通过 v-modal 语法糖实现双向数据流
