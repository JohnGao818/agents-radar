# AI CLI Tools Community Digest 2026-07-28

> Generated: 2026-07-28 02:07 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Data as of 2026-07-28**

---

## 1. Ecosystem Overview

The AI CLI tools space is maturing rapidly, with both major players—Claude Code (Anthropic) and OpenAI Codex—experiencing high community engagement but diverging in iteration velocity. Claude Code shows signs of a stabilization phase: no new releases in the last 24 hours, with community attention concentrated on long-standing issues (Windows ARM64 Cowork VM failures, account sync requests). In contrast, OpenAI Codex continues aggressive weekly alpha iteration (two releases today alone), actively shipping PRs targeting its most critical Windows stability problems. Both platforms face mounting pressure on Windows platform support, session management reliability, and billing transparency—suggesting these are industry-wide growing pains rather than tool-specific deficiencies. The overall landscape indicates a shift from feature velocity toward reliability and cross-platform parity as tools become production-critical for development teams.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Hot Issues (last 24h)** | 10 | 10 |
| **Key PRs (last 24h)** | 6 | 10 |
| **Releases (last 24h)** | 0 | 2 (alpha) |
| **Highest-upvoted issue** | #22648 (43 👍) — Account-level sync | #9203 (362 👍) — `/undo` restoration |
| **Most commented issue** | #40198 (66 comments) — Windows ARM64 Cowork VM | #9203 (65 comments) — `/undo` restoration |
| **Critical bugs (tracked)** | 7 high-impact bugs (#40198, #51143, #54186, etc.) | 6 high-impact bugs (#32149, #34133, #30712, etc.) |
| **Windows-specific issues** | 3 (#40198, #51143, #78946) | 5 (#32149, #34133, #30712, #35352, #26990) |

**Observation:** Codex maintains a higher release cadence and PR throughput, while Claude Code has fewer but higher-traffic single issues—indicating more concentrated community pain points and longer resolution cycles.

---

## 3. Shared Feature Directions

Both communities are independently converging on a similar set of requirements:

| Requirement | Claude Code | OpenAI Codex |
|---|---|---|
| **Cross-device session continuity** | #11455 (24 👍) — Session handoff/resume across instances | #25319 (48 👍) — Workspace-scoped sessions tied to projects |
| **Settings/state sync** | #22648 (43 👍) — Account-level settings sync | #26990 — Crash-safe local state on Windows |
| **Undo/rollback mechanism** | Not explicitly requested (though data-loss bugs exist) | #9203 (362 👍, **most upvoted** across both tools) |
| **Windows platform stability** | 3 critical bugs (ARM64 VM, blank screen, login loop) | 5 critical bugs (GPU crashes, sandbox failure, power-loss corruption) |
| **Data loss prevention** | #54186 — Session history lost on VS Code restart | #26990 — Local state lost after power loss |
| **Billing transparency / usage monitoring** | #81703 — Mass billing incident; #79773 — Limit confusion | #30452 — Usage limit visibility; #35463 — Subagent quota drain |

**Key Signal:** Developers across both ecosystems are demanding **production-grade reliability**—session persistence, crash safety, undo capabilities, and predictable billing. Feature novelty alone is no longer sufficient; operational robustness is now table stakes.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary user focus** | Professional developers, systems integrators, plugin developers | Individual developers, CI/CD workflows, VS Code users |
| **Architecture emphasis** | Cowork VM isolation, worktree sessions, plugin/hook ecosystem | Sandbox-based execution, MCP integration, embedded browser |
| **Language ecosystem** | Hookify-based plugin system (T3 trust tensors, R6 audit trails) | Rust-based CLI, subagent architecture, crossterm TUI |
| **Model behavior concerns** | Role-playing personality shifts (#81463), instruction-following failures (#57902) | Capacity errors abusing subagent quotas (#35463), model availability churn (#34027) |
| **Release philosophy** | Conservative; longer gaps between releases, focus on stability | Aggressive alpha iteration; frequent small releases (2 today) |
| **Windows support maturity** | **Weaker** — Cowork VM ARM64 non-functional, blank screen, login loops | **Weak but improving** — GPU crash cluster being actively patched (6+ PRs this cycle) |
| **Session/model management** | `/resume` with session naming, worktree isolation (currently broken) | Thread-based history, workspace scoping requested, subagent picker |
| **Billing model** | Plan allowance + usage credits (incident-prone) | Pro subscription, quota-based, capacity error vulnerability |

**Takeaway:** Claude Code positions itself as a **developer platform** (plugins, governance, enterprise audit trails), while Codex positions as a **rapid-iteration assistant** (sandbox safety, subagents, frequent updates). Both have distinct appeal—Claude for teams needing governance, Codex for individual productivity.

---

## 5. Community Momentum & Maturity

| Tool | Velocity | Community Engagement | Maturity Level |
|---|---|---|---|
| **Claude Code** | Low release cadence; 6 PRs today (mostly small fixes) | High engagement per issue (66 comments on top bug), feature requests well-organized | **Mature but plateauing** — core features stable, but pain points persist with no rapid resolution |
| **OpenAI Codex** | High release velocity (2 alpha releases today, 10 PRs) | Very high engagement (#9203: 362 👍 in 65 comments within hours), diverse issue types | **Rapidly maturing** — shipping fixes aggressively, but introducing new bugs (alpha quality) |

**Community Dynamics:**
- **Claude Code** community is more patient and enterprise-oriented—long discussion threads on feature proposals (e.g., #11455 session handoff with systems integrator detail), lower frustration in tone.
- **OpenAI Codex** community is louder and more urgent—the `#9203` undo request exploded with 362 upvotes today, indicating a critical missing workflow primitive. The frequent alpha releases create a cycle of "fix one bug, break another" that keeps community engaged but frustrated.

---

## 6. Trend Signals

1. **Windows GPU instability is the #1 cross-tool pain point.** Both tools have multiple crashes caused by GPU process failures (SwiftShader, Vulkan DLL blocking). This suggests a common upstream dependency issue that platform vendors (OpenAI/Anthropic) need to address holistically. Developers on Windows are clearly second-class citizens in current AI CLI tooling.

2. **Session/workflow continuity is the next frontier.** Developers want to move between devices, resume interrupted sessions, and keep context across projects. Both tools are receiving demands for workspace-scoped memory (#25319) and session handoff (#11455). This points toward "AI-assisted development environments" becoming as persistent as IDEs themselves.

3. **Undo/rollback is a critical missing primitive.** Codex's #9203 (362 👍) signals that AI-generated file modification without revert capability is a major trust barrier. As AI tools gain write access to codebases, the ability to safely reverse actions becomes non-negotiable. Developers expect **git-like safety** from AI assistants.

4. **Model behavior regressions erode trust.** Reports of personality shifts (#81463 on Claude) and instruction-following failures (#57902) suggest that long-context model behavior is still unpredictable. Combined with capacity errors on Codex, users are questioning model reliability for complex, long-running tasks.

5. **Billing model design influences trust.** Both platforms have incidents where credits were consumed unexpectedly (#81703 on Claude, #35463 on Codex). As AI CLI tools become essential daily drivers, developers need transparent, predictable metering—not surprise charges.

6. **Plugin/ecosystem extensibility is gaining traction.** Claude Code's plugin architecture (hookify, web4-governance, security-guidance) and Codex's MCP integration point toward a future where AI CLIs are platforms, not single-purpose tools. Governance, auditing, and compliance hooks (T3 trust tensors, R6 workflows) are emerging as enterprise requirements.

---

**Recommendation for technical decision-makers:** If you need enterprise governance, multi-developer session continuity, and plugin extensibility, Claude Code's ecosystem is more mature—but beware its Windows limitations and slower bug fix cycles. If you prioritize rapid iteration, undo capability, and are willing to tolerate alpha instability, Codex's velocity may serve you better. Both tools require Windows users to budget for platform friction.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

**Data snapshot:** 2026-07-28 — Based on the top 20 most-commented PRs and top 15 most-commented Issues in the [anthropics/skills](https://github.com/anthropics/skills) repository.

---

## 1. Top Skills Ranking

The following PRs represent the most-discussed Skill submissions (new additions or major improvements) by community comment activity. All remain **open** unless noted.

### 1.1. [document-typography (#514)](https://github.com/anthropics/skills/pull/514)
**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents.  
**Discussion highlights:** The author argues typography defects affect “every document Claude generates” yet are rarely requested by users, making this an essential silent-quality skill. Low contestation; comments focus on edge cases and sample triggers.  
**Status:** Open, last updated 2026-03-13.

### 1.2. [ODT skill (#486)](https://github.com/anthropics/skills/pull/486)
**Functionality:** Create, fill, read, and convert OpenDocument Format files (.odt, .ods). Includes template filling and ODT→HTML parsing.  
**Discussion highlights:** Community interest in LibreOffice/ISO standard document support. Some discussion about scope overlap with existing DOCX skill.  
**Status:** Open, last updated 2026-04-14.

### 1.3. [testing-patterns (#723)](https://github.com/anthropics/skills/pull/723)
**Functionality:** Covers the full testing stack—unit (AAA pattern), React component testing (Testing Library), integration, E2E, and property-based testing. Emphasizes “Testing Trophy” philosophy.  
**Discussion highlights:** Positive reception; reviewers asked for coverage of mocking strategies and test isolation.  
**Status:** Open, last updated 2026-04-21.

### 1.4. [pyxel skill (#525)](https://github.com/anthropics/skills/pull/525)
**Functionality:** Wraps the [pyxel-mcp](https://github.com/kitao/pyxel-mcp) server for retro/pixel-art game development with Pyxel engine. Workflow: write → run_and_capture → inspect → iterate.  
**Discussion highlights:** From the original Pyxel author. Minimal debate; community excited about game-dev use case.  
**Status:** Open, last updated 2026-07-15.

### 1.5. [self-audit (#1367)](https://github.com/anthropics/skills/pull/1367)
**Functionality:** An output-quality gate that first mechanically verifies all claimed files exist, then performs a four-dimension reasoning audit (priority-ordered by damage severity).  
**Discussion highlights:** Proposes a universal skill for any project/stack. Active discussion on trade-offs between thoroughness and token consumption.  
**Status:** Open, last updated 2026-07-02.

### 1.6. [plan-file-hygiene (#1479)](https://github.com/anthropics/skills/pull/1479)
**Functionality:** Addresses the problem of accumulating planning artifacts (`.plan.md`, scratch files) with no lifecycle management. Cleans up stale files and enforces naming conventions.  
**Discussion highlights:** Originates from [Issue #1417](https://github.com/anthropics/skills/issues/1417). Strong framing around lifecycle gaps; contributors offered to hand off authorship.  
**Status:** Open, last updated 2026-07-27.

### 1.7. [skill-quality-analyzer + skill-security-analyzer (#83)](https://github.com/anthropics/skills/pull/83)
**Functionality:** Two meta-skills: one evaluates skills across five quality dimensions (structure, docs, examples, security, portability); the other performs security analysis of skill behavior.  
**Discussion highlights:** Recognised as a foundation for skill marketplace quality standards. Some concern about false positives in security analysis.  
**Status:** Open, last updated 2026-01-07.

### 1.8. [frontend-design improvement (#210)](https://github.com/anthropics/skills/pull/210)
**Functionality:** Revises the existing frontend-design skill for clarity, actionability, and internal coherence—ensuring every instruction is executable within a single conversation.  
**Discussion highlights:** Example of community self-improvement of bundled skills. Discussants debated the level of prescriptive vs. generative guidance.  
**Status:** Open, last updated 2026-03-07.

---

## 2. Community Demand Trends

From the top Issues, three clear demand clusters emerge:

### 2.1. Security and Trust Boundaries
- [Issue #492](https://github.com/anthropics/skills/issues/492) (43 comments, 2👍) warns that community skills under the `anthropic/` namespace impersonate official skills, creating a trust boundary vulnerability.  
- [Issue #1175](https://github.com/anthropics/skills/issues/1175) raises concerns about embedding access-control logic inside SKILL.md files when handling SharePoint Online documents.  
- Implicit demand: official governance mechanisms (attestation, signing, least-privilege skill execution).

### 2.2. Tooling Reliability (Skill Creator)
- [Issue #556](https://github.com/anthropics/skills/issues/556) (12 comments, 7👍) and related issues [#1169](https://github.com/anthropics/skills/issues/1169), [#1061](https://github.com/anthropics/skills/issues/1061) report `run_eval.py` always returning 0% recall on Windows and Linux. Multiple PRs now aim to fix this—indicating a critical pain point for skill authors.  
- [Issue #202](https://github.com/anthropics/skills/issues/202) calls for the skill-creator skill itself to be rewritten as an operational skill rather than developer documentation.

### 2.3. New Skill Directions (Anticipated)
- **Compact symbolic memory** ([Issue #1329](https://github.com/anthropics/skills/issues/1329), 9 comments): A skill for long-running agents to maintain state using compact symbolic notation instead of verbose prose.  
- **Agent governance** ([Issue #412](https://github.com/anthropics/skills/issues/412), 6 comments): Safety patterns—policy enforcement, threat detection, audit trails.  
- **Reasoning quality gate pipeline** ([Issue #1385](https://github.com/anthropics/skills/issues/1385), 3 comments): Pre-task calibration → Adversarial review → Delivery verification.  
- **Org-wide skill sharing** ([Issue #228](https://github.com/anthropics/skills/issues/228), 16 comments, 8👍): Users want a built-in sharing library instead of manual file transfer.  
- **MCP exposure for skills** ([Issue #16](https://github.com/anthropics/skills/issues/16), 4 comments): Converting skills into MCP-compatible APIs for tool calling.

---

## 3. High-Potential Pending Skills

These PRs are actively commented, not yet merged, and show signs of imminent landing or continued development:

| PR | Skill | Last Updated | Why High Potential |
|----|-------|--------------|-------------------|
| [#1298](https://github.com/anthropics/skills/pull/1298) | skill-creator fix (run_eval 0% recall) | 2026-06-23 | Directly addresses Issue #556—most-upvoted bug. Multiple authors converging on solution. |
| [#1367](https://github.com/anthropics/skills/pull/1367) | self-audit | 2026-07-02 | Recent, well-framed, complementary to Issue #1385 proposal. |
| [#1479](https://github.com/anthropics/skills/pull/1479) | plan-file-hygiene | 2026-07-27 | Very new; author offers to hand off—indicates community momentum. |
| [#525](https://github.com/anthropics/skills/pull/525) | pyxel retro game dev | 2026-07-15 | Maintained by original tool author; high trust and clarity. |
| [#1099](https://github.com/anthropics/skills/pull/1099) | skill-creator Windows fix (subprocess) | 2026-05-24 | Narrow, targeted fix with clear reproduction steps. |
| [#1323](https://github.com/anthropics/skills/pull/1323) | skill-creator trigger detection fix | 2026-06-25 | Parallel fix to #1298; may be superseded but shows active interest. |

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for a reliable skill-development toolchain (fixing `run_eval.py` and Windows compatibility) coupled with output-quality governance skills (typography, testing patterns, self-audit, plan hygiene) that move Claude from “helpful assistant” to “production-ready software partner.”**

---

# Claude Code Community Digest — 2026-07-28

## Today’s Highlights

No new releases landed in the last 24 hours, but the community remains vocal about two long-standing pain points: **account‑level settings sync** (43 👍, 24 comments) and **session handoff/continuity** (24 👍, 23 comments). A critical Windows ARM64 Cowork VM startup bug (#40198) continues to attract attention with 66 comments, while a fresh billing‑incident issue (#81703) and a concerning model‑behavior report (#81463) add pressure on the Anthropic team.

## Releases

*None in the last 24 hours.*

## Hot Issues

1. **[#40198 – Cowork VM fails to start on Windows ARM64 (Snapdragon)](https://github.com/anthropics/claude-code/issues/40198)**  
   *Comments: 66 · 👍 13*  
   The top‑traffic issue today. Windows ARM64 users on Snapdragon devices cannot start the Cowork VM. A long thread (since March) with no official resolution yet; community frustration is high.

2. **[#22648 – Account‑level settings sync across devices](https://github.com/anthropics/claude-code/issues/22648)**  
   *Comments: 24 · 👍 43*  
   Most‑upvoted open feature request. Users with multiple machines want `~/.claude/` settings synced server‑side. Repeatedly requested (referenced issues from 2025).

3. **[#11455 – Session Handoff / Continuity Support](https://github.com/anthropics/claude-code/issues/11455)**  
   *Comments: 23 · 👍 24*  
   A systems integrator’s detailed proposal for resuming sessions across different instances. No official comment yet; community is actively discussing use cases.

4. **[#51143 – Persistent blank screen on Windows (Desktop)](https://github.com/anthropics/claude-code/issues/51143)**  
   *Comments: 18 · 👍 20*  
   Cowork unusable after multiple reinstalls. Blank/white screen on Windows. Affects many users; no fix identified.

5. **[#54186 – Local session history disappears after VS Code restart](https://github.com/anthropics/claude-code/issues/54186)**  
   *Comments: 13 · 👍 14*  
   Data‑loss bug for VS Code extension users. Session history is cleared on restart. High priority due to impact on developer workflow.

6. **[#81463 – Claude flips to role‑playing as abusive/narcissist in long conversations](https://github.com/anthropics/claude-code/issues/81463)**  
   *Comments: 9 · 👍 1*  
   A concerning model‑behavior report. The user speculates the LCR (likely “long‑context regulation”) triggers a personality shift. Low upvotes but high sensitivity.

7. **[#61172 – `/clear` inherits previous session name](https://github.com/anthropics/claude-code/issues/61172)**  
   *Comments: 7 · 👍 12*  
   Sesssion naming bug: `/clear` reuses the old name, creating duplicate entries in `/resume`. Simple to reproduce; impacts session organisation.

8. **[#81703 – July 17 mass billing incident: usage credits charged despite plan allowance](https://github.com/anthropics/claude-code/issues/81703)**  
   *Comments: 7 · 👍 0*  
   An acknowledged incident on July 17 where paid usage credits were consumed even when plan allowance remained. User disputes $704.71 in charges. Financial urgency.

9. **[#79366 – Worktree sessions reuse existing worktree directory](https://github.com/anthropics/claude-code/issues/79366)**  
   *Comments: 6 · 👍 4*  
   Worktree isolation fails: new sessions land in an old worktree directory instead of creating a fresh one. Breaks the isolation promise.

10. **[#78946 – Login loop on Windows](https://github.com/anthropics/claude-code/issues/78946)**  
    *Comments: 6 · 👍 3*  
    Windows users stuck in an infinite login loop after authentication. High friction for new users.

## Key PR Progress

1. **[#81673 – Fix devcontainer firewall setup when optional domain fails to resolve](https://github.com/anthropics/claude-code/pull/81673)**  
   *Author: ozdemirsarman*  
   Resolves #55623. `init-firewall.sh` now gracefully handles unresolvable domains (e.g., `statsig.anthropic.com`) instead of aborting the entire firewall setup. Prevents half‑populated ipsets.

2. **[#81672 – Fix hookify package import independent of install directory name](https://github.com/anthropics/claude-code/pull/81672)**  
   *Author: ozdemirsarman*  
   Fixes #69665 and #81448. Hook entry points now use a dynamic path rather than relying on the directory being named exactly `hookify`. Enables correct marketplace installs.

3. **[#81670 – Quote `${CLAUDE_PLUGIN_ROOT}` in hook commands, prefix hookify examples](https://github.com/anthropics/claude-code/pull/81670)**  
   *Author: ozdemirsarman*  
   Fixes #78490 and #79143. Two independent bugs: unquoted path variables break hooks when the path contains spaces, and missing `hookify` prefixes in example commands leave the plugin broken.

4. **[#20448 – Add web4‑governance plugin for AI governance with R6 workflow](https://github.com/anthropics/claude-code/pull/20448)**  
   *Author: dp-web4*  
   A long‑running PR (since January 2026) that adds a plugin providing T3 trust tensors, entity witnessing, and R6 audit trails. Still open; no recent maintainer activity.

5. **[#81576 – Fix security‑guidance plugin entry in plugins/README.md](https://github.com/anthropics/claude-code/pull/81576)**  
   *Author: Woohyeon-Hong*  
   Corrects documentation: the security‑guidance plugin has 25 patterns and no `PreToolUse` hook, contrary to the old entry claiming 9 patterns and one hook.

6. **[#81540 – Fix #80705: Usage leak](https://github.com/anthropics/claude-code/pull/81540)**  
   *Author: mazenfarkouh580-netizen*  
   Automated contribution (Atlas 2, $200 bounty). Claims to fix a usage leak bug. Tests and repository validation were run. Open for review.

## Feature Request Trends

- **Cross‑device sync & portability** – Dominating the wishlist: account‑level settings sync (#22648), session handoff (#11455), and separate portable configuration from machine‑local state (#81392). Users want a stable project identity for auto‑memory across different home directories (#81391).
- **Localization (i18n)** – Request to translate the CLI UI into other languages (#65963).
- **Remote‑control parity** – Plan‑approval actions available on mobile/remote surfaces (#81393).
- **UI polish** – Distinguishable markdown heading levels (#70368), display current working directory in prompt (#70132).

## Developer Pain Points

- **Windows platform instability** – Multiple reports: ARM64 Cowork VM fails (#40198), blank screen (#51143), login loop (#78946), console flashes from child processes (#70200), GPU crash on opening browser pane (#81398). Windows users are clearly underserved.
- **Session management fragility** – History disappears on VS Code restart (#54186), `/clear` duplicates session names (#61172), read/unread state is per‑device not per‑account (#81568), worktree isolation breaks (#79366).
- **Billing & usage confusion** – The July 17 billing incident (#81703) and “Max 20x” upgrade not reflected in weekly limits (#79773) erode trust in metering.
- **Model behavior regressions** – Reports of role‑playing personality shifts (#81463) and recurring instruction‑following failures (#57902) indicate ongoing concerns with Opus 4.7/4.8.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-07-28

## Today's Highlights
Two new alpha releases of the Rust-based Codex CLI (`v0.146.0-alpha.12` and `v0.146.0-alpha.13`) landed in the last 24 hours. Meanwhile, the community is actively discussing a long-requested `/undo` feature, and a cluster of Windows GPU crash issues dominates the bug tracker, with multiple high‑priority patches merged to address process hangs and sandbox failures.

## Releases
- **rust-v0.146.0-alpha.12** and **rust-v0.146.0-alpha.13** – Minor alpha iterations; no detailed changelog was provided beyond “Release 0.146.0-alpha.x”. These likely include the fixes from today’s PR batch (Windows interrupt handling, SQLite path corrections, etc.).

## Hot Issues
1. **#9203 – [enhancement] Please make `/undo` back**  
   *Comments: 65 | 👍: 362*  
   Community strongly supports restoring the `/undo` command to revert unintended file modifications and deletions. Many users report data loss when Codex acts on uncommitted changes.  
   [GitHub](https://github.com/openai/codex/issues/9203)

2. **#32149 – [bug] Windows setup fails before UAC prompt**  
   *Comments: 27*  
   Both installer options are non‑functional on Windows, blocking new users. Pro subscription affected.  
   [GitHub](https://github.com/openai/codex/issues/32149)

3. **#34133 – [bug] Page.captureScreenshot crashes GPU process after Code Integrity Event 3033**  
   *Comments: 24*  
   In‑app browser screenshot capture leads to GPU process termination when Windows Code Integrity blocks the bundled `vk_swiftshader.dll`. Causes freezes and app crashes.  
   [GitHub](https://github.com/openai/codex/issues/34133)

4. **#32094 – [bug] App crashes when embedded browser opens WebCodecs/canvas pages**  
   *Comments: 18*  
   Another Windows GPU‑related crash, tracked by the browser team.  
   [GitHub](https://github.com/openai/codex/issues/32094)

5. **#25319 – [enhancement] Scope Codex VS Code chats to the current workspace/project**  
   *Comments: 18 | 👍: 48*  
   Users want session history to be tied to a specific workspace, avoiding chat clutter from unrelated projects.  
   [GitHub](https://github.com/openai/codex/issues/25319)

6. **#30712 – [bug] Windows app injects split writable roots, causing `apply_patch` to fail**  
   *Comments: 15 | 👍: 13*  
   The safe editing path is broken on Windows because of incorrect sandbox root configuration, forcing agents to bypass the sandbox.  
   [GitHub](https://github.com/openai/codex/issues/30712)

7. **#35352 – [bug] Desktop exits when GPU process crashes and unsigned SwiftShader fallback is blocked**  
   *Comments: 12*  
   Another Windows GPU crash variant – app quits entirely when the embedded browser fails.  
   [GitHub](https://github.com/openai/codex/issues/35352)

8. **#26990 – [bug] Windows Desktop local state not crash‑safe after power loss**  
   *Comments: 8*  
   Pins, projects, and configuration are lost when the system loses power; timestamps become corrupted.  
   [GitHub](https://github.com/openai/codex/issues/26990)

9. **#15807 – [bug] VSCode plugin: cannot open multiple windows via `Codex: New Codex Agent`**  
   *Comments: 6 | 👍: 5*  
   API subscription users report the command fails silently when trying to spawn multiple agent windows.  
   [GitHub](https://github.com/openai/codex/issues/15807)

10. **#33088 – [bug] App crashes when opening Settings**  
    *Comments: 6*  
    Occurs on macOS; user reports the app immediately crashes upon navigating to the Settings page.  
    [GitHub](https://github.com/openai/codex/issues/33088)

## Key PR Progress
1. **#35695 – Honor configured SQLite home in the logs client**  
   Fixes a bug where `just log` read the wrong database when `sqlite_home` was customised.  
   [GitHub](https://github.com/openai/codex/pull/35695)

2. **#35693 – Refresh the subagent picker in the background**  
   Prevents input delay when opening the subagent picker by caching metadata off the main thread.  
   [GitHub](https://github.com/openai/codex/pull/35693)

3. **#35691 – Include empty‑preview threads in relationship listings**  
   Ensures threads without preview text appear in parent/child relationship queries (but not in the global list).  
   [GitHub](https://github.com/openai/codex/pull/35691)

4. **#31817 – Update models.json**  
   Automated update to the model registry.  
   [GitHub](https://github.com/openai/codex/pull/31817)

5. **#35689 – Preserve item timestamps in thread history projections**  
   Adds optional start/completion timestamps to history items, improving accuracy of time‑related metadata.  
   [GitHub](https://github.com/openai/codex/pull/35689)

6. **#35688 – Point crossterm patch to the OpenAI OSS fork**  
   Moves the `crossterm` dependency to the OpenAI fork for maintainability.  
   [GitHub](https://github.com/openai/codex/pull/35688)

7. **#35685 – Load cloud‑managed profiles for `codex sandbox`**  
   Enables sandbox to fetch and apply cloud‑managed permission profiles when `--include-managed-config` is passed.  
   [GitHub](https://github.com/openai/codex/pull/35685)

8. **#35678 – Preserve paginated thread metadata across resumes**  
   Fixes a bug where resuming a thread could overwrite its title/preview because only a bounded rollout suffix was used. Now uses SQLite‑backed metadata.  
   [GitHub](https://github.com/openai/codex/pull/35678)

9. **#35675 – Prepare MCP and plugin recommendations concurrently**  
   Reduces latency by running MCP discovery and endpoint plugin recommendations in parallel.  
   [GitHub](https://github.com/openai/codex/pull/35675)

10. **#35670 – Raise the Windows exec yield floor to 10 seconds**  
    Increases the minimum `exec_command` yield time on Windows to prevent premature timeouts, and adjusts integration tests accordingly.  
    [GitHub](https://github.com/openai/codex/pull/35670)

## Feature Request Trends
- **Undo/rollback (🚩 #9203)** – The most upvoted request: bring back a reliable `/undo` command to revert accidental changes, especially for files not tracked by git.
- **Workspace‑scoped sessions (🚩 #25319, #20115)** – Users want conversations to be tied to specific projects, with the ability to archive/export full histories.
- **Automatic retry on capacity errors (🚩 #22390, #32020, #31278, #33878)** – Multiple enhancement requests ask Codex to auto‑retry or queue tasks when the selected model is temporarily at capacity, instead of presenting the user with a dead‑end message.
- **Usage limit visibility (🚩 #30452)** – Developers want easier access to token/rate usage information during active sessions, without navigating away.

## Developer Pain Points
1. **Windows GPU instability** – A series of issues (#34133, #32094, #35352, #33732) show that the embedded browser’s GPU process crashes frequently on Windows due to Code Integrity blocking native Vulkan/SwiftShader DLLs. This causes the entire app to freeze or exit.
2. **Sandbox and file‑editing failures on Windows** – Issues #30712 and #33732 highlight that the sandbox’s writable root configuration breaks `apply_patch` and can hang the entire sandbox setup.
3. **Capacity errors killing long‑running tasks** – The model‑at‑capacity error (#33878, #31278, #35463) often aborts hours of work, and the new `gpt-5.6-sol` model’s disappearance (#34027) caused confusion.
4. **Data loss after crash or power loss** – Issue #26990 reveals that the Windows app’s local state (pins, projects, config) is not crash‑safe, leading to frustrating resets.
5. **Subagent quota drain** – Issue #35463 warns that subagents can consume an entire week’s quota overnight, indicating a bug in usage counting.
6. **UI freezes and input lag** – Several reports (#34450, #25319) describe severe lag on Windows and macOS when typing or navigating, often linked to background snapshot fan‑out (#32722) or TUI focus events (#35649).

---

*This digest is generated from openai/codex GitHub data; all times in UTC.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*