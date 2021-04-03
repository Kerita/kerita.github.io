---
toc: true
title: travis-ci 构建报错
categories: 构建
tags: travis-ci
date: 2021/4/2
---

## 起因

之前博客配置了 `travis-ci` 的自动构建，昨晚写完 {% post_link 2021/event-loop %}，push 到 `GitHub` 就去睡觉了。早上起来看没有构建成功，报了以下错误：

```
The command "eval yarn --frozen-lockfile " failed.
```

<!-- more -->

我的 `.travis.yml` 并没有配置使用 `yarn` 作为依赖管理工具，结合这个 [issue](https://github.com/zoeyg/binance/issues/78#issuecomment-692523504)，猜想是 travis 默认使用 `yarn` 作为依赖管理工具了，并且执行了 `yarn --frozen-lockfile`。

## 解决办法

有了上面的猜想，我就决定在 `.travis.yml` 配置一下命令，并推到远程，构建成功。

```
install:
  - yarn
```
