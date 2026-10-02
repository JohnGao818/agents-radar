# OpenClaw Ecosystem Digest 2026-10-02

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-10-02 03:49 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-10-02

## 1. Today's Overview

OpenClaw is operating at very high velocity: 500 issues and 500 PRs were touched in the last 24 hours, with 303 issues still open/active and 319 PRs open (181 PRs merged/closed, 197 issues closed). Activity is dominated by the *extended-stable*/2026.9.x lines, and the day's signal is mixed — a healthy flow of closed regressions alongside a cluster of P0 crash-loop, memory-leak, and disk-growth reports that are increasingly Windows- and large-fleet-centric. Overall project health reads as **high-throughput but stability-strained**: maintainers are shipping a security/reliability-focused LTS patch while a backlog of long-lived (Feb–Jul) defects still awaits product decisions. The clawsweeper triage bot is visibly gatekeeping with labels like `needs-product-decision`, `needs-security-review`, and `manual-only`, which is slowing some fixes to a crawl.

---

## 2. Releases

### v2026.8.34 — gateway-only `extended-stable` (LTS equivalent)
- **What it is:** A snapshot of OpenClaw from the end of August 2026, re-cut today with critical security updates plus reliability and performance fixes, and new model support.
- **Scope:** Gateway-only (no client/app bundles).
- **Breaking changes:** None explicitly declared in the release note.
- **Migration notes:** Positioned as the current LTS track — users on unstable 2026.9.x lines can treat this as the conservative fallback. Verify plugin compatibility before downgrading, given the number of 2026.9.x-only regressions currently in flight (see §5).
- **Links:** no release URL was supplied in the dataset.

> Note: The digest snapshot contains no separate patch release for the `2026.9.x` line today, despite several release-blocker bugs reported against 2026.9.5–9.7 (`impact:ux-release-blocker`). PR #163074 ("backport release-critical update and session repairs") indicates a `2026.9.8` release candidate is being stabilized.

---

## 3. Project Progress

