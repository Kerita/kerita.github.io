---
title: React 的虚拟 DOM
categories: 深入浅出 React
date: 2021-07-28
---

虚拟 DOM 是使用 JS 对象来描述真实 DOM 结构。在数据发生改变时，虚拟 DOM 也发生改变，通过对比新旧虚拟 DOM 结构(diff)，找出二者差异，对真实 DOM 结构做更新(patch)。

<!-- more -->

## 为什么要有虚拟 DOM

- 提高更新效率
  模板引擎方案更新需要手动生成 DOM，每次更新都需要重新生成所有涉及更新部分的 DOM，使用虚拟 DOM 实现按需更新。
- 提升开发体验
  使用 jQuery 直接操作 DOM，操作麻烦；使用虚拟 DOM，实现数据驱动视图，提升开发体验。
- 跨平台开发
  虚拟 DOM 将 UI 描述为 JS 对象，具体的渲染交给 render 函数，因此使用 React 生态的 React Native 可以同时开发 iOS 和 Android App。Write once, run anywhere。
