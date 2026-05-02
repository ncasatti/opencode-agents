# Nix Flakes

Flakes standardize how Nix projects declare dependencies and outputs.

## Structure
```nix
{
  description = "Project environment";

  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";
    flake-utils.url = "github:numtide/flake-utils";
  };

  outputs = { self, nixpkgs, flake-utils }:
    flake-utils.lib.eachDefaultSystem (system:
      let pkgs = nixpkgs.legacyPackages.${system}; in
      {
        devShells.default = pkgs.mkShell {
          buildInputs = with pkgs; [ nodejs python3 ];
        };
      }
    );
}
```

## Essential Commands
- `nix flake init`: Create `flake.nix`.
- `nix flake update`: Update `flake.lock`.
- `nix develop`: Enter project environment.
- `direnv` + `use flake`: Recommended for daily work.

## Updating
- `nix flake update`: Update all inputs.
- `nix flake lock --update-input <input>`: Update specific input.
- **Always commit `flake.lock` to version control.**
