# OpenClaw Ecosystem Digest 2026-07-22

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-22 02:12 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-07-22

## 1. Today's Overview

OpenClaw is operating at extremely high activity levels: **500 issues and 500 PRs were updated in the last 24 hours**. Of these, 396 issues remain open/active, 104 were closed; 336 PRs are open, 164 were merged or closed. **No new releases** were published today. The community continues to focus on security improvements (masked secrets, capability-based permissions), bug fixes for session state corruption and provider compatibility, and a wave of localization and UI enhancements. Several P0/P1 regressions remain unresolved, indicating that stability is the top priority for maintainers.

## 2. Releases

**None.** No new versions were released in the reporting period.

## 3. Project Progress

Notable PRs merged or closed today (selected from top-comment PRs):

- **#112417** – `feat(ui): add text search/filter to model picker` (closed). Adds a real-time search input to the Control UI model picker to filter models by name, label, or provider.  
- **#102228** – `Install ClawHub packages for new Claw agents` (closed). Introduces exact artifact resolution, trust decisions, and package lifecycle handling for ClawHub packages.  
- **#110739** – `fix(agents): cap sessions_list tool limit before gateway dispatch` (closed). Prevents pathological `limit` values from causing gateway issues.  
- **#91383** – `Telegram normal reply can start mid-URL / lose opening text when message begins with Markdown links` (closed). Fixes a parsing regression in Telegram reply streaming.

