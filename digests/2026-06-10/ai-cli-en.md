# AI CLI Tools Community Digest 2026-06-10

> Generated: 2026-06-10 02:58 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date:** 2026-06-10 | **Data sources:** Community digest summaries for Claude Code (Anthropic) and OpenAI Codex

## 1. Ecosystem Overview

The AI CLI tools landscape for June 2026 is characterized by rapid model upgrades and persistent platform stability challenges. Anthropic released Claude Fable 5 (Mythos-class), a major leap in capability, while OpenAI Codex shipped web search from code mode in its stable Rust-based CLI. Both ecosystems are grappling with fragile Windows support, session data loss after updates, and growing user demands for cross-platform parity. Community engagement remains high, with hundreds of upvotes on key feature requests and dozens of comments per hot issue, indicating a mature but still unsettled user base. The parallel emergence of similar pain points across tools suggests that reliability and platform support are now the top priorities for developers.

## 2. Activity Comparison

| Metric | Claude Code (v2.1.170) | OpenAI Codex (rust-v0.139.0) |
|--------|------------------------|------------------------------|
| **Hot issues highlighted** | 10 (range: 2–406 upvotes) | 10 (range: 4–125 upvotes) |
| **Key PRs highlighted** | 9 | 10 |
| **Stable release today** | ✅ v2.1.170 (Fable 5) | ✅ rust-v0.139.0 (web search) |
| **Alpha/pre-release builds** | Not reported | rust-v0.140.0-alpha.2, two α builds for v0.139 |
| **Top issue engagement** | #65697 (Linux desktop) – 406 👍, 31 comments | #2909 (multi-root workspace) – 125 👍, oldest open |
| **Critical bug with community heat** | #42776 (Windows relaunch lock) – 86 comments | #24391 (Windows sandbox spawn failure) – 44 comments, 25 👍 |

**Observations:** Both tools have roughly similar issue and PR volumes in today’s digest. Claude Code shows higher peak upvotes (406 vs. 125), indicating a very vocal segment demanding Linux desktop support. Codex has a more diverse set of alpha builds, suggesting faster iteration cadence on the Rust CLI.

## 3. Shared Feature Directions

Requirements that appear across both communities:

| Requirement | Claude Code | OpenAI Codex |
|-------------|-------------|--------------|
| **Linux desktop / native app** | #65697 – 406 👍, most requested | Not explicit, but multi-root workspace (#2909) is the top VS Code ask |
| **Windows reliability** | #42776 orphaned lock, #66778 path virtualization, #66775 data loss | #24391 sandbox spawn fail, #27278 elevated sandbox blocks node_repl |
| **Session / chat history persistence** | #66760 unrecoverable session, #66754 request for `/history` | #20741 / #23979 chat histories missing after update, #21128 capped recent list |
| **Cost / usage transparency** | #66762 ultracode cost visibility, #59634 rate-limit-aware scheduling | #19585 Pro limit depleting unusually fast, #27242 compaction burning tokens |
| **Model selection flexibility** | #66757 – alternative model support, Fable 5 locked to Opus | Not explicitly raised, but community context compaction issues suggest need for more granular control |
| **Remote / headless operation** | #29006 – 94 👍 for remote control sessions | Not directly, but streaming file APIs (#27190) and MCP improvements support programmatic use |

