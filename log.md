# Wiki Log

## [2026-05-18] fix | index.md + log.md 修复
- index.md 内容重复叠加问题修复，重新组织为 19 页四组结构
- log.md 同样问题修复
- 清理概念页中不存在的 wikilink（死链接导致关系图孤立节点）

## [2026-05-18] create | AI Agent 开发学习路线
- 创建: queries/ai-agent-learning-guide.md（五层递进：概念→Skill→工具/MCP→Context→Harness）

## [2026-05-18] create | Harness Engineering 驾驭工程
- 来源: awesome-harness-engineering (975⭐) + 《马书》(1.3K⭐) + Martin Fowler + Anthropic/OpenAI/Google 官方
- 创建: concepts/harness-engineering.md（六大层级+权威来源+退化设计原则+Claude Code源码分析）

## [2026-05-18] create | cheat-on-content 内容创作 AI 校准系统
- 来源: GitHub XBuilderLAB/cheat-on-content (2.3K⭐)
- 创建: concepts/cheat-on-content.md（闭环架构+命令+安装+与通用AI区别）

## [2026-05-18] create | Pretext 文本测量引擎
- 识别视频10「前端渲染新革命」项目为 chenglou/pretext (47K⭐)
- 更新: raw/transcripts/douyin-frontend-rendering-revolution.md（补充项目信息）
- 创建: concepts/pretext-text-engine.md（API用法+本地Demo+适用场景）
- 本地Demo已构建: /tmp/pretext-demo/ (http://localhost:8888)

## [2026-05-18] ingest | 抖音视频批量导入（9个视频 → 6个概念页）
- 来源: 10个抖音链接（含1个重复），提取自 Ali厂长、力气强、小常、阿坚学不会AI、木子不写代码、Chris IT先生、开源项目盘点、广叔AI
- 创建 raw 转录:
  - raw/transcripts/douyin-claude-md-over-200-lines.md — CLAUDE.md超过200行后最该做的事 (Ali厂长)
  - raw/transcripts/douyin-claude-md-too-long-agent-ignores.md — CLAUDE.md越长Agent越不听 (Ali厂长)
  - raw/transcripts/douyin-claude-code-mcp-browser.md — Claude Code MCP浏览器联动 (力气强)
  - raw/transcripts/douyin-obsidian-creation-workflow.md — Obsidian创作全流程 (小常)
  - raw/transcripts/douyin-ai-paper-writing-prompt.md — AI论文写作Prompt (阿坚)
  - raw/transcripts/douyin-ai-video-editing-hyperframe.md — AI视频剪辑Hyperframe (木子)
  - raw/transcripts/douyin-hermes-agent-intro.md — HermesAgent介绍 (Chris IT先生)
  - raw/transcripts/douyin-deer-flow-multi-agent.md — deer-flow多智能体 (开源项目盘点)
  - raw/transcripts/douyin-frontend-rendering-revolution.md — 前端渲染新革命 (广叔AI)
- 创建概念页:
  - concepts/claude-md-optimization.md — 合并视频1+6，CLAUDE.md三步优化法+五个常见坑
  - concepts/claude-code-mcp-browser.md — MCP浏览器联动配置步骤
  - concepts/obsidian-card-note-workflow.md — 卡片笔记写作法三阶段全流程
  - concepts/ai-video-editing-hyperframe.md — Hyperframe智能体驱动视频剪辑
  - concepts/deer-flow-multi-agent.md — deer-flow并行多智能体架构与竞品对比
- 更新: index.md (总页面数 11→16)

## [2026-05-16] create | Hermes 日记推送工作流
- 创建: concepts/Hermes-日记推送工作流.md（Obsidian→Notion→GitHub 三端推送+API要点+坑）

## [2026-05-16] create | Hermes Agent 三层路由架构设计
- 创建: concepts/Hermes-Agent-三层路由架构设计.md（实战复盘→三层架构→设计决策→推广）
- 配套: GitHub Gist + routing-template skill + SOUL.md

## [2026-05-16] create | Claude Code 6个隐藏能力
- 来源: 抖音@阿森编程日记
- 创建: concepts/Claude-Code-6个隐藏能力.md（/init、Plan Mode、/compact、自定义命令、Sub Agent、Hooks）

## [2026-05-16] create | AI Agent 核心概念对照
- 创建: concepts/AI-Agent-核心概念对照.md（Prompt/System Prompt/Soul/Memory/Skill/CLAUDE.md/Tool/MCP 八个概念对照）

## [2026-05-15] update | 补充 Karpathy 模式缺失项
- 创建: raw/ 子目录（articles/papers/transcripts/assets）+ README
- 更新: SCHEMA.md — 添加 Architecture 三层说明、confidence/contested 字段定义、Provenance Markers 出处标记、raw sources frontmatter 规范、Update Policy
- 更新: 全部 6 个 wiki 页面补充 confidence/contested/contradictions 字段
  - concepts/马克思主义.md — confidence: low（单来源 web-search）
  - concepts/论持久战.md — confidence: low（单来源 web-search）
  - concepts/Claude-Code-7个必装Skill.md — confidence: medium（抖音+GitHub 交叉验证）
  - concepts/axton-obsidian-visual-skills.md — confidence: medium（抖音+GitHub 交叉验证）
  - entities/家味协同项目概览.md — confidence: high（可直接验证的项目文件）
  - queries/知识库压缩工具调研.md — confidence: low（AI 生成，未验证）

## [2026-05-08] create | Wiki 初始化

## [2026-05-08] ingest | 世界观铺设
- 明知山小说设定（已迁移至 workspace/明知山）

## [2026-05-09] create | 关键角色/妖/地点设定
- 明知山小说设定（已迁移至 workspace/明知山）

## [2026-05-09] create | 项目记忆入库
- 创建: entities/家味协同项目概览.md

## [2026-05-09] create | 知识库压缩工具调研
- 创建: queries/知识库压缩工具调研.md

## [2026-05-09] migrate | 明知山内容迁移至 workspace
- 迁移 24 页面 → ~/Downloads/workspace/明知山/
- 删除 knowledge-base 中重复文件
- 保留: 项目概览、工具调研

## [2026-05-09] ingest | 马克思主义 + 论持久战
- 创建: concepts/马克思主义.md（哲学·政治经济学·科学社会主义）
- 创建: concepts/论持久战.md（三阶段·人民战争·游击战战略）
- 更新: index.md（5页）

## [2026-05-13] ingest | Claude Code 7个必装Skill + Obsidian可视化Skill
- 来源: 抖音@阿森编程日记 / @赛博牛马
- 创建: concepts/Claude-Code-7个必装Skill.md（Superpowers⭐189k/PDF内置/humanizer-zh⭐7.5k/planning-with-files⭐21k/frontend-design⭐29/skill-review内置/skill-creator⭐915）
- 创建: concepts/axton-obsidian-visual-skills.md（⭐2.8k, Excalidraw/Mermaid/Canvas）
- 补充: anthropics/claude-code⭐123k, obra/superpowers⭐189k, superpowers-zh⭐2.8k
- 更新: 两页均加入 GitHub star 数据、仓库链接、安装命令
- 更新: index.md（7页）