Several localization-related PRs remain open (e.g., #111542, #111544, #112441), indicating ongoing work to internationalize the TUI and native apps.

## 4. Community Hot Topics

Issues with the highest engagement (comments + reactions):

- **#10659** – [Feature Request: Masked Secrets – Prevent Agent from Accessing Raw API Keys](openclaw/openclaw Issue #10659)  
  *15 comments, 4 👍* – Strong demand for a system that allows agents to *use* API keys without *seeing* them to prevent prompt injection and accidental leaks.  
- **#85030** – [Bug: MCP tools not injected into subagent (sessions_spawn) sessions](openclaw/openclaw Issue #85030)  
  *11 comments, 5 👍* – MCP tool schemas are not passed to spawned subagents, breaking documented use cases; users are asking for an urgent fix.  
- **#101290** – [CLI startup preflight corrupts live state DB while gateway running – P0 regression](openclaw/openclaw Issue #101290)  
  *13 comments* – Critical database corruption bug on macOS; vanilla SQLite control does not reproduce.  
- **#20786** – [Feature: Telegram Business Bot support](openclaw/openclaw Issue #20786)  
  *9 comments, 6 👍* – Users want to receive business messages and handle business connections in Telegram.  
- **#84527** – [Feature: Add Antigravity CLI (agy) as CLI backend to replace deprecated google-gemini-cli](openclaw/openclaw Issue #84527)  
  *5 comments, 11 👍* – High demand for migration to the new Google CLI backend before the June 18 deadline.

**Underlying needs**: Security (secret isolation, MCP tool boundaries), stability (database integrity), platform compatibility (new CLI backends, Telegram business features).

## 5. Bugs & Stability

Active P0/P1 bugs reported or updated in the last 24 hours (ranked by severity):

| Issue | Severity | Summary | Fix PR? |
|-------|----------|---------|---------|
| #101290 | **P0** | Database corruption on macOS while gateway running (SQLite malformed) – regression | None identified |
| #86996 | **P1** | Active Memory + Codex path causes long latency, hook timeouts, gateway event-loop stalls | None |
| #85030 | **P1** | MCP tools not injected into spawned subagent sessions | None |
| #106779 | **P1** | llama.cpp provider fails with 400 on OpenClaw 2026.7.1 | None |
| #53408 | **P1** | Write/exec tool parameters silently dropped after long conversations | None |
| #90840 | **P1** | Subagent raw output delivered to chat instead of parent summary – regression | None |
| #95441 | **P1** | GitHub Copilot gpt-5.5 persists encrypted content after fixes | None |
| #111498 | **P1** | Main agent blocked by persistent workspace-state migration after Anthropic auth recovery | None |
| #108473 | **P1** | `cron` tool schema breaks llama.cpp tool-calling (unanchored regex pattern) | None |
| #95612 | **P1** | cli-backend agent against Anthropic returns 401 while shell works | None |
| #88562 | **P1** | models.json generator writes apiKey as plain string instead of secret-ref – security | None |

**Observations**: Most high-severity bugs are not linked to any open fix PR. Database corruption (#101290) and MCP subagent injection (#85030) are particularly impactful. Several relate to subagent and tool interaction patterns, suggesting a systemic issue in the session/agent lifecycle.

## 6. Feature Requests & Roadmap Signals

High-priority enhancement requests that may appear in the next release (based on priority label, comment count, and thumbs-up):

- **#10659** – Masked Secrets (P1, 4 👍) – Likely candidate due to security focus.
- **#16670** – Onboarding Wizard should include Memory/Embedding setup (P2, 1 👍) – Low complexity, high impact for new users.
- **#13751** – Feishu plugin: remove dependency on contact directory permission (P1, 2 👍) – Privacy/security improvement.
- **#7722** – Filesystem Sandboxing Config (P2, 4 👍) – Long-standing request for access control.
- **#13219** – Per-model usage logging for cost tracking (P2, 1 👍) – Operational need.
- **#12678** – Capability-based permissions for skills/tools (P2) – Aligns with security roadmap.

**Prediction**: The next minor version (2026.7.x) will likely ship Masked Secrets (#10659) and the onboarding wizard fix (#16670), as both have been open for months and have clear implementation paths. Localization (PRs #111542, #111544) is also a strong candidate.

## 7. User Feedback Summary

Recurring pain points expressed across issues and PRs:

- **Database reliability**: Users on macOS experienced repeated SQLite corruption, erasing session history (#101290).
- **Tool injection gaps**: MCP tools and custom tool schemas do not propagate to subagents, breaking complex workflows (#85030, #15032).
- **Slow or hung sessions**: Active Memory and certain model combinations cause timeouts and unresponsive gateways (#86996).
- **Parameter drops**: After long conversations, tool parameters are silently lost (#53408).
- **Onboarding friction**: New users miss memory configuration, leading to non-persistent bots (#16670).
- **Localization gaps**: TUI and CLI outputs remain English-only; contributors are actively submitting translations (PRs #111542, #111544).

Satisfaction: Users appreciate the rapid development pace and the community’s responsiveness, but frustration is high over persistent regressions and missing security features.

## 8. Backlog Watch

Issues and PRs that remain open for extended periods and require maintainer attention:

| Item | Created | Comments | Status |
|------|---------|----------|--------|
| #7722 – Filesystem Sandboxing | 2026-02-03 | 10 comments | P2, needs product decision |
| #8299 – Config option to suppress sub-agent announce | 2026-02-03 | 8 comments | P2, needs maintainer review |
| #13364 – Expose before_tool_call/after_tool_call hooks | 2026-02-10 | 7 comments | P2, needs security review |
| #13751 – Feishu permission reduction | 2026-02-11 | 7 comments | P1, needs security review |
| #12678 – Capability-based permissions | 2026-02-09 | 6 comments | P2, needs security review |
| #14785 – Reduce tool schema token overhead | 2026-02-12 | 9 comments | P2, needs product decision |
| PR #100146 – sessions_yield diagnostic emission | 2026-07-05 | 0 comments | Ready for maintainer look |
| PR #95887 – Container update guidance | 2026-06-22 | 0 comments | Ready for maintainer look |

These items have been open for over a month (some since February) with clear value but no movement. The `needs-product-decision` and `needs-maintainer-review` labels indicate they are awaiting prioritization from the core team. Addressing them would significantly improve security posture and developer experience.

---

*Data sourced from GitHub OpenClaw repository as of 2026-07-22 00:00 UTC. Top‑comment items only; full dataset unavailable.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## 1. Ecosystem Overview

The personal AI agent open-source landscape is bifurcating into two distinct but interdependent tracks: **core infrastructure platforms** (exemplified by OpenClaw) that provide the runtime, tooling, and session orchestration layer, and **derivative/verticalized agents** (exemplified by Hermes Agent) that build opinionated user experiences on top of those foundations. Both projects are under very active development, but their activity patterns reveal different maturity stages. OpenClaw is experiencing a wave of security-conscious feature requests and stability regression management at massive scale (500+ issues/PRs per day), while Hermes Agent is consolidating around plugin extensibility and platform-specific rendering fixes at a smaller scale (50 issues/PRs per day). The common thread across both ecosystems is a pressing need for **session state integrity, tool permission boundaries, and memory configuration control** — suggesting the community is transitioning from "can it work?" to "can it be trusted and controlled?"

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|-------------|
| **24h Issue Updates** | 500 (396 open, 104 closed) | 50 (46 open, 4 closed) |
| **24h PR Updates** | 500 (336 open, 164 merged/closed) | 50 (46 open, 4 merged/closed) |
| **New Releases (24h)** | None | None |
| **P0/P1 Bugs (active)** | 10+ | 2 (P1) |
| **Community Engagement** | Very high (15+ comments on top issues) | Moderate (5-13 comments on top issues) |
| **Feature Request Velocity** | High (5+ high-priority open) | Moderate (3 high-priority open) |
| **Health Score** | 6/10 — High activity, but many regressions and unresolved P0/P1 bugs | 7/10 — Smaller scope, faster bug closure, but critical deadlock and crash issues |

**Health score rationale:** OpenClaw’s raw activity volume is impressive, but the ratio of open to closed items (396/500 issues) and the presence of a P0 database corruption bug (#101290) with no fix PR indicate stability challenges. Hermes Agent has a smaller surface area but suffers from a worker deadlock (#68915) and a desktop crash (#65868) that directly impact production use cases.

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Scale and ecosystem gravity:** 10x the issue/PR volume of Hermes Agent indicates a larger community, more contributors, and faster feature iteration
- **Security-first roadmap:** Masked Secrets (#10659), capability-based permissions (#12678), and secret-ref adherence (#88562) signal a deliberate investment in enterprise-grade security — Hermes has no equivalent proposal
- **Localization maturity:** Multiple active translation PRs (Spanish, Brazilian Portuguese) — Hermes has none visible
- **Platform diversity:** Telegram Business bot support (#20786), multiple MCP integrations, sandboxing (#7722)

**Technical approach differences:**
- OpenClaw uses a **centralized gateway + session lifecycle model** with SQLite state persistence (vulnerable to corruption per #101290)
- Hermes Agent opts for a **desktop-first architecture** (Rust→V8 IPC bridge) with TUI/CLI surfaces and plugin SDK experimentation
- OpenClaw focuses on **LLM provider compatibility** (llama.cpp, Google Gemini CLI, Anthropic); Hermes shows more interest in **platform integration** (TouchDesigner, Cloudflare, X Chat)

**Community size comparison:**
- OpenClaw: ~500 daily updates, 396 open issues, 336 open PRs — likely 1,000+ active contributors
- Hermes Agent: ~50 daily updates, 46 open issues, 46 open PRs — likely 100-200 active contributors
- OpenClaw enjoys a **roughly 10:1 community size advantage** across all activity metrics

## 4. Shared Technical Focus Areas

Both projects are converging on the same set of pain points, indicating ecosystem-wide requirements:

| Requirement | OpenClaw | Hermes Agent |
|-------------|----------|-------------|
| **Masked/sealed secrets** | #10659 (P1, 4👍) | No equivalent — gap |
| **Protected/immutable skills** | Capability-based permissions (#12678) | #25083 (7 comments, needs decision) |
| **Session state reliability** | #101290 (P0 DB corruption) | #68920 (lease leaks), #68979 (message re-stacking) |
| **Tool/subagent propagation** | #85030 (MCP not injected into subagents) | #27683 (web tools missing plugin init) |
| **Cross-platform rendering** | Localization PRs (#111542, #111544) | #38786 (Windows images), #68990 (Thai marks) |
| **Plugin/tool extensibility** | Filesystem sandboxing (#7722) | #64900 (plugin send_message), #68964 (per-function filtering) |

**Key gap in Hermes Agent:** No visible equivalent to OpenClaw's masked secrets or capability-based permissions. This suggests Hermes Agent may need to either adopt OpenClaw's security model or develop its own to serve enterprise users.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|-------------|
| **Target user** | Power users, developers, enterprise teams | Tinkerers, desktop users, plugin developers |
| **Primary surface** | CLI + TUI + gateway API | Desktop app (Rust/V8) + TUI + mobile ambitions |
| **Memory model** | Hardcoded MEMORY.md (controversial — #47349 request to rename) | Also hardcoded MEMORY.md (#47349 filed against Hermes too) |
| **Plugin approach** | Built-in tools + ClawHub packages | Plugin SDK (#64900) + TUI widget SDK (#68306) |
| **Security posture** | Proactive (masked secrets, sandboxing, capability permissions) | Reactive (no visible security features beyond smart-approval #68701) |
| **LLM provider support** | Expansive (llama.cpp, Gemini CLI, Anthropic, Copilot) | Limited (OpenRouter, Anthropic — no llama.cpp issues reported) |
| **Risk profile** | Regression-heavy due to scale (P0 DB corruption, MCP injection gaps) | Edge-case unstable (worker deadlocks, desktop crashes, process orphans) |

**Strategic positioning:** OpenClaw is building a **general-purpose agent operating system** with security, localization, and enterprise readiness as key differentiators. Hermes Agent is building a **plugin-friendly agent desktop experience** with platform diversity and UI customization as its moat. They are not direct competitors — Hermes could potentially become a desktop frontend to OpenClaw's backend.

## 6. Community Momentum & Maturity

**Activity Tiers:**

| Tier | Project | Characteristics |
|------|---------|-----------------|
| **1 — Hyper-growth** | OpenClaw | 500 daily updates, but bug closure rate lags (396/500 open). Community is pushing security/features faster than maintainers can stabilize. |
| **2 — Active consolidation** | Hermes Agent | 50 daily updates, faster bug closure (4/50 closed). Team appears to be stabilizing v0.19 before next major release. |

**Iteration speed:**
- **OpenClaw:** Rapid feature delivery (model picker search, ClawHub packages, localization) but at the cost of regressions. The P0 database corruption bug suggests testing gaps in core infrastructure.
- **Hermes Agent:** Slower feature velocity but more targeted fixes. The team is prioritizing CI stability (PR #68896), widget-grid hardening (#68999), and plugin SDKs — suggesting a "build the foundation right" philosophy.

**Maturity assessment:**
- OpenClaw is **mid-maturity** — the product vision is clear and broad, but operational stability is not yet production-grade
- Hermes Agent is **early-maturity** — stable for simple use cases, but critical bugs (deadlocks, desktop crashes) block production adoption for complex workflows

## 7. Trend Signals

For AI agent developers, the following industry trends emerge from today's data:

1. **Security is the new feature frontier** — Both communities are demanding masked secrets, immutable skills, and capability-based permissions. Expect this to become table stakes for any serious agent platform within 3-6 months. Developers building on top of these frameworks should architect for secret isolation from day one.

2. **Session state management is the new "database" problem** — Database corruption, lease leaks, message re-stacking, and tool parameter drops reveal that persistent agent state is poorly handled. This mirrors early relational database maturity. Expect specialized agent state stores (not just SQLite) to emerge as a market.

3. **Platform diversity is accelerating** — Telegram business bots, X Chat, TouchDesigner, Cloudflare, and mobile targets indicate agents are moving beyond CLI/chat into embedded and verticalized experiences. Developers should invest in platform-agnostic tool abstractions (MCP-like) rather than single-platform integrations.

4. **Configuration granularity is a UX crisis** — Users do not want hardcoded memory files, fixed tool schemas, or opaque secret handling. The demand for per-session, per-tool, per-model configuration signals that "one-size-fits-all" agents are failing. Expect config-as-code or UI-based policy editors to become differentiators.

5. **Stability is being rediscovered** — The volume of unanswered P0/P1 bugs (OpenClaw's database corruption, Hermes' worker deadlock) suggests that both projects prioritized feature velocity over reliability. As adoption scales, regression prevention and crash recovery will become the #1 investment area — especially for enterprise procurement.

6. **Plugin SDKs will define platform lock-in** — Hermes' TUI widget SDK (#68306) and cross-surface theme SDK (#68857) signal a bet on ecosystem extensibility. OpenClaw's ClawHub packages serve a similar purpose. The winner will likely be the one that makes plugin development easiest while maintaining security boundaries.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-22

## 1. Today's Overview
Hermes Agent maintained a high activity level over the last 24 hours, with 50 issues and 50 PRs receiving updates. Of these, 4 issues were closed (3 bug fixes, 1 duplicate) and 4 PRs were merged or closed (2 test/CI fixes, 1 TUI hardening, 1 Kanban fix). No new releases were cut, indicating the team is consolidating for a future release. The community is actively filing feature requests and reporting bugs, particularly around session state leaks, plugin extensibility, and platform-specific tooling.

## 2. Releases
**None.** No new releases were published in the last 24 hours. The latest known release remains v0.19.x (referenced in issues #68858, #65868).

## 3. Project Progress
Only a few PRs were merged/closed today, but they address important stability and CI issues:

- **#68896 (closed)** – [fix(tests): anchor MCP breaker opened_at to monotonic now](https://github.com/NousResearch/hermes-agent/pull/68896) – Kills a CI-only flake in MCP circuit-breaker tests.
- **#68999 (closed)** – [fix(ui-tui): widget-grid hardening — review fast-follow for #20379](https://github.com/NousResearch/hermes-agent/pull/68999) – Hardens MCP revision handshake, grid layout locking, and pan mutex safety after a deep review of the new widget-grid system.
- Three closed bugs were also fixed on main:
  - **#27683** – [web_tools.py missing plugin discovery](https://github.com/NousResearch/hermes-agent/issues/27683) – Web search/extract/crawl now works out of the box.
  - **#38786** – [Image generation not displayed on Windows Desktop](https://github.com/NousResearch/hermes-agent/issues/38786) – Local image paths now render correctly in Hermes Desktop.
  - **#54675** – [Gateway token leakage in multiplexed profiles](https://github.com/NousResearch/hermes-agent/issues/54675) – Per-profile secret scoping fixed.

## 4. Community Hot Topics
The most active discussions highlight a desire for **greater configurability and safety**:

| Issue/PR | Comments | Summary |
|----------|----------|---------|
| [#47349 – Feature: Configurable Memory Backends](https://github.com/NousResearch/hermes-agent/issues/47349) | 13 | Rename `memory.md` to `rules.md` and allow disabling hardcoded memory files in favor of external backends (honcho, fact_store). |
| [#27683 – Web tools silent failure](https://github.com/NousResearch/hermes-agent/issues/27683) (closed) | 8 | Plugin init missing caused web tools to fail; now fixed. |
| [#25083 – Feature: Immutable/protected skills](https://github.com/NousResearch/hermes-agent/issues/25083) | 7 | Agents can currently modify any skill; request for a protected/skill-lock mechanism. |
| [#68915 – Worker deadlock on backgrounded server](https://github.com/NousResearch/hermes-agent/issues/68915) | 5 | P1 bug: agent deadlocks when LLM launches a long-lived process with `&`. |
| [#64900 – Plugin extensibility for send_message](https://github.com/NousResearch/hermes-agent/issues/64900) | 5 | Request to allow plugins to add platform-specific send fields/handlers without editing core code. |

The top-voted issue (#47349 with 1 👍) and #25083 both point to a community need for **explicit control over agent behavior** (memory sources, skill protection).  

## 5. Bugs & Stability
**Critical / P1:**
- **#68915 (open)** – [Worker deadlocks when agent backgrounds a server via `&`](https://github.com/NousResearch/hermes-agent/issues/68915) – No fix PR yet. Workaround not available. **High impact** for dev-server workflows.
- **#65868 (open)** – [Desktop v0.17.0 crashes in Rust→V8 IPC bridge (SIGTRAP)](https://github.com/NousResearch/hermes-agent/issues/65868) – Renderer crash-loop and main-process abort. No fix PR.

**High / P2:**
- **#68920 (open)** – [Desktop/TUI sessions leak active-session leases](https://github.com/NousResearch/hermes-agent/issues/68920) – `max_concurrent_sessions` blocks new sessions over time. No fix PR.
- **#68858 (open)** – [In-place compaction + FTS maintenance saturates disk I/O](https://github.com/NousResearch/hermes-agent/issues/68858) – Can wedge gateway shutdown on large state.db. No fix PR.
- **#69033 (open)** – [Local terminal orphans child processes on Windows](https://github.com/NousResearch/hermes-agent/issues/69033) – Missing process-group detachment. No fix PR.
- **#69008 (open)** – [OpenRouter deepseek-v4-flash tool continuation fails](https://github.com/NousResearch/hermes-agent/issues/69008) – `content[].thinking` must be passed back. No fix PR.
- **#68911 (open)** – [Gateway force-redacts standalone E.164 phone numbers](https://github.com/NousResearch/hermes-agent/issues/68911) – No trusted-profile opt-in. No fix PR.
- **#68944 (open)** – [`hermes mcp add` silently absorbs `--env` into args](https://github.com/NousResearch/hermes-agent/issues/68944) – No fix PR.

**Medium / P3 with fix PRs in progress:**
- **#69040 (open)** – [TUI candidate-inclusive display on warm/live (fix verified for #65919 fallout)](https://github.com/NousResearch/hermes-agent/pull/69040)
- **#68999 (merged)** – Widget-grid hardening (see Project Progress).

**Fixed today:**
- #27683, #38786, #54675 (all closed on main).

## 6. Feature Requests & Roadmap Signals
Community requests cluster around three themes:

1. **Pluggable memory & tools** – #47349 (configurable memory backends), #64900 (plugin send_message), #68964 (per-function tool filtering).
2. **UI/UX improvements** – #61042 (TUI `/compress` type-ahead), #68970 (searchable timezone dropdown), #69025 (settings search bar), #68951 (Atomic Hermes mobile target for send_message).
3. **Safety & governance** – #25083 (immutable skills), #68701 (inject network context into smart-approval guard).

New PRs suggest the next version may include:
- **X Chat (encrypted DMs) platform plugin** – [#68930 (open)](https://github.com/NousResearch/hermes-agent/pull/68930)
- **Cross-surface theme SDK** – [#68857 (open)](https://github.com/NousResearch/hermes-agent/pull/68857) (themes CLI, TUI, and desktop live)
- **TUI widget-app SDK** – [#68306 (open)](https://github.com/NousResearch/hermes-agent/pull/68306)
- **Cloudflare MCP catalog entry** – [#68044 (open)](https://github.com/NousResearch/hermes-agent/pull/68044)
- **TouchDesigner MCP + skill** – [#68607 (open)](https://github.com/NousResearch/hermes-agent/pull/68607)

These indicate a push toward **platform diversity** and **self-service theming/plugin SDKs**.

## 7. User Feedback Summary
From today’s issue activity, users are actively running Hermes in varied environments and hitting:

- **Frustration with mandatory memory files** (#47349) – "There is no way to opt out of MEMORY.md."
- **Process deadlocks in real workflows** (#68915) – "Worker becomes unrecoverable… whole session is lost."
- **Platform-specific rendering bugs** (#68990 – Thai marks, #38786 – Windows image blocking, #68937 – PDF links on macOS).
- **Configuration granularity complaints** (#68964, #25083) – "No way to protect critical skills".
- **Session state corruption** (#68979 – messages re-stacked at bottom) and **lease leaks** (#68920) causing total session lockout.

Overall sentiment: users are pushing the agent hard but encountering **stability edge cases** and **lack of opt-out configurability** for built-in behaviors. Satisfaction is evident from feature requests, but bug volume suggests the recent v0.19 release introduced regressions in session management and desktop rendering.

## 8. Backlog Watch
Several open issues from previous months have not seen maintainer response or resolution:

- **#23207 (May 10)** – [Question: how to use web search via Ollama (feature present in OpenClaw)](https://github.com/NousResearch/hermes-agent/issues/23207) – Only 3 comments, no maintainer reply.
- **#25083 (May 13)** – [Feature: Immutable/protected skills](https://github.com/NousResearch/hermes-agent/issues/25083) – 7 comments, tagged `needs-decision`. Awaiting maintainer decision.
- **#47349 (June 16)** – [Configurable Memory Backends](https://github.com/NousResearch/hermes-agent/issues/47349) – 13 comments, tagged `needs-decision`. No maintainer update since creation.

These are community-valued features that remain in limbo. If the project aims to reduce user friction, **#47349** and **#25083** should be prioritized for a Go/No-Go decision.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*