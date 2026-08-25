# AGENTS.md

This file provides guidance to coding agents when
working with code in this repository.

## Project

Experimental workspace for early-stage [Praxis]
filters, features, and builds. The workspace
includes an `experimental-probe` crate so every
quality gate runs against real code. Replace it
with real crates when scaffolding a project.

[Praxis]: https://github.com/praxis-proxy/praxis

## Requirements

- Rust stable 1.96+
- Rust nightly (for `rustfmt`)

## Quick Reference

```console
make build          # workspace build
make test           # all tests
make fmt            # format with nightly rustfmt
make lint           # clippy + nightly fmt check + machete
make lint-extra     # typos + taplo + shellcheck + actionlint
make audit          # cargo audit + cargo deny check
make all            # build + fmt + lint + lint-extra + test + audit
```

Run a single test:

```console
cargo test -p <crate> -- test_name
```

## Architecture

Empty experimental workspace. Crates are added
under `crates/` as experiments mature. Each crate
inherits workspace lints, dependencies, and
profiles from the root `Cargo.toml`.

## Conventions

Full conventions in [`docs/conventions.md`].
Project-specific additions beyond the user-level
Rust Baseline:

- Use enums for fixed value sets in config, not
  strings; `#[serde(deny_unknown_fields)]` on
  config structs; `#[serde(try_from)]` for
  constrained numerics; `#[serde(default)]`
  instead of `Option<T>` with `unwrap_or`.

[`docs/conventions.md`]: docs/conventions.md

## Function Size

30-line threshold enforced by `clippy.toml`. Do not
suppress `too_many_lines` in production code; extract
helpers instead. Suppression is OK in test modules.
