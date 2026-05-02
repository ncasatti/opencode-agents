---
name: nix
description: NixOS declarative configuration, Flakes, and environment management.
---

# Nix/NixOS

Nix is a purely functional package manager and NixOS is a Linux distribution built on Nix principles. This skill provides a modular reference for declarative system management and reproducible development environments.

## Modules

- [FLAKES.md](FLAKES.md) — Modern dependency management and project environments.
- [NIXOS.md](NIXOS.md) — System configuration, modules, and service management.
- [TROUBLESHOOTING.md](TROUBLESHOOTING.md) — Common issues and maintenance.
- [MIGRATION.md](MIGRATION.md) — NixOS setup and best practices.

## When to Use

✅ **Use this skill when:**
- Setting up reproducible development environments with Nix.
- Configuring NixOS systems declaratively.
- Working with Nix Flakes for project dependencies.
- Troubleshooting NixOS configuration or package management.

❌ **Don't use this skill for:**
- General Linux system administration (use `sysadmin` skill).
- Nix language deep-dive (refer to Nix Pills).

## Quick Reference

| Concept | NixOS Approach |
|---------|----------------|
| Install packages | Declare in `configuration.nix` |
| System config | Edit `configuration.nix` |
| Rollback | `nixos-rebuild switch --rollback` |
| Dev environments | `nix develop` or `direnv` |

## Best Practices

- **Version your system:** Commit `configuration.nix` to git.
- **Use Flakes for projects:** Modern, reproducible, standard.
- **Lock dependencies:** Always commit `flake.lock`.
- **Modularize configuration:** Split into logical modules.
- **Test before applying:** Use `nixos-rebuild test` before `switch`.
