
- #### Automated every 2-3 Hrs from [NixOS/nixpkgs](https://github.com/NixOS/nixpkgs)
> The [Markdown README](https://github.com/Azathothas/NixOS-Packages/blob/main/README.md) **may not render because of huge file size.**
> - View [RAW](https://pub.ajam.dev/repos/Azathothas/NixOS-Packages/nixpkgs.txt): https://pub.ajam.dev/repos/Azathothas/NixOS-Packages/nixpkgs.txt
> - View [Markdown](https://pub.ajam.dev/repos/Azathothas/NixOS-Packages/README.md.txt): https://pub.ajam.dev/repos/Azathothas/NixOS-Packages/README.md.txt
> #### Why?
> - I wanted an `easy to parse`, `automatable` metadata for nix packages I could [`compile/cross-compile statically`](https://bin.ajam.dev/) for [Azathothas/Toolpacks](https://github.com/Azathothas/Toolpacks).
> - If [search.nixos.org](https://github.com/NixOS/nixos-search) ever offers an **`easy-to-use`** API, this repo will be Archived.
> > - https://github.com/NixOS/nixos-search/issues/296
---
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

#https://askubuntu.com/a/1471201 (https://www.freedesktop.org/software/systemd/man/latest/systemd.resource-control.html)
systemd-run --scope -p CPUQuota="60%" -p MemoryMax="8192M" -p MemoryHigh="4096M" --user nix search "nixpkgs#pkgsStatic" "^" --extra-experimental-features nix-command --extra-experimental-features flakes --refresh --quiet


#Check if only package `xyz` can be built
nix search "nixpkgs#pkgsStatic" "xyz" --extra-experimental-features nix-command --extra-experimental-features flakes --refresh --quiet
```

- #### legacyPackages
> - https://www.reddit.com/r/programmingcirclejerk/comments/13vptkz/the_legacy_in_legacypackages_doesnt_imply_that/
