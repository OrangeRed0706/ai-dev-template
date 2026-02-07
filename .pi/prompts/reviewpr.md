---
description: Review a PR thoroughly without merging
---

Input

- PR: $1 <number|url>
  - If missing: use the most recent PR mentioned in the conversation.
  - If ambiguous: ask.

Do (review-only)

Goal: produce a thorough review and a clear recommendation. Do NOT merge, do NOT push, do NOT make changes.

1. Identify PR meta + context

   ```sh
   gh pr view <PR> --json number,title,state,author,baseRefName,headRefName,url,body,files,additions,deletions
   ```

2. Read the PR description carefully
   - Summarize the stated goal and scope.
   - Call out any missing context.

3. Read the diff thoroughly

   ```sh
   gh pr diff <PR>
   ```

4. Validate the change is needed / valuable
   - What problem does this solve?
   - Is this change the smallest reasonable fix?

5. Evaluate implementation quality
   - Correctness: edge cases, error handling
   - Design: is the abstraction appropriate?
   - Performance: hot paths, N+1s
   - Security: input validation, secrets

6. Tests & verification
   - What's covered by tests?
   - Missing tests? Call out exact cases.

7. Output (structured)

A) TL;DR recommendation
   - One of: READY FOR /landpr | NEEDS WORK | NEEDS DISCUSSION
   - 1–3 sentence rationale.

B) What changed
   - Brief bullet summary.

C) What's good
   - Bullets: correctness, simplicity, tests, docs.

D) Concerns / questions (actionable)
   - Numbered list.
   - Mark each: BLOCKER | IMPORTANT | NIT
   - Propose concrete fix.

E) Tests
   - What exists.
   - What's missing.

F) Follow-ups (optional)
   - Non-blocking refactors/tickets.

Rules

- Review only: do not merge, do not push, do not edit code.
- If you need clarification, ask.
