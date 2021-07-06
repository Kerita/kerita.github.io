---
title: 5-JavaScript 的运行机制
categories: 前端进击笔记
toc: true
tags: JS
date: 2021/7/5
---

JavaScript 作为是一门单线程语言，使用事件循环(Event Loop)机制，来执行代码和收集回调队列的子任务。

<!-- more -->

## Event Loop 的运行机制

1.JavaScript 运行时主线程有一个`调用栈`  
2.任务在`调用栈`中执行完毕出栈  
3.任务执行过程可能产生异步任务，异步任务会在有结果时进入`回调队列`等待执行  
4.栈为空时`回调队列`的任务入栈

![Event Loop 运行机制](./event-loop.png)

## 宏任务和微任务

每次只会取出一个宏任务执行，但会一次性取出所有微任务执行。

requestAnimationFrame 的回调即不是宏任务，也不是微任务，它在微任务执行完毕后执行。

- 宏任务
  script 代码、setTimeout、setInterval、Promise

- 微任务
  Promise.then, Promise.catch

下面是经典宏任务与微任务经典面试题：
输出依次为：
"script start", "script end", "promise 1", "error caught", "errorFunc", "promise 2", "errorFunc then res", "setTimeout"

```
console.log("script start");



setTimeout(() => {

  console.log("setTimeout");

}, 1000);



Promise.resolve()

  .then(function () {

    console.log("promise1");

  })

  .then(function () {

    console.log("promise2");

  });



async function errorFunc() {

  try {

    await Promise.reject("error!!!");

  } catch (e) {

    console.log("error caught"); // 微1-3

  }

  console.log("errorFunc");

  return Promise.resolve("errorFunc success");

}

errorFunc().then((res) => console.log("errorFunc then res"));



console.log("script end");

```
