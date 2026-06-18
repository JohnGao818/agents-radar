# AI CLI Tools Community Digest 2026-06-18

> Generated: 2026-06-18 03:33 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date: 2026-06-18**

---

## 1. Ecosystem Overview

The AI CLI tools landscape continues its rapid maturation, with both Claude Code and OpenAI Codex shipping multiple releases this week while grappling with scaling pains around authentication, platform parity, and usage transparency. Community engagement remains exceptionally high—Claude Code's usage-limits issue alone has generated 1,475 comments—indicating that users are deeply invested in these tools for daily production work. Both ecosystems show a clear shift from experimental adoption to enterprise-grade expectations, with demands for regional pricing, robust remote workflows, and reliable async interaction patterns dominating the conversation. The underlying signal is clear: developers are no longer evaluating whether to use AI CLI tools, but demanding they meet the same reliability and UX standards as traditional developer tooling.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Notable Issues Today** | 10 (highlighted from backlog) | 10 (highlighted from backlog) |
| **Key PRs Updated (24h)** | 7 | 10 |
| **Today's Releases** | v2.1.181 (stable, with changelog) | 3 alpha releases (v0.141.0-alpha.5–.7, no changelog) |
| **Highest-Engagement Issue** | #16157 (1,475 comments, 691 👍) | #23794 (170 comments, 168 👍) |
| **Release Cadence Pattern** | Weekly stable releases + hotfixes | Multiple daily alphas, silent updates |

**Key observation:** Claude Code ships one well-documented release with visible feature work; Codex ships three silent alphas, suggesting either rapid internal iteration or CI automation without developer-facing documentation.

---

## 3. Shared Feature Directions

Both communities independently demand the same core capabilities, indicating strong cross-tool consensus:

| Shared Requirement | Claude Code Evidence | OpenAI Codex Evidence |
|---|---|---|
| **Real-time usage visibility** | #68931 (CPU spin at 100%), context-limit errors (#69154) | #23794 (missing token/context meter, 168 👍), #17827 (configurable status line, 71 👍) |
| **Async/non-blocking interaction** | #50246 (message queue mode, 99 👍), #68998 (queue multiple prompts) | #28813 (pause active goals before Esc), #28104 (goal lifecycle) |
| **Remote/SSH workflow improvements** | #5277 (image paste in SSH, 31 👍), #34255 (reconnection, 90 👍) | #25749 (auth lockouts blocking remote login) |
| **Authentication flexibility** | #17432 (India pricing/INR billing) | #25749 (legacy phone bypass), #25737 (passkey-only login) |
| **Platform parity (Windows/ARM)** | #39636 (Snapdragon Cowork VM, 29 comments) | #25178 (Windows screenshot COM error, 11 comments) |
| **MCP/plugin integration reliability** | #26094 (object serialization bug, 19 👍) | #28790 (plugin manifest path lists), #17574 (MCP management) |

