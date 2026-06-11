# OpenClaw Ecosystem Digest 2026-06-11

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-11 03:33 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

Okay, here is the structured project digest for OpenClaw, generated from the provided GitHub data for 2026-06-11.

---

## OpenClaw Project Digest — 2026-06-11

### 1. Today's Overview

The OpenClaw project is in a **high-activity state**, driven by the release of a major security-focused beta (`v2026.6.6-beta.1`) and intense community bug reporting and feature discussion. A very high volume of 469 open issues and 396 open pull requests indicates a massive backlog, with maintainers likely stretched thin. The community is actively raising critical bugs related to message leaks, session management, and security boundaries, while a significant number of feature requests suggest strong user demand for better configurability, cost controls, and platform support. The release indicates a primary focus on hardening security, which aligns with many of the top-voted and most-commented issues.

### 2. Releases

- **`v2026.6.6-beta.1`**: This is the sole release in the last 24 hours.
    - **Summary**: A **major security-focused release** that significantly tightens security boundaries across numerous subsystems.
    - **Details**: The release notes highlight boundary tightening for transcripts, sandbox binds, host environment inheritance, MCP stdio, Codex HTTP access, native search policy, elevated sender checks, deleted-agent ACP bypasses, loopback tools, Discord moderation, and Teams group access.
    - **Breaking Changes**: The notes explicitly call out "substantially tighter" security boundaries, which implies a high likelihood of breaking changes for users with custom configurations, plugins, or integrations relying on the previously permissive defaults.
    - **Migration Notes**: Users should carefully review their `sandbox`, `exec`, `web_fetch`, and channel-specific (Discord, Teams) configurations, as previously allowed behaviors may now be blocked. The release is a beta, suggesting it is intended for testing before a stable release.

### 3. Project Progress

In the last 24 hours, 104 PRs were merged or closed. Key areas of advancement include:

- **Agent & Session Reliability**:
    - PR #90128 (closed): Fixes a critical bug where a manual `/model` override was silently dropped during session rollover.
    - PR #91921 (open): Aims to fix background execution completion, ensuring the agent receives a proper `[OpenClaw exec completion]` notification instead of a confusing `[heartbeat poll]`.
    - PR #91985 (open): Fixes a heartbeat bug where inferred commitments were marked as sent even when delivery was suppressed, causing them to disappear silently.
- **Platform & Provider Support**:
    - PR #84938 (closed): Fixes the forwarding of `reasoning_content` from OpenAI-compatible providers like MiMo, enabling their use with the gateway.
    - PR #92072 (open): Addresses the broken image input support for `google-gemini-cli` models at the gateway.
    - PR #92081 (open): An enterprise-focused PR enhancing the new Microsoft Teams voice/video provider, fixing echo, adding replay-proof handshakes, and per-thread sessions.
- **Security & Tooling**:
    - PR #47523 (open): A significant PR preflighting tool name collisions and tightening trust for local media passthrough, preventing potential security bypasses.
- **Data & Persistence**:
    - PR #92079 (open): Fixes a `providerKey` mismatch when using `memory index --force`, which could lead to database corruption or inconsistency.

### 4. Community Hot Topics

The community is deeply engaged with several critical issues, primarily concerning **message leaks, data loss, and session state corruption**.

- **Issue #25592: Text between tool calls leaks to messaging channels** (31 comments) - This "Diamond Lobster" severity issue details a major UX problem where internal agent processing output is leaked to users on platforms like Slack and iMessage. The underlying need is for a clear filter or "buffer" that separates internal agent reasoning from user-facing conversation.
- **Issue #44925: Subagent completion silently lost** (19 comments) - Reports multiple failure modes where subagent tasks fail without any retry, notification, or error handling. This highlights a need for robust, observable, and retryable task orchestration.
- **Issue #88838: Track core session/transcript SQLite migration** (19 comments) - A maintainer-driven issue to track the high-risk migration of core runtime state to SQLite. It reflects the community's need for a stable, auditable, and performant state system, but also the project's caution in handling it.
- **Issue #32473: Control UI requires device identity (HTTPS)** (17 comments, 👍 4) - A regression and security blocker for users on non-localhost setups (e.g., VPS). The community needs a flexible, configurable identity requirement for the web UI, not a hard requirement for HTTPS/localhost.
- **Issue #29387: Bootstrap files in agentDir silently ignored** (14 comments, 👍 5) - A high-impact bug where per-agent configuration files are ignored, forcing users to rely on a shared workspace. The underlying need is for robust, per-agent configurability that actually works.
- **Issue #58450: Agent can promise a follow-up without action** (15 comments, 👍 2) - A user-experience bug where the agent hallucinates a commitment to a background task. The community needs better tracking and enforcement of in-progress actions.

