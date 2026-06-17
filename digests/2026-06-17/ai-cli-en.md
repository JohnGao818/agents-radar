# AI CLI Tools Community Digest 2026-06-17

> Generated: 2026-06-17 03:40 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Ecosystem — 2026-06-17

## 1. Ecosystem Overview

The AI developer tool CLI space is characterized by rapid iteration, with both major players shipping new releases this week despite lingering cross-platform stability issues. Community engagement remains high, with Windows-specific problems dominating the issue tracker for both Claude Code and OpenAI Codex, while feature requests increasingly focus on extensibility (MCP/plugin ecosystems), session-level control, and cost transparency. The divergence in release cadence—Claude Code issuing a stable patch vs. Codex pushing alpha builds—reflects different maturity stages, but both tools are actively evolving based on real-world user pain points.

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Notable Issues** | 10 hot issues (up to 87 comments) | 10 hot issues (up to 46 comments) |
| **Key PRs** | 10 PRs (5 security/infra-focused) | 10 PRs (6 feature-oriented) |
| **Releases Today** | v2.1.179 (stable, fix regressions) | rust-v0.141.0-alpha.3 & .4 (alpha, no changelog) |
| **Community Contribution** | Strong (AZERDSQ131 – 6+ PRs merged) | Moderate (mostly internal/team PRs) |

Both tools show similar volume of tracked activity, but Claude Code has a higher engagement ceiling on individual issues (87 comments vs. 46), suggesting a larger active user base voicing concerns. Codex’s alpha releases indicate active development but less production-grade stability communication.

## 3. Shared Feature Directions

Several requirements are emerging across both communities:

