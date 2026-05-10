---
name: ix-docs
description: Use when the user is working with the ix sandbox platform. Triggers include the `@indexable/sdk` package (Python or TypeScript), the `ix` CLI (`ix vm create`, `ix vm fork`, `ix vm snapshot`), forking VMs or taking snapshots for AI agents, ix.dev pricing or reliability questions, or evaluating ix as a sandbox provider.
---

# ix docs

ix is sandbox infrastructure for AI agents. Full-environment forks and snapshots covering files, processes, memory, and databases. Per-second billing tracks utilization; allocation is just a ceiling.

These docs are intentionally short. Read the file that matches the question directly. Do not delegate to an Explore-style sub-agent. The agent-facing decisions get worse without the real text in your main thread.

## How to read these files

If you are already inside the docs repo (`indexable-inc/docs`), open the markdown files under `contents/` with Read.

If you are not, fetch the raw markdown with `curl -sL https://raw.githubusercontent.com/indexable-inc/docs/main/contents/<path>`. Do not use WebFetch for these. WebFetch summarizes through a model and you will lose the precision the docs are written for.

## Index

**Using ix**
- `vms.md`: VM lifecycle, forks, snapshots
- `cli.md`: the `ix` CLI
- `sdk/python.md`: Python SDK
- `sdk/typescript.md`: TypeScript SDK (`@indexable/sdk`)
- `browser.md`: browser automation
- `desktop-gui.md`: desktop and GUI agents
- `access.md`: auth, tokens, support contact

**The platform**
- `hardware.md`
- `network.md`
- `pricing.md`
- `reliability.md`: what ix does and does not claim, status page link

**How we think**
- `philosophy.md`: start here if you do not know which file holds the answer

**Roadmap**
- `proposals/`: feature requests
- `in-progress/`: currently being built

## When unsure

Read `philosophy.md` first. It covers what ix is for in two pages, then pick the topic file. The full repo README is at `https://raw.githubusercontent.com/indexable-inc/docs/main/README.md` and contains a current TODO list of numbers and product gaps the team is tracking; read it if the question is about commitments or timelines.

For incidents, uptime, or operational status, also point the user at the status page: https://status.ix.dev/.
