# OpenClaw Ecosystem Digest 2026-06-19

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-19 03:55 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-19

## 1. Today's Overview

OpenClaw remains in a phase of intense active development and community debugging. In the last 24 hours, 500 issues and 500 pull requests have been updated, with 31 issues closed and 58 PRs merged or closed. The project has 469 open issues and 442 open PRs, indicating a high volume of work in progress. No new releases were published today. The majority of recent activity centers on session-state bugs, provider integration regressions, and channel-specific delivery issues—particularly around Codex/OpenAI, Telegram, and Discord. Several high-priority issues are accumulating maintainer reviews and product decisions, suggesting the team is actively triaging but may be resource-constrained.

## 2. Releases

**None.** No new versions were published today.

## 3. Project Progress

Notable merged/closed pull requests from the top 30 PRs:

- **#94453** (closed) — `fix: default cron runMode to "due" instead of "force" (#94270)`  
  A security-focused fix that prevents unintended execution of scheduled jobs outside their time windows by defaulting `runMode` to `"due"` (respecting schedule guards) instead of `"force"`.  
  [PR #94453](https://github.com/openclaw/openclaw/pull/94453)

- **#89203** (closed) — `refactor: route SDK session compatibility through seam`  
  Routes the public plugin SDK and runtime session-entry helpers through a file-backed session accessor seam, while keeping legacy exports as deprecated compatibility aliases. This is part of a larger safe-sync-file story.  
  [PR #89203](https://github.com/openclaw/openclaw/pull/89203)

Additionally, several open PRs are progressing toward maintainer review or automerge:

- **#86719** — `fix(skills): retarget stale plugin skill symlinks` (automerge)
- **#94478** — `fix(doctor): repair legacy Codex route persistence` (automerge)
- **#93814** — `fix(trajectory): export legacy v1 sessions without entry timestamps` (automerge)
- **#84794** — `Clean up isolated cron sessions after runs` (automerge)
- **#94746** — `fix(note): prevent clack from re-breaking copy-sensitive tokens` (automerge)

These indicate steady progress on CLI maintenance and export hygiene.

## 4. Community Hot Topics

The most active issues by comment count and reactions:

- **#86538** (11 comments, 1 👍) — **Session write-lock timeouts block subagent delivery lanes**  
  A P1 diamond lobster bug where JSONL write-lock contention stalls main, cron, and subagent lanes. Users report this as a persistent reliability issue.  
  [Issue #86538](https://github.com/openclaw/openclaw/issues/86538)

- **#84516** (11 comments, 2 👍) — **Codex app-server: long agent replies silently truncated at ~1000-1100 chars**  
  A platinum hermit bug affecting headless Codex/OAuth agents. The model does not abort but responses are cut mid-sentence.  
  [Issue #84516](https://github.com/openclaw/openclaw/issues/84516)

- **#54531** (11 comments, 1 👍) — **feat: Force reply to originating channel (Telegram/Discord/WhatsApp)**  
  A long-standing feature request (since March) that remains open and stale, but has high community interest.  
  [Issue #54531](https://github.com/openclaw/openclaw/issues/54531)

- **#85103** (10 comments, 1 👍) — **Model fallback chain not triggered on provider-wide quota exhaustion**  
  Diamond lobster P1 bug where `EmbeddedAttemptSessionTakeoverError` blocks fallback when the primary provider hits a 429.  
  [Issue #85103](https://github.com/openclaw/openclaw/issues/85103)

- **#59330** (9 comments, 14 👍) — **Control UI Raw mode permanently disabled since 2026.3.31**  
  A closed issue (but recently updated) with the highest reaction count. The fix appears to have been applied, but the volume of reactions shows how disruptive this regression was.  
  [Issue #59330](https://github.com/openclaw/openclaw/issues/59330)

The underlying needs span three themes: **(1)** session isolation and concurrency reliability, **(2)** provider fallback and truncation handling, and **(3)** channel reply fidelity. These dominate the community's attention.

## 5. Bugs & Stability

**Critical (P1 / Diamond Lobster)** — multiple new and active regressions:

- **#86538** — Session write-lock timeouts blocking delivery lanes. No fix PR directly linked.  
- **#84516** — Codex truncation at ~1000 chars. No fix PR.  
- **#86519** — Duplicate replies on Telegram after 5.20 update. Persistent across versions.  
- **#85103** — Fallback chain not triggered on quota exhaustion.  
- **#85251** — Codex turn goes silent after `notification:turn/started`.  
- **#94570** (created today) — Discord channel sessions lose context after reset.  
- **#84903** — Single stalled session blocks entire Gateway event loop (isolation failure).  
- **#85030** — MCP tools not injected into subagent sessions.  
- **#83184** — Heartbeat-driven agent replies leave `pendingFinalDelivery` stuck.

**Notable P1 regressions with linked fixes in progress:**

- **#86050** (regression) — Gateway buffers claude-cli stream events, surfaces only final message. A fix PR may be in review.  
- **#83736** — Gateway should tolerate minor node version skew during upgrades. Linked PR exists.  
- **#84610** — Gateway loops with SIGTERM after upgrade on WSL2. No fix PR yet.

**Recently closed bugs:**

- **#94309** (closed today) — Telegram Desktop does not offer Quote & Reply on OpenClaw bot messages. The fix appears to have been identified.  
- **#83964** (closed) — `@openclaw/codex` `ERR_MODULE_NOT_FOUND` for package `openclaw`. Resolved.

**Overall stability assessment:** The project has a high density of P1 bugs, many impacting session state and message delivery. The number of PRs in review suggests the core team is actively fixing, but the fix pipeline may be slower than the rate of bug reports. Users should expect intermittent delivery failures and may need to monitor the open bug list before upgrading.

## 6. Feature Requests & Roadmap Signals

Several enhancement issues have accumulated and are likely candidates for the next release:

- **#11665** (P2, Feb 2026) — Webhook session reuse when `sessionKey` is consistent. Multiple comments request multi-turn conversation support in hook contexts. High priority for automation workflows.  
  [Issue #11665](https://github.com/openclaw/openclaw/issues/11665)

- **#7722** (P2, Feb 2026) — Filesystem sandboxing config (`tools.fileAccess`). Security-focused, with 4 👍.  
  [Issue #7722](https://github.com/openclaw/openclaw/issues/7722)

- **#81061** (P2, May) — Pre-routing inbound message hook (`before_route_inbound_message`) for channel bridging.  
  [Issue #81061](https://github.com/openclaw/openclaw/issues/81061)

- **#81913** (P2, May) — Expose stable plugin SDK surface for installed skill workflows.  
  [Issue #81913](https://github.com/openclaw/openclaw/issues/81913)

- **#86237** (P3, May) — Rename `cron` subsystem to disambiguate from system cron. The collision is causing real operational issues.  
  [Issue #86237](https://github.com/openclaw/openclaw/issues/86237)

**Prediction for next version:** Webhook session reuse (`#11665`) and the cron subsystem rename (`#86237`) have the most supporting evidence (comment activity, linked PRs). The plugin SDK surface (`#81913`) may follow as a larger architectural change. Filesystem sandboxing is likely deferred given its security review requirements.

## 7. User Feedback Summary

- **Pain point: Session reliability.** Users report that a single stalled session can block all other sessions (e.g., #84903), and that session takeover errors are opaque (#84583). This erodes trust in day-to-day usage.

- **Pain point: Message delivery failures.** Duplicate replies (#86519), silent truncation (#84516), and channel-specific reply loss (#79308, #82002) are causing confusion, especially in Telegram and Discord groups.

- **Pain point: Upgrade fragility.** Multiple reports of upgrades breaking the Gateway, especially on macOS (#85027) and WSL2 (#84610). Users are forced to restore from backups or reinstall.

- **Positive signal: Community engagement.** Issue reporters provide detailed reproduction steps, logs, and root cause analysis. This indicates a technically sophisticated user base that is invested in improving the project.

- **Frustration: Backlog of decisions.** Several P1 issues have been awaiting maintainer review or product decision for weeks (e.g., #54531, #11665). Users express dissatisfaction with the pace of triage.

## 8. Backlog Watch

**Issues that have been open >30 days without a maintainer response or fix PR:**

- **#54531** (March 25) — Force reply to originating channel. Stale label. 11 comments.  
- **#11665** (Feb 8) — Webhook session reuse. 9 comments, linked PR open.  
- **#7722** (Feb 3) — Filesystem sandboxing. 8 comments.  
- **#81061** (May 12) — Pre-routing hook. 7 comments, linked PR open.  
- **#81525** (May 13) — media-understanding routes images without validation. 5 comments.

**PRs needing maintainer attention:**

- **#86584** — `fix(agents): gate owned-write publish on pre-append fingerprint` — status: `⏳ waiting on author` but also `needs-maintainer-review`.  
- **#86577** — `fix(discord): persist inbound replay recovery` — status: `⏳ waiting on author`.  
- **#86627** — `Keep core doctor health in contribution order` — status: `👀 ready for maintainer look`.  

These items represent the highest debt in the project. Without resolution, they risk accumulating more community frustration and delaying stability improvements.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem

## 1. Ecosystem Overview

The personal AI assistant and agent open-source landscape is characterized by intense, community-driven development with a strong emphasis on session reliability, provider integration, and multi-platform delivery. Two major projects—OpenClaw and Hermes Agent—dominate the conversation, both exhibiting high issue/PR throughput but diverging in architectural approach and maturity. The ecosystem is actively grappling with session state consistency, provider fallback logic, and channel-specific delivery fidelity, while feature demand is shifting toward multi-agent orchestration, plugin SDK stabilization, and platform parity. Neither project has released a new version in the past 24 hours, but both show sustained development velocity, with OpenClaw processing 58 PRs and 31 issues closed versus Hermes's 2 PRs and 5 issues closed in the same period.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| Issues updated (24h) | 500 | 50 |
| PRs updated (24h) | 500 | 50 |
| Open issues | 469 | 45 |
| Open PRs | 442 | 48 |
| Issues closed (24h) | 31 | 5 |
| PRs merged/closed (24h) | 58 | 2 |
| Release today | None | None |
| Critical (P1) bugs active | 9+ | 4 |
| Health score* | Moderate - High bug density, slow triage, active fix pipeline | Moderate - Fewer bugs, faster issue closure, but new P1s emerging |

**Health score** is a qualitative assessment based on bug-to-fix ratio, triage responsiveness, and backlog debt.

**Key observation:** OpenClaw operates at roughly 10x the issue/PR volume of Hermes Agent, but its closure rate is proportionally lower (31/500 vs 5/50). This suggests either a larger user base generating more reports, or a more strained triage process. Hermes closes issues at a higher rate relative to incoming volume, indicating a more responsive maintenance cycle.

## 3. OpenClaw's Position

**Advantages over peers:**
- **Scale of community engagement:** 500 issues and 500 PRs updated daily vs Hermes's 50 each—indicating a significantly larger active user and contributor base.
- **Channel breadth:** Specific adapters for Telegram, Discord, and WhatsApp are under active debugging, suggesting more mature multi-platform support.
- **Cron/scheduling subsystem:** A distinct feature with security-conscious design (defaulting to `"due"` instead of `"force"`) that Hermes lacks.
- **Session state management:** Dedicated work on file-backed session accessors, write-lock isolation, and subagent delivery lanes.

**Technical approach differences:**
- OpenClaw uses a **JSONL write-lock** session persistence model, which is causing contention issues (P1 bug #86538). Hermes uses SQLite (`state.db`, `sessions.json`) and has its own session data loss bugs (#48519), but the SQLite approach may scale better under concurrent access.
- OpenClaw has a distinct **Gateway** component that buffers stream events and can introduce latency (#86050). Hermes integrates gateway and CLI more tightly.
- OpenClaw's **Codex/OpenAI integration** is a major pain point (truncation, silent turns), whereas Hermes's provider issues center on MCP tool exposure and model fallback.

**Community size comparison:** OpenClaw's raw numbers (469 open issues, 442 open PRs) dwarf Hermes (45 open issues, 48 open PRs). However, this may partly reflect lower triage throughput rather than proportionally larger user base. Hermes's community appears more focused and possibly more technically sophisticated (e.g., detailed Doer/Reviewer deployment reports, WhatsApp guide contributions).

## 4. Shared Technical Focus Areas

Both projects are converging on several critical requirements:

| Focus Area | OpenClaw | Hermes Agent |
|------------|----------|--------------|
| **Session persistence & recovery** | Write-lock timeouts (#86538), session isolation failure (#84903) | Sub-profile session loss (#48519), compressed session ID rotation (#33618) |
| **Provider fallback & truncation** | Quota exhaustion not triggering fallback (#85103), Codex truncation at ~1k chars (#84516) | Provider/model override per turn requested (#41190), empty content fallback fix (#48795) |
| **Channel-specific delivery** | Duplicate Telegram replies (#86519), Discord context loss after reset (#94570) | Telegram not updating in desktop (#48702), Slack/Feishu formatting PRs (#48737, #48807) |
| **Upgrade fragility** | Gateway breaks on macOS (#85027) and WSL2 (#84610) | Update fails on system Python with PEP 668 (#48721) |
| **Plugin/extension capabilities** | SDK session compat refactoring (#89203), exposed plugin SDK surface requested (#81913) | MCP tools not exposed in TUI (#41625), plugin-based routing requested (#41190) |
| **Multi-agent orchestration** | Subagent delivery lanes blocked by write-lock (#86538) | Doer/Reviewer pattern (#34592), delegate profile/model overrides (#35409) |

**Underlying need:** Users demand **reliable, persistent, cross-platform conversations** with graceful degradation when providers fail. Both projects are investing in session isolation and fallback logic, but neither has fully solved the core consistency problem.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Core feature focus** | Session management, cron/scheduling, channel bridging | Multi-agent orchestration, MCP integration, platform formatting |
| **Target user** | Power users and automation engineers needing scheduled jobs and multi-channel delivery | Individual developers and teams needing structured collaboration and platform-rich output |
| **Session architecture** | JSONL write-lock file-based, with seam for SDK compatibility | SQLite (`state.db`, `sessions.json`) with sub-profile support |
| **Community engagement style** | High-volume bug reporting, slower triage, longer-lived feature requests | Lower volume but faster issue resolution, more feature PRs from community |
| **Key differentiator** | Robust cron subsystem with security guards; channel reply fidelity | Doer/Reviewer orchestration; structured data output (tables, cards); i18n framework |
| **Biggest risk** | Write-lock contention can stall entire system; Codex truncation breaks production use | Session data loss under sub-profiles; update failures on system Python |

**Strategic implication:** OpenClaw is positioning as the **reliable infrastructure layer** for personal AI assistants (scheduling, multi-channel, session persistence). Hermes is positioning as the **collaborative agent platform** (multi-agent patterns, rich formatting, extensibility). These are complementary rather than directly competitive—but OpenClaw's current stability challenges undermine its infrastructure narrative.

## 6. Community Momentum & Maturity

**Tier 1: Rapidly iterating, high engagement, stability challenged**
- **OpenClaw:** Extremely high issue/PR volume, active debugging of critical session and delivery bugs, but fix pipeline is slow relative to bug intake. Backlog of decisions (issues open >30 days without maintainer response) suggests maintainer team may be under-resourced. Community is technically sophisticated and invested, but frustration with triage pace is evident.

**Tier 2: Rapidly iterating, moderate engagement, faster fix cycle**
- **Hermes Agent:** Lower raw volume but higher closure rate and more community-contributed PRs (Slack tables, Feishu cards, i18n, delegate improvements). Several P1 bugs fixed today. The Doer/Reviewer pattern and i18n framework indicate active architectural innovation. New P1 bugs (Gateway exit code 75, session data loss) show that stability is still a moving target.

**Maturity assessment:** Neither project has reached a stable release. Both are in **active development with breaking changes and regressions**. OpenClaw shows signs of scaling strain (high bug debt, slow triage), while Hermes is more agile but still lacks production-hardened session reliability.

## 7. Trend Signals

**Industry trends extracted from community feedback:**

1. **Session persistence is the number one reliability requirement.** Both projects have critical bugs where conversations are lost due to write-lock contention, sub-profile state gaps, or compression rotation. Users are unwilling to accept non-deterministic session behavior—this is a barrier to enterprise adoption.

2. **Multi-agent orchestration is shifting from theory to practice.** The Doer/Reviewer pattern in Hermes (#34592) and subagent delivery lanes in OpenClaw (#86538) show real-world demand for structured multi-agent workflows. The market is moving beyond single-agent chatbots toward agent collaboration with memory, delegation, and hindsight.

3. **Provider independence is non-negotiable.** Fallback chains, model takeover, and reseller vs native provider preferring (#48731) are all active pain points. Users want to route around provider outages without losing context.

4. **Platform parity is expected.** Rich formatting (tables, cards, markdown) on messaging platforms like Slack, Feishu, Telegram, and Discord is no longer a nice-to-have—it's a core requirement. Both projects have PRs or issues addressing platform-specific rendering.

5. **Upgrade stability lags feature velocity.** Breaking changes on macOS, WSL2, and system Python environments are causing user churn. The community values backward compatibility and smooth upgrades over novel features.

**Value for AI agent developers:**
- Prioritize **session isolation and recovery** as the foundational reliability primitive before adding orchestration or formatting features.
- Invest in **provider-agnostic fallback architectures** that gracefully handle quota exhaustion, truncation, and silent failures.
- Build **plugin/extension SDKs with stable surfaces** early—both communities are demanding standardized interfaces for skills, tools, and routing hooks.
- Expect **multi-agent patterns** (delegation, review loops, hindsight memory) to become standard within 6-12 months. Prepare for orchestration primitives.
- **Platform formatting libraries** (tables, cards, structured output) will become essential, especially for enterprise and team deployments. Consider contributing to or adopting cross-platform rendering standards.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-19

## 1. Today’s Overview
Hermes Agent continues to show extremely high activity, with **50 issues and 50 pull requests updated in the last 24 hours**. The project maintains a robust community-driven development pace: 45 open issues and 48 open PRs remain, while 5 issues and 2 PRs were closed/merged today. No new releases were published. The conversation is dominated by bug reports (especially around session persistence, MCP integration, and platform-specific adapters) alongside substantial feature contributions (Slack/Feishu table rendering, i18n framework, dashboard usage quotas). Several **P1 (critical) bugs** were fixed today, but new P1 issues appeared, indicating ongoing stability challenges in the gateway and update subsystems.

## 2. Releases
**None** — no new versions were tagged today.

## 3. Project Progress
Two pull requests were merged/closed today (details not available in the top 20 list), and **5 issues were closed**, reflecting concrete progress:

- **P1 FD leak fix** – [#37369](https://github.com/NousResearch/hermes-agent/issues/37369) (Telegram gateway `response_store.db` file descriptor leak) was closed.
- **P1 session data loss fix** – [#41386](https://github.com/NousResearch/hermes-agent/issues/41386) (CLI/Desktop prompts running live-only when `state.db` unavailable) closed.
- **P1 SQLite regression fix** – [#47002](https://github.com/NousResearch/hermes-agent/issues/47002) (`SessionDB.__init__` crash on SQLite without trigram tokenizer in v0.16.0) closed.
- **WhatsApp feature request** – [#47477](https://github.com/NousResearch/hermes-agent/issues/47477) (one-file guide for WhatsApp group sending) closed, likely resolved or superseded.

Several open PRs today address important stability and correctness issues (see *Bugs & Stability*), with commits like replacing `assert` statements with proper error handling and fixing double-counting of cached tokens.

## 4. Community Hot Topics
The most active discussions (by comment count and reactions) highlight key user concerns:

- **Doer/Reviewer dual-role orchestration** – [#34592](https://github.com/NousResearch/hermes-agent/issues/34592) (5 comments) shares a real-world deployment of a parallel execution + hindsight memory pattern. This reflects strong demand for multi-agent collaboration primitives.
- **MCP tools not exposed in TUI** – [#41625](https://github.com/NousResearch/hermes-agent/issues/41625) (5 comments, 1 👍) describes a blocking integration gap: MCP server tools discovered by CLI are invisible to the agent in TUI mode. This is a **P2 bug** with high community impact.
- **Gemma 4 / Ollama compatibility** – [#45924](https://github.com/NousResearch/hermes-agent/issues/45924) (3 comments, 1 👍) reports a basic failure with locally deployed models, indicating provider integration fragility.
- **Mission/project source-of-truth** – [#48011](https://github.com/NousResearch/hermes-agent/issues/48011) (2 comments, 1 👍) calls for a first-class strategic work primitive, signaling users need more structured project context than current memory/skills/session search provide.

## 5. Bugs & Stability
Today’s bug landscape spans from **critical session loss** to **minor diagnostic false positives**. Below is a severity-ranked summary:

| Issue | Component | Severity | Description | Fix PR exists? |
|-------|-----------|----------|-------------|----------------|
| [#48746](https://github.com/NousResearch/hermes-agent/issues/48746) | CLI/Gateway | **P1** | Gateway on macOS self-restart exits with code 75; launchd may treat it as permanent failure → service stuck in zombie state. | Not yet |
| [#48721](https://github.com/NousResearch/hermes-agent/issues/48721) | CLI | **P1** | `hermes update` on system Python (no venv) targets wrong interpreter and hits PEP 668 on macOS Homebrew Python 3.14. | Not yet |
| [#48519](https://github.com/NousResearch/hermes-agent/issues/48519) | Gateway | **P1** | Sub-profile gateway: `sessions.json` populated but `state.db` remains empty → complete session data loss (related to #40344, #46144). | Not yet |
| [#41625](https://github.com/NousResearch/hermes-agent/issues/41625) | TUI | **P2** | MCP tools discovered but not exposed to agent in TUI mode. | Not yet |
| [#33618](https://github.com/NousResearch/hermes-agent/issues/33618) | Agent/CLI | **P2** | Persistent `/goal` lost after context compression rotates session ID. | Not yet |
| [#41517](https://github.com/NousResearch/hermes-agent/issues/41517) | Gateway/TUI | **P2** | Desktop/Dashboard chat worker loses selected profile and falls back to default. | Not yet |
| [#48649](https://github.com/NousResearch/hermes-agent/issues/48649) | CLI/Cron | **P2** | Cron jobs not profile-aware: skills and storage use global paths. | Not yet |
| [#48689](https://github.com/NousResearch/hermes-agent/issues/48689) | CLI | **P2** | `hermes doctor` reports stale npm vulnerability and false-positive `gemini (invalid API key)`. | Not yet |

**Fix PRs submitted today** for several critical issues:
- [#48801](https://github.com/NousResearch/hermes-agent/pull/48801) – double-counting cached input tokens (Codex usage accounting)
- [#48798](https://github.com/NousResearch/hermes-agent/pull/48798) – replaces 4 `assert` statements in production code (browser, Docker) with proper error handling
- [#48802](https://github.com/NousResearch/hermes-agent/pull/48802) – replaces `assert` in API server restart path
- [#48795](https://github.com/NousResearch/hermes-agent/pull/48795) – falls back to `reasoning_content` when model returns empty `content`
- [#48794](https://github.com/NousResearch/hermes-agent/pull/48794) – guards empty length-continuation messages
- [#48804](https://github.com/NousResearch/hermes-agent/pull/48804) – displays active model in `/status` command (fixes [#48715](https://github.com/NousResearch/hermes-agent/issues/48715))

## 6. Feature Requests & Roadmap Signals
A number of high-quality feature requests and PRs indicate likely roadmap direction:

- **Multi-agent orchestration & delegation** – [#34592](https://github.com/NousResearch/hermes-agent/issues/34592) (Doer/Reviewer pattern) and [#35409](https://github.com/NousResearch/hermes-agent/issues/35409) (profile/model override for `delegate_task`) signal growing demand for structured multi-agent workflows. PR [#48806](https://github.com/NousResearch/hermes-agent/pull/48806) tightens the delegate background task contract.
- **Unified plugin-based routing** – [#41190](https://github.com/NousResearch/hermes-agent/issues/41190) proposes a single hook to override provider/model per turn. This would unify fragmented routing logic.
- **Platform parity & rich formatting** – PRs for Slack table blocks ([#48737](https://github.com/NousResearch/hermes-agent/pull/48737)) and Feishu CardKit tables ([#48807](https://github.com/NousResearch/hermes-agent/pull/48807)) show that users expect Hermes to output structured data on messaging platforms.
- **Windows native support** – [#48716](https://github.com/NousResearch/hermes-agent/issues/48716) requests a package to run without Docker/WSL2. This is a recurring request from the Windows community.
- **Configuration hot-reload** – [#47058](https://github.com/NousResearch/hermes-agent/issues/47058) (1 👍) asks for live config changes without restarting the dashboard.
- **Mission/project primitive** – [#48011](https://github.com/NousResearch/hermes-agent/issues/48011) (1 👍) suggests a first-class source-of-truth for strategic work. Given the existing Doer/Reviewer practice, this could become a key feature.

**Likely next-version candidates**: MCP tool exposure fix, profile-aware cron, external context files (PR [#48809](https://github.com/NousResearch/hermes-agent/pull/48809)), i18n framework (PR [#23243](https://github.com/NousResearch/hermes-agent/pull/23243)), and delegate/profile model overrides.

## 7. User Feedback Summary
Real pain points from the community this week:

- **Session data loss** – Users report conversations disappearing when using sub-profiles ([#48519](https://github.com/NousResearch/hermes-agent/issues/48519)) or during context compression ([#33618](https://github.com/NousResearch/hermes-agent/issues/33618)). This erodes trust in long-running sessions.
- **Update failures** – System Python users on macOS/Ubuntu hit PEP 668 errors, making updates unreliable ([#48721](https://github.com/NousResearch/hermes-agent/issues/48721), [#30594](https://github.com/NousResearch/hermes-agent/issues/30594)).
- **Model/provider switching** – Users struggle with `/model` preferring native provider over reseller ([#48731](https://github.com/NousResearch/hermes-agent/issues/48731)) and `/status` not reflecting the active model ([#48715](https://github.com/NousResearch/hermes-agent/issues/48715)).
- **Desktop real-time updates** – Telegram sessions not updating in the desktop app ([#48702](https://github.com/NousResearch/hermes-agent/issues/48702)) limits cross-platform usage.
- **Cron not profile-aware** – Skills and storage from non-default profiles are not honored ([#48649](https://github.com/NousResearch/hermes-agent/issues/48649)).

On the positive side, users are actively contributing solutions (e.g., Doer/Reviewer deployment report, WhatsApp guide) and are enthusiastic about sharing improvements.

## 8. Backlog Watch
Several important items have remained open for weeks and may require maintainer attention:

- [#30594](https://github.com/NousResearch/hermes-agent/issues/30594) (May 22) – `hermes update` lazy-backend refresh fails with PEP 668 when installed against system Python. Still open, no confirmed fix PR.
- [#33618](https://github.com/NousResearch/hermes-agent/issues/33618) (May 28) – Persistent `/goal` lost after context compression. No fix PR yet.
- [#34592](https://github.com/NousResearch/hermes-agent/issues/34592) (May 29) – Doer/Reviewer practice sharing; no maintainer response visible. While not a bug, it signals an unaddressed feature area.
- [#27738](https://github.com/NousResearch/hermes-agent/pull/27738) (May 18) – PR to update `lark-oapi` SDK (Feishu) remains open without review comments.
- [#

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*