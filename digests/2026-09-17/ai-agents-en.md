# OpenClaw Ecosystem Digest 2026-09-17

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-09-17 03:09 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-09-17

## 1. Today's Overview

OpenClaw remains in a high-velocity, high-churn state: 500 issues and 500 pull requests were updated in the last 24 hours, with 331 issues still open/active (169 closed) and 296 PRs open (204 merged or closed). No new releases shipped, so the entire day's work is concentrated on stabilizing the 2026.9.3 → 2026.9.4 upgrade path and the Gateway runtime. The dominant signal is a cluster of **P0/P1 Gateway stability defects** — memory leaks, crash-loops, zombie processes, and starvation on large agent fleets — several of which already have maintainer-authored fix PRs in review. On the positive side, maintainer throughput is strong (many `steipete`-authored fixes landed in the top PR set), and a number of long-standing bugs (#146265, #31331, #145929, #87407, #111985, #111578, #146719) were closed. Overall health: **active but strained**, with reliability of updates and large-fleet operation as the critical path.

## 2. Releases

**No new releases in this window.** The most recent shipped line referenced throughout the dataset is **2026.9.4** (with 2026.9.3 as the prior stable), both of which are the subject of extensive update-failure and regression reports. No breaking-change or migration notes are available from this data.

## 3. Project Progress

No PR details were provided for the 204 merged/closed PRs, but the open PR pipeline shows a coordinated stabilization push, largely by maintainers:

