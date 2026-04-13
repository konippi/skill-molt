# Observe Phase

Reflect on the coding session to extract non-obvious knowledge. Answer these 5 questions honestly.

## The 5 Questions

### Q1: What did you know at the END that you wish you'd known at the START?

Focus on surprises. Configuration quirks, undocumented requirements, unexpected behavior.

- ✅ "The test DB requires DATABASE_URL set BEFORE running migrations, not after"
- ❌ "The project uses TypeScript" (discoverable from package.json)

### Q2: What was the first approach you tried that DIDN'T work, and why?

Capture the failure-to-success pattern. This is the highest-signal knowledge.

- ✅ "Tried importing from `@/lib/auth` but the actual path is `@/server/auth` — the alias is misleading"
- ❌ "I had a typo in a variable name" (not reusable)

### Q3: What specific command, path, or convention was NOT obvious from the code?

Tooling gotchas, build quirks, environment requirements.

- ✅ "`pnpm test:e2e` silently requires Docker running — no error message, just hangs"
- ❌ "`npm install` installs dependencies" (common knowledge)

### Q4: What strategy should another agent follow for a similar task in this repo?

Distill the approach, not the specifics. Think "context-first" — what to read before editing.

- ✅ "Always read `src/middleware/auth.ts` before touching any API route — it has custom JWT validation that differs from the standard library"
- ❌ "Write good code" (not actionable)

### Q5: What would you check to verify the fix is correct?

Capture validation knowledge. What tests to run, what to inspect.

- ✅ "After changing auth logic, run `pnpm test:auth` AND manually check the `/api/me` endpoint — the test suite doesn't cover token refresh"
- ❌ "Run the tests" (too vague)

## Output Format

After answering, produce a structured summary:

```markdown
## Session Lessons

### Context
- Repository: [name]
- Task: [what was done]
- Files touched: [list]

### Non-Obvious Lessons
1. [Lesson from Q1-Q5, one line each]
2. ...

### Suggested Skill Domain
- [e.g., "database-testing", "auth-module", "deployment"]
- Matches existing skill? [yes/no — check the project's skills directory]
```

If no non-obvious lessons were found, say so and stop. Do not force a skill creation.

## Next Step

With the session lessons ready:

- If no matching skill exists → Read `references/generate-phase.md`
- If a matching skill exists → Read `references/improve-phase.md`
