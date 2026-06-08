# GitHub 热门项目待校验列表

> 2026-06-08 · 来源：GitHub Trending Daily

---

## 1. mvanhorn/last30days-skill

| 项目 | 详情 |
|------|------|
| **地址** | https://github.com/mvanhorn/last30days-skill |
| **星数** | 31,144 ⭐ |
| **语言** | Python 3.12+ |
| **本地路径** | `~/Downloads/workspace/gh-projects/last30days-skill/` |
| **大小** | 37MB |
| **许可** | MIT |

### 简介
AI Agent 技能包——跨 Reddit / X / YouTube / HN / Polymarket 搜索任意话题，由 AI 代理合成精炼摘要。安装方式：`npx skills add mvanhorn/last30days-skill -g`，在 Claude Code / Codex / Cursor 等 50+ Agent Skills 宿主中通过 `/last30days <topic>` 调用。

### 运行状态
- ⚠️ **不可直接测试**：需要 API Key（Reddit、X、YouTube 等），无 Key 时脚本超时
- Python 3.12 环境 OK
- 零依赖（纯 Python 标准库 + 第三方 API）

### 校验建议
- [ ] 配置 Reddit API Key 后测试 `/last30days` 搜索功能
- [ ] 验证跨平台（Claude Code / Codex / Hermes）安装兼容性
- [ ] 检查数据去重和摘要质量

---

## 2. Leonxlnx/taste-skill

| 项目 | 详情 |
|------|------|
| **地址** | https://github.com/Leonxlnx/taste-skill |
| **星数** | 36,743 ⭐ |
| **语言** | TypeScript / Markdown (Agent Skills) |
| **本地路径** | `~/Downloads/workspace/gh-projects/taste-skill/` |
| **大小** | 5.5MB |
| **许可** | MIT |

### 简介
"反流水线前端框架"——给 AI Agent 注入设计品味。包含 13 个技能（taste-skill、brutalist-skill、minimalist-skill、image-to-code-skill、imagegen-frontend-web 等），阻止 AI 生成无聊的通用 UI。官网：tasteskill.dev。

### 技能列表
| 技能 | 大小 | 用途 |
|------|------|------|
| taste-skill | 1,206 行 | 反模板前端设计 |
| image-to-code-skill | 1,228 行 | 图转代码 |
| imagegen-frontend-mobile | 1,465 行 | 移动端参考图生成 |
| imagegen-frontend-web | 987 行 | Web 端参考图生成 |
| brandkit | 798 行 | 品牌工具包 |
| brutalist-skill | 92 行 | 野兽派风格 |
| minimalist-skill | 85 行 | 极简风格 |
| soft-skill | 98 行 | 柔和风格 |
| redesign-skill | 178 行 | 重设计 |
| stitch-skill | 184 行 | 页面拼接 |

### 运行状态
- ✅ **已下载可用**：纯 Markdown + Shell 技能包，无需运行环境
- 安装：`npx skills add Leonxlnx/taste-skill -g`

### 校验建议
- [ ] 在 Claude Code 中加载技能，测试生成的网页设计质量
- [ ] 对比使用 taste-skill 前后的 UI 差异
- [ ] 验证与 Hermes + gstack 的兼容性

---

## 3. lfnovo/open-notebook

| 项目 | 详情 |
|------|------|
| **地址** | https://github.com/lfnovo/open-notebook |
| **星数** | 27,293 ⭐ |
| **语言** | Python 3.11+ / TypeScript (Next.js) |
| **本地路径** | `~/Downloads/workspace/gh-projects/open-notebook/` |
| **大小** | 8.9MB |
| **许可** | MIT |

### 简介
NotebookLM 的开源替代品——隐私优先的 AI 研究助手。上传 PDF/音频/视频/网页，生成笔记、语义搜索、AI 聊天、专业播客。**三件套架构**：React/Next.js 前端 + FastAPI 后端 + SurrealDB 图数据库。支持 8+ AI 提供商（OpenAI/Anthropic/Google/Groq/Ollama 等）。

### 运行要求
- Docker Compose（推荐，一键启动 SurrealDB + API + Web UI）
- 或手动：SurrealDB + Python 3.11 + Node.js

### 运行状态
- ⚠️ **待测试**：Docker 方案最可行，需 `docker compose up`
- 依赖较多（FastAPI、LangGraph、SurrealDB、content-core 等）

### 校验建议
- [ ] Docker Compose 启动全栈（`docker compose up`）
- [ ] 上传 PDF 文档测试内容提取
- [ ] 测试语义搜索和 AI 问答
- [ ] 测试播客生成功能
- [ ] 对比 Google NotebookLM 的功能完整度

---

## Hermes Agent 更新

| 项目 | 状态 |
|------|------|
| **当前版本** | `a6a0a5b1b` (2026-06-05) |
| **最新版本** | `30c791361` (v2026.6.5 + 15 commits) |
| **更新状态** | ✅ **已更新** |
| **更新内容** | api_server 健康检查、credits 追踪系统、i18n 多语言（日/繁中）、桌面端多 Profile、keybind 系统、Discord 语音混音等 |

---

## 汇总

| 项目 | 可运行 | 优先级 | 下一步 |
|------|--------|--------|--------|
| last30days-skill | 需 API Key | ⭐⭐⭐ | 配置 Key → 测试搜索 |
| taste-skill | 立即可用 | ⭐⭐⭐ | 加载到 Claude Code 测试设计质量 |
| open-notebook | Docker 启动 | ⭐⭐ | `docker compose up` 全栈验证 |
| hermes-agent | ✅ 已更新 | - | 重启 Gateway 生效 |

---

*生成时间：2026-06-08 · 数据源：[GitHub Trending](https://github.com/trending?since=daily)*
