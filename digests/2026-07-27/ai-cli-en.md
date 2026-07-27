# AI CLI Tools Community Digest 2026-07-27

> Generated: 2026-07-27 02:32 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: Claude Code vs. OpenAI Codex
**Date**: 2026-07-27  
**Analyst**: Senior Technical Analyst, AI Developer Tools Ecosystem

---

## 1. Ecosystem Overview

The AI CLI tools landscape in mid-2026 is characterized by a stable duopoly between Anthropic's Claude Code and OpenAI's Codex, both of which are mature but grappling with reliability regressions introduced during rapid feature expansion. Neither tool shipped a new release in the past 24 hours, yet both communities logged 10+ noteworthy issues—spanning entitlement bugs, sandbox bypasses, and Windows-specific instability. The dominant theme across both ecosystems is a tension between autonomy (auto-mode, parallel execution, subagents) and safety (sandbox enforcement, hook guardrails, authentication)—a balancing act that neither tool has fully solved. Developer trust is being eroded by silent failures and opaque error paths, while feature demand clusters around cross-environment synchronization, Linux support, and hardened security defaults.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Hot Issues (this digest)** | 10 | 10 |
| **Open PRs (this digest)** | 7 | 1 (plus 9 recently closed) |
| **Releases (last 24h)** | None | None |
| **Highest-engagement issue** | #28791 — Sync CLI ↔ desktop (108 👍) | #11023 — Linux desktop app (852 👍) |
| **Critical stability issues** | 3 (#72027, #80199, #81306) | 3 (#34260, #34133, #30712) |
| **Windows-specific bugs** | 3 (#81306, #81484, #81519) | 4 (#34260, #34133, #26562, #30712) |
| **PRs merged/closed (recent)** | 0 (all open) | 9 (mostly MCP OAuth stack, TUI fixes) |

**Key observation**: Codex shows higher engagement per issue (852 👍 vs. 108 👍 for top requests) and more PR throughput (9 merged vs. 0 for Claude), but both tools are in a "maintenance stability" phase with no new releases.

---

## 3. Shared Feature Directions

The following requirements appear across **both communities**, indicating industry-wide unmet needs:

| Need | Claude Code Evidence | Codex Evidence |
|---|---|---|
| **Cross-environment sync** | #28791: CLI ↔ desktop conversation history (108 👍) | #11023: Linux desktop app (852 👍) — parity demand signals cross-platform sync needs |
| **Sandbox hardening & fail-closed** | #81421 (sandbox silently bypassed), #81423 (IPv6 firewall bypass), #81458 (hooks silently skipped) | #30712 (apply_patch broken → PowerShell fallback bypasses sandbox) |
| **Windows stability & parity** | #81306 (MSIX crash + data loss), #81484 (hang on invocation) | #34260 (WMI exhaustion), #34133 (GPU crash from Code Integrity), #26562 (missing Computer Use plugin) |
| **Silent failure detection** | #76870 (LSP returns incomplete results without error), #81458 (6,865 skipped guardrails) | #17320 (TRACE logging ignores RUST_LOG, causing undocumented disk I/O) |
| **Authentication & entitlement reliability** | #72027 (Pro subscriber blocked by entitlement sync bug) | #31573 (OAuth issuer validation failures), #34306 (safety blocks) |
| **Sandbox/security auditability** | #81458 (hooks fail silently, no user signal) | #30712 (sandbox bypass is silent by design—fallback behavior) |

**Notable**: Both communities are pushing for **managed sandbox policies** (Claude's `failIfUnavailable`, Codex's in-app update policy #35537) and **visible error paths**—a clear industry signal that agent autonomy requires comparable safety transparency.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary focus** | Security governance & plugin extensibility | Cross-platform desktop parity & MCP ecosystem integration |
| **Target user** | Enterprise/security-conscious developers | Pro users on macOS/Windows (Linux demand high but unmet) |
| **Technical approach** | Plugin-based sandbox (bash-sandbox, security-guidance plugin); auto-mode classifier for permissions | Browser-based GPU rendering (SwiftShader); sandbox via apply_patch/powershell; MCP OAuth tokens |
| **Community top issue** | CLI ↔ desktop sync (#28791) | Linux desktop app (#11023) |
| **PR velocity & direction** | Low (7 open, 0 merged); focusing on firewall, sandbox, documentation fixes | High (9 merged); MCP OAuth serialization, TUI optimization, update policy |
| **Model behavior quirks** | Auto-mode classifier misidentifies permissions (#80716) | GPT-5.6 serializes parallel calls, costing 27–45% extra (#35050) |
| **Windows maturity** | Poor (crash, data loss, 2.3s Bash overhead) | Poor to moderate (GPU crashes, WMI exhaustion, but more reported workarounds) |
| **Unique strength** | Governance plugins (web4-governance, security-guidance reviewer) | MCP OAuth serialization stack (enterprise authentication robustness) |

**Key differentiators**: Claude Code leans into **governance and audit trails** (T3 trust tensors, R6 audit workflows), while Codex prioritizes **ecosystem integration** (MCP OAuth, VS Code panel, Computer Use). Claude's plugin model is more modular for enterprise customization; Codex's merged MCP OAuth stack suggests a stronger bet on standardized authentication protocols.

---

## 5. Community Momentum & Maturity

| Factor | Claude Code | OpenAI Codex |
|---|---|---|
| **Community size (engagement level)** | Moderate (108 👍 max, 10–27 comments per issue) | High (852 👍 max, 12–187 comments per issue) |
| **PR responsiveness** | Low (7 open, 0 merged in digest period) | High (9 merged, 1 open—MCP OAuth as complete project) |
| **Issue resolution velocity** | Stagnant (critical bugs like #72027 and #80716 unresolved) | Mixed (GPU crash #34133 still open, but MCP OAuth stack fully merged) |
| **Windows community pain** | High: 3 of 10 hot issues are Windows-specific | Very high: 4 of 10 hot issues are Windows-specific |
| **Maturity signal** | Late-stage: regressions in auto-mode, sandbox, and billing suggest technical debt | Growth-stage: high feature demand (Linux), active MCP infrastructure buildout |
| **Open source contribution** | Low (7 PRs, all from maintainers or plugins) | Moderate (community-reported issues, maintainer-driven PRs) |

**Analysis**: Codex has **2–8× more community engagement** per issue and higher PR throughput, but also has more severe unresolved stability problems (GPU crash, WMI exhaustion). Claude Code's community is smaller but more enterprise-oriented (governance plugins, sandbox hardening). Both tools show signs of **mature-product fatigue**—regressions in core features while adding new capabilities.

---

## 6. Trend Signals

1. **The silent failure epidemic is a industry-wide liability**. Both tools have bugs where critical guardrails, sandboxes, or logging silently stop working (Claude's hooks, LSP; Codex's TRACE logging, sandbox bypass). For developers, this means **no agent tool should trust its own error reporting**—implement external health-check probes and audit trails.

2. **Windows continues to be a second-class platform for AI CLIs**, despite 30%+ developer market share. GPU isolation (Code Integrity blocking SwiftShader), WMI resource exhaustion, and sandbox path injection are fundamental OS-level issues that neither vendor has solved. Developers on Windows should expect 3–5× more crashes and plan for sandbox bypasses.

3. **Governance is displacing autonomy as the primary community concern**. Claude's web4-governance plugin (T3 trust tensors, R6 audit) and Codex's MCP OAuth serialization stack (#30295–#30416) signal that the market is moving from "what can the agent do?" to "how do we prove what the agent did?"—a maturation essential for regulated industries.

4. **Model-behavior costs are becoming visible to users**. Codex #35050 (GPT-5.6 serializing parallel calls, costing 27–45% extra) and Claude's auto-mode classifier loops (#80716) show that **LLM orchestration inefficiencies directly impact wallet and time budgets**. Developers should monitor per-call batching behavior and consider explicit parallelization directives in prompts.

5. **Cross-environment synchronization is the next UX frontier**. Both top community requests (Claude #28791 CLI↔desktop sync, Codex #11023 Linux desktop) point to a future where developers expect **session continuity across CLI, IDE, and desktop app**—a capability neither tool delivers reliably today. For developers choosing a tool, **session portability should be a near-term roadmap criterion**.

6. **Managed update policies and quota controls are enterprise table-stakes**. Codex's in-app update policy (#35537) and Claude's usage cap bugs (#80199) both reflect growing enterprise demand for **administrative control over update timing and resource consumption**. Tools that cannot offer locked-down update channels will face adoption barriers in regulated environments.

---

*Report prepared for technical decision-makers evaluating AI CLI tooling for production workflows. Data sourced from public community digests dated 2026-07-27.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
**Data Source:** github.com/anthropics/skills (official repository)  
**Snapshot Date:** 2026-07-27  

---

## 1. Top Skills Ranking (Most-Discussed Pull Requests)

The following PRs attracted the highest community engagement (sorted by comment count). All remain **open** as of the snapshot date.

### 🥇 `fix(skill-creator): run_eval.py always reports 0% recall` (PR [#1298](https://github.com/anthropics/skills/pull/1298))  
**Functionality:** Fixes the `run_eval.py` script used to evaluate skill description quality. The bug causes every skill to report `recall=0%`, making the description-optimization loop optimize against noise. The PR addresses Windows stream reading, trigger detection, and parallel worker issues.  
**Discussion highlights:** Multiple independent reproductions confirmed the bug. The fix touches the core tooling for skill development.  
**Status:** Open (last updated 2026-06-23)

### 🥈 `Add document-typography skill` (PR [#514](https://github.com/anthropics/skills/pull/514))  
**Functionality:** Prevents common typographic problems in AI-generated documents: orphan word wrap, widow paragraphs, and numbering misalignment. Targets the visual quality of Claude’s output.  
**Discussion highlights:** Users noted these issues are pervasive but rarely requested explicitly—the skill fills a gap in output quality control.  
**Status:** Open (last updated 2026-03-13)

### 🥉 `fix(pdf): correct case-sensitive file references in SKILL.md` (PR [#538](https://github.com/anthropics/skills/pull/538))  
**Functionality:** Fixes 8 case-sensitivity mismatches in the PDF skill’s documentation (e.g., `REFERENCE.md` → `reference.md`). Breaks on case-sensitive file systems (Linux/macOS).  
**Discussion highlights:** A small but high-impact fix; demonstrates community attention to cross-platform correctness.  
**Status:** Open (last updated 2026-04-29)

### 4. `Add ODT skill — OpenDocument text creation and template filling` (PR [#486](https://github.com/anthropics/skills/pull/486))  
**Functionality:** Enables Claude to create, fill, read, and convert OpenDocument Format files (.odt, .ods). Covers LibreOffice workflows and ISO-standard document formats.  
**Discussion highlights:** Demand for open-source document interoperability; complements the existing DOCX skill.  
**Status:** Open (last updated 2026-04-14)

### 5. `Improve frontend-design skill clarity and actionability` (PR [#210](https://github.com/anthropics/skills/pull/210))  
**Functionality:** Rewrites the frontend-design skill to ensure every instruction is executable within a single conversation, with specific, steerable guidance.  
**Discussion highlights:** Focus on making skills action-oriented rather than educational; aligns with community critique of overly verbose skill designs.  
**Status:** Open (last updated 2026-03-07)

### 6. `Add skill-quality-analyzer and skill-security-analyzer` (PR [#83](https://github.com/anthropics/skills/pull/83))  
**Functionality:** Two meta-skills: **skill-quality-analyzer** evaluates skills across Structure & Documentation, Correctness, Completeness, Robustness, and Consistency; **skill-security-analyzer** audits skills for security vulnerabilities (command injection, path traversal, etc.).  
**Discussion highlights:** Meta-analysis tools are highly anticipated—they enable systematic quality assurance of the growing skill ecosystem.  
**Status:** Open (last updated 2026-01-07)

### 7. `feat(skills): add self-audit — mechanical verification + four-dimension reasoning quality gate` (PR [#1367](https://github.com/anthropics/skills/pull/1367))  
**Functionality:** A universal skill that audits AI output before delivery: verifies claimed output files exist, then performs a four-dimension reasoning audit in damage-severity order.  
**Discussion highlights:** Positions as a “final quality gate” for any task; discussion included integration with existing improvement loops.  
**Status:** Open (last updated 2026-07-02)

---

## 2. Community Demand Trends (from Issues)

The top issues (by comment count) reveal the following high-demand directions:

| Issue | Topic | Comments | Key Demand |
|-------|-------|----------|------------|
| [#492](https://github.com/anthropics/skills/issues/492) | Security: namespace trust boundary abuse | 43 | Community skills under `anthropic/` namespace are misleading; need clear provenance and permission scoping |
| [#228](https://github.com/anthropics/skills/issues/228) | Org-wide skill sharing | 16 | Direct sharing mechanisms (shared library, links) instead of manual file transfer |
| [#556](https://github.com/anthropics/skills/issues/556) | `run_eval.py` 0% trigger rate | 12 | **Bug fixing the skill-creator evaluation pipeline** is the community’s top operational pain point |
| [#62](https://github.com/anthropics/skills/issues/62) | Skills disappeared after rename | 10 | Need better skill storage and sync stability |
| [#1329](https://github.com/anthropics/skills/issues/1329) | `compact-memory` skill proposal | 9 | Symbolic notation for compact agent state—reducing context consumption |
| [#202](https://github.com/anthropics/skills/issues/202) | skill-creator should be updated to best practice | 8 | Existing skill is too educational, not actionable; request optimization |
| [#412](https://github.com/anthropics/skills/issues/412) | Agent governance skill proposal | 6 | Safety patterns, policy enforcement, threat detection for agent systems |
| [#189](https://github.com/anthropics/skills/issues/189) | Duplicate skills from overlapping plugins | 6 | Need deduplication and cleaner skill plugin boundaries |

**Summary of trends:**  
- **Skill development tooling** dominates: the `skill-creator` pipeline and its evaluation scripts are the most critical infrastructure the community wants fixed.  
- **Security & trust** is a rising concern: issues around namespace abuse (PR #492) and permission handling show the ecosystem needs hardening as it scales.  
- **Enterprise & collaboration** features (org sharing, deduplication) point to growing professional adoption.  
- **Novel skill categories** receiving strong community signals: document typography, ODT/OpenDocument, color expertise, game development (Pyxel), and memory-compaction for long-running agents.

---

## 3. High-Potential Pending Skills

The following PRs have active discussion and appear close to landing:

- **PR [#1298](https://github.com/anthropics/skills/pull/1298)** – The `run_eval.py` fix is the most commented PR. It directly addresses the #1 bug (#556) and unblocks all skill optimization workflows. Likely to merge quickly once reviewed.  
- **PR [#514](https://github.com/anthropics/skills/pull/514)** – `document-typography` fills a clear user-facing quality gap. Low risk, high value.  
- **PR [#1367](https://github.com/anthropics/skills/pull/1367)** – `self-audit` skill has a complete implementation and a companion issue ([#1385](https://github.com/anthropics/skills/issues/1385)) proposing a reasoning quality gate pipeline.  
- **PR [#1302](https://github.com/anthropics/skills/pull/1302)** – `color-expert` (by meodai) offers deep color-science knowledge (ISCC-NBS, Munsell, OKLCH, etc.)—a rare specialized domain skill with strong implementation.  
- **PR [#525](https://github.com/anthropics/skills/pull/525)** – `pyxel` skill for retro game development with Pyxel MCP server. Author is the project maintainer, so integration is well-informed.  
- **PR [#83](https://github.com/anthropics/skills/pull/83)** – The meta-analysis skills are the only quality-assurance tools in the ecosystem; they would immediately improve maintainer and community confidence in skill submissions.

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for robust, self-improving skill creation tooling**—fixing `run_eval.py`’s 0% recall bug, adding dedicated quality-analysis and security-audit skills, and shifting skill documentation from human-educational to machine-actionable format—while the skill proposals themselves lean toward document formatting, open interoperability, and agent governance.

---

# Claude Code Community Digest — 2026-07-27

## Today's Highlights

The community is grappling with a cluster of regressions and reliability issues — a bug in the auto-mode classifier forces repeated manual approvals (#80716), Pro subscribers are blocked by an entitlement sync bug (#72027), and a VS Code extension regression hides externally created session transcripts (#71500). No new releases landed in the last 24 hours, but seven open pull requests address firewall bypasses, sandbox hardening, and documentation fixes.

## Releases

No new releases in the last 24 hours. The latest stable version remains as previously reported.

## Hot Issues (10 noteworthy)

1. **[#28791 — Sync conversation history between CLI and Claude Code desktop app](https://github.com/anthropics/claude-code/issues/28791)**  
   *27 comments, 108 👍*  
   The most upvoted open feature request. Users want seamless continuity between CLI sessions and the desktop app. Conversations started in one environment are invisible in the other, breaking workflows that switch between the two.

2. **[#80716 — Auto-mode classifier incorrectly detects permission mode change in plan mode](https://github.com/anthropics/claude-code/issues/80716)**  
   *7 comments, 15 👍*  
   In plan mode, read-only tool calls trigger the auto-mode classifier to repeatedly request manual approval, even though no mode change occurred. This creates a frustrating loop that kills productivity in planning sessions.

3. **[#72027 — Individual Pro subscriber blocked: “organization disabled” → “Max or Pro required”](https://github.com/anthropics/claude-code/issues/72027)**  
   *6 comments*  
   A critical entitlement sync bug prevents paying Pro users from accessing Claude Code at all. The system first claims the organization is disabled, then demands a higher plan. No workaround has been confirmed.

4. **[#80199 — Max X5 Usage Instantly Reaches 100% After Software Update](https://github.com/anthropics/claude-code/issues/80199)**  
   *5 comments*  
   Max-tier users report that usage caps hit 100% immediately after a software update, with no prior warning or rollback option. The issue suggests a reset of usage tracking or a misconfiguration in the update process.

5. **[#71500 — VS Code extension: sessions sidebar omits externally-created session transcripts](https://github.com/anthropics/claude-code/issues/71500)**  
   *4 comments*  
   Regression in 2.1.187–2.1.191. Session transcript files created or modified outside the VS Code extension (e.g., by the CLI) no longer appear in the sidebar. Breaks multi-environment workflows.

6. **[#76870 — LSP tool returns silently incomplete results (cold-index race + stale file state)](https://github.com/anthropics/claude-code/issues/76870)**  
   *3 comments*  
   Two distinct bugs cause the built-in LSP tool to return truncated symbol results without any error. Cold-index race (first query before language server finishes indexing) and stale file state both lead to unreliable code navigation.

7. **[#81306 — Windows Desktop crash wedged the MSIX package; recovery destroyed local app data](https://github.com/anthropics/claude-code/issues/81306)**  
   *3 comments*  
   A crash in the native Windows binary (Claude Code 2.1.219) left the MSIX package unrecoverable. Manual removal of the package also deleted local app data including code-tab group assignments and crash dumps — a data-loss scenario.

8. **[#81458 — Hook launch failures (exit 127) are silent and non-blocking](https://github.com/anthropics/claude-code/issues/81458)**  
   *2 comments*  
   When a hook command cannot be launched, Claude Code silently logs a non-blocking error and lets the tool call proceed. One session recorded 6,865 skipped guardrail invocations with zero user-visible signal.

9. **[#78529 — DNS resolution fails when /etc/resolv.conf has trailing inline comments](https://github.com/anthropics/claude-code/issues/78529)**  
   *1 comment, 2 👍*  
   The Bun runtime fails to parse `nameserver` lines that contain inline comments (e.g., `nameserver 8.8.8.8 # my dns`), producing `getaddrinfo ETIMEOUT`. This affects many Linux configurations.

10. **[#64479 — Edit tool fails on mixed literal/escape Unicode in multi-line old_string](https://github.com/anthropics/claude-code/issues/64479)**  
    *5 comments*  
    The Edit tool cannot handle `old_string` text that mixes literal Unicode codepoints with `\uXXXX` escape sequences across multiple lines. The fallback swap attempt also fails, leaving the file unchanged without a clear error.

## Key PR Progress (7 open pull requests)

1. **[#81500 — Fix 404 walkthrough links in the AWS gateway example](https://github.com/anthropics/claude-code/pull/81500)**  
   Seven references to the AWS deployment walkthrough point to a URL that returns 404. This PR updates all links in README and setup scripts to the correct path.

2. **[#20448 — Add web4-governance plugin for AI governance with R6 workflow](https://github.com/anthropics/claude-code/pull/20448)**  
   A new plugin introducing T3 trust tensors, entity witnessing, and R6 audit trails for AI governance. Aims to provide cryptographic provenance for agent actions.

3. **[#38167 — Use authenticated request to GitHub API in devcontainer firewall script](https://github.com/anthropics/claude-code/pull/38167)**  
   The devcontainer's firewall init script hits GitHub API rate limits in shared IP environments. This PR passes `GH_TOKEN` to authorize requests, avoiding denial-of-service during setup.

4. **[#81426 — Support Windows venv layout for security-guidance agentic reviewer](https://github.com/anthropics/claude-code/pull/81426)**  
   The agentic commit reviewer in the security-guidance plugin skipped entirely on Windows. This PR adapts the bootstrap hook to detect Windows virtual environment paths, making the reviewer available on win32.

5. **[#68693 — Make duplicate label additive, don't replace existing labels](https://github.com/anthropics/claude-code/pull/68693)**  
   The `closeIssueAsDuplicate` script was wiping all existing labels (platform/area/priority) when marking an issue as duplicate. This PR changes the API call to add the `duplicate` label without replacing others.

6. **[#81423 — Block IPv6 egress to close firewall allowlist bypass](https://github.com/anthropics/claude-code/pull/81423)**  
   The devcontainer firewall configured `iptables` for IPv4 but left IPv6 unrestricted. On dual-stack Docker networks, all IPv6 traffic bypasses the allowlist entirely. This PR adds `ip6tables` rules to close the gap.

7. **[#81421 — Make bash-sandbox example fail closed when sandbox unavailable](https://github.com/anthropics/claude-code/pull/81421)**  
   The `settings-bash-sandbox.json` example omits `failIfUnavailable`. When the sandbox cannot initialize, Claude Code silently runs commands outside the sandbox. This PR adds the setting to fail closed as documented.

## Feature Request Trends

The most-requested feature directions, distilled from all open issues this week:

- **Cross-environment sync** — #28791 (CLI ↔ desktop conversation history) and #80798 (promote/demote subagents to sessions) point to a strong desire for seamless continuity across CLI, desktop, VS Code, and subagent workspaces.
- **Localization and accessibility** — #69078 (Russian UI) and similar requests for other languages show growing demand for non-English interfaces.
- **Sandbox and security hardening** — Multiple issues and PRs (#81421, #81423, #81458) reflect community pressure for reliable sandbox enforcement and visible guardrail execution.
- **Multi-session safety** — #74386 (worktree cleanup discarding work) and #81505 (model modifying wrong worktree) highlight the need for better isolation and liveness signals between concurrent sessions.

## Developer Pain Points

Recurring frustrations this week:

- **Entitlement and usage tracking bugs** — #72027 (Pro blocked), #80199 (usage instantly 100%), and #70758 (session limits depleting faster) erode trust in the billing system.
- **Silent failures** — #81458 (hooks silently skipped), #76870 (LSP returns incomplete results without error), and #78529 (DNS failure with misleading ETIMEOUT) make debugging opaque.
- **VS Code extension regressions** — #71500 (sidebar omits external sessions) and #80087 (false positive "CLI not on PATH") disrupt integrated workflows.
- **Windows-specific instability** — #81306 (crash wedges MSIX, data loss), #81484 (hang on any invocation), and #81519 (2.3s overhead per Bash tool call) continue to plague Windows users.
- **Auto-mode classifier unpredictability** — #80716 (repeated manual approval in plan mode) shows the classifier still misidentifies tool permissions, breaking autonomy.
- **Unicode and edit tool fragility** — #64479 (mixed literal/escape Unicode in multi-line edits) demonstrates edge cases where file modification can silently fail.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# Codex Community Digest — 2026-07-27

## Today's Highlights
No new releases landed in the last 24 hours, but the community continues to push for a **Linux desktop app** (#11023) with overwhelming support (852 👍, 187 comments) — the highest-engagement issue in the repository. Windows stability remains the dominant theme, with multiple high-traffic bugs around **GPU process crashes** tied to code integrity blocking bundled Vulkan shaders, and an **unbounded process-cleanup loop** that can exhaust the WMI provider on Windows. On the PR side, OpenAI merged a large **MCP OAuth serialization stack** and a batch of **TUI session improvements**; a new policy for **managed in-app updates** was also landed.

## Releases
*None in the last 24 hours.*

---

## Hot Issues (10 noteworthy)

1. **[#11023 — Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)** — The community’s top feature request. 852 👍 and 187 comments. Many users cite macOS performance regressions (issue #10432) as a reason they need a Linux-native app. Clear demand for cross-platform parity.

2. **[#34260 — Windows Desktop: unbounded taskkill.exe/conhost.exe cleanup storm exhausts WMI](https://github.com/openai/codex/issues/34260)** — A severe Windows stability bug. Codex enters a loop spawning hundreds of `taskkill` processes, each with a `conhost.exe` child, exhausting WMI quotas and making the machine unusable. 32 comments, 10 👍. High-impact for Windows Pro users.

3. **[#17320 — Excessive SQLite WAL writes during streaming due to TRACE logs ignoring RUST_LOG](https://github.com/openai/codex/issues/17320)** — A persistent performance bug across platforms. TRACE-level logging is hard-coded rather than respecting `RUST_LOG`, causing heavy SQLite write-ahead log writes during streaming. 27 comments, 39 👍. Affects VSCode/Codium on Linux.

4. **[#31573 — OAuth authentication fails at issuer validation](https://github.com/openai/codex/issues/31573)** — CLI users hitting authentication roadblocks with OAuth issuer validation. 24 comments, 55 👍. Free-tier users are especially affected.

5. **[#24948 — Codex session logs grow to 700MB–2GB](https://github.com/openai/codex/issues/24948)** — Disk usage explosion from compaction history and raw tool output. 23 comments. Pro users with long sessions are hit hardest. Updated today — still open.

6. **[#34133 — Page.captureScreenshot crashes GPU process after Code Integrity Event 3033 rejects bundled vk_swiftshader.dll](https://github.com/openai/codex/issues/34133)** — Windows GPU crash triggered by the in-app browser taking screenshots. Code Integrity blocks the bundled SwiftShader DLL, cascading into crashes. 20 comments. High visibility for Windows + Arc/NVIDIA GPU users.

7. **[#26562 — Computer Use plugin unavailable in Codex Desktop on Windows](https://github.com/openai/codex/issues/26562)** — A major feature gap for Windows Pro subscribers. Computer Use (remote desktop actions) simply doesn’t appear. 18 comments, 3 👍.

8. **[#30712 — Windows app injects split writable roots, causing apply_patch to fail](https://github.com/openai/codex/issues/30712)** — The sandbox’s safe edit path (`apply_patch`) is broken on Windows, forcing agents to fall back to writing files via PowerShell (bypassing sandbox). 14 comments, 13 👍. Serious security concern.

9. **[#35050 — GPT-5.6 often serializes independent Code Mode calls; explicit batching reduced weighted usage by 27–45%](https://github.com/openai/codex/issues/35050)** — A model-behavior bug report with hard data. The user shows that GPT-5.6 serializes calls that should be parallel, and manually batching reduced API weighted usage by 27–45%. 13 comments, 16 👍. Potentially costs users significant credits.

10. **[#32530 — VS Code Codex panel intermittently stuck loading on Linux](https://github.com/openai/codex/issues/32530)** — Local webview assets fail with `net::ERR_FAILED` on Ubuntu 26.04. 12 comments, 12 👍. Reproducible and blocking for Linux IDE users.

---

## Key PR Progress (10 important changes)

1. **[#35537 — Add managed policy for in-app updates](https://github.com/openai/codex/pull/35537)** *(Closed)* — New functionality for administrators to disable in-app updates via `requirements.toml`. Exposed through `configRequirements/read`. Important for enterprise/gov deployments.

2. **[#35530 — Track model and personality in world state](https://github.com/openai/codex/pull/35530)** *(Closed)* — Persists model and personality selections into world-state snapshots. Generates model-switch and personality instructions during replay. Foundational for smarter session continuity.

3. **[#35525 — Skip inactive TUI threads without pending user interaction](https://github.com/openai/codex/pull/35525)** *(Closed)* — Performance optimization for the TUI: only collects buffered requests from threads that have pending user input. Reduces noise on side-thread switches.

4. **[#35524 — Preserve terminal turn errors in replayed history](https://github.com/openai/codex/pull/35524)** *(Closed)* — Fixes a bug where errors embedded in turn completion events were lost during history replay. Now correctly shows model-overload errors in the TUI trace.

5. **[#35523 — Shut down the in-process outbound router explicitly](https://github.com/openai/codex/pull/35523)** *(Closed)* — Resolves a shutdown livelock where detached processor work kept the outbound router alive. Cleaner teardown for the app-server.

6. **[#30295 — Serialize MCP OAuth login and logout](https://github.com/openai/codex/pull/30295)** *(Closed, stacked)* — Part of the large MCP OAuth serialization stack. Ensures concurrent login/logout operations are properly serialized to avoid race conditions.

7. **[#30296 — Report MCP OAuth Auto store drift](https://github.com/openai/codex/pull/30296)** *(Closed, stacked)* — Adds drift detection for shared OAuth token stores, enabling recovery when state diverges.

8. **[#30294 — Route MCP OAuth recovery through Codex](https://github.com/openai/codex/pull/30294)** *(Closed, stacked)* — All MCP OAuth token refresh/recovery now flows through a centralized Codex handler rather than per-provider logic.

9. **[#30416 — Serialize authoritative MCP OAuth refresh transactions](https://github.com/openai/codex/pull/30416)** *(Closed, stacked)* — The final layer of the MCP OAuth stack. Ensures refresh transactions are atomic and serialized, preventing double-refresh and token invalidation.

10. **[#30985 — Let idle auto-attached threads unload](https://github.com/openai/codex/pull/30985)** *(Open)* — Distinguishes implicit observer attachments from explicit retaining subscriptions. Idle core-created threads now reach the 30-minute unload lifecycle, reducing memory pressure. Still under review.

---

## Feature Request Trends

The most-requested feature directions across the issue tracker are:

- **Linux desktop app** (#11023, 852 👍) — By far the most demanded feature, driven by macOS performance issues and enterprise Linux adoption.
- **Windows feature parity** — Multiple gaps persist: missing Computer Use plugin (#26562), broken sandbox `apply_patch` (#30712), and blocked GPU features (#34133, #27828). Windows Pro users feel they are second-class.
- **Restored/adjustable context windows** (#34619, 6 👍) — Users want GPT-5.6 Sol’s 372k context window back, or at least an opt-in toggle to retain long-context capabilities.
- **Subagents and sessions disk usage controls** (#24948, #34061) — Demand for limits on session log growth and subagent disk consumption. Users want configurable retention policies.
- **MCP OAuth reliability** (#31573, #30295 stack) — Authentication robustness is a recurring request, particularly around issuer validation and token refresh.

---

## Developer Pain Points

Several recurring frustrations emerge from the data:

1. **Windows GPU stability crisis** — Multiple issues (#34133, #27828, #35352, #32094) all trace to the same root cause: bundled SwiftShader DLLs are rejected by Windows Code Integrity (Event 3033), crashing the GPU process and making the app unlaunchable. This is the single highest-impact stability issue.

2. **Excessive disk I/O** — Two separate issues (#17320, #35092) report hard-coded TRACE-level logging that ignores `RUST_LOG`, causing high-frequency SQLite WAL writes even when logging is supposedly disabled. The community has pointed out the fix but it remains unaddressed.

3. **Windows WMI exhaustion** (#34260) — The unbounded `taskkill` loop is a critical resource-exhaustion bug that can effectively DOS a developer’s machine. No workaround documented.

4. **Sandbox bypass on Windows** (#30712) — When `apply_patch` fails due to incorrect writable root injection, agents automatically fall back to writing files via PowerShell, completely bypassing the sandbox. This undermines the core security model for Windows users.

5. **Authentication friction** (#31573, #34306, #31786) — OAuth issuer validation failures, “content can’t be shown” safety blocks, and remote-control pairing issues create significant onboarding friction, especially for free-tier and CLI-first users.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*