# Wiki Log

Append-only operation log. Never edit or delete past entries.

Format: `## [YYYY-MM-DD] <operation> | <title or summary>`
Operations: `ingest` | `query` | `lint` | `note`

Parse last N entries: `grep "^## \[" wiki/log.md | tail -10`

---

## [2026-04-08] note | Wiki initialized
Created base directory structure, CLAUDE.md, index.md, log.md, overview.md. No sources ingested yet.
