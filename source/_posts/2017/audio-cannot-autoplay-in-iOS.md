---
title: 解决iOS下音频无法自动播放
toc: true
categories: 前端
tags: [移动端,iOS,audio,HTML]
date: 2017/8/21
---
Bieber走后，开始接手公司的全景分享系统，主要是利用这个系统做一些活动页面。有个需求需要在 h5 中加背景音乐，打开链接后立即播放。原本想不就是 audio 标签加 autoplay 属性值吗？简单。但如果这么简单就不会有这篇文章了。

<!-- more -->
### 问题描述
写完在Chrome的移动端模式下测试，链接打开背景音乐就自动播放，通过钉钉将局域网测试链接发给同事，也正常。但是到了h5的主战场微信就不行了，在Safari打开也是不行。

查了资料是 iOS 内的 Safari 禁止音频自动播放，所以 Safari 下无法自动播放音频，采用 iOS 内 Safari 打开链接的微信也不行，而钉钉自己内置了浏览器，所以没问题。

### bug原因
接着找资料看能不能hack掉Safari这个糟糕的特性（官方文档是说怕音频自动播放消耗流量，但是图片也会啊，难道就禁止大图片了？），只找到 iOS4 的hack方法，在 iOS8 都失效，更不用说现在已经 iOS10 了。最后的解决办法是，在 document 绑定 touchstart/click 事件，用户触摸或者点击屏幕，音频就自动播放。

但你可能会奇怪？ iOS 下朋友圈有些 h5 背景音乐不是自动播放吗？这是因为微信的 SDK 给出了解决办法。

### 解决代码
下面给出完整的代码。

```     // bg-audio为audio标签id
        // 解决iOS禁止自动播放音频
        // 微信自动播放音频
        let bgAudio = document.getElementById('bg-audio')
        bgAudio.play();
        document.addEventListener("WeixinJSBridgeReady",function () {
            bgAudio.play();
        }, false);
        // 其他应用在click/touch时触发播放
        document.addEventListener('click', function () {
            bgAudio.play()
        })  
        document.addEventListener('touchstart', function () {
            bgAudio.play()
        })  
```

### 视频播放
关于视频播放，可以看看这两篇博文
[移动端视频播放那些事儿](http://leonshi.com/2015/09/06/mobile-video-play/)
[iOS 10 Safari 视频播放新政策](https://imququ.com/post/new-video-policies-for-ios10.html)

### 活动页面
[NPC 不破不立改造展](https://s.insta360.com/g/a2b1b5d7d9304b5d7da952d9d0afe39c?activity=npc&noad=true&from=singlemessage&isappinstalled=0)
[双城对话 圳京世界](https://s.insta360.com/g/7f8a2003b99c61939ff85ef4bd61a829?activity=crland&noad=true&from=groupmessage&isappinstalled=0)
