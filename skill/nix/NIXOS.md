# NixOS System Configuration

## Basic Structure
```nix
{ config, pkgs, ... }:
{
  imports = [ ./hardware-configuration.nix ];

  environment.systemPackages = with pkgs; [ vim git ];

  boot.loader.grub.enable = true;
  networking.hostName = "nixos-machine";
  system.stateVersion = "24.05";
}
```

## Modular Configuration
Split complex systems into modules:
```nix
imports = [
  ./modules/desktop.nix
  ./modules/development.nix
];
```

## Common Services
- **Nginx**: `services.nginx.enable = true;`
- **PostgreSQL**: `services.postgresql.enable = true;`
- **Docker**: `virtualisation.docker.enable = true;`
