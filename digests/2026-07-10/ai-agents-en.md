# OpenClaw Ecosystem Digest 2026-07-10

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-10 02:37 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-10

## Today's Overview
OpenClaw shows exceptional community engagement and development velocity, with 500 issues and 500 pull requests updated in the last 24 hours. Of those, 185 issues were closed and 207 PRs were merged or closed, indicating a strong focus on resolving outstanding problems. No new releases were cut today, but the high PR throughput—including several maintainer-driven fixes—suggests a release may be imminent. The project continues to mature through aggressive regression hunting and stability improvements, though several critical P1 bugs remain open for weeks or months, pointing to a bottleneck in maintainer capacity.

## Releases
None — no new versions were published within the last 24 hours.

## Project Progress
207 PRs were merged or closed today. Key merged fixes include:

- **[PR #103260](https://github.com/openclaw/openclaw/pull/103260)** – `fix(xai)`: Align current model catalog and tools for xAI (Grok 4.20, Grok Fast)
- **[PR #103243](https://github.com/openclaw/openclaw/pull/103243)** – `fix(browser)`: Handle managed Chrome spawn errors (EACCES, ENOENT, etc.)
- **[PR #103204](https://github.com/openclaw/openclaw/pull/103204)** – `fix(test)`: Restore OpenRouter and Fireworks live coverage in CI
- **[PR #103183](https://github.com/openclaw/openclaw/pull/103183)** – `fix(gateway)`: Large chat messages no longer stall the Gateway during input sanitization
- **[PR #98090](https://github.com/openclaw/openclaw/pull/98090)** – `fix`: Recover precheck context overflows with measured counts
- **[PR #97939](https://github.com/openclaw/openclaw/pull/97939)** – `feat`: Add Computer Use plugin manifest contract
- **[PR #103259](https://github.com/openclaw/openclaw/pull/103259)** – `fix(ci)`: Build iOS without a named simulator device
- **[PR #103264](https://github.com/openclaw/openclaw/pull/103264)** – `fix(ci)`: Pin Kova timeout signal contract

Several open PRs also advanced important features:

- **[PR #102637](https://github.com/openclaw/openclaw/pull/102637)** – `fix(macos)`: Harden fresh AI onboarding (P0, waiting on author)
- **[PR #101864](https://github.com/openclaw/openclaw/pull/101864)** – `feat(android)`: Manage skills from settings (open, needs proof)
- **[PR #103096](https://github.com/openclaw/openclaw/pull/103096)** – `feat(iOS)`: Privacy screen location controls (open, waiting on author)

## Community Hot Topics
The most active discussions (by comment count) reveal deep concerns about reliability and silent failures:

### 1. Subagent Completion Silently Lost
**[Issue #44925](https://github.com/openclaw/openclaw/issues/44925)** (21 comments, P1, diamond lobster)
> Subagent task orchestration has multiple failure modes where results are silently lost: completion announce fails (E31, E42, E45), no retry, no notification, no auto-restart on timeout. Affects Telegram forum bot users heavily.

### 2. Cron AgentTurn Sends Unsupported Thinking Value
**[Issue #63918](https://github.com/openclaw/openclaw/issues/63918)** (18 comments, P2, closed)
> Cron jobs with `payload.kind=agentTurn` send `thinking=none` to OpenAI models like gpt-5-nano that only accept `minimal`. Causes 400 error. Closed but discussion ongoing.

### 3. Tool Outputs Rendered as Unreadable Image Attachments
**[Issue #99241](https://github.com/openclaw/openclaw/issues/99241)** (15 comments, P1, open)
> In long-running workflows, tool results collapse into `(see attached image)` placeholders, rendering stdout/stderr unreadable to the agent. Similar to closed [#100782](https://github.com/openclaw/openclaw/issues/100782) which reported this for Discord specifically.

### 4. gh-issues Skill Injects Untrusted Data into Sub-Agent Prompts
**[Issue #45740](https://github.com/openclaw/openclaw/issues/45740)** (14 comments, P2, open)
> Raw GitHub issue bodies and review comments are injected directly into sub-agent prompts without sanitization. Security impact rated diamond lobster.

### 5. Per-Agent Memory-Wiki Vault Configuration
**[Issue #63829](https://github.com/openclaw/openclaw/issues/63829)** (12 comments, P1, feature request, 10 👍)
> Users want per-agent isolated knowledge wiki vaults instead of a single global vault. High upvotes indicate strong community demand.

### 6. room_event Destabilizes Prompt Cache
**[Issue #102175](https://github.com/openclaw/openclaw/issues/102175)** (12 comments, P1, regression)
> `room_event` forces `message_tool_only` despite `visibleReplies=automatic`, changing cache keys and destabilizing prompt caching.

**Underlying need:** The community is asking for **reliable, recoverable task execution** and **clear error surfaces** (instead of silent failures or opaque placeholders). Security concerns around injection are also mounting.

## Bugs & Stability
The project has a large open bug inventory. Below are the most severe reported/updated in the last 24h, ranked by priority (P0/P1/P2):

| Issue | Priority | Summary | Fix PR Exists? |
|-------|----------|---------|----------------|
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | P1 | Subagent completion silently lost | No fix PR linked |
| [#99241](https://github.com/openclaw/openclaw/issues/99241) | P1 | Tool outputs rendered as image attachments | No fix PR linked |
| [#100782](https://github.com/openclaw/openclaw/issues/100782) | P1 (closed) | All tool results rendered as images in Discord | No fix PR in issue (but PR [#102341](https://github.com/openclaw/openclaw/pull/102341) addresses Discord rendering) |
| [#89278](https://github.com/openclaw/openclaw/issues/89278) | P1 | Codex OAuth refresh succeeds but cron/heartbeat fail with 10s timeout | No fix PR linked |
| [#49876](https://github.com/openclaw/openclaw/issues/49876) | P1 | Cron sessions deliver hallucinated output on tool failure | No fix PR linked |
| [#52249](https://github.com/openclaw/openclaw/issues/52249) | P1 | ACP parent session stuck until refresh when child completes | No fix PR linked |
| [#84569](https://github.com/openclaw/openclaw/issues/84569) | P1 | WhatsApp session stalls on long model_call, reply never delivered | No fix PR linked |
| [#54155](https://github.com/openclaw/openclaw/issues/54155) | P1 | Gateway memory leak: 389MB → 14.7GB over 4 days | No fix PR linked |
| [#99912](https://github.com/openclaw/openclaw/issues/99912) | P1 (closed) | Agent heartbeat routes to wrong agent's session | No fix PR linked (closed without merge?) |
| [#53540](https://github.com/openclaw/openclaw/issues/53540) | P1 | Embedded runner "Network connection lost" on large tool parameters | No fix PR linked |
| [#43661](https://github.com/openclaw/openclaw/issues/43661) | P0 (closed) | Session hangs indefinitely on compaction timeout, duplicate messages | No fix PR linked |
| [#88870](https://github.com/openclaw/openclaw/issues/88870) | P1 (closed) | Stuck-session recovery aborts long active runs at ~6min | No fix PR linked |
| [#45494](https://github.com/openclaw/openclaw/issues/45494) | P1 | Cron agent jobs silently time out on LLM API outages | No fix PR linked |
| [#46786](https://github.com/openclaw/openclaw/issues/46786) | P1 | `tools.elevated.enabled: true` breaks exec routing logic | No fix PR linked |
| [#94251](https://github.com/openclaw/openclaw/issues/94251) | P1 | Ollama remote provider streaming not consumed | No fix PR linked |
| [#43996](https://github.com/openclaw/openclaw/issues/43996) | P1 | Sandbox container exits immediately with no-new-privileges | No fix PR linked |
| [#44502](https://github.com/openclaw/openclaw/issues/44502) | P1 | Discord routing / mention-gating

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

**Date: 2026-07-10**

---

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem is characterized by extremely high development velocity accompanied by growing pains in reliability and stability. Both OpenClaw and Hermes Agent demonstrate vibrant communities with hundreds of contributions daily, yet both struggle with significant bug backlogs—particularly around task execution, provider integration, and user-facing reliability. The landscape is bifurcating between "core infrastructure" projects (like OpenClaw) that aim to be a universal reference platform, and more focused agent implementations (like Hermes) that optimize for specific user experiences. A shared tension is emerging: rapid feature iteration is outpacing the robustness required for production personal AI assistants, with silent failures, session management issues, and integration regressions recurring across both projects.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues touched (24h)** | 500 | 50 |
| **Issues closed (24h)** | 185 | 16 |
| **Open issue count** | ~315 (inferred) | 34 |
| **PRs touched (24h)** | 500 | 50 |
| **PRs merged/closed (24h)** | 207 | 6 |
| **Releases (24h)** | 0 | 0 |
| **Latest version** | Not stated | v0.18.1 (referenced) |
| **P0/P1 bugs open** | ~18 (multiple P1, 1 P0 closed) | ~3 P1, several P2 |
| **Community health score** | ⚠️ Unstable / High volatility | ⚠️ Moderate / Brittle stability |

**Interpretation:**
- OpenClaw operates at roughly **10x the raw activity volume** of Hermes Agent across all metrics.
- However, OpenClaw also has a proportionally larger open bug inventory and a higher number of critical (P1) issues that have remained unresolved for weeks or months.
- Hermes Agent has a smaller backlog but a higher ratio of regressions relative to its release cadence, suggesting integration fragility.

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale of community:** 500 daily active contributors (versus 50 for Hermes) creates a robust review pipeline and faster time-to-fix for common issues.
- **Platform breadth:** OpenClaw supports iOS, Android, macOS, Browser (Chrome), Gateway, and Discord/Telegram/WhatsApp—significantly wider than Hermes's Desktop + Slack/WeCom/QQBot focus.
- **Integration depth:** Active model catalog alignment (Grok 4.20, Grok Fast), Computer Use plugin contract, and CI coverage for OpenRouter/Fireworks indicate an intentional strategy to be the universal reference implementation.
- **Stability investment:** The 207 PRs merged today include fixes for Chrome spawn errors, Gateway sanitization stalls, precheck context overflows, and iOS CI builds—showing systematic regression hunting.

**Technical Approach Differences:**
- OpenClaw: **Gateway-centric architecture** with a sandbox runtime, subagent orchestration, and memory-wiki vaults. Heavier emphasis on task management and session persistence.
- Hermes Agent: **Desktop-first agent** with rule enforcement, reasoning effort controls, and multiplex provider profiles. Lighter infrastructure, more focused on end-user configuration.

**Community Size Comparison:**
- OpenClaw clearly commands the larger contributor base and issue volume, suggesting broader adoption and more third-party integrators.
- Hermes's 20 upvotes on the "remote agent + local tools" feature request indicates a passionate but smaller power-user community.

---

## 4. Shared Technical Focus Areas

Both projects independently surfaced the same class of reliability and safety concerns, indicating these are ecosystem-wide priorities:

| Focus Area | OpenClaw Evidence | Hermes Agent Evidence |
|------------|-------------------|------------------------|
| **Silent task failures** | Subagent results silently lost (#44925, P1); Cron jobs hallucinate output on tool failure (#49876, P1) | Cron store overwritten across profiles (#61768, P1); Agent violates stored rules (#60429, fixed) |
| **Provider integration fragility** | Ollama remote not consumed (#94251); OpenRouter "Unknown" app; ZAI cascade key exhaustion | QQBot infinite reconnect loop (#52914); ZAI key exhaustion (#61487); Nous inference unreachable (#60715) |
| **Rule/safety enforcement** | Untrusted GitHub data injected into prompts (#45740, P2, security); Tool outputs unreadable (#99241) | Rule enforcement fixed (#61805); Vietnamese diacritics rendering (#61804); Dark theme detection (#61803) |
| **Session/stability issues** | Memory leak 389MB→14.7GB (#54155); Heartbeat routing to wrong session (#99912); Stuck sessions (#88870, #43661) | Dashboard WebSocket regression (#61696); Pinned sessions vanish (#51685) |
| **Cross-platform rendering** | Discord tool results as images (#100782); Cron agentTurn thinking value error (#63918) | WeCom image upload not cached (#61762); Slack rich_blocks null error (#56615) |

**Cross-cutting requirements:**
1. **Retry and recovery mechanisms** for subagent and cron tasks
2. **Sanitization and safety layers** for injected data (GitHub bodies, tool outputs)
3. **Unified provider error handling** (quota exhaustion, timeouts, endpoint switching)
4. **Platform-specific rendering fidelity** (Discord, Slack, WeCom, QQBot)
5. **Session-level isolation** (per-agent memory, profile separation)

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary role** | Universal reference platform / infrastructure | Purpose-built personal agent for end-users |
| **Target user** | Developers, third-party integrators, open-source contributors | Power users, desktop-first, multi-instance deployments |
| **Architecture** | Gateway + sandbox + subagent orchestration | Desktop app + provider profiles + tool execution |
| **Platform support** | iOS, Android, macOS, Browser, Discord, Telegram, WhatsApp, Slack | Desktop (Electron), Slack, WeCom, QQBot |
| **Feature focus** | Model catalog alignment, CI infrastructure, session management, plugin contracts | Rule enforcement, reasoning effort controls, visual configuration, provider switching |
| **Key differentiator** | Breadth of integrations and scale of community | User experience polish (themes, diagnostics, multiplex profiles) |
| **Weakness** | Large P1 bug inventory, maintainer bottleneck, long-standing unresolved issues | Regression fragility after releases, smaller contributor base, limited platform reach |

**Strategic takeaway:**
- OpenClaw is positioning as the **kernel of the AI agent OS**—the reference that others build on.
- Hermes Agent is optimizing for **consumption**—making agent behavior predictable and configurable for non-developer power users.
- The two could be complementary: Hermes could reduce regressions by leveraging OpenClaw's gateway/sandbox stack, while OpenClaw could adopt Hermes's rule enforcement and reasoning controls.

---

## 6. Community Momentum & Maturity

**Activity Tiers:**

| Tier | Projects | Characteristics |
|------|----------|-----------------|
| **Rapidly iterating** (beta/volatile) | OpenClaw | 500 daily contributions, high PR throughput, aggressive bug hunting, but unresolved P1s linger for weeks |
| **Consolidating** (post-release stabilization) | Hermes Agent | 50 daily contributions, active regression fixing, but visible integration fragility from v0.18.1 |

**Maturity Assessment:**

- **OpenClaw:** Demonstrates **pre-1.0 momentum**—the project ships fixes rapidly but lacks the capacity to close all critical bugs. The ratio of merged PRs to open P1 bugs (~207:18) suggests that the maintainer team prioritizes volume over depth. A release appears imminent given the high closure rate.
- **Hermes Agent:** Appears to be in a **stabilization phase** after v0.18.1, with maintainers (`vystartasv`) focused on regression fixes. However, growing backlog (34 open issues) and lack of maintainer response on long-standing feature requests (69-day-old #18715, 60-day-old #23524) could dampen community enthusiasm if not addressed.

**Risk Signals:**
- OpenClaw: Maintainer bottleneck on P1 bugs; community may start forking if critical issues (silent failures, security injection) remain unfixed.
- Hermes Agent: Regression density suggests insufficient integration testing before releases; may lose power-user trust if WeCom/QQBot/Desktop bugs persist.

---

## 7. Trend Signals

The following industry trends are extractable from the community feedback in both projects:

### 1. The Reliability Paradox
> *"Subagent completion silently lost"* (OpenClaw #44925) + *"Cron store overwritten across profiles"* (Hermes #61768)

Users demand **anthropic-level reliability** (i.e., tasks always complete or clearly fail) from open-source agents. Silent failures, hallucinated outputs, and corrupted state are the top pain points. **For AI agent developers:** invest in observability, retry policies, and explicit failure surface area (error codes, notifications).

### 2. Provider Fragmentation is Accelerating
> OpenClaw supports xAI (Grok), Ollama, OpenRouter, Fireworks, ZAI; Hermes supports Nous, Gemini via Antigravity, OpenRouter, ZAI

The ecosystem is fragmenting across 10+ providers, each with unique API semantics (thinking values, endpoint patterns, quota models). **For developers:** build an abstraction layer that normalizes provider behavior (rate limits, error codes, streaming) rather than hard-coding integration logic.

### 3. Security is an Afterthought
> *"gh-issues skill injects untrusted data into sub-agent prompts"* (OpenClaw #45740, P2)

Both projects have injection vulnerabilities (GitHub bodies, tool outputs as images) that could be exploited for prompt injection or data exfiltration. **For AI agent developers:** treat all external data (GitHub, Slack, tool stdout) as untrusted and apply sanitization layers by default.

### 4. Multi-Instance and Isolation is a Core Requirement
> *"Per-Agent Memory-Wiki Vault Configuration"* (OpenClaw #63829, 10 👍) + *"Remote agent + local tools"* (Hermes #18715, 20 👍)

Users want **per-agent or per-profile isolation** (memory, cron, tools) rather than global state. **For developers:** design storage, session, and execution contexts as tenant-aware from the start.

### 5. Desktop UX is Still Breaking
> *"Pinned sessions disappear"* (Hermes #51685) + *"vision_analyze ignores config"* (#48269) + *"Dashboard WebSocket regression"* (#61696)

The Desktop client remains a consistent source of regressions, suggesting that **UI-as-integration-point** is harder to stabilize than backend services. **For developers:** consider separating frontend and backend lifecycles, or investing heavily in end-to-end testing for every UI release.

### 6. Reasoning Configuration is Evolving
> *"Auto reasoning mode"* (Hermes #40306) + *"Per-cron reasoning effort"* (#23524) + *"Cron agentTurn thinking value"* (OpenClaw #63918)

Users want dynamically adjustable reasoning effort, not just static "high/low/minimal" toggles. **For developers:** build reasoning as a configurable pipeline stage (auto-detect complexity, per-task override) rather than a binary switch.

---

## Summary Recommendation

**For technology decision-makers:**
- **If building on OpenClaw:** Plan for a **stability buffer**—expect unresolved P1 bugs for 2-4 weeks and build your own retry/recovery mechanisms on top. The project’s value is in integration breadth and community velocity, not production readiness.
- **If building on Hermes Agent:** Expect **regressions after minor releases**—pin versions strictly and invest in provider-agnostic error handling. Hermes's rule enforcement and reasoning controls are ahead of OpenClaw for end-user-facing deployments.

**Cross-project collaboration opportunity:** A joint working group on **task reliability and error surface standardization** (retry semantics, failure notifications, session isolation) would benefit both projects and the broader ecosystem.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Project Digest: Hermes Agent — 2026-07-10

## 1. Today’s Overview
The Hermes Agent project shows high activity today with 50 issues and 50 PRs touched in the last 24 hours. The community is heavily engaged in bug reporting and feature discussion, while the maintainers have merged several fixes targeting rule enforcement, code-block rendering, and theme compatibility. No new releases were published today. The **open issue count remains high (34)**, and the ratio of **closed vs. open items is low for both issues (16/50) and PRs (6/50)**, indicating a growing backlog that may require prioritisation.

## 2. Releases
**None** – no new versions were released today. The latest available version appears to be v0.18.1 (referenced in bug reports).

## 3. Project Progress
Six pull requests were merged or closed today, all authored by user `vystartasv`. These primarily address reported bugs:

- [#61805 [CLOSED]](https://github.com/NousResearch/hermes-agent/pull/61805) – **Rule enforcement**: Fixes agent violating behavioural rules by injecting stored rules into the system prompt during skill execution.
- [#61804 [CLOSED]](https://github.com/NousResearch/hermes-agent/pull/61804) – **Vietnamese diacritics in code blocks**: Adds Noto Sans Mono as a fallback monospace font for better non-Latin Unicode coverage.
- [#61803 [CLOSED]](https://github.com/NousResearch/hermes-agent/pull/61803) – **Zed dark themes**: Changes background detection to ignore inherited `COLORFGBG` when the terminal background is actually dark.
- [#61698 [CLOSED]](https://github.com/NousResearch/hermes-agent/pull/61698) – **Noisy probes to non-OpenAI endpoints**: Stops Hermes from making spurious `GET` requests to `/api/tags`, `/v1/props`, etc. when using an OpenAI provider.
- [#61696 [CLOSED]](https://github.com/NousResearch/hermes-agent/pull/61696) – **Dashboard WebSocket regression**: Fixes blank session rendering after a recent WebSocket change.
- [#61695 [CLOSED]](https://github.com/NousResearch/hermes-agent/pull/61695) – **Gateway multiplex profile model error**: Ensures secret retrieval runs in the correct scope when `multiplex_profiles` is used.

Additionally, several open PRs may be merge candidates soon: [#61813](https://github.com/NousResearch/hermes-agent/pull/61813) (cron profile isolation), [#61812](https://github.com/NousResearch/hermes-agent/pull/61812) (ACP tool-generation status), and [#61811](https://github.com/NousResearch/hermes-agent/pull/61811) (another fix for Vietnamese diacritics).

## 4. Community Hot Topics
The most discussed issues and PRs this period reflect strong interest in **multi‑instance setups**, **provider reliability**, and **rule compliance**.

| Issue/PR | Comments | Reactions | Summary |
|----------|----------|-----------|---------|
| [#52914](https://github.com/NousResearch/hermes-agent/issues/52914) [CLOSED] | 17 | 👍 6 | **QQBot infinite retry loop** – After an update, the QQBot gateway enters an infinite reconnect loop because `is_reconnect` parameter is missing. |
| [#18715](https://github.com/NousResearch/hermes-agent/issues/18715) [OPEN] | 8 | 👍 20 | **Remote agent + local tool execution** – Users want to run a remote Hermes instance while keeping tools local. High 👍 count signals strong demand for this architecture. |
| [#61487](https://github.com/NousResearch/hermes-agent/issues/61487) [CLOSED] | 5 | – | **ZAI provider cascade‑marks all keys** – A per‑key quota exhaustion causes every key in the pool to be incorrectly marked as exhausted. |
| [#61099](https://github.com/NousResearch/hermes-agent/issues/61099) [CLOSED] | 4 | – | **OpenRouter “Unknown” App** – Hermes requests intermittently show as “Unknown” in OpenRouter logs. |
| [#60429](https://github.com/NousResearch/hermes-agent/issues/60429) [OPEN] | 4 | – | **Agent violating rules** – Saved rules are not enforced during skill execution (now fixed in #61805). |
| [#47828](https://github.com/NousResearch/hermes-agent/issues/47828) [CLOSED] | 4 | – | **`/mode` model switch keeps old provider’s endpoint** – post-switch requests hit the previous provider’s base URL. |

**Underlying needs**: The community is demanding more robust identity/routing support (remote agents, provider switching) and more resilient provider integrations (QQBot, ZAI, OpenRouter). The 20 👍 on feature request #18715 indicates this is a highly desired capability.

## 5. Bugs & Stability
Several high‑severity bugs were reported or updated today. The most critical are:

- **P1**: [#61768](https://github.com/NousResearch/hermes-agent/issues/61768) – **Cross‑profile cron‑store overwrite** – On multi‑profile desktop setups, one profile’s cron jobs can be destructively cloned into another’s. A fix PR [#61813](https://github.com/NousResearch/hermes-agent/pull/61813) is open.
- **P2**: [#60715](https://github.com/NousResearch/hermes-agent/issues/60715) – **Nous inference API timeout** – The Nous Portal inference endpoint is completely unreachable from the reporter’s environment.
- **P2**: [#61762](https://github.com/NousResearch/hermes-agent/issues/61762) – **WeCom image upload not perceived** – Images sent to WeCom Bot are not saved to cache, causing “please send the image” loops.
- **P3**: [#60429](https://github.com/NousResearch/hermes-agent/issues/60429) – **Agent violates rules** (now fixed in #61805).
- **P3**: [#48269](https://github.com/NousResearch/hermes-agent/issues/48269) – `vision_analyze` ignores `config.yaml` changes in Electron build.
- **P3**: [#51685](https://github.com/NousResearch/hermes-agent/issues/51685) – **Pinned sessions disappear from Desktop sidebar** when they fall off the loaded page.
- **P3**: [#56615](https://github.com/NousResearch/hermes-agent/issues/56615) – **Slack rich_blocks fail** due to `null` column_settings.

Several P1/P2 bugs were closed in the last 24 hours (e.g., #60794, #61145, #47828), indicating active triage.

## 6. Feature Requests & Roadmap Signals
New and trending feature requests suggest the community is focused on **better reasoning control**, **provider expansion**, and **UI management**:

- [#52657](https://github.com/NousResearch/hermes-agent/issues/52657) – **Gemini via Antigravity** (3 👍) – Support for Gemini Pro subscription through the Antigravity provider.
- [#40306](https://github.com/NousResearch/hermes-agent/issues/40306) – **Auto reasoning mode** (1 comment) – Automatically choose low/medium/high reasoning effort based on query complexity (like ChatGPT).
- [#23524](https://github.com/NousResearch/hermes-agent/issues/23524) – **Per‑cron reasoning effort** (3 comments) – Override reasoning effort per scheduled job.
- [#35410](https://github.com/NousResearch/hermes-agent/issues/35410) – **RP‑initiated logout** (3 comments) – Dashboard logout should terminate the IdP session.
- [#53521](https://github.com/NousResearch/hermes-agent/issues/53521) – **Plugin management UI** – Add a graphical plugin manager to Hermes Desktop.

**Predictions**: Auto‑reasoning (#40306) and Gemini integration (#52657) are likely candidates for the next minor release, given their user appeal and alignment with the existing provider framework. The plugin UI (#53521) may be deferred to a later UI overhaul.

## 7. User Feedback Summary
Real pain points expressed in today’s issues:

- **Rule enforcement is unreliable** – Users report that the agent does not always follow stored rules, undermining trust (#60429). The merged fix #61805 should alleviate this.
- **Desktop visualisation is broken** – Pinned sessions disappear (#51685), vision configuration is ignored (#48269), and assistant responses are truncated (#61807). These are impacting daily use of the Desktop client.
- **Provider switching is fragile** – `/mode` switches preserve old endpoints (#47828) and cron store data is corrupted across profiles (#61768).
- **Platform‑specific regressions** – QQBot (infinite loop #52914), WeCom (image handling #61762), Slack (rich_blocks #56615), and Discord (blocking SQLite #60794) all show recent regressions, suggesting integration instability after the v0.18.1 update.
- **Desired architecture**: The high upvotes on #18715 (remote agent + local tools) indicate that many users want to decouple the agent’s runtime from tool execution, a pattern that would enable more flexible deployment.

Overall, sentiment is mixed: users appreciate active bug fixing, but the volume of regressions points to a need for more thorough integration testing before releases.

## 8. Backlog Watch
The following important issues and PRs have remained open for an extended period without maintainer response or resolution:

| Issue/PR | Age | Comments | Impact |
|----------|-----|----------|--------|
| [#18715](https://github.com/NousResearch/hermes-agent/issues/18715) (Remote agent + local tools) | 69 days | 8 | High community interest (20 👍); no apparent maintainer comment. |
| [#35410](https://github.com/NousResearch/hermes-agent/issues/35410) (OIDC RP‑initiated logout) | 41 days | 3 | Security‑adjacent; no maintainer follow‑up. |
| [#23524](https://github.com/NousResearch/hermes-agent/issues/23524) (Per‑cron reasoning effort) | 60 days | 3 | Valuable for power users; not yet acknowledged. |
| [#40306](https://github.com/NousResearch/hermes-agent/issues/40306) (Auto reasoning mode) | 34 days | 1 | Could simplify user experience; no comment from team. |
| [#48269](https://github.com/NousResearch/hermes-agent/issues/48269) (vision_analyze ignores config) | 22 days | 1 | Annoying Desktop bug; no fix proposed. |
| [#51685](https://github.com/NousResearch/hermes-agent/issues/51685) (Pinned sessions vanish) | 16 days | 3 | Directly affects Desktop usability; no response. |

The lack of maintainer engagement on long‑standing feature requests and confirmed bugs is a concern for project health. Prioritising these would improve community trust and reduce frustration.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*