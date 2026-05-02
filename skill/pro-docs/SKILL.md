---
name: pro-docs
description: Guide for generating professional software documentation. Use when writing READMEs, API references, architecture docs, or any project documentation.
---

# Professional Software Documentation

## Quick start

When creating documentation, adhere to the Minimum Viable Documentation principle: write short, useful documents. Separate content into Tutorials, How-to guides, Technical reference, and Explanation.

## Workflows

### 1. Planning Documentation
- [ ] **Identify the Audience:** Determine if the user needs a tutorial, how-to, reference, or explanation.
- [ ] **Choose the Right File:** Don't create monolithic files. Use `README.md`, `INSTALLATION.md`, `REFERENCE.md`, `ARCHITECTURE.md`, etc.
- [ ] **Avoid Duplication:** Never repeat information. Link to existing docs.

### 2. Writing Content
- [ ] **Write for Humans:** Use clear, plain language. List the simplest use case first.
- [ ] **Format Consistently:** Use proper Markdown headings (`#`, `##`, `###`), bolding for critical paths, and syntax-highlighted code blocks.
- [ ] **Use Tables:** Present environment variables, API parameters, or feature comparisons in Markdown tables.

### 3. Structuring the Repository
- [ ] **README.md:** The entry point. Include description, badges, prerequisites, fast install, basic usage, and navigation links.
- [ ] **Navigation:** Include back-links to `README.md` in all sub-documents. Add a Table of Contents for long files.

## Advanced features

For detailed architectural principles, repository structure, and formatting rules, see [REFERENCE.md](REFERENCE.md).