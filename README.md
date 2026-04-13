# skill-molt

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-DA7857)](https://agentskills.io)
[![Version](https://img.shields.io/badge/version-0.1.0-blue.svg)](SKILL.md)

> Agent skill that creates and improves other skills from your coding sessions. Zero dependencies. Works with any agent.

Ancient arthropods grow by molting — shedding their old shell to emerge larger and stronger. Your agent skills should do the same.

## Install

```bash
npx skills add konippi/skill-molt
```

Or manually:

```bash
git clone https://github.com/konippi/skill-molt.git
ln -s /path/to/skill-molt ~/.claude/skills/skill-molt       # Claude Code
ln -s /path/to/skill-molt .kiro/skills/skill-molt           # Kiro CLI
ln -s /path/to/skill-molt .agents/skills/skill-molt         # Codex / Cursor / Gemini CLI
```

## Why

Coding agents are stateless. The agent that spent an hour debugging your auth flow yesterday has no memory of it today. Skills solve this by giving agents reusable procedural knowledge — but writing good skills is hard, and hand-written skills decay silently as tools and APIs change.

skill-molt automates the hard part: it extracts non-obvious lessons from real sessions and structures them into skills that actually help.

## What It Does

After a coding session that involved trial-and-error or non-obvious workarounds, skill-molt helps your agent:

1. **Observe** — Reflect on the session with 5 structured questions to extract non-obvious knowledge
2. **Generate** — Create a new SKILL.md from the lessons learned
3. **Improve** — Update an existing skill with new knowledge (shed the old, keep the new)
4. **Validate** — Run 6 pass/fail checks to ensure quality

All output is Markdown. No Python, no scripts, no external dependencies. Works alongside existing skills — it creates new ones for uncovered domains and improves existing ones when it finds new knowledge.

## Usage

When a session involves trial-and-error, error recovery, or non-obvious workarounds, the agent will propose creating or improving a skill from the experience. You decide whether to proceed.

You can also trigger it manually:

```text
> What did we learn from this session?
```

The agent proposes changes for your review — nothing is applied without your approval.

## Core Principle

> Only include what the agent could NOT have known before the session.

If it's discoverable from the codebase — README, config files, code comments — it doesn't belong in a skill. Skills capture tooling gotchas, non-obvious conventions, and lessons from failure.

This follows the skill library concept from [Voyager (NeurIPS 2023)](https://arxiv.org/abs/2305.16291), where agents accumulate reusable skills from experience to compound their capabilities over time. skill-molt applies this to coding agents: real session failures become tomorrow's procedural knowledge.

Unlike Voyager's game environment, coding environments lack an automatic verification loop — so skill-molt keeps a human in the loop for review, and uses natural-language procedures instead of executable code to stay agent-agnostic.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). The easiest way to contribute is adding real-world examples to `examples/`.

## License

[MIT](./LICENSE)
