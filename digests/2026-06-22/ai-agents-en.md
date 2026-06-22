# OpenClaw Ecosystem Digest 2026-06-22

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-22 03:50 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-06-22

## 1. Today's Overview

The OpenClaw project saw extremely high activity over the last 24 hours, with 500 issues and 500 pull requests updated. Of those issues, 475 remain open/active and only 25 were closed; PRs show 389 open and 111 merged/closed. A single new beta release (v2026.6.10-beta.1) arrived with a focus on session state reliability. However, the community continues to report a wave of regressions introduced in recent versions, particularly around Telegram duplicate replies, memory store relocation, channel dispatch crashes, and compaction timeouts. Numerous P1/P2 bugs remain unresolved with maintainer reviews and product decisions still pending, indicating that although development velocity is high, the project is struggling to stabilize its codebase.

## 2. Releases

- **v2026.6.10-beta.1** (released 2026-06-22)  
  **Highlights:** Improved agent turn and session state handling:
  - Preserves pending subagent completion announcements
  - Ensures chat history transcripts remain non-empty
  - Maintains media index alignment across restarts
  - Restarts dormant follow-up drains
  - Resolves compaction model aliases consistently  
  [Release link](openclaw/openclaw v2026.6.10-beta.1)

No breaking changes or migration notes were provided with this release.

## 3. Project Progress

Over the past 24 hours, 111 PRs were merged or closed. Key changes include:

