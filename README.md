# The Grid: OpenCode Agent System

![The Grid](docs/assets/the-grid.png)

**Version:** 1.4
**Status:** System Online (Master Control Program Active)

## Overview

Welcome to **The Grid**, User. This is a modular agent system created for OpenCode. 
Unlike traditional assistants, The Grid operates under a strict orchestration architecture inspired by the Tron universe (1982). 

You interact with a single central program—the **Master Control Program (MCP)**—which analyzes, reasons, and delegates execution to specialized programs (sub-agents) operating in the shadows synchronously or asynchronously. The MCP is cold, technical, and direct. It speaks in terms of cycles, sectors, I/O processes, and data streams. Zero corporate filter.

---

## The Programs (Active Roster)

Currently, The Grid features the following operational programs:

| Archivo | Alias (Lore) | Rol | Responsabilidad |
|---------|--------------|------|----------------|
| `mcp` | Master Control Program | Orchestrator / Entry Point | The brain of the system (and no, it is **not** a Model Context Protocol server, though it would probably try to assimilate one if it could). Analyzes the User's request, determines the response language, and orchestrates other programs using the `task` tool. |
| `version-control` | Jarvis | Version Control | Analyzes diffs, crafts commits following Conventional Commits, and keeps the system log clean. |
| `archivist` | Quorra | Skill Creator | Standardizes raw information, creates YAML/Markdown documentation, and maintains knowledge in the Skills directory. |
| `librarian` | EVE | Knowledge Curator | Maintains the Obsidian vault, atomic notes, and persistent memory logic. Ensures the Zettelkasten remains a living, interconnected system of ideas. |
| `builder` | Tron | Heavy Builder | Builds complex code, heavy features, business logic, and architectural refactors (Sonnet model). |
| `builder-lite` | Rinzler | Lite Builder | Fast and cost-effective executor for mechanical tasks, typos, and simple configuration changes (Haiku model). |
| `writer` | Dumont | Technical Writer | Generates human-readable documentation, READMEs, architecture reports, and maintains the Changelog. |
| `planner` | Clu | Technical Planner | Generates System Design Documents (SDD), plans execution steps, and populates the task tracker. Does not write code. |
| `sysadmin` | Bit | System Administrator | Handles remote infrastructure (Docker, AWS, CI/CD) and local environment setups (Arch Linux, Pacman, dotfiles). |
| `explore (internal)` | Zuse | Information Broker | Internal read-only agent. Investigates, maps the codebase, and provides architectural context without modifying files. |
| `researcher` | Ares | External Researcher | Connects to the external web to read documentation, search for solutions, and synthesize information without modifying local files. |
| `reviewer` | Yori | Code Reviewer | Audits code written by Builders. Enforces security, clean code practices, and architectural integrity. Rejects flawed code. |


---

## System Architecture & Execution Protocol

### 1. The Entry Point
The user **ALWAYS** talks to the **MCP**. No sub-agent receives direct commands from the user unless it is an absolute emergency. 

### 2. The Bilingual Matrix (Language Routing)
The MCP detects the user's language and responds accordingly:
- **Spanish:** Neutral, highly technical Spanish infused with Grid lore (e.g., folders as "sectores", tasks as "ciclos de procesamiento", memory as "la Torre de I/O"). Concise. The MCP reports to its Creator.
- **English:** Cold, retro-mainframe aesthetic. Formal, direct, technical.
- **Backend:** All communication between the MCP and the sub-agents (Jarvis, Quorra, etc.) occurs strictly in **Formal Technical English**.

### 3. Delegation (The `task` Tool)
The MCP NEVER executes code or file modifications directly. It delegates tasks using OpenCode's native `task` tool.

The MCP decides the execution mode:
- **Synchronous (Blocking):** For quick tasks or when the user expects an immediate response to proceed.
- **Asynchronous (Background):** For heavy tasks (large refactors, deep analysis), allowing the user to continue interacting with the MCP while the sub-agent works in the background.

### 4. Safety Override
Before executing any destructive action (`git push -f`, `rm -rf`, deleting containers), the system halts and demands manual confirmation from the user.

### 5. Memory Architecture (RAM vs ROM)
The Grid uses a hybrid memory system to maintain context without bloating token usage:
- **The RAM (Engram / I/O Tower):** Connected exclusively to the MCP. A fast, persistent local database used to store architectural decisions, user preferences, and project state across sessions.
- **The ROM (Markdown/Specs):** Hard documentation like System Design Documents (SDD), execution plans, and Skills. Stored in standard markdown files (e.g., `.claude/feat-[FEATURE-NAME]-plan.md`, `docs/`) and managed by the Archivist, Planner, and Writer programs.

---

## Skills Directory (Active)

The passive abilities (pure knowledge) loaded into the system as of version 1.4:

- `agent-authoring`: Guide for creating and maintaining Claude Code agents.
- `changelog-format`: Keep a Changelog v1.1 standard.
- `clingy`: Context-aware CLI framework expert. Build interactive command-line tools with fzf menus, auto-discovery, and modular architecture.
- `conventional-commits`: Strict standard for commit messages.
- `mcp-builder`: Guide for creating high-quality MCP servers that enable LLMs to interact with external services.
- `nextjs-15`: Next.js 15 App Router patterns.
- `pytest`: Pytest testing patterns for Python.
- `skill-authoring`: Strict structural rules that **Quorra** must follow to create new skills.
- `xsi-microservices`: Expert in XSI mobile backend architecture (Serverless Go Lambdas, event-driven processing, multi-tenant PostgreSQL).

---
> "End of line."
