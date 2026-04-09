# Wiki Log

Append-only operation log. Never edit or delete past entries.

Format: `## [YYYY-MM-DD] <operation> | <title or summary>`
Operations: `ingest` | `query` | `lint` | `note`

Parse last N entries: `grep "^## \[" wiki/log.md | tail -10`

---

## [2026-04-08] note | Wiki initialized
Created base directory structure, CLAUDE.md, index.md, log.md, overview.md. No sources ingested yet.

## [2026-04-09] ingest | AI 2027
处理 raw/AI 2027.md（585行，来自 ai-2027.com）。创建：sources/ai-2027.md、entities/openbrain.md、entities/deepcent.md、concepts/ai-alignment.md、concepts/intelligence-explosion.md、concepts/ai-rnd-multiplier.md、concepts/neuralese.md、concepts/ida.md、concepts/us-china-ai-race.md、concepts/model-weight-security.md。更新 index.md 和 overview.md。共触及 12 个 wiki 页面。
