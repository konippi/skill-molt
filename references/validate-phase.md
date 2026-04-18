# Validate Phase

Run 6 pass/fail checks on a generated or updated skill. All must pass before presenting to the user.

## Checklist

### Check 1: Path Check

Verify every file path and resource reference mentioned in the skill exists or is valid.

- Read the skill body and extract all file paths, directory references, URLs, and resource identifiers
- For each file path, confirm it exists in the project
- For each URL or API endpoint, confirm it is well-formed and uses the expected protocol
- Reject any path that traverses outside the project directory (e.g., `../../`, `/etc/`, absolute paths outside the project root)
- **Pass**: All referenced paths exist and are within the project; all URLs are well-formed
- **Fail**: List the missing or out-of-scope paths. Suggest corrections.

### Check 2: Command Check

Verify every command and tool reference mentioned in the skill is executable or valid.

- Extract all shell commands and CLI tool references from the skill body
- For each command, confirm the binary exists (e.g., `which pnpm`, `which aws`)
- For non-CLI tools (e.g., API calls, dashboard steps), confirm the tool or service name is correct
- Flag dangerous patterns: `rm -rf` with broad paths, piped installs (`curl | bash`), `sudo`, system-level config changes (`/etc/`). If flagged, add a warning comment in the skill.
- **Pass**: All commands and tools are available and no unacknowledged dangerous patterns
- **Fail**: List unavailable commands or unflagged dangerous patterns. Suggest alternatives.

### Check 3: Relevance Check

Verify each statement contains non-inferable information. See `references/quality-criteria.md` for criteria.

- For each instruction or rule in the skill body, ask: "Could I figure this out by reading the codebase alone?"
- **Pass**: Every statement contains knowledge NOT discoverable from code, config, or README
- **Fail**: List the inferable statements. Remove them or replace with non-obvious knowledge.

### Check 4: Length Check

Verify the skill is concise.

- Body (excluding frontmatter): ≤ 50 lines
- Description: non-empty, ≤ 1024 characters
- Description does NOT summarize the workflow (trigger only)
- **Pass**: Within limits and description is a trigger
- **Fail**: Identify what to cut or move to references/

### Check 5: Description Trigger Check

Verify the description works as a trigger, not a summary.

- Read the description field
- Does it tell the agent WHEN to use the skill? (Good)
- Does it tell the agent HOW the skill works? (Bad — agent will skip the body)
- Does it include specific keywords users would type? (Good)
- Does it include negative triggers to prevent over-activation? (Good)
- **Pass**: Description is a trigger with keywords and boundaries
- **Fail**: Rewrite the description following the trigger pattern.

### Check 6: Secret Check

Verify the skill does not contain secrets or credentials.

- Scan the skill body for: API keys, passwords, tokens, connection strings, private keys
- Common patterns: `sk-`, `AKIA`, `ghp_`, `Bearer`, `-----BEGIN`, base64-encoded blocks
- Check for hardcoded IPs, internal hostnames, or non-public URLs
- **Pass**: No secrets or credentials detected
- **Fail**: List detected patterns. Replace with placeholders (e.g., `<your-api-key>`).

## After Validation

- **All pass**: Present the skill to the user with a summary of what was created or changed and why. Do NOT save without user approval.
- **Any fail**: Fix the failing checks and re-run validation. Repeat until all pass.
