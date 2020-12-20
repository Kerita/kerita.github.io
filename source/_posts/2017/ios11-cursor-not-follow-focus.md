---
title: iOS11 光标不跟随焦点
categories: 前端
tag: iOS
date: 2017/12/3
---

最近遇到一个新鲜的 bug —— iOS11 Safari 中 modal 上的 input 光标不跟随焦点，即当 input 获得焦点准备输入时，光标并不在 input 元素中。

<!-- more -->

之所以会有这个 bug 的原因是因为，当输入框获取焦点弹出输入法时，，Safari 向下移动页面，导致光标不跟随焦点。

谷歌搜索看到[这篇文章（需翻墙）](https://hackernoon.com/how-to-fix-the-ios-11-input-element-in-fixed-modals-bug-aaf66c7ba3f8),了解到三种解决办法。

- 不要讲 input 放在 modal，这种方法简单粗暴，但是可行性却很低。

- 将 modal 中 mask 的兄弟元素且为 input 祖先元素的元素 position 设置为 absolute。可能会导致一些意外问题，具体看 modal 的写法。 <a href="#position-absolute">代码</a>

- 将 body 高度设置为 100vh, overflow 设置为 hidden，当然这种方法在 modal 消失需要重设这两个属性为原来的值。但如果 modal 高度gaoyu 100vh时，这种方法就无效了。<a href="#height-100vh">代码</a>


### 参考链接
[How to fix the iOS 11 input element in fixed modals bug](https://hackernoon.com/how-to-fix-the-ios-11-input-element-in-fixed-modals-bug-aaf66c7ba3f8)

<a id="position-absolute"></a>
```
<!DOCTYPE html>
<html>
  <head>
    <title>iOS11 cursor</title>
    <meta name="viewport" content="width=device-width">
  </head>
  <style>

    .ios11 .modal-ct{
      position: absolute;
    }

    
    body {
      height: 200vh;
    }
    .modal {
    }

    .mask {
      background: black;
      opacity: 0.3;
      position: fixed;
      left: 0;
      top: 0;
      right: 0;
      bottom: 0;
    }
    .modal-ct {
      position: fixed;
      left: 0;
      top: 0;
      right: 0;
      bottom: 0;
    }
    input {
      font-size: 16px;
    }
  </style>
  <body>
    
    <div class="modal">
      <div class="mask"></div>
        <div class="modal-ct">
            <input />
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
        </div>
    </div>
    <div id="other">
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. Atque dolorem nam, in optio magni expedita corporis, labore veritatis delectus eaque ipsum aperiam ratione incidunt mollitia? Numquam, quos fugiat! Odit, nobis?
        
            Lorem ipsum dolor sit, amet consectetur adipisicing elit. Assumenda, vel adipisci libero quae sint iusto dignissimos quam quibusdam molestiae sunt dolore soluta nihil cumque sit? Quidem accusamus est ad iure.
        
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
    </div>

    <script>
      (function () {
        var ua = navigator.userAgent,
        iOS = /iPad|iPhone|iPod/.test(ua),
        iOS11 = /OS 11_0_1|OS 11_0_2|OS 11_0_3|OS 11_1/.test(ua);
        // ios 11 bug caret position
        if (iOS && iOS11) {
          document.body.setAttribute('class', 'ios11')
        }
      })()
    </script>
  </body>
</html>
```

<a id="height-100vh"></a>
```
<!DOCTYPE html>
<html>
  <head>
    <title>iOS11 cursor</title>
    <meta name="viewport" content="width=device-width">
  </head>
  <style>
    
    body {
      height: 200vh;
    }

    .ios11 {
      height: 100%;
      overflow: hidden;
    }
    .modal {
    }

    .mask {
      background: black;
      opacity: 0.3;
      position: fixed;
      left: 0;
      top: 0;
      right: 0;
      bottom: 0;
    }
    .modal-ct {
      position: fixed;
      left: 0;
      top: 0;
      right: 0;
      bottom: 0;
      padding-top: 100px;
    }
    input {
      font-size: 16px;
    }
    #other {
      display: none;
    }
  </style>
  <body>

    <div class="modal">
      <div class="mask"></div>
        <div class="modal-ct">
            <input />
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
            <p>lorem</p>
        </div>
    </div>
    <div id="other">
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. Atque dolorem nam, in optio magni expedita corporis, labore veritatis delectus eaque ipsum aperiam ratione incidunt mollitia? Numquam, quos fugiat! Odit, nobis?
        
            Lorem ipsum dolor sit, amet consectetur adipisicing elit. Assumenda, vel adipisci libero quae sint iusto dignissimos quam quibusdam molestiae sunt dolore soluta nihil cumque sit? Quidem accusamus est ad iure.
        
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
    </div>

    <script>
      (function () {
        var ua = navigator.userAgent,
        iOS = /iPad|iPhone|iPod/.test(ua),
        iOS11 = /OS 11_0_1|OS 11_0_2|OS 11_0_3|OS 11_1/.test(ua);
        // ios 11 bug caret position
        if (iOS && iOS11) {
          document.body.setAttribute('class', 'ios11')
        }
      })()
    </script>
  </body>
</html>
```
