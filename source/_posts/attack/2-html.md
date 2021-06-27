---
title: 2-HTML
categories: 前端进击笔记
toc: true
tags: HTML
date: 2021/6/27
---

浏览器在加载页面的过程会用到 GUI 渲染线程和 JavaScript 引擎线程，其中 GUI 渲染线程负责 HTML，JavaScript 引擎线程负责执行 JavaScript 脚本。

<!-- more -->

## 加载过程

浏览器访问网页时首先获取到的都是一个 HTML 文档，继而开始解析 HTML 文档里的标签。对于大部分普通标签如 p, div, header 浏览器会直接渲染；对于 link 标签，浏览器会去获取外部资源；对于 script 标签的处理比较特殊，因为 JS 脚本会修改页面内容，所以浏览器此时会停止页面渲染，待解析并执行 JS 后，才会继续渲染页面。

如果加载时间或者运行时间过长，页面就会出现空白或者“卡死”状态，影响用户体验。

## 延迟脚本加载和执行

脚本的加载和执行都会阻塞页面的渲染，然而并不是所有的脚本立即需要的，例如负责统计和监控的脚本。

script 标签有三个属性可以用来延迟加载和执行, async, defer, preload。

- async
  async 会让脚本异步加载，加载完成会立即执行

- defer
  defer 会让脚本异步加载，加载完成后等到所有的 HTML 标签解析完毕才会执行

- preload
  使用 link 标签的 preload 属性，可以实现提前加载当前页面资源，支持加载音视频、字体、图片、样式表、JS 脚本等文件，加载过程不会阻塞渲染和 document 的 onload 事件。

- prefetch
  prefetch 使用方法与 preload 类似。但用来加载接下来可能会使用到的资源。

## 事件委托

基于 HTML 文档的树形结构，我们可以利用事件冒泡原理，将子元素事件委托给父元素统一处理。

## 参考资料

- [用 preload 预加载页面资源](https://mp.weixin.qq.com/s/ytl3EduxfpjcbOyYT74MLg)
