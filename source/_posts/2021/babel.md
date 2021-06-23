---
title: 什么是 babel？
categories: 前端
toc: true
tags: 工程化
date: 2021/6/24
---

## 什么是 babel

babel 对自己的定位：下一代 JavaScript 的编译器。它将新语法、新 API 编译成兼容代码，以便在老版本的浏览器也能使用。

<!-- more -->

babel 基于插件架构，如果什么插件都不提供，babel 也不做什么事情，其作用如下。

```
const babel = code => code
```

## babel 配置

可以在项目根目录使用 .babelrc(.js), babel.config.json, babel.config.js 进行配置。

```
module.exports = (api) => {
  // 缓存配置
  api.cache(true);

  return {
		// 箭头函数转换插件
    plugins: ["@babel/plugin-transform-arrow-functions"],
  };
};
```

## @babel/polyfill

```
/* test.js */
const fn = () => {}
new Promise(() => {})


/* test-compiled.js */
var fn = function fn() {};
new Promise(function () {});
```

上面的配置生成的代码中，Promise 并没有并转换。难道 IE 8 支持 Promise？

不是的，Promise 是新的 API 而不是新的语法，无法被 transform，只能被 polyfill，因此在项目里引入 @babel/polyfill。

但是此时会全量引入 @babel/polyfill，因而在 babel@7.4.0 版本已经被废弃，而是使用 corejs，可以使用 @babel/preset-env 的 useBuiltIns 配置配合 corejs，实现按需引入。

## Plugins 和 Presets

JS 有非常多新的语法和 API，如果一个个添加非常麻烦。因而，babel 提供了很多 presets，presets 就是插件合集，方便进行配置。

```
@babel/preset-env for compiling ES2015+ syntax
@babel/preset-typescript for TypeScript
@babel/preset-react for React
@babel/preset-flow for Flow
```

因而，配置文件变成

```
module.exports = (api) => {
  // 缓存配置
  api.cache(true);

  return {
    plugins: ["@babel/plugin-transform-arrow-functions"],
    presets: ["@babel/preset-env"],
  };
};

```

## @babel/preset-env

由上面可知，preset-env 可帮助我们转换 ES6 代码，同时我们可以使用 target 来配置指定的运行环境。

```
module.exports = (api) => {
  // 缓存配置
  api.cache(true);

  return {
    plugins: ["@babel/plugin-transform-arrow-functions"],
    presets: [
			["@babel/preset-env", {
      "targets": "IE >= 8"
    	}]
		],
  };
};

```

## useBuiltIns

@babel/preset-env 配置 useBuiltIns，决定如何处理 polyfill。

有三个配置项 entry, usage, false(默认值)。

```
module.exports = (api) => {
  // 缓存配置
  api.cache(true);
	// 配置为 entry/usage时，需要制定 corejs 版本
  return {
    presets: [
      [
        "@babel/preset-env",
        {
          targets: "IE >= 8",
          useBuiltIns: "usage",
          corejs: { version: "3.15", proposals: true },
        },
      ],
    ],
  };
};
```

- entry
  entry 需要在项目入口引入 polyfill，生成的代码也会引进对应的 polyfill

引入

```
import "core-js/es/array";
import "core-js/proposals/math-extensions";
```

输出(取决于环境)

```
import "core-js/modules/es.array.unscopables.flat";
import "core-js/modules/es.array.unscopables.flat-map";
import "core-js/modules/esnext.math.clamp";
import "core-js/modules/esnext.math.deg-per-rad";
import "core-js/modules/esnext.math.degrees";
import "core-js/modules/esnext.math.fscale";
import "core-js/modules/esnext.math.rad-per-deg";
import "core-js/modules/esnext.math.radians";
import "core-js/modules/esnext.math.scale";
```

- usage
  usage 则会扫描所有代码，只引入需要的 polyfill
  输入

  ```
  const fn = () => {

  console.log("test");
  };

  	new Promise(() => {});
  ```

  输出

  ```
  "use strict";

  require("core-js/modules/es.object.to-string.js");

  require("core-js/modules/es.promise.js");

  var fn = function fn() {
  	console.log("test");
  };

  new Promise(function () {});
  ```

- false
  不为每个文件自动添加 polyfill，也不将 import "core-js" 或 import "@babel/polyfill" 转换为单个 polyfill。

```

```
