# AI CLI Tools Community Digest 2026-06-06

> Generated: 2026-06-06 02:47 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem

## Ecosystem Overview

The AI CLI developer tools landscape is characterized by rapid internal iteration alongside persistent community friction points. Both Anthropic and OpenAI are shipping multiple releases per week, but the majority of functional improvements come from internal teams rather than community contributions. The dominant themes across both ecosystems are multi-account management, agent-to-agent collaboration, and platform consistency—particularly the gap between desktop/IDE experiences and terminal CLI behavior. Developer trust is being eroded by token waste, authentication fragility, and session reliability issues, which remain the highest-priority unaddressed pain points. The underlying signal is clear: the user base has moved past initial experimentation into production dependency, and the tools' infrastructure is struggling to keep pace.

## Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|--------|------------|--------------|
| **Noteworthy Issues** | 10 (4 high-signal) | 10 (1 closed, 9 open) |
| **Active PRs (24h)** | 4 (2 meaningful) | 10 (all open, active) |
| **Releases (24h)** | 3 (v2.1.165–167) | 2 (rusty-v8, rust toolchain) |
| **Top Issue Engagement** | #27302: 195 comments, 261 👍 | #10450: 177 comments, 674 👍 |
| **PR Velocity** | Low; Anthropic internal dev dominates | Moderate; community PRs more active |
| **Bug vs. Feature Split** | 60% bugs, 40% features | 50% bugs, 50% features |

Claude Code shows higher release velocity from the vendor but lower community PR engagement, suggesting a more closed development model. OpenAI Codex has more community PR activity, though many are still pending review. Both tools have similar issue volumes, but Claude Code's issues skew toward higher engagement and stronger sentiment (more reactions per comment), indicating a more vocal power-user base.

## Shared Feature Directions

Both communities independently converged on **four common unmet needs**:

1. **Multi-account and credential management**: Both issues trackers have top-voted requests for switching between personal/work accounts without re-authentication. Claude Code's #27302 (261 👍) and Codex's implicit account-switching gaps reflect identical pain: users maintain multiple identities (GitHub, enterprise SSO, personal) and need seamless session-level switching.

