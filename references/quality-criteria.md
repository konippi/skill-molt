# Quality Criteria

Criteria for evaluating skill quality. Reference this when unsure whether a skill meets the bar.

## The Non-Inferable Principle

If the agent could discover it by reading the codebase, do not include it. Inferable information inflates token cost without improving outcomes.

**Test**: For each line, ask: "If I deleted this line and gave the agent only the codebase, would it figure this out?" If yes, delete the line.

## Description Quality

The description determines whether the skill is selected. Poor descriptions cause the agent to skip the skill or pick the wrong one.

**Rules**:

- Description tells WHEN, not HOW
- Include specific keywords users type
- Include negative triggers ("Do NOT use for...")
- Under 1024 characters, 2-4 sentences

## Actionable Content Ratio

Every line should be a command, a condition, a rule, or a verification step.

**Test**: For each line, ask: "What does the agent DO with this information?" If the answer is "nothing" or "just know it", rewrite as an action or delete.

## Failure Patterns Are Valuable

The "Gotchas" section of a skill should capture failure patterns:

- What the naive approach is and why it fails
- What error message (or lack thereof) you'll see
- What the correct approach is

## Context-First Strategy

Skills should instruct the agent to gather context before editing.

**Test**: Does the skill's workflow start with a "read" or "check" step before any "edit" or "create" step?
