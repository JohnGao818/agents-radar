# OpenClaw Ecosystem Digest 2026-07-09

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-09 02:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-07-09

## Today's Overview

OpenClaw shows extremely high activity with 500 issues and 500 pull requests updated in the last 24 hours – an unusually busy day. Of those, 457 issues remain open/active and 43 were closed; 407 PRs are open and 93 were merged/closed. The project is dealing with multiple critical stability, security, and performance regressions, particularly around session management, messaging leaks, and provider fallback. No new releases were produced today. While the community is highly engaged (many high-comment-count issues), the overall health is strained by unresolved P0/P1 blockers and a growing backlog of maintainer-review-needed items.

## Releases

None today. The latest stable release remains 2026.3.x (referenced in older issues); future releases likely to address the mounting stack of P1 bugs.

## Project Progress (Merged/Closed PRs Today)

93 PRs were merged or closed. Notable closed items from the top-30-by-comment list include:

- **#102359** – `fix(openai): stringify replayed tool call arguments` (closed). Fixes Ollama cloud models rejecting embedded-agent follow-ups when replayed `tool_calls[].function.arguments` is an object instead of a string.
- **#98299** – `feat: add hosted feed envelope verifier` (closed). Adds signed envelope verifier for upcoming feed refresh and source-profile PRs.
- **#101296** – `fix(whatsapp): suppress unhandled rejections from void fire-and-forget calls` (closed). Prevents gateway crashes when async calls fail.
- **#101668** – `fix(cron): keep system event queued when main-session heartbeat is disabled` (closed). Ensures system events are not silently dropped when heartbeat is disabled.

These merges primarily address provider compatibility, security primitives, channel reliability (WhatsApp, cron), and error handling. No major new features landed today.

## Community Hot Topics

### Most Discussed Issues (by comments)

