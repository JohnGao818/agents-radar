# AI CLI Tools Community Digest 2026-06-07

> Generated: 2026-06-07 03:30 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date**: 2026-06-07 | **Scope**: Claude Code, OpenAI Codex

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem is experiencing a maturation phase where **reliability and session management** have overtaken raw feature velocity as the dominant community concern. Both Claude Code and OpenAI Codex face similar growing pains—extended session failures, data persistence bugs, and integration friction with external systems (MCP, custom models, proxies)—indicating that the user base has moved past experimentation into production dependency. A clear divergence is emerging: Claude Code's community is grappling with **model-specific regressions** tied to Opus version updates, while Codex users are increasingly focused on **cross-platform compatibility and self-hosted model support**. Both ecosystems show strong demand for **autonomous/multi-agent workflows**, signaling that developers now expect these tools to operate as long-running infrastructure rather than interactive assistants.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Hot Issues Tracked** | 10 | 10 |
| **PRs in Progress** | 5 | 10 |
| **Recent Release** | v2.1.168 (bug-fix) | None in last 24h |
| **Top-Reaction Issue** | #22543 (201 👍) – Cowork VM perf | #13018 (103 👍) – Thread deletion |
| **Critical Regressions** | Opus 4.7/4.8 thinking blocks, tool-call parsing | Chat history loss post-update, MCP namespace breaks |
| **Security/Sandbox PRs** | 1 (env forwarding) | 1 (config permission overrides) |

**Key observation**: Codex is in a more active development cycle (2× the open PRs) but has no recent release, whereas Claude Code shipped a patch while still carrying a backlog of high-severity unaddressed issues.

---

## 3. Shared Feature Directions

Four cross-cutting requirements are materializing across both tool communities:

