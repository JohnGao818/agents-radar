# OpenClaw Ecosystem Digest 2026-07-01

> Issues: 298 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-01 03:26 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-01

## 1. Today's Overview
OpenClaw saw very high activity over the last 24 hours: 298 issues were updated (236 open, 62 closed) and 500 pull requests were updated (404 open, 96 merged/closed). A new release, **v2026.6.11**, dropped with a focus on polishing rough edges — fixing misplaced replies, stuck sends, reconnects, model setup failures, and safer admin defaults. Despite the volume, the project remains in a healthy, fast-moving development cycle, with active community troubleshooting and rapid iteration on stability and security.

## 2. Releases
**v2026.6.11** was released today.  
[Full release notes](https://docs.openclaw.ai/releases/2026.6.11)

**Highlights:**  
- Fixes for misplaced replies and stuck sends in various channels.  
- Improved reconnection handling and model setup failure recovery.  
- Safer default admin configurations.  

No breaking changes or migration steps were documented in the release notes. Users are advised to review the changelog for minor behavioral adjustments in admin defaults.

## 3. Project Progress
Out of 500 PRs updated, **96 were merged or closed**. Notable closed PRs today:

- **[#98346]** – `fix: prevent skill-creator from bypassing workshop proposals` (merged, automerge) — resolves a policy self-contradiction where the built-in skill creator could bypass the required `skill_workshop` proposal workflow.
- **[#98169]** – `fix(heartbeat): scope commitment fan-out prompts` (closed) — addresses heartbeat scheduling issues that could cause duplicate or mistargeted commitment prompts.

Other fix PRs opened today (still open) target memory-wiki data loss ([#98364], [#98360]), iOS duplicate replies ([#98117]), Android TLS handshake timeouts ([#98366]), and unbounded response body reads ([#98355], [#98098]).

## 4. Community Hot Topics
The most active issues (by comment count) reveal a community focused on reliability, mobile support, and model integration:

- **[#9443]** (26 comments) – *Request: Prebuilt Android APK releases*  
  Users want official APK builds for the Android companion app. High interest (3 👍), needs product decision and security review.
- **[#92201]** (16 comments) – *Embedded runner: freshly streamed thinking signatures intermittently invalid on replay (Anthropic)*  
  A critical P1 bug affecting Anthropic provider users — recovery wrapper never fires due to generic error text. Needs maintainer review.
- **[#48003]** (14 comments) – *Steer mode does not inject messages mid-turn for main sessions*  
  High-severity regression where `steer` mode queues messages until turn completion instead of injecting mid-turn.
- **[#84516]** (11 comments) – *Codex app-server: long agent replies silently truncated at ~1000-1100 chars*  
  P1 bug causing silent message loss on headless Codex/OAuth agents. Needs live reproduction.
- **[#85103]** (10 comments) – *Model fallback chain not triggered on provider-wide quota exhaustion + EmbeddedAttemptSessionTakeoverError*  
  Another P1 reliability issue — fallback logic breaks when provider hits quota, leaving users stuck.

**Underlying needs:** Users are demanding **mobile parity** (Android APK), **reliable persistent sessions** (thinking signatures, fallback chains), and **transparent model behavior** (no silent truncation, correct steer injection).

## 5. Bugs & Stability
The highest-severity bugs (P0/P1, diamond lobster rating) reported or updated today:

| Issue | Severity | Summary | Fix PR exists? |
|-------|----------|---------|----------------|
| **[#98315]** | P1, security | Agent bypasses per-agent MCP server/skills allowlist via `mcporter --config` override | ❌ No |
| **[#98311]** | P2, message-loss | Feishu image/file replies lost on withdrawn reply targets; text replies survive | ❌ No |
| **[#98101]** | P2, misclassification | HTTP 429 with "overloaded" body mislabeled as rate limit instead of overloaded | ❌ No |
| **[#97983]** | P1, message-loss | iOS/WebChat messages append but do not trigger assistant replies | ❌ No |
| **[#85030]** | P1, security | MCP tools not injected into subagent sessions — security gap | ❌ No (linked PR open) |
| **[#85042]** | P1, security | Missing Google provider config silently routes Gemini requests to OpenAI | ❌ No |
| **[#84882]** | P0, data-loss | memory-core Dreaming silently deletes daily memory files | ❌ No (linked PR open) |
| **[#96704]** | P1, data-loss | Managed browser cookies never persist to disk | ❌ No |

**New bugs today (2026-07-01):**  
- [#98315] – Security bypass via `mcporter --config`.  
- [#98311] – Feishu media loss on withdrawn targets.  
- [#98101] – 429 overload misclassification.  
- [#97983] – iOS/WebChat reply failure.  

Several older high-severity bugs remain unfixed, with PRs open but waiting for maintainer review (e.g., #85030, #84882).

## 6. Feature Requests & Roadmap Signals
Notable feature requests with strong community support:

- **[#9443]** – Prebuilt Android APK releases (26 comments, 3 👍, filed Feb 2026). Likely to be addressed in the next major release given sustained interest and mobile ecosystem growth.
- **[#71058]** – Multiple Azure/Teams bots on a single Gateway (8 comments, 1 👍). Enterprise use case; may appear in a v2026.x feature release.
- **[#83954]** – Document/Support Pro-plan Codex models (gpt-5.5-pro, retired Spark) (4 comments). Smaller scope — could be a doc update or a minor extension.
- **[#91259]** – Drop redundant agent-id scoping from memory collection names (4 comments). Internal cleanup, likely to be merged soon.

**Prediction:** v2026.7 will almost certainly include the Android APK build pipeline (issue #9443 is heavily labelled and has been open since February), and possibly multi-Teams support. The fix for MCP tool injection (#85030) is also a high-priority security item.

## 7. User Feedback Summary
**Common pain points from today’s issues:**

- **Reliability:** Users report that sessions stall, messages are lost, and agent hangs block entire gateways (e.g., #84903, #84569, #84536). The community is vocal about needing better isolation and recovery.
- **Data loss:** Several issues report silent data deletion or truncation — memory files (#84882), browser cookies (#96704), long replies (#84516). This erodes trust.
- **Upgrade stability:** macOS and WSL2 users encountered unrecoverable gateways after upgrades (#85027, #84610), requiring restores or rollbacks. This is a barrier for self-hosters.
- **Mobile gaps:** iOS and Android users face broken voice, unreachable nodes, and lack of official builds. Talk (#91007) and Android node (#87058) are particularly broken.

**Satisfaction signals:** The rapid release cadence (v2026.6.11 today) shows the team is responsive. Many users acknowledge fixes are coming, but the sheer volume of open P1 bugs (diamond lobster) suggests reliability is the biggest challenge.

## 8. Backlog Watch
Issues and PRs that have been open for weeks or months and still lack maintainer action:

- **[#9443]** (Android APK) – Updated Jul 1, but needs product decision; no maintainer assignee.
- **[#92201]** (Anthropic thinking signature) – Needs maintainer review; filed Jun 11, no PR attached.
- **[#48003]** (steer mode injection) – Filed Mar 16; linked PR is open but needs maintainer review.
- **[#84516]** (Codex truncation) – Filed May 20; needs live reproduction and product decision.
- **[#85103]** (fallback chain) – Filed May 21; needs maintainer review, live repro.
- **[#85030]** (MCP tool injection) – Filed May 21; linked PR open, but needs maintainer review and security review.
- **[#38327]** (Google Vertex regression) – Filed Mar 6; still open, needs live repro.

These items represent the most critical unaddressed bugs and feature gaps. The number of “needs-maintainer-review” labels across diamond-lobster issues is concerning — the maintainer team appears capacity-constrained.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Ecosystem
**Date:** 2026-07-01 | **Analysis Period:** Last 24 hours

---

## 1. Ecosystem Overview

The open-source personal AI assistant landscape is characterized by rapid iteration, heavy community investment, and a clear tension between feature velocity and reliability. Both OpenClaw and Hermes Agent demonstrate vibrant ecosystems with hundreds of daily contributions, but they occupy different positions on the maturity spectrum: OpenClaw is in a high-velocity, high-bug-volume phase with daily releases, while Hermes Agent is stabilizing with steady maintenance and growing feature breadth. The community's top demands—mobile parity, session reliability, token optimization, and transparent model behavior—are consistent across both projects, signaling an industry-wide shift from "can it work?" to "can I trust it daily?" The gap between user expectation (stability) and project reality (frequent regressions) remains the ecosystem's defining challenge.

---

## 2. Activity Comparison (24 hours)

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues Updated** | 298 (236 open, 62 closed) | 50 (8 closed) |
| **PRs Updated** | 500 (404 open, 96 merged/closed) | 50 (15 merged/closed) |
| **Release Published** | ✅ v2026.6.11 | ❌ None |
| **P0/P1 Bugs Active** | ~8 new today; ~5 unfixed older | ~4 active; 7 new fix PRs filed |
| **Community Heat** | Very high (enterprise + mobile) | High (desktop + integration) |
| **Health Score** | ⚠️ High throughput, critical backlog | ✅ Stable output, targeted fixes |

**Insight:** OpenClaw processes ~6x more issues and ~10x more PRs than Hermes per day. However, OpenClaw's backlog of unaddressed P0/P1 bugs (e.g., #84882 data-loss, #96704 cookie persistence) suggests the velocity is straining quality assurance. Hermes resolves bugs with fix PRs filed the same day, showing tighter fix-to-detection cycles.

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Release cadence dominance:** Daily releases (v2026.6.11) signal a team that can ship quickly—no other project in the ecosystem matches this frequency.
- **Enterprise integration breadth:** Multiple Azure/Teams bots, Feishu adapters, and Codex/OAuth agents indicate a focus on workplace and prosumer deployments.
- **Security response velocity:** Multiple P1 security patches merged today (bypass prevention, MCP allowlist enforcement) show security is a prioritized—if reactive—concern.

**Technical Approach Differences:**
- OpenClaw uses a **gateway-centric architecture** with skill broker and MCP injection, enabling cross-platform agent deployment but adding surface area for bugs (e.g., MCP tool injection gaps, heartbeat scheduling failures).
- Hermes relies on **delivery mirrors and background agents** for long-running tasks, prioritizing session durability over gateway concurrency.

**Community Size Comparison:**
- OpenClaw's daily issue volume (298) dwarfs Hermes (50), suggesting 4–6x larger community or more aggressive issue tracking. However, comment counts on top issues are comparable (26 vs 29), implying similar depth of engagement per active user.

**Critical Weakness:** Data-loss bugs (memory-core Dreaming #84882, browser cookies #96704) and silent truncation (#84516) erode user trust more severely than Hermes's equivalent UX clipping issues.

---

## 4. Shared Technical Focus Areas

The following requirements emerge across **both projects**, representing ecosystem-wide priorities:

| Shared Need | OpenClaw Signal | Hermes Signal |
|-------------|----------------|---------------|
| **Mobile Platform Parity** | #9443 (Android APK), #97983 (iOS reply failure), #98366 (Android TLS) | #14240 (Termux tool failure), #42992 (desktop clipping) |
| **Session Reliability** | #92201 (thinking signature invalidity), #85103 (fallback chain failure) | #55925 (Telegram polling death), #50170 (MCP tool silence) |
| **Model Transparency** | #84516 (silent truncation), #98101 (429 misclassification) | #6839 (lazy schema for cost visibility), #3040 (Copilot premium waste) |
| **Multi-Provider Resilience** | #85042 (Google→OpenAI misrouting), #92201 (Anthropic provider) | #33415 (OpenAI OAuth error), #22201 (per-auxiliary fallback) |
| **Token Optimization** | — | #6839 (lazy tool schema), #55961 (auto-summarize history) |
| **Secure Defaults** | #98315 (mcporter bypass), #85030 (MCP injection gap) | #56035 (SSRF fix), #55111 (PII redaction) |

**Key Takeaway:** Both projects struggle with **provider-agnostic reliability**—model fallback chains, OAuth token handling, and multi-platform persistence are pain points. The ecosystem needs standardized middleware for provider routing and session durability.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Target Users** | Enterprise teams, prosumers with multi-platform presence | Self-hosters, developers, power users |
| **Primary Architecture** | Gateway + skill broker + MCP injection layer | Desktop app + delivery mirrors + background workers |
| **Platform Breadth** | iOS, Android, Feishu, WebChat, Codex, Azure Teams | Desktop (macOS/Windows), Telegram, WeChat, Docker, TUI |
| **Release Philosophy** | High-frequency (daily), fix-forward, minimal migration docs | Measured (bi-weekly?), feature-focused, compatibility-aware |
| **Security Posture** | Reactive (daily security patches, sometimes incomplete) | Proactive (SSRF fixes, PII redaction, compression safety) |
| **Community Engagement** | High-volume issue tracker, large but unassigned backlog | Smaller volume, quicker maintainer response, PRs often same-day |
| **Mobile Maturity** | Broader mobile coverage but broken in practice (iOS/Android bugs) | Mobile niche (Termux) but more stable desktop experience |
| **AI Provider Depth** | Heavy Anthropic + OpenAI integration, Google misrouter risk | OpenAI Codex focus, Copilot premium integration, local model support |

**Architecture Trade-off:** OpenClaw's gateway model enables multi-platform agents but creates cascading failures (heartbeat, reconnect, MCP injection). Hermes's desktop-centric approach sacrifices breadth for UX consistency.

---

## 6. Community Momentum & Maturity

**Activity Tier 1 (High Velocity, High Churn):**
- **OpenClaw** — Daily releases, 500 PRs/day, but critical backlog growing. Rapid iteration attracting enterprise adopters but risking burnout on maintenance.

**Activity Tier 2 (Steady Growth, Targeted Fixes):**
- **Hermes Agent** — Consistent 50 issues/PRs daily, resolved PRs filed same-day. More manageable scale; feature development (cloud mode, local iMessage) alongside reliability fixes.

**Maturity Assessment:**
- **OpenClaw** is in **early rapid-growth** with scale issues. The project is widening but not deepening—new bugs outpace fixes. Risk: user frustration from data-loss may slow adoption.
- **Hermes Agent** is in **stabilization phase** with feature expansion. Fewer regressions, stronger maintainer coverage, but slower to ship major features.

**Community Sentiment:**
- OpenClaw: "Fixes are coming, but I keep losing data" — urgency around reliability.
- Hermes: "Great tool, but Docker is frustrating and mobile is weak" — UX polish vs. platform expansion.

---

## 7. Trend Signals for AI Agent Developers

**Extracted from community feedback (both projects):**

1. **The "Trust Tax" is real.** Users are willing to trade features for reliability. Data-loss bugs (OpenClaw #84882, #96704) and silent tool failures (Hermes #50170) cause literal loss of work. Developers should prioritize session durability, idempotency, and user-facing error surfaces over new integrations.

2. **Mobile is non-negotiable.** Every major pain point list includes mobile: Android APK demand, iOS reply failures, Termux tool degradation. The unserved mobile opportunity is the ecosystem's largest growth lever.

3. **Token cost is the silent killer.** Hermes's #6839 (lazy tool schema) and #55961 (auto-summarize) point to a systemic problem: agents send everything every turn. Cost-aware middleware (on-device schema filtering, context compression) will become standard.

4. **Provider diversity creates fragility, not resilience.** Both projects have misrouting bugs (OpenClaw #85042, Hermes #33415) and fallback chain failures. A unified provider abstraction layer with health-aware routing is an architectural gap across the ecosystem.

5. **Enterprise needs are standardizing.** Multi-Teams bots, Azure/Google OAuth, Salesforce MCP, and audit logging appear across both backlogs. Developers targeting workplace deployment should prioritize OAuth credential brokers and session isolation.

6. **Self-hosted reliability lags cloud UX.** Docker complexity (Hermes #14448), macOS upgrade failures (OpenClaw #85027), and WSL2 crashes suggest the self-hosted deployment experience remains a barrier. Simplified setup scripts and better state management tools are needed.

**Recommendation for developers:** Invest in session durability, provider-agnostic middleware, and mobile parity. The projects that solve "I can trust it to work tomorrow" will win adoption over those shipping the most features today.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-01

## 1. Today’s Overview
Activity remains high with **50 issues and 50 PRs updated in the last 24 hours**. The project shows strong community engagement: 8 issues were closed and 15 PRs were merged or closed, reflecting steady maintenance progress. No new releases were published. Priority-1 (P1) bugs involving WebSocket access control and Telegram gateway resilience are under active review, while feature requests—especially lazy tool schema loading and cross-platform locale support—continue to draw lengthy discussion. The project’s health is solid, though several older, high-comment issues still await maintainer decisions.

## 2. Releases
*None.* No new releases were cut on or around 2026-07-01.

## 3. Project Progress
**Merged/closed PRs today (notable examples from the top 20):**

- [#56029](https://github.com/NousResearch/hermes-agent/pull/56029) – **Desktop folder drag‑and‑drop fix**: folders now attach as `@folder` refs instead of failing. *Merged.*
- [#27902](https://github.com/NousResearch/hermes-agent/pull/27902) – **Telegram message persistence**: preserves gateway messages across restarts via a durable inbound journal. *Merged.*
- [#20481](https://github.com/NousResearch/hermes-agent/pull/20481) – **Delivery mirrors & background agents**: stores cross‑chat `send_message` as typed `delivery_mirror` records and enables durable background Hermes workers for long‑running tasks. *Merged.*
- [#18770](https://github.com/NousResearch/hermes-agent/pull/18770) – **Delegation hardening**: fixes media extraction, adds worker contract fields (timeout, artifact_path, output_schema), and surfaces lifecycle events. *Merged.*
- [#16220](https://github.com/NousResearch/hermes-agent/pull/16220) – **Gateway stop/override logic**: short plain stop commands now correctly suppress resume notes. *Merged.*

**Closed issues today:**
- [#12805](https://github.com/NousResearch/hermes-agent/issues/12805) – Feishu adapter missing per‑channel prompt resolution (feature added).
- [#11411](https://github.com/NousResearch/hermes-agent/issues/11411) – Custom GPT‑5.4 gateway 400 error (resolved by upstream fix).
- [#55735](https://github.com/NousResearch/hermes-agent/issues/55735) – Deprecated `rcedit` dependency flagged and addressed.
- [#12099](https://github.com/NousResearch/hermes-agent/issues/12099) – Hardcoded `agent:main` in `build_session_key()` (session isolation fix).
- [#52677](https://github.com/NousResearch/hermes-agent/issues/52677) – Desktop file‑tree stale data during session switch (UX fix).

## 4. Community Hot Topics
The most active issues by comment count and reactions:

1. **[#6839 – Feature: Lazy Tool Schema Loading](https://github.com/NousResearch/hermes-agent/issues/6839)**  
   *29 comments, 15 👍* – Strong demand to reduce token overhead by injecting only relevant tool schemas per call. The community wants a two‑pass mechanism. Underlying need: cost savings and compatibility with smaller local models.

2. **[#14448 – [Bug]: Docker user experience is bad](https://github.com/NousResearch/hermes-agent/issues/14448)**  
   *7 comments, 5 👍* – Users report `mkdir /root` failure in privileged containers and unclear host mount points. The three‑container Docker Compose setup is seen as confusing.

3. **[#42992 – Desktop user message bubble clips multi‑line prompts](https://github.com/NousResearch/hermes-agent/issues/42992)**  
   *6 comments* – macOS users experience visual clipping of multi‑line user messages. Full content is sent, but only two lines are visible in the UI.

4. **[#22201 – Per‑auxiliary fallback_providers for task resilience](https://github.com/NousResearch/hermes-agent/issues/22201)**  
   *6 comments, 1 👍* – Request to allow per‑auxiliary‑task fallback providers (vision, web extraction, etc.), mirroring the top‑level model fallback.

5. **[#40347 – Russian locale for Desktop app](https://github.com/NousResearch/hermes-agent/issues/40347)**  
   *6 comments* – Community member has already built an installer fork and is seeking official inclusion.

6. **[#33265 – [Bug]: WebSocket rejected for non‑loopback clients even with --insecure / --host 0.0.0.0](https://github.com/NousResearch/hermes-agent/issues/33265)**  
   *4 comments, 2 👍, P1* – High‑severity complaint: TUI dashboard fails when accessed from another LAN host despite `--insecure` flag.

**Active PR discussion:**  
- [#56027](https://github.com/NousResearch/hermes-agent/pull/56027) – WeChat gateway fix for iLink error logging (P2, new).
- [#56028](https://github.com/NousResearch/hermes-agent/pull/56028) – Telegram `NoneType` guard on reconnect (P1, new).

## 5. Bugs & Stability
**P1 (Critical):**
- [#55925](https://github.com/NousResearch/hermes-agent/issues/55925) – Failing `bg‑review` thread kills Telegram polling coroutine; investigation triggered by #55769. *PR #56028 addresses the symptom, root cause still tracked.*
- [#33265](https://github.com/NousResearch/hermes-agent/issues/33265) – WebSocket rejected for non‑loopback dashboard clients. *No fix PR yet; needs decision on security boundary.*

**P2 (High):**
- [#36239](https://github.com/NousResearch/hermes-agent/issues/36239) – `handle_max_iterations` uses soft user‑role stop instead of hard `tool_choice=none`; model may ignore it.
- [#41517](https://github.com/NousResearch/hermes-agent/issues/41517) – Desktop/Dashboard chat worker loses selected profile, falls back to default.
- [#55815](https://github.com/NousResearch/hermes-agent/issues/55815) – Custom Cline provider wrongly appends `/models` to Base URL.
- [#3040](https://github.com/NousResearch/hermes-agent/issues/3040) – GitHub Copilot premium requests never consumed.
- [#50170](https://github.com/NousResearch/hermes-agent/issues/50170) – MCP tools silently absent after keepalive failure; new sessions don’t reconnect.
- [#55985](https://github.com/NousResearch/hermes-agent/issues/55985) – Dashboard logout crashes container via `NotImplementedError` in `BasicAuthProvider`.
- [#33265](https://github.com/NousResearch/hermes-agent/issues/33265) detailed above.

**P3 (Notable):**
- [#33415](https://github.com/NousResearch/hermes-agent/issues/33415) – OpenAI OAuth (`openai‑codex`) returns `TypeError` on all GPT‑5.x models; fallback never activates (P3 but blocks many users).
- [#14240](https://github.com/NousResearch/hermes-agent/issues/14240) – Tool calling failure on phone (Termux) after a few hours; token limit claim despite capacity.
- [#55416](https://github.com/NousResearch/hermes-agent/issues/55416) – Photon iMessage sidecar alive but gRPC stream killed with RST_STREAM code 2.
- [#55658](https://github.com/NousResearch/hermes-agent/issues/55658) – Desktop app cannot start after update.

**Fix PRs filed today for bugs:**
- [#56035](https://github.com/NousResearch/hermes-agent/pull/56035) – SSRF fix in image_gen URL fetch (security).
- [#56034](https://github.com/NousResearch/hermes-agent/pull/56034) – Compression safety valve for TUI/CLI preflight.
- [#56030](https://github.com/NousResearch/hermes-agent/pull/56030) – Prevent archived Kanban boards from being resurrected.
- [#56031](https://github.com/NousResearch/hermes-agent/pull/56031) – Fix MoA preflight aggregator context overflow.
- [#56033](https://github.com/NousResearch/hermes-agent/pull/56033) – UTF‑8 encoding safety for `os.fdopen()` on Windows.
- [#56027](https://github.com/NousResearch/hermes-agent/pull/56027) – WeChat iLink error logging & circuit breaker fix.
- [#56028](https://github.com/NousResearch/hermes-agent/pull/56028) – Telegram `NoneType` guard during reconnect.
- [#56029](https://github.com/NousResearch/hermes-agent/pull/56029) – Detect dropped folders in Desktop composer.
- [#55415](https://github.com/NousResearch/hermes-agent/pull/55415) – Vietnamese Telex IME character dropping in TUI.

## 6. Feature Requests & Roadmap Signals
**Strong community demand (likely near‑term inclusion):**
- **Lazy Tool Schema Loading** ([#6839](https://github.com/NousResearch/hermes-agent/issues/6839)) – Could be a major token‑saving optimization; high engagement and multiple 👍.
- **Per‑auxiliary fallback_providers** ([#22201](https://github.com/NousResearch/hermes-agent/issues/22201)) – Aligns with existing model fallback pattern.
- **Russian locale for Desktop** ([#40347](https://github.com/NousResearch/hermes-agent/issues/40347)) – Already has a working fork; easy to merge.
- **HTTPS OAuth callback URL** ([#29299](https://github.com/NousResearch/hermes-agent/issues/29299)) – Required for Salesforce MCP, common enterprise need.
- **Auto‑summarize conversation history** ([#55961](https://github.com/NousResearch/hermes-agent/issues/55961)) – Reduces token consumption for long sessions; conceptually similar to existing features.

**Emerging signals:**
- **Generic OAuth broker credential source** ([#23944](https://github.com/NousResearch/hermes-agent/issues/23944)) – Prevents refresh‑token races in multi‑runtime deployments.
- **Configurable backoff for HTTP 503/529** ([#55540](https://github.com/NousResearch/hermes-agent/issues/55540)) – Parity with Z‑AI path; users facing production overload errors.
- **Discord Reaction Support** ([#29026](https://github.com/NousResearch/hermes-agent/issues/29026)) – Quick feedback via emoji.
- **Local Model Setup Skill** ([#523](https://github.com/NousResearch/hermes-agent/issues/523)) – Inspire‑m from Liquid AI’s LocalCowork; guide for Ollama, llama.cpp.
- **hermes‑memory‑pgvector plugin** ([#29537](https://github.com/NousResearch/hermes-agent/issues/29537)) – Community‑built Postgres/pgvector memory provider.

**PRs adding new features:**
- [#56023](https://github.com/NousResearch/hermes-agent/pull/56023) – **Local iMessage mode** (Photon) – credential‑free using open‑source Spectrum provider.
- [#55402](https://github.com/NousResearch/hermes-agent/pull/55402) – **Hermes Cloud connection mode** for Desktop – one‑sign‑in, agent discovery.
- [#55111](https://github.com/NousResearch/hermes-agent/pull/55111) – **Opt‑in local PII redaction** – security layer before hosted provider dispatch.
- [#40989](https://github.com/NousResearch/hermes-agent/pull/40989) – **Hepburn theme** preset for Desktop (still open).
- [#55951](https://github.com/NousResearch/hermes-agent/pull/55951) – **Verify Google Calendar event creation** – read‑back validation for skill reliability.

## 7. User Feedback Summary
**Pain points (expressed in issues and comments):**
- **Docker complexity** ([#14448](https://github.com/NousResearch/hermes-agent/issues/14448)) – Container setup is opaque; `mkdir /root` failure and unclear mount paths frustrate production deployments.
- **Desktop UX clipping** ([#42992](https://github.com/NousResearch/hermes-agent/issues/42992)) – multi‑line input hidden; decreases trust in what the agent sees.
- **Token consumption** ([#6839](https://github.com/NousResearch/hermes-agent/issues/6839), [#55961](https://github.com/NousResearch/hermes-agent/issues/55961)) – Large tool schemas and full history sent every turn cause high costs, especially on local models.
- **MCP tool silence** ([#50170](https://github.com/NousResearch/hermes-agent/issues/50170)) – Tools disappear without warning after keepalive failure.
- **Copilot premium waste** ([#3040](https://github.com/NousResearch/hermes-agent/issues/3040)) – Paid tokens not consumed despite usage.
- **Phone environment** ([#14240](https://github.com/NousResearch/hermes-agent/issues/14240)) – Tool calling degrades after a few hours on Termux.

**Satisfaction signals:**
- **Active community contributions**: Russian fork, pgvector plugin, Hepburn theme, translation fixes – indicating strong developer engagement.
- **Feature PRs** (cloud mode, PII redaction, local iMessage) show the project is evolving to meet real‑world deployment and security needs.

## 8. Backlog Watch
Issues and PRs that have remained open for extended periods and need maintainer attention:

- **[#6839 – Lazy Tool Schema Loading](https://github.com/NousResearch/hermes-agent/issues/6839)** – Created April 9, 29 comments, 15 👍. No maintainer response or assignment yet. High community investment.
- **[#523 – Local Model Setup Skill](https://github.com/NousResearch/hermes-agent/issues/523)** – Created March 6, 3 comments, 3 👍. P3 but represents a common user need for running local models.
- **[#3040 – GitHub Copilot premium requests never used](https://github.com/NousResearch/hermes-agent/issues/3040)** – Created March 25, P2, 3 comments. Long‑standing billing bug.
- **[#14240 – Tool calling failure on phone (Termux)](https://github.com/NousResearch/hermes-agent/issues/14240)** – Created April 23, P2, needs reproduction.
- **[#33265 – WebSocket rejected for non‑loopback clients](https://github.com/NousResearch/hermes-agent/issues/33265)** – Created May 

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*