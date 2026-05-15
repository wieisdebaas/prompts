---
description: Break a PRD into a Kanban board of independently grabbable, vertical-slice issues.
mode: agent
---

# To Issues

Turn a PRD into a set of independently grabbable issues, each a thin vertical slice.

## Workflow

1. **Locate the PRD.**
   - If a PRD path or issue URL was given, fetch/read it.
   - Otherwise search the repo (`docs/prd/**`, `docs/**/prd*.md`, recent `.md` files) and ask me to confirm the right one.
2. **Explore the codebase.** Use `semantic_search`, `grep_search`, and `read_file` to understand where each part of the PRD will land. Note conventions (test framework, folder layout, naming).
3. **Draft vertical slices.** Each issue must:
   - Cut through every relevant layer (UI → API → data → tests) end-to-end, even if trivially.
   - Be a *tracer bullet*: it flushes out unknown unknowns early.
   - Be independently grabbable when possible — explicitly mark `Blocked by: #N` only when truly necessary.
   - Be sized so one engineer (or agent) can finish it in a single focused session.
4. **For each issue, produce:**

   ```markdown
   ### <Short title>

   **Goal:** one sentence.

   **User-visible behavior after merge:** what changes that a user/QA could observe.

   **Touches:** list of files/modules.

   **Acceptance criteria:**
   - [ ] testable bullet
   - [ ] testable bullet

   **Blocked by:** none | #1, #2

   **Notes / gotchas:** anything the implementer should not have to rediscover.
   ```

5. **Show the board.** After listing all issues, render a small dependency table:

   | # | Title | Blocked by | Parallelizable? |
   |---|-------|------------|-----------------|

6. **Offer to create them.** Ask whether to:
   - Save as `docs/issues/<n>-<slug>.md` files, or
   - Open as GitHub issues with `gh issue create` (one per slice).

## Anti-patterns to refuse

- Horizontal slices ("add DB schema", "add API layer", "add UI"). Reject and re-slice vertically.
- Mega-issues that bundle unrelated work.
- Issues without acceptance criteria.
