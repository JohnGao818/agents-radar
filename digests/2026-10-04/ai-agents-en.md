# OpenClaw Ecosystem Digest 2026-10-04

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-10-04 04:04 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

⚠️ Summary generation failed.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report
## Personal AI Agent / Assistant Open-Source Ecosystem — 2026-10-04

> **Data completeness notice:** This report is built from the two supplied digests. The **OpenClaw digest failed to generate** (no content), and the **Hermes Agent digest is truncated** mid-item at issue `#132497`. All cross-project comparisons are therefore **single-source** and must be read as directional, not conclusive. Items inferred rather than evidenced are explicitly marked.

---

## 1. Ecosystem Overview

The personal AI assistant ecosystem on 2026-10-04 is defined by **high inbound velocity colliding with constrained maintainer throughput**: a single mid-stage project (Hermes Agent) absorbed 50 issue and 50 PR updates in 24 hours while closing only 3 PRs. The dominant engineering conversation has shifted from capability acquisition to **trust and durability** — silent data loss, cross-owner agent collaboration, and reproducible installs now outrank model/tool features as community priorities. Architecturally, the ecosystem is converging on a **thin core plus a plugin/catalog distribution model**, with heavyweight integrations (Home Assistant, marketing tools) actively being pushed out of core. Simultaneously, platform parity (Windows event-loop blocking) and remote/self-hosted deployment robustness remain unresolved, indicating the ecosystem is still in the "make it survivable" phase rather than the "make it delightful" phase. The ratio of P0/P1 defects to visible fix PRs is elevated, making **reliability engineering the ecosystem's binding constraint**.

---

## 2. Activity Comparison

| Metric (last 24h) | **OpenClaw** (core reference) | **Hermes Agent** |
|---|---|---|
| Issues touched | Not reported | 50 |
| Issues closed | Not reported | 9 |
| Active/open issues | Not reported | 41 |
| Issue close rate | Not reported | 18% of touched |
| PRs touched | Not reported | 50 |
| PRs merged/closed | Not reported | **3** |
| Open PRs | Not reported | **47** |
| Merge throughput | Not reported | **6%** of touched PRs |
| Release status | **Unknown — summary failed** | No release, no changelog |
| Highest-severity open defect | Not reported | **P0** `#132401` (data destruction, **no fix PR**) |
| Open P1 defects | Not reported | 2 (`#132504`, `#132547`) — no fix PRs |
| Activity trend | Not assessable | Very high inbound; throughput-bound |
| **Health score** | **Not assessable** | **4.0 / 10 — Guarded** |

**Health score methodology (Hermes only):**

| Dimension | Weight | Score | Rationale |
|---|---|---|---|
| Merge/close throughput | 3.0 | 1.5 | 3 of 50 touched PRs closed |
| Issue closure ratio | 3.0 | 1.5 | 9 of 50 touched issues closed |
| Release cadence | 2.0 | 0.5 | No release, no changelog |
| P0/P1 backlog w/ no fix PR | 2.0 | 0.5 | 1 P0 + 2 P1 open and unfixed |
| **Total** | **10.0** | **4.0** | Guarded |

**Caveat:** A 24-hour window is a poor basis for absolute health. The score reflects *throughput pressure*, not project quality — Hermes closed two P1 installer/launcher bugs in the same window, which is genuine forward progress.

---

## 3. OpenClaw's Position

**This section cannot be substantiated.** OpenClaw's digest failed entirely, so no activity, release, defect, or community metrics exist in the source data. What follows is positioning analysis based strictly on the dataset's own framing, with confidence levels stated.

**What the dataset establishes (high confidence):**
- OpenClaw is designated the **"core reference"** implementation (`github.com/openclaw/openclaw`), implying it plays the canonical architecture / interface-definition role in this landscape rather than competing on feature breadth.
- It is the only project in this pair given a role label rather than a peer label — a structural, not quantitative, distinction.

**What remains unverified (explicitly inferred, not evidenced):**
- **Advantages vs. peers:** A reference-implementation position typically confers (a) interface/schema authority that derivative projects must track, (b) lower feature-shipping velocity but higher stability expectations, and (c) outsized influence relative to commit volume. None of this is confirmed by the supplied data.
- **Technical approach differences:** Cannot be assessed. No architecture, transport, plugin, or deployment detail exists for OpenClaw. **No evidence in this dataset suggests a code or lineage relationship between OpenClaw and Hermes Agent** — that should not be assumed.
- **Community size comparison:** Not measurable. Hermes shows 36 comments on its top issue (`#97681`) and 12–15 comments on secondary threads; OpenClaw has no equivalent signal available.

**Recommendation:** Treat OpenClaw as **unknown-state** in any decision artifact. Required to close the gap: issue/PR counts, open-PR backlog depth, release cadence, top-commented issues, and P0/P1 inventory.

