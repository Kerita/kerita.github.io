---
title: new 做了什么
categories: 前端
toc: true
tags: JS
date: 2021/4/13
---

## JavaScript 中 new 做了什么

我们使用 new 和构造函数产生一个新的对象，那在这个过程 new 做了什么呢？

1. 生成一个空的对象 obj
2. 将 obj 的原型指向构造函数的 prototype
3. 将 obj 赋值 给上下文 this
4. 将 this 返回

因此，下面代码将打印出 true 和 a

<!-- more -->

```js
function Base() {
  console.log(this.__proto__ === Base.prototype); // true
}

Base.prototype = {
  a: "a",
};

const obj1 = new Base();
console.log(obj1.a); // a
```

## 特殊情况：构造函数返回一个对象

当构造函数显式返回一个对象时，new 操作符会将该对象返回，而不是返回 this。因此，如下代码打印出来的是 b，而不是 a。

若显式返回的是 null 对象或者其他数据类型，也会将 this 返回。

```js
function BaseReturnObj() {
  this.a = "a";

  return {
    a: "b",
  };
}

const obj2 = new BaseReturnObj();
console.log(obj2.a); // b
```