1. **#25592** – *Text between tool calls leaks to messaging channels* (35 comments, 1 👍)  
   [Issue link](https://github.com/openclaw/openclaw/issues/25592)  
   **Underlying need:** End users are seeing internal LLM processing output (e.g., error handling, narration) as visible messages on Slack, iMessage, etc., causing severe UX confusion. Community wants a mechanism to suppress or divert non-user-facing text.

2. **#44925** – *Subagent completion silently lost — no retry, no notification, no auto-restart on timeout* (21 comments, 1 👍)  
   [Issue link](https://github.com/openclaw/openclaw/issues/44925)  
   **Underlying need:** Subagent tasks fail in multiple silent ways (completion announce fails, timeouts) without any recovery or notification. Orchestration is unreliable for production use.

3. **#48003** – *Steer mode does not inject messages mid-turn for main sessions* (15 comments, 3 👍)  
   [Issue link](https://github.com/openclaw/openclaw/issues/48003)  
   **Underlying need:** The `steer` mode was supposed to allow mid-turn user intervention but queuing delays injection until turn ends, breaking interactive workflows.

4. **#85333** – *openclaw doctor --fix 4-5x slower on 2026.5.20 (55s → 229s+)* (15 comments, 1 👍)  
   [Issue link](https://github.com/openclaw/openclaw/issues/85333)  
   **Underlying need:** Performance regression severely impacts operational tooling. Root cause identified as session snapshot path traversal bottleneck. Community wants an immediate fix or revert.

5. **#45740** – *gh-issues skill: untrusted issue body injected directly into sub-agent prompt* (14 comments, 1 👍)  
   [Issue link](https://github.com/openclaw/openclaw/issues/45740)  
   **Underlying need:** Security concern: raw GitHub issue content is injected without sanitization, enabling prompt injection attacks.

### Most Upvoted Feature Request

- **#39604** – *Add tools.web.fetch.allowPrivateNetwork* (11 👍, 13 comments)  
   [Issue link](https://github.com/openclaw/openclaw/issues/39604)  
   **Underlying need:** Operators need opt-in access to internal network resources via `web_fetch` (currently blocked), especially for self-hosted tools and local services.

## Bugs & Stability

### P0 (Release Blockers)

- **#43661** – *Session hangs indefinitely when compaction times out, causing repeated duplicate message sends*  
   [Issue link](https://github.com/openclaw/openclaw/issues/43661)  
   Maturity: stable. No fix PR linked; still needs maintainer review.

### P1 (Critical)

- **#25592** – Text between tool calls leaks to channels. [Issue link](https://github.com/openclaw/openclaw/issues/25592)  
   Linked PR? No new fix PR seen. Needs product decision and security review.

- **#44925** – Subagent completion silently lost. [Issue link](https://github.com/openclaw/openclaw/issues/44925)  
   Linked PR open (clawsweeper:linked-pr-open), but not identified in today’s merged list.

- **#48003** – Steer mode broken. [Issue link](https://github.com/openclaw/openclaw/issues/48003)  
   Linked PR open.

- **#85333** – `doctor --fix` performance regression. [Issue link](https://github.com/openclaw/openclaw/issues/85333)  
   No fix PR linked; needs live repro.

- **#94228** – Native Anthropic path: `Invalid signature in thinking block` 400 on long tool-use threads. [Issue link](https://github.com/openclaw/openclaw/issues/94228)  
   Linked PR open? (clawsweeper:linked-pr-open). Appears to be a critical provider compatibility issue.

- **#41165** – Telegram DMs can still land in agent:main:main after fix. [Issue link](https://github.com/openclaw/openclaw/issues/41165)  
   Linked PR open. Regression of session isolation.

- **#38327** – “Cannot convert undefined or null to object” on google-vertex/gemini. [Issue link](https://github.com/openclaw/openclaw/issues/38327)  
   Stale since March 6. No new activity.

- **#45494** – Cron jobs silently time out on sustained LLM HTTP 500 instead of fast-failing. [Issue link](https://github.com/openclaw/openclaw/issues/45494)  
   Needs live repro.

- **#43996** – Sandbox container exits immediately with `exec /usr/bin/sleep: operation not permitted`. [Issue link](https://github.com/openclaw/openclaw/issues/43996)  
   Security/crash-loop impact. Linked PR #44098 (stale, XS fix for pidsLimit) but not merged.

### Notable Security Issues

- **#45740** – gh-issues skill prompt injection (P2, diamond lobster). [Issue link](https://github.com/openclaw/openclaw/issues/45740)
- **#44905** – Discord leaks internal tool-call traces (P1, platinum hermit). [Issue link](https://github.com/openclaw/openclaw/issues/44905)
- **#39604** – Private network access feature request (P2, diamond lobster). [Issue link](https://github.com/openclaw/openclaw/issues/39604)

### Regressions

- **#43747** – Memory management is in chaos (P2, diamond lobster). [Issue link](https://github.com/openclaw/openclaw/issues/43747)
- **#38439** – Webchat avatar endpoint 404 (P2, platinum hermit). [Issue link](https://github.com/openclaw/openclaw/issues/38439)
- **#45594** – Cron silent timeout regression (P1, platinum hermit). [Issue link](https://github.com/openclaw/openclaw/issues/45494)

## Feature Requests & Roadmap Signals

### Likely Candidates for Next Release

- **Per-agent cost budgets (#42475)** – high demand (12 comments, 1 👍) – operator necessity for cost control.
- **Pre-reset agentic memory flush (#45608)** – 11 comments, 4 👍 – prevents loss of ongoing reasoning before session reset.
- **MathJax/LaTeX support in Control UI (#42840)** – 8 comments, 9 👍 – strong user desire for scientific communication.
- **Backup CLI exclude patterns (#40786)** – 7 comments – improves backup usability and security.
- **Gateway lifecycle hooks (#43454)** – 7 comments – extensibility for workspace automation.
- **Reasoning stream / thinking indicator (#42276)** – 6 comments – parity with OpenAI/Grok UX.
- **Distributed Agent Runtime RFC (#42026)** – 7 comments, 3 👍 – long-term architectural vision.

### Less Likely but Discussed

- **Multi-session architecture (#48874)** – RFC with 7 comments.
- **YAML config support (#45758)** – 7 comments, 2 👍 – nice-to-have.
- **Cross-channel TUI visibility (#40678)** – 6 comments, 1 👍 – complex to implement.

## User Feedback Summary

**Pain Points:**
- **Message leaks** – internal processing text appearing in user channels (most upvoted concern).
- **Subagent unreliability** – silent failures, lost completions, no retry.
- **Steer mode broken** – mid-turn injection not working as documented.
- **Performance regressions** – `doctor --fix` 4–5x slower; compaction causing session hangs.
- **Provider-specific bugs** – Anthropic thinking block signature error, Gemini null conversion, Ollama tool arguments object.
- **Security gaps** – prompt injection via gh-issues, Discord tool-trace leaks, sandbox pidsLimit missing.
- **Memory management inconsistency** – different users experiencing different storage backends.
- **Media delivery issues** – Feishu image loss, image generation success but delivery failure.
- **Cron reliability** – timeouts, silent skips, isolated session setup failures.

**Satisfaction Indicators:**
- High community engagement (many comments, reactions).
- Users filing detailed reproducible bug reports and feature requests.
- Some PRs actively being reviewed and merged; maintainers responding.

**Dissatisfaction Indicators:**
- Many P1 bugs have “needs-maintainer-review” and “no-new-fix-pr” tags, indicating slow resolution.
- Multiple stale issues (e.g., #38327 from March 6, #42276 from March 10) still open.
- Regression in recent releases (e.g., 2026.5.20 performance, 2026.3.2 Gemini crash) frustrates users.
- “Beta release blocker” and “ux-release-blocker” tags suggest project feels unstable for production.

## Backlog Watch

### Old High-Importance Issues Awaiting Maintainer Action

1. **#38327** – *“Cannot convert undefined or null to object”* (P1, diamond lobster) – created 2026-03-06, last updated 2026-07-09. No fix PR. Stale.  
   [Issue link](https://github.com/openclaw/openclaw/issues/38327)

2. **#38439** – *Webchat avatar endpoint 404* (P2, platinum hermit) – created 2026-03-07, last updated 2026-07-08. No fix PR.  
   [Issue link](https://github.com/openclaw/openclaw/issues/38439)

3. **#39476** – *A2A sessions_send duplicate messages* (P1, platinum hermit) – created 2026-03-08, last updated 2026-07-09. No fix PR.  
   [Issue link](https://github.com/openclaw/openclaw/issues/39476)

4. **#39604** – *Feature: allowPrivateNetwork* (P2, diamond lobster) – created 2026-03-08, 11 👍, no fix PR.  
   [Issue link](https://github.com/openclaw/openclaw/issues/39604)

5. **#44098** – *fix(security): add default pidsLimit for sandbox containers* (PR) – created 2026-03-12, stale, needs real-behavior-proof.  
   [PR link](https://github.com/openclaw/openclaw/pull/44098)

6. **#42276** – *Reasoning stream / thinking indicator* (enhancement, P2) – created 2026-03-10, 6 comments, no action.  
   [Issue link](https://github.com/openclaw/openclaw/issues/42276)

These items represent unresolved friction for operators and developers. Without maintainer review, they risk becoming permanent debt.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Open Personal AI Agent Ecosystem
**Date:** 2026-07-09

---

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is experiencing a phase of intense, volatile growth marked by high community engagement but significant reliability debt. Both OpenClaw and Hermes Agent show daily activity volumes that signal strong developer interest—500+ issues/PRs for OpenClaw and 50+ for Hermes—yet both projects struggle with P1/P2 bugs around session management, provider fallback, and security hardening. The landscape is bifurcated: one project (OpenClaw) serves as the core reference implementation bearing the weight of foundational stability work, while the other (Hermes) focuses on end-user polish, desktop/CLI parity, and gateway integrations. Common pain points—message leaks, silent failures, cross-platform inconsistencies—reveal that the ecosystem has not yet achieved production-grade reliability despite rapid iteration.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|---|---|---|
| **Open Issues** | 457 | 47 |
| **Closed Issues (24h)** | 43 | 3 |
| **Open PRs** | 407 | 49 |
| **Merged/Closed PRs (24h)** | 93 | 1 |
| **Release (24h)** | None | v0.18.2 (patch) |
| **P0/P1 Blockers** | 10+ identified (P0: #43661) | 0 P0, 12+ P2 |
| **Health Signal** | Strained – high activity, growing backlog, stale critical bugs | Healthy – responsive patching, moderate bug debt |

**Health Score Interpretation:**
- **OpenClaw** – 6/10: Extreme activity indicates community vitality but the P0 release blocker and numerous “needs-maintainer-review” tags suggest maintainers are overwhelmed. The project is in a *crisis-of-scale* phase.
- **Hermes Agent** – 8/10: Lower raw numbers but higher resolution velocity. The same-day patch (v0.18.2) demonstrates effective triage. Bug debt exists but is mostly P2 and newer.

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Ecosystem gravity:** As the core reference implementation, OpenClaw attracts the bulk of community attention—10x the issue/PR volume of Hermes. This creates a larger pool of contributors, bug reports, and feature requests.
- **Architectural scope:** OpenClaw tackles deeper infrastructure problems (session compaction, sandbox containers, A2A protocol, subagent orchestration) that Hermes does not yet address. It is the platform layer.
- **Provider compatibility breadth:** Fixes for Ollama, Anthropic, Google Vertex, and WhatsApp indicate a wider provider surface area than Hermes’s primary OpenAI/OpenRouter focus.

**Technical Approach Differences:**
- OpenClaw uses a **subagent architecture** with explicit session management and compaction; Hermes appears more monolithic with session state attached to launchers (CLI/Desktop/gateway).
- Sandbox isolation (pidsLimit, containers) is unique to OpenClaw—Hermes does not mention sandboxing.

**Community Size Comparison:**
- OpenClaw’s daily activity (500 issues/PRs) dwarfs Hermes (50), but raw volume does not equal velocity. OpenClaw’s **closure rate (93 PRs merged vs. 407 open)** is ~19%, while Hermes’s (1 merged vs. 49 open) is ~2%—but OpenClaw’s open PR count includes many from earlier periods of higher throughput.
- **Upvote-weighted demand:** Hermes’s top feature (#39691, 12 👍) has higher per-capita enthusiasm than OpenClaw’s most-upvoted feature (#39604, 11 👍) despite OpenClaw’s larger base.

---

## 4. Shared Technical Focus Areas

The following requirements surface independently in **both** projects, indicating ecosystem-wide gaps:

| Requirement | OpenClaw | Hermes Agent |
|---|---|---|
| **Session reliability** – hanging, silent loss, duplicate messages | #43661 (compaction hang), #44925 (subagent loss), #39476 (duplicate messages) | #61220 (expiry not finalizing), #48098 (stale “summarizing” after compaction) |
| **Provider fallback transparency** – silent failures, buffered notices | #35419 (fallback silent) – *same issue number exists in OpenClaw* | #35419 (Hermes also has this issue), #61048 (fallback ignored) |
| **Security hardening** – prompt injection, tool-trace leaks, sandbox | #45740 (gh-issues injection), #44905 (Discord trace leak), #43996 (sandbox crash) | #5254 (tool repeats with LM-Studio – potential injection surface) |
| **Cross-platform UX parity** – text truncation, session discoverability | #38439 (webchat avatar 404), #25592 (leaks to messaging channels) | #39534 (Chinese text cut), #59224 (CLI hides Desktop sessions) |
| **Reasoning/thinking indicator** – streaming display for thought blocks | #42276 (open feature request) | #18241 (TUI chronological order) |
| **Compression and context management** – per-tool vs. full-summary | Underlying issue in session compaction (#43661) | #39691 (headroom-ai per-tool compression – 12 👍) |

**Finding:** The ecosystem is converging on *observability of internal state* (what is the agent thinking? did fallback fire? why is it stuck?) as the dominant unmet need.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|---|---|---|
| **Primary target user** | Operators, self-hosters, integrators building on reference architecture | End-users, desktop-first, casual and power users |
| **Deployment model** | CLI + gateway + sandbox; heavy infrastructure | Desktop app + CLI + gateway; lighter footprint |
| **Provider strategy** | Broad (OpenAI, Anthropic, Ollama, Google, WhatsApp, Telegram) | Narrower (OpenAI, OpenRouter, Nous inference, LM-Studio, WeCom) |
| **UI/UX investment** | Moderate (webchat, TUI, steering mode) | High (Desktop GUI, “/plan”, reasoning panel, system tray, unread badges) |
| **Security posture** | Explicit sandboxing, pidsLimit, signature verification | No sandboxing; focus on OIDC logout and config validation |
| **Cross-platform** | Linux/macOS focus; Windows issues visible | Windows support actively regressing (Chinese cut-off, file path encoding) |
| **Community engagement style** | High-volume, lower-resolution (many open items) | Lower-volume, higher-resolution (quick patches, active PR review) |

**Key Takeaway:** OpenClaw is the *infrastructure project*; Hermes is the *user experience project*. They serve different layers of the stack but share a common foundation in session management and provider routing.

---

## 6. Community Momentum & Maturity

**Activity Tiers:**

- **Tier 1 – Rapid iteration with stability risk (OpenClaw):** 500 daily events, 93 merges/24h, but 10+ P1s and a P0 blocker. The project is moving fast but accumulating technical debt faster than it can resolve it. The “beta release blocker” tag signals the maintainers themselves perceive immaturity.
- **Tier 2 – Stable, responsive iteration (Hermes Agent):** 50 daily events, quick patch releases, bug fixes that land within 24–48h of reports. The bug debt is younger and lower severity. Hermes appears to be exiting “rapid prototyping” and entering “polish and scale.”

**Maturity Assessment:**
- **OpenClaw** is in an *adolescent crisis* – community size has outgrown maintainer capacity. The risk is contributor burnout and fork potential.
- **Hermes** is in *steady adolescence* – enough capacity to patch, but still accumulating feature debt (ACP server, compression, reasoning display) that may slow as codebase grows.

---

## 7. Trend Signals

Six industry trends extracted from community feedback across both projects:

1. **Compression as first-class primitive:** Users no longer accept “summarize everything.” They want per-tool, per-turn, configurable compression (OpenClaw’s compaction + Hermes’s headroom-ai integration). *For developers: build compression hooks into agent cores, not as afterthoughts.*

2. **Fallback transparency:** Silent fallback is a top complaint in both projects. Users need to know *when* fallback fires, *why* (e.g., rate limit, model down), and *what the next model is*. *For developers: emit structured fallback events; don’t treat fallback as an internal implementation detail.*

3. **Cross-platform is hard, Windows is bleeding:** Both projects have Windows-specific regressions (file paths, Chinese rendering, build failures). The user base is increasingly multi-platform, but Linux/macOS dominance leaves Windows behind. *For developers: if you target Windows, invest in CI coverage for path encoding, Unicode, and file system differences.*

4. **Security is reactive, not proactive:** Both projects have open prompt injection vulnerabilities (gh-issues, Discord traces) that are acknowledged but not fixed. The community is filing security issues faster than maintainers can triage. *For developers: adopt input sanitization as a default behavior for any user-supplied content that enters agent prompts.*

5. **Reasoning model UX is under-designed:** Both projects have open feature requests for thinking indicators, chronological interleaving, and expanded reasoning blocks. As reasoning models (o1, Claude 3.5, Gemini 2.5 Pro) become default, the lack of structured thought display is a UX gap. *For developers: design UI components for streaming thought blocks now; they will become table stakes within six months.*

6. **Session state is the new database:** Both projects treat sessions as infinite, mutable streams. Issues around compaction, expiry, duplicate messages, and silent loss reveal that session management is the hardest unsolved engineering problem in personal AI agents. *For developers: treat session lifecycle with the same rigor as database transactions—ACID-like guarantees for message ordering, idempotent writes, and explicit failure notifications.*

---

*Report generated from community digest data for 2026-07-09. All issue references are from the respective project repositories.*

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-09

## Today's Overview

Hermes Agent saw extremely high activity in the last 24 hours, with **50 issues** and **50 pull requests** updated, alongside **1 new patch release**. 47 issues remain open, 3 were closed; 49 PRs are open and 1 was merged/closed. The community is heavily engaged, with multiple critical bug reports and feature requests emerging, particularly around Windows platform support, gateway integrations, and desktop UI polish. The pace suggests a healthy, responsive project with sustained contributor momentum.

## Releases

**v2026.7.7.2 (Hermes Agent v0.18.2)** – July 7, 2026  
A same-day patch on v0.18.1 that fixes a blocking Docker build issue:  
- **fix(whatsapp):** unpin Baileys from a git commit; use published `7.0.0-rc13` instead.  
No breaking changes or migration notes required.  
[View release](https://github.com/NousResearch/hermes-agent/releases/tag/v2026.7.7.2)

## Project Progress

Only **one PR was merged/closed** in the last 24 hours (not among the top-20 listed), indicating a relatively quiet day for landings. However, **three issues were closed**:

- **Closed** (`#28260`): *custom_providers with self-signed HTTPS endpoints fail* – now resolved.  
- **Closed** (`#61087`): *Desktop app does not stop gateway on quit (macOS)* – presumably fixed.  

Several fix PRs are in flight that target open bugs (see *Bugs & Stability*). The merged PR likely addressed a minor fix; specifics were not among the top-20 PRs.

## Community Hot Topics

The following issues and PRs generated the most discussion and reactions today:

- **#39691** [OPEN] – *Feat: integrate headroom-ai for tool output compression*  
  **9 comments, 12 👍**  
  Top community demand – users want smarter, per-tool compression rather than full-conversation summarization.  
  [Issue link](https://github.com/NousResearch/hermes-agent/issues/39691)

- **#59224** [OPEN, P2] – *Classic CLI /resume listing hides Desktop sessions*  
  **8 comments**  
  Frustration about session discoverability across launchers.  
  [Issue link](https://github.com/NousResearch/hermes-agent/issues/59224)

- **#39534** [OPEN, P3] – *Desktop Windows cuts off Chinese prompt in chat window*  
  **7 comments**  
  Language-specific rendering bug frustrating Chinese-speaking users.  
  [Issue link](https://github.com/NousResearch/hermes-agent/issues/39534)

- **#569** [OPEN] – *Agent Client Protocol (ACP) Server Mode*  
  **2 comments, 9 👍**  
  Long-standing request to integrate with Zed, JetBrains, Neovim via ACP.  
  [Issue link](https://github.com/NousResearch/hermes-agent/issues/569)

- **#18241** [OPEN, P3] – *TUI: show thinking blocks and tool calls in chronological order*  
  **2 comments, 4 👍**  
  Users want interleaved reasoning/tool-call display for reasoning models.  
  [Issue link](https://github.com/NousResearch/hermes-agent/issues/18241)

**Underlying needs**: Better context management (compression), cross-platform session visibility, multi-platform support (iMessage via Blooio PR #61250), and richer UI for reasoning models.

## Bugs & Stability

**Critical/High-severity bugs (P2) reported or updated in the last 24 hours:**

1. **#59224** – *CLI /resume hides Desktop sessions* (P2) – No fix PR yet.  
2. **#58646** – *QQ bot adapter startup failure: unexpected keyword 'is_reconnect'* (P2) – No fix PR.  
3. **#48098** – *Desktop shows stale "Summarizing thread" after compaction resumes* (P2) – No fix PR.  
4. **#5254** – *Tool calls repeating when using LM-Studio* (P2, created Apr 5, still open) – No fix PR.  
5. **#35419** – *Successful fallback activation is silent because buffered notices are never flushed* (P2) – No fix PR.  
6. **#39047** – *Auxiliary compression routes provider-qualified Gemini model to Codex backend* (P2) – No fix PR.  
7. **#39838** – *notification_sources config never read by gateway* (P2) – No fix PR.  
8. **#61220** – *Session expiry finalization doesn't set end_reason, stale recovery reopens expired sessions* (P2) – No fix PR.  
9. **#61207** – *'/plan' doesn't write a plan file anymore* (P2) – No fix PR.  
10. **#61211** – *WeCom file upload fails with FileNotFoundError due to percent-encoded filename > MAX_PATH* (P2) – **Fix PR #61253 exists.**  
11. **#61048** – *Kanban worker ignores fallback_providers* (P3, but affects reliability).  
12. **#60715** – *Nous inference API completely unreachable* (P2, needs-repro) – Possibly an environment issue.  

**Moderate-severity (P3):**  
- #39534 (Chinese prompt cut off)  
- #39558 (intermediate assistant text disappears)  
- #61099 (OpenRouter "Unknown" App intermittently)  

**Platform-specific:** Several bugs affect Windows (file path encoding, Chinese rendering).  

**Summary:** The project has a sizable bug debt, especially around session state, gateway adapters, and provider fallback. Some have accompanying fix PRs (WeCom encoding, OIDC logout, desktop tool expansion), but many remain unaddressed.

## Feature Requests & Roadmap Signals

Highlights from feature requests updated today:

- **#39691** – Tool output compression via headroom-ai (12 👍) – Likely candidate for next minor version.  
- **#50718** – Session visibility & notifications (unread markers, OS badges) – Strong user demand.  
- **#569** – ACP Server Mode for editor integration – Long-standing, but still open.  
- **#53617** – Desktop GUI: keep reasoning panel expanded – Small UX improvement.  
- **#23524** – Per-cron reasoning effort overrides – Useful for scheduled tasks.  
- **#61246** – Minimize to system tray on close (Windows) – Duplicate request.  
- **#61193** – Show full terminal command in desktop app – Usability enhancement.  
- **#61249** – Approval bar truncates multi-line diffs – Approval workflow usability.  
- **#61243** – Self-hosted OIDC RP-Initiated Logout – Enterprise security feature.  

**Prediction for v0.19:** The high-reaction compression feature (#39691) and session visibility improvements (#50718) are likely candidates, given their popularity and community engagement.

## User Feedback Summary

**Pain points expressed:**

- "Chinese text cut off after update" – rendering regression on Windows Desktop.  
- "QQ bot adapter fails to connect on reconnection" – gateway integration instability.  
- "Stale 'Summarizing thread' status after compaction" – misleading UI state.  
- "Tool calls repeating when using LM-Studio" – core agent issue affecting non-OpenAI providers.  
- "Desktop app does not stop gateway on quit" – expected behavior not met.  
- "Can't see full terminal command in desktop app" – transparency loss.  
- "Plan command stopped writing plan files" – regression in /plan functionality.  
- "Fallback activation is silent" – users want to know when fallback kicks in.  
- "WeCom file upload fails with Chinese filenames" – Windows path length limitation.  

**Satisfaction signals:** High engagement (50 issues/PRs in 24h) suggests active and invested community. The quick patch release (v0.18.2) shows responsive maintenance. No positive praise is captured in the data, but the volume of contribution is a positive indicator.

## Backlog Watch

Long-standing issues and PRs that have not received maintainer attention or are stuck:

| Item | Created | Last Update | Notes |
|------|---------|-------------|-------|
| **#5254** – Tool calls repeating with LM-Studio (P2) | 2026-04-05 | 2026-07-09 | Open for 3 months, no fix PR |
| **#569** – ACP Server Mode (feature) | 2026-03-07 | 2026-07-08 | 9 👍, no PR merged |
| **#18241** – TUI chronological order (feature, P3) | 2026-05-01 | 2026-07-09 | 4 👍, no PR |
| **#23524** – Per-cron reasoning effort (feature, P3) | 2026-05-11 | 2026-07-09 | Low maintainer activity |
| **#39534** – Chinese text cut off (P3) | 2026-06-05 | 2026-07-09 | Continued user frustration |
| **#39754** – Fix Hindsight embedded dependency (PR) | 2026-06-05 | 2026-07-09 | Open for a month |
| **#53118** – Desktop build fix when ignore-scripts=true (PR) | 2026-06-26 | 2026-07-09 | Waiting for review |
| **#52094** – Persist model visibility preferences (PR) | 2026-06-24 | 2026-07-09 | Open, needed for UX |
| **#52209** – Register auxiliary as valid web extract backend (PR) | 2026-06-25 | 2026-07-09 | Open, addresses config confusion |

These items may require maintainer prioritization, especially the older P2 bug (#5254) and the highly-demanded ACP feature (#569).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*