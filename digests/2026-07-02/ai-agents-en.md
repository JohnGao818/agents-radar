# OpenClaw Ecosystem Digest 2026-07-02

> Issues: 251 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-02 02:52 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-02

## 1. Today's Overview

OpenClaw saw extremely high activity in the past 24 hours: **251 issues** (142 open, 109 closed) and **500 pull requests** (433 open, 67 merged/closed) were updated. This volume signals a period of intense development and issue triaging, likely driven by the recent `v2026.6.11` release and its associated regressions. No new releases were published today. Despite the high volume, several critical bugs remain unresolved and are drawing significant community attention, while a steady flow of fix PRs indicates active maintenance.

---

## 2. Releases

No new releases were published today. The latest available version remains `v2026.6.11`.

---

## 3. Project Progress

In the last 24 hours, **67 pull requests were merged or closed**. Notable closed PRs include:

- **#68936** — Autofix pipeline for PR review comments + Windows daemon (large feature).
- **#76370** — Fix to hide operator-only exec controls from model args (security).
- **#93209** — Test helper for auto-cleaning temp directories (test infrastructure).
- **#98341** — Bounded JSON response reads in Feishu channel (OOM prevention).
- **#98355** — Bounded JSON response reads in Google Meet extension (OOM prevention).
- **#98047** — Guard malformed SSE frames in OpenRouter music generation (stability).
- **#98366** — Various closed bug fixes and minor improvements.

These represent ongoing efforts to improve stability, security, and developer tooling. No major new features were merged.

---

## 4. Community Hot Topics

The most active issues and PRs (by comment count and reactions) reflect deep concerns about reliability and data integrity:

