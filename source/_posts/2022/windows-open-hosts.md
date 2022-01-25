---
title: Parallels 上的 Windows 系统编辑 Hosts 文件
categories: 工具
date: 2022-01-05
---

在 Parallels 安装了 Windows 10 系统，直接编辑 hosts 文件提示没有权限保存，用以下方法解决：

1.打开 hosts 文件所在的文件夹

```
cd C:\Windows\System32\drivers\etc
```

2.cmd 用管理员身份打开
3.cmd 上输入命令 notepad hosts

```
notepad hosts
```
