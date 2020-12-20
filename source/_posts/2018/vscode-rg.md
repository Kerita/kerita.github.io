---
title: rg.exe 占用 100% CPU
categories: 小技巧
tags: [vscode, 编辑器]
date: 2018/2/19
toc: true
---
Windows 上使用 VSCode 遇到一个问题，打开项目时，整个电脑基本卡死，Ctrl+Shift+Esc 发现 rg.exe 占用 100% 的 CPU。
<!--  more -->
在 github 看到，是因为是 cnpm 的原因，解决方法如下：

## 下载 vscode1.18以上版本 

## 增加配置
安装完成后 文件>首选项>设置
```
    "search.followSymlinks": false
```