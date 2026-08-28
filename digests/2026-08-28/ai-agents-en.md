# OpenClaw Ecosystem Digest 2026-08-28

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-08-28 08:47 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-08-28

## Today's Overview

OpenClaw saw very high triage and development activity in the last 24 hours: 500 issues and 500 PRs were updated, with 164 issues and 151 PRs closed/merged. No new release was cut today. Maintainer-heavy PR batches (especially by `steipete`) landed across the gateway, Control UI, macOS companion, and plugin/sandbox areas. The project remains release-stable in cadence, but several P0/P1 reliability regressions around resource leaks, session-state corruption, and channel message delivery are keeping maintainers busy.

## Project Progress

Closed/merged PRs today show progress in performance, security-policy UX, session management, and agent-boundary correctness:

- **Perf:** [PR #131442](https://github.com/openclaw/openclaw/pull/131442) — "perf(plugins): unify progressive plugin cache ownership" addresses a 90.6-second live profile stall caused by repeated package metadata rediscovery during health/status/model lookups.
- **Security/Policy UX:** [PR #116489](https://github.com/openclaw/openclaw/pull/116489) and follow-up [PR #120900](https://github.com/openclaw/openclaw/pull/120900) land the install-policy warning flow: external `security.installPolicy` can return `warn`, and an admin can deliberately acknowledge a warning before continuing a plugin install.
- **Session/UI:** [PR #128995](https://github.com/openclaw/openclaw/pull/128995) makes full session actions (pin, unread, icon, session ID, move to group) available from the chat header.
- **Gateway/Agents:** [PR #126424](https://github.com/openclaw/openclaw/pull/126424) — "fix(gateway): keep conversation delivery within agent bindings" fixes multi-agent operators using conversation tools outside their intended agent boundaries.
- **Build/tooling:** [PR #123975](https://github.com/openclaw/openclaw/pull/123975) cleans up wedged `tsgo` process trees on timeout/signal and adds a bounded `OPENCLAW_TSGO_TIMEOUT_MS` watchdog.

Notable issue closures today also suggest fixes landed for high-profile reports: [Issue #106914](https://github.com/openclaw/openclaw/issues/106914) (`models list` crash), [Issue #103884](https://github.com/openclaw/openclaw/issues/103884) (GPT-5.6 Sol rejected by Codex runtime), [Issue #106760](https://github.com/openclaw/openclaw/issues/106760) (Telegram multi-content-block text erase), and [Issue #116010](https://github.com/openclaw/openclaw/issues/116010) (persistent sessions capped at 128k).

## Community Hot Topics

The most-commented issues today center on gateway/session reliability and cost control:

- [Issue #42475](https://github.com/openclaw/openclaw/issues/42475) — Per-agent cost budget enforcement at the gateway level (23 comments). Operators want daily/monthly caps enforced before model dispatch to avoid runaway spend.
- [Issue #125626](https://github.com/openclaw/openclaw/issues/125626) — OpenClaw 2026.8.1 beta feedback thread (22 comments). Release validation and community regression reporting.
- [Issue #91009](https://github.com/openclaw/openclaw/issues/91009) — P0 Codex `PreToolUse` hook relay spawns CPU-bound `openclaw-hooks` processes and stalls gateway RPC (21 comments, 2 👍).
- [Issue #48003](https://github.com/openclaw/openclaw/issues/48003) — Steer mode does not inject messages mid-turn for main sessions (20 comments, 4 👍). Root cause traced to `KeyedAsyncQueue` change in March.
- [Issue #87744](https://github.com/openclaw/openclaw/issues/87744) — Codex-backed Telegram turns repeatedly time out before `turn/completed` (18 comments, 4 👍). Pattern points to reliability issues in Codex app-server integration.

Underlying needs: operators are pushing for cost governance, deterministic mid-turn steering, and fewer silent failure modes in the Codex runtime and channel delivery layers.

## Bugs & Stability

Ranked by severity and community impact:

| Severity | Issue | Summary |
|---|---|---|
| P0 | [Issue #91009](https://github.com/openclaw/openclaw/issues/91009) | Codex `PreToolUse` hook relay spawns CPU-bound processes and stalls gateway RPC; `impact: crash-loop`. |
| P1 | [Issue #131150](https://github.com/openclaw/openclaw/issues/131150) | Slack DMs silently dropped for all accounts after gateway restart in multi-account socket mode; `prepareSlackMessage` returns null pre-gate. |
| P1 | [Issue #125344](https://github.com/openclaw/openclaw/issues/125344) | `memory-core` local embedding workers and Codex app-servers leak with no idle TTL, strangling the gateway cgroup. |
| P1 | [Issue #87109](https://github.com/openclaw/openclaw/issues/87109) | Gateway heap grows to 1073MB+ at idle on macOS; cron jobs fail silently under memory pressure. |
| P1 | [Issue #100941](https://github.com/openclaw/openclaw/issues/100941) | Gateway drops concurrent in-process tool-to-gateway WebSocket connections (`1006`) under parallel fan-out, with misleading "Gateway crashed" error. |
| P1 | [Issue #129314](https://github.com/openclaw/openclaw/issues/129314) | Hidden "next-turn runtime context" message is occasionally dispatched as a visible standalone turn. |
| P1 | [Issue #86215](https://github.com/openclaw/openclaw/issues/86215) | Codex OAuth refresh failures can wedge an agent for hours without alerting or profile rotation. |
| P2 | [Issue #103198](https://github.com/openclaw/openclaw/issues/103198) | WebChat image attachments not mapped to real media store path; image tool receives `image_0`. |

Several open PRs today address adjacent reliability issues, including [PR #131672](https://github.com/openclaw/openclaw/pull/131672) (WhatsApp unmatched attachments across captioned replacement) and [PR #130563](https://github.com/openclaw/openclaw/pull/130563) (prevent early final responses in sequential subagent runs).

## Feature Requests & Roadmap Signals

Strong roadmap signals from today's data:

- **Per-agent cost budgets** ([Issue #42475](https://github.com/openclaw/openclaw/issues/42475)) — likely candidate for a near-term gateway feature; tied to operator spending controls.
- **Multi-slot memory architecture** ([Issue #60572](https://github.com/openclaw/openclaw/issues/60572)) — replace single `plugins.slots.memory` with purpose-specific memory slots; 3 👍, enhancement label.
- **Slack modal support** ([Issue #88154](https://github.com/openclaw/openclaw/issues/88154)) — first-class structured input for interactive workflows.
- **Control UI plugin contribution slots** ([Issue #71736](https://github.com/openclaw/openclaw/issues/71736)) — SDK surface for chat modes, approval cards, input guards, and status surfaces.
- **Agent-facing scheduling API** ([Issue #71712](https://github.com/openclaw/openclaw/issues/71712)) — recurring cron jobs created by agents with non-forgeable provenance.
- **Persistent task-status surface** ([Issue #52640](https://github.com/openclaw/openclaw/issues/52640)) — especially for long-running Discord/channel turns.
- **JSONL session-replay harness** ([Issue #80176](https://github.com/openclaw/openclaw/issues/80176)) — Codex×Pi parity Phase 5; replay real transcripts across runtimes and diff trajectories.
- **Theme customization system** ([Issue #28300](https://github.com/openclaw/openclaw/issues/28300)) — preset themes + custom theme studio in Control UI; 5 👍.

Given current PR focus, the next minor release will likely prioritize reliability and performance over new user-facing features, but cost budgets, Slack modals, and memory-slot improvements are the strongest candidate roadmap items.

## User Feedback Summary

Real pain points captured today:

- **Multi-account Slack

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant / Agent Open-Source Ecosystem
**Data window:** 2026-08-28 (last 24 hours)

> **Data availability note:** The Hermes Agent digest generation failed for this period, so no issue/PR metrics, release status, or community signals are available. To avoid fabrication, Hermes-specific values are marked **N/A** and the analysis is necessarily OpenClaw-centric. Any cross-project claims involving Hermes should be treated as unverified until its digest is restored.

---

## 1. Ecosystem Overview

The open-source personal AI assistant / agent ecosystem is consolidating around gateway-centric architectures that unify multiple messaging channels (Slack, Telegram, WhatsApp, Discord, WebChat), multiple model runtimes (Codex, Pi), and plugin-based memory/tooling under a single control plane. Community attention is shifting from raw capability demos toward production concerns: cost governance, session reliability, deterministic mid-turn control, and cross-runtime behavioral parity. Maintainers are investing heavily in performance (caching, process lifecycle), security-policy UX (install warnings and acknowledgement flows), and agent-boundary correctness. The density of triage in a 24-hour window — 500 issues and 500 PRs updated in a single project — indicates a large, actively engaged operator base running these agents in real deployments. At the same time, recurring P0/P1 regressions in channel delivery and gateway stability show the field is still maturing on operational durability.

---

## 2. Activity Comparison

| Project | Issues (updated / closed) | PRs (updated / merged) | Release status | Health score* |
|---|---|---|---|---|
| **OpenClaw** | 500 / 164 | 500 / 151 | Stable cadence; no release cut today | **7/10** |
| **Hermes Agent** | N/A — digest generation failed | N/A | N/A | N/A |

*Health score (1–10) weighs triage velocity, closure efficiency (~33% issues, ~30% PRs), release stability, and severity of open regressions. OpenClaw's score reflects exceptional maintainer throughput and release discipline, offset by multiple open P0/P1 reliability issues (resource leaks, dropped channel messages, gateway stalls).

---

## 3. OpenClaw's Position

- **Advantages vs. peers:** Very high maintainer velocity (151 PRs merged/day), broad channel coverage (Slack, Telegram, WhatsApp, Discord, WebChat), cross-runtime support (Codex + Pi with parity work), and a plugin/sandbox architecture with progressive cache ownership that suggests attention to real-world scale.
- **Technical approach:** Gateway-first design with agent bindings that enforce conversation-delivery boundaries; a `KeyedAsyncQueue`-based session engine; plugin lifecycle with security install-policy warnings; persistent session state and a Control UI for session management. This positions it as the "core reference" implementation in its ecosystem.
- **Community size comparison:** Quantitative comparison against Hermes is not possible today. However, 1,000 combined issue/PR updates in 24 hours and 20+ comment threads on hot issues indicate a large operator base — likely among the most active in the niche. Maintainer-heavy PR batches (`steipete`) suggest a partially sponsored/core-team-driven development model.

---

## 4. Shared Technical Focus Areas

*Caveat: with Hermes data unavailable, these are extracted from OpenClaw's community alone; they are the strongest candidates for cross-project trends and should be validated against other projects once digests are available.*

| Focus area | Specific need (referenced in OpenClaw) |
|---|---|
| **Cost governance** | Per-agent daily/monthly budget caps enforced at gateway level before model dispatch (#42475) |
| **Deterministic mid-turn control** | Steer mode that injects messages mid-turn for main sessions (#48003, root-caused to March `KeyedAsyncQueue` change) |
| **Resource lifecycle management** | Idle TTLs for local embedding workers and Codex app-servers to prevent gateway cgroup strangulation (#125344); heap growth to 1GB+ at idle (#87109) |
| **Runtime reliability & parity** | Codex-backed turns timing out before `turn/completed` (#87744); JSONL session-replay harness for Codex×Pi parity (#80176) |
| **Channel delivery robustness** | Slack DMs dropped after gateway restart in multi-account socket mode (#131150); WhatsApp unmatched attachments (#131672, open PR) |
| **Memory architecture specialization** | Replace single `plugins.slots.memory` with purpose-specific memory slots (#60572) |
| **Agent-facing scheduling** | Recurring cron jobs created by agents with non-forgeable provenance (#71712) |
| **Security-policy UX** | External `installPolicy` returning `warn` with explicit admin acknowledgement (#116489, #120900) |

---

## 5. Differentiation Analysis

While Hermes-specific comparison data is unavailable, OpenClaw's differentiation within the broader ecosystem is clear from its architecture and roadmap:

- **Feature focus:** Channel-first operations (chat headers with full session actions), cost containment, and interactive surfaces (Slack modals, Control UI plugin slots) rather than raw agent intelligence.
- **Target users:** Operators and power users running persistent, multi-channel, multi-account agent deployments — evidenced by concerns around Slack multi-account socket mode, runaway spend, and cron-job reliability.
- **Technical architecture:** A gateway/control-plane pattern with strict agent bindings, a plugin sandbox with progressive caching, and a `tsgo`-based build toolchain with bounded watchdog timeouts. This is a systems-engineering-heavy design, prioritizing operational control over model flexibility.
- **Safety posture:** Install-policy warning flows and agent-boundary enforcement suggest a governance-first stance, not just a UX convenience.

---

## 6. Community Momentum & Maturity

- **Rapidly iterating (high velocity):** OpenClaw — 500 issues and 500 PRs touched in 24 hours; 151 PRs merged; active P0/P1 bugfixing alongside feature work

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ Summary generation failed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*