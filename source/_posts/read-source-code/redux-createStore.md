---
title: Redux createStore 源码
categories: 源码阅读
date: 2021-08-10
---

## 参数传递

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

## subscribe 与 dispatch

Redux 是一个单向的数据流框架，使用“发布-订阅”模式。当 state 发生变化时，就会执行订阅函数，Redux createStore 中暴露出来最常用的也是这两个函数 subscribe 和 dispatch。当然，当使用 react-redux 时，react-redux 将 subscribe 变成透明的，并做优化。

![Store 暴露出来的变量其实很简单](./createStore-store.png)

```
// subscribe 订阅方法，它将会定义 dispatch 最后执行的 listeners 数组的内容
    function subscribe(listener) {
        // 校验 listener 的类型
        if (typeof listener !== 'function') {
          throw new Error('Expected the listener to be a function.')
        }
        // 禁止在 reducer 中调用 subscribe
        // 该变量的修改在 dispatch 中，reducer 执行前设置为 true，reducer 执行后设置为 false，保证不会在 reducer 中新增订阅
        if (isDispatching) {
          throw new Error(
            'You may not call store.subscribe() while the reducer is executing. ' +
              'If you would like to be notified after the store has been updated, subscribe from a ' +
              'component and invoke store.getState() in the callback to access the latest state. ' +
              'See https://redux.js.org/api-reference/store#subscribe(listener) for more details.'
          )
        }
        // 该变量用于防止调用多次 unsubscribe 函数
        let isSubscribed = true;
        // 确保 nextListeners 与 currentListeners 不指向同一个引用
        ensureCanMutateNextListeners();
        // 注册监听函数
        nextListeners.push(listener);

        // 返回取消订阅当前 listener 的方法
        return function unsubscribe() {
            if (!isSubscribed) {
                return;
            }
            isSubscribed = false;
            ensureCanMutateNextListeners();
            const index = nextListeners.indexOf(listener);
            // 将当前的 listener 从 nextListeners 数组中删除
            nextListeners.splice(index, 1);
        };
    }

    // 定义 dispatch 方法，用于派发 action
    function dispatch(action) {
        // 校验 action 的数据格式是否合法
        if (!isPlainObject(action)) {
          throw new Error(
            'Actions must be plain objects. ' +
              'Use custom middleware for async actions.'
          )
        }

        // 约束 action 中必须有 type 属性作为 action 的唯一标识
        if (typeof action.type === 'undefined') {
          throw new Error(
            'Actions may not have an undefined "type" property. ' +
              'Have you misspelled a constant?'
          )
        }

        // 若当前已经位于 dispatch 的流程中，则不允许再度发起 dispatch（禁止套娃）
        if (isDispatching) {
          throw new Error('Reducers may not dispatch actions.')
        }
        try {
          // 执行 reducer 前，先"上锁"，标记当前已经存在 dispatch 执行流程
          isDispatching = true
          // 调用 reducer，计算新的 state
          currentState = currentReducer(currentState, action)
        } finally {
          // 执行结束后，把"锁"打开，允许再次进行 dispatch
          isDispatching = false
        }

        // 触发订阅
        const listeners = (currentListeners = nextListeners);
        for (let i = 0; i < listeners.length; i++) {
            const listener = listeners[i];
            listener();
        }
        return action;
    }
```

## getState

- getState 利用闭包机制获取当前最新的 state
- 其他地方 dispatch、subscribe 里当然也有用到闭包，只是对于开发者来说是透明的，没有感知的

```
    // 记录当前的 state
    let currentState = preloadedState;

    ......
    // 返回当前的 state
    function getState() {
        return currentState;
    }

```
