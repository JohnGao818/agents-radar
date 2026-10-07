# OpenClaw Ecosystem Digest 2026-10-07

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-10-07 04:02 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-10-07

## 1. Today's Overview

OpenClaw is operating at very high activity: **1,000 tracked items updated in the last 24 hours** (500 issues, 500 PRs), with **275 of those closed** (138 issues, 137 PRs) — an unusually strong close-out ratio that suggests maintainers are actively draining backlogs rather than accumulating them. No new release shipped today, leaving the most recent published line at **2026.9.6**, and several of the highest-comment issues are regressions reported against that 2026.9.x series. The dominant theme in today's data is **runtime resource exhaustion and state-database pressure**: unbounded worker-thread memory growth, zombie child-process accumulation, and SQLite lock/IO timeouts dominate the P0 list. At the same time, the PR queue skews heavily toward `steipete`-authored maintenance batches (perf, test pruning, refactors) plus a long tail of stale community fix PRs from early September still awaiting maintainer review.

**Health signal:** high throughput and good closure velocity, but a concerning cluster of **release-blocker-tagged (P0 / ux-release-blocker) regressions** that have persisted for 1–3 weeks without merged fixes. Stability investment, not feature velocity, appears to be the current bottleneck.

---

## 2. Releases

**None.** No new releases were published in the last 24 hours, and no release notes are available for this window.

