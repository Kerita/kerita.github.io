---
title: 什么是 JSX
categories: 深入浅出 React
date: 2021-07-23
---

在使用 React 开发项目的过程，我们都会使用 JSX 来描述 UI。今天我们就来聊聊什么是 JSX。

<!-- more -->

## 什么是 JSX

根据 [React 官网](https://reactjs.org/docs/introducing-jsx.html)介绍 JSX 是 JavaScript 的语法拓展，它看起来像是模板语言，但拥有 JavaScript 的全部能力。解释一下就是：

- 可以使用类 HTML 语法和 JavaScript 语法来描述 UI
- 每个类 HTML 标签最终都将被转换为使用 JavaScript 语句 React.createElement。React.createElement 第一个参数为改标签类型，第二个参数为传递给它的属性，第三个及之后的元素为它的子标签。
- JSX 是 React.createElement 的语法糖，打包过程中通过 [@babel/plugin-transform-react-jsx](https://github.com/babel/babel/blob/main/packages/babel-plugin-transform-react-jsx/src/create-plugin.ts) 成 React.createElement

下面我们举个例子，读者可使用 [Babel 编译器](https://babeljs.io/repl#?browsers=Chrome%2069&build=&builtIns=false&corejs=3.6&spec=false&loose=false&code_lz=MYewdgzgLgBAhjAvDAFAHgCYEsBuA-AKwgA80B6bfASiA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=false&presets=env%2Creact&prettier=false&targets=&version=7.14.8&externalPlugins=) 进行实验。

```
// 一段 JSX
const a = (<div>jsx</div>)

// 使用 Babel 编译后
const a = /*#__PURE__*/React.createElement("div", null, "jsx");
```

## 为什么要使用 JSX

JSX 只是 React.createElement 的语法糖，所以可以直接使用 React.createElement 来描述 UI。但使用 React.createElement 来描述 UI 不够直观清晰，写法冗长，效率不够高。所以实际项目开发过程，我们一般使用 JSX。

```
// 使用 JSX
<div>
	<h2><span className="test">1</span></h2>
	<h2><span className="test">2</span></h2>
	<h2><span className="test">3</span></h2>
	<h2><span className="test">4</span></h2>
	<h2><span className="test">5</span></h2>
	<h2><span className="test">6</span></h2>
</div>

// 使用 React.createElement
/*#__PURE__*/
React.createElement("div", null, /*#__PURE__*/React.createElement("h2", null, /*#__PURE__*/React.createElement("span", {
  className: "test"
}, "1")), /*#__PURE__*/React.createElement("h2", null, /*#__PURE__*/React.createElement("span", {
  className: "test"
}, "2")), /*#__PURE__*/React.createElement("h2", null, /*#__PURE__*/React.createElement("span", {
  className: "test"
}, "3")), /*#__PURE__*/React.createElement("h2", null, /*#__PURE__*/React.createElement("span", {
  className: "test"
}, "4")), /*#__PURE__*/React.createElement("h2", null, /*#__PURE__*/React.createElement("span", {
  className: "test"
}, "5")), /*#__PURE__*/React.createElement("h2", null, /*#__PURE__*/React.createElement("span", {
  className: "test"
}, "6")));
```