Notably, **session persistence** and **Windows stability** are the two most pressing cross-tool pain points, affecting paid users and blocking adoption on a major platform.

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|-----------|-------------|--------------|
| **Model behaviour focus** | Heavy: multiple issues on Opus skepticism, self-favoring bias, contrarian outputs (#66273, #64991) | Minimal: no equivalent model-behavior issues reported |
| **Release strategy** | Monolithic – one stable release with model upgrade; no alpha/beta channels mentioned | Dual-track – stable rust-v0.139.0 alongside rapid alpha builds (v0.139 alpha 2/3, v0.140 alpha) |
| **Plugin / hook ecosystem** | Rich: PR review toolkit, security-guidance plugin, mid-session hook enforcement (#65953), agent identification (#66761) | Light: MCP connectivity improvements, but no dedicated plugin marketplace discussed |
| **Target user profile** | Power users in long interactive sessions (debatable model calibration) and CI/CD workflows (remote control ask) | VS Code-first developers (multi-root workspace top request), sandbox-heavy usage on Windows |
| **Technical architecture pain points** | Shell scripting `set -e` bugs causing silent failures (#66573, #66416), unique session corruption via content block type "fallback" | Sandbox architecture regressions (spawn, elevation), SQLite state handling after updates, context compaction enums |

**Summary:** Claude Code excels in depth of agent/plugin capabilities but struggles with model behavior quirks and Linux desktop absence. Codex prioritises stable CLI + VS Code integration and is iterating faster on infrastructure (PathUri, streaming APIs) but suffers from update-induced data loss and sandbox fragility.

## 5. Community Momentum & Maturity

- **Claude Code** has a highly engaged community, evidenced by 406 upvotes on a single feature request and sustained heated threads on Windows bugs (86 comments on #42776). The recent Fable 5 release likely drives new interest, but unresolved Linux desktop gap may cap growth. Issues around model skepticism and session unrecoverability suggest power users are pushing the tool to its limits, indicating strong adoption but also high expectations.

- **OpenAI Codex** shows more moderate upvote peaks (125) but a broader set of open alpha builds, signalling ongoing rapid development. The concentration of issues on chat history disappearance (multiple issues across macOS/Windows) points to a regression-prone update process. The community appears smaller but actively reports regressions, which can be a sign of a fast-moving codebase. The “Thinking” stuck state (#24287) and usage limit depletion (#19585) are classic maturity pains.

**Maturity assessment:** Both tools are past early adoption but not yet in a reliability plateau. Claude Code may have more overall users (higher engagement numbers), while Codex is iterating more aggressively on infrastructure (streaming, MCP, PathUri). Neither has achieved platform stability on Windows.

## 6. Trend Signals

From cross-tool community feedback, several industry-wide signals emerge:

1. **Reliability trumps new features** – Users are consistently most vocal about session data loss, stuck states, and platform crashes. The “wow factor” of new models (Fable 5) is immediately shadowed by basic UX failures.

2. **Cross-platform parity is non-negotiable** – Linux and Windows users will abandon or workaround tools that ignore their platform. The 406 upvotes for a Linux Claude desktop are a clear demand signal for any AI CLI vendor.

3. **Cost observability is a growing pain point** – As multi-agent workflows and ultracode modes become common, users demand transparent, predictable consumption. Both communities report hidden charges and rapid limit depletion.

4. **Agent orchestration needs better tooling** – Requests for remote control (Claude #29006), agent ID propagation (#66761), and streaming file APIs (Codex #27190) indicate that users are building complex pipelines and need richer programmatic interfaces.

5. **Model behaviour customization is coming** – The Claude Code thread on alternative model support (#66757) and the deep reports on model bias (#66273, #64991) suggest that developers want to choose models per task and tune calibration, not just accept a fixed behaviour.

6. **Plugin ecosystems are a double-edged sword** – While Claude Code’s plugin system enables powerful workflows, it also introduces maintenance overhead (manifest sync, shell-script correctness). The trend is toward more structured, less fragile plugin interfaces (similar to MCP improvements in Codex).

**Bottom line for decision-makers:** When evaluating AI CLI tools for your team, prioritise platform compatibility (especially if using Windows or Linux) and session reliability over raw model capability. Both vendors are actively addressing these gaps, but today’s digests show neither has fully solved them. For teams needing rich agent orchestration, Claude Code’s ecosystem is more mature; for VS Code-centric workflows and frequent updates, Codex’s rapid alpha cadence may offer faster bug fixes (but also introduces regression risk).

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

**Data snapshot:** github.com/anthropics/skills · 2026-06-10

---

## 1. Top Skills Ranking

The following Pull Requests attracted the most community discussion. Note: all are **open** unless stated otherwise.

### #514 – Document Typography Skill
- **Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents.
- **Discussion highlights:** Addresses a universal pain point—typographic flaws in Claude-generated docs. The conversation focuses on scope boundaries (should it also handle LaTeX?).
- **Status:** Open  
  [PR #514](https://github.com/anthropics/skills/pull/514)

### #486 – ODT Skill (OpenDocument text creation, template filling, ODT→HTML)
- **Functionality:** Full-featured skill for creating, filling, reading, and converting OpenDocument Format files (.odt, .ods). Triggers on mentions of “ODT”, “ODS”, “LibreOffice document”, etc.
- **Discussion highlights:** Strong interest from LibreOffice and open-source document workflows. Reviewers debated whether to merge with the existing DOCX skill or keep separate.
- **Status:** Open  
  [PR #486](https://github.com/anthropics/skills/pull/486)

### #210 – Improve Frontend-Design Skill Clarity and Actionability
- **Functionality:** Revises the frontend-design skill to ensure every instruction is actionable within a single Claude conversation, with specific guidance to steer behavior without over‑promising.
- **Discussion highlights:** High engagement around what constitutes a "good" skill description. Community members shared concrete examples of where the old skill failed.
- **Status:** Open  
  [PR #210](https://github.com/anthropics/skills/pull/210)

### #83 – Skill-Quality-Analyzer and Skill-Security-Analyzer
- **Functionality:** Two meta-skills: one evaluates Skills across structure, documentation, examples, resources, and validation; the other checks for security risks (injection, secret exposure, privilege escalation).
- **Discussion highlights:** Broad consensus that the ecosystem needs quality gates. Debate centered on false positives from the security analyzer and whether these should become required CI checks.
- **Status:** Open  
  [PR #83](https://github.com/anthropics/skills/pull/83)

### #538, #539, #541 – Lubrsy706 Fix Trio (PDF, skill-creator, DOCX)
- **Functionality:**  
  - #538: Fixes 8 case-sensitive file reference mismatches in the PDF skill (breaks on Linux).  
  - #539: Adds YAML pre-validation to detect unquoted description fields containing colons.  
  - #541: Prevents DOCX corruption by avoiding `w:id` collision between tracked changes and existing bookmarks.
- **Discussion highlights:** These small, targeted fixes generated high comment counts because they affect every skill author and document user. The YAML validator was especially debated for edge cases.
- **Status:** All open  
  [#538](https://github.com/anthropics/skills/pull/538) · [#539](https://github.com/anthropics/skills/pull/539) · [#541](https://github.com/anthropics/skills/pull/541)

### #181 – SAP-RPT-1-OSS Predictor Skill
- **Functionality:** Wraps SAP’s open-source tabular foundation model for predictive analytics on business data, guiding Claude on model invocation, feature engineering, and result interpretation.
- **Discussion highlights:** The first enterprise ML model integration proposed for the Skills ecosystem. Discussions covered version pinning, licensing, and whether the skill should be split into predictor + data-prep.
- **Status:** Open  
  [PR #181](https://github.com/anthropics/skills/pull/181)

### #1140 – Agent-Creator Meta-Skill and Multi-Tool Fix
- **Functionality:** Adds an `agent-creator` meta-skill for task-specific agent sets, fixes `evaluation.py` to handle parallel tool calls correctly, and adds Windows support for `recalc.py`.
- **Discussion highlights:** A “meta-skill for building skills” that generated excitement. The multi-tool evaluation fix resolved a long-standing bug in the test harness.
- **Status:** Open  
  [PR #1140](https://github.com/anthropics/skills/pull/1140)

---

## 2. Community Demand Trends

From the top Issues, the most‑anticipated new Skill directions are:

| Trend | Key Issue | Signal |
|---|---|---|
| **Org-wide skill sharing & management** | [#228](https://github.com/anthropics/skills/issues/228) (13 comments, +7) | Users want a shared skill library or direct sharing links instead of manual file transfers. |
| **Evaluation & testing tooling** | [#556](https://github.com/anthropics/skills/issues/556) (12 comments, +7), [#1169](https://github.com/anthropics/skills/issues/1169) | `run_eval.py` has systemic recall bugs; the community is investing heavily in fixing the eval loop. |
| **Security & trust boundaries** | [#492](https://github.com/anthropics/skills/issues/492) (7 comments, +2) | Concerns about community skills impersonating official Anthropic skills under the `anthropic/` namespace. |
| **Skill portability / bundling** | [#1220](https://github.com/anthropics/skills/issues/1220), [#1156](https://github.com/anthropics/skills/issues/1156) | Demand for multi-file preloading and per-skill portability labels to avoid workspace-specific assumptions. |
| **Agent governance & safety** | [#412](https://github.com/anthropics/skills/issues/412) | Proposal for a skill that teaches Claude governance patterns (policy enforcement, threat detection, trust scoring). |
| **MCP/REST integration** | [#16](https://github.com/anthropics/skills/issues/16), [#29](https://github.com/anthropics/skills/issues/29) | Interest in exposing Skills as MCPs and using them with Bedrock. |
| **Duplicate & identity management** | [#189](https://github.com/anthropics/skills/issues/189), [#61](https://github.com/anthropics/skills/issues/61) | Skills installed from different plugins cause duplicates; loading errors on Team plans are unresolved. |

The strongest recurring theme is **skill authoring and evaluation toolchain reliability** — the community is spending more effort fixing how skills are built, tested, and validated than on the skills themselves.

---

## 3. High-Potential Pending Skills

These open PRs have active discussion and are most likely to land in the near future:

- **#1140 agent-creator meta-skill** – Addresses issue #1120, includes evaluation and Windows fixes. Recent update on 2026-06-02 suggests imminent merge.
- **#509 CONTRIBUTING.md** – Closes #452, a simple but impactful community health fix. Fresh PR with clear scope.
- **#723 testing-patterns skill** – Comprehensive guide (unit testing, React, Cypress, Playwright). Strong alignment with community demand for quality patterns.
- **#154 shodh-memory skill** – Persistent context across conversations. Reviewed by multiple maintainers; discussion nearing resolution.
- **#568 ServiceNow platform skill** – Broad enterprise coverage. Reviewer comments mostly positive, with requests to slim down the scope.
- **#190 n8n-builder + n8n-debugger** – Production-tested. Has been open since Dec 2025, but still active; likely to merge after resolving skill naming conventions.
- **#1099 Windows subprocess pipe fix** – Critical bug blocking Windows users from running evaluations. Small change, high impact.
- **#363 feature-dev workflow fix** – Fixes TodoWrite overwrite bug in `/feature-dev`. Active since Feb, but discussion has converged.

---

## 4. Skills Ecosystem Insight

The community’s most concentrated demand is for **robust skill authoring tooling and evaluation infrastructure** — over half of the top PRs and issues focus not on end‑user skills, but on improving how skills are built, validated, tested, and shared reliably across platforms (Windows, case‑sensitive filesystems, YAML parsing, eval loops), revealing that the ecosystem’s bottleneck is shifting from skill **creation** to skill **quality assurance and portability**.

---

# Claude Code Community Digest – 2026-06-10

## Today's Highlights

Anthropic released **Claude Code v2.1.170** featuring the new **Claude Fable 5** (Mythos-class) model, described as the most capable model ever made generally available. The release is accompanied by a surge of community activity: a long-running Windows relaunch bug (#42776) continues to frustrate users, while the demand for an official Linux desktop build (#65697) now garners over 400 upvotes. Several critical bugs around session corruption and tool-call failures are also drawing attention.

## Releases

**v2.1.170** – [Release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.170)

- Introducing **Claude Fable 5**: a Mythos-class model with capabilities exceeding any previously released model. Update to v2.1.170 for access. [Anthropic announcement](https://www.anthropic.com/news/claude-fable-5-mythos-5)
- Fixed session handling.

## Hot Issues

1. **[#42776] Claude Code Desktop fails to Relaunch on Windows due to orphaned process file lock** – [Issue](https://github.com/anthropics/claude-code/issues/42776)  
   *86 comments, 31 👍*  
   A persistent Windows bug blocking app relaunch. Community workarounds exist but no fix in sight. High priority for Windows users.

2. **[#65697] Official Claude Desktop build for Linux (Ubuntu LTS / Debian)** – [Issue](https://github.com/anthropics/claude-code/issues/65697)  
   *31 comments, 406 👍*  
   The most upvoted feature request. Developers on Linux feel neglected; many resort to workarounds or leave the platform.

3. **[#61889] CVP approved user being blocked on benign queries on claude.ai** – [Issue](https://github.com/anthropics/claude-code/issues/61889)  
   *29 comments, 3 👍*  
   False-positive safety blocking affecting paying users, eroding trust in moderation.

4. **[#29006] Enable Remote Control for Claude Code sessions in Claude Desktop App** – [Issue](https://github.com/anthropics/claude-code/issues/29006)  
   *28 comments, 94 👍*  
   Strong demand for headless/remote session management, particularly for CI/CD and team workflows.

5. **[#33153] Bundled Bun binary lacks AVX baseline support – crashes on non-AVX CPUs** – [Issue](https://github.com/anthropics/claude-code/issues/33153)  
   *9 comments, 9 👍*  
   Crashes on older Macs and virtual machines. Easy to fix (swap to baseline Bun) but not addressed.

6. **[#66273] Opus self-favoring asymmetric skepticism, unstable calibration** – [Issue](https://github.com/anthropics/claude-code/issues/66273)  
   *5 comments*  
   Deep behavioral issue: model treats its own claims uncritically while questioning user input. Raises concerns for reliability in long sessions.

7. **[#66760] API 400: harness emits content block with type: "fallback" – session permanently unrecoverable** – [Issue](https://github.com/anthropics/claude-code/issues/66760)  
   *4 comments*  
   Critical bug: an invalid content block kills the session entirely. No recovery possible; data loss for users.

8. **[#66761] Workflow-tool agent() subagents omit x-claude-code-agent-id / parent-agent-id** – [Issue](https://github.com/anthropics/claude-code/issues/66761)  
   *2 comments, 3 👍*  
   Inconsistent agent identification breaks downstream tooling and observability for multi-agent workflows.

9. **[#64991] Opus 4.8: forced balance-slot criticism, critique-for-its-own-sake** – [Issue](https://github.com/anthropics/claude-code/issues/64991)  
   *3 comments, 1 👍*  
   Detailed report of model behavior making sessions nearly unusable due to relentless contrarian outputs.

10. **[#66763] PR monitor chips never retire – survive PR close, merge, archive, restart** – [Issue](https://github.com/anthropics/claude-code/issues/66763)  
    *2 comments*  
    UX bug: stale GitHub PR indicators clutter the desktop interface with no way to dismiss them.

## Key PR Progress

1. **[#66650] fix(pr-review-toolkit): use full author name in plugin manifest** – [PR](https://github.com/anthropics/claude-code/pull/66650)  
   Consistency fix for the bundled plugin’s metadata. Small but important for plugin discovery.

2. **[#66608] fix(#66592): False positive Usage Policy block on lattice gauge theory question (Fable 5)** – [PR](https://github.com/anthropics/claude-code/pull/66608)  
   Automated fix via REAPR addressing a safety classifier overreach on legitimate scientific queries. Critical for model trust.

3. **[#66607] fix(#66595): Fable 5 safety classifier auto-switches to Opus mid-session during authorized security testing** – [PR](https://github.com/anthropics/claude-code/pull/66607)  
   Another REAPR fix: classifier incorrectly downgrades model during in-scope security work.

4. **[#66577] fix(marketplace): sync security-guidance version and description with plugin.json** – [PR](https://github.com/anthropics/claude-code/pull/66577)  
   Resolves metadata drift between marketplace registry and plugin source.

5. **[#66575] fix(pr-review-toolkit): use full author name in plugin.json** – [PR](https://github.com/anthropics/claude-code/pull/66575)  
   Same correction as #66650 but in the plugin’s own manifest. Ensures author name consistency across the repo.

6. **[#66573] fix(ralph-wiggum): restore dead error handlers broken by set -euo pipefail** – [PR](https://github.com/anthropics/claude-code/pull/66573)  
   Shell script fixes: `set -e` was silencing error-handling code, making failures silent and unrecoverable.

7. **[#66572] [WIP] Repeated "Image couldn't be processed" API errors consuming usage limit** – [PR](https://github.com/anthropics/claude-code/pull/66572)  
   Work in progress addressing a costly API error loop that burns usage credits without delivering results.

8. **[#66416] fix(plugin-dev): validator scripts abort on first finding due to set -e** – [PR](https://github.com/anthropics/claude-code/pull/66416)  
   Similar to #66573: `set -e` in plugin validation scripts stops at the first error instead of reporting all linter issues.

9. **[#65723] Claude/subscription debate chat rx ewi** – [PR](https://github.com/anthropics/claude-code/pull/65723)  
   Title unclear; likely a draft or test PR. Low visibility.

## Feature Request Trends

- **Linux desktop build** (#65697) remains the single most requested feature, with 406 upvotes. Many developers are unable or unwilling to use the CLI on Linux without a proper desktop app.
- **Remote control / headless operation** (#29006) is the second-largest ask (94 👍). Users want to manage Claude Code sessions programmatically or from a CI pipeline.
- **Alternative model support** (#66757) becomes more pressing now that Fable 5 is out but locked to Opus in Claude Code. Users want to choose models per task (cost vs. capability).
- **Rate-limit-aware deferred scheduling** (#59634) and **ultracode mode cost visibility** (#66762) reflect a growing concern about usage limits and cost management, especially with multi-agent workflows.
- **Session recovery and history commands** (#66754): the removal of `/history` has broken workflows where users need to revisit past messages.
- **Plugin/hook runtime improvements**: mid-session hook enforcement (#65953) and better agent-tool identification (#66761) are recurring themes.

## Developer Pain Points

- **Windows platform instability**: Orphaned process locks (#42776), MSIX path virtualization bugs (#66778), session data loss on update (#66775), and cursor visibility issues in Windows Terminal (#66398) make the Windows experience fragile.
- **Linux desktop gap**: No official desktop client forces users to either tolerate a CLI-only experience or seek unofficial workarounds, impacting adoption.
- **Model behavior degradation**: Reports of hallucinated user messages (#66771), stubbornly contrarian outputs (#64991), and asymmetric skepticism (#66273) erode trust, especially in long sessions.
- **Session-level data loss**: Invalid API responses (e.g., `type: "fallback"` in #66760) can lock a session permanently with no recovery path.
- **Settings and hook inconsistencies**: Mid-session settings changes (#66765) and hook additions (#65953) are ignored until restart, breaking automation workflows.
- **PR monitor UX**: Stale PR chips that survive merge, archive, and restart (#66763) clutter the desktop UI and lack any cleanup mechanism.
- **Cost surprises**: Ultracode mode can silently consume a full usage window via subagent fleets (#66762), leaving users unable to complete their original task.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-10

## Today’s Highlights
The team shipped **rust-v0.139.0** with support for standalone web search from code mode, while two pre-release alpha builds rolled out for v0.139 and v0.140. On the bug front, a concentrated wave of reports continues around **disappearing chat histories** after Desktop updates—now spanning multiple OS and app versions. The community also flagged a **Windows sandbox regression** and a new `invalid_enum_value` compaction error. Infrastructure PRs are focusing on streaming file APIs, MCP reliability, and path abstraction migration.

## Releases
- **rust-v0.139.0** (stable) — Code mode can now call standalone web search directly, including from nested JavaScript tool calls, receiving plaintext results. Also improved tool/connector input schema handling (preserving `oneOf`/`allOf`) and large schema compaction.
- **rust-v0.140.0-alpha.2**, **rust-v0.139.0-alpha.3**, **rust-v0.139.0-alpha.2** — Pre-release builds, no detailed changelog.

## Hot Issues (10 selected)

1. **[#24391](https://github.com/openai/codex/issues/24391)** – **Windows sandbox: spawn setup refresh fails** on Codex CLI 0.133.0. High engagement (44 comments, 25 👍) – breaking Windows agent execution after update, multiple workarounds attempted.  
2. **[#20741](https://github.com/openai/codex/issues/20741)** – **Chat histories disappeared** after Codex Desktop update on macOS. 33 comments, 14 👍. Persistent theme: local SQLite data intact but UI fails to list threads.  
3. **[#19585](https://github.com/openai/codex/issues/19585)** – **Pro weekly usage limit depletes unusually fast** on 5.5, worsened by unstable context compaction. 29 comments, 26 👍 – strong community resonance, impacts daily workflow.  
4. **[#21128](https://github.com/openai/codex/issues/21128)** – **Desktop silently hides project conversations** outside the global recent-50 window. 23 comments, 16 👍. Core UX concern – makes app unreliable as persistent memory for projects.  
5. **[#23979](https://github.com/openai/codex/issues/23979)** – **Local project conversation history missing** after update; threads still in `state_5.sqlite`. 20 comments, 4 👍. Similar root cause pattern across macOS and Windows.  
6. **[#26493](https://github.com/openai/codex/issues/26493)** – **Context compaction fails with `invalid_enum_value`** for `context_compaction` on Windows. 16 comments, 4 👍. New regression that breaks long sessions.  
7. **[#24287](https://github.com/openai/codex/issues/24287)** – **UI stuck in “Thinking”** after prompt; Stop fails, turn becomes invisible after restart. 14 comments. Affects Pro users, unclear if server-side or client bug.  
8. **[#2909](https://github.com/openai/codex/issues/2909)** – **Support for multi-root workspaces** in VS Code extension. 125 👍, oldest open enhancement. Highly requested feature for monorepo setups.  
9. **[#16717](https://github.com/openai/codex/issues/16717)** – **Configurable Windows agent shell** (PowerShell/git-bash). Closed as enhancement, 15 👍. Users want bash on Windows for better command generation.  
10. **[#27278](https://github.com/openai/codex/issues/27278)** – **Windows Desktop: elevated sandbox blocks node_repl**; unelevated fixes bridge but Computer Use pipe missing. Newly opened, 4 comments – demonstrates ongoing Windows sandbox friction.

## Key PR Progress (10 selected)

1. **[#27190](https://github.com/openai/codex/pull/27190)** – **Add streaming file APIs** (pull-based reads/writes) to app-server v2 and exec-server. Enables efficient large-file handling with positional reads and bounded commits.  
2. **[#27261](https://github.com/openai/codex/pull/27261)** – **Make MCP connection startup fallible** – separates required-server validation from manager construction, improving error handling for misconfigured MCP servers.  
3. **[#27127](https://github.com/openai/codex/pull/27127)** – **Forward assistant output to realtime through handoffs** – ensures frontend model hears all user-facing Codex messages for coherent voice experience.  
4. **[#27276](https://github.com/openai/codex/pull/27276)** – **Reduce archive rollout lookup CPU** – optimizes thread archiving by directly locating rollout files via UUID, avoiding expensive fallback searches.  
5. **[#25232](https://github.com/openai/codex/pull/25232)** (closed) – **Derive window generation from effective rollout lineage** – fixes `x-codex-window-id` after rollback/resume to correctly track compaction history.  
6. **[#19047](https://github.com/openai/codex/pull/19047)** (+ [#19049](https://github.com/openai/codex/pull/19049) & [#19051](https://github.com/openai/codex/pull/19051)) – **Add run task identity primitives** and opt ChatGPT auth into agent identity – foundational stack for simplified HAI single-run-task authentication.  
7. **[#27280](https://github.com/openai/codex/pull/27280)** – **Add `PathUri` native conversion APIs** – centralizes host-native path conversion ahead of ExecutorFileSystem migration.  
8. **[#27282](https://github.com/openai/codex/pull/27282)** – **Migrate ExecutorFileSystem to `PathUri`** – changes internal operations to use `PathUri` while keeping wire format unchanged.  
9. **[#27246](https://github.com/openai/codex/pull/27246)** – **Strip image detail from Responses Lite requests** – reduces payload size and potential processing overhead.  
10. **[#27078](https://github.com/openai/codex/pull/27078)** (closed) – **Emit goal lifecycle analytics** – adds `/goal` event tracking, missing until now. Follows earlier PR [#26182](https://github.com/openai/codex/pull/26182).

## Feature Request Trends
- **Multi-root workspace support** ([#2909](https://github.com/openai/codex/issues/2909), 125 👍) remains the #1 feature ask, blocking many monorepo workflows.
- **Configurable agent shell on Windows** ([#16717](https://github.com/openai/codex/issues/16717)) – users want to switch from PowerShell to bash/Git Bash for more reliable command generation.
- **Better chat history retention and visibility** – multiple issues implicitly request persistent sidebar/search for all local threads, not a capped recent list.
- **Usage/token efficiency improvements** – the Pro limit depletion issue ([#19585](https://github.com/openai/codex/issues/19585)) signals demand for more transparent and predictable context compaction.

## Developer Pain Points
- **Chat history disappearance after updates** is the most frequent and disruptive bug – affects macOS, Windows, and Linux across Desktop and CLI. Data remains on disk but UI stops listing it. Workarounds often require manual SQLite manipulation.
- **Windows sandbox reliability** – spawn setup failures, elevation issues, missing node_repl, and MCP client start failures. Multiple open issues ([#24391](https://github.com/openai/codex/issues/24391), [#26158](https://github.com/openai/codex/issues/26158), [#27278](https://github.com/openai/codex/issues/27278)) indicate this is a significant platform gap.
- **Context compaction errors** – `invalid_enum_value` and `context_length_exceeded` failures block long-running sessions, especially on remote SSH and mobile handoff ([#26493](https://github.com/openai/codex/issues/26493), [#22890](https://github.com/openai/codex/issues/22890)).
- **Usage limits depleting unexpectedly** – Pro users report 5.5 burning through weekly quotas 20× faster than expected, compounded by unstable compaction ([#19585](https://github.com/openai/codex/issues/19585), [#27242](https://github.com/openai/codex/issues/27242)).
- **UI stuck in “Thinking” state** with nonfunctional Stop button and lost turns ([#24287](https://github.com/openai/codex/issues/24287)) – degrades user trust when recovery requires restart.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*