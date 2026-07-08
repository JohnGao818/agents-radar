# OpenClaw Ecosystem Digest 2026-07-08

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-08 02:21 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-08

## 1. Today’s Overview

OpenClaw remains in a high-activity development phase with **500 issues** and **500 PRs** updated in the last 24 hours. Of those PRs, **139 were merged or closed**, signaling strong momentum toward stabilization. No new releases were published today. The project continues to tackle deep structural challenges in session isolation, subagent orchestration, memory management, and security – with several “diamond lobster” rated issues (the highest severity tier) still open. Community engagement is healthy, but many critical bugs remain unassigned or waiting for maintainer decisions. The sheer volume of open items (379 open issues, 361 open PRs) suggests a backlog that may require triage prioritisation.

## 2. Releases

No new releases today. The last known release referenced is `2026.5.20` (based on issue #85333). Users should continue monitoring the [releases page](https://github.com/openclaw/openclaw/releases) for upcoming versions.

## 3. Project Progress

Several notable PRs were merged or closed today:

- **`#98963`** (closed) – Fix `--mcp-config` variadic argument handling (collect all values instead of only first).
- **`#100794`** (closed) – Retry `readdirSync` on transient catalog write race (FsSafeError) during gateway background refresh.
- **`#99576`** (closed) – Add per-session delete button to Control UI sessions view (fixes macOS WebKit confirmation dialog).
- **`#101927`** (open) – Bind Android app chat to a dedicated session, isolating app history from other surfaces.
- **`#101920`** (open) – Self-healing fix for reply-session-init conflict preventing session wedging (fixes #101909).
- **`#101950`** (open) – Reduce tool-result token over-count in mid-turn precheck (fixes #101929).
- **`#101932`** (open) – Prevent stalls when parent token probing hangs during session fork.
- **`#101755`** (open) – Persist Claw artifact provenance refs (SQLite tables for apply records).

Additionally, a wave of cache-cap PRs landed across multiple channels (Mattermost, Feishu, LINE, Google Chat, Slack, Matrix, Telegram, Zalo) – all targeting unbounded in-process Map growth, a systematic reliability improvement.

*[Full PR list](https://github.com/openclaw/openclaw/pulls?q=is%3Apr+updated%3A2026-07-08)*

## 4. Community Hot Topics

### Most Commented Issues

| Issue | Title | Comments | Reactions |
|-------|-------|----------|-----------|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | Text between tool calls leaks to messaging channels | 33 | 👍1 |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | Subagent completion silently lost — no retry, no notification | 21 | 👍1 |
| [#11829](https://github.com/openclaw/openclaw/issues/11829) | Security Roadmap: Protecting API Keys from Agent Access | 20 | 👍0 |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) | Signal daemon stop() race condition on SIGUSR1 restart | 17 | 👍0 |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) | Tiered bootstrap file loading for progressive context control | 17 | 👍0 |
| [#85333](https://github.com/openclaw/openclaw/issues/85333) | `openclaw doctor --fix` 4-5x slower on 2026.5.20 (55s → 229s+) | 15 | 👍1 |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) | Bootstrap files in agentDir silently ignored | 14 | 👍5 |
| [#99241](https://github.com/openclaw/openclaw/issues/99241) | Tool outputs render as image attachments, unreadable to agent | 13 | 👍1 |
| [#39604](https://github.com/openclaw/openclaw/issues/39604) | Feature: `tools.web.fetch.allowPrivateNetwork` | 13 | 👍11 |
| [#43367](https://github.com/openclaw/openclaw/issues/43367) | Multi-agent orchestration unstable: config overwrites, session-lock failures | 13 | 👍1 |

### Analysis

The most heated discussion surrounds **message leakage** (#25592) – internal processing text appearing in user channels, which is a fundamental UX and trust problem. The **subagent silent loss** (#44925) reflects a core reliability gap in the orchestration layer. API key security (#11829) continues to draw attention, indicating enterprise/adoption concerns. The performance regression in `doctor --fix` (#85333) has 15 comments suggesting users are impacted in production. The `allowPrivateNetwork` feature (#39604) has the highest reaction count (11 👍), showing strong demand for controlled private network access.

## 5. Bugs & Stability

### Critical (P1, Diamond Lobster)

| Issue | Summary | Impact | Fix PR? |
|-------|---------|--------|---------|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | Text between tool calls leaks to messaging channels | Security, message loss | PR open (linked) |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | Subagent completion silently lost – no retry/notification | Session state, message loss | PR open (linked) |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) | Signal daemon stop() race condition on SIGUSR1 – orphaned processes | Message loss, crash loop | PR open (linked) |
| [#85333](https://github.com/openclaw/openclaw/issues/85333) | `doctor --fix` 4-5x slower – session snapshot path traversal bottleneck | Session state, crash loop | No fix PR |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) | Bootstrap files in agentDir silently ignored | Session state, security | PR open (linked) |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) | `exec` tool does not inherit `skills.entries.*.env` environment variables | Security, auth-provider | PR open (linked) |
| [#43367](https://github.com/openclaw/openclaw/issues/43367) | Multi-agent orchestration: concurrent agent add/config overwrites, session-lock failures | Session state, message loss, auth-provider | PR open (linked) |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | "Cannot convert undefined or null to object" with google-vertex/gemini-3.1-pro-preview | Auth-provider, crash loop | No fix PR |
| [#41165](https://github.com/openclaw/openclaw/issues/41165) | Telegram DMs still land in agent:main:main after #40519 | Session state, message loss | PR open (linked) |
| [#99241](https://github.com/openclaw/openclaw/issues/99241) | Tool outputs render as image attachments, unreadable to agent | Session state, message loss | No fix PR |

### Notable Regressions

- **#85333**: Performance regression in `doctor --fix` reported as 4-5x slower (stale, no fix).
- **#31583**: `exec` tool env variable inheritance regression.
- **#38327**: Google Vertex/Gemini model crash regression.
- **#43747**: Memory management regression – inconsistent behavior across users.
- **#38439**: Webchat avatar endpoint returns 404 regression.

### Security-Related Bugs

Several open issues involve security exposure: API key leakage (#11829, #31583), private network access (#39604), and bootstrap file ignoring (#29387). The `security audit` PRs (#100945, #100953) aim to address visibility gaps in control-plane exposure and plugin command surfaces.

## 6. Feature Requests & Roadmap Signals

| Issue | Feature | Comments | 👍 | Likely Next Version |
|-------|---------|----------|----|---------------------|
| [#22438](https://github.com/openclaw/openclaw/issues/22438) | Tiered bootstrap file loading | 17 | 0 | Medium – addresses token waste |
| [#39604](https://github.com/openclaw/openclaw/issues/39604) | `tools.web.fetch.allowPrivateNetwork` | 13 | 11 | High – strong demand, clear scope |
| [#42475](https://github.com/openclaw/openclaw/issues/42475) | Per-agent cost budget enforcement | 12 | 1 | Medium – gateway-level |
| [#27445](https://github.com/openclaw/openclaw/issues/27445) | `announceTarget` for sub-agent completion routing | 11 | 5 | Medium – orchestration improvement |
| [#22358](https://github.com/openclaw/openclaw/issues/22358) | Post-subagent completion extension hook | 12 | 1 | Low – hook infrastructure needed |
| [#20786](https://github.com/openclaw/openclaw/issues/20786) | Telegram Business Bot support | 8 | 6 | Medium – niche but popular |
| [#42840](https://github.com/openclaw/openclaw/issues/42840) | MathJax/LaTeX in Control UI | 8 | 9 | High – strong user reaction |
| [#28300](https://github.com/openclaw/openclaw/issues/28300) | Theme customization system | 6 | 5 | Low – cosmetic |
| [#33413](https://github.com/openclaw/openclaw/issues/33413) | Slack tool-level progress in thread status | 8 | 3 | Medium – UX improvement |
| [#42026](https://github.com/openclaw/openclaw/issues/42026) | Distributed Agent Runtime (Control Plane / Agent Runtime split) | 7 | 3 | Long-term – RFC stage |
| [#35203](https://github.com/openclaw/openclaw/issues/35203) | Multi-agent collaboration enhancement (capability profiling, blackboard, etc.) | 10 | 0 | Long-term – RFC |

Predictions for next release:
- **`allowPrivateNetwork`** (#39604) is small, well-defined, and has high community support – likely to land soon.
- **LaTeX rendering** (#42840) is also a relatively contained UI change with strong reactions.
- **Per-agent cost budgets** (#42475) and **announceTarget** (#27445) are important for production operators and may be included as part of the ongoing multi-agent stability push.

## 7. User Feedback Summary

**Pain Points (most frequently expressed):**

1. **Message leakage / UX noise** – Users are frustrated that internal tool execution text (errors, acknowledgements) appears in chat channels (#25592, #39406). This undermines the assistant’s professional appearance.
2. **Subagent reliability** – Silent failures, lost results, and lack of observability when spawning subagents (#44925, #43367) cause users to lose trust in multi-agent workflows.
3. **Memory inconsistency** – Users report completely different memory management behaviors across installations (#43747, #40418). Some see chunking/embedding, others see raw file storage – confusing.
4. **Performance regressions** – `doctor --fix` slowdown (4-5x) is a tangible operational hit for production users (#85333).
5. **Tool output degradation** – Long-running or ANSI-heavy tool outputs being replaced by `(see attached image)` placeholders (#99241, #96857) blinds the agent to its own results.

**Satisfaction signals:**
- High engagement on feature requests (many with 5+ 👍)
- Active PR contributions from the community (e.g., hugenshen landing multiple cache-cap fixes)
- Detailed bug reports with clear reproduction steps show invested users

**Dissatisfaction signals:**
- Multiple P1 diamond lobster bugs have been open for months (e.g., #25592 since Feb)
- Several stable/mature issues marked `needs-maintainer-review` or `needs-product-decision` have not seen progress
- Some bugs labeled `stale` (e.g., #85333, #41744) suggest maintainers may be struggling with triage capacity

## 8. Backlog Watch

### Long-unanswered Important Issues

| Issue | Opened | Last Update | Days Open | Flags |
|-------|--------|-------------|-----------|-------|
| [#11829](https://github.com/openclaw/openclaw/issues/11829) | 2026-02-08 | 2026-07-07 | ~150 | Security roadmap, 20 comments |
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | 2026-02-24 | 2026-07-07 | ~134 | P1, diamond lobster, 33 comments |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) | 2026-02-21 | 2026-07-08 | ~137 | P1, diamond lobster, 17 comments |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) | 2026-02-28 | 2026-07-08 | ~130 | P1, diamond lobster, 14 comments |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) | 2026-03-02 | 2026-07-08 | ~128 | P1, diamond lobster, 13 comments |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | 2026-03-06 | 2026-07-07 | ~124 | P1, diamond lobster, 10 comments |
| [#85333](https://github.com/openclaw/openclaw/issues/85333) | 2026-05-22 | 2026-07-07 | ~47 | Stale, P1, platinum hermit |

### Issues Needing Maintainer Decision

- **#22438** – Tiered bootstrap loading: `needs-product-decision` since Feb 21.
- **#27445** – `announceTarget`: `needs-product-decision` since Feb 26.
- **#40418** – Automated session memory preservation: closed without merge? Needs re-evaluation.
- **#42026** – Distributed Agent Runtime: RFC needs maintainer review and decision.
- **#43454** – Gateway lifecycle hooks: `needs-product-decision` with security review.

### PRs Stuck in Review

- **#14432** – System prompt guidance for sub-agents: opened Feb 12, still `waiting on author`.
- **#101755** – Persist Claw artifact provenance: opened today but already marked `maintainer` – will need attention.
- **#101927** – Android app dedicated session: `waiting on author` for proof.

### Recommendation

Maintainers should prioritise closing the **diamond lobster P1 bugs** that have been open for 4+ months, especially #25592 (message leakage) and #44925 (subagent silent loss), as they erode core trust. The `needs-product-decision` queue also deserves a triage pass to unblock feature development. The systematic cache-cap PRs by hugenshen are a good sign of proactive stability work – similar efforts should be applied to the memory and subagent reliability areas.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is maturing rapidly, with reference implementations like OpenClaw and production-focused forks like Hermes Agent driving parallel innovation. Both projects share core challenges—session isolation, memory management, multi-agent orchestration, and security—but diverge in scope and community governance. The ecosystem is characterized by high issue/PR churn, with hundreds of daily updates, indicating a rapidly evolving yet still unstable foundation. Enterprise adoption is constrained by reliability gaps (e.g., silent subagent failures, message leakage) and performance regressions, while user demand for configurability, private network access, and feedback loops grows.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Open Issues** | 379 | 37 |
| **Open PRs** | 361 | 43 |
| **Issues Updated (24h)** | 500 | 50 |
| **PRs Updated (24h)** | 500 | 50 |
| **PRs Merged/Closed (24h)** | 139 | 7 |
| **Latest Release** | 2026.5.20 (May 20) | v0.18.1 (July 7) |
| **Health Signals** | High severity backlog (10+ P1 diamond lobster), stale critical bugs, strong community but triage bottleneck | Smaller backlog, faster patch cadence, active maintainer response, but some persistent regressions |

**Health Score (subjective):**
- **OpenClaw**: 6/10 – High velocity but drowning in critical bugs; risk of community fatigue.
- **Hermes Agent**: 8/10 – Managed growth with weekly patch releases; better issue-to-resolution ratio.

## 3. OpenClaw’s Position

OpenClaw remains the **core reference implementation**, with a significantly larger community (500 vs 50 daily issue updates) and a broader feature surface (multi-account, subagent orchestration, MCP). Its advantages include deeper architectural exploration (distributed runtime RFC, artifact provenance, tiered bootstrap loading) and a more mature security roadmap (API key protection, private network controls). However, this breadth comes at a cost: OpenClaw suffers from **triage overload**—379 open issues and 361 open PRs, many P1 “diamond lobster” bugs unassigned for months. Hermes Agent, as a fork, benefits from a narrower scope and faster release cycle, but lacks OpenClaw’s ecosystem influence and feature depth.

**Community size comparison:** OpenClaw has ~10x the daily GitHub activity volume. Hermes Agent has a more engaged per-issue discussion rate (3–10 comments per active issue vs. OpenClaw’s 1–33), suggesting a tighter, more responsive community.

## 4. Shared Technical Focus Areas

Both projects independently highlight **three converging requirements**:

| Requirement | OpenClaw Signals | Hermes Agent Signals |
|-------------|-----------------|----------------------|
| **Session isolation & config scoping** | #101927 (Android dedicated session), #43367 (multi-agent config overwrites) | #50404, #54990 (profile config leaks) |
| **Subagent/delegate reliability** | #44925 (silent completion loss), #27445 (announceTarget) | #50199, #18946 (delegate config ignored), #60631 (gateway cron drain) |
| **Feedback/learning loops** | #3506 (durable feedback routing) from Hermes; OpenClaw lacks equivalent feature request (gap) | #27438 (emoji reinforcement), #60556 (feedback routing) |
| **Private network access control** | #39604 (allowPrivateNetwork) – 11 👍 | #34390 (--allowed-hosts for dashboard) – 10 comments |

These patterns indicate that the ecosystem is prioritizing **multi-tenant, production-grade isolation** and **adaptive behavior** as the next frontiers beyond basic chat functionality.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Target user** | Power users / developers self-hosting complex multi-agent setups | Production operators / teams wanting a stable, slimmed-down agent |
| **Feature focus** | Orchestration (subagents, session forking), artifact provenance, gateway-level hooks | Dashboard UX, provider compatibility, minimal install, desktop imprints |
| **Architecture** | Monolithic core with plugin channels; RFC for distributed control/agent split | Forked from OpenClaw; maintains compatibility but trims bloat (e.g., optional skills) |
| **Release cadence** | Monthly-ish (last: May 20) | Weekly patches (v0.18.1 on July 7) |
| **Risk tolerance** | Higher—experimental features (e.g., tiered bootstrap, distributed runtime) in active discussion | Lower—fixes and hardening prioritized; new features require strong community demand |

**Key takeaway:** OpenClaw is the **innovation engine**; Hermes Agent is the **stability fork**. Decision-makers should pick OpenClaw for cutting-edge multi-agent workflows and Hermes Agent for reliable, single-instance deployments.

## 6. Community Momentum & Maturity

- **Tier 1 – High momentum/rapid iteration:** OpenClaw (500+ daily updates, 139 merges/day) but with risk of burnout. Hermes Agent (50 daily updates, 7 merges/day) is slower but more deliberate.
- **Tier 2 – Stabilizing:** Both projects are closing high-severity bugs, but OpenClaw’s critical backlog (10+ P1 issues >4 months old) indicates it is still in a “stabilization struggle” phase. Hermes Agent’s weekly patch releases suggest it is approaching maturity.
- **Maturity indicators:** Hermes Agent has a cleaner backlog and faster fix cycles. OpenClaw has more community-contributed features (e.g., cache-cap PRs, artifact provenance) but lacks maintainer bandwidth to shepherd them.

## 7. Trend Signals

From community feedback across both projects, three industry trends stand out for AI agent developers:

1. **Production isolation is non-negotiable.** Users demand per-session, per-profile, and per-deployment isolation (config, memory, network) to prevent cross-contamination. The “single-tenant” era is ending; multi-tenant awareness (even for single-user setups) is becoming standard.
2. **Feedback-driven adaptation is the next UX leap.** Features like Hermes’ emoji reinforcement and durable feedback routing signal that users want agents to learn from interactions without manual fine-tuning. OpenClaw’s silence on this is a strategic gap.
3. **Security boundaries are shifting inward.** Both communities push for control over private network access, API key protection from agents, and explicit host whitelisting—reflecting a move from “trust the agent” to “trust but verify” at the infrastructure level. This is critical for enterprise adoption.

**For developers:** Invest in session isolation, config scoping, and feedback loops early. The projects that solve orchestration reliability (OpenClaw) and slim stable deployment (Hermes) will dominate the ecosystem.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-07-08

## 1. Today’s Overview

Hermes Agent continues to see high community engagement, with **50 issues** and **50 pull requests** updated in the last 24 hours. **37 issues remain open** (active discussion or awaiting resolution) while **13 were closed**; on the PR side, **43 are open** and **7 have been merged or closed**. A new **v0.18.1 (v2026.7.7)** patch release shipped yesterday, rolling up approximately 660 PRs from the previous week. Activity spans across bug fixes, feature development, and infrastructure hardening, indicating a healthy, fast-moving project. The community is particularly vocal around config isolation, multi-profile support, and delegate-task reliability.

## 2. Releases

**New Release: v0.18.1 (v2026.7.7)**  
[GitHub Release](https://github.com/NousResearch/hermes-agent/releases/tag/v2026.7.7)

- **Type:** Patch release.
- **Scope:** Aggregates ~660 PRs merged since v0.18.0 (July 1), including bug fixes, hardening, and in-progress feature work.
- **Impact:** No breaking changes or migration notes documented; intended as a stable tagged release for downstream consumers (Docker images, PyPI, hosted deployments).

## 3. Project Progress

**Merged/Closed PRs (7 total, notable picks):**

- **#60317** – *fix(environments): profile-aware snapshot store paths + owner-only perms on writes* – fixes stale snapshot paths in multi‑profile runtimes (Dashboard/TUI/cron), closing two related issues.
- **#60285** – *fix(agent): detect same-result tool loops even when args vary* – improves tool-loop guardrails to catch infinite loops where arguments change but result stays constant (e.g., `execute_code` with varying inputs but identical output).
- **#57601** – *fix: forward reasoning_effort for custom providers (GLM-5.2 on ARK)* – ensures `reasoning_effort` config values reach upstream APIs for OpenAI‑compatible custom providers, resolving a silent drop bug.
- **#60317** and **#60285** represent the only two closed PRs listed in the top-20 block. The remaining 5 merged/closed PRs likely address minor doc fixes or duplicate submissions.

## 4. Community Hot Topics

The following issues and PRs generated the most discussion (comments/reactions) and reveal key community needs:

| Item | Comments | Topic | Underlying Need |
|------|----------|-------|----------------|
| **#34390** [Open](https://github.com/NousResearch/hermes-agent/issues/34390) | 10 | `--allowed-hosts` flag for dashboard behind reverse proxy (Tailscale, nginx) | **Security + deployment flexibility** – users need explicit host‑header whitelisting when exposing the dashboard externally. |
| **#19986** [Open](https://github.com/NousResearch/hermes-agent/issues/19986) | 9 | Make non‑core bundled skills optional / minimal default install | **Install size & maintenance burden** – users want a leaner default footprint and control over which skills are loaded. |
| **#6838** [Closed](https://github.com/NousResearch/hermes-agent/issues/6838) | 7 | MiniMax provider connection drops after switching from OpenClaw | **Provider compatibility** – regression after provider migration; community seeking robust error handling for third‑party APIs. |
| **#3506** [Open](https://github.com/NousResearch/hermes-agent/issues/3506) | 3 | Durable feedback routing (memory + skills + follow‑up planning) | **Learning & personalisation** – users want Hermes to remember preferences and adapt behaviour over time without manual tuning. |
| **#60584** [Closed](https://github.com/NousResearch/hermes-agent/issues/60584) | 3 | `hermes chat -q` clears screen and scrollback after response | **UX regression** – one‑shot mode destroys visible output, making it unusable for quick queries. |

## 5. Bugs & Stability

**High‑severity bugs reported today (P1 – P2):**

| ID | Severity | Description | Fix PR Exists? |
|----|----------|-------------|----------------|
| [#60525](https://github.com/NousResearch/hermes-agent/issues/60525) | **P1** | `write_file()` writes invalid JSON/YAML/TOML to disk before syntax check – invalid content is reported as successful. | Yes – PRs [#60629](https://github.com/NousResearch/hermes-agent/pull/60629) and [#60618](https://github.com/NousResearch/hermes-agent/pull/60618) both open. |
| [#60631](https://github.com/NousResearch/hermes-agent/pull/60631) (PR) | **P1** | Gateway shutdown does not drain in‑flight cron jobs, causing silent work loss. | Yes – PR [#60631](https://github.com/NousResearch/hermes-agent/pull/60631) open. |
| [#60543](https://github.com/NousResearch/hermes-agent/issues/60543) | **P2** | `/steer` race condition – out‑of‑band message lost when arriving between tool drain and next API call. | No dedicated fix PR yet. |
| [#60551](https://github.com/NousResearch/hermes-agent/issues/60551) | **P2** | `hermes config set` writes string scalar for list keys, breaking list‑type settings like `terminal.env_passthrough`. | No. |
| [#60584](https://github.com/NousResearch/hermes-agent/issues/60584) (closed) | **P2** | One‑shot mode clears screen/scrollback – resolved (closed). | Already fixed in v0.18.1? Data shows closed. |
| [#60616](https://github.com/NousResearch/hermes-agent/issues/60616) | **P3** | `hermes -z` crashes with SIGABRT when `memory.provider=honcho` after correct response output. | No fix PR yet. |
| [#60597](https://github.com/NousResearch/hermes-agent/issues/60597) | **P2** | UI wrapper crash on Gemini provider when accessing stream response without `read()` – frontend/backend mismatch. | No. |
| [#60603](https://github.com/NousResearch/hermes-agent/issues/60603) | **P2** | `/compress` command not recognized in Desktop UI. | Likely UI routing issue; no fix PR yet. |
| [#60572](https://github.com/NousResearch/hermes-agent/issues/60572) | **P3** | Dashboard spawns MCP server processes unnecessarily, causing duplicates when gateway is also running. | No. |

**Summary:** Today’s bug reports concentrate on **file I/O safety** (P1), **gateway lifecycle** (P1), **command race conditions** (P2), and **cross‑provider compatibility** (P2). At least two high‑severity issues have active fix PRs.

## 6. Feature Requests & Roadmap Signals

Top feature requests from the community (by discussion activity):

- **Dashboard reverse‑proxy support** ([#34390](https://github.com/NousResearch/hermes-agent/issues/34390)) – explicit `--allowed-hosts` flag to safely expose the dashboard behind Tailscale or nginx.
- **Minimal default install** ([#19986](https://github.com/NousResearch/hermes-agent/issues/19986)) – make non‑core skills optional to reduce upgrade weight and clutter.
- **Durable feedback routing** ([#3506](https://github.com/NousResearch/hermes-agent/issues/3506)) – use memory + skills to learn from user feedback across sessions.
- **Emoji reaction reinforcement** ([#27438](https://github.com/NousResearch/hermes-agent/issues/27438)) – leverage 👍/❤️/👎 on messaging platforms as learning signals.
- **Contribution‑driven shell** ([PR #60638](https://github.com/NousResearch/hermes-agent/pull/60638)) – replace desktop’s hardcoded shell with a self‑hosted layout‑tree platform.
- **Dynamic‑workflow orchestration skill** ([PR #59907](https://github.com/NousResearch/hermes-agent/pull/59907)) – re‑landing a previously reverted PR for multi‑step workflow composition.
- **Activity heartbeat** ([PR #60278](https://github.com/NousResearch/hermes-agent/pull/60278)) – background work sessions show as “active” in dashboard/mobile.
- **Desktop imprints** ([PR #60581](https://github.com/NousResearch/hermes-agent/pull/60581)) – one‑tap thumbs up/down with persistent memory.

**Prediction for next version:** The high‑interest `--allowed-hosts` flag (feature request #34390) has strong user demand and no technical blockers, so it may land in v0.18.2. The minimal install feature (#19986) is a longer‑term architectural change but continues to receive attention.

## 7. User Feedback Summary

- **Pain points:**
  - Config isolation is broken – changes in one profile affect all profiles (Discord settings, workspace CWD) – issues [#50404](https://github.com/NousResearch/hermes-agent/issues/50404), [#54990](https://github.com/NousResearch/hermes-agent/issues/54990).
  - Delegation configuration (`delegate_task base_url`, `background`) is ignored at runtime because config caching is stale – issues [#50199](https://github.com/NousResearch/hermes-agent/issues/50199), [#18946](https://github.com/NousResearch/hermes-agent/issues/18946), [#46944](https://github.com/NousResearch/hermes-agent/issues/46944).
  - Gateway crashes on macOS with `SystemExit: 75` (Tempfail) – issue [#45454](https://github.com/NousResearch/hermes-agent/issues/45454) (persists across versions).
  - Discord configuration via config.yaml is silently ignored when env vars are present – issue [#32263](https://github.com/NousResearch/hermes-agent/issues/32263).
  - On Windows, ffmpeg not auto‑discovered for voice features – issue [#60624](https://github.com/NousResearch/hermes-agent/issues/60624).

- **Satisfaction signals:** Users are actively contributing PRs for i18n ([#38846](https://github.com/NousResearch/hermes-agent/pull/38846)), security hardening ([#60636](https://github.com/NousResearch/hermes-agent/pull/60636)), and new features (desktop imprints, contribution‑driven shell). The rapid release cadence (v0.18.1 one week after v0.18.0) suggests maintainers are responsive.

## 8. Backlog Watch

The following open issues and PRs have remained unresolved for an extended period or lack maintainer response, risking community frustration:

| Item | Open Since | Status | Why Watch |
|------|------------|--------|-----------|
| **#19986** – Minimal install / optional skills | 2026-05-05 | Open, no maintainer comment | High community interest (9 comments, 3 👍) but no roadmap commitment. |
| **#3506** – Durable feedback routing | 2026-03-28 | Open, last update 2026-07-08 | Long‑standing feature request with broad implications; still in discussion. |
| **#27438** – Emoji reaction reinforcement | 2026-05-17 | Open, no maintainer response | Low‑effort feature that could significantly improve UX on messaging platforms. |
| **#38846** – i18n PR for 15 desktop locales | 2026-06-04 | Open, no review activity | Large PR (11 new locales) that would benefit a global user base; needs maintainer review. |
| **#45454** – Gateway crash on macOS (EX_TEMPFAIL) | 2026-06-13 | Open, no diagnostic updates | Persists across several releases; users may abandon the platform on macOS. |

---

*Generated from GitHub activity on 2026-07-08. Data sources: issues and PRs updated in the last 24 hours.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*