# OpenClaw Ecosystem Digest 2026-07-11

> Issues: 429 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-11 02:12 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-07-11

## 1. Today’s Overview
Project activity remains very high, with **429 issues and 500 PRs updated in the last 24 hours**. Of these, 236 issues are open/active and 314 PRs are open. Community engagement is strong, but critical stability problems persist – especially a severe gateway memory leak (RSS grows to 15.5 GB) and a prompt‑cache regression that breaks across session boundaries. No new releases were published today. The large number of open PRs (some with high risk tags) suggests the maintainer team is actively reviewing and merging, but several long‑standing feature requests and security‑related issues are still awaiting maintainer decisions.

## 2. Releases
**None** – no new versions or tags were published today.

## 3. Project Progress
Today **186 PRs were merged or closed**, though details of those specific closures are not available from the top‑30 snapshot (all listed PRs are open at the time of analysis). Notable open PRs that advanced include:

- **fix(memory‑wiki): stop duplicate bridge imports under polling** ([#91828](https://github.com/openclaw/openclaw/pull/91828)) – addresses memory exhaustion in large bridge‑mode vaults; now ready for maintainer look.
- **fix(gateway): enforce plugin‑ownership check in sessions.patch** ([#103534](https://github.com/openclaw/openclaw/pull/103534)) – closes a security gap where one plugin could mutate another plugin’s sessions.
- **fix(ui): chat workspace rail and detail panel break narrow panes** ([#104033](https://github.com/openclaw/openclaw/pull/104033)) – UX fix for narrow split‑view windows.
- **feat(codex): supervise native Codex sessions** ([#104045](https://github.com/openclaw/openclaw/pull/104045)) – large PR enabling management of Codex‑discovered sessions.
- **feat: enforce agent‑scoped usage budgets** ([#104060](https://github.com/openclaw/openclaw/pull/104060)) – new cost guardrail at the runtime boundary.
- **fix(discord): stop retrying non‑idempotent sends** ([#103867](https://github.com/openclaw/openclaw/pull/103867)) – prevents duplicate messages after transport failures.
- **feat(webui): reintroduce opt‑in AI purpose titles for tool calls** ([#103989](https://github.com/openclaw/openclaw/pull/103989)) – addresses a UX regression from a previous always‑on feature.

## 4. Community Hot Topics
The most active issues by comment count (20–15 comments) reflect deep community concern about reliability and security:

| Issue | Comments | Reactions (👍) | Summary |
|-------|----------|----------------|---------|
| [#99241](https://github.com/openclaw/openclaw/issues/99241) | 20 | 2 | Tool outputs become image attachments, invisible to agent (P1) |
| [#102175](https://github.com/openclaw/openclaw/issues/102175) | 16 | 1 | Prompt cache breaks across room‑event / policy / Responses boundaries (P2 regression) |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | 15 | 4 | Masked Secrets – prevent agent from seeing raw API keys (P1 enhancement) |
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | 15 | 1 | Gateway memory leak 350 MB → 15.5 GB over days (P0) |
| [#12602](https://github.com/openclaw/openclaw/issues/12602) | 14 | 0 | Slack Block Kit support for richer messages (P2) |
| [#63829](https://github.com/openclaw/openclaw/issues/63829) | 13 | 10 | Per‑agent memory‑wiki vault configuration (closed, but heavily upvoted) |

The **memory leak (#91588)** and the **tool‑output invisibility (#99241)** are the most discussed and highest‑priority issues. The **Masked Secrets (#10659)** request continues to attract attention, indicating that prompt‑injection protection is a top community concern.

## 5. Bugs & Stability
Several critical and high‑severity bugs were active today:

| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| **P0** | [#91588](https://github.com/openclaw/openclaw/issues/91588) | Gateway memory leak, RSS climbs to 15.5 GB, OOM kills | No linked PR yet |
| **P0** | [#101763](https://github.com/openclaw/openclaw/issues/101763) | Hosted Molty model selector sends dot‑separated id, API fails | Not yet |
| **P1** | [#99241](https://github.com/openclaw/openclaw/issues/99241) | Tool outputs become unreadable image attachments | Not yet |
| **P1** | [#84569](https://github.com/openclaw/openclaw/issues/84569) | WhatsApp session stalls on long model call, reply never delivered | [#84569](https://github.com/openclaw/openclaw/issues/84569) has linked PR (open) |
| **P1** | [#83959](https://github.com/openclaw/openclaw/issues/83959) | Codex app‑server startup retries exhaust before replacement ready | Linked PR open |
| **P1** | [#87109](https://github.com/openclaw/openclaw/issues/87109) | Gateway heap grows to 1073 MB+ at idle, cron jobs silently fail | Not yet |
| **P1** | [#99681](https://github.com/openclaw/openclaw/issues/99681) | Discord plugin does not auto‑reconnect after WS 1006 close | Not yet |
| **P1** | [#68691](https://github.com/openclaw/openclaw/issues/68691) | Sandbox zombie processes accumulate under PID 1 | Closed, but may re‑emerge |
| **P2** | [#102175](https://github.com/openclaw/openclaw/issues/102175) | Prompt cache breaks across boundaries (regression) | Not yet |
| **P2** | [#44749](https://github.com/openclaw/openclaw/issues/44749) | Concurrent `allow‑always` approvals lose entries (race condition) | Closed without fix? Re‑examining |
| **P2** | [#78362](https://github.com/openclaw/openclaw/issues/78362) | Control UI CSP blocks Zod Function() constructor (closed) | Closed, but might reappear |
| **P3** | [#91283](https://github.com/openclaw/openclaw/issues/91283) | `minSecurity` inverted – `full` treated as most restrictive | Closed |

**Key stability concern**: The gateway memory leak (#91588) has no fix PR yet, and the prompt‑cache regression (#102175) could affect long‑running sessions. The Discord disconnect issue (#99681) also remains unresolved.

## 6. Feature Requests & Roadmap Signals
The most‑requested features today (by comment count and upvotes) indicate strong demand for:

- **Masked Secrets** ([#10659](https://github.com/openclaw/openclaw/issues/10659)) – Agent cannot see raw API keys (P1, 15 comments, 4 👍)
- **Per‑agent memory‑wiki vault** ([#63829](https://github.com/openclaw/openclaw/issues/63829)) – isolated knowledge wikis per agent (P1, 13 comments, 10 👍) – *closed but may be planned*
- **Slack Block Kit support** ([#12602](https://github.com/openclaw/openclaw/issues/12602)) – rich interactive messages (P2, 14 comments)
- **Streaming TTS pipeline for voice calls** ([#8355](https://github.com/openclaw/openclaw/issues/8355)) – sentence‑level LLM→TTS→audio (P2, 6 comments, 2 👍)
- **Filesystem sandboxing config** ([#7722](https://github.com/openclaw/openclaw/issues/7722)) – `tools.fileAccess` (P2, 11 comments, 4 👍)
- **Group session consolidation** ([#7524](https://github.com/openclaw/openclaw/issues/7524)) – `groupScope` option (P2, 6 comments, 4 👍)
- **Batch API support** ([#9865](https://github.com/openclaw/openclaw/issues/9865)) – cost savings for background tasks (P2, 5 comments)
- **Multi‑lane sub‑agent concurrency** ([#10467](https://github.com/openclaw/openclaw/issues/10467)) – separate queues per lane (P2, 5 comments)

**Prediction**: **Masked Secrets** and **per‑agent memory‑wiki** are likely candidates for the next minor release given their P1 priority and high engagement. Streaming TTS and Slack Block Kit are also strong contenders for a subsequent feature‑rich release.

## 7. User Feedback Summary
Community sentiment is **mixed** – enthusiasm for OpenClaw’s extensibility is tempered by frequent reliability issues.

**Common pain points**:
- **Memory leaks and OOM crashes** (#91588, #87109, #68691) – users report gateway restarts multiple times per week.
- **Silent message loss** (#99241, #84569, #85714, #99681) – agents cannot read tool outputs, WhatsApp replies never delivered, Discord messages drop.
- **Configuration fragility** – OAuth token refresh lacks retry (#8673), provider cooldowns block users after billing recovery (#70903), webhook session keys ignored (#11665).
- **Missing integrations** – Slack Block Kit, WhatsApp stickers/call events, Feishu pagination bug (#93928), iOS location permission (#86217).
- **Security gaps** – agent can see plaintext API keys (#10659), no filesystem sandbox (#7722), race condition in approval allowlist (#44749).

**Positive signals**:
- High issue and PR volume indicates an active and invested user base.
- Several feature requests have large upvotes (#63829 with 10 👍, #10659 with 4 👍).
- Users are willing to file detailed bug reports with logs and reproduction steps, which aids maintainers.

## 8. Backlog Watch
Long‑standing issues that have not received maintainer action or decision:

| Issue | Created | Comments | Priority | Status |
|-------|---------|----------|----------|--------|
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | 2026-02-06 | 15 | P1 | Needs product decision & security review |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) | 2026-02-03 | 11 | P2 | Needs product decision & security review |
| [#9409](https://github.com/openclaw/openclaw/issues/9409) | 2026-02-05 | 9 | P2 | Needs product decision |
| [#8299](https://github.com/openclaw/openclaw/issues/8299) | 2026-02-03 | 9 | P2 | Needs product decision |
| [#7476](https://github.com/openclaw/openclaw/issues/7476) | 2026-02-02 | 7 | P2 | Needs product decision |
| [#7524](https://github.com/openclaw/openclaw/issues/7524) | 2026-02-02 | 6 | P2 | Needs product decision & security review |
| [#8355](https://github.com/openclaw/openclaw/issues/8355) | 2026-02-03 | 6 | P2 | Needs product decision |
| [#6890](https://github.com/openclaw/openclaw/issues/6890) | 2026-02-02 | 6 | P2 | Needs product decision |
| [#12602](https://github.com/openclaw/openclaw/issues/12602) | 2026-02-09 | 14 | P2 | Needs product decision |
| [#11665](https://github.com/openclaw/openclaw/issues/11665) | 2026-02-08 | 11 | P2 | Needs product decision & security review |

Additionally, the **gateway memory leak (#91588, P0, since June 9)** has

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent Open-Source Ecosystem
**Date: 2026-07-11**  
**Projects Analyzed: OpenClaw, Hermes Agent**

---

## 1. Ecosystem Overview

The personal AI assistant and agent open-source ecosystem is experiencing rapid growth, with two major reference implementations—OpenClaw and Hermes Agent—driving innovation in autonomous task execution, multi-platform integration, and context-aware reasoning. Daily activity across both projects exceeds 500 combined issues and PRs, reflecting a deeply engaged developer community. However, the ecosystem faces maturation challenges: critical stability issues (memory leaks, session corruption) coexist with sophisticated feature requests around credential security, multi-agent coordination, and cost governance. The trajectory suggests a shift from rapid feature prototyping toward hardening production-grade reliability and enterprise-grade access controls.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues Updated (24h)** | 429 (236 open) | 50 (3 closed today) |
| **PRs Updated (24h)** | 500 (314 open) | 50 (12 merged/closed today) |
| **Release Status** | No release today | No release today (latest v0.18.2, 2026-07-07) |
| **Critical Bugs (P0/P1)** | 7 (including P0 memory leak, P0 model selector bug) | 3 P2 (e.g., LSP leak, background fork skill loss) |
| **Community Engagement** | High: 20+ comments on top issues, 10+ upvotes on feature requests | Moderate: 7 comments max, thoughtful requests but fewer reactions |
| **Maintainer Responsiveness** | Active merging (186 PRs closed) but many long-standing decisions pending | Responsive: same-day fix PRs for several bugs |
| **Health Score (Subjective)** | 6.5/10 – High energy but critical stability risks | 7.5/10 – Smaller scale but more stable iteration |

**Key Insight:** OpenClaw operates at a much larger scale (8x issues, 10x PRs) but carries more unresolved critical bugs. Hermes Agent is leaner and more focused, with faster turnaround on reported issues.

---

## 3. OpenClaw’s Position

- **Advantages Over Peers**  
  - **Extensibility**: Plugin-based architecture supports deep integrations (Discord, WhatsApp, Slack, Codex) – broader than Hermes Agent’s current scope.  
  - **Scale of community**: 10x the issue/PR volume indicates a larger contributor base and faster feature velocity.  
  - **Core reference status**: OpenClaw is the “core reference” implementation, likely driving upstream standards for agent runtime patterns (session management, memory-wiki, gateways).

- **Technical Approach Differences**  
  OpenClaw uses a gateway-centric runtime with plugin ownership checks and per-agent vaults, whereas Hermes Agent leans on a Desktop/TUI-first design with a lighter gateway layer. OpenClaw’s memory leak (15.5GB RSS) and prompt-cache regression highlight complexity risks from its more modular but less bounded architecture.

- **Community Size Comparison**  
  OpenClaw’s 429 issues vs Hermes’ 50, and 500 PRs vs 50, suggests an **~8–10x larger active community**. However, OpenClaw’s heavily upvoted feature requests (e.g., per-agent vault: 10 👍) indicate a vocal power-user base, while Hermes’ community is smaller but more focused on usability polish.

---

## 4. Shared Technical Focus Areas

Both projects are converging on several key requirements:

| Area | OpenClaw | Hermes Agent |
|------|----------|--------------|
| **Memory/Resource Leaks** | Gateway leak (P0), heap growth at idle (P1) | LSP subprocess leak (P2), MCP server leak (P2) |
| **Credential Security** | Masked Secrets (P1, #10659) – prevent agent from seeing API keys | Prompt-injection scanners miss variants (P2, #27284) |
| **Context Management** | Prompt cache breaks across boundaries (P2, #102175) | Two-phase pruning requested (#513), compaction corruption (closed) |
| **Platform Integration Polish** | Discord reconnect, WhatsApp session stalls, Slack Block Kit | Teams typing indicator stuck, email subject hardcoded, Signal truncation |
| **Multi-Agent Coordination** | Sub-agent concurrency, group session consolidation | Per-subagent model override, per-profile tab lease |
| **Configuration Persistence** | OAuth token refresh, provider cooldowns | Dashboard rewrites custom providers, Bedrock wizard incomplete |

**Emerging shared need:** Robust, user-controllable context pruning (two-phase compaction) and environment-agnostic credential shielding are becoming table stakes for production agent systems.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary Interface** | Gateway/API-driven (multi-platform bots, codex) | Desktop + TUI + terminal (developer-facing) |
| **Target User** | Platform operators, automation engineers | Individual power users, developers (e.g., coding assistants) |
| **Key Deployment Model** | Server-side gateway (bridge-mode, plugins) | Local desktop app with optional gateway |
| **Architecture** | Plugin-based, memory-wiki, strict session ownership | Lightweight RPC, inline context compaction, browser tools |
| **Feature Levers** | Cost budgets, agent-scoped budgets, batch APIs | Approval hooks, volatile skills, pricing overrides |
| **Stability Priority** | Functionality breadth > reliability (many P0/P1 open) | Reliability > feature speed (fewer critical bugs, faster fixes) |
| **Community Character** | Large, vocal, feature-hungry, tolerates instability | Smaller, detail-oriented, values polish and UX |

**Bottom Line:** OpenClaw is the “Swiss Army knife” for building agent infrastructures; Hermes Agent is the “refined sports car” for individuals needing a reliable daily driver.

---

## 6. Community Momentum & Maturity

| Tier | Projects | Characteristics |
|------|----------|----------------|
| **Rapidly Iterating** | OpenClaw | High issue/PR churn, critical bugs unresolved, many pending feature decisions. Community growth is fast but unstable. |
| **Stabilizing** | Hermes Agent | Consistent merges, fewer regressions, responsive maintainers. Approaching a “boring but reliable” phase. |

**Trend:** OpenClaw’s momentum could tip either way: either maintainers resolve the memory leak and cache regression (accelerating enterprise adoption) or the bug backlog frustrates contributors. Hermes’ measured pace suggests it will soon reach v1.0 stability, possibly overtaking OpenClaw in production trustworthiness despite smaller community.

---

## 7. Trend Signals for AI Agent Developers

1. **Memory Leaks Are the #1 Production Roadblock** – Both projects report unchecked memory growth (gateway, LSP subprocesses, heap at idle). Developers should prioritize memory profiling and graceful cleanup in agent runtimes.

2. **Credential Exfiltration Is a Growing Concern** – Users explicitly demand agents never see raw API keys (OpenClaw #10659) and injection scanners must handle obfuscated variants (Hermes #27284). Expect security reviews to become mandatory for agent approval.

3. **Context Management Is Underserved** – Single-phase compaction is costly and error-prone. Two-phase pruning (Hermes #513) and across-session prompt caching (OpenClaw #102175) indicate a need for smarter, user-controlled context lifecycle.

4. **Platform Integration Reliability > New Channels** – Both projects spend disproportionate effort fixing Discord reconnects, WhatsApp stalls, Teams typing indicators, and email subject customization. Users value reliable existing integrations over new shiny ones.

5. **Concurrency at Multiple Levels** – Multi-agent sub-task delegation (Hermes per-subagent model override, OpenClaw multi-lane concurrency) and per-profile tab leases for browser tools are emerging as differentiators. Agent developers must design for safe concurrent resource access.

6. **Cost Visibility and Governance** – OpenClaw’s agent-scoped budgets and batch API support, and Hermes’ pricing overrides and cache cost handling, show a maturing expectation to control spend in production agent fleets.

**Recommendation:** For teams building AI agent infrastructure, prioritize a **memory-leak-tight, credential-safe, context-efficient** runtime before adding new channels or features. The community is signaling that stability governs adoption.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-07-11

---

## 1. Today's Overview

The Hermes Agent project saw extremely high activity over the last 24 hours, with 50 issues and 50 PRs updated. Of those, 3 issues were closed and 12 PRs were merged or closed, reflecting a strong focus on bug fixes and performance improvements. No new releases were published. The community continues to engage deeply, filing thoughtful feature requests and reporting nuanced bugs, particularly around the Desktop and TUI experiences, credential workflows, and context management. The maintainers appear to be actively processing contributions, with several PRs addressing critical path issues such as cron heartbeats, WebSocket reconnect behaviour, and IME input handling.

---

## 2. Releases

No new releases were tagged in the last 24 hours. The latest known version is v0.18.2 (2026-07-07). Omit further details.

---

## 3. Project Progress

**Merged/Closed PRs today (10 of 12 listed):**

- **[#62155](https://github.com/NousResearch/hermes-agent/pull/62155)** – `fix(cron): bind claim heartbeats to dispatch owner`. Prevents stale runners from extending expired claims, tightening cross‑process cron safety.
- **[#62141](https://github.com/NousResearch/hermes-agent/pull/62141)** – `revert: remove unproven owner‑thread FD release`. Rolls back an earlier socket‑abort change that was not reproducible; restores the stable shutdown‑only boundary.
- **[#53993](https://github.com/NousResearch/hermes-agent/pull/53993)** – `fix(tui): split IME backspace text keypresses`. Fixes a TUI parser bug where IME recomposition chunks containing backspace were discarded.
- **[#53522](https://github.com/NousResearch/hermes-agent/pull/53522)** – `fix(desktop): preserve active chat on reconnect`. Prevents sleep/wake WebSocket reconnects from being treated as a new session.
- **[#53497](https://github.com/NousResearch/hermes-agent/pull/53497)** – `fix(tui): run prompt submits off the RPC loop`. Moves `prompt.submit` to a thread pool so tool execution does not block the RPC handler.
- **[#52840](https://github.com/NousResearch/hermes-agent/pull/52840)** – `perf(model): reuse provider models cache in memory`. Adds in‑memory snapshot caching for model listings.
- **[#52438](https://github.com/NousResearch/hermes-agent/pull/52438)** – `perf(model): reuse auth store during provider listing`. Loads auth store once per listing call.
- **[#52435](https://github.com/NousResearch/hermes-agent/pull/52435)** – `fix(tests): find Windows virtualenvs in run_tests`. Adds Windows venv probing and path normalisation.
- **[#52433](https://github.com/NousResearch/hermes-agent/pull/52433)** – `perf(profiles): allow lightweight profile listing`. Introduces keyword‑only flags to skip expensive per‑profile detail costs.
- **[#52425](https://github.com/NousResearch/hermes-agent/pull/52425)** – `fix(update): log elapsed time for update stages`. Adds stage‑level timing to help users identify slow steps.

**Closed issues today:**

- **[#50295](https://github.com/NousResearch/hermes-agent/issues/50295)** – Bedrock cost display: pricing layer now handles cache cost fields.
- **[#55677](https://github.com/NousResearch/hermes-agent/issues/55677)** – Context compaction Jinja error: root cause addressed (likely via related PRs).

---

## 4. Community Hot Topics

The most active discussions (by comment count) centre on configuration bugs, UI consistency, and forward‑looking features:

| Issue | Comments | Summary |
|-------|----------|---------|
| [#52496](https://github.com/NousResearch/hermes-agent/issues/52496) | 7 | Dashboard `/api/model/set` rewrites named custom providers to `openrouter`. User pain with persistency of `custom_providers` settings. |
| [#48098](https://github.com/NousResearch/hermes-agent/issues/48098) | 7 | Desktop UI keeps showing "Summarizing thread" after compaction resumes – a visual stale‑state bug affecting trust in the interface. |
| [#28156](https://github.com/NousResearch/hermes-agent/issues/28156) | 5 | Bedrock+Claude wizard accepts bearer‑only credentials but runtime fails; also region picker shows unroutable profiles in EU. Dual bug impacting AWS users. |
| [#513](https://github.com/NousResearch/hermes-agent/issues/513) | 4 | Feature request for two‑phase context management (prune then compact), inspired by Kilocode. High interest from power users. |
| [#27284](https://github.com/NousResearch/hermes-agent/issues/27284) | 4 | Prompt‑injection scanners in memory/MCP miss multi‑word `ignore … instructions` variants. Security‑conscious users are engaged. |
| [#46947](https://github.com/NousResearch/hermes-agent/issues/46947) | 4 | Outbound email subject is hardcoded – no way to set a custom subject for cron‑delivered reports or agent‑initiated messages. |

**Underlying needs:** Users are demanding better **configuration transparency** (custom provider persistence), **UI feedback** (accurate status indicators), **robust cloud onboarding** (Bedrock credential flow), **smarter context management** (cost‑efficient pruning), **stronger security** (injection scanner completeness), and **more flexible platform integrations** (email subject control).

---

## 5. Bugs & Stability

### New / Reporting Today (2026-07-11) – sorted by severity:

| Issue | Severity | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| [#62397](https://github.com/NousResearch/hermes-agent/issues/62397) | P2 | Background review fork can’t patch skills because prompt never calls `skill_view` and guard refuses write. Silent learning loss. | ✅ [#62400](https://github.com/NousResearch/hermes-agent/pull/62400) (open) |
| [#62394](https://github.com/NousResearch/hermes-agent/issues/62394) | P2 | Teams typing indicator animates forever after response – suspected leaked `_keep_typing` task. | ❌ Not yet |
| [#62383](https://github.com/NousResearch/hermes-agent/issues/62383) | P2 | Weixin iLink cron delivery fails with `ret=-2` (rate limited) when `context_token` is stale, instead of proper token expiry handling. | ❌ Not yet |
| [#62324](https://github.com/NousResearch/hermes-agent/issues/62324) | P3 | Desktop: `stage-native-deps.mjs` drops execute bit on `node-pty`’s `spawn-helper`, breaking built‑in terminal. | ❌ Not yet |
| [#62170](https://github.com/NousResearch/hermes-agent/issues/62170) | P2 | TUI shows stale session content after switching sessions (v0.18.1). Needs reproduction. | ❌ Not yet |
| [#25016](https://github.com/NousResearch/hermes-agent/issues/25016) | P2 | LSP idle subprocesses are never reaped – long‑running gateways accumulate ~200 MB per server forever. (Pre‑existing, updated today.) | ❌ Not yet |

### Previously reported regressions still open:

- [#60385](https://github.com/NousResearch/hermes-agent/issues/60385) – MCP server process leak on reconnect (P2).
- [#53329](https://github.com/NousResearch/hermes-agent/issues/53329) – Non‑git project folders show duplicate lanes (P3).
- [#40077](https://github.com/NousResearch/hermes-agent/issues/40077) – Desktop crash on NVIDIA 580+ drivers (Ubuntu 24.04) (P3).
- [#57828](https://github.com/NousResearch/hermes-agent/issues/57828) – Lazy backend refresh fails can corrupt venv with no recovery (P2).

**Overall stability rating:** Moderate. Several P2 bugs affect daily use (UI staleness, process leaks, cron delivery). The maintainers are responsive – many fixes are landing the same day or within a few days – but a backlog of resource‑leak issues (LSP, MCP) and critical credential bugs (Bedrock) remain.

---

## 6. Feature Requests & Roadmap Signals

### Featured requests from today:

- **[#62375](https://github.com/NousResearch/hermes-agent/issues/62375)** – Make remote attachment uploads bounded and resumable (Desktop). Addresses file size limits and single‑shot upload fragility.
- **[#62369](https://github.com/NousResearch/hermes-agent/issues/62369)** – Inject message timestamps into agent context for better time awareness across multi‑day sessions.
- **[#62339](https://github.com/NousResearch/hermes-agent/issues/62339)** – Per‑profile tab lease/registry so concurrent agents don’t collide on the same browser tab.
- **[#62338](https://github.com/NousResearch/hermes-agent/issues/62338)** – Per‑tab CDP target routing for same‑profile concurrency (follow‑up to #49691).
- **[#61249](https://github.com/NousResearch/hermes-agent/issues/61249)** – Desktop approval bar truncates multi‑line diffs – a UI request with an open fix PR [#62092](https://github.com/NousResearch/hermes-agent/pull/62092).

### Other high‑interest requests still open:

- [#513](https://github.com/NousResearch/hermes-agent/issues/513) – Two‑phase context management (prune then compact). Could appear in next minor release given community traction.
- [#36656](https://github.com/NousResearch/hermes-agent/issues/36656) – Volatile skills (load content for one turn only). Reduces context bloat.
- [#58731](https://github.com/NousResearch/hermes-agent/issues/58731) – Per‑subagent model override in `delegate_task`. Critical for multi‑role agent teams.
- [#9403](https://github.com/NousResearch/hermes-agent/issues/9403) – Pricing overrides, contract pricing, and sync CLI. Phase 4 of pricing architecture.

**Prediction for next version:** The concurrency improvements for browser tools (#62338/#62339) and the approval bar fix (#62092) are likely to be merged soon. The two‑phase context management (#513) may also land if the maintainers prioritise it.

---

## 7. User Feedback Summary

**Pain points expressed:**

- **Configuration confusion:** Multiple users report that custom provider settings (especially custom:* names) are rewritten by the dashboard ( [#52496](https://github.com/NousResearch/hermes-agent/issues/52496) ) and that the Bedrock wizard accepts incomplete credentials ( [#28156](https://github.com/NousResearch/hermes-agent/issues/28156) ).
- **UI inconsistencies:** The Desktop/TUI frequently shows stale status (e.g., "Summarizing thread" after completion, [#48098](https://github.com/NousResearch/hermes-agent/issues/48098) ), duplicate lanes for non‑git projects ( [#53329](https://github.com/NousResearch/hermes-agent/issues/53329) ), and indistinguishable message bubbles ( [#57104](https://github.com/NousResearch/hermes-agent/issues/57104) ).
- **Context handling gaps:** Context compaction can corrupt sessions on the 2nd/3rd attempt ( [#55677](https://github.com/NousResearch/hermes-agent/issues/55677) – closed), and the single‑phase summarisation is costly ( [#513](https://github.com/NousResearch/hermes-agent/issues/513) ).
- **Platform integrations missing polish:** Email subject is hardcoded ( [#46947](https://github.com/NousResearch/hermes-agent/issues/46947) ), Signal deliveries are truncated ( [#57929](https://github.com/NousResearch/hermes-agent/issues/57929) – PR open), and Teams typing indicator breaks ( [#62394](https://github.com/NousResearch/hermes-agent/issues/62394) ).

**Satisfaction signals:**

- Users are enthusiastic about new features like approval hooks ( [#61249](https://github.com/NousResearch/hermes-agent/issues/61249) ) and named browser profiles ( [#49691](https://github.com/NousResearch/hermes-agent/issues/49691) ).
- Several users filed thoughtful feature requests with clear use cases (e.g., per‑agent model overrides, volatile skills, message timestamps), indicating a sophisticated and engaged community.
- Maintainers are responsive – many bug reports have associated PRs or are quickly labelled and triaged.

---

## 8. Backlog Watch

The following important issues have received minimal recent maintainer attention or remain open for weeks with no clear resolution:

| Issue | Created | Last Update | Severity | Summary |
|-------|---------|-------------|----------|---------|
| [#25016](https://github.com/NousResearch/hermes-agent/issues/25016) | 2026-05-13 | 2026-07-11 | P2 | LSP idle subprocesses never reaped – memory leak in long‑running gateways. |
| [#28156](https://github.com/NousResearch/hermes-agent/issues/28156) | 2026-05-18 | 2026-07-10 | P1 | Bedrock+Claude wizard

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*