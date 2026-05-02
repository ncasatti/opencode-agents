# Troubleshooting

## Common Issues
- **Command not found**: Add to `environment.systemPackages` and `nixos-rebuild switch`.
- **Flake lock out of sync**: Run `nix flake update` and commit `flake.lock`.
- **Store full**: Run `nix-collect-garbage -d` and `nix-store --optimise`.
- **Rollback failed**: Check `nixos-rebuild list-generations`.

## Maintenance
- `nix-collect-garbage`: Remove unreachable packages.
- `nix-collect-garbage -d`: Remove old generations.
- `nix-store --optimise`: Hard-link identical files.
