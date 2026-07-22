# AI CLI Tools Community Digest 2026-07-22

> Generated: 2026-07-22 02:12 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date:** 2026-07-22 | **Sources:** Claude Code, OpenAI Codex community digests

---

## 1. Ecosystem Overview

The AI CLI tools landscape is experiencing a bifurcation between **productivity innovation** and **platform stability**. Claude Code (v2.1.217) is advancing UX features (emoji autocomplete, hookify fixes) while wrestling with high-impact reliability gaps—remote session disconnects and agent crash-loops that erode trust in headless workflows. OpenAI Codex (rust-v0.145.0) is investing heavily in **cross-project portability** (expanded `/import` for Cursor/Claude migrations) and **infrastructure hardening** (HTTP client migration, Windows process lifecycle control), but remains plagued by runaway Git polling and sandbox regressions. Both communities signal that **Windows parity** and **background agent robustness** are the dominant cross-cutting pain points, with Windows-specific issues dominating the top-10 bug lists on both trackers.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Hot Issues** | 10 tracked (99 👍 peak, 4 months open) | 10 tracked (48 👍 peak, multiple open) |
| **Key PRs** | 10 merged (hookify fixes, AWS example, TTS) | 10 merged (HTTP client migration, Windows sandbox, skill budgets) |
| **Latest Release** | v2.1.217 (emoji autocomplete, disk-full warnings) | rust-v0.145.0 (+3 alphas; paginated threads, `/import` expansion) |
| **Release Cadence** | Minor releases ongoing | Major release with experimental features |
| **Top Issue Severity** | Silent disconnects, MCP call drops, fd-storm kernel panic | Runaway Git/taskkill processes, WMI exhaustion, bwrap regression |
| **Platform-Specific Pain** | Windows: update-forces-reboot, scrollbar broken | Windows: process storms, Defender conflicts, sandbox elevation |

**Key observation:** Both tools share a common problem cluster—**background processes leaking resources**—but manifest differently (Claude Code: fd exhaustion → kernel panic; Codex: git/taskkill storms → desktop freeze).

---

## 3. Shared Feature Directions

