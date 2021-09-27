---
title: React 组件之间数据传递
categories: 深入浅出 React
tags: React
date: 2021-07-26
---

知识点：

- 单向数据流即数据只能从父组件向自组件流动
- 四种 React 组件进行数据传递的方法：props/context/EventEmitter/Redux

React 是一个构建用户界面的 JavaScript 库，其思想是用数据驱动视图。

可以用如下代码来表示：

```
UI = render(data)
```

data 就是 React 界面的核心。在渲染用户界面时，data 不是静止不动的，它可能需要在父子组件之间共享、可能需要在兄弟组件共享以及其他层次关系的组件之间共享。下面我们就讲 4 种组件间数据传递的方式。

<!-- more -->

- props 和 回调函数
  通过 props 传递，通过回调函数改变，这种方式适用于父子组件与兄弟组件间的数据传递，其他层级关系的组件使用此种方法传递比较冗余。

<iframe src="https://codesandbox.io/embed/props-and-callback-kd9ry?fontsize=14&hidenavigation=1&module=%2Fsrc%2FFather.js&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="props-and-callback"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

- Context API
  Context API 可以作为模块组件间的数据共享，共享的数据应该是在模块内的频繁使用和改变的。Context API 主要氛围三个部分：

  - 使用 React.createContext 创建 context
  - 从 context 获取 Provider 和 Consumer
  - 使用 Provider 提供数据，使用 Consumer 获取数据

<iframe src="https://codesandbox.io/embed/context-eume2?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Context"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

## Redux

在 Redux 的整个工作过程如下，其数据流是严格单向的。
![Redux 工作流程](./redux.png)

## 发布订阅模式

发布订阅模式其实分为三个部分，依赖收集器、发布者和订阅者。

依赖收集器在订阅者订阅时，将回调函数收集起来，等到发布者发布的时候，执行依赖收集器里对应的订阅函数。

<iframe src="https://codesandbox.io/embed/event-yuq0j?fontsize=14&hidenavigation=1&module=%2Fsrc%2FFather.js&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="event"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>
