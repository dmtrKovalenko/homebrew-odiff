# homebrew-odiff

A [Homebrew](https://brew.sh) tap for [**odiff**](https://github.com/dmtrKovalenko/odiff) — the fastest pixel-by-pixel image visual-difference tool.

## Install

```sh
brew install dmtrKovalenko/odiff/odiff
```

or tap first, then install:

```sh
brew tap dmtrKovalenko/odiff
brew install odiff
```

Upgrade later with:

```sh
brew upgrade odiff
```

## Supported platforms

The formula installs the prebuilt binary published on each upstream GitHub
release:

| Platform | Asset |
| --- | --- |
| macOS Intel | `odiff-macos-x64` |
| macOS Apple Silicon | `odiff-macos-arm64` |
| Linux x86_64 | `odiff-linux-x64` |
| Linux arm64 | `odiff-linux-arm64` |

Windows and RISC-V builds are published upstream but are not distributed
through Homebrew.

## How it stays up to date

This tap does **not** compile anything. `Formula/odiff.rb` simply points at the
prebuilt binaries attached to an upstream release, together with their SHA-256
checksums.

The formula is regenerated automatically by
[`.github/workflows/update-formula.yml`](.github/workflows/update-formula.yml):

- It runs hourly (and can be triggered manually via **Actions → Update formula
  → Run workflow**).
- It asks the GitHub API for the latest stable release of
  `dmtrKovalenko/odiff`.
- If that version differs from the one in `Formula/odiff.rb`, it downloads the
  four binary assets, hashes them, rewrites the formula, and commits the change.

All of that logic lives in [`scripts/update-formula.sh`](scripts/update-formula.sh),
so you can also run it locally:

```sh
gh auth login          # once, if needed
./scripts/update-formula.sh
```

## Notes

- The formula only becomes installable once an upstream release carries the
  prebuilt binary assets (`v4.4.0` and newer). Releases built before the
  prebuilt-binary workflow are skipped automatically.
- macOS binaries are ad-hoc signed by the Zig toolchain, so they run without a
  developer certificate. Homebrew strips the download quarantine attribute on
  install.
