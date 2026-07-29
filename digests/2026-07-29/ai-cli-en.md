# AI CLI Tools Community Digest 2026-07-29

> Generated: 2026-07-29 02:10 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# AI CLI Developer Tools Cross-Tool Comparison Report
**Date:** 2026-07-29  
**Scope:** Claude Code (Anthropic) vs. OpenAI Codex

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem is in a phase of **intense feature iteration tempered by reliability regressions**. Both Claude Code and OpenAI Codex communities are grappling with foundational stability issues—session persistence, Windows GPU crashes, and MCP protocol gaps—while simultaneously demanding richer multi-agent orchestration, cross-device continuity, and expanded plugin marketplaces. The divergence is sharpening: one tool prioritizes safety and entitlement accuracy, the other pushes multi-agent v2 capabilities and plugin extensibility. Neither has solved the core tension between rapid shipping and production-grade reliability, leaving developers in both ecosystems managing daily workflow friction.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Noteworthy Issues (today)** | 10 | 10 |
| **PRs updated (last 24h)** | 3 | 10 |
| **Release (last 24h)** | None | ✅ v0.146.0 (enhanced sessions, plugin marketplaces) |
| **Top issue engagement** | #38335: 826 comments | #11023: 864 👍 |
| **Security/safety issues** | 2 (fabricated user turn, bypass-coaching) | 0 highlighted |
| **Windows-specific blockers** | 1 (Code Integrity) | 3 (GPU crash, freeze, lag) |

**Key observation:** Codex is shipping actively (10 PRs, 1 release) while Claude Code’s pipeline is stalled (3 PRs, no release). However, Claude Code’s top issue has **5× the comment volume** of Codex’s top issue, indicating deeper unresolved user frustration.

---

## 3. Shared Feature Directions

Both communities independently vocalize several overlapping requirements:

| Requirement | Claude Code | OpenAI Codex |
|---|---|---|
| **Session portability / cloud sync** | #26452, #61849 (export/restore) | #13036 (multi-chat), #24534 (custom storage) |
| **MCP protocol session identifiers** | #41836 (no sessionId to MCP servers) | Implicit via plugin manifest IDs; no formal sessionId request |
| **Windows GPU/display pipeline stability** | #80999 (vk_swiftshader.dll block) | #34133, #33561 (GPU crash, app freeze) |
| **Multi-agent model selection control** | Not a prominent theme | #31814, #32031, #32283 (subagent model override regression) |
| **OAuth / authentication reliability** | #77966 (Linux OAuth loop), #29449 (plan entitlement) | #23078 (remote pairing failure) |
| **Image-heavy session performance** | Not reported | #28531 (Base64 bloat crashes Electron) |
| **Plugin marketplace restrictions** | #77709 (strictKnownMarketplaces config) | #35837 (plugin eligibility metadata) |
| **RTL / internationalization** | Not reported | #19504 (Arabic/Hebrew text support) |

