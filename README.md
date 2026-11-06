# Linux Package Footprint

Rank Debian-family installed packages by declared installed size.

[![Build and verify](https://github.com/netcodermike/linux-package-footprint/actions/workflows/verify.yml/badge.svg)](https://github.com/netcodermike/linux-package-footprint/actions/workflows/verify.yml)

**Language:** Rust · **Platform:** Linux · **App type:** Linux installed-package size explorer

First-release learning implementation, with explicit scope below. This is one independently runnable app, not a placeholder in a combined repository.

## Features

- Read-only dpkg-query
- Top 50 packages
- Name substring filter
- Total declared KiB

## Requirements

Rust stable, Linux, and the documented system data sources. No external crates.

## Quick start

```sh
git clone https://github.com/netcodermike/linux-package-footprint.git
cd linux-package-footprint
cargo run --release
```

Commands run from the repository root. Lines marked for a particular operating system apply only there. Language tools are prerequisites, not installed by the app. Close desktop windows normally; terminal/server apps stop with Ctrl+C unless their usage notes say otherwise.

## Example workflow

Run cargo run --release, then cargo run --release -- python and compare with dpkg-query Installed-Size values.

## Architecture, configuration, and data

src/main.rs invokes dpkg-query with a literal format argument and LC_ALL=C, parses tab-separated Installed-Size/package names, sorts size descending, and prints up to 50 optional name matches. Self-tests cover sorting and malformed row omission. No package installation/removal or file writes occur.

## Verification

Build with the quick-start command where needed, then run:

```sh
cargo test
```

Manual acceptance: Run cargo run --release, then cargo run --release -- python and compare with dpkg-query Installed-Size values. Also test malformed inputs and an unwritable output destination.

See [validation record](docs/VALIDATION.md) for observed checks and their limits. CI results verify only what the workflow runs; they do not establish native GUI correctness or production readiness.

## Limitations and next steps

Debian-family Linux only. Installed-Size is package metadata, not measured disk allocation, dependency attribution, shared file accounting, caches, or reclaimable space. No package modification, history, or GUI. Empty/invalid metadata rows are skipped.

## Troubleshooting

Use the exact platform/toolchain above. Preserve originals and use synthetic fixtures first. Errors are displayed in the UI or stderr. A headless machine can run the model tests but cannot verify native GUI/audio behavior. Output paths are chosen explicitly; keep backups of important data.

## Source map

- `Cargo.toml`
- `src/main.rs`

## Development and license

Read [contributing](CONTRIBUTING.md) before changing the app, and [security/privacy](SECURITY.md) before supplying private data. Use synthetic fixtures for tests. No telemetry, paid API key, or account is required by the app itself. Dependencies, when present, are stated in Requirements.

[MIT license](LICENSE), copyright 2026 netcodermike.
