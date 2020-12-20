---
title: React 组件清除定时器
categories: 前端
tags: React
date: 2018/2/16
---

在 React 组件定义一个计时器，在组件卸载的时候就应该清除掉。

<!-- more -->

```
componentWillUnmount () {
    this.loadInterval && clearInterval(this.loadInterval)
    this.loadInterval = false
}
```
