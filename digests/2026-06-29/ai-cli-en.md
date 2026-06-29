# AI CLI Tools Community Digest 2026-06-29

> Generated: 2026-06-29 03:31 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# AI CLI Developer Tools: Cross-Tool Comparison Report
**Date:** 2026-06-29 | **Analyst:** Senior Technical Analyst, AI Developer Tools Ecosystem

---

## 1. Ecosystem Overview

The AI CLI tools development landscape is characterized by rapid iteration on agentic workflows, but the community is increasingly vocal about **cost control** and **operational reliability** as core pain points. Both Claude Code and OpenAI Codex face parallel issues—uncontrolled token burn, session continuity failures, and authentication friction—while pursuing distinct architectural philosophies. Claude Code’s community is driving a **plugin ecosystem** and **policy-gated tool execution**, whereas OpenAI Codex’s community is demanding **non-blocking startup** and **usage transparency**. The tools are converging on multi-agent orchestration, but diverging in how they handle safety, extensibility, and desktop-vs-CLI parity. Developers are gravitating toward whichever tool offers better **cost predictability** and **session durability** for long-running tasks.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Hot Issues (last 24h)** | 10 selected (high severity) | 10 selected (mixed severity) |
| **Total Comments on Top Issues** | ~310 combined | ~283 combined |
| **Top Issue Engagement** | #63875 (110 👍, 72 comments) | #28224 (404 👍, 99 comments) |
| **Open PRs (last 24h)** | 5 (including 1 meta PR) | 10 (heavy engineering activity) |
| **New Releases** | None | None |
| **Critical Security/Cost Bugs** | 3 active (subagent recursion, stale cache, workflow overrun) | 1 active (SQLite log churn, mitigated but unresolved) |
| **Feature Requests (trending)** | Plugin ecosystem, session persistence, cost visibility | Configurable context budgets, non-blocking startup, usage transparency |

**Observation:** Claude Code shows higher engagement on acute bugs (cost leaks, infinite recursion), while OpenAI Codex shows sustained pressure on a single high-visibility issue (SSD writes). OpenAI Codex has a higher PR throughput, suggesting active engineering investment.

---

## 3. Shared Feature Directions

Multiple requirements appear across both tool communities, indicating industry-wide convergence:

| Shared Need | Claude Code Signals | OpenAI Codex Signals |
|---|---|---|
| **Cost & Budget Controls** | #68619 (recursion), #70459 (stale cache), #72127 (workflow overrun) — 3 distinct cost bugs | #28224 (log churn impacting SSD), #30510 (inaccurate token usage) |
| **Session Continuity & Persistence** | #72012 (lost conversation on reopen), #72121 (save chat as skill) | #21839 (re-approval after update), #30515 (automation clutter) |
| **Non-blocking/Async Startup** | Implicit demand from workflow tool behavior (#72127) | #30500, #30509 (MCP non-blocking for reviews), #30399 (async startup orchestration) |
| **Plugin/Agent Extensibility** | #72037 (handover), #72014 (protect-mcp), #42142 (desktop /plugin) | #30493 (multi-agent hint config), #30516 (agent logging) |
| **Model Compatibility Guards** | N/A (single-model focus) | #30224, #30406, #30422 (header blocking GPT-5.5), #30487 (fallback from unsupported effort) |
| **Usage Transparency** | #72035 (show context window), #1757 (re-auth friction) | #28161 (reset expiration), #30488 (redemption picker UI), #30510 (token accuracy) |

**Takeaway:** The top shared theme is **uncontrolled cost/token consumption**—both communities are demanding better visibility, gating, and guardrails for agentic spending. Session durability is the second priority.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Core Focus** | Plugin-driven extensibility; deep agentic workflows with subagents | Stable desktop/TUI experience; enterprise integration (MCP, Slack) |
| **Target User** | Power CLI users, plugin developers, cost-sensitive individual developers | Pro subscribers, enterprise teams, users needing multi-model support (GPT-5.4/5.5) |
| **Safety Approach** | Policy gates (Cedar-based, `protect-mcp`); fail-closed enforcement | Sandbox restrictions (Guardian); write-approval modes; review isolation |
| **Multi-Agent Architecture** | Subagent spawning with recursion control (buggy); handover plugin for LLM-to-LLM context | Multi-agent V2 with explicit delegation guidance (PR #30511); async MCP startup |
| **Desktop vs. CLI Parity** | CLI leads; desktop lacks `/plugin`, `/cowork` history (#42142) | App-focused; CLI reports packaging issues (#28402) |
| **Authentication Model** | Daily re-auth prompts (#1757); persistent friction after 1 year | Update-triggered re-approval (#21839); less frequent complaints |
| **Performance Issues** | TUI scroll regressions, IntelliJ EDT violations, mouse-click bugs | macOS `syspolicyd` CPU loops, Windows freezes, SSD log churn |
| **Community Sentiment** | High frustration on cost bugs; optimism on plugin ecosystem | Fatigue on persistent log churn; appreciation for transparency PRs |

**Strategic Insight:** Claude Code is betting on **extensibility** and **policy enforcement** as its differentiators, accepting complexity in return for power. OpenAI Codex is doubling down on **stability** and **user experience**—reducing friction in startup, reviews, and authorization. The choice between them depends on whether a team values plugin flexibility (Claude) or predictable reliability (Codex).

---

## 5. Community Momentum & Maturity

| Indicator | Claude Code | OpenAI Codex |
|---|---|---|
| **Community Size (estimated)** | Larger issue volume (10 selected from many); higher engagement per issue | Smaller issue count but high upvote totals on #28224 (404 👍) |
| **Iteration Velocity** | Moderate (0 releases today, 5 PRs) | High (10 PRs today, focused on non-blocking and UI) |
| **Bug Resolution Time** | Mixed—#1757 (auth) open 1 year; #63875 (tool parse) still active | Slow for #28224 (partial fix after multiple merges); #20214 (Windows freeze) long-standing |
| **Feature Maturity** | Plugin ecosystem is emerging but fragile—no marketplace, desktop gap | MCP integration is active but blocking; multi-agent V2 in refinement |
| **Community Sentiment** | **Frustrated but engaged** —users filing detailed cost-bug reports and plugin PRs | **Stable but weary** —users appreciate fixes but tired of recurring log/performance issues |

**Assessment:**
- **Claude Code** has a more **volatile, high-energy** community. It is rapidly iterating on new concepts (handover, policy gates) but accumulating technical debt in cost control and session stability.
- **OpenAI Codex** has a **steady, enterprise-oriented** community. It is methodically grinding down high-priority issues (log churn, startup latency) with structured PRs, but at a slower pace that frustrates power users.

Both tools are **mature in core functionality** but are still **maturing in operational reliability**—cost leaks and session failures are premature for products charging per-token.

---

## 6. Trend Signals

1. **Cost as a Feature, Not a Side Effect** — The single loudest signal across both communities: users want *explicit, gated control* over token spending. Claude Code’s three simultaneous cost bugs (recursion, stale cache, workflow overrun) and OpenAI Codex’s SSD panic are early warnings. Vendors that fail to build budget visibility, authorization gates, and fail-stop mechanisms will lose trust.

2. **Non-blocking by Default** — OpenAI Codex is leading a push toward async startup (MCP, reviews, subagents running in background). Users reject linear blocking. Expect all CLI tools to adopt lazy initialization, parallel orchestration, and progress indicators for background tasks.

3. **Authentication Fatigue** — Claude Code’s year-old daily re-auth bug (#1757) persists, while OpenAI Codex has periodic re-approval after updates. This is a silent churn driver—users will switch tools if login friction is not eliminated.

4. **Context Budget Transparency** — Both communities demand visibility into what occupies their context window and how much it costs. Hardcoded percentages (OpenAI Codex’s 2% skill limit) and stale precompute summaries (Claude Code’s auto-compaction) are unacceptable. Expect **debug commands** and **configurable budgets** to become table stakes.

5. **Plugin/MCP Ecosystems Need Safety** — The emergence of policy-gated tool execution (Claude Code’s `protect-mcp`, OpenAI Codex’s Guardian updates) signals a shift from *permissive* to *fail-closed* security for third-party tools. Developers building plugins should expect **signature verification**, **policy decision receipts**, and **sandbox enforcement**.

6. **Session as a First-Class Object** — Losing conversation context on reopen (#72012) or failing to persist session IDs across invocations is no longer acceptable. The community is demanding **named, durable, inspectable sessions** that can be resumed, forked, and shared (e.g., handover plugin #72037).

7. **Desktop vs. CLI Parity is Non-Negotiable** — Feature gaps (Claude Code desktop missing `/plugin`, OpenAI Codex CLI packaging broken on Apple Silicon) create confusion and distrust. Teams evaluating these tools for deployment should prefer whichever form factor matches their fleet, but monitor parity timelines.

---

## Summary for Decision-Makers

| Factor | Recommendation |
|---|---|
| **If you need maximum plugin flexibility** | Claude Code (but monitor cost-control fixes) |
| **If you need stable, predictable operation** | OpenAI Codex (but verify SSD impact on your hardware) |
| **If you deploy to teams >10 users** | Wait for cost gates and session durability fixes in either tool |
| **If you are building on MCP** | Both work; prefer OpenAI Codex for MCP startup controls |
| **If cost predictability is critical** | Neither tool is ready—build explicit budget monitoring wrappers |

**Bottom Line:** Both tools are in a **quality-of-life maturation phase**—core workflows work, but operational sharp edges (cost, sessions, auth) remain. The community is voting with bug reports and PRs. The vendor that ships budget controls and session durability first will win the loyalty of professional developers.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-06-29 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The community's most-discussed pull requests reveal a dual focus: **fixing the skill-creation evaluation pipeline** and **submitting new domain-specific skills**. Below are the 7 most-attended PRs by comment volume and cross-references.

| Rank | PR | Skill / Focus | Status | Key Discussion Theme |
|------|----|---------------|--------|----------------------|
| 1 | [#1298](https://github.com/anthropics/skills/pull/1298) | `run_eval.py` recall=0% fix | **OPEN** | Pipeline reports 0% recall for all descriptions; community independently reproduced (#556, #1169, #1061). Fix installs eval artifact as real skill, adds Windows stream reading, trigger detection, parallel workers. |
| 2 | [#514](https://github.com/anthropics/skills/pull/514) | **document-typography** — typographic quality control for generated docs | **OPEN** | Orphan/widow prevention, numbering alignment. Addresses quality gap in AI-generated documents. |
| 3 | [#486](https://github.com/anthropics/skills/pull/486) | **ODT skill** — OpenDocument creation, template filling, parse ODT→HTML | **OPEN** | First OpenDocument format skill; covers .odt, .ods, LibreOffice interoperability. |
| 4 | [#210](https://github.com/anthropics/skills/pull/210) | **frontend-design** — clarity and actionability overhaul | **OPEN** | Revises existing skill for single-conversation usability; community debated instruction specificity vs. open-ended guidance. |
| 5 | [#83](https://github.com/anthropics/skills/pull/83) | **skill-quality-analyzer** + **skill-security-analyzer** (meta-skills) | **OPEN** | Two evaluation skills: quality across 5 dimensions (structure, documentation, etc.) and security scanning. |
| 6 | [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** — full-stack testing methodology skill | **OPEN** | Covers Testing Trophy model, AAA pattern, React Testing Library, Playwright E2E; strong community interest in quality tooling. |
| 7 | [#154](https://github.com/anthropics/skills/pull/154) | **shodh-memory** — persistent cross-conversation memory for agents | **OPEN** | Introduces `proactive_context` calls, rich memory structure, context window management. |

**Notable Pattern**: The #1 most-discussed item is *not a new skill* but rather a critical bug fix in `run_eval.py` — the evaluation pipeline that powers skill description optimization. This bug (0% recall reported for every description, [#556](https://github.com/anthropics/skills/issues/556)) has been independently reproduced by 10+ users across Windows and Linux, and multiple PRs ([#1298](https://github.com/anthropics/skills/pull/1298), [#1323](https://github.com/anthropics/skills/pull/1323), [#1099](https://github.com/anthropics/skills/pull/1099), [#1050](https://github.com/anthropics/skills/pull/1050)) attempt to resolve it — indicating a **pipeline reliability crisis** that is blocking all skill optimization work.

---

## 2. Community Demand Trends

From the Issues tracker, five clear demand vectors emerge:

### 🔴 Critical: Pipeline Reliability (29 comments, 7 👍)
- **Issue [#556](https://github.com/anthropics/skills/issues/556)**: `run_eval.py` 0% trigger rate — render's the description optimization loop useless. Directly blocks any skill author from effectively tuning their SKILL.md descriptions. Connected to [#1169](https://github.com/anthropics/skills/issues/1169) (recall=0% even on literal slash-command queries) and [#1061](https://github.com/anthropics/skills/issues/1061) (Windows compatibility failures including PATHEXT, cp1252 encoding, and select-on-pipes crashes).

### 🔴 Security & Trust Boundary (29 comments, 2 👍)
- **Issue [#492](https://github.com/anthropics/skills/issues/492)**: Community skills distributed under the `anthropic/` namespace impersonate official skills. Users may grant elevated permissions to what they believe are Anthropic-vetted skills. This is the **most-commented issue** in the entire repository.

### 🟡 Organizational Features (14 comments, 7 👍)
- **Issue [#228](https://github.com/anthropics/skills/issues/228)**: Request for org-wide skill sharing without manual file transfer. Currently requires Slack/Teams + manual upload per user. A shared skill library or direct sharing link would unblock enterprise adoption. **Highest +1 count in Issues** at 7.

### 🟡 Skill Duplication & Namespace Collisions (6 comments, 9 👍)
- **Issue [#189](https://github.com/anthropics/skills/issues/189)**: Installing both `document-skills` and `example-skills` plugins creates duplicate skills because they contain identical content. **Highest reaction count** (9 👍) indicating broad frustration.

### 🟢 Emerging Skill Directions (multiple proposals)
- **Agent governance** ([#412](https://github.com/anthropics/skills/issues/412)): Policy enforcement, threat detection, trust scoring, audit trails for agent systems.
- **Compact memory** ([#1329](https://github.com/anthropics/skills/issues/1329)): Symbolic notation for compact agent state to reduce context window consumption.
- **MCP exposure** ([#16](https://github.com/anthropics/skills/issues/16)): Expose Skill capabilities as MCP (Model Context Protocol) endpoints.

---

## 3. High-Potential Pending Skills

These open PRs have active community engagement and are likely to land soon:

1. **[skill-quality-analyzer / skill-security-analyzer](https://github.com/anthropics/skills/pull/83)** (PR #83, created 2025-11-06, updated 2026-01-07) — Meta-skills for evaluating skill quality and security. Matches the top community concern (#492) around trust boundaries. Likely to be merged following security audit resolution.

2. **[document-typography](https://github.com/anthropics/skills/pull/514)** (PR #514, created 2026-03-04, updated 2026-03-13) — Solves a universal pain point (orphan words, widowed headers in AI-generated documents). Low complexity, high impact.

3. **[ODT skill](https://github.com/anthropics/skills/pull/486)** (PR #486, created 2026-03-01, updated 2026-04-14) — Fills an obvious format gap alongside the existing PDF and DOCX skills. Interoperability with LibreOffice ecosystem.

4. **[shodh-memory](https://github.com/anthropics/skills/pull/154)** (PR #154, created 2025-12-19, updated 2026-03-03) — Persistent memory across conversations. Addresses the "stateless agent" limitation; complements the proposed compact-memory skill (#1329).

5. **[AppDeploy](https://github.com/anthropics/skills/pull/360)** (PR #360, created 2026-02-09, updated 2026-05-04) — Deploys full-stack web apps from Claude. Bridges the gap between code generation and deployment — a workflow the community clearly wants.

6. **[testing-patterns](https://github.com/anthropics/skills/pull/723)** (PR #723, created 2026-03-22, updated 2026-04-21) — Comprehensive testing methodology skill. The Testing Trophy model and Playwright E2E coverage fill a gap in the existing skills collection.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is a reliable, secure, and cross-platform skill development pipeline** — the top three discussion threads all center on pipeline bugs (run_eval 0% recall, Windows crashes, trust boundary abuse), not on any single skill domain, indicating that the skill authoring experience itself is the primary bottleneck to ecosystem growth.

---

# Claude Code Community Digest — 2026-06-29

## Today's Highlights

The community is sounding the alarm on compounding cost bugs: auto-compaction is holding stale ~200k-token prefixes, and subagent recursion is burning through entire plans without warning. A critical `workflow` tool incident today consumed a 5x plan in 5 minutes with no authorization prompt, while the desktop app continues to lack basic `/plugin` support. No new releases landed today, but two plugin PRs (handover and policy-gated MCP protection) signal growing demand for extensibility.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues (10 selected)

**1. [#63875 — Tool call parse error interrupts sessions (72 comments, 👍110)](https://github.com/anthropics/claude-code/issues/63875)**  
*Recurring error: "The model's tool call could not be parsed (retry also failed)"*  
The most-upvoted open bug this week. During normal sessions, Claude Code intermittently aborts mid-task with a tool-call parse failure. Cross-platform (Windows reported), high frustration due to lost progress.

**2. [#1757 — Constant re-authentication required (73 comments, 👍63)](https://github.com/anthropics/claude-code/issues/1757)**  
*[BUG] Claude code requires users to constantly login*  
Users report daily OAuth prompts despite having authenticated the night before. Opened June 7, still active a year later — a persistent user experience regression for the `auth` area.

**3. [#68619 — Subagent spawning infinite recursion burns tokens (26 comments, 👍8)](https://github.com/anthropics/claude-code/issues/68619)**  
*[CRITICAL] Subagent spawning and subagent pattern bugs trigger infinite recursion, infinite token usage*  
Agents spawn child agents 50+ levels deep, ignoring `CLAUDE_CODE_FORK_SUBAGENT=0`. Permission denials trigger more spawning instead of stopping. Compounds with HTTP-based file fetching from GitHub repos.

**4. [#70459 — Auto-compaction cost bugs: stale precompute + cache-miss (4 comments, 👍3)](https://github.com/anthropics/claude-code/issues/70459)**  
*Stale precompute keeps ~200k tokens verbatim, and that prefix is repeatedly cache-created instead of cache-read*  
Two compounding problems: `/compact` reuses a ~47-minute-old precompute summary, then the stale prefix is re-ingested (cache-created) on every request instead of cache-read. Directly impacts API bill.

**5. [#72127 — Workflow tool burned entire 5x plan in ~5 minutes (3 comments, 👍0)](https://github.com/anthropics/claude-code/issues/72127)**  
*Workflow tool burned entire 5x plan in ~5 minutes with no warning or authorization prompt*  
Filed today. User rejected an Agent tool call, said "continue," and Claude silently launched 8–10 parallel research agents that consumed the whole budget. No permission gate fired.

**6. [#42142 — Desktop app missing `/plugin` command (9 comments, 👍8)](https://github.com/anthropics/claude-code/issues/42142)**  
*Claude Code Desktop Doesn't Have /plugin Command and cannot add plugin marketplaces*  
Feature gap between CLI and desktop editions. Claude hallucinates plugin support when users ask — a documentation and parity issue now 3 months old.

**7. [#59979 — Mouse wheel scrolls input history instead of transcript (11 comments)](https://github.com/anthropics/claude-code/issues/59979)**  
*2.1.143 regression: mouse wheel scrolls input history instead of chat transcript (Windows)*  
CLOSED but noteworthy — a TUI regression that inverted scroll behavior. Was resolved, but indicates fragility in the input-history vs. chat-scroll boundary.

**8. [#72121 — Save finished chat as skill or agent in one click (4 comments)](https://github.com/anthropics/claude-code/issues/72121)**  
*Save a finished chat as a skill or agent in one click*  
Filed yesterday, already gaining traction. Users want to promote ad-hoc sessions to reusable skills/agents without manually constructing prompt templates.

**9. [#72012 — Agent View: reopening stopped session loses conversation (3 comments)](https://github.com/anthropics/claude-code/issues/72012)**  
*Reopening a stopped/completed background session respawns with a new session-id, prior conversation is lost (v2.1.195, macOS)*  
Session continuity bug in Agent View — blocks multi-session workflows via the fleet roster.

**10. [#72188 — Terminal focus-in consumed as permission denial (1 comment, 👍1)](https://github.com/anthropics/claude-code/issues/72188)**  
*Terminal focus-in event consumed as prompt denial in permission dialog*  
Filed today. A terminal focus-in escape sequence or mouse click is interpreted as a "deny" action in permission prompts. Under-reported but dangerous — could silently block legitimate tool calls.

---

## Key PR Progress (all 5 open/updated in last 24h)

**1. [#72037 — Add handover plugin](https://github.com/anthropics/claude-code/pull/72037)**  
Exports session context as structured Markdown for LLM-to-LLM handoffs. Enables sharing context across Claude sessions or with other models — a direct response to context-loss complaints.

**2. [#72014 — Add protect-mcp plugin](https://github.com/anthropics/claude-code/pull/72014)**  
Fail-closed Cedar policy gate with signed receipts. Blocks policy-violating tool calls before execution and produces offline-verifiable decision receipts. Sits alongside `security-guidance` but enforces rather than warns.

**3. [#62315 — Fix hookify event filtering in pre/post hooks](https://github.com/anthropics/claude-code/pull/62315)**  
CLOSED. Patches event filtering in the hook system. Relevant for anyone building custom hooks that depend on precise event routing.

**4. [#41447 — Open source Claude Code (meta PR)](https://github.com/anthropics/claude-code/pull/41447)**  
Still open. Closes 5 related issues (#59, #456, #2846, #22002, #41434). Community continues to push for full source availability.

**5. [#72000 — Docs: update plugin install instructions](https://github.com/anthropics/claude-code/pull/72000)**  
Updates installation docs to recommend official installers. Small but signals maturation of the plugin ecosystem.

---

## Feature Request Trends

- **Plugin & Hooks Ecosystem**: Multiple requests for first-class plugin marketplaces, `/plugin` parity on desktop, and ability to save chats as skills/agents (e.g., [#42142](https://github.com/anthropics/claude-code/issues/42142), [#72121](https://github.com/anthropics/claude-code/issues/72121)).
- **Agent View & Session Management**: Demands for persistent background session IDs, resumption without conversation loss, and better UI for managing concurrent agents ([#72012](https://github.com/anthropics/claude-code/issues/72012), [#72035](https://github.com/anthropics/claude-code/issues/72035)).
- **Cost Visibility & Control**: Requests for debug commands showing full context-window contents ([#72035](https://github.com/anthropics/claude-code/issues/72035)), plus obvious need for budget gates on `workflow` and subagent spawning.
- **Authentication & Security**: Users want session persistence without daily re-auth, and better handling of false-positive security flags for legitimate local network tools ([#1757](https://github.com/anthropics/claude-code/issues/1757), [#72168](https://github.com/anthropics/claude-code/issues/72168)).
- **MCP & Extensibility**: Growing interest in policy-gated MCP tool execution (e.g., `protect-mcp` plugin) and structured context handoffs between LLM sessions.

---

## Developer Pain Points

1. **Authentication Friction** — [#1757](https://github.com/anthropics/claude-code/issues/1757): Daily re-login required despite stable sessions. TLS cert chain issues on platform.claude.com also breaking OAuth flows ([#71766](https://github.com/anthropics/claude-code/issues/71766)).
2. **Cost Leaks & Uncontrolled Token Burn** — [#68619](https://github.com/anthropics/claude-code/issues/68619), [#70459](https://github.com/anthropics/claude-code/issues/70459), [#72127](https://github.com/anthropics/claude-code/issues/72127): Subagent recursion, stale cache prefixes, and silent parallel workflow launches are draining plans with no authorization gates. Three separate cost bugs active simultaneously.
3. **Tool-Call Parsing Failures** — [#63875](https://github.com/anthropics/claude-code/issues/63875): Frequent "retry also failed" errors that abort in-progress work. Causes session instability for long-running tasks.
4. **Session Management Regressions** — [#72012](https://github.com/anthropics/claude-code/issues/72012), [#72171](https://github.com/anthropics/claude-code/issues/72171): Background tasks orphaned across invocations, session IDs not stable, prior conversations lost on reopen.
5. **Sandbox & Platform Incompatibilities** — [#64301](https://github.com/anthropics/claude-code/issues/64301): Bash sandbox (bubblewrap) corrupts `!` to `\!`; [#50674](https://github.com/anthropics/claude-code/issues/50674): Cowork fails on ARM64 despite passing readiness check.
6. **TUI & IDE Integration Glitches** — [#59979](https://github.com/anthropics/claude-code/issues/59979): Mouse scroll regression on Windows; [#72173](https://github.com/anthropics/claude-code/issues/72173): `CLAUDE_CODE_DISABLE_MOUSE_CLICKS` broke text selection; [#71455](https://github.com/anthropics/claude-code/issues/71455): IntelliJ EDT violation regressed.
7. **Desktop vs. CLI Feature Gap** — [#42142](https://github.com/anthropics/claude-code/issues/42142): Desktop app lacks `/plugin`, `/cowork` history, and chat history display — the CLI remains the superior experience.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

## OpenAI Codex Community Digest — 2026-06-29

---

### Today’s Highlights

No releases landed in the last 24 hours. The community remains focused on a persistent cluster of SQLite log‑churn bugs that, despite recent mitigations (PRs #29432 and #29457), continue to trouble macOS and Windows users with excessive SSD writes. Meanwhile, a new wave of reports (#30224, #30406, #30422) shows that the `X‑OpenAI‑Internal‑Codex‑Responses‑Lite` header is blocking GPT‑5.5 usage for many Plus subscribers. On the Pull Request side, OpenAI engineers are prioritising non‑blocking MCP startup, review isolation, and richer usage‑reset UI.

---

### Releases

None in the last 24 hours.

---

### Hot Issues

1. **#28224 – SQLite feedback logs can write ~640 TB/year**  
   *99 comments, 404 👍*  
   The most visible bug of the month. Three merges (released in `0.142.0`) cut 85% of log writes, but follow‑up reports (#29532, #30405) show residual churn still affects macOS and Windows. SSD endurance remains a concern.  
   [openai/codex Issue #28224](https://github.com/openai/codex/issues/28224)

2. **#30224 – “This model is not supported” with `X‑OpenAI‑Internal‑Codex‑Responses‑Lite`**  
   *53 comments, 19 👍*  
   Multiple users (see also #30406, #30422) report that GPT‑5.5 fails in the Codex App when this internal header is present, while GPT‑5.4 and the ChatGPT app work fine. A server‑side fix is expected.  
   [openai/codex Issue #30224](https://github.com/openai/codex/issues/30224)

3. **#25719 – macOS `syspolicyd` / `trustd` CPU and memory runaway**  
   *36 comments, 55 👍*  
   Codex Desktop on Apple Silicon triggers a persistent `trustd`/`syspolicyd` loop, consuming CPU and memory. Users report it as a major daily annoyance.  
   [openai/codex Issue #25719](https://github.com/openai/codex/issues/25719)

4. **#29532 – Residual SQLite TRACE log churn after `rust‑v0.142.0`**  
   *24 comments, 7 👍*  
   The partial fix from #29432/#29457 didn’t fully resolve the issue on macOS. `logs_2.sqlite` WAL still sees high‑frequency writes.  
   [openai/codex Issue #29532](https://github.com/openai/codex/issues/29532)

5. **#20214 – Windows 11 freezes/stutters with sufficient resources**  
   *20 comments, 38 👍*  
   A long‑standing complaint about UI freezes on Win11 despite adequate RAM/CPU. Users are calling for a dedicated performance pass.  
   [openai/codex Issue #20214](https://github.com/openai/codex/issues/20214)

6. **#19679 – Make skills context budget configurable**  
   *15 comments, 23 👍*  
   Skills descriptions are currently hardcoded to 2% of the context window. When many skills are installed, descriptions get truncated without user control.  
   [openai/codex Issue #19679](https://github.com/openai/codex/issues/19679)

7. **#30364 – GPT‑5.5 reasoning token clustering at 516/1034/1552**  
   *14 comments, 13 👍*  
   A data‑driven report showing that GPT‑5.5 responses are locked to fixed reasoning‑token counts, potentially degrading complex task performance.  
   [openai/codex Issue #30364](https://github.com/openai/codex/issues/30364)

8. **#21839 – Pre‑existing sessions requiring re‑approval**  
   *10 comments*  
   After an update, previously approved sessions now demand manual re‑approval, disrupting Pro users’ workflows.  
   [openai/codex Issue #21839](https://github.com/openai/codex/issues/21839)

9. **#13200 – `codex mcp login` fails for Slack MCP**  
   *8 comments, 55 👍*  
   Dynamic client registration is not supported, blocking Slack MCP integration. Enterprise users are particularly affected.  
   [openai/codex Issue #13200](https://github.com/openai/codex/issues/13200)

10. **#28161 – Show expiration dates for usage resets**  
    *4 comments, 38 👍*  
    Users want to know which reset credit will be consumed and when each expires, rather than just a count of “resets available.”  
    [openai/codex Issue #28161](https://github.com/openai/codex/issues/28161)

---

### Key PR Progress

1. **#30516 – Add explicit agent communication logging**  
   Introduces a unified JSON log format for agent start/end events, improving observability in multi‑agent workflows.  
   [openai/codex PR #30516](https://github.com/openai/codex/pull/30516)

2. **#30511 – Restore v1 delegation guidance**  
   Clarifies that “depth” or “research” requests do not authorise subagent spawning and that critical‑path work should stay local.  
   [openai/codex PR #30511](https://github.com/openai/codex/pull/30511)

3. **#30500 – Run reviews without unfinished MCP servers**  
   Review sessions now skip waiting for MCP OAuth handshake, allowing code review to start immediately while MCP initialises in the background.  
   [openai/codex PR #30500](https://github.com/openai/codex/pull/30500)

4. **#30509 – Allow review while MCP startup runs in the background**  
   Separates “turn active” from “MCP starting” states so that `/review` can proceed without blocking on MCP.  
   [openai/codex PR #30509](https://github.com/openai/codex/pull/30509)

5. **#30488 – Show reset details in redemption picker**  
   Implements the feature requested in #28161: loads and displays each reset credit’s expiry time and which credit will be consumed.  
   [openai/codex PR #30488](https://github.com/openai/codex/pull/30488)

6. **#30320 – Guardian Policy Update**  
   Clarifies sandbox restrictions (don’t apply to reviewed model) and ensures banned low‑severity actions are still denied.  
   [openai/codex PR #30320](https://github.com/openai/codex/pull/30320)

7. **#30482 – Add writes app approval mode**  
   A new `writes` approval mode: read‑only tools skip approval, all other tools prompt, providing finer control.  
   [openai/codex PR #30482](https://github.com/openai/codex/pull/30482)

8. **#30493 – Configurable multi‑agent mode hint text**  
   Allows deployments to pin a stable hint text for multi‑agent V2 instead of relying on model‑catalog state.  
   [openai/codex PR #30493](https://github.com/openai/codex/pull/30493)

9. **#30487 – Fall back from unsupported reasoning effort**  
   Prevents failed inference when a cross‑thread message requests a reasoning effort (e.g., `max`) that the model does not support.  
   [openai/codex PR #30487](https://github.com/openai/codex/pull/30487)

10. **#30480 – Fix duplicate unicode keyboard input**  
    Disables unused Kitty alternate‑key reporting to avoid duplicate characters in Windows Terminal and Warp.  
    [openai/codex PR #30480](https://github.com/openai/codex/pull/30480)

---

### Feature Request Trends

- **Configurable context budgets** – Users want the skills‑description percentage (currently hardcoded to 2%) to be adjustable, or at least provide warnings when budgets are exceeded.  
- **Usage‑limit transparency** – Multiple requests (#28161, #30510) ask for detailed breakdowns of reset credits, including expiration dates and per‑model consumption.  
- **Non‑blocking startup** – Issue #30399 synthesises demands for MCP, subagent, and startup orchestration to be fully async and observable, especially for multi‑machine workflows.  
- **Automation hygiene** – #30515 highlights that cron automations clutter the main conversation list; users want a separate view or grouping for automated runs.  
- **Model compatibility guards** – The recurring `X‑OpenAI‑Internal‑Codex‑Responses‑Lite` errors (#30224, #30406) are driving requests for graceful fallback or clearer error messages when a model cannot use internal optimisations.

---

### Developer Pain Points

- **SSD endurance from excessive logging** – Issues #28224, #29532, #30405 remain the top concern. Even after the 85% reduction, users on macOS and Windows still see `logs_2.sqlite` churn.  
- **Application freezes and stutters** – #20214 (Windows) and #25719 (macOS `syspolicyd`) cause daily interruptions despite ample system resources.  
- **MCP / subagent blocking** – Code review and general startup are delayed by MCP initialisation (#30500, #30509), and sub‑agents occasionally hang indefinitely (#30400).  
- **Model‑specific failures** – The `X‑OpenAI‑Internal‑Codex‑Responses‑Lite` header blocks GPT‑5.5 for many Plus subscribers, with no graceful fallback to GPT‑5.4.  
- **Inaccurate token usage** – #30510 reports that the desktop app displays outdated or inaccurate token/usage counts, making quota management unreliable.  
- **CLI packaging incompatibility** – #28402 shows the `aarch64‑apple‑darwin` binary links private system libraries (`liblzma`, `libbz2`), causing App Store rejection.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*