## Versioning policy

Release versions track the Arturo version being packaged, with an optional packaging revision:

```text
v<arturo-version>[-r<revision>]
```

| Tag | Meaning |
|---|---|
| `v0.10.0` | Initial repository release packaging Arturo 0.10.0 |
| `v0.10.0-r1` | First packaging revision for Arturo 0.10.0 |
| `v0.10.0-r2` | Second packaging revision for Arturo 0.10.0 |
| `v0.10.1` | Initial repository release packaging Arturo 0.10.1 |

### Upstream versions

The base version always matches the Arturo release being packaged. Packaging changes do not increment Arturo’s major, minor, or patch version.

### Packaging revisions

Increment the revision when publishing changes for the same Arturo version, including build fixes, dependency adjustments, Windows integration fixes, or downstream patches.

Revisions start at `r1` after the initial release and reset when the Arturo version changes. Release notes must describe any downstream patches that change runtime behavior.

Documentation-only changes do not normally require a release.

### MSYS2 package versions

`PKGBUILD` remains authoritative for MSYS2 package versions:

- `pkgver` identifies the Arturo version.
- `pkgrel` identifies the MSYS2 packaging revision and increases when the package changes.

The GitHub `rN` suffix counts releases in this repository independently of `pkgrel`. Each release must state the corresponding `pkgver-pkgrel`.

### Release guarantees

Published tags and release artifacts are immutable. Corrections require a new release.

This repository follows upstream-aligned package versioning rather than strict Semantic Versioning. Packaging revisions are stable releases unless explicitly marked as prereleases.
