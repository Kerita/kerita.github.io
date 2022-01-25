---
title: React 小技巧
categories: 前端
tags: React
date: 2018/2/15
---

使用 React.js 一段时间了，把使用过程遇到的小坑和小技巧记录下来，希望能够帮助到其他人。

## 显示 html

```
<div dangerouslySetInnerHTML={{ __html: LANG.auth_register_tips1 }}/>
```

## 传数组给子组件

1. PureRender —— 当 porps 与 state 传入时，通过浅比较决定是否要重新渲染
2. shouldComponentUpdate() 钩子默认返回 true，可以重新

## 组件间通信

1. flux 架构

2. 父组件向子组件 —— props

3. 子组件向父组件 —— props.funciton 接收参数

4. 利用事件机制

## 高阶组件（HOC）

高阶函数，可以传入函数作为参数的函数，如 map,sort,reduce。高阶组件包装了另一个组件的组件。

1. 属性代理 （Props Proxy）
2. 反向继承 （Inheritance Inversion）

<!-- more -->

## Immutable.js

因为数据是不可变的，可以避免引用传值的问题，但也麻烦

## 无状态组件

使用无状态组件，只从父组件接收 props，可以提高组件的渲染性能

```
const HelloWorld = (props) => <div>{props.name}</div>
ReactDOM.render(<HelloWorld name="HelloWorld" />,App)
```

## componentWillReceiveProps 中取 props 的值

注意应该取 nextProps,而不是 this.props

## bind 绑定函数

利用 bind 绑定函数，是默认有 event 这个参数的，只是这个参数在给定参数之后

```
  handleClockClick (id, e) {
    console.log(id,e)
  }

 <button onClick={this.handleClockClick.bind(this, 2)}>Clock</button>
```

## 列表的 key

- key 不会传给组件，如果需要使用 key 的值，另外命名为其他属性传进去
- 当一个列表顺序会重排时，不适合使用数组的索引作为 key

## 受控组件

可变的状态保存在组件的 state 中

## ES6 计算属性名

对象的属性也可以计算，使用 [] 包围

## constructor 与 getInitialState、getDefaultProps 的区别

- getInitialState 与 getDefaultProps 在 React.createClass 时使用,此时是使用 ES5 语法
- constructor 在 ES6 类语法中使用,如果此时要设置默认 props 与 设置 state，可以如下操作

```
constructor (props) {
    super(props)
    this.state = {
    }
}

static get  defaultProps () {
    return {
        time: time
    }
}
```

## ES6 类中，函数 this 不默认指向 对象

## 获取元素

- this.getDomNode 已经在低版本被移除了，现在设置 ref=xxx，然后使用 this.refs.xxx 访问 DOM 元素
- ref 可以赋值两种类型，一种是字符串，一种是函数, 字符串只能用在类组件，DOM 元素使用函数，纯函数组件不能使用 ref。旧版本 DOM 元素虽然可以使用 ref，但是 React 已不推荐。

```
ref="test" // this.refs.test 访问

ref={test => this.test = test} // this.test 访问

```

## 组合 VS 继承

React 推荐使用组合，而不是继承，组合在 UI 来的更加直观，代码看起来也比较容易，更符合我们的认知，也符合 React component-base 的特性。

## 当只写属性名时，默认值为 true

```
<MyComponent isStock/>
// isStock 默认为 true
```

## true,false,null,undefined 与 0

- true,false,null,undefined 不会被 React 渲染，但同为 falsy 值的 0 会
- 用法,控制输出

```
<div>
{ arr.length > 0 && 'has'}
<div>

<div>
{ isVisible && <Test />}
</div>
```

## PropTypes 类型检查

React.PropTypes 已在 React v15.5

```
import PropTypes from 'prop-types'
```

## Fragment

聚合子元素列表，而不必添加额外的元素 -- 16.2.0 开始支持

```
<>
    <button> 1 </button>
    <button> 2 </button>
</>
```

## createPortal

- 将子节点挂载到父组件以外组件的方法，在 render 方法中使用，不能挂载到父组件，因为此时父组件都没有渲染好，无法获取到 DOM
- 行为上跟其他子节点没有区别，因为 React DOM 树上依然在这个组件上，包括事件冒泡等东西

```
import { createPortal } from 'react-dom'
createPortal(this.props.children, document.getElementById('portal-root'))
```

## 错误边界

componentDidCatch 错误边界，为组件定义一个父组件，父组件捕获错误，并提供回退的 UI

- 用法

```
  componentDidCatch(error, info) {
    this.setState({ hasError: true });
    console.log(error, info)
  }
```

- 无法捕获的错误
  事件处理
  异步代码 （例如 setTimeout 或 requestAnimationFrame 回调函数）
  服务端渲染
  错误边界自身抛出来的错误 （而不是其子组件）

## 高级组件就是函数

- 不应该在高阶组件修改原组件的属性
- 利用函数包裹组件，返回一个新的组件
- 为组件切换不同的数据源

1. Showcase 组件，利用 getData (Showcase, data)函数包裹，获取不同数据

- 不要在 render 中使用高阶组件
  因为每一次挂载组件，都会重新获取一个高阶组件的实例
- hoistNonReactStatic
  将原始组件的静态方法拷贝到包裹组件中

## 容器组件

- 处理数据订阅和状态管理
- 高阶组件是参数化的容器组件

## rander prop

标题相同，利用高阶组件把标题渲染到不同的组件

## React 中使用 Web component

这个时候有一点要注意的是，对于 Web component 应该使用 class,而不是 className

## lable 的 for

for 是 JS 的保留字，所以使用 htmlFor 替代 for

## style 属性

浏览器后缀除了 ms 以外，都应该以大写字母开头。这就是为什么 WebkitTransition 有一个大写字母 W。

```
const divStyle = {
  WebkitTransition: 'all', // note the capital 'W' here
  msTransition: 'all' // 'ms' is the only lowercase vendor prefix
};
```

## 在 IE11 以下使用 React16

React16 依赖集合类型 Map 和 Set，在未提供原生支持的浏览器，需要使用一个 polyfill,例如 core-js 和 babel-polyfill
使用 core-js 支持

```
import 'core-js/es6/map';
import 'core-js/es6/set';

import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

## componentDidMount 请求服务器数据

在 componentDidMount 请求服务器数据并利用 setState 时应注意，在组件卸载 componentWillUnmount 应该把去求去掉

## 参考资料

[react 进阶漫谈](https://segmentfault.com/a/1190000008356407)
[React 中文文档](https://doc.react-china.org/)
