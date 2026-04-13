# Generate Phase

Create a new SKILL.md from the session lessons produced by the Observe Phase.

## Prerequisites

- Session lessons from Observe Phase (the structured summary)
- Confirmed that no existing skill covers 80%+ of this domain

## Procedure

### Step 0: Locate the skills directory

Find where to save the new skill:

1. Look for an existing skills directory in the project root (e.g., `.claude/skills/`, `.agents/skills/`, `.kiro/skills/`)
2. If one is found, use it
3. If multiple are found or none exist, ask the user where to save
4. Never place a SKILL.md directly in the project root

### Step 1: Determine the skill name

- Use kebab-case, lowercase, max 64 characters
- Name should describe the DOMAIN, not the action (e.g., `database-testing` not `fix-db-tests`)
- Check: does a directory with this name already exist in the project's skills directory?
  - If yes → stop, read `references/improve-phase.md` instead

### Step 2: Write the frontmatter

Use the template from `assets/skill-template.md`. Fill in:

- `name`: the kebab-case name from Step 1
- `description`: 2-4 sentences. Write as a TRIGGER, not a summary.
  - Start with "Use when..." to tell the agent WHEN to activate
  - Include specific keywords users would type
  - Do NOT describe the workflow — the agent must load the body to learn that
  - Add "Do NOT use for..." to prevent over-triggering

### Step 3: Write the body

Rules for every line:

1. **Would removing this line cause the agent to make a mistake?** If no, cut it.
2. **Could the agent discover this from the codebase?** If yes, cut it.
3. **Is this a procedure or an explanation?** If explanation, rewrite as a procedure.

Structure:

```markdown
# [Skill Name]

## Workflow

1. [First action — specific command or file to read]
2. [Second action]
   - If [condition] → [alternative action]
3. [Verification step — how to confirm it worked]

## Rules

- [Non-obvious constraint from session lessons]
- [Another constraint]

## Gotchas

- [Specific pitfall that caused failure in the session]
```

Before writing, read `examples/good-skill.md` as a reference and `examples/bad-skill.md` to see what to avoid.

### Step 4: Size check

- Body: under 50 lines (excluding frontmatter)
- If over 50 lines, split reference material into a `references/` subdirectory
- Each line must be actionable — no filler

### Step 5: Decide — add, merge, or discard

- **Add**: The lessons are new and no existing skill overlaps → create the file
- **Merge**: An existing skill covers a related domain → read `references/improve-phase.md`
- **Discard**: The lessons are too specific to one task, or already inferable → do not create

## Next Step

Do not present the skill to the user yet. Read `references/validate-phase.md` now and run all 6 checks.
