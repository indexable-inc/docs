# Virtual Machines

VMs boot in ~1 second from any OCI image.

> [!NOTE]
> ~1s is median for cached images in a warm region. First pull of a large image is slower. Full VMs with their own kernel; PID 1 is your entrypoint; systemd works.

## Create

```bash
ix vm create <image> [--region us-east|us-west]
```

```bash
ix vm create ubuntu:24.04
ix vm create postgres:16
ix vm create my-registry.com/my-app:latest
```

## Fork

```bash
ix vm fork <vm-id> [--count N]
```

Forks are copy-on-write. Disk blocks are deduplicated, so each fork costs only the bytes that diverge from the parent.

```bash
ix vm fork vm-7f3a              # one fork
ix vm fork vm-7f3a --count 100  # 100 forks
```

## Snapshot

```bash
ix vm snapshot <vm-id>
```

Captures memory and disk. Snapshots are immutable. Restore or fork from them later.

## Restore

```bash
ix vm restore <vm-id> --snapshot <snap-id>
```

VM resumes exactly where the snapshot was taken.

## List

```bash
ix vm list
```

```
ID       STATUS   VCPU  MEM     REGION
vm-7f3a  running  2     8 GiB   us-east
vm-a1b2  running  2     8 GiB   us-east
vm-c3d4  stopped  4     16 GiB  us-west
```

## SSH / exec / delete

```bash
ix vm ssh <vm-id>
ix vm exec <vm-id> -- <command>
ix vm delete <vm-id>
```