**Synthesis:** The market is converging on three pillars—visibility into what the AI is doing, ability to work alongside it asynchronously, and frictionless remote access across all platforms.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary UX paradigm** | CLI-first with TUI; Cowork VM enables agentic sandboxes | CLI + Desktop app; real-time voice/agent identity stack |
| **Agent architecture** | Subagent hierarchy (nested routing, parent-child orchestration) | Goal lifecycle management (pause/resume, single-run tasks) |
| **Configuration surface** | `/config key=value` inline, `~/.claude/settings.json`, remote config injection | `~/.codex/instructions/*.md`, plugin manifest path lists |
| **Platform maturity** | Linux/macOS focus; Windows ARM support behind (Cowork VM bugs) | macOS Desktop app dominant; Windows/fragile; CLI rust builds cross-platform |
| **Pricing model** | Subscription (Max plan $X/month); strong India pricing demand (#17432) | Usage-based with rate limits; Business/Pro tiers |
| **Community pain tolerance** | High tolerance but vocal; 1,475 comments on one bug shows deep investment | Lower engagement per issue; more blocked users (auth lockouts) |
| **Integration depth** | VS Code extension, JetBrains WIP, MCP server ecosystem | Desktop app, ChatGPT auth convergence, plugin skills |

**Strategic takeaway:** Claude Code leans into **agentic sandboxing and orchestration** (Cowork VM, subagents, MCP) while Codex focuses on **chat-as-IDE** with real-time voice and desktop-native experiences. Claude Code's community is louder and more demanding because they're using it for heavier production workflows.

---

## 5. Community Momentum & Maturity

**Claude Code** exhibits peak community intensity:
- The #16157 usage-limits thread (1,475 comments) is unprecedented in scale for developer tooling—users are effectively organizing around a common pain point.
- Feature requests (message queue, image paste in SSH, subagent routing) show sophisticated, multi-step workflows already in production.
- PR activity reveals active internal development responding to community feedback (code-review re-review logic, Dockerfile fixes).
- **Assessment:** Mature but strained. Community is deeply invested and vocal; trust is fragile due to pricing/limit transparency issues.

**OpenAI Codex** shows rapid but quieter iteration:
- Three alpha releases in one day suggests fast CI/CD but lacks community documentation.
- The top issue (#23794, 168 👍) is less than 12% the engagement of Claude Code's top issue—indicating either a smaller user base or less vocal community.
- PRs focus on infrastructure (time synchronization, agent identity, plugin paths) rather than user-facing features.
- **Assessment:** Rapid iteration with less community transparency. Likely a younger developer adoption curve, or users who are less reliant on daily blocking workflows.

**Maturity verdict:** Claude Code has more production-critical users and thus more friction; Codex has more foundational infrastructure work and less community noise.

---

## 6. Trend Signals

Six actionable trends for developers evaluating these tools:

### 1. Pricing Localization is Becoming a Dealbreaker
The India-specific pricing request (#17432) on Claude Code (444 👍) signals that global developers expect local currency billing. OpenAI currently does not face this pressure publicly, but the market will demand parity. **Action:** Evaluate total cost of ownership in your currency and region before committing.

### 2. Async Agent Interaction is the Next UX Frontier
Both communities independently request non-blocking workflows—queue mode, goal pause/resume, interrupt handling. The era of "watch the AI type line-by-line" is ending; developers want to dispatch work and return. **Action:** Prioritize tools with mature goal lifecycle management; this will become table-stakes within 6 months.

### 3. Remote Development is a First-Class Requirement
SSH image paste (Claude Code #5277, since Aug 2025) and auth lockouts on remote machines (Codex #25749) show that CLI tools must treat remote workspaces as primary, not secondary. Cloud-based dev environments (GitHub Codespaces, AWS Cloud9) are the target deployment. **Action:** Test any tool under SSH immediately; if auth fails or features degrade, it's not production-ready.

### 4. Platform Parity is Non-Negotiable for Enterprise
Windows ARM (Snapdragon X Plus) and macOS Intel/Apple Silicon compatibility gaps are blocking real users. Claude Code's Cowork VM bug and Codex's Windows screenshot failure both indicate incomplete testing matrices. **Action:** Verify your entire team's hardware stack, especially Windows on ARM and macOS Intel with security restrictions.

### 5. Usage Transparency Builds Trust
The lack of visible token/context meters (Codex #23794) and unpredictable rate limits (Claude Code #16157) erode trust faster than any feature gap. Users are demanding telemetry they can see and act on. **Action:** Choose tools that expose real-time usage data in the UI; dark patterns will be penalized.

### 6. MCP/Plugin Ecosystem is Still Immature
Both tools struggle with MCP integration (object serialization bugs, OAuth constraints, manifest handling). The promise of a universal plugin layer is real, but implementation is fragile. **Action:** Don't bet core workflows on MCP plugins today; verify compatibility with your specific servers (Notion, VS Code, etc.) before relying on them.

---

**Analyst Verdict:** Claude Code is the heavy-lifting production tool with a more demanding user base; OpenAI Codex is iterating faster on infrastructure but has less proven community resilience. Neither has solved platform parity or pricing transparency. Choose based on your primary workflow depth (Claude Code for agentic sandboxing) vs. desktop/chat integration (Codex for real-time collaboration).

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** github.com/anthropics/skills | **Date:** 2026-06-18

---

## 1. Top Skills Ranking (Most-Discussed PRs)

### #514 – Document Typography Skill
**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents — a quality-control layer for document output.
**Discussion Highlights:** The PR identifies a universal pain point: typographic defects in every Claude-generated document. Commenters focused on whether this should be a standalone skill or integrated into core document skills. Strong consensus that the problem is real and widespread.
**Status:** OPEN ([PR #514](https://github.com/anthropics/skills/pull/514))

### #486 – ODT Skill (OpenDocument Creation & Parsing)
**Functionality:** Creates, fills, reads, and converts `.odt`/`.ods` files; parses ODT to HTML. Triggers on any mention of OpenDocument, LibreOffice, or ODF formats.
**Discussion Highlights:** The community debated scope — whether to include template filling or restrict to basic creation. Strong interest from enterprise users working in LibreOffice environments.
**Status:** OPEN ([PR #486](https://github.com/anthropics/skills/pull/486))

### #83 – Skill-Quality-Analyzer & Skill-Security-Analyzer (Meta-Skills)
**Functionality:** Two meta-skills evaluating other skills across structure/documentation (20%), code quality, security, and more. Aimed at the skill marketplace.
**Discussion Highlights:** Significant discussion around whether security analysis should be a mandatory gating step before skills are accepted. Some concern about meta-skills becoming a bottleneck in the submission pipeline.
**Status:** OPEN ([PR #83](https://github.com/anthropics/skills/pull/83))

### #181 – SAP-RPT-1-OSS Predictor Skill
**Functionality:** Interfaces with SAP's open-source tabular foundation model for predictive analytics on SAP business data (released at SAP TechEd 2025).
**Discussion Highlights:** Enterprise-focused attention; commenters noted the narrow domain but high value for SAP customers. Questions about API key management and model hosting surfaced.
**Status:** OPEN ([PR #181](https://github.com/anthropics/skills/pull/181))

### #1298 – skill-creator: Fix run_eval.py 0% Recall Bug
**Functionality:** Repairs the core evaluation loop that was reporting `recall=0%` for all descriptions, making the description-optimization loop useless. Also fixes Windows stream reading, trigger detection, and parallel workers.
**Discussion Highlights:** 10+ independent reproductions confirm the bug. This is the most critical infrastructure fix in the queue — multiple contributors have been blocked from developing new skills.
**Status:** OPEN ([PR #1298](https://github.com/anthropics/skills/pull/1298))

### #723 – Testing Patterns Skill
**Functionality:** Comprehensive testing skill covering the Testing Trophy model, AAA unit test patterns, React component testing with Testing Library, integration testing, and E2E testing.
**Discussion Highlights:** Commenters requested additional coverage for mocking strategies and snapshot testing. Generally positive reception; seen as filling a gap in the developer workflow skillset.
**Status:** OPEN ([PR #723](https://github.com/anthropics/skills/pull/723))

### #568 – ServiceNow Platform Skill
**Functionality:** Broad ServiceNow assistant covering ITSM, ITOM, ITAM/SAM, FSM, HRSD, CSDM, Vulnerability Response, Security Incident Response, and IntegrationHub.
**Discussion Highlights:** One of the most comprehensive enterprise skills proposed. Discussion centered on whether it should be split into multiple focused skills. Strong demand from IT operations teams.
**Status:** OPEN ([PR #568](https://github.com/anthropics/skills/pull/568))

---

## 2. Community Demand Trends (from Issues)

| Trend | Key Issues | Signal |
|---|---|---|
| **Skill Discovery & Sharing** | [#228](https://github.com/anthropics/skills/issues/228) – org-wide sharing; [#184](https://github.com/anthropics/skills/issues/184) – agentskills.io broken | High — users want better distribution mechanisms beyond manual file transfers |
| **Skill-Creator Tooling Reliability** | [#556](https://github.com/anthropics/skills/issues/556) – run_eval 0% trigger rate; [#1169](https://github.com/anthropics/skills/issues/1169) – identical recall bug; [#1061](https://github.com/anthropics/skills/issues/1061) – Windows compatibility; [#202](https://github.com/anthropics/skills/issues/202) – outdated skill-creator design | **Critical** — multiple issues confirm the skill-development loop is fundamentally broken for many users |
| **Deduplication & Plugin Architecture** | [#189](https://github.com/anthropics/skills/issues/189) – duplicate skills from overlapping plugins | Moderate — ecosystem needs better dependency management |
| **Security & Trust Boundaries** | [#492](https://github.com/anthropics/skills/issues/492) – community skills under anthropic/ namespace; [#1175](https://github.com/anthropics/skills/issues/1175) – context window concerns with SPO documents | Growing — as skills gain system access, governance becomes a concern |
| **Enterprise Integration** | [#29](https://github.com/anthropics/skills/issues/29) – Bedrock support; [#412](https://github.com/anthropics/skills/issues/412) – agent-governance skill proposal | Moderate — enterprise users need cloud deployment and safety patterns |
| **Skill Format Evolution** | [#1220](https://github.com/anthropics/skills/issues/1220) – multi-file bundling; [#16](https://github.com/anthropics/skills/issues/16) – MCP exposure | Emerging — users want richer skill packaging and protocol integration |

**Most-Anticipated New Skill Directions:**
1. **Agent Governance / Safety Patterns** — Policy enforcement, threat detection, audit trails for agent systems
2. **Multi-Format Document Handling** — ODT, typography fixes, better PDF/Office support
3. **Enterprise Platform Integrations** — ServiceNow, SAP, SharePoint Online
4. **Developer Workflow Automation** — Testing patterns, code review, CI/CD integration

---

## 3. High-Potential Pending Skills (Active PRs Likely to Land Soon)

| PR | Skill | Why It May Land Soon |
|---|---|---|
| [#1298](https://github.com/anthropics/skills/pull/1298) | fix(run_eval): 0% recall + Windows fixes | **Highest priority** — unblocks all skill-creator users; multiple contributors; recent activity (June 2026) |
| [#1099](https://github.com/anthropics/skills/pull/1099) | fix(run_eval): Windows subprocess crash | Complements #1298; focused OS compatibility fix |
| [#1050](https://github.com/anthropics/skills/pull/1050) | fix(skill-creator): Windows subprocess + encoding | Additional Windows fix; 1-line changes per bug — minimal review burden |
| [#361](https://github.com/anthropics/skills/pull/361) | Detect unquoted YAML special characters | Direct fix for silent parsing failures; complements #539 (already in review) |
| [#362](https://github.com/anthropics/skills/pull/362) | Fix UTF-8 panic on multi-byte characters | Prevents Rust panics in CLI; clear root cause and solution |
| [#181](https://github.com/anthropics/skills/pull/181) | SAP-RPT-1-OSS predictor | Strong enterprise demand; well-scoped |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns skill | Broad developer appeal; fills a clear gap |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliable skill-authoring infrastructure (run_eval, Windows compatibility, YAML validation, multi-byte support) rather than new skill content — the development loop itself is the bottleneck, with 4 of the top 10 most-discussed PRs and 4 of the top 15 most-commented issues all addressing tooling bugs that prevent skill creation and evaluation.**

---

# Claude Code Community Digest – 2026-06-18

## Today’s Highlights

A new release (v2.1.181) introduces inline setting configuration via `/config` and opt-in Apple Events support for sandboxed commands. The community remains focused on a long-running usage-limits bug (#16157, 1475 comments) that continues to frustrate Max subscribers, while a strong call for India-specific pricing (#17432, 444 👍) reflects growing global demand. Several critical bug reports emerged around subagent routing and an idle CPU busy-spin on macOS ARM64.

## Releases

**v2.1.181** (released today)  
[View on GitHub](https://github.com/anthropics/claude-code/releases/tag/v2.1.181)  

- **`/config key=value` syntax** – now works in interactive, `-p`, and Remote Control modes, allowing settings like `thinking=false` to be changed inline.  
- **`sandbox.allowAppleEvents`** – new opt-in setting enables sandboxed commands to send Apple Events on macOS.  
- **`CLAUDE_CLIENT_P…`** – additional client‑side configuration (details incomplete in changelog).  

## Hot Issues (10 of note)

1. **[#16157] Instantly hitting usage limits with Max subscription**  
   *Bug | macos, cost, api* | 1475 comments, 691 👍  
   Users with Max plans report being throttled immediately after reset. Community reaction is intense, with many citing broken trust in pricing promises.  
   [Issue link](https://github.com/anthropics/claude-code/issues/16157)

2. **[#17432] India‑Specific Pricing Plans (INR)**  
   *Enhancement | cost, external* | 198 comments, 444 👍  
   Users request locally priced plans analogous to OpenAI and Google offerings. High reaction indicates strong market demand.  
   [Issue link](https://github.com/anthropics/claude-code/issues/17432)

3. **[#34255] Remote Control: automatic reconnection broken**  
   *Bug | macos, ios* | 50 comments, 90 👍  
   Connection drops silently without recovery, forcing manual intervention. Affects productivity for remote workflows.  
   [Issue link](https://github.com/anthropics/claude-code/issues/34255)

4. **[#50246] Message queue mode**  
   *Enhancement | tui* | 32 comments, 99 👍  
   Users want to queue prompts while Claude is busy instead of interrupting. Resonates with anyone doing complex multi‑step tasks.  
   [Issue link](https://github.com/anthropics/claude-code/issues/50246)

5. **[#39636] Cowork VM guest kernel never boots on Snapdragon X Plus (ARM64)**  
   *Bug | windows, cowork* | 29 comments, 9 👍  
   Connection timeout on Windows ARM devices – a critical blocker for ARM users of the Cowork feature.  
   [Issue link](https://github.com/anthropics/claude-code/issues/39636)

6. **[#25128] Drag and drop not working in VS Code extension chat panel**  
   *Bug | macos, ide* | 20 comments, 40 👍  
   Regression introduced in v2.1.6. Works in CLI but the VS Code panel is broken; disrupts file sharing workflows.  
   [Issue link](https://github.com/anthropics/claude-code/issues/25128)

7. **[#63870] Bash tool calls emitted as raw `<invoke>` text**  
   *Bug | macos, model, bash* | 17 comments, 20 👍  
   Instead of executing, Bash tool invocations are printed as literal text. Contains detailed JSONL evidence from 23 malformed calls.  
   [Issue link](https://github.com/anthropics/claude-code/issues/63870)

8. **[#5277] Image paste in SSH / remote sessions**  
   *Question | linux, tui* | 17 comments, 31 👍  
   Users developing on remote servers via SSH cannot paste images into the CLI. A long‑standing request (since Aug 2025).  
   [Issue link](https://github.com/anthropics/claude-code/issues/5277)

9. **[#26094] MCP object parameters serialized as strings, breaking Notion MCP**  
   *Bug | desktop, MCP* | 13 comments, 19 👍  
   Claude Desktop serialises object parameters incorrectly, causing write failures with MCP servers like Notion.  
   [Issue link](https://github.com/anthropics/claude-code/issues/26094)

10. **[#68931] Idle session pinned at ~100% CPU (event‑loop busy‑spin) on macOS ARM64**  
    *Bug | macos, tui, perf* | 3 comments, 0 👍 (recent)  
    Intermittent high CPU usage with no agent activity – heats up machine and fans spin. Impacts all macOS users.  
    [Issue link](https://github.com/anthropics/claude-code/issues/68931)

## Key PR Progress (7 items, all updated in the last 24h)

1. **[#41611] Add the missing source to Claude Code**  
   Small fix adding a missing source reference. Open since March.  
   [PR link](https://github.com/anthropics/claude-code/pull/41611)

2. **[#41447] feat: open source Claude Code ✨**  
   Symbolic PR attempting to open‑source the codebase. Closes multiple old issues. Unlikely to be merged but reflects community desire.  
   [PR link](https://github.com/anthropics/claude-code/pull/41447)

3. **[#69226] Update frontend‑design skill (merged/closed)**  
   Bumps plugin version to 1.1.0 with improvements to the frontend‑design skill. Installed copies will auto‑update.  
   [PR link](https://github.com/anthropics/claude-code/pull/69226)

4. **[#19867] fix(code‑review): allow re‑reviews when new commits are pushed**  
   Smart skip logic added – Claude will now re‑review if new commits exist since its last comment. `--force` flag to bypass.  
   [PR link](https://github.com/anthropics/claude-code/pull/19867)

5. **[#33443] fix: Update Dockerfile to use native installer**  
   Moves from deprecated `npm install` to native install for claude‑code in dev containers, using Node 24.14.  
   [PR link](https://github.com/anthropics/claude-code/pull/33443)

6. **[#60427] docs: use standard GitHub capitalization in README** (closed)  
   Minor branding fix in README.  
   [PR link](https://github.com/anthropics/claude-code/pull/60427)

7. **[#60732] docs: polish plugins README wording** (closed)  
   Tweaked one sentence for natural reading.  
   [PR link](https://github.com/anthropics/claude-code/pull/60732)

## Feature Request Trends

The most‑requested feature directions from recent issues are:

- **Regional pricing & billing** – India‑specific INR plans (#17432) and broader frustration with USD‑only subscriptions. Expect more pressure for localised plans.
- **Non‑blocking interaction** – Message queue mode (#50246) and queue‑multiple‑prompts (#68998) reflect a strong desire to work asynchronously without interrupting active agents.
- **Remote & SSH improvements** – Image paste in SSH (#5277), remote MCP OAuth viability (#69205), and better remote control reconnection (#34255) dominate the remote‑workflow wishlist.
- **Subagent hierarchy** – Recent bugs (#69212, #69249) and requests for subagent result routing to the correct parent indicate growing interest in nested agent orchestration.
- **IDE integration polish** – Auto‑accept edits in JetBrains (#69241), fixing drag‑drop in VS Code (#25128), and eliminating process pollution (#69227) show users want seamless editor integration.

## Developer Pain Points

Recurring frustrations that have generated high community engagement:

- **Usage limit unpredictability** – #16157 (1475 comments) is the biggest pain point. Max subscribers feel misled and are demanding transparency on rate limits.
- **Windows / ARM compatibility** – Cowork on Snapdragon X Plus (#39636), keyboard conflicts (#23146), and GPU crash loops (#68956) show Windows support remains fragile.
- **Tool execution regressions** – Bash tool emitting raw text (#63870) and “Unhandled case” banner halting execution (#59156) are alarming for reliability.
- **MCP integration glitches** – Object parameter serialisation (#26094) breaks server integration. Combined with OAuth constraints on remote machines (#69205), this is a blocker for serious MCP usage.
- **Performance issues** – Idle CPU busy‑spin on macOS (#68931) and hidden scrollbar on Windows dark themes (#69250) degrade daily UX.
- **Context length / cost friction** – The 1M‑context usage‑credits error (#69154) and disappearing model options (#69109) add to billing confusion.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-18

*Technical analysis of the openai/codex repository by an AI developer tools analyst.*

---

## 1. Today's Highlights

Three rust alpha releases (v0.141.0-alpha.5 through .7) landed without changelog details, but the community remains focused on unresolved platform stability and authentication issues. The most active thread this week is a closed bug about the missing visible context/token indicator in Codex Desktop, which amassed 170 comments and 168 👍, underscoring strong demand for real‑time usage visibility. Meanwhile, several high‑impact PRs are laying groundwork for app‑server time synchronization, improved plugin manifest handling, and goal lifecycle management.

---

## 2. Releases

Three new **rust** pre‑releases were published in the last 24 hours:
- [rust-v0.141.0-alpha.5](https://github.com/openai/codex/releases/tag/rust-v0.141.0-alpha.5)
- [rust-v0.141.0-alpha.6](https://github.com/openai/codex/releases/tag/rust-v0.141.0-alpha.6)
- [rust-v0.141.0-alpha.7](https://github.com/openai/codex/releases/tag/rust-v0.141.0-alpha.7)

No accompanying notes or feature lists were published; these appear to be incremental build chain updates.

---

## 3. Hot Issues

*Top 10 noteworthy issues, ranked by community engagement and impact.*

1. **[#23794] Codex Desktop no longer shows visible context/token usage indicator**  
   *Closed* – 170 comments, 168 👍  
   A regression in the latest desktop update removed the in‑app token/context meter. User backlash is significant, as real‑time visibility is critical for managing long sessions.  
   [Link](https://github.com/openai/codex/issues/23794)

2. **[#25749] Codex requires verification of an inaccessible legacy phone number**  
   *Open* – 49 comments, 30 👍  
   Users with MFA and Google OAuth cannot bypass an old phone‑number OTP step, effectively locking them out of Codex Desktop while ChatGPT web works fine.  
   [Link](https://github.com/openai/codex/issues/25749)

3. **[#25719] macOS Codex Desktop triggers syspolicyd / trustd CPU and memory runaway**  
   *Open* – 31 comments, 39 👍  
   Persistent high CPU usage from system security daemons, likely related to code signing checks on repeated Electron restarts. Affects both Intel and Apple Silicon.  
   [Link](https://github.com/openai/codex/issues/25719)

4. **[#17827] Customizable status line in TUI**  
   *Enhancement* – 16 comments, 71 👍  
   Request to match Claude Code’s configurable bottom bar (token usage, model, rate limits, git branch). High community demand.  
   [Link](https://github.com/openai/codex/issues/17827)

5. **[#21211] Thread navigation/loading slows from unbounded metadata and eager hydration**  
   *Open* – 12 comments, 2 👍  
   Performance degrades as thread count grows; SQLite bloat and eager history hydration are root causes. A long‑standing pain point for heavy users.  
   [Link](https://github.com/openai/codex/issues/21211)

6. **[#24006] Codex cannot access its local database after macOS update**  
   *Open* – 11 comments, 9 👍  
   App fails to launch with “database disk image is malformed”; common after version bumps. Still no official recovery tool.  
   [Link](https://github.com/openai/codex/issues/24006)

7. **[#25737] Codex CLI login forces SMS OTP step‑up on security‑key‑only accounts**  
   *Open* – 11 comments, 6 👍  
   Even with FIDO2 hardware keys, the CLI forces a phone OTP flow that the web login correctly skips.  
   [Link](https://github.com/openai/codex/issues/25737)

8. **[#25178] Windows Computer Use screenshot fails on Windows 10 22H2**  
   *Open* – 11 comments, 4 👍  
   `SetIsBorderRequired` call fails with a COM error, breaking screenshot capture for remote‑control workflows.  
   [Link](https://github.com/openai/codex/issues/25178)

9. **[#25921] Crashpad pending dumps grow without limit (+5 GB/day)**  
   *Open* – 9 comments, 2 👍  
   Unbounded crash report accumulation under `~/Library/Application Support/com.openai.codex/web/Crashpad/pending` can fill disks rapidly.  
   [Link](https://github.com/openai/codex/issues/25921)

10. **[#8190] “Codex ran out of room in the model’s context window” error**  
    *Open* – 8 comments, 2 👍  
    Users hitting context limits even after clearing history; likely a compact/remote‑compact bug not fully resolved.  
    [Link](https://github.com/openai/codex/issues/8190)

---

## 4. Key PR Progress

*Top 10 pull requests showing active development, including long‑running features and critical fixes.*

1. **[#28835] Add app-server current-time implementation (varlatency 3/n)**  
   Implements a `currentTime/read` method for server‑side time awareness.  
   [Link](https://github.com/openai/codex/pull/28835)

2. **[#28836] Support assistant realtime append text**  
   Enables replaying voice‑overlap segments as conversation items in realtime sessions.  
   [Link](https://github.com/openai/codex/pull/28836)

3. **[#28790] Support plugin manifest path lists**  
   Allows plugins to expose skills from multiple directories via `skills` array syntax.  
   [Link](https://github.com/openai/codex/pull/28790)

4. **[#19049] feat: opt ChatGPT auth into agent identity**  
   Part of the HAI single‑run‑task stack; introduces JWT‑based agent identity for task registration.  
   [Link](https://github.com/openai/codex/pull/19049)

5. **[#19051] feat: use run agent task auth for inference**  
   Continues the agent identity stack by wiring authentication into inference calls.  
   [Link](https://github.com/openai/codex/pull/19051)

6. **[#28838] Support Codex home instructions directory**  
   Loads `~/.codex/instructions/*.md` as global instructions, preserving existing override precedence.  
   [Link](https://github.com/openai/codex/pull/28838)

7. **[#28813] Pause active goals before Esc interrupts**  
   Fixes #28104: pressing `Esc` now updates goal status to paused (matching `Ctrl+C` behaviour).  
   [Link](https://github.com/openai/codex/pull/28813)

8. **[#28814] Assign response item IDs when recording history**  
   Ensures client‑created response items get stable IDs for reliable resume and rollout persistence.  
   [Link](https://github.com/openai/codex/pull/28814)

9. **[#28824] Current time reminders impl for system clock (varlatency 2/n)**  
   Adds host‑injectable time provider and records UTC developer reminders before model requests.  
   [Link](https://github.com/openai/codex/pull/28824)

10. **[#28784] fix(install): support older awk checksum parsing**  
    Fixes an installer bug affecting systems with `mawk` where SHA checksum extraction failed.  
    [Link](https://github.com/openai/codex/pull/28784)

---

## 5. Feature Request Trends

The most consistent feature demands from recent issues and PRs fall into three categories:

- **Real‑time usage visibility** – Users want a persistent token/context indicator in both the Desktop app and TUI (see #23794, #17827).
- **Authentication flexibility** – Requests for passkey‑only login paths, phone‑number removal, and “Advanced Account Security“ support in the CLI (#25749, #25737).
- **Customisable terminal UI** – A configurable status line (model, rate limits, git branch) is the top‑voted enhancement (#17827).

Other recurring themes include improved thread performance (#21211), better MCP plugin management (#17574, #27132), and a more robust goal/pause system (#28104 / #28813).

---

## 6. Developer Pain Points

Several high‑frequency bugs create recurring friction for the developer community:

- **Database corruption after updates** – The `state_5.sqlite` malformed error (#24030, #24006) reappears with nearly every new release, with no automated repair path.
- **Auth lockouts** – Legacy phone‑number verification (#25749) and SMS step‑up on security‑key accounts (#25737) block routine access, especially for Business/Pro users.
- **Performance regressions** – macOS syspolicyd runaway (#25719), unbounded Crashpad dumps (#25921), and thread-loading slowdowns (#21211) affect daily workflows.
- **Cross‑platform inconsistencies** – Windows Computer Use screenshot failures (#25178) and macOS Intel locked‑operation signing errors (#24207) fragment the user experience.
- **Rate limit / meter inaccuracies** – The 5‑hour usage meter sometimes reports faster consumption than telemetry (#28823), and the reset button fails (#28380), causing confusion.

These pain points suggest that stability, authentication, and cross‑platform parity remain the top priorities for engineering.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*