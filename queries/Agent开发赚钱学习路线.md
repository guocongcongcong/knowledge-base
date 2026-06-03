---
title: Agent开发赚钱学习路线
created: 2026-06-03
updated: 2026-06-03
type: query
tags: [ai-tools, agent, 变现, 学习路线, workflow]
sources: [https://www.coze.cn, https://dify.ai, https://n8n.io, https://github.com/trending]
confidence: medium
contested: false
contradictions: []
---

# Agent 开发赚钱学习路线

> 目标：用 AI Agent 开发能力变现。覆盖平台选择、技能树、变现路径。

---

## 一、三个层级，递进式学习

### L1：无代码 Agent 搭建（1-2 周可接单）

**平台：Coze（扣子）/ Dify / n8n**

学什么：
- ✅ Prompt 工程（人设 + 结构化输出）
- ✅ Chatflow / Workflow 可视化编排
- ✅ 插件调用 + 知识库 RAG
- ✅ 发布到 Telegram/微信/飞书

能做什么：
- 给淘宝/拼多多商家做智能客服 Bot（500-2000/个）
- 给自媒体做 AI 自动回复助手
- 给教育机构做智能助教

**为什么从这里开始**：零代码，出活快，市场需求大。

### L2：API + 工作流自动化（2-4 周）

**平台：n8n / Dify 工作流模式**

学什么：
- ✅ HTTP 请求节点 + API 对接
- ✅ 数据库读写（MySQL/Postgres）
- ✅ Webhook 触发 + 定时任务
- ✅ 多步骤自动化流水线

能做什么：
- 企业数据自动采集 → AI 分析 → 日报推送（3000-8000/套）
- 电商订单自动处理 + AI 客服
- 内容自动发布流水线（写 → 审 → 发）

### L3：代码级 Agent 开发（4-8 周）

**工具：Claude Code / Codex / Cursor + MCP + Skills**

学什么：
- ✅ MCP 协议（Model Context Protocol）
- ✅ Skill 编写（Hermes/Claude Code 的 Skill 系统）
- ✅ Tool calling + Function calling
- ✅ RAG 系统搭建
- ✅ 多 Agent 编排

能做什么：
- 给企业做私有化 Agent 部署（10000-50000/项目）
- 开发 Claude Code/Codex 的 Skill 插件
- 搭建行业垂直 Agent（法律/医疗/金融）

---

## 二、三大变现路径

### 路径 A：模板市场卖货

| 平台 | 变现方式 | 门槛 |
|------|---------|------|
| Coze | Bot 商店上架 + 插件商店 | 低 |
| n8n | Featured 模板 + Affiliate 分成 | 中 |
| Dify | 模板市场 | 低 |
| GitHub | 开源 Skill/Workflow 模板赚 Star → 接定制单 | 中 |

**策略**：先做 10 个免费模板攒口碑 → 接定制单 → 上架付费模板。

### 路径 B：接单/外包

| 客户类型 | 需求 | 单价 |
|---------|------|------|
| 淘宝/拼多多卖家 | AI 客服 Bot | 500-2000 |
| 自媒体博主 | 自动回复 + 内容生成 | 1000-3000 |
| 中小企业 | 数据采集 + AI 分析 + 日报 | 3000-8000 |
| 教育/培训机构 | 智能助教 | 3000-10000 |
| 大企业 | 私有化 Agent 部署 | 10000-50000 |

**获客渠道**：闲鱼/淘宝挂服务 → 小红书/抖音发案例 → B站发教程引流 → 猪八戒/Upwork。

### 路径 C：做自己的 AI 产品

1. 找到一个垂直场景（如：律师合同审查 Bot）
2. 用 Coze/Dify 先做出 MVP
3. 抖音/小红书发内容获取种子用户
4. 免费 → 付费转化
5. 后续升级到代码级部署（私有化）

---

## 三、技能树

```
Agent 开发赚钱
├── Prompt 工程 ★★★★★
│   ├── 人设编写
│   ├── 结构化输出控制
│   └── Few-shot 示例
├── 工作流编排 ★★★★★
│   ├── Coze Chatflow
│   ├── Dify Workflow
│   └── n8n Workflow
├── RAG 知识库 ★★★★
│   ├── 文档分段策略
│   ├── 向量检索
│   └── 混合检索（关键词 + 语义）
├── API 对接 ★★★★
│   ├── HTTP 请求
│   ├── 数据库读写
│   └── Webhook
├── MCP 协议 ★★★
│   ├── Tool 定义
│   └── Server 搭建
├── Skill 编写 ★★★
│   ├── Hermes Skill
│   └── Claude Code Skill
├── 前端基础 ★★
│   ├── HTML/CSS（做 Bot 卡片）
│   └── 简单的 Web 部署
└── 获客/销售 ★★★★★
    ├── 闲鱼/淘宝上架
    ├── 小红书/抖音发案例
    └── B站发教程引流
```

---

## 四、推荐学习顺序（8周计划）

| 周 | 学习内容 | 产出 |
|----|---------|------|
| 1 | Coze 基础：创建第一个 Bot + 发布到微信 | 一个能用的 Bot |
| 2 | Coze 进阶：Chatflow + 知识库 + 插件 | 带业务逻辑的 Bot |
| 3 | n8n/Dify 基础工作流 | 一个自动化流程 |
| 4 | API 对接 + 数据库操作 | 一个数据驱动的 Bot |
| 5 | RAG 搭建 + 分段优化 | 一个知识库问答 Bot |
| 6 | 接第一个单（低价练手） | 实际交付一个项目 |
| 7 | Skill 编写 + MCP 入门 | 一个可复用的 Skill |
| 8 | 做 3 个模板上架 + 发推广内容 | 开始有被动收入 |

---

## 五、关键资源

| 资源 | 地址 |
|------|------|
| Coze 国内版 | https://www.coze.cn |
| Coze Bot 商店 | https://www.coze.cn/store/bot |
| Dify 模板市场 | https://dify.ai/templates |
| n8n 工作流模板 | https://n8n.io/workflows |

---

## 相关笔记

- [[Coze扣子-Agent开发平台全攻略]]
- [[Dify与n8n模板市场分析]]
- [[如何写出一个好的Skill]]
- [[Claude-Code-7个必装Skill]]
- [[AI-Agent-核心概念对照]]