**Context from in-flight issues:** Multiple update-path failures against the current stable line (**2026.9.4 → 2026.9.5 → 2026.9.6**) were active today, including [#154924](https://github.com/openclaw/openclaw/issues/154924) (`global-install-failed`), [#157319](https://github.com/openclaw/openclaw/issues/157319) (`state-migrated-no-rollback`, closed today), and [#154114](https://github.com/openclaw/openclaw/issues/154114) (candidate rehearsal rejects working model auth, closed today). Users on 2026.9.4/2026.9.5 should treat update verification as the highest-risk step until these paths stabilize.

---

## 3. Project Progress

**Closed/merged: 137 PRs and 138 issues in 24h.** Notable closures and their significance:

| Item | Type | What it resolves |
|---|---|---|
| [#157126](https://github.com/openclaw/openclaw/issues/157126) | Issue (security, P1) | claude-cli MCP bridge inherited the request scope of whichever gateway request lazily started it; after restart-recovery, owner turns lost `operator.admin`. Closed — security-scoped fix landed. |
| [#150132](https://github.com/openclaw/openclaw/issues/150132) | Issue (P1, message-loss) | `claude-cli` `--include-partial-messages` deltas metered against a frozen 8 MiB per-turn stdout cap, discarding final replies on long tool-heavy turns. Closed. |
| [#90213](https://github.com/openclaw/openclaw/issues/90213) | Issue (regression) | Legacy state migration warnings persisted after `openclaw doctor --fix`. Closed. |
| [#85334](https://github.com/openclaw/openclaw/issues/85334) | Issue (data-loss) | `doctor --fix` injected a `plugins.load.paths` entry pointing at bundled plugin dir, causing circular warnings. Closed. |
| [#94251](https://github.com/openclaw/openclaw/issues/94251) | Issue (P1) | Ollama remote provider streaming not consumed (`model_call:started` never progressed). Closed. |
| [#154114](https://github.com/openclaw/openclaw/issues/154114) | Issue (P0) | `openclaw update` rehearsal failing with "No usable, authenticated, tool-capable inference route" despite working auth. Closed (not-repro-on-main). |
| [#157319](https://github.com/openclaw/openclaw/issues/157319) | Issue (P0) | 2026.9.6 update verification failure + stale codex app-server records. Closed. |
| [#50126](https://github.com/openclaw/openclaw/issues/50126) | Issue (security/message-loss) | Inconsistent `message:sent` / `message_sent` hook coverage across outbound paths. Closed. |
| [#166434](https://github.com/openclaw/openclaw/pull/166434) | PR (perf) | Avoid catalog workers for native login rechecks — directly relevant to the worker-thread leak family. |
| [#166435](https://github.com/openclaw/openclaw/pull/166435) | PR (fix) | Avoid false `EPROCESSGROUP_CLEANUP_FAILED` cleanup errors after tooling exits. |

**New work opened today (2026-10-07, by `steipete` et al.):**
- [#166443](https://github.com/openclaw/openclaw/pull/166443) — preserve worktrees used by live sessions (prevents worktree removal breaking parent subprocess launches).
- [#166441](https://github.com/openclaw/openclaw/pull/166441) — reconcile root node workspaces and surface underlying node errors instead of `UNAVAILABLE`.
- [#166442](https://github.com/openclaw/openclaw/pull/166442) — Control UI: keep delegated subagents in the *running* panel while descendants are alive.
- [#166439](https://github.com/openclaw/openclaw/pull/166439) — batch test-reduction ("remove low-value tests, batch d001").
- [#166429](https://github.com/openclaw/openclaw/pull/166429) — reuse avatar thumbnails across repeat views (image-worker eviction fix).
- [#166440](https://github.com/openclaw/openclaw/pull/166440) — new tool to capture the Gateway host screen (security-boundary, needs proof).

**Directional read:** this cycle is dominated by hardening and maintenance work — process/worktree lifecycle correctness, catalog-worker consolidation, and UI state truthfulness — rather than new user-facing features.

---

## 4. Community Hot Topics

Ranked by comment count:

1. **[#159662](https://github.com/openclaw/openclaw/issues/159662) — 20 comments — Unbounded memory leak in `prepared-model-catalog.worker.js`** (OPEN, P0, crash-loop)
   Provider-agnostic, workload-independent monotonic RSS growth (~4–5 GB/h; 2.5 GB → 8–10 GB in 60–90 min) reproduced on cold reboot + provider bisect. The single most-discussed issue today. *Underlying need:* users need a reproducible, provider-independent memory bound on the worker layer; the "reproduced on cold reboot + provider bisect" framing pressures maintainers to treat this as architectural, not config-specific.

2. **[#97616](https://github.com/openclaw/openclaw/issues/97616) — 18 comments — Unreaped hook/tool child processes → zombie accumulation** (OPEN, P1, regression, crash-loop, message-loss)
   Zombies accumulate under the main `openclaw` process (`openclaw-hooks`, `bash`, `codex`), degrading runtime over time. *Need:* deterministic subprocess reaping and a watchdog for orphaned hook execution.

3. **[#79902](https://github.com/openclaw/openclaw/issues/79902) — 15 comments — Companion-friendly SQLite transcript/session seams** (OPEN, stale, feature)
   Advanced consumers want canonical runtime state access without scraping opaque blobs. *Need:* stable public data contracts over the database-first runtime introduced by #78595.

4. **[#43367](https://github.com/openclaw/openclaw/issues/43367) — 15 comments — Multi-agent orchestration instability** (OPEN, stale, P2, data-loss/message-loss/auth-provider)
   Concurrent `openclaw agents add` overwrites config; session-lock failures; detached child work. *Need:* concurrency-safe config mutation and session locking for parallel agent batches.

5. **[#127229](https://github.com/openclaw/openclaw/issues/127229) — 15 comments — Telegram watchdog falsely tombstones durable updates** (OPEN, P1, diamond lobster)
   Durably spooled Telegram DMs tombstoned before the transport tracker settles during context-overflow compaction. *Need:* ordering guarantees between watchdog and transport adoption.

6. **[#136183](https://github.com/openclaw/openclaw/issues/136183) — 14 comments — Command executor hangs spawning `ssh`** (OPEN, regression, P2)
   SIGTERM while waiting for server banner; regression since 2026.8.1, persists in 2026.8.2. *Need:* protocol-aware timeouts instead of blanket SIGTERM.

7. **[#96975](https://github.com/openclaw/openclaw/issues/96975) — 13 comments — Isolate subagent completion from parent context** (OPEN, feature/bug)
   Heavy subagent workloads inject long reports/tool output into the parent, inflating context. *Need:* status + child session link by default, opt-in full payload.

8. **[#83959](https://github.com/openclaw/openclaw/issues/83959) — 13 comments — Codex app-server startup retries exhaust before replacement ready** (OPEN, crash-loop)
   `codex app-server client is closed` on scheduled background turns.

9. **[#157126](https://github.com/openclaw/openclaw/issues/157126) — 12 comments — CLOSED** — claude-cli MCP bridge scope inheritance / `operator.admin` loss. Security-relevant; closed today.

10. **[#160386](https://github.com/openclaw/openclaw/issues/160386) — 11 comments — 2026.9.6 SQLite I/O pressure on large session stores** (OPEN, P0, release blocker)
    WebUI RPC timeouts + `STATE_DATABASE_READ_ADMISSION_INVALIDATED`.

**PR-side hot topics:**
- **[#102379](https://github.com/openclaw/openclaw/pull/102379)** — MS Teams mention/forward normalization (XL, P2, merge-risk: security-boundary, needs proof).
- **[#158903](https://github.com/openclaw/openclaw/pull/158903)** — require configured worker placement for sessions (enterprise opt-in policy, XL).
- **[#121932](https://github.com/openclaw/openclaw/pull/121932)** — Feishu: stop inbound mentions cascading into replies.
- **[#143329](https://github.com/openclaw/openclaw/pull/143329)** — macOS: keep Apple Event permission probes off the cooperative thread pool (paired node going dead).

**Underlying-need synthesis:** the community's hot list is overwhelmingly about **correctness under sustained load** — memory, child processes, session DB contention, and message delivery exactly-once semantics — rather than new capabilities.

---

## 5. Bugs & Stability

Ranked by severity. "Fix PR?" indicates a linked/open PR identified in today's data.

### P0 / Release-Blocker

| Issue | Summary | Age | Fix PR? |
|---|---|---|---|
| [#159662](https://github.com/openclaw/openclaw/issues/159662) | `prepared-model-catalog.worker.js` unbounded memory leak, ~4–5 GB/h, provider-agnostic | 10 days | Indirect: [#166434](https://github.com/openclaw/openclaw/pull/166434) reduces redundant catalog-worker prep, but does not close the leak |
| [#160386](https://github.com/openclaw/openclaw/issues/160386) | 2026.9.6 on large session stores → SQLite I/O pressure, WebUI RPC timeouts, `STATE_DATABASE_READ_ADMISSION_INVALIDATED` | 9 days | No |
| [#148307](https://github.com/openclaw/openclaw/issues/148307) | `database is locked` on 464 MB agent DB, zero freelist; reclamation 9–47 s vs 5 s busy timeout | 23 days | No |
| [#155191](https://github.com/openclaw/openclaw/issues/155191) | Native memory leak in 2026.9.5 — RSS +1 GiB/30 s while V8 heap flat | 16 days | No |
| [#152965](https://github.com/openclaw/openclaw/issues/152965) | Hot-reloading a

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — 2026-10-07

**Scope note:** This report is constrained by available data. OpenClaw has a full digest; **Hermes Agent’s summary generation failed**, so no quantitative or qualitative Hermes data can be verified here. Hermes rows are marked unavailable to avoid fabricated comparison.

---

## 1. Ecosystem Overview

The personal AI assistant / agent open-source landscape in late 2026 is shifting from “can it call a model?” to “can it stay reliable under sustained, multi-agent, long-session load?” OpenClaw’s data shows a mature, hyperactive project where the dominant work is runtime hardening: memory bounds, subprocess lifecycle, SQLite state contention, message-delivery guarantees, and security scoping. Feature velocity is present, but it is no longer the main constraint; stability engineering is. The missing Hermes Agent digest prevents a true two-project comparison, but OpenClaw’s digest alone is a strong signal that the ecosystem’s next competitive frontier is operational correctness.

---

## 2. Activity Comparison

| Project | Issues count | PR count | Release status | Health score / assessment |
|---|---:|---:|---|---|
| **OpenClaw** | 500 updated in 24h; 138 closed | 500 updated in 24h; 137 closed | No release in last 24h; latest published line **2026.9.6** | **6.5/10** analyst-derived: very high throughput and closure velocity, but elevated P0/release-blocker stability risk |
| **Hermes Agent** | Data unavailable | Data unavailable | Data unavailable | **Unknown** — digest generation failed |

**Notes:**  
- Counts are “updated in last 24h,” not total open backlog.  
- OpenClaw closed **275 tracked items in 24h** (138 issues + 137 PRs), which is unusually high for a single day.  
- The health score is an analyst estimate derived from digest signals, not a project-published metric.

---

## 3. OpenClaw’s Position

**Advantages vs. peers:** OpenClaw shows top-tier community throughput: **1,000 tracked items updated in 24h**, with **275 closures**. That implies a large contributor/reporter base and active maintainer drain of backlog. It also has strong maintainer-led maintenance batches, especially from `steipete`, targeting performance, test reduction, worktree lifecycle, and worker consolidation.

**Technical approach differences:** OpenClaw appears to be a full self-hosted agent runtime, not just a model wrapper. Its architecture includes a gateway/control UI, SQLite-backed session/state persistence, catalog workers, subprocess bridges (`claude-cli`, `codex app-server`), multi-channel integrations (Telegram, Feishu, MS Teams), subagent orchestration, and explicit security boundaries. This is closer to an “agent operating system” than a single-purpose assistant.

**Community size comparison:** Direct Hermes comparison is impossible from the supplied data. However, by raw activity, OpenClaw is in a very high tier for an open-source agent project. Its challenge is not attention; it is converting that attention into merged stability fixes and release confidence.

---

## 4. Shared Technical Focus Areas

With only OpenClaw data available, these are OpenClaw-led signals. Hermes cannot be confirmed as sharing them.

| Focus area | OpenClaw evidence | Emerging requirement |
|---|---|---|
| **Bounded resource lifecycle** | [#159662](https://github.com/openclaw/openclaw/issues/159662) worker memory leak ~4–5 GB/h; [#155191](https://github.com/openclaw/openclaw/issues/155191) native leak; [#97616](https://github.com/openclaw/openclaw/issues/97616) zombie child processes | Hard RSS caps, worker pooling, deterministic subprocess reaping, watchdog for orphaned hooks |
| **State DB contention / large session stores** | [#160386](https://github.com/openclaw/openclaw/issues/160386) SQLite I/O pressure, `STATE_DATABASE_READ_ADMISSION_INVALIDATED`; [#148307](https://github.com/openclaw/openclaw/issues/148307) `database is locked`; [#79902](https://github.com/openclaw/openclaw/issues/79902) stable transcript/session seams | WAL/busy-timeout tuning, freelist reclamation, compaction, public data contracts |
| **Message delivery exactly-once / ordering** | [#127229](https://github.com/openclaw/openclaw/issues/127229) Telegram watchdog tombstones durable updates; [#150132](https://github.com/openclaw/openclaw/issues/150132) stdout cap discards final replies; [#50126](https://github.com/open

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ Summary generation failed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*