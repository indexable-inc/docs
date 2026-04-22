# Reliability

ix is early. Read [What we don't claim yet](#what-we-dont-claim-yet) before committing production load.

## Simulation testing

Correctness-critical paths run under a deterministic simulator with fault injection: network partitions, disk errors, clock skew, process crashes, concurrent fork races. Failures replay exactly.

Surfaces under continuous test:

- Custom filesystem (copy-on-write, block dedup, fork isolation)
- Snapshot and restore (memory + disk consistency)
- VM lifecycle and scheduler

## Storage: VCFS

Custom filesystem underneath forks, snapshots, and tiering.

- **Content-addressed dedup across VMs.** Identical blocks stored once regardless of source (fork, OCI layer, same package across tenants). Forking a 100 GiB VM costs only divergent bytes. Snapshots are references into the same store. See [pricing](pricing.md).
- **Tiered durability.** Hot on local NVMe, warm replicated in-region, cold in redundant cross-zone object storage. Idle blocks spill down automatically.

Designed for fsync-heavy workloads (Postgres, MySQL, SQLite WAL). Writes hit local NVMe; dedup runs out of band. No published benchmarks yet comparing in-VM Postgres to bare-metal. If database performance matters, run your workload on both and compare.

## Security isolation

Each VM runs under `ix-vmm`, built on rust-vmm/KVM. Firecracker-like: small attack surface, minimal device model, one VM per host process. Network isolation is per-VM virtio-net on TAP. VMs don't see each other's traffic unless explicitly grouped ([network](network.md)).

> [!WARNING]
> KSM (cross-tenant memory page merging) is on by default. Timing side channels can in principle reveal whether a specific page exists in a neighbor. If you run sensitive key material, we can pin you to a KSM-disabled host or dedicated bare metal.

## Business continuity

- **Acquisition.** Keep the service running; honor active contracts. Escrow a migration window if the acquirer won't continue the product.
- **Wind-down.** Open-source the VMM and filesystem for self-hosting.
- **Portability.** Snapshots export as OCI images at any time.

> [!NOTE]
> These are intentions. If you need contractual terms, ask on Slack. Enterprise customers on dedicated bare metal get source access and self-host runbooks.

## Support

Goal: 24/7 human coverage. Currently close. Slack response usually minutes during working hours. See [access](access.md#support).

## What we don't claim yet

> [!WARNING]
> These are things other mature providers offer that we don't yet. Read this list before putting production load on ix.
>
> - Five-nines availability.
> - Multi-region HA (and no EU / APAC regions at all today).
> - Formal certifications (SOC 2, HIPAA, ISO 27001). Process starting soon.
> - Self-serve signup. Today onboarding is manual; see [access](access.md).
> - Public availability / durability SLAs with credits. Not yet default.

Why we invest in the substrate before the certifications: [philosophy](philosophy.md#reliable-but-early).

## SLAs on request

No default SLA yet. If you need contractual uptime, durability, MTTR, or data-residency terms, email [andrew@ix.dev](mailto:andrew@ix.dev). We'll scope something signed with credits. Enterprise/dedicated customers get this at onboarding.
