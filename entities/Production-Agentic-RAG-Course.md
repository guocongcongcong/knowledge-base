---
title: Production Agentic RAG Course
created: 2026-06-03
updated: 2026-06-03
type: entity
tags: [ai-tools, rag, agent, 学习路线, langgraph, fastapi, opensearch]
sources: [https://github.com/jamwithai/production-agentic-rag-course]
confidence: high
contested: false
contradictions: []
---

# Production Agentic RAG Course

> GitHub: [jamwithai/production-agentic-rag-course](https://github.com/jamwithai/production-agentic-rag-course)
> 6.4k ⭐ · 1.5k Fork · 39 Commits · MIT License
> 本地路径: `~/Downloads/workspace/agent-learning-vault/production-agentic-rag-course/`

---

## 是什么

面向学习者的生产级 RAG 系统工程课程。从零构建 arXiv 论文研究助手，逐步掌握现代 RAG 系统的全链路工程能力。

**核心理念**：先打搜索基础（BM25 关键词搜索），再叠向 AI 增强（向量混合检索）——而非上来就向量。

---

## 技术栈

| 组件 | 用途 |
|------|------|
| FastAPI | REST API（port 8000） |
| PostgreSQL 16 | 论文元数据存储 |
| OpenSearch 2.19 | 混合检索引擎 |
| Apache Airflow 3.0 | 数据管道调度 |
| Ollama | 本地 LLM |
| Docling | 科学 PDF 解析 |
| Gradio | 用户聊天界面 |
| Langfuse | RAG 监控追踪 |
| Redis | 响应缓存 |
| LangGraph | Agentic RAG 工作流 |
| Telegram Bot | 移动端接入 |

---

## 7 周课程

| 周 | 主题 | 产出 |
|:--:|------|------|
| 1 | 基础设施 | Docker + FastAPI + PG + OpenSearch + Airflow |
| 2 | 数据管道 | arXiv API → Docling PDF 解析 → Airflow DAG |
| 3 | 关键词搜索 | BM25 + OpenSearch Query DSL + 相关性评分 |
| 4 | 混合检索 | 智能分块 + 语义理解 + 关键词结合 |
| 5 | 完整 RAG | 本地 LLM + 流式响应 + Gradio 界面 |
| 6 | 生产监控 | Langfuse 追踪 + Redis 缓存 |
| 7 | Agentic RAG | LangGraph 决策 + Telegram Bot 移动端 |

---

## 学习方法

```bash
cd ~/Downloads/workspace/agent-learning-vault/production-agentic-rag-course

# 1. 配置环境
cp .env.example .env

# 2. 安装依赖（Python 3.12+, uv 包管理器）
uv sync

# 3. 启动全部服务
docker compose up --build -d

# 4. 验证
curl http://localhost:8000/api/v1/health

# 5. 启动对应周的 Jupyter notebook
uv run jupyter notebook notebooks/week1/week1_setup.ipynb
```

---

## 服务端口

| 服务 | 端口 | 地址 |
|------|:--:|------|
| API 文档 | 8000 | http://localhost:8000/docs |
| Gradio 聊天 | 7861 | http://localhost:7861 |
| Langfuse 监控 | 3000 | http://localhost:3000 |
| Airflow | 8080 | http://localhost:8080 |
| OpenSearch | 5601 | http://localhost:5601 |

---

## 与学习路线的对照

- L2（API + 工作流）：Week 1-3 覆盖
- L3（代码级 Agent）：Week 5-7 全中
- RAG 知识库：Week 4 分块策略即最优实践
- 变现路径 C（做自己的 AI 产品）：Week 7 Telegram Bot 就是 MVP 范例

---

## 相关笔记

- [[Agent开发赚钱学习路线]]
- [[AI-Agent-核心概念对照]]
