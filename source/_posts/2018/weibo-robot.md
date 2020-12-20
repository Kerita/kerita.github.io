---
title: 动手写一个微博机器人
categories: node
toc: true
tag: 应用
date: 2018/2/13
---

在 [@ruanyf](https://weibo.com/1400854834/FE4pC8Rwh?type=comment#_rnd1518538999890) 老师的微博上看到“有人用推特定时发推告诉你今年的进度”，想着可以写一个微博机器人每天自动发微博倒数，一番折腾之后已经上线了，请戳 [@  201X进度条](https://weibo.com/kerita)。

<!-- more -->

具体实现过程如下（使用的语言是 Node.js）：
## 申请微博网页应用
在 [微博开放平台](http://open.weibo.com/connect) 申请一个网页应用
 <div style="text-align:center">
 {% asset_img test-web-app.png 申请应用%}
 </div>

## 获取应用 token
在 [API测试工具](http://open.weibo.com/tools/console) 获取应用 token，取得接入权限
 <div style="text-align:center">
 {% asset_img get-token.png 获取 token%}
 </div>

## 修改 nodewibo 包
项目是利用 nodeweibo 包来发送微博，因为新浪微博接口的权限调整，所以需要自己修改 nodewibo 包。在 nodeweibo 包 lib/config/config.json 文件增加如下代码（其实是增加 share 接口）。
```
		{
			"func":"share",
			"host":"https://api.weibo.com",
			"path":"/2/statuses/share.json",
			"rmethod":["POST"]
		}
```

## 利用 node-schedule 包定时发送微博
利用 node-schedule 设置定时服务， 利用上面新增的 nodeweibo share 接口，手动将 token 作为参数，发送微博。
 <div style="text-align:center">
 {% asset_img weibo.png 发送微博%}
 </div>

## 未审核应用
上面看到应用名称为未审核，只要补全资料，提交申请，就能显示真正的应用名称，审核还是很容易通过的。

## 其他功能
nodeweibo 包接口丰富，除了发微博，还可以定时发表评论、获取时间线微博、定时读取某个用户微博等,可以继续拓展。

## 上线
代码放到阿里云服务器，利用 pm2 运行并守护进程。

## 代码
完整代码将稍后整理好，补上


## 参考资料
[微博比特币价格机器人](http://blog.haipo.me/?p=1168)



