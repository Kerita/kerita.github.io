---
title: sourceType 错误
categories:
date: 2021-08-03
---

[升级 Babel 配置过程](./replaceAll-is-not-a-function) 除了遇到 `replaceAll-is-not-a-function` 问题，还遇到关于 Babel sourceType 配置的问题。

<!-- more -->

## 报错 ES Modules 不能使用 module.exports 或者 exports.\*

![ES Modules 不能使用 `module.exports` 或者 `exports.*`](./module-type-error.png)

项目代码

![依赖包代码](./pmmmwh-code.png)

## 为什么会报错呢

之前设置 `useBuiltIns` 为 `false`，是在项目入口的最前面引入所有的 `polyfill`；而使用 `usage`，会在对应需要 polyfill 的地方引入 `polyfill`，并且 Babel 默认是以 `import` 引入 polyfill 的。

Webpack 认为有 `import` 语法的就是 ES Module，ES Module 不能有 `exports`，所以报错了。

解决办法，让 Babel 不默认使用 `import`，而是根据文件自动推断，配置 Babel `sourceType` 为 `unambiguous`。

![](./babel-sourceType.png)

## 配置优化

设置 Babel `sourceType` 为 `unambiguous` 会对所有文件都去推断，多出很多额外的工作。可以使用 `overrides` 覆盖对某个包的配置。
![overrides 配置](./babel-overrides.png)

```
    overrides: [
      {
        // 自动推断类型
        include: './node_modules/@pmmmwh',
        sourceType: 'unambiguous',
      },
    ],

```

## 参考资料

- [Babel sourceType 配置](https://babeljs.io/docs/en/options#sourcetype)
- [Babel overrides 配置](https://babeljs.io/docs/en/options#overrides)
