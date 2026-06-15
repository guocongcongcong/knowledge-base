---
title: "Voice Reader 项目详解 — AI语音读文档Web应用"
created: 2026-06-15
updated: 2026-06-15
type: concept
order: 7
tags: [Voice Reader, TTS, FastAPI, React, Edge TTS, 语音朗读, markitdown]
confidence: high
contested: false
contradictions: []
related: ["[[苏格拉底·七 系统分析]]", "[[Socratopia 苏格拉底+二次元学习法 分析]]"]
---

# Voice Reader — AI 语音读文档

## 一句话

上传任何格式的文档 → 自动转 Markdown → AI 语音朗读全文/选中文字。本地优先，数据不出设备。

## 项目路径

`~/Downloads/workspace/voice-reader/`

## 是干什么的

把 PDF、Word、PPT、Excel、EPUB 等 12 种格式的文件**拖进去**，自动转成可读的 Markdown，然后用微软 Edge TTS（免费、高质量）**语音朗读**出来。选中任意段落可以单独朗读。本质是一个"文档→语音"的本地 Web 工具。

与此前 socratic-seven（苏格拉底教学法）互补——socratic-seven 是"AI老师提问你回答"，voice-reader 是"AI帮你把教材读出来"。

## 技术栈

| 层 | 技术 |
|---|---|
| 文档转换 | markitdown (Microsoft) — PDF/DOCX/PPTX/XLSX/EPUB → MD |
| 语音合成 | Edge TTS — 微软免费TTS，130+音色，7种精选中文音色 |
| 后端 | FastAPI + Python 3.12 + aiosqlite |
| 前端 | React 19 + Vite + TypeScript + TailwindCSS |
| MD渲染 | react-markdown + remark-gfm |
| 存储 | 本地SQLite + 文件系统（`data/` 目录） |

## 核心架构

```
浏览器（用户）
  │  拖拽上传 PDF/DOCX/PPTX...
  ▼
POST /api/upload  →  markitdown 转 MD  →  存 data/markdown/
  │
  ▼
文档列表页面 → 点击某文档 → 进入阅读器
  │
  ├─ 选中任意文字 → POST /api/docs/:id/tts/selection  →  Edge TTS 朗读选中
  └─ 朗读全文   → GET  /api/docs/:id/tts?voice=X&rate=Y →  Edge TTS 朗读全文
                    GET  /api/docs/:id/tts/stream         →  SSE流式词级高亮
```

## 关键设计决策

### 混合命令式/声明式选区架构

React 虚拟 DOM 和浏览器 Selection API 是天敌——React 每次重渲染会销毁 DOM 节点，Selection 对象随之失效。解决方案：

- **React 管理**（声明式）：Toolbar、播放控件、文件列表
- **useRef 管理**（命令式）：文本容器DOM、Selection/Range序列化、TTS词级高亮

react-markdown 渲染一次到 `<div ref={contentRef}>` 后交权给命令式代码。用户选中文字 → 序列化 Range → 发送后端。TTS 播放时 SSE 推送词边界事件 → 命令式 Range API 高亮（不触发 React 重渲染）。这是一个教科书级的 React 混合架构案例。

### Edge TTS 词边界模拟

Edge TTS 原生只提供 **SentenceBoundary** 事件（句子级），不提供 **WordBoundary**（词级）。为了做逐字高亮动画，TTSEngine 自己实现了一个 tokenizer：

- 中文汉字 → 逐字拆分
- 英文单词 → 整体保留
- 标点 → 独立 token
- 将句子时长平均分配给内部的每个字词

这虽然不如真实的词级时间戳精确，但在中文逐字高亮场景下完全够用。

### 数据完全本地

- 文档存储在 `data/documents/`
- 转换后的 MD 在 `data/markdown/`
- 生成的音频在 `data/audio/`
- 元数据在 `data/voice_reader.db` (SQLite)

所有数据都在本地磁盘上，不依赖任何云服务（除了 Edge TTS 需要网络调用微软的免费 API）。

## API 端点

