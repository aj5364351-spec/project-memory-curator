# Project Memory Curator — Give Your AI Assistant Persistent Project Memory

> **AI agents forget everything between sessions. Now they don't have to.**
>
> A single command initializes `.agent-knowledge/` — six categorized Markdown files that give your AI coding assistant persistent, auditable, git-trackable project memory. No databases. No APIs. No lock-in.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)
[![Platform: Any](https://img.shields.io/badge/Platform-Claude%20Code%20%7C%20Codex%20%7C%20Cursor%20%7C%20Any-blue)]()

---

## The Problem

Every time you start a new AI coding session, you're starting from zero. You re-explain your project's tech stack, re-discover which commands work, and re-debug problems you've already solved. Existing "memory" solutions lock your data into proprietary clouds, vector databases, or hidden caches you can't review, edit, or trust.

## The Solution

**Project Memory Curator** creates a `.agent-knowledge/` directory in your project root — six plain Markdown files that any file-capable agent can read and update. It retrieves only the most relevant entries before each task, and after verified work is complete, proposes structured updates for you to review, edit, or approve.

---

## Quick Start

### Install as a Claude Code / Codex skill

```bash
git clone https://github.com/aj5364351-spec/project-memory-curator \
  ~/.claude/skills/project-memory-curator
```

Restart your session. The skill loads automatically.

### Initialize your first project

```
检查并初始化 .agent-knowledge/
```

The agent scans your project, drafts a preview, and writes the knowledge base on your confirmation.

### Or use as a standalone template

Copy `assets/agent-knowledge/` into your project root as `.agent-knowledge/` and start editing. Any AI agent with filesystem access can consume it — no skill required.

---

## Knowledge Categories

| File | Purpose | Anti-pattern |
|---|---|---|
| `project.md` | Tech stack, directory structure, module boundaries | Temporary implementation details |
| `preferences.md` | Confirmed long-term preferences, constraints, collaboration habits | Inferred preferences |
| `runbook.md` | Verified commands: start, test, build, deploy, recover | Untested commands, credentials |
| `decisions.md` | Architecture decisions with context, rationale, and impact | Unsupported assumptions |
| `experiences.md` | Verified debugging, fix, deployment, and optimization lessons | Raw logs, unknown root causes |
| `todo-memory.md` | Candidates that need further verification — **never treated as fact** | Actionable facts |

---

## Hard Rules

- **No secrets.** Keys, tokens, passwords, credentials, private URLs, emails, customer data — never stored.
- **No guesses.** Unconfirmed observations go to `todo-memory.md` with `置信度：待确认` (confidence: unconfirmed); they are never applied as facts.
- **No chat logs.** Only conclusions with clear future reuse value; raw conversations and full logs are discarded.
- **Respect existing norms.** `AGENTS.md`, `CLAUDE.md`, `.cursor/rules` take precedence. Conflicts are surfaced to the user immediately.
- **Preview-then-save.** Writing requires explicit user confirmation or a persisted `auto-save=on` toggle. Every write is re-read and verified after commit.

### Auto-Save

Add a single magic comment to your knowledge base README to enable persistent auto-save:

```markdown
<!-- project-memory-curator:auto-save=on -->
```

No hooks, no platform features — just a comment in a Markdown file.

---

## Platform-Agnostic by Design

Uses only directory listing, text search, file read, and file write — capabilities every competent agent already has. Works across Claude Code, Codex, Cursor, Windsurf, and any other AI coding tool with filesystem access. No hooks, no custom tools, no network calls, no database.

---

## Structure

```
project-memory-curator/
├── SKILL.md                          # Skill definition (Chinese, works with any language)
├── README.md                         # This file
├── LICENSE                           # MIT
├── .gitignore
├── agents/
│   └── openai.yaml                   # Cross-platform agent metadata
├── references/
│   └── memory-entry-format.md        # Entry format specification
└── assets/
    └── agent-knowledge/
        ├── README.md                 # Knowledge base index + auto-save toggle
        ├── project.md                # Tech stack & architecture template
        ├── preferences.md            # User preferences template
        ├── runbook.md                # Commands & operations template
        ├── decisions.md              # Architecture decisions template
        ├── experiences.md            # Engineering experiences template
        └── todo-memory.md            # Unconfirmed candidates template
```

## Language

The skill definition is written in Chinese. The templates ship in Chinese by default. The knowledge base content you write can be in any language — the structure is fully language-agnostic.

---

## Companion

This skill shares the same `.agent-knowledge/` directory with **[Intelligent Experience Extractor](https://github.com/aj5364351-spec/intelligent-experience-extractor)** — a focused extension for extracting structured `problem → root cause → solution → verification → prevention` chains from verified debugging, build, deployment, and operations work.

Together they form a complete project knowledge system. Install both for the full workflow.

---

## License

MIT © 2026 zorix
