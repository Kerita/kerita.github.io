---
title: 商城性能优化想法
toc: true
categories: 前端
tags: [性能, 优化]
date: 2018/2/14
---

一些关于商城性能优化的想法。

<!-- more -->

## 压缩图片资源
保证图片质量情况下，尽量争取PC端每张图片不超过 200kb，移动端每张图片不超过 100kb,采用智图对图片进行压缩。

1.急需压缩清单
- 产品页缩略图
- 产品页展示图
- 产品简介和包装清单图片

2.待压缩清单
- banner 图
- 首页产品图片
- 首页头部图片

## 图片使用规范
尽量使用压缩率更高的 jpg 图片，而不是 png 图片，争取使用 webp 图片

1.尽量采用 jpg 格式
png 是无损压缩，jpg 是有损压缩，不需要透明度的情况下，使用 jpg 格式

2.使用 webp 格式图片（待定）
允许的情况下，在PC端 chrome，移动端 chrome 和 原生 android  浏览器，以及 Opera 浏览器可以使用 webp 格式
2015年第三季度，京东在强制双核浏览器使用 chrome 内核进行渲染之后，统计数据显示使用 chrome 的比例高达 60%
    2017年11月25日，caniuse 上支持 webp 的浏览器份额
China
72.89%    +    0.62%    =    73.51%
Global
72.41%    +    0.23%    =    72.64%

## 产品简介图区分桌面端和移动端
产品简介图同时加载了移动端资源和桌面端资源，亟待优化


