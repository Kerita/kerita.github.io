---
title: webpack Scope Hoisting 配置
categories: webpack
date: 2021-08-24
---

JavaScript 中就存在 Hoisting，将“变量声明”和“函数声明”提升到作用域顶部，Webpack 的 Scope Hoisting 也是类似的道理，将引入模块提升到当前模块声明，减少引入模块的声明，减少函数声明，缩小体积。

## 参考资料

- [Scope Hoisting 配置](https://cloud.tencent.com/developer/article/1663231#:~:text=Scope%20Hoisting%20%E6%98%AFwebpack3%20%E7%9A%84,%EF%BC%8C%E3%80%8C%E8%BF%90%E8%A1%8C%E6%9B%B4%E5%BF%AB%E3%80%8D%E3%80%82)