**Closed today (selection of the 197 closed items):**
- **[#161953](https://github.com/openclaw/openclaw/issues/161953)** — Windows `sessions.create` deterministic failure ("publication owner is no longer current") from `win32 \\?\` SQLite path leaking into the creation guard. P0 release blocker, now closed.
- **[#161828](https://github.com/openclaw/openclaw/issues/161828)** — Windows `chat.send`/heartbeat `DataCloneError` via nested `input.request.env` Proxy. P0.
- **[#161654](https://github.com/openclaw/openclaw/issues/161654)** — Windows cron/agent `WorkerTaskError 'unavailable'` (DataCloneError), the top-level `readExactEntries` variant.
- **[#157067](https://github.com/openclaw/openclaw/issues/157067)** — Windows isolated cron passing an uncloneable `process.env` Proxy to the session-history worker.
- **[#85030](https://github.com/openclaw/openclaw/issues/85030)** — MCP tools not injected into `sessions_spawn` subagents (diamond-lobster rated, 6 👍).
- **[#112160](https://github.com/openclaw/openclaw/issues/112160)** — SSH sandbox not staging inbound media into an existing remote workspace.
- **[#141102](https://github.com/openclaw/openclaw/issues/141102)** — Collection-review jobs remaining enabled for ineligible rooted execution.
- **[#55694](https://github.com/openclaw/openclaw/issues/55694)** — Agent infinite tool-call retry loop flooding chats (Feishu).

**PRs advancing (open but active today):**
- **[PR #163195](https://github.com/openclaw/openclaw/pull/163195)** (P1) — Fix finished subagents failing to wake parents on overlapping registry writes; ready for maintainer look.
- **[PR #163074](https://github.com/openclaw/openclaw/pull/163074)** (P1) — Backport of release-critical update, Windows copy, performance, memory, and delegated-work fixes into the `2026.9.8` RC.
- **[PR #161105](https://github.com/openclaw/openclaw/pull/161105)** (P1) — Run scheduled work with current agent tools (cron tool-inventory drift).
- **[PR #163171](https://github.com/openclaw/openclaw/pull/163171)** — Retain Doctor repair for July provider aliases.
- **[PR #161421](https://github.com/openclaw/openclaw/pull/161421)** (P1, security-sensitive) — Fix paired clients timing out behind queued connection metadata.
- **[PR #163164](https://github.com/openclaw/openclaw/pull/163164)** / **[PR #163230](https://github.com/openclaw/openclaw/pull/163230)** / **[PR #163225](https://github.com/openclaw/openclaw/pull/163225)** — macOS sidebar filtering, Codex init-timeout diagnostics, and incognito actor session facts.

**Assessment:** The Windows `DataCloneError` family — the single largest coherent regression cluster — appears largely closed on the issue side today, which is a meaningful stability win for the 2026.9.x line.

---

## 4. Community Hot Topics

| Item | Comments | Signal |
|---|---|---|
| [#143524](https://github.com/openclaw/openclaw/issues/143524) — SQLite WAL grows to 1.4–2.8 GB despite `wal_autocheckpoint=1000`; blocks gateway startup (Windows) | 103 | **Hottest issue.** P0, gold-shrimp, release blocker. Unbounded WAL is a foundational storage-engine problem. |
| [#153257](https://github.com/openclaw/openclaw/issues/153257) — 2026.9.5 turned a stable environment into an 8-hour failure recovery session | 40 | Strong emotional signal; upgrade regret from the 2026.9.x line. |
| [#149538](https://github.com/openclaw/openclaw/issues/149538) — Gateway reaches ready but never serves; `/health` starves on a **632-agent fleet** | 23 | Enterprise-scale/scaling concern. |
| [#157067](https://github.com/openclaw/openclaw/issues/157067) — Windows cron env Proxy (now closed) | 21 | Windows cluster. |
| [#139710](https://github.com/openclaw/openclaw/issues/139710) — Plugin-generation supersede kills system-agent turn + planner fallback | 18 | Misleading `openclaw onboard` remedy surfaces a real DX problem. |
| [#148707](https://github.com/openclaw/openclaw/issues/148707) — Reply lost: "no active tool authority snapshot" on session displacement (2026.9.4 regression) | 17 | Message-loss, needs product decision. |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) — Unreaped hook/tool child processes → zombie accumulation | 16 | **Open since June 29.** |
| [#85030](https://github.com/openclaw/openclaw/issues/85030) — MCP tools not injected into subagents (closed today) | 16 | 6 👍. |
| [#114612](https://github.com/openclaw/openclaw/issues/114612) — `memory-core` SQLite tables have no retention policy, will fill disk | 15 | Long-running storage-growth theme. |
| [#159662](https://github.com/openclaw/openclaw/issues/159662) — `prepared-model-catalog.worker.js` leaks ~4–5 GB/h, provider-agnostic | 14 | Fresh P0 leak. |

**Underlying needs:** (1) **Storage-lifecycle discipline** — WAL, `memory_index_chunks`, `memory_embedding_cache` all grow without bound; users want retention/compaction defaults. (2) **Windows parity** — an outsized share of regressions are win32-only. (3) **Large-scale reliability** — the 632-agent fleet and large-session-store reports point to architectural limits in the state DB and event loop. (4) **Honest error surfaces** — multiple issues complain that user-facing errors misattribute cause (inference "unreachable" when it's a supersede bug).

---

## 5. Bugs & Stability

Ranked by severity (P0 first), with fix-PR presence where known:

**P0 / crash-loop / release blockers**
1. **[#143524](https://github.com/openclaw/openclaw/issues/143524)** — SQLite WAL unbounded growth, gateway startup blocked (Windows). *No fix PR.*
2. **[#149538](https://github.com/openclaw/openclaw/issues/149538)** — Gateway ready but never serves; event loop starved; RSS climbs (632-agent fleet). *Needs info.*
3. **[#159662](https://github.com/openclaw/openclaw/issues/159662)** — `prepared-model-catalog.worker.js` ~4–5 GB/h leak. *No fix PR.* Related: **[#160522](https://github.com/openclaw/openclaw/issues/160522)** (1.15 GB despite 512 MB cap).
4. **[#160521](https://github.com/openclaw/openclaw/issues/160521)** — Gateway crash: read-admission seal → unhandled rejection in `reconcileActive`. *Needs live repro.*
5. **[#158239](https://github.com/openclaw/openclaw/issues/158239)** — Gateway fails to start on kernels < 5.6 (no `openat2`, JS fs-safe fallback). *No fix PR.*
6. **[#160386](https://github.com/openclaw/openclaw/issues/160386)** — 2026.9.6 severe SQLite I/O pressure, WebUI RPC timeouts, `STATE_DATABASE_READ_ADMISSION_INVALIDATED` on large stores.
7. **[#155859](https://github.com/openclaw/openclaw/issues/155859)** — Startup wall-time scales with plugin count; discord/codex/weixin dominate 120 s budget.
8. **[#115642](https://github.com/openclaw/openclaw/issues/115642)** — Billing cooldown outlives provider outage on subscription auth (~5 h lockout).
9. **[#115256](https://github.com/openclaw/openclaw/issues/115256)** — Desktop app boot-loops the gateway; `doctor` fix is reverted by the app.

**P1 / regressions**
- **[#97616](https://github.com/openclaw/openclaw/issues/97616)** — Zombie child-process leak (Jun 29, still open).
- **[#84037](https://github.com/openclaw/openclaw/issues/84037)** — Codex app-server steady-state CPU/helper overhead.
- **[#114234](https://github.com/openclaw/openclaw/issues/114234)** — Usage-cost refresh lock unreleasable after PID-reusing restart (containers).
- **[#114211](https://github.com/openclaw/openclaw/issues/114211)** — Matrix room agents loop on no-reply output / stale replay.
- **[#148707](https://github.com/openclaw/openclaw/issues/148707)** — Message loss on session displacement.
- **[#161976](https://github.com/openclaw/openclaw/issues/161976)** — WhatsApp DM replies fail at durable registry handoff post-restart.
- **[#157126](https://github.com/openclaw/openclaw/issues/157126)** — claude-cli MCP bridge inherits first-request scope; owner turns lose `operator.admin` (security).
- **[#91804](https://github.com/openclaw/openclaw/issues/91804)** — Internal reasoning leakage (privacy regression since 2026.6.5).

**Windows cluster (largely closed today):** [#161953](https://github.com/openclaw/openclaw/issues/161953), [#161828](https://github.com/openclaw/openclaw/issues/161828), [#161654](https://github.com/openclaw/openclaw/issues/161654), [#157067](https://github.com/openclaw/openclaw/issues/157067) — all closed; backport tracked in **[PR #163074](https://github.com/openclaw/openclaw/pull/163074)**.

**Fix-PR status:** Most open P0s have `clawsweeper:no-new-fix-pr`. PRs exist for `exec` approval replay ([#138396](https://github.com/openclaw/openclaw/pull/138396)), domain/IMAP routing ([#138120](https://github.com/openclaw/openclaw/pull/138120)), and Codex concurrency ([#138089](https://github.com/openclaw/openclaw/pull/138089)) — all marked `stale` and awaiting maintainer review.

---

## 6. Feature Requests & Roadmap Signals

| Request | Issue | Status / Prediction |
|---|---|---|
| **Denylist mode for `exec-approvals`** ("allow all except X") | [#6615](https://github.com/openclaw/openclaw/issues/6615) (8 👍, since Feb 1), [#71097](https://github.com/openclaw/openclaw/issues/71097) | Duplicate-tracked, `needs-security-review`. **Likely candidate for a security-focused minor** — low blast radius, clear ask, twice-filed. |
| **Audit log for agent memory changes** (append-only, tamper detection) | [#20935](https://github.com/openclaw/openclaw/issues/20935) | `needs-product-decision`. Pairs naturally with the `memory-core` retention bugs; **plausible next-cycle roadmap item** if the storage rework lands. |
| **Short-term recall retention / dreaming promotion** fixes | [#150635](https://github.com/openclaw/openclaw/issues/150635), [#121232](https://github.com/openclaw/openclaw/issues/121232) | Ranker/applier disagreement is a functional gap; strong signal for a memory-core overhaul. |
| **MCP tool exposure into subagents** | [#85030](https://github.com/openclaw/openclaw/issues/85030) (closed), [#114154](https://github.com/openclaw/openclaw/issues/114154) | Closed-then-residual; keep watching for regressions in `bundle-mcp`. |
| **Doctor/update hygiene** | [#138040](https://github.com/openclaw/openclaw/pull/138040), [#137944](https://github.com/openclaw/openclaw/pull/137944),

---

## Cross-Ecosystem Comparison

**Caveat:** Only the OpenClaw digest was successfully generated. Hermes Agent’s summary failed, so no Hermes issue/PR/release metrics are available. This report is therefore an OpenClaw-centric benchmark with a Hermes visibility gap; no Hermes numbers have been inferred.

---

## 1. Ecosystem Overview

The personal AI assistant / agent open-source ecosystem in late 2026 is shifting from “does it run?” to “does it run safely, cheaply, and at fleet scale?” OpenClaw shows a high-velocity core gateway project under stability strain: massive issue/PR throughput, an LTS-style backport process, and growing enterprise-scale concerns around storage lifecycle, Windows parity, memory leaks, and multi-agent authority. Hermes Agent data is unavailable, so cross-project comparison is limited, but the OpenClaw signals likely generalize: MCP/subagent orchestration, auditability, exec approvals, memory retention, and honest error surfaces are becoming table stakes. The ecosystem is maturing, but maintainer triage and release engineering are now visible bottlenecks.

---

## 2. Activity Comparison

| Project | Issues | PRs | Release Status | Health Score |
|---|---|---|---|---|
| **OpenClaw** | 500 touched in 24h; 303 open/active; 197 closed | 500 touched in 24h; 319 open; 181 merged/closed | **v2026.8.34** gateway-only `extended-stable` LTS patch; **2026.9.8 RC** backport in progress via PR #163074; no separate 2026.9.x patch today | No formal numeric score in source. Qualitative: **high-throughput, stability-strained**; mature release governance but elevated production risk |
| **Hermes Agent** | Summary generation failed; no data | Summary generation failed; no data | Unknown | Unknown |

**OpenClaw signal:** Activity is extremely high but bifurcated — healthy closure of Windows regression clusters, alongside unresolved P0 crash-loop, memory-leak, and disk-growth reports.

---

## 3. OpenClaw’s Position

**Advantages vs. available peer data:** OpenClaw is the clearest reference implementation in this dataset. It has a large community surface — 500 issues and 500 PRs touched in 24h, with a hot issue at 103 comments — and a mature release ladder: conservative `extended-stable` LTS plus fast-moving `2026.9.x` lines. It supports broad platform and integration coverage: Windows/macOS/Linux, SSH sandboxing, cron/scheduled agents, MCP, plugin generation, and IM bridges such as Feishu, Matrix, and WhatsApp.

**Technical approach differences:** OpenClaw is gateway-centric, with a gateway-only LTS artifact, SQLite WAL/state DB persistence, worker processes, plugin inventory drift fixes, MCP subagent injection, and a triage bot (`clawsweeper`) applying labels like `needs-product-decision`, `needs-security-review`, and `manual-only`. This is closer to an operations-grade assistant platform than a lightweight agent framework.

**Community size:** By the available data, OpenClaw is very large and highly active. However, without Hermes metrics, direct peer comparison is impossible. OpenClaw’s scale is also its stress point: a 632-agent fleet report, large-session SQLite pressure

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ Summary generation failed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*