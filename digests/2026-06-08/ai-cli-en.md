# AI CLI Tools Community Digest 2026-06-08

> Generated: 2026-06-08 03:36 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date:** 2026-06-08 | **Prepared for:** Technical Decision-Makers

---

## 1. Ecosystem Overview

The AI CLI tool ecosystem is in a period of **high demand but mounting friction**. Both Claude Code and OpenAI Codex face critical reliability challenges—usage-limit exhaustion, model quality regressions, and platform-specific blockers—that erode developer trust. The community discourse reveals a widening gap between user expectations (stable, predictable tools) and current reality (opaque throttling, broken sandboxes, and flaky remote sessions). Despite this, investment in **extensibility (MCP/plugin ecosystems)** and **cross-platform support** remains strong, indicating the ecosystem is maturing beyond experimental usage toward production-grade tooling. The absence of new releases from either tool in the past 24 hours suggests a consolidation phase rather than rapid iteration.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Top 10 Issues (Total Comments)** | ~1,587 comments | ~242 comments |
| **Top 10 Issues (Total Reactions)** | ~1,062 👍 | ~560 👍 |
| **Hot Issue Dominance** | Single bug (#16157) accounts for 1,476 comments (93%) | Distributed; top issue has 100 comments |
| **Active PRs (Last 24h)** | 1 (non-substantive, placeholder) | 10 (including merged/closed) |
| **New Releases** | None | None |
| **Dev Activity Signal** | Stalled; focus on issue triage | Active; internal and external contributions |

**Key observations:**
- Claude Code's community is **louder and more concentrated**—one usage-limit bug (#16157) dominates discourse, suggesting systemic frustration.
- OpenAI Codex shows **healthier engineering velocity** with 10 active PRs, including infrastructure, SDK, and plugin improvements.
- Both tools are **release-dormant** today, consistent with a mid-week development cycle or post-release stabilization.

---

## 3. Shared Feature Directions

Three cross-cutting requirements emerge from both communities:

### A. Native Linux Desktop Support
- **Claude Code** (#65697): 316 👍, 24 comments. Currently lacks `.deb`/`.rpm` builds; users rely on third-party wrappers.
- **OpenAI Codex** (#11023): 510 👍, 100 comments. Most upvoted issue overall; users cite power consumption and platform lock-in.
- **Signal:** Linux developers represent a vocal, underserved demographic in both ecosystems. The demand is not just for terminal usage but for **full desktop integration** (GUI, notifications, file access).

### B. Rate Limit Transparency & Fairness
- **Claude Code** (#16157, #66150, #66165): Max subscribers burn quotas in minutes; server-side throttling is poorly communicated.
- **OpenAI Codex** (#12299, #26512): Users hit limits prematurely despite remaining allowance; passive quota draining undermines trust.
- **Signal:** Both tools suffer from **opaque usage accounting**. Developers cannot distinguish between genuine consumption, failed request charges, and server-side throttling. This is a trust-critical failure.

### C. Cross-Platform Reliability (Windows & Linux)
- **Claude Code Windows:** `spawn ENOENT` for MCP servers (#58510), corrupted path startup, broken scroll wheel (#65833).
- **Claude Code Linux:** Broken `bwrap` sandbox on merged-usr distros; UTF-8 copy corruption.
- **OpenAI Codex Windows:** OS error 740 (UAC) blocking sandbox spawn (#25362); severe WSL2 performance degradation (#25715).
- **OpenAI Codex Linux:** No desktop app, forcing CLI-only or third-party workarounds.
- **Signal:** **Windows is the most broken platform** for both tools. Linux suffers from neglect rather than breakage. macOS enjoys best-in-class support across the board.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary Use Case** | Collaborative coding (Cowork, Dispatch, Remote Sessions) | Autonomous agent workflows (Computer Use, plugin ecosystem) |
| **Community Focus** | Model quality assurance (Opus 4.8 regressions) | Platform stability (sandbox, SDK, connectors) |
| **Extensibility** | MCP servers, hooks, permission workflows | Plugin marketplace, SDKs (Python, TypeScript), global instructions API |
| **Key Pain Point** | Usage limits & model reliability | Windows sandbox & WSL performance |
| **Development Cadence** | Issue-driven, slower PR velocity | Feature-driven, faster PR velocity with infrastructure investment |

**Detailed analysis:**

- **Claude Code** differentiates on **collaborative features** (Cowork, Dispatch, remote session state) but is hampered by **model quality regressions** in Opus 4.8 (malformed tool calls, forced criticism, hallucinated XML). The community is focused on **trust restoration** rather than new features.

- **OpenAI Codex** differentiates on **extensibility and SDK maturity**. PRs this week show investment in global instructions API (#26831), plugin caching (#26934, #26932), and Python SDK goal turns (#26920). The community pain is **infrastructure-level** (sandbox, WSL, plugin stability), suggesting a more diverse user base with complex integrations.

- **Model strategy divergence:** Claude Code is grappling with a **single model regression** (Opus 4.8) affecting the entire workflow. OpenAI Codex faces a **model availability issue** (gpt-5.5 listed but 404) that undermines model selection trust. Both are **model trust problems**, but Claude's is deeper (systemic behavior) while OpenAI's is operational (resolvable deployment bug).

- **Target user split:** Claude Code appears more focused on **individual developers and small teams** (collaboration, hooks, permission workflows). OpenAI Codex targets **platform builders and integration-heavy users** (SDKs, plugins, global instruction lifecycle, subagent coordination).

---

## 5. Community Momentum & Maturity

| Metric | Claude Code | OpenAI Codex | Verdict |
|---|---|---|---|
| **Engagement Volume** | Very High (1,476 comments on single bug) | Moderate (242 comments across top 10) | Claude has louder, more concentrated engagement |
| **Engineering Responsiveness** | Low (1 non-substantive PR in 24h) | High (10 PRs, including infrastructure) | Codex is iterating faster |
| **Issue Resolution Velocity** | Stalled (usage-limit bug open since January) | Mixed (some PRs closed, but foundational issues persist) | Neither tool is resolving core pain points quickly |
| **Community Maturity** | High (detailed model analysis, workaround discussion) | Moderate (more new-user confusion, basic authentication issues) | Claude community is more technically sophisticated |
| **Open Source Health** | Weak (single PR, placeholder title) | Strong (external contributions, clear PR structure) | Codex has healthier open-source processes |

**Overall assessment:**
- **Codex has better engineering velocity** and **healthier open-source practices**, but its community is less technically sophisticated and faces more basic onboarding friction.
- **Claude Code has a more engaged, technically mature community** producing detailed model analysis (71 sub-issues in #64991), but the **development team appears unresponsive** to the most critical bugs, creating a trust deficit.
- **Neither tool is in a "mature" state.** Both are struggling with fundamental reliability issues that should have been resolved before reaching paid subscription tiers.

---

## 6. Trend Signals

### For Technical Decision-Makers

1. **Model reliability is the new frontier.** The Opus 4.8 regressions (malformed tool calls, forced criticism) and gpt-5.5 404 errors signal that **model quality is not keeping pace with feature development**. When planning adoption, budget for model-version pinning, fallback models, and rigorous testing against your specific workloads.

2. **Platform-specific lock-in is real.** macOS users enjoy near-seamless experiences; Windows and Linux users face systemic barriers (sandbox failures, WSL performance, missing desktop apps). If your team is heterogeneous, **expect 2–3× more friction for non-macOS developers**.

3. **Usage-limit opacity is a trust killer.** Both tools charge premium subscription prices but cannot reliably account for consumption. This creates adversarial dynamics between tool vendors and users. **Negotiate clear usage accounting SLAs** before committing to enterprise agreements.

4. **Extensibility is accelerating, but infrastructure lags.** Both ecosystems invest in plugin/MCP/SDK layers, but the underlying sandbox, path resolution, and permission systems are fragile. **Expect integration breakage** with each update—plan for testing windows and rollback capabilities.

5. **Community signals matter more than release notes.** The most valuable intelligence for adoption decisions comes from issue tracker sentiment, not marketing materials. Claude Code's #64991 (71 sub-issues with Opus 4.8) is a **canary in the coal mine** for systematic model quality problems.

6. **Linux remains an afterthought.** Despite vocal demand (316 👍 for Claude, 510 👍 for Codex), neither vendor has delivered a native Linux desktop experience. This represents both a **risk for Linux-heavy teams** and a **potential opportunity** for vendors who address it.

### Recommendation

For **production-critical workflows**, neither tool is currently reliable enough for unattended operation. Consider:
- **Claude Code** for **collaborative coding** in macOS-only teams, with strict usage monitoring.
- **OpenAI Codex** for **integration-heavy pipelines** (SDK, plugins) where engineering velocity and extensibility outweigh platform stability concerns.
- **Both tools** require **fallback strategies** (alternative models, manual intervention) for critical tasks.

The ecosystem is in a **growth-stage reliability trough**. Investment in tooling should be paired with **testing infrastructure** to catch regressions early and **vendor-agnostic fallbacks** to mitigate platform-specific failures.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-06-08 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following PRs have attracted the most community discussion and attention. **All remain open** — none have been merged to date.

### #514 – Document Typography Skill
**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses a universal pain point in Claude's document output quality.

**Status:** Open since 2026-03-04 | [View PR](https://github.com/anthropics/skills/pull/514)

### #486 – ODT Skill (OpenDocument Format)
**Functionality:** Enables creation, template filling, reading, and conversion of .odt and .ods files. Triggers on mentions of ODT, ODS, LibreOffice, or OpenDocument.

**Discussion:** The highest-commented PR in the repository. Broad interest in open-source document format support.

**Status:** Open since 2026-03-01 | [View PR](https://github.com/anthropics/skills/pull/486)

### #210 – Frontend-Design Skill Clarity Improvements
**Functionality:** Revises the existing frontend-design skill for better actionability — ensuring every instruction is executable within a single conversation and steering Claude's behavior with specificity.

**Status:** Open since 2026-01-05 | [View PR](https://github.com/anthropics/skills/pull/210)

### #83 – Meta Skills: Quality Analyzer & Security Analyzer
**Functionality:** Two proposed meta-skills for evaluating other skills. The quality analyzer scores across Structure & Documentation (20%), while the security analyzer audits for vulnerabilities.

**Discussion:** Represents community interest in skills *about* skills — quality assurance and trust verification for the ecosystem.

**Status:** Open since 2025-11-06 | [View PR](https://github.com/anthropics/skills/pull/83)

### #1140 – Agent-Creator Meta-Skill
**Functionality:** A meta-skill for creating task-specific agent sets. Includes fixes for multi-tool evaluation parallelism and Windows `%APPDATA%` support.

**Status:** Open since 2026-05-15 | [View PR](https://github.com/anthropics/skills/pull/1140)

### #723 – Testing Patterns Skill
**Functionality:** Comprehensive testing skill covering the Testing Trophy model, unit testing (AAA pattern), React component testing (Testing Library), and test philosophy guidance.

**Status:** Open since 2026-03-22 | [View PR](https://github.com/anthropics/skills/pull/723)

### #568 – ServiceNow Platform Skill
**Functionality:** Broad ServiceNow platform assistant covering ITSM, ITOM, ITAM/SAM Pro, FSM, HRSD, CSM, SPM, Vulnerability Response, Security Incident Response, and IntegrationHub.

**Discussion:** Largest single-platform enterprise skill submitted — reflects demand for enterprise IT tooling integration.

**Status:** Open since 2026-03-08 | [View PR](https://github.com/anthropics/skills/pull/568)

### #335 – Masonry AI Image & Video Generation Skill
**Functionality:** Wraps Masonry CLI for AI image generation (Imagen 3.0) and video generation (Veo 3.1) with job management capabilities.

**Status:** Open since 2026-02-04 | [View PR](https://github.com/anthropics/skills/pull/335)

---

## 2. Community Demand Trends

From the most-discussed Issues, five clear demand patterns emerge:

**Enterprise Sharing & Collaboration (#228, 13 comments, 👍7)**
Users want org-wide skill sharing without manual file transfer via Slack. A shared skill library or direct sharing links inside Claude.ai is the most-requested feature. [View Issue](https://github.com/anthropics/skills/issues/228)

**Eval Tooling Reliability (#556, 11 comments, 👍7)**
`run_eval.py` consistently reports 0% trigger rates across all queries — the core optimization loop is effectively broken. Multiple users report identical symptoms, making this a blocking issue for skill creators. [View Issue](https://github.com/anthropics/skills/issues/556)

**Skill Portability & Namespace Trust (#492, 7 comments)**
Community skills distributed under the `anthropic/` namespace create a trust boundary vulnerability. Users may grant elevated permissions to skills they believe are official. [View Issue](https://github.com/anthropics/skills/issues/492)

**Duplicate Skill Installation (#189, 6 comments, 👍8)**
The `document-skills` and `example-skills` plugins contain identical content, causing redundant context window consumption. The README's documented separation of concerns is not reflected in actual distribution. [View Issue](https://github.com/anthropics/skills/issues/189)

**Skill-Creator Best Practices (#202, 8 comments)**
The meta-skill reads like documentation for humans rather than instructions for Claude. Verbose, educational tone undermines token efficiency and violates naming guidelines. [View Issue](https://github.com/anthropics/skills/issues/202)

---

## 3. High-Potential Pending Skills

These PRs have active comment threads and appear close to resolution or demonstrate significant community investment:

**#444 – AURELION Skill Suite** (kernel, advisor, agent, memory)
Four skills implementing a structured cognitive + memory framework. Last updated 2026-05-06 — active refinement underway. [View PR](https://github.com/anthropics/skills/pull/444)

**#363 – feature-dev Workflow Fix** (TodoWrite overwrite bug)
Fixes a critical bug where Phase 6 (Quality Review) and Phase 7 (Summary) are skipped due to TodoWrite replacing the entire todo list on each call. Last updated 2026-06-03 — very recent activity. [View PR](https://github.com/anthropics/skills/pull/363)

**#190 – n8n-builder & n8n-debugger**
Four production-tested community skills including n8n workflow builder and debugger, plus a .faf context format expert. Last updated 2026-05-18. [View PR](https://github.com/anthropics/skills/pull/190)

**#1099/#1050 – Windows Compatibility Fixes**
Two PRs addressing `run_eval.py` and subprocess crashes on Windows. These unblock significant portions of the Windows user base and are actively discussed. [View PR #1099](https://github.com/anthropics/skills/pull/1099) | [View PR #1050](https://github.com/anthropics/skills/pull/1050)

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for meta-quality tooling (skill evaluation, security auditing, and developer experience) and enterprise document/workflow integration (ODT, ServiceNow, SharePoint), with document typography quality as the single most-discussed Skill submission to date.**

---

# Claude Code Community Digest – 2026-06-08

## Today’s Highlights
No new releases landed in the past 24 hours. The community remains highly vocal about a critical usage‑limit bug (#16157, 1476 comments) that plagues Max subscribers. Demand for a native Linux desktop build (#65697) continues to surge, while several Opus 4.8 model issues—including malformed tool calls and forced criticism—signal growing concerns about model reliability.

## Releases
**None.** No new versions were published in the last 24 hours.

## Hot Issues (10 selected from top 30 by activity)

1. **[#16157] [BUG] Instantly hitting usage limits with Max subscription**  
   *1476 comments, 691 👍*  
   The single most active issue. Max‑tier users report burning through their full quota within minutes of starting a session. The community has been discussing workarounds and waiting for a fix since January.  
   [View Issue](https://github.com/anthropics/claude-code/issues/16157)

2. **[#45937] Dispatch main conversation permanently offline**  
   *33 comments*  
   The main Dispatch thread shows “offline” on mobile even while individual Cowork tasks run correctly. Persistent across reconnects. Affects remote collaboration.  
   [View Issue](https://github.com/anthropics/claude-code/issues/45937)

3. **[#65697] [FEATURE] Official Claude Desktop build for Linux**  
   *24 comments, 316 👍*  
   Strongly requested by the Linux community. Currently no packaged `.deb`/`.rpm` build, forcing users to run via third‑party wrappers. High demand for Ubuntu LTS / Debian support.  
   [View Issue](https://github.com/anthropics/claude-code/issues/65697)

4. **[#25128] [BUG] Drag and drop not working in VS Code extension**  
   *19 comments, 39 👍*  
   Regression introduced around v2.1.6; still broken through v2.1.39. File drag‑and‑drop works in terminal/CLI but fails in the chat panel. Multiple duplicates consolidated here.  
   [View Issue](https://github.com/anthropics/claude-code/issues/25128)

5. **[#62466] [BUG] Repeated “Image couldn’t be processed” API errors consuming usage**  
   *18 comments*  
   Users are charged for failed image‑processing requests that never deliver results. The error loops can burn through usage limits without producing output.  
   [View Issue](https://github.com/anthropics/claude-code/issues/62466)

6. **[#58510] [BUG] Windows: plugin‑shipped MCP servers using bare `npx` fail with `spawn ENOENT`**  
   *7 comments*  
   A fix for LSP plugins (#17312) did not cover the MCP spawn path. Official plugins relying on bare `npx` as command break on Windows.  
   [View Issue](https://github.com/anthropics/claude-code/issues/58510)

7. **[#63604] [BUG] Opus 4.8 repeatedly emits malformed `tool_use` blocks**  
   *4 comments, 8 👍*  
   Entire responses are discarded when Opus 4.8 generates invalid `<invoke>` XML. The issue is not present in Opus 4.7. Affects workflow reliability.  
   [View Issue](https://github.com/anthropics/claude-code/issues/63604)

8. **[#65833] [BUG] v2.1.150: scroll wheel no longer scrolls conversation**  
   *3 comments*  
   A recent regression in the TUI—mouse scroll now sends arrow keys, cycling through input history instead of scrolling output.  
   [View Issue](https://github.com/anthropics/claude-code/issues/65833)

9. **[#64991] [MODEL] Opus 4.8: forced balance‑slot criticism, attention‑driven context collapse**  
   *1 comment, 1 👍*  
   A detailed report cataloguing 71 sub‑issues with Opus 4.8: unfounded self‑critique, “critique‑for‑its‑own‑sake” in initial CoT, and context window collapse. Points to systemic model behavior problems.  
   [View Issue](https://github.com/anthropics/claude-code/issues/64991)

10. **[#66160] [BUG] Raw `<invoke>` XML printed to terminal, session hangs**  
    *2 comments*  
    On Windows, Opus 4.8 occasionally dumps raw XML to the output and then stalls until the user sends a message. Highly disruptive for unattended sessions.  
    [View Issue](https://github.com/anthropics/claude-code/issues/66160)

## Key PR Progress
Only one pull request received activity in the last 24 hours:

- **[#58673] s** – This PR, opened on 2026‑05‑13, carries the placeholder title “s” and has no substantive description. No reviews or merges are visible. It does not represent a meaningful contribution.  
  [View PR](https://github.com/anthropics/claude-code/pull/58673)

**Note:** No other pull requests were updated. The repository’s development activity appears focused on issues rather than code changes this week.

## Feature Request Trends
The most frequently requested directions from recent issues include:

- **Linux native desktop build** (#65697) – The community is calling for official support beyond the terminal TUI.
- **Accessibility & voice mode** (#42700) – Text‑to‑speech readback and voice control for Remote Cowork sessions.
- **VS Code integration enhancements** – A setting to disable automatic file attachment (#66162), and a global session history view across projects (#49095).
- **Hook & permission workflow improvements** – Ability to update input in the `PermissionRequest:ExitPlanTool:Approve` hook (#16001).
- **Third‑party provider compatibility** – Proper context window detection for Anthropic‑compatible APIs (#46416) and reduced friction when using alternative endpoints.

## Developer Pain Points
Recurring frustrations evident from the issue tracker:

- **Usage‑limit exhaustion** (#16157, #62466) – Both genuine consumption and failed requests consume quotas, leaving developers unable to work.
- **Dispatch / Cowork offline failures** (#45937, #65887) – Remote session state is flaky; the main conversation stays offline even when tasks succeed.
- **MCP and sandbox fragility** (#58510, #64768, #64799) – MCP servers fail to initialise across platforms, and the `bwrap` sandbox is broken on merged‑usr Linux distros.
- **Model quality regressions (Opus 4.8)** (#63604, #64991, #66160) – Malformed tool calls, forced criticism, and hallucinated XML output are eroding trust in the latest model iteration.
- **Platform‑specific showstoppers** – Windows: `spawn ENOENT`, broken scroll wheel, corrupted path startup. Linux: authentication state mismatch, UTF‑8 copy corruption. The Linux ecosystem in particular feels underserved.
- **Rate‑limiting confusion** (#66150, #66165) – Users report being rate‑limited even with active subscriptions, with unclear messaging about server‑side throttling vs. account limits.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-08

## Today's Highlights
The community is grappling with a critical `gpt-5.5` model 404 error (#26892) that makes the model listed but unusable in both Desktop and CLI, drawing 21 comments in a single day. Windows users continue to suffer from sandbox setup failures (especially OS error 740) and severe performance degradation under WSL. Meanwhile, the long-standing request for a Linux desktop app (#11023) remains the most upvoted issue (510 👍, 100 comments), signaling a strong unmet demand.

## Releases
No new releases in the last 24 hours.

## Hot Issues (Top 10 by Comment Count)
- **[#11023 – Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)** (Suhaibinator)  
  510 👍 | 100 comments. The most requested feature – a native Linux app. Users cite power consumption and platform lock-in as blockers.

- **[#25715 – Codex App Unusable Slow with WSL as Agent environment](https://github.com/openai/codex/issues/25715)** (AndreTeixeira1998)  
  36 comments. Routine operations become painfully slow when using WSL2; affects Pro subscribers.

- **[#26892 – gpt-5.5 listed but requests fail with 404 “Model not found”](https://github.com/openai/codex/issues/26892)** (qing-yan-a)  
  21 comments (newly created June 7). Model metadata shows availability but API returns 404. gpt-5.4 works. High urgency.

- **[#12299 – "You've hit your usage limit" despite 10% rate limit remaining](https://github.com/openai/codex/issues/12299)** (justinTM)  
  19 comments. Rate limiting logic appears inconsistent; users rationing weekly limits are hit prematurely.

- **[#11881 – GitHub PR review fails: "create a Codex account and connect to github"](https://github.com/openai/codex/issues/11881)** (nicoloceneda)  
  16 comments | 28 👍. Connector enabled but authentication still fails; multiple users report same confusion.

- **[#25500 – Desktop Projects sidebar shows "No chats" for older conversations](https://github.com/openai/codex/issues/25500)** (kezh9527)  
  14 comments. Conversations exist on disk but UI fails to list them; session JSONL remains readable.

- **[#23131 – TypeScript SDK JSONL parser fails on multiline MCP tool results](https://github.com/openai/codex/issues/23131)** (bongsu-rapportlabs)  
  11 comments. Patch available – critical for SDK users handling complex tool outputs.

- **[#25362 – Windows sandbox failed spawn setup refresh OS error 740](https://github.com/openai/codex/issues/25362)** (TheB1ak3)  
  9 comments | 5 👍. Computer Use on Windows fails due to permission elevation issues.

- **[#7808 – Running out of room in context window is immediately fatal to that chat thread](https://github.com/openai/codex/issues/7808)** (normancates)  
  9 comments | 8 👍. Long tasks abruptly terminate without graceful degradation; affects Plus users.

- **[#10605 – macOS dock badge shows unread count with no way to view/dismiss](https://github.com/openai/codex/issues/10605)** (artwist-polyakov)  
  7 comments | 9 👍. Persistent badge annoyance; app lacks notification history.

## Key PR Progress (Top 10 by Activity)
- **[#26937 – Test Windows managed deny-read enforcement](https://github.com/openai/codex/pull/26937)** (abhinav-oai)  
  New test to ensure `deny_read` permissions are enforced even via Python subprocesses in the sandbox.

- **[#26831 – Add global instructions contributor API](https://github.com/openai/codex/pull/26831)** (anp-oai)  
  Extracts global instructions from Config into an explicit extension point, enabling embedders to supply them without coupling to core config.

- **[#26830 – Characterize global instruction lifecycle](https://github.com/openai/codex/pull/26830)** (anp-oai)  
  Adds end-to-end tests for instruction behavior across thread creation, compaction, resume, forks, and subagents before changing semantics.

- **[#26639 – fix(tui): scope MCP startup status by thread](https://github.com/openai/codex/pull/26639)** (fcoury-oai)  
  *Closed*. Prevents child thread failures from polluting parent transcript; fixes session refresh replay issues.

- **[#26935 – Owen/local analytics](https://github.com/openai/codex/pull/26935)** (owenlin0)  
  External contribution; introduces local analytics capabilities (requires contribution guidelines review).

- **[#26918 – Address newly reported Rust advisories](https://github.com/openai/codex/pull/26918)** (friel-openai)  
  Patches `RUSTSEC-2026-0173` and `RUSTSEC-2026-0097` (proc-macro-error2, rand) and updates advisory config.

- **[#26934 – Prune stale curated plugin caches](https://github.com/openai/codex/pull/26934)** (xl-openai)  
  Removes cached plugins no longer in the marketplace, fixing stale Google Sheets plugin issues.

- **[#26932 – Use cached remote plugin catalog for plugin list](https://github.com/openai/codex/pull/26932)** (xl-openai)  
  Returns plugin listing from local cache when available, reducing latency and reliance on `/ps/plugins/list`.

- **[#26662 – feat(app-server): filter threads by parent](https://github.com/openai/codex/pull/26662)** (btraut-openai)  
  Enables app-server clients to query a thread's immediate children, critical for subagent coordination and recovery.

- **[#26920 – Add Python SDK goal turns](https://github.com/openai/codex/pull/26920)** (aibrahim-oai)  
  Exposes `goal=True` on Python SDK `run` and `turn`; persists goals atomically with stable IDs and aggregated results.

## Feature Request Trends
- **Linux Desktop App** (#11023, 510 👍) remains the most demanded feature – Windows and macOS users are frustrated by performance and power issues.
- **Version selection and rollback** (#26914) – Users paying $100/mo want the ability to pin or rollback app versions after breaking updates.
- **Rate limit transparency** (#12299, #26512) – Better visibility into weekly limits and passive quota draining.
- **Improved context window handling** (#7808) – Graceful degradation or continuation instead of fatal thread termination.

## Developer Pain Points
- **Windows sandbox reliability** – Multiple issues (#25362, #24050, #25419) show OS error 740 (UAC) and sandbox spawn failures, blocking Computer Use, MCP tools, and basic command execution.
- **Model availability inconsistency** – gpt-5.5 being listed but returning 404 (#26892, #26910) undermines trust in model selection. Similar past issues with gpt-5.4 (#18793).
- **WSL performance** (#25715, #25004) – Routine operations and even terminal UI flicker under WSL2, impacting a large segment of Windows developers.
- **Plugin and connector instability** – Plugins disappear after restart (#25809), Notion connector tool not found (#19924), GitHub auth loops (#11881), and Chrome connection problems (#23805).
- **Context window fatality** (#7808) – Long sessions are abruptly killed without warning, forcing users to start over with no way to recover progress.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*