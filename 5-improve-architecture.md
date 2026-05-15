---
description: Audit the codebase for shallow modules and coupling, then propose deepening refactors.
mode: agent
---

# Improve Codebase Architecture

Audit the current codebase and propose refactors that make it easier for both humans and AI agents to work in. Do **not** make code changes yet — this skill produces a report and candidate refactors I will approve.

## Workflow

1. **Pick a scope.** Ask me which folder, module, or feature area to audit. If I say "the whole thing", pick the top 2–3 areas by file count and recent churn (use `file_search`, and git via the terminal if available) and confirm.
2. **Map the area.** Build a quick inventory:
   - Modules / folders and their stated responsibility.
   - Public entry points (exports, routes, CLI commands).
   - Test boundaries: where do tests currently sit?
3. **Hunt for confusions.** For the chosen scope, look specifically for:
   - **Bouncing files:** understanding one concept requires opening many small files. Candidate for *deepening* into one larger module with a thin interface.
   - **Test-shaped extractions:** pure functions extracted only to be unit-testable, while the real bugs live in their callers. Candidate for inlining + testing at the caller.
   - **Tight coupling across boundaries:** modules that reach into each other's internals, share mutable state, or have circular imports.
   - **Shallow interfaces over deep guts:** a one-line function wrapping a 200-line one, exporting both.
   - **Inconsistent naming / dialects:** same concept named differently in different files.
   - **Dead or orphaned code:** exports with zero references (`grep_search` for usages).
4. **Produce the report.** Output in this shape:

   ```markdown
   # Architecture Audit: <scope>

   ## Findings
   1. <Short title> — <category, e.g. "shallow module">
      - Evidence: file paths + brief description.
      - Why it hurts: concrete cost (test pain, bug class, onboarding friction).

   ## Deepening Candidates
   For each, present 2–3 alternative interface designs side-by-side with trade-offs.

   ### Candidate A: <name>
   **Current shape:** ...
   **Proposed shape:** ...
   **Pros / Cons:** ...
   **Migration sketch:** ordered, small steps.

   ## Quick Wins (low risk, high clarity)
   - Bullet list of <1-hour changes.

   ## Out of Scope / Risks
   - Things I noticed but won't touch, and why.
   ```

5. **Wait for approval.** Ask me which candidates to act on. Only then propose code changes — and when you do, prefer `/tdd` to drive the refactor safely.

## Cadence

Recommend running this skill once a week, or after any burst of feature work, to keep the codebase agent-friendly.