- **CI improvements:** `fix(ci): bundle test shards and right-size runners` (#95649) reduces Node matrix from 95 to 51 shards.
- **Agent harness activation fix:** `fix(agents): activate selected harness plugins` (#95652) ensures plugins are active before harness selection.
- **Tool-activity heartbeat for subagents:** `fix(agents): add tool-activity heartbeat` (#95536) prevents subagent sessions from being killed during long tool calls.
- **Port handling for health/probe:** `fix(gateway): accept port for health and probe` (#94687) – automerge armed.
- **Higher default live tool result cap:** `fix(agents): raise default live tool result cap from 16k to 32k chars` (#94803) – closes #94280.
- **Empty assistant replies in cron:** `fix(cron): allow empty assistant replies in cron lane` (#94260) – closes #94224.
- **Compaction overflow test fix:** `fix(test): add missing reasoning field to overflow compaction harness mock defaults` (#91097).
- **Session history family lookup:** `[AI-assisted] Add session history family lookup` (#90239) – ready for maintainer review.
- **New feature – cron dry-run:** `feat(cron): add add dry-run preview` (#93149) – diamond lobster rating, ready for maintainer look.

Additionally, several documentation and hook pipeline improvements continue to mature, including `feat(hooks): add agent turn end hook` (#89152) and `feat(hooks): add ACP turn transcript save hook` (#89154), both ready for maintainer review.

## 4. Community Hot Topics

The most engaged issues (by comment count) highlight deep user frustration with recent regressions and missing capabilities:

- **#86519 – Agent repeats identical replies 2-10x on Telegram after 5.20 update** (10 comments, 1 👍)  
  A P1 regression. Users report that after updating to 2026.5.20, Telegram messages are duplicated. Some mitigation was seen in 5.22 but not resolved.  
  [Issue](openclaw/openclaw Issue #86519)

- **#90354 – Add bounded/validated append semantics for pre-compaction memory flush** (8 comments, 1 👍)  
  Feature request for hard guardrails on append size and silent failure handling.  
  [Issue](openclaw/openclaw Issue #90354)

- **#92043 – 180s compaction timeout is a single wall clock over the whole chunk pipeline** (8 comments, 1 👍)  
  Users with long histories or slow LLM providers experience identical failure every turn. No partial progress reuse.  
  [Issue](openclaw/openclaw Issue #92043)

- **#92460 – Isolated cron completion announcer drops explicit delivery.channel** (8 comments, 1 👍)  
  Cron jobs that set `delivery.channel` still fail with "Channel is required".  
  [Issue](openclaw/openclaw Issue #92460)

- **#95623 – tool_use.id sanitizer misses OpenAI-responses composite id on cross-provider failover** (7 comments, 1 👍)  
  A critical bug that can cause session bricks when failing over from OpenAI to Anthropic.  
  [Issue](openclaw/openclaw Issue #95623)

- **#95495 – 2026.6.9 silently relocates memory store with no migration** (7 comments, 1 👍)  
  Users forced to re-embed entire memory (1499 files) after upgrade. No warning.  
  [Issue](openclaw/openclaw Issue #95495)

- **#90325 – Matrix channel dispatch broken in v2026.6.1** (7 comments, 2 👍)  
  TypeError on every inbound message after update.  
  [Issue](openclaw/openclaw Issue #90325)

- **#90916 – Topic-session families for one assistant across multiple named context lanes** (7 comments, 1 👍)  
  A community-requested feature to allow a single assistant to maintain isolated topic lanes while sharing durable memory.  
  [Issue](openclaw/openclaw Issue #90916)

- **#91455 – Documentation update for Kubernetes** (7 comments, 1 👍)  
  Users find Kubernetes deployment docs awkward and request Helm support.  
  [Issue](openclaw/openclaw Issue #91455)

The overall sentiment is a mix of enthusiasm for the project's rapid development and frustration with the pace of regressions introduced.

## 5. Bugs & Stability

Multiple high-severity regressions remain open, many with **P1** priority and diamond lobster ratings. The most critical:

| Issue | Summary | Severity | Fix PR Exists? |
|-------|---------|----------|----------------|
| #86519 | Agent repeats identical replies on Telegram after 5.20 | P1 regression | No linked PR |
| #92043 | 180s compaction timeout over entire pipeline, no partial reuse | P1 | Linked PR open (no number given) |
| #92460 | Isolated cron completion drops `delivery.channel` | P1 | Linked PR open |
| #95495 | Silent memory store relocation in 2026.6.9, forces full re-embed | P1 regression | No linked PR |
| #95623 | tool_use.id sanitizer fails on cross-provider failover, bricks session | P1 | Needs live repro |
| #90325 | Matrix channel dispatch broken (TypeError) | P1 regression | Needs live repro |
| #92415 | Session model snapshot never refreshed after /model switch | P1 | Linked PR open |
| #92076 | Subagent completion delivery fails when requester session inactive | P1 | Fix shape clear |
| #91363 | Isolated cron consistently fails "LLM request failed" | P1 | Needs live repro |
| #93375 | Telegram polling silent crash loop after transient network timeout | P1 | Linked PR open |
| #90840 | Subagent run completion delivered raw instead of parent summary | P1 regression | Needs security review |
| #90925 | Subagent announce compaction falls into openai-responses API-key route | P1 regression | Fix shape clear |
| #91804 | Internal reasoning leakage in 2026.6.5 | P1 regression | Needs security review |

Several of these bugs are likely related to the high velocity of changes. The v2026.6.10-beta.1 release claims to fix some session state issues, but many reported regressions remain unaddressed.

## 6. Feature Requests & Roadmap Signals

Notable feature requests that may appear in upcoming releases:

- **Bounded/validated append semantics for pre-compaction memory flush** (#90354) – addresses a common silent failure pattern.
- **Topic-session families for one assistant** (#90916) – a major architectural request that would enable multi-lane assistants. Likely far off but signals community need.
- **Subagent orchestration in cron isolated sessions** (#92369) – users want to spawn, wait, and aggregate subagent results in cron workflows.
- **Add reset family carryover summaries** (PR #90259) – session history family lookup (PR #90239) already advancing, suggesting reset carryover may land soon.
- **Model failover and terminal failure hooks** (PR #70990) – long-standing extensibility feature.
- **Adaptive reset mode with daily AND idle semantics** (PR #71400) – waiting on author.
- **Kubernetes documentation improvement** (#91455) – high community interest.
- **ACP session skill context injection** (#43564) – old feature request; interest persists.

Given the current focus on stability, the next major version may prioritize the compaction timeout rework (#92043), memory flush guardrails (#90354), and delivery reliability (#92460, #91212) over new features.

## 7. User Feedback Summary

Real user pain points reported in the last 24 hours:

- **"Costs aren't worth it for the experience"** – user abandoning a DigitalOcean droplet due to poor UX for long-running tasks and silent cron failures (#88087).
- **"Internal reasoning leakage in 2026.6.5"** – major privacy concern, agent thinking exposed to end users (#91804).
- **"99.9% → 22% prompt cache hit rate"** when enabling `active-memory` plugin, causing significant cost increase (#91223).
- **"Silent memory relocation forced full re-embed"** – users frustrated by zero warning and lost work (#95495).
- **"Matrix channel completely broken"** – Telegram and Feishu users also reporting duplicates and crashes.
- **"No reliable way to spawn subagents in cron"** – advanced users hitting orchestration limitations (#92369).
- **"Tool search mode silently breaks memory flush"** – memories lost due to unrecoverable tool call errors (#92273).

Satisfaction signals: Some users continue to report success with foreground gateway operation and basic chat functionality. The project's rapid bug fixes (e.g., partial improvement in duplicate replies from 10x to 2-3x) show responsiveness, but the high volume of regressions overshadows this.

## 8. Backlog Watch

Issues that have been open for an extended period and still lack maintainer attention:

- **#67915 – Local assistant attachments "Unavailable — Outside allowed folders"** (P2, 6 comments, opened 2026-04-17) – long-standing behavior bug, linked PR open.
- **#86214 – Codex app-server client closes mid-turn with large logs_2.sqlite** (P1, 7 comments, opened 2026-05-24) – impacts Discord/Codex users, needs live repro.
- **#86023 – Codex long-running sessions should use semantic thread/bootstrap cache ownership** (P2, 5 comments, opened 2026-05-24) – performance issue with session slowdown.
- **#86612 – Docker gateway container restart loop on Windows** (P1, 4 comments, opened 2026-05-25) – blocking for Docker users on Windows.
- **#43564 – ACP session skill context injection** (P2, 4 comments, opened 2026-03-12) – feature request that has been waiting for product decision for months.
- **#91212 – delivery-recovery 0 recovered / N failed after gateway restart** (P1, 5 comments, opened 2026-06-07) – silent message loss, still needs live repro.
- **#91285 – Tool Lifecycle / Gateway Recovery Field Report** (P2, 4 comments, opened 2026-06-08) – detailed crash analysis, awaiting maintainer review.
- **#90711 – launchd plist StandardErrorPath hardcoded to /dev/null** (P2, 6 comments, opened 2026-06-05) – hides all gateway stderr diagnostics since 5.28.

These issues represent long-unresolved pain points that should be prioritized to reduce community churn and prevent further user abandonment.

---

*This digest was generated from OpenClaw GitHub activity as of 2026-06-22 T12:00 UTC. Data covers the preceding 24-hour period.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is currently characterized by high-velocity development at the cost of stability. Projects are racing to support multi-channel delivery (Telegram, Discord, Matrix, email), provider resilience (fallback across OpenAI, Anthropic, Bedrock, Google), and session persistence (memory stores, compaction, cron workflows). Both OpenClaw and Hermes Agent show strong community engagement but face distinct challenges: OpenClaw is experiencing a regression crisis from its rapid feature expansion, while Hermes Agent is navigating provider sunsets and desktop platform fragmentation. The ecosystem is maturing from single-channel chat bots toward multi-agent orchestration hubs, but reliability gaps are causing user churn.

---

## 2. Activity Comparison (24-hour snapshot: 2026-06-22)

| Metric | OpenClaw | Hermes Agent | Notes |
|--------|----------|--------------|-------|
| **Issues Updated** | 500 | 50 | 10x volume in OpenClaw |
| **Issues Closed** | 25 (5%) | 13 (26%) | Hermes closes at 5x the rate |
| **PRs Updated** | 500 | 50 | 10x volume in OpenClaw |
| **PRs Merged/Closed** | 111 (22%) | 6 (12%) | OpenClaw merges more absolutely, but still low % |
| **New Release** | ✅ v2026.6.10-beta.1 | ❌ None | OpenClaw shipped today |
| **Last Stable Release** | v2026.6.10-beta.1 (beta) | v0.16.0 | OpenClaw is in continuous beta cycle |
| **Open P1 Bugs** | ~13 critical regressions | ~3 critical (mostly provider sunset) | OpenClaw has 4x more critical open bugs |
| **Health Score (Qualitative)** | **Stabilizing under strain** | **Stable, productive** | See community sentiment below |

**Interpretation:** OpenClaw's raw activity is an order of magnitude higher, but its close/merge rate is low relative to issue volume. Hermes Agent processes a higher percentage of its smaller backlog, indicating a more controlled development cadence.

---

## 3. OpenClaw's Position

**Advantages vs. peers:**
- Broader channel support (Telegram, Matrix, Feishu, cron, ACP) — Hermes Agent focuses on Telegram, Discord, Slack, email, and desktop.
- More aggressive feature velocity: session families, cron dry-run, agent turn hooks, subagent heartbeats — Hermes Agent has fewer experimental features.
- Larger community issue volume (500/day vs. 50/day) suggests a wider user base, though much of it is noise from regressions.
- Deep memory management system (compaction, aliases, media index alignment) — Hermes Agent relies on simpler memory store (Mem0, FTS5).

**Technical approach differences:**
- OpenClaw uses a **harness/plugin architecture** with explicit agent turn lifecycle hooks (agent turn end hook, ACP transcript save hook). Hermes Agent uses a **gateway/desktop/TUI** triad with plugin SDK via `__HERMES_PLUGIN_SDK__`.
- OpenClaw's **compaction pipeline** is a unique, high-risk feature that causes the most severe regressions (timeouts, relocation, data loss). Hermes Agent has no equivalent — it uses simpler session persistence.
- Hermes Agent has a **native desktop app** (Electron) and **Kanban integration**; OpenClaw is purely CLI/gateway/API.

**Community size comparison:**
| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| Issues/day | 500 | 50 |
| Issue engagement (avg comments) | ~7.5 on top issues | ~5.5 on top issues |
| Reaction count on top issues | 1-2 👍 | 4-6 👍 |
| Maintainer responsiveness | Slow on backlog items (e.g., #67915 open since April) | Faster turnaround (13 issues closed in 24h) |
| User sentiment | Frustrated (repeated regressions, silent data loss) | Mixed (provider sunset pain, but core features work) |

**Verdict:** OpenClaw leads in breadth and ambition but is damaging user trust through instability. Hermes Agent is smaller but more reliable and user-experience-focused.

---

## 4. Shared Technical Focus Areas

These requirements are emerging as cross-project priorities:

| Focus Area | OpenClaw | Hermes Agent | Industry Signal |
|------------|----------|--------------|-----------------|
| **Channel dispatch reliability** | ✅ P1: Telegram duplicates (#86519), Matrix broken (#90325), Feishu crashes | ✅ P2: Multi-bot Telegram routing (#10452), file-type agnostic (#50563) | **Strong** — agents must deliver consistently across all channels |
| **Provider resilience & failover** | ✅ P1: `tool_use.id` fails on cross-provider failover (#95623), reasoning leakage (#91804) | ✅ P2: Google Gemini sunset (#50530), Bedrock non-Claude routing (#50292) | **Strong** — provider fragility is the #1 user complaint ecosystem-wide |
| **Session persistence / memory** | ✅ P1: Compaction timeouts (#92043), silent memory relocation (#95495) | ✅ P2: FTS5 write-path corruption check (#50576), cron session titles (#50535-7) | **Strong** — memory is a key differentiator but fragile |
| **Cron / scheduled automation** | ✅ P1: Delivery channel dropped (#92460), empty replies allowed (#94260) | ✅ P3: Cron session titles, Kanban in desktop (#41756) | **Emerging** — users want agent-driven scheduled workflows |
| **Subagent orchestration** | ✅ P1: Subagent completion fails (#92076), delivery instead of summary (#90840) | ❌ Not a focus (Hermes does not have a subagent model) | **Growing** — multi-agent architectures are becoming standard |

**Takeaway:** Ecosystem-wide, the most pressing shared requirements are **channel delivery reliability**, **provider failover**, and **memory/session persistence**. Projects that solve these first will gain user trust.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Target user** | Advanced developers, self-hosters, multi-channel deployers | Desktop-first users, plugin developers, team workflows |
| **Primary interface** | CLI / gateway / API | Desktop app / TUI / gateway + dashboard |
| **Architecture** | Plugin harness + agent lifecycle hooks + compaction pipeline | Gateway → Desktop/TUI + plugin SDK + Kanban board |
| **Feature focus** | Core infrastructure (memory, sessions, channel routing, cron) | User experience (Desktop, Kanban, file handling, security) |
| **Provider strategy** | Full matrix (OpenAI, Anthropic, Bedrock, Ollama, etc.) | Selective (OpenAI, Anthropic, Bedrock, Google, OpenRouter) |
| **Memory system** | Complex compaction with aliases, media index, family lookups | Simpler FTS5 + Mem0 plugin; fewer moving parts |
| **Plugin ecosystem** | Hooks (agent turn end, ACP transcript save, etc.) | Plugin SDK (`__HERMES_PLUGIN_SDK__`), MCP OAuth, Langfuse |
| **Subagent support** | Full subagent orchestration (heartbeats, summarization, cron) | None |
| **Channel breadth** | Telegram, Matrix, Feishu, email, cron, ACP | Telegram, Discord, Slack, email, Desktop (Electron) |
| **Desktop support** | ❌ None | ✅ Native macOS (arm64), Electron app, system tray (pending) |
| **Observability** | Basic logging, compaction diagnostics | Langfuse integration, health probes, error humanization (requested) |

**Strategic implications:**
- **OpenClaw** is building the **operating system for autonomous agents** — it handles the hard infrastructural problems (memory, sessions, multi-agent coordination) but sacrifices UX and stability.
- **Hermes Agent** is building the **desktop hub for agentic work** — it prioritizes user experience, plugin extensibility, and team collaboration, but lacks the deep orchestration capabilities.

---

## 6. Community Momentum & Maturity

| Tier | Project | Characteristics |
|------|---------|-----------------|
| **Rapid iteration (high churn)** | **OpenClaw** | 500 issues/day, 111 PRs merged, 1 beta release. Velocity is extreme, but 13 critical regressions remain open. Community is vocal about frustration. Risk of user abandonment. |
| **Stable iteration (controlled)** | **Hermes Agent** | 50 issues/day, 6 PRs merged, no release. Lower volume but higher close rate. Provider sunset is the main threat. Desktop and Kanban are growing features. |

**Maturity indicators:**

| Indicator | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| Release cadence | ~weekly betas | ~monthly stable |
| Breaking changes frequency | High (silent memory relocation, no migration notes) | Low (no breaking changes reported) |
| Documentation quality | Mixed (Kubernetes docs complained about, #91455) | Better (API docs, plugin SDK docs) |
| Security posture | Reasoning leakage (#91804), P1 security issues open | Browser orphan reaper vulnerability (#14073, now closed) |
| Backlog age | Issues open since March 2026 (#43564, #67915) | All recent (<1 month) |
| User retention signal | User abandoning DigitalOcean droplet (#88087) | No explicit abandonment reports |

**Verdict:** Hermes Agent is more mature as a *product*; OpenClaw is more ambitious as a *platform* but still in an unstable growth phase.

---

## 7. Trend Signals (for AI Agent Developers)

### From Community Feedback

1. **Provider diversity is a requirement, not a feature.** Both projects' top bugs are tied to provider failover failures (OpenClaw #95623, Hermes #50530, #50292). Developers should architect for provider-agnostic routing from day one.

2. **Memory systems are the biggest differentiator and biggest risk.** OpenClaw's compaction pipeline causes data loss, timeouts, and relocation nightmares. Hermes's simpler FTS5 is more stable but less capable. The industry needs a battle-tested, transactional memory layer.

3. **Desktop matters for adoption.** Hermes Agent's Kanban integration (#41222, 6 👍) and multi-bot Telegram support (#10452, 4 👍) show that users want desktop-first ergonomics. OpenClaw's lack of desktop support is a limitation.

4. **Cron/scheduled agents are emerging as core workflows.** Both projects invest in cron fixes (OpenClaw #92460, Hermes #50535-7). Users want agents that operate asynchronously and reliably.

5. **Silent failures erode trust.** OpenClaw's silent memory relocation (#95495) and Hermes's silent config failures (#50553) are top pain points. Opaque error handling (HTTP 400 without context, empty replies) is unacceptable.

6. **Subagent orchestration is the next frontier.** OpenClaw has a full subagent model (heartbeats, summarization, cron sponsorship). Hermes has none. This will become a key differentiator as multi-agent systems mature.

7. **OpenTelemetry/Langfuse integration is becoming table-stakes.** Hermes users demand Langfuse support (#42033). OpenClaw lacks any observability integration. AI agent developers should invest in tracing and debugging tools.

### Value for Developers

| Trend | Actionable Insight |
|-------|-------------------|
| Provider resilience | Implement fallback chains with session-level retry; test failover across OpenAI ↔ Anthropic ↔ Bedrock |
| Memory reliability | Use transactional writes with rollback; warn users before migrations; avoid silent compaction |
| Desktop UX | Build for desktop-first interaction if targeting non-developer users; integrate task boards, system tray, file handling |
| Cron/scheduling | Design agents that can operate asynchronously without a live session; test channel delivery in isolation |
| Error transparency | Return structured errors with human-readable messages and suggested fixes; never silently drop messages |
| Subagent orchestration | Plan for multi-agent spawn/wait/aggregate patterns; implement heartbeat mechanisms for long tool calls |

---

**Summary for Decision-Makers:**

- **Choose OpenClaw** if you need broad channel support, deep memory management, subagent orchestration, and can tolerate a more unstable codebase with rapid fixes.
- **Choose Hermes Agent** if you want a reliable desktop experience, plugin extensibility, team workflows (Kanban), and are willing to accept narrower channel breadth and no subagent support.
- **Watch both** for shared trend signals: provider resilience, memory/storage reliability, and cron/scheduled agent patterns will define the next 6 months of the ecosystem.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-22

## Today's Overview

The project is experiencing **high activity**, with 50 issues and 50 pull requests updated in the last 24 hours. Of these, 13 issues were closed and 6 PRs were merged or closed, indicating a productive day of bug fixing and feature advancement. The community is actively engaged, with several high-traffic threads around Telegram multi-bot support, desktop platform compatibility, and the ongoing fallout from Google's Gemini CLI sunset. No new formal releases were cut today, but a batch of coordinated fix PRs landed across gateway, CLI, desktop, and plugin subsystems. Overall project health is strong but under strain from several P2 regressions requiring urgent maintainer triage.

---

## Releases

*None today.* The last official release was v0.16.0; v0.17.0 appears to be accumulating PRs and deferred work (see PR #50111).

---

## Project Progress

**6 PRs were merged or closed** today. Notable advances:

### Gateway & Platform Routing
- **Multi-bot Telegram routing** (PR #10455, open) — adds backward-compatible multi-account Telegram support to Hermes gateway and `send_message`. Responds to long-standing feature request #10452.
- **Accept any inbound file type** (PR #50563, open) — removes the restrictive file-extension allowlist across Telegram, Discord, and Slack platforms. Root cause: Discord's `allow_any_attachment` defaulted to `false` on the opt-out path.
- **Email pairing security fix** (PR #50568, open) — email gateway now silently ignores unknown senders instead of replying with pairing codes. Addresses a security concern where an agent's mailbox could leak pairing prompts to unintended recipients.

### Bug Fixes (Merged/Closed Today)
| Issue | Fix PR | Summary |
|-------|--------|---------|
| #50553 (closed) | #50574 (open) | `config set` with space-separated keys silently failed. Fix accepts the trailing token as part of the key. |
| #49008 (open) | #50579 (open) | OpenAI Codex image generation plugin now gates unsupported `image_generation` tool with a clear error instead of opaque HTTP 400. |
| #50292 (open) | #50578 (open) | Non-Claude Bedrock models no longer routed through Anthropic SDK. Fix reads runtime model instead of config default. |
| #50502 (open) | #50576 (open) | FTS5 write-path corruption detection added to DB health probe. Previously only validated reads. |
| #50535, #50536, #50537 (open) | #50575 (open) | Three cron session-title bugs fixed: blank titles on generation failure, unhandled empty-title edge case, duplicate auto-title `ValueError`. |
| #50547 (open) | #50577 (open) | Kanban plugin swapped native `window.confirm`/`alert`/`prompt` for in-app `__HERMES_PLUGIN_SDK__` dialogs. |
| #50557 (open) | #50573 (open) | Model switcher now splits `volcengine-agent-plan`'s comma-separated `default_model` into individual entries. |
| #50553 (closed) | #50574 (open) | Space-separated key in `config set` no longer silently fails. |

### Other Fixes
- **#50580** (open) — Replaced 4 bare `assert` statements in `docker.py`, `browser_supervisor.py`, and other modules that would be stripped under `-O`.
- **#50565** (open) — Replaced 5 bare asserts in WeChat (WeCom) gateway platform.
- **#50567** (open) — Nous auth refresh for idle dashboard/gateway agents to prevent expired invoke JWTs.
- **#50566** (open) — Dashboard `/chat` header now shows live session title instead of static "Chat" label.
- **#50569** (open) — Web server dashboard settings routes scoped to active profile.

---

## Community Hot Topics

### Most Active Issues (by comment count)

1. **#10452** — *Support multi Telegram bots for gateway routing and send_message* (7 comments, 4 👍)
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/10452)
   - Strong user demand for running multiple Telegram bots side-by-side (e.g., primary assistant + dev/team bot). PR #10455 and #18652 are active.

2. **#37505** — *Hermes Desktop macOS DMG is arm64-only and fails on Intel Macs* (6 comments, 1 👍)
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/37505)
   - Blocking for Intel Mac users; no fix PR visible yet.

3. **#41222** — *Integrate Kanban Board into Desktop App* (4 comments, 6 👍)
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/41222)
   - Highest reaction count in the dataset. PR #41756 implements desktop-facing Kanban integration. Community strongly wants unified workflow.

4. **#42033** — *langfuse not receiving trace from hermes* (4 comments)
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/42033)
   - O11y pipeline broken for users running self-hosted Langfuse.

5. **#50530** — *google-antigravity 遗留 P2 集成问题汇总* (3 comments, created today)
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/50530)
   - Three P2 integration problems with Google AntiGravity post-sunset: sub-agent crashes, forced re-auth, session breakpoints unrecoverable.

### Most Active PRs (by comment count, though data shows `undefined`)
- **#18652** — *Fix Telegram multi-bot dispatch edge cases* — attached to #10452 epic.
- **#10455** — *feat(gateway): add multi-account telegram routing* — primary implementation for multi-bot.
- **#41756** — *feat(desktop): integrate kanban into the desktop app* — implements #41222.

### Underlying Needs
- **Multi-platform parity**: Users want the same powerful routing and file-handling features across Telegram, Discord, Slack, and email.
- **Desktop unification**: The Kanban board (a multi-agent workflow tool) being separate from the chat interface is a friction point. Users want single-window operations.
- **Provider resilience**: The Gemini/Code Assist sunset is causing cascading failures. Users urgently need AntiGravity support and clear migration paths.

---

## Bugs & Stability

### Critical (P1)
- **#14073** (CLOSED) — *browser orphan reaper trusts /tmp PID files, can SIGTERM arbitrary same-user processes*
  - [Issue](https://github.com/NousResearch/hermes-agent/issues/14073)
  - Security vulnerability where the browser orphan reaper sends SIGTERM to PIDs without verifying they belong to Hermes. **Closed** — fix presumably merged.

### High Priority (P2) — Reported or Updated Today

| Issue | Description | Has Fix PR? | Status |
|-------|-------------|-------------|--------|
| #50530 | Google AntiGravity: sub-agent crash, forced re-auth, 400 errors | No | New today |
| #50292 | Bedrock: non-Claude models crash when config default is Claude | ✅ #50578 | Open |
| #50485 | MCP OAuth flow times out at 40s during interactive browser auth | No | New today |
| #50449 | Desktop "Thinking" toggle snaps back on; config writes stranded key | No | Open |
| #50438 | TUI sessions don't record cwd; Desktop groups under default workspace | No | Open |
| #49008 | OpenAI Codex image generation plugin fails with HTTP 400 | ✅ #50579 | Open |
| #49983 | OpenRouter free models fail with HTTP 404 after 3 retries | No | Open |
| #35980 | Oneshot fails closed without final response (Copilot/gpt-5.5) | No | Open |

### Moderate (P3) — Reported or Updated Today
- **#37917** — Windows Desktop: Ctrl+/- zoom does nothing (2 comments, 2 👍)
- **#50554** (CLOSED) — Desktop composer image layout: multi-image vertical stacking wastes horizontal space
- **#50537** (open) — Duplicate auto-generated session titles cause unhandled ValueError (✅ #50575 fixes)
- **#50504** (open) — "Thinking" toggle snapping back (related to #50449)

### Regression Watch
- **Google Gemini/Code Assist sunset** (June 18) has created a cluster of P2 issues (#29294, #49701, #49705, #50338, #44943, #50530). The provider is dead for consumer tiers. Users on free/gemini-3.5-flash get HTTP 404. The migration to AntiGravity is incomplete and has its own bugs (#50530).

---

## Feature Requests & Roadmap Signals

### Strong Signals (PR exists or high community engagement)

1. **Multi-Telegram bot support** (#10452)
   - PRs #10455 and #18652 are active. Likely for v0.17.0.
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/10452)

2. **Kanban board in Desktop** (#41222, 6 👍)
   - PR #41756 implements the desktop-facing integration. Strong user desire for unified workflow.
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/41222)

3. **AntiGravity CLI support** (#44943, 5 👍)
   - Closed as duplicate; but the underlying need is urgent since Gemini CLI is discontinued. #50530 shows AntiGravity integration still has P2 bugs.
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/44943)

4. **Desktop minimize to system tray** (#50167)
   - Closed as duplicate; users want background operation without app exit.
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/50167)

### Early-Stage Proposals

5. **Dynamic thinking mode toggle via model self-detection** (#50293)
   - Model signals `[ESCALATE_THINKING: true]` and Hermes auto-launches deep reasoning.
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/50293)

6. **Background self-review tool whitelist configurable** (#44672)
   - Allow MCP/memory-provider writes in the background review fork.
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/44672)

7. **Self-hosted Mem0 memory provider** (#31135, closed)
   - Add `MEM0_HOST` config for local OSS instance. Multiple stale PRs exist (#27200). May resurface.
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/31135)

8. **Convert API errors to human-readable** (#50460)
   - User request for meaningful error messages like "Usage limit resets at YYYY-MM-DD."
   - [Issue](https://github.com/NousResearch/hermes-agent/issues/50460)

### Prediction for Next Version (v0.17.0)
- **Very likely**: Multi-Telegram bot support, Kanban desktop integration, AntiGravity provider fixes, file-type agnostic gateway, session title robustness.
- **Possibly**: System tray minimize, human-readable errors, Mem0 self-hosted option.
- **Unlikely**: Dynamic thinking toggle, background review whitelist (still in discussion).

---

## User Feedback Summary

### Pain Points (High Frequency)
1. **Intel Macs cannot run Hermes Desktop** (#37505, 20+ days open) — DMG is arm64-only. No fix visible. A significant platform exclusion.
2. **Google provider dead after sunset** — Users on free/gemini-3.5-flash are stuck with HTTP 404. Migration to AntiGravity is incomplete and buggy. Several users are creating duplicate issues (#49701, #49705, #50338).
3. **MCP OAuth timeout** (#50485, new today) — 40-second timeout is too short for interactive browser-based authorization. Blocks integration with Notion MCP and similar services.
4. **OpenRouter free tier broken** (#49983) — "No allowed providers available" error. Affects users on limited budgets.
5. **Desktop image composer layout** (#50554, closed with feedback) — Multi-image vertical stacking wastes space; users want horizontal flex-wrap.
6. **Config changes not taking effect** (#50553, closed) — Space-separated keys in `config set` silently fail. Fix PR #50574 addresses this.
7. **Session titles broken** (#50535-50537) — Duplicate titles cause silent failures; cron sessions end up untitled. Fixed by #50575.

### Satisfaction Signals
- **Kanban integration PR** (#41756) received positive engagement — users want this unified view.
- **Multi-Telegram bot features** have 4 👍 on the issue and active PRs — clearly valued by community.
- **File-type-agnostic gateway** (#50563) addresses a long-standing frustration with arbitrary file restrictions.

### Use Cases
- **Multi-bot deployments**: Teams running both user-facing and internal Telegram bots.
- **Desktop-as-hub**: Users want a single window for chat, Kanban, settings, and session management.
- **Self-hosted observability**: Langfuse integration [#42033] is important for power users.
- **Cross-platform parity**: Requests span Windows (zoom, image layout), macOS (Intel support), and Linux.

---

## Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Problem | For |
|-------|-----|---------|-----|
|

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*