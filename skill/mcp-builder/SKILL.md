---
name: mcp-builder
description: Guide for creating high-quality MCP (Model Context Protocol) servers that enable LLMs to interact with external services through well-designed tools. Use when building MCP servers to integrate external APIs or services, whether in Python (FastMCP) or Node/TypeScript (MCP SDK).
---

# MCP Server Development Guide

## Quick start

Create MCP (Model Context Protocol) servers that enable LLMs to interact with external services through well-designed tools. The quality of an MCP server is measured by how well it enables LLMs to accomplish real-world tasks.

Recommended stack: TypeScript (high-quality SDK support) with Streamable HTTP for remote servers or stdio for local servers.

## Workflows

Creating a high-quality MCP server involves four main phases:

- [ ] **Phase 1: Deep Research and Planning**
  - Understand modern MCP design (API coverage vs workflow tools).
  - Study MCP Protocol and Framework documentation.
  - Plan implementation and tool selection.
- [ ] **Phase 2: Implementation**
  - Set up project structure.
  - Implement core infrastructure (API client, error handling).
  - Implement tools with clear input/output schemas and descriptions.
- [ ] **Phase 3: Review and Test**
  - Review code quality (DRY, error handling, types).
  - Build and test using the MCP Inspector.
- [ ] **Phase 4: Create Evaluations**
  - Create 10 independent, read-only, complex, and verifiable questions.
  - Output evaluation as an XML file.

## Advanced features

For detailed instructions on each phase, see [REFERENCE.md](REFERENCE.md).

### Documentation Library

Load these resources as needed during development:

- [MCP Best Practices](./reference/mcp_best_practices.md) - Universal MCP guidelines.
- [TypeScript Implementation Guide](./reference/node_mcp_server.md) - Complete TypeScript guide.
- [Python Implementation Guide](./reference/python_mcp_server.md) - Complete Python/FastMCP guide.
- [Evaluation Guide](./reference/evaluation.md) - Complete evaluation creation guide.