| Issue | Comments | 👍 | Summary |
|-------|----------|---|---------|
| [**#92201**](https://github.com/openclaw/openclaw/issues/92201) | 17 | 1 | Intermittent invalid thinking signatures on Anthropic replay; recovery wrapper never fires because error text is generic. **Diamond lobster** severity. |
| [**#7707**](https://github.com/openclaw/openclaw/issues/7707) | 13 | 0 | Feature: Memory Trust Tagging by Source — prevent memory poisoning from untrusted content. |
| [**#45608**](https://github.com/openclaw/openclaw/issues/45608) | 11 | 4 | Feature: Pre-reset agentic memory flush before `/new` and daily resets. |
| [**#38327**](https://github.com/openclaw/openclaw/issues/38327) | 10 | 3 | Regression: "Cannot convert undefined or null to object" with google-vertex/gemini-3.1-pro-preview in v2026.3.2. |
| [**#94228**](https://github.com/openclaw/openclaw/issues/94228) | 10 | 2 | Native Anthropic path: replaying thinking blocks bricks long tool-use threads ("Invalid signature"). |
| [**#98416**](https://github.com/openclaw/openclaw/issues/98416) | 6 | 5 | Bug: v2026.6.11 published dist missing reentrancy guard → reply session initialization conflicted. |

**Underlying needs**: Users are asking for better robustness in streaming signature validation, transparent memory management (tagging, flushing, preservation), and faster resolution of regressions introduced in recent releases. The high number of diamond-lobster and platinum-hermit tagged issues indicates these are top priority.

---

## 5. Bugs & Stability

Several critical bugs were reported or updated today, many of them regressions:

### Critical / P1

- [**#98416**](https://github.com/openclaw/openclaw/issues/98416) — **Missing reentrancy guard** in v2026.6.11 dist: leads to conflicted reply session init. 5 👍. No fix PR yet.
- [**#98672**](https://github.com/openclaw/openclaw/issues/98672) — **Sessions breaking constantly** after 2026.6.11 upgrade. Reported as regression.
- [**#98528**](https://github.com/openclaw/openclaw/issues/98528) — **Tool output returns empty** after first call per turn (2026.6.11 regression). No fix PR linked.
- [**#98740**](https://github.com/openclaw/openclaw/issues/98740) — **Mattermost native slash commands return 401** after 6.11 plugin externalization. No fix PR yet.
- [**#98327**](https://github.com/openclaw/openclaw/issues/38327) — Long-standing **"Cannot convert undefined or null to object"** with Gemini (since March). Still open.
- [**#98565**](https://github.com/openclaw/openclaw/issues/98565) — **Container image upgrades skip migrations** before gateway startup.

### High / P2

- [**#98713**](https://github.com/openclaw/openclaw/issues/98713) — Model `opencode-go/kimi-k2.6` resolves to `deepseek-v4-pro` at runtime.
- [**#98540**](https://github.com/openclaw/openclaw/issues/98540) — Composer shows idle state while agent is executing tools.

### Fix PRs available

- [#98788](https://github.com/openclaw/openclaw/pull/98788) — Fix missing `operator.write` scope in auth-none deployments (#98614).
- [#98819](https://github.com/openclaw/openclaw/pull/98819) — Fix Mattermost `401` by resolving public artifacts from plugin roots (addresses #98740).
- [#98826](https://github.com/openclaw/openclaw/pull/98826) — Preserve non-array tool result replay text (fixes replay regression).
- [#98862](https://github.com/openclaw/openclaw/pull/98862) — Fix MS Teams proactive sends after conversation migration.

Many of the P1 regressions appear to be linked to the `v2026.6.11` release and are being actively addressed.

---

## 6. Feature Requests & Roadmap Signals

The most-discussed features point toward better memory management and security:

| Issue | Summary | Likely for Next Release |
|-------|---------|-------------------------|
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | **Memory Trust Tagging by Source** — tag memory entries by trust level. | Medium — needs security review and product decision. |
| [#45608](https://github.com/openclaw/openclaw/issues/45608) | **Pre-reset agentic memory flush** — run memory flush before `/new` and daily reset. | High — similar mechanism already exists for compaction. |
| [#40418](https://github.com/openclaw/openclaw/issues/40418) | **Automated Session Memory Preservation & Synthesis** — preserve and consolidate knowledge across sessions. | Medium — overlaps with #45608. |
| [#90916](https://github.com/openclaw/openclaw/issues/90916) | **Topic-session families** — multiple named context lanes per agent. | Low — conceptual, no implementation. |
| [#20935](https://github.com/openclaw/openclaw/issues/20935) | **Audit log for agent memory changes** — tamper detection. | Low — security review pending. |
| [#95477](https://github.com/openclaw/openclaw/issues/95477) | **Post-task self-reflection for skill auto-creation** + prefix cache optimization. | Low — duplicate concerns raised. |

Given the high volume of memory-related bugs (lost context, stale memory, missing flushes), it is likely that **memory lifecycle improvements** will appear in the next minor release.

---

## 7. User Feedback Summary

Users are reporting:

- **Frustration with regressions**: Several users upgraded to `2026.6.11` and immediately hit session breaks, empty tool outputs, or auth failures. The sentiment is that the release may have been rushed.
- **Desire for better memory persistence**: Multiple feature requests and bug reports revolve around memory not being preserved across resets or compactions.
- **Authentication and security concerns**: Issues like Mattermost 401 (migration bug) and Discord WebSocket proxy bypass highlight integration pain.
- **Positive signals**: Despite bugs, the community remains engaged, with high numbers of 👍 on bug reports and feature requests, and active participation in issue discussions.

One user (noted in #98416) requested a quicker hotfix, and several reported satisfaction with the quick response from maintainers on previous issues.

---

## 8. Backlog Watch

Several high-severity issues have been open for weeks or months without resolution, despite maintainer tags:

| Issue | Age | Severity | Status |
|-------|-----|----------|--------|
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | ~4 months (since Mar 6) | P1, regression | Needs maintainer review, product decision |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | ~5 months (since Feb 3) | P2, diamond lobster | Needs maintainer review, product decision, security review |
| [#45608](https://github.com/openclaw/openclaw/issues/45608) | ~3.5 months (since Mar 14) | P2, diamond lobster | Needs maintainer review, product decision, security review |
| [#20935](https://github.com/openclaw/openclaw/issues/20935) | ~4.5 months (since Feb 19) | P2, diamond lobster | Needs maintainer review, product decision, security review |
| [#78562](https://github.com/openclaw/openclaw/issues/78562) | ~2 months (since May 6) | P1, platinum hermit | Needs product decision, live repro |
| [#80131](https://github.com/openclaw/openclaw/issues/80131) | ~2 months (since May 10) | P2, platinum hermit | Needs maintainer review, product decision |

Several PRs also remain in "waiting on author" or "needs proof" state, including [#72932](https://github.com/openclaw/openclaw/pull/72932) (gateway startup fix) and [#73403](https://github.com/openclaw/openclaw/pull/73403) (agent channel routing). These could benefit from maintainer attention to move forward.

**Overall project health**: Very high activity, but regression churn is concerning. The team appears responsive to critical issues, but backlog of high-priority feature requests and security reviews is growing.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Agent Open-Source Ecosystem
**Date:** 2026-07-02

## 1. Ecosystem Overview

The personal AI assistant and agent open-source landscape is experiencing an intense phase of rapid iteration, driven by post-release stabilization cycles and growing community expectations for production-grade reliability. Both OpenClaw and Hermes Agent shipped major releases in the past week, triggering a surge of regression fixes, security patches, and feature requests that dominate current development activity. The ecosystem is bifurcating between foundational infrastructure projects (OpenClaw's reference implementation) and application-focused agent frameworks (Hermes Agent's autonomy features), though both share critical challenges in memory management, streaming reliability, and cross-platform authentication. User sentiment reflects high engagement but growing impatience with regressions that break core workflows, signaling that the market is moving from "building excitement" to "demanding stability."

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues Updated (24h)** | 251 (142 open, 109 closed) | 50 (44 open, 6 closed) |
| **PRs Updated (24h)** | 500 (433 open, 67 merged/closed) | 50 (35 open, 15 merged/closed) |
| **Latest Release** | v2026.6.11 (Jun 11) | v0.18.0 "The Judgment Release" (Jul 1) |
| **PR Merge Rate (24h)** | 67 | 15 |
| **Critical Bugs (P0/P1)** | ~6 active P1 regressions | 1 P0 (closed), ~7 P2 active |
| **Community Contributors** | Not specified (reference project) | 370+ contributors in last cycle |
| **Project Health Score** | Mixed – very high activity but concerning regression churn | Solid – rapid post-release bug closure, healthy contributor momentum |

**Context:** OpenClaw's dramatically higher issue/PR counts reflect its role as the core reference implementation with broader surface area (multi-platform plugins, Windows daemon, 100+ integrations). Hermes Agent shows more focused, manageable post-release activity typical of a smaller but highly engaged community.

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale & Breadth:** As the reference implementation, OpenClaw has the widest integration surface (Mattermost, MS Teams, Google Meet, Feishu, OpenRouter, Anthropic, Gemini). This makes it the de facto standard for multi-platform agent deployment.
- **Security Focus:** Active work on operator-only exec controls (#76370), bounded JSON reads to prevent OOM (#98341, #98355), and malformed SSE frame guards (#98047) show stronger security hardening than Hermes Agent's post-release patch cycle suggests.
- **Memory Innovation:** OpenClaw is pioneering memory trust tagging (#7707), pre-reset agentic flushes (#45608), and session memory preservation (#40418) – features Hermes Agent has not yet addressed publicly.

**Technical Approach Differences:**
- OpenClaw uses a **plugin-based architecture** with a Windows daemon and broad platform support, while Hermes Agent focuses on **unified agent reasoning** with platform-specific adapters (Telegram, Discord, iMessage).
- OpenClaw's release cadence appears slower but more methodical (v2026.6.11 → now), whereas Hermes Agent ships named releases with thematic identity (v0.18.0 "The Judgment").

**Community Size Comparison:**
- OpenClaw has higher raw activity (251 issues/day) but the digest lacks contributor count. Hermes Agent explicitly cites 370+ contributors in one cycle, suggesting stronger distributed contributor engagement. OpenClaw may have more *corporate/enterprise* contributors given its reference status, while Hermes may have more *individual developers*.

**Verdict:** OpenClaw dominates in breadth and infrastructure maturity; Hermes leads in community velocity and focused autonomy features.

## 4. Shared Technical Focus Areas

Both projects reveal overlapping requirements emerging from their communities:

| Requirement | OpenClaw | Hermes Agent |
|-------------|----------|--------------|
| **Memory lifecycle management** | #7707 (trust tagging), #45608 (pre-reset flush), #40418 (preservation) | Not yet public – but token overhead concern (#13983) implies context/memory issues |
| **Authentication reliability** | Mattermost 401 (#98740), auth-none deployments (#98788), MS Teams migration fix (#98862) | OAuth PKCE state cookie (#56750), headless MCP reconnect (#56673) |
| **Streaming/RPC robustness** | SSE frame guarding (#98047), bounded JSON reads (#98341), thinking signature validation (#92201, #94228) | Not explicitly stated, but token overhead (#13983) and toolset loss (#56732) suggest similar pain |
| **Tool execution reliability** | Empty tool output regression (#98528), malformed SSE frames (#98047) | Computer_use capture failure (#56704), terminal toolset loss (#56732) |
| **Platform-specific issues** | Windows daemon (#68936), Google Meet, Feishu, MS Teams | Windows console flashes (#56747), Linux/WSL computer_use (#56704) |

**Implied shared need:** Both communities are demanding **immutable context management** – predictable memory, stable streaming, and robust authentication that survives upgrades.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary Focus** | Core infrastructure & reference implementation | Agent autonomy & reasoning features |
| **Target User** | Developers building custom agent stacks | End-users wanting conversational autonomy |
| **Release Theme** | Stability-focused, fix-oriented | Feature-forward ("Judgment" – reasoning/autonomy) |
| **Integration Breadth** | 100+ plugins, enterprise platforms | Focused adapters (Telegram, Discord, iMessage, Web) |
| **Security Posture** | Proactive hardening (exec controls, OOM prevention, SSE guards) | Reactive (P0 shell escape fixed in v0.18.0) |
| **Memory Strategy** | Advanced: trust tagging, pre-reset flushes, session synthesis | Not publicly addressed; token overhead is community concern (#13983) |
| **Contributor Model** | Top-down reference project with corporate involvement | Bottom-up community with 370+ contributors |
| **Bug Closure Velocity** | High but regressions accumulate | Very high – many bugs closed within 24h |
| **Feature Backlog** | Growing – 5+ diamond/platinum issues blocked on product decisions | Focused – top-voted feature (#5712) aligns with release theme |

**Key Insight:** OpenClaw is *defensive* (preventing failure across many integrations), while Hermes Agent is *offensive* (shipping novel autonomy features with fast follow-up fixes). A developer evaluating both would choose OpenClaw for building reliable multi-platform infrastructure and Hermes for experimenting with autonomous agent loops.

## 6. Community Momentum & Maturity

**Activity Tiers:**

- **Tier 1 (Extreme):** OpenClaw – 251 issues + 500 PRs in 24h, but regression churn raises concern about release discipline.
- **Tier 2 (High):** Hermes Agent – 50 issues + 50 PRs, but healthy post-release ratio (15 merges vs 35 open) and rapid bug closure indicate good process.

**Iteration Speed:**
- **Hermes Agent is iterating faster** – closed 949 issues in one cycle, fixed shell escape P0, and shipped v0.18.0 with 1,720 commits. Bugs are closed within hours of reporting (#56533 closed same day).
- **OpenClaw is stabilizing under load** – 67 merges/day but P1 regressions from v2026.6.11 remain open (#98416, #98672, #98528). The backlog of diamond-lobster issues (some 4+ months old) suggests capacity constraints on product decisions.

**Maturity Signals:**
- Both have mature CI (test helpers, infrastructure types moving from beta to stable).
- OpenClaw shows signs of **enterprise maturity** (security reviews, OOM prevention, audit logs).
- Hermes shows **startup-stage velocity** (rapid feature shipping, fast bug fixes, but security gaps like the shell escape).

**Recommendation for decision-makers:** OpenClaw for production deployments requiring compliance and multi-platform support; Hermes for rapid prototyping and autonomy-focused products.

## 7. Trend Signals

**Industry Trends Extracted from Community Feedback:**

1. **“Zero trust memory” is the next frontier.** Both communities are demanding memory trust tagging, pre-reset flushes, and audit logs. This signals that naive context accumulation is no longer acceptable – users want *verifiable* agent memory that doesn’t leak or poison.

2. **Platform adapter fragility is a top pain point.** iMessage death spirals (Hermes #49858), Mattermost 401 (OpenClaw #98740), and Windows console flashes (Hermes #56747) show that multi-platform agents are brittle. Developers should invest in robust adapter lifecycle management and automatic reconnection.

3. **Token overhead awareness is rising.** Simple prompts consuming 16K tokens (Hermes #13983) and empty tool outputs (OpenClaw #98528) indicate that agent systems are wasting context budget on system prompts, validation logic, and inefficient streaming. Expect optimization of token usage to become a competitive advantage.

4. **Autonomy features are converging on “background awareness.”** Hermes’ top feature (#5712 – cron results into live chat) and OpenClaw’s memory flush stories both point to a future where agents work *proactively* rather than reactively. Developers should plan for event-driven agent architectures, not just chat completion loops.

5. **Authentication is a growing attack surface.** PKCE state cookie issues (Hermes #56750), Mattermost plugin auth (OpenClaw #98740), and OAuth reconnect hangs (Hermes #56673) reveal that security architecture for multi-platform agents is still immature. Expect more attention on OAuth state management, token rotation, and credential verification.

**Value for AI Agent Developers:**
- Prioritize **memory reliability** over new features – users will churn if context is lost mid-conversation.
- Invest in **platform adapter resilience** – one broken channel makes the whole agent seem unreliable.
- Audit your **token overhead** – developers of both projects underestimate how much system prompt bloat costs them.
- Plan for **proactive agent behaviors** – the market is shifting from “chatbot” to “digital employee” expectations.

---

**Bottom line:** The personal AI agent ecosystem is healthy, chaotic, and rapidly maturing. OpenClaw offers breadth and infrastructure depth; Hermes Agent offers velocity and feature innovation. A developer building for production should monitor both: deploy on OpenClaw for stability, experiment on Hermes for inspiration – and expect consolidation around memory management, authentication, and proactive autonomy within the next two quarters.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-02

## Today's Overview

Hermes Agent is showing **very high activity** following the release of v0.18.0 (“The Judgment Release”) on July 1. In the last 24 hours, **50 issues** (44 open, 6 closed) and **50 pull requests** (35 open, 15 merged/closed) were updated, indicating a healthy post-launch cycle of bug reports, feature discussions, and rapid fixes. The project closed **949 issues** over the last release cycle with contributions from **370+ community members**, underscoring strong contributor momentum. Today’s merged PRs focused on critical bug fixes (voice message transcription, dashboard stale-process cleanup, MCP stderr filtering) and test coverage improvements, while community discussion centered on deep autonomy features and platform-specific stability regressions.

## Releases

### v2026.7.1 – Hermes Agent v0.18.0 (The Judgment Release)  
**Released:** July 1, 2026  

- **Scale:** ~1,720 commits · 998 merged PRs · 2,215 files changed · ~251,000 insertions · ~41,000 deletions · 949 issues closed · 370+ community contributors  
- **Theme:** “The Judgment” – Major improvements to agent reasoning, autonomy, and decision-making.  
- **Notable changes (from release notes snippet):**  
  - Likely includes enhanced cron autonomy (see issue #5712) and new context-handling logic.  
- **Breaking changes / migration:** No explicit notes provided in the snippet; users should consult the full release changelog.  
- **Implication:** This is a substantial release – users upgrading from v0.17.0 should expect new features, possible configuration shifts, and resolution of many long-standing bugs.

## Project Progress

Today **15 PRs were merged or closed**, addressing a range of bugs and code quality:

| PR | Type | Summary |
|----|------|---------|
| [#56752](https://github.com/NousResearch/hermes-agent/pull/56752) | bug (closed) | fix(tui): check prebuilt bundle before requiring ui-tui/ workspace – prevents install abort |
| [#56754](https://github.com/NousResearch/hermes-agent/pull/56754) | feature (closed) | feat(skills): add surf crypto data skill (duplicate of #56755) |
| [#56743](https://github.com/NousResearch/hermes-agent/pull/56743) | bug (closed) | fix(gateway): transcribe voice messages during pending clarify – unblocks Telegram voice in clarification flows |
| [#45285](https://github.com/NousResearch/hermes-agent/pull/45285) | feature (closed) | fix(mcp): rotate and filter stderr logs – reduces log noise from MCP subprocesses |
| [#43877](https://github.com/NousResearch/hermes-agent/pull/43877) | test (closed) | test(gateway): cover fallback key env aliases |
| [#43876](https://github.com/NousResearch/hermes-agent/pull/43876) | bug (closed) | fix(cron): require exact silent marker for delivery suppression |
| [#43878](https://github.com/NousResearch/hermes-agent/pull/43878) | test (closed) | test(tools): cover malformed array coercion warnings |
| [#22359](https://github.com/NousResearch/hermes-agent/pull/22359) | chore (closed) | chore(gitignore): ignore CocoIndex code cache |
| [#22369](https://github.com/NousResearch/hermes-agent/pull/22369) | bug (closed) | fix(tui): prevent transcript tail cutoff |
| [#30651](https://github.com/NousResearch/hermes-agent/pull/30651) | feature (closed) | feat(agent): add provider fallback telemetry helper |

**Takeaway:** The team is actively shipping regression fixes and preventative tests, particularly for TUI, gateway, MCP, and cron subsystems.

## Community Hot Topics

The most active discussions (by comments/reactions) reveal strong user interest in deeper autonomy and critical platform reliability.

- **[#5712 – Feature: True Autonomy – Automatically Inject Cron Results into Live Gateway Chat Sessions](https://github.com/NousResearch/hermes-agent/issues/5712)**  
  *11 comments · 11 👍*  
  Request to allow cron job outputs to be injected into active chat sessions (e.g., Telegram, Discord) so agents can surface background results without manual polling. The idea builds on existing cron capabilities and is the top-voted feature request.

- **[#49858 – Bug: Photon iMessage sidecar death causes silent reconnect death spiral](https://github.com/NousResearch/hermes-agent/issues/49858)**  
  *8 comments*  
  Critical bug where the iMessage adapter enters an unrecoverable state after the Photon sidecar crashes, requiring full gateway restart. Users reporting complete channel loss.

- **[#13983 – Bug: 16K Tokens consumption by default](https://github.com/NousResearch/hermes-agent/issues/13983)**  
  *6 comments · 1 👍*  
  Performance concern: a simple “who u?” prompt consumes 16K+ tokens, raising questions about default system prompt overhead and bloated context.

- **[#55658 – Bug: It cannot be started after updating](https://github.com/NousResearch/hermes-agent/issues/55658)**  
  *4 comments*  
  User reports desktop app fails to launch after upgrading – potential regression in v0.18.0.

- **[#56533 – Bug: /journey slash command leaks raw ANSI escape codes (CLOSED)](https://github.com/NousResearch/hermes-agent/issues/56533)**  
  *4 comments*  
  Promptly closed – cosmetic issue in TUI/Desktop that degraded chat readability.

**Underlying needs:** Users want seamless autonomy (cron→chat injection), robust platform adapter recovery (iMessage), and minimal token overhead for basic interaction. The rapid closure of #56533 shows responsiveness to UI/UX regressions.

## Bugs & Stability

New and reopened bugs reported today (2026-07-02), ranked by severity (label P0–P2 shown):

| Issue | Severity | Component | Description | Fix PR? |
|-------|----------|-----------|-------------|---------|
| [#56750](https://github.com/NousResearch/hermes-agent/issues/56750) | P2 – auth | Dashboard | Remote dashboard OAuth fails with ‘Missing PKCE state cookie’ (SameSite=Lax issue) | [#56751](https://github.com/NousResearch/hermes-agent/pull/56751) (open) |
| [#56747](https://github.com/NousResearch/hermes-agent/issues/56747) | P2 – Windows | Desktop | Blank terminal console windows flash on Windows when agent runs tools | No PR yet |
| [#56732](https://github.com/NousResearch/hermes-agent/issues/56732) | P2 | CLI/Tools | hermes-api-server / hermes-acp lose entire terminal toolset (silent subset-check failure) | No PR yet |
| [#56727](https://github.com/NousResearch/hermes-agent/issues/56727) | P2 | Agent/Kimi | Kimi /coding endpoint thinking incorrectly blocked (PR #49143 regression) | No PR yet |
| [#56717](https://github.com/NousResearch/hermes-agent/issues/56717) | P2 | CLI | Non-default profile can keep stale runtime after update, causing ImportError | No PR yet |
| [#56704](https://github.com/NousResearch/hermes-agent/issues/56704) | P2 | Tools | computer_use capture fails on Linux/WSL with `int(None)` on pid/window_id | No PR yet |
| [#56673](https://github.com/NousResearch/hermes-agent/issues/56673) | P2 | MCP/Auth | Headless MCP OAuth reconnect hangs on no-refresh-token credential | No PR yet |
| [#56749](https://github.com/NousResearch/hermes-agent/issues/56749) | P3 | Agent | MoA mode: get_model_context_length() does not forward custom_providers, forcing 256k default | No PR yet |
| [#36846](https://github.com/NousResearch/hermes-agent/issues/36846) | **P0 – Security** | Terminal | Dangerous-command denylist bypassable with trivial shell escapes (CLOSED) | Closed today – fix in v0.18.0? |
| [#28260](https://github.com/NousResearch/hermes-agent/issues/28260) | P2 | Config | custom_providers with self-signed HTTPS endpoints fail with APIConnectionError (CLOSED) | Closed today |
| [#56533](https://github.com/NousResearch/hermes-agent/issues/56533) | P2 | TUI/Desktop | /journey slash command leaks raw ANSI escape codes (CLOSED) | Closed today |

**Stability summary:** Several P2 regressions emerged today, especially around authentication (PKCE cookie), platform-specific issues (Windows console flashes, Linux computer_use), and feature regressions (Kimi thinking block). The community is actively reporting and the team is already attaching fix PRs (e.g., #56751). The security bypass (P0) was closed, indicating a fix was already released.

## Feature Requests & Roadmap Signals

Top feature requests active or opened today:

- **[#5712 – True Autonomy: Inject Cron Results into Live Chat Sessions](https://github.com/NousResearch/hermes-agent/issues/5712)**  
  Highest-voted open feature. Likely to drive the next release focus on bridging cron and real-time conversation.

- **[#56655 – Task-aware per-turn model routing via pre_llm_call model override](https://github.com/NousResearch/hermes-agent/issues/56655)**  
  Plugin-based model selection per message (coding, quick answer, deep reasoning). Aligns with multi-provider architecture.

- **[#10572 – Support payload filtering or script param in webhooks](https://github.com/NousResearch/hermes-agent/issues/10572)**  
  Request to trigger only on specific webhook conditions (e.g., Todoist label changes). Practical integration need.

- **[#43625 – Desktop App: Live message sync from other platforms](https://github.com/NousResearch/hermes-agent/issues/43625)**  
  Cross-platform message unification – important for multi-device users.

- **[#54432 – Deduplicate Codex gpt-5.5 autoraise notice without disabling autoraise](https://github.com/NousResearch/hermes-agent/issues/54432)**  
  Spam reduction in Discord sessions.

- **[#56513 – Desktop app for Linux without installing the whole Hermes Agent](https://github.com/NousResearch/hermes-agent/issues/56513)**  
  Split client from server – a strong signal for a standalone desktop UI.

- **[#54393 – Dashboard font customization](https://github.com/NousResearch/hermes-agent/issues/54393)**  
  UX polish request.

**Prediction:** Next minor release (v0.18.1 or v0.19.0) will likely address the cron-injection feature (#5712) and the per-turn model routing (#56655), given community demand and alignment with the “Judgment” autonomy theme.

## User Feedback Summary

- **Satisfaction:** The huge release momentum (949 closed issues, 370+ contributors) indicates a thriving community. Many bugs are closed within 24 hours (e.g., #56533, #36846). Users appreciate rapid iteration.

- **Pain points (real quotes/context):**
  - “v0.17.0 Docker image cannot use Exa search backend at all” (#49445, closed) – resolved today.
  - “Simple `who u?` consumes 16K tokens – is this normal?” (#13983) – performance concern.
  - “Desktop app failed on cold start for three consecutive days” (#44668) – Windows startup reliability.
  - “Photon iMessage channel stays dead until entire Gateway is manually restarted” (#49858) – adapter reliability.
  - “`/journey` outputs raw ANSI codes like `?[38;2;...m` in chat bubbles” (#56533) – UI regression quickly fixed.

- **Common themes:** Users want zero-touch background autonomy, resilient platform bridges (iMessage, WhatsApp, Discord), lower token overhead, and a polished desktop experience for remote agents.

## Backlog Watch

Items that have been open for a while without recent maintainer movement:

- **[#5712 – True Autonomy (Apr 7)](https://github.com/NousResearch/her

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*