---

## 4. Shared Technical Focus Areas

Because only one project produced usable data, these are **single-source requirement clusters** that are characteristic of the wider ecosystem. Cross-project confirmation is pending OpenClaw data.

| # | Requirement | Evidence | Confidence it generalizes |
|---|---|---|---|
| 1 | **Durable scratch/TMPDIR lifecycle** — logging, quarantine, keep-markers, no silent deletion | Hermes P0 `#132401` (15 comments, no fix PR) | **High** — any agent that points `TMPDIR` at its own cache and invites long-running work inherits this |
| 2 | **Federated multi-agent collaboration without surrendering control** — per-owner models, tools, memory, credentials | Hermes `#97681` (36 comments, 4 👍, open ~5 weeks) | **High** — the strategic center of gravity in the dataset |
| 3 | **Core/plugin decoupling + catalog distribution** | Hermes PR `#132469` (Home Assistant out of core), `#132572–#132573` (3 catalog additions) | **High** — architectural norm for this ecosystem |
| 4 | **Reproducible, non-ephemeral installs** — never publish scratch-tree interpreters into launchers | Hermes `#131745` (closed), fix in PR `#132570` | **High** — install fragility is a universal onboarding risk |
| 5 | **Windows platform parity** — no synchronous named-pipe reads on the event loop; PID reuse; cookie purge | Hermes P1 `#132547` (no fix PR) | **Medium-High** |
| 6 | **Prompt-injection false-positive recovery** — vendor 403 must not poison the session | Hermes P1 `#132504` (bundled skill contains literal `<tool>`) | **Medium-High** — any project routing through hosted model gateways |
| 7 | **Async correctness** — no blocking calls on event-loop threads; thread-pool saturation guards | Hermes `#131375`, PR `#132575` | **Medium-High** |
| 8 | **Session durability across gateway restarts** | Hermes (active cluster per overview) | **Medium** |
| 9 | **Streaming transcript fidelity in desktop UI** | Hermes `#128468` (12 comments), `#132477` | **Medium** |
| 10 | **Path-traversal hardening in shipped static-file skills** | Hermes PR `#130804` | **Medium** — applies to any bundled skill surface |
| 11 | **Approval/guardian safety without friction** | Hermes `#131375` | **Medium** |

---

## 5. Differentiation Analysis

Only Hermes Agent can be characterized. OpenClaw differentiation is **not assessable**.

| Axis | Hermes Agent | OpenClaw |
|---|---|---|
| **Role in ecosystem** | Full-featured personal agent w/ desktop, gateway, plugins | Core reference (role label only) |
| **Feature focus** | Multi-gateway/multi-Bot collaboration; plugin catalog; bundled skills; Desktop + `serve` + `tui-rpc` surfaces | Unknown |
| **Target users** | Individual operators running personal Bots on self-chosen infrastructure; teams via inbound webhooks (Teams fan-out, PR `#129377`) | Unknown — presumably downstream consumers of the reference |
| **Architecture signals** | Thin core + `optional-skills` + catalog plugins; UDS wake-inbox transport; durable wake layer (closed `#28570`/`#28852`); Relay session model | Unknown |
| **Distribution model** | Auto-installed catalog plugins scoped to profile usage (`homeassistant`, `socialforge`, `contentforge`, `digital-marketing-pro`) | Unknown |
| **Interface surface** | Desktop, gateway, TUI-RPC, Relay, Teams/WhatsApp/Home Assistant integrations | Unknown |
| **Notable posture** | Extensibility-first, actively *reducing* core surface area | Reference-stability posture (inferred only) |

**Key structural difference (if one exists):** a reference implementation optimizes for **conformance and interface stability**, whereas Hermes optimizes for **surface-area expansion with active pruning**. These are complementary lifecycle stages, not competitors — but this is hypothesis, not verified fact.

---

## 6. Community Momentum & Maturity

**Activity tiers (Hermes only — OpenClaw unrated):**

| Tier | Project | Status |
|---|---|---|
| **Rapid iteration (throughput-bound)** | Hermes Agent | 50 issues + 50 PRs touched/24h; 47 PRs open; 0 releases |
| **Unrated** | OpenClaw | No data |

**Hermes Agent maturity read:**

- **Momentum: very high, community-led.** 36 comments on `#97681` and 12–15 comments on P0/P2 threads within days of filing indicates a dense, engaged contributor base — not a single-maintainer project.
- **Maturity: mid-stage, unstable.** No release cut in the window, 47 open PRs against 3 closures, and two of the three highest-severity defects have **no visible fix PR**. The project is accumulating review debt faster than it retires it.
- **Stabilizing signals present but sub-dominant:** two P1 installer/launcher bugs were fully closed (`#123238`, `#131745`) with a root-cause fix PR (`#132570` — `_is_scratch_python` detection). Long-dormant issues from 2026-05-19 (`#28570`/`#28852`, durable wake layer) also closed. This is evidence of deliberate debt retirement, just at insufficient volume.
- **Diagnosis:** the bottleneck is **review and merge capacity**, not contributor supply or idea flow. Issue flow is healthier than PR flow (18% vs. 6% closure).

