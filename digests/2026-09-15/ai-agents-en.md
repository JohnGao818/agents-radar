# OpenClaw Ecosystem Digest 2026-09-15

> Issues: 462 | PRs: 500 | Projects covered: 2 | Generated: 2026-09-15 03:09 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-09-15

*Source: github.com/openclaw/openclaw · Data window: last 24h*

---

## 1. Today's Overview

OpenClaw is in an extremely high-activity maintenance phase: **462 issues** and **500 pull requests** were updated in the last 24 hours, with no new release cut. The issue tracker shows a heavy triage/cleanup wave — 168 issues closed (many stale items from April–May) against 294 still-active — while PR throughput remains strong at 228 merged/closed versus 272 open. The dominant engineering theme today is **event-loop and CPU performance work on the Gateway**, led by maintainer `steipete` with a cluster of PRs moving SQLite-backed reads/writes (session lists, usage pricing, cron saves) off the main thread. In parallel, a **P0 update/upgrade reliability cluster around 2026.9.3/2026.9.4** continues to generate user reports across Windows, macOS, and Linux. Overall health reads as *responsive but strained*: maintainers are actively shipping fixes and closing backlog, but core stability (session state, message delivery, update handoff) remains the top open risk.

---

## 2. Releases

**No new releases in the last 24 hours.** Latest stable line referenced in reports is **2026.9.3 / 2026.9.4**, which is itself the subject of an active P0 reliability tracking issue ([#145252](https://github.com/openclaw/openclaw/issues/145252)). Users on `latest`/`beta` both report pointing at 2026.9.4. No migration notes applicable today.

---

## 3. Project Progress

**Note on data:** PR-level comment counts were unavailable (`undefined`) for all top-30 PRs, so ranking below is by maintainer status, labels, and merge state rather than comment volume.

### Merged / Closed PRs (selected)
- **[#148662 CLOSED]** `test: share and strengthen main-thread SQLite observations` — consolidates six duplicated SQLite spies and tightens async-config coverage so cached statements executing on the main thread can't escape detection. ([link](https://github.com/openclaw/openclaw/pull/148662))

### Fast-moving open PRs (maintainer-owned, performance cluster)
- **[#148713]** `fix(gateway): reduce CPU work in session lists and searches` — caches repeated plugin-metadata resolution for large session projections. ([link](https://github.com/openclaw/openclaw/pull/148713))
- **[#148712]** `improve: reduce CPU spent assembling session listings` — stops rebuilding physical-store/reader keys per row. ([link](https://github.com/openclaw/openclaw/pull/148712))
- **[#148709]** `refactor: keep usage pricing SQLite reads off the Gateway thread` ([link](https://github.com/openclaw/openclaw/pull/148709))
- **[#148594]** `improve(cron): move data-only saves off the caller thread` — removes blocking SQLite writes from Telegram target writeback and unguarded service saves. ([link](https://github.com/openclaw/openclaw/pull/148594))
- **[#148706]** `fix(ui): avoid session reloads when Activity recaps update` — fixes repeated chat/sidebar full-list reloads. ([link](https://github.com/openclaw/openclaw/pull/148706))

### Notable fix PRs advancing (ready for maintainer look / needs proof)
- **[#148656]** `fix(plugins): load a plugin-owned CLI backend whose provider reuses a core model api` (P1, Closes #148584). ([link](https://github.com/openclaw/openclaw/pull/148656))
- **[#148612]** `fix(exec): node approvals no longer reject routed agent sessions` (P1, security-boundary). ([link](https://github.com/openclaw/openclaw/pull/148612))
- **[#148311]** `fix(mcp): release runtime capacity slot on cleanup failure` (P1) — closes a leak of session MCP runtime slots that exhausted the 256-runtime ceiling after ~20h. ([link](https://github.com/openclaw/openclaw/pull/148311))
- **[#117151]** `fix: stop surviving Linux subprocesses after agent cancellation` (P1, security/availability). ([link](https://github.com/openclaw/openclaw/pull/117151))
- **[#144819]** `fix(update): report configuration failures during repair` ([link](https://github.com/openclaw/openclaw/pull/144819))
- **[#145534]** `fix(channels): reject blank integer channel add options` ([link](https://github.com/openclaw/openclaw/pull/145534))
- **[#134404]** `fix(gateway): bound unattributable proxy warnings per source` ([link](https://github.com/openclaw/openclaw/pull/134404))

**Assessment:** A concentrated, high-leverage performance pass is in flight. If the SQLite-off-thread cluster lands, it should materially reduce Gateway CPU and event-loop stalls — directly relevant to the open P1 [#119720](https://github.com/openclaw/openclaw/issues/119720).

---

## 4. Community Hot Topics

Ranked by comment count (reactions noted where available):

| Rank | Item | Status | Comments | Why it matters |
|---|---|---|---|---|
| 1 | [#25592 — Text between tool calls leaks to messaging channels](https://github.com/openclaw/openclaw/issues/25592) | OPEN, P1, 🦞 diamond lobster | 40 | Internal narration/error text is routed to Slack/iMessage as user-visible messages. Security + session-state tagged; linked PR open. |
| 2 | [#97616 — Unreaped hook/tool child processes (zombie accumulation)](https://github.com/openclaw/openclaw/issues/97616) | OPEN, P1 | 30 | Zombie processes accumulate under the main daemon causing runtime degradation. |
| 3 | [#88312 — Codex app-server turn-completion stall regression](https://github.com/openclaw/openclaw/issues/88312) | **CLOSED**, P1, 🐚 platinum hermit | 22 (👍5) | Regression of #84076; highest reaction count in the set — indicates strong user demand for a durable fix. |
| 4 | [#119720 — Synchronous persistence/transcript maintenance blocks Gateway event loop](https://github.com/openclaw/openclaw/issues/119720) | OPEN, P1, 🦞 diamond lobster | 20 | The exact problem the current maintainer PR cluster targets. |
| 5 | [#48788 — Centralized filename encoding utility (multi-encoding Content-Disposition)](https://github.com/openclaw/openclaw/issues/48788) | OPEN, P3, stale, 🌊 off-meta tidepool | 20 | International (Feishu/Shift-JIS/EUC-KR/GB18030) filename correctness; affects all channel adapters. |
| 6 | [#102175 — Embedded prompt cache breaks across room-event/policy/Responses boundaries](https://github.com/openclaw/openclaw/issues/102175) | OPEN, P2, security review | 19 | Long-lived sessions lose provider prompt-cache reuse; cost/latency impact. |
| 7 | [#144911 — MCP server init timeout crashes the Gateway](https://github.com/openclaw/openclaw/issues/144911) | OPEN, P1, 🦞 diamond lobster | 16 | Unhandled rejection in child-cleanup path takes down the whole Gateway. |

**Underlying needs analysis:** The top threads cluster around three unmet user expectations — (1) **isolation between agent internals and user-facing channels**, (2) **process/resource hygiene** (zombies, MCP slots, subprocess survival), and (3) **session/message integrity under concurrency** (drops during active reply runs, prompt-cache breaks). The high reaction count on the closed Codex stall regression (#88312, 👍5) signals users want *confirmed, permanent* fixes for inference stalls, not just closure.

---

## 5. Bugs & Stability

### P0 / Release-blocking
- **[#146860 OPEN]** Windows managed update handoff cannot obtain process-start identity under `LogonType: InteractiveToken` → update stalls in `activating`, settles `abandoned`. (10 comments) [link](https://github.com/openclaw/openclaw/issues/146860)
- **[#145252 OPEN]** Tracking index: 2026.9.3 / 2026.9.4 update, upgrade and recovery reliability. [link](https://github.com/openclaw/openclaw/issues/145252)
- **[#145510 OPEN]** Update failure: `runtime-verification-failed` (2026.9.3 → 2026.9.4, win32/x64); needs-info. [link](https://github.com/openclaw/openclaw/issues/145510)
- **[#123326 OPEN]** Explicit multi-agent Codex migration crash-loops Gateway startup while detecting legacy sidecars. [link](https://github.com/openclaw/openclaw/issues/123326)
- **[#125333 OPEN]** `totalTokens` inflation still reproduces (fix only covered `api === "cli"`; memory-flush path is unguarded). [link](https://github.com/openclaw/openclaw/issues/125333)
- **[#148614 CLOSED / #145072 CLOSED]** Update failures now closed: Darwin `runtime-verification-failed`; macOS npm update `Package rollback launcher backup changed`. [[#148614]](https://github.com/openclaw/openclaw/issues/148614) [[#145072]](https://github.com/openclaw/openclaw/issues/145072)

### P1 / High severity (open)
- **#25592** internal text leaking to channels (security) — *linked PR open*.
- **#97616** zombie child-process accumulation — regression.
- **#119720** event loop blocked by synchronous persistence — *maintainer PR cluster in flight*.
- **#144911** MCP init timeout → unhandled rejection crashes Gateway — labeled `queueable-fix`.
- **#139847** message dropped while a reply run is active (`no active tool authority snapshot`, regression in 2026.9.2) — `queueable-fix`. [link](https://github.com/openclaw/openclaw/issues/139847)
- **#145152** stuck-session recovery reports force-clear as abort, releases lane by session id (2026.7.1) — `queueable-fix`. [link](https://github.com/openclaw/openclaw/issues/145152)
- **#125570** Skill Workshop update overwrites live skill `description`, silently breaking skill routing (data loss). [link](https://github.com/openclaw/open

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — Personal AI Assistant / Agent OSS Ecosystem  
**Window: 2026-09-15 (last 24h)**

> **Data caveat:** The Hermes Agent digest failed to generate. This report therefore compares OpenClaw against Hermes only where data exists; Hermes fields are marked **N/A**. Quantitative findings are OpenClaw-centric. The OpenClaw health score below is a derived qualitative assessment, not a source-provided metric.

---

## 1. Ecosystem Overview

The 2026-09-15 window shows a mature agent/assistant ecosystem in **high-velocity maintenance mode**, not feature-expansion mode. OpenClaw alone processed **462 issues and 500 PRs in 24h**, with a heavy triage wave (168 issues closed) and strong merge throughput (228 PRs merged/closed). The dominant engineering themes are operational hardening: **Gateway event-loop/CPU performance, update/upgrade reliability, process/resource hygiene, channel isolation, and MCP lifecycle management**. Hermes Agent data is unavailable, so cross-project pattern confirmation is not possible; however, the visible OpenClaw signal is that agent platforms are increasingly judged on reliability, performance, upgrade safety, and security boundaries as much as model capability.

---

## 2. Activity Comparison

| Project

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ Summary generation failed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*