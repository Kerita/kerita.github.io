---
title: 1-组件库方案
categories: 组件库
date: 2022-02-20
---

## 构建组件库前需要确定的三个点

1.确定组件库的整体架构设计
对于组件库架构最重要的点就是，使用单包结构，还是使用多包结构。

    - 单包结构
    	- 发布过程中，需要将整个包发布
    	- 组件库中组件互相引用方便
    - 多包结构：
    	- 需要使用 lerna 管理 Monorepo 架构的组件库
    	- 组件库中组件互相引用不方便
    	- 发布时可以只发布更新的组件

<!-- more -->

2.确定组件库的基础技术能力

- 构建能力
  构建组件库推荐使用 Rollup，构建项目推荐 Webpack。
- 文档能力
  可以用 Docz、VuePress、StoryBook、Styleguidist 等工具构建组件库文档。

  3.组件库对外文档服务