---

## 7. Trend Signals

Signals extracted from community feedback, ranked by confidence and developer relevance:

1. **Trust and durability are now the primary adoption barrier.** A silent 24h prune deleting multi-day agent work generated the highest-emotion thread in the dataset. Developers should treat **quarantine, keep-markers, and deletion audit logs** as baseline table stakes, not features. Any agent that

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent — Project Digest
**Date: 2026-10-04** | Repo: [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## 1. Today's Overview

Hermes Agent is in a **high-velocity but merge-constrained state**: 50 issues and 50 PRs were touched in the last 24h, yet only 3 PRs were merged/closed against 47 still-open PRs, and no release was cut. Issue flow is healthier than PR flow — 9 issues were closed (including two P1 installer/launcher bugs, [#123238](https://github.com/NousResearch/hermes-agent/issues/123238) and [#131745](https://github.com/NousResearch/hermes-agent/issues/131745)), leaving 41 active. The day's most urgent item is a **P0 data-destruction report**, [#132401](https://github.com/NousResearch/hermes-agent/issues/132401), where a 24h idle prune of the shared `scratch` TMPDIR silently deletes multi-day agent work with no log, quarantine, or keep-marker. A clear cluster of defects is also forming around **launcher/install robustness** (scratch-tree Python baked into published commands), **Windows platform behavior** (named-pipe blocking, cookie purge, PID reuse), and **session durability** across gateway restarts. Meanwhile, roadmap work continues on multi-Bot collaboration ([#97681](https://github.com/NousResearch/hermes-agent/issues/97681), 36 comments) and on moving heavyweight integrations out of core into the plugin catalog.

**Activity assessment:** Very high inbound activity; review/merge throughput is the bottleneck. Stability risk is elevated by the ratio of P0/P1 bugs to visible fix PRs.

---

## 2. Releases

**No new releases in the last 24h.** No changelog, breaking-change, or migration notes to report. Several in-flight fixes (launcher, providers, terminal cleanup) are queued in open PRs and would logically land in the next version.

---

## 3. Project Progress

Only 3 PRs were merged/closed in the window, and none of them appear in the top-20-by-comments sample, so specific merge contents cannot be enumerated from this data. What *did* advance today is issue resolution on the install/launcher track:

- **[#123238](https://github.com/NousResearch/hermes-agent/issues/123238) [CLOSED, P1]** — Launching under a different `HERMES_HOME` rewrote shared checkout launchers to point at that home's Python; deleting the temp home then bricked `hermes`. This was the root-cause pattern behind today's launcher fix PR.
- **[#131745](https://github.com/NousResearch/hermes-agent/issues/131745) [CLOSED, P1]** — Launchers published against an e2e scratch Python caused an exit-127 gateway crash loop after reboot. **Fix PR exists: [#132570](https://github.com/NousResearch/hermes-agent/pull/132570)** ("never bake scratch-tree interpreters into published commands"), adding `_is_scratch_python` detection with fallback to store Python.
- **[#79471](https://github.com/NousResearch/hermes-agent/issues/79471) [CLOSED, P2]** — One-shot execution exited without emitting the Relay session-end event, leaving root sessions open.
- **[#28570](https://github.com/NousResearch/hermes-agent/issues/28570) / [#28852](https://github.com/NousResearch/hermes-agent/issues/28852) [CLOSED, P3]** — The agent-wake UDS transport + durable wake-inbox durability layer, both filed 2026-05-19, were closed together.
- **[#117861](https://github.com/NousResearch/hermes-agent/issues/117861) [CLOSED, P2]** — Cloudflare 1014 (CNAME Cross-User Banned) breaking Dashboard Auth0 login.
- **[#65426](https://github.com/NousResearch/hermes-agent/issues/65426) [CLOSED, P3]** — WhatsApp integration profile-scoping question resolved.

**In-flight work with visible momentum (open PRs):**
- [#132469](https://github.com/NousResearch/hermes-agent/pull/132469) — Home Assistant (gateway platform + toolset) decoupled from core into the `homeassistant` catalog plugin, auto-installed for profiles that used it.
- [#132573](https://github.com/NousResearch/hermes-agent/pull/132573), [#132572](https://github.com/NousResearch/hermes-agent/pull/132572), [#132571](https://github.com/NousResearch/hermes-agent/pull/132571) — three plugin-catalog additions (socialforge, contentforge, digital-marketing-pro).
- [#132575](https://github.com/NousResearch/hermes-agent/pull/132575) — fail-fast saturation guard for the `tui-rpc` LONG-handler thread pool.
- [#130804](https://github.com/NousResearch/hermes-agent/pull/130804) — path-traversal hardening in two shipped `optional-skills` static file servers.
- [#129377](https://github.com/NousResearch/hermes-agent/pull/129377) — multiple incoming Teams webhooks (fan-out delivery).

---

## 4. Community Hot Topics

| Rank | Item | Comments | 👍 | Signal |
|---|---|---|---|---|
| 1 | [#97681 — Let Bots collaborate across gateways](https://github.com/NousResearch/hermes-agent/issues/97681) | 36 | 4 | Open since **2026-08-29** |
| 2 | [#132401 — scratch prune destroys multi-day agent work](https://github.com/NousResearch/hermes-agent/issues/132401) | 15 | 0 | P0, filed 2026-10-03 |
| 3 | [#128468 — Desktop duplicated render + scroll jumping](https://github.com/NousResearch/hermes-agent/issues/128468) | 12 | 1 | P2, open since 2026-09-29 |
| 4 | [#123238 — HERMES_HOME rebinds launchers](https://github.com/NousResearch/hermes-agent/issues/123238) | 6 | 0 | Resolved today |
| 5 | [#125746 — plugin load `dictionary changed size during iteration`](https://github.com/NousResearch/hermes-agent/issues/125746) | 5 | 0 | Marked duplicate |
| 6 | [#131375 — smart-approval guardian crashes on event-loop threads](https://github.com/NousResearch/hermes-agent/issues/131375) | 5 | 0 | P2 |

**Underlying needs analysis:**
- **#97681 is the strategic center of gravity.** The framing — personal Bots, each running where its owner chooses, with its own models/tools/memory/credentials, collaborating *without anyone giving up control* — is a federated multi-agent vision. The 4 👍 plus 36 comments on a P2 issue suggests this is a flagship direction, not a niche request. Its longevity (open ~5 weeks) is both a sign of design complexity and a backlog risk.
- **#132401 is the highest-emotion thread.** Users are losing days of parked agent work to a silent 24h prune of `~/.hermes/cache/scratch`, which Hermes itself points `TMPDIR`/`TMP`/`TEMP` at and tells agents to use. The requested remedy is a full durability protocol: logging, quarantine, keep-markers. This is a trust issue, not just a bug.
- **#128468 signals Desktop UX debt** around streaming: duplicated message render plus scroll jumping erodes confidence in transcript as ground truth.
- **#131375 reveals an async-architecture smell**: sync Relay completion raising on event-loop threads means every flagged command escalates in Desktop/`serve` sessions — safety features becoming friction.

---

## 5. Bugs & Stability

**Ranked by severity (today's active set):**

**P0 — Critical / data loss**
- [#132401](https://github.com/NousResearch/hermes-agent/issues/132401) — 24h idle delete of `TMPDIR`-pointed scratch silently destroys multi-day agent work; no log, no quarantine, no keep-marker. **No visible fix PR.**

**P1 — High impact**
- [#132504](https://github.com/NousResearch/hermes-agent/issues/132504) — Three bundled skills contain the literal `<tool>`; OpenRouter returns `403 prompt injection patterns detected`, mislabelled as a firewall block, and **poisons the entire session** thereafter. **No visible fix PR.**
- [#132547](https://github.com/NousResearch/hermes-agent/issues/132547) — Windows: `_profile_reconcile_watcher` blocks the gateway event loop on a synchronous named-pipe read; `shutdown_watchdog` hard-kills with exit 75. Explicitly distinguished from #105279/#100014. **No visible fix PR.**
- [#123238](https://github.com/NousResearch/hermes-agent/issues/123238) — *(closed today)* deleted temp home bricking `hermes`.
- [#131745](https://github.com/NousResearch/hermes-agent/issues/131745) — *(closed today)* exit-127 gateway crash loop; **fix in [#132570](https://github.com/NousResearch/hermes-agent/pull/132570)**.

**P2 — Notable**
- [#128468](https://github.com/NousResearch/hermes-agent/issues/128468) — Desktop transcript duplicate render + scroll jumping during streaming (12 comments — most-discussed open bug).
- [#131375](https://github.com/NousResearch/hermes-agent/issues/131375) — smart-approval guardian crash on event-loop threads; every flagged command escalates.
- [#132477](https://github.com/NousResearch/hermes-agent/issues/132477) — `_relay_thinking` still re-emits plain reply text as `reasoning.available` on master; reply fragments render twice in Desktop (observed on `glm-5.3-flash`).
- [#132497](https://github.com/NousResearch/hermes-agent/issues/132497) — Explicit session archive only flips the flag; runtime, active-s

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*