- **Autonomous/Multi-Agent Pipelines**
  - *Claude Code*: Proposal #56913 for tiered Opus brains + Sonnet workers with persistent state
  - *Codex*: Underlying architecture (side threads #26754, strict mode images #25704) supporting agentic patterns
  - *Signal*: Both communities want long-running task orchestration, not just single-turn coding

- **MCP Ecosystem and Custom Model Interoperability**
  - *Claude Code*: OAuth trailing-slash bug (#52871), `allowed-tools` vs agent tools confusion (#65916)
  - *Codex*: MCP namespace tools broken for non-OpenAI providers (#26234), ongoing MCP UI capabilities PR (#26686)
  - *Signal*: Developers need MCP to work transparently across model backends—this is a blocker for enterprise adoption

- **Effective Session Management**
  - *Claude Code*: Remote session resync after drops (#28571), plan upgrade not resetting limits (#29223)
  - *Codex*: History disappearance (#20741, #23979), hidden conversations beyond recent-50 (#21128), thread deletion (#13018)
  - *Signal*: Session state is a first-class asset; data loss is the #1 trust-eroding issue

- **Tool-Call Reliability**
  - *Claude Code*: "Could not be parsed" errors (#62123) after long-form text
  - *Codex*: CJK duplication causing token overflow (#26305), namespace flattening bugs
  - *Signal*: Model-generated tool calls are still brittle, especially with non-English content and extended sessions

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary Pain Points** | Model-version regressions (Opus thinking), performance bloat, billing UX | Session data loss, cross-platform gaps, custom model friction |
| **Target User Profile** | Heavy IDE users (VSCode) and agentic workflow builders | CLI-first power users, local model enthusiasts, cross-platform teams |
| **Development Philosophy** | Plugin ecosystem + deep model integration | Extension API + platform abstraction (path URIs, global instructions decoupling) |
| **Technical Risk Profile** | Model-dependent failures (version upgrades break features) | Platform-dependent failures (OS-specific rendering, Windows quirks) |
| **Community Innovation** | Autonomous agent architecture proposals, design system plugins | Worktree/tmux workflows, standalone web search, structured instruction snapshots |
| **Enterprise Readiness** | MCP OAuth and proxy gaps blocking deployments | Permission sandbox (#26839), cross-platform path URIs (#26840) addressing infra needs |

**Critical differentiation**: Claude Code's architecture is tightly coupled to Anthropic's model capabilities, making it vulnerable to upstream model changes (Opus 4.7→4.8 thinking regression). Codex's approach—building extension APIs, decoupled instruction loading, and cross-platform abstractions—signals a bet on **platform durability** over model specificity. This will matter for organizations choosing long-term tool investments.

---

## 5. Community Momentum & Maturity

**Claude Code** has a **higher-engagement but more volatile community**: the top issue (#22543) received 201 👍, and multiple issues exceed 40 comments. The community is actively proposing architectural solutions (tiered agent systems, plugin redesigns), indicating sophisticated, invested users. However, the **rate of open regressions** (Opus thinking across two consecutive versions, recurring tool-call failures) suggests the development cycle is reactive to model changes rather than proactive. The minor v2.1.168 release with undocumented fixes does not inspire confidence in addressing root causes.

**OpenAI Codex** shows **broader but lower-engagement issue volume**: top issue (#13018) at 103 👍, most around 15–20. This could reflect either a smaller user base or higher satisfaction—but the **persistent chat history bugs** (multiple issues reporting the same pattern since May 22) indicate a systemic quality gap. The **PR pipeline is stronger**: 10 open PRs actively refactoring core architecture (global instructions, path URIs, MCP capabilities) versus Claude Code's 5 (mostly documentation and small fixes). Codex is investing in **platform groundwork** while still shipping features (standalone web search, side thread fixes).

**Maturity verdict**: Codex is iterating faster on infrastructure; Claude Code has a more vocal, architecturally-minded user base pushing for advanced features despite reliability gaps.

---

## 6. Trend Signals

Four industry trends emerge from this cross-tool analysis:

1. **Session persistence is the new reliability frontier**
   Both tools face the same fundamental failure: users cannot trust that their work survives updates, connection drops, or timeouts. This will drive investment in **transactional session storage** and **resumable conversation state**—likely a competitive differentiator within 6 months.

2. **Custom model support is non-negotiable for expansion**
   Codex's MCP namespace bug (#26234) and Claude Code's missing `ANTHROPIC_BASE_URL` forwarding (#65875) both block self-hosted deployments. As enterprises seek data sovereignty, the inability to route through proxies (LiteLLM, Bifrost) or local models (Ollama, LM Studio) will become an adoption ceiling.

3. **"Tool-call glue" is the unsolved ergonomic problem**
   Both communities report model-generated tool calls failing in unpredictable ways—especially with long context, non-English content, or non-OpenAI providers. The **serialization/deserialization layer** between model output and tool execution is a systemic fragility that no tool has fully addressed.

4. **Multi-agent architectures require platform-level primitives**
   Claude Code's #56913 (tiered brains) and Codex's side-thread preparation (#26754) both point to a future where AI CLI tools are **orchestration platforms**, not single-agent assistants. The tools that provide first-class agent routing, state management, and process isolation will define the next generation.

**Recommendation for developers**: If you prioritize **cutting-edge model capabilities** and have flexibility to work around regressions, Claude Code's community is shaping the agentic future. If you need **reliable session management, custom model integration, and cross-platform consistency**, Codex's infrastructure investments better serve production deployments—but wait for the history persistence bugs to be resolved.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
*Data as of 2026‑06‑07 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Pull Requests represent the most actively discussed new Skill submissions, based on comment volume and community engagement. All remain **open** as of the data snapshot.

| # | Skill / PR | Functionality | Discussion Highlights | Link |
|---|------------|---------------|----------------------|------|
| 1 | **document-typography** (#514) | Prevents orphan words/widows and numbering misalignment in AI‑generated documents – a universal pain point. | High interest due to broad applicability; comments focus on edge cases and integration with existing doc skills. | [PR #514](https://github.com/anthropics/skills/pull/514) |
| 2 | **ODT skill** (#486) | Creates, fills, reads, and converts OpenDocument files (.odt/.ods) – essential for LibreOffice/ISO‑standard workflows. | Discussion covers template filling edge cases and ODT‑to‑HTML conversion accuracy. | [PR #486](https://github.com/anthropics/skills/pull/486) |
| 3 | **skill‑quality‑analyzer & skill‑security‑analyzer** (#83) | Meta‑skills that evaluate skills across five quality dimensions and detect security issues. | Considerable debate about scoring criteria and false‑positive rates for security checks. | [PR #83](https://github.com/anthropics/skills/pull/83) |
| 4 | **SAP‑RPT‑1‑OSS predictor** (#181) | Integrates SAP’s open‑source tabular foundation model for predictive analytics on business data. | Discussion of model hosting, latency, and licensing within the Skills ecosystem. | [PR #181](https://github.com/anthropics/skills/pull/181) |
| 5 | **testing‑patterns** (#723) | Covers the full testing stack: philosophy (Trophy model), unit testing, React component testing, E2E, and visual testing. | Highly praised for completeness; ongoing conversation about balancing breadth vs. token consumption. | [PR #723](https://github.com/anthropics/skills/pull/723) |
| 6 | **ServiceNow platform** (#568) | Broad assistant for ITSM, ITOM, ITAM, FSM, SecOps, and IntegrationHub – not limited to scripting. | Community feedback requesting split into smaller, focused skills; author defending unified approach. | [PR #568](https://github.com/anthropics/skills/pull/568) |
| 7 | **shodh‑memory** (#154) | Persistent memory system that surfaces relevant context across conversations using `proactive_context`. | Discussion of privacy implications and memory eviction strategies. | [PR #154](https://github.com/anthropics/skills/pull/154) |
| 8 | **feature‑dev** (#363) | Fixes a TodoWrite overwrite bug that causes workflow phases to be skipped – addresses a core workflow reliability issue. | Community contributors validating the fix across multiple use‑cases; high‑urgency patching. | [PR #363](https://github.com/anthropics/skills/pull/363) |

---

## 2. Community Demand Trends

The Issues tracker reveals the community’s strongest unmet needs:

| Trend | Example Issue(s) | Description |
|-------|------------------|-------------|
| **Org‑wide skill sharing** | [#228](https://github.com/anthropics/skills/issues/228) (13 comments, 7 👍) | Users want a shared skill library or direct sharing links instead of manual file transfer. |
| **Reliable evaluation tooling** | [#556](https://github.com/anthropics/skills/issues/556) (11 comments, 6 👍), [#202](https://github.com/anthropics/skills/issues/202) | `run_eval.py` bug causing 0% trigger rates; demand for a best‑practice skill‑creator that is operational, not educational. |
| **Windows compatibility** | Implicit in multiple bug reports (e.g., [#556](https://github.com/anthropics/skills/issues/556) subprocess issues) | Subprocess and encoding bugs break skill‑creator and evaluation on Windows – cross‑platform support is a top pain point. |
| **Security & trust boundary** | [#492](https://github.com/anthropics/skills/issues/492) (7 comments, 2 👍) | Community skills distributed under `anthropic/` namespace create trust‑boundary risks; need for clear labeling or sandboxing. |
| **Duplicate / confusing installations** | [#189](https://github.com/anthropics/skills/issues/189) (6 comments, 8 👍) | `document-skills` and `example-skills` plugins install identical content, wasting context window. |
| **Agent governance patterns** | [#412](https://github.com/anthropics/skills/issues/412) (4 comments) | Proposed skill for policy enforcement, threat detection, and audit trails – interest in safety‑critical agent behavior. |
| **Multi‑file reference preloading** | [#1220](https://github.com/anthropics/skills/issues/1220) (2 comments) | Skills split across multiple `.md` files don’t get bundled; request for inline bundling or multi‑file delivery. |

---

## 3. High‑Potential Pending Skills

These active‑comment PRs are likely to land soon, based on recent updates and clear utility:

| Skill / PR | Key Feature | Recent Activity | Link |
|------------|-------------|-----------------|------|
| **agent‑creator** (#1140) | Meta‑skill for task‑specific agent sets; fixes multi‑tool evaluation & Windows support. | Updated 2026‑06‑02; addresses issue #1120. | [PR #1140](https://github.com/anthropics/skills/pull/1140) |
| **Windows subprocess fixes** (#1099, #1050) | Fixes `run_eval.py` crash and subprocess encoding on Windows 11. | Both updated late May 2026; critical for non‑macOS users. | [#1099](https://github.com/anthropics/skills/pull/1099), [#1050](https://github.com/anthropics/skills/pull/1050) |
| **AURELION skill suite** (#444) | Four skills (kernel, advisor, agent, memory) for structured cognitive + memory framework. | Updated 2026‑05‑06; comprehensive framework with broad appeal. | [PR #444](https://github.com/anthropics/skills/pull/444) |
| **Masonry image/video generation** (#335) | Generates images and videos via Imagen 3.0 / Veo 3.1; job management included. | Updated 2026‑03‑14; addresses growing demand for generative media skills. | [PR #335](https://github.com/anthropics/skills/pull/335) |
| **n8n‑builder & n8n‑debugger** (#190) | Expert‑level n8n workflow building and debugging, plus faf‑expert for persistent context. | Updated 2026‑05‑18; production‑tested, low risk. | [PR #190](https://github.com/anthropics/skills/pull/190) |

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for infrastructure robustness (Windows compatibility, evaluation reliability, security governance) and enterprise‑grade skill content (SAP, ServiceNow, ODT, governance patterns), while also pushing for meta‑tools that help create, analyze, and share skills safely across organizations.**

---

# Claude Code Community Digest — 2026-06-07

## Today's Highlights
A minor bug‑fix release (v2.1.168) landed, though the community remains focused on three persistent themes: **Opus extended‑thinking rendering failures** (both 4.7 and 4.8), a **severe performance regression** caused by the Cowork feature’s 10 GB VM bundle, and growing demand for **autonomous multi‑agent workflows**. Several high‑impact bugs (parsing errors, MCP OAuth breakage, and false‑positive policy blocks) continue to generate active discussion.

## Releases
- **v2.1.168** — Contains bug fixes and reliability improvements. No new features or breaking changes were documented.

## Hot Issues (10 selected)
1. **[🐛 #22543 – Cowork 10 GB VM bundle degrades performance](https://github.com/anthropics/claude-code/issues/22543)**  
   High‑priority, on‑call bug with 201 👍. The Cowork feature creates a 10 GB bundle under `~/Library/Application …`, causing severe UI lag and slow startup. Community is requesting an immediate fix or a configuration option.

2. **[🐛 #62123 – Tool call could not be parsed (Opus 4.7, macOS/VSCode)](https://github.com/anthropics/claude-code/issues/62123)**  
   48 comments, 97 👍. Models’ tool calls fail with “could not be parsed (retry also failed)”, halting workflows. Reproduction widespread on macOS+VSCode.

3. **[🐛 #49322 – Opus 4.7 thinking summaries not rendered in VSCode](https://github.com/anthropics/claude-code/issues/49322)**  
   44 comments. The extended‑thinking “summarized” display is missing in the VS Code extension, making the feature nearly unusable for IDE users.

4. **[🐛 #49268 – Harness doesn’t set display: "summarized" for Opus 4.7](https://github.com/anthropics/claude-code/issues/49268)**  
   44 comments, 70 👍. Root cause identified: the API default for `display` changed in Opus 4.7, but Claude Code’s harness does not request summarization. A fix is pending.

5. **[🐛 #23377 – GitHub Issue Prompt Too Long](https://github.com/anthropics/claude-code/issues/23377)**  
   42 comments. When processing GitHub issues with large context, the prompt exceeds allowed limits, causing failures. Workaround: manual truncation.

6. **[🌟 #56913 – Make autonomous Claude Code viable](https://github.com/anthropics/claude-code/issues/56913)**  
   26 comments. A detailed proposal for tiered Opus brains + Sonnet workers + persistent state to enable long‑running autonomous pipelines. High interest despite initial 0 👍 (likely because it’s an enhancement – community is discussing architecture).

7. **[🐛 #29223 – Plan upgrade not resetting session limits](https://github.com/anthropics/claude-code/issues/29223)**  
   20 comments, 27 👍. Upgrading a plan still leaves the rate limit stuck at the old tier until a new session is started – a billing/user‑experience bug.

8. **[🐛 #52871 – MCP OAuth trailing slash breaks Entra ID auth](https://github.com/anthropics/claude-code/issues/52871)**  
   17 comments. The `resource` parameter in OAuth flow has a trailing slash, causing `AADSTS9010010` errors. Enterprise users are blocked.

9. **[🐛 #28571 – Remote control session fails to resync after connection drop](https://github.com/anthropics/claude-code/issues/28571)**  
   17 comments, 50 👍. iOS ↔ desktop remote sessions silently disconnect with no indication; messages go missing. Needs resync logic.

10. **[🐛 #63358 – Opus 4.8 empty thinking blocks](https://github.com/anthropics/claude-code/issues/63358)**  
    10 comments (rapidly growing). Same regression as #49268 now affects Opus 4.8 – thinking blocks are returned empty, so nothing is displayed in chat.

## Key PR Progress (5 total)
1. **[🚀 #39370 – feat(plugins): add frontend‑design‑system plugin](https://github.com/anthropics/claude-code/pull/39370)**  
   *Closed.* A new plugin that generates design specs (wireframes, OKLCH color theory, design tokens) before writing code, complementing the existing `frontend-design` plugin.

2. **[📝 #65919 – docs(agent‑development): document `CLAUDE_PLUGIN_ROOT` limitation](https://github.com/anthropics/claude-code/pull/65919)**  
   *Open.* Adds a known‑limitations section to SKILL.md: subagents receive `CLAUDE_PLUGIN_ROOT` as a literal string instead of a resolved path (affects ≤ 2.1.166). Includes a resolution matrix.

3. **[📝 #65916 – docs(mcp‑integration): clarify `allowed-tools` vs agent tools enforcement](https://github.com/anthropics/claude-code/pull/65916)**  
   *Open.* Documents that `allowed-tools` in commands is an **auto‑approval** list, not a capability boundary; `tools:` in subagent frontmatter is a hard restriction.

4. **[🛠 #65666 – Fix dev container issues](https://github.com/anthropics/claude-code/pull/65666)**  
   *Closed.* Removes firewall‑blocked DNS domains and adds a mechanism to pass the API key from the local environment into the dev container.

5. **[🐛 #65875 – fix: Forward `ANTHROPIC_BASE_URL` to agentic_review child process](https://github.com/anthropics/claude-code/pull/65875)**  
   *Open.* The advisor feature spawns a child process that ignored `ANTHROPIC_BASE_URL`, breaking proxy/gateway setups (e.g., LiteLLM, Bifrost). This PR forwards the env variable.

## Feature Request Trends
- **Autonomous / multi‑agent architectures** (#56913, #65975) – Users want Claude Code to orchestrate long‑running pipelines using tiered models and persistent state.
- **MCP ecosystem expansions** – Requests for Gmail label management (#36547), pluggable memory backends (#48465), and custom authentication flows.
- **UI/UX improvements** – Language localization (#31413), customizable message colors (#65857), model/thinking‑mode indicators in VS Code (#28986).
- **IDE integration depth** – Better monorepo support for LSP find‑references (#45625), real‑time hook enforcement (#65953).
- **Cost transparency and control** – Suggestions for smarter context compaction and per‑task budgeting.

## Developer Pain Points
- **Extended‑thinking regressions** – Opus 4.7 and 4.8 both exhibit missing or empty thinking summaries. This is the most consistently reported issue across platforms.
- **Tool‑call corruption** – Multiple reports (#62123, #64684, #65965) of tool calls being malformed, especially after long‑form text or in long sessions. A “could not be parsed” error is a common dead‑end.
- **Performance bloat** – The Cowork VM bundle (#22543) and redundant context resubmission (#42647) cause significant slowdowns and unexpected token burn.
- **False‑positive usage policy blocks** – Benign queries (healthcare, field‑mapping) being flagged (#59540, #65973), frustrating legitimate usage.
- **Platform‑specific gaps** – Windows LSP tool path resolution (#59114), folder‑renaming bug (#58889), and Git Bash quirks remain unaddressed.
- **OAuth and proxy friction** – MCP OAuth trailing‑slash bug (#52871) and missing `ANTHROPIC_BASE_URL` forwarding for subprocesses (#65875) hinder enterprise and gateway deployments.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-07

## Today's Highlights
A wave of reports about chat histories disappearing after application updates continues to dominate community discussion, with many users confirming the underlying data remains on disk. On the development side, OpenAI engineers are actively refactoring the global instructions system and introducing a new extension API for cross-platform path handling and MCP capabilities. A long-standing request for CLI worktree/tmux flags (#12862) maintains high traction, while a critical bug preventing non-OpenAI model providers from calling MCP tools (#26234) draws attention from the local-model community.

## Releases
No new releases in the last 24 hours.

## Hot Issues
*(10 noteworthy issues, selected for community impact and discussion activity)*

- **#20741** [bug, app, session] – Chat histories disappeared after update, macOS.  
  *29 comments, 14 👍*  
  Users on macOS Tahoe report all local project conversations gone after updating to version 26.429.30905. Many commenters confirm the data still exists in `~/.codex` but the UI fails to load them.  
  [Link](https://github.com/openai/codex/issues/20741)

- **#13018** [enhancement, app, closed] – Allow deleting threads in Codex app.  
  *23 comments, 103 👍*  
  The most upvoted issue this week. Users demand a native delete option instead of only archiving threads. The issue was closed, suggesting a feature may be in the pipeline.  
  [Link](https://github.com/openai/codex/issues/13018)

- **#21128** [bug, app, session] – Desktop silently hides conversations outside the recent-50 window.  
  *20 comments, 16 👍*  
  Older project conversations become invisible from the UI when they fall off the global recent conversation list. Community considers this a critical workflow blocker for long-term projects.  
  [Link](https://github.com/openai/codex/issues/21128)

- **#12862** [enhancement, TUI] – Add `--worktree` and `--tmux` CLI flags.  
  *16 comments, 71 👍*  
  Highly requested feature to start an isolated git worktree session and attach to tmux in one command. Already scripted by many users manually.  
  [Link](https://github.com/openai/codex/issues/12862)

- **#23979** [bug, app, session] – History missing after update, threads still in `state_5.sqlite`.  
  *16 comments, 4 👍*  
  Another data-disappearance report after May 22 update. Users can manually recover sessions but the desktop app refuses to index them.  
  [Link](https://github.com/openai/codex/issues/23979)

- **#26234** [bug, mcp, CLI, custom-model] – MCP namespace tools flattened incorrectly for non-OpenAI providers (Ollama, LM Studio, OpenRouter).  
  *14 comments, 22 👍*  
  Tools exposed via MCP are never callable by models when using local or third-party endpoints. The proprietary `"type": "namespace"` serialization breaks compatibility.  
  [Link](https://github.com/openai/codex/issues/26234)

- **#23686** [bug, codex-web, rate-limits] – Personal Usage Chart not loading on Analytics page.  
  *11 comments, 15 👍*  
  The usage details bar chart shows an empty state despite available data. Affects Free & Pro users on the web interface.  
  [Link](https://github.com/openai/codex/issues/23686)

- **#21232** [bug, windows-os, app, imagen, performance] – App freezes when opening image-heavy projects.  
  *9 comments, 14 👍*  
  Windows users with many generated images experience full UI freezing. The issue appears related to image rendering in the sidebar.  
  [Link](https://github.com/openai/codex/issues/21232)

- **#25820** [bug, auth, rate-limits, CLI] – Codex CLI login blocked by phone verification rate limit (Pro subscriber).  
  *10 comments, 1 👍*  
  Pro subscribers are unable to authenticate Codex CLI due to aggressive phone verification rate limiting on the ChatGPT login flow.  
  [Link](https://github.com/openai/codex/issues/25820)

- **#26305** [bug, custom-model, context, app] – Chinese/CJK output duplicated in history leading to runaway token growth.  
  *7 comments, 0 👍*  
  With GPT-5.5 via Amazon Bedrock, streamed Chinese text is duplicated into the message history, causing prompt tokens to exceed the model limit. English equivalent succeeds.  
  [Link](https://github.com/openai/codex/issues/26305)

## Key PR Progress
*(10 significant open pull requests)*

- **#26840** – Add typed cross-platform path URIs.  
  Introduces stable path identifiers that work across local and remote environments without OS-specific interpretation.  
  [Link](https://github.com/openai/codex/pull/26840)

- **#26839** – Block project config permission overrides (security).  
  Addresses a security report (BUGB 15876) by adding approval policy and sandbox enforcement to prevent unauthorized config changes.  
  [Link](https://github.com/openai/codex/pull/26839)

- **#26754** – Prepare side threads off the TUI event loop.  
  Fixes a deadlock that occurs when the TUI prepares a side conversation while many events are emitted. Moves fork preparation off the main loop.  
  [Link](https://github.com/openai/codex/pull/26754)

- **#25704** – Normalize Codex images for Responses strict mode.  
  Feature-flagged change to convert local/data URL images into prepared data URIs before sending to `/responses` in strict mode.  
  [Link](https://github.com/openai/codex/pull/25704)

- **#26834** – Adopt global instructions contributors.  
  Core stops owning global instruction loading; hosts and the extension API now supply instructions via explicit contributors.  
  [Link](https://github.com/openai/codex/pull/26834)

- **#26833** – Persist structured instruction snapshots.  
  Ensures history-sharing threads retain the instructions active at creation time, preserving correctness across resume, forks, and compaction.  
  [Link](https://github.com/openai/codex/pull/26833)

- **#26832** – Add CODEX_HOME instructions contributor.  
  Moves CODEX_HOME instruction discovery out of `codex-core` into a dedicated crate, enabling future extension points.  
  [Link](https://github.com/openai/codex/pull/26832)

- **#26831** – Add global instructions contributor API.  
  Creates a formal extension point for hosts to supply global instructions, decoupling loading from core configuration.  
  [Link](https://github.com/openai/codex/pull/26831)

- **#26686** – feat(mcp): propagate client UI capabilities.  
  Adds semantic MCP app UI capabilities to the handshake; preserves profiles across thread start, resume, fork, and turn handling.  
  [Link](https://github.com/openai/codex/pull/26686)

- **#26719** – Enable standalone web search in code mode.  
  Exposes the standalone web search tool to code mode and returns plaintext output, with integration tests for both direct and code-mode paths.  
  [Link](https://github.com/openai/codex/pull/26719)

## Feature Request Trends
The community is consistently asking for improved **thread management** (native delete, better sidebar search, and option to show all local threads). **CLI productivity** enhancements such as isolated worktree/tmux sessions and quota summary status lines receive strong upvotes. There is also growing demand for **prompt snippets/panels** and **MCP interoperability** with local and third-party model providers. Additionally, users want **timezone-localized rate limit messages** and **better visibility into usage analytics**.

## Developer Pain Points
The most pressing and recurring frustration is **chat history disappearing after application updates**, with dozens of open issues reporting the same pattern: data persists on disk but the UI fails to index or display it. **Performance regressions** (high CPU from metadata processing, freezing on image-heavy projects, runaway disk writes) are a close second. **Custom model support** continues to be a pain point—especially MCP namespace incompatibility with non-OpenAI endpoints and CJK text duplication causing token exhaustion. **Authentication blockages** (phone verification ratelimit on CLI login) also disrupt Pro subscribers. Finally, **lack of thread deletion** and **sidebar search omissions** are persistent workflow complaints.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*