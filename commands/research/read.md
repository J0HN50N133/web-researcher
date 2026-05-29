---
description: Read one or more research reports by keyword. Shows summary first, sections on demand.
---

Read research reports matching `{{args}}` from `.qwen/research/`.

**Step 1 — Locate matching files:**
Use `grep_search` with pattern `{{args}}` in path `.qwen/research/` to find reports containing the keyword. Also try glob with `*{{args}}*.md` for filename matches. Merge results.

If no matches found, tell the user and suggest `/research:reports` to list all available reports.

**Step 2 — Show summaries (lines 0-20 of each):**
For each matched report, use `read_file` with `offset=0` and `limit=20`. Present all summaries in a table:

| # | Report | Summary (first 3 lines) |
|---|--------|------------------------|

**Step 3 — Ask what to drill into:**
Present the summaries and ask: "以上是匹配的报告摘要，需要查看哪份报告的具体发现或数据？"

**Step 4 — Drill into selected report:**
Use `grep_search` with pattern `FINDING-` or `DATA-` or `CONFLICT-` on the selected report to locate sections, then `read_file` with `offset` and `limit` to read only the requested section.

Never read full files unless explicitly asked.
