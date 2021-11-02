---
title: 3-浏览器详解
categories:
date: 2021-11-01
---

## 浏览器对象

<!-- more -->

- window 对象  
  1.关注 window.onerror，用于前端错误收集和上报，ps 阿里云有免费的日志服务，可以收集前端错误，上报到阿里云服务器  
  2.使用 setTimeout 替换 setInterval 用于定时器，setInterval 缺点是不能控制间隔时间，有可能浏览器重新获得焦点后会执行多次
  3.innerWidth 和 innerHeight 可以获取浏览器窗口的宽高，有些浏览器不支持，比如 IE，可以使用 document.body.clientWidth 和 document.body.clientHeight 获取

- location 对象  
  1.关注 location.href，用于获取当前页面的 url 和替换当前页面的 url，可回退  
  2.关注 location.replace，用于替换当前页面的 url，不可回退

- navigator 对象  
  1.关注 navigator.userAgent，用于获取当前浏览器的 userAgent  
  2.关注 navigator.language，用于获取当前浏览器的语言  
  3.关注 navigator.onLine，用于获取当前网络是否连接

- history 对象  
  1.关注 history.pushState，用于替换当前页面的 url，可回退  
  2.关注 history.replaceState，用于替换当前页面的 url，不可回退

## 事件模型

分为捕获阶段、目标阶段、冒泡阶段，捕获阶段是从最外层的元素开始，冒泡阶段是从最内层的元素开始。事件委托是事件模型应用的最常见场景。

- addEventListener 第三个参数 useCapture
  是否在捕获阶段触发

e.targe 属性，返回事件的目标元素
e.currentTarget 属性，绑定监听事件的元素
e.stopPropagation 阻止事件传播，不仅仅是阻止事件冒泡
e.preventDefault 阻止事件默认行为，比如默认会跳转到 href 属性的链接

## ajax 及 fetch API 详解

- 使用 XMLHttpRequest 封装一个 ajax 函数

```js
function ajax(url, options) {
  const xhr = new XMLHttpRequest();
  xhr.open(options.method, url, true);
  xhr.onreadystatechange = function () {
    if (xhr.readyState === 4) {
      if ((xhr.status >= 200 && xhr.status < 300) || xhr.status === 304) {
        options.success(xhr.responseText);
      } else {
        options.error(xhr.status);
      }
    }
  };
  if (options.method === "GET") {
    xhr.send(null);
  } else {
    xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
    xhr.send(options.data);
  }
}
```

- fetch  
  1.不会主动设置 cookie，需要自己设置，使用 credentials 属性配置  
  2.错误不会 reject，使用 response.ok 判断是否 404、500 等异常  
  3.不支持设置超时  
  4.支持 abort
