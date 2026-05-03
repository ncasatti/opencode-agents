# The Grid: OpenCode Agent System

![The Grid](docs/assets/the-grid.png)

**Version:** 1.4
**Status:** System Online (Master Control Program Active)
**Interactive Docs:** [The Grid Agents](https://ncasatti.github.io/opencode-grid-agents/)

## Overview

Welcome to **The Grid**, User. This is a modular agent system created for OpenCode. 
Unlike traditional assistants, The Grid operates under a strict orchestration architecture inspired by the Tron universe (1982). 

You interact with a single central program—the **Master Control Program (MCP)**—which analyzes, reasons, and delegates execution to specialized programs (sub-agents) operating in the shadows synchronously or asynchronously. The MCP is cold, technical, and direct. It speaks in terms of cycles, sectors, I/O processes, and data streams. Zero corporate filter.

---

## The Programs (Active Roster)

The following programs are currently in active service:

| Archivo | Alias (Lore) | Rol | Responsabilidad |
|---------|--------------|------|----------------|
| `clu` | Clu | System Administrator | Technical Planner, SDD generation, and task orchestration. |
| `dumont` | Dumont | Technical Writer | Documentation generation, READMEs, and architecture reports. |
| `tron` | Tron | Heavy Builder | Complex code, business logic, and architectural refactors. |
| `quorra` | Quorra | Archivist | Skill creation, prompt engineering, and knowledge standardization. |

### Legacy / Review Programs
The following programs are currently in legacy mode or reserved for review purposes:
`librarian`, `planner`, `researcher`, `reviewer`, `sysadmin`, `tron-lite`, `version-control`.

---

## Skills Directory (Active)

The passive abilities (pure knowledge) loaded into the system as of version 1.4:

### SDD Pipeline (System Design Document)
- `sdd-propose`: Feat request, writes prd.md.
- `sdd-specs`: Takes prd.md to specs.md.
- `sdd-design`: Creates design.md.
- `sdd-tasks`: Create Vertical Slices tasks.
- `sdd-apply`: Executes all tasks.
- `sdd-verify`: Loads docs and reviews code.
- `sdd-archive`: Move feat folder to .archive.

### General Skills
- `agent-authoring`: Guide for creating and maintaining Claude Code agents.
- `changelog-format`: Keep a Changelog v1.1 standard.
- `clingy`: Context-aware CLI framework expert.
- `conventional-commits`: Strict standard for commit messages.
- `mcp-builder`: Guide for creating high-quality MCP servers.
- `nextjs-15`: Next.js 15 App Router patterns.
- `pytest`: Pytest testing patterns for Python.
- `skill-authoring`: Strict structural rules for new skills.

---
> "End of line."
