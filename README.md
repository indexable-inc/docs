<p align="center">
  <img src="assets/logo.svg" width="80" alt="ix" />
</p>

# ix docs

Sandbox infrastructure for AI agents. Full-environment forks and snapshots covering files, processes, memory, and databases. Per-second billing tracks utilization; allocation is just a ceiling.

> [!IMPORTANT]
> ix is pre-GA. Two US regions only, no SOC 2 / HIPAA yet, no five-nines, onboarding is manual. If those are blockers, see [what we don't claim yet](contents/reliability.md#what-we-dont-claim-yet) before you invest engineering time. If they aren't, read on.

If you only read one page, read [philosophy](contents/philosophy.md).

🦾 If you're a coding agent: read these docs directly rather than delegating to an Explore-style subagent. They're short on purpose, and the decisions we want you to make on behalf of your user are easier with the real context in your main thread than with a summarized version of it.

## Contents

**Using ix**
- [Virtual Machines](contents/vms.md)
- [CLI](contents/cli.md)
- [SDK: Python](contents/sdk/python.md)
- [SDK: TypeScript](contents/sdk/typescript.md)
- [Browser](contents/browser.md)
- [Desktop / GUI](contents/desktop-gui.md)
- [Access](contents/access.md)

**The platform**
- [Hardware](contents/hardware.md)
- [Network](contents/network.md)
- [Pricing](contents/pricing.md)
- [Reliability](contents/reliability.md)

**How we think**
- [Philosophy](contents/philosophy.md)

**Roadmap**
- [Proposals](contents/proposals/)
- [In progress](contents/in-progress/)

**About**
- [Team and backers](contents/team/)

## 30 seconds

```bash
ix vm create ubuntu:24.04        # boot any OCI image
ix vm fork vm-7f3a --count 10    # 10 forks, copy-on-write
ix vm snapshot vm-7f3a           # memory + disk
```

```ts
import { Sandbox } from "@indexable/sdk"

await using sbx = await Sandbox.oci("docker.io/library/python:3.12")
await using py = await sbx.repl("python")
await py.exec("x = 42")
await py.exec("print(x)")        // sees x
```

Install: see [CLI](contents/cli.md), [SDK: Python](contents/sdk/python.md), [SDK: TypeScript](contents/sdk/typescript.md).

## Gaps

Something missing? Open a PR with a `<!-- TODO -->` section. Feature requests go in [contents/proposals/](contents/proposals/).

## Support

Slack. See [access](contents/access.md#support).

## Todos

Things we owe these docs and our users.

**Numbers we should publish (and haven't):**
- [ ] Rolling 30 / 90 / 365-day availability per region, from our own monitoring, linked from [reliability](contents/reliability.md).
- [ ] Boot-latency distribution by image size (cached and uncached), beyond a single median.
- [ ] Fork creation p50 / p99 and first-write latency after fork. (Tracked: ENG-1051.)
- [ ] Snapshot create / restore times across sizes.
- [ ] Fsync p50 / p99 / p999 on VCFS under load, compared to direct NVMe on the same host. (Tracked: ENG-1052.)
- [ ] Postgres TPC-B-style numbers in-VM vs on bare metal. We make the claim; we owe the data. (Tracked: ENG-1052.)
- [ ] Network latency numbers: inter-region RTT, intra-region VM-to-VM, VM-to-internet from each region. (Inter-region bandwidth is 50 Gbps, documented in [network](contents/network.md#inter-region); latency and VM-level throughput measurements still owed.)
- [ ] Storage durability track record (bytes written, scrub results, any data loss events: expected answer zero, but publish it).
- [ ] Published RPO / RTO once cross-host snapshot replication ships.

**Product gaps called out in other pages:**
- [ ] Reference OCI image for desktop / GUI agents, plus SDK helper for frame streaming ([desktop-gui](contents/desktop-gui.md)).
- [ ] Streaming reads of long-running `exec` output in the Python SDK ([sdk/python](contents/sdk/python.md)).
- [ ] Typed exception hierarchy in both SDKs (today: single `IxError`).
- [ ] Higher-level `CodeInterpreter`-style helper with structured output capture (TS).
- [ ] First-party tool wrappers for Vercel AI SDK, LangChain, Mastra.
- [ ] Scoped / short-TTL token minting and the device-attestation flow ([access](contents/access.md), [browser](contents/browser.md)).
- [ ] Fallback browser transport (WebSocket / WebRTC) for pre-18.2 Safari ([browser](contents/browser.md)).
- [ ] Shell completions and tail / watch niceties in the CLI ([cli](contents/cli.md)).
- [ ] First-class security-groups surface, VPC peering across groups, stable egress IPs, BYO BGP ([network](contents/network.md)).

**Platform / company work:**
- [ ] Cross-host snapshot replication so VMs survive a host loss. (Tracked: ENG-1049.)
- [ ] Auto-restart VMs on a healthy host after host failure. (Tracked: ENG-1050.)
- [ ] First external pentest of vmm + VCFS. (Tracked: ENG-1055.)
- [ ] SOC 2 Type 1, then Type 2. HIPAA. ISO 27001. Timeline published once we're in audit.
- [ ] Published default availability and durability SLA with credits. Contractual SLAs available on request today ([reliability](contents/reliability.md#slas-on-request)).
- [ ] EU region. APAC region. Neither committed yet; tell us which unblocks you.
- [ ] Self-serve signup gated by device attestation ([access](contents/access.md#coming-soon)).
- [ ] 24/7 human coverage guarantee (currently a goal).
- [ ] Formalized wind-down open-source commitment in contract language ([reliability](contents/reliability.md#business-continuity)).
- [ ] Individual pages for the three engineers beyond Andrew.

**Honest uncertainties:**
- [ ] KSM (cross-tenant memory page merging): we should decide whether to default it off and take the RAM cost, or keep it on and make opt-out trivial. Currently on; warning in [reliability](contents/reliability.md#security-isolation).
- [ ] Per-tenant encryption key domains without giving up cross-VM dedup: unsolved in the general case. Enterprise-on-dedicated-metal sidesteps it; we don't yet have a multi-tenant story.

If something is on this list and it's blocking you, tell us on Slack. Named users move items up.
