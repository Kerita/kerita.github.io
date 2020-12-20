---
title: ES6变量解构引发的面试题的猜想
toc: true
categories: 前端
tags: JS
date: 2017/8/31
---

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。（来自阮一峰ES6教程）

<!-- more -->

### 交换变量值
同时阮一峰还说了用变量解构可以对很轻松的实现对两个值进行交换，他给出了例子，关于面试题的猜想就是由这个例子引发的。

### 面试题
```
let x = 1
let y = 2
[x,y] = [y,x]

console.log(x)
console.log(y)
```
请问上面的代码将输出什么？
A. 2 1
B. Uncaught ReferenceError: y is not defined

按照前面的说法，选A。但之所以能成为面试题，是因为有坑。

### 考点
- 变量解构。 利用变量解构可以进行赋值。
- JS什么时候必须加分号。第一个字符是'['，'(','+','-', '/',此时上一行不加分号，就不会将上下两行代码分开。

所以不加分号时，上面的代码变成这样。因为let声明变量暂时性死区的特性，此时的2[x,y]中的y还是未定义，所以是ReferenceError。

```
let x=1
let y = 2[x,y] = [y,x]
```

### 参考链接
[ECMAScript 6 入门](http://es6.ruanyifeng.com/)
[JavaScript 语句后应该加分号么？](https://www.zhihu.com/question/20298345)