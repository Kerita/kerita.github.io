husky 是一个 Node.js 包，可以让我们更方便地管理 Git Hook。基于 Git pre-commit Hook，我们可以在代码 commit 之前做格式检查，保证代码规范。

如何配置 husky + ESlint + Prettier + lint-staged 可以参考[这篇文章](https://segmentfault.com/a/1190000022497035)，讲得很详细，这里不再赘述。

下面我们分析下 husky 的源码。