| Theme | Tools | Specific Needs |
|---|---|---|
| **Reliable Session Recovery** | Claude Code, Codex | Automatic reconnection on disconnect; resilient 1M-context session checkpointing; compact/restore without full context replay |
| **MCP Tool-Call Guarantees** | Claude Code (#79992), Codex (sandbox tool routing) | Silent drops after approval gate; need idempotent dispatch, retry logic, and telemetry for tool-call lifecycle |
| **Windows Platform Parity** | Claude Code (#72215, #76357), Codex (#17229, #33776) | Scrollbar/input handling, MSIX update without reboot, termination of orphaned child processes, TUI navigation fixes |
| **Background Agent Stability** | Claude Code (#75037, #79920), Codex (sub-agent PRs) | Crash-loop protection, file descriptor limits, configurable token caps, billing enforcement after spend limit hit |
| **Cross-Platform Path Handling** | Claude Code (#79644, #79645), Codex (#34625) | Spaces in macOS paths, UTF-8 encoding defaults, Windows virtual terminal mode interference |
| **Sub-Agent/Multi-Session Improvements** | Claude Code (#78460), Codex (#33364) | Remove arbitrary 8k token caps, prevent destructive git operations by subagents, paginated history for long-running sessions |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Feature Focus** | Developer UX polish (emoji autocomplete, TTS hook, hookify plugin system) | Cross-tool portability (migrate Cursor/Claude settings), experimental memory/threads |
| **Target Users** | Individual developers, plugin authors, Remote Control heads | Enterprise teams, multi-repo workspaces, sandboxed CI/CD |
| **Technical Approach** | Plugin-based extensibility (hookify), AWS/GCP reference deployments | Sandbox-first (bubblewrap, Windows elevated sandbox), HTTP client architectural cleanup |
| **Reliability Investment** | Fixing existing feature gaps (hookify path quoting, encoding) | Infrastructure hardening (proxy-aware HTTP, job object process termination) |
| **Pain Point Priority** | Remote session trust, MCP call reliability, background daemon leaks | Windows process lifecycle control, sandbox regression prevention, Git polling debouncing |
| **Community Engagement** | High-urgency issues (99 👍) open for 4 months; focus on macOS | Broad Windows bug cluster (13 👍 each, 17-29 comments); Linux sandbox regression re-opened |

**Takeaway:** Claude Code is iterating on **developer delight and plugin ecosystem** while Codex is focused on **architectural resilience and cross-platform portability**. Codex’s `/import` feature directly targets Claude Code users, indicating competitive positioning, while Claude Code’s hookify fixes suggest a maturing extensibility layer.

---

## 5. Community Momentum & Maturity

- **Claude Code**: High urgency but slower resolution. Issue #34255 (remote disconnect) has 99 👍 and 57 comments over 4 months—this is a trust-eroding bug that remains unresolved despite being the top community concern. The hookify fixes (5 PRs in one day) show strong iteration velocity on plugin infrastructure. The fd-storm kernel panic (#79920) is a critical safety concern for automated workflows. **Verdict:** Mature feature surface, but reliability gaps threaten adoption in production/CI.

- **OpenAI Codex**: More intense community engagement concentrated on Windows-specific pain. The top-10 bug list contains 8 Windows process-spawning issues, with cross-referencing (e.g., #17229, #29492, #20567 are variants of the same root cause). The rapid-fire alpha releases (3 in one day) indicate aggressive iteration, and the HTTP client migration PR series (#34630, #34645) suggests architectural debt reduction. **Verdict:** Rapidly evolving, Windows-heavy user base, investing in infrastructure maturity.

- **Community Health Comparison**: Codex has higher comment volumes per Windows issue (17-29 comments) suggesting more engaged troubleshooting; Claude Code’s top issue (#34255) has 57 comments but zero resolution—risk of community fatigue.

---

## 6. Trend Signals

1. **Windows is the new frontier for AI CLI tools.** Both tools have Windows-specific bugs in their top-5 pain points. The inability to safely update, terminate processes, or render TUI output predictably on Windows is a barrier to enterprise adoption. Codex’s job-object-based process tree termination (#34624) and sandbox hardening (#34629) represent best-practice responses.

2. **Background agent reliability is a production prerequisite.** The fd-storm kernel panic (Claude Code) and runaway taskkill storms (Codex) both stem from unmanaged background processes. Expect hardening around file descriptor limits, process group die-with-parent semantics, and graceful degradation when system resources are exhausted.

3. **MCP tool-call guarantees are under-specified.** Both tools report silent failures after approval gates (Claude Code #79992) and routing mismatches (Codex sandbox proxy). The community needs a standardized tool-call lifecycle (dispatch → execute → confirm → retry) with observable telemetry.

4. **Large-context session fragility remains unsolved.** Claude Code’s 1M-context unrecoverable errors (#74544) and premature auto-compact warnings mirror broader industry challenges with infinite-context models. Expect checkpointing, chunked recovery, and partial compact as required features.

5. **Plugin/hook ecosystems demand cross-platform path hygiene.** Both tools fixed UTF-8 encoding (Claude Code #79645) and path quoting (Claude Code #79644) issues in the same week. Windows/macOS path handling is consistently the top cause of hook/plugin breakage—a pattern that will repeat as more third-party extensions emerge.

6. **Entitlement/credit transparency is a growing concern.** Claude Code’s Fable 5 gating bug (#79360) and Codex’s spend-limit enforcement gaps signal that users expect clear, predictable billing for model access—especially when sub-agents or third-party models are involved.

---

*Report generated from community digest data on 2026-07-22.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
*Data as of 2026-07-22 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking (Most-Discussed Pull Requests)

The following PRs attracted the highest community engagement (by comment volume). All remain **open** unless noted.

### 🥇 `fix(skill-creator): run_eval.py always reports 0% recall` (#1298)
- **Functionality**: Fixes a critical bug in the skill‑creator toolchain where `run_eval.py` consistently reports `recall=0%`, making the description‑optimization loop (`run_loop.py`, `improve_description.py`) optimize against noise. The fix installs the eval artifact as a real skill, corrects Windows stream‑reading, trigger detection, and parallel‑worker issues.
- **Discussion highlights**: The root cause is deeply tied to how Claude CLI processes commands – the community has independently reproduced the bug across environments (#556, #1169, #1061). The PR is seen as the “master fix” for a blocker that has stalled skill authoring.
- **Status**: Open – high urgency, multiple contributors involved.

### 🥈 `Add document-typography skill` (#514)
- **Functionality**: A skill that prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI‑generated documents – issues that affect nearly every Claude‑generated document.
- **Discussion highlights**: The skill addresses a universal pain point; reviewers praised its clear trigger definitions and practical examples. The author provided before/after samples showing measurable quality improvement.
- **Status**: Open – nearing final review.

### 🥉 `fix(pdf): correct case‑sensitive file references in SKILL.md` (#538)
- **Functionality**: Fixes 8 case‑sensitivity mismatches in the PDF skill’s `SKILL.md` (e.g., `REFERENCE.md` → `reference.md`) that break on case‑sensitive filesystems (Linux/macOS).
- **Discussion highlights**: A straightforward but important reliability fix – the community noted this also affects cross‑platform CI and Docker usage.
- **Status**: Open (merged-like, but still open in data).

### #4 `Add ODT skill — OpenDocument text creation and template filling` (#486)
- **Functionality**: Enables Claude to create, fill, read, and convert OpenDocument Format files (.odt, .ods). Covers LibreOffice document workflows and template filling.
- **Discussion highlights**: The skill is comprehensive; reviewers discussed overlap with existing `docx` and `pdf` skills and requested clearer separation of concerns.
- **Status**: Open – awaiting re‑review after author updates.

### #5 `Improve frontend‑design skill clarity and actionability` (#210)
- **Functionality**: Revises the frontend‑design skill to make every instruction actionable within a single conversation, ensuring guidance is specific enough to steer Claude’s behavior.
- **Discussion highlights**: This is a quality‑of‑life improvement for an existing skill. The community debated the balance between brevity and specificity; the PR represents a model for skill refinement.
- **Status**: Open.

### #6 `Add skill‑quality‑analyzer and skill‑security‑analyzer to marketplace` (#83)
- **Functionality**: Two meta‑skills: **skill‑quality‑analyzer** evaluates skills across five dimensions (structure, documentation, etc.), and **skill‑security‑analyzer** audits skills for security issues (e.g., path traversal, command injection).
- **Discussion highlights**: One of the earliest meta‑skill proposals; the community sees it as essential for a trusted Skills ecosystem. However, concerns were raised about false positives and the overhead of running analysis on every skill.
- **Status**: Open – long‑standing, still relevant.

### #7 `fix(docx): prevent tracked change w:id collision with existing bookmarks` (#541)
- **Functionality**: Prevents document corruption when the DOCX skill adds tracked changes to documents that already have bookmarks – the `w:id` ID space is shared across OOXML elements.
- **Discussion highlights**: A subtle but critical bug that could corrupt user documents silently. Author provided a clear root‑cause analysis.
- **Status**: Open.

### #8 `Add pyxel skill for retro game development` (#525)
- **Functionality**: A skill that integrates Claude with the Pyxel retro game engine via MCP, enabling iterative game development (write → run‑and‑capture → inspect → fix loop).
- **Discussion highlights**: A creative, well‑contained skill that showcases MCP integration. Community members shared their own Pyxel creations.
- **Status**: Open (updated as recently as 2026-07-15).

---

## 2. Community Demand Trends (from Issues)

The top‑voted and most‑discussed Issues reveal five clear demand clusters:

| Demand Area | Representative Issues | Signal |
|-------------|----------------------|--------|
| **🔒 Trust & security** | #492 (namespace impersonation, 43 comments, 👍2) – community skills under `anthropic/` namespace create trust‑boundary risks | **Highest engagement issue overall** – users want official vetting or a distinct namespace. |
| **🏢 Enterprise / org features** | #228 (org‑wide skill sharing, 14 comments, 👍7) – requesting direct sharing links or a shared skill library | Strongest upvote count (7) – indicates a professional user base. |
| **🛠️ Skill‑creator tooling reliability** | #556 (run_eval 0% trigger rate, 12 comments, 👍7), #1169 (recall=0% on literal commands), #1061 (Windows compatibility) | **Most technical demand** – the skill‑creator pipeline is the primary blocker for community contributions. |
| **🧠 Advanced agent patterns** | #1329 (compact‑memory – symbolic notation for agent state, 9 comments), #412 (agent‑governance – safety patterns), #1385 (reasoning quality gate pipeline) | Emerging interest in meta‑skills that manage Claude’s own behavior and memory. |
| **🔌 Ecosystem integration** | #16 (expose Skills as MCPs), #29 (Bedrock support), #184 (agentskills.io broken) | Demand for broader platform reach and standardized APIs. |

**Most anticipated new skill directions**:  
- **Agent safety & governance** (policy enforcement, audit trails)  
- **Memory & context management** (compact symbolic notation)  
- **Quality assurance / review pipelines** (reasoning gates, mechanical verification)  

---

## 3. High‑Potential Pending Skills (Active‑Comment PRs Not Yet Merged)

These PRs have sustained discussion and are likely to land soon:

1. **#1298 – `fix(skill-creator): run_eval.py always reports 0% recall`**  
   *The #1 blocker for the entire skill‑authoring workflow. Multiple authors are contributing fixes – expect a merge within weeks.*

2. **#1367 – `feat(skills): add self‑audit — mechanical verification + four‑dimension reasoning quality gate`**  
   *A universal audit skill that verifies output files and performs a structured reasoning audit. Gained traction as a complementary piece to agent‑governance.*

3. **#1302 – `Add color‑expert skill`**  
   *Comprehensive color knowledge (color naming systems, spaces, accessibility). Low controversy, well‑scoped – likely to merge soon after minor feedback.*

4. **#723 – `feat: add testing‑patterns skill`**  
   *Covers testing philosophy, unit testing, React component testing, and TDD. Broadly useful; final touches on trigger specificity.*

5. **#210 – `Improve frontend‑design skill clarity`**  
   *Already reviewed, awaiting final approval – a model PR for iterative skill improvement.*

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for reliable, secure, and cross‑platform skill‑authoring tooling** – the unresolved `run_eval.py` bug and the namespace‑impersonation vulnerability are the top blockers to scaling the Skills ecosystem, while complementary high‑value skills (document typography, testing patterns, color expertise) demonstrate that once the toolchain stabilizes, the community is ready to deliver a rich library of production‑ready skills.

---

*Links: [Pull Requests](https://github.com/anthropics/skills/pulls?q=sort%3Acomments-desc) | [Issues](https://github.com/anthropics/skills/issues?q=sort%3Acomments-desc)*

---

# Claude Code Community Digest — 2026-07-22

## Today’s Highlights
**v2.1.217** ships emoji shortcode autocomplete and disk‑full warnings for transcript writes. The community continues to hammer on two high‑impact bugs: remote control silent disconnects (#34255, 57 comments, 99 👍) and a Fable 5 entitlement gating flaw (#79360, 30 👍). On the PR front, the team landed a bulk set of **hookify** fixes (entrypoints, encoding, quoting) and an AWS Gateway deployment example. Three fresh bugs from the last 24 hours (MCP tool‑call drops, session freeze, fd‑storm kernel panic) signal emerging stability concerns.

---

## Releases
**v2.1.217** — [Release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.217)
- **Emoji shortcode autocomplete**: type `:heart:` → ❤️, or `:hea` for suggestions. Disable via `emojiCompletionEnabled`.
- **Transcript write warnings**: alerts when writes fail (e.g. disk full) or session saving is off due to an inherit.

---

## Hot Issues (10 most noteworthy)

1. **[#34255 – Remote Control auto‑reconnection broken](https://github.com/anthropics/claude-code/issues/34255)**  
   *57 comments, 99 👍. macOS/iOS.* Connection drops silently with no recovery. Highest community urgency; 4 months old but still open.

2. **[#79360 – Fable 5 gated behind credits on Max with setup‑token auth](https://github.com/anthropics/claude-code/issues/79360)**  
   *5 comments, 30 👍. macOS.* Inference‑only scope cannot read entitlements, so Fable 5 is blocked despite active Max plan. Directly affects paid users.

3. **[#45810 – Marketplace update button unclickable](https://github.com/anthropics/claude-code/issues/45810)**  
   *15 comments, 6 👍. Plugins area.* The “Update” button is greyed out even when a newer version exists. Blocks plugin maintenance.

4. **[#72215 – Fullscreen mode: no scrollbar, arrows/PageUp/PageDown broken](https://github.com/anthropics/claude-code/issues/72215)**  
   *6 comments, 4 👍. Windows TUI.* Once output exceeds one screen, earlier output becomes inaccessible. Fundamental UX regression.

5. **[#76357 – Windows MSIX update fails with “file in use”; app unlaunchable](https://github.com/anthropics/claude-code/issues/76357)**  
   *6 comments, 4 👍. Windows Desktop.* Every update forces a reboot. Related to [#70733](https://github.com/anthropics/claude-code/issues/70733) (Cowork tab missing after reinstall).

6. **[#79992 – macOS: MCP filesystem tool calls silently dropped](https://github.com/anthropics/claude-code/issues/79992)**  
   *4 comments, 0 👍.* Started 2026‑07‑21→22. Approval gate passes but server never receives `tools/call`. Survives app rollback/reinstall — hints at a deeper dispatch bug.

7. **[#79921 – Sessions freeze until another session receives input](https://github.com/anthropics/claude-code/issues/79921)**  
   *3 comments, 0 👍.* Desktop & VS Code only (web works). Suggests IPC/event‑loop contention.

8. **[#75037 – Background agent crash‑loop & lost completion records](https://github.com/anthropics/claude-code/issues/75037)**  
   *3 comments, 0 👍. macOS.* `claude --bg` sessions terminate fast; `claude agents` reattach crashes. Blocks automated workflows.

9. **[#74544 – 1M‑context session unrecoverable on ECONNRESET](https://github.com/anthropics/claude-code/issues/74544)**  
   *2 comments, 0 👍. macOS/Networking.* Cold cache + large payload → ECONNRESET, and `/compact` also fails (needs full context). Session is lost.

10. **[#79920 – fd storm exhausts file table → kernel panic](https://github.com/anthropics/claude-code/issues/79920)**  
    *2 comments, 0 👍. macOS.* Background daemon accumulates file descriptors, hits ENFILE, then launchd SIGBUS → panic. Critical for headless automation.

---

## Key PR Progress (10 most important)

1. **[#79898 – Add Claude apps gateway on AWS example](https://github.com/anthropics/claude-code/pull/79898)**  
   Reference deployment artifacts for Amazon Bedrock. Sibling to existing GCP examples.

2. **[#79889 – fix(hookify): make hook entrypoints runnable without CLAUDE_PLUGIN_ROOT](https://github.com/anthropics/claude-code/pull/79889)**  
   Silently skipped path setup when env var absent. Now works standalone.

3. **[#79873 – fix(hookify): prompt rules never fire](https://github.com/anthropics/claude-code/pull/79873)**  
   `event: prompt` rules read wrong payload key (`user_prompt` vs `prompt`). Now fixed.

4. **[#79647 – fix(hookify): resolve imports independent of plugin dir name](https://github.com/anthropics/claude-code/pull/79647)**  
   Hard‑coded package name broke when directory was renamed. Fixes #69665.

5. **[#79645 – fix(hookify): read rule/transcript files as UTF‑8](https://github.com/anthropics/claude-code/pull/79645)**  
   Default encoding (cp1252 on Windows) corrupted example files with emoji/arrows.

6. **[#79644 – fix: quote ${CLAUDE_PLUGIN_ROOT} in plugin hook commands](https://github.com/anthropics/claude-code/pull/79644)**  
   Spaces in macOS `~/Library/Application Support/...` caused word‑splitting. Fixes #78490.

7. **[#79643 – docs(commit-commands): align /commit-push-pr description with behavior](https://github.com/anthropics/claude-code/pull/79643)**  
   Documentation claimed branch‑level description; tool only uses staged/unstaged diff.

8. **[#79642 – docs(plugin-dev): correct marketplace name to claude-code-plugins](https://github.com/anthropics/claude-code/pull/79642)**  
   README pointed to non‑existent `claude-code-marketplace`. Fixes #70064.

9. **[#79640 – fix(ralph-wiggum): use disable-model-invocation instead of invalid key](https://github.com/anthropics/claude-code/pull/79640)**  
   `hide-from-slash-command-tool` is not recognized; replaced with valid frontmatter.

10. **[#79620 – feat: text‑to‑speech read‑aloud hook for accessibility](https://github.com/anthropics/claude-code/pull/79620)**  
    Multi‑platform TTS (Linux Piper, macOS say, PowerShell). Markdown‑aware, code‑skip heuristic.

---

## Feature Request Trends

- **Productivity shortcuts** – emoji autocomplete (just shipped), better slash‑command resolution, workflow schema flexibility.
- **Reliability & robustness** – automatic reconnection for remote sessions, MCP tool‑call guarantees, resilient 1M‑context session recovery.
- **Platform parity** – Windows scrollbar/scroll fix, MSIX update without reboot, Linux light/dark theme following system signals.
- **Agent subsystem improvements** – remove arbitrary 8000‑token cap on subagents, prevent destructive git operations by subagents, better billing enforcement (stop charging after spend limit).
- **UX polish** – ability to remove entries from “Recent” folders list, enable/disable update buttons reliably, gateway credential re‑login without leaving session.
- **Documentation accuracy** – several PRs today address mismatched docs vs. behavior (commit commands, marketplace name, frontmatter keys).

---

## Developer Pain Points

- **Update failures on Windows** (#76357) force a full reboot — most‑upvoted platform‑specific blocker.
- **Silent connection drops** (#34255, #79992, #79921) undermine trust in remote/MCP workflows.
- **Agent stability** (#75037, #79920, #78460) — background sessions leak FDs, crash‑loop, and cap output tokens at 8k, frustrating CI/automation users.
- **1M‑context fragility** (#74544, #79665) — cold cache leads to unrecoverable errors; auto‑compact warning fires at 177k instead of 1M.
- **Plugin/hookify ergonomics** – path quoting (#79644), UTF‑8 encoding (#79645), import resolution (#79647) – all fixed today but indicate deeper Windows/macOS path handling gaps.
- **Entitlement/credit mismatches** (#79360, #75757) – paid Max users blocked from Fable 5; subagents billed after spend limit hit.

---

*Generated from [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code) data up to 2026-07-22.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-07-22

## Today’s Highlights
The **rust-v0.145.0** release landed with experimental paginated thread history, sub-agent support, and expanded `/import` for Cursor/Claude Code migrations. Meanwhile, a wave of Windows-related issues continues to dominate the tracker: dozens of reports detail runaway `git.exe`, `taskkill.exe`, and `conhost.exe` processes that freeze the desktop and exhaust WMI. A closed Linux sandbox regression (bwrap `RTM_NEWADDR`) was also re‑opened in spirit, underscoring ongoing sandbox stability challenges.

## Releases
- **rust-v0.145.0** ([release](https://github.com/openai/codex/releases/tag/rust-v0.145.0))  
  - Experimental paginated thread history with efficient resume, search, persisted names, sub‑agent support, and memories (#33364, #33907, #34085, #34229, #34386).  
  - Expanded `/import` to migrate Cursor and Claude Code settings, MCP servers, plugins, sessions, and project commands.  
- Three alpha releases (0.145.0-alpha.28, .29, .30) published without additional changelogs.

## Hot Issues (Top 10 by Activity)
1. **#14919** [CLOSED] *bwrap: Failed RTM_NEWADDR: Operation not permitted* – Linux sandbox regression after CLI update; 44 comments, 48 👍.  
   [openai/codex Issue #14919](https://github.com/openai/codex/issues/14919)

2. **#17229** [OPEN] *Codex Windows App keeps spawning `git.exe status --porcelain=v1 -z` and leaves orphan processes* – 29 comments, 6 👍.  
   [openai/codex Issue #17229](https://github.com/openai/codex/issues/17229)

3. **#33776** [OPEN] *ChatGPT.exe spawns hundreds of taskkill.exe/conhost.exe processes, causing WMI storms and DWM degradation* – 17 comments, 13 👍.  
   [openai/codex Issue #33776](https://github.com/openai/codex/issues/33776)

4. **#30527** [OPEN] *Windows 10: Codex app triggers Microsoft Defender Behavior Monitoring / high CPU* – 16 comments, 13 👍.  
   [openai/codex Issue #30527](https://github.com/openai/codex/issues/30527)

5. **#34260** [OPEN] *Unbounded taskkill.exe/conhost.exe cleanup storm exhausts WMI* – 15 comments, 8 👍.  
   [openai/codex Issue #34260](https://github.com/openai/codex/issues/34260)

6. **#29492** [OPEN] *Windows Codex desktop app creates empty .git folder, then spawns git process repetitively* – 14 comments, 9 👍.  
   [openai/codex Issue #29492](https://github.com/openai/codex/issues/29492)

7. **#20567** [OPEN] *Windows App keeps spawning ~1000 git commands per minute NON STOP* – 13 comments, 2 👍.  
   [openai/codex Issue #20567](https://github.com/openai/codex/issues/20567)

8. **#33875** [OPEN] *High CPU triggered by Windows Defender & WMI when launching Codex Desktop* – 12 comments, 11 👍.  
   [openai/codex Issue #33875](https://github.com/openai/codex/issues/33875)

9. **#29408** [OPEN] *Windows Desktop leaves repeated/stuck git.exe polling processes in multi-repo workspace* – 11 comments, 2 👍.  
   [openai/codex Issue #29408](https://github.com/openai/codex/issues/29408)

10. **#20933** [OPEN] *Windows desktop app triggers multiple git.exe add -A processes on project open, causing severe CPU/disk usage* – 11 comments, 10 👍.  
    [openai/codex Issue #20933](https://github.com/openai/codex/issues/20933)

**Why they matter:** The Windows process‑spawning issues are the most upvoted and commented‑on bugs this week. They directly impact developer productivity by freezing machines, exhausting system resources, and triggering antivirus storms. The recurring *bwrap* regression (#14919) also signals a need for more robust sandbox testing across Linux releases.

## Key PR Progress (Top 10 by Impact)
1. **#34645** – Always assign response item IDs in all session types (streamed, forked, compacted, non‑OpenAI providers).  
   [openai/codex PR #34645](https://github.com/openai/codex/pull/34645)

2. **#34644** – Verify Git plugin SHA checkouts to prevent branch‑name collisions when checking out pinned commits.  
   [openai/codex PR #34644](https://github.com/openai/codex/pull/34644)

3. **#34641** – Harden managed proxy setup for sandboxed executions (bubblewrap socket accessibility, proxy routing).  
   [openai/codex PR #34641](https://github.com/openai/codex/pull/34641)

4. **#34637** – Attribute code‑review findings to repository rules (AGENTS.override.md, etc.) only when guidance adds material.  
   [openai/codex PR #34637](https://github.com/openai/codex/pull/34637)

5. **#34636** – Keep the TUI open when a turn/start fails; finalize the pending turn and resume input handling.  
   [openai/codex PR #34636](https://github.com/openai/codex/pull/34636)

6. **#34630** – Add a policy‑aware `HttpClientBuilder` for configuring proxies, redirects, diagnostics without exposing the transport.  
   [openai/codex PR #34630](https://github.com/openai/codex/pull/34630)

7. **#34629** – Harden Windows elevated sandbox startup (DACL checks, ACL refresh, command run/permissions).  
   [openai/codex PR #34629](https://github.com/openai/codex/pull/34629)

8. **#34624** – Terminate Windows process trees with job objects to stop child processes on session end while allowing background descendants on normal exits.  
   [openai/codex PR #34624](https://github.com/openai/codex/pull/34624)

9. **#34626** – Scale skill metadata budgets with model context windows (2% of context window, capped at 4,000 tokens).  
   [openai/codex PR #34626](https://github.com/openai/codex/pull/34626)

10. **#34625** – Fix Windows TUI navigation key handling caused by virtual terminal input mode interference.  
    [openai/codex PR #34625](https://github.com/openai/codex/pull/34625)

**Highlights:** The HTTP client migration series (#34630, #34645, #34643) is a significant architectural cleanup. Windows‑specific fixes (#34629, #34624, #34625) directly address the runaway process and sandbox issues reported in the top bugs.

## Feature Request Trends
- **Windows process lifecycle control** – Users repeatedly ask for the ability to limit or debounce Git polling, prevent empty `.agent`/`.git` folder creation, and terminate orphaned `taskkill.exe` processes.
- **Sandbox reliability and diagnostics** – The *bwrap RTM_NEWADDR* regression and Windows sandbox elevation failures highlight a demand for transparent sandbox logs and automatic fallback modes.
- **Cross‑platform consistency** – Several issues note that the same project works smoothly in the VS Code extension but triggers storms in the standalone Windows app.
- **Sub‑agent & memory support** – The experimental paginated thread history and sub‑agent features from v0.145.0 are the most anticipated; users want better integration with custom MCP servers and multi‑repo workspaces.

## Developer Pain Points
- **Uncontrolled Git background processes** – Spawning hundreds of `git status`, `git add -A`, and `git ls-files` commands per minute, often in an infinite loop, is the single largest pain point. Users report system‑wide freezes, WMI provider exhaustion, and Windows Defender high‑CPU alerts.
- **Orphan `taskkill` / `conhost` storms** – The desktop app enters a cleanup loop that leaves hundreds of `taskkill.exe` and `conhost.exe` processes alive, exhausting kernel objects and making the machine unresponsive.
- **Sandbox breakage after updates** – Linux users face broken sandbox execution (bwrap) after minor CLI updates, with no clear downgrade path.
- **Empty `.git` directory creation** – The app creates empty `.git` folders in non‑Git workspaces, triggering repeated scanning and Defender interference.
- **Silent tool failures** – `apply_patch` fails silently on Windows when installed via MSIX, and Computer Use plugins report “not active” due to session model conflicts.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*