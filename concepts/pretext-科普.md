---
title: Pretext — 纯 TS 文本测量引擎（科普版）
created: 2026-05-19
updated: 2026-05-19
type: concept
order: 
tags: [ai-tools, frontend, text-layout, performance, beginner]
sources:
  - https://github.com/chenglou/pretext
confidence: high
contested: false
contradictions: []
---

# Pretext — 纯 TS 文本测量引擎

## 一句话

**在浏览器里精确测量文字尺寸，但不触发浏览器最慢的操作——回流（reflow）。**

---

## 先理解背景：浏览器测文字为什么慢？

浏览器渲染一个网页时分两步：

```
1. 算位置（Layout/Reflow）→ "这个字放哪？多宽？多高？"
2. 画出来（Paint）        → "现在画上去"
```

问题在于第 1 步。浏览器算位置时，**一个元素的位置变了，可能牵连整个页面重新计算**。这过程叫「回流」（reflow），是浏览器最慢的操作之一。

比如你让浏览器测一段文字的宽度：
```js
element.getBoundingClientRect().width  // 触发 reflow！
```

每次调用这个方法，浏览器都可能要重新算一遍页面布局。如果你在循环里调用它（比如虚拟滚动列表有 1000 行），页面就会卡死。

**Pretext 的解法：不经过浏览器，自己算。**

---

## Pretext 怎么做到的？

Pretext 的策略分两步：

### 第一步：用 Canvas 校准一次

```
"中" 这个字在 16px 的字体下到底多宽？
→ 用 Canvas 画一次，测量像素宽度 → 记下来
```

这一步叫 `prepare()`。它做一次性的「校准」——用浏览器字体引擎作为标准答案，测出每个字符的宽度，缓存起来。

### 第二步：纯算术排版

有了字符宽度缓存后，排版就变成了纯算术：
```
"AGI 春天到了 🚀"，16px 字体，容器宽 320px
→ 逐字累加宽度，超 320px 就换行
→ 全程不碰 DOM，不触发 reflow
```

这一步叫 `layout()`。它只用缓存的数字做加减法，**比浏览器快了 10-100 倍**。

---

## 打个比方

| 传统方式 | Pretext |
|---------|---------|
| 你要知道一本书多厚 | 你要知道一本书多厚 |
| → 把整本书排版印出来 | → 提前知道每页能放多少字 |
| → 量纸张厚度 | → 用字数 ÷ 每页字数 = 页数 |
| 慢、费资源 | 快、纯计算 |

Pretext 就是「提前知道每页能放多少字」的那个角色。

---

## 为什么这个东西重要？

### 场景 1：虚拟滚动

假设你有一个聊天记录列表，10 万条消息。你不能把 10 万条全渲染出来（浏览器会卡死）。虚拟滚动的做法是——只渲染屏幕上看得见的那几条。

但问题是：**你得知道每条消息多高，才能算出滚动条的位置。** 传统做法是猜测行高（"每条大概 50px"），猜错了滚动条就乱跳。

用 Pretext：精确算出每条消息的高度，滚动丝滑。

### 场景 2：服务端生成 PDF

服务器上没有浏览器。你怎么知道一段文字排版后多高？Pretext 不依赖浏览器，Node.js 环境直接跑。

### 场景 3：AI 生成 UI

如果 AI Agent 要生成一个网页，它需要知道"标题放这里会不会溢出""导航栏够不够宽"。Pretext 让 AI 能在生成代码前就精确计算文本布局。

### 场景 4：Canvas 富文本编辑器

Canvas 是画布，不是 DOM。没有 `getBoundingClientRect`。要在 Canvas 上排版文字，Pretext 是完美的工具。

---

## 代码有多简单？

```ts
import { prepare, layout } from '@chenglou/pretext'

// 第一步：校准（做一次）
const prepared = prepare('AGI 春天到了 🚀', '16px Inter')

// 第二步：排版（可以反复调用，超快）
const { height, lineCount } = layout(prepared, 320, 20)
// → { height: 72, lineCount: 3 }
// 意思是：16px 字体，320px 宽的容器，这段文字占 3 行，总高 72px
```

就这么两行。返回高度和行数。全程没碰 DOM。

---

## 多语言支持

Pretext 原生支持：
- 中文 / 日文 / 韩文（CJK——等宽字符，换行规则复杂）
- 阿拉伯文（RTL 从右到左书写）
- Emoji（宽度不一致）
- 任何浏览器支持的书写系统

---

## 谁做的

作者 Cheng Lou，前 Facebook/Meta React 核心团队成员。47,000+ GitHub Stars。纯 TypeScript，零运行时依赖。

GitHub: https://github.com/chenglou/pretext

---

## 一句话总结

> 传统方式测文字 = 每次都要排版印刷再量厚度。Pretext = 提前量好每个字的宽度，之后纯算术。快了 10-100 倍，而且服务端也能用。

## 相关

- [[AI-Agent-核心概念对照]] — Agent 的基础概念
- [[claude-code-mcp-browser]] — Claude Code 浏览器联动