| 端点 | 方法 | 功能 |
|------|------|------|
| `/api/upload` | POST | 上传文档（multipart/form-data），自动转换MD |
| `/api/docs` | GET | 文档列表（分页） |
| `/api/docs/:id` | GET | 文档详情+全文MD内容 |
| `/api/docs/:id` | DELETE | 删除文档 |
| `/api/docs/:id/tts` | GET | 全文语音合成 → 返回MP3 |
| `/api/docs/:id/tts/selection` | POST | 选中文字语音合成 |
| `/api/docs/:id/tts/stream` | POST | 流式TTS + SSE词边界事件 |
| `/api/voices` | GET | 可用音色列表 |
| `/api/health` | GET | 健康检查 |

## 支持的文件格式

| 格式 | 扩展名 |
|------|--------|
| 纯文本 | .txt |
| Markdown | .md |
| HTML | .html, .htm |
| Word | .docx |
| PowerPoint | .pptx |
| Excel | .xlsx |
| PDF | .pdf |
| CSV | .csv |
| XML | .xml |
| JSON | .json |
| EPUB电子书 | .epub |

## 7种精选中文音色

| 音色 | 性别 | 风格 | 适用场景 |
|------|------|------|---------|
| **Xiaoxiao** | 女 | 标准播报 | 通用，默认推荐 |
| **Yunxi** | 男 | 新闻播报 | 长文朗读 |
| Yunyang | 男 | 专业播报 | 播客风格 |
| Xiaoyi | 女 | 温柔 | 故事/散文 |
| Yunjian | 男 | 体育解说 | 激情朗读 |
| Yunxia | 男 | 卡通 | 儿童内容 |
| Xiaobei | 女 | 东北话 | 方言朗读 |

## 如何启动

### 第一步：启动后端

```bash
cd ~/Downloads/workspace/voice-reader/backend
source ../venv/bin/activate
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

验证：`curl http://localhost:8000/api/health` 应返回 `{"status":"ok","default_voice":"zh-CN-XiaoxiaoNeural"}`

### 第二步：启动前端（新终端窗口）

```bash
cd ~/Downloads/workspace/voice-reader/frontend
npm run dev
```

浏览器打开 `http://localhost:5173`

### 第三步：使用

1. 拖拽 PDF/DOCX/MD 等文件到上传区
2. 等待"转换中..."完成
3. 点击文档卡片进入阅读器
4. 选中任意文字 → 点"朗读选中"
5. 或点"朗读全文"听整篇

## 与 socratic-seven 的关系

| 维度 | socratic-seven | voice-reader |
|------|---------------|-------------|
| 功能 | AI老师苏格拉底教学 | AI语音朗读文档 |
| 输入 | 人在Claude Code中对话 | 人上传文档/选中文字 |
| 输出 | AI提问+反馈 | AI语音朗读 |
| 核心价值 | 提取式学习（被动→主动） | 多模态输入（视觉→听觉） |
| 使用场景 | 深度学习/系统理解 | 快速浏览/碎片时间听 |
| 驱动 | Claude Code | FastAPI + Edge TTS |

**互补关系**：socratic-seven 解决"怎么学得更深"，voice-reader 解决"怎么学得更省力"。同样的教材放 socratic-seven 里是被老师追问，放 voice-reader 里是被 AI 读给你听。两个工具可以串联：用 voice-reader 听完一章建立全局印象 → 进 socratic-seven 被三位老师追问细节。

## 当前状态

**已完成**：Phase 2（后端核心）+ Phase 3（前端界面）。8个端点 + 6个前端组件全部实现，后端校验、前端TS编译通过。

**未完成**：Phase 1（可行性验证报告）未产出正式文档。Phase 4（联调打磨）中的 SSE 流式词级高亮前端未接入（后端 `/api/docs/:id/tts/stream` 端点已实现，但 `Reader.tsx` 的音频播放走的是非流式 `/api/docs/:id/tts`）。

## 常见问题

**Q: 为什么上传后看不到文件？**
A: 后端没启动或者端口被占用。`lsof -tiTCP:8000` 检查8000端口。确认返回 `/api/health` 的内容是 `"default_voice"` 而不是 `"socratic-verse-web-backend"`——后者是另一个项目占用了端口。

**Q: 前端浏览器打开报 CORS 错误？**
A: 后端 CORS 已配置 `localhost:5173`。确认前端确实跑在 5173 端口。

**Q: 支持 .pages / .numbers 吗？**
A: 不支持。只支持 converter.py 里 `SUPPORTED_FORMATS` 列的12种格式。
