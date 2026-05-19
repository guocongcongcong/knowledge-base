---
title: Hermes 日记推送工作流
created: 2026-05-16
updated: 2026-05-16
type: concept
tags: [hermes, diary, notion, github, automation, 日记系统]
sources: ["Hermes session 2026-05-16 实战"]
confidence: high
contested: false
contradictions: []
---

# Hermes 日记推送工作流

每天会话结束后，Hermes 将当日工作自动记录到三个地方：Obsidian 本地文件、Notion 数据库、GitHub Gist 公网备份。

## 为什么是这三个

| 目标 | 用途 | 特点 |
|------|------|------|
| Obsidian（本地） | 日常浏览、全文检索、与知识库联动 | 本地文件，Obsidian 双向链接 |
| Notion | 数据库管理、标签筛选、跨设备查看 | 结构化属性，select/multi_select 分类 |
| GitHub Gist | 公网备份、分享链接 | 永久链接，无需登录查看 |

**不推微信。** 微信是即时通讯工具，不适合存档类内容。日记是知识资产，放在可检索、可链接的地方更有价值。

## 文件结构

### Obsidian 日记

路径：`~/Downloads/workspace/hermes-diary/Daily/2026-MM-DD.md`

格式：
```markdown
---
date: YYYY-MM-DD
tags: [标签列表]
---

# YYYY-MM-DD

## 对话
- 条目1
- 条目2

## 完成
- 条目1

## 推送状态
- Notion: ✅ / ❌
- GitHub: ✅ / ❌

## 备忘
- 条目1
```

### Notion 数据库

- DB ID：`35cb3f11-a33d-80ec-99b2-f038b1b6ea93`
- 名称：Hermes日记
- API 版本：`2022-06-28`

属性：

| 属性名 | 类型 | 说明 |
|--------|------|------|
| 日期，名称 | title | 日期格式 YYYY-MM-DD |
| 分类 | select | 开发/写作/健身/生活/系统 |
| 关键词 | multi_select | hermes/烟火神州/自动化/日记系统/长篇/Obsidian 等 |
| 摘要 | rich_text | 一句话概要 |
| Obsidian文件 | url | Obsidian 文件链接 |
| 状态 | select | 已同步/草稿/已完成 |

**正文（blocks）**：创建页面后，用 `PATCH /v1/blocks/{page_id}/children` 写入，结构与 Obsidian 日记镜像。使用 heading_2 + bulleted_list_item。

### GitHub Gist

用 `gh gist create` 上传日记文件。公开 Gist，获取永久链接后写回日记的「推送状态」栏。

```bash
gh gist create --public --desc "Hermes 日记 YYYY-MM-DD" \
  ~/Downloads/workspace/hermes-diary/Daily/YYYY-MM-DD.md
```

## 推送流程

```
会话结束
  │
  ├─→ 1. 写 Obsidian 日记文件
  │     YAML frontmatter + ## 对话 + ## 完成 + ## 推送状态 + ## 备忘
  │
  ├─→ 2. 同步 Notion
  │     ① 查 schema 确认属性名
  │     ② POST /v1/pages 创建页面（properties）
  │     ③ PATCH /v1/blocks/{id}/children 写入正文
  │
  ├─→ 3. 推 GitHub Gist
  │     gh gist create 上传 .md 文件
  │     获取 URL → 写回日记推送状态栏
  │
  └─→ 4. 更新 CLAUDE.md（如有推送目标变更）
```

## Notion API 要点

### 查 schema（每次先做）

```bash
curl -s "https://api.notion.com/v1/databases/35cb3f11-a33d-80ec-99b2-f038b1b6ea93" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28"
```

### 创建页面

```bash
curl -s -X POST "https://api.notion.com/v1/pages" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "parent": {"database_id": "35cb3f11-a33d-80ec-99b2-f038b1b6ea93"},
    "properties": {
      "日期，名称": {"title": [{"text": {"content": "2026-05-16"}}]},
      "分类": {"select": {"name": "系统"}},
      "关键词": {"multi_select": [{"name": "hermes"}]},
      "状态": {"select": {"name": "已完成"}},
      "摘要": {"rich_text": [{"text": {"content": "概要"}}]}
    }
  }'
```

### 写入正文

```bash
curl -s -X PATCH "https://api.notion.com/v1/blocks/{page_id}/children" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"children": [...]}'
```

每次最多 100 blocks。

## 坑

- **属性名**："日期，名称" 不是 "日期名称"。"日期，名称" 中间是中文逗号。每次先查 schema 不靠记忆
- **API 版本**：数据库创建和写入用 `2022-06-28`，搜索用 `2025-09-03`
- **关键词**：只使用 schema 里已有的 multi_select options，不新增（否则报错）
- **分类**：只使用已有 select options：开发/写作/健身/生活/系统
- **env var 名**：`NOTION_API_KEY`，不是 `NOTION_TOKEN`

## 相关

- [[Hermes-Agent-三层路由架构设计]] — 其中 routing skill 触发了本条日记的写入
- [[AI-Agent-核心概念对照]] — Memory/Skill/CLAUDE.md 在日记推送中的角色
- [[Claude-Code-6个隐藏能力]] — 子 agent 并行写小说的技术基础
