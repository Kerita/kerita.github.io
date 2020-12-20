---
title: z-index 不起作用
categories: 前端
tags: CSS
date: 2018/2/18
---

z-index 只在 position 非 static 的元素生效,而一个元素的 position 默认为 static，static 元素想让  z-index 生效，可以设置元素 position 为 relative。

<!-- more -->