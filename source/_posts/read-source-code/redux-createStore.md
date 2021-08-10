---
title: Redux createStore 参数传递的精妙之处
categories: 源码阅读
date: 2021-08-10
---

Redux createStore 是 Redux 初始化函数，在参数传递时有个有意思的实现。

判断 `preloadState` 是否为函数，如果为函数将其作为 `enhancer` 处理，并重新赋值 `preloadState` 为 `undefined`。

<!-- more -->

这样即可在不传入第二个 `preloadState` 的情况下，传入第三个参数 `enhancer`。

其实现如下：

```
function createStore(reducer,preloadedState, enhancer) {
    // 这里处理的是没有设定初始状态的情况，也就是第一个参数和第二个参数都传 function 的情况
    if (typeof preloadedState === 'function' && typeof enhancer === 'undefined') {
        // 此时第二个参数会被认为是 enhancer（中间件）
        enhancer = preloadedState;
        preloadedState = undefined;
    }
    // 当 enhancer 不为空时，便会将原来的 createStore 作为参数传入到 enhancer 中
    if (typeof enhancer !== 'undefined') {
        return enhancer(createStore)(reducer, preloadedState);
    }
		......
}
```
