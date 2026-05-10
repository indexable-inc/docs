# CLI

```bash
curl -fsSL https://ix.dev/install.sh | sh
```

Auth reads `IX_TOKEN` from the environment. Create one at https://ix.dev/tokens.

> [!NOTE]
> Thin wrapper over the API. Everything here is also available via [Python](sdk/python.md) and [TypeScript](sdk/typescript.md) SDKs.

## Commands

| Command | |
|---|---|
| `ix vm create <image>` | Boot a VM from an OCI image |
| `ix vm fork <vm-id>` | Fork a running VM |
| `ix vm snapshot <vm-id>` | Snapshot memory + disk |
| `ix vm restore <vm-id> --snapshot <id>` | Restore from a snapshot |
| `ix vm list` | List VMs |
| `ix vm delete <vm-id>` | Delete a VM |
| `ix vm ssh <vm-id>` | SSH into a VM |
| `ix vm exec <vm-id> -- <cmd>` | Run a command |

## Flags

| Flag | |
|---|---|
| `--region us-east \| us-west` | Region to create in |
| `--count <n>` | Number of forks |
| `--snapshot <id>` | Snapshot to restore |
