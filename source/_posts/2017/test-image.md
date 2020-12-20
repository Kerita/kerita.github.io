---
title: test-image
date: 2017-06-13 10:57:14
tags: hexo
toc: true
categories: 小技巧
---

** 如何在Markdown中插入图片，使得编译之后，在hexo首页和文章页都能看到呢？ **

<!--more-->

### 设置 post_asset_folder
在根目录下的_config.yml设置post_asset_folder:true

### _posts目录下创建文章同名目录

### 引入图片
```
{% asset_img example.png text %}
```
{% asset_img example.png This is a image%}




### 参考链接
[Hexo博客搭建之在文章中插入图片](https://yanyinhong.github.io/2017/05/02/How-to-insert-image-in-hexo-post/)
