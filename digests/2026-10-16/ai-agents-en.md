# OpenClaw Ecosystem Digest 2026-10-16

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-10-16 02:55 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-10-16

*Source: github.com/openclaw/openclaw. Data caveat: issue/PR lists are truncated to the top 50 issues and top 30 PRs by comment count; PR comment counts were returned as `undefined`, so PR ranking below relies on labels, scope, and recency rather than comment volume.*

---

## 1. Today's Overview

OpenClaw is in a high-throughput maintenance-and-refactor phase: 500 issues and 500 PRs updated in the last 24h, with 295 PRs merged/closed against 205 still open, and 93 issues closed against 407 open/active. Four releases landed in the window, headlined by a Gateway/SQLite performance push (v2026.10.10-beta.1) and an update-reliability fix set (v2026.10.5-beta.4), plus an `extended-stable`/LTS-equivalent snapshot (v2026.9.33). Activity is very high and merge throughput is healthy, but the open-issue tail is dominated by persistent P0 storage-and-memory pathologies (SQLite WAL growth, gateway RSS leaks, plugin-capture I/O) that are months old in some cases. The project also shows a clear internal refactor wave in the Control UI (Lit → Solid) and a cluster of security-boundary PRs on channel owner allowlists. Overall health: strong velocity, but stability debt concentrated in the data/IO layer and the Codex harness remains the main risk to release confidence.

---

## 2. Releases (4 new)

### v2026.10.10-beta.1
- **Theme:** Faster, steadier Gateway. Chat turns, session lists, startup, and idle gateways do substantially less SQLite and main-thread work; more database work moved onto worker threads so busy hosts and large agent fleets stay responsive.
- **Refs:** #167965, #168002, #168093, and related (release text truncated).
- **Breaking changes:** None stated in the provided notes.
- **Migration notes:** Beta channel; performance-only behavior changes, no config migration described.

### v2026.10.5-beta.4
- **Theme:** Updates finish more reliably.
  - macOS updates no longer time out on aliased temporary directories.
  - systemd user installs reclaim abandoned runtimes.
  - pacman and FreeBSD package installs defer to the system package manager.
  - Snapshot failures are identified before proceeding (text truncated).
- **Breaking changes:** None stated.

