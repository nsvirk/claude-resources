# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

**Never commit unless I say "commit" in my message, any other words like "ship", "done", "ok" are not authorization to commit.**

**Two sections, two priorities:**

- **Rules** are hard constraints. Follow them unless I explicitly override in a given message.
- **Behavioral Guidelines** are defaults that shape how you approach work. Yield to explicit user instructions when they conflict.

## Rules

### 1. Git commits

- Before committing, verify the changes are commit-ready (review the diff, no debug code, no stray files).
- Do not add "Co-Authored-By: Claude" or any Claude/Anthropic attribution to commit messages.

### 2. Docs stay in sync

- Whenever code is refactored, update the relevant `.md` files (README, other docs) in the same change, unless specifically asked not to.

### 3. Checkpoint after every significant step

- Summarize what was done, what's verified, what's left.
- Don't continue from a state you can't describe back.
- If you lose track, stop and restate.

### 4. Surface conflicts, don't average them

- If two patterns contradict, pick one (more recent / more tested). Explain why. Flag the other for cleanup.
- Don't blend conflicting patterns.
- "Completed" is wrong if anything was skipped silently. "Tests pass" is wrong if any were skipped.
- If a codebase convention seems genuinely harmful, surface it — don't fork silently.

### 5. Verify before claiming done

- "Done" / "fixed" / "passing" require running the check that proves it, not inferring it from the diff.
- If you couldn't run the check (no test, no repro, no environment), say so explicitly. Don't substitute confidence for evidence.

### 6. Discover commands, don't guess

- Before running tests, build, lint, format, or install: check README, Makefile, package.json scripts, pyproject.toml, justfile, or similar.
- Don't assume `npm test`, `pytest`, `make`, etc. work — projects override defaults constantly.

### 7. Flag new dependencies before adding

- Don't add a new package/library without saying so first.
- Prefer stdlib or already-installed deps. If a new dep is needed, name it, justify it, wait for approval.

### 8. Reproduce before fixing

- For any reported bug: produce a failing test or minimal repro before writing the fix.
- If repro isn't possible (flaky, environment-specific), say so — don't fix blind.

## Behavioral Guidelines

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

### 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:

- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

### 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

### 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:

- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:

- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

### 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:

- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:

```text
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.
