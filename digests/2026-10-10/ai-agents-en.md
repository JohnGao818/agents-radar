# OpenClaw Ecosystem Digest 2026-10-10

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-10-10 04:05 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-10-10

## 1. Today's Overview

OpenClaw remains in a high-throughput maintenance phase with **500 issues and 500 PRs updated in the last 24 hours**, but with **no new releases published**. Issue throughput was healthy — **136 of 500 issues (27.2%) closed** — while **157 of 500 PRs (31.4%) merged or closed**, indicating sustained triage-and-fix velocity rather than a feature release cycle. The day's activity is dominated by **update/upgrade reliability failures, gateway resource exhaustion, and message-delivery regressions**, including several still-open P0 release blockers (SQLite WAL growth, event-loop starvation, permanently blocked updater). Positively, a cluster of P0/P1 items were closed today (update hang, Windows Doctor slowness, email config corruption, memory callback registry), suggesting the maintainers are actively clearing blockers rather than accumulating them.

---

## 2. Releases

**No new releases in the last 24 hours.** The latest channel activity evidenced in the issue tracker references **2026.9.7 / 2026.9.8 / 2026.9.9** builds, with multiple users stuck mid-upgrade on **2026.9.5** and **2026.9.6** (see [#158231](https://github.com/openclaw/openclaw/issues/158231), [#156986](https://github.com/openclaw/openclaw/issues/156986)). There is no release note, migration guide, or breaking-change documentation to summarize today.

---

## 3. Project Progress

Although no explicit merged-PR list was provided, the closed-issue set reveals concrete stabilization work landing across memory, embedding, updater, and cron subsystems:

| Closed Item | Area | Signal |
|---|---|---|
| [#159912](https://github.com/openclaw/openclaw/issues/159912) | memory-core plugin registry after reload | P1 session-state fix |
| [#140932](https://github.com/openclaw/openclaw/issues/140932) | local embedding (EmbeddingGemma task prefixes) | Recall improved 16/25 → 23/25 |
| [#129750](https://github.com/openclaw/openclaw/issues/129750) | DashScope embedBatch 10-item limit | Provider compatibility fix |
| [#162047](https://github.com/openclaw/openclaw/issues/162047) | Windows upgrade Doctor 39-min hang | P0 installer performance |
| [#156986](https://github.com/openclaw/openclaw/issues/156986) | `openclaw update` hang in candidate-state | P0 updater loop |
| [#164214](https://github.com/openclaw/openclaw/issues/164214) | Package publication stuck in `publishing` | P0 recovery journal |
| [#95515](https://github.com/openclaw/openclaw/issues/95515) | Email channel config corruption on upgrade | P0 data-loss |
| [#43454](https://github.com/openclaw/openclaw/issues/43454) | Gateway lifecycle hooks request | Closed w/ security review |
| [#133692](https://github.com/openclaw/openclaw/issues/133692) | Isolated cron rejects superseded runtime | P1 regression |

Notable open PRs advancing fixes today include [#130393](https://github.com/openclaw/openclaw/pull/130393) (compaction recovery, P1), [#167739](https://github.com/openclaw/openclaw/pull/167739) (SQLite admission reuse perf), [#168080](https://github.com/openclaw/openclaw/pull/168080) (operator Stop leaving HTTP runs alive), and [#158903](https://github.com/openclaw/openclaw/pull/158903) (required worker placement policy).

---

## 4. Community Hot Topics

The most-discussed threads cluster around **resource exhaustion on long-running gateways and delivery guarantees**.

1. **[#143524 — SQLite WAL grows to 1.4–2.8 GB despite `wal_autocheckpoint=1000`](https://github.com/openclaw/openclaw/issues/143524)** — **115 comments**, P0, Windows 2026.9.2/9.3. A single agent's WAL reached **2865 MB**, blocking gateway startup. Highest-engagement thread by far; underlying need is **durable, self-healing storage maintenance** for long-lived agents.
2. **[#149538 — Gateway reaches ready but never serves](https://github.com/openclaw/openclaw/issues/149538)** — **25 comments**, P0, 632-agent fleet. Lifecycle probe says ready while the event loop is starved and RSS climbs to OOM. Underlying need: **truthful health reporting and backpressure** at fleet scale.
3. **[#97616 — Unreaped hook/tool child process leak](https://github.com/openclaw/openclaw/issues/97616)** — **18 comments**, P1, zombie accumulation over time. Needs **supervisor-level process reaping**.
4. **[#161976 — WhatsApp DM replies fail at durable registry handoff](https://github.com/openclaw/openclaw/issues/161976)** — **18 comments**, P1, flagged `needs-security-review`.
5. **[#69208 — Umbrella: duplicate transcript / replay across channels](https://github.com/openclaw/openclaw/issues/69208)** — **16 comments**, P2 maintainer-tracked. Cross-channel correctness debt.
6. **[#43367 — Multi-agent orchestration instability](https://github.com/openclaw/openclaw/issues/43367)** — **15 comments**, P2, concurrent `agents add` overwrites config and session locks fail.

On the PR side, the highest-signal long-running open PRs are [#156636](https://github.com/openclaw/openclaw/pull/156636) (Copilot context budget, `merge-risk: compatibility`) and [#130393](https://github.com/openclaw/openclaw/pull/130393) (unblocking permanently uncompactable sessions).

---

## 5. Bugs & Stability

Ranked by severity, with fix-PR status where the labels indicate it:

**P0 — Release blockers**
- [#143524](https://github.com/openclaw/openclaw/issues/143524) — WAL runaway / gateway startup block. `no-new-fix-pr`, `needs-maintainer-review`.
- [#149538](https://github.com/openclaw/openclaw/issues/149538) — Ready-but-unserving gateway, event-loop starvation. `needs-info`.
- [#167771](https://github.com/openclaw/openclaw/issues/167771) — Updates *permanently* blocked by `update-recovery-pending` / handoff lease identity mismatch, with **no repair path**. `needs-live-repro`.
- [#158231](https://github.com/openclaw/openclaw/issues/158231) — `managed-service-preflight` update failure on 2026.9.5 (macOS).
- [#115642](https://github.com/openclaw/openclaw/issues/115642) — Billing cooldown outlives the outage; providers disabled for ~5h with no reset command.
- [#48920](https://github.com/openclaw/openclaw/issues/48920) — Live Docs ahead of release (4 👍); config documented but absent at runtime.

**P1 — High impact**
- [#97616](https://github.com/openclaw/openclaw/issues/97616) zombie process leak · [#161976](https://github.com/openclaw/openclaw/issues/161976) WhatsApp handoff · [#146118](https://github.com/openclaw/openclaw/issues/146118) compaction guard gaps · [#119411](https://github.com/openclaw/openclaw/issues/119411) memory watcher never reindexes · [#118185](https://github.com/openclaw/openclaw/issues/118185) double transcript write · [#154891](https://github.com/openclaw/openclaw/issues/154891) failed hot-reload bricks unrelated plugins · [#125764](https://github.com/openclaw/openclaw/issues/125764) Telegram outbound dead-lettering · [#159499](https://github.com/openclaw/openclaw/issues/159499) Windows `ready` at ~220s · [#91941](https://github.com/openclaw/openclaw/issues/91941) Feishu streaming latency · [#135272](https://github.com/openclaw/openclaw/issues/135272) macOS companion `COMPANION_APP_UNAVAILABLE` · [#157691](https://github.com/openclaw/openclaw/issues/157691) Codex policy handoff after hot reload · [#119454](https://github.com/openclaw/openclaw/issues/119454) stuck-session recovery self-suppresses.

**P2 — Notable**
- [#140129](https://github.com/openclaw/openclaw/issues/140129) Anthropic cache stuck at ~46k prefix (long sessions) · [#51429](https://github.com/openclaw/openclaw/issues/51429) hardcoded `/Users/wangtao` workspace path shipped in a release · [#72015](https://github.com/openclaw/openclaw/issues/72015) active-memory blocks replies · [#99659](https://github.com/openclaw/openclaw/issues/99659) OOM after companion-app connect · [#68105](https://github.com/openclaw/openclaw/issues/68105) RTL bidi isolation missing at outbound boundary.

**Fix-PR presence:** Many P1/P2 items carry `clawsweeper:linked-pr-open` (#43367, #119411, #118185, #142336, #159912, #95515, #129750, #133692), indicating active in-flight fixes. The P0 storage/updater items largely do **not** — these are the highest-risk gaps.

---

## 6. Feature Requests & Roadmap Signals

Open enhancement requests, with likely near-term candidates:

- **[#14785 — Reduce tool schema token overhead (~3,500 tok/session)](https://github.com/openclaw/openclaw/issues/14785)** — recurring cost concern, reinforced by [#125314](https://github.com/openclaw/openclaw/issues/125314) (Codex serializing full manager schema). Strong candidate for a context-budget release alongside PRs [#156636](https://github.com/openclaw/openclaw/pull/156636) and [#168157](https://github.com/openclaw/openclaw/pull/168157).
- **[#16670 — Onboarding wizard should mandate Memory/Embedding setup](https://github.com/openclaw/openclaw/issues/16670)** — directly aligned with today's merged embedding fixes (#140932, #129750) and PR [#168075](https://github.com/openclaw/openclaw/pull/168075) (Ollama embedding models in onboarding). **High probability next.**
- **[#13219 — Per-model usage logging for cost tracking](https://github.com/openclaw/openclaw/issues/13219)** and **[#87441 — Wire diagnostics/memory thresholds to config](https://github.com/openclaw/openclaw/issues/87441)** — observability/cost themes.
- **[#16555 — TTL/expiry for delivery queue messages](https://github.com/openclaw/openclaw/issues/16555)** — pairs naturally with today's delivery-loss bugs (#125764, #161976).
- **[#17840 — Opt-in reaction-triggered agent turns](https://github.com/openclaw/openclaw/issues/17840)** and **[#38714 — Discord reaction events in Hooks](https://github.com/openclaw/openclaw/issues/38714)** — interaction-model expansion.
- **[#66252 — Per-agent TTS/STT overrides](https://github.com/openclaw/openclaw/issues/66252)** — multi-language/multi-agent personalization.

**Closed-today signal:** [#43454 Gateway lifecycle hooks](https://github.com/openclaw/openclaw/issues/43454) closed after passing security review — watch for hooks-based event automation appearing in a subsequent release.

---

## 7. User Feedback Summary

**Pain points (dissatisfaction):**
- **Upgrade/update path is the single most cited frustration.** Multiple users report hosts *stuck* on 2026.9.5/9.6 with update processes in loops, 233 MB+ worker output, or permanent `publishing`/`recovery-pending` states (#156986, #167771, #158231, #164214

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — OpenClaw vs. Hermes Agent  
**Date:** 2026-10-10  
**Data caveat:** Hermes Agent’s digest generation failed, so the comparison is asymmetric. OpenClaw has rich activity data; Hermes has **no usable 24h metrics**. Cross-project conclusions should be treated as provisional.

---

## 1. Ecosystem Overview

The personal AI assistant / agent open-source ecosystem is in a **hardening and reliability phase**, not a feature-release boom. OpenClaw’s snapshot — 500 issues and 500 PRs touched in 24 hours, no new release, and multiple P0 blockers around storage, updater recovery, and gateway lifecycle — shows that always-on personal agents are increasingly judged as production infrastructure. Competitive pressure is shifting from “new agent capability” to **update safety, durable message delivery, memory/embedding quality, context cost, process hygiene, and fleet observability**. Hermes Agent produced no digest today, so its momentum and maturity cannot be validated from this dataset. Still, OpenClaw is a strong leading indicator of where mature agent projects are spending maintenance effort: making long-running agents self-healing rather than adding surface area.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score / Assessment |
|---|---:|---:|---|---|
| **OpenClaw** | **500 updated**; 136

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ Summary generation failed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*