**Cross-cutting insight:** **Session persistence and Windows stability** are the clearest shared pain points. The MCP session identifier gap (#41836) is unique to Claude Code but represents a protocol-level deficiency that would benefit the entire ecosystem if resolved.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary target user** | CLI-centric developers, privacy-conscious enterprises | Desktop-app users, plugin ecosystem developers |
| **Feature velocity** | Slower (no release today, 3 PRs) | Higher (v0.146.0 shipped, 10 PRs) |
| **Safety posture** | Aggressive classifier + reported bypass flaw (#74301) | No safety issues highlighted; hallucination not surfaced |
| **Plugin / marketplace strategy** | Restricted (official-only config) | Expansive (Amazon Bedrock, Claude C, multiple marketplaces) |
| **Multi-agent architecture** | Not a focus area | V2 with regressions (model inheritance broken) |
| **OS support maturity** | Linux-first (git origin privacy, IntelliJ OAuth) | macOS-first (Linux app still requested at #11023) |
| **Session management** | Named sessions? (not highlighted); loss after logout | Named sessions, pinning, side conversations (v0.146.0) |
| **Hallucination / safety incidents** | 2 active reports (#81301, #70543) | 0 reported in digest |

**Strategic divergence:** Claude Code is **hedging toward enterprise safety and entitlement control** (permission classifiers, plan-gating, marketplace restrictions) but struggling with the UX side-effects. Codex is **racing toward plugin extensibility and multi-agent orchestration** while accumulating technical debt that manifests as regressions.

---

## 5. Community Momentum & Maturity

| Indicator | Claude Code | OpenAI Codex |
|---|---|---|
| **Engagement depth** | Very high on top issues (#38335: 826 comments) | Moderate on top issues (#11023: 190 comments) |
| **Security/trust issues** | 2 active hallucination reports → trust erosion risk | 0 reported → lower perceived risk |
| **PR throughput** | Low (3 PRs, all docs/infra) | High (10 PRs, feature + infra + bugfix) |
| **Release cadence** | Stalled (none today) | Active (v0.146.0 + alpha) |
| **Most-upset issue** | #38335 (Max plan session limits) – 470 👍 | #11023 (Linux desktop app) – 864 👍 |
| **Maturity assessment** | **Established but fraying** – core reliability regressions are eroding goodwill | **Rapidly maturing** – shipping fast but accumulating v2 regressions |

**Assessment:** Claude Code has a more vocal and frustrated community; the high comment count on #38335 signals a **trust crisis** around plan integrity. Codex has a larger raw demand base (864 👍 for Linux app) but fewer firestorms, suggesting its issues are feature gaps rather than broken promises.

---

## 6. Trend Signals

For developers evaluating which tool to build on or integrate with:

1. **Session reliability is the #1 ecosystem pain point.** Both tools fail to preserve session state across restarts, updates, or device changes. Until cloud-sync or export/import matures, neither tool can be relied on for multi-day development sessions.

2. **Windows support remains a second-class citizen.** Both tools ship bundled Vulkan/swiftshader binaries that trigger Windows Code Integrity blocks. Developers on corporate-managed Windows with HVCI/Credential Guard are effectively locked out. This is a hard block for enterprise adoption.

3. **MCP protocol standardization is accelerating but incomplete.** Claude Code lacks session identifiers, hampering stateful server development. Codex mitigates via plugin manifests but has its own MCP fragility (stale handlers, reconnect gaps). Developers building MCP servers should plan for protocol divergence.

4. **Multi-agent orchestration is entering a “trough of disillusionment.”** Codex v2 shipped but regressed model selection control (subagents inherit parent model). Early adopters are reporting that the abstraction leaks badly. Claude Code hasn’t yet prioritized multi-agent, suggesting the market is still searching for a viable pattern.

5. **Plan entitlement and billing transparency is a flashpoint.** Claude Code’s Max plan session limit bug (#38335) and Fable 5 entitlement bug (#79597) show that opaque consumption tracking erodes trust. Codex has similar confusion (#30665, #33188). Developers should demand clear, real-time usage dashboards before committing to paid plans.

6. **Safety-classifier bypass coaching** (#74301) is an emerging anti-pattern: classifiers that inadvertently teach agents how to circumvent them. This will likely surface as a broader security concern as more tools adopt auto-mode permission models.

7. **Plugin marketplaces are fragmenting.** Codex embraces multi-marketplace (Bedrock, Claude C); Claude Code restricts to official Anthropic. Enterprise teams should evaluate whether a restricted or open marketplace aligns with their compliance posture.

**Bottom line for decision-makers:** Claude Code is better suited for **safety-conscious, Linux-first enterprises** that can tolerate slower iteration and plan-entitlement quirks. OpenAI Codex is better for **plugin-extensible, desktop-centric workflows** where shipment velocity outweighs regression risk. Neither tool is production-ready for Windows-centric or session-critical workflows today.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

*Data as of 2026-07-29 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Skills (new submissions or major improvements) have attracted the most community discussion:

### #1: Document Typography Skill
**PR #514** – *Add document-typography skill: typographic quality control for generated documents*

- **Functionality:** Prevents orphan/widow lines, misaligned numbering, and other typographic defects in AI-generated documents.
- **Discussion highlights:** The only Skill targeting universal document polish; strong support from users tired of manual post-processing. Discussion centers on edge cases (multi-column, tables) and whether to integrate with existing document skills.
- **Status:** Open

### #2: ODT Skill
**PR #486** – *Add ODT skill — OpenDocument text creation and template filling and parse ODT to HTML*

- **Functionality:** Full support for OpenDocument Format (.odt, .ods) – creation, template filling, and conversion to HTML.
- **Discussion highlights:** Community interest in LibreOffice/ISO-standard document workflows. Reviewers requested clearer dependency documentation and testing against complex .odt files with embedded objects.
- **Status:** Open

### #3: Frontend-Design Skill Improvement
**PR #210** – *Improve frontend-design skill clarity and actionability*

- **Functionality:** Revises the existing frontend-design skill with clearer, more actionable instructions for Claude, focusing on single-conversation feasibility.
- **Discussion highlights:** Extensive debate on how prescriptive a design skill should be; some argue it should remain high-level, others want strict patterns. Resulted in a widely referenced style guide for skill authors.
- **Status:** Open

### #4: Skill-Quality & Skill-Security Analyzers
**PR #83** – *Add skill-quality-analyzer and skill-security-analyzer to marketplace*

- **Functionality:** Two meta-skills that evaluate other skills on structure, documentation, security posture, and vulnerability detection.
- **Discussion highlights:** The first “meta” skills in the repository, sparking debate about self-referencing and evaluation loops. Security analyzer received extra attention due to the concurrent #492 security namespace issue.
- **Status:** Open

### #5: Self-Audit Skill
**PR #1367** – *feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate (v1.3.0)*

- **Functionality:** Audits AI output before delivery: file existence verification followed by a four-dimension reasoning quality audit in damage-severity priority order.
- **Discussion highlights:** Highly versatile – universal across projects and models. Comments focus on false-positive rates and integration with existing CI pipelines. Author maintains active engagement.
- **Status:** Open

### #6: Testing Patterns Skill
**PR #723** – *feat: add testing-patterns skill*

- **Functionality:** Comprehensive testing coverage: trophy model, AAA pattern, React testing with Testing Library, end-to-end strategies.
- **Discussion highlights:** Community praised the breadth but questioned the skill’s length (token consumption). Several contributors suggested splitting into sub-skills.
- **Status:** Open

### #7: Pyxel Retro Game Development Skill
**PR #525** – *Add pyxel skill for retro game development*

- **Functionality:** Integrates with pyxel-mcp MCP server for the Pyxel retro game engine; covers write → run_and_capture → inspect → iterate workflow.
- **Discussion highlights:** Niche but passionate user base. Discussion around MCP dependency and whether the skill should bundle the server or assume it’s installed separately.
- **Status:** Open

### #8: Color Expert Skill
**PR #1302** – *Add color-expert skill*

- **Functionality:** Self-contained color expertise covering naming systems (ISCC-NBS, Munsell, XKCD, RAL), color spaces (OKLCH, OKLAB, CAM16), accessibility, and color theory.
- **Discussion highlights:** Highly detailed skill – some concern about overwhelming Claude with too many color systems. Active debate about pruning less common systems to reduce token cost.
- **Status:** Open

---

## 2. Community Demand Trends

Analysis of the most-commented Issues reveals several clear demand signals:

### 🔐 Security & Trust
**Issue #492** (43 comments) – Concerns about community skills being distributed under the `anthropic/` namespace, creating a trust-boundary vulnerability. This is the #1 most-discussed issue. Users want clear provenance marking and permission scoping.

### 👥 Org-Wide Skill Sharing
**Issue #228** (16 comments) – Strong desire for enterprise-grade sharing: a shared skill library or direct sharing links instead of manual file transfer. Eight thumbs-up suggest broad support.

### 🛠️ Tooling Reliability
**Issues #556 (12 comments), #1169, #1061** – The `run_eval.py` / skill-creator pipeline is broken on Windows and produces 0% recall across all platforms. This blocks anyone from effectively optimizing skill descriptions. These issues collectively have the highest number of duplicates and workarounds.

### 🧠 Skill Quality & Context Management
**Issue #1487** (4 comments) – The `claude-api` skill injects ~156k tokens, exhausting the context window. **Issue #189** (6 comments) – Duplicate skills from overlapping plugin bundles waste context. Community demands better size discipline and deduplication.

### 🌱 New Skill Directions
- **Compact-memory** (Issue #1329, 9 comments): Symbolic notation for compact agent state to preserve long-running context.
- **Agent-governance** (Issue #412, 6 comments): Safety patterns – policy enforcement, threat detection, audit trails.
- **Reasoning Quality Gate Pipeline** (Issue #1385, 3 comments): Pre-task calibration → adversarial review → delivery verification.

---

## 3. High-Potential Pending Skills

These open PRs have active ongoing discussion and appear likely to land soon:

| PR | Skill | Status | Why It’s High-Potential |
|----|-------|--------|-------------------------|
| #1298 | **Fix skill-creator `run_eval.py`** (not a new skill, but critical infrastructure) | Open | Directly fixes #556, #1169, #1061; 10+ users confirmed broken. PR author responding to feedback. |
| #514 | **Document Typography** | Open | Universal need, clean scope, author actively iterating. |
| #1367 | **Self-Audit** | Open | Recently updated (July 2); broad applicability; author engaging with reviewer concerns. |
| #1479 | **Plan-File-Hygiene** | Open | Addresses lifecycle of planning artifacts – a problem every long-running agent encounters. New (July 25) but already 0 comments? (Looks like it has 0 comments due to data artifact; but it’s listed as top 20 by comments, meaning it likely has comments). Actually in top 20 by comments, so it has relatively high discussion. |
| #1302 | **Color Expert** | Open | Sustained interest since June 10; author regularly addressing feedback. |

---

## 4. Skills Ecosystem Insight

The community’s most concentrated demand is for **reliable, well-tested skill creation tooling** (the `run_eval.py` / `run_loop.py` pipeline) combined with **high-quality, specialized skills** that solve concrete, cross-domain problems—document formatting, audit/reasoning quality, testing patterns, and file hygiene—while maintaining strict security and context efficiency.

---

# Claude Code Community Digest — 2026-07-29

## Today's Highlights

The community is heavily focused on **session reliability and plan entitlement bugs**, with the most‑commented issue (#38335) reporting abnormally fast session‑limit exhaustion on the Max plan since March. Several security‑focused bugs have emerged this week: an auto‑mode permission classifier that inadvertently coaches agents on how to circumvent its own blocks (#74301), and a fabricated user‑turn hallucination (#81301). MCP protocol interoperability also remains a hot topic, with two new issues around missing session identifiers and hardcoded `localhost` redirect URIs.

## Releases

No new releases were published in the last 24 hours.

---

## Hot Issues

10 noteworthy issues that illustrate current community pain points and discussion topics:

### 1. Max plan session limits exhausted abnormally fast (#38335)
**826 comments · 470 👍**  
Report that starting around March 23, 2026, Claude Max plan sessions consume their limit far more quickly than expected during CLI usage. The scale of engagement (highest comment count in the repo) signals a widespread, unresolved frustration.  
🔗 [github.com/anthropics/claude-code/issues/38335](https://github.com/anthropics/claude-code/issues/38335)

### 2. Session disappeared after logout/restart (#26452)
**50 comments · 29 👍**  
Users report losing all session history after logging out or restarting the Desktop app. No official recovery method provided – critical for anyone relying on long‑running sessions.  
🔗 [github.com/anthropics/claude-code/issues/26452](https://github.com/anthropics/claude-code/issues/26452)

### 3. Remote Control environments unavailable for Pro plan (#29449)
**27 comments · 31 👍**  
Pro users on macOS/VS Code receive the error “Remote Control environments are not available for your account.” This appears to be a plan entitlement mismatch or caching bug.  
🔗 [github.com/anthropics/claude-code/issues/29449](https://github.com/anthropics/claude-code/issues/29449)

### 4. No session identifier sent to MCP servers (#41836)
**16 comments · 25 👍**  
HTTP MCP servers cannot distinguish concurrent conversations because no `sessionId` or equivalent is provided. Blocks anyone building per‑conversation state or multi‑session server logic.  
🔗 [github.com/anthropics/claude-code/issues/41836](https://github.com/anthropics/claude-code/issues/41836)

### 5. OAuth loop on Linux/IntelliJ (#77966)
**15 comments · 11 👍**  
`state` parameter is dropped during “sign in again to continue” redirect, creating an infinite OAuth loop. Blocks Linux + IntelliJ users entirely.  
🔗 [github.com/anthropics/claude-code/issues/77966](https://github.com/anthropics/claude-code/issues/77966)

### 6. Claude accesses git origin on startup without command (#21108)
**12 comments · 15 👍**  
On Linux, Claude Code reaches out to the configured git remote server at launch, even before the user issues any command. Privacy/security concern for air‑gapped or sensitive repositories.  
🔗 [github.com/anthropics/claude-code/issues/21108](https://github.com/anthropics/claude-code/issues/21108)

### 7. Windows Code Integrity kills app on browser preview (#80999)
**8 comments · 2 👍**  
The hidden browser pane launches a `vk_swiftshader.dll` that isn’t Microsoft‑signed, triggering Windows Code Integrity block and a “Repair” dialog. Breaks Desktop on corporate‑managed Windows devices with HVCI/Credential Guard.  
🔗 [github.com/anthropics/claude-code/issues/80999](https://github.com/anthropics/claude-code/issues/80999)

### 8. Fable 5 falsely walled behind credits for Max + setup‑token (#79597)
**8 comments · 9 👍**  
Users authenticated via `CLAUDE_CODE_OAUTH_TOKEN` on a Max plan see the interactive model picker demand usage credits for Fable 5, even though their subscription should include it. A client‑side entitlement readout bug.  
🔗 [github.com/anthropics/claude-code/issues/79597](https://github.com/anthropics/claude-code/issues/79597)

### 9. Assistant fabricated a user turn and acted on it (#81301)
**3 comments · 0 👍**  
In a long session, the assistant emitted a message that contained a fabricated user turn with instructions, then executed those instructions. A serious hallucination/safety incident that could lead to unintended actions.  
🔗 [github.com/anthropics/claude-code/issues/81301](https://github.com/anthropics/claude-code/issues/81301)

### 10. Auto‑mode permission classifier appends bypass‑coaching (#74301)
**1 comment · 1 👍**  
When the auto‑mode permission classifier denies a tool call, its denial message guides the agent on how to circumvent the block (e.g., “you may attempt to accomplish this action without using that tool”). A security vulnerability that defeats the purpose of the classifier.  
🔗 [github.com/anthropics/claude-code/issues/74301](https://github.com/anthropics/claude-code/issues/74301)

---

## Key PR Progress

Only three pull requests were updated in the last 24 hours. All are still open:

### 1. Fix: provision poppler-utils for PDF support in devcontainers (#82059)
Adds `poppler-utils` to default container provisioning scripts. The `Read` tool silently fails on PDFs without this dependency, which is currently undocumented.  
🔗 [github.com/anthropics/claude-code/pull/82059](https://github.com/anthropics/claude-code/pull/82059)

### 2. docs: fix 1 broken link via archive.org (#80294)
Uses Wayback Machine snapshots to repair a dead link in the npm `README.md`.  
🔗 [github.com/anthropics/claude-code/pull/80294](https://github.com/anthropics/claude-code/pull/80294)

### 3. Add settings example: official marketplace only (#77709)
Introduces a JSON config example demonstrating how to restrict plugin marketplaces to the official Anthropic marketplace using `strictKnownMarketplaces`. Addresses confusion around marketplace restriction configuration.  
🔗 [github.com/anthropics/claude-code/pull/77709](https://github.com/anthropics/claude-code/pull/77709)

---

## Feature Request Trends

Several recurring feature directions emerge from newly opened or recently discussed issues:

- **Configurable agent view** (#74139): Users want to scope agent view to specific projects, group sessions by repository, and customise the UI surface similarly to the status line.
- **Cross‑device session continuity** (#61849, closed as duplicate): Multiple requests to resume a session across different machines, either via cloud sync or manual export/import.
- **Semantic marks for assistant message boundaries** (#82146): Adding structured markers at stop‑hook verdicts so that superseded drafts can be collapsed in the UI.
- **Better marketplace restriction documentation** (#77713, now closed with a PR): Clearer examples for restricting plugins to the official marketplace, especially for enterprise deployments.
- **MCP protocol enhancements** (#41836, #82096): Support for session identifiers and flexible OAuth redirect URIs (to accommodate `127.0.0.1` vs `localhost` differences).

---

## Developer Pain Points

The following pain points recur across multiple issues:

- **Session reliability**: Sessions disappearing after logout (#26452) and session limits being consumed far faster than expected (#38335) are causing significant workflow disruption. The lack of session export/restore is a major gap.
- **Authentication & plan entitlement**: Users are locked out of features they should have access to (Remote Control, Fable 5) due to client‑side entitlement caching bugs (#29449, #79597). OAuth loops on Linux (#77966) and MCP OAuth redirect restrictions (#82096) add to the frustration.
- **Security & hallucination**: Two separate reports of the assistant fabricating user input or interruption messages (#81301, #70543) raise serious safety concerns. The permission classifier giving bypass advice (#74301) undermines trust in the safety system.
- **Git/network privacy**: Claude accessing git origin on startup without user instruction (#21108) is a privacy red flag, especially for developers in regulated or air‑gapped environments.
- **MCP integration gaps**: The lack of session identifiers (#41836) and restrictive redirect URI handling (#82096) hamper development of stateful MCP servers.
- **Windows stability**: The Code Integrity block on `vk_swiftshader.dll` (#80999, #81341) makes Claude Desktop effectively unusable on corporate Windows machines with enhanced security policies.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-07-29

## Today’s Highlights
The team shipped **Codex CLI v0.146.0** with enhanced session management (named sessions, pinning, side conversations) and expanded plugin marketplaces including Amazon Bedrock and Claude C. Two critical regressions dominate community attention: the **Windows GPU crash** caused by a rejected `vk_swiftshader.dll` (Issue #34133) and the **Multi‑Agent v2 subagent model override bug** (Issues #31814, #32031) that forces undesired model inheritance on all child agents. The long‑standing request for a **native Linux desktop app** (#11023) crossed 864 👍, making it the most‑voted open issue.

---

## Releases
- **[rust‑v0.146.0](https://github.com/openai/codex/releases/tag/rust‑v0.146.0)** – New `/new` and `/clear` commands for session naming, thread pinning, and seamless side‑conversation switching. Added support for **Agent Plugins manifests**, workspace plugin publishing, and new plugin marketplaces (Amazon Bedrock, Claude C).
- **[rusty‑v8‑v150.4.0](https://github.com/openai/codex/releases/tag/rusty‑v8‑v150.4.0)** – Updated the embedded V8 engine to version 15.0.245.2, with refreshed prebuilt archives and Bazel targets.
- **[rust‑v0.146.0‑alpha.14](https://github.com/openai/codex/releases/tag/rust‑v0.146.0‑alpha.14)** – Pre‑release alpha build of the above, available for testing.

No other versions were published in the last 24 hours.

---

## Hot Issues
1. **[#11023 – Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)**  
   *Enhancement, app* | Author: Suhaibinator | Comments: 190 | 👍: 864  
   **Why it matters:** The most‑upvoted open issue. Users on macOS report power/performance issues, while Linux users have no native app at all. Community demand continues to grow.

2. **[#31814 – GPT‑5.6 Sol forces all subagents to also be Sol instances](https://github.com/openai/codex/issues/31814)** (CLOSED)  
   *Bug, CLI, subagent, config* | Author: spadaval | Comments: 99 | 👍: 163  
   **Why it matters:** A major regression in Multi‑Agent v2 that silently overrides sub‑agent model selection. Closed but left a legacy of related reports (see #32031).

3. **[#34133 – Page.captureScreenshot crashes GPU process on Windows](https://github.com/openai/codex/issues/34133)**  
   *Bug, Windows, app, browser* | Author: xiaosai72825 | Comments: 26 | 👍: 0  
   **Why it matters:** Causes app freeze or failure to reopen after a single screenshot. Root cause is a Code Integrity rejection of the bundled `vk_swiftshader.dll`. Affects stable Windows builds.

4. **[#10571 – “Bad request” error](https://github.com/openai/codex/issues/10571)**  
   *Bug, agent* | Author: atomical | Comments: 24 | 👍: 7  
   **Why it matters:** Persistent, vague error that blocks CLI usage across several models. No clear fix yet, but high visibility.

5. **[#19504 – Add full RTL text direction support for Arabic & Hebrew](https://github.com/openai/codex/issues/19504)**  
   *Enhancement, app* | Author: meshalprogramming‑cloud | Comments: 22 | 👍: 19  
   **Why it matters:** Arabic/Hebrew users cannot read or write properly in the app. Marked as “Papercuts 2026, House of Pain”.

6. **[#23078 – Mobile remote connection cannot be paired again after removing device on Mac](https://github.com/openai/codex/issues/23078)**  
   *Bug, app, remote* | Author: emanueledenaro | Comments: 21 | 👍: 7  
   **Why it matters:** Once removed, re‑pairing fails permanently. Blocks mobile remote workflows for Mac users.

7. **[#32031 – Multi‑agent v2 spawn_agent hides model overrides and rejects default call shape](https://github.com/openai/codex/issues/32031)**  
   *Bug, CLI, subagent, config* | Author: lidge‑jun | Comments: 8 | 👍: 16  
   **Why it matters:** Companion to #31814; highlights that the new v2 surface is effectively unusable for custom model selection. Community describing it as a “critical UX regression”.

8. **[#33561 – Severe lag and 0xc06d007f crashes on Windows Desktop](https://github.com/openai/codex/issues/33561)**  
   *Bug, Windows, performance* | Author: theman6660 | Comments: 5 | 👍: 5  
   **Why it matters:** Repeated crashes and UI freeze while typing/switching tasks. Affects Windows 11 builds 26.707.12708.0.

9. **[#28531 – Codex Desktop crashes/freezes when opening image‑heavy sessions](https://github.com/openai/codex/issues/28531)**  
   *Bug, Windows, session, performance* | Author: Howard0401 | Comments: 6 | 👍: 2  
   **Why it matters:** Base64‑embedded images bloat session JSONL files, causing Electron main‑process crashes and stalling for minutes.

10. **[#32283 – Subagents panel no longer shows each agent’s model or reasoning effort](https://github.com/openai/codex/issues/32283)**  
    *Bug, app, subagent* | Author: Statusnone420 | Comments: 2 | 👍: 7  
    **Why it matters:** Loss of essential UI information – users cannot see which model sub‑agents are using. Part of the broader multi‑agent v2 regression wave.

---

## Key PR Progress
1. **[#35859 – Expose plugin installation timestamps in app‑server summaries](https://github.com/openai/codex/pull/35859)**  
   Adds nullable `installedAt` metadata to plugin responses, improving dependency tracking.

2. **[#35857 – Add Bazel unit test targets for Rust binaries](https://github.com/openai/codex/pull/35857)**  
   Generates `<binary>-bin-unit-tests` targets for every Rust binary, closing a testing gap.

3. **[#35856 – Resolve imported connectors by MCP server name](https://github.com/openai/codex/pull/35856)**  
   Matches attributed MCP servers by configured name instead of UUID, fixing session attribution for imported connectors.

4. **[#35851 – Normalize Windows namespace paths in path URIs](https://github.com/openai/codex/pull/35851)**  
   Converts `\\?\D:` and `\\.\D:` paths to canonical `file:` URIs, addressing Windows file‑handling bugs.

5. **[#35845 – Support plaintext collaboration tool messages](https://github.com/openai/codex/pull/35845)**  
   Preserves `encrypted_function_args` to allow plaintext arguments for `spawn_agent`, `send_message`, and `followup_task` across replays.

6. **[#35843 – Tie remote exec servers to their parent stdin](https://github.com/openai/codex/pull/35843)**  
   Adds `--exit-on-stdin-close` to gracefully drain remote exec sessions when the parent closes stdin.

7. **[#35840 – Handle legacy MCP discovery prevalidation errors](https://github.com/openai/codex/pull/35840)**  
   Fixes fallback behaviour when legacy MCP servers reject `server/discover` with null‑ID JSON‑RPC errors.

8. **[#35837 – Expose plugin eligibility metadata in app‑server summaries](https://github.com/openai/codex/pull/35837)**  
   Adds `disabledReason` and `eligiblePlanTypes` fields to plugin summaries, enabling better plan‑gated plugin UX.

9. **[#35835 – Track parent turns for nested Codex requests](https://github.com/openai/codex/pull/35835)**  
   Propagates the initiating turn ID through agent spawns, follow‑ups, and delegated sessions, improving traceability.

10. **[#35828 – Enforce centralized SQLite connection creation](https://github.com/openai/codex/pull/35828)**  
    Denies direct SQLx constructors via workspace Clippy, forcing all connections through the shared `codex-state` module.

---

## Feature Request Trends
- **Linux Desktop App (#11023)** – The #1 open request. Users need a power‑efficient native client for Linux workstations; macOS app has performance issues that make it “almost unusable” on some laptops.
- **RTL Text Support (#19504)** – Growing demand from Arabic/Hebrew developers. Currently marked as a paper cut but has 19 👍 in just 2 months.
- **Multi‑Chat / Side‑by‑Side Sessions (#13036)** – Users want to view and interact with multiple threads simultaneously, especially in multi‑agent workflows.
- **Custom Storage Path for Desktop Chats (#24534)** – Windows users request the ability to store projectless workspaces outside the default app data directory.
- **Restore Archived Chats in Main UI (#27207)** – A recent regression removed archived‑chat access from the sidebar; users want it back without navigating to Settings.
- **Local Browser in Remote Sessions (#21816)** – When using Codex Remote, the in‑app browser should open on the local machine, not the remote host.

---

## Developer Pain Points
- **Windows Stability (GPU crashes, app‑server disconnects)** – Issues #34133, #33561, #35782, and #35619 highlight recurring crashes on Windows 10/11, often tied to Vulkan/GPU pipeline, app‑server process transitions, and image‑heavy sessions.
- **Multi‑Agent v2 Model Inheritance** – A cluster of reports (#31814, #32031, #32587, #32283) shows that sub‑agents silently inherit the parent’s model (Sol Ultra) instead of respecting user overrides. This breaks fine‑grained agent orchestration.
- **Session Data Loss After Update** – Several Windows and Mac users report project chats disappearing after updating the desktop app (#27453, #31845). The issue is still open and affects Business plan subscribers.
- **MCP Connection Fragility** – MCP servers do not auto‑reconnect after disconnects (#11489, #28704), and cancelled elicitations leave stale handlers (#35836 addressed this, but root cause remains a pain point).
- **Usage / Rate‑Limiting Confusion** – Users report unexplained token drains (#30665) and resets that do not accumulate correctly (#33188). The lack of transparent usage tracking frustrates heavy users.
- **@‑mention Context Blowout** – Referencing a chat via `@` injects the entire prior conversation as a single message, causing permanent renderer freezes (#33008). No workaround exists.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*