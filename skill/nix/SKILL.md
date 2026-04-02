---
name: nix
description: NixOS declarative configuration, Flakes, and environment management for systems migrating from Arch Linux.
compatibility: Claude Code, OpenCode
metadata:
  author: MCP
  version: 1.0.0
  tags: nixos, nix, declarative, flakes, environment, configuration
---

# Nix/NixOS

## Overview

Nix is a purely functional package manager and NixOS is a Linux distribution built on Nix principles. Unlike Arch Linux's imperative approach (install → configure → maintain), NixOS uses **declarative configuration**: your entire system state is defined in code (`configuration.nix`), reproducible across machines, and easily rolled back.

This skill covers the core concepts, Nix Flakes (modern dependency management), environment setup, and best practices for agents helping users migrate from Arch to NixOS.

## When to Use

✅ **Use this skill when:**
- Helping a user migrate from Arch Linux to NixOS
- Setting up reproducible development environments with Nix
- Configuring NixOS systems declaratively
- Working with Nix Flakes for project dependencies
- Troubleshooting NixOS configuration or package management
- Optimizing Nix store and garbage collection

❌ **Don't use this skill for:**
- General Linux system administration (use sysadmin skill)
- Package manager comparisons (use as reference only)
- Nix language deep-dive (reference Nix manual)

---

## Quick Reference

### Core Concepts

| Concept | Arch Equivalent | NixOS Approach |
|---------|-----------------|----------------|
| Install packages | `pacman -S pkg` | Declare in `configuration.nix` |
| System config | Edit `/etc/` files | Edit `configuration.nix` |
| Rollback | Manual backup | `nixos-rebuild switch --rollback` |
| Reproducibility | Manual documentation | Entire system in version control |
| Dev environments | Manual setup | `nix develop` or `nix-shell` |

### Essential Commands

```bash
# System management
sudo nixos-rebuild switch              # Apply configuration.nix changes
sudo nixos-rebuild test                # Test changes without persisting
sudo nixos-rebuild boot                # Apply on next boot
sudo nixos-rebuild switch --rollback   # Revert to previous generation

# Flakes (modern approach)
nix flake init -t github:nixos/templates/flake-utils  # Create flake.nix
nix flake update                       # Update lock file
nix develop                            # Enter project environment
nix build                              # Build project

# Garbage collection
nix-collect-garbage                    # Remove unused packages
nix-collect-garbage -d                 # Also remove old generations
nix-store --gc                         # Deep garbage collection

# Querying
nix-env -qa                            # List available packages (legacy)
nix search nixpkgs pkg-name            # Search packages (Flakes)
nix flake show                         # Show flake outputs
```

### Arch → NixOS Mental Model

| Arch Workflow | NixOS Workflow |
|---------------|----------------|
| `pacman -S nginx` | Add `services.nginx.enable = true;` to `configuration.nix` |
| Edit `/etc/nginx/nginx.conf` | Use `services.nginx.virtualHosts` in `configuration.nix` |
| `systemctl restart nginx` | `sudo nixos-rebuild switch` (automatic) |
| Manual backup before changes | Automatic generation tracking (rollback anytime) |
| `pacman -Syu` | `sudo nixos-rebuild switch` (pulls latest nixpkgs) |

---

## Core Concepts

### 1. Declarative Configuration

**The Shift:** Arch is imperative (you run commands that change state). NixOS is declarative (you describe desired state in code).

```nix
# /etc/nixos/configuration.nix
{ config, pkgs, ... }:

{
  # System packages (always available)
  environment.systemPackages = with pkgs; [
    vim
    git
    curl
  ];

  # Services (declaratively configured)
  services.openssh.enable = true;
  services.openssh.ports = [ 22 ];

  # Networking
  networking.hostName = "nixos-machine";
  networking.interfaces.eth0.ipv4.addresses = [{
    address = "192.168.1.100";
    prefixLength = 24;
  }];

  # User management
  users.users.nico = {
    isNormalUser = true;
    extraGroups = [ "wheel" "docker" ];
    shell = pkgs.zsh;
  };
}
```

**Key Principle:** Every configuration change is tracked as a "generation". You can roll back instantly.

### 2. Immutability & Purity

- **Immutable system files:** `/nix/store/` contains all packages in content-addressed paths.
- **No global state pollution:** Each package is isolated; removing one doesn't break others.
- **Reproducibility:** Same `configuration.nix` + same `flake.lock` = identical system on any machine.

### 3. Nix Flakes (Modern Approach)

Flakes standardize how Nix projects declare dependencies and outputs. They replace the older `default.nix` + `shell.nix` pattern.

**Structure:**
```nix
# flake.nix
{
  description = "Project environment";

  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";
    flake-utils.url = "github:numtide/flake-utils";
  };

  outputs = { self, nixpkgs, flake-utils }:
    flake-utils.lib.eachDefaultSystem (system:
      let
        pkgs = nixpkgs.legacyPackages.${system};
      in
      {
        devShells.default = pkgs.mkShell {
          buildInputs = with pkgs; [
            nodejs
            python3
            postgresql
          ];
        };

        packages.default = pkgs.hello;
      }
    );
}
```

