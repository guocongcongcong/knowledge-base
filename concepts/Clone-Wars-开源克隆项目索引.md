---
title: "Clone-Wars — 100+热门网站开源克隆索引"
created: 2026-06-14
updated: 2026-06-14
type: concept
order: 6
tags: [开源项目, 前端学习, 克隆项目, 学习路径, 全栈实践]
confidence: high
contested: false
contradictions: []
related: ["[[freeCodeCamp-开源编程教育平台]]", "[[苏格拉底·七 系统分析]]"]
---

# Clone-Wars — 100+热门网站开源克隆索引

## 一句话

**35k star，100+热门网站的开源克隆项目合集，每个项目标注源码、演示、技术栈、教程链接和 GitHub 星标。** 前端学习者的"实践地图"——想学什么技术栈，就去找对应的克隆项目拆解。

## 基本信息

| 维度 | 数据 |
|------|------|
| Stars | 35,204 |
| Forks | 3,169 |
| 创建 | 2020年12月（Gourav Goyal） |
| 网址 | gourav.io/clone-wars |
| GitHub | github.com/GorvGoyl/Clone-Wars |

## 项目结构

分为两类表格：

### 表1：带教程的克隆（Clones with Tutorials）

全栈克隆 + 免费视频教程。适合"跟着做一遍"：

| 克隆对象 | 技术栈 | 教程来源 |
|---------|--------|---------|
| Airbnb | Sanity SDK, Next.js, React Hooks | YouTube |
| Instagram | React Native, Firebase, Redux | freeCodeCamp |
| Netflix | React, Apollo GraphQL, DataStax | YouTube |
| Twitter | Vue.js, Quasar, Firebase | freeCodeCamp |
| WhatsApp | Android Studio, Firebase | freeCodeCamp |
| Discord | Django | YouTube (Traversy Media) |
| YouTube | React JS, Rapid API, Material UI 5 | YouTube |

### 表2：克隆/替代品（无需教程，直接拆源码）

100+项目，覆盖所有主流产品：

- **社交媒体**：Reddit (Lemmy/PieFed)、Twitter、Instagram、TikTok、Snapchat
- **音视频**：Spotify (10+个克隆)、Netflix (15+个克隆)、YouTube、Twitch
- **工具**：Notion (Focalboard/AppFlowy)、Airtable (Baserow/NocoDB)、Postman (Hoppscotch/Insomnia)
- **通讯**：Slack (Mattermost/Rocket.Chat/Zulip)、Telegram (Tinode)、WhatsApp
- **电商**：Amazon、Airbnb、Shopify
- **其他**：1Password (Bitwarden)、Algolia (MeiliSearch)、Obsidian (Zettlr)

## 为什么值得入库

### 1. 它是一个"技术栈 → 实战项目"的映射表

传统学习路径是"先学React，再找项目练"。Clone-Wars 反转了——"你想做Instagram？好，这个克隆用React Native + Firebase，去拆它的源码，同时学这两样。"

对 socratic-seven 的学习者来说，这比纯教材更有效：教材讲概念，Clone-Wars 提供可拆解的真实代码。

### 2. 它证明了"克隆学习法"的有效性

Airbnb、Netflix、Spotify 这些产品的克隆版，功能少得多但架构是真实的。拆解一个 Netflix 克隆比读十篇 React 教程学到的东西多——因为你在看一个完整系统如何组织，而不是孤立地学组件语法。

这种"拆解克隆→对比原始产品→理解设计决策"的三步法与苏格拉底教学法天然契合——AI伙伴可以问："为什么这个 Spotify 克隆用了 Redux 而不是 Context？你看看原始 Spotify 的架构，你觉得他们会用什么？"

### 3. 可以直接作为 socratic-seven 的实践教材

建议：
1. 将 Clone-Wars 的精选项目（Airbnb/Spotify/Netflix/Notion 克隆）作为 socratic-seven 的"拆解练习"教材
2. 每一轮练习 = 拆一个克隆的源码 → AI追问设计决策 → 自己实现一个最小版本
3. 这比看教程效率高得多——你不是在学语法，你是在逆向工程一个产品

## 最佳拆解候选（按学习价值排序）

| 排名 | 克隆对象 | 推荐理由 |
|:---:|------|------|
| 1 | Netflix 克隆 (roseflix) | React + TypeScript + MongoDB 全栈，有演示站 |
| 2 | Spotify 克隆 (angular-spotify) | Angular + TailwindCSS + NgRx 状态管理 |
| 3 | Airbnb 克隆 (realbnb) | Next.js + Prisma + GraphQL + TypeScript |
| 4 | Notion 替代 (AppFlowy) | Flutter + Rust，本地优先的笔记应用 |
| 5 | Reddit 替代 (Lemmy) | ActivityPub + Rust + PostgreSQL，联邦式架构 |

---

*来源：GitHub Trending 2026-06-14 + GitHub API + README全文分析*
