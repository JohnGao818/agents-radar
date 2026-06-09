# OpenClaw Ecosystem Digest 2026-06-09

> Issues: 500 | PRs: 472 | Projects covered: 2 | Generated: 2026-06-09 02:45 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-09

## 1. Today’s Overview

The OpenClaw project is operating at high velocity: **500 issues** and **472 PRs** were updated in the last 24 hours, with **64 issues closed** and **141 PRs merged or closed**. Two new beta releases landed today (v2026.6.5-beta.5 and v2026.6.5-beta.3), suggesting an active release cycle. However, the open issue count (436) combined with a large number of stale, high-severity bugs indicates the community is heavily testing and reporting regressions, while maintainers are focusing on critical fixes (transcript corruption, auth scoping, provider transport errors). The project remains in a “bumpy but moving” state — many improvements are landing, but stability is a recurring concern.

## 2. Releases

Two releases were published:

- **v2026.6.5-beta.5** and **v2026.6.5-beta.3** (both tagged 2026.6.5)  
  - **Key changes**:  
    - QQBot now strips model reasoning/thinking scaffolding before native delivery, preventing raw `<thinking>` content from leaking into channel replies. (PRs #89913, #90132, thanks @openperf)  
    - MCP tool results now coerce `resource_link`, `resource`, `audio`, malformed image, and other unexpected content types to safe fallbacks.  
  - **No explicit breaking changes or migration notes** are listed in the release highlights.  

Given the beta versioning and the focus on channel-specific fixes, operators should test these updates in non-production environments before upgrading.

## 3. Project Progress

Today’s 141 merged/closed PRs include several notable fixes and refactors:

- **Transcript image redaction fix** ([#91529](https://github.com/openclaw/openclaw/pull/91529)) – Preserves validated opaque image payloads during redaction, repairing already-poisoned session image blocks.  
- **ImageContent data preservation** ([#90856](https://github.com/openclaw/openclaw/pull/90856)) – Fixes a permanent session break after image messages.  
- **Windows config opener fix** ([#91536](https://github.com/openclaw/openclaw/pull/91536)) – Corrects the Dashboard “Open config” action on Windows (replaces non-existent `-LiteralPath` with `-FilePath`).  
- **Refactor: drop unused async Kysely driver** ([#91526](https://github.com/openclaw/openclaw/pull/91526)) – Removes dead code, reducing maintenance surface.  
- **Memory-core: exclude archived transcripts from Dreaming corpus** ([#90433](https://github.com/openclaw/openclaw/pull/90433)) – Prevents cron/subagent noise from polluting daily analysis.  
- **Docker store seed fix** ([#91547](https://github.com/openclaw/openclaw/pull/91547)) – Ensures platform optional packages (e.g., Codex ACP) are architecture-aware.  

These fixes address critical stability and usability issues, especially around session data integrity and cross-platform operation.

## 4. Community Hot Topics

The most active discussions (by comment count) reveal deep user concerns:

- **Filename encoding utility** ([#48788](https://github.com/openclaw/openclaw/issues/48788)) – 18 comments. Proposes a centralized solution for multi-encoding Content-Disposition handling (Shift-JIS, EUC-KR, GB18030). Users need a robust, framework-level fix rather than per-adapter patches.  
- **Control UI requires HTTPS/localhost** ([#32473](https://github.com/openclaw/openclaw/issues/32473)) – 17 comments, 4 👍. A regression that blocks users on VPS/Docker setups without device identity. Strong demand for a workaround or config option.  
- **OpenAI ChatGPT Responses transport fails** ([#90083](https://github.com/openclaw/openclaw/issues/90083)) – 15 comments, 3 👍. Post-upgrade breakage for gpt-5.4/5.5, causing connection errors. Highly disruptive for users on latest models.  
- **Community Skill Development & ClawHub** ([#50090](https://github.com/openclaw/openclaw/issues/50090)) – 15 comments, 2 👍. Users highlight the gap between promise and practice – skill ecosystem is underpowered, Driftnet has been unreliable.  
- **Session context confusion** ([#32296](https://github.com/openclaw/openclaw/issues/32296)) – 14 comments. Agent replies to earlier messages instead of current ones, causing conversation misalignment. A core session-state bug affecting many users.  

The underlying need is **reliability and security**: users are encountering regressions that break basic functionality (auth, message delivery, session progression), while also requesting architectural improvements (skill governance, encoding standards).

## 5. Bugs & Stability

Ranked by severity (P1 highest):

| ID | Title | Priority | Impact | Fix PR exists? |
|----|-------|----------|--------|----------------|
| [#90083](https://github.com/openclaw/openclaw/issues/90083) | OpenAI ChatGPT Responses transport fails (gpt-5.4/5.5) | P1 | auth-provider, connectivity | No linked PR |
| [#32296](https://github.com/openclaw/openclaw/issues/32296) | Agent replies to previous message (session context confusion) | P1 | session-state, message-loss | No linked PR |
| [#43367](https://github.com/openclaw/openclaw/issues/43367) | Multi-agent orchestration unstable (config overwrites, session-lock failures) | P1 | session-state, message-loss, auth-provider | Has linked PR (open) |
| [#48003](https://github.com/openclaw/openclaw/issues/48003) | Steer mode does not inject messages mid-turn for main sessions | P1 | session-state, message-loss | Has linked PR (open) |
| [#44905](https://github.com/openclaw/openclaw/issues/44905) | Discord leaks internal tool-call traces to channel | P1 | security, message-loss | No linked PR |
| [#51396](https://github.com/openclaw/openclaw/issues/51396) | clearUnboundScopes strips operator scopes unconditionally | P1 | security, auth-provider | Has linked PR (open) |
| [#49876](https://github.com/openclaw/openclaw/issues/49876) | Cron sessions hallucinate output when tools fail | P1 | session-state, security | No linked PR |
| [#32473](https://github.com/openclaw/openclaw/issues/32473) | Control UI requires device identity (regression) | P2 | security, auth-provider | No linked PR |
| [#43747](https://github.com/openclaw/openclaw/issues/43747) | Memory management chaos (regression) | P2 | session-state | No linked PR |
| [#52186](https://github.com/openclaw/openclaw/issues/52186) | TTS elevenlabs generates audio but OpenAI voice plays instead (regression) | P2 | auth-provider | No linked PR |
| [#45740](https://github.com/openclaw/openclaw/issues/45740) | gh-issues skill: untrusted body injected into sub-agent prompt | P2 | security | Has linked PR (open) |

Several P1 bugs have open fix PRs, indicating maintainer awareness. However, a large number remain unaddressed, especially security issues and session-state regressions.

**Notable closed bugs today**:  
- [#88929](https://github.com/openclaw/openclaw/issues/88929) – Feishu streaming card typewriter effect / truncated content (closed, fix released).  
- [#65156](https://github.com/openclaw/openclaw/issues/65156) – Memory vector search broken in v4.11 (SQLite ABI mismatch) – closed with fix.

## 6. Feature Requests & Roadmap Signals

Several high-interest features suggest where the project may invest next:

- **Centralized filename encoding** ([#48788](https://github.com/openclaw/openclaw/issues/48788)) – Likely candidate for next release given the PR #48578 groundwork and strong community backing.  
- **Skill ecosystem improvements** ([#50090](https://github.com/openclaw/openclaw/issues/50090), [#43260](https://github.com/openclaw/openclaw/issues/43260), [#50199](https://github.com/openclaw/openclaw/issues/50199)) – Per-skill model routing, skill priority, and ClawHub reliability are recurring themes.  
- **Per-agent cost budgets** ([#42475](https://github.com/openclaw/openclaw/issues/42475)) – Gateway-level cost caps requested by operators to prevent runaway spend.  
- **Security scanning for skill installation** ([#45031](https://github.com/openclaw/openclaw/issues/45031)) – User proposes integrating AgentShield; if accepted, could be a major trust improvement.  
- **Multi-session architecture RFC** ([#48874](https://github.com/openclaw/openclaw/issues/48874)) – Shared LLM + isolated sessions + public knowledge base; a long-term architectural shift.  
- **MathJax/LaTeX in Control UI** ([#42840](https://github.com/openclaw/openclaw/issues/42840)) – 5 👍, highly requested for scientific/mathematical communication.  
- **YAML config support** ([#45758](https://github.com/openclaw/openclaw/issues/45758)) – 2 👍, DevOps-friendly alternative to JSON5.  

Given the high volume of regressions, the immediate roadmap is likely focused on stability fixes, but the filename encoding utility and skill ecosystem features have strong momentum.

## 7. User Feedback Summary

**Pain points** repeatedly expressed:

- **Regressions**: Several users report “worked before, now fails” across authentication, session state, memory, and TTS. New versions introduce instability.  
- **Session handling**: Context confusion (#32296), stale timestamps in cron (#44993), zombie subagents (#48573), and false “busy” state (#87387 via #87474) frustrate daily use.  
- **Configuration complexity**: Hardcoded developer paths shipped to release (#51429), nested OPENCLAW_HOME directories (#45765), and live docs ahead of releases (#48920) cause setup failures.  
- **Security/safety**: Internal tool-call leaks on Discord (#44905), untrusted GitHub issue body injection (#45740), and hallucinated cron output (#49876) erode trust.  
- **Community skill ecosystem**: Users want ClawHub to be more reliable and skills to be prioritizable and model-aware.  

**Satisfaction signals**: Users are actively reporting bugs and contributing solutions (e.g., @openperf on QQBot, @jimmielightner on OpenAI transport). The community is engaged and cares deeply about product quality.

## 8. Backlog Watch

Long-standing, important issues that need maintainer attention:

| Issue | Created | Stale | Priority | Impact | Notes |
|-------|---------|-------|----------|--------|-------|
| [#32473](https://github.com/openclaw/openclaw/issues/32473) – Control UI requires HTTPS/localhost | 2026-03-03 | Yes | P2 | security, auth-provider | 17 comments, 4 👍. No fix PR in sight. |
| [#45740](https://github.com/openclaw/openclaw/issues/45740) – gh-issues skill injection | 2026-03-14 | Yes | P2 | security | Open PR exists but still stale. |
| [#43367](https://github.com/openclaw/openclaw/issues/43367) – Multi-agent orchestration unstable | 2026-03-11 | No (but P1) | P1 | session-state, message-loss | Has linked PR, but still needs maintainer review. |
| [#50090](https://github.com/openclaw/openclaw/issues/50090) – Community Skill Development & ClawHub | 2026-03-19 | Yes | P2 | ecosystem | Needs product decision; key to platform growth. |
| [#48003](https://github.com/openclaw/openclaw/issues/48003) – Steer mode not injecting messages mid-turn | 2026-03-16 | Yes | P1 | session-state, message-loss | Linked PR open but waiting on author. |
| [#44905](https://github.com/openclaw/openclaw/issues/44905) – Discord leaks tool-call traces | 2026-03-13 | Yes | P1 | security, message-loss | No fix PR; security review needed. |
| [#48788](https://github.com/openclaw/openclaw/issues/48788) – Centralized filename encoding | 2026-03-17 | Yes | P2 | data-loss | High community interest; product decision pending. |

These items span over 3 months without resolution, especially critical security and session-state bugs. The project should consider assigning dedicated maintainers to these high-impact issues to reduce backlog and improve user confidence.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Open-Source Personal AI Agent Ecosystem

## 1. Ecosystem Overview

The open-source personal AI agent landscape is currently characterized by **high-velocity development** paired with **significant stability friction**. Both OpenClaw and Hermes Agent are operating at substantial scale, with hundreds of daily contributions and active community engagement, yet both face recurring regressions in session state, authentication, and cross-platform reliability. The ecosystem is bifurcating: projects are either pursuing broad multi-channel integration (OpenClaw) or deep desktop/gateway workflow optimization (Hermes), while both grapple with skill ecosystem maturity, cost governance, and security hardening as users demand production-grade behavior. The community's tolerance for instability is low—users consistently report “worked before, now fails” across critical paths, signaling that maintainer focus on regression prevention and backward compatibility is becoming a competitive differentiator.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues updated (24h)** | 500 | 50 |
| **PRs updated (24h)** | 472 | 50 |
| **Issues closed (24h)** | 64 | 4 |
| **PRs merged/closed (24h)** | 141 | 4 |
| **Open issues** | 436 | 46 |
| **Open PRs** | ~331 (estimated from 472 updated − 141 closed) | 46 |
| **Release status** | Two beta releases today (v2026.6.5-beta.3 & .5) | No new release |
| **Health score** | Moderate-High — high throughput, but many regressions and P1 bugs without fix PRs | Moderate — lower throughput, growing backlog, critical macOS/Docker bugs unaddressed |

**Key insight:** OpenClaw operates at roughly **10× the raw velocity** of Hermes Agent, but this comes with a correspondingly larger open issue count and a higher proportion of high-severity regressions. Hermes’ lower merge rate suggests a more conservative or resource-constrained maintainer approach.

## 3. OpenClaw's Position

**Advantages over peers:**
- **Raw velocity and investment:** 500 daily issue updates and 141 merged PRs indicate an active maintainer team and large contributor base. This allows faster response to critical bugs (e.g., transcript image redaction fix #91529 merged same-day).
- **Multi-platform channel reach:** Native support for QQBot, Feishu, Discord, and Control UI gives it broadest channel coverage among open-source agent frameworks.
- **Session state sophistication:** Despite current bugs, OpenClaw's session orchestration (multi-agent, cron, steer mode, dreaming) is more ambitious than Hermes’ delegate-task model.
- **MCP tool ecosystem:** Active investment in tool-result coercion and skill governance positions OpenClaw for richer third-party integrations.

**Technical approach differences:**
- OpenClaw is **session-state-centric** — it treats conversation state as a first-class entity with persistence, redaction, and isolation mechanisms. Hermes relies more on per-request context passing.
- OpenClaw uses a **transport abstraction layer** (ChatGPT responses, MCP tools, channel adapters) whereas Hermes focuses on a **gateway + TUI/desktop** architecture.
- OpenClaw ships **more complex memory systems** (archival exclusion from dreaming corpus, vector search fixes) indicating heavier investment in long-term knowledge management.

**Community size comparison:**
OpenClaw's community is substantially larger by activity metrics (~10× issue/PR volume). However, Hermes’ 50 open PRs from community members suggests a **healthy, engaged contributor base** relative to its smaller scale. OpenClaw's higher volume also means more noise—436 open issues vs. 46 for Hermes.

**Risk:** OpenClaw’s velocity risks **regression fatigue** — users report new versions breaking auth, session delivery, and TTS. Without a dedicated stabilization phase, trust may erode despite rapid feature delivery.

## 4. Shared Technical Focus Areas

The following requirements emerge across both projects, indicating systemic needs in the agent ecosystem:

| Focus Area | OpenClaw Signals | Hermes Signals |
|------------|------------------|----------------|
| **Security governance for skills/plugins** | #45031 AgentShield integration; #45740 gh-issues injection; #44905 Discord tool-call leaks | #27997 Declarative Skill Protection Policy; PR #42514 Matrix recovery key hardening |
| **Session state integrity** | #32296 context confusion; #48003 steer mode injection; #43367 multi-agent chaos; #42449 (through shared singleton) | #42449 delegate_task corrupts parent context_length; #42120 incomplete turn loss on stop |
| **Containerization & deployment reliability** | #91547 Docker architecture-aware seeds; #32473 Control UI HTTPS/localhost regression | #34457 s6-log lock collision; #30399 Matrix gateway pip package missing; #42376 macOS launchctl bootstrap |
| **Cost tracking & budget governance** | #42475 per-agent cost budgets (feature request) | #42477 cost tracking undercounts; PR #42554 three root causes patched |
| **Community skill ecosystem maturity** | #50090 ClawHub unreliability; #43260 skill priority; #50199 model routing per skill | #27997 skill protection; growing need for model-agnostic skill interfaces |

**Implication:** The ecosystem is converging on three pain points: **security for extensibility**, **session reliability under concurrency**, and **production-grade deployment tooling**. Projects that invest in these areas will differentiate.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary user** | Operators of multi-channel agent fleets (Discord, QQ, Feishu, web) | Individual power users running agents on desktop (macOS/Linux) with TUI |
| **Key feature focus** | Session orchestration, memory management, channel adapter breadth, MCP tool ecosystem | Desktop UX, macOS support, cost analytics, skill safety, gateway reliability |
| **Architecture** | Monolithic with transport abstraction; session-state as core primitive | Gateway + dashboard/desktop (TUI); per-request context passing |
| **Release cadence** | Frequent beta releases (2 today); rapid iteration | Slower, less frequent releases; stability-oriented |
| **Community contribution ratio** | High volume, many small fixes | Lower volume, more feature proposals and policy discussions |
| **Risk profile** | Regression-prone; new features sometimes break existing paths | Backlog accumulation; critical macOS/Docker bugs stall user onboarding |
| **Skill ecosystem approach** | ClawHub marketplace approach (currently unreliable) | Declarative protection policy, less focus on marketplace |

**Competitive edge:** OpenClaw wins on **channel breadth and feature ambition**; Hermes wins on **desktop UX focus and security-first skill design**. For enterprise/ops users, OpenClaw is the natural choice; for individual developer agents on personal machines, Hermes may be more polished.

## 6. Community Momentum & Maturity

**Activity Tiers:**

- **Tier 1 — High Velocity / Stabilizing:** **OpenClaw** maintains massive daily throughput but is in a “stabilization paradox” — it ships fixes quickly but introduces new regressions at a similar rate. The ecosystem maturity is **beta quality** with production aspirations.
- **Tier 2 — Moderate Velocity / Repairing:** **Hermes Agent** is iterating more deliberately, with a clear focus on gateway reliability, macOS parity, and cost tracking. Its backlog of unaddressed P1 bugs (launchd death spiral, Matrix gateway) suggests maintainer bandwidth is constrained.

**Rapidly iterating:** OpenClaw (by volume). However, rapid iteration without a hardening release leads to user trust erosion.

**Stabilizing:** Neither project has reached a stability plateau. Hermes is closer in intent but has unaddressed critical bugs. Both need a **dedicated stabilization cycle** to reduce the “worked before, now fails” pattern.

**Maturity signals:**
- Both projects have **active skill/plugin discussions**, indicating an ecosystem beyond core dev.
- **Security conversations** are maturing (AgentShield, Declarative Skill Protection) — a sign that the community cares about production safety.
- **Backlog watch items span 3+ months** in both projects — a common challenge in fast-growing open-source projects.

## 7. Trend Signals

**Industry trends extracted from community feedback (value for AI agent developers):**

1. **Skill ecosystem governance is the next frontier.** Users are no longer satisfied with “install any skill” — they demand declarative safety policies, per-skill model routing, and auditability. Projects that fail to provide security tooling (sandboxing, injection prevention, least-privilege scoping) will lose enterprise trust.

2. **Session state is the hardest problem in AI agents.** Both projects’ top bugs involve context confusion, stale state, and message ordering. Developers building multi-turn agents should invest heavily in session isolation, replay safety, and conflict detection before scaling.

3. **Containerization parity is not optional.** Docker users are blocked by missing packages (Hermes Matrix) and log lock loops. The expectation is that Docker images should be production-ready day one—community workarounds erode confidence.

4. **Cost visibility is table stakes, not a feature.** Users want real-time, per-agent, per-cost-driver breakdowns. Undercounts (Hermes) and missing caps (OpenClaw) indicate the ecosystem is still catching up to cloud-native cost observability norms.

5. **macOS support is a reputational risk.** Both projects have unresolved macOS-specific bugs (launchd, plist, file paths). As Apple devices dominate developer desktops, neglecting macOS parity will create a vocal, frustrated user segment.

6. **Community wants standards, not ad-hoc fixes.** The filename encoding issue (#48788) and skill protection policy (#27997) both call for centralized, framework-level solutions rather than per-adapter workarounds. This signals a maturation from “build fast” to “build right.”

**For AI agent developers:** The data suggests that **session reliability, skill security, and cross-platform deployment** are the three non-negotiable investment areas. The current landscape rewards projects that can deliver a stable, secure, multi-platform experience over those that ship the widest feature set first.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-09

## 1. Today's Overview
The project is experiencing a period of **very high activity**, with 50 issues and 50 pull requests updated in the last 24 hours. 46 issues remain open alongside 46 open PRs, and only 4 items were closed/merged in each category – suggesting a **growing backlog** and heavy community engagement. No new releases were published today. The high number of open items indicates active triage and ongoing work, but also reveals friction points in reliability (Docker, macOS launchd, Matrix gateway) and user experience (clipboard, cost tracking, UI state bugs). The maintainers appear focused on stabilising the gateway and desktop app ahead of a probable upcoming release.

## 2. Releases
**No new releases** were published on 2026-06-09. The latest available version remains the previous one (v0.16.0, as inferred from issue references). Users should monitor upcoming releases for fixes to the high-severity bugs reported today.

## 3. Project Progress
Today **4 pull requests were merged or closed** (details not in the top‑20 list), while the remaining 46 remain open. Notable open PRs that signal progress toward specific fixes:
- **#42555** (fix gateway planned-stop marker for systemd) – addresses clean shutdown for systemd users.
- **#42554** (fix cost tracking undercounts) – three root causes identified and patched (gateway drops token fields, pricing alias, missing API call costs).
- **#42553** (kanban_db migration safety guard) – prevents duplicate-column errors under concurrent workers.
- **#42552** (cron conditional MCP init and robust datetime parsing) – improves cron job reliability.
- **#42548** (title generator timeout) – prevents blocking when upstream provider is slow.
- **#42514** (Matrix recovery key to file instead of logging) – security hardening.
- **#42488** (subprocess timeout in managed_uv.py) – prevents CLI hangs on network stalls.

Several other PRs today add features (resizable terminal pane, platform-aware core tool deferral, web search cascade backend, MCP catalog addition). These indicate a dual focus on fixing critical bugs and incrementally improving the developer/end‑user experience.

## 4. Community Hot Topics
The most active issues (by comment count) revolve around **core reliability and configuration pain points**:

- **#27997** (7 comments) – *Declarative Skill Protection Policy*: Community strongly desires a single source of truth for skill safety rules. The problem is spread across 6+ files with inconsistent enforcement. This feature would reduce accidental data leaks and simplify policy administration.
- **#24860** (6 comments, 1 👍) – *Dashboard Chat paste broken*: Ctrl+V and image paste do not work in the TUI backend. This is a frequent user annoyance that blocks efficient data entry.
- **#34457** (6 comments, 3 👍) – *s6-log lock collision in multi-container setups*: Docker users are hitting an endless log crash loop when sharing a volume between gateway and dashboard containers. This is a major roadblock for production deployments.
- **#30399** (6 comments, 3 👍) – *Matrix gateway missing pip package*: The official Docker image cannot run the Matrix gateway because `mautrix[encryption]` is absent. Users are forced to build custom images.
- **#21549** (4 comments) – *launchd double‑spawn death spiral*: macOS users suffer an infinite restart loop when two gateway instances start simultaneously. The issue has been open for a month with no fix merged.
- **#42130** (4 comments, closed) – *OpenRouter authentication header missing*: A setup bug that left users unable to use OpenRouter at all. Was closed today, likely indicating a fix was merged outside the top‑20 list.

Underlying needs: **simplified configuration, consistent Docker experience, and robust macOS support**.

## 5. Bugs & Stability
Several high‑ and medium‑severity bugs were reported or updated today:

**P1 (Critical)**
- **#21549** – *launchd double‑spawn death spiral*: Second gateway instance exits with code 1, causing macOS to restart indefinitely. No fix PR yet (PR #42555 only addresses systemd).  
- **#42449** – *delegate_task corrupts parent context_length via shared singleton*: Child agent overwrites parent’s ChatCompressor, leading to silent context corruption. No fix PR yet.  
- **#42524** – *macOS 26 gateway start exits with launchctl exit 5*: Falls back to detached process, breaking proper process management. Reported today.  

**P2 (High)**
- **#34457** – *s6-log lock loop* (Docker). Fix still pending.  
- **#30399** – *Matrix gateway missing package* (Docker).  
- **#24860** – *Dashboard paste broken*.  
- **#42120** – *Incomplete turn content lost on stop button*: User loses partial streamed response.  
- **#42405** – *Memory at capacity → zero‑match retry loop → silent hang*: Agent never responds to user.  
- **#42376** – *launchctl bootstrap broken on macOS 26.5.1* due to plist `LimitLoadToSessionType`.  

**P3 (Moderate)**
- **#41898** – Assistant response flashes and disappears with NVIDIA NIM provider.  
- **#42466** – Cron job “cannot schedule new futures” race with Hindsight memory.  
- **#42409** – Artifacts timestamps render as Jan 1970 (epoch‑seconds passed to millisecond constructor).  
- **#42431** – Desktop Files panel always ENOENT in remote mode.  
- **#42401** – Prompts discarded when navigating away from chat screen.  

**Fixes in progress:** PR #42554 directly addresses cost tracking bug #42477; PR #42514 hardens Matrix recovery key logging; PR #42488 adds subprocess timeouts; PR #42543 caps web search timeouts.

## 6. Feature Requests & Roadmap Signals
The following feature requests received attention today and are strong candidates for inclusion in the next release:

- **#27997** – *Declarative Skill Protection Policy*: Centralised, consistent safety rules for skills. Expected to be high priority given the security implications.
- **#38357** – *Show sessions from all profiles in Desktop sidebar*: Multi‑profile users want a unified session list. Simple UX improvement.
- **#42506** – *Add usememos as official memory provider*: Lightweight note‑taking alternative. Community interest is growing.
- **#41988** – *Default sampling params for custom local providers*: Currently no way to set temperature/top_p/top_k for local servers. Essential for advanced users.
- **#16675 and #38641** – *WeCom (WeChat Work) improvements*: Provide instant acknowledgement and streaming support. Niche but valued by Chinese users.
- **#12020** – *Toggle for hermes.tool.progress events in API response*: Needed for OpenAI‑compatible front‑end compatibility. Open since April.

Given the volume of stability work, the next version will likely focus on **skill safety, cost tracking, macOS reliability, and user‑experience polish**. The Declarative Skill Protection Policy (#27997) and default sampling params (#41988) seem most road‑mappable.

## 7. User Feedback Summary
Real pain points expressed by the community:

- **macOS users** are especially frustrated: launchd death spiral (#21549), plist issues on macOS 26 (#42376, #42524), and missing OpenRouter support (#42130) suggest the macOS experience is lagging behind Linux.
- **Docker users** face an unusable Matrix gateway (#30399) and log lock loops (#34457) – blocking containerised production use.
- **Desktop app users** report a broken paste (#24860), lost content on stop (#42120), disappearing prompts (#42401), and incorrect timestamps (#42409). The desktop app is still maturing rapidly.
- **Advanced users** are concerned about missing default sampling params for local models (#41988) and inadequate memory handling (#42405). The “memory at capacity hang” bug is a showstopper for heavy memory users.
- **Cost tracking** is essentially non‑functional for many (see #42477, PR #42554), undermining trust in usage analytics.

Satisfaction signals: The community is actively contributing PRs (50 open) and engaging in thoughtful feature discussion (7‑comment threads). The high number of contributions suggests the project remains healthy and responsive.

## 8. Backlog Watch
Several important issues have remained unanswered or unassigned for extended periods:

- **#12020** – *Toggle for progress events* (created 2026-04-18, 2 comments). No maintainer response. Affects all OpenAI‑compatible front‑end integrations.
- **#16675** – *WeCom instant acknowledgement* (created 2026-04-27, 1 comment). No activity.
- **#21549** – *launchd double‑spawn death spiral* (created 2026-05-07, 4 comments). No official fix merged despite being P1 critical.
- **#24860** – *Dashboard paste broken* (created 2026-05-13, 6 comments). No fix PR visible.
- **#27997** – *Declarative Skill Protection Policy* (created 2026-05-18, 7 comments). Feature request with strong consensus, but no PR yet.
- **#30399** – *Matrix gateway missing package* (created 2026-05-22, 6 comments). No Docker image update.

These items, if left unattended, risk eroding confidence in the project’s responsiveness. The first three represent **blocking bugs** for significant user groups (macOS, paste users, WeCom). Maintainers should prioritise commenting or assigning to reassure the community.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*