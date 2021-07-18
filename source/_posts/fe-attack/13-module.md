---
title: 前端模块标准和 Webpack 工作流程
categories: 前端进击笔记
toc: true
date: 2021/07/18
---

## CommonJS 与 ES6 Module 的区别

可以参考本博客之前的文章 [CommonJS 与 ES6 Module 的区别](/04/03/2021/module/)

<!-- more -->

## Webpack 工作流程

Webpack 的使用中有 4 个核心概念：入口（entry）、输出（output）、Loader、插件（plugins），其工作流程如下：

1.通过 entry 指定的入口开始，解析各个文件模块间的依赖。

2.根据模块间的依赖关系，开始对各个模块进行编译。

3.编译过程中，根据配置的规则对一些模块使用 Loader 进行编译处理。

4.根据插件的配置，对 Loader 编译后的代码进行封装、优化、分块、压缩等。

5.最终 Webpack 整合各个模块，根据依赖关系将它们打包成最终的一个或者多个文件。
