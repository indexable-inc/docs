# Pricing

Per-second billing on actual resource use. No reserved-capacity charges.

> [!NOTE]
> Leased bare metal with no hyperscaler underneath. Details in [hardware](hardware.md).

## Rates

| Resource | Rate | ≈ monthly at 100% |
|---|---|---|
| vCPU | $0.000008/s | $20 |
| GiB RAM | $0.000003/s | $8 |
| TiB disk | $0.000002/s | $5 |

## How it works

Allocation is a ceiling. Billing tracks utilization. A 64-vCPU VM at 1% CPU costs the same as a 1-vCPU VM at 64%.

## Example

4 vCPU, 8 GiB RAM, 100 GiB disk, running at 20% CPU / 80% memory:

```
vCPU:   $0.000008/s x 0.8  = $0.000006/s
RAM:    $0.000003/s x 6.4  = $0.000019/s
disk:   $0.000002/s x 0.1  = $0.000000/s
                           ────────────
                             $0.000025/s  (~$65/mo)
```

## Storage

Block-level deduplication. Forking a 100 GiB VM does not cost 100 GiB. You pay for blocks that differ from the parent.

## Included

- Snapshots (free; they are the dedup mechanism)
- Forks (copy-on-write; pay for divergent blocks only)
- Network: IPv4 + IPv6, up to 25 Gbps, no per-byte fees

## Enterprise

If ix will be a meaningful part of your stack, we can deploy bare metal into your datacenter (or colo next to your existing footprint) and run ix on it. Pricing moves from per-second utilization to a fixed monthly, sized to your fleet. Custom SLAs and region layouts are on the table. Email [andrew@ix.dev](mailto:andrew@ix.dev).
