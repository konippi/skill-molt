# Security Policy

skill-molt is Markdown only — no executable code, no network calls, no external dependencies. The risk surface is the **skills it generates**, not skill-molt itself.

## Reporting Vulnerabilities

If you discover a security issue, please **do not open a public issue**.

Use [GitHub's private vulnerability reporting](https://github.com/konippi/skill-molt/security/advisories/new).

## Generated Skill Review

skill-molt requires human approval before saving any skill. Always review generated skills for:

- Hardcoded secrets (API keys, tokens, passwords, connection strings)
- Destructive commands (`rm -rf`, `curl | bash`, `sudo` operations)
- Paths that reference files outside the project directory

## Known Limitations

skill-molt processes session content as input for skill generation. If used in a repository containing adversarial content (e.g., prompt injection in README or code comments), the generated skill may reflect that content. The human-review requirement is the primary mitigation.