### 5. Bugs & Stability

The project is suffering from a significant number of critical (P1/P0) and high-severity ("Diamond Lobster" rated) bugs. Key issues reported or updated today include:

- **Critical / P1**:
    - [#44925](openclaw/openclaw Issue #44925): Subagent completion silently lost (No fix PR linked).
    - [#25592](openclaw/openclaw Issue #25592): Text between tool calls leaks to channels (No fix PR linked).
    - [#32296](openclaw/openclaw Issue #32296): Agent replies to previous message (Session context confusion) (No fix PR linked).
    - [#29387](openclaw/openclaw Issue #29387): Bootstrap files in `agentDir` silently ignored (No fix PR linked).
    - [#31331](openclaw/openclaw Issue #31331): Docker + Sandbox workspace access fails (No fix PR linked).
    - [#43661](openclaw/openclaw Issue #43661): Session hangs on compaction timeout, causing duplicate message sends (No fix PR linked).
- **High Priority / P2**:
    - [#32473](openclaw/openclaw Issue #32473): Control UI requires HTTPS (Regression) (No fix PR linked).
    - [#31583](openclaw/openclaw Issue #31583): `exec` tool doesn't inherit `env` from skill config (Regression) (No fix PR linked).
    - [#43747](openclaw/openclaw Issue #43747): Memory management is in chaos (Regression) (No fix PR linked).
    - [#40540](openclaw/openclaw Issue #40540): `openclaw update` fails with EBUSY on Windows (No fix PR linked).
- **Stability Note**: The volume of "regression" bugs (e.g., #32473, #31583, #38327) is a serious concern, suggesting that new features or fixes are introducing regressions in previously working functionality. The `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision` labels on many of these top issues indicate a **maintainer bottleneck** in triaging and prioritizing fixes.

### 6. Feature Requests & Roadmap Signals

The community is actively requesting features that would improve flexibility, cost control, and user experience.

- **High Demand / Likely for Next Version**:
    - **Per-Agent Cost Budgets** ([#42475](openclaw/openclaw Issue #42475)): Enforcing spend limits at the gateway. This is a classic operational need for production deployments.
    - **Persistent Memory / Session Synthesis** ([#40418](openclaw/openclaw Issue #40418)): Automating the preservation and synthesis of session knowledge on `/new`. This is a foundational user-experience improvement.
    - **Natural-Language Rule Learning** ([#41366](openclaw/openclaw Issue #41366)): Durable rule training that works across agents and sessions, making agent behavior more configurable by end-users.
- **Moderate Demand / Possible Consideration**:
    - **Private Network Access for web_fetch** ([#39604](openclaw/openclaw Issue #39604)): An opt-in flag to allow agent access to internal services.
    - **`model` field in SKILL.md** ([#43260](openclaw/openclaw Issue #43260)): Allows routing specific skills to cheaper or more capable models. A strong signal for cost and performance optimization.
    - **Post-Subagent Extension Hook** ([#22358](openclaw/openclaw Issue #22358)): Enables plugin-based observability and logging.
- **Long-Term Roadmap Signal**:
    - **Multi-Agent Collaboration Enhancement** ([#35203](openclaw/openclaw Issue #35203)): A comprehensive RFC for capability profiling, shared blackboards, and cost governance. This signals the community's desire to move beyond simple orchestration to true multi-agent systems.
    - **Wear OS App** ([PR #47604](openclaw/openclaw PR #47604)): A large, AI-suggested PR for an Android Watch UI, showing ambition for mobile use cases.
    - **Adaptive Resource Limits** ([PR #47706](openclaw/openclaw PR #47706)): Auto-tuning performance for ARM/low-memory devices, pointing towards broader platform support.

### 7. User Feedback Summary

User feedback reveals significant satisfaction with the core functionality of OpenClaw, but mounting frustration with **reliability, configuration complexity, and opaque failures**.

- **Pain Points**:
    - **Message Leaks & Noise**: Users are dissatisfied with internal agent processing text leaking to public channels (e.g., [#25592](openclaw/openclaw Issue #25592), [#44905](openclaw/openclaw Issue #44905)).
    - **Silent Failures & Data Loss**: The agent promising follow-ups and then doing nothing ([#58450](openclaw/openclaw Issue #58450)) or subagents failing silently ([#44925](openclaw/openclaw Issue #44925)) are cited as major frustrations and degrade trust.
    - **Configuration is Fragile**: Users report that configuration (like bootstrap files, env vars) is silently ignored or broken in specific contexts (e.g., Docker, agent directories), causing hard-to-debug issues ([#29387](openclaw/openclaw Issue #29387), [#31583](openclaw/openclaw Issue #31583)).
    - **Memory Inconsistency**: One user explicitly stated, "Memory management is in chaos" ([#43747](openclaw/openclaw Issue #43747)), with different instances behaving differently. This points to poor debugging and observability of the memory system.
    - **Update is Unreliable**: A Windows user reported `openclaw update` failing with `EBUSY` ([#40540](openclaw/openclaw Issue #40540)), preventing them from receiving security fixes.
- **Use Cases**: Users are deploying OpenClaw in diverse real-world environments: Docker/VPS, Telegram forums, Discord servers, and corporate Teams, highlighting its value as a universal AI interface. The complex multi-agent orchestration use case is a significant driver for many top issues.

### 8. Backlog Watch

Several critical and high-priority issues and PRs are stuck in the backlog, waiting for maintainer action.

- **Critical Issues Awaiting Maintainer Decision/Grooming**:
    - [#25592](openclaw/openclaw Issue #25592): Text between tool calls leaks. Also needs product decision.
    - [#44925](openclaw/openclaw Issue #44925): Subagent completion lost. Also needs product decision.
    - [#32296](openclaw/openclaw Issue #32296): Agent replies to wrong message. Also needs live repro and product decision.
    - [#29387](openclaw/openclaw Issue #29387): Bootstrap files silently ignored. Needs security review and product decision.
    - [#31331](openclaw/openclaw Issue #31331): Docker sandbox breaks workspace access. Needs product decision.
    - [#31583](openclaw/openclaw Issue #31583): `exec` tool ignores skill env. Needs security review and product decision.
- **High-Value PRs Stalled**:
    - [#47523](openclaw/openclaw PR #47523): Agents: tighten tool name trust and preflight tool collisions. Status: `👀 ready for maintainer look`. This is a critical security hardening PR waiting for review.
    - [#92073](openclaw/openclaw PR #92073): fix: handle explicit silent assistant replies. Status: `📣 needs proof`. This addresses a key part of the "message leak" problem.
    - [#75662](openclaw/openclaw PR #75662): fix(agents): pause yielded main-session runs. Status: `⏳ waiting on author`. A key fix for session management.
    - [#47604](openclaw/openclaw PR #47604): feat(android): add Wear OS app MVP. Status: `📣 needs proof`. A major feature with high community interest that appears stalled.
- **Community Feature Requests with No Maintainer Action**: Many high-voted features (e.g., [#39604](openclaw/openclaw Issue #39604) private network access, [#42475](openclaw/openclaw Issue #42475) per-agent budgets, [#16670](openclaw/openclaw Issue #16670) onboarding wizard for memory) have been open for 1-3 months and are stuck with `clawsweeper:needs-product-decision` labels. This suggests a strategic bottleneck in deciding which features to prioritize.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs Hermes Agent

## 1. Ecosystem Overview

The personal AI assistant / agent open-source ecosystem continues to mature in mid-2026, driven by two prominent reference implementations—**OpenClaw** and **Hermes Agent**—each representing distinct architectural philosophies. Both projects are experiencing sustained high-velocity development, with hundreds of issues and pull requests processed weekly. The community is converging on a set of shared operational needs: robust session management, cost governance, security hardening, and multi-platform support. However, each project’s approach to these challenges—ranging from architectural decisions (monolithic gateway vs modular runtime) to target audience (power users vs broad accessibility)—creates meaningful differentiation. The ecosystem overall is healthy, with rapid iteration balanced against growing pains in maintainer bandwidth and bug regression management.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|---|---|---|
| **Open Issues** | 469 | 47 (open, out of 50 total) |
| **Open PRs** | 396 | 47 (open, out of 50 total) |
| **New Issues (24h)** | Not reported directly; high volume of updates | 3 closed, many updated |
| **New PRs (24h)** | 104 merged/closed | 3 closed |
| **Recent Release** | v2026.6.6-beta.1 (today) | None |
| **Release Focus** | Security hardening, breaking changes | – |
| **Maintainer Bottleneck** | High (many issues labelled `needs-maintainer-review`) | Moderate (quick fix PRs for critical bugs) |
| **Health Score** (estimated) | **3/5** – active but backlogged, regression-heavy | **4/5** – responsive maintainers, fewer regressions |

**Interpretation**: OpenClaw operates at a much larger scale (10× more issues and PRs) but with a corresponding maintainer bottleneck. Hermes Agent shows tighter control over issue and PR volume, suggesting a smaller but more focused community.

## 3. OpenClaw’s Position

**Advantages over Hermes Agent:**
- **Scale & Breadth**: OpenClaw’s community is significantly larger, evidenced by 469 open issues vs 50. This translates to a richer feature request pipeline and broader platform support (Discord, Teams, Slack, iMessage, Wear OS).
- **Security-first release**: The v2026.6.6-beta.1 release is a headline-grabbing hardening push that addresses message leaks, sandbox escapes, and SSRF. This positions OpenClaw as the security-conscious choice.
- **Multi-agent orchestration**: OpenClaw explicitly supports subagent tasks, multi-agent collaboration (RFC #35203), and advanced session synthesis — capabilities that are less prominent in Hermes’s roadmap.

**Technical approach differences:**
- OpenClaw employs a **monolithic core reference** with a plugin/extension system, while Hermes uses a **modular gateway + desktop + CLI** architecture.
- OpenClaw’s state management is migrating to SQLite (high-risk, high-reward); Hermes uses SessionDB with per-thread connections.
- OpenClaw’s cost governance features (per-agent budgets, model routing per skill) are more mature than Hermes’s current capabilities.

**Community size comparison:**
- OpenClaw’s issue volume (469) vs Hermes (50) suggests a user base roughly 5–10× larger, though both projects likely share overlapping enthusiasts.

## 4. Shared Technical Focus Areas

The following requirements emerge clearly across **both projects**, indicating ecosystem-wide pain points:

| Requirement | OpenClaw Evidence | Hermes Agent Evidence |
|---|---|---|
| **Message leak prevention** | Issue #25592 — tool call text leaks to channels | PR #43940 — close persistence-boundary redaction gaps |
| **Subagent/background task reliability** | Issue #44925 — subagent completion silently lost; Issue #58450 — agent promises without action | Issue #24187 — SessionDB silent turn skip; Issue #43899 — cron model failures |
| **Cost control & usage limits** | Issue #42475 — per-agent cost budgets | Issue #43915 — Bedrock transient faults (indirect) |
| **Cross-platform compatibility** | Docker sandbox (Issue #31331), Windows update failures (Issue #40540) | Docker permissions (Issue #23402), macOS launchd crashes (Issue #43842) |
| **Security hardening** | Multiple PRs in v2026.6.6-beta.1 | PR #43937/#43938/#43942 — WeCom, SSRF, tar extraction |
| **Accessibility / localization** | Issue #32473 — HTTPS requirement for UI (usability barrier) | Issue #26689 — VoiceOver; Issue #40239 — Portuguese localization |

**Key insight**: Both projects are investing heavily in **session integrity** and **invisible failure reduction** — the “silent data loss” class of bugs degrades user trust and is being treated as a top priority.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|---|---|---|
| **Target user** | Power users, DevOps, enterprise teams (Teams voice, corporate moderation) | Individual developers, hobbyists, accessibility-focused users |
| **Primary use case** | Multi-agent orchestration, production-grade assistant with cost management | Personal assistant across many chat platforms (Telegram, WeCom, Matrix), desktop app |
| **Architecture** | Centralized core with plugin system; SQLite migration underway | Modular gateway + separate desktop/CLI clients; per-thread SessionDB |
| **Platform support** | Wide: Slack, Discord, Teams, iMessage, Telegram, Wear OS | Broad: Telegram, WeCom, Matrix, macOS, Docker, Windows, Bedrock |
| **Cost governance** | Explicit per-agent budgets, skill-level model routing | Emerging (cron model config, Bedrock streaming) |
| **Accessibility** | Largely unaddressed; HTTP-only UI blocker | Active: VoiceOver, localization PRs, desktop app |
| **Security posture** | Aggressive hardening with breaking changes | Incremental, defense-in-depth patches |
| **Release cadence** | Beta releases with significant breaking changes | Smaller, more frequent fixes without major breaking changes |

**Summary**: OpenClaw aims to be the **multi-agent operating system** for advanced deployments; Hermes Agent aims to be the **friendly, cross-platform personal assistant** with a lower barrier to entry.

## 6. Community Momentum & Maturity

**Activity tiers:**

- **High-velocity, high-churn (OpenClaw)**: Merging 100+ PRs daily, releasing major betas, but suffering from regression fatigue and maintainer bottleneck. The community is large and vocal, driving feature demand faster than maintainers can process.
- **Steady, responsive (Hermes Agent)**: Lower volume but faster turnaround for critical bugs (e.g., cron fix PR opened same day as report). Fewer regressions, more stable for daily use.

**Maturity signals:**
- OpenClaw is in a **growth phase** — the feature set is expanding rapidly, but stability is lagging. The v2026.6.6-beta.1 label indicates cautious rollout.
- Hermes Agent is in a **stabilization phase** — incremental fixes and platform support, with less focus on groundbreaking new features.

**Which is rapidly iterating?** Both, but OpenClaw iterates at a larger scale and higher volatility. Hermes iterates more conservatively.

## 7. Trend Signals

From community feedback across both projects, several industry-wide trends emerge that are valuable for AI agent developers:

1. **Silent failures are the #1 trust killer**. Both projects’ top bugs involve the agent silently dropping tasks (subagents, background promises, cron jobs). Developers should invest in **observability, retry logic, and user-facing failure notification**.

2. **Cost governance is moving from “nice-to-have” to “must-have”**. Users in both communities demand per-agent budgets, model routing, and spend tracking. Expect this to become a standard feature in all agent frameworks.

3. **Multi-platform support is non-negotiable**. Users deploy on macOS, Docker, Windows, Telegram, Teams, WeCom, and Matrix. Agent projects that ignore any of these risk fragmenting their user base.

4. **Security hardening is a differentiator**. OpenClaw’s beta release and Hermes’s flurry of security PRs show that users are increasingly sensitive to message leaks, SSRF, and sandbox escape. The bar for safe defaults is rising.

5. **Accessibility and localization are growing demands**. Hermes’s VoiceOver and pt-BR requests signal that international and disabled users are a significant part of the early adopter base.

6. **Multi-agent orchestration is the next frontier**. OpenClaw’s RFC #35203 (multi-agent collaboration) and subagent issues reflect a market that wants agents solving problems **together**, not just with one LLM call.

**Recommendation for developers**: Build with **observable, fault-tolerant state management** from the start. Prioritize cost controls and security boundaries equally with core agent capabilities. Plan for both power-user flexibility and accessible defaults.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-06-11

## Today's Overview
Hermes Agent shows **very high activity**, with 50 issues and 50 pull requests updated in the last 24 hours—indicating a bustling development cycle. The vast majority remain open (47 each), reflecting ongoing discussion and work-in-progress. Three issues and three PRs were closed/merged today, suggesting moderate merge velocity. No new releases were published. The project is healthy with a clear focus on bug fixing (especially P1/P2 stability issues), security hardening, cross-platform compatibility (macOS, Docker, Windows, Telegram, WeCom), and incremental feature refinements.

## Releases
No new releases today.

## Project Progress
Two pull requests were merged/closed today:

- **#43602 (CLOSED) – docs: clarify Baoyu image generation workflow**  
  Improves documentation on how the bundled Baoyu skills generate images, adding a rule against manual SVG/HTML/Pillow rendering.

- **#43948 (CLOSED) – fix(memory): pass live model name to MemoryProvider.on_turn_start**  
  Fixes a contract mismatch where the model name was not actually passed to memory providers, aligning implementation with documented API.

Additionally, the following PRs remain open but represent major ongoing efforts:
- **#43039** – Action Runtime refactor (gateway exec paths, model-picker, SessionState)
- **#26051** – Preserve context on compression failures
- **#31477** – Emit recovery-path final response through stream_delta_callback
- **#34460** – Per-thread SessionDB connections (performance)
- **#18506** – Matrix gateway native tools and reaction controls (long-running)

## Community Hot Topics
The most active discussions this period:

1. **[#23402] Bug: Docker with HERMES_UID permissions issue** (15 comments, 3 👍)  
   *Author:* mmartial – Ongoing issue with Unraid template and container chat permissions. High engagement suggests Docker deployment is a popular but fragile path.

2. **[#26689] Accessibility improvements for blind VoiceOver users** (9 comments)  
   *Author:* xiaopinpin-music – Detailed UX pain points for screen-reader users on macOS. Community showing strong support for inclusive design.

3. **[#6626] Gemma 4 tool calling support** (5 comments, 3 👍)  
   *Author:* spprod35 – Parser availability and configuration for Gemma 4 via vLLM. Points to growing interest in newer open models.

4. **[#40239] Portuguese (pt-BR) language support in desktop app** (4 comments, 2 👍)  
   *Author:* alexander-stack1 – Localization request backed by existing TUI translations. Highlights demand for non-English users.

5. **[#43952] fix(cron): prevent empty model from reaching the API** (new PR, undefined comments)  
   Immediate fix for a P1 bug reported the same day (#43899). Community responsive to critical issues.

## Bugs & Stability

### P1 (Critical)
- **#43899** – Cron jobs fail with 'Model parameter is required' when model not explicitly set. **Fix PR #43952** opened same day.
- **#24187** – SessionDB silently skips current turn when message repair shortens history. No fix PR yet.
- **#43842** – macOS: plist refresh bootout from inside gateway kills CLI before bootstrap; agent-initiated self-update leaves service unloaded. No fix PR yet.
- **#43953** – Hermes Desktop crashes when running multiple profile sessions simultaneously. No fix PR yet.

### P2 (High)
- **#25290** – Cron jobs split across profile directories (closed, but underlying design issue persists).
- **#17198** – Gateway restart race condition causes Weixin token conflict.
- **#43475** – `/restart` bricks launchd-managed gateway on macOS (exits 0, not relaunched).
- **#43835** – Telegram: double messages (tool output + response body).
- **#43666** – Redaction gaps at persistence boundary (tool output file dumps, compaction blocks, DB URIs). **Fix PR #43940** opened.
- **#43915** – Bedrock streaming transient faults abort turn non-retryably.
- **#43575** – Webhook signature validation doesn't support Fireflies V2.
- **#43946** – Non-Claude Bedrock models fail with malformed tool/message payloads.

### P3 (Medium)
- **#43558** – MemoryProvider.on_pre_compress() return value discarded (fix PR #43948 merged).
- **#43621** – update_fact leaves old category HRR bank stale.
- **#43622** – remove_fact leaves orphaned entities.
- **#43900** – Ollama local models capped at 4096-token context.
- **#43476** – Desktop: /goal swallows command.
- **#43865** – Desktop: Chat does not auto-scroll to bottom.
- **#43944** – Voice conversation TTS cuts off content.
- **#43951** – vision_analyze tool should auto-disable when main model lacks vision.

### Security Fixes in PRs
- **#43937** – WeCom callback constant-time signature comparison.
- **#43938** – Block SSRF in yuanbao download_url.
- **#43940** – Close persistence-boundary redaction gaps.
- **#43942** – Harden curator rollback tar extraction (symlink/abs-path escape).

## Feature Requests & Roadmap Signals

### User-Requested Features
- **Portuguese (pt-BR) localization** (#40239) – likely to be picked up given existing TUI translations.
- **Cross-interface session and history synchronization** (#43928) – multiple users asking for unified experience across Desktop, Gateway, Telegram.
- **Graceful session resume / reset-awareness** (#43008) – agent should notify on context loss.
- **Container .env mode configurability** (#43473) – for host-mounted .env readability.
- **Accessibility overhaul** (#26689) – VoiceOver support would be a major UX improvement.

### Roadmap Signals from PRs
- **#43950** – Normalize Gemma 4 reasoning tokens for UI rendering (shows active support for non-OpenAI models).
- **#43949** – Config-driven Telegram callback→text routes (inline keyboard bridging).
- **#43947** – Fix DeepSeek Anthropic-compatible endpoint compatibility (thinking block preservation).
- **#34609** – Opt-in X-Hermes-User-Id header for per-user memory scope (multi-tenant HTTP API).
- **#18506** – Matrix gateway parity (third stacked PR) indicates ongoing expansion of platform support.
- **#43942** – Security hardening of curator rollback (defense-in-depth).

**Prediction for next version:** Expect a release focused on stability fixes (P1 cron, macOS launchd, Desktop crash), security patches (redaction, SSRF, tar extraction), and incremental platform support (Gemma 4, DeepSeek, Telegram callback routes). Localization and Matrix may land in subsequent versions.

## User Feedback Summary
- **Pain points:** Docker permissions, macOS gateway restart failures, Desktop crashes on multi-profile, TTS truncation, double Telegram messages, and cron model configuration gaps. These suggest that multi-profile and cross-platform reliability are major friction areas.
- **Satisfaction:** Users are active in filing detailed bug reports and feature requests, indicating strong engagement and willingness to contribute. The community quickly provides fix PRs (e.g., #43952 for cron issue).
- **Use cases:** Users are deploying Hermes on Unraid (Docker), macOS (launchd), Windows (Node.js slow updates), and integrating with Telegram, WeCom, and Amazon Bedrock. Accessibility and localization needs show a diverse user base.
- **Dissatisfaction:** Silent context loss (#24187, #43008) and unsafe defaults (Ollama context cap, unconditional .env permission reset) reduce trust in persistent conversations.

## Backlog Watch
Several important issues/PRs remain open with no maintainer response or resolution:

1. **#6626** (2026-04-09) – Gemma 4 tool calling support  
   High community interest (3 👍, 5 comments). No maintainer update despite being open for 2 months.

2. **#17198** (2026-04-29) – Gateway restart race condition with Weixin token  
   Platform-specific but no fix or workaround documented.

3. **#18506** (2026-05-01) – Matrix gateway native tools PR  
   Open for 40+ days, marked as draft. Depends on earlier PR #18505 which may also be stalled.

4. **#24187** (2026-05-12) – SessionDB silent turn skip (P1)  
   Critical bug with no assignee or comment from maintainers.

5. **#25290** (2026-05-13) – Cron jobs split across profiles (closed but core issue unresolved)  
   Closed without a code fix; users may encounter the same fragmentation.

6. **#26689** (2026-05-16) – Accessibility for VoiceOver users  
   Detailed UX report with no maintainer acknowledgment.

**Recommendation:** Maintainers should prioritize the P1 bugs (#24187, #43899, #43842, #43953) and provide updates on long-standing feature requests like Gemma 4 support and accessibility to keep the community engaged.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*