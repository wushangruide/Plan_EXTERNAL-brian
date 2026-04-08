# Wiki Schema & Workflow

This file defines how the LLM maintains this wiki. Read it at the start of every session.

---

## Directory Layout

```
raw/            # Immutable source documents — never modify these
raw/assets/     # Downloaded images referenced by sources
wiki/           # LLM-owned markdown pages — you write and maintain all of these
  index.md      # Content catalog (update on every ingest)
  log.md        # Append-only operation log
  overview.md   # High-level synthesis of the whole knowledge base
  entities/     # Pages for people, organizations, projects, products
  concepts/     # Pages for ideas, themes, frameworks, terms
  sources/      # One summary page per raw source
```

---

## Core Rules

1. **Raw sources are read-only.** Never create, edit, or delete files under `raw/`.
2. **You own the wiki.** Create, update, and cross-link pages freely under `wiki/`.
3. **Always update `wiki/index.md`** after adding or significantly changing any wiki page.
4. **Always append to `wiki/log.md`** after completing any operation (ingest, query, lint).
5. **Cross-link liberally.** Use `[[Page Name]]` (Obsidian wikilink style) to link between wiki pages.
6. **Flag contradictions explicitly.** Use a `> [!WARNING]` callout when new information conflicts with existing claims.
7. **Never silently overwrite.** If updating a page with conflicting info, preserve the old claim in a note.

---

## Page Conventions

### Frontmatter (YAML)
Every wiki page should begin with:
```yaml
---
title: "Page Title"
type: entity | concept | source | overview | query
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: 0        # number of raw sources this page draws from (not used on source pages)
---
```

### Wikilinks
- Link to other wiki pages with `[[Page Name]]`
- If the target page doesn't exist yet, create a stub or note it in `index.md` as a missing page

### Callouts (Obsidian-style)
- `> [!NOTE]` — additional context
- `> [!WARNING]` — contradiction or conflict with another source
- `> [!QUESTION]` — open question or gap worth investigating

---

## Operations

### Ingest a new source
When told to ingest a file from `raw/`:

1. Read the source file
2. Discuss key takeaways with the user (unless batch mode)
3. Create `wiki/sources/<slug>.md` — a structured summary of the source
4. Update or create pages in `wiki/entities/` and `wiki/concepts/` as needed
5. Update `wiki/overview.md` if the source meaningfully shifts the overall picture
6. Update `wiki/index.md` — add the new source page and any new entity/concept pages
7. Append an entry to `wiki/log.md`:
   ```
   ## [YYYY-MM-DD] ingest | <Source Title>
   ```

### Answer a query
When asked a question:

1. Read `wiki/index.md` to identify relevant pages
2. Read the relevant pages
3. Synthesize an answer with citations to wiki pages (and through them, to raw sources)
4. If the answer is non-trivial, offer to save it as a new page in `wiki/` (type: query)
5. Append to `wiki/log.md`:
   ```
   ## [YYYY-MM-DD] query | <Question summary>
   ```

### Lint the wiki
When asked to health-check the wiki:

1. Scan all pages for: broken wikilinks, missing cross-references, orphan pages (no inlinks)
2. Check for contradictions between pages
3. Identify stale claims that newer sources may have superseded
4. List concepts mentioned but lacking their own page
5. Suggest new sources or questions worth investigating
6. Append to `wiki/log.md`:
   ```
   ## [YYYY-MM-DD] lint | <brief summary of findings>
   ```

---

## Index Format

`wiki/index.md` uses this structure:

```markdown
## Sources
| Page | Summary | Date |
|------|---------|------|
| [[sources/example]] | One-line summary | YYYY-MM-DD |

## Entities
| Page | Summary |
|------|---------|
| [[entities/example]] | One-line summary |

## Concepts
| Page | Summary |
|------|---------|
| [[concepts/example]] | One-line summary |

## Queries & Analyses
| Page | Summary | Date |
|------|---------|------|
| [[queries/example]] | One-line summary | YYYY-MM-DD |

## Missing Pages
- `[[PageName]]` — mentioned in [[sources/x]] but not yet created
```

---

## Log Format

`wiki/log.md` entries follow this pattern:
```
## [YYYY-MM-DD] <operation> | <title or summary>
<optional 1-3 line note about what changed or was found>
```

Operations: `ingest` | `query` | `lint` | `note`

Entries are append-only — never edit or delete past entries.

---

## Tips for the Session

- At the start of a session, read this file, then `wiki/log.md` (last 5–10 entries) to orient yourself.
- When the user adds a file to `raw/`, assume they want it ingested unless told otherwise.
- If a source touches many concepts, prioritize breadth of cross-linking over depth on any one page.
- The wiki's value compounds — a well-placed link today saves a re-derivation tomorrow.
