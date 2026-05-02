---
name: agent-authoring
description: Architect, design, and audit AI agents using structured prompts, cognitive frameworks, and tool design principles. Use when creating a new agent, writing system prompts, or auditing agent architecture.
---

# Agent Authoring

## Quick start

When designing a new agent, follow these core steps:
1. Define the **Cognitive Framework** (Memory & Action spaces).
2. Choose a **Reasoning Pattern** (ReAct, Plan-and-Execute, Reflection).
3. Draft the **System Prompt** using Markdown, Role-Based Definition, and the ICE Method.
4. Design **Tools** with clear names, docstrings, and error handling.

## Workflows

### 1. Designing a New Agent
- [ ] Define the agent's role and boundaries.
- [ ] Select the appropriate reasoning pattern based on task complexity.
- [ ] Determine if subagent orchestration is needed (Coordinator + Specialists).
- [ ] Draft the system prompt (see REFERENCE.md for principles).

### 2. Auditing an Existing Agent
- [ ] Check prompt structure (Markdown, ICE Method, Strategic Repetition).
- [ ] Verify tool definitions (verb-noun names, explicit type hints, error handling).
- [ ] Evaluate across Reasoning, Action, and Execution layers.

## Advanced features

For detailed principles on Prompt Engineering, Tool Design, and Evaluation, see [REFERENCE.md](REFERENCE.md).
