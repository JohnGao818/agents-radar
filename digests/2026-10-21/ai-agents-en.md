# OpenClaw Ecosystem Digest 2026-10-21

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-10-21 03:06 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

⚠️ Summary generation failed.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — 2026-10-21

**Scope caveat:** The supplied dataset covers two projects. Hermes Agent has a complete digest; OpenClaw’s summary generation failed. OpenClaw figures are therefore marked **N/A** rather than inferred as zero. The health score is an analyst rubric, not a vendor metric: activity throughput, closure/drain balance, release cadence, risk concentration, and backlog cleanup.

---

## 1. Ecosystem Overview

The personal AI assistant / agent open-source landscape is shifting from one-shot CLI demos toward **continuously running, multi-surface systems**. The visible engineering pain is no longer only model quality; it is memory governance, gateway reliability, tool-contract compatibility, session semantics, and provider billing correctness. Hermes Agent shows high daily churn but a clear **intake-over-drain imbalance**, with no release cut and many P2 operational risks accumulating on `main`. Open

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent — Project Digest, 2026-10-21

## 1. Today's Overview

Hermes Agent remains highly active but is showing a clear **intake-over-drain imbalance**: 50 issues and 50 PRs were touched in the last 24 hours, yet only 1 issue was closed (#94928) and only 4 PRs were merged or closed. That 49:1 open-to-closed issue ratio and 46:4 PR ratio indicate a growing triage backlog even as raw activity stays strong. No release was cut, so the current `main` continues to accumulate unreleased fixes and features. The day's work clusters around four themes: **memory-system governance and privacy**, **gateway reliability/log durability/session state**, **`computer_use` contract drift against cua-driver 0.3x**, and **provider/model-billing correctness**. Notably, three long-lived community PRs from July/August were closed today (#61483, #61533, #135989), a positive sign of backlog cleanup — but several equally old items (#61497, #60802, #89166) remain untouched at the decision level.

---

## 2. Releases

**None.** No new version was published in the last 24 hours, and the "Latest Releases" feed is empty. All fixes and features described below are currently unreleased on `main`; users on stable builds will not see them until the next tag.

---

## 3. Project Progress

Four PRs were merged/closed in the last 24h, three of which close out long-standing bugs:

| PR | Status | Description | Impact |
|---|---|---|---|
| [#135989](https://github.com/NousResearch/hermes-agent/pull/135989) | CLOSED | `fix(skills)`: make `grounded-citations` sentence splitting and word counting CJK-aware | Fixes verification being effectively blind to Chinese/Japanese prose (no inter-word spaces, `。！？；` terminators). Open since Oct 10. |
| [#142306](https://github.com/NousResearch/hermes-agent/pull/142306) | CLOSED | `fix(install-e2e)`: desktop smoke accepts the canonical gateway Desktop attaches to | Unblocks Linux `+desktop` install/update CI legs that were failing with "found 0 listeners on port 37497" after #106742. |
| [#61533](https://github.com/NousResearch/hermes-agent/pull/61533) | CLOSED | `fix(memory)`: tolerate delimiter-adjacent whitespace | Removes a hard lock on `replace`/`remove` memory writes caused by cosmetic whitespace near `§` delimiters. Open since **July 9** (~3.5 months). |
| [#61483](https://github.com/NousResearch/hermes-agent/pull/61483) | CLOSED | `fix(send_message)`: fall back to `TELEGRAM_BOT_TOKEN` env token | Closes #61467; env-only Telegram deployments can now deliver messages. Open since **July 9**. |

**Net assessment:** progress today was disproportionately *backlog clearance* rather than new capability delivery. No user-facing feature shipped. Several high-value fixes (#142343 for `computer_use`, #142335 for browser real-profile, #119324 for cron profile scope) are staged but still open.

---

## 4. Community Hot Topics

Ranked by comment volume:

1. **[#135039 — Memory write-time budget enforcement & acceptance pipeline](https://github.com/NousResearch/hermes-agent/issues/135039)** (11 comments, P3/needs-decision)
   Proposes that `MEMORY.md` / `USER.md` be governed by a size budget and a write-time acceptance test, since both files are injected into *every* future turn and directly drive latency and cost. The high comment count on a P3 signals this is really a **product-architecture debate**, not a small patch: where is the line between "always-applicable facts" and session-scoped context?

2. **[#142036 — `logs/gateway.log` silently stops after restart](https://github.com/NousResearch/hermes-agent/issues/142036)** (8 comments, P2/Windows)
   The running gateway produces zero runtime logs post-restart, making transient failures unreproducible from disk. This is an **observability-critical** bug: it degrades every other gateway bug's diagnosability.

3. **[#94928 — `terminal`/`read_file` return empty output when pipe FDs exceed `FD_SETSIZE`](https://github.com/NousResearch/hermes-agent/issues/94928)** (8 comments, **CLOSED**, P2/Linux)
   After uptime, every command returns `{"output": "", "exit_code": 0}` — commands run but all stdout/stderr is discarded. The only issue closed today, and a satisfying resolution to a nasty, insidious class of failure.

4. **[#89166 — Cross-process session lease wait floods chat gateways every 15s](https://github.com/NousResearch/hermes-agent/issues/89166)** (7 comments, P2, tagged `sweeper:risk-message-delivery`)
   When two processes intentionally share a durable conversation (Desktop + Weixin gateway), the lease-wait callback emits a human-facing status message every 15 seconds, starving final delivery. Underlying need: **multi-surface session sharing without user-visible noise**.

5. **[#142037 — Desktop composer model label goes stale after switching](https://github.com/NousResearch/hermes-agent/issues/142037)** (7 comments, P3)
   Session state switches correctly but the UI label doesn't until re-entry. High comment count relative to severity suggests broad reproduction — a cheap, high-visibility polish win.

**Pattern:** the community's attention is concentrated on **cost/latency of always-injected context**, **gateway observability**, and **multi-process session semantics** — i.e., the pains of running Hermes continuously rather than in one-shot CLI use.

---

## 5. Bugs & Stability

No P1-class issues appear in today's set; **P2 is the effective ceiling**. Ranked by severity and blast radius:

### Critical (P2, systemic or data/security-relevant)

- **[#110126 — Output-cap/truncation as a four-subsystem systemic failure class](https://github.com/NousResearch/hermes-agent/issues/110126)** (P2, DeepSeek V4 root cause)
  Argues `finish_reason='length'` spirals are *one* failure class reproduced across four subsystems, currently scattered over **35+ open issues**. If accurate, this is the single highest-leverage stability item in the tracker and warrants a tracking-issue promotion. **No fix PR referenced.**

- **[#116788 — Background memory reviewer persists facts the user explicitly asked not to save](https://github.com/NousResearch/hermes-agent/issues/116788)** (P2, `tool/memory`, `risk-session-state`)
  A privacy/consent violation reproduced with a visual-impairment fact the user asked to exclude. Combined with [#142250](https://github.com/NousResearch/hermes-agent/issues/142250) (docs claiming `memory.write_approval: false` allows free writes while code stages patches regardless), this looks like a **coherent memory-consent defect cluster**. **No fix PR.**

- **[#139662 — Messaging-platform sessions unresumable from Desktop after gateway restart](https://github.com/NousResearch/hermes-agent/issues/139662)** (P2, Discord/Feishu/WeCom)
  `session.resume` returns `not_found`; explicitly related to #134889 ("same loss family"). **No fix PR.**

- **[#142288 — Gateway drops native vision images from history after one turn](https://github.com/NousResearch/hermes-agent/issues/142288)** (P2, Discord)
  Persisted text says "you can see it natively now… [screenshot]" while the pixels are gone — silent context corruption across turns. **No fix PR.**

- **[#141822 — Human messages starve behind internal background wakes](https://github.com/NousResearch/hermes-agent/issues/141822)** (P2, gateway queue)
  Background-process completions and human follow-ups share one strict FIFO; depth-cap requeue can drop human messages entirely. **No fix PR.**

- **[#142301 — `reclaim_task` releases a live worker's claim → duplicate concurrent workers](https://github.com/NousResearch/hermes-agent/issues/142301)** (P2, cron, **filed today**)
  Two concurrent runs of the same task. Classic race; newly reported, so triage is presumably just starting.

- **[#81281 — Egress: sandbox cannot reach mapped providers (rootless bind + `require: true`)](https://github.com/NousResearch/hermes-agent/issues/81281)** (P2, Docker rootless)
  Blocks containerized deployments behind iron-proxy. **No fix PR.**

- **[#142203 — 402 "covers at most N output tokens" is not parsed, so the affordable-cap clamp never fires](https://github.com/NousResearch/hermes-agent/issues/142203)** (P2, billing)
  A recoverable provider response is treated as terminal. Direct revenue/cost impact for metered users.

### Notable (P2 tooling contract breaks — *fix PRs exist*)

- **[#142342 — `computer_use` sends properties the live cua-driver schema rejects](https://github.com/NousResearch/hermes-agent/issues/142342)** (filed today) → **fix PR [#142343](https://github.com/NousResearch/hermes-agent/pull/142343) is open.** cua-driver 0.32+ uses `additionalProperties: false`, so `double_click.button` and `drag.from_element` are *hard refusals*, not ignored.
- **[#135872 — Element clicks refused on cua-driver 0.34: `unknown argument element_index`](https://github.com/NousResearch/hermes-agent/issues/135872)** — same root cause family; **no PR linked yet**, but #142343 likely subsumes part of it.
- **[#126521 — `drag` by element index always fails; `win+d` presses bare `d` and reports success](https://github.com/NousResearch/hermes-agent/issues/126521)** (P2, macOS, `needs-repro`) — false-success reporting is the dangerous part.

### Other

- **[#142324 — Pillow pinned to 12.3.0; GHSA-78g4-xqwv-q3g8 fixed only in 13.0.0](https://github.com/NousResearch/hermes-agent/issues/142324)** (P3 security, filed today, High CVSS 8.1 heap overflow in libopenjp2). Constraint conflict: `browser-harness==0.1.13` also requires Pillow 12.3.0 — needs a coordinated bump.
- **[#141448 — `hermes pm gc` deletes a dependency generation 12 live processes are running from](https://github.com/NousResearch/hermes-agent/issues/141448)** (P2, Windows). "A lease proves selection, not use" — elegant diagnosis of a destructive lifecycle bug

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*