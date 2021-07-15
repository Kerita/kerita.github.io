---
title: 前端框架模板引擎的实现原理
categories: 前端进击笔记
toc: true
tags: 浏览器
date: 2021/7/15
---

## Vue 模板引擎工作过程

以 Vue 为例子，对于开发者编写的 Vue 代码，Vue 会将其进行以下处理从而渲染到页面中：

1.解析语法生成 AST 对象；

2.根据生成的 AST 对象，完成 data 数据初始化；

3.根据 AST 对象和 data 数据绑定情况，生成虚拟 DOM 对象；

4.将虚拟 DOM 对象生成真正的 DOM 元素插入到页面中，此时页面会被渲染。

## JSX 和模板引擎是什么关系

JSX 是一种模板语法，@babel/plugin-transform-react-jsx 插件将 JSX 转换为 React.createElement 语法，React.createElement 生成虚拟 DOM——也就是 AST，再根据 AST 生成 HTML。因为 JSX 可以理解为模板语法，@babel/plugin-transform-react-jsx 插件 和 React.createElement 可以理解为模板引擎。