**Key Files:**
- `flake.nix` — Declares inputs (dependencies) and outputs (what the flake provides)
- `flake.lock` — Locks exact versions (commit to version control for reproducibility)

### 4. Development Environments

**Option A: `nix develop` (Flakes)**
```bash
cd /path/to/project
nix develop  # Enters shell with dependencies from flake.nix
```

**Option B: `nix-shell` (Legacy, still valid)**
```bash
nix-shell -p nodejs python3 postgresql  # Ad-hoc environment
```

**Option C: `direnv` + Flakes (Recommended for daily work)**
```bash
# .envrc
use flake
```
Then `direnv allow` — automatically enters environment when you `cd` into the directory.

---

## Nix Flakes Deep Dive

### Flake Inputs

Inputs are dependencies. They can be:
- **GitHub repos:** `github:owner/repo` or `github:owner/repo/branch`
- **Local paths:** `path:/home/user/my-project`
- **Registries:** `nixpkgs` (shorthand for `github:nixos/nixpkgs`)

```nix
inputs = {
  nixpkgs.url = "github:nixos/nixpkgs/nixos-24.05";
  nixpkgs-unstable.url = "github:nixos/nixpkgs/nixos-unstable";
  flake-utils.url = "github:numtide/flake-utils";
  my-lib = {
    url = "github:myorg/my-lib";
    inputs.nixpkgs.follows = "nixpkgs";  # Share nixpkgs version
  };
};
```

### Flake Outputs

Outputs define what the flake provides. Common patterns:

```nix
outputs = { self, nixpkgs, flake-utils }:
  flake-utils.lib.eachDefaultSystem (system:
    let
      pkgs = nixpkgs.legacyPackages.${system};
    in
    {
      # Development shell
      devShells.default = pkgs.mkShell { ... };

      # Packages to build
      packages.default = pkgs.hello;
      packages.my-app = pkgs.callPackage ./default.nix { };

      # Apps (runnable programs)
      apps.default = {
        type = "app";
        program = "${pkgs.hello}/bin/hello";
      };

      # Checks (tests)
      checks.default = pkgs.runCommand "test" { } ''
        ${pkgs.hello}/bin/hello > $out
      '';
    }
  );
```

### Updating Flakes

```bash
nix flake update              # Update all inputs to latest
nix flake update nixpkgs      # Update only nixpkgs
nix flake lock --update-input nixpkgs  # Same as above
```

Always commit `flake.lock` to version control.

---

## NixOS System Configuration

### Basic Structure

```nix
# /etc/nixos/configuration.nix
{ config, pkgs, ... }:

{
  imports = [
    ./hardware-configuration.nix
    ./modules/networking.nix
    ./modules/services.nix
  ];

  # System packages
  environment.systemPackages = with pkgs; [ vim git ];

  # Boot configuration
  boot.loader.grub.enable = true;
  boot.loader.grub.device = "/dev/sda";

  # Networking
  networking.hostName = "my-machine";

  # Time zone
  time.timeZone = "UTC";

  # Locale
  i18n.defaultLocale = "en_US.UTF-8";

  # Users
  users.users.root.initialPassword = "changeme";

  # System version
  system.stateVersion = "24.05";
}
```

### Modular Configuration

For complex systems, split configuration into modules:

```nix
# /etc/nixos/configuration.nix
{ config, pkgs, ... }:

{
  imports = [
    ./hardware-configuration.nix
    ./modules/desktop.nix
    ./modules/development.nix
    ./modules/services.nix
  ];

  system.stateVersion = "24.05";
}
```

```nix
# /etc/nixos/modules/development.nix
{ config, pkgs, ... }:

{
  environment.systemPackages = with pkgs; [
    git
    neovim
    rustup
  ];

  programs.direnv.enable = true;
}
```

### Common Service Configurations

**Nginx:**
```nix
services.nginx.enable = true;
services.nginx.virtualHosts."example.com" = {
  forceSSL = true;
  enableACME = true;
  locations."/" = {
    proxyPass = "http://localhost:3000";
  };
};
```

**PostgreSQL:**
```nix
services.postgresql.enable = true;
services.postgresql.package = pkgs.postgresql_15;
services.postgresql.initialScript = pkgs.writeText "init.sql" ''
  CREATE USER myuser WITH PASSWORD 'mypass';
  CREATE DATABASE mydb OWNER myuser;
'';
```

**Docker:**
```nix
virtualisation.docker.enable = true;
users.users.nico.extraGroups = [ "docker" ];
```

---

## Package Management

### System Packages vs User Packages

**System packages** (in `configuration.nix`):
- Available to all users
- Managed by `nixos-rebuild`
- Declarative and reproducible

**User packages** (legacy `nix-env`):
- ❌ **Avoid** — imperative, breaks reproducibility
- Use Flakes or `environment.systemPackages` instead

### Installing Packages

**Declaratively (Recommended):**
```nix
environment.systemPackages = with pkgs; [
  vim
  git
  htop
  neovim
];
```

