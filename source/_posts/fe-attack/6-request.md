---
title: 浏览器如何进行网络请求
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

根据域名如 `kerita.me` 查找到对应的 ip。在开发过程经常有配置 hosts 的操作，相当于系统缓存了 DNS 信息，直接访问配置的 IP 地址即可，无需继续查询。

## 跨域解决方案

同源策略是浏览器的安全策略，它用于限制一个 origin 的文档或者它加载的脚本如何能与另一个源的资源进行交互。

如果两个 URL 的协议（protocol）、域名（host）和端口（port）一致，则这两个 URL 同源。

- jsonp
  jsonp 的原理是使用 script 标签访问一个链接，该链接返回一段 JS 脚本，JS 脚本会执行指定的函数并返回数据。之所以使用 script，是因为其 src 属性是没有同源策略的限制，而 XMLHttpRequest 和 fetch 有。

  [在线访问](https://kerita.me/fe-attack-demo/6-request/jsonp.html)

  ```
  	<script>
  		function callback(data) {
  			document.write(JSON.stringify(data.data))
  		}
  	</script>
  	<script src="https://photo.sina.cn/aj/index?callback=callback&page=1&cate=recommend"></script>
  ```

- 跨域资源共享 CORS（Cross-origin resource sharing）
  CORS 是一种基于 HTTP 头的机制，允许 Web 应用服务器进行跨源访问控制。

  服务器在在请求响应头部添加 `Access-Control-Allow-Origin` 字段。当字段值为 `*` 或者当前访问域时，表示允许跨域请求；当该字段不存在时，表示不能进行跨域访问。

  Nginx CORS 配置如下：

  ```
  location ~ \.php$ {
  		# options 针对复杂请求的预检
      if ($request_method = 'OPTIONS') {
          add_header 'Access-Control-Allow-Origin' '*' always;
          add_header 'Access-Control-Allow-Methods' 'GET,POST,OPTIONS,PUT,DELETE' always;
          add_header 'Access-Control-Allow-Headers' '*' always;
          add_header 'Access-Control-Max-Age' 1728000 always;
          add_header 'Content-Length' 0;
          add_header 'Content-Type' 'text/plain; charset=utf-8';
          return 204;
      }

      if ($request_method ~* '(GET|POST|DELETE|PUT)') {
          add_header 'Access-Control-Allow-Origin' '*' always;
      }
  }
  ```

- window.postMessage

## 三次握手和四次挥手

- 三次握手(three-way handshake)
  三次握手是为了解决“信道不可靠问题”，至少需要三次通信才能确保客户端与服务端的接收能力与发送能力都是正常的，并且二者彼此也知道是正常的。

  1.第一次握手：客户端发送 SYN 报文给服务端；  
  2.第二次握手：服务端收到客户端的 SYN 报文，发送自己的 SYN 报文；  
  3.第三次握手：客户端收到服务端的 SYN 报文，发送 ACK 报文。

- 四次挥手（four-way handshake）
  三次挥手是为了确保客户端与服务端的接收能力和发送能力都没有问题，四次挥手则是为了确保双方都已经准备好关闭。

  1.第一次挥手：客户端准备好关闭，发送 FIN 报文给服务端；  
  2.第二次挥手：服务端接收到客户端的 Fin 报文，发送 ACK 报文，此时服务端不能立即关闭，因为数据可能还没有传输完；  
  3.第三次挥手：服务端准备好关闭，发送 FIN 报文给客户端；  
  4.第四次挥手：客户端收到服务端的 FIN 报文，发送 ACK 报文。

## 封装 XMLHttpRequest

```
		function request(option) {
			const xhr = new XMLHttpRequest()
			xhr.onreadystatechange = function () {
				if (xhr.readyState === 4) {
					if (xhr.status === 200) {
						if (option.success && typeof option.success === 'function') {
							option.success(xhr.response)
						}
					} else {
						if (option.error && typeof option.error === 'function') {
							option.error()
						}
					}
				}
			}
			xhr.open(option.method, option.url, true)

			if (option.method === 'POST') {
				xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
			}

			xhr.send(option.method === 'POST' ? option.data : null)
		}

		request({
			url: 'https://openapi.insta360.com/store/meta/home/listItems?X-Language=zh_cn&X-Country=CN',
			method: 'get',
			success: res => console.log(res)
		})
```

## 参考资料

- [跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)
- [三次握手和四次挥手](https://zhuanlan.zhihu.com/p/86426969)
