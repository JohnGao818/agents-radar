# AI CLI Tools Community Digest 2026-06-16

> Generated: 2026-06-16 03:40 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Ecosystem Comparison Report: Claude Code vs. OpenAI Codex

**Date:** 2026-06-16  
**Prepared for:** Technical decision-makers and AI developer tooling engineers

---

## 1. Ecosystem Overview

The AI CLI tooling landscape is maturing rapidly, with both Claude Code and OpenAI Codex shipping production-quality releases while wrestling with the same fundamental challenge: scaling multi-agent workflows without sacrificing reliability. Both communities are vocal about persistent memory, cross-platform stability, and safety-tunability—indicating that the market has moved beyond novelty and now demands enterprise-grade session management and resource governance. The convergence on extensibility hooks and subagent control patterns suggests an emerging consensus architecture for agentic coding assistants, while platform-specific friction (Windows, Linux) remains a key competitive battleground. Notably, the volume of duplicate bug reports and the presence of community-built workarounds for missing features signal that both ecosystems have reached critical mass.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Latest stable release** | v2.1.178 (today) | v0.140.0 (today) |
| **Release cadence** | Frequent point releases + patches | Structured major/minor + alpha cycles |
| **Notable issues** | 10 highlighted; 53 max comments, 163 👍 | 10 of 50+ highlighted; 113 max comments, 583 👍 |
| **Notable PRs** | 10 key; 6 open, 4 closed | 10 of 50+ key; mix of open/merged |
| **Community engagement per issue** | Higher ratio of duplicates (ENOSPC: 5+ dupes) | Higher absolute upvotes (Linux desktop: 583) |
| **Feature request volume** | Persistent memory, VS Code control, session lifecycle | Linux desktop, session stability, safety whitelisting |

**Key observation:** Claude Code generates more discussion per bug (higher duplicate density), while OpenAI Codex commands higher absolute vote counts on a smaller number of high-profile feature requests.

---

## 3. Shared Feature Directions

The following requirements appear independently across both tool communities:

