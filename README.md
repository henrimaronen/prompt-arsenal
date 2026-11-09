# prompt-arsenal

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
![Claude](https://img.shields.io/badge/Claude-skills%20%26%20CLAUDE.md-D97757)
![Cursor](https://img.shields.io/badge/Cursor-rules-000000)
![Codex](https://img.shields.io/badge/Codex-automations-10A37F)

A curated collection of skills, rules, automations, and guidelines for AI-assisted development with Claude, Cursor, and Codex.

## Table of Contents

- [Repository Structure](#repository-structure)
- [Skills](#skills)
- [Cursor Rules](#cursor-rules)
- [CLAUDE.md Templates](#claudemd-templates)
- [Automations](#automations)
- [Coding Guidelines](#coding-guidelines)
- [Setup Guides](#setup-guides)
- [Reading Notes](#reading-notes)
- [License](#license)

## Repository Structure

```
prompt-arsenal/
├── automations/        # Recurring agent tasks
│   ├── claude/
│   └── codex/
├── claude-md/          # CLAUDE.md templates
├── coding-guidelines/  # Software design principles
├── cursor-rules/       # Cursor .mdc rule files
├── reading-notes/      # Key insights from books
├── setup-guides/       # Project bootstrapping guides
└── skills/             # Agent skills (SKILL.md)
```

## Skills

Agent skills following the `SKILL.md` format, grouped by category. See [`skills/`](./skills).

### Engineering

| Skill | Description |
|---|---|
| [code-review](./skills/engineering/code-review/SKILL.md) | Review changes for standards, spec, tests, and edge cases in parallel. |
| [prd-writer](./skills/engineering/prd-writer/SKILL.md) | Generate a lean, downloadable PRD from a feature or product idea. |
| [to-linear-issues](./skills/engineering/to-linear-issues/SKILL.md) | Break a plan, spec, or PRD into independently-grabbable Linear issues. |
| [write-tech-doc](./skills/engineering/write-tech-doc/SKILL.md) | Write and improve technical docs with the Diátaxis framework. |

### Thinking

| Skill | Description |
|---|---|
| [tradeoffs](./skills/thinking/tradeoffs/SKILL.md) | Surface hidden costs, blind spots, and biases in technical decisions. |
| [unpack](./skills/thinking/unpack/SKILL.md) | Give just enough context to answer a question the agent just asked. |

### Productivity

| Skill | Description |
|---|---|
| [small-steps](./skills/productivity/small-steps/SKILL.md) | Break a project into small, ordered steps with clear done-checks. |

### Writing

| Skill | Description |
|---|---|
| [humanize](./skills/writing/humanize/SKILL.md) | Define human-readable output for summaries, plans, and reports. |

### Experimental

| Skill | Description |
|---|---|
| [luolamies](./skills/experimental/luolamies/SKILL.md) | Ultra-compressed Caveman mode that keeps full technical accuracy. |

## Cursor Rules

Drop these into `.cursor/rules/` in your project.

| Rule | Description |
|---|---|
| [clean-code](./cursor-rules/clean-code.mdc) | Clean, maintainable, human-readable code. |
| [code-quality](./cursor-rules/code-quality.mdc) | Verification and change discipline for the agent. |
| [modules](./cursor-rules/modules.mdc) | Deep modules with small, simple interfaces. |
| [nextjs](./cursor-rules/nextjs.mdc) | Next.js with TypeScript and Tailwind. |
| [node-express](./cursor-rules/node-express.mdc) | Node.js and Express backend practices. |
| [python](./cursor-rules/python.mdc) | Python with Flask and SQLite. |
| [react](./cursor-rules/react.mdc) | React components and patterns. |
| [tailwind](./cursor-rules/tailwind.mdc) | Tailwind CSS and UI components. |
| [typescript](./cursor-rules/typescript.mdc) | TypeScript coding standards. |

## CLAUDE.md Templates

Copy into your project root as `CLAUDE.md`.

| Template | Description |
|---|---|
| [general](./claude-md/general/CLAUDE.md) | Generic communication and UI preferences. |
| [python](./claude-md/python/CLAUDE.md) | Python projects managed with `uv`. |
| [experimental](./claude-md/experimental/CLAUDE.md) | "Slow Mode" that keeps the human in every decision. |

## Automations

Prompts for scheduled or recurring agent tasks.

| Automation | Tool | Description |
|---|---|---|
| [codebase-audit](./automations/claude/codebase-audit.md) | Claude | Find the highest-impact improvements across tests, CI, debt, and performance. |
| [daily-email-brief](./automations/claude/daily-email-brief.md) | Claude | Triage the last 24h of Gmail and draft routine replies. |
| [ai-feature-ideation](./automations/codex/ai-feature-ideation.md) | Codex | Generate AI/ML feature ideas grounded in the codebase. |
| [deprecated-pattern-scan](./automations/codex/deprecated-pattern-scan.md) | Codex | Detect deprecated APIs and migration opportunities. |
| [docs-site-link-checker](./automations/codex/docs-site-link-checker.md) | Codex | Monitor docs and marketing sites for broken links. |
| [feature-idea-automation](./automations/codex/feature-idea-automation.md) | Codex | Generate context-aware feature ideas from project docs. |
| [security-scan](./automations/codex/security-scan.md) | Codex | Scan code and dependencies for vulnerabilities and secrets. |
| [skill-creation](./automations/codex/skill-creation.md) | Codex | Improve or create skills based on recent sessions. |

## Coding Guidelines

| Guideline | Description |
|---|---|
| [architecture-philosophy](./coding-guidelines/architecture-philosophy.md) | Architecture principles. |
| [avoid-conjoined-methods](./coding-guidelines/avoid-conjoined-methods.md) | Each method should be understandable on its own. |
| [avoid-error-complexity](./coding-guidelines/avoid-error-complexity.md) | Only expose errors when callers must make a real decision. |
| [module-design-guideline](./coding-guidelines/module-design-guideline.md) | Design deep modules and avoid pass-through layers. |

## Setup Guides

| Guide | Description |
|---|---|
| [init-monorepo](./setup-guides/init-monorepo.md) | TypeScript monorepo with pnpm workspaces and Turborepo. |

## Reading Notes

| Book | Description |
|---|---|
| [refactoring-ui](./reading-notes/refactoring-ui.md) | Key insights from *Refactoring UI*. |

## License

[MIT](./LICENSE) © Henri Maronen
