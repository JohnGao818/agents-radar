# OpenClaw Ecosystem Digest 2026-07-21

> Issues: 353 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-21 02:14 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

## OpenClaw Project Digest – 2026-07-21

### 1. Today's Overview
The project is experiencing very high activity, with **353 issues** and **500 PRs** updated in the last 24 hours. Among issues, 225 remain open and 128 were closed; PRs saw 110 merged/closed against 390 still open. No new releases were published today. The community is heavily engaged in triaging regressions and reliability problems, particularly around session state loss, context compaction failures, and platform-specific message delivery (Telegram, Discord, Google Chat). The maintainer team is actively reviewing and merging fixes for high-priority bugs, with several PRs labelled P0/P1 moving through the pipeline.

### 2. Releases
**None** – no new versions were released today.

### 3. Project Progress
**Merged/closed PRs today:** 110 PRs were merged or closed. Notable changes include:

- **Plugin host command cleanup** – `#111602` (open) fixes orphan child processes after time-out by killing the process tree.
- **Stuck-session recovery guard** – `#111622` (open) adds run-handle identity checks to prevent cross-run interference.
- **TTS text churn elimination** – `#83988` (open) defers text settlement for final-mode TTS in Telegram.
- **Dev mode env suppression** – `#112011` (open) stops dev gateways from inheriting shell environment auto-configuration.
- **Cron task history pruning** – `#111938` (open) ages out stale terminal cron rows after 30 days.
- **MiniMax provider response shape fix** – `#111696` (open) adapts to new API shape.
- **MCP disabled flag honored** – `#108676` (open) prevents spawning disabled servers.
- **Prototype pollution prevention** – `#107978` (open) blocks `__proto__` in JSON Schema hydration.
- **Amazon Bedrock malformed image handling** – `#111872` (open) provides graceful error on bad base64.
- **Sidebar naming parity & iOS roster pagination** – `#112004` (open) synchronises web/iOS UI.
- **Novita static model catalog** – `#111621` (open) exposes models correctly.
- **Security audit symlinked skills** – `#111801` (open) follows symlinks for workspace skills.
- **Exec tool result redaction** – `#81185` (open, large PR) prepares redaction of exec payloads.
- **npm 12 JSON shape fix** – `#109699` (closed) resolved install metadata issues.
- **SSRF bypass via DNS** – `#111098` (open) uses `isIP` to guard loopback checks.
- **Canvas snapshot validation** – `#108987` (open) normalises base64 handling.
- **Configless gateway rebind** – `#111841` (open) allows activation of standalone gateways without explicit model config.
- **Preserve invalid config during baseline setup** – `#112010` (open) prevents data loss.
- **Fixed typingMode "message" start** – `#111601` (open) delays typing indicator.
- **OTel diagnostics for one-shot agents** – `#100845` (open) exports telemetry from `--local` runs.
- **User naming for new agents** – `#112009` (closed) fixes bootstrap prompt.
- **Board fixture dropdown legibility** – `#111998` (open) fixes theme contrast.
- **UI re-render after input history navigation** – `#111890` (open).
- **Maturity scorecard parallelism** – `#112008` (open) speeds up QA evidence generation.
- **Subagent native announceTarget** – `#101248` (open, large) implements routing for subagent completions.
- **Session stream mode command** – `#93218` (open) adds per-session streaming control.
- **Cron payload timeout override clearing** – `#111917` (open) allows removal of stored timeout.
- **Discord voice CDN upload cancellation** – `#111269` (open) cancels unread body to avoid leaks.

### 4. Community Hot Topics
The most active discussions (by comment count and reactions) centre on reliability and security:

