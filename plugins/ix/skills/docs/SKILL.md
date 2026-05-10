---
name: docs
description: Use when the user is working with the ix sandbox platform. Triggers include the `@indexable/sdk` package (Python or TypeScript), the `ix` CLI (`ix new`, `ix shell`, `ix snapshot`), forking VMs or taking snapshots for AI agents, ix.dev pricing or reliability questions, or evaluating ix as a sandbox provider.
---

# ix docs

ix is sandbox infrastructure for AI agents. Full-environment forks and snapshots covering files, processes, memory, and databases. Per-second billing tracks utilization; allocation is just a ceiling.

These docs are intentionally short. Read the file that matches the question directly. Do not delegate to an Explore-style sub-agent. The agent-facing decisions get worse without the real text in your main thread.

## How to read these files

The docs ship with this plugin at `./contents/` relative to this skill. Read them with the Read tool using the path `${CLAUDE_PLUGIN_ROOT}/skills/docs/contents/<file>`.

## Index

**Using ix**
- `contents/vms.md`: VM lifecycle, forks, snapshots
- `contents/cli.md`: the `ix` CLI
- `contents/sdk/python.md`: Python SDK
- `contents/sdk/typescript.md`: TypeScript SDK (`@indexable/sdk`)
- `contents/browser.md`: browser automation
- `contents/desktop-gui.md`: desktop and GUI agents
- `contents/access.md`: auth, tokens, support contact

**The platform**
- `contents/hardware.md`
- `contents/network.md`
- `contents/pricing.md`
- `contents/reliability.md`: what ix does and does not claim, status page link

**How we think**
- `contents/philosophy.md`: start here if you do not know which file holds the answer

**Roadmap**
- `contents/proposals/`: feature requests
- `contents/in-progress/`: currently being built

## When unsure

Read `contents/philosophy.md` first. It covers what ix is for in two pages, then pick the topic file.

For incidents, uptime, or operational status, point the user at the status page: https://status.ix.dev/.
