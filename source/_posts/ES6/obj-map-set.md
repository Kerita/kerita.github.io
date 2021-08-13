---
title: Object，Map，Set 区别
categories: ES6
date: 2021-08-13
---

## Object

Object 是 key-value 的数据结构，与 JSON 结构一样。[点击链接可查看以下示例](https://codesandbox.io/s/object-nku94?file=/index.html:659-691)

- 记录器
  有时候我们也把 Object 当做一个记录器，例如记录某个列表的状态。

```
      const list = [
        {
          id: 1
        },
        {
          id: 2
        }
      ];

      const obj = {};

      list.forEach((item) => {
        obj[item.id] = item.id > 1 ? true : false;
      });

			console.log(obj); // {1: false, 2: true}
```

<!-- more -->

- Object 的 key 只能为原型类型
  如果将引用类型作为 Object 的 key，会自动调用该引用类型的 toString() 方法转为字符串。

  ```
      console.log(obj);

      console.log(Object.keys(obj)); // {1: false, 2: true, [object Object],[object Object]: 1}

  ```

- Object.keys()
  Object 的静态方法，将传入的 obj 的 key 放到同一个数组。

```
console.log(Object.keys(obj)); // ["1", "2"]
```

- Object.values()
  Object 的静态方法，将传入的 obj 的 value 放到同一个数组。

```
console.log(Object.values(obj)); // [false, true]
```

## Map（字典）

Map 是 key-value 结构，key 可以是任何类型的值。

操作方法：

- set(key, value)：向字典中添加新元素
- get(key)：通过键查找特定的数值并返回
- has(key)：判断字典中是否存在键 key
- delete(key)：通过键 key 从字典中移除对应的数据
- clear()：将这个字典中的所有元素删除

遍历方法：

- keys()：将字典中包含的所有键名以迭代器形式返回
- values()：将字典中包含的所有数值以迭代器形式返回
- entries()：返回所有成员的迭代器
- forEach()：遍历字典的所有成员

## WeakMap

key 是弱引用，即 value 是正常引用。但没有其他地方引用 key，垃圾回收机制就会将 key 回收。WeakMap 是不可枚举的。

操作方法：

- has(key)：判断是否有 key 关联对象
- get(key)：返回 key 关联对象（没有则则返回 undefined）
- set(key)：设置一组 key 关联对象
- delete(key)：移除 key 的关联对象

## Set（集合）

- 成员唯一、无序且不重复。
- [value, value]，键值与键名是一致的（或者说只有键值，没有键名）
- 可以遍历，操作方法有：add、delete、has

遍历方法：

- keys()：返回一个包含集合中所有键的迭代器
- values()：返回一个包含集合中所有值得迭代器
- entries()：返回一个包含 Set 对象中所有元素得键值对迭代器
- forEach(callbackFn, thisArg)：用于对集合成员执行 callbackFn 操作，如果提供了 thisArg 参数，回调中的 this 会是这个参数，没有返回值

## WeakSet

- 成员都是对象
- 成员都是弱引用，可以被垃圾回收机制回收，可以用来保存 DOM 节点，不容易造成内存泄漏
- 不能遍历，方法有 add、delete、has

## 使用场景

- Map 与 WeakMap
  Map 可以提供任何值的映射，是更完美的 hash 结构，例如要映射数组对应的值，Object 满足不了，可使用 Map。

  WeakMap 的 key 只能为引用，不再其他地方引用就会回收。下面把 DOM 作为 key，DOM 消失监听函数也会消失。

```
// 代码1
ele1.addEventListener('click', handler1, false);
ele2.addEventListener('click', handler2, false);

// 代码2
const listener = new WeakMap();

listener.set(ele1, handler1);
listener.set(ele2, handler2);

ele1.addEventListener('click', listener.get(ele1), false);
ele2.addEventListener('click', listener.get(ele2), false);
```

- Set 与 WeakSet
  Set 与 WeakSet 可以用展开语法，实现数组去重。当然 WeakSet 的值只能为引用类型。

```
var set = new Set([1, 2, 3, 4, 4]);
[...set]
// [1, 2, 3, 4]
```

## 参考资料

- [前端面试题之 Set,Map 的区别](https://zhuanlan.zhihu.com/p/81234278)
