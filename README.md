# skill-molt

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-DA7857)](https://agentskills.io)

Ancient arthropods grow by molting — shedding their old shell to emerge larger and stronger. Your agent skills should do the same.

Human-AI co-evolution for agent skills. Extract what matters from real sessions, validate quality, and shed what's stale. Works with any agent.

## Install

```bash
npx skills add konippi/skill-molt
```

Or manually:

```bash
git clone https://github.com/konippi/skill-molt.git
ln -s /path/to/skill-molt ~/.claude/skills/skill-molt       # Claude Code
ln -s /path/to/skill-molt ~/.kiro/skills/skill-molt         # Kiro CLI
ln -s /path/to/skill-molt ~/.openclaw/skills/skill-molt     # OpenClaw
ln -s /path/to/skill-molt ~/.agents/skills/skill-molt       # Codex / Cursor / Gemini CLI
```

For project-scoped installation, use `.claude/skills/`, `.kiro/skills/`, or `.agents/skills/` in your project root instead.

## Why

AI agents are stateless. The agent that spent an hour solving a complex workflow yesterday has no memory of it today. Skills solve this by giving agents reusable procedural knowledge — but writing good skills is hard, and they decay silently as models internalize knowledge, tools change, and upstream APIs break.

Fully automated skill generation doesn't work either — [SkillsBench (2026)](https://arxiv.org/abs/2602.12670) found that human-curated skills improve agent performance by 16 percentage points, while self-generated skills provide no benefit. The gap isn't automation — it's quality.

skill-molt bridges this: it extracts non-obvious lessons from real sessions through human-AI collaboration, validates quality, structures them into skills that actually help, and retires them when they go stale.

## Core Principle

> Only include what the agent could NOT have known before the session.

If it's discoverable from the codebase — README, config files, code comments — it doesn't belong in a skill. Skills capture tooling gotchas, non-obvious conventions, and lessons from failure.

This follows the skill library concept from [Voyager (NeurIPS 2023)](https://arxiv.org/abs/2305.16291), where agents accumulate reusable skills from experience to compound their capabilities over time. [Agent Workflow Memory (ICML 2025)](https://arxiv.org/abs/2409.07429) showed that agents can induce reusable workflows from past experience, and [ChemAgent (ICLR 2025)](https://arxiv.org/abs/2501.06590) demonstrated that a self-updating skill library improves domain performance by up to 46%. skill-molt applies these ideas to any agent: real session failures become tomorrow's procedural knowledge.

Unlike fully automated approaches, skill-molt keeps a human in the loop for review and uses natural-language procedures instead of executable code to stay agent-agnostic. The improve cycle is inspired by [ACE (ICLR 2026)](https://arxiv.org/abs/2510.04618), which shows that treating context as an evolving playbook outperforms static approaches.

## What It Does

After a session that involved trial-and-error or non-obvious workarounds, skill-molt helps your agent:

1. **Observe** — Reflect on the session with 5 structured questions to extract non-obvious knowledge
2. **Generate** — Create a new SKILL.md from the lessons learned
3. **Improve** — Update an existing skill with new knowledge (shed the old, keep the new)
4. **Validate** — Run 6 pass/fail checks to ensure quality
5. **Decay** — Evaluate each line for staleness and retire what no longer earns its token cost

All output is Markdown — no compiled code, no external dependencies. Works alongside existing skills: it creates new ones for uncovered domains, improves existing ones when it finds new knowledge, and shrinks or retires them when they go stale.

## Usage

After installing, skill-molt works automatically. When a session involves trial-and-error, error recovery, or non-obvious workarounds, the agent will propose creating or improving a skill from the experience.

You can also trigger it directly:

```text
> What did we learn from this session?
> Improve the deployment skill with what we learned today
> Shrink the CI skill — half of it feels outdated
```

The agent proposes changes for your review — nothing is saved without your approval. See [`examples/molt-cycle.md`](examples/molt-cycle.md) for a create → improve walkthrough.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](./LICENSE)
