---
title: setState 是同步还是异步的
categories: 深入浅出 React
date: 2021-07-29
---

在我们使用 class 组件时，基本都会使用到 setState，因为唯有使用 setState 更新数据，才能实现数据驱动视图的效果。

<!-- more -->

## 同步还是异步

我们先来看 setState 是同步的还是异步的：
1、依次点击“点我增加”、“点我增加三倍”和“点我减少”，在控制台可以看到以下输出。

```
increment setState前的count 0
increment setState后的count 0


triple setState前的count 1
triple setState后的count 1


reduce setState前的count 2
reduce setState后的count 1
```

2、分析下结果

- 点击“点我增加”，setState 前后打印 count 都为 0，说明是异步更新；
- 点击“点我增加三倍”， setState 前后打印 count 皆为 1，说明多来几个 setState，React 也是异步的，而且是批量一起的。
- 点击“点我减少”，setState 前为 2，setState 后为 1，说明 setState 生效，说明 setTimeout 下，setState 是同步的。

3、结论
setState 不是简单的同步或者异步，在不同场景下 setState 会表现不同。在 React 生命周期钩子函数和合成事件中，setState 表现为异步；在 setTimeout、setInterval 等函数中，包括在 DOM 原生事件中，它都表现为同步。这种差异本质上是 React 的事务机制和批量更新机制决定的。

<iframe src="https://codesandbox.io/embed/setstate-yz93g?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="setState"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

## setState 更新过程

setState 源码的更新过程如下：
1.setState 执行进入 enqueueSetState 函数
2.enqueueSetState 进入 enqueueUpdate
3.enqueueUpdate 通过 isBatchingUpdate 判断当前是否在批量更新中。如果是，把组件加入 dirtyComponents 进行更新；否则，开始批量更新。

![setState 更新过程](./setState.png)

## 同步与异步原因

因为生命周期钩子函数和合成事件执行之前，React 都会执行 batchUpdate，此时 isBatchingUpdate 被设为 true。执行 setState 操作的组件进入批量的 dirtyComponents 中等待更新，setState 在代码执行上是同步，但由于进入等待队列进行批量更新，表现为异步。

而在 setTimeout 和 setInterval 中，没有执行 batchUpdate，所以表现为同步更新。

## 参考资料

- [深入 setState 机制](https://github.com/sisterAn/blog/issues/26)
- [setState](https://github.com/QiQi57/react-setstate)