- **Gateway crash theory → fix:** [PR #150427](https://github.com/openclaw/openclaw/pull/150427) "keep child cleanup failures from crashing the Gateway" (related to #144911, #144941).
- **Large-fleet memory growth:** [PR #150354](https://github.com/openclaw/openclaw/pull/150354) "curb Gateway memory growth after large fleets start" (related to #149538).
- **Reply-loop / duplicate-answer fixes:** [PR #150527](https://github.com/openclaw/openclaw/pull/150527) (P1, repeated `REPLY_SKIP` and child reply loops) and [PR #150539](https://github.com/openclaw/openclaw/pull/150539) (closes #150410).
- **Update/upgrade recovery:** [PR #150494](https://github.com/openclaw/openclaw/pull/150494) "continue when service inspection is unavailable," [PR #150153](https://github.com/openclaw/openclaw/pull/150153) "keep task recovery working across shared Gateway updates."
- **Agent/model selection correctness:** [PR #150423](https://github.com/openclaw/openclaw/pull/150423) (fixes #149796), [PR #149916](https://github.com/openclaw/openclaw/pull/149916) (fixes #149867).

Notable **closed issues** signaling resolved work: [#146265](https://github.com/openclaw/openclaw/issues/146265) (AsyncWorkScope closed process-wide), [#31331](https://github.com/openclaw/openclaw/issues/31331) (Docker workspaceAccess), [#145929](https://github.com/openclaw/openclaw/issues/145929) (auth profile lock), [#90098](https://github.com/openclaw/openclaw/issues/90098) (large attachments), [#87407](https://github.com/openclaw/openclaw/issues/87407) (Anthropic socket fallback), [#111985](https://github.com/openclaw/openclaw/issues/111985) (**security**: memory-core OAuth token to embeddings API), [#111578](https://github.com/openclaw/openclaw/issues/111578) (gateway auth token dropped on update), [#146719](https://github.com/openclaw/openclaw/issues/146719) (Windows updater path).

## 4. Community Hot Topics

| Item | Comments | Signal |
|---|---|---|
| [#97616](https://github.com/openclaw/openclaw/issues/97616) — zombie child-process leak | 30 | P1, message-loss + crash-loop |
| [#91588](https://github.com/openclaw/openclaw/issues/91588) — Gateway RSS 350MB → 15.5GB OOM | 25 | P1, session-state |
| [#144911](https://github.com/openclaw/openclaw/issues/144911) — MCP init timeout crashes Gateway | 24 | Diamond-lobster triage, fix PR #150427 exists |
| [#126360](https://github.com/openclaw/openclaw/issues/126360) — `AgentSelectionRequiredError` log flood | 17 | Multi-agent `explicit` ownership |
| [#150201](https://github.com/openclaw/openclaw/issues/150201) — Windows snapshot update failure | 14 | P0, ux-release-blocker |
| [#137332](https://github.com/openclaw/openclaw/issues/137332) — requester-settle batches retry forever | 13 | Diamond-lobster, queueable fix |
| [#149538](https://github.com/openclaw/openclaw/issues/149538) — Gateway ready but starved (632 agents) | 12 | P0 |
| [#146394](https://github.com/openclaw/openclaw/issues/146394) — npm global-install update failure | 11 | P0 |

**Underlying needs:** operators running *large, multi-agent fleets* on long-lived Gateways are hitting resource leaks and event-loop starvation; *single-user* operators are blocked by update/upgrade failures and session-state loss. There is also a clear demand for **observability** — dispatch telemetry ([#76247](https://github.com/openclaw/openclaw/issues/76247)) and diagnosis-friendly logs (the `AgentSelectionRequiredError` flood).

## 5. Bugs & Stability (ranked by severity)

**P0**
- [#150201](https://github.com/openclaw/openclaw/issues/150201) — Windows update candidate snapshot fails on 2026.9.3; Gateway SQLite check times out. *No fix PR shown.*
- [#149538](https://github.com/openclaw/openclaw/issues/149538) — `main` reaches ready but never serves; `/health` times out. **Fix in flight:** PR #150354.
- [#146394](https://github.com/openclaw/openclaw/issues/146394) — `global-install-failed` on 2026.9.3 (linux/arm64).
- [#144739](https://github.com/openclaw/openclaw/issues/144739) — 2026.9.3 → 2026.9.4 runs old version against schema-17 state.
- [#148681](https://github.com/openclaw/openclaw/issues/148681) — update failure at `finalize:doctor` (2026.9.4).
- [#145252](https://github.com/openclaw/openclaw/issues/145252) — maintainer tracking issue for 2026.9.3/9.4 update reliability.

**P1**
- [#97616](https://github.com/openclaw/openclaw/issues/97616) — unreaped hook/tool child processes → zombie accumulation. *No fix PR shown.*
- [#91588](https://github.com/openclaw/openclaw/issues/91588) — Gateway memory leak to 15.5GB, repeated OOM restarts. *No fix PR shown.*
- [#144911](https://github.com/openclaw/openclaw/issues/144911) — MCP init timeout crashes Gateway via unhandled rejection. **Fix PR #150427.**
- [#148529](https://github.com/openclaw/openclaw/issues/148529) — start→ready ~12 min on a 632-agent fleet (vs ~2s previously).
- [#148707](https://github.com/openclaw/openclaw/issues/148707) — lost reply: "no active tool authority snapshot" (2026.9.4 regression).
- [#137332](https://github.com/openclaw/openclaw/issues/137332) — requester-settle batches retry forever after ownership check.
- [#101929](https://github.com/openclaw/openclaw/issues/101929) — context-overflow estimator over-counts 2.3–2.6×.
- [#136311](https://github.com/openclaw/openclaw/issues/136311) — reindex lock never released; 19GB of orphaned temp DBs.
- [#134925](https://github.com/openclaw/openclaw/issues/134925) — main thread ~100% CPU per turn on ARM64/Pi.
- [#119411](https://github.com/openclaw/openclaw/issues/119411) — memory file watcher never reindexes; `Dirty: no` misreports.

**Notable closed regressions:** [#118018](https://github.com/openclaw/openclaw/issues/118018) (stale subagent completion), [#146265](https://github.com/openclaw/openclaw/issues/146265) (AsyncWorkScope), [#146719](https://github.com/openclaw/openclaw/issues/146719) (Windows updater).

**Assessment:** the pattern points to lifecycle/resource management in the Gateway (child processes, memory, async work scope, locks) as the top systemic risk, compounded by a fragile self-update pipeline that spans npm, launchd/systemd, and Windows extended-path handling.

## 6. Feature Requests & Roadmap Signals

- **Deterministic/gateway-lite mode** — [#86881](https://github.com/openclaw/openclaw/issues/86881) (closed this window) asked for a no-AI-harness channel/webhook gateway.
- **One-way A2A dispatch mode** — [#44309](https://github.com/openclaw/openclaw/issues/44309) to stop reply-back

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — AI Agent / Personal AI Assistant OSS  
**Date:** 2026-09-17  
**Projects in scope:** OpenClaw, Hermes Agent  
**Scope caveat:** Hermes Agent’s digest failed to generate. All Hermes metrics below are **N/A / unknown**, so cross-project comparison is asymmetric. OpenClaw data is complete.

---

## 1. Ecosystem Overview

Only OpenClaw provided a usable community digest, limiting true cross-project comparison. The personal AI assistant / agent OSS landscape remains high-velocity and infrastructure-heavy: OpenClaw alone recorded **1,000 issue/PR updates in 24 hours**. The critical path is no longer basic agent capability but operational reliability: Gateway runtime lifecycle, memory/process leaks, self-update, and large multi-agent fleet scaling. Community demand is shifting toward observability, protocol interop (MCP/A2A), and safer upgrades. Runtime stability is now the main gating factor for production adoption.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | Open/Active Issues | Closed Issues | PRs Updated (24h) | Open PRs | Merged/Closed PRs | Release Status | Health Score* |
|---|---:|---:|---:|---:|---:|---:|---|---|
| **OpenClaw** | 500 | 331 | 169 | 500 | 296 | 204 | No new release; latest referenced line **2026.9.4**, prior stable **2026.9.3** | **6/10 — Active but strained (Amber)** |
|

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ Summary generation failed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*