2. **Agent-to-agent and cross-session collaboration**: Claude Code requests an inter-machine Agent-to-Agent protocol (#28300) and session communication (#65590). Codex users want subagent status visibility (#16900) and parallel subagent execution (#22099). Both are seeking multi-agent orchestration, but Claude Code is thinking about distributed agents across machines, while Codex focuses on hierarchical parent-child subagent management within a session.

3. **MCP/connector lifecycle improvements**: Both communities report MCP-related friction. Claude Code has namespace collisions between web connectors and local MCP tools (#65516). Codex users request project-scoped MCP pools (#20883) and report startup deadlocks being addressed in PR #26432. The underlying need is predictable, resource-efficient plugin lifecycle management.

4. **Platform consistency pain**: Both tools suffer from feature parity gaps between terminal, desktop, VS Code, and web. Claude Code's missing models in CLI picker (#63456) and SIGTERM timeout differences (#62202) mirror Codex's aggregation summaries in desktop view (#19891) and Windows-specific sandbox failures (#24391). Users expect identical behavior regardless of interface.

**Unique to Claude Code**: Settings sync across devices (#22648) and configurable fallback models (just shipped). **Unique to Codex**: Remote development support (just closed) and plugin marketplace infrastructure (active PR stack).

## Differentiation Analysis

**Feature focus**: Claude Code emphasizes reliability infrastructure (fallback models, glob pattern deny rules, Cowork collaboration) and targets advanced power users managing complex agent workflows. OpenAI Codex is investing in ecosystem expansion—plugin sharing, remote development, and permission profiles—suggesting a platform play rather than a tool play.

**Target users**: Claude Code's issue tracker suggests an audience of professional developers running multi-hour sessions with complex tool chains, managing costs, and hitting reliability ceilings. Codex's community skews toward developers working in heterogeneous environments (Windows + WSL2, macOS) who need sandbox isolation and subagent parallelism. Claude Code's users are deeper into production dependency; Codex's users are still fighting basic environment setup.

**Technical approach**: Claude Code uses a single-agent architecture with configurable fallback models and restrictive deny rules—prioritizing correctness and control. Codex uses a subagent-based architecture with guardian reviews and MCP process pools—prioritizing parallelism and extensibility. Claude Code's three-version burst today (v2.1.165–167) suggests rapid hotfix cycles; Codex's PR stack for plugin sharing indicates deliberate feature development.

**Platform maturity**: Claude Code is macOS-first with inconsistent desktop/VS Code behavior. Codex explicitly supports Windows/WSL2 but struggles with performance and sandbox reliability there. Neither tool has solved cross-platform consistency.

## Community Momentum & Maturity

**Claude Code**: The community is more engaged (195 comments on top issue) and more frustrated. The 7-month-old macOS Activity Monitor bug (#12433) and persistent image processing failures (#60334) suggest that core bug fixing is not keeping pace with feature shipping. The low community PR velocity indicates either a steep contribution barrier or lack of transparency. Anthropic is dominating development internally (3 releases/day), but community trust is fragile due to unresolved cost-related bugs.

**OpenAI Codex**: The community is larger on raw upvotes (674 on #10450) but less vocal per issue. The closure of the remote development request signals that OpenAI is listening to top requests. The active PR stack for plugin sharing (PRs #26703, #26704, #26701) and MCP lifecycle (#26432) shows a healthy development pipeline. However, Windows users represent a persistently underserved segment—sandbox failures and performance regressions are recurring themes.

**Maturity assessment**: Claude Code is more mature in agent reliability (fallback models, deny rules) but less mature in ecosystem development. Codex is more mature in community-contributed code and feature progression but less mature in core stability across platforms. Neither tool has achieved production-grade reliability across all common workflows.

## Trend Signals

1. **Multi-account and credential management is the #1 unmet need across both ecosystems.** Developers need to work across personal and organizational identities within a single session. This is a prerequisite for enterprise adoption.

2. **Agent-to-agent protocols are emerging organically.** Users are building their own solutions for inter-session and inter-machine collaboration. This will likely become a platform feature within 6–12 months, possibly standardizing on MCP extensions.

3. **Platform consistency is a competitive differentiator.** The tool that delivers identical behavior across terminal, desktop, VS Code, and web will win switching users from the competitor. Currently, neither has solved this.

4. **Cost governance is becoming critical.** Token waste bugs (Claude Code #60334) and idle quota drain (Codex #26600) represent real financial losses for paying users. Tools that provide transparent cost visibility and proactive warning systems will build user trust.

5. **Plugin/connector marketplaces are the next frontier.** Codex is actively building plugin catalog infrastructure. Claude Code has connectors but no marketplace. The trend points toward ecosystem lock-in via extensibility—the tool with the richest plugin ecosystem will dominate.

6. **Subagent parallelism is a performance bottleneck.** Both user bases are hitting concurrency limits. The tool that ships robust, observable subagent orchestration first will have a significant productivity advantage for large-scale codebase operations.

7. **Windows support remains the weakest link for both tools.** No AI CLI tool has credible Windows-first reliability. For enterprise adoption in mixed-OS environments, this is a blocking issue.

**Recommendation for developers evaluating these tools**: Choose Claude Code if you prioritize agent reliability, agent-to-agent workflows, and are willing to accept macOS-centric behavior. Choose Codex if you need plugin extensibility, remote development, and can tolerate Windows instability. Neither tool is production-ready across all platforms today; expect to invest in workarounds regardless of choice.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot: 2026-06-06 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

### #1: document-typography (#514)
*Author: PGTBoos | Status: Open | [View PR](https://github.com/anthropics/skills/pull/514)*

**Functionality:** Addresses three persistent typographic defects in AI-generated documents — orphan word wrap, stranded section headers (widow paragraphs), and numbering misalignment.

**Discussion highlights:** The skill tackles a universal pain point; contributors noted these issues affect "every document Claude generates." The PR has generated sustained discussion since March 2026, suggesting strong community resonance with document quality improvements.

---

### #2: ODT skill — OpenDocument text creation (#486)
*Author: GitHubNewbie0 | Status: Open | [View PR](https://github.com/anthropics/skills/pull/486)*

**Functionality:** Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods), targeting LibreOffice and ISO-standard document workflows.

**Discussion highlights:** This is the first dedicated ODF skill submission. Commenters highlighted the gap in open-source document format support within the official collection. The PR's extended timeline (March–April 2026) reflects the complexity of properly implementing the specification.

---

### #3: skill-quality-analyzer + skill-security-analyzer (#83)
*Author: eovidiu | Status: Open | [View PR](https://github.com/anthropics/skills/pull/83)*

**Functionality:** Meta-skills that evaluate other skills across five quality dimensions (Structure, Clarity, Correctness, Completeness, Portability) and security posture.

**Discussion highlights:** As the repository accumulated more community submissions, demand for quality assurance tooling grew. This PR was early (Nov 2025) but remains active, indicating ongoing refinement of evaluation criteria.

---

### #4: testing-patterns (#723)
*Author: 4444J99 | Status: Open | [View PR](https://github.com/anthropics/skills/pull/723)*

**Functionality:** Comprehensive testing guidance covering the Testing Trophy model, unit testing (AAA pattern), React Testing Library, integration, E2E, and accessibility testing.

**Discussion highlights:** The skill generated strong interest from developers seeking structured testing guidance within Claude sessions. Its breadth (full-stack coverage) was praised but also prompted requests for more framework-specific examples.

---

### #5: AURELION skill suite — kernel, advisor, agent, memory (#444)
*Author: Chase-Key | Status: Open | [View PR](https://github.com/anthropics/skills/pull/444)*

**Functionality:** A four-skill cognitive framework: structured thinking templates (5-floor hierarchy), professional knowledge management, autonomous agent patterns, and persistent memory.

**Discussion highlights:** The largest single skill suite submission generated debate about scope and maintainability. Commenters noted the "5-floor cognitive framework" could conflict with other organizational skills. The PR has been active since February 2026 with ongoing reviews.

---

### #6: feature-dev workflow fix (#363)
*Author: Mr-Neutr0n | Status: Open | [View PR](https://github.com/anthropics/skills/pull/363)*

**Functionality:** Fixes a TodoWrite overwrite bug that skips Quality Review (Phase 6) and Summary (Phase 7) during the `/feature-dev` workflow.

**Discussion highlights:** This bugfix represents a critical workflow reliability issue. The PR received sustained attention (Feb–June 2026) because TodoWrite behavior affects *all* multi-phase skills, not just feature-dev.

---

### #7: ServiceNow platform skill (#568)
*Author: Vanka07 | Status: Open | [View PR](https://github.com/anthropics/skills/pull/568)*

**Functionality:** Broad ServiceNow assistant covering ITSM, ITOM, ITAM/SAM, FSM, HRSD, CSM, SPM/PPM, Vulnerability Response, and IntegrationHub.

**Discussion highlights:** Enterprise demand for ServiceNow support is evident. The breadth of coverage was both praised and questioned — some reviewers preferred narrower, focused skills. The PR has been in active discussion since March 2026.

---

### #8: n8n-builder + n8n-debugger (#190)
*Author: Wolfe-Jam | Status: Open | [View PR](https://github.com/anthropics/skills/pull/190)*

**Functionality:** Two skills for n8n workflow automation: building workflows from scratch and debugging existing ones, plus a faf-expert skill for Foundational AI-context Format files.

**Discussion highlights:** This PR bundles multiple skills, reflecting community interest in workflow automation. The faf-expert component also signals growing demand for persistent project context frameworks.

---

## 2. Community Demand Trends

### 🏢 Org-wide skill sharing (#228)
*Status: Open, 13 comments | [View Issue](https://github.com/anthropics/skills/issues/228)*

The highest-commented issue demands enterprise-grade skill distribution. Users want native organization-level sharing — currently forced to use Slack/Teams for `.skill` file transfers. **This is the #1 feature request** by community engagement.

### 🔒 Security & trust boundaries (#492)
*Status: Open, 7 comments | [View Issue](https://github.com/anthropics/skills/issues/492)*

Community-raised security concern: "community skills distributed under the `anthropic/` namespace create a trust boundary vulnerability." Users are demanding clearer namespace separation between official and community submissions.

### ⚙️ Skill-creator tooling reform (#202)
*Status: Closed, 8 comments | [View Issue](https://github.com/anthropics/skills/issues/202)*

Closed but influential: the skill-creator skill was criticized as "developer documentation, not an operational skill." This drove multiple PRs (#539, #1050, #1099) to improve validation, Windows compatibility, and YAML parsing.

### 📋 Platform compatibility (Windows, Bedrock)
*#29 (Bedrock), #1050/#1099 (Windows)*

Multiple issues highlight cross-platform friction. Skill development tooling (`run_eval.py`, `run_loop.py`) fails on Windows due to subprocess and encoding bugs — a barrier to broader community contribution.

### 📦 Multi-file bundling (#1220)
*Status: Open, 2 comments | [View Issue](https://github.com/anthropics/skills/issues/1220)*

Emerging demand: skills split across multiple reference files need inline bundling so all context is delivered on invocation, not just `SKILL.md`.

---

## 3. High-Potential Pending Skills

These open PRs have active discussion and are likely to land soon:

| PR | Skill | Expected Impact |
|----|-------|-----------------|
| [#538](https://github.com/anthropics/skills/pull/538) | PDF case-sensitive fix | Unblocks PDF skill on case-sensitive filesystems (Linux/macOS) |
| [#539](https://github.com/anthropics/skills/pull/539) | YAML validation in skill-creator | Prevents silent parsing failures; foundational tooling improvement |
| [#541](https://github.com/anthropics/skills/pull/541) | DOCX tracked-change ID collision | Fixes document corruption; high-impact for DOCX reliability |
| [#1099](https://github.com/anthropics/skills/pull/1099) | Windows run_eval.py crash | Unblocks Windows contributors; eliminates `precision=100% recall=0%` false reports |
| [#1050](https://github.com/anthropics/skills/pull/1050) | Windows subprocess/encoding | Companion fix to #1099; enables `run_loop.py` on Windows 11 |
| [#1140](https://github.com/anthropics/skills/pull/1140) | agent-creator meta-skill | Task-specific agent sets; multi-tool evaluation fix; Windows path support |
| [#363](https://github.com/anthropics/skills/pull/363) | feature-dev workflow phases | Critical bugfix affecting all multi-phase skills; long review cycle suggests imminent merge |
| [#181](https://github.com/anthropics/skills/pull/181) | SAP-RPT-1-OSS predictor | Enterprise analytics use case; SAP foundation model integration |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is split between document generation skills (typography, ODT, DOCX) and foundational skill-creator tooling improvements (validation, cross-platform compatibility, evaluation reliability), with enterprise sharing infrastructure emerging as the top feature request for the ecosystem's next maturity phase.**

---

# Claude Code Community Digest — 2026-06-06

## Today's Highlights

Anthropic shipped **v2.1.166** with a major reliability improvement: configurable fallback models (up to three) that activate when the primary model is overloaded, plus expanded glob pattern support in deny rules. Meanwhile, community attention remains fixed on the **multiple Connector accounts request** (#27302) and a critical **image processing bug** (#60334) that has burned significant conversation tokens for many users. Several OAuth credential corruption issues are also drawing developer scrutiny.

---

## Releases

Three minor versions landed in the last 24 hours:

- **v2.1.166** — Feature release. Introduces `fallbackModel` setting, allowing users to configure up to three fallback models tried in sequence when the primary model is overloaded or unavailable. The `--fallback-model` CLI flag now also applies in interactive sessions. Additionally, glob patterns (`"*"`) are now supported in the deny rule tool-name position.
- **v2.1.165** — Bug fixes and reliability improvements.
- **v2.1.167** — Bug fixes and reliability improvements (immediately follows v2.1.166).

The fallback model feature is the standout change — addressing a long-standing pain point where model unavailability would hard-stop sessions. No breaking changes or new deprecations in this batch.

---

## Hot Issues (10 Noteworthy)

### 🔥 High Signal
1. **[#27302 — Support multiple Connector accounts](https://github.com/anthropics/claude-code/issues/27302)**  
   *Author: nathanmargaglio · 195 comments · 261 👍*  
   The most-requested feature in the entire issue tracker. Developers want to switch between multiple Connector accounts (e.g., personal vs. work GitHub) without logging out. No official response yet; community workarounds are growing in the comments.

2. **[#60334 — Image processing failures causing token waste](https://github.com/anthropics/claude-code/issues/60334)**  
   *Author: cristian-milea · 54 comments · 14 👍*  
   A persistent bug where API errors silently remove images from conversations, burning ~70% of the 5-hour usage window. Users report receiving "image removed" errors despite never attaching images. Likely relates to upstream image re-processing during context compaction.

3. **[#63875 — Tool call parsing failures interrupting sessions](https://github.com/anthropics/claude-code/issues/63875)**  
   *Author: shenxiu · 42 comments · 62 👍*  
   "The model's tool call could not be parsed (retry also failed)" — this error kills in-progress actions mid-task, forcing session restarts. High reproducibility across platforms. Community suspects it correlates with long context windows and complex tool chains.

4. **[#28300 — Multi-agent collaboration across machines](https://github.com/anthropics/claude-code/issues/28300)**  
   *Author: MarioK1975 · 23 comments · 0 👍*  
   Requests an Agent-to-Agent protocol enabling Claude Code instances on different machines to collaborate. While low on reactions, the discussion is detailed — covering MCP extensions, WebRTC, and shared file-system approaches.

5. **[#22648 — Account-level settings sync across devices](https://github.com/anthropics/claude-code/issues/22648)**  
   *Author: wesleyfolly · 23 comments · 37 👍*  
   Settings stored in `~/.claude/` are not synced across machines. Users with Linux + macOS workflows must manually duplicate configurations. Multiple dupe issues exist (#6037, #19634, #13461, #12119).

### ⚠️ Noteworthy Bugs
6. **[#12433 — Activity Monitor shows version number, not 'claude'](https://github.com/anthropics/claude-code/issues/12433)**  
   *Author: shaanmajid · 19 comments · 22 👍*  
   Cosmetic but persistent macOS bug since November 2025. Process appears as `2.0.53` instead of `claude` in Activity Monitor, making it difficult to find and kill processes. Still unfixed after 7 months.

7. **[#63456 — Opus 4.8 not selectable in CLI `/model`](https://github.com/anthropics/claude-code/issues/63456)**  
   *Author: uplinkdgroup · 17 comments · 11 👍*  
   `Opus 4.8` is available on the web interface but missing from the CLI model picker. Users with the model on their account cannot access it via `/model`. Likely a version-detection or capability-reporting bug on the client side.

8. **[#62202 — Process exits with SIGTERM every 5 minutes in Desktop/VS Code](https://github.com/anthropics/claude-code/issues/62202)**  
   *Author: SharedAccKaT · 2 comments · 1 👍*  
   Claude Code child process is killed with SIGTERM exactly every 300 seconds in the Desktop app and VS Code extension, but not in the terminal CLI. Points to a wrapper timeout mechanism that doesn't account for extended thinking or tool execution.

9. **[#65756 — Cowork blocked by "Usage credits required for 1M context"](https://github.com/anthropics/claude-code/issues/65756)**  
   *Author: Tombombadil81 · 3 comments · 0 👍*  
   A false positive: users with enabled usage credits are blocked from using Cowork, with the error triggering at just 7% session usage during context compaction. The `/model` workaround does not help.

10. **[#65516 — MCP tools not surfacing when web connectors are present](https://github.com/anthropics/claude-code/issues/65516)**  
    *Author: MarkSlosberg · 3 comments · 0 👍*  
    MCP servers registered via `claude mcp add` fail to surface their tools when the same connector type is also configured through the claude.ai web interface. Likely a namespace collision in the tool provider registry.

---

## Key PR Progress (4 Updated in Last 24h)

Only four PRs were active today — the repository appears to be in a low-velocity period for community contributions:

1. **[#65619 — fix(plugins): align frontend-design author with marketplace entry](https://github.com/anthropics/claude-code/pull/65619)**  
   *Author: systemblueio · 0 comments*  
   Fixes a `plugin.json` metadata issue where two authors were packed into a single-string `author.name` field, causing malformed rendering in plugin UIs. Clean, focused patch — likely to merge quickly.

2. **[#65666 — Fix dev container issues](https://github.com/anthropics/claude-code/pull/65666)**  
   *Author: sgt101 · 0 comments*  
   Resolves DNS resolution failures in the devcontainer by removing problematic domain references, plus adds an env-var mechanism for injecting API keys. Practical quality-of-life fix for contributors.

3. **[#65723 — Claude/subscription debate chat rx ewi](https://github.com/anthropics/claude-code/pull/65723)**  
   *Author: nowordsformylove · 0 comments · Title unclear*  
   Description is empty or minimal — likely a test or draft PR. No community traction.

4. **[#58673 — s](https://github.com/anthropics/claude-code/pull/58673)**  
   *Author: sjbrenchley89 · 0 comments*  
   Single-character PR title and no description. Appears to be a non-functional submission. Open since May 13.

**Note:** Community PR volume is very low today. Most active development appears to be internal Anthropic releases (three new versions in 24h).

---

## Feature Request Trends

**1. Multi-account and multi-connector support**  
The dominant request across the tracker. Users want to: switch between multiple connector accounts (#27302, 195 comments), sync settings across devices (#22648), and manage multiple service accounts within a single Claude Code installation. This is clearly the #1 unmet need for power users.

**2. Agent-to-agent and cross-session collaboration**  
Users increasingly want Claude Code instances to communicate — across machines (#28300), between sessions in different project directories (#65456), and within structured "session teams" where sessions can talk to each other interactively (#65590). This reflects growing adoption of multi-agent workflows.

**3. Model flexibility improvements**  
Requests include: switching models mid-session for existing Cowork tasks (#49649), making certain large-context models consistently available (#63456), and configuring per-task model selection. The new `fallbackModel` feature partially addresses this, but users want more granular control.

**4. IDE and UI polish**  
Specific requests include: collapsing unchanged lines in the desktop diff viewer (#65311), preventing session title truncation in VSCode's Ctrl+Tab switcher (#65776), and adding a branch selector to the iOS code UI (#55500).

---

## Developer Pain Points

**1. Token waste and cost leakage**  
The most expensive bugs currently active: image processing failures burn usage window time (#60334, 54 comments), and false "usage credits required" errors block Cowork sessions (#65756). Both cause direct financial loss for paying users.

**2. Authentication fragility**  
Multiple reports of credential state corruption: OAuth refresh mishandling transient 5xx responses leads to persistent 401 loops (#61912), stale refresh tokens require manual credential file deletion (#65761), and `claude auth status` reports logged in while actual requests fail (#65725). Authentication is the second-most painful area after cost.

**3. Session interruptions**  
Mid-task failures due to unparseable tool calls (#63875), SIGTERM timeouts in non-CLI environments (#62202), and assistant text blocks silently dropped from transcripts (#65620) erode trust in session reliability. Each forces a full restart.

**4. Model availability gaps**  
Models available via claude.ai web are not always accessible in the CLI (#63456), and the `/model` picker lags behind web capabilities. Combined with the recent `fallbackModel` release, this suggests a server-side discoverability problem rather than a UI one.

**5. Inconsistent platform behavior**  
The same feature works differently across terminal CLI, VS Code extension, Desktop app, and web — leading to confusion and platform-specific workarounds. The SIGTERM 5-minute timeout (#62202) and missing model picker options (#63456) are prime examples.

---

*Next digest: 2026-06-13. Data source: [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-06

## Today’s Highlights
The community’s most requested feature – remote development for the Codex Desktop App – has been closed, likely signalling imminent or shipped support. Meanwhile, Windows and WSL2 users continue to struggle with sandbox setup failures and severe performance regressions, gathering dozens of comments and workarounds. Internally, the team is advancing plugin sharing, MCP lifecycle management, and a new standalone web search capability in code mode.

## Releases
- [`rusty-v8-v149.2.0`](https://github.com/openai/codex/releases/tag/rusty-v8-v149.2.0) – Updated V8 binding dependency.
- [`rust-v0.138.0-alpha.5`](https://github.com/openai/codex/releases/tag/rust-v0.138.0-alpha.5) – Pre‑release of the Rust toolchain used by Codex CLI (no further details provided).

## Hot Issues (10 Noteworthy)

1. **[#10450 – Remote Development in Codex Desktop App](https://github.com/openai/codex/issues/10450)** (CLOSED, 177 comments, 674 👍)  
   *The top‑voted feature request ever. Its closure suggests official remote/project‑based development support is on the way.*

2. **[#18258 – ‘Computer Use plugin unavailable’ on macOS](https://github.com/openai/codex/issues/18258)** (OPEN, 39 comments, 41 👍)  
   *Persistent plugin loading error with a community‑driven workaround (enable `features.apps` and repair cache). Affects many macOS users.*

3. **[#25715 – Codex App unusably slow with WSL as agent environment](https://github.com/openai/codex/issues/25715)** (OPEN, 31 comments, 29 👍)  
   *Routine turns take minutes. Windows‑on‑WSL performance is a major pain point for developers relying on Linux toolchains.*

4. **[#24391 – Windows sandbox spawn setup refresh fails on CLI 0.133.0](https://github.com/openai/codex/issues/24391)** (OPEN, 28 comments, 22 👍)  
   *After updating to 0.133.0, shell commands fail with sandbox initialization errors. Affects npm‑global installs on Windows.*

5. **[#11527 – Agent loop fails to start after task recognition](https://github.com/openai/codex/issues/11527)** (CLOSED, 22 comments)  
   *Agent gets stuck waiting for input instead of running autonomously. Closed, but serves as a historical symptom of early agent loop issues.*

6. **[#2920 – Change model/thinking through a keyboard shortcut](https://github.com/openai/codex/issues/2920)** (CLOSED, 12 comments, 41 👍)  
   *A long‑standing UX enhancement that would avoid retyping `/model`. Likely implemented or planned given its closure.*

7. **[#20883 – Project‑scoped MCP process pool instead of per‑session](https://github.com/openai/codex/issues/20883)** (OPEN, 10 comments)  
   *MCP servers spawn per chat, wasting resources. Users request a shared pool per workspace.*

8. **[#16900 – Subagent status and parent‑child wait mechanism](https://github.com/openai/codex/issues/16900)** (OPEN, 10 comments, 4 👍)  
   *Parent threads prematurely retry tasks that child subagents are still handling. No visibility into subagent health.*

9. **[#22099 – Parallel‑first subagents and non‑blocking background tasks](https://github.com/openai/codex/issues/22099)** (OPEN, 10 comments)  
   *A community fork (“Open Codex CLI”) explores proactive parallelism. Users want better concurrent subagent execution and lifecycle management.*

10. **[#19891 – ‘For coding’ view hides edited file names and commands behind summaries](https://github.com/openai/codex/issues/19891)** (OPEN, 7 comments, 7 👍)  
    *A recent app regression that collapses detailed changes into aggregate summaries, reducing transparency for coding tasks.*

## Key PR Progress (10 Important)

1. **[#26719 – Enable standalone web search in code mode](https://github.com/openai/codex/pull/26719)** (OPEN)  
   *Brings `/v1/alpha/search` to code‑mode workflows, allowing agents to fetch live web data without leaving the coding context.*

2. **[#26715 – Load direnv environment into shell snapshots](https://github.com/openai/codex/pull/26715)** (OPEN)  
   *Fixes environment capture for users relying on `direnv` – a critical enabler for project‑specific environment variables.*

3. **[#26432 – Release MCP manager lock before listing tools](https://github.com/openai/codex/pull/26432)** (OPEN)  
   *Resolves a startup deadlock where MCP tool listing blocked session shutdown. Improves multi‑session stability.*

4. **[#26713 – Report unusable MCP OAuth credentials as logged out](https://github.com/openai/codex/pull/26713)** (OPEN)  
   *Prevents false “OAuth authenticated” status when tokens are expired without a refresh capability. Reduces confusion for MCP servers.*

5. **[#26717 – Stop guardian reviews when parent turns are interrupted](https://github.com/openai/codex/pull/26717)** (OPEN)  
   *Prevents guardian approval reviews from running indefinitely after the parent turn is cancelled. Better error propagation in the UI.*

6. **[#26687 – Pair thread environment settings](https://github.com/openai/codex/pull/26687)** (OPEN)  
   *Ensures thread CWD and environment are updated atomically, avoiding silent desynchronisation of execution context.*

7. **[#26703 – TUI Plugin sharing – render remote plugin catalog sections](https://github.com/openai/codex/pull/26703)** (OPEN)  
   *Builds the UI for browsing remote plugin catalogs alongside local ones – a step toward a plugin marketplace.*

8. **[#26704 – TUI Plugin sharing – cover remote plugin catalog flows](https://github.com/openai/codex/pull/26704)** (OPEN)  
   *Adds focused tests for install, uninstall, deduplication, and share management of remote plugins.*

9. **[#26701 – TUI Plugin sharing – add remote plugin identity](https://github.com/openai/codex/pull/26701)** (OPEN)  
   *Foundational plumbing to distinguish local vs. remote plugins in the TUI popup flows.*

10. **[#26678 – Permission profiles: expose availability to clients](https://github.com/openai/codex/pull/26678)** (OPEN)  
    *Improves enterprise permission visibility by filtering profiles that are effectively unavailable due to policy requirements.*

## Feature Request Trends
- **Remote / Project‑Based Development** (#10450) – The most popular request, now apparently addressed.
- **MCP Lifecycle Improvements** – Users want project‑scoped MCP server pools (#20883), better startup diagnostics (#24439), and reduced memory usage (#11324, #21984).
- **Subagent Parallelism & Observability** – Demand for parallel‑first subagents (#22099), status checking (#16900), and orphaned process cleanup (#19197).
- **Plugin / Catalog Sharing** – Multiple PRs in the TUI plugin stack indicate active work on a remote plugin marketplace and sharing capabilities.
- **Config Profiles via CLI** (#4849) – Developers want to select custom model/provider profiles from the command line without editing config files.

## Developer Pain Points
- **Windows Sandbox & WSL2 Instability** – Repeated spawn setup failures (#24391), infinite configure loops (#23137), and severe app slowness when using WSL (#25715, #20967, #25799). Windows support remains a reliability gap.
- **App Performance Regressions** – Micro‑freezes after prompts (#26401), freezes when pasting text (#26697), and aggregation summaries hiding file changes (#19891) frustrate daily usage.
- **Subagent Orphans & Stuck Tasks** – Permissions requests causing infinite `/goal` loops that burn usage quotas (#22833), orphaned subagents that freeze sessions (#19197), and premature parent‑child retries (#16900).
- **Reconnection & Background Quota Drain** – Repeated reconnect loops (#26274) and quota decreasing during idle time (#26600) point to underlying session management issues.
- **MCP Startup/Teardown Delays** – Headed browser MCP processes accumulate (#21984), memory grows with multi‑tasking (#11324), and diagnostic commands are missing (#24439).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*