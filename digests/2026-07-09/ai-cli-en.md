# AI CLI Tools Community Digest 2026-07-09

> Generated: 2026-07-09 02:35 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date**: 2026-07-09 | **Analyst**: Senior Technical Analyst

---

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem, dominated by **Claude Code** (Anthropic) and **OpenAI Codex**, is experiencing a maturation phase punctuated by growing pains in cost management, cross-platform reliability, and agent autonomy. Both communities report **significant billing and quota transparency issues**—users across platforms feel blindsided by token/credit consumption spikes, undermining trust in these tools for daily development workflows. Meanwhile, a clear divergence is emerging: Claude Code is leaning into **multi-agent orchestration** with tiered model architectures, while Codex is prioritizing **tooling integration** (LSP, benchmarking) and **infrastructure reliability** (proxy support, sandbox fixes). The most telling signal is that **both communities are actively requesting features from each other**: Codex users want Claude Code's `/delete` and memory directory patterns; Claude Code users want Codex's first-class MCP and Computer Use support.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Top Issues (today)** | 10 listed | 10 listed |
| **Hot Issue Comments (top)** | 43 (#56913, autonomous agents) | 142 (#28224, SSD write amplification) |
| **Hot Issue Upvotes (top)** | 51 (#26904, `/delete` command) | 427 (#8745, LSP integration) |
| **Key PRs (today)** | 7 merged/in progress | 10 merged/in progress |
| **Release Status** | v2.1.205 (patch release) | Pre-release alphas (rust-v0.144.0-alpha.1/2) |
| **Open Source Progress** | PR #41447 (open 3+ months) | Not open sourced |
| **Notable Regressions** | Token consumption spike (4–10×), Windows Cowork disappearance | Tool-call mis-namespacing, update failure on 0.143.x |
| **Critical Bug Severity** | High (bill-impacting token drain) | Critical (SSD endurance threat, 640 TB/year writes) |

**Key takeaway**: Codex has higher community engagement on individual issues (142 comments vs 43) and more PR throughput today (10 vs 7), but Claude Code's issues are more concentrated on cost-related bugs that affect daily usage. Codex's SSD bug is a **system-level reliability threat** that is more severe in potential hardware damage.

---

## 3. Shared Feature Directions

Despite different architectures, **both communities converge on several key requirements**:

| Feature Need | Claude Code Evidence | OpenAI Codex Evidence |
|---|---|---|
| **Memory/Context Improvements** | `/delete` command (51👍), session management requests, `/fork` branching | Topic-based memory directories (#19758), disable 60s auto-resolve (#28969) |
| **Agent Autonomy & Orchestration** | Tiered Opus/Sonnet multi-agent architecture (#56913, 43 comments) | LSP auto-detect for symbol intelligence (#8745, 427👍), Computer Use in CLI (#20851) |
| **Slash Commands & UX Shortcuts** | `/delete`, `/fork`, `--worktree` requests | `/aliases` request for prompt shortcuts (#31666) |
| **Plugin/MCP Ecosystem** | `protect-mcp` plugin (PR #72014), plugin install merging (#75392) | Plugin install for backend dependency IDs (PR #31694) |
| **Cross-Platform Reliability** | Windows Cowork regression (#75321), OneDrive rename failure (#45178), UTF-8 surrogates (#64777) | Sandbox `apply_patch` failure on Windows (#29072), Amazon Linux tool-call regression (#31511) |
| **Cost/Billing Transparency** | 3 dominant issues on token consumption (#42249, #55053, #54776) | Systemic billing regression draining credits (#31668), rate-limit bugs (#31682) |
| **Session Management** | `/delete` (51👍), statusLine setting in desktop (#60097) | Session cap removal in VS Code (#15368) |

**Common thread**: Users across both platforms are demanding **autonomous, persistent agents with transparent billing**—they want tools that can run long workflows (CI/CD, data pipelines, content generation) without surprise costs or arbitrary session cliffs.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary Focus** | Agent orchestration, multi-model hierarchies | Tooling integration, infrastructure reliability |
| **Target User** | Developers requiring long-running autonomous workflows (ML training, content pipelines) | Developers needing IDE-like intelligence (LSP, diagnostics) and robust cross-platform support |
| **Technical Approach** | Tiered Opus/Sonnet sub-agents with persistent state; Cedar policy gates for security | HTTP client factory pattern for proxy compliance; Bazel-based macrobenchmarking |
| **Plugin/Extension Model** | MCP plugins with Cedar policy enforcement (`protect-mcp`), `--scope project` merging issues | Backend dependency ID resolution, plugin install elicitation flow |
| **Windows Support** | Struggling: 5+ active Windows-specific bugs (Cowork, OneDrive, IME, surrogates) | Struggling: sandbox path crashes, filename length errors, but fewer reported issues |
| **Performance Monitoring** | Community-driven token tracking, no built-in kill switch | Divan-based e2e macrobenchmarks, telemetry standardization (OpenTelemetry spans) |
| **Open Source** | Long-running PR (#41447) to open-source core | Proprietary, no open-source signals |
| **Cost Model** | Session window + daily quota, opaque compression | Monthly credits, billing regression causing single-day drain |

**Key insight**: Claude Code is **architecturally more ambitious** (agent hierarchies, policy gates) but **operationally less transparent** (token accounting, context compression). Codex is **engineering more conservatively** (proxy support, standard telemetry, benchmarking) but **struggles with systemic billing bugs**.

---

## 5. Community Momentum & Maturity

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Issue Engagement** | Moderate (max 43 comments, 51👍) | High (max 142 comments, 427👍) |
| **PR Velocity** | Lower (7 key PRs today) | Higher (10 key PRs today) |
| **Regression Awareness** | High (3 repeated token bugs, Windows cluster) | Very high (SSD bug alarm, billing panic) |
| **Feature Request Sophistication** | Advanced (tiered agents, policy gates, persistent state) | Intermediate (LSP, memory directories, Computer Use in CLI) |
| **Documentation Gaps** | Plugin installation merging, hook handler types | Sandbox path configuration, session cap rationale |
| **Open Source Maturity** | Public PR to open-source, long but stalled | No open-source plans evident |

**Assessment**:
- **Claude Code** has a **more mature but frustrated community**—users see the vision (autonomous agents, policy gates) but are held back by cost opacity and Windows bugs. The open-source PR (#41447) signals a willingness to engage with the broader community, but progress is slow.
- **OpenAI Codex** has **higher raw engagement and faster iteration** (more PRs, faster major bug fixes like the 85% SSD fix) but suffers from **systemic reliability issues** (billing, tool-call regressions) that erode trust. The 427👍 for LSP shows a clear, unmet user need that Codex is not yet addressing.

---

## 6. Trend Signals

Five industry trends emerging from community feedback, with actionable insights for developers:

### 1. **Cost Transparency is a Deal-Breaker**
Both communities report surprise billing events. Claude Code users see 4–10× token spikes; Codex users face full credit drains in one day. **Developers should demand upfront cost estimates and kill switches before adopting any CLI tool for production workflows.**

### 2. **Autonomous Agents Require Guardrails**
The #1 feature request in both ecosystems is for agents that can run long, self-directed workflows without manual intervention. But community experience shows this requires:
- Loop detection (Claude Code sub-agents burn millions of tokens in loops)
- Persistent state (not just memory summaries)
- User-configurable kill switches

### 3. **Cross-Platform (Especially Windows) is an Afterthought**
Both tools treat Windows as a second-class citizen. Claude Code has 5+ active Windows bugs; Codex has sandbox crashes and update failures. **If your team uses Windows, budget for workarounds or consider delaying adoption.**

### 4. **Plugin/MCP Ecosystems are the Next Frontier**
Claude Code's `protect-mcp` plugin (Cedar policy gate + signed receipts) and Codex's backend dependency ID resolution point toward **enterprise-grade, policy-controlled AI tool use**. This is where the tools will differentiate in 6–12 months.

### 5. **"Computer Use" is Converging with CLI**
Codex community wants Computer Use as a CLI primitive (#20851), not just a desktop app feature. This suggests a **convergence of desktop and CLI paradigms**—the CLI is becoming the universal interface, with MCP as the integration layer.

---

## Recommendations for Technical Decision-Makers

| Use Case | Recommended Tool | Rationale |
|---|---|---|
| Long-running autonomous workflows (CI/CD, pipelines) | **Claude Code** (with caution) | Multi-agent architecture is more mature, but monitor token costs closely |
| IDE-integrated development, debugging | **OpenAI Codex** | LSP demand shows community wants IDE-level intelligence, but wait for billing regression fix |
| Cross-platform team (Windows + Mac + Linux) | **Neither (use with fallbacks)** | Both have significant Windows bugs; consider workaround scripts |
| Enterprise security (policy gates, audit trails) | **Claude Code** | `protect-mcp` plugin is ahead; Cedar policy gates are more enterprise-ready |
| High-throughput, cost-sensitive environments | **OpenAI Codex** (after SSD fix) | Faster iteration, better benchmarking, but pin to stable pre-0.143.x versions |

**Bottom line**: Both tools are powerful but **not production-ready for unsupervised use**. Developers should implement their own cost monitoring, loop detection, and cross-platform testing until these ecosystems mature.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Source:** github.com/anthropics/skills | **Snapshot:** 2026-07-09

---

## 1. Top Skills Ranking

The following Skills PRs have attracted the most community discussion and technical scrutiny:

### 1. `skill-creator` — Run-Eval Overhaul (#1298)
- **Functionality:** Fixes `run_eval.py` which has been reporting 0% recall for all skill descriptions across multiple independent reproductions. Patches Windows stream reading, trigger detection logic, and parallel worker coordination.
- **Discussion:** References issue #556 (12 comments) — a critical blocker for the entire description-optimization workflow. This is the most technically contested PR in the repository.
- **Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/1298)

### 2. `document-typography` — Typographic Quality Control (#514)
- **Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Targets universal problems in Claude's document output.
- **Discussion:** Addresses a pervasive UX pain point. Minimal controversy — the community broadly agrees these issues matter.
- **Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/514)

### 3. `odt` — OpenDocument Text Creation (#486)
- **Functionality:** Creates, fills, reads, and converts ODT/ODS files. Triggers on mentions of "ODT", "ODS", "ODF", "OpenDocument", "LibreOffice".
- **Discussion:** Significant interest from open-source and enterprise users who need LibreOffice compatibility. Relatively straightforward acceptance path.
- **Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/486)

### 4. `self-audit` — Mechanical + Reasoning Quality Gate (#1367)
- **Functionality:** Audits AI output before delivery — mechanical file verification followed by a four-dimension reasoning audit in damage-severity priority order. Universal across any project/stack/model.
- **Discussion:** Recently opened (2026-06-28) but already attracting attention as a meta-skill for output quality assurance. Represents a new category of safety-focused Skills.
- **Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/1367)

### 5. `testing-patterns` — Full-Stack Testing Guide (#723)
- **Functionality:** Comprehensive coverage of testing philosophy (Trophy model), unit testing (AAA pattern), React component testing (Testing Library), and E2E/integration testing.
- **Discussion:** Addresses a clear skill gap — developers want Claude to generate better tests. Well-received structure.
- **Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/723)

### 6. `color-expert` — Color Knowledge Skill (#1302)
- **Functionality:** Self-contained color expertise covering naming systems (ISCC-NBS, Munsell, XKCD, RAL), color spaces (OKLCH, OKLAB, CAM16), accessibility contrast, and color harmonies.
- **Discussion:** Niche but authoritative — contributed by a known color-systems expert (meodai). Demonstrates domain-specific depth.
- **Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/1302)

### 7. `skill-quality-analyzer` + `skill-security-analyzer` — Meta-Skills (#83)
- **Functionality:** Two meta-skills for evaluating other Skills across five quality dimensions (structure, documentation, performance, security, UX) and security-specific analysis.
- **Discussion:** First serious attempt at community-driven quality standards. Early-stage but signals demand for skill governance.
- **Status:** Open | [GitHub](https://github.com/anthropics/skills/pull/83)

---

## 2. Community Demand Trends

From Issues activity, the community's most anticipated new Skill directions are:

1. **Security & Trust Boundaries** (#492, 34 comments) — The top-voted issue concerns community skills distributed under the `anthropic/` namespace, creating impersonation risk. Demand for identity verification and permission-scoping frameworks.
2. **Organizational Skill Sharing** (#228, 14 comments) — Enterprise users want org-wide skill libraries, direct sharing links, and centralized management instead of manual `.skill` file distribution.
3. **Skill-Creator Reliability** (#556, #1169, #1061 — collectively ~20 comments) — The description-optimization loop is effectively broken for many users. Three independent issues report 0% recall in `run_eval.py`. Core infrastructure demand.
4. **External Integration** — Issues requesting MCP exposure (#16) and AWS Bedrock compatibility (#29) indicate demand for Skill portability beyond the Claude Code client.
5. **Duplicate Detection** (#189, 6 comments) — Installing `document-skills` and `example-skills` together creates identical skill entries. Community wants deduplication logic.
6. **Agent Governance** (#412, 6 comments) — Proposed skill for policy enforcement, threat detection, and audit trails in agent systems. A security-focused skill direction.

---

## 3. High-Potential Pending Skills

These open PRs have active discussion and technical maturity indicating near-term merge likelihood:

| Skill | PR | Key Contribution |
|-------|----|-----------------|
| `document-typography` | [#514](https://github.com/anthropics/skills/pull/514) | Orphan/widow prevention for generated docs |
| `odt` | [#486](https://github.com/anthropics/skills/pull/486) | LibreOffice/OpenDocument support |
| `testing-patterns` | [#723](https://github.com/anthropics/skills/pull/723) | Full-stack testing methodology |
| `color-expert` | [#1302](https://github.com/anthropics/skills/pull/1302) | Authoritative color-systems knowledge |
| `SAP-RPT-1-OSS` predictor | [#181](https://github.com/anthropics/skills/pull/181) | Tabular foundation model for business analytics |
| `self-audit` | [#1367](https://github.com/anthropics/skills/pull/1367) | Reasoning quality gate + file verification |

All six are open with healthy community engagement. The `odt` and `document-typography` PRs have been open since early March 2026 — they are mature and likely awaiting maintainer review bandwidth.

Additionally, the **Windows compatibility fixes** cluster (#1099, #1050, #362, #361) represents a coordinated community effort to unblock Windows users from the skill-creator toolchain entirely.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for foundational infrastructure reliability** — the `skill-creator` evaluation loop is currently broken on Windows and produces 0% recall for all descriptions, making the entire Skill optimization pipeline unusable, while simultaneously the community requests deeper quality assurance (self-audit, testing patterns, typographic controls) and enterprise-grade distribution (security namespacing, org sharing, external integrations) atop that repaired base.

---

# Claude Code Community Digest – 2026-07-09

## Today’s Highlights

A new patch release (v2.1.205) fixes invalid schema handling and session transcript tampering, but the community’s attention is focused on a wave of cost- and agent‑related issues. Three long‑standing “excessive token consumption” reports (all opened in April–May) continue to dominate discussion, while fresh bugs around stuck background agents and a Windows Cowork regression suggest stability and transparency on billing remain top pain points. The most‑upvoted feature request this week is still the `/delete` command (51 👍), and a high‑profile enhancement for truly autonomous multi‑agent workflows remains the most commented issue of the month.

## Releases

**v2.1.205** – [Release page](https://github.com/anthropics/claude-code/releases/tag/v2.1.205)
- Added an auto‑mode rule that blocks tampering with session transcript files.
- Fixed `--json-schema` silently producing unstructured output when the schema was invalid, and schemas using the `format` keyword being rejected.
- Fixed a message sent while Claude was working being truncated (silent cut‑off).

## Hot Issues

1. **#56913** [[link]](https://github.com/anthropics/claude-code/issues/56913) – **Make autonomous Claude Code viable** (43 comments)  
   *Enhancement* proposing tiered Opus controllers + Sonnet sub‑agents + persistent state. The highest‑engagement discussion in the repo, reflecting strong demand for long‑running orchestration (pipelines, ML training, content workflows). Community is split on cost vs. reliability.

2. **#42249** [[link]](https://github.com/anthropics/claude-code/issues/42249) – **Extreme token consumption on macOS** (40 comments, 17 👍)  
   Normal dev tasks (read, edit, git) drain daily quota in ~1 hour. Users suspect a regression in tool‑call token accounting. 20× customers report sudden spikes.

3. **#55053** [[link]](https://github.com/anthropics/claude-code/issues/55053) – **5‑hour session window depletion 5–10× faster since Apr 29** (37 comments, 12 👍)  
   Light editing sessions burn 20–25% of the window in under an hour. Sonnet sub‑agents blamed for the acceleration.

4. **#54776** [[link]](https://github.com/anthropics/claude-code/issues/54776) – **100% quota in 1–2 hours** (33 comments, 12 👍)  
   Similar to #42249/#55053 – user went from 10% to 100% usage per session. No platform‑specific root cause identified yet.

5. **#61993** [[link]](https://github.com/anthropics/claude-code/issues/61993) – **Sub‑agents cannot spawn sub‑agents on Windows** (19 comments)  
   `Task`/`Agent` primitives not exposed in nested contexts. Limits multi‑layer agent decomposition for Windows users.

6. **#45178** [[link]](https://github.com/anthropics/claude-code/issues/45178) – **Cowork fails on Windows 11 with OneDrive (EXDEV)** (14 comments)  
   Cross‑device link error when renaming files within the same directory. OneDrive’s file‑system shim breaks the rename operation.

7. **#64777** [[link]](https://github.com/anthropics/claude-code/issues/64777) – **API 400: UTF‑8 surrogates in JSON body** (8 comments)  
   Mid‑conversation error on Windows + VS Code. Caused by invalid UTF‑8 surrogates, possibly from clipboard or file content.

8. **#69781** [[link]](https://github.com/anthropics/claude-code/issues/69781) – **Image paste fails with UTF‑8 surrogate error** (7 comments)  
   Reproducible on macOS desktop app. Same root cause as #64777 – surrogates not allowed in request body.

9. **#72080** [[link]](https://github.com/anthropics/claude-code/issues/72080) – **Sub‑agents stuck in infinite loops** (6 comments)  
   Main agent recovers from loops, but sub‑agents now inherit the same behaviour, burning massive tokens before being killed.

10. **#75321** [[link]](https://github.com/anthropics/claude-code/issues/75321) – **Cowork tab missing on Windows 11 Home 25H2** (5 comments)  
    Worked for weeks, then disappeared after auto‑update. Backend reports `yukonSilver status=unsupported` despite full virtualization support.

## Key PR Progress

1. **#75938** [[link]](https://github.com/anthropics/claude-code/pull/75938) – **fix(sweep): unstarve `markStale` via search API**  
   Prevents stale‑label machinery from only walking the oldest issues by switching to a search‑based approach that skips unactionable items.

2. **#41447** [[link]](https://github.com/anthropics/claude-code/pull/41447) – **feat: open source claude code** (still open after 3+ months)  
   Long‑running PR aiming to release the core under an open‑source license. Closes many related issues.

3. **#75541** [[link]](https://github.com/anthropics/claude-code/pull/75541) – **fix(sweep): paginate issue events and honor unlabeled when closing expired**  
   Fixes auto‑close logic that missed lifecycle labels beyond the first 100 events.

4. **#72014** [[link]](https://github.com/anthropics/claude-code/pull/72014) – **Add protect-mcp plugin: fail‑closed Cedar policy gate + signed receipts**  
   New plugin that blocks tool calls violating policies and produces offline‑verifiable receipts. A step toward enterprise MCP governance.

5. **#68673** [[link]](https://github.com/anthropics/claude-code/pull/68673) – **fix(scripts): break pagination when page is not full**  
   Minor pagination bug fix for script infrastructure.

6. **#75537** [[link]](https://github.com/anthropics/claude-code/pull/75537) – **fix(hook-development): recognize all five hook handler types**  
   Updates the `plugin-dev` skill to document and validate all supported hook types (from two to five), closing a long‑standing developer experience gap.

7. **#75529** [[link]](https://github.com/anthropics/claude-code/pull/75529) – **docs(code-review plugin): clarify relationship to bundled `/code-review` skill**  
   Documents that the `code-review` plugin (PR review via `gh`) is separate from the built‑in local‑diff `/code-review` skill, and fixes installation instructions.

## Feature Request Trends

The community is converging on several high‑value feature areas:

- **Autonomous multi‑agent orchestration** – The most commented issue (#56913) calls for a tiered brain architecture: an Opus “director” spawning Sonnet workers with persistent state. This would unlock long‑running, self‑directed workflows (CI/CD, data pipelines, content generation).
- **Session management** – The top‑voted request (#26904, 51 👍) wants a `/delete` command. Other requests include `/fork` (conversation branching, #46451 closed but still desired) and `--worktree` support in VS Code for parallel sessions (#69554).
- **Desktop UI improvements** – Users want the `statusLine` setting (git worktree, cwd) exposed in the desktop app (#60097), and a dynamic timestamp per prompt to keep the model aware of elapsed time in long sessions (#73800).
- **Plugin ecosystem** – The `protect-mcp` plugin (PR #72014) shows interest in security‑hardened MCP tool calls. The community also demands better plugin installation – the current `--scope project` overwrites rather than merges `installed_plugins.json` (#75392).

## Developer Pain Points

Recurring frustrations across the issue tracker:

- **Cost & quota transparency** – Sudden token spikes (4x–10x) with no clear cause; session windows depleting unrealistically fast. Users feel blindsided by billing – the three top‑commented bugs all revolve around token consumption.
- **Agent loop deadlocks** – Sub‑agents getting stuck in infinite “count <invoke” loops, sometimes burning millions of tokens before crashing (#72080, #67636, #75314). No built‑in kill switch or loop detection.
- **Windows compatibility** – A cluster of Windows‑specific bugs: Cowork missing after updates (#75321), OneDrive cross‑device rename failures (#45178), CJK IME input broken (#75920), drive‑letter case not canonicalised (#75855), and UTF‑8 surrogate errors in API requests (#64777).
- **Unclear context compression** – When sessions grow long, the model loses access to earlier conversation history, yet the UI still displays it – leading to confusion and no user‑facing opt‑out (#75924).
- **API reliability** – Frequent `ECONNRESET` errors (#72422) and subscription blocking with opaque “organization has disabled” messages (#75944) disrupt workflows without clear remediation steps.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

Here is the **OpenAI Codex Community Digest** for **2026-07-09**.

---

## Today’s Highlights
The community is feeling the heat from a **major I/O and SSD endurance bug** (Issue #28224) where SQLite feedback logging could theoretically write 640 TB/year—though a fix has reduced logs by 85%. Meanwhile, a **systemic billing regression** is affecting multiple paid accounts (Issue #31668), draining monthly credits after a single prompt. On the development side, a new **e2e macrobenchmarking framework** (PR #31295) has landed, promising more rigorous performance tracking going forward.

## Releases
Two **pre-release alpha versions** were published in the last 24 hours:
- **`rust-v0.144.0-alpha.1`** (2026-07-09)
- **`rust-v0.144.0-alpha.2`** (2026-07-09)

No changelog details are available for these builds, though they likely contain fixes for the 0.143.x instability reported this week (tool-call regressions, update failure, etc.).

## Hot Issues (Top 10)
1. **[#28224] SQLite feedback logs could write ~640 TB/year**  
   *Tags: bug, CLI, performance*  
   A 142-comment firestorm. The sheer scale of the potential write amplification (640 TB/year) alarmed the community (+427 👍). Fix PRs have been merged in v0.142.0, reducing logs by 85%, and the reporter is closing the issue.  
   [View Issue](https://github.com/openai/codex/Issue%20#28224)

2. **[#8745] LSP integration (auto-detect + auto-install) for Codex CLI**  
   *Tags: enhancement, agent*  
   The most popular feature request (+407 👍, 55 comments). Users want built-in Language Server Protocol support so Codex can use diagnostics and symbol intelligence directly. Community consensus: this would dramatically reduce hallucinated imports and wrong API usage.  
   [View Issue](https://github.com/openai/codex/Issue%20#8745)

3. **[#29072] Windows `apply_patch` fails due to sandbox-setup.exe path issue**  
   *Tags: bug, windows-os, sandbox, tool-calls*  
   A show-stopper for Windows users: every `apply_patch` call crashes because the sandbox setup EXE can't launch from the package path. The community is frustrated (40 comments), as the workaround requires manual path edits.  
   [View Issue](https://github.com/openai/codex/Issue%20#29072)

4. **[#15368] Increase session cap in VS Code extension**  
   *Tags: enhancement, extension*  
   Pro users are hitting hard session limits in VS Code. Evidence from local extension code suggests an arbitrary cap. This is a common pain point for power users running long workflows.  
   [View Issue](https://github.com/openai/codex/Issue%20#15368)

5. **[#28969] Add setting to disable 60-second auto-resolve for questions**  
   *Tags: bug, enhancement, CLI, plan*  
   The aggressive auto-resolve timer (60s) is causing agent plans to abort prematurely. The community (+92 👍) wants an explicit disable setting, especially for complex planning tasks where model thinking takes longer.  
   [View Issue](https://github.com/openai/codex/Issue%20#28969)

6. **[#31520] Update command fails with "Could not find Codex package"**  
   *Tags: bug, CLI*  
   A fresh regression (12 comments) affecting users upgrading from 0.142.x to 0.143.x. The installer can't find the platform-specific npm asset, leaving users stuck.  
   [View Issue](https://github.com/openai/codex/Issue%20#31520)

7. **[#26860] GPT-5.5 xhigh stops mid-task via Amazon Bedrock**  
   *Tags: bug, CLI, custom-model, connectivity, aws-bedrock*  
   A recurring issue on both Windows and Linux: the model silently stops mid-task when routed through Amazon Bedrock. The community suspects a timeout mismatch between Codex’s CLI and Bedrock’s inference endpoint.  
   [View Issue](https://github.com/openai/codex/Issue%20#26860)

8. **[#19758] Topic-based memory directory with agent-initiated writes**  
   *Tags: enhancement, agent, memory*  
   Users are asking for a structured memory architecture: topic-based directories instead of a monolithic `memory_summary.md`. This borrows from Claude Code’s memdir layout and the oh-my-codex memory system.  
   [View Issue](https://github.com/openai/codex/Issue%20#19758)

9. **[#20851] First-class Computer Use support in Codex CLI**  
   *Tags: enhancement, MCP, CLI, computer-use*  
   Computer Use is currently tied to the desktop app. Developers want it as a first-class CLI capability, exposing the MCP helper directly without app dependencies.  
   [View Issue](https://github.com/openai/codex/Issue%20#20851)

10. **[#28643] File reference line links unreliable in Codex Desktop App**  
    *Tags: bug, app*  
    A persistent UX annoyance: clicking file references with line numbers often fails to jump. This undermines trust in the app’s output display.  
    [View Issue](https://github.com/openai/codex/Issue%20#28643)

## Key PR Progress (Top 10)
1. **[#31694] Allow plugin installs for backend dependency IDs**  
   *Author: cravuri-oai*  
   Extends `request_plugin_install` to resolve exact backend plugin IDs even when they aren't in the recommended list. Cleans up the install-elicitation flow.  
   [View PR](https://github.com/openai/codex/PR%20#31694)

2. **[#31176] Retry goals after model capacity errors**  
   *Author: etraut-openai*  
   Active goals currently stop on any error. This PR makes model-capacity errors retryable (no token cost), preventing unnecessary user intervention on transient overloads.  
   [View PR](https://github.com/openai/codex/PR%20#31176)

3. **[#31361] Route model discovery through HTTP client factory**  
   *Author: bolinfest*  
   Fixes a startup-critical issue where `/models` ignored OS proxy settings. Now model catalog refreshes respect `features.respect_system_proxy`.  
   [View PR](https://github.com/openai/codex/PR%20#31361)

4. **[#31362] Route realtime and memories through HTTP client factory**  
   *Author: bolinfest*  
   Extends the proxy-respect fix to realtime calls and memory summarization, ensuring all first-party API requests follow system proxy policy.  
   [View PR](https://github.com/openai/codex/PR%20#31362)

5. **[#31295] Add `codex help` e2e macrobenchmark**  
   *Author: anp-oai*  
   Introduces a Bazel-backed end-to-end benchmark suite using Divan. Starts with a simple `codex --help` benchmark as a deterministic first consumer.  
   [View PR](https://github.com/openai/codex/PR%20#31295)

6. **[#31687] Standardize JSON-RPC request spans in exec-server**  
   *Author: anp-oai*  
   Adds `rpc.system`, `rpc.method`, and `rpc.request_id` to exec-server spans, matching app-server telemetry conventions for better debugging.  
   [View PR](https://github.com/openai/codex/PR%20#31687)

7. **[#31689] Centralize client RPC spans in exec-server**  
   *Author: anp-oai*  
   Moves RPC instrumentation into the shared `call_inner` path, ensuring all client requests (including `environment/info`) get traced properly.  
   [View PR](https://github.com/openai/codex/PR%20#31689)

8. **[#30188] Persist TurnItems for paginated thread rollouts**  
   *Author: owenlin0*  
   New threads with `history_mode: "paginated"` now persist `ItemCompleted` events in rollout JSONL. This is foundational for long-context thread support.  
   [View PR](https://github.com/openai/codex/PR%20#30188)

9. **[#31429] CI: smoke Bazel e2e benchmarks**  
   *Author: anp-oai*  
   Adds a `just bench-e2e-smoke` target to the Linux GNU Bazel CI job, ensuring the macrobenchmark path stays runnable.  
   [View PR](https://github.com/openai/codex/PR%20#31429)

10. **[#31428] Add e2e benchmark entrypoints**  
    *Author: anp-oai*  
    Stable local and CI entrypoints for Bazel macrobenchmarks: `just bench-e2e` for optimized runs, `just bench-e2e-smoke` for quick checks.  
    [View PR](https://github.com/openai/codex/PR%20#31428)

## Feature Request Trends
- **LSP Integration (Issue #8745):** The most-upvoted request (+407). Users want Codex to auto-detect and install language servers for symbol intelligence and diagnostics.
- **Memory & Context Improvements (Issues #19758, #28969):** A push toward topic-based memory directories and user-controlled auto-resolve timers for long-running planning sessions.
- **First-class CLI Computer Use (Issue #20851):** Developers want Computer Use decoupled from the desktop app, as a CLI-accessible MCP capability.
- **Session & Scaling Enhancements (Issue #15368, #23324):** Requests to remove the session cap in VS Code and allow sub-agent auto-approval policies to inherit from parent agents.
- **Slash Commands (Issue #31666):** A request for `/aliases` to create local prompt shortcuts, mimicking tools like Interbase CLI.

## Developer Pain Points
- **Massive SQLite Write Amplification (Issue #28224):** The most critical bug this week. 640 TB/year of writes could physically destroy consumer SSDs within months. The 85% fix is live, but the severity shook trust in default logging defaults.
- **Cross-Platform Sandbox Crashes (Issues #29072, #31511, #31611):** Windows and Amazon Linux users face `apply_patch` failures, false “filename too long” errors, and `unsupported call: exec_command` regressions in 0.143.0.
- **Tool-Call Regressions in GPT-5.5 (Issues #31609, #31665):** The latest models are mis-namespacing tool calls (`exec_commandexec_command`), breaking core workflows. Users are pinning to older CLI versions as a workaround.
- **High CPU/Resource Drain (Issues #30248, #31676):** macOS Desktop spins at 100% CPU from a single heartbeat automation; Windows Desktop freezes after typing a prompt.
- **Rate-Limit & Billing Bugs (Issues #31668, #31682):** Paid users are seeing their monthly credits drained in a single day, with resets failing and counters incorrectly decremented. This is systemic and causing billing alarm.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*