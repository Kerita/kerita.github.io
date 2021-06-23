---
title: 什么是 npx？
categories: 前端
toc: true
tags: 工程化
date: 2021/6/23
---

## 什么是 npx

npx 是一个用来运行 npm 包的工具，而无需全局安装该 npm 包，它随着 npm 5.2 版本发布。

<!-- more -->

1.调用项目内部模块

```
babel test.js --watch --out-file test-compiled.js
```

运行上面命令，npx 将在当前目录下的 node_modules/bin 寻找 babel 运行

2.避免全局安装模块
运行上面命令，npx 将 create-react-app 下载到一个临时目录，使用以后再删除。

```
npx create-react-app react-test
```
