---
title: .npmrc 与 npm config 命令
categories: 前端
toc: true
tags: npm
date: 2021/3/29
---

# .npmrc 是什么

.npmrc 是 npm 的配置文件。当运行 npm 命令时，会从 .npmrc 文件读取相关配置。

对于中国开发者，最常见的 .npmrc 配置是设置淘宝源，加快 npm 包的下载速度。

```jsx
registry=https://registry.npm.taobao.org/
```

<!-- more -->

## .npmrc 文件位置

我们可以在四个路径配置和编辑 .npmrc 文件

- 项目根目录(/path/to/my/project/.npmrc)
- 用户目录(~/.npmrc)
- 全局目录($PREFIX/etc/npmrc)
- npm 目录(/path/to/npm/npmrc)

## .npmrc 优先级

项目 .npmrc 文件 > 用户级 .npmrc 文件> 全局级 .npmrc 文件 > npm 内置的 .npmrc 文件

## .npmrc 文件格式

npmrc 文件是 `key = value` 格式，可以通过 `npm config` 命令进行配置。npmrc 文件中，以 `;` 或者`#` 卡头的语句会被解析为注释。

# npm config 命令

我们可以通过 npm config 命令管理 npm 的配置，默认更改的是用户目录下的 .npmrc 文件。加上 -g/—global 参数，更改的则是全局目录下的 .npmrc 文件。n'p'm

```
npm config set <key> <value> [-g|--global]
npm config get <key>
npm config delete <key>
npm config list [-l] [--json]
npm config edit
npm get <key>
npm set <key> <value> [-g|--global]
```
