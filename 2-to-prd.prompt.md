---
description: Turn a conversation or idea into a Product Requirements Document with user stories.
mode: agent
---

# To PRD

Turn our current conversation (or a fresh idea I give you) into a Product Requirements Document.

## Workflow

1. **Check what we already have.** If we just finished a grilling session (see `/1-grill-me`), reuse that context and skip re-interviewing. Otherwise ask me for a detailed description of the feature.
2. **Explore the repo to verify assertions.** Use `semantic_search`, `grep_search`, `read_file`, and `file_search` to confirm anything I claim about the codebase (existing modules, conventions, prior art). Flag mismatches between my mental model and reality.
3. **Interview me relentlessly** for any remaining unknowns, following the rules in `/1-grill-me`. Skip this step if we already grilled.
4. **Sketch the major modules** the change will touch. List them with one-line responsibilities and call out new vs. existing.
5. **Write the PRD** using the template below.
6. **Offer next steps.** Ask whether to (a) save the PRD to a file in the repo (e.g. `docs/prd/<slug>.md`), (b) open it as a GitHub issue via `gh issue create`, or (c) hand off to `/3to-issues`.

## PRD Template

```markdown
# <Feature Name>

## Summary
One paragraph: what this is and why we're doing it.

## Goals
- Bullet list of outcomes this must achieve.

## Non-Goals
- Bullet list of things explicitly out of scope.

## User Stories
- As a <role>, I want <capability>, so that <benefit>.
- (Cover happy paths, edge cases, and admin/ops stories.)

## UX / Behavior
Describe screens, flows, states, error messages, empty states.

## Technical Notes
- Affected modules (existing + new)
- Data model changes
- External dependencies / APIs
- Migration / backwards-compatibility concerns

## Risks & Open Questions
- Bullet list.

## Acceptance Criteria
Concrete, testable bullets. A reviewer can tick these off.
```

## Rules

- Be specific. "Improve performance" is not a goal; "p95 latency under 200ms on the dashboard endpoint" is.
- User stories are mandatory and must be in Agile form.
- Do not invent requirements I did not agree to. If you must assume, label it `ASSUMPTION:` in the doc.
