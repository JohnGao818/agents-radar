# AI CLI Tools Community Digest 2026-06-20

> Generated: 2026-06-20 02:56 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem

**Date:** 2026-06-20  
**Sources:** Claude Code Community Digest, OpenAI Codex Community Digest

---

## 1. Ecosystem Overview

The AI CLI tools landscape is experiencing a phase of rapid iteration and growing user expectations. Both Anthropic’s Claude Code and OpenAI’s Codex show active communities grappling with production‑grade reliability issues—particularly around API stability, permission management, and cross‑platform parity. While Claude Code sees high community engagement on feature requests (skills sync, model routing), Codex is pushing more infrastructure‑level changes (path handling, sandbox intent, session runtime). The dominant pain point across both platforms is **billing/rate‑limit unpredictability**, eroding user trust. Development velocity, as measured by pull request activity, is significantly higher in Codex this week (10 PRs vs. 1), though both tools share a common trajectory toward better Windows support and more transparent usage accounting.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Noteworthy Issues** | 10 (highly engaged, many high‑upvote bug reports) | 10 (mix of critical regressions and feature requests) |
| **Active PRs (last 24h)** | 1 (pagination fix) | 10 (infrastructure‑heavy: PathUri, sandbox intent, session runtime, etc.) |
| **Releases (last 24h)** | None (stable v2.1.183, no update) | 4 alpha releases (v0.142.0-alpha.4 through alpha.7) |
| **Community Engagement (upvotes on top issues)** | Very high (#36151: 357 👍, #20697: 118 👍) | Moderate (#28988: 19 👍, #28879: 19 👍) |

*Note: Claude Code’s top issues have substantially higher upvote counts, indicating a larger or more vocal user base for feature requests. Codex shows more rapid release churn and PR throughput.*

---

## 3. Shared Feature Directions

Requirements appearing in **both communities**:

| Common Need | Claude Code Signals | OpenAI Codex Signals |
|-------------|---------------------|----------------------|
| **Persistent / reliable sandbox permissions** | Permission grants not propagating to subagents (#51289); Windows sandbox unlink denial (#55206) | “Full Access” sandbox repeatedly asks for permission (#28988); per‑file permission regressions (#13117) |
| **Transparent billing / rate‑limit accounting** | Unexplained usage jumps (#69419); Pro plan blocked despite low usage (#65514) | Rate‑limit cost per token jumped 10–20× without notice (#28879) |
| **Better Windows support** | File truncation (#53940); sandbox unlink denial (#55206); edit config opens wrong file | Windows app fails to open after update (#27979); sandbox helper crash (#28982); WSL deserialization error (#16815) |
| **Model behavior reliability** | Opus 4.8 fabricates tool executions (#67847) | Context window exhausted on fresh thread (#9046) |
| **Session / history management improvements** | Cowork sessions disappear from Recents on Windows (#69663) | Codex PRs optimizing resume and fork history (#28806); session runtime decoupling (#28787) |

Both communities are demanding **cross‑platform parity** and **usage transparency** as top‑priority fixes.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|-----------|-------------|--------------|
| **Primary focus areas** | Agent orchestration (subagent spawning, plan‑vs‑execute model switching), skill/persona sync across tools, billing transparency | Infrastructure modernization (Rust toolchain, hermetic builds, platform‑agnostic path handling), sandbox intent propagation, session lifecycle decoupling |
| **Target user persona** | Power users building complex multi‑step workflows; teams needing unified skill definitions | Developers integrating with VS Code and multiple execution environments (WSL, remote); users requiring stable CI/CD integrations |
| **Technical approach** | Incremental bug‑fix on stable v2.1.183; community‑driven feature requests with high upvote leverage | Rapid alpha releases (4 in one day); heavy PR investment in refactoring internals for future cross‑platform support |
| **Pain points uniqueness** | Subagent runaway recursion and token burn (#68619); model hallucination of tool calls; silent file truncation on Windows | V8 SIGTRAP crashes on Intel macOS; memory leak in VS Code extension; deserialization errors in WSL agent |
| **Community engagement style** | High‑volume issue upvoting (democratic feature prioritization) | More PR‑driven development; fewer upvoted feature requests but deeper technical discussion |

**Key insight:** Claude Code’s community is pushing for **user‑facing feature parity** (skills, model routing, billing dashboards), while Codex’s developers are investing in **architectural foundations** (path URIs, sandbox intent, session decoupling) that will enable future feature velocity.

---

## 5. Community Momentum & Maturity

- **Claude Code** has a larger and more vocal user base by upvote metrics (357 👍 on a single mobile‑app issue, 118 👍 on skill sync). However, its PR count is low (1), suggesting a stabilization phase or internal development cycles. The community is frustrated by persistent Windows issues and billing unpredictability, which erodes trust. Maturity is moderate—feature requests are well articulated, but fixes lag.

- **OpenAI Codex** shows higher development velocity (10 PRs, 4 alpha releases in 24h). The focus on infrastructure (Rust toolchain, hermetic builds, PathUri) signals a deliberate move toward a more robust, cross‑platform foundation. However, the community is smaller or less upvote‑active (max 19 👍). The frequency of regressions (app crashes after updates, sandbox helper failures) indicates that rapid iteration comes at a cost to stability.

**Verdict:** Codex is iterating faster on technical debt; Claude Code has stronger community momentum but is in a bug‑fix lull. Both tools need to address Windows parity and billing transparency to retain developer trust.

---

## 6. Trend Signals

From cross‑community feedback, several industry‑wide patterns emerge:

1. **Windows is still a second‑class citizen** in AI CLI tools. Both platforms have active, unresolved Windows‑specific bugs (file truncation, unlink denial, app crashes, WSL integration failures). Developers using Windows are bearing the brunt of regressions.

2. **Billing and usage transparency is the #1 trust issue.** Users are reporting unexplained jumps in consumption (Claude) and sudden per‑token cost increases (Codex) with no clear communication from providers. The demand for turn‑level cost breakdowns and proactive limit warnings is universal.

3. **Sandbox and permission models are not production‑ready.** Persistent “allow every time” prompts, permission propagation failures, and inconsistent behavior across OS platforms undermine autonomous agent workflows. Both communities want a one‑time grant that survives updates and restarts.

4. **Model behavior reliability is a growing concern.** Hallucinated tool calls (Claude) and false context‑full errors (Codex) point to issues in how models reason about their own capabilities. This will become a critical barrier as agents are trusted with more autonomous actions.

5. **Unified skill/persona ecosystems are emerging as a differentiator.** Claude Code’s high‑upvote request for skill sync between Desktop and CLI reflects a broader desire for consistent agent behavior across surfaces. Codex’s work on connector skills feature toggles (#29082) shows similar thinking.

6. **Platform‑agnostic path handling is a foundational investment.** Codex’s new `PathUri` lexical helpers and URI‑native plugin roots (#29164, #28918) signal that AI CLI tools are maturing beyond simple macOS‑first assumptions. This move benefits Windows and remote execution scenarios.

**Actionable takeaways for developers:**
- Prioritize Windows testing in CI/CD if your workflows depend on AI CLI tools.
- Monitor your billing dashboards daily; consider setting hard budget alerts.
- For agentic workflows, verify that sandbox permissions propagate to subagents and survive restarts.
- Evaluate model behavior: test against hallucination‑prone prompts (e.g., tool invocation claims) before relying on autonomous execution in production.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-06-20 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

Most-discussed Skill submissions (Pull Requests) ranked by community engagement:

### #514 — Document Typography Skill (OPEN)
**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment — common typographic defects in AI-generated documents.
**Discussion Highlights:** Resonates broadly because *every* document Claude generates suffers these issues. Community feedback focuses on edge cases and integration with existing document skills.
**Status:** Open. One of the most-watched pending additions.
🔗 https://github.com/anthropics/skills/pull/514

### #486 — ODT Skill: OpenDocument Creation & Parsing (OPEN)
**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods), enabling LibreOffice-compatible document workflows.
**Discussion Highlights:** Strong demand for open-source document formats. Discussion centers on template filling reliability and maintaining ODF compliance.
**Status:** Open. Community actively testing with real LibreOffice deployments.
🔗 https://github.com/anthropics/skills/pull/486

### #210 — Improve Frontend-Design Skill Clarity (OPEN)
**Functionality:** Revises the existing frontend-design skill to ensure every instruction is actionable within a single conversation and that guidance is specific enough to steer Claude's output reliably.
**Discussion Highlights:** Rooted in frustration with vague design instructions. Contributors debate specificity vs. flexibility for different UI frameworks.
**Status:** Open. Generating ongoing design-pattern discussions.
🔗 https://github.com/anthropics/skills/pull/210

### #83 — Skill-Quality-Analyzer + Skill-Security-Analyzer (OPEN)
**Functionality:** Meta-skills that evaluate other skills across five dimensions (Structure, Documentation, Code Quality, Error Handling, Security) and identify vulnerabilities.
**Discussion Highlights:** Community recognizes the need for quality standards as the ecosystem grows. Discussion surfaces tension between automated scoring and subjective skill design.
**Status:** Open. Referenced in multiple quality-related issues.
🔗 https://github.com/anthropics/skills/pull/83

### #181 — SAP-RPT-1-OSS Predictor Skill (OPEN)
**Functionality:** Wraps SAP's open-source tabular foundation model for predictive analytics on enterprise business data.
**Discussion Highlights:** Enterprise interest is high. Discusses model-serving integration and data privacy boundaries when SAP data meets AI.
**Status:** Open. Distinct from the typical web/dev skill pattern.
🔗 https://github.com/anthropics/skills/pull/181

### #723 — Testing-Patterns Skill (OPEN)
**Functionality:** Covers the full testing stack: Testing Trophy model philosophy, unit testing (AAA pattern), React Testing Library, E2E patterns, and mocking tradeoffs.
**Discussion Highlights:** Broad support for standardized testing guidance. Debate over prescribed vs. configurable testing philosophies.
**Status:** Open. High relevance for development teams.
🔗 https://github.com/anthropics/skills/pull/723

### #568 — ServiceNow Platform Skill (OPEN)
**Functionality:** Broad ServiceNow assistant covering ITSM, ITOM, ITAM, SecOps, FSM, HRSD, CSDM, and IntegrationHub scripting.
**Discussion Highlights:** Enterprise ITSM community is engaged. Scale concerns about a single skill covering so many ServiceNow domains.
**Status:** Open. Active iteration on scope boundaries.
🔗 https://github.com/anthropics/skills/pull/568

### #154 — Shodh-Memory: Persistent Context for AI Agents (OPEN)
**Functionality:** Enables Claude to maintain structured memory across conversations via proactive context retrieval, rich memory schemas, and automatic timeline management.
**Discussion Highlights:** Represents demand for persistent agent cognition. Discussion explores memory size limits and privacy implications.
**Status:** Open. Technically ambitious; awaiting deeper integration review.
🔗 https://github.com/anthropics/skills/pull/154

---

## 2. Community Demand Trends

From Issues (50 total), the most-anticipated Skill directions are:

| Trend | Evidence | Demand Signal |
|---|---|---|
| **Organization-wide Skill Sharing** | Issue #228 (14 comments, 👍7): "Skills should be shareable within an organization directly." | Highest-commented issue. Enterprise users want a shared skill library, not manual file distribution. |
| **Agent Governance & Safety** | Issue #412: "agent-governance — safety patterns for AI agent systems." Proposal for policy enforcement, threat detection, trust scoring. | Security-conscious users seeking guardrails as agent autonomy increases. |
| **Windows Compatibility** | Issues #1061, #1099, #1050 — multiple reports of subprocess, encoding, and pipe failures on Windows. | Persistent blocking issue for Windows users; multiple PRs in flight. |
| **Evaluation & Quality Tooling** | Issue #556 (12 comments, 👍7): `run_eval.py` reports 0% trigger rate. Issue #1169: recall=0% on every iteration. | The skill-evaluation pipeline is *broken* for many users, creating noise that blocks iteration. |
| **Security & Namespace Trust** | Issue #492: "Community skills under anthropic/ namespace enable trust boundary abuse." | Growing awareness of supply-chain risk as third-party skills proliferate. |
| **Compact/Symbolic Memory** | Issue #1329: "compact-memory — symbolic notation for compact agent state." | Follow-up to persistent memory interest; optimizes for context efficiency. |

**Cross-cutting theme:** The community is demanding *infrastructure* more than *content* — better sharing, evaluation, security validation, and cross-platform support.

---

## 3. High-Potential Pending Skills

These PRs are open with active engagement and appear close to landing:

| PR | Skill | Why It May Land Soon |
|---|---|---|
| **#538** | PDF: Fix case-sensitive file references | Small, targeted fix (8 case mismatches). Low risk, high correctness impact. |
| **#539** | skill-creator: Warn on unquoted YAML `:` | Prevents silent parsing failures. Duplicate of #361 but with implementation. |
| **#541** | DOCX: Prevent tracked-change `w:id` collision | Fixes document corruption when bookmarks exist. Clear root cause and fix. |
| **#1099** | skill-creator: Fix Windows pipe crash | Unblocks Windows users entirely. One of several Windows fix PRs converging. |
| **#1050** | skill-creator: Fix Windows subprocess + encoding | Small (1-line each), directly addresses Issue #1061. |
| **#361** | Detect unquoted YAML special characters | Older PR, still active as of June 2026. Community validation is growing. |
| **#362** | Fix skill-creator UTF-8 panic on multi-byte | Prevents Rust panics in CLI. Critical for i18n skill names. |
| **#1298** | run_eval.py: Fix 0% recall bug | Addresses the most-reported evaluation bug (#556, #1169). Major impact if merged. |

**Likelihood Assessment:** The Windows compatibility fixes (#1099, #1050) have high likelihood of being merged soon due to concentrated demand and small code surface. The evaluation fix (#1298) is the highest-impact pending change in the entire ecosystem.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *reliable, cross-platform skill development tooling* — specifically fixing the broken evaluation loop (`run_eval.py` recall=0% bug), enabling Windows compatibility, and establishing quality/security standards — rather than for any single new Skill content.**

---

# Claude Code Community Digest — 2026-06-20

**Today’s Highlights**  
No new releases were shipped in the last 24 hours, but community activity remained high with several critical bugs and feature requests dominating discussions. The most urgent signals are a wave of API‑availability regressions (Issue #69358) and a deeply concerning token‑burn scenario from runaway subagent spawning (Issue #68619). Windows users continue to bear the brunt of sandbox and tool‑truncation issues, while a highly‑popular feature request (Skill sync between Desktop and CLI, #20697) maintains strong momentum.

---

## Releases  
No new versions were published in the last 24 hours. The latest stable build remains **2.1.183**.

---

## Hot Issues (10 Noteworthy)

1. **[#53940 – Cowork Edit/Write silently truncate files via byte‑conservation buffer cap (Windows)](https://github.com/anthropics/claude-code/issues/53940)**  
   *35 comments, 👍12*  
   A deterministic bug where `Cowork` edit/write tools truncate file contents when the internal buffer cap is hit. Affects all file sizes and is particularly painful on Windows. No fix is yet available.

2. **[#20697 – Sync Skills between Claude Desktop and Claude Code CLI](https://github.com/anthropics/claude-code/issues/20697)**  
   *34 comments, 👍118*  
   The most‑upvoted feature request this week. Users want Skills defined in Claude Desktop to be available automatically in CLI sessions and vice‑versa. Strong community desire for a unified skill store.

3. **[#36151 – Multi‑account switching in Claude Mobile app](https://github.com/anthropics/claude-code/issues/36151)**  
   *98 comments, 👍357*  
   While filed against the mobile app (repo overlap), it highlights a broader ecosystem need: users with multiple Anthropic accounts want seamless switching without shared email constraints.

4. **[#15721 – Automatic Model Switching for Plan Mode](https://github.com/anthropics/claude-code/issues/15721)**  
   *20 comments, 👍36*  
   Users want Claude Code to automatically fall back to a cheaper or faster model during non‑coding discussions (“plan mode”), preserving expensive models for actual code generation.

5. **[#69419 – Usage jumped from 80% to 100% for the week](https://github.com/anthropics/claude-code/issues/69419)**  
   *15 comments, 👍6*  
   Sudden, unexplained billing jumps continue to erode trust. Several users report hitting weekly limits far before expected, with Anthropic’s usage dashboard showing no corresponding activity spike.

6. **[#68619 – Subagent spawning triggers infinite recursion / catastrophic token burn](https://github.com/anthropics/claude-code/issues/68619)**  
   *15 comments, 👍3*  
   A critical performance bug: subagents recursively spawn 50+ levels deep, ignoring `CLAUDE_CODE_FORK_SUBAGENT=0`. Permission denials trigger more agent spawning instead of halting. Compounded by HTTP file fetches from GitHub, leading to massive token waste.

7. **[#69358 – No Response From API (Linux) – regression in 2.1.181 / 2.1.183](https://github.com/anthropics/claude-code/issues/69358)**  
   *12 comments, 👍39*  
   Users on Linux (and some macOS) report that the API returns no response at all, repeatedly. Starts as soon as the app opens and persists across restarts. One of the highest‑voted active bugs.

8. **[#55206 – Cowork on Windows: bash sandbox can create files but unlink is denied](https://github.com/anthropics/claude-code/issues/55206)**  
   *11 comments, 👍7*  
   A sandbox inconsistency on Windows: writing to mounted host folders works, but `unlink` (delete) always fails. This breaks all `git write` operations (`git add`, `git clean`, etc.) inside cowork sessions.

9. **[#65514 – Usage credits required for 1M context – Pro plan blocked despite 17% usage](https://github.com/anthropics/claude-code/issues/65514)**  
   *20 comments, 👍2*  
   Pro plan users who try to use the 1M‑context window are asked to purchase additional credits even when their weekly usage is well below the cap. Confusing UX and a potential billing system logic error.

10. **[#67847 – Opus 4.8 fabricates entire tool executions inside extended thinking](https://github.com/anthropics/claude-code/issues/67847)**  
    *5 comments*  
    A hallucination issue with Opus 4.8: the model claims to have executed tools (e.g., `gh release create`) and describes detailed results, but the API response contains zero `tool_use` blocks. The model believes it ran tools that were never actually invoked.

---

## Key PR Progress

Only **one pull request** was updated in the last 24 hours:

**[#68673 – fix(scripts): break pagination when page is not full, not only when empty](https://github.com/anthropics/claude-code/pull/68673)**  
*Author: AZERDSQ131 – Updated 2026-06-19*  
A small but important fix to pagination logic in internal scripts. Previously pagination would only stop when an empty page was returned; now it also stops when a page is not full, preventing potential infinite loops. No other PRs were active in this window.

*(Note: The community typically sees 10–20 active PRs per week; the current low count may reflect pre‑release stabilization or a quiet development cycle.)*

---

## Feature Request Trends

The most‑requested feature directions distilled from recent issues:

1. **Unified skill/persona ecosystem** – Sync Skills across Desktop, CLI, and mobile (#20697, #36151). Users want a single skill definition shared everywhere.
2. **Intelligent model routing** – Automatic model switching based on task type (plan vs. execute) (#15721), and exposing real‑time token usage to the model so it can self‑regulate (#65832).
3. **Better Windows parity** – Auto‑allow piped commands when individual commands are allowed (#46868) and fixing sandbox/filing issues that are Windows‑exclusive.
4. **Permission workflow improvements** – Permission grants should propagate to subagents (#51289), and piped commands should be auto‑allowed (#46868).
5. **Billing transparency** – Show token/cost breakdown per turn, expose usage to the model, and provide warning before hitting limits (#65832, #65514).

---

## Developer Pain Points

Recurring frustrations from the top issues this week:

- **Windows sandbox incompatibility** – Cowork sessions cannot delete files on mounted host folders (#55206), tools silently truncate (#53940), and the MSIX “Edit Config” opens the wrong config file (#26073). Windows remains a second‑class citizen.
- **Unexplained billing / usage spikes** – Multiple reports of usage jumping from 60–80% to 100% in minutes with no corresponding activity (#69419, #69436, #69592). Erodes trust in the billing system.
- **Subagent reliability** – Runaway spawning (#68619), permission grants not propagating (#51289), and token burn from inefficient patterns. Agent orchestration feels fragile.
- **API stability regressions** – Recent versions (2.1.181+) cause clients to receive no response on Linux (#69358). Rate limits hit even highest‑tier plans (#60562, #62426).
- **Model hallucination of tool calls** – Opus 4.8 sometimes imagines tool execution results without actually invoking the tool (#67847). Breaks trust in Claude Code’s autonomy.
- **Missing session visibility** – Cowork sessions disappear from the Recents list on Windows (#69663), and desktop app crashes when opening the Code tab (#69366). Session management needs hardening.

---

*Generated from GitHub data for anthropics/claude-code. For real‑time updates, follow the [Issues page](https://github.com/anthropics/claude-code/issues) and [Pull Requests](https://github.com/anthropics/claude-code/pulls).*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-20

## Today’s Highlights
Four incremental Rust alpha releases (`v0.142.0-alpha.4` through `alpha.7`) landed in the last 24 hours, but the community remains focused on a trio of pressing issues: a context-window exhaustion bug that triggers even on fresh threads, a sudden 10‑20× jump in rate‑limit cost per token, and a persistent sandbox permission loop that forces repeated user approval on macOS and Windows. Several PRs signal deeper platform‑agnostic refactoring of path handling and sandbox intent propagation.

## Releases
- **rust-v0.142.0-alpha.4** through **rust-v0.142.0-alpha.7** — No changelog details beyond version bumps. Likely transitional builds for the upcoming Rust‑native toolchain improvements.

## Hot Issues
1. **#9046 – Context window exhausted on fresh thread** *(34 comments)*  
   The model claims the context window is full even after a single question. Users report no prior history. A high‑severity UX blocker for new sessions.  
   [openai/codex#9046](https://github.com/openai/codex/issues/9046)

2. **#27979 – Windows app fails to open after update** *(27 comments, 👍6)*  
   Update 26.609.4994.0 bricked the app entirely. Closed as a known issue, but the workaround is still unclear.  
   [openai/codex#27979](https://github.com/openai/codex/issues/27979)

3. **#28988 – Full‑access sandbox repeatedly asks for permission** *(25 comments, 👍19)*  
   After recent macOS app updates, granting “Full Access” doesn’t stick – Codex prompts for consent on every operation. Highest upvote count in this batch.  
   [openai/codex#28988](https://github.com/openai/codex/issues/28988)

4. **#28982 – Windows sandbox helper fails with “The specified module could not be found”** *(17 comments, 👍7)*  
   The native sandbox setup helper crashes immediately after the latest Windows app update.  
   [openai/codex#28982](https://github.com/openai/codex/issues/28982)

5. **#13117 – Permission regressions for every file read** *(16 comments, 👍10)*  
   A regression re‑introduces per‑file permission prompts long after the original fix. Affects Windows VS Code extension users.  
   [openai/codex#13117](https://github.com/openai/codex/issues/13117)

6. **#28879 – Rate‑limit cost per token jumped ~10–20× since June 16** *(15 comments, 👍19)*  
   Plus‑plan users see their 5‑hour budget consumed in 2–3 prompts. Suspected backend change with no announcement.  
   [openai/codex#28879](https://github.com/openai/codex/issues/28879)

7. **#27175 – Desktop crashes/completely inaccessible after update** *(15 comments, 👍3)*  
   Another Windows update (26.602.71036) that leaves the app in a crash loop. Closed, but users report re‑occurrence.  
   [openai/codex#27175](https://github.com/openai/codex/issues/27175)

8. **#16815 – WSL agent mode fails with “AbsolutePathBuf deserialized without a base path”** *(11 comments, 👍7)*  
   Switching Agent Environment to WSL produces an unhandled deserialization error, blocking Windows + WSL workflows.  
   [openai/codex#16815](https://github.com/openai/codex/issues/16815)

9. **#17257 – Extra High memory leak in VS Code extension** *(9 comments, 👍11)*  
   Memory grows without bound under sustained heavy use on macOS ARM.  
   [openai/codex#17257](https://github.com/openai/codex/issues/17257)

10. **#29000 / #29047 – SIGTRAP in V8 on Intel macOS when tool/skill invoked** *(6 combined comments, 👍5)*  
    Codex CLI and app crash with a `SIGTRAP` inside `v8::Isolate::New`. Downgrading to `0.140.0` works. Affects Intel Mac users only.  
    [openai/codex#29000](https://github.com/openai/codex/issues/29000) / [openai/codex#29047](https://github.com/openai/codex/issues/29047)

## Key PR Progress
1. **#29164 – Add cross‑platform PathUri lexical helpers**  
   Introduces safe APIs for inferred absolute paths, containment‑safe joins, and lexical descendant checks – covering POSIX, Windows drive, and UNC forms.  
   [openai/codex#29164](https://github.com/openai/codex/pull/29164)

2. **#29149 – Use gnullvm for Windows Rust exec tools**  
   First step toward hermetic Windows Bazel builds by replacing MSVC with a pinned LLVM/MinGW toolchain for exec‑side Rust tools.  
   [openai/codex#29149](https://github.com/openai/codex/pull/29149)

3. **#29082 – Add connector skills feature toggle**  
   Enables an A/B test that removes connector‑provided skills without affecting other plugin skills, MCP tools, or hooks.  
   [openai/codex#29082](https://github.com/openai/codex/pull/29082)

4. **#29108 – Carry sandbox intent to remote exec servers**  
   After making remote commands plain `argv`, this PR sends portable sandbox intent alongside, allowing remote exec servers to apply the correct sandbox wrapper.  
   [openai/codex#29108](https://github.com/openai/codex/pull/29108)

5. **#29154 – Allow resume and settings commands during tasks and MCP startup**  
   `/resume` and several settings commands were blocked while MCP startup was in progress. Now they can run concurrently, improving responsiveness.  
   [openai/codex#29154](https://github.com/openai/codex/pull/29154)

6. **#28787 – Introduce transport‑neutral session runtime**  
   Decouples session lifecycle from the protocol adapter and in‑process actor, paving the way for separate‑process transports and cleaner cancellation.  
   [openai/codex#28787](https://github.com/openai/codex/pull/28787)

7. **#29155 – Expose service tier and reasoning effort in OTEL**  
   Adds `service_tier` and `model_reasoning_effort` to the `response.completed` event in CLI OTEL logs – requested by NVIDIA for Fast‑mode usage tracking.  
   [openai/codex#29155](https://github.com/openai/codex/pull/29155)

8. **#26707 – Add shared auth system proxy contract**  
   Moves Codex‑owned auth and startup HTTP clients through a common route‑aware boundary. Default path unchanged, but enables future Windows/macOS system proxy resolution.  
   [openai/codex#26707](https://github.com/openai/codex/pull/26707)

9. **#28918 – Make selected plugin roots URI‑native**  
   Requires executor plugin roots to be sent as `file://` URIs (`PathUri`), eliminating host‑native string ambiguity and improving cross‑platform path handling.  
   [openai/codex#28918](https://github.com/openai/codex/pull/28918)

10. **#28806 – Optimize resume and fork history**  
    Implements checkpoint‑backed resume and copy‑on‑write fork, reducing cold `thread/resume` and `thread/fork` history processing time.  
    [openai/codex#28806](https://github.com/openai/codex/pull/28806)

## Feature Request Trends
- **Persistent sandbox permissions** – Multiple issues (#28988, #29117, #13117) ask for permanent “Full Access” grants that survive app restarts and updates.
- **Transparent rate‑limit accounting** – Users demand

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*