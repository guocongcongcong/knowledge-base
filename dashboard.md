---
cssclass: dashboard
---

<style>
  :root {
    --db-bg: #1a1b2e;
    --db-card: #232438;
    --db-card-hover: #2a2b42;
    --db-accent: #7c5cfc;
    --db-accent2: #5b8def;
    --db-text: #e2e8f0;
    --db-text-muted: #8b8fa3;
    --db-border: #2d2e42;
  }

  body {
    --db-bg: #1a1b2e;
    --db-card: #232438;
    --db-card-hover: #2a2b42;
    --db-accent: #7c5cfc;
    --db-accent2: #5b8def;
    --db-text: #e2e8f0;
    --db-text-muted: #8b8fa3;
    --db-border: #2d2e42;
  }

  .db-wrap {
    max-width: 960px;
    margin: 0 auto;
    padding: 48px 32px;
    font-family: -apple-system, BlinkMacSystemFont, 'Inter', sans-serif;
    color: var(--db-text);
    line-height: 1.6;
  }

  .db-header {
    margin-bottom: 52px;
  }
  .db-header h1 {
    font-size: 34px;
    font-weight: 800;
    letter-spacing: -0.5px;
    margin: 0 0 8px 0;
    background: linear-gradient(135deg, var(--db-accent), var(--db-accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .db-header .sub {
    font-size: 14px;
    color: var(--db-text-muted);
  }

  .db-stats {
    display: flex;
    gap: 16px;
    margin-bottom: 48px;
  }
  .db-stat-card {
    flex: 1;
    background: var(--db-card);
    border: 1px solid var(--db-border);
    border-radius: 12px;
    padding: 20px 24px;
    transition: background 0.2s, transform 0.15s;
  }
  .db-stat-card:hover {
    background: var(--db-card-hover);
    transform: translateY(-2px);
  }
  .db-stat-icon { font-size: 24px; margin-bottom: 8px; }
  .db-stat-number {
    font-size: 28px;
    font-weight: 700;
    letter-spacing: -0.5px;
    color: #fff;
  }
  .db-stat-label {
    font-size: 13px;
    color: var(--db-text-muted);
    margin-top: 2px;
  }

  .db-section-title {
    font-size: 12px;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 1px;
    color: var(--db-text-muted);
    margin: 0 0 14px 0;
  }

  /* Quick Links */
  .db-grid-4 {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 14px;
    margin-bottom: 48px;
  }
  .db-quick-link {
    background: var(--db-card);
    border: 1px solid var(--db-border);
    border-radius: 10px;
    padding: 18px 16px;
    text-align: center;
    text-decoration: none;
    display: block;
    transition: background 0.2s, transform 0.15s;
  }
  .db-quick-link:hover {
    background: var(--db-card-hover);
    transform: translateY(-2px);
  }
  .db-quick-link .icon { font-size: 26px; display: block; margin-bottom: 8px; }
  .db-quick-link .label { font-size: 14px; font-weight: 600; color: var(--db-text); }
  .db-quick-link .sub { font-size: 12px; color: var(--db-text-muted); margin-top: 3px; }

  /* Two Column */
  .db-cols {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
    margin-bottom: 48px;
  }
  .db-card {
    background: var(--db-card);
    border: 1px solid var(--db-border);
    border-radius: 12px;
    padding: 20px 24px;
  }
  .db-card-title {
    font-size: 12px;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.8px;
    color: var(--db-text-muted);
    margin: 0 0 16px 0;
  }
  .db-card-list {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  .db-card-list li {
    padding: 9px 0;
    border-bottom: 1px solid rgba(255,255,255,0.04);
    font-size: 14px;
  }
  .db-card-list li:last-child { border-bottom: none; }
  .db-card-list a {
    color: var(--db-accent2);
    text-decoration: none;
    font-weight: 500;
  }
  .db-card-list a:hover { color: var(--db-accent); }
  .db-card-list .meta {
    font-size: 12px;
    color: var(--db-text-muted);
    margin-left: 8px;
  }

  /* Triggers */
  .db-triggers {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 12px;
    margin-bottom: 48px;
  }
  .db-trigger {
    background: var(--db-card);
    border: 1px solid var(--db-border);
    border-radius: 10px;
    padding: 16px 20px;
    text-decoration: none;
    display: flex;
    align-items: center;
    gap: 12px;
    transition: background 0.2s, transform 0.15s;
  }
  .db-trigger:hover {
    background: var(--db-card-hover);
    transform: translateY(-1px);
  }
  .db-trigger .icon { font-size: 22px; }
  .db-trigger .t-label { font-size: 14px; font-weight: 600; color: var(--db-text); }
  .db-trigger .t-desc { font-size: 12px; color: var(--db-text-muted); margin-top: 2px; }

  /* News */
  .db-news { margin-bottom: 48px; }
  .db-news-card {
    background: var(--db-card);
    border: 1px solid var(--db-border);
    border-radius: 12px;
    padding: 20px 24px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    transition: background 0.2s;
  }
  .db-news-card:hover { background: var(--db-card-hover); }
  .db-news-left { display: flex; align-items: center; gap: 14px; }
  .db-news-left .icon { font-size: 28px; }
  .db-news-left .title { font-size: 15px; font-weight: 600; color: var(--db-text); }
  .db-news-left .desc { font-size: 13px; color: var(--db-text-muted); }
  .db-news-badge {
    background: rgba(124, 92, 252, 0.15);
    color: var(--db-accent);
    font-size: 12px;
    font-weight: 600;
    padding: 4px 12px;
    border-radius: 20px;
  }

  /* Footer */
  .db-footer {
    border-top: 1px solid var(--db-border);
    padding-top: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 13px;
    color: var(--db-text-muted);
  }
  .db-footer .highlight { color: var(--db-accent2); }

  .markdown-preview-view .db-wrap a.internal-link {
    color: var(--db-accent2);
  }
  .markdown-preview-view .db-wrap a.internal-link:hover {
    color: var(--db-accent);
    text-decoration: none;
  }
</style>

<div class="db-wrap">

  <!-- Header -->
  <div class="db-header">
    <h1>✦ 知识库</h1>
    <p class="sub">AI Agent · 工作流 · 深度研究 · 星期一 自动刷新 ⚡</p>
  </div>

  <!-- Stats -->
  <div class="db-stats">
    <div class="db-stat-card">
      <div class="db-stat-icon">📄</div>
      <div class="db-stat-number">55</div>
      <p class="db-stat-label">笔记总数</p>
    </div>
    <div class="db-stat-card">
      <div class="db-stat-icon">🧠</div>
      <div class="db-stat-number">36</div>
      <p class="db-stat-label">概念笔记</p>
    </div>
    <div class="db-stat-card">
      <div class="db-stat-icon">✏️</div>
      <div class="db-stat-number">8</div>
      <p class="db-stat-label">待办事项</p>
    </div>
    <div class="db-stat-card">
      <div class="db-stat-icon">📊</div>
      <div class="db-stat-number">184K</div>
      <p class="db-stat-label">总字符数</p>
    </div>
  </div>

  <!-- Quick Links -->
  <p class="db-section-title">快捷入口</p>
  <div class="db-grid-4">
    <a href="concepts/" class="db-quick-link">
      <span class="icon">🧠</span>
      <span class="label">概念库</span>
      <span class="sub">36 篇笔记</span>
    </a>
    <a href="entities/" class="db-quick-link">
      <span class="icon">📦</span>
      <span class="label">项目实体</span>
      <span class="sub">7 个项目</span>
    </a>
    <a href="queries/" class="db-quick-link">
      <span class="icon">🔍</span>
      <span class="label">研究查询</span>
      <span class="sub">5 条查询</span>
    </a>
    <a href="2026-06-14.html" class="db-quick-link">
      <span class="icon">📰</span>
      <span class="label">今日新闻</span>
      <span class="sub">最新日报</span>
    </a>
  </div>

  <!-- Core Concepts + Todos -->
  <div class="db-cols">

    <div class="db-card">
      <p class="db-card-title">📌 核心概念</p>
      <ul class="db-card-list">
        <li>[[AI-Agent-核心概念对照]]</li>
        <li>[[Claude-Code-6个隐藏能力]]</li>
        <li>[[Hermes-Agent-三层路由架构设计]]</li>
        <li>[[pretext-科普]]</li>
        <li>[[deer-flow-multi-agent]]</li>
      </ul>
    </div>

    <div class="db-card">
      <p class="db-card-title">✅ 待办事项</p>
      <ul class="db-card-list">
        <li><span style="color:#f97316">○</span> 配置 Reddit API Key 后测试 `/last30days` 搜索功能 <span class="meta">[[gh-projects-verification]]</span></li>
        <li><span style="color:#f97316">○</span> 验证跨平台（Claude Code / Codex / Hermes）安装兼容性 <span class="meta">[[gh-projects-verification]]</span></li>
        <li><span style="color:#f97316">○</span> 检查数据去重和摘要质量 <span class="meta">[[gh-projects-verification]]</span></li>
        <li><span style="color:#f97316">○</span> 在 Claude Code 中加载技能，测试生成的网页设计质量 <span class="meta">[[gh-projects-verification]]</span></li>
        <li><span style="color:#f97316">○</span> 对比使用 taste-skill 前后的 UI 差异 <span class="meta">[[gh-projects-verification]]</span></li>
        <li><span style="color:#f97316">○</span> 验证与 Hermes + gstack 的兼容性 <span class="meta">[[gh-projects-verification]]</span></li>
        <li><span style="color:#f97316">○</span> Docker Compose 启动全栈（`docker compose up`） <span class="meta">[[gh-projects-verification]]</span></li>
        <li><span style="color:#f97316">○</span> 上传 PDF 文档测试内容提取 <span class="meta">[[gh-projects-verification]]</span></li>

      </ul>
    </div>

  </div>

  <!-- One-click Triggers -->
  <p class="db-section-title">⚡ 一键触发</p>
  <div class="db-triggers">
    <a href="log.md" class="db-trigger">
      <span class="icon">📝</span>
      <span><span class="t-label">写日记</span><br><span class="t-desc">打开工作日志</span></span>
    </a>
    <a href="index.md" class="db-trigger">
      <span class="icon">📋</span>
      <span><span class="t-label">全站索引</span><br><span class="t-desc">浏览所有笔记</span></span>
    </a>
    <a href="concepts/_database.md" class="db-trigger">
      <span class="icon">🗃️</span>
      <span><span class="t-label">概念数据库</span><br><span class="t-desc">36 条概念条目</span></span>
    </a>
    <a href="entities/_database.md" class="db-trigger">
      <span class="icon">📦</span>
      <span><span class="t-label">实体数据库</span><br><span class="t-desc">7 个项目档案</span></span>
    </a>
  </div>

  <!-- Recent Updates -->
  <p class="db-section-title">🕐 最近更新</p>
  <div class="db-card" style="margin-bottom: 48px;">
    <ul class="db-card-list">
        <li>[[dashboard]] <span class="meta">2026-06-15</span></li>
        <li>[[socratic-verse-zhihu-article-v2]] <span class="meta">2026-06-15</span></li>
        <li>[[log]] <span class="meta">2026-06-15</span></li>
        <li>[[socratic-verse-technical-architecture]] <span class="meta">2026-06-15</span></li>
        <li>[[socratic-verse-marketing-plan]] <span class="meta">2026-06-15</span></li>

    </ul>
  </div>

  <p class="db-section-title">每日新闻</p>
  <div class="db-news">
    <a href="news/2026-06-14.html" style="text-decoration: none;">
      <div class="db-news-card">
        <div class="db-news-left">
          <span class="icon">📰</span>
          <div>
            <div class="title">新闻日报 · 2026-06-14</div>
            <div class="desc">百度热搜 + GitHub Trending + 官方媒体</div>
          </div>
        </div>
        <span class="db-news-badge">最新</span>
      </div>
    </a>
  </div>

  <!-- Footer -->
  <div class="db-footer">
    <span>🔗 最近提交 · <span class="highlight">c565686</span> Rewrite tone: position Socratic Verse as learner/practitione</span>
    <span>📊 总字符 <span class="highlight">184,279</span> · 2026-06-15 星期一</span>
  </div>

</div>