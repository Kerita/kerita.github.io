---
title: word-wrap&word-break
toc: true
categories: 前端
tag: CSS3
date: 2017/7/4
---

在开发Insta360官网英文版的时候，曾遇到单词太长如何换行的问题。谷歌一下，搞定需求，但是对这两个CSS3属性还是一知半解，借着阅读《CSS3实用指南》的契机，把他们理清。

<!-- more -->

### 不指定word-wrap与work-break值
在不显式指定word-wrap和word-break属性值，并忽略从祖先元素继承值（这两个属性都可以继承），即这两个CSS属性的值都为normal时，讨论浏览器对长单词如何渲染。

1. 以汉字为代表的CJK类文字
CJK类(Chinese, Japanese, Korean and Vietnamese)文字中，每个文字都被当做一个单词，正常情况下，不存在长单词溢出或者换行问题，浏览器可以比较好的渲染
```

div {
    width: 100px;
    border: 1px solid #ccc;
}

<div>谷歌一下，搞定需求，但是对对这两个CSS3属性还是一知半解，借着阅读《CSS3实用指南》的契机，把他们理清。</div>
```
 <div style="text-align:center"><img src="http://7xpofw.com1.z0.glb.clouddn.com/not-use-cjk.png" width="300px" height="150px" alt="not-use-cjk.png"/></div>

2. 以英文为代表的latin文字

- 当出现此类文字的长单词在当前行无法放下时，浏览器在父容器范围内寻找单词中可换行点进行换行，包括‘？’或者‘-’等。
```
div {
    width: 500px;
    border: 1px solid #ccc;
}


<div> a long word   a long word  https://www.google.com.hk/search?q=CJKV&oq=CJKV&aqs=chrome..6-9i57j0l5.1919j0j1&sourceid=chrome&ie=UTF-8</div>
```
 <div style="text-align:center"><img src="http://7xpofw.com1.z0.glb.clouddn.com/not-use-url.png" width="535px" height="120px" alt="not-use-url.png"/></div>

- 当可换行点在父容器外时，在父容器外换行；当没有可换行点时，独立一行显示；如果独立一行仍放不下，溢出显示。

```
div {
    width: 100px;
    border: 1px solid #ccc;
}
<div> a long word   a long word  dddddddddddddddddddddddddd</div>
```
 <div style="text-align:center"><img src="http://7xpofw.com1.z0.glb.clouddn.com/not-use-latin.png" width="475px" height="110px" alt="not-use-latin.png"/></div>


### 使用word-wrap
word-wrap在新的标准命名为overflow-wrap，word-wrap作为一个别名，仍可使用，并且主流浏览器都支持。

word-wrap关心两个值：normal和break-word。而normal作为默认值，渲染结果可在上面知道。break-word呢，当前行且在父容器内有可换行点时换行；当前行没有可换行点时，独立一行显示；独立一行仍放不下的，在将溢出处自动换行。

- 当前行有可换行点
```
div {
        width: 200px;
        border: 1px solid #ccc;
        word-wrap: break-word;
    }

 <div> a long word  search?q=CJKV&oq=CJKV&aqs=chrome..69i57j0l5.1919j0j1&sourceid=chrome&ie=UTF-8</div>
```
 <div style="text-align:center"><img src="http://7xpofw.com1.z0.glb.clouddn.com/word-wrap-url.png" width="575px" height="160px" alt="word-wrap-url.png"/></div>
- 当前行无可换行点

```
div {
        width: 200px;
        border: 1px solid #ccc;
        word-wrap: break-word;
    }

<div> a long word  https://www.google.com.hk/search?q=CJKV&oq=CJKV&aqs=chrome..69i57j0l5.1919j0j1&sourceid=chrome&ie=UTF-8</div>
```
 <div style="text-align:center"><img src="http://7xpofw.com1.z0.glb.clouddn.com/word-wrap-longword.png" width="505px" height="200px" alt="word-wrap-longword"/></div>


 ### 使用word-break
work-break关心三个值：normal,break-all,keep-all。normal的效果上面可见。

- break-all
看到一个好的例子来解释这个属性就是：资本家总是极尽可能的压榨工人，break-all就是极尽可能的利用所有空间，不另起一行，且在每一行行在将溢出处换行。
```
 div {
        width: 200px;
        border: 1px solid #ccc;
        word-break: break-all;
    }
 <div> a long word  https://www.google.com.hk/search?q=CJKV&oq=CJKV&aqs=chrome..69i57j0l5.1919j0j1&sourceid=chrome&ie=UTF-8</div>
```
 <div style="text-align:center"><img src="http://7xpofw.com1.z0.glb.clouddn.com/keep-all.png" width="590px" height="165px" alt="break-all"/></div>

- keep-all
keep-all就是在normal的基础上，让CJK文字也按溢出显示。同时也会让一些中文标点符号是做可换行点，且一些符号如《》还必须同行显示。
```
div {
    width: 200px;
    border: 1px solid #ccc;
    word-break: keep-all;
}
<div>谷歌一下，搞定需求，但是对对这两个CSS3属性还是一知半解，借着阅读啦啦啦啦《CSS3实用指南》的契机，把他们理清。</div>
```
 <div style="text-align:center"><img src="http://7xpofw.com1.z0.glb.clouddn.com/keep-all.png" width="535px" height="175px" alt="keep-all"/></div>

 ### 同时使用

 - word-wrap:break-word;与word-break:break-all;
 这个时候就是不溢出，不另起一行，随处换行。

 - word-wrap:break-word;与word-break:break-all;
不溢出，另起一行，中文标点符号成为成为可换行符。



### 参考链接

- [你真的了解word-wrap和word-break的区别吗？](http://www.cnblogs.com/2050/archive/2012/08/10/2632256.html)

- [word-wrap——MDN](https://developer.mozilla.org/de/docs/Web/CSS/word-wrap)

- [word-break——MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/word-break)

- [overflow-wrap——MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow-wrap)


