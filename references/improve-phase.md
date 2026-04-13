# Improve Phase

Update an existing skill with new knowledge from the current session. This is the "molt" — shedding outdated content and growing new.

## Prerequisites

- Session lessons from Observe Phase
- An existing skill identified as matching the current domain

## Procedure

### Step 1: Read the existing skill

Read the full SKILL.md of the skill to improve. Note:

- Which lines are still accurate
- Which lines reference outdated paths, commands, or patterns
- What's missing based on the new session lessons

### Step 2: Identify new knowledge

Compare session lessons against the existing skill:

- **New**: Lesson not covered by any existing line → add it
- **Updated**: Lesson contradicts or refines an existing line → replace it
- **Stale**: Existing line references something that no longer exists or is now inferable → remove it
- **Unchanged**: Existing line is still accurate and non-inferable → keep it

### Step 3: Apply changes

For each change:

1. **Adding**: Insert at the most relevant section. Keep the skill's existing structure.
2. **Replacing**: Swap the old line for the new one. Preserve the surrounding context.
3. **Removing**: Delete the line. If this leaves an empty section, remove the section header too.

### Step 4: Re-check constraints

After all changes:

- Body still ≤ 50 lines? If not, identify what to cut or move to references/
- Every line still non-inferable? Re-apply the "could I find this in the codebase?" filter
- Description still works as a trigger? Update keywords if the skill's scope changed
- No regression? Confirm no previously useful Gotchas or Rules were removed without replacement

## Next Step

Do not present the skill to the user yet. Read `references/validate-phase.md` now and run all 6 checks.
