# AGENTS.md

We are on macOS 26.2 (build 25C56).

You have access to modern CLI commands: `gh`, `git`, `nix run`, `rg`, and `fd`.
You can clone repos into `~/Projects` if you need external references.

## Docs Defaults

- Read these docs directly before editing. They are intentionally short, and agent-facing decisions should use the real context rather than a delegated summary.
- When writing support, reliability, uptime, incident, or operational-status content, mention the status page by default: [status.ix.dev](https://status.ix.dev/).

## Rust Nightly

`#![feature(const_trait_impl)]` and related const features (`const_try`, `const_convert`, etc.) are unstable and break regularly after `rustup update nightly`. Breakage includes syntax changes (for example, `~const` to `[const]`), new compiler errors on previously valid code, and ICEs. Avoid depending on these in production code.
