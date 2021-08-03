---
title: React 合成事件源码阅读
categories: 源码阅读
date: 2021-08-03
---

React 合成事件是基于事件委托机制，构建的自定义事件体系。将需要监听的事件类型都收集起来放在 document 元素上，待事件触发通过 `event.target` 将事件分发给相关元素。

以下是分发时收集相关元素代码，包括两次遍历和获取父元素：

<!-- more -->

### 两次遍历

```
  function traverseTwoPhase(inst, fn, arg) {
  // 定义一个 path 数组
  var path = [];
  while (inst) {
    // 将当前节点收集进 path 数组
    path.push(inst);
    // 向上收集 tag===HostComponent 的父节点
    inst = getParent(inst);
  }

  var i;
  // 从后往前，收集 path 数组中会参与捕获过程的节点与对应回调
  for (i = path.length; i-- > 0;) {
    fn(path[i], 'captured', arg);
  }

  // 从前往后，收集 path 数组中会参与冒泡过程的节点与对应回调
  for (i = 0; i < path.length; i++) {
    fn(path[i], 'bubbled', arg);
  }
}
```

### 获取父元素

```
function getParent(inst: Fiber | null): Fiber | null {
  if (inst === null) {
    return null;
  }
  do {
    inst = inst.return;
    // TODO: If this is a HostRoot we might want to bail out.
    // That is depending on if we want nested subtrees (layers) to bubble
    // events to their parent. We could also go through parentNode on the
    // host node but that wouldn't work for React Native and doesn't let us
    // do the portal feature.
  } while (inst && inst.tag !== HostComponent);
  if (inst) {
    return inst;
  }
  return null;
}
```
