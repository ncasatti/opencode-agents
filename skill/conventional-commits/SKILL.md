---
name: conventional-commits
description: Estándar estricto para mensajes de commit. Use when creating commits, writing commit messages, or reviewing version control history.
---

# Conventional Commits Standard

## Quick start

You must follow this format for all git commits:
`<type>(<scope>): <description>`

Example: `feat(auth): add jwt login endpoint`

## Workflows

### 1. Writing a Commit Message
- [ ] **Determine the Type:** Select the appropriate type based on the nature of the change.
- [ ] **Determine the Scope (Optional):** Identify the section of the codebase affected.
- [ ] **Write the Description:** Use imperative, present tense ("add" not "added"). Keep it under 50 characters. No period at the end.
- [ ] **Format:** Combine them as `<type>(<scope>): <description>`. ONLY write the title. NO body, NO extra lines.

## Types Description

- `feat`: A new feature for the user, not a new feature for build script.
- `fix`: A bug fix for the user, not a fix to a build script.
- `docs`: Changes to the documentation only.
- `style`: Formatting, missing semi colons, etc; no production code change.
- `refactor`: Refactoring production code, eg. renaming a variable.
- `test`: Adding missing tests, refactoring tests; no production code change.
- `chore`: Updating grunt tasks etc; no production code change.
- `perf`: A code change that improves performance.
- `ci`: Changes to our CI configuration files and scripts.
- `build`: Changes that affect the build system or external dependencies.
- `revert`: Reverts a previous commit.

## Scopes

Scopes are optional and project-specific. Common examples:
- `auth`: Authentication/Authorization
- `ui`: User interface components
- `db`: Database operations
- `api`: API endpoints and calls
- `config`: Configuration files
- `deps`: Dependency updates

**Note:** Define project-specific scopes in your project's `AGENTS.md` file.

## Examples

- `feat(auth): add jwt login endpoint`
- `fix(db): resolve connection timeout in production`
- `refactor(sync): unify logging system in SincronizacionApiActivity`
- `fix(ui): repair broken submit button onClick handler`
- `feat(api): add pagination support for getAvanceVenta`
- `chore(build): update Kotlin version to 1.9.0`