- **Tool outputs rendered as images** – [#99241](https://github.com/openclaw/openclaw/issues/99241) (23 comments, 2 👍) – long-running tool results collapse into unreadable image placeholders, breaking agent reasoning. Still open, rated **Platinum Hermit**.
- **Turn-completion stall regression** – [#88312](https://github.com/openclaw/openclaw/issues/88312) (22 comments, 5 👍) – Codex-backed multi-tool turns stall since 2026.5.27. Now closed, indicating a fix was applied.
- **Memory trust tagging** – [#7707](https://github.com/openclaw/openclaw/issues/7707) (19 comments) – requests source-based trust levels for memory to prevent poisoning. Open since February.
- **Telegram session timeouts** – [#87744](https://github.com/openclaw/openclaw/issues/87744) (17 comments, 3 👍) – Codex-backed Telegram turns repeatedly time out on 2026.5.27. Still open, Diamond Lobster.
- **False follow-up promises** – [#58450](https://github.com/openclaw/openclaw/issues/58450) (16 comments, 4 👍) – agent claims it will follow up but never starts an action. Open three months.
- **Masked secrets** – [#10659](https://github.com/openclaw/openclaw/issues/10659) (15 comments, 4 👍) – requests a system to hide raw API keys from agents. Open since February.

Underlying needs: Users are frustrated by reliability regressions that break multi-turn workflows, especially across different chat platforms (Telegram, Discord, Slack, Google Chat). There is a strong desire for **session-level controls** (streaming mode, turn limits, timeout overrides) and **security hardening** (secret masking, permission manifests, denylists for exec). The community is also watching the analysis of leaked Claude Code source (issues #58730, #58398) and pushing for better compaction architecture and sandbox isolation.

### 5. Bugs & Stability
Several high-severity bugs remain open, many with P1 priority and Platinum Hermit/Diamond Lobster ratings:

| Bug | Severity | Status | Fix PR? |
|-----|----------|--------|---------|
| Tool output as image attachment ([#99241](https://github.com/openclaw/openclaw/issues/99241)) | Critical (agent cannot read own output) | Open | None linked |
| Telegram time-out loop ([#87744](https://github.com/openclaw/openclaw/issues/87744)) | Critical (sessions fail permanently) | Open | None linked |
| Context overflow auto-compaction loop ([#78562](https://github.com/openclaw/openclaw/issues/78562)) | High (repeated compaction with no progress) | Open | None linked |
| Subagent completion fails on inactive session ([#92076](https://github.com/openclaw/openclaw/issues/92076)) | High (message loss) | Open | None linked |
| Google Chat space messages silently ignored ([#58514](https://github.com/openclaw/openclaw/issues/58514)) | Medium (DM works, groups fail) | Open | None linked |
| Discord gzip decompression failure on Node v26 ([#79752](https://github.com/openclaw/openclaw/issues/79752)) | Medium (platform-specific) | Closed | Likely fixed |
| Runtime tool surface returns blank after gateway operations ([#99586](https://github.com/openclaw/openclaw/issues/99586)) | High (tool surface becomes invisible) | Open | None linked |
| Active Memory + Codex causes long latencies and hook timeouts ([#86996](https://github.com/openclaw/openclaw/issues/86996)) | High (unusable for Telegram) | Open | None linked |
| Event loop frozen, HTTP timeouts ([#56733](https://github.com/openclaw/openclaw/issues/56733)) | Critical (Gateway unresponsive) | Open | None linked |
| Anthropic provider disappears from model picker ([#109017](https://github.com/openclaw/openclaw/issues/109017)) | Medium (UX friction) | Open | None linked |
| models.json writes apiKey as plain string ([#88562](https://github.com/openclaw/openclaw/issues/88562)) | High (security leak) | Open | None linked |

Regressions reported today: The majority of open P1 bugs are labelled as regressions that appeared in versions 2026.5.27, 2026.5.5, or 2026.5.20. No new regression was filed today, but existing ones remain unresolved.

### 6. Feature Requests & Roadmap Signals
Long-standing feature requests with strong community support continue to accumulate:

- **Memory Trust Tagging by Source** ([#7707](https://github.com/openclaw/openclaw/issues/7707)) – open since Feb, 19 comments. Could become a priority after the recent focus on security.
- **Masked Secrets** ([#10659](https://github.com/openclaw/openclaw/issues/10659)) – open since Feb, 15 comments, 4 👍. Likely to be addressed given the PR [#81185](https://github.com/openclaw/openclaw/pull/81185) on exec tool redaction.
- **Skill Permission Manifest** ([#12219](https://github.com/openclaw/openclaw/issues/12219)) – open since Feb, aligns with security audit improvements (see PR [#111801](https://github.com/openclaw/openclaw/pull/111801)).
- **Per-model generation timeout** ([#8724](https://github.com/openclaw/openclaw/issues/8724)) – open since Feb, 5 comments. Could appear alongside the new cron timeout override capabilities.
- **`session:end` internal hook** ([#10142](https://github.com/openclaw/openclaw/issues/10142)) – open since Feb, 5 comments. Useful for workflow orchestration.
- **`maxTurns`/`maxToolCalls` limit** ([#9912](https://github.com/openclaw/openclaw/issues/9912)) – open since Feb, 5 comments. Could be implemented as a session-level config.
- **Exec sandbox isolation** ([#58730](https://github.com/openclaw/openclaw/issues/58730)) – open since March, inspired by Claude Code leak. High probability of being addressed given security trend.
- **Multi-layer compaction** ([#58398](https://github.com/openclaw/openclaw/issues/58398)) – also from Claude Code analysis. Could reduce compaction-related bugs.

Prediction for next version: Likely includes the **subagent announce routing** (PR [#101248](https://github.com/openclaw/openclaw/pull/101248)), **exec result redaction** (PR [#81185](https://github.com/openclaw/openclaw/pull/81185)), **session stream mode** (PR [#93218](https://github.com/openclaw/openclaw/pull/93218)), and security improvements around prototype pollution and secret handling.

### 7. User Feedback Summary
Real user pain points expressed in the last 24 hours include:

- **Reliability frustration:** Multiple reports of agents "stopping before confirming turn complete" (#88312), sessions that cannot deliver answers (#87744), and compaction loops that make the agent unusable (#78562, #59618). Users describe a "retry loop" that never recovers.
- **Message loss and invisibility:** Tool outputs becoming image placeholders (#99241) and agent messages being buried by system events (#64810) cause users to feel answers are "swallowed".
- **Platform fragmentation:** Bugs specific to Google Chat spaces (#58514), Slack multi-workspace (#58523), Discord gzip (#79752), and Telegram topics (#64810) indicate that core message delivery paths are not robust across all chat backends.
- **Security concerns:** Users explicitly ask for protection against credential theft (#10659, #12219) and prompt injection (#7707). The leaked Claude Code source has raised expectations for better sandboxing and compaction.
- **Configuration pitfalls:** Users struggle with model picker missing Anthropic models (#109017), exec failing on LAN (#94032), and secrets being written as plaintext (#88562). These create a perception of instability.
- **Positive signals:** The PR activity and responsiveness from maintainers (e.g., closing #88312, fixing #109699) are appreciated. The upcoming exec redaction and session stream mode are well-received features.

### 8. Backlog Watch
Important issues that have been open for months without a fix or maintainer response:

- **#7707** – Memory Trust Tagging (Feb 3, 19 comments, no assignee). Stale label applied.
- **#10659** – Masked Secrets (Feb 6, 15 comments, 4 👍). Linked to open PR #81185 but PR is still in proof stage.
- **#58450** – False follow-up promises (Mar 31, 16 comments, 4 👍). Stale, no fix PR.
- **#8299** – Config option to suppress sub-agent announce (Feb 3, 8 comments). Stale.
- **#39406** – Suppress transient tool error warnings (Mar 8, 7 comments). Stale.
- **#12219** – Skill Permission Manifest (Feb 9, 6 comments). Stale.
- **#6615** – Exec approval denylist (Feb 1, 8 comments, 8 👍). Linked open PR exists but stalled.
- **#58514** – Google Chat space messages ignored (Mar 31, 8 comments). Stale.
- **#56733** – Event loop frozen (Mar 29, 6 comments). Stale, no fix PR.
- **#86684** – Subagent wake compacts parent branch at low usage (May 26, 8 comments). Needs live repro.

These long-unresolved issues, especially those with P1 priority and high community engagement, represent significant risk to user trust if not addressed soon. The maintainers should consider triaging at least the top 5 (by comment count or security impact) in the next sprint.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## 1. Ecosystem Overview
The personal AI assistant and agent open-source landscape is entering a phase of rapid maturation, with projects facing twin pressures: delivering reliable multi-turn workflows across diverse chat platforms and hardening security against credential theft and prompt injection. Both OpenClaw and Hermes Agent are building comprehensive agent runtimes, but they emphasize different layers of the stack. OpenClaw focuses on core gateway reliability, session recovery, and enterprise-grade security controls, while Hermes Agent prioritizes rapid iteration, cross-platform session bridging, and desktop/TUI experiences. The ecosystem is converging around shared requirements for context compaction, plugin extensibility, and cost-aware model management.

## 2. Activity Comparison

| Metric                       | OpenClaw (core)                          | Hermes Agent                             |
|------------------------------|------------------------------------------|------------------------------------------|
| **Issues updated (24h)**     | 353 (225 open, 128 closed)               | 50 (exact open/closed not specified)     |
| **PRs updated (24h)**        | 500 (390 open, 110 merged/closed)        | 50 (6 merged/closed in top-20 sample)    |
| **Latest release**           | None today (v2026.6.x?)                  | v0.19.0 “Quicksilver” (Jul 20, 2026)    |
| **Release scale**            | No release today                         | ~2,245 commits, ~1,065 merged PRs        |
| **Health score (inferred)**  | Moderate – high bug volume but active triage; many P0/P1 regressions remain open | Moderate – post-release stabilization; critical packaging bug (#68311) undermines trust |
| **Key risk**                 | Proliferation of unresolved P1 regressions (e.g., Telegram timeouts, tool output as images) | sdist contains destructive `os.kill` test; desktop session state inconsistency |

**Assessment:** OpenClaw shows higher raw activity volume, suggesting a larger contributor base, but also a larger backlog of open issues. Hermes Agent’s activity is concentrated in post-release stabilization with fast fix response, but its critical packaging bug is a liability.

## 3. OpenClaw’s Position
- **Advantages vs. peers:** Larger developer community (500 PRs/day vs. 50), more structured bug triage (P0/P1 labels, Platinum Hermit severity ratings), and deeper security focus (prototype pollution prevention, exec result redaction, SSRF fixes). OpenClaw’s PR pipeline includes major features like subagent routing and session stream mode, indicating a more mature development process.
- **Technical approach differences:** OpenClaw appears to be an all-in-one agent runtime with a strong emphasis on gateway orchestration, platform message delivery, and long-session reliability. Hermes Agent leans into cross-platform bridging, desktop/TUI, and plugin extensibility, with a newer release cadence.
- **Community size comparison:** OpenClaw’s 24-hour update counts (353 issues, 500 PRs) are ~7x and ~10x higher than Hermes Agent’s, suggesting a significantly larger contributor and user base. However, Hermes Agent’s v0.19.0 changelog claims 450+ community contributors – a sign of broad engagement despite lower daily activity.

## 4. Shared Technical Focus Areas
Common requirements emerging across both projects include:

- **Session state reliability** – Both projects report bugs with messages lost, sessions stalling, or context incorrectly compacted (OpenClaw #99241, #87744; Hermes #67600, #68261).
- **Cross-platform message delivery** – Users demand consistent behavior across Telegram, Discord, Slack, Google Chat, BlueBubbles, and CLI. Platform-specific bugs (OpenClaw #58514, Hermes #34372) indicate work is needed.
- **Security hardening** – Both communities request secret masking, permission manifests, exec sandboxing, and protection against prompt injection / memory poisoning (OpenClaw #7707, #10659; Hermes #68311 packaging bug).
- **Tool output handling** – Agents cannot always read their own tool outputs when rendered as images (OpenClaw #99241) or when messages are buried (Hermes #68324). Solutions for structured tool output representation are needed.
- **Cron and timeout management** – Both projects have open issues for cron job failures (OpenClaw #111938, Hermes #2788) and per-session timeouts (OpenClaw #8724, Hermes #66868).
- **Plugin/customization extensibility** – OpenClaw’s MCP disabled flag and Hermes’ request for plugin-extensible `send_message` (#64900) show demand for modular backends.

## 5. Differentiation Analysis
| Dimension               | OpenClaw                                | Hermes Agent                            |
|-------------------------|-----------------------------------------|-----------------------------------------|
| **Primary focus**       | Core gateway reliability, security, and multi-platform message delivery | Desktop/TUI, cross-platform session bridging, and rapid feature iteration |
| **Target users**        | Developers and ops who need a reliable agent backend for production deployment | Power users and early adopters who want cutting-edge UI and multi-platform integration |
| **Architecture**        | Monolithic gateway with plugin host, session recovery, and granular session controls | Modular agent with desktop app, CLI, and bridge modules; plugin lifecycle catalog in progress |
| **Risk tolerance**      | Conservative – many open regressions but slow to ship unless confidence is high | Aggressive – v0.19.0 shipped with known rough edges (“Hermes is the mess”) and a critical packaging bug |
| **Community dynamics**  | Large volume of issue/PR activity; maintainer teams actively merging fixes for P0/P1 | Smaller daily volume but high contributor count per major release; post-release stabilization fast |
| **Key differentiator**  | Security-oriented features (prototype pollution, exec redaction, secret masking) | Cross-platform session bridging and desktop session state management |

## 6. Community Momentum & Maturity
- **Activity tiers:** OpenClaw is in a **high-velocity triage** phase – heavy bug reporting and fix merging, but regression pile-up indicates scaling challenges. Hermes Agent is in **post-release stabilization** – major feature drop followed by intense bug patching. Both projects are rapidly iterating, but OpenClaw has higher absolute volume.
- **Stabilization signals:** OpenClaw has not released a new version recently; its backlog of P1 regressions suggests a release may be deferred until critical bugs (e.g., Telegram timeouts, tool output as images) are resolved. Hermes Agent released v0.19.0 yesterday and has opened several fix PRs within 24 hours, indicating a faster release cycle.
- **Maturity indicators:** OpenClaw exhibits more mature engineering practices (structured severity ratings, PR pipelines for large features like subagent routing). Hermes Agent’s packaging bug (#68311) is a serious quality gap, suggesting less mature release automation.

## 7. Trend Signals
From community feedback and bug reports across both projects, several industry trends are clear:

- **Session-level controls are essential.** Users demand the ability to set per-session streaming mode, turn limits, timeout overrides, and explicit session end hooks. Both projects have open issues and in-progress PRs for such controls.
- **Security is the #1 rising concern.** The leaked Claude Code source code has raised expectations for sandbox isolation, memory trust tagging, and credential protection. Features like exec redaction (OpenClaw) and permission manifests are likely to become baseline requirements.
- **Multi-platform consistency is non-negotiable.** Agent users run across Telegram, Discord, Slack, Google Chat, and native apps. Bugs that affect only one platform (e.g., Google Chat spaces, BlueBubbles, Discord gzip) are considered critical for daily drivers.
- **Tool output must be machine-readable.** Agents that cannot parse their own tool outputs due to image rendering or message suppression break autonomous workflows. Structured tool result representation (e.g., JSON instead of images) is a growing demand.
- **Cost and provider management is becoming a feature.** Both projects have issues around model provider configuration, fallback behavior, and API key handling. Users want fine-grained control over which models are used and how costs are tracked.
- **Plugin ecosystems are immature.** Both communities are calling for standardized plugin/hook APIs. Hermes Agent is defining a lifecycle event catalog; OpenClaw has MCP disabled flag and skill permission manifests. This area will be a key differentiator.

**For AI agent developers:** The data shows that building a production-ready agent requires investing heavily in session state persistence, cross-platform message delivery reliability, and security-by-design. Projects that fail to address these fundamental concerns will lose user trust, regardless of feature velocity.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-21

## Today’s Overview

Hermes Agent is in a period of **extremely high velocity**, with 50 issues and 50 pull requests updated in the last 24 hours. The community just received **v0.19.0 “The Quicksilver Release”** (v2026.7.20), a massive milestone incorporating ~2,245 commits, ~1,065 merged PRs, and over 3,300 closed issues from 450+ contributors. Activity today is centred on post-release stabilization — many new bugs focus on desktop session rendering, cron job failures, and platform‑specific integration regressions. The project team is responding quickly, with numerous fix PRs opened in the same 24‑hour window (e.g., #68327, #68329, #68320). Overall project health is strong, though a critical security‑packaging issue (#68311) and several long‑standing feature requests remain open.

## Releases

**v0.19.0 — The Quicksilver Release (v2026.7.20)**  
*Released July 20, 2026*  
Highlights from the release notes:
- ~2,245 commits, ~1,065 merged PRs, ~300,000 insertions, ~36,000 deletions.
- ~3,300 issues closed, 450+ community contributors.
- The release note itself warns: **“Hermes is the mess”** — indicating known rough edges.

While the full changelog was not provided in this digest, the scale suggests major architectural changes (likely the plugin lifecycle catalog, session bridging groundwork, and massive desktop/TUI overhaul). No explicit breaking changes or migration notes were included in the snippet; users upgrading from v0.18.0 should watch for desktop session empty‑sidebar bugs (#67600) and cron job OAuth exhaustion issues (#46511, #66868).

## Project Progress

Six PRs were merged/closed today (from the top‑20 list):
- **#68305** – Auto‑fix lint/formatting (automated bot)
- **#54895** – WebUI now shows runtime model and fallback indicator in sidebar badge (closes #54509)
- **#57642** – Detects and warns when curated OpenRouter models are removed from the live API
- **#46511** – Cron job fallback when credential pool exhausted (OAuth providers) – closed as implemented on main
- **#67817** – Telegram connection fix for ‘HTTPXRequest’ attribute read‑only (closed as fixed)
- **#68301** – Native session bridging feature request closed as duplicate (consolidated under another issue)

Features that advanced today include: fallback model visibility in the UI, OpenRouter model staleness detection, and multiple desktop session rendering fixes (see Bugs & Stability).

## Community Hot Topics

| Issue/PR | Type | Comments | Summary |
|----------|------|----------|---------|
| [#67600](NousResearch/hermes-agent Issue #67600) | Bug (P2) | 9 | Desktop session sidebar empty only for `default` profile; backend serves rows, but frontend fails to render |
| [#4335](NousResearch/hermes-agent Issue #4335) | Feature (P3) | 8 | Cross‑platform session context sharing (CLI ↔ Telegram) — one of the most requested features |
| [#2788](NousResearch/hermes-agent Issue #2788) | Bug (P2) | 6 | Cron jobs never run or fail silently – no logging |
| [#64900](NousResearch/hermes-agent Issue #64900) | Feature (P3) | 5 | Allow plugins to extend `send_message` schema/dispatch – a key extensibility gap |
| [#64231](NousResearch/hermes-agent Issue #64231) | Chore (P3) | 5 | Define lifecycle‑event catalog and batch‑triage pending hook PRs – maintainer attention needed |
| [#34372](NousResearch/hermes-agent Issue #34372) | Bug (P2) | 5 | BlueBubbles duplicate message processing (every iMessage handled twice) |
| [#68244](NousResearch/hermes-agent Issue #68244) | Bug (P2) | 4 | After update with “not restoring local changes”, agent won’t start at all |
| [#68311](NousResearch/hermes-agent Issue #68311) | Bug (P1) | 3 | **Critical**: every published sdist ships a test that can kill the user’s entire login session (`os.kill(-1, SIGTERM)`) |

The underlying need in the most active discussions is **session predictability and state consistency** — users experience messages landing in wrong sessions, disappearing assistant messages, and lost context across platforms. The BlueBubbles double‑processing (#34372) and empty sidebar (#67600) are particularly frustrating for daily‑driver users.

## Bugs & Stability

**P1 – Critical**
- [#68311](NousResearch/hermes-agent Issue #68311): Every published sdist from 0.13.0 to 0.19.0 contains a test file that can execute `os.kill(-1, SIGTERM)` if run outside the test suite. **No fix PR yet** — users should avoid `pip install hermes-agent[sdist]` until a patch release (likely v0.19.1).

**P2 – High Impact**
- [#67600](NousResearch/hermes-agent Issue #67600): Desktop session sidebar empty for `default` profile (named profiles work). No fix PR identified yet.
- [#68244](NousResearch/hermes-agent Issue #68244): Update destroys ability to restart agent/dashboard after declining restore prompt. No fix PR yet.
- [#68324](NousResearch/hermes-agent Issue #68324): Desktop assistant messages vanish when switching chats (user messages remain). Fix PR [#68329](NousResearch/hermes-agent PR #68329) opened today.
- [#68261](NousResearch/hermes-agent Issue #68261): TUI skill credential prompts routed to wrong session. No fix PR.
- [#34372](NousResearch/hermes-agent Issue #34372): BlueBubbles double‑handles every iMessage (still open after months). Fix PR [#45317](NousResearch/hermes-agent PR #45317) is open.
- [#29866](NousResearch/hermes-agent Issue #29866): `brew upgrade` breaks TLS certificates – all platforms fail. No fix PR.

**P3 – Moderate**
- [#68300](NousResearch/hermes-agent Issue #68300) (implied by PR #68319): Telegram rich‑hint import crashes if Telegram extra not installed. Fix PR [#68319](NousResearch/hermes-agent PR #68319) opened.
- [#55369](NousResearch/hermes-agent Issue #55369): Union `integer|string` tool args drop leading zeros (e.g., `"007"` → `7`). No fix PR.
- [#66868](NousResearch/hermes-agent Issue #66868): Cron job model calls fail 401 outside runtime session (provider collapses to “custom”). No fix PR.

## Feature Requests & Roadmap Signals

- **Cross‑platform session bridging** (#4335, #68301) – the most upvoted feature (👍2) and consolidated as a duplicate. Likely a roadmap item for v0.20.0.
- **Plugin extensibility for `send_message`** (#64900) – central to allowing custom platform backends. Decision needed.
- **Lifecycle event catalog & hook standard** (#64231) – P3 but requested by maintainer `teknium1` – suggests internal prioritisation.
- **MCP Server Management CLI** (#690) – another long‑standing gap (created Mar 2026). Could appear in next minor release.
- **Configurable keybindings** (#4256) – +6 upvotes, strong demand from power users. No movement yet.
- **Skills callable mid‑prompt** (#67316) – limited UX; likely to be fixed soon.

**Prediction for v0.20.0:** Based on activity, the plugin lifecycle catalog (#64231) and session bridging (#4335) could land, alongside fixes for the most critical P1 bugs (#68311).

## User Feedback Summary

- **Pain points:** Desktop session state remains the biggest friction – empty sidebar, disappearing assistant messages, wrong‑session routing. Users report “massive skill pollution” (#57626) when sub‑agents receive skill‑library injections. Cron job reliability is a recurring theme (#2788, #66868).
- **Use cases:** Many users run Hermes across multiple platforms (Telegram, Discord, BlueBubbles, Slack). They expect seamless context sharing between CLI, desktop, and mobile gateways. The lack of unified session state is a top complaint.
- **Satisfaction:** The release cadence and community responsiveness are generally well received (450+ contributors). However, the `sdist` packaging bug (#68311) could erode trust if not fixed quickly.

## Backlog Watch

Issues that have remained unanswered or in low‑priority state for a long time, needing maintainer triage:

| Issue | Created | Priority | Summary | Notes |
|-------|---------|----------|---------|-------|
| [#2788](NousResearch/hermes-agent Issue #2788) | 2026-03-24 | P2 | Cron jobs never run / silent failures | No maintainer response; 6 comments |
| [#4335](NousResearch/hermes-agent Issue #4335) | 2026-03-31 | P3 | Cross‑platform session sharing | High demand (👍2); 8 comments; stale |
| [#690](NousResearch/hermes-agent Issue #690) | 2026-03-08 | P3 | MCP server management CLI | Created by maintainer `teknium1` – likely stalled |
| [#2228](NousResearch/hermes-agent Issue #2228) | 2026-03-20 | P2 | System error messages appear as role=user | No PR; 3 comments |
| [#4256](NousResearch/hermes-agent Issue #4256) | 2026-03-31 | P3 | Configurable keybindings | 👍6; very popular; no activity |
| [#2513](NousResearch/hermes-agent Issue #2513) | 2026-03-22 | P3 | Custom provider lacks context length auto‑detection | 3 comments; needs maintainer decision |
| [#2975](NousResearch/hermes-agent Issue #2975) | 2026-03-25 | P3 | WhatsApp bridge misses macOS Node runtimes | 4 comments; no progress |
| [#3944](NousResearch/hermes-agent Issue #3944) | 2026-03-30 | P2 | Slack integration fails with dependency warning | 5 comments; still open |

These issues affect adoption, especially for power users and those relying on cron or multi‑platform setups. The project would benefit from a dedicated backlog‑triage session.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*