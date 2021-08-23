---
title: webpack chunk 与 bundle
categories: webpack
date: 2021-08-23
---

chunk 和 bundle 都是 webpack 的重要概念，今天我们来理解它们。

<!-- more -->

## chunk

来自 webpack 词汇表的诠释：

> Chunk: This webpack-specific term is used internally to manage the bundling process. Bundles are composed out of chunks, of which there are several types (e.g. entry and child). Typically, chunks directly correspond with the output bundles however, there are some configurations that don't yield a one-to-one relationship.

`chunk` 是 webpack 内部用于管理打包过程的一个特定名词，也就是 chunk 是一个打包过程的概念，。**_bundle 是由 chunk 组成的，一般 bundle 和 chunk 一一对应，但是由其他配置会改变一一对应关系，也就是一个 bundle 可以对应多个 chunk。_**

## bundle

来自 webpack 词汇表的诠释：

> Produced from a number of distinct modules, bundles contain the final versions of source files that have already undergone the loading and compilation process.

bundle 是源代码的最终产物，已经经历过加载和编译过程。

## 参考资料

- [webpack 词汇表](https://webpack.js.org/glossary/)
- [What are module, chunk and bundle in webpack?](https://stackoverflow.com/questions/42523436/what-are-module-chunk-and-bundle-in-webpack)
