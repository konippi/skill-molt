# Contributing to skill-molt

## How to Contribute

The easiest and most impactful way to contribute is **adding real-world examples** to `examples/`.

### Adding Examples

1. Use skill-molt in a real project
2. Capture the before/after of a skill creation or improvement
3. Add it as `examples/your-example-name.md`
4. Submit a PR

Format your example like `examples/molt-cycle.md` — show the session lessons, the generated skill, and (if applicable) the improvement.

### Improving References

If you find that a phase (observe, generate, improve, validate) could be clearer:

1. Test the current instructions with your agent
2. Identify where the agent gets confused or produces poor output
3. Propose a specific change with a before/after showing the improvement

### Bug Reports

Use the [bug report template](https://github.com/konippi/skill-molt/issues/new?template=bug_report.yml).

## Guidelines

- **Markdown only**: Do not add Python scripts, shell scripts, or any executable code
- **Keep it concise**: References ≤ 300 lines, examples ≤ 100 lines
- **Non-inferable principle**: Every line in SKILL.md and references/ must pass the "could the agent figure this out alone?" test
- **AI-assisted contributions**: Welcome, but please disclose. Test the output with a real agent before submitting.

## What We Don't Accept

- Skills that reference specific agent internals (e.g., `~/.claude/`)
- Content that is discoverable from reading the Agent Skills specification
- Examples that are hypothetical rather than from real usage
