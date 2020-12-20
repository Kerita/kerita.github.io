---
title: less calc 不起作用
categories: 前端
tags: ['CSS3', 'less']
date: 2018/2/28
---

在 less 中使用 CSS3 的 calc 语法时会自动计算，需要采用如下写法,注意减号左右都有空格。

```
width: calc(~"100% - 30px");
```
