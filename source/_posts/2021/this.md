---
title: this 指向
categories: 前端
toc: true
tags: JS
date: 2021/4/12
---

this 永远指向一个对象

## 普通函数

this 的指向完全取决于函数调用的位置

## 箭头函数

this 被设置为他被创建时的环境

## call,apply,bind

- call,apply 改变函数调用的 this 指向，立即执行，call 的参数逐个传递，apply 数组形式传递
- bind 返回一个函数，并改变它的 this 指向，而且只能改变一次，bind 的参数逐个传递
