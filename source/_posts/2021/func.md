---
title: 什么是函数式编程
categories: React
date: 2021-07-25
---

## 什么是函数式编程

函数式编程是一种编程范式。编程范式是基于程序语言的特点对程序语言进行分类的一种方式，常见的编程范式有：函数式编程、指令式编程、过程式编程、面向对象编程等等。

在面向对象编程中，程序则是一系列相互作用的对象，由于方法论的不同，面向对象编程范式又分为基于类编程和基于原型编程。

函数式编程的理论基础 Lambda 演算。Lambda 演算是一种数学的抽象，是研究函数如何抽象定义、函数如何被引用以及递归的形式系统。一个函数式编程程序会被看作是一个无状态的函数计算的序列，正如函数关心的是数据的映射，函数式编程也是如此。

<!-- more -->

## 函数式编程的特点

函数式编程具有 5 个鲜明的特点。  
1.函数是“第一等公民”  
“第一等公民”是指函数可以当做参数传递、可以当做其他函数的返回值、可以传递给变量或者可以存放在数据结构中。

下面使用 Lambda 表达式定义的匿名函数赋值给变量 `a`。

```
const a = () => {}
```

2.只用“表达式”，不用“语句”  
“语句”表示执行某种操作，“表达式”表示运算的过程，并且有返回值。

3.没有副作用
函数要保持独立，所有功能就是返回一个新的值，没有其他行为，尤其是不得修改外部变量的值。

4.不修改状态  
函数式编程只是返回新的值，不修改系统变量。因此，函数式编程通过参数传递状态不修改参数，也是它的一个重要特点。

5.引用透明
只依赖于输入的参数，任何时候只要参数相同，引用函数所得到的返回值总是相同的。

## React 和函数式编程有什么关系

- React 数据驱动视图的思想可以当做一种函数式编程
  React 的 state 是函数的参数，view 是函数的输出，只要 state 相同，view 就相同。

  下面的无状态函数组件提现了这个风格，视图的展示只与 count 值有关。

  ```
  function Counter({
  	count
  }) {
  	return <div>{count}</div>
  }
  ```

- 使用函数式编程思想进行缓存
  函数引用透明，参数相同返回就相同。React 利用这个特性，将参数与输出结果作为键值对缓存起来。当参数一样时，无需再次计算，直接返回之前计算的结果。

## 参考资料

- [函数式编程初探](https://www.ruanyifeng.com/blog/2012/04/functional_programming.html)
- [函数式编程](https://zh.wikipedia.org/wiki/%E5%87%BD%E6%95%B0%E5%BC%8F%E7%BC%96%E7%A8%8B)
- [Lamda 演算](https://zh.wikipedia.org/wiki/%CE%9B%E6%BC%94%E7%AE%97#%E9%9D%9E%E5%BD%A2%E5%BC%8F%E5%8C%96%E7%9A%84%E7%9B%B4%E8%A6%BA%E6%8F%8F%E8%BF%B0)
- [函数式编程在 Redux/React 中的应用](https://tech.meituan.com/2017/10/12/functional-programming-in-redux.html)
