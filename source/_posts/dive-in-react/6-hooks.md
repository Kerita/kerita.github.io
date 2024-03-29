---
title: React Hooks 设计思想
categories: 深入浅出 React
tags: React
date: 2021-07-27
---

## 知识点：

### 为什么推出 Hooks

- 告别复杂的 class 组件
- 拆分逻辑和复用逻辑

hooks 使用原则

- 只能在函数组件或者自定义 Hooks 中调用 Hooks
- 不能在条件语句或者循环语句使用 Hooks

为什么不能在条件语句或者循环语句使用 Hooks？

以 `const [count, setCount] = useState()` 为例，当 React 内部存储 count 这个值时并没有指定一个名字存储。当下一次 render 时，React 想要重新取出 count 的值时，是从链表结构里按照执行顺序取出来。因而，为了保证执行 hooks 的准确性，React 使用链表的数据结构并顺序取值，如果在条件语句或者循环语句使用 Hooks，取值就会出错。

要解决这种办法，可以传入一个 key 作为 useState 的第二个参数，但是实现起来没那么优雅。

```
const [count, setCount] = useState(initState, key)
```

## 什么是 Hooks

Hooks 是 React 16.8 版本出现的特性，它是诸如 useState、useEffect 等一系列钩子函数。Hooks 的出现开发者在不需要写 class 组件时，也能具有 state 和其他 React 特性，函数组件从 stateless 变成 stateful。

<!-- more -->

## 为什么要有 Hooks

最大的原因就是 class 组件过于繁琐。使用 class 组件需要继承 React.component，需要在 constructor 中定义 state，需要对方法使用 bind 或者箭头函数让 this 指向组件，组件里的逻辑难以复用，等等。

Hooks 组件在部分场景可完全替换 class 组件，提升开发体验，可以从下面四个方面进行理解。

- 告别复杂的 class 组件
  class 组件中的方法，需要使用 bind 或者箭头函数让 this 指向组件，才能实现对 this 的访问。

- 实现更好的逻辑拆分
  在 class 组件中，可能会把很多不相关的初始化逻辑都放在 componentDidMount，或者把相关的订阅和取消订阅逻辑分别散落在 componentDidMount 和 componentWillUnmount。

  useEffect 则很好的实现逻辑的拆分，将相关的逻辑放在同个 useEffect，将不相关的逻辑放在不同的 useEffect。

- 实现状态复用
  使用自定义 Hooks，可以很好的实现状态逻辑的复用。例如可以很方便的定义 Modal 的状态逻辑：

  ```
  function useModal() {
  		const [modalVisible, setModalVisible] = useState(false)

      const openModal = useCallback(() => {
      	setModalVisible(true)
      }, [])

      const closeModal = uesCallback(() => {
      	setModalVisible(false)
      }, [])

      return {
      	modalVisible,
      	openModal,
      	closeModal
      }

  }
  ```

- 函数组件从设计思想上来看，更加契合 React 的理念
  如果用公式来描述 React，可以表达为 UI = render(state)。函数组件非常契合这种数据驱动思想，函数组件能更方便的访问数据和控制数据的更改。

## Hooks 不是万能的

- Hooks 还没有完全具有 class 组件的能力，getSnapshotBeforeUpdate、componentDidCatch 生命周期目前仍是缺失的
- Hooks 的使用需要时刻注意依赖问题，务必使用 eslint-plugin-react-hooks 插件进行检验，否则很容易造成死循环。

## Hooks 有两个使用原则：

- 只在 React 函数中调用 Hook；
- 不要在循环、条件或嵌套函数中调用 Hook。

## Hooks 实现

Hooks 是基于链表的结构实现，所以不要在循环、条件或嵌套函数中调用 Hook。采用链表结构为了顺序调用，按顺序完成对 `useState` 值的赋值，因为 hooks 不知道应该取出哪个值，所以采用顺序调用取出值。

## 参考资料

- [Hooks 的动机](https://zh-hans.reactjs.org/docs/hooks-intro.html)
