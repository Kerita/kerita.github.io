---
title: 前端模块化与模块加载器
toc: true
categories: 前端
tag: 模块化
date: 2017/6/12
---
前端模块化这个概念自从去年开始一直出现在视野里，在某次面试的时候还被问傻眼了，但都整理这方面的知识，这一次决定彻底清楚。跑题了，回到正题。模块化是啥？简单来说，前端JS文件越来越多，而且相互之间还存在着依赖关系，利用模块化可以更好地管理和加载这些JS文件。
<!--more-->

本文主要是对前端模块化common.js,AMD,CMD和模块加载器require.js,sea.js和webpack进行梳理。
## common.js,AMD,CMD
 
 这三个东西都是模块化的规范，主要规定怎么组织模块和如何引入模块，区别如下：
 
- common.js:common.js通过require同步加载所有模块，通过exports或module.exports来导出需要暴露的接口，服务器端的Node.js遵循这种规范。
```
require("module");
require("../file.js");
exports.doStuff = function() {};
module.exports = someValue;
```
- AMD:服务器端的资源都是在本地磁盘，使用同步加载没有什么问题，但是浏览器不能这样，假如文件过大，会一直处于加载状态，浏览器进入“假死”状态。所以就出现了AMD这种适用于浏览器端的异步加载的模块化标准，require.js这个模块加载器就是这种规范的实现。
```
define("module", ["dep1", "dep2"], function(d1, d2) {
  return someExportedValue;
});
require(["module", "../file"], function(module, file) { /* ... */ });
```
 
- CMD：与AMD一样，CMD也是一个用于浏览器的模块加载器，不同之处在于，AMD会一口气把需要的模块加载出来，而CMD则是用到时再加载。同时呢，CMD与common.js的规范保持很大的兼容，sea.js这种模块加载器就是这种规范的实现。
```
define(function(require, exports, module) {
  var $ = require('jquery');
  var Spinning = require('./spinning');
  exports.doSomething = ...
  module.exports = ...
})
```
 
## require.js，sea.js与webpack
 
如上面所言，require.js与sea.js是模块加载器，webpack相比较下，更像是模块加载器+gulp/grunt，同时更具备多种优点，例如可以对图片、css进行打包、兼容AMD、CMD、common.js、ES6格式的模块，通过强大的插件系统更能实现各种强大的功能。
 
webpacke重要的两个组成——loader和插件，loader更针对某一类型文件，插件更像是在整个打包过程起作用。详细学习webpack，可以看 [https://github.com/Kerita/webpack-tutorial](https://github.com/Kerita/webpack-tutorial)
 
- loader: 用于加载各种文件——css,less,vue,jsx，图片等
 
- 插件：开启服务器、实现热加载等功能。
 
 
## 小结
 
common.js,AMD,CMD是模块化规范，require.js,sea.js,webpack模块加载器，现在比较流行是使用webpack构建项目，React和Vue.js官方脚手架都是采用这种方式。
 
 
 
 
 
 
 
 
 
 
 
 
 