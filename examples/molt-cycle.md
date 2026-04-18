# Molt Cycle Example

A complete example of creating a skill, then improving it after a second session. Commands and tools shown are illustrative — adapt to your actual stack.

## Session 1: Initial Creation

**Task**: Set up CI/CD pipeline for a Next.js project on Vercel.

**Observe Phase output**:

```markdown
### Non-Obvious Lessons
1. `vercel.json` rewrites must be defined BEFORE catch-all routes — order matters
2. Preview deployments use a different `NEXT_PUBLIC_API_URL` than production — must set per-environment
3. Build cache breaks when `next.config.js` changes — need `vercel --force` after config edits
4. The `vercel env pull` command overwrites `.env.local` without warning
```

**Generated Skill** (`vercel-deployment/SKILL.md`):

```markdown
---
name: vercel-deployment
description: >-
  Use when deploying to Vercel, configuring preview environments, or
  debugging deployment failures in Next.js projects. Do NOT use for
  local development setup or non-Vercel hosting.
---

# Vercel Deployment

## Workflow

1. Read `vercel.json` — check that rewrites are ordered before catch-all routes
2. Verify environment variables: `vercel env ls`
   - Confirm `NEXT_PUBLIC_API_URL` is set separately for Preview and Production
3. Deploy: `vercel --prod`
   - If deploy fails after config change → `vercel --force --prod`
4. Verify: check the deployment URL returns 200

## Rules

- Rewrite rules in `vercel.json` are order-dependent — specific routes before catch-all
- Never run `vercel env pull` without backing up `.env.local` first — it overwrites silently

## Gotchas

- Build cache persists across deploys. After changing `next.config.js`, use `--force` or the build uses stale config.
- Preview and Production environments have separate env vars. Setting one does not set the other.
```

## Session 2: Improvement (The Molt)

**Task**: Debug a failing preview deployment. Discovered new knowledge.

**Observe Phase output**:

```markdown
### Non-Obvious Lessons
1. Vercel's build timeout is 45 minutes — our monorepo build hits 40min, dangerously close
2. `vercel logs <url>` only shows last 1000 lines — for full logs, use `vercel logs <url> --all`
3. The "Functions" tab in Vercel dashboard shows cold start times — useful for debugging slow API routes
```

**Improved Skill** (changes marked with `+` and `-`):

```diff
  ## Workflow

  1. Read `vercel.json` — check that rewrites are ordered before catch-all routes
  2. Verify environment variables: `vercel env ls`
     - Confirm `NEXT_PUBLIC_API_URL` is set separately for Preview and Production
  3. Deploy: `vercel --prod`
     - If deploy fails after config change → `vercel --force --prod`
+ 4. Check logs: `vercel logs <deployment-url> --all`
+    - Default `vercel logs` only shows last 1000 lines — use `--all` for full output
  5. Verify: check the deployment URL returns 200

  ## Gotchas

  - Build cache persists across deploys. After changing `next.config.js`, use `--force`.
  - Preview and Production environments have separate env vars.
+ - Build timeout is 45 minutes. Monorepo builds approaching 40min need optimization or `turbo` caching.
+ - `vercel logs` without `--all` truncates to 1000 lines. Always use `--all` for debugging.
```

## What Happened

1. **Session 1**: 4 non-obvious lessons → new skill created
2. **Session 2**: 3 new lessons → 2 added to existing skill, 1 discarded (dashboard tip was too UI-specific)
3. **Session 3**: Decay review → 2 lines removed, 1 rewritten. The skill got smaller and more accurate.
4. **The molt**: Skills grow, shed, and shrink. That's the cycle.

## Session 3: Decay (The Shed)

**Trigger**: The agent followed the skill's `--force` instruction but Vercel's behavior had changed — `--force` was no longer needed after a platform update that fixed cache invalidation.

**Decay Phase evaluation** (3 tests per line):

```markdown
### Line: "After changing next.config.js, use --force or the build uses stale config"
- Model internalization: ❌ Not stale — silent cache behavior isn't common knowledge
- Upstream accuracy: ✅ STALE — Vercel fixed automatic cache invalidation in March 2026
- Inferability shift: N/A
→ Remove or rewrite

### Line: "Build timeout is 45 minutes"
- Model internalization: ✅ STALE — this is now in Vercel's official docs and models know it
- Upstream accuracy: ✅ Still true
- Inferability shift: ✅ STALE — `vercel.json` now shows `"buildTimeout": 2700` with a comment
→ Remove

### Line: "vercel env pull overwrites .env.local without warning"
- Model internalization: ❌ Not stale — still a common gotcha
- Upstream accuracy: ❌ Still true, no fix shipped
- Inferability shift: ❌ No docs or error message added
→ Keep
```

**Decayed Skill** (changes marked with `+` and `-`):

```diff
  ## Workflow

  1. Read `vercel.json` — check that rewrites are ordered before catch-all routes
  2. Verify environment variables: `vercel env ls`
     - Confirm `NEXT_PUBLIC_API_URL` is set separately for Preview and Production
  3. Deploy: `vercel --prod`
-    - If deploy fails after config change → `vercel --force --prod`
  4. Check logs: `vercel logs <deployment-url> --all`
     - Default `vercel logs` only shows last 1000 lines — use `--all` for full output
  5. Verify: check the deployment URL returns 200

  ## Gotchas

- - Build cache persists across deploys. After changing `next.config.js`, use `--force`.
  - Preview and Production environments have separate env vars.
- - Build timeout is 45 minutes. Monorepo builds approaching 40min need optimization or `turbo` caching.
  - `vercel logs` without `--all` truncates to 1000 lines. Always use `--all` for debugging.
```