| Shared Need | Claude Code References | OpenAI Codex References | Notes |
|---|---|---|---|
| **Persistent memory / session state** | #47023 (hooks), #38536 (team memory), community-built 3-tier markdown solutions | #3355 (sleep reconnection), #28263 (resume visibility) | Both communities building workarounds; official hooks would unify |
| **Agent/subagent reliability** | #68727 (Sonnet 1M context), #50267 (path permissions), #68735 (early termination) | #27331 (multi_agent_v2 400 error) | Multi-agent workflows are the primary pain point in both tools |
| **Cross-platform file path handling** | #68700, #68694 (Windows backslash normalization) | #28094 (WSL → C:\home), #12661 (Edge vs VS Code) | Windows second-class citizenship persists |
| **Resource governance** | #64366 (MCP fan-out crash), #29045 (1.8GB VM) | #25719 (syspolicyd CPU runaway) | Both have runaway resource consumption patterns |
| **Selective tool permissioning** | v2.1.178 `Tool(param:value)` syntax | #27965 (`default_tools_approval_mode`) | Both shipping granular approval controls this cycle |
| **Extensibility hooks** | #47023 (session lifecycle), #51537 (10K char output limit) | #28396 (external agent import), #28429 (interruptible sleep) | Plugin/hook ecosystems maturing in both tools |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary release model** | Desktop + CLI; heavier on TUI with VS Code extension | CLI-first with VS Code extension; Linux desktop app is top request |
| **Permissioning philosophy** | Rule-based (`Tool(param:value)`, hook-based deny) | Config-based (`default_tools_approval_mode`, per-app override) |
| **Agent model strategy** | Subagent blocking by model type (e.g., block Opus) | Multi-agent feature is experimental and currently broken |
| **Extensibility depth** | Hooks system (pre/post tool, event:all fallback), skills directory loading | Plugin recommendation cache, credential brokering, endpoint-level plugins |
| **Safety approach** | MCP-based isolation; community reporting false positives | Cybersecurity classifier with false-positive backlash (#27817, #28015) |
| **Platform prioritization** | macOS-first; Windows improvements in current PR batch | macOS-first; Windows friction flagged, Linux ignored |
| **Data management** | Session history lost on desktop update (#48334) | Session deletion added in v0.140.0; /goal sessions hidden (#28263) |
| **Maturity indicator** | Bug duplication and regression density suggest established but brittle | Single mega-request (Linux, 583👍) suggests unmet fundamental need |

**Strategic takeaway:** Claude Code is investing in *permission granularity and extensibility* for power users already in the ecosystem. OpenAI Codex is investing in *observability (token dashboards) and platform expansion* to grow the user base.

---

## 5. Community Momentum & Maturity

**Claude Code** has a higher-engagement, more technically sophisticated community. The presence of multiple community-built workarounds (3-tier markdown memory, knowledge-graph solutions) before official hooks exist indicates a developer audience willing to build on top of the tool. The high duplicate bug count (ENOSPC: 5+ issues) suggests either triage bottlenecks or a particularly frustrating bug that resists fix. The v2.1.31+ release cadence shows rapid iteration, but the data-loss regression (#48334) erodes trust in auto-update reliability.

**OpenAI Codex** commands higher raw community enthusiasm (583 upvotes for Linux desktop vs. Claude's 163 for VS Code settings). The v0.14x numbering indicates the tool is younger in its public lifecycle. The structured alpha/beta release pipeline (v0.141.0-alpha.2) and active PR flow (50+ today) suggest a faster development velocity, but the broken `multi_agent_v2` feature (#27331) and recurring false-positive safety blocks indicate that feature breadth is prioritized over stability.

**Maturity assessment:**
- Claude Code: Higher per-user maturity, deeper ecosystem, battle-tested but accumulating stability debt
- OpenAI Codex: Faster feature iteration, higher top-of-funnel demand, less polished but growing quickly

---

## 6. Trend Signals

1. **Multi-agent is the next frontier—and it's still brittle.** Both tools ship multi-agent features that break in common scenarios. Expect significant investment in subagent lifecycle management, resource limits, and error recovery in the next 3–6 months.

2. **Persistent memory is the #1 unsolved UX gap.** Memory hooks, team-level knowledge bases, and session resumption are the most-requested missing features across both ecosystems. Community-built solutions indicate strong latent demand.

3. **Safety-tunability is becoming a competitive differentiator.** Claude Code's `Tool(param:value)` and OpenAI Codex's false-positive backlash both point to the same insight: developers need *configurable* safety—not just on/off, but context-aware whitelisting and model-level blocking.

4. **Desktop apps are causing disproportionate pain.** Resource bloat (1.8GB VM, CPU runaway), platform-specific crashes, and data-loss during updates suggest that both tools are pushing desktop architectures that outpace their resource management maturity. The industry may see a pivot to lighter-weight runtimes.

5. **Windows support remains an aftermarket problem.** Both tools ship macOS-first; Windows users bear the cost of path manipulation, elevation bugs, and missing features. A tool that cracks Windows-first UX could capture a large underserved segment.

6. **Extensibility is becoming standard, not special.** Both communities expect hooks, plugins, and credential brokering as baseline features. The differentiation will shift from "does it have plugins?" to "how composable and debuggable are the plugins?"

---

*Data sources: Claude Code community digest 2026-06-16 (v2.1.178), OpenAI Codex community digest 2026-06-16 (v0.140.0). Both tools' GitHub repositories referenced for issue and PR data.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot:** github.com/anthropics/skills | **Date:** 2026-06-16

---

## 1. Top Skills Ranking

The following pull requests have drawn the most community attention, based on comment volume and sustained discussion activity.

### 1. Document Typography ([PR #514](https://github.com/anthropics/skills/pull/514))
**Functionality:** Prevents orphan word wrap (1–6 words stranded on a new line), widow paragraphs (section headers at page bottom), and numbering misalignment in AI-generated documents — issues that affect virtually every document Claude produces.
**Discussion highlights:** Reviewers noted the skill addresses a pervasive quality gap. The core question was whether typographic rules should be enforced as a skill or built into Claude's base document generation.
**Status:** Open, updated March 2026.

### 2. ODT Skill ([PR #486](https://github.com/anthropics/skills/pull/486))
**Functionality:** Enables creation, template-filling, reading, and conversion of OpenDocument Format files (.odt, .ods). Triggers on keywords like "ODT", "ODS", "LibreOffice", and "OpenDocument."
**Discussion highlights:** Heavy interest from LibreOffice/enterprise users. The main discussion thread centers on whether ODT support should remain a community skill or be upstreamed into Claude's core capabilities.
**Status:** Open, updated April 2026.

### 3. Frontend-Design Skill Clarity ([PR #210](https://github.com/anthropics/skills/pull/210))
**Functionality:** Comprehensive revision of the existing `frontend-design` skill to ensure every instruction is actionable within a single conversation and specific enough to steer Claude's behavior without requiring human interpretation.
**Discussion highlights:** The PR sparked a meta-discussion about skill writing standards — balancing brevity with precision, and whether skills should teach patterns or enforce rules.
**Status:** Open, updated March 2026.

### 4. Skill Quality & Security Analyzers ([PR #83](https://github.com/anthropics/skills/pull/83))
**Functionality:** Two meta-skills: `skill-quality-analyzer` (evaluates skills across structure, documentation, examples, and resources) and `skill-security-analyzer` (security posture review for skill definitions).
**Discussion highlights:** Community feedback praised the meta-skill approach but requested clearer scoring criteria and integration with CI pipelines. Security analysis was deemed especially valuable for enterprise adoption.
**Status:** Open, updated January 2026.

### 5. SAP-RPT-1-OSS Predictor ([PR #181](https://github.com/anthropics/skills/pull/181))
**Functionality:** Integrates SAP's open-source tabular foundation model for predictive analytics on SAP business data, released at SAP TechEd 2025.
**Discussion highlights:** Generated strong interest from SAP ecosystem users. Questions focused on model size/performance tradeoffs and whether the skill should include data pre-processing pipelines.
**Status:** Open, updated March 2026.

### 6. Agent-Creator Meta-Skill ([PR #1140](https://github.com/anthropics/skills/pull/1140))
**Functionality:** A meta-skill for generating task-specific agent sets. Also includes fixes for multi-tool evaluation correctness and Windows `%APPDATA%` path support.
**Discussion highlights:** Addresses a frequently requested capability — programmatic skill composition. The multi-tool evaluation fix resolved a long-standing bug affecting skill testing.
**Status:** Open, updated June 2026.

### 7. Testing Patterns Skill ([PR #723](https://github.com/anthropics/skills/pull/723))
**Functionality:** Comprehensive skill covering testing philosophy (Testing Trophy model), unit testing (AAA pattern, edge cases), React component testing, integration testing, E2E, and visual regression.
**Discussion highlights:** Reviewers debated whether the Testing Trophy model should be configurable vs. hardcoded. Strong demand from frontend-heavy teams.
**Status:** Open, updated April 2026.

### 8. AURELION Skill Suite ([PR #444](https://github.com/anthropics/skills/pull/444))
**Functionality:** Four skills from the AURELION ecosystem: `aurelion-kernel` (5-floor cognitive framework for structured thinking), plus advisor, agent, and memory skills for professional knowledge management.
**Discussion highlights:** The cognitive framework approach was polarizing — some praised its depth, others felt it added too much overhead for simple interactions. The memory skill was the most universally welcomed component.
**Status:** Open, updated May 2026.

---

## 2. Community Demand Trends

The most active Issues reveal five clear demand clusters:

- **Org-wide skill sharing & management** — [Issue #228](https://github.com/anthropics/skills/issues/228) (14 comments, 7 👍) calls for native skill sharing within organizations, eliminating the current download/upload workflow. This is the single most-upvoted feature request.
- **Skill evaluation reliability** — [Issue #556](https://github.com/anthropics/skills/issues/556) (12 comments, 7 👍) and [Issue #1169](https://github.com/anthropics/skills/issues/1169) report that `run_eval.py` consistently produces 0% trigger rates, making the description-optimization loop optimize against noise. The community is frustrated by broken tooling that undermines skill iteration.
- **Document & format expansion** — Strong, sustained demand for broader document format support (ODT, advanced typography, multi-file skill preloading via [Issue #1220](https://github.com/anthropics/skills/issues/1220)).
- **Security & governance** — [Issue #492](https://github.com/anthropics/skills/issues/492) (7 comments) raises trust boundary concerns about community skills under the `anthropic/` namespace. [Issue #1175](https://github.com/anthropics/skills/issues/1175) asks about access control patterns for SharePoint Online integrations. The community wants security patterns explicitly encoded as skills.
- **Windows compatibility** — [Issue #1061](https://github.com/anthropics/skills/issues/1061) and multiple PRs (PR #1099, PR #1050) highlight that skill-creator scripts are largely unusable on native Windows Python due to subprocess, encoding, and pipe selection issues. This is an infrastructure blocker, not a feature gap.

A secondary theme is **meta-skill authoring tools**: [Issue #202](https://github.com/anthropics/skills/issues/202) critiques the skill-creator itself for reading like documentation rather than a functional skill, and [Issue #62](https://github.com/anthropics/skills/issues/62) reports skill disappearance problems — both pointing to a need for better skill lifecycle management.

---

## 3. High-Potential Pending Skills

These open PRs show sustained comment activity and address clear community needs — they are the most likely to merge soon:

| Skill | PR | Last Updated | Why It Matters |
|---|---|---|---|
| Document Typography | [#514](https://github.com/anthropics/skills/pull/514) | 2026-03-13 | Fixes a universal document quality problem; low complexity, high impact. |
| ODT Support | [#486](https://github.com/anthropics/skills/pull/486) | 2026-04-14 | Fills a major format gap for enterprise/LibreOffice users. |
| Agent-Creator | [#1140](https://github.com/anthropics/skills/pull/1140) | 2026-06-02 | Directly addresses meta-skill demand; includes critical bug fixes. |
| Testing Patterns | [#723](https://github.com/anthropics/skills/pull/723) | 2026-04-21 | Comprehensive coverage of the testing stack; strong developer interest. |
| AURELION Suite | [#444](https://github.com/anthropics/skills/pull/444) | 2026-05-06 | Persistent memory + structured thinking; novel capability. |
| CONTRIBUTING.md | [#509](https://github.com/anthropics/skills/pull/509) | 2026-03-19 | Removes a community health blocker (25% → improved GitHub metrics). |
| Script fixes (Windows) | [#1298](https://github.com/anthropics/skills/pull/1298) | 2026-06-11 | Fixes 0% recall bug across three scripts; highly requested. |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for tools that make skills themselves easier to create, evaluate, and share reliably** — meta-skills, evaluation infrastructure, and org-wide distribution channels are receiving more engagement than any single domain-specific skill.

---

# Claude Code Community Digest — 2026-06-16

## Today’s Highlights

A new release (v2.1.178) introduces `Tool(param:value)` syntax for permission rules, enabling precise blocking of subagents by model type. The community continues to push for persistent memory and shared team memory, while a spate of duplicate ENOSPC false-positives on macOS has become the most-discussed bug cluster. Several plugin-focused PRs landed, improving Windows compatibility and tooling reliability.

---

## Releases

**v2.1.178** (just published)

- **`Tool(param:value)` permission syntax** – Permission rules can now match a tool’s input parameters with `*` wildcards, e.g. `Agent(model:opus)` to block Opus subagents.
- **Nested skill loading** – Skills placed in `.claude/skills` subdirectories now load when working on files in that hierarchy; name clashes are resolved in favour of the nested skill.
- [Full release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.178)

---

## Hot Issues (10 Noteworthy)

### 1. VS Code: Setting to disable auto-attach of open file/selection  
[#24726](https://github.com/anthropics/claude-code/issues/24726) – 53 comments, 163 👍  
The most-upvoted open request. Users want control over whether context is automatically added from the active editor. Strong community demand.

### 2. Desktop spawns 1.8GB Hyper-V VM on every launch  
[#29045](https://github.com/anthropics/claude-code/issues/29045) – 27 comments, 56 👍  
Even for chat-only use, the desktop app provisions a heavy VM. Users concerned about resource waste; marked as `invalid` but still actively discussed.

### 3. Proposal: Expose compact/session lifecycle hooks for external memory layers  
[#47023](https://github.com/anthropics/claude-code/issues/47023) – 22 comments, 4 👍  
Directly addresses five older memory-related feature requests. Community is already building 3-tier markdown and knowledge-graph solutions. The core improvement requested is transcript access at compact events.

### 4. Desktop app update deletes session history  
[#48334](https://github.com/anthropics/claude-code/issues/48334) – 16 comments, 3 👍  
`v2.1.34/2.1.63/2.1.92` → `2.1.101` update corrupts `sessions-index.json` and `.jsonl` files. Data-loss severity; users asked to back up manually.

### 5. Mousewheel scrolls input history instead of chat history (Windows)  
[#12953](https://github.com/anthropics/claude-code/issues/12953) – 16 comments, 14 👍  
Long-standing TUI issue on Windows. Reproducible across versions. High popular support given age.

### 6. Feature Request: Shared Team Memory  
[#38536](https://github.com/anthropics/claude-code/issues/38536) – 13 comments, 6 👍  
Knowledge flows between engineers are lost today. Proposal for a shared, persisting context layer at the team level – complements #47023.

### 7. ENOSPC false-positive on subprocess output (macOS)  
[#63909](https://github.com/anthropics/claude-code/issues/63909) – 12 comments, 19 👍  
Bash tool reports “temp filesystem is full (0MB free)” despite free disk. At least 5 duplicates (e.g. #65166, #65915). Highest-bug-activity cluster right now.

### 8. Unbounded MCP server fan-out crashes macOS (kernel panic)  
[#64366](https://github.com/anthropics/claude-code/issues/64366) – 12 comments, 0 👍  
Every Cowork/agent session spawns new MCP server instances; on M2 Max/32GB this causes kernel panics. Resource exhaustion at architectural level.

### 9. Opus 4.8 returns empty thinking blocks  
[#63358](https://github.com/anthropics/claude-code/issues/63358) – 10 comments, 10 👍  
`claude-opus-4-8` returns thinking blocks with an empty `thinking` field. Regression mirrors Opus 4.7 (#49268). UI has nothing to display.

### 10. CLI 2.1.154 breaks with API Error 422 – invalid message role “system”  
[#63423](https://github.com/anthropics/claude-code/issues/63423) – 8 comments, 2 👍  
Recent CLI update sends malformed role strings; blocks all API calls. Forces workarounds with `--raw` or older versions.

---

## Key PR Progress (10 Important)

### 1. Fix triage bot marking Desktop issues as invalid  
[#68678](https://github.com/anthropics/claude-code/pull/68678) (closed)  
The issue triage bot’s validity check incorrectly excluded Claude Desktop bug reports. Now Desktop issues are properly triaged.

### 2. Add `/bug` command to file GitHub issues from terminal  
[#68707](https://github.com/anthropics/claude-code/pull/68707) (open)  
New `bug-reporter` plugin keeps the entire bug-report flow inside Claude Code, auto-collecting environment info.

### 3. Fix hookify loading only `event:all` rules for unknown tools  
[#68672](https://github.com/anthropics/claude-code/pull/68672) (closed)  
When a tool name isn’t `Bash`/`Edit`/`Write`/`MultiEdit`, all rules were loaded instead of just `event:all`. Now narrows correctly.

### 4. Fix PostToolUse hooks cannot return `permissionDecision: deny`  
[#68671](https://github.com/anthropics/claude-code/pull/68671) (closed)  
The rule engine incorrectly allowed `deny` on PostToolUse. Now rejects with a clear error, preventing silent misuse.

### 5. Correct pagination break condition and HTTP 2xx status check  
[#68681](https://github.com/anthropics/claude-code/pull/68681) (closed)  
GitHub API loops broke on `length === 0` instead of `length < 100`, prematurely stopping pagination. Now correct.

### 6. Fix `learning-output-style` for Windows paths  
[#68700](https://github.com/anthropics/claude-code/pull/68700) (closed)  
Backslashes in `CLAUDE_PLUGIN_ROOT` broke bash commands; also missing `bash` prefix caused invocation failure.

### 7. Guard ralph-wiggum against bash 3.x `nounset` on macOS  
[#68702](https://github.com/anthropics/claude-code/pull/68702) (open)  
macOS ships bash 3.2; empty array expansion triggers `set -u` abort. Fix added condition to guard `PROMPT_PARTS`.

### 8. Strip CRLF from Python version probe on Windows  
[#68701](https://github.com/anthropics/claude-code/pull/68701) (open)  
`\r` from Python stdout caused `$v` to be `"3\r"` instead of `"3"`, making the version check always fail.

### 9. Normalize `CLAUDE_PLUGIN_ROOT` backslashes for Windows security-guidance  
[#68694](https://github.com/anthropics/claude-code/pull/68694) (open)  
Backslashes consumed as escape sequences produce mangled paths. Now normalises with `sed` before use.

### 10. Fix ralph-wiggum state file path in help.md  
[#68690](https://github.com/anthropics/claude-code/pull/68690) (open)  
Documented path `.claude/.ralph-loop.local.md` mismatched actual path `.claude/ralph-loop.local.md`. Corrected.

---

## Feature Request Trends

1. **Persistent & Shared Memory** – Multiple high-engagement issues (#47023, #38536) ask for external memory hooks and team-level knowledge persistence. The community is already building workarounds; official hooks would unify these efforts.

2. **VS Code Integration Control** – #24726 (disable auto-attach) and #33058 (add multiple selections incrementally) both reflect demand for finer-grained IDE context management.

3. **Conversation Management** – #65615 (archive/delete conversations) and #48334 indirectly (data-loss prevention) show need for session lifecycle tooling.

4. **Granular Tool Permissioning** – The new `Tool(param:value)` syntax directly addresses requests for selective subagent/model blocking. Expect more issues requesting parameter matching extensions.

5. **Hook & Plugin Ecosystem Maturation** – The 10,000-char hook output limit (#51537) and requests for compact lifecycle hooks indicate users want more powerful, composable extensibility.

---

## Developer Pain Points

- **ENOSPC False Positives (macOS)** – At least 5 duplicate issues report the Bash tool aborting commands with a made-up “temp filesystem full” error. Community frustrated by inability to suppress or work around it.  
- **Data Loss on Desktop Update** – Session history wiped during version upgrades (#48334). Trust in auto-update is shaken.  
- **Model Regressions (Opus 4.8, System Role)** – Two independent regressions (#63358, #63423) break core functionality (thinking blocks, API compatibility). Developers working with Opus models are hit hardest.  
- **Resource Exhaustion (MCP Fan-Out, VM Bloat)** – Unbounded server spawning (#64366) and growing desktop VM disk images (#65577) cause macOS kernel panics and out-of-disk failures.  
- **Subagent Reliability** – Sonnet subagents fail with 1M context (#68727), background subagents can’t write to allowed paths (#50267), and agent loops terminate prematurely (#68735). The multi-agent workflow is still brittle.  
- **UI/UX Nuisances** – VS Code thinking toggle inverted (#49739), scroll not working in conversation panel (#68732), mousewheel misdirection in TUI (#12953). Minor but high-frequency complaints.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-16

## Today's Highlights

OpenAI rolled out **Codex CLI v0.140.0** with new token usage dashboards and improved `/goal` handling for large inputs, alongside several alpha releases for the Rust-based variant. The community is most vocal about **demanding a native Linux desktop app** (Issue #11023, 583 👍), **persistent Windows and macOS performance regressions**, and a crop of **false-positive cybersecurity flags** that interrupt legitimate workflows. Pull request activity focused on plugin recommendation caching, credential brokering, and a new interruptible `sleep` tool for agent models.

## Releases

- **v0.140.0** (full release)
  - Added `/usage` views for daily, weekly, and cumulative token activity per account.
  - `/goal` now preserves oversized text, large pasted blocks, and image attachments (including in remote app-server sessions).
  - Permanent session deletion added.
- **v0.141.0-alpha.1** and **v0.141.0-alpha.2** – preliminary next-cycle builds.
- **v0.140.0-alpha.20** through **v0.140.0-alpha.22** – incremental nightly alpha refinements.

[Full release notes](https://github.com/openai/codex/releases)

## Hot Issues (10 of 50)

1. **[#11023 – Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)**  
   *Created Feb 7, 2026 | 113 comments, 583 👍*  
   The most-requested feature. Users unable to use the macOS app due to power issues want a Linux native client.

2. **[#12661 – Markdown file:// links open in Edge instead of VS Code on Windows](https://github.com/openai/codex/issues/12661)**  
   *47 comments, 43 👍*  
   Long-standing UX bug; 47 replies indicate heavy Windows developer frustration.

3. **[#3355 – Error sending request after MacBook sleeps](https://github.com/openai/codex/issues/3355)**  
   *37 comments*  
   Persists since Sept 2025; network reconnection on wake remains broken for long-running tasks.

4. **[#21527 – Codex is really too slow](https://github.com/openai/codex/issues/21527)**  
   *32 comments, 17 👍*  
   Generic performance complaint spanning both app and VS Code extension; users cite model response latency.

5. **[#25719 – macOS syspolicyd/trustd CPU runaway](https://github.com/openai/codex/issues/25719)**  
   *26 comments, 33 👍*  
   Recurring macOS memory/CPU leak triggered by Desktop app; multiple duplicates exist.

6. **[#27817 – False positive cybersecurity flag on tax filing](https://github.com/openai/codex/issues/27817)**  
   *18 comments*  
   Legitimate finance work blocked by safety classifier. User had to join “Trusted Access for Cyber” program.

7. **[#28015 – False positive repeatedly blocks local repo maintenance (CLI)](https://github.com/openai/codex/issues/28015)**  
   *18 comments*  
   Same pattern as #27817 but in CLI; interrupts paid Pro sessions with extra prompts for routine DevOps tasks.

8. **[#28094 – WSL project paths rewritten as C:\home, losing chat associations](https://github.com/openai/codex/issues/28094)**  
   *13 comments*  
   Windows + WSL users experience broken session-path mapping after recent Desktop update.

9. **[#28190 – rg (ripgrep) blocked by macOS](https://github.com/openai/codex/issues/28190)**  
   *9 comments, 7 👍*  
   Codex CLI dependency `rg` triggers macOS security prompts; prevents CLI operation on macOS.

10. **[#27331 – multi_agent_v2 breaks every turn with 400 error](https://github.com/openai/codex/issues/27331)**  
    *4 comments, 5 👍 (sev3)*  
    Experimental multi-agent feature completely non-functional when enabled; API validation fails even without sub-agent spawning.

## Key PR Progress (10 of 50)

1. **[#28396 – Record external agent import results](https://github.com/openai/codex/pull/28396)**  
   Persists success/failure of external agent imports in state DB, improving reliability of plugin/AGENTS.md imports.

2. **[#28307 – Queue TUI follow-ups through app-server](https://github.com/openai/codex/pull/28307)**  
   Enables durable message queue for follow-ups in TUI mode, reducing client-side memory and enabling ordered dispatch.

3. **[#28441 – Use expect in integration tests](https://github.com/openai/codex/pull/28441)**  
   Cleans up test code by allowing `expect` under Bazel Clippy, reducing verbose `unwrap_or_else` patterns.

4. **[#28399 – Add recommended plugin endpoint cache](https://github.com/openai/codex/pull/28399)**  
   Parses and caches plugin suggestions per account/backend, preventing duplicate warm-ups.

5. **[#27965 – Support `default_tools_approval_mode` in apps._default](https://github.com/openai/codex/pull/27965)**  
   New config option to set default tool approval mode, with documented precedence over per-tool/per-app settings.

6. **[#27704 – Activate endpoint plugin recommendations](https://github.com/openai/codex/pull/27704)**  
   Integrates endpoint recommendation selection into turn construction, eliminating first-turn cache race.

7. **[#28163 – Use local environment for user shell commands](https://github.com/openai/codex/pull/28163)**  
   Fixes user shell commands to use the selected turn environment (e.g., remote) instead of legacy session dir.

8. **[#28034 – Add local credential broker](https://github.com/openai/codex/pull/28034)**  
   Virtualizes GitHub/OpenAI credentials into dummy child tokens; real credentials injected only via MITM proxy.

9. **[#27982 – Start guardian child session at parent initialization](https://github.com/openai/codex/pull/27982)**  
   Reduces latency of auto-review by creating the Guardian child session up-front rather than on demand.

10. **[#28429 – Add interruptible sleep tool](https://github.com/openai/codex/pull/28429)**  
    Built-in `sleep` tool for models to pause without holding a shell process; interruptible when new turn input arrives.

## Feature Request Trends

- **Linux desktop app** – Still the single most upvoted request (583 👍). Users cite macOS power/speed issues and want to leverage Linux hardware.
- **Cross-platform session stability** – Many requests for seamless WSL path handling, macOS sleep reconnection, and Windows elevation consistency.
- **False-positive safety tuning** – Repeated flags on tax, personal finance, and local DevOps tasks erode trust; community asks for context-aware whitelisting.
- **Computer Use on Windows** – Several reports that the Computer Use installation entry is missing on Windows (Hong Kong region flagged specifically).
- **Multi-agent configuration** – Early adopters of `multi_agent_v2` hit showstopper bugs; requests for clearer documentation and fallback behaviour.

## Developer Pain Points

- **Performance across all platforms** – Generic slowness complaints (#21527) dominate, with platform-specific spikes (macOS syspolicyd, Windows WSL latency, Windows firewall interference).
- **Session resumption issues** – `/goal`-first sessions repeatedly hidden from resume lists (#28263, #28423), forcing users to manually supply thread IDs.
- **False-positive cybersecurity blocks** – #27817 and #28015 highlight that even paying Pro users are interrupted by overeager safety checks during legitimate work.
- **Windows-specific friction** – Broken WSL paths (#28094), elevation problems (#25296, #28107), missing Computer Use (#28435), and `codex.exe` access-denied crashes (#28031) create a poor Windows experience.
- **Unstable experimental features** – `multi_agent_v2` (#27331) and Guardian review retry logic (#26334) show that cutting-edge features often degrade usability before stabilizing.

---

*Data source: [github.com/openai/codex](https://github.com/openai/codex) – snapshot 2026-06-16.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*