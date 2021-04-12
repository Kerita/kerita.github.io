---
title: 奇妙的 var,function,let
categories: 前端
toc: true
tags: JS
date: 2021/4/12
---

## var 与 function

- var,function 不存在块作用域
- var, function 声明时会有变量提升,function 变量提升会提到最前面（块作用域定义除外），并且初始化，var 也会提升，但赋值为 undefined
<!-- more -->

```
console.log(v) // undefined
{
	var v = 'v'
}

console.log(f1) // ƒ f() {}
function f1() {}

console.log(f2) // undefined
{
	function f2() {}
}

```

## let

- let 存在块作用域，定义前不允许访问
- 若 let 与 var 存在同个作用域，会报错
- 若 let 与 function 存在同个作用域，会报错；除非二者中有且只有一个，位于块作用域中；此时谁声明在块作用域内访问块作用域的，块作用域外访问块作用域外的

```
		let l = 'l'

		{
			console.log(l) // ƒ l() {}
			function l() {}
			console.log(l) // ƒ l() {}
		}

		console.log(l) // l
```
