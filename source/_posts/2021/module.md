---
title: CommonJS 与 ES6 Module 的区别
categories: 前端
toc: true
tags: 模块化
date: 2021/4/5
---

JavaScript 起初只是用来做页面的的简单交互，随着 Web 应用的复杂性越来越高，维护成本越来越大，模块化标准也在 ES6 版本应运而生。当然，在 ES6 Module 出现之前，社区在使用 Node.js 的过程中，也形成了适合 Node.js 的 CommonJS 模块标准。

<!-- more -->

基本小时候我们都玩过积木，积木暴露出它的接口，我们使用积木暴露的接口，构造我们想要的东西。积木里面的构造是怎样，我们并不能知道。模块亦是如此，模块暴露出变量，我们引用暴露出来的变量，构造我们的应用。

## CommonJS 标准

---

#### 导出

有两种导出方式，但最好不要混用。若使用逐个导出后，又使用全部导出，逐个导出的变量将全都被覆盖。因为导出代码的逻辑如下，实质是将 `module.exports` 赋值给 `exports`。

```
const module = {
	exports = {}
}

const exports = module.exports
```

1.全部导出

```
module.exports = {}
```

2.逐个导出

```
exports.{variableName} = {variableValue}
```

#### 导入

导出的是一个对象，CommonJS 导入是这个对象的拷贝值，当导出对象发生变化，导入的值也不会改变。我们可以使用如下语法进行导入：

```
const calculator = require('./calculator)

const { add } = require('./calculator)
const { sum } = require('./calculator)
```

## ES6 Module

---

ES6 Module 也有两种导出方式——默认导出和命名导出，二者可以混用。命名导出即导出的变量都有一个名字，导入的时候用这个名字就能找到它，默认导出其实是一种特殊的命名导出，它的变量名是 `default`，直接导入时就会导入 `default` 这个变量。命名导出只能在变量声明就导出，默认导出则无需这样。

1.默认导出

```
export default variableName
```

2.命名导出

```
// 逐个命名导出
export const / let variableName

// 大括号一起命名导出，推荐写法，可以方便知道模块导出那些变量
export {
	variableName1,
	variableName2
}
```

#### 导入

对于默认导出和命名导出，导入如下。`React`为默认导出变量，直接导入即可；`Component`为命名导出变量，需要使用大括号导入。导入时，若同时存在，默认导出变量需要在命名导出变量之前。

我们也可使用 `import *` 语法导入所有导出变量，并作为对象赋予一个变量名。

```
import React, { Component } from 'react'

import * as AllReact from 'react'
```

## CommonJS 与 ES6 Module 的区别

---

#### 动态和静态

CommonJS 对于模块间依赖的建立发生在代码运行阶段，我们可以在代码运行的过程，再确定是引入模块 A 还是模块 B。

ES6 Module 对于模块间依赖的建立是在代码编译阶段，只能够在模块顶层作用域导入、导出。

ES6 Module 依赖关系的确定性有助与死代码的检测和排除，静态分析工具可以检测使用未被调用的模块和接口，并在打包时剔除，有助于减小打包资源体积。

#### 值拷贝与动态映射

CommonJS 导入的是导出值的拷贝，但导出值变化时，到导入值不会改变；而 ES6 Module 则是动态映射，会随着导出值的改变而变。

笔者在项目中使用过该特性，定义一个常量模块 `Constant`，其他文件引用这个常量文件。从接口获取到用户配置的常量，并修改 `Constant` 的值，如 `Constant.A`。
