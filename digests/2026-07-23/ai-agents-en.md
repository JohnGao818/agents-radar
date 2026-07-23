# OpenClaw Ecosystem Digest 2026-07-23

> Issues: 451 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-23 02:23 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-23

## Today’s Overview

OpenClaw saw extremely high activity in the past 24 hours, with **451 issues** and **500 pull requests** updated. Of those, 152 issues and 204 PRs were closed or merged, indicating a strong focus on bug-fixing and maintenance. However, 299 open issues and 296 open PRs signal a substantial backlog. No new releases were published today. The project continues to address a wide range of regressions, performance bottlenecks, and feature gaps, with maintainers actively reviewing community contributions.

## Releases

*None today.*

## Project Progress

The community merged or closed **204 pull requests** in the last 24 hours. Notable merges from the top-traction PRs include:

- [#112845](https://github.com/openclaw/openclaw/pull/112845) — fix(release): restore saved validation attempt guidance (closed).
- [#112723](https://github.com/openclaw/openclaw/pull/112723) — fix(ios): show full multiline Markdown list items (closed).
- [#112794](https://github.com/openclaw/openclaw/pull/112794) — fix(telegram): keep message mutations in forum topics (closed).
- [#112836](https://github.com/openclaw/openclaw/pull/112836) — fix(ui): keep user footer controls in reading order (closed).

A large batch of fixes touched agents, scripts, gateway stability, and channel plugins (Telegram, Matrix, Signal, Discord). Several open PRs with `ready for maintainer look` status (e.g., [#110562](https://github.com/openclaw/openclaw/pull/110562), [#109460](https://github.com/openclaw/openclaw/pull/109460), [#109515](https://github.com/openclaw/openclaw/pull/109515)) signal that additional improvements are queued for review.

## Community Hot Topics

The most active issue by far remains **[#75: Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)** with **115 comments** and **80 👍**. This long-standing enhancement request (filed January 2026) continues to draw strong community interest. Users are eager for desktop clients beyond macOS/iOS/Android; the issue is tagged `clawsweeper:needs-product-decision`.

Other highly commented issues:

- [#85333](https://github.com/openclaw/openclaw/issues/85333) (17 comments) — `openclaw doctor --fix` 4–5× slower after a recent update; a performance regression under active discussion.
- [#13583](https://github.com/openclaw/openclaw/issues/13583) (16 comments) — Request for pre‑response enforcement hooks (hard gates) to enforce mandatory tool calls in high-stakes workflows.
- [#91009](https://github.com/openclaw/openclaw/issues/91009) (15 comments) — CPU‑bound `openclaw-hooks` processes spawned by Codex PreToolUse causing gateway RPC stalls.
- [#10659](https://github.com/openclaw/openclaw/issues/10659) (15 comments) — Feature request for masked secrets to prevent agents from reading raw API keys.

The underlying needs reflect a maturing platform: users want **cross-platform desktop support**, **stronger security guarantees**, **better performance predictability**, and **enforceable policy controls** for production deployments.

## Bugs & Stability

Many high-severity bugs were reported or updated today. Below is a representative selection by severity:

| Issue | Severity | Summary | Fix PR? |
|-------|----------|---------|---------|
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | P0 (blocker) | Gateway fails to start after update to 2026.7.1 — regression | None linked |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | P1 | Codex hooks spawn CPU‑bound processes, stalling gateway RPC | [#101777](https://github.com/openclaw/openclaw/pull/101777) (open) may address similar |
| [#85333](https://github.com/openclaw/openclaw/issues/85333) | P1 | `doctor --fix` performance regression (55s → 229s) | None linked |
| [#92043](https://github.com/openclaw/openclaw/issues/92043) | P1 | Compaction timeout (180s) fails identically every turn for long histories | None linked |
| [#108580](https://github.com/openclaw/openclaw/issues/108580) | P1 | Cron tool schema incompatible with llama.cpp grammar‑constrained calling | None linked |
| [#39807](https://github.com/openclaw/openclaw/issues/39807) | P1 | Billing error (402) causes infinite retry death spiral with no backoff | None linked |
| [#90840](https://github.com/openclaw/openclaw/issues/90840) | P1 | Subagent run completion delivered as raw output instead of parent summary | None linked |
| [#99054](https://github.com/openclaw/openclaw/issues/99054) | P1 | Teams app removal/re-add retains prior session history (data bleed) | None linked |
| [#99773](https://github.com/openclaw/openclaw/issues/99773) | P2 | Hot reload drops `include`‑defined models from registry, causing “Unknown model” errors | None linked |
| [#65538](https://github.com/openclaw/openclaw/issues/65538) | P1 | Screen reader announces every token during streaming (accessibility) | None linked |

Several other P1 regressions (Windows gateway stalls, Moonshot slow model resolution, Discord stalls) were closed as stale or fixed in earlier releases. The high number of P1 issues without linked fix PRs suggests that maintainers are still triaging root causes.

## Feature Requests & Roadmap Signals

The most popular feature request is **[#75: Linux/Windows apps](https://github.com/openclaw/openclaw/issues/75)** (80 👍, 115 comments). Given its sustained attention, it is a strong candidate for the next major release.

Other notable requests:

- [#13583](https://github.com/openclaw/openclaw/issues/13583) — **Pre-response enforcement hooks** (hard gates for mandatory tool-call rules). Essential for compliance in finance/security workflows.
- [#10659](https://github.com/openclaw/openclaw/issues/10659) — **Masked secrets** to prevent agents from leaking API keys. Aligns with growing security awareness.
- [#38568](https://github.com/openclaw/openclaw/issues/38568) — Inject **context window percentage** into system prompt runtime section.
- [#9912](https://github.com/openclaw/openclaw/issues/9912) — `maxTurns`/`maxToolCalls` config to limit agent loops.
- [#10142](https://github.com/openclaw/openclaw/issues/10142) — `session:end` internal hook event for workflow orchestration.

On the PR side, several large features are in review:

- [#88504](https://github.com/openclaw/openclaw/pull/88504) — Multi‑slot memory role architecture (feature showcase).
- [#112773](https://github.com/openclaw/openclaw/pull/112773) — Portable agent policy settings (also allow, deny, workspace-only filesystem).
- [#104018](https://github.com/openclaw/openclaw/pull/104018) — Readiness conditions and providers for gateway health checks.
- [#111544](https://github.com/openclaw/openclaw/pull/111544) — Localize TUI status summary (i18n).
- [#112000](https://github.com/openclaw/openclaw/pull/112000) — Refactor prompt to use plain inbound context labels (security improvement).

These indicate the project is moving toward **multi-tenancy, policy enforcement, localization, and deeper extensibility**.

## User Feedback Summary

User sentiment is mixed: while the community actively contributes fixes and requests, the sheer volume of regressions (especially in performance and channel reliability) causes frustration. Frequent complaints include:

- **Performance regressions** (`doctor --fix` 4× slower, Codex hooks consuming 100% CPU, compaction timeouts).
- **Channel instability** (Telegram forum bugs, WhatsApp auto-reply failure, LINE intermittent silence, Matrix startup hangs).
- **Security gaps** (unmasked secrets, prompt injection vectors, leftover session data after Teams removal).
- **Missing platform parity** (Linux/Windows apps, desktop clients).
- **Configuration friction** (hot reload losing models, `tools.deny` not respected for Codex, validation errors preventing fixes from persisting).

On the positive side, users who participate in feature discussions (especially #75, #10659, #13583) show high engagement and appreciation for the project’s direction. The open‑source community is vibrant, with many first‑time contributors submitting small fixes.

## Backlog Watch

Several high‑importance issues and PRs have been waiting for maintainer attention for weeks or months. Key items:

| Item | Age | Notes |
|------|-----|-------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | 7 months | Linux/Windows apps – needs product decision. Overdue. |
| [#85333](https://github.com/openclaw/openclaw/issues/85333) | 2 months | doctor --fix performance regression – needs maintainer review and live repro. |
| [#13583](https://github.com/openclaw/openclaw/issues/13583) | 5 months | Hard enforcement hooks – needs product decision and security review. |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | 5 months | Masked secrets – needs product decision and security review. |
| [#39807](https://github.com/openclaw/openclaw/issues/39807) | 4 months | Billing error infinite retry – linked PR open but no maintainer signoff. |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | 1 month | Codex CPU‑bound hooks – needs maintainer review and live repro. |
| [#88504](https://github.com/openclaw/openclaw/pull/88504) | 2 months | Large memory feature PR – status “needs proof” for weeks. |
| [#112000](https://github.com/openclaw/openclaw/pull/112000) | 2 days | Prompt refactor – waiting on author but high merge risk; needs prompt attention. |

The project’s health is strong in terms of community participation but strained by the volume of unresolved regressions and backlogged feature reviews. A focused sprint on closing the oldest P1 issues and merging long‑pending PRs would significantly improve perceived responsiveness.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Open-Source Personal AI Assistant Ecosystem

**Date:** 2026-07-23  
**Projects Analyzed:** OpenClaw (core reference), Hermes Agent (Nous Research)

---

## 1. Ecosystem Overview

The personal AI assistant and agent open-source landscape is maturing rapidly, with two dominant reference implementations demonstrating contrasting strategies. Both projects are experiencing high community engagement, but the ecosystem is bifurcating: OpenClaw acts as a broad platform with extensive plugin support and channel diversity, while Hermes Agent focuses on multi-agent orchestration and memory management. Common pain points include cross-platform desktop support, security hardening, and session state consistency across channels. The community is increasingly vocal about production-grade requirements such as policy enforcement, performance predictability, and secrets protection, indicating a shift from experimental to enterprise-ready usage.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | Issues Closed (24h) | PRs Updated (24h) | PRs Merged/Closed (24h) | Release Today | Health Score* |
|---------|----------------------|---------------------|-------------------|-------------------------|---------------|---------------|
| **OpenClaw** | 451 | 152 | 500 | 204 | None | **5/10** |
| **Hermes Agent** | 50 | 4 (est.) | 50 | 11 | None | **7/10** |

*Health Score based on ratio of closed-to-open items, severity of open regressions, and maintainer responsiveness. OpenClaw suffers from a large backlog (299 open issues, 296 open PRs) and multiple unaddressed P1 regressions. Hermes Agent, despite fewer absolute numbers, demonstrates faster closure cycles and immediate fix PRs for reported bugs.

---

## 3. OpenClaw's Position

- **Advantages:** Largest community (451 issues, 500 PRs daily), broadest channel support (Telegram, Matrix, Signal, Discord, WhatsApp, Teams), and most mature plugin/agent architecture. Strong feature-request momentum (e.g., Linux/Windows apps with 80 👍).
- **Technical Approach:** Monolithic core with layered plugin system, emphasis on channel independence and gateway stability. Uses hooks (Codex, PreToolUse) for extensibility – but these introduce performance and security risks.
- **Community Size vs. Peers:** OpenClaw's daily activity is roughly **9×** that of Hermes Agent, indicating a larger contributor base. However, this scale also creates triage bottlenecks and delayed product decisions on high-profile issues (e.g., #75 Linux/Windows apps waiting 7 months).
- **Key Weakness:** Maintainer bandwidth insufficient to close the gap between bug reports and fixes. Several P1 regressions (e.g., `doctor --fix` 4× slower, gateway startup regression #108435) lack linked fix PRs.

---

## 4. Shared Technical Focus Areas

Both projects reveal overlapping community demands, signaling cross-cutting requirements for the ecosystem:

| Requirement | OpenClaw | Hermes Agent | Common Pain Points |
|-------------|----------|--------------|-------------------|
| **Cross-platform desktop support** | #75 (80 👍, 7 months old) | #4335 (session sharing across platforms) | Linux/Windows clients, unified session state |
| **Secrets/masked keys protection** | #10659 (15 comments, 5 months old) | #12651 (`.env` sanitizer) | Prevent agents from leaking API keys |
| **Performance & scalability** | #85333 (`doctor --fix` 4× slower), #91009 (CPU-bound hooks) | #62708 (silent context overflow), #69745 (memory wipe) | Predictable latency, stable memory usage |
| **Channel reliability** | Telegram forum bugs, LINE silence | Telegram >15 MB upload timeout, Desktop reconnect loops | Reliable file delivery, consistent message delivery |
| **Policy & enforcement hooks** | #13583 (pre-response hard gates) | Implicit (delegation model) | Compliance for production workflows |
| **Session state continuity** | Not explicitly requested | #4335 cross-platform sharing | Seamless transitions between CLI, desktop, and chat |

Both projects are actively experiencing regressions in session management, media handling, and performance, indicating a shared need for **robust testing infrastructure** and **regression detection**.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary focus** | Multi-channel gateway + plugin ecosystem | Multi-agent orchestration + memory management |
| **Target users** | Power users, self-hosters, enterprise deployments with diverse chat platforms | Developers building autonomous workflows, agent teams, desktop-first users |
| **Technical architecture** | Large monorepo with many plugins, hooks for extensibility; risk of configuration friction (hot reload drops models) | Modular codebase with clear subsystem boundaries (memory, delegation, skills); fast iteration on specific features |
| **Feature velocity** | High – but diffused across many channels; decision latency on long-standing issues | Lower absolute volume, but **faster time-to-fix** (many same-day PRs for filed bugs) |
| **Community engagement** | Extremely high but noisy; many duplicate or stale issues | Smaller but more focused; detailed bug reports with reproduction steps |
| **Key innovation risk** | Hooks (Codex) causing CPU-bound stalls, gateway RPC failures | Memory file wipe (P0 data loss) due to read failure handling |
| **Release cadence** | Irregular, no release today despite high activity | No release today, but patch expected soon given PR maturity |

The two projects serve complementary roles: OpenClaw as the **stability-and-scope** platform for multi-channel deployments; Hermes Agent as the **agility-and-orchestration** framework for advanced agent workflows.

---

## 6. Community Momentum & Maturity

| Tier | Project | Indicators |
|------|---------|------------|
| **Rapidly iterating (high velocity, high responsiveness)** | Hermes Agent | 50 PRs/day, 11 merged in 24h, many same-day fix PRs; 7/10 health score despite P0 data loss bug (fix PR exists) |
| **High activity with triage friction** | OpenClaw | 500 PRs/day, 204 merged, but 299 open issues and 296 open PRs; 5/10 health score due to unresolved P1 regressions and 7-month-old feature requests without decisions |
| **Stabilizing** | Neither project | Both are still in active growth phase, but OpenClaw shows signs of needing a stabilization sprint (e.g., focusing on the oldest P1 bugs and merging long-pending PRs) |

OpenClaw's sheer volume masks a growing maintenance debt. Hermes Agent, though smaller, demonstrates better cycle time from bug report to fix.

---

## 7. Trend Signals

The following industry-wide trends emerge from community feedback across both projects:

1. **Cross-platform desktop clients are no longer a nice-to-have.** With 80+ reactions on OpenClaw #75 and persistent requests on Hermes Agent for session sharing, desktop (Linux/Windows) parity is the #1 unmet expectation for AI assistant tools.

2. **Security becomes a first-class requirement.** Masked secrets (#10659), prompt injection protection, and data bleed prevention (Teams session retention) are being demanded by early production users. Expect integration with secret stores (Vault, 1Password) within 6 months.

3. **Policy enforcement is the next frontier.** Hard gates for tool calls, mandatory compliance hooks, and workspace-only filesystem policies (PR #112773) indicate that enterprise governance is now driving feature requests, not just personal productivity.

4. **Performance regression detection is critical.** Both projects have P1 regressions that degrade user experience by 4–10× (OpenClaw `doctor --fix`, Hermes Agent context overflow). Automated benchmarking and regression alerts must be built into CI.

5. **Modular memory architectures are converging.** OpenClaw’s multi-slot memory PR (#88504) and Hermes Agent’s `filter_by_agent_id` (#69744) suggest a shift toward profile-scoped, agent-isolated memory – essential for multi-tenant and team deployments.

6. **Channel reliability remains a weak link.** Telegram upload timeouts, Discord stalls, and WhatsApp silent failures are recurring themes. The ecosystem needs standardized channel testing suites and adaptive retry protocols.

---

**Bottom line for technical decision-makers:**  
- Choose **OpenClaw** if you need broad channel coverage, plugin extensibility, and a large community to draw from – but be prepared for slower resolution of regressions and feature decisions.  
- Choose **Hermes Agent** if you prioritize rapid iteration, advanced multi-agent workflows, and responsive maintainers – but expect a smaller channel plugin set and occasional data-integrity risks.  
- Both projects urgently need investment in **regression testing**, **performance benchmarking**, and **security hardening** to meet production demands.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-07-23

## 1. Today's Overview
Hermes Agent is experiencing an **extremely active day**, with 50 issues and 50 pull requests updated in the last 24 hours. The majority of issues remain open (46 of 50), indicating sustained community engagement and rapid triage. The project saw 11 PRs merged or closed, reflecting ongoing progress across desktop, CLI, gateway, and memory subsystems. No new releases were published, but the volume of activity suggests a release may be imminent as many fixes and features reach maturity. Key areas of focus are **session state management**, **gateway/platform integration**, and **Windows compatibility**.

## 2. Releases
No new releases were published on this day. The latest release remains v0.19.0 (2026.7.20). Given the high PR activity and several critical bug fixes in flight, a patch or minor release is expected soon.

## 3. Project Progress
**Merged/closed PRs (11 total)** – Notable examples include:

- [#69694 – `feat(delegation): allow per-task model selection in delegate_task`](https://github.com/NousResearch/hermes-agent/pull/69694) – Closed feature: enables different models for subagents in batch delegation.
- [#69699 – `fix(ci): publish inline E2E evidence`](https://github.com/NousResearch/hermes-agent/pull/69699) – Closed CI fix: improves pipeline reliability.
- [#69683 – `fmt(js): npm run fix auto-fix`](https://github.com/NousResearch/hermes-agent/pull/69683) – Closed: automated formatting fix merged.
- [#64090 – `fix(codex): extend native Responses web_search to openai-codex`](https://github.com/NousResearch/hermes-agent/pull/64090) – Closed: extends web search support for OpenAI Codex backend.
- [#68302 & #68979 – Desktop session bugs closed](https://github.com/NousResearch/hermes-agent/issues/68302) – Two desktop UI bugs fixed: sidebar session clicks when Skills & Tools view is active, and long-thread re-stacking after compression.

**Notable open work** advancing today:
- [#69744 – `feat(mem0): add filter_by_agent_id option`](https://github.com/NousResearch/hermes-agent/pull/69744) – New option for memory isolation across profiles.
- [#69749 – `feat(skills): hermes-loop kanban software factory`](https://github.com/NousResearch/hermes-agent/pull/69749) – Bundled skill for multi-hour build trains.
- [#69752 – `fix(codex): extend native Responses web_search to openai-codex`](https://github.com/NousResearch/hermes-agent/pull/69752) – Companion to #64090, now on `main`.

## 4. Community Hot Topics
The most discussed issues this week (by comment count and reactions):

- [#4335 – **Feature Request: Cross-platform session context sharing (CLI ↔ Telegram)**](https://github.com/NousResearch/hermes-agent/issues/4335) – 9 comments, 2 👍  
  *Need:* Users want seamless conversation continuity across CLI, Telegram, Discord, etc. Currently each platform maintains isolated session stores, causing disjointed experiences.

- [#66875 – **[Bug]: Latest session does not switch after navigating to Plugins/Artifacts tab and back**](https://github.com/NousResearch/hermes-agent/issues/66875) – 7 comments  
  *Need:* Desktop dashboard session navigation is broken when non-chat tabs are visited, causing workflow friction.

- [#62936 – **[Bug]: Telegram uploads >~15 MB always fail with TimedOut**](https://github.com/NousResearch/hermes-agent/issues/62936) – 6 comments  
  *Need:* Environmental timeout variables don't affect Python Telegram Bot's media upload timeout, blocking large file delivery.

- [#21341 – **[Bug]: nixosModule `documents` option installs files to wrong paths**](https://github.com/NousResearch/hermes-agent/issues/21341) – 5 comments  
  *Need:* Nix module configuration misaligns file paths, preventing correct loading of personality/memory files.

The high engagement on cross-platform session sharing and Telegram file delivery reflects the community's desire for a **unified multi-channel experience** and **reliable media handling**.

## 5. Bugs & Stability
**Critical (P0):**
- [#69745 – `fix(memory): don't wipe MEMORY.md when a read-modify-write reads it as unreadable`](https://github.com/NousResearch/hermes-agent/pull/69745) – **Data loss bug:** any read failure on memory file was degraded to empty, causing silent total data loss on `add`. A fix PR exists and is open.

**High (P1):**
- [#62708 – **Silent context-overflow: no warning when compression is blocked**](https://github.com/NousResearch/hermes-agent/issues/62708) – Context keeps growing silently until hard provider limit, leaving users confused.

**Medium (P2):**
- [#69738 – **`/reload` deletes container-supplied env config**](https://github.com/NousResearch/hermes-agent/issues/69738) – Reloading environment removes container environment variables (Docker `-e` / env_file), breaking containerized deployments.
- [#69737 – **`checkpoints.enabled` is ignored in one-shot sessions**](https://github.com/NousResearch/hermes-agent/issues/69737) – One-shot (`hermes -z`) doesn't respect checkpoint configuration.
- [#69709 – **`supports_vision` override not resolved for CLI `--provider` with named custom_providers**](https://github.com/NousResearch/hermes-agent/issues/69709) – Vision capability lookup broken for custom providers.
- [#69638 – **Desktop: queued large image reconnect-loops and persists tens of MB in localStorage**](https://github.com/NousResearch/hermes-agent/issues/69638) – WebSocket message limits cause repeated reconnects and storage bloat.

**Low (P3):**
- [#69660 – **Queued messages appear in thread history with timer instead of queue drawer**](https://github.com/NousResearch/hermes-agent/issues/69660) – UI regression from recent PR.

Several P2 bugs have **accompanying fix PRs** (e.g. #69751, #69747, #69652), indicating rapid response from the maintainer team.

## 6. Feature Requests & Roadmap Signals
Top feature requests filed today:

- [#69726 – `feat(whatsapp): support channel_skill_bindings for auto-loading group skills`](https://github.com/NousResearch/hermes-agent/issues/69726) – Extending platform-specific config to WhatsApp. Likely to land in next minor release given existing Discord/Slack support.
- [#69744 – `feat(mem0): add filter_by_agent_id option`](https://github.com/NousResearch/hermes-agent/pull/69744) – Memory isolation per profile; PR is already open.
- [#69749 – `feat(skills): hermes-loop kanban software factory`](https://github.com/NousResearch/hermes-agent/pull/69749) – New bundled skill; shows interest in long-running autonomous workflows.

**Roadmap indicators:**
- Cross-platform session sharing (#4335) is a long-standing request with high engagement; could be a major upcoming feature.
- Subagent lifecycle API (PR #63359) and delegation model selection (#69694) point toward **advanced multi-agent orchestration**.
- i18n expansion (PR #38846) and profile-scoped deep links (PR #67392) signal continued polish of the desktop UI.

## 7. User Feedback Summary
Users express **frustration with session state fragmentation** across platforms and **file upload reliability** on Telegram. The desktop UI has several regressions around session switching and queued messages, reflecting recent code churn. Windows users face extra pain with atomic file writes (`ERROR_SHARING_VIOLATION`) and shell init resolution.

On the positive side, the community is **highly engaged**, filing detailed bug reports with reproduction steps and environment context. The presence of multiple “sweeper” bot labels (e.g., `sweeper:risk-session-state`) indicates automated risk assessment is active. Users appreciate the **rapid iteration** – many bugs have fix PRs opened the same day they were reported.

## 8. Backlog Watch
Older, important issues that have not seen recent maintainer activity:

- [#21341 – `[Bug]: nixosModule documents option installs files to wrong paths`](https://github.com/NousResearch/hermes-agent/issues/21341) – Filed 2026-05-07, last updated 2026-07-22 (comment from user only). Nix users await a fix.
- [#12651 – `.env sanitizer does not remove documented KEY=*** placeholders`](https://github.com/NousResearch/hermes-agent/issues/12651) – Filed 2026-04-19, last updated 2026-07-22 (bot label). Security-adjacent credential confusion.
- [#18539 – `[Bug]: /queue FIFO chain drops MEDIA files`](https://github.com/NousResearch/hermes-agent/issues/18539) – Filed 2026-05-01, last updated 2026-07-22. Only last item gets media delivery.
- [#25837 – `[Bug]: vision_analyze / browser_vision can brick session by inlining oversized image`](https://github.com/NousResearch/hermes-agent/issues/25837) – Filed 2026-05-14, critical for Anthropic users. No fix PR in sight.
- [#21521 – `[BUG] unhandled auth_type oauth_minimax warning`](https://github.com/NousResearch/hermes-agent/issues/21521) – Filed 2026-05-07, minor but generates log noise for MiniMax users.

These issues may require **maintainer attention** to assign priority or solicit contributions, as they affect important user groups (Nix, Anthropic, Windows) and have remained open for months.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*