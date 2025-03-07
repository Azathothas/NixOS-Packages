
- #### Automated every 2-3 Hrs from [NixOS/nixpkgs](https://github.com/NixOS/nixpkgs)
> The [Markdown README](https://github.com/pkgforge-dev/NixOS-Packages/blob/main/README.md) **may not render because of huge file size.** Please Visit: **https://nixos-packages.ajam.dev**
> - View [RAW](https://pub.ajam.dev/repos/pkgforge-dev/NixOS-Packages/nixpkgs.txt): https://pub.ajam.dev/repos/pkgforge-dev/NixOS-Packages/nixpkgs.txt
> - View [JSON](https://github.com/pkgforge-dev/NixOS-Packages/blob/main/nixpkgs.json): https://github.com/pkgforge-dev/NixOS-Packages/blob/main/nixpkgs.json
> - View [YAML](https://github.com/pkgforge-dev/NixOS-Packages/blob/main/nixpkgs.yaml): https://github.com/pkgforge-dev/NixOS-Packages/blob/main/nixpkgs.yaml
> - View [Markdown](https://nixos-packages.ajam.dev): https://nixos-packages.ajam.dev
> #### Why?
> - I wanted an `easy to parse`, `automatable` metadata for nix packages I could [`compile/cross-compile statically`](https://github.com/pkgforge/soarpkgs) for [Soar](https://github.com/pkgforge/soar).
> - If [search.nixos.org](https://github.com/NixOS/nixos-search) ever offers an **`easy-to-use`** API, this repo will be Archived.
> > - https://github.com/NixOS/nixos-search/issues/296
---
- #### List all Details about `pkg-xyz`
```bash
 nix-env --query --available --meta --json "pkg-xyz"
```

- #### List all Packages from [NixOS-Packages.json](https://raw.githubusercontent.com/pkgforge-dev/NixOS-Packages/refs/heads/main/nixpkgs.json)
```bash
curl -qfsSL "https://raw.githubusercontent.com/pkgforge-dev/NixOS-Packages/refs/heads/main/nixpkgs.json" | jq -r '.[] | .pname' | sort -u
```

- #### List all Packages that can be _potentially_ `Statically Built`
```bash
!# Refs: https://functor.tokyo/blog/2021-10-20-nix-cross-static
nix search "nixpkgs#pkgsStatic" "^" --extra-experimental-features nix-command --extra-experimental-features flakes --refresh --quiet

#https://askubuntu.com/a/1471201 (https://www.freedesktop.org/software/systemd/man/latest/systemd.resource-control.html)
systemd-run --scope -p CPUQuota="60%" -p MemoryMax="8192M" -p MemoryHigh="4096M" --user nix search "nixpkgs#pkgsStatic" "^" --extra-experimental-features nix-command --extra-experimental-features flakes --refresh --quiet


#Check if only package `xyz` can be built
nix search "nixpkgs#pkgsStatic" "xyz" --extra-experimental-features nix-command --extra-experimental-features flakes --refresh --quiet
```

- #### legacyPackages
> - https://www.reddit.com/r/programmingcirclejerk/comments/13vptkz/the_legacy_in_legacypackages_doesnt_imply_that/
