---
title: Could not find a declaration file for module-name
categories: TS
date: 2022-05-10
---

Could not find a declaration file for module-name 可能有两种情况：

### 1.引入第三库

安装 @types/module-name，为第三库提供类型声明。

```
npm install -D @types/module-name
```

<!-- more -->

### 2.引入自己的文件

在一个 global.d.ts 的文件中添加模块声明，并在 tsconfig.js 中引入 global.d.ts 文件。

<!-- global.d.ts -->

```
declare module 'foo';
```

<!-- tsconfig.js -->

```
  {
    "compilerOptions": {
			...
      },
      "include": [
        "global.d.ts",   // declaration file path
      ],
    }
```

### 参考资料

- [Could not find a declaration file for module 'module-name'. '/path/to/module-name.js' implicitly has an 'any' type](https://stackoverflow.com/questions/41292559/could-not-find-a-declaration-file-for-module-module-name-path-to-module-nam?page=1&tab=scoredesc#tab-top)
