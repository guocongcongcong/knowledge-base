---
title: Coze扣子-Agent开发平台全攻略
created: 2026-06-03
updated: 2026-06-03
type: concept
tags: [ai-tools, coze, agent, workflow, 变现]
sources: [https://www.coze.cn, https://www.coze.com]
confidence: medium
contested: false
contradictions: []
---

# Coze（扣子）Agent 开发平台全攻略

> 字节跳动的 AI Agent 开发平台。国内版 coze.cn，国际版 coze.com。

---

## 平台定位

核心两件事：
- **Agent（对话型 Bot）**：跟用户对话，自动调用插件/工作流/知识库
- **AI Application（独立应用）**：有完整 UI 和业务逻辑

---

## 一个 Agent 的 7 大模块

### 1. 模型选择（Models）
- 国内外模型全有：GPT-4o、Claude、DeepSeek、豆包、通义千问等
- 策略：客服用便宜的、创意生成用强的
- 可调 temperature、top_p 等参数

### 2. Prompt 工程
- 人设 Prompt（System Prompt）：定义角色、语气、边界
- 结构化提示：条件分支、输出格式控制
- 有独立的 Prompt 管理库，可复用

### 3. Chatflow 模式（策略核心）
- 把对话从自由 LLM 回答变成**节点式决策流**
- 条件判断、循环、意图识别节点
- 示例：用户说"退款" → 走售后工作流 → 检查订单状态 → 自动处理或转人工

### 4. 技能三件套
- **插件（Plugins）**：API 调用，300+ 官方 + 可自建
- **工作流（Workflows）**：可视化编排（LLM 节点 + 代码节点 + HTTP 节点 + 数据库节点）
- **卡片（Cards）**：结构化 UI 回复（商品卡片、表单）

### 5. 知识库（Knowledge Base）
- 文本 / 表格 / 图片三类知识库
- 分段策略决定检索质量

### 6. 记忆（Memory）
- 变量（Variable）：跨对话持久化（用户偏好、历史记录）
- 数据库（Database）：多行结构化存储

### 7. 用户体验
- Opening Question：开场白引导
- Shortcut：快捷指令

---

## 从 0 到上线操作流程

| Step | 操作 |
|------|------|
| 1 | 注册 → 创建 Agent（或从模板商店 Fork） |
| 2 | 配置基础设置（Prompt + 模型 + Chatflow 模式） |
| 3 | 加技能（插件 / 工作流 / 知识库） |
| 4 | 右侧调试面板实时测试 |
| 5 | 一键发布到 Discord/Telegram/Slack/LINE/WhatsApp/飞书/微信/API |
| 6 | 变现：提交到作品社区/模板商店 → 被推荐 → 获得曝光 |

---

## 关键策略要点

| 维度 | 策略 |
|------|------|
| 意图识别 | Chatflow 开头放意图识别节点，分流不同场景 |
| 多模型路由 | 简单问题走便宜的模型，复杂问题切强模型 |
| 知识库分段 | 按 topic 分块 + 加元数据标注 |
| 容错 | 插件调用失败时 fallback 到预设回复 |
| 多轮对话 | 用变量保存用户状态 |
| 成本控制 | 限制 max token、控制检索条数、缓存常见问答 |

---

## 变现途径

- 提交 Bot 到作品社区 → 被推荐 → 获得曝光和用户
- 自建插件提交到插件商店 → 别人使用你的插件
- 模板商店 Fork 热门模板修改后提交


## 模板市场

| 市场 | 地址 |
|------|------|
| Bot 商店 | https://www.coze.cn/store/bot |
| 插件商店 | https://www.coze.cn/store/plugin |

**高需求模板类型：**
- 🔥 DeepSeek AI 综合助手（搜索/读链接/生成图片/思维导图/文档/视频文案）
- 🛒 电商售后客服（物流、支付、售后问答）
- 📚 教育智能助教（课件生成、作业批改）
- 🎨 内容生成（漫画视频生成）
- 🤖 通用智能客服

---

## 相关平台对比

- [[Dify与n8n模板市场分析]]
- [[Agent开发赚钱学习路线]]