- **Windows as first‑class platform** — Both tools face repeated Windows-specific bugs: orphaned process locks (Claude #42776), app crashes on non‑ASCII paths (Codex #27506), infinite git processes (Codex #20567), and WSL2 scrolling regressions (Claude). The demand for parity with macOS/Linux is clear.

- **Session‑level context control** — Users want to manage the working directory mid‑session (Codex #12464 `/cwd` command; Claude #37569 requests `–no-stream` and better loop control). Token budget management is also common: Claude users report runaway agent loops (#68961) while Codex introduces shared session token budgets (PR #28494).

- **MCP / plugin ecosystem growth** — Both tools are investing in MCP or plugin extensibility. Claude has MCP server configuration leaks (#65429) and skill-creator process leaks (#68933); Codex is building TUI plugin sharing (PR #26705–#26703) and supporting object‑valued MCP manifests (PR #28580). The common need is robust, sandboxed third-party integration.

- **Cost / quota transparency** — Claude users hit billing bugs (#65514, #68978) and want better rate‑limit visibility. Codex users experience context window exhaustion (#18052) and demand graceful degradation. Both communities seek predictable consumption.

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|-----------|-------------|--------------|
| **Primary user pain** | Model reliability (Opus 4.8 malformed tool calls, quota miscalibration) | Auth barriers (phone‑number lockout, account recovery) and desktop data visibility |
| **Extensibility approach** | MCP servers, hooks, workflows, `/bug` command, security‑guidance PRs | Plugin catalog in TUI, remote MCP OAuth refresh, credential broker |
| **Target environment** | CLI-heavy, with Desktop app for Windows (roughest platform) | Desktop + CLI, with strong VS Code integration (detached chat requests) |
| **Community contribution** | External contributor (AZERDSQ131) driving infrastructure fixes | Fewer external PRs; focus on internal API and proxy improvements |
| **Release maturity** | Stable patches weekly; changelogs detailed | Alpha releases with minimal notes; slower issue resolution for critical bugs (e.g., phone verification) |

Claude Code leans into **model‑fidelity and extensibility infrastructure** – the community demands better model behavior (Opus 4.8) and secure plugin execution. OpenAI Codex prioritizes **user experience and authentication** – the top issue is a locked account, and the most‑upvoted feature is session‑level directory switching. Codex’s PRs also show deeper architectural work (workload identity federation, credential brokering) aimed at enterprise CI/CD adoption.

## 5. Community Momentum & Maturity

Claude Code demonstrates **higher community momentum** based on comment volume per issue, active external contributor PRs (6+ from one contributor in a single day), and a clear release cadence with transparent changelogs. The Windows relaunch bug (#42776) alone has 87 comments, indicating a vocal, engaged user base. However, the model reliability issues (Opus 4.8) reveal a vulnerability in its quality core.

OpenAI Codex has a **dedicated but more constrained community**. The phone‑number lockout (#25749) shows systemic auth friction that slows adoption. The alpha releases suggest the Rust rewrite is still maturing; the lack of changelogs may erode trust. Codex’s strength lies in deeper enterprise features (managed config enforcement, workload identity) that signal long‑term investment, but current pain points around data loss and desktop stability are more fundamental.

## 6. Trend Signals

From the combined community feedback, several industry‐level signals emerge for developers and decision‑makers:

- **Windows support is the next frontier.** Both tools are bleeding on Windows. Organizations deploying AI coding assistants on Windows should budget extra time for debugging process leaks, path encoding issues, and App‑specific crashes. This is a critical gap in “developer experience” claims.

- **Model quality remains the primary value driver.** Claude’s Opus 4.8 issues show that users quickly revert when model reliability degrades. Tool developers must tightly couple model updates with rigorous tool‐call validation, or risk losing trust faster than they can patch UI bugs.

- **Token budget and cost governance are becoming table‑stakes.** Users are no longer willing to “let the agent run free.” Both communities demand transparent quotas, the ability to limit context consumption, and visible billing logic. This is especially important for enterprise adoption.

- **Credential and security management is evolving.** The move toward OIDC authentication (Codex PR #27713), local credential brokers (Codex #28034), and symlink escape prevention (Claude #68689) signals a shift from “get it working” to “get it secure” – a necessary evolution as these tools access production environments.

- **Remote workspaces and cross‑platform portability are emerging needs.** Codex’s SSH remote workspaces request and Claude’s WSL‑specific config leaks point to a future where the CLI runs across diverse compute environments. Tooling must handle hybrid cloud/local setups seamlessly.

*Developers evaluating AI CLI tools should weigh immediate stability (Claude Code’s faster patch cycle) against enterprise auth and workspace features (Codex’s evolving proxy and federation support). Both need to invest in Windows robustness to become truly universal.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
*Data snapshot: 2026-06-17 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Pull Requests represent the most-discussed skill proposals and improvements in the community, based on comment activity and engagement.

| # | PR | Skill | Functionality | Status |
|---|-----|-------|---------------|--------|
| 1 | [#514](https://github.com/anthropics/skills/pull/514) | **document-typography** | Prevents orphaned words, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses a universal pain point in Claude’s output. | Open (since Mar 2026) |
| 2 | [#486](https://github.com/anthropics/skills/pull/486) | **ODT skill** | Creates, fills, reads, and converts OpenDocument files (.odt, .ods). Targets LibreOffice and ISO-standard document workflows. | Open (since Mar 2026) |
| 3 | [#210](https://github.com/anthropics/skills/pull/210) | **frontend-design** | Revises the existing frontend-design skill for greater clarity, actionability, and single-conversation execution. High interest from frontend developers. | Open (since Jan 2026) |
| 4 | [#83](https://github.com/anthropics/skills/pull/83) | **skill-quality-analyzer / skill-security-analyzer** | Meta-skills that evaluate other skills on structure, documentation, and security. Reflects the community’s desire for quality assurance tooling. | Open (since Nov 2025) |
| 5 | [#181](https://github.com/anthropics/skills/pull/181) | **SAP-RPT-1-OSS predictor** | Integrates SAP’s open-source tabular foundation model for predictive analytics on business data. Enterprise-focused. | Open (since Dec 2025) |
| 6 | [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | Comprehensive testing skill covering the full stack: unit, React component, integration, and E2E testing. Follows the Testing Trophy model. | Open (since Mar 2026) |
| 7 | [#568](https://github.com/anthropics/skills/pull/568) | **servicenow** | Broad ServiceNow platform assistant covering ITSM, ITOM, SecOps, ITAM, FSM, SPM, and IntegrationHub. | Open (since Mar 2026) |
| 8 | [#444](https://github.com/anthropics/skills/pull/444) | **AURELION suite** (kernel, advisor, agent, memory) | Structured cognitive framework for professional knowledge management with persistent memory and agent orchestration. | Open (since Feb 2026) |

**Discussion themes**: The community is actively debating skill scope (narrow vs. platform-wide), cross-platform compatibility (especially Windows), and the need for meta-skills that improve skill creation and validation. PRs related to the `skill-creator` tooling (e.g., #538, #539, #541, #1298) also draw heavy engagement, indicating that the **developer experience of building skills** is a top concern.

---

## 2. Community Demand Trends

From the top Issues (sorted by comment volume), four clear demand clusters emerge:

1. **Skill sharing & distribution** — Issue [#228](https://github.com/anthropics/skills/issues/228) (14 comments) calls for org-wide skill sharing without manual file transfers. Users want a shared skill library or direct sharing links inside Claude.ai.

2. **Tooling reliability** — Issues [#556](https://github.com/anthropics/skills/issues/556) (12 comments) and [#1169](https://github.com/anthropics/skills/issues/1169) (3 comments) report that `run_eval.py` always returns 0% recall, breaking the skill-description optimization loop. Multiple contributors are reproducing the bug on different platforms.

3. **Security & trust** — Issue [#492](https://github.com/anthropics/skills/issues/492) (7 comments) highlights that community skills are distributed under the `anthropic/` namespace, creating trust-boundary vulnerabilities. A related issue [#1175](https://github.com/anthropics/skills/issues/1175) (4 comments) raises security concerns around embedding access control logic inside `SKILL.md` for SharePoint document handling.

4. **Cross-platform compatibility** — Issues [#1061](https://github.com/anthropics/skills/issues/1061) (3 comments) and the ongoing *Windows subprocess bugs* (seen across multiple PRs) show strong demand for native Windows support in the skill-creator scripts. Users on Windows cannot evaluate or optimize skills without patching.

**Emerging skill directions** (from new skill proposals):
- **Agent governance** — Issue [#412](https://github.com/anthropics/skills/issues/412) proposes a skill for safety patterns (policy enforcement, threat detection, audit trails).
- **MCP integration** — Issue [#16](https://github.com/anthropics/skills/issues/16) asks to expose skills as MCP servers, enabling programmatic APIs for skill functionality.
- **AWS Bedrock compatibility** — Issue [#29](https://github.com/anthropics/skills/issues/29) (4 comments) requests guidance or adaptation for running skills on Bedrock.

---

## 3. High-Potential Pending Skills

These open PRs have active discussions and recent updates, making them likely candidates for merging in the near term:

- **[#723 – testing-patterns](https://github.com/anthropics/skills/pull/723)** (updated 2026-04-21)  
  A full-stack testing skill with unit, React, and E2E coverage. The comprehensive scope and clear demand (testing is a universal developer need) make it a strong candidate.

- **[#444 – AURELION suite](https://github.com/anthropics/skills/pull/444)** (updated 2026-05-06)  
  A structured cognitive framework with persistent memory. The ecosystem of four skills (kernel, advisor, agent, memory) addresses the growing need for multi-session context management.

- **[#568 – servicenow](https://github.com/anthropics/skills/pull/568)** (updated 2026-04-23)  
  A broad enterprise platform skill. Its breadth may require refinement, but the high enterprise interest and active maintainer suggest progress.

- **[#1298 – fix(skill-creator): run_eval.py always reports 0% recall](https://github.com/anthropics/skills/pull/1298)** (updated 2026-06-11)  
  This is a critical infrastructure fix. With 10+ independent reproductions of the bug, the PR’s resolution is urgent and likely to be merged soon.

- **[#361 / #362 – YAML and UTF-8 fixes for quick_validate.py](https://github.com/anthropics/skills/pull/361)** (updated 2026-06-10)  
  These twin PRs prevent silent parsing failures and Rust panics. They eliminate two major friction points for skill creators.

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for robust, cross-platform tooling that validates, tests, and shares skills—reflecting a shift from “what can a skill do?” to “how do we reliably build and distribute skills at scale?”**

---

# Claude Code Community Digest — 2026-06-17

## Today's Highlights

Anthropic shipped **v2.1.179** fixing WSL2 mouse-wheel scrolling and mid-stream connection drops, patching a pair of regressions from last week. The community is buzzing around **Opus 4.8 performance concerns** (#63604, #68820, #68624) and a **stubborn Windows desktop relaunch bug** (#42776) that has attracted 87 comments. A massive wave of infrastructure PRs from contributor **AZERDSQ131** landed across scripts, security guidance, and CI tooling.

## Releases

**v2.1.179** — Released today
- Fixed mid-stream connection drops: partial responses are now preserved instead of showing a raw error, and the spinner no longer gets stuck at "running tool"
- Fixed mouse-wheel scrolling in WSL2 under Windows Terminal and VS Code (regression in v2.1.172)
- Fixed a sandbox `denyR` issue (details truncated in changelog)

## Hot Issues

1. **[#42776] Windows Desktop Relaunch Fails Due to Orphaned Process File Lock**  
   *87 comments, 31 👍*  
   The most active open issue. Claude Code Desktop cannot relaunch on Windows because a previous process holds a file lock. Community has reproduced across multiple Windows builds but no fix yet.  
   [Link](https://github.com/anthropics/claude-code/issues/42776)

2. **[#65514] Pro Plan Blocked Despite 17% Usage for 1M Context**  
   *17 comments*  
   Users on the Pro plan with plenty of remaining quota are being told they need credits to use the 1M context window. Likely a billing/inventory logic bug.  
   [Link](https://github.com/anthropics/claude-code/issues/65514)

3. **[#30533] [CLOSED] Microsoft 365 MCP: Add Support for Reading Email Attachments**  
   *17 comments, 15 👍*  
   A popular feature request now closed (presumably merged). Community wanted MCP-based access to email attachments from Microsoft 365. Good sign for MCP ecosystem growth.  
   [Link](https://github.com/anthropics/claude-code/issues/30533)

4. **[#63604] Opus 4.8 Repeatedly Emits Malformed tool_use Blocks**  
   *10 comments, 12 👍*  
   Entire responses discarded because the model sends broken `tool_use` blocks. Users report reverting to Opus 4.7 works fine. Model reliability concern.  
   [Link](https://github.com/anthropics/claude-code/issues/63604)

5. **[#42417] [CLOSED] New Renderer: Japanese Text Clipboard Garbled on Windows (Mojibake via OSC 52)**  
   *9 comments, 9 👍*  
   Fixed in a recent build but highlights ongoing i18n challenges with the TUI renderer on Windows.  
   [Link](https://github.com/anthropics/claude-code/issues/42417)

6. **[#65429] System Prompt Consumes ~9.3M Tokens on Every Session After Installing Claude Desktop (WSL)**  
   *9 comments*  
   MCP servers configured on Windows bleed into WSL sessions, causing massive token consumption before any work begins. Cost and UX bug.  
   [Link](https://github.com/anthropics/claude-code/issues/65429)

7. **[#68933] skill-creator Eval/Optimizer Leaks MCP Child Processes, Forces Hard Reboot**  
   *4 comments*  
   Headless `claude -p` processes each boot MCP servers, leading to memory exhaustion. Reproducible with Firebase MCP.  
   [Link](https://github.com/anthropics/claude-code/issues/68933)

8. **[#37569] Feature Request: Option to Disable Streamed Response Output**  
   *3 comments, 15 👍*  
   Many developers find token-by-token streaming distracting. They want a `--no-stream` flag to receive the complete response at once.  
   [Link](https://github.com/anthropics/claude-code/issues/37569)

9. **[#68969] Workflow Tool: args Arrives JSON-Stringified; Named Workflow Edits Don't Hot-Reload**  
   *2 comments*  
   Two bugs in one report: `args` parameter is double-encoded, and changes to saved workflows aren't picked up mid-session.  
   [Link](https://github.com/anthropics/claude-code/issues/68969)

10. **[#68978] Pro Subscription Rate-Limited After Single Deep Research Run**  
    *1 comment*  
    Users report exhausting their entire Pro quota after one intensive research session, suggesting the usage accounting may be miscalibrated.  
    [Link](https://github.com/anthropics/claude-code/issues/68978)

## Key PR Progress

1. **[#46351] Enable PowerShell Tool on macOS and Linux When pwsh is Available**  
   *Closed — significant feature*  
   Unlocks PowerShell as a native tool on non-Windows platforms if PowerShell Core is installed. Addresses a long-standing gap.  
   [Link](https://github.com/anthropics/claude-code/pull/46351)

2. **[#68787] fix(scripts): Add Error Message to edit-issue-labels.sh**  
   *Open*  
   Silent exit code 1 replaced with a human-readable stderr message when no label arguments are provided.  
   [Link](https://github.com/anthropics/claude-code/pull/68787)

3. **[#68786] fix(plugin-dev): Avoid Shell Injection in test-hook.sh via Stdin Redirection**  
   *Open — security*  
   Replaces a vulnerable `bash -c` pattern with safer heredoc/redirection to prevent injection via `$TEST_INPUT`.  
   [Link](https://github.com/anthropics/claude-code/pull/68786)

4. **[#68785] fix(plugin-dev): Hook JSON to Stdout, Tighten su\* Glob, Fix CI Detection**  
   *Open*  
   Fixes three bugs in example hook scripts: stderr vs stdout for JSON, overly broad glob patterns, and CI environment detection.  
   [Link](https://github.com/anthropics/claude-code/pull/68785)

5. **[#68673] fix(scripts): Break Pagination When Page Is Not Full**  
   *Open*  
   Prevents infinite pagination loops in CI scripts by stopping when a page has fewer items than the page size.  
   [Link](https://github.com/anthropics/claude-code/pull/68673)

6. **[#68678] fix(triage): Don't Mark Claude Desktop Issues as Invalid**  
   *Open*  
   Adjusts the triage bot to not auto-close Desktop issues as invalid, reducing noise from misclassified reports.  
   [Link](https://github.com/anthropics/claude-code/pull/68678)

7. **[#68679] fix(ralph-wiggum): Strip Control Characters Before Promise Comparison**  
   *Open*  
   Sanitizes output strings before matching against expected promises in the CI test framework.  
   [Link](https://github.com/anthropics/claude-code/pull/68679)

8. **[#68689] fix(security-guidance): Block Symlink Escape in Extensibility Config Reads**  
   *Open — security*  
   Prevents path traversal through symbolic links when reading configuration files for plugins/workflows.  
   [Link](https://github.com/anthropics/claude-code/pull/68689)

9. **[#68694] fix(security-guidance): Normalize CLAUDE_PLUGIN_ROOT Path Separators on Windows**  
   *Open*  
   Ensures backslash-forward slash consistency when resolving plugin root paths on Windows.  
   [Link](https://github.com/anthropics/claude-code/pull/68694)

10. **[#68707] feat(bug-reporter): Add /bug Command to File GitHub Issues from the Terminal**  
    *Open — new feature*  
    Allows users to file bugs directly from within Claude Code via a `/bug` slash command, streamlining feedback.  
    [Link](https://github.com/anthropics/claude-code/pull/68707)

## Feature Request Trends

- **MCP Ecosystem Expansion** — Users want more MCP integrations (Microsoft 365 attachments [#30533], better MCP stdio troubleshooting docs [#47635]) and better handling of MCP server configuration across platforms (WSL vs Windows [#65429]).
- **UI/UX Control** — Demand for disabling live streaming [#37569] and improving rendering on Windows Terminal (mojibake fixes [#42417], enhanced keyboard handling [#68979]) and SSH sessions [#13504].
- **Cost and Quota Transparency** — After individual reports like [#65514] and [#68978], the community wants better quota accounting, rate-limit visibility, and throttling options.
- **Extensibility Tooling** — Workflow hot-reload [#68969], plugin development improvements (PRs related to `hookify` and `plugin-dev`), and a `/bug` command [#68707] all point to a desire for a more self-serviceable platform.

## Developer Pain Points

- **Windows First-Class Experience** — The most recurring pain: orphaned process locks [#42776], UTF-8 mojibake in clipboard [#42417], WSL2 scrolling regression [#42776 (scroll fix in release)], desktop app sending macOS URIs [#51701], and path separator inconsistencies [#68694]. Windows remains the roughest platform.
- **Opus 4.8 Reliability** — Multiple reports of malformed tool calls [#63604], degraded speed at high effort [#68820, #68624], and high quota consumption after reset [#68973]. Users feel the model quality regressed from 4.7.
- **MCP Configuration Cost** — Installing MCP servers on one platform (e.g., Windows Desktop) bloats token consumption on another (e.g., WSL) to nearly 10M tokens per session [#65429]. Child process leaks from MCP in skill-creator are causing hard reboots [#68933].
- **Agent Loop Overruns** — Several reports of agents making excessive tool calls, draining quota without user benefit [#68961, #65580]. The notification routing bug [#68065] adds confusion when agents complete.
- **API Gateway Compatibility** — Sending `thinking: {type: adaptive}` to non-Anthropic models behind custom `ANTHROPIC_BASE_URL` breaks those proxies [#68551] — a hard blocker for multi-provider setups.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-17

## Today's Highlights
Two Rust alpha releases landed (v0.141.0-alpha.3 and .4) with no detailed changelog. The most attention-grabbing issue remains a blocked account recovery path (#25749, 46 comments, 30 👍), and a surge of Windows-specific bugs – including Computer Use bootstrap failures and non-ASCII profile crashes – signals that cross-platform stability is a growing pain point. On the feature side, a long-running request for a `/cwd` TUI command (#12464, 21 👍) is gaining traction.

## Releases
- **rust-v0.141.0-alpha.4** — tagged as `0.141.0-alpha.4`. No release notes beyond the version bump.
- **rust-v0.141.0-alpha.3** — tagged as `0.141.0-alpha.3`. Same minimal changelog.

*GitHub: [Releases](https://github.com/openai/codex/releases)*

## Hot Issues (10 noteworthy)
1. **#25749** — *Codex requires verification of an inaccessible legacy phone number and provides no recovery path* (46 comments, 30 👍)  
   A user who can log in via Google OAuth is blocked because Codex demands a phone‑number verification step for an old number they no longer have. No alternative recovery flow exists. This is a critical auth barrier affecting real accounts.

2. **#21128** — *Desktop silently hides project conversations outside the global recent‑50 window* (27 comments, 17 👍)  
   Older conversations become invisible in the UI, making the desktop app unreliable for long‑term project memory. Users report this as a “silent data loss” UX flaw.

3. **#25865** — *App freezes when pasting JSON stack traces with escaped backslashes into composer* (9 comments, 7 👍)  
   Enterprise users are hit hard by a full‑app freeze during debugging workflows. The root cause appears to be a regex or parsing blow‑up on escaped sequences.

4. **#27287** — *Computer Use bootstrap fails on Windows: @oai/sky internal subpath is not exported* (9 comments, 9 👍)  
   The `@computer` command can’t start because of a missing export in the bundled `@oai/sky` package. This is a blocker for Windows users wanting agent‑driven desktop automation.

5. **#27506** — *[Windows] App crashes ~1s after launch when user profile path contains non‑ASCII (Korean) characters* (9 comments, 6 👍)  
   A `windows-updater.node` crash caused by `__char_to_wide: Illegal byte sequence`. Impacts users with non‑Latin‑script Windows account names.

6. **#20567** — *Windows App keeps spawning ~1000 git commands per minute NON STOP* (9 comments, 1 👍)  
   An apparent infinite loop of `git` process creation, overwhelming the system. Enterprise users affected.

7. **#12464** — *[Enhancement] /cwd command to switch working directory without restarting session* (7 comments, 21 👍)  
   Highly upvoted feature request. Currently the CLI/TUI requires a full session restart to change the working directory, which breaks long‑lived agent workflows.

8. **#18052** — *Codex ran out of room in the model's context window. Start a new thread or clear earlier history* (10 comments, 2 👍)  
   Frequent error message in long agent sessions. Users want a more graceful approach than manual thread management.

9. **#27536** — *macOS: code_sign_clone grows unbounded (62 GB+) across Codex auto‑updates* (5 comments, 0 👍)  
   An Electron temp‑folder leak that silently eats disk space. While fewer comments, the 62 GB figure is alarming for developers on constrained SSDs.

10. **#19913** — *[Enhancement] Add default parent folder setting for “Start from scratch” projects* (6 comments, 26 👍)  
    The second‑most‑upvoted feature request. Users want a single config to avoid manually navigating to the same project root every time.

*Full list: [GitHub Issues](https://github.com/openai/codex/issues)*

## Key PR Progress (10 important)
1. **#28651** — *exec-server: expose environment registry payloads*  
   Moves private serialization structs into public types so proxy services can deserialize and forward Noise registration / harness‑key payloads. Improves extensibility.

2. **#28409** — *Enforce exact managed config values*  
   Extends `requirements.toml` with exact‑value enforcement for six settings (e.g., `log_dir`, `model_catalog_json`). Warns on startup if managed values drift – important for enterprise deployments.

3. **#27713** — *Prototype workload identity federation for CLI auth* (do not merge)  
   A prototype that lets Codex CLI authenticate via workload identity (OIDC) instead of personal tokens. A step toward CI/CD‑friendly auth.

4. **#26705 / #26704 / #26703** — *TUI Plugin Sharing series (3 PRs)*  
   Polish remote plugin catalog rows, add focused coverage, and render catalog sections. Brings plugin discovery and sharing to the TUI, matching desktop features.

5. **#28219** — *Canonicalize default tool namespaces*  
   Standardizes how tool namespaces are resolved, reducing ambiguity and collisions – especially important as custom tools proliferate.

6. **#27946** — *Use input items for Responses Lite tools*  
   Switches to `additional_tools` and developer items instead of top‑level tool arrays. Keeps the API 1‑to‑1 and paves the way for forced namespacing.

7. **#28494** — *Add shared session token budgets*  
   Introduces an opt‑in token budget shared across a root thread and all its descendants. Prevents runaway agent sessions in complex workflows.

8. **#28647** — *[rmcp-client] Coordinate MCP OAuth refresh across clients*  
   Fixes a race where multiple app clients start from the same persisted refresh token and concurrently trigger provider refresh. Adds coordination to avoid broken sessions.

9. **#28034** — *Add experimental local credential broker*  
   Moves injectable local credentials behind the managed network proxy, preventing child processes from reading and exfiltrating real values. A security‑sensitive improvement.

10. **#28580** — *Support object‑valued plugin MCP manifests*  
    Fixes parsing of `plugin.json` when `mcpServers` is declared as an object (e.g., `"./mcp.json"`) instead of a string. Allows broader MCP server integration.

*Full list: [GitHub Pull Requests](https://github.com/openai/codex/pulls)*

## Feature Request Trends
- **Session‑level working directory management** – The `/cwd` command (#12464) is the most‑requested CLI feature. Users want to change directories mid‑session without losing agent state.
- **Project defaults** – Setting a default parent folder for new projects (#19913) would eliminate repetitive manual navigation.
- **SSH remote workspaces as a first‑class desktop feature** (#21509). Users want to manage remote dev environments from the Codex Desktop app, not just the CLI.
- **Detached chat windows in VS Code** (#16615). Developers want to pop out chat sessions into separate VS Code windows for multi‑monitor setups.
- **Token budget / context management** – While #18052 is a bug report, the underlying desire for smarter context‑window handling (automatic summarization, graceful degradation) appears across multiple threads.

## Developer Pain Points
1. **Windows‑specific stability regressions** – Computer Use bootstrap fails (#27287, #28121), app crashes on non‑ASCII paths (#27506), infinite git process spawning (#20567), and EBUSY errors (#28275) make Windows a second‑class citizen.
2. **Conversation visibility and data loss** – The “recent‑50” limit (#21128) and unrecoverable long threads (#25215) erode trust in the desktop app as a reliable knowledge store.
3. **Auth and account recovery** – The legacy phone‑number dead end (#25749) is the highest‑engagement issue. Users locked out of their own account have no escape hatch.
4. **Performance under load** – JSON paste freezes (#25865), large rollout JSONL files causing freezing (#22991, #26161), and long git diffs lagging the app (#13809) are recurring.
5. **Context window exhaustion** – The “ran out of room” error (#18052) remains a daily frustration for users running long agent sessions, with no built‑in solution short of manual thread splitting.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*