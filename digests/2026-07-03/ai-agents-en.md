# OpenClaw Ecosystem Digest 2026-07-03

> Issues: 196 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-03 02:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-03

## Today’s Overview

The project remains highly active, with **196 issues** updated in the last 24 hours (123 open, 73 closed) and **500 pull requests** receiving updates (425 open, 75 merged/closed). A new beta release (v2026.7.1-beta.1) introduces support for OpenAI GPT-5.6 and an external harness attachment feature. However, the issue tracker continues to show a significant number of **P1 regressions and reliability problems**, particularly around session state loss, message delivery failures, and OAuth authentication instability. Several high-severity bugs remain open, suggesting that while feature work progresses, stability and user experience are pressing concerns.

## Releases

**v2026.7.1-beta.1**  
- **OpenAI GPT-5.6 support:** OpenClaw now recognizes the GPT-5.6 model family across catalog, capability, and runtime selection paths. (PR #98333, thanks @steipete-oai)  
- **External harness attachment:** `openclaw attach` launches an external harness against an existing Gateway session.  
- No breaking changes or migration notes were mentioned.

## Project Progress

In the last 24 hours, **75 PRs were merged or closed**. Notable among them:  
- [#96691](https://github.com/openclaw/openclaw/pull/96691) – **fix(browser):** correct `ssrf-runtime` import path to fix lazy-load failure (closed)  
- [#99024](https://github.com/openclaw/openclaw/pull/99024) – **fix(gateway):** tighten CSP `connect-src` from bare `ws:/wss:` to explicit endpoints (closed)  
- [#96894](https://github.com/openclaw/openclaw/pull/96894) – **fix:** detect Cloudflare Sandbox as container environment via `cloudchamber` cgroup (closed)  
- [#99297](https://github.com/openclaw/openclaw/pull/99297) – **fix(shared/text):** strip standalone `<parameter>` tool-call wrappers in assistant visible text (closed)  
- [#99319](https://github.com/openclaw/openclaw/pull/99319) & [#99321](https://github.com/openclaw/openclaw/pull/99321) – **test:** add unit tests for Zod parsing utilities and boolean coercion helpers (both closed)  
- [#99252](https://github.com/openclaw/openclaw/pull/99252) – closed as superseded by #99253 (safety issue – see Bugs & Stability).  

Many other open PRs are actively advancing features such as Signal status reactions ( [#98791](https://github.com/openclaw/openclaw/pull/98791) ), Amazon Bedrock prompt caching ( [#99324](https://github.com/openclaw/openclaw/pull/99324) ), and the long-running SQLite storage flip ( [#98236](https://github.com/openclaw/openclaw/pull/98236) ).

## Community Hot Topics

The following issues received the highest engagement (by comment count and reactions) in the last 24 hours:

- **[#25592](https://github.com/openclaw/openclaw/issues/25592) – Text between tool calls leaks to messaging channels**  
  *33 comments, P1, security/message-loss impact.*  
  Underlying need: agent internal processing text (error handling, acknowledgements) is incorrectly delivered as visible channel messages, degrading UX and risking information leaks.

- **[#88312](https://github.com/openclaw/openclaw/issues/88312) – Codex turn-completion stall regression**  
  *19 comments, P1, regression of #84076.*  
  Underlying need: multi-tool agent turns stall with “Codex stopped before confirming the turn was complete” on version 2026.5.27+, affecting all ChatGPT Plus subscribers.

- **[#92201](https://github.com/openclaw/openclaw/issues/92201) – Anthropic thinking signatures invalid on replay**  
  *18 comments, P1, session-state/message-loss.*  
  Underlying need: embedded runner (Slack) intermittently persists corrupted thinking blocks; recovery logic fails due to generic error text.

- **[#73148](https://github.com/openclaw/openclaw/issues/73148) – Image tool fails with opaque “Failed to optimize image” when sharp is not installed**  
  *14 comments, P1, message-loss.*  
  Underlying need: no clear error message or fallback for missing native dependency; users cannot diagnose the issue.

- **[#38327](https://github.com/openclaw/openclaw/issues/38327) – “Cannot convert undefined or null to object” with Gemini 3.1**  
  *10 comments, P1, regression in 2026.3.2.*  
  Underlying need: embedded agent fails on every message after update; affects Google Vertex users.

- **[#87744](https://github.com/openclaw/openclaw/issues/87744) – Telegram turns time out waiting for turn/completed**  
  *10 comments, P1, session-state/message-loss.*  
  Underlying need: Codex-backed Telegram sessions never reach terminal state after update to 2026.5.27.

- **[#75593](https://github.com/openclaw/openclaw/issues/75593) – Subagents list empty after spawn**  
  *10 comments, P1, session-state.*  
  Underlying need: `/subagents list` shows nothing even after successful spawn; regression of earlier fix.

- **[#35203](https://github.com/openclaw/openclaw/issues/35203) – RFC: Multi-Agent Collaboration Enhancement**  
  *9 comments, P2, feature request.*  
  Underlying need: capability profiling, shared blackboard, layered memory, and token governance to improve multi-agent coordination.

- **[#98416](https://github.com/openclaw/openclaw/issues/98416) – v2026.6.11 dist missing reentrancy guard**  
  *8 comments, P1, session-state/message-loss.*  
  Underlying need: reply session initialization is not serialized, causing conflicts; fix was in source but not in published dist.

## Bugs & Stability

Several severe bugs were reported or updated in the last 24 hours, many with P1 priority:

### Critical / Safety
- **[#99253](https://github.com/openclaw/openclaw/issues/99253) – Assistant self-inserted a fabricated user turn and answered it as real input** (P1, maturity:stable, open)  
  *Safety concern: model hallucinates a user message inside its own response.*  
- **[#98790](https://github.com/openclaw/openclaw/issues/98790) – Concurrent agent-to-agent turn poisons transcript permanently** (P1, data-loss, open)  
  *Race condition leads to unrecoverable session corruption and Anthropic API rejection.*

### Regressions & Reliability
- **[#99305](https://github.com/openclaw/openclaw/issues/99305) – Bedrock Claude Sonnet 5 prompt caching broken** (P2, open)  
  *Zero cache hits; full context re-transmitted every turn, causing 10–20× cost.*  
  *Fix PR: [#99324](https://github.com/openclaw/openclaw/pull/99324) (open, awaiting author).*
- **[#99183](https://github.com/openclaw/openclaw/issues/99183) – Local embedding worker fails with ENOENT after Node upgrade** (P2, open)  
  *Fork() inherits execPath of deleted binary; fix PR [#99318](https://github.com/openclaw/openclaw/pull/99318) submitted.*
- **[#98614](https://github.com/openclaw/openclaw/issues/98614) – sessions_spawn missing scope operator.write (regression in 2026.6.11)** (P1, open)  
  *Blocks agent spawning in OAuth deployments.*
- **[#99046](https://github.com/openclaw/openclaw/issues/99046) – iOS photos permission not recognized when set to Limited Access** (open)  
  *Breaks photo tool on iOS 18+.*

### Message-Loss & Rendering
- **[#99241](https://github.com/openclaw/openclaw/issues/99241) – Tool outputs render as unreadable image attachments** (open)  
  *Agent cannot read its own tool results; renders as “(see attached image)”.*
- **[#99186](https://github.com/openclaw/openclaw/issues/99186) – Cyrillic UTF-8 tool results rendered as image attachment** (closed, P1)  
  *Similar rendering issue for non-ASCII.*
- **[#99071](https://github.com/openclaw/openclaw/issues/99071) – Repeated Codex Apps plugin discovery causing excessive disk I/O** (P1, open)  
  *Potential crash from I/O saturation.*

### OAuth / Auth
- **[#98702](https://github.com/openclaw/openclaw/issues/98702) – Inherited OAuth rejected for built-in runtime** (P1, open)  
  *main works, but sub‑agents fail with same profile.*
- **[#99120](https://github.com/openclaw/openclaw/issues/99120) – OAuth refresh false-green falls back to invalidated credential** (P1, closed)  
  *Credential appears healthy but is actually stale.*

## Feature Requests & Roadmap Signals

The following feature requests have drawn community attention and may influence upcoming releases:

- **[#35203](https://github.com/openclaw/openclaw/issues/35203) – Multi-Agent Collaboration Enhancement** (RFC, P2, 9 comments)  
  *Capability profiling, shared blackboard, layered memory, token cost governance.*  
  *Likely to be partially addressed in a future v2026.8 release.*

- **[#47910](https://github.com/openclaw/openclaw/issues/47910) – Provider fallback by failure class (quarantine auth-broken providers)** (P1, open, 7 comments)  
  *Avoid retrying providers with known bad auth. Strong community desire.*

- **[#75947](https://github.com/openclaw/openclaw/issues/75947) – UI quality update based on UX scoring** (P3, enhancement, 7 comments)  
  *Redesign of config pages for accessibility and readability.*

- **[#81084](https://github.com/openclaw/openclaw/issues/81084) – MSTeams channel-bound agents opt-out from per-thread sessions** (P2, open, 3 comments)  
  *Teams users need a per‑channel session option.*

- **[#77165](https://github.com/openclaw/openclaw/issues/77165) – Auto-generate session titles via AI summarization** (P3, enhancement, 2 comments)  
  *Replace truncated first‑message titles with AI‑generated descriptions.*

- **[#32530](https://github.com/openclaw/openclaw/issues/32530) – Auto-discovery of agent configurations from external workspaces** (P2, enhancement, 3 comments)  
  *Reduce manual registration burden for multi‑agent setups.*

- **[#11623](https://github.com/openclaw/openclaw/issues/11623) – Floating agent bubbles (Clawi) for macOS** (P3, enhancement, 2 comments)  
  *Visual indicator per running agent.*

**Roadmap prediction:** The `provider fallback by failure class` (#47910) has high community support and is already assigned P1; it is a strong candidate for the next minor release. The SQLite storage refactor ([#98236](https://github.com/openclaw/openclaw/pull/98236)) is a major infrastructure change that may land in a 2026.8 beta, unlocking better session management.

## User Feedback Summary

- **Pain points:**
  - **“Text between tool calls leaks to channels”** (#25592) is a long-standing UX issue (since February) that directly impacts daily use.
  - **OAuth reliability** remains a top frustration: tokens appear valid but fail silently, requiring manual re-login (e.g., #99120, #98702, #71865).
  - **Regression fatigue** – multiple users report that stable workflows break after minor updates (e.g., #88312, #98416, #98614).
  - **Tool output rendering** – large, binary, or Cyrillic output is sometimes replaced with unreadable image placeholders (#99241, #99186), breaking the agent’s ability to use its own results.
  - **Multi‑agent state corruption** – concurrent subagent completions and announce steering cause silent message loss (#92433, #98790).

- **Use cases:**
  - Heavy reliance on **multi‑agent workflows** with subagents and inter‑agent messaging (e.g., #35203, #75593, #92433).
  - **Cross‑platform messaging channels** – Telegram, Slack, Discord, Signal, Feishu, and Android/iOS all see active bug reports.
  - **OAuth‑protected deployments** (Codex, OpenAI, Google Vertex) where token management is critical.

- **Satisfaction/dissatisfaction:**
  - While community engagement remains high (many PRs, detailed bug reports), the **volume of P1 regressions** indicates ongoing stability challenges.


---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Open-Source AI Agent Ecosystem
**Date:** 2026-07-03 | **Scope:** OpenClaw, Hermes Agent

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is characterized by rapid feature iteration combined with persistent stability challenges. Both OpenClaw and Hermes Agent are actively shipping new capabilities—OpenClaw with GPT-5.6 support and external harness attachment, Hermes with a growing optional-skill ecosystem and injection-defence hardening—but both are grappling with regressions that erode user trust. The community is demanding better multi-agent state management, reliable OAuth token handling, and cross-platform message delivery guarantees. Across both projects, the most pressing pain points converge on three themes: tool-call leakage into user-facing channels, multi-agent state corruption under concurrency, and silent credential failures that force manual recovery. The ecosystem is maturing but has not yet reached a stability baseline that supports production deployment without careful monitoring.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues updated (24h)** | 196 | 50 |
| **Open issues** | 123 | 43 |
| **Closed issues (24h)** | 73 | 7 |
| **PRs updated (24h)** | 500 | 50 |
| **Open PRs** | 425 | 32 |
| **Merged/closed PRs (24h)** | 75 | 18 |
| **Release status** | Beta v2026.7.1-beta.1 | No release today |
| **P1 open issues** | ~15+ (exact count not provided) | 2–3 |
| **Health score** | Moderate — high throughput, but significant regression backlog | Moderate-high — steady fix pace, but desktop quality lagging |

**Interpretation:** OpenClaw operates at roughly 4× the issue volume and 10× the PR volume of Hermes Agent. This reflects a larger contributor base and broader platform surface (Gateway, browser, multiple LLM providers). However, OpenClaw’s P1 count is also proportionally higher, indicating that velocity has not yet been matched by stability. Hermes Agent shows a healthier closure rate relative to its issue count and has only 1–2 high-severity open bugs, but its desktop experience is accumulating lower-priority defects.

---

## 3. OpenClaw’s Position

**Advantages over peers:**
- **Largest community surface** — 500 PRs/day and 196 issues/day indicate a contributor base that dwarfs most other agent frameworks. This creates a richer ecosystem of integrations, bug reports, and fix contributions.
- **Platform breadth** — supports multiple LLM backends (OpenAI, Anthropic, Bedrock, Gemini, Vertex) and multiple messaging channels (Telegram, Slack, Discord, Signal, Feishu, iOS/Android). Hermes Agent also supports multi-channel but with fewer provider integrations.
- **Infrastructure maturity** — Gateway session management, CSP hardening, and SQLite storage refactor (PR #98236) suggest deeper architectural investment.
- **Latest model support** — GPT-5.6 support landed today; Hermes has no equivalent mention.

**Technical approach differences:**
- OpenClaw positions itself as a *core reference implementation* for AI agent infrastructure. Its architecture emphasizes gateway-based session orchestration, external harness attachment, and provider-agnostic runtime selection.
- Hermes Agent focuses more on *end-user desktop experience* with TUI, dashboard, and macOS/Windows desktop clients. Its skill ecosystem (mind memory, unbroker, post-compress hooks) is more end-user oriented.
- OpenClaw’s injection-defence approach is CSP-based (tightened `connect-src` in PR #99024); Hermes addresses it via `/steer` command collision detection and security PR #57475 (hardline bypass prevention).

**Community size comparison:** OpenClaw’s activity levels (~200 issues/day, ~500 PRs/day) suggest a contributor community roughly 4–5× larger than Hermes Agent (~50 issues/day, ~50 PRs/day). This aligns with OpenClaw’s status as the more widely referenced core project in the ecosystem.

---

## 4. Shared Technical Focus Areas

| Requirement | Projects Affected | Specific Evidence |
|-------------|------------------|-------------------|
| **Tool-call leakage prevention** | OpenClaw, Hermes Agent | OL #25592 (text between tool calls leaks to channels, P1, 33 comments); HA #36934 (`/steer` flagged as prompt injection, P1, 8 comments). Both projects need better isolation between agent-internal processing and user-visible output. |
| **Multi-agent state consistency** | OpenClaw, Hermes Agent | OL #98790 (concurrent agent-to-agent turn poisons transcript, P1); OL #75593 (subagents list empty after spawn, P1); HA #24782 (subagent fallback uses parent’s base_url, P2). Both encounter race conditions and cache incoherence in subagent orchestration. |
| **OAuth token reliability** | OpenClaw, Hermes Agent | OL #98702 (inherited OAuth rejected for sub-agents, P1); OL #99120 (OAuth refresh false-green, P1); HA #23944 (generic OAuth broker, P3 backlog). Silent credential expiration is a systemic pain point. |
| **Cross-platform message delivery** | OpenClaw, Hermes Agent | OL #87744 (Telegram turns time out, P1); HA #52914 (QQBot infinite retry loop, P2); HA #53449 (Telegram duplicate replies, P2). Each platform introduces unique delivery behavior that breaks assumptions. |
| **Desktop client quality** | Hermes Agent (primary); OpenClaw (indirect) | HA #38602 (thin-client desktop requested, 37 👍); HA #44456 (desktop `/compress` unrecognized); HA #47368 (delete profile fails silently). Hermes has a desktop-specific quality gap. OpenClaw’s iOS photos permission bug (#99046) and macOS traffic lights fix (#57455 in Hermes) show cross-platform UI issues are universal. |
| **Provider fallback intelligence** | OpenClaw, Hermes Agent | OL #47910 (provider fallback by failure class, P1, 7 comments); HA #56073 (delayed auto-resume for rate limits, closed). Both recognize that current fallback strategies are too simplistic. |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary identity** | Core reference implementation / LLM gateway | Personal desktop AI assistant with skill ecosystem |
| **Target user** | Developers building agent systems, platform operators | End-users, power users, desktop-first consumers |
| **Key architecture** | Gateway-session model, external harness attachment, provider-agnostic runtime | Desktop/TUI client, plugin-based skills, injection-defense framework |
| **LLM support** | Broad (OpenAI, Anthropic, Bedrock, Gemini, Vertex) | Fewer providers explicitly mentioned; focus on high-resistance models (Opus 4.8) |
| **Community contribution model** | Large, decentralized, high issue/PR churn | Smaller but engaged; skill ecosystem encourages community plugins |
| **Stability posture** | Feature velocity > stability; many P1 regressions open | Desktop bugs accumulating but core stability better; lower P1 count |
| **Differentiating feature** | GPT-5.6 support, external harness, SQLite refactor | Thin-client mode (upvoted), mind memory skill, unbroker security skill |
| **Integration focus** | Multi-channel messaging (Telegram, Slack, Signal, Feishu, etc.) | Desktop (macOS, Windows, Linux) and gateway platforms |
| **Injection defense** | CSP-based (connect-src restrictions) | Hardline bypass prevention, `/steer` collision detection |

**Key insight:** OpenClaw is the infrastructure layer; Hermes Agent is the application layer. They are complementary rather than directly competitive. An operator could use OpenClaw as the core gateway and Hermes Agent as a desktop frontend, though this is not a documented integration path.

---

## 6. Community Momentum & Maturity

**Activity tiers:**

| Tier | Project | Characteristics |
|------|---------|----------------|
| **Rapid iteration** (Tier 1) | OpenClaw | 500 PRs/day, 196 issues/day, new beta with major features. However, high P1 count and regression fatigue suggest iteration outpacing stabilization. |
| **Steady growth** (Tier 2) | Hermes Agent | 50 PRs/day, 50 issues/day, no release today. Desktop quality lagging but core fixes landing. Low-risk trajectory; community is happy enough to contribute skills. |

**Maturity assessment:**
- **OpenClaw:** High feature maturity (broad provider support, multi-channel, session gateway), but low operational maturity (frequent regressions, silent failures, OAuth instability). The project is in a “feature-rich but brittle” phase. The SQLite storage refactor (#98236) could unlock better session management and reduce state-loss bugs, but it is still open.
- **Hermes Agent:** Lower feature breadth but higher per-feature polish. The desktop experience is the weakest link, and the priority gap (P3 desktop bugs accumulating) suggests the maintainer team is focusing on core gateway/defence work. The thin-client demand (#38602) signals a shift toward server-client split architecture, which would reduce desktop complexity.

**Backlog concerns:**
- OpenClaw has no explicitly identified long-stale issues in today’s digest, but the volume of open issues (123) combined with P1 regressions that have been open for months (e.g., #25592 since February, #73148 since pre-2026) indicates triage bandwidth is strained.
- Hermes Agent has 9 identified backlog items, including a P2 LiteLLM context size issue (#8465, since April) and a P3 Honcho memory crash (#33485, since May). These are lower severity but could become blockers as user bases grow.

---

## 7. Trend Signals

**Extracted from community feedback, actionable for AI agent developers:**

1. **Tool-call output isolation is a critical UX and security risk.**  
   Both projects see users reporting that agent-internal processing leaks into user-visible channels. Developers building agent frameworks must treat tool-call boundaries as security boundaries with strict output filtering. This is not just a UX issue—it can lead to information disclosure (OL #25592 is labelled as “security/message-loss”).

2. **Multi-agent state corruption is the top architectural challenge.**  
   Race conditions in concurrent subagent execution (OL #98790) and transcript poisoning are not edge cases—they are occurring in production. Any project supporting subagents needs transactional state management and per-turn locking. The ecosystem lacks a reference design for this.

3. **OAuth token management remains brittle across the ecosystem.**  
   Silent credential expiration (OL #99120), inherited OAuth failures (OL #98702), and generic OAuth broker requests (HA #23944) all point to the same gap: there is no standard, robust token refresh mechanism that works across providers. This is a fundamental blocker for enterprise adoption.

4. **Desktop quality is the next frontier, but thin-client architectures are preferred.**  
   Hermes’ most-upvoted request (37 👍) is a thin-client mode that delegates compute to a remote server. This mirrors broader industry trends toward lightweight frontends. Developers should invest in decoupling desktop UI from backend processing rather than trying to make full desktops reliable across platforms.

5. **Provider fallback strategies need to be failure-class-aware.**  
   Both projects recognize that retrying a provider with known bad auth (OL #47910) or blindly switching on rate limits (HA #56073) is wasteful. Future fallback systems should classify failures (auth, rate-limit, model-unsupported, transient) and route accordingly. This is a high-value, low-complexity improvement.

6. **Cross-platform message delivery discrepancies are a persistent source of bugs.**  
   Telegram, QQBot, Signal, and Slack each introduce unique behaviors (timeout loops, duplicate replies, image rendering issues). Developers should build platform-specific adapters as isolated components with clear failure contracts, not assume uniform gateway behavior.

7. **Community values explicit error messages over opaque failures.**  
   OL #73148 (“Failed to optimize image” when sharp is missing) and HA #56704 (`int(None)` crash in computer_use) both demonstrate that users need actionable diagnostics. Investing in error classification and user-facing guidance (rather than generic fallbacks) directly improves satisfaction and reduces support burden.

---

**Bottom line for decision-makers:** OpenClaw offers the broadest platform reach and largest community, but requires careful regression management and monitoring. Hermes Agent is a safer bet for desktop-centric deployments, especially with the upcoming thin-client mode. Both projects would benefit from shared standardization on OAuth token management, tool-call output isolation, and failure-class-based provider fallback—areas where the ecosystem as a whole has not yet converged.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-07-03

## 1. Today’s Overview
Project activity remains high with 50 issues and 50 PRs updated in the last 24 hours. 7 issues were closed and 18 PRs were merged or closed, indicating steady progress on bug fixes and features. However, the volume of open issues (43) and open PRs (32) suggests the maintainer team is working through a significant backlog. No new releases were published today, and the project continues to address stability and usability regressions, particularly around the Desktop experience, gateway platforms, and injection-defence collisions.

## 2. Releases
No new releases were published today.

## 3. Project Progress
**Merged/Closed PRs today (notable):**
- [#57455](https://github.com/NousResearch/hermes-agent/pull/57455) – fix(desktop): stop macOS Tahoe misplacing the traffic lights (closed)
- [#57457](https://github.com/NousResearch/hermes-agent/pull/57457) – fix(desktop): hide Windows updater console during hand-off (closed)
- [#57445](https://github.com/NousResearch/hermes-agent/pull/57445) – fix(dashboard-auth): catch NotImplementedError in auth_login for password-only providers (closed)
- [#56073](https://github.com/NousResearch/hermes-agent/pull/56073) – Add delayed auto-resume for provider rate limits (closed)

**Closed Issues today:**
- [#29171](https://github.com/NousResearch/hermes-agent/issues/29171) – Kanban waiting states feature (closed after community discussion)
- [#53773](https://github.com/NousResearch/hermes-agent/issues/53773) – TUI WebSocket disconnect during long-running delegate_task (P1, closed)
- [#57390](https://github.com/NousResearch/hermes-agent/issues/57390) – STEER_CHANNEL_NOTE false-positive prompt injection loop (duplicate, closed)
- [#21562](https://github.com/NousResearch/hermes-agent/issues/21562) – native image generation reference_images support (closed)

These merges show focused efforts on Desktop polish, gateway resilience, and injection-defence hardening.

## 4. Community Hot Topics
Most active issues by comment count and reactions:

| Issue | Comments | Reactions | Summary |
|-------|----------|-----------|---------|
| [#52914](https://github.com/NousResearch/hermes-agent/issues/52914) | 12 | 4 👍 | QQBot gateway infinite retry loop after update |
| [#36934](https://github.com/NousResearch/hermes-agent/issues/36934) | 8 | 0 | `/steer` flagged as prompt injection by high-resistance models (Opus 4.8) – P1 |
| [#38602](https://github.com/NousResearch/hermes-agent/issues/38602) | 8 | 37 👍 | Feature request: Desktop client-only installation (thin-client mode) |
| [#44456](https://github.com/NousResearch/hermes-agent/issues/44456) | 7 | 1 👍 | Desktop `/compress` not recognized (command dispatch bug) |
| [#53449](https://github.com/NousResearch/hermes-agent/issues/53449) | 4 | 0 | Telegram duplicate replies on short messages |
| [#47368](https://github.com/NousResearch/hermes-agent/issues/47368) | 4 | 0 | Desktop "Delete profile" silently fails |
| [#38270](https://github.com/NousResearch/hermes-agent/issues/38270) | 4 | 1 👍 | Desktop not surfacing live Telegram sessions |

The most upvoted issue (#38602, 37 👍) shows strong demand for a thin-client desktop mode. The P1 injection collision (#36934) and the QQBot loop (#52914) are generating high concern.

Other notable PRs with no comments but active today:
- [#57475](https://github.com/NousResearch/hermes-agent/pull/57475) – security: close hardline bypass via interpreter `-c` payloads
- [#56859](https://github.com/NousResearch/hermes-agent/pull/56859) – feat(optional-skills): add mind – brain-like offline project memory skill
- [#57438](https://github.com/NousResearch/hermes-agent/pull/57438) – feat(skills): add security/unbroker (autonomous data-broker removal)

## 5. Bugs & Stability
**High severity (P1):**
- [#36934](https://github.com/NousResearch/hermes-agent/issues/36934) – `/steer` prompt injection false-positive with Opus 4.8 (open, no fix PR yet)
- [#53773](https://github.com/NousResearch/hermes-agent/issues/53773) – TUI WebSocket disconnect during long delegate_task (closed; fix likely part of closed PR)

**Medium severity (P2):**
- [#52914](https://github.com/NousResearch/hermes-agent/issues/52914) – QQBot infinite retry loop (open)
- [#53449](https://github.com/NousResearch/hermes-agent/issues/53449) – Telegram duplicate replies (open)
- [#56704](https://github.com/NousResearch/hermes-agent/issues/56704) – computer_use capture crash on Linux/WSL (`int(None)`) (open)
- [#47368](https://github.com/NousResearch/hermes-agent/issues/47368) – Desktop "Delete profile" fails silently (open)
- [#52470](https://github.com/NousResearch/hermes-agent/issues/52470) – Dashboard auto-restart silently fails due to env inheritance (open)
- [#44456](https://github.com/NousResearch/hermes-agent/issues/44456) – Desktop `/compress` not recognized (open)
- [#46556](https://github.com/NousResearch/hermes-agent/issues/46556) – Desktop `/compress` duplicate (open)
- [#24782](https://github.com/NousResearch/hermes-agent/issues/24782) – Subagent fallback model uses parent's base_url (open)
- [#25106](https://github.com/NousResearch/hermes-agent/issues/25106) – CLI `--global` model switch doesn't persist all fields (open)

**New today (2026-07-03):**
- [#57444](https://github.com/NousResearch/hermes-agent/issues/57444) – Desktop: `/background` completed tasks never show result panel (P3, open)
- [#57405](https://github.com/NousResearch/hermes-agent/issues/57405) – Model selector crashes on macOS: 'dict' object has no attribute 'lower' (P3, open)
- [#57381](https://github.com/NousResearch/hermes-agent/issues/57381) – `hermes-setup` fails on Python 3.14 (distutils removed) (P3, open)
- [#56704](https://github.com/NousResearch/hermes-agent/issues/56704) – computer_use crash (P2, open)
- [#53049](https://github.com/NousResearch/hermes-agent/issues/53049) – Desktop left menu keeps refreshing, high CPU (P3, open)

Several of these bugs have associated fix PRs in the open PR list (e.g., #57471 fixes profile persistence, #57470 fixes PYTHONPATH leak, #57456 fixes launchd user ids), indicating active remediation.

## 6. Feature Requests & Roadmap Signals
Strongly requested improvements:
- **Thin-client Desktop** ([#38602](https://github.com/NousResearch/hermes-agent/issues/38602), 37 👍) – likely to be prioritized for next minor release.
- **Kanban waiting states** ([#29171](https://github.com/NousResearch/hermes-agent/issues/29171), closed) – suggestion to differentiate `blocked` states; may be picked up for future plugin improvements.
- **Vertex / Service Account GUI support** ([#56687](https://github.com/NousResearch/hermes-agent/issues/56687)) – enterprise authentication configuration in Desktop/Web UI.
- **Pricing overrides and contract pricing** ([#9403](https://github.com/NousResearch/hermes-agent/issues/9403)) – phase 4 of pricing architecture, still open.
- **Secrets management Phase 4** ([#3630](https://github.com/NousResearch/hermes-agent/issues/3630)) – advanced security features (ephemeral, external vaults, audit).

New feature PRs today:
- [#57438](https://github.com/NousResearch/hermes-agent/pull/57438) – security/unbroker skill (data-broker removal)
- [#56859](https://github.com/NousResearch/hermes-agent/pull/56859) – mind offline memory skill
- [#57461](https://github.com/NousResearch/hermes-agent/pull/57461) – post_compress hook for ContextEngine
- [#57225](https://github.com/NousResearch/hermes-agent/pull/57225) – warn pip/Homebrew installs are unsupported

These suggest the project is expanding its optional-skill ecosystem and providing extension points for memory and context management. The deprecation of pip/Homebrew installs points to a consolidation of official installation channels.

## 7. User Feedback Summary
- **Pain points:** Desktop command routing bugs (`/compress`, model selector crash, profile deletion) are causing frustration. The Telegram duplicate message issue (even without long messages) and the injection false-positive with high-resistance models are impacting trust and usability.
- **Use cases:** Users want a lightweight desktop client that connects to a remote Hermes agent (thin-client). They also express need for better Kanban workflow support (waiting states) and enterprise-grade OAuth handling (Vertex provider, generic OAuth broker).
- **Satisfaction:** The community is actively contributing skills and bug fixes, indicating strong engagement. However, the high number of open bugs in Desktop suggests rapid feature development has outpaced quality assurance in that area.

## 8. Backlog Watch
Issues/PRs that have been open for a long time with no recent maintainer response or low activity:

| Issue/PR | Created | Last Updated | Priority | Status |
|----------|---------|--------------|----------|--------|
| [#3630](https://github.com/NousResearch/hermes-agent/issues/3630) – Phase 4 secrets security | 2026-03-28 | 2026-07-02 | P3 | Open |
| [#8465](https://github.com/NousResearch/hermes-agent/issues/8465) – Proper LiteLLM context size detection | 2026-04-12 | 2026-07-03 | P2 | Open (5 👍) |
| [#9403](https://github.com/NousResearch/hermes-agent/issues/9403) – Pricing overrides and sync CLI | 2026-04-14 | 2026-07-02 | P3 | Open |
| [#23944](https://github.com/NousResearch/hermes-agent/issues/23944) – Generic OAuth broker credential source | 2026-05-11 | 2026-07-02 | P3 | Open (2 👍) |
| [#24782](https://github.com/NousResearch/hermes-agent/issues/24782) – Subagent fallback base_url bug | 2026-05-13 | 2026-07-02 | P2 | Open |
| [#25106](https://github.com/NousResearch/hermes-agent/issues/25106) – CLI model switch persistence | 2026-05-13 | 2026-07-02 | P2 | Open |
| [#33485](https://github.com/NousResearch/hermes-agent/issues/33485) – Honcho memory shutdown abort (SIGABRT) | 2026-05-27 | 2026-07-02 | P3 | Open |

The LiteLLM context size issue (#8465, 5 👍) has been open since April and is a known pain point for users of custom providers. The subagent fallback bug (#24782) and CLI model persistence (#25106) are both P2 and may need maintainer triage. The Honcho memory SIGABRT (#33485) is a stability issue that could be critical for users relying on hybrid memory mode.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*