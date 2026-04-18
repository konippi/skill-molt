# Decay Phase

Determine whether each line in an existing skill is still alive — non-inferable, accurate, and worth its token cost. Skills that only grow eventually harm the agent through context pollution.

## Why Skills Decay

Three forces shrink a skill over time:

1. **Model internalization**: Knowledge that was non-obvious when the skill was written may now be part of the model's training data or reasoning capability. Including it wastes tokens and can degrade performance.
2. **Upstream change**: Commands, paths, APIs, or conventions referenced in the skill may have changed or been removed. Stale instructions cause the agent to fail silently.
3. **Inferability shift**: Project changes (new README sections, better error messages, updated config comments) can make previously non-obvious knowledge discoverable from the codebase.

## When to Apply

Use these criteria during the Improve Phase (Step 2: Identify new knowledge) to evaluate existing lines marked as potentially **Stale**. Also apply when a skill feels bloated or when the agent follows a skill instruction that leads to a wrong outcome.

## Staleness Criteria

For each line in the skill body, run these three tests:

### Test 1: Model Internalization

> "If I gave the agent this task with NO skill loaded, would it already know this?"

Try mentally removing the line. If the agent would still do the right thing because the knowledge is common or well-documented upstream, the line is stale.

- ✅ Stale: "Use `aws s3api head-object` to verify uploads" — widely documented, models know this
- ❌ Not stale: "`aws s3 cp` exits 0 even on incomplete large file uploads" — silent failure, not in docs

### Test 2: Upstream Accuracy

> "Is this still true?"

- Does the command still exist? Does the flag still work?
- Does the path still resolve? Has the file moved or been renamed?
- Has the API behavior changed in a recent version?

If the answer is no, the line is stale. Either remove it or replace it with the current truth.

### Test 3: Inferability Shift

> "Could the agent now discover this by reading the codebase?"

Check whether the project has added documentation, error messages, or config comments that make this knowledge discoverable. What was non-inferable at skill creation time may be inferable now.

- ✅ Stale: Skill says "use port 5433 for test DB" but `docker-compose.test.yml` now has a comment `# Test DB port: 5433`
- ❌ Not stale: Port is still only in the compose file with no comment, and the dev DB uses 5432 — easy to confuse

## After Evaluation

- **Lines that fail any test**: Mark as Stale in the Improve Phase. Remove them.
- **Lines that pass all three tests**: Keep. They are still earning their token cost.
- **All lines stale**: The skill has completed its lifecycle. Propose retiring the entire skill.
- **Skill shrinks below useful threshold**: If only 1-2 lines remain, consider merging into a related skill instead.
