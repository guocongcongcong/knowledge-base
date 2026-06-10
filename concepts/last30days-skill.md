---
title: last30days-skill
created: 2026-06-10
updated: 2026-06-10
type: concept
tags: [ai-tools, skills, research, social-media, claude-code, agent-skills]
sources: [https://github.com/mvanhorn/last30days-skill]
confidence: high
contested: false
contradictions: []
---

# last30days-skill

## 是什么 / What

**一个 AI Agent 技能插件，可跨 Reddit、X、YouTube、TikTok、Hacker News、Polymarket、GitHub 等 12+ 平台搜索近 30 天内任意话题的讨论，并按真实用户参与度（点赞/转发/下注金额）排名合成结构化摘要。**

An AI agent skill that researches any topic across 12+ platforms (Reddit, X, YouTube, TikTok, Hacker News, Polymarket, GitHub, etc.) within the last 30 days, scoring results by real user engagement (upvotes/likes/real-money bets) and synthesizing a grounded summary.

- **作者**: [mvanhorn](https://github.com/mvanhorn)
- **仓库**: [github.com/mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)
- **Star**: ~37,000+ (曾 GitHub Trending #1)
- **语言**: Python 3.12+ + Node.js (vendorized Bird X 客户端)
- **许可**: MIT
- **兼容**: Claude Code / Codex / Cursor / GitHub Copilot / Gemini CLI / Hermes Agent 等 50+ [Agent Skills](https://agentskills.io) 宿主机

## 核心理念 / Core Idea

Google 编辑排名。**last30days 按人的真实行为排名。**

Reddit 点赞。X 转发。YouTube 观看量。TikTok 互动。Polymarket 真金白银下注的预测赔率 —— 每天都有人在用注意力和钱包投票。last30days 并行搜索所有平台，用真实参与度评分，然后 AI 合成一份简洁摘要。

**没有单一 AI 能做到这一点。** Google 不碰 Reddit 评论。ChatGPT 有 Reddit 但搜不了 X。Gemini 有 YouTube 但没有 Reddit。Claude 原生一个都没有。但你可以自带 API key 和浏览器 token，让 Agent 一次搜完所有平台。

## 数据源 / Sources

| 来源 | 免费/付费 | 需要什么 |
|------|----------|---------|
| **Reddit** (含评论+点赞数) | 免费 | 无需任何配置 |
| **Hacker News** | 免费 | 无需任何配置 |
| **Polymarket** (预测市场赔率) | 免费 | 无需任何配置 |
| **GitHub** (PR/issue/repo) | 免费 | `gh` CLI 已安装即可 |
| **YouTube** (完整字幕) | 免费 | `brew install yt-dlp` |
| **X / Twitter** | 免费 | 浏览器登录 x.com（cookie-jar）或 XAI_API_KEY（付费） |
| **TikTok** | 100次免费 | `SCRAPECREATORS_API_KEY` |
| **Instagram Reels** | 100次免费 | 同上 |
| **Threads** | 100次免费 | 同上 |
| **Bluesky** | 免费 | `BSKY_HANDLE` + app password |
| **Truth Social** | 免费 | `TRUTHSOCIAL_TOKEN` |
| **Perplexity Sonar** (深度搜索+引用) | 按量付费 | `OPENROUTER_API_KEY` |
| **Web 搜索** (Brave/Exa/Serper) | 2000次/月免费 | `BRAVE_API_KEY` |

## 工作流程 / How It Works

### 7 步流水线

```
用户: /last30days "NVIDIA 财报反应"
   ↓
1. 解析意图 → 识别 QUERY_TYPE（GENERAL/NEWS/COMPARISON/PROMPTING/RECOMMENDATIONS）
   ↓
2. 智能前置研究 (Step 0.55) → 解析 X handles、GitHub repos、subreddits、TikTok hashtags
   ↓
3. 并行搜索 (ThreadPoolExecutor) → Reddit + X + YouTube + TikTok + HN + Polymarket + GitHub + ...
   ↓
4. 丰富化 (enrichment) → 获取真实点赞/评论/字幕（不依赖 AI 估算）
   ↓
5. 跨源聚合 (cluster merging) → "同一事件在 Reddit+X+YT 三条线"合并为一个集群
   ↓
6. 评分排序 → 按参与度、相关性、新鲜度加权
   ↓
7. 合成摘要 → AI 生成"人们真正在讨论什么"的简报（带来源引用）
```

### 关键架构特点

- **智能解析 (Intelligent Search)**: v3 引擎不会盲目搜关键词。输入 "OpenClaw" → 自动解析出 @steipete、r/openclaw、r/ClaudeCode、正确的 YouTube 频道和 TikTok 话题标签。先理解、再搜索。
- **跨源去重 (Cross-Source Cluster Merging)**: 同一个故事出现在 Reddit/X/YouTube 三个平台 → 合并为一个集群，不是三个重复条目。
- **Reddit 公开 JSON 增强**: 不依赖 API key，直接拉取 Reddit `.json` 端点获取真实点赞数、评论数、点赞率、top 10 评论。
- **X 双后端**: 优先使用免费 Bird 客户端 (cookie-jar 认证)，fallback 到 xAI API。
- **GitHub 人物模式**: 当 topic 是一个人时，从关键词搜索切换为 `user:{handle}` 作者范围搜索 → "他们最近提交了什么、合并了什么 PR"。

## v3 新特性 / v3 Features

1. **可分享的 HTML 简报**: `/last30days <topic> --emit=html` → 自包含暗色主题 HTML 文件，可直接丢到 Slack/邮件/Notion
2. **智能搜索 (Intelligent Search)**: Python 前置大脑解析实体 → 搜对的人和社区
3. **Best Takes**: 第二裁判评分幽默度和病毒传播度 → 每条搜索附带最精彩的吐槽
4. **单次对比 (Single-Pass Comparison)**: "CLI vs MCP" 过去三次串行跑需要 12 分钟，v3 一次跑 3 分钟
5. **自动发现竞品对比**: `/last30days OpenAI --competitors` → 自动发现 Anthropic、xAI 并做三方对比
6. **ELI5 模式**: 说 "eli5 on" 用白话重写同一份数据

## 安装方式 / Install

| 平台 | 命令 | 更新方式 |
|------|------|---------|
| **Claude Code** (推荐) | `/plugin marketplace add mvanhorn/last30days-skill` | 市场自动更新 |
| **Codex/Cursor/Copilot/Gemini** | `npx skills add mvanhorn/last30days-skill -g` | `npx skills update last30days -g` |
| **claude.ai** (Web) | 下载 `.skill` 文件上传 | 重新下载上传 |
| **OpenClaw** | `clawhub install last30days-official` | `clawhub update` |
| **手动** | `git clone` + `ln -s skills/last30days ~/.claude/skills/last30days` | `git pull` |

## 配置要点 / Configuration

- **输出目录**: 默认为 `~/Documents/Last30Days/`，设置 `LAST30DAYS_MEMORY_DIR` 覆盖
- **趋势监控**: `--store` 持久化到 SQLite → `watchlist.py` 定时运行 → `briefing.py` 生成日报/周报
- **`.env` 文件位置**: 项目级 `.claude/last30days.env`（优先）或全局 `~/.config/last30days/.env`
- **macOS Keychain**: 可用 `setup-keychain.sh` 将 API key 存入系统钥匙串
- **多项认证**: `AUTH_TOKEN` + `CT0`（X cookie）、`XAI_API_KEY`、`SCRAPECREATORS_API_KEY`、`BRAVE_API_KEY`、`BSKY_HANDLE` + `BSKY_APP_PASSWORD`

## 典型使用场景 / Use Cases

1. **会前调查**: `/last30days Peter Steinberger` → 本月 23 个 PR、OpenAI Codex 团队、对抗 Anthropic 禁令、打造 LobsterOS
2. **突发事件**: `/last30days 伊朗 美国` → 战争第 38 天、特朗普最后通牒、油价 $126、PolyMarket 74% 停火概率
3. **工具对比**: `/last30days OpenClaw vs Hermes` → 实时 GitHub 星数对比、架构差异、社区讨论
4. **出行前查**: `/last30days Universal Epic Universe` → 在建项目、排队时间、年票状态
5. **快速学习**: `/last30days AI 视频工具提示词写法` → 社区最佳实践 + 直接输出可用的 production prompt

## 输出合约 / Output Contract

last30days 有严格的输出格式约定（5 条 LAW），确保每次搜索都产出一致、高质量、无 AI 套话的简报：

- **LAW 1**: 不在末尾加 `Sources:` 块（引擎的 emoji-tree footer 就是引用）
- **LAW 2**: 不用自创标题（badge 行就是标题），比较类查询除外
- **LAW 3**: 不用 em-dash（用 ` - ` 代替 `—`）
- **LAW 4**: 不用 `##` section 标题，比较类查询除外
- **LAW 5**: 引擎 footer（`✅ All agents reported back!`）必须原样吐出

## 关键文件结构 / Key Files

| 文件 | 用途 |
|------|------|
| `skills/last30days/SKILL.md` | 技能规范（1709行，运行时合约） |
| `skills/last30days/scripts/last30days.py` | 主引擎入口 |
| `skills/last30days/scripts/lib/pipeline.py` | 多源检索编排 |
| `skills/last30days/scripts/lib/reddit_public.py` | Reddit 公开 JSON 搜索 |
| `skills/last30days/scripts/lib/bird_x.py` | X/Twitter 免费搜索（Bird 客户端） |
| `skills/last30days/scripts/lib/dedupe.py` | URL 去重 |
| `skills/last30days/scripts/lib/relevance.py` | 相关性评分 |
| `CONFIGURATION.md` | 用户配置参考（API key / flag / 趋势监控） |
| `docs/how-search-works.md` | 搜索引擎架构文档 |
| `CONCEPTS.md` | 术语表（Skill / Engine / Harness） |

## 相关项目 / Related

- [[goose]] — 开源 AI Agent 框架，可本地开发
- [[tolaria]] — 开源 Markdown 知识库桌面应用
- [[hermes-agent]] — 多平台 AI Agent（微信/Telegram/Discord）
- [[claude-code]] — 宿主平台，最常用 Harness
