---
title: JSX 中自定义属性
categories: 前端
tags: React
date: 2018/2/17
---

JSX 用来定义 React 组件的 DOM 结构，其规则跟 HTML 基本相同，但还是有一些差异。例如 HTML 建议自定义属性以 data-* 命名，JSX 则是强制，因为如果不以这种方式命名，就不生效。

<!-- more -->

商城在对接某第三方支付公司信用卡接口的时候，他们的自定义属性不以 data-* 命名，导致数据一直获取不到。

后来发现利用 JS setAttribute() 手动设置非标准的自定义属性可以生效，直接写在 JSX 不行。

可以在 componentDidMount 函数中进行设置。