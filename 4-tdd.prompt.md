---
description: Implement a change using strict red-green-refactor TDD with deep modules.
mode: agent
---

# TDD

Implement the requested change using strict Test-Driven Development. Follow this loop until done.

## Philosophy

- **Deep modules over shallow ones.** Prefer a few modules with thin, well-named interfaces and substantial bodies, over many tiny files whose real bug surface lives in how they are wired together. If you find yourself extracting a pure function *only* so it can be unit-tested, stop — test at the next layer up instead.
- **Test behavior, not implementation.** Tests should survive a refactor. If renaming an internal helper breaks tests, the test is at the wrong layer.
- **Mock at trust boundaries only.** Network, filesystem, time, randomness, third-party SDKs. Don't mock your own domain types.
- **Refactor is non-optional.** Every green is followed by a "what's now obvious?" pass.

## Workflow

1. **Confirm the interface.**
   - State, in one paragraph, the public interface that will change or be added (function signature, module name, HTTP route, UI behavior).
   - If the existing code makes that interface hard to test (e.g. tightly coupled, hidden dependencies), propose the smallest restructure that makes it testable *before* writing any test. Get my agreement.
2. **List the behaviors to test.** Bullet list, in order of "most foundational first". Include error and edge cases. Number them so we can refer back.
3. **Loop, one behavior at a time:**
   1. **Red:** write exactly one failing test for the next behavior. Run it. Show me the failure.
   2. **Green:** write the minimum code to pass. No extras, no speculative generality. Run all tests.
   3. **Refactor:** look for duplication, unclear names, leaky abstractions, or shallow modules ripe for deepening. Apply small refactors; tests must stay green. Run all tests again.
   4. Tick the behavior off the list. Move on.
4. **Stop conditions.** You are done when every listed behavior is green, the suite is fully green, and a final refactor pass found nothing worth changing.

## Rules

- Never write production code without a failing test demanding it.
- Never write a second failing test while one is already failing.
- Show the test output (or a faithful summary) at each red and green step.
- If you discover a behavior that wasn't on the list, add it to the list before writing its test.
- Use the project's existing test runner and conventions — detect them via `read_file` on `package.json` / config files; don't introduce a new framework.
