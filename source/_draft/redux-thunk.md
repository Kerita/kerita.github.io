---
title: redux-thunk 原理解析
categories: react
date: 2022-01-11
---

<!-- more -->

## 过程

- redux dispatch 只能接收一个包含 action 的 plain object
- redux-thunk 让 redux 支持接收 function，并将 dispatch,getState 作为参数传入

## 作用

- 不用 redux-thunk 也可实现异步 dispatch action，只需要在异步操作结束的后 dispatch
- redux-thunk 可以将异步操作函数封装起来