**Ad-hoc with Flakes:**
```bash
nix shell nixpkgs#nodejs nixpkgs#python3
```

**Legacy (Don't use):**
```bash
nix-env -i nodejs  # ❌ Imperative, breaks reproducibility
```

### Finding Packages

```bash
# Search nixpkgs
nix search nixpkgs nodejs

# Browse online
# https://search.nixos.org/packages
```

---

## Garbage Collection & Maintenance

### Understanding Nix Store

The Nix store (`/nix/store/`) contains all packages. Each package is content-addressed:
```
/nix/store/abc123-package-name-1.0/
```

Old generations accumulate; garbage collection removes unused packages.

### Garbage Collection Commands

```bash
# Remove unreachable packages
nix-collect-garbage

# Remove unreachable packages AND old generations
nix-collect-garbage -d

# Deep garbage collection (slower, more thorough)
nix-store --gc

# Check store size
du -sh /nix/store

# Optimize store (hard-link identical files)
nix-store --optimise
```

### Automatic Garbage Collection

```nix
# /etc/nixos/configuration.nix
nix.gc.automatic = true;
nix.gc.dates = "weekly";
nix.gc.options = "--delete-older-than 30d";
```

---

## Best Practices

### DO ✅

- **Version your system:** Commit `configuration.nix` to git
- **Use Flakes for projects:** Modern, reproducible, standard
- **Lock dependencies:** Always commit `flake.lock`
- **Modularize configuration:** Split into logical modules
- **Use `nix develop`:** For project-specific environments
- **Read NixOS options:** `man configuration.nix` or https://search.nixos.org/options
- **Test before applying:** Use `nixos-rebuild test` before `switch`
- **Keep generations:** Rollback is your safety net

### DON'T ❌

- **Don't use `nix-env`:** It's imperative and breaks reproducibility
- **Don't edit `/etc/` directly:** Changes are lost on `nixos-rebuild`
- **Don't ignore `flake.lock`:** Commit it; it ensures reproducibility
- **Don't mix Flakes and legacy:** Choose one approach per project
- **Don't assume packages exist:** Search before declaring; some may need custom derivations
- **Don't skip `system.stateVersion`:** It's needed for safe upgrades

### Project Structure (Flakes)

```
my-project/
├── flake.nix              # Declares inputs and outputs
├── flake.lock             # Locked versions (commit this!)
├── .envrc                 # direnv integration (optional)
├── src/                   # Source code
├── default.nix            # Package definition (optional)
└── README.md
```

### NixOS System Structure

```
/etc/nixos/
├── configuration.nix      # Main config
├── hardware-configuration.nix  # Auto-generated
├── modules/
│   ├── desktop.nix
│   ├── development.nix
│   └── services.nix
└── secrets/               # Encrypted secrets (optional)
```

---

## Troubleshooting

### "Command not found" after `nixos-rebuild`

**Cause:** Package not in `environment.systemPackages` or not in `$PATH`.

**Fix:**
```nix
environment.systemPackages = with pkgs; [ missing-package ];
sudo nixos-rebuild switch
```

### Flake lock file out of sync

**Cause:** `flake.lock` doesn't match `flake.nix` inputs.

**Fix:**
```bash
nix flake update
git add flake.lock
git commit -m "Update flake.lock"
```

### `nix develop` not working

**Cause:** `flake.nix` missing or malformed.

**Fix:**
```bash
nix flake check  # Validate flake.nix
nix flake show   # Show available outputs
```

### Store is full (`/nix/store` huge)

**Cause:** Old generations and unused packages accumulating.

**Fix:**
```bash
nix-collect-garbage -d
nix-store --optimise
```

### Can't rollback to old generation

**Cause:** Generation was garbage collected.

**Fix:**
```bash
sudo nixos-rebuild switch --rollback  # Rollback to previous
nixos-rebuild list-generations        # See available generations
```

---

## Arch → NixOS Migration Checklist

- [ ] Install NixOS (use official ISO)
- [ ] Review `hardware-configuration.nix` (auto-generated)
- [ ] Migrate system packages to `environment.systemPackages`
- [ ] Migrate service configs to declarative modules
- [ ] Set up user accounts with `users.users.*`
- [ ] Configure networking, hostname, timezone
- [ ] Test with `nixos-rebuild test`
- [ ] Apply with `sudo nixos-rebuild switch`
- [ ] Commit `configuration.nix` to git
- [ ] For projects: Create `flake.nix` with dependencies
- [ ] Set up `direnv` for automatic environment loading

---

## Related Skills

- **sysadmin:** General Linux system administration
- **conventional-commits:** Version control standards (for committing configuration changes)

---

## References

- [NixOS Manual](https://nixos.org/manual/nixos/stable/)
- [Nix Flakes Documentation](https://nixos.wiki/wiki/Flakes)
- [Nixpkgs Package Search](https://search.nixos.org/packages)
- [NixOS Options Search](https://search.nixos.org/options)
- [Nix Pills](https://nixos.org/guides/nix-pills/) (Learning Nix language)
