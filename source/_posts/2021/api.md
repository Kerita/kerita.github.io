---
title: 接口对接 SOP —及时沟通、前置风险并解决
categories: 前端
toc: true
tags: 项目
date: 2021/7/8
---

## 接口对接过程遇到的问题

在开发一个项目的时候，接口对接是必不可少的。接口对接也不止发生在前端后端之间，也发生在后端与其他业务线、后端与外部系统，也就是说接口对接是频繁的，并且是重要的。

然而，在对接过程中，往往我们会遇到以下问题：

- 没有接口文档，接口口头或者企业微信简单确认（特别是只有一两个接口时）
- 接口文档没有确定交付时间，或者到时间没有交付
- 接口文档不全，接口缺失或者接口字段缺失
- 接口变更，实际接口与接口文档不一致
- ......

## SOP 的重要性

接口对接是一个很小但是很重要的事情，接口对接不顺畅，可能会导致项目返工以及进度落后。在丰富的工程实践中，我总结了一套接口对接 SOP，针对接口对接过程中的种种问题，将接口对接变成一步步标准化的流程，减少遗漏和错误，提高接口对接过程中的工作效率。

该 SOP 的策略是：通过主动沟通、及时沟通，保证接口不成为阻塞开发的障碍，及时将在对接过程中存在的风险暴露，将风险前置并且解决，达到对接流畅的目的。

## 我的接口对接 SOP

### 1.确定接口文档交付时间

在项目评审阶段，确定好接口文档交付时间，有两个主要原因。

接口交付时间会影响到接口对接下游的开发进度和排期
在企业微信消息或者项目进度表确定时间，尽量确保接口文档按时交付

### 2.主动索要接口

临近交付时间了，可以主动索取接口文档，提高交付准时性。

有时候虽然按时交付了，但是交付质量非常一般，如多个接口缺失、接口返回错误。所以，交付时对齐、评估并快照接口就显得非常重要。

### 3.交付时对齐、评估并快照接口

接口文档交付时，作为下游，不是回一句 ”收到“ 就够了，而应该分三步走。

- 对齐接口

  对齐本次有哪些接口
  接口分别在哪些地方使用
  就算只有一两个接口也应该落地到接口文档，方便自己还有后来人对接

- 评估接口

  评估接口的方法就是：一个个看接口返回，评估不通过的，及时沟通调整。
  对于比较复杂的接口，交付前应该协商好接口方案，上下游共同将方案确定。

  - 确定接口字段，确定是否满足前端业务需求
  - 评估接口方案是否会影响性能
  - 确定有推送，以及推送的数据结构
  - .....

- 快照接口

  快照接口是将接口文档通过截图、或者复制等方式快照，包括接口请求方法、content-type、以及返回。

  快照接口主要是防止开发过程接口变更，导致联调时接口与一开始约定不一致，最后浪费时间在最终的沟通上。当然，快照接口策略是比较麻烦的，对于一些复杂的接口或者一些特殊情况，我们才视情况使用。

### 4.明白我们的最终目标

接口上下游最终目标是一致，都是把项目完成，把项目做好。可能接口对接过程中，会有出现这样那样问题，但我们都应该保持积极向上昂扬的态度，推动事情发展，保证最终目标的达成。永远相信美好的事情将会发生。

以上。
