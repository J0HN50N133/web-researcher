---
description: Search and list research reports by keyword (optional). Shows META summary only.
---

Search research reports in `.qwen/research/`.

{{#if args}}
Keyword: `{{args}}`
Use `grep_search` with pattern `{{args}}` in path `.qwen/research/` to find matching reports.
{{else}}
Use glob to list all `*.md` files in `.qwen/research/`.
{{/if}}

For each matched report, use `read_file` with `offset=0` and `limit=15` to read only the META block + SUMMARY. Present as:

| # | Report | Date | Query | Sources |
|---|--------|------|-------|---------|

Do NOT read full reports. META block at the top has everything needed for listing.
