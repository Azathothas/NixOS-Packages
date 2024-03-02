- #### List all Details about `pkg-xyz`
```bash
 nix-env --query --available --meta --json "pkg-xyz"
```

- #### List all Packages from [NixOS-Packages.json](https://pub.ajam.dev/repos/Azathothas/NixOS-Packages/nixpkgs.json)
```bash
curl -qfsSL "https://pub.ajam.dev/repos/Azathothas/NixOS-Packages/nixpkgs.json" | jq -r '.[] | .pname' | sort -u
```

- #### List all Packages that can be _potentially_ `Statically Built`
```bash
!# Refs: https://functor.tokyo/blog/2021-10-20-nix-cross-static
nix search "nixpkgs#pkgsStatic" "^" --extra-experimental-features nix-command --extra-experimental-features flakes --refresh --quiet

#Check if only package `xyz` can be built
nix search "nixpkgs#pkgsStatic" "xyz" --extra-experimental-features nix-command --extra-experimental-features flakes --refresh --quiet
```
