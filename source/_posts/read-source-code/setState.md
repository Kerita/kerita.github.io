---
title: setState 源码阅读
categories: 源码阅读
date: 2021-08-03
---

在理解[setState 是同步还是异步的](/07/29/dive-in-react/11-setState/) 时，梳理下 setState 的源码逻辑，如下：

<!-- more -->

![setState 逻辑](./setState.png)

`setState` 同步或者异步取决于是在什么地方调用，在生命周期函数或者 React 合成事件回调表现为异步，因为 React 提前执行了 `batchUpdates`，将 `isBatchingUpdate` 设置为 `true`，所以会将 `setState` 的组件放入 `dirtyComponents` 中，等到生命周期函数或者合成事件回调执行完毕后更新。
