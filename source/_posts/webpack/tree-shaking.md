---
title: Webpack Tree Shaking 配置
categories: webpack
date: 2021-08-17
---

Tree Shaking 翻译过来就是“摇树”。我们可以想象一下，对着一棵梨树的树干摇一摇，树上成熟的梨子就会掉下来。webpack 使用 Tree Shaking 处理代码，结合 ES6 模块静态引入依赖关系确定的特点，对代码进行静态分析，将那些没有用到的代码（Dead Code）“摇出来”——删掉。

<!-- more -->

Tree Shaking 是 Dead Code Elimination （无用代码消除技术）的一种实现形式。Tree Shaking 依赖于 ES6 模块特性，在 ES6 模块出现之前，主要使用 Uglify 来对 JavaScript 代码进行 DCE。Uglify 的缺点是不会跨文件 做 DCE，所以对于已定义却没有引用的模块代码，无法处理。因而，Tree Shaking 也应运而生。
