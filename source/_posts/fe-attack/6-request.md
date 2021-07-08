---
title: 网络请求
categories: 前端进击笔记
toc: true
tags: Ajax
date: 2021/7/6
---

## 输入一个 URL 敲下回车键发生了什么

1.DNS 域名解析（此处涉及 DNS 的寻址过程），找到网页的存放服务器；

2.浏览器与服务器建立 TCP 连接；

3.浏览器发起 HTTP 请求；

4.服务器响应 HTTP 请求，返回该页面的 HTML 内容；

5.浏览器解析 HTML 代码，并请求 HTML 代码中的资源（如 JavaScript、CSS、图片等，此处可能涉及 HTTP 缓存）；

6.浏览器对页面进行渲染呈现给用户（此处涉及浏览器的渲染原理）。

<!-- more -->

## DNS 解析

## 跨域解决方案

同源策略是浏览器的安全策略，它用于限制一个 origin 的文档或者它加载的脚本如何能与另一个源的资源进行交互。

如果两个 URL 的协议（protocol）、域名（host）和端口（port）一致，则这两个 URL 同源。

- jsonp
- 跨域资源共享 CORS

## 封装 XMLHttpRequest

## 封装 fetch
