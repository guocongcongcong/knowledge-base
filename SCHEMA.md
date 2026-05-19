# Wiki Schema

## Domain
通用知识库

## Architecture

三层结构（Karpathy LLM Wiki 模式）：

- **Layer 1 — raw/**: 原始资料，不可变。LLM 只读不写。
- **Layer 2 — concepts/ entities/ queries/**: Wiki 页面，LLM 编写维护。**已配置为 Notion Bases 数据库**（表格/看板视图），每页的 frontmatter 自动映射为数据库列。
- **Layer 3 — SCHEMA.md**: 行为规范，约束 LLM 操作。
- **Templates/**: Obsidian 模板，LLM 通过模板格式写入新页面。Hermes 不读模板文件，直接按模板格式 write_file。

## Conventions
- 文件名: 中文或小写英文+连字符
- 每个页面必须含 YAML frontmatter（含 confidence 和 contested 字段）
- 用 `[[wikilinks]]` 链接其他页面 (每页 ≥2 个出链)
- 更新页面必更新 `updated` 日期
- 新页面必须加入 `index.md`
- 所有操作追加到 `log.md`
- 消化来源时，原始内容存入 `raw/` 对应子目录

## Frontmatter
```yaml
---
title: 页面标题
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | comparison | query
tags: []
sources: []
# 质量标记（必填）
confidence: high | medium | low   # 论断的可信度
contested: false                   # true=存在未解决的矛盾
contradictions: []                 # 与本页矛盾的页面 slug 列表
---
```

### confidence 说明
- **high**: 多来源交叉验证，事实明确
- **medium**: 单一可靠来源，或部分验证
- **low**: 单一来源、观点性强、或信息可能过时

### contested 说明
当新信息与现有内容矛盾时：
1. 不静默覆盖
2. 两方观点都保留，标注日期和出处
3. 标记 `contested: true`
4. 填入 `contradictions: [page-slug]`

## Provenance Markers
多来源（3+）页面在段落末尾标注出处：
```
这是某个论断。^[raw/articles/source-name.md]
```
让读者能追溯每句话的来源，不必重读全文。

## Tag Taxonomy
- **文化/神话**: mythology, folklore, symbolism, chinese-culture, five-elements
- **历史**: ancient-china, dynasty, archaeology
- **天文**: astronomy, constellation, star-lore
- **哲学**: taoism, confucianism, yin-yang, fengshui
- **AI 工具**: ai-tools, claude-code, skills, obsidian, knowledge-base
- **Meta**: comparison, timeline, summary

## Page Thresholds
- 出现 2+ 来源 或 单来源核心主题 → 创建页面
- 超过 200 行 → 拆分子页面
- 完全被替代 → 归档到 `_archive/`
- 单来源页面默认 `confidence: low`，除非来源权威性极高

## Raw Sources 规范
存入 `raw/` 的文件必须含 frontmatter：
```yaml
---
source_url: https://原始链接
ingested: YYYY-MM-DD
sha256: <body 的 hex digest>
---
```
`sha256` 用于重新消化同一 URL 时检测内容漂移。

## Update Policy
新信息与现有内容矛盾时：
1. 检查日期——新来源通常取代旧来源
2. 如确实矛盾，保留两方观点并标注日期
3. frontmatter 标记 `contested: true` + `contradictions: [page]`
4. Lint 时标记供人工审核
