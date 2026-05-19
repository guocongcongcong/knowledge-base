---
title: Pretext — 纯 TS 文本测量引擎
created: 2026-05-18
updated: 2026-05-18
type: concept
tags: [ai-tools, typescript, frontend, text-layout, canvas, animation, open-source]
sources:
  - https://www.douyin.com/video/7640876069596227300
  - https://github.com/chenglou/pretext
confidence: high
contested: false
contradictions: []
---

# Pretext — 纯 TS 文本测量引擎

## 是什么

Pure TypeScript 多行文本测量与排版库。**不碰 DOM，不触发 reflow**，用 Canvas 预计算字符宽度后纯算术排版。^[raw/transcripts/douyin-frontend-rendering-revolution.md]

- GitHub: https://github.com/chenglou/pretext
- Stars: 47,100+
- 作者: Cheng Lou（前 Facebook/Meta React 团队）
- 官方 Demo: https://chenglou.me/pretext
- 社区 Demo: https://somnni-dreams.github.io/pretext-demos

## 为什么重要

浏览器里测量文本（`getBoundingClientRect`、`offsetHeight`）会触发 **layout reflow**——浏览器最昂贵的操作之一。Pretext 绕过了它，用自己的文本测量逻辑，用浏览器字体引擎作为 ground truth 校准。

**这意味着**：
- 虚拟滚动不再需要猜测行高和缓存
- 复杂用户态布局（masonry、JS 驱动的 flexbox）无需 CSS hack
- 可以在服务器端做文本排版
- AI 驱动的 UI 生成可以精确测量文本而不需要完整浏览器环境

## API 两种用法

### 用法1：测量段落高度（不碰 DOM）

```ts
import { prepare, layout } from '@chenglou/pretext'

const prepared = prepare('AGI 春天到了. بدأت الرحلة 🚀', '16px Inter')
const { height, lineCount } = layout(prepared, 320, 20)
// 纯算术！无 DOM layout 和 reflow！
```

`prepare()` 做一次性工作：规范化空白、分词、应用粘连规则、用 Canvas 测量片段。`layout()` 是廉价热路径：在缓存宽度上做纯算术。

### 用法2：手动排版（Canvas / SVG 渲染）

```ts
import { prepareWithSegments, layoutWithLines } from '@chenglou/pretext'

const prepared = prepareWithSegments(text, '18px "Helvetica Neue"')
const { lines } = layoutWithLines(prepared, 320, 26)
lines.forEach((line, i) => ctx.fillText(line.text, 0, i * 26))
```

高级用法还有：
- `measureLineStats()` — 获取行数、最大行宽
- `walkLineRanges()` — 遍历行范围而不构建字符串
- `layoutNextLineRange()` — 逐行路由文本（宽度可变场景，如文字绕排图片）
- `materializeLineRange()` — 从范围还原完整行字符串

## 多语言支持

原生支持 CJK（中日韩）、Arabic（RTL 从右到左）、emoji、软连字符等所有浏览器支持的书写系统。

## 安装

```bash
npm install @chenglou/pretext    # 安装
```

纯 TypeScript，零运行时依赖。

## 在线 Demo

- **GitHub Pages**: https://guocongcongcong.github.io/pretext-demo/
- **GitHub Repo**: https://github.com/guocongcongcong/pretext-demo

## 本地 Demo

```bash
git clone https://github.com/guocongcongcong/pretext-demo.git
cd pretext-demo
python3 -m http.server 8888
# 访问 http://localhost:8888
```

Demo 包含三个交互示例：
1. 文本测量：输入文本实时计算高度、行数，零 reflow
2. DOM vs Pretext 性能对比
3. 多语言渲染（中文、阿拉伯语、日语、韩语、英语）

## 适用场景

- 虚拟滚动 / 窗口化列表（精确行高，无需猜测）
- Canvas 富文本编辑器
- 服务端 PDF 生成中的文本排版
- SVG 数据可视化中的文本标注
- AI Agent 生成的 UI 需要精确文本测量

## 参见

- [[claude-code-mcp-browser]] — Claude Code 浏览器联动
- [[deer-flow-multi-agent]] — 另一个高星开源项目
- 官方文档: https://chenglou.me/pretext
