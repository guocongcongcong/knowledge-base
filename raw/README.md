# Raw Sources

> **不可变层** — LLM 只读不写。所有原始资料存放在此。

## 子目录

| 目录 | 用途 |
|------|------|
| `articles/` | 网页文章、博客、公众号 |
| `papers/` | 学术论文、PDF |
| `transcripts/` | 视频字幕、会议记录、访谈 |
| `assets/` | 图片、图表等附件 |

## 文件规范

每个原始文件必须含 frontmatter：

```yaml
---
source_url: https://原始链接
ingested: YYYY-MM-DD
sha256: <hex digest of body>
---
```

`sha256` 用于重新消化同一 URL 时检测内容是否变化（漂移检测）。
