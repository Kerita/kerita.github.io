---
title: webpack hash, chunkhash, contenthash 区别
categories: webpack
date: 2021-08-23
---

当我们对 webpack output 的 filename 和 chunkFilename 配置时，使用合理的 hash 值有利于浏览器的缓存，减少二次加载时的文件数量。

filename 是对打包后 bundle 名称进行配置，chunkFilename 是对切割出来的 chunk 名称进行配置。

<!-- more -->

## hash

hash 与整个项目的构建相关，设置为 hash 时，所有 bundle 与 chunk 使用相同的 hash。只要某一个文件发生改变，hash 就会发生改变。

## chunkhash

chunkhash 计算与 bundle 内容相关，只要其中一个 chunk 内容发生变化，chunkhash 就会发生变化。

## contenthash

contenthash 只与与文件本身内容相关。
