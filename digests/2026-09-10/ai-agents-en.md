# OpenClaw Ecosystem Digest 2026-09-10

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-09-10 02:51 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-09-10

## 1. Today's Overview

OpenClaw shows **very high throughput** today: 500 issues and 500 PRs updated in the last 24 hours, with 194 issues closed and 252 PRs merged/closed, against 306 still-active issues and 248 open PRs. No new releases were published, so the project is in a heavy stabilization/integration window rather than a shipping cycle. Activity is dominated by regression triage (several P0/P1 regressions from the 2026.8.x→2026.9.x migration wave), session-state/event-loop reliability work, and a broad multi-platform UI push (iOS/macOS/Web UI conversation actions and profile binding). Overall health is **strong on throughput but strained on stability** — a high ratio of P0/P1 regressions tied to recent releases is the main risk signal.

---

## 2. Releases

**No new releases in this window.** The "Latest Releases" section is empty. Notably, several open issues reference upgrade paths against 2026.9.1–2026.9.3 (e.g. #142585, #143278, #141617), suggesting the 2026.9.x line is live in the field and accumulating migration-blocker reports rather than new version drops.

---

## 3. Project Progress

**Closed / merged today (sampled):**

| Item | Type | Outcome |
|---|---|---|
| [#143579](https://github.com/openclaw/openclaw/pull/143579) | PR (CLOSED) | UI: expand Dashboard directly from its side-panel tab |
| [#143626](https://github.com/openclaw/openclaw/pull/143626) | PR (CLOSED) | Retain copied engine registries through cleanup |
| [#143561](https://github.com/openclaw/openclaw/pull/143561) | PR (CLOSED) | Reject unknown accounts before channel removal |
| [#135111](https://github.com/openclaw/openclaw/issues/135111) | Issue (CLOSED) | Intermittent "malformed JSON arguments" on v2026.8.1 (26 comments) |
| [#137927](https://github.com/openclaw/openclaw/issues/137927) | Issue (CLOSED) | Internal context block leak into visible Telegram text |
| [#137813](https://github.com/openclaw/openclaw/issues/137813) | Issue (CLOSED) | **P0** Windows gateway never starts after 2026.9.1 |
| [#140971](https://github.com/openclaw/openclaw/issues/140971) | Issue (CLOSED) | Feishu plugin tools silently dropped in message-driven runs |
| [#116851](https://github.com/openclaw/openclaw/issues/116851) | Issue (CLOSED) | Beta blocker: codex final replies lost for SQLite sessions |
| [#91352](https://github.com/openclaw/openclaw/issues/91352) | Issue (CLOSED) | Codex OAuth migration stale profile / app inventory failure |
| [#133692](https://github.com/openclaw/openclaw/issues/133692) | Issue (CLOSED) | Isolated cron superseded runtime generation rejection |

**Features advancing in open PRs:**
- **Native model/auth alignment** — [#143588](https://github.com/openclaw/openclaw/pull/143588) aligns native sign-in with model runtime choices; [#132453](https://github.com/openclaw/openclaw/pull/132453) exposes Codex usage per login.
- **Model choice fidelity** — [#142100](https://github.com/openclaw/openclaw/pull/142100) preserves exact model choices across reloads/fallbacks.
- **Conversation actions stack (draft)** — [#143587](https://github.com/openclaw/openclaw/pull/143587) (gateway profile binding), [#143610](https://github.com/openclaw/openclaw/pull/143610) (iOS), [#143615](https://github.com/openclaw/openclaw/pull/143615) (macOS), [#143631](https://github.com/openclaw/openclaw/pull/143631) (iOS voice actions).
- **Update safety** — [#140339](https://github.com/openclaw/openclaw/pull/140339) retains compatible package rollback and safe recovery admission.
- **Worker/gateway reliability** — [#135838](https://github.com/openclaw/openclaw/pull/135838) (stop provisioning after turn authority closes), [#143372](https://github.com/openclaw/openclaw/pull/143372) (bounded ready capacity), [#143633](https://github.com/openclaw/openclaw/pull/143633) (retain compaction services through issued work).

---

## 4. Community Hot Topics

**Most-discussed Issues (by comment count):**

1. **[#135111](https://github.com/openclaw/openclaw/issues/135111) — 26 comments (CLOSED)** — Intermittent malformed JSON tool-call arguments on v2026.8.1 with claude-sonnet-5. Highest-engagement item of the window; resolved as closed. Underlying need: **provider-parsing robustness / clear error surfaces** when upstream models emit non-conforming tool calls.
2. **[#97616](https://github.com/openclaw/openclaw/issues/97616) — 15 comments (OPEN)** — Unreaped hook/tool child processes → zombie accumulation and runtime degradation. Long-lived (filed June, still active Sept). Underlying need: **process lifecycle hygiene** in long-running gateways.
3. **[#119720](https://github.com/openclaw/openclaw/issues/119720) — 15 comments (OPEN)** — Synchronous agent persistence/transcript maintenance blocking the Gateway event loop at scale. Underlying need: **async I/O scheduling and backpressure** to prevent gateway stalls under load.
4. **[#137927](https://github.com/openclaw/openclaw/issues/137927) — 14 comments (CLOSED)** — Internal context block leaking into visible Telegram text. Underlying need: **strict separation of internal scaffolding from user-visible surfaces**.
5. **[#43367](https://github.com/openclaw/openclaw/issues/43367) — 14 comments (OPEN)** — Multi-agent orchestration instability (config overwrites, session-lock failures). Underlying need: **concurrency-safe agent config and lock semantics**.
6. **[#139714](https://github.com/openclaw/openclaw/issues/139714) — 13 comments (OPEN)** — `openclaw status` stuck on "update in progress" forever. Underlying need: **update state machine correctness / terminal state guarantees**.

**Notable PRs (comments not surfaced in dataset):** [#143501](https://github.com/openclaw/openclaw/pull/143501) (P0 sandbox canonical-destination authorization), [#143588](https://github.com/openclaw/openclaw/pull/143588) (native sign-in alignment), [#142626](https://github.com/openclaw/openclaw/pull/142626) (iMessage feedback, automerge armed), [#141079](https://github.com/openclaw/openclaw/pull/141079) (Telegram late stall reactions).

**Pattern:** The community's dominant concerns are **reliability under scale** (event loop, process leaks, locks), **boundary correctness** (internal content leaking to visible surfaces, provider read gates), and **migration pain** across the 2026.8→2026.9 line.

---

## 5. Bugs & Stability

**P0 / Release-blocker class:**

| Issue | Status | Summary | Fix PR? |
|---|---|---|---|
| [#137813](https://github.com/openclaw/openclaw/issues/137813) | CLOSED | Windows gateway never starts after 2026.9.1 — `--task-supervisor` exits 0 silently | Closed |
| [#142585](https://github.com/openclaw/openclaw/issues/142585) | OPEN | **Regression/migration blocker**: 2026.9.3 Doctor refuses valid legacy workspace setup & attestation import | Not indicated |
| [#115642](https://github.com/openclaw/openclaw/issues/115642) | OPEN | Billing cooldown outlives outage on subscription auth — needs probe-based recovery / manual reset | Not indicated |
| [#141617](https://github.com/openclaw/openclaw/issues/141617) | CLOSED | 2026.9.2 npm update stuck at `phase=requested, status=running` | Closed |

**P1 / High severity (open):**

- [#97616](https://github.com/openclaw/openclaw/issues/97616) — Zombie child-process accumulation (message-loss, crash-loop tags).
- [#119720](https://github.com/openclaw/openclaw/issues/119720) — Gateway event-loop blocked by synchronous persistence (crash-loop).
- [#132762](https://github.com/openclaw/openclaw/issues/132762) — Overflow retry succeeds on a tool result with no final delivery (**fix-shape-clear / queueable-fix**).
- [#127148](https://github.com/openclaw/openclaw/issues/127148) — Codex `sessions.compact` acquires second app-server → active-writer conflict.
- [#140010](https://github.com/openclaw/openclaw/issues/140010) — Windows sleep/resume: WebSocket reconnects fail 30–60s+ (crash-loop).
- [#138042](https://github.com/openclaw/openclaw/issues/138042) — Gateway control requests stall for 157–276s (crash/hang).
- [#136311](https://github.com/openclaw/openclaw/issues/136311) — memory-core reindex lock reacquired on every start; 19 GB orphaned temp DBs.
- [#115367](https://github.com/openclaw/openclaw/issues/115367) — Provider-owned read gate requires `origin: bundled`, but privileged chat surfaces ship as external plugins → reads locked to current conversation (security).
- [#139274](https://github.com/openclaw/openclaw/issues/139274) — Native `/codex bind` drops voice-note attachments, skips STT (**fix-shape-clear / queueable-fix**).
- [#125570](https://github.com/openclaw/openclaw/issues/125570) — Skill Workshop update overwrites live skill `description`, silently breaking routing (data-loss).
- [#128637](https://github.com/openclaw/openclaw/issues/128637) — Multi-agent setups throw `AgentSelectionRequiredError` on ambient operations.

**Notable closed regressions** (fixes landed in window): [#135111](https://github.com/openclaw/openclaw/issues/135111) (malformed JSON args), [#137927](https://github.com/openclaw/openclaw/issues/137927) (Telegram context leak), [#140971](https://github.com/openclaw/openclaw/issues/140971) (Feishu tools dropped), [#116851](https://github.com/openclaw/openclaw/issues/116851) (codex final replies lost), [#95121](https://github.com/openclaw/openclaw/issues/95121) (Codex OAuth ~28s latency), [#96732](https://github.com/openclaw/openclaw/issues/96732) (reasoning_content leak with kimi-k2.6).

**Assessment:** Stability is the top risk. Multiple **crash-loop, message-loss, data-loss, and security** tags cluster around session persistence, provider auth, and gateway event-loop contention — all consistent with load/scale stress on the Gateway.

---

## 6. Feature Requests

---

## Cross-Ecosystem Comparison

**Data caveat:** Only the OpenClaw digest was successfully generated. Hermes Agent’s summary failed, so Hermes metrics, architecture, and community signals are unavailable. This report is therefore OpenClaw-centric

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ Summary generation failed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*