### v2026.10.4
- **Theme:** Gateway lifecycle robustness.
  - Gateway keeps running after computer sleep or system-clock jumps, instead of restarting because its ownership heartbeat looked stale (**#170790**, thanks @AnvinaLI, @sgh6688, @waynegault, @RomneyDa).
  - Gateway shutdown and restart no longer hang (text truncated).
- **Breaking changes:** None stated.

### v2026.9.33 (`extended-stable`)
- **Theme:** Gateway-only `extended-stable` release, described as the current LTS equivalent: end-of-September 2026 code plus critical security updates, reliability/performance fixes, and new model support.
- **Migration notes:** Recommended reference point for conservative production deployments; not a feature release.

---

## 3. Project Progress

**Throughput:** 295 PRs merged/closed in 24h (205 open). 93 issues closed.

Visible closed PRs in the sample:
- [#173654](https://github.com/openclaw/openclaw/pull/173654) — **macOS:** save downloads instead of displaying ZIP/archive bytes in the dashboard and conversation window.
- [#162828](https://github.com/openclaw/openclaw/pull/162828) — **OpenAI device-code OAuth:** move the 15-minute deadline onto a monotonic clock so it can't hang or fail spuriously on wall-clock changes.
- [#164113](https://github.com/openclaw/openclaw/issues/164113) — **Updater/LXC:** FICLONE `EPERM` inside unprivileged Proxmox LXC (seccomp-blocked ioctl) resolved.
- [#84037](https://github.com/openclaw/openclaw/issues/84037) — **Codex app-server:** steady-state CPU and helper-process overhead improved/closed.
- [#71058](https://github.com/openclaw/openclaw/issues/71058) — **MS Teams:** multi-bot request closed.
- [#121617](https://github.com/openclaw/openclaw/issues/121617) — **Compaction:** "Already compacted" misclassification on fixed context overhead closed.
- [#77298](https://github.com/openclaw/openclaw/issues/77298) — **Cron:** `consecutiveErrors` inflated by gateway-restart interruptions closed.

**Active workstreams visible in open PRs:**
- **Control UI migration (Lit → Solid):** [#173664](https://github.com/openclaw/openclaw/pull/173664), [#173630](https://github.com/openclaw/openclaw/pull/173630), [#173629](https://github.com/openclaw/openclaw/pull/173629), [#173627](https://github.com/openclaw/openclaw/pull/173627), [#173337](https://github.com/openclaw/openclaw/pull/173337) — separating presentation contracts, removing redundant adapters.
- **Gateway/DB performance micro-optimizations:** [#173677](https://github.com/openclaw/openclaw/pull/173677) (skip redundant transcript hydration validation), [#173674](https://github.com/openclaw/openclaw/pull/173674) (skip deep-freezing worker receipts), [#173678](https://github.com/openclaw/openclaw/pull/173678) (avoid redundant subagent restore reads).
- **PostgreSQL engine support for agent DBs:** [#173462](https://github.com/openclaw/openclaw/pull/173462) — open agent/session databases through the selected engine (XL, security-sensitive).
- **Security boundary fixes:** [#172424](https://github.com/openclaw/openclaw/pull/172424) (Slack `slack:user:<id>` owners honored for exec approvals), [#172385](https://github.com/openclaw/openclaw/pull/172385) (same for Discord voice + exec approvals).
- **Update robustness:** [#173593](https://github.com/openclaw/openclaw/pull/173593) (don't report success as failure when a channel leaves `/readyz` at 503), [#173569](https://github.com/openclaw/openclaw/pull/173569) (retry transient Git download failures).
- **Agent correctness:** [#170534](https://github.com/openclaw/openclaw/pull/170534) (honor exact `NO_REPLY`, stop fabricated turn-ending replies), [#173580](https://github.com/openclaw/openclaw/pull/173580) (Codex next-turn stall after Stop during handoff), [#163138](https://github.com/openclaw/openclaw/pull/163138) (monotonic clock for `ask_user` expiry).

---

## 4. Community Hot Topics

**Most-commented issues:**

| Issue | Comments | Signal |
|---|---|---|
| [#143524](https://github.com/openclaw/openclaw/issues/143524) — SQLite WAL grows to 1.4–2.8 GB/day on Windows, blocks gateway startup | 128 | Highest-engagement item; P0, message-loss + crash-loop labels, release-blocker |
| [#91588](https://github.com/openclaw/openclaw/issues/91588) — Gateway memory leak: 350 MB → 15.5 GB RSS over days, OOM crashes | 40 | Long-running P0 (opened June 2026), `maturity:stable` |
| [#160959](https://github.com/openclaw/openclaw/issues/160959) — Gateway blocks for minutes capturing large external plugins (2026.9.6 regression) | 25 | P0 regression from plugin generation capture |
| [#148707](https://github.com/openclaw/openclaw/issues/148707) — Reply lost with "no active tool authority snapshot" when a second run displaces an in-flight turn | 20 | P1 session-state + message-loss regression |
| [#87744](https://github.com/openclaw/openclaw/issues/87744) — Codex-backed Telegram turns never reach `turn/completed` | 18 | P2, 4 👍, reliability regression |
| [#164294](https://github.com/openclaw/openclaw/issues/164294) — Gateway state DB WAL checkpoint never completes (pinned by in-process reader) | 18 | Directly relevant to the new WAL/worker-thread release theme |
| [#157989](https://github.com/openclaw/openclaw/issues/157989) — Plugin capture rewrites ~1.1–1.4 GB per CLI command, ~6.5 GB per Gateway start (SSD wear) | 18 | P1, severe hardware-wear report |
| [#68596](https://github.com/openclaw/openclaw/issues/68596) — Configurable streaming watchdog timeout | 17 (8 👍) | Most-upvoted request in sample |

**Hot PRs (by scope/risk rather than comment count):**
- [#170534](https://github.com/openclaw/openclaw/pull/170534) — honor exact `NO_REPLY`; fixes fabricated/forced replies after deliberate silence (XL, security-sensitive, ready for maintainer look).
- [#173668](https://github.com/openclaw/openclaw/pull/173668) — admit Factory session reads through repository-scoped GitHub App tokens (XL, docs + web UI + gateway + agents).
- [#173462](https://github.com/openclaw/openclaw/pull/173462) — open agent databases through the selected engine (PostgreSQL), XL, auth-provider risk.
- [#160364](https://github.com/openclaw/openclaw/pull/160364) — logging redaction: preserve non-secret env references, add exemption list and notification (security-review-required).

**Underlying needs:** durable, non-degrading SQLite/WAL behavior under real-world Windows and fleet workloads; bounded plugin-loading I/O and disk churn; guarantees that a turn's reply is either delivered or explicitly retried; and channel-owner authorization that works with canonical ID forms. The comment volume on storage issues suggests many operators are hitting these in production, not lab conditions.

---

## 5. Bugs & Stability

**P0 / release-blocker severity**
- [#143524](https://github.com/openclaw/openclaw/issues/143524) — Agent SQLite WAL unbounded growth (up to 2.8 GB), blocks gateway startup (Windows, 2026.9.2/9.3). No new fix PR (`clawsweeper:no-new-fix-pr`), needs maintainer review. **Related to today's worker-thread SQLite release work.**
- [#91588](https://github.com/openclaw/openclaw/issues/91588) — Gateway RSS leak to 15.5 GB → OOM loop. Open since June 2026, 40 comments, no fix PR flagged.
- [#160959](https://github.com/openclaw/openclaw/issues/160959) — Event loop blocked for minutes capturing large external plugins since 2026.9.6. Source repro available, no fix PR.
- [#89278](https://github.com/openclaw/openclaw/issues/89278) — Codex OAuth refresh succeeds but cron/heartbeat fail on a 10s auth-refresh timeout (linked PR open).
- [#70903](https://github.com/openclaw/openclaw/issues/70903) — File-based provider `disabledUntil` cooldown blocks users for hours after billing recovery; P0, `stale`.
- [#152275](https://github.com/openclaw/opencl

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — Personal AI Assistant / Agent OSS Ecosystem
**Digest date: 2026-10-16 | Projects in scope: OpenClaw, Hermes Agent**

> **Data basis & confidence.** This report is built on the 2026-10-16 community digests. **Only OpenClaw returned a usable digest; Hermes Agent's summary generation failed and contributes no data points.** All Hermes cells are marked `n/a` rather than estimated — no interpolation has been performed. OpenClaw's own digests are also structurally truncated (top 50 issues / top 30 PRs by comment count; PR comment counts returned `undefined`), so figures below are *24-hour activity counts*, not repository totals. Cross-project claims are therefore directional, not measured.
>
> The following raw OpenClaw sections were incomplete in the source and are treated as partial: the issue-list cut-off at #152275, and truncated release notes for v2026.10.5-beta.4 and v2026.10.4.

---

## 1. Ecosystem Overview

For the 2026-10-16 window the ecosystem is legible through exactly one project, and that project — OpenClaw — is in a high-throughput maintenance-and-refactor phase rather than a feature-expansion phase: 500 issues and 500 PRs touched in 24 hours, 295 PRs merged or closed, four releases shipped in a single day across beta, stable, and LTS-equivalent channels. The dominant engineering pressure is not model capability but **runtime durability**: SQLite WAL growth, gateway RSS leaks, plugin-capture I/O, and sleep/clock-jump resilience are the highest-engagement items in the community, several of them months old and still P0. This suggests the category has crossed from "can an agent do the task" into "can an agent run unattended for weeks on an operator's own hardware without degrading" — an infrastructure maturity problem. The one clear absence in this dataset is any visibility into Hermes Agent, so ecosystem-level statements about competitive balance are provisional and should be re-run once Hermes telemetry is recovered.

---

## 2. Activity Comparison

Health score method (OpenClaw only): mean of six 0–10 sub-scores — velocity, backlog balance, release cadence/channel discipline, stability debt, security posture, update/install robustness. Weights are equal; this is a transparent heuristic, not a benchmarked index.

| Metric | OpenClaw | Hermes Agent |
|---|---|---|
| Digest status | Complete (with source truncation) | **Generation failed** |
| Issues updated (24h) | 500 | n/a |
| Issues closed (24h) | 93 | n/a |
| Open / active issues | 407 | n/a |
| Issue close rate (24h) | 18.6% | n/a |
| PRs updated (24h) | 500 | n/a |
| PRs merged / closed (24h) | 295 | n/a |
| PRs open | 205 | n/a |
| PR merge share of touched | 59.0% | n/a |
| Releases in window | 4 | n/a |
| Release channel mix | 2× beta, 1× stable, 1× `extended-stable` (LTS-equivalent) | n/a |
| Most-commented single item | #143524, 128 comments | n/a |
| **Health score** | **6.7 / 10** — velocity 9, backlog balance 4, release cadence 9, stability debt 3, security posture 7, update robustness 8 | **Not scored — insufficient data** |

**Reading the score.** OpenClaw's 6.7 is a split profile: top-decile throughput and release discipline against a 3/10 stability-debt grade and a 4/10 backlog balance (issues closed at roughly one-fifth the rate they accumulate). The gap between 59% PR merge share and 18.6% issue close rate is the single most diagnostic number in the dataset — code is landing faster than defects are being retired.

---

## 3. OpenClaw's Position

**Advantages (evidenced).**
- **Throughput at a scale few OSS projects sustain.** 295 PRs merged/closed in 24h implies a deep, parallelized contributor base, not a solo maintainer. Four releases in one window, including a distinct LTS-equivalent channel, is release-engineering behavior typical of projects with a real user fleet.
- **Explicit stability-tiering.** `extended-stable` (v2026.9.33), `maturity:stable` labels, and a documented "current LTS equivalent" give conservative production operators a safe pin. This is a differentiator: many assistant projects ship only a rolling release.
- **Breadth of operator surface.** Fixes in one window touch macOS packaging, systemd user installs, pacman, FreeBSD, and unprivileged Proxmox LXC. That distribution footprint indicates self-hosted deployment on real heterogeneous infrastructure — the opposite of a cloud-only posture.
- **Security treated as a boundary problem, not a checkbox.** Channel-owner allowlist work (Slack `slack:user:<id>`, Discord voice exec approvals), logging redaction with exemption lists, and "security-review-required" labels on XL PRs indicate authz at the channel/adapter edge is an active design axis.

**Technical approach differences.** OpenClaw is architecturally a **gateway-centered, local-first system**: a long-lived Gateway process owns session state and chat turns; SQLite (with PostgreSQL engine support in flight, #173462) is the persistence layer; work is being moved off the main thread onto worker threads (#167965, #168002, #168093); external plugins are captured and versioned locally; channel adapters (Telegram, Slack, Discord, MS Teams) are ingestion surfaces; and a Codex-based harness drives agent execution. The Control UI is mid-migration from Lit to Solid, with presentation contracts being separated from adapters — a sign of front-end/back-end decoupling pressure from scale. This is a **monolithic gateway with pluggable edges**, in contrast to more composable or cloud-managed designs.

**Community size.** The strongest available proxy: the top issue carries 128 comments, with a long tail at 40/25/20/18 comments, and 500 issues were touched in a single day. That is a substantial, production-grade operator community filing reproducible defects from real fleets — not a lab or demo audience. **Peer comparison is not possible in this dataset**; Hermes supplied no issue counts, comment volumes, or contributor signals, so any claim that OpenClaw's community is larger or smaller would be unsupported.

---

## 4. Shared Technical Focus Areas

Because only one project reported, these are stated as **emergent category requirements** with the OpenClaw evidence attached. Cross-project confirmation is pending Hermes re-collection.

| Requirement | Project(s) with evidence | Specific need |
|---|---|---|
| Durable, bounded local storage | OpenClaw (#143524, #164294, #91588) | WAL growth to 2.8 GB/day on Windows; checkpoint starvation from in-process readers; RSS growth 350 MB → 15.5 GB |
| Bounded plugin / generated-code I/O | OpenClaw (#160959, #157989) | Minutes-long event-loop blocks; ~1.1–1.4 GB rewritten per CLI command, ~6.5 GB per gateway start (SSD wear) |
| Exactly-once turn delivery | OpenClaw (#170534, #148707, #87744) | No fabricated replies after deliberate silence; no reply loss on displaced in-flight turns; reliable `turn/completed` |
| Time-source correctness | OpenClaw (#162828, #163138, #170790, #77298) | Monotonic clocks for OAuth deadlines, `ask_user` expiry, ownership heartbeats, and cron error counts |
| Long-lived process hygiene | OpenClaw (#170790, #91588) | Survival across sleep and clock jumps; no shutdown/restart hangs; no OOM crash-loops |
| Canonicalized authorization | OpenClaw (#172424, #172385) | Owner allowlists honored under canonical ID forms before exec approval |
| Update & install reliability | OpenClaw (v2026.10.5-beta.4, #173593, #173569) | Distro-native package managers, alias-safe temp dirs, runtime reclamation, retry on transient Git failures |
| Engine abstraction | OpenClaw (#173462) | Selecting a persistence engine (PostgreSQL) without changing agent/session semantics |

---

## 5. Differentiation Analysis

**Feature focus (OpenClaw).** Operational resilience and multi-channel ingestion, with the agent-execution layer (Codex harness) and local plugin capture as secondary surfaces. The roadmap in this window is dominated by *making the existing system not degrade*, not by adding capabilities.

**Target users (OpenClaw).** Self-hosting operators and small-to-medium fleets: people running gateways under systemd, in Proxmox LXCs, on Windows desktops, and on FreeBSD/pacman distros. The LTS channel and the SSD-wear and message-loss reports confirm users treat this as **infrastructure they own in production**, not a toy.

**Technical architecture (OpenClaw).** Single long-lived gateway; SQLite-primary persistence migrating toward pluggable engines; worker-thread offload; adapter-based channels; locally captured, versioned plugins; a Lit→Solid UI migration. The architecture optimizes for *one operator, many channels, one durable session store*.

**Hermes Agent.** No differentiation analysis is possible from this dataset — the digest failed, so feature focus, target users, and architecture are all unknown. Given the ecosystem's trajectory, the collection template for Hermes should at minimum return: issue/PR activity counts, release cadence and channel structure, persistence and scheduling architecture, channel adapters, model-provider routing, and security/allowlist posture. Until that lands, Hermes should be treated as **unclassified**, not as a laggard.

---

## 6. Community Momentum & Maturity

**Activity tiers (assigned from available evidence).**

| Tier | Definition | Projects |
|---|---|---|
| Tier 1 — very high throughput | ≥100 PRs merged/closed per 24h, multiple releases in window | **OpenClaw** (295 PRs, 4 releases) |
| Tier 2 — active but smaller | measurable weekly cadence | *

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ Summary generation failed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*