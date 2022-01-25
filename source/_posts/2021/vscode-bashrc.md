---
title: VS Code Resolving shell environment fails 提示
date: 2021-12-14
---

某次升级完 VS Code 之后，打开窗口便一直出现一个错误提示。如下所示。

```
Unable to resolve your shell environment in a reasonable time.
Please review your shell configuration.
```

点击错误提示下方的官方文档按钮，进入官方文档，查看如何解决。文档说是加载终端配置的时间太长了，才出现的错误；终端配置文件可能是 `~/.bashrc` 和 `~/.zshrc`。

查看终端配置文件，发现我并没有 `~/.bashrc`，猜想可能是该文件缺失导致的。

<!-- more -->

![加载错误](./shell-env-error.png)

使用 vi 打开 `~/.bashrc`，添加如下内容：`echo You are great!`，并输入`:wq` 命令保存。

重新 VS Code 错误提示消失，成功解决问题。
