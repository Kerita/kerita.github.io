---
title: webpack 优化策略
categories: webpack
date: 2021-09-15
---

优化 webpack 配置，提高打包速度，减少打包体积。

## 一些插件

- DLL
- moment-locales-webpack-plugin
- mini-css-extract-plugin
- thread-loader

## loader

- image-webpack-loader
  压缩图片
- url-loader
  将图片转出 base64

## babel

- babel-import-plugin

## 模块使用

- lodash-es

## 配置

- cache
- sourcemap

## 参考资料

- [Optimize your libraries with webpack](https://github.com/GoogleChromeLabs/webpack-libs-optimizations)
