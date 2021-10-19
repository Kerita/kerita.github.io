---
title: 1-了解 Promise
categories: 前端进阶
date: 2021-09-29
---

Promise 是 ES6 内置的对象，用一个对象实例表示某个操作最终是成功或者失败，并且将成功值或者原因暴露出来，它主要解决了异步编程过程中存在的两个问题：  
1.回调地狱问题  
2.信任问题

<!-- more -->

## 解决的问题

1.回调地狱问题

- 传统异步编程
  传统异步编程中，如果需要多次将请求的返回结果当做下次请求的参数，便需要不断在回调函数中嵌套请求，形成回调地狱。回调地狱代码嵌套，可读性差。

```js
ajax('/url1', {param: {}},  (res1) => {
    ajax('/url2, {param: res1}, (res2) => {
        ajax('/url3, {param: res2}, (res3) => {
            // 继续回调
        })
    })
})
```

- Promise 编程
  Promise 将请求结果在 then 函数的参数中返回；如果 then 的回调返回的也是一个 Promise，其已成功的值或者已失败的原因也可在链式调用的 then 函数参数中找到。

```js
const promise = new Promise((resolve, reject) => {
  ajax("/url1", { param: {} }, (res1) => {
    resolve(res1);
  });
}).then((res1) => {
  return new Promise((resolve, reject) => {
    ajax('/url2, { param: res1 }, (res2) => {
        resolve(res2)
    })
  });
}).then((res2) => {
    ajax('/url3, {param: res2}, (res3) => {
        // operation res2
    })
});
```

2.信任问题
传统异步编程中，当我们使用一个信任度比较低的库 `ajax`，将传入的回调函数完全交给库控制，其执行次数可能为多次，是我们无法控制的。

```js
ajax("/url", { param: {} }, (res) => {
  if (res) {
    handleSuccess(res);
  } else {
    handleError();
  }
});
```

利用 Promise 的状态只能更改一次的特点，我们可以实现控制的反转，按回调函数只执行一次。

```js
new Promise((resolve, reject) => {
  ajax("/url", { param: {} }, (res) => {
    if (res) {
      resolve(res);
    } else {
      reject();
    }
  });
}).then(handleSuccess, handleError);
```

## Promise/A+ 规范

Promise 的规范成为 Promise/A+ 规范，可以通过以下文档，了解 Promise 的具体规范

- [Promise Spec](https://promisesaplus.com/)
- [Promise Spec 翻译](https://juejin.cn/post/6844903767654023182)
- [Promise - MDN 文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [Promise — 阮一峰](https://es6.ruanyifeng.com/?search=promise&x=0&y=0#docs/promise)

## 实现 Promise

理解一个东西最好的方式就是实现它，可以根据以上规范，逐步实现一个 Promise。

[个人实现的 Promise 以及一些 Promise 相关练习](https://github.com/Kerita/fe-adavance/tree/master/1-promise)
