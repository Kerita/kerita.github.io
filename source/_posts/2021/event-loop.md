---
toc: true
title: 什么是事件循环 (Event Loop)
categories: 前端
tags: JS
date: 2021/4/1
---

# 事件循环

事件循环 (Event Loop) 是 JavaScript 运行的机制，事件循环负责执行代码、收集和处理事件以及执行队列中的子任务。浏览器与 Node.js 的事件循环存在差异。

事件循环机制为什么要分为微任务和宏任务呢？因为**_插队_**。当微任务执行的时候，其产生的微任务依旧可以在本次事件循环执行，实现了插队效果。利用此插队效果，不用等待下一次事件循环执行完宏任务才执行微任务。

<!-- more -->

## JavaScript 为什么设计成单线程

JavaScript 一开始是作为浏览器脚本，主要负责操作页面的 DOM 操作和事件响应，如果设计成多线程，多个线程同时对 DOM 进行操作，需要耗费的资源比较多，操作后处理逻辑也复杂，因而使用单线程 + 异步更适合运行在浏览器上。

## 浏览器的事件循环

---

### 浏览器的事件循环如下：

1. 从宏任务 (Macro Queue) 队列中取出一个任务放入执行栈，并执行
2. 从微任务 (Micro Queue) 队列按”先进先出“的原则取出任务，并逐一执行，此时产生的微任务放入队列中，等待取出执行
3. 所有的微任务执行完后，如果是渲染周期，则先执行 requesetAnimationFrame 队列中的所有任务，再进行渲染
4. 重复步骤 1

![浏览器的事件循环](./browser-event-loop.png)

### 宏任务与微任务有哪些

- 微任务

```
Promise.then 等
```

- 宏任务

```
setTimeout,setInterval,script 的代码, I/O, UI 交互事件, postMessage等等，
除了微任务的都是宏任务
```

## requestAnimationFrame 的回调函数

其中 requesetAnimationFrame 的回调函数并不是宏任务，也不是微任务。

### 代码验证

**通过[代码示例](https://codepen.io/Kerita/pen/yLgMdwe)的控制台输出，可以验证我们以上的结论。**

```
console.log("start");

setTimeout(() => {
  console.log("setTimeout");
}, 0);

requestAnimationFrame(() => {
  console.log("requestAnimationFrame");
});

new Promise((resolve) => {
  console.log("Promise");

  resolve();
}).then(() => {
  console.log("Promise resolve");
});

console.log("end");
```

** 控制台输出 **

```
"start";
"Promise";
"end";
"Promise resolve";
"requestAnimationFrame";
"setTimeout";

```

代码的执行顺序如下：

1. 执行所有主流程语句，依次打印出"start"，"Promise"，"end"
2. 执行进入微任务队列的任务,打印出"Promise resolve"
3. 接着执行 requestAnimationFrame，打印出 "requestAnimationFrame"（验证了 requestAnimationFrame 即不是宏任务，也不是微任务）
4. 最后执行 setTimeout 的回调，打印出 "setTimeout"

### 影响

通过了解事件循环，有助于了解浏览器内部的运行机制，更好的书写代码；运用宏任务和微任务的特点，写出性能更好的代码

- setTimeout/setInterval 作为宏任务计时是不准确，它们只能保证回调函数在指定时间进入等待队列，而不是立即执行
- 对于耗时任务，我们可以通过 setTimeout 将其拆分为各种小任务
- 避免 Promise.then 这样的微任务产生死循环

## Node.js 的事件循环

---

### Node.js 的事件循环如下：

1. 在固定队列随机选择一个队列，从队列中取出第一个任务执行
2. 执行 nextTick 队列中的所有任务
3. 执行 promise 队列中的所有任务
4. 回到步骤 1

![Node的事件循环](./node-event-loop.png)

### Node.js 的固定队列

![](./node-queue.png)

## setImmediate 与 nextTick

setImmediate 需要等到下个循环才能执行，nextTick 才是立马执行

## 推荐视频

[https://www.youtube.com/watch?v=u1kqx6AenYw&t=853s&ab_channel=JSConf](https://www.youtube.com/watch?v=u1kqx6AenYw&t=853s&ab_channel=JSConf)
