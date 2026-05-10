# Proposals

Things people want ix to do.

> [!TIP]
> A proposal with a named advocate and a real use case is the most effective way to influence what we build next. We read everything, but we prioritize what blocks a specific user.

If your use case is already covered by a file in here, open a PR adding your GitHub handle to that file's `advocates` list. If it isn't, open a PR with a new `<name>.md`. Proposals help even if you're not sure you'll end up using ix: they tell us what people are asking for.

## Format

`proposals/<name>.md` with YAML frontmatter:

```markdown
---
advocates:
  - "@your-gh-handle"
  - "@a-coworker-who-also-wants-this"
---

# Short title

What you want. Why. What you'd use it for. How other sandbox providers (E2B, Modal, Firecracker, Daytona, whatever) handle it today if relevant.
```

Keep it short. One page is plenty.

## Lifecycle

- **proposals/** is the backlog. Anyone can open a PR.
- **[in-progress/](../in-progress/)** is what the ix team is actively building. When we start a proposal, its file moves there.
- When it ships, the file is deleted and the feature lives in the main docs.
