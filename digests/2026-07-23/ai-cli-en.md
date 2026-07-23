# AI CLI Tools Community Digest 2026-07-23

> Generated: 2026-07-23 02:23 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Ecosystem — 2026-07-23

## Ecosystem Overview

Both Claude Code and OpenAI Codex communities are actively engaged, but the character of that engagement diverges significantly. Claude Code shipped a single polished release (v2.1.218) with substantive UX improvements, while Codex landed four rapid-fire Rust alpha releases, signalling ongoing client-side iteration. Across both ecosystems, process/resource management and platform-specific stability are the dominant pain points—users are demanding production-grade reliability rather than new features. The most upvoted feature requests in both communities (99 👍 on Claude Code for cross-session context sharing; 151 👍 on Codex for user-configurable auto-resolution) point to a shared desire for **user-controlled, stateful workflows** that span sessions and tools without surprise behavior.

## Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Releases (last 24h)** | v2.1.218 (1 release) | rust-v0.146.0-alpha.1 through alpha.4 (4 releases) |
| **Hot Issues tracked** | 10 selected; highest engagement: #80002 (56 comments, 25 👍), #39523 (33 comments, 18 👍) | 10 selected; highest engagement: #28969 (53 comments, 151 👍), #12491 (27 comments) |
| **Key PRs tracked** | 10 (3 merged, 6 open, 1 closed) | 10 (all open/merged; no rejections tracked) |
| **Release maturity** | Stable, single release with changelog | Rapid alpha churn, no detailed changelogs |
| **Community engagement intensity** | High: long-running meta issues (9 months), duplicates, sustained voting | High: top issues have 50+ comments, strong upvote concentration |

## Shared Feature Directions

The following requirements appear **independently in both communities**, suggesting genuine unmet needs in the AI CLI tool category:

- **Cross-session context persistence**: Claude Code #13843 (99 👍) wants to transfer planning from web UI to CLI; Codex #25319 (47 👍) wants per-workspace chat isolation. Both communities want conversations to survive session boundaries and tool switches.
- **Process/resource management**: Claude Code has auto-compact failures (#80196) and transcript loss (#80405); Codex has zombie MCP processes (#12491, 1300+ zombies) and file-descriptor leaks (#26984, cumulative EMFILE). **Reliable lifecycle management is the #1 stability gap across both tools.**
- **Platform-specific regressions**: macOS Filesystem extension dispatch (#80002) in Claude Code parallels Windows sandbox failures (#22428) and process storms (#33778) in Codex—both tools ship platform bugs that block core workflows for significant user segments.
- **User control over automation timing**: Claude Code users want mid-task steering parity (#71726); Codex users want to disable or adjust the 60-second auto-resolve timer (#28969, 151 👍). Both communities reject opaque, non-configurable timeouts.
- **Task/structured workflow reliability**: Claude Code reports Task/Todo tools vanishing mid-session (#80401, #80213); Codex reports hooks breaking after desktop updates (#21639). Structured automation workflows are regressing in both tools.

## Differentiation Analysis

**Feature focus**: Claude Code leans into **plugin extensibility and context management**—the `/planwith` command (#18217), account profiles plugin (#80326), and twilight design-workflow plugin (#80008) all extend the tool’s surface area via plugins. Codex focuses on **multi-agent durability and Rust client performance**—thread pinning (#34840), batch plugin metadata (#34851), and waking sleeping agent threads (#34852) target concurrency and responsiveness.

**Target users**: Claude Code appears to target **structured planning-first workflows** (skills, tasks, plan modes, background subagents) suitable for enterprise or disciplined development teams. Codex targets **proactive automation users** who rely on hooks, background agents, and MCP integrations—developers who want the tool to act, not just plan.

**Technical approach**: Claude Code v2.1.218 uses **background subagents** to keep conversation history clean; Codex alpha releases emphasize **native Rust client iteration** for performance. Claude Code’s ecosystem is plugin-centric; Codex’s is hook- and MCP-centric. The divergence in extensibility models (plugins vs. hooks/MCP) creates very different upgrade risk profiles and community contributions.

**Key strategic gap for each**: Claude Code’s permissions system is fundamentally broken (#39523, 9-month meta, 12+ duplicates)—a trust issue that undermines its structured workflow value prop. Codex has a Windows instability cluster that is disproportionate to its user base—sandbox failures, process storms, token exchange errors—indicating a systematic testing gap on that platform.

## Community Momentum & Maturity

**Claude Code** has a **more vocal, persistent community**: meta-issues survive 9+ months with sustained duplicates, feature requests reach 99 👍, and platform-specific bugs get 56 comments. The community is deeply invested and expects enterprise-grade reliability from a tool that explicitly targets structured workflows. The PR pipeline shows both autonomous-agent contributions (#80241) and experimental new features (#80008), indicating a healthy contributor base. **Maturity indicator**: high; the tool is stable but its core trust mechanisms (permissions, task tools) show systemic fractures.

**OpenAI Codex** is **iterating faster but with more surface churn**: four alpha releases in one day suggests active development, but the lack of changelogs and the persistence of critical bugs (zombie MCP processes open 5 months; hooks regression open 3 months) point to velocity at the expense of polish. The 151-upvote auto-resolution request indicates a passionate user base that feels unheard. **Maturity indicator**: medium; the Rust client is getting serious investment, but GUI and hook reliability lag behind.

**Community health warning**: Both tools have issues with >50 comments that remain unresolved for months. The industry norm for developer tools at this scale would be a 30–60 day resolution cadence for high-severity bugs; both tools exceed that window for their most painful issues.

## Trend Signals

1. **Process lifecycle is the new reliability frontier**: Four separate severe resource-leak/persistence issues across both tools. As AI CLI tools adopt long-running agents, subagents, and MCP integrations, **process lifecycle management** (reaping, fd cleanup, zombie prevention) has become the single largest stability gap. Developers building complementary tooling should prioritize clean teardown and monitoring.

2. **Cross-platform testing disparity is costing users**: Both tools have platform-specific bugs (macOS, Windows, Linux) that block core workflows. The fact that Claude Code’s Filesystem extension never dispatches on macOS (#80002) or that Codex’s Windows sandbox consistently fails (#22428) suggests **platform-specific CI/CD gaps**. Developers evaluating these tools for cross-platform teams should budget for workarounds.

3. **Users demand session state that outlives the terminal**: The convergence on cross-session context sharing (Claude Code #13843, Codex #25319) indicates that users treat AI CLI sessions as **persistent cognitive artifacts**, not ephemeral interactions. Tool designers should prioritize structured state export/import and session handoff between modalities (web ↔ CLI ↔ IDE).

4. **Plugin/MCP ecosystem creates new attack surfaces**: Both tools face issues where third-party integration points degrade core reliability—MCP zombie processes in Codex, vanishing task tools in Claude Code. **Integration durability** is becoming as important as core model quality.

5. **User trust erodes silently**: Hallucinated “verified” changes (Claude Code #80348), plan-mode violations (Codex), and silent behavior changes (Codex prerelease modes shipped in stable) all erode user confidence. The AI CLI tool sector is entering a **trust discipline phase** where predictable, honest tool behavior is the differentiator—not raw capability.

**Recommendation for developers**: If you rely on structured, repeatable workflows (planning, tasks, skills), Claude Code’s plugin ecosystem offers more scaffolding—but plan for permissions and task-tool workarounds. If you need proactive automation and multi-agent concurrency, Codex’s Rust client is receiving serious investment—but budget for Windows-specific testing and process-leak monitoring. In either case, **do not assume core reliability**; test your specific workflow path thoroughly before committing to production use.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-07-23 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Pull Requests represent the most actively discussed Skill submissions, ranked by community engagement and discussion depth.

### #1298 — Fix: `run_eval.py` always reports 0% recall *(OPEN)*
**Skill:** `skill-creator` (meta-skill for creating/optimizing other Skills)  
**Discussion highlights:** Addresses a critical bug affecting at least 10 independent reproductions (#556). The root cause spans three dimensions: the eval artifact wasn't installed as a real skill, Windows stream reading was broken, and trigger detection logic failed to match skill names correctly. The PR has become a focal point for skill-creator reliability, with parallel fixes converging across multiple contributors.  
**Status:** Open, actively iterating  
🔗 [PR #1298](https://github.com/anthropics/skills/pull/1298)

### #514 — Add `document-typography` skill *(OPEN)*
**Skill:** Typographic quality control for AI-generated documents  
**Discussion highlights:** Targets orphan word wrap (1–6 words stranded on a new line), widow paragraphs, and numbering misalignment—problems users report as pervasive across Claude's output. The community response indicates strong demand for output quality assurance that goes beyond content correctness to presentation polish.  
**Status:** Open  
🔗 [PR #514](https://github.com/anthropics/skills/pull/514)

### #486 — Add `odt` skill — OpenDocument text creation *(OPEN)*
**Skill:** Create, fill, read, and convert OpenDocument Format files (.odt, .ods)  
**Discussion highlights:** Addresses a clear gap for LibreOffice and open‑source document workflows. The skill covers template filling, ODT-to-HTML conversion, and ISO standard document formats. Discussion centers on the complexity of handling ODF's XML structure versus simpler alternatives.  
**Status:** Open  
🔗 [PR #486](https://github.com/anthropics/skills/pull/486)

### #1367 — Add `self-audit` skill — mechanical verification + reasoning quality gate *(OPEN)*
**Skill:** Two‑stage audit before delivery: file existence verification followed by a four‑dimension reasoning audit in damage‑severity priority order  
**Discussion highlights:** A universal skill applicable to any project and model. The four dimensions (soundness, completeness, consistency, safety) are evaluated with explicit severity ranking. The PR proposal has spawned a related issue (#1385) proposing a three‑gate pipeline, indicating growing community interest in output assurance.  
**Status:** Open, rapid iteration (4 updates in 5 days)  
🔗 [PR #1367](https://github.com/anthropics/skills/pull/1367)

### #723 — Add `testing-patterns` skill *(OPEN)*
**Skill:** Comprehensive testing guidance covering the full stack—philosophy (Testing Trophy model), unit tests (AAA pattern), React Testing Library, integration and E2E patterns  
**Discussion highlights:** The community has been requesting structured testing guidance for Claude's code generation. Discussion notes that the skill must balance comprehensiveness with token efficiency—a recurring tension in skill design.  
**Status:** Open  
🔗 [PR #723](https://github.com/anthropics/skills/pull/723)

### #525 — Add `pyxel` skill for retro game development *(OPEN)*
**Skill:** MCP‑server integration for the Pyxel retro game engine; covers write → run_and_capture → inspect → iterate workflow  
**Discussion highlights:** Notable for being a skills submission that integrates with an external MCP server, demonstrating the skill system's extensibility. The author is the original Pyxel creator, lending credibility. Recent updates show continued interest.  
**Status:** Open (updated 2026‑07‑15)  
🔗 [PR #525](https://github.com/anthropics/skills/pull/525)

### #83 — Add `skill-quality-analyzer` and `skill-security-analyzer` *(OPEN)*
**Skill:** Two meta‑skills evaluating skills across structure/documentation (20%), and security analysis respectively  
**Discussion highlights:** Proposes quality scoring with explicit dimension weights (creativity 25%, correctness 25%, completeness 20%, etc.). The security analyzer directly addresses the namespace trust problem later raised in Issue #492. Discussion surfaces tension between standardization and creative flexibility.  
**Status:** Open (created 2025‑11‑06, still active 2026‑01)  
🔗 [PR #83](https://github.com/anthropics/skills/pull/83)

---

## 2. Community Demand Trends

The most frequently requested new Skill directions, distilled from Issue discussions and PR rationales:

| Trend | Evidence | Signal Strength |
|---|---|---|
| **Output quality assurance / auditing** | Self‑audit (#1367), document‑typography (#514), three‑gate pipeline proposal (#1385), reasoning gate (#1367) | Highest — multiple independent proposals converging |
| **Tooling reliability (skill‑creator)** | #556, #1169, #1061, #1099, #1050, #362, #361 — a cascade of bugs in `run_eval.py`, Windows compatibility, YAML parsing | Critical mass — 7+ issues, 5+ PRs |
| **Organization‑wide sharing & governance** | #228 (org sharing), #492 (namespace security), #1175 (SPO security concerns), #189 (duplicate skill conflicts) | Growing — enterprise adoption blockers |
| **Cross‑platform & document interoperability** | ODT skill (#486), DOCX fix (#541), PDF fix (#538), typography skill (#514) | Steady — Office/open‑source format gaps |
| **Meta‑skills for skill quality** | Skill‑quality‑analyzer (#83), skill‑security‑analyzer (#83), compact‑memory (#1329) | Emerging — community maturing own standards |
| **Safety & governance patterns** | Agent‑governance proposal (#412), security namespace (#492), reasoning audit (#1367/#1385) | Nascent but high‑impact — trust boundary concerns |

**Key insight:** The community is demanding *reliability infrastructure* more than new domain‑specific skills. The top three trends all relate to making existing skills produce consistent, verifiable output.

---

## 3. High‑Potential Pending Skills

These PRs are actively discussed, not yet merged, and appear likely to land soon based on momentum and community need:

| Skill | PR | Created | Last Updated | Why It's High‑Potential |
|---|---|---|---|---|
| **skill‑creator reliability fix** | [#1298](https://github.com/anthropics/skills/pull/1298) | 2026‑06‑10 | 2026‑06‑23 | Addresses #556, #1169, #1061 — the ecosystem's most blocking bug; multiple contributors converging |
| **self‑audit (v1.3.0)** | [#1367](https://github.com/anthropics/skills/pull/1367) | 2026‑06‑28 | 2026‑07‑02 | Rapid iteration; spawned pipeline proposal (#1385); fills clear QA gap |
| **color‑expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | 2026‑06‑10 | 2026‑07‑21 | Niche but well‑specified; author is established color‑systems expert; self‑contained scope |
| **testing‑patterns** | [#723](https://github.com/anthropics/skills/pull/723) | 2026‑03‑22 | 2026‑04‑21 | Broad demand; covers full stack; complements existing code‑gen skills |
| **pyxel (retro games)** | [#525](https://github.com/anthropics/skills/pull/525) | 2026‑03‑05 | 2026‑07‑15 | External MCP integration model; original Pyxel author; sustained updates |
| **document‑typography** | [#514](https://github.com/anthropics/skills/pull/514) | 2026‑03‑04 | 2026‑03‑13 | Addresses universal pain point (typographic orphans/widows); low implementation risk |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *reliability and quality infrastructure* — fixing the skill‑creator toolchain, building output‑audit gates, and establishing trust boundaries — rather than for new domain‑specific skills, signaling that the ecosystem is maturing from a collection of experiments into a production platform requiring correctness guarantees.**

---

# Claude Code Community Digest — 2026-07-23

## Today's Highlights

Release v2.1.218 ships a notable improvement: `/code-review` now runs as a background subagent, keeping conversations clean and supporting stacked slash commands. Meanwhile, the community is buzzing about a critical macOS bug (#80002, 56 comments) where the desktop app never dispatches tool calls to the first-party Filesystem extension, and a long‑standing meta‑issue (#39523) about broken bypass‑permissions mode has resurfaced with 12 duplicates over nine months. Several reports about Task/Todo tools vanishing mid‑session or being unavailable in CLI (#80213, #80210, #80401) suggest a regression affecting structured task workflows.

## Releases

- **v2.1.218** — [Release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.218)  
  - `/code-review` now executes as a **background subagent**, so review work no longer fills the conversation history and stacked slash‑command targets remain intact.  
  - Added **screen‑reader announcements** for word and line deletions (`Option+Delete`, `Ctrl+W`, `Cmd+Backspace`).

No other releases in the last 24 hours.

## Hot Issues (10 selected)

1. **#80002 — [macOS] Desktop never dispatches `tools/call` to first‑party Filesystem extension**  
   `tools/list` succeeds, but no `tools/call` appears in any log. 56 comments, 25 👍. High severity for macOS users relying on local file access.  
   [Issue](https://github.com/anthropics/claude-code/issues/80002)

2. **#39523 — [META] Bypass permissions mode fundamentally broken (9‑month trail, 12+ duplicates)**  
   No official resolution in sight. 33 comments, 18 👍. Users report the `bypassPermissions` setting does nothing despite being enabled.  
   [Issue](https://github.com/anthropics/claude-code/issues/39523)

3. **#13843 — [Enhancement] Share conversation context from Claude.ai to Claude Code**  
   99 👍, 25 comments. The most‑upvoted feature request: users want to transfer planning context from the web interface into a CLI session seamlessly.  
   [Issue](https://github.com/anthropics/claude-code/issues/13843)

4. **#71726 — [Feature] Desktop app: inject queued messages mid‑task (CLI steering parity)**  
   In CLI you can type while Claude works; the desktop app blocks until the turn finishes. 9 comments, 16 👍.  
   [Issue](https://github.com/anthropics/claude-code/issues/71726)

5. **#78933 — [Windows] Remote Control never connects: `Cannot read properties of undefined (reading 'session_url')`**  
   8 comments, 0 👍 but multiple affected users. Desktop app fails both connect and disconnect.  
   [Issue](https://github.com/anthropics/claude-code/issues/78933)

6. **#77966 — [Linux/IntelliJ] OAuth loop: state parameter dropped after re‑authentication redirect**  
   7 comments, 6 👍. A cross‑platform auth bug that makes CLI login unavailable on Linux.  
   [Issue](https://github.com/anthropics/claude-code/issues/77966)

7. **#80348 — Fable 5 hallucinates “verified” changes while target is unchanged**  
   Model confidently asserts a copy change was made and verified when it wasn’t. 3 comments, highlights trustworthiness concerns with new Fable models.  
   [Issue](https://github.com/anthropics/claude-code/issues/80348)

8. **#80403 — [Windows/MSIX] Webview repeatedly unresponsive → white screen (kill and reload loop)**  
   Linked to version 1.24012.1.0 rollout. Fresh report but similar to earlier blank‑screen issues (#51143 etc.).  
   [Issue](https://github.com/anthropics/claude-code/issues/80403)

9. **#80213 — Task/Todo tools unavailable in top‑level CLI session despite `CLAUDE_CODE_ENABLE_TASKS=true`**  
   Same account, same version works in Desktop CLI but not in a standalone terminal. Suggests a session‑type regression. 2 comments, 1 👍.  
   [Issue](https://github.com/anthropics/claude-code/issues/80213)

10. **#80407 — User‑level skills (`~/.claude/skills`) not available in Desktop Home/Cowork sessions**  
    New report; CLI reads custom skills, but desktop sessions use a separate Anthropic‑managed bundle. User confusion.  
    [Issue](https://github.com/anthropics/claude-code/issues/80407)

## Key PR Progress (all 10 recent PRs)

1. **#18217 — [CLOSED] feat(plugins): add `/planwith` command for inline plan mode prompts**  
   Merged. Enables `//planwith <prompt>` to start planning without a separate `/plan` toggle.  
   [PR](https://github.com/anthropics/claude-code/pull/18217)

2. **#80353 — docs(gcp): stop on checksum mismatch**  
   Hardens GCP gateway deployment script to exit when binary checksum fails. Infrastructure improvement.  
   [PR](https://github.com/anthropics/claude-code/pull/80353)

3. **#80326 — Add account profiles plugin (experimental)**  
   Manages multiple `CLAUDE_CONFIG_DIR` environments for personal/work/client accounts on one machine.  
   [PR](https://github.com/anthropics/claude-code/pull/80326)

4. **#80294 — docs: fix 1 broken link via archive.org**  
   Fixes a dead npm link in README.  
   [PR](https://github.com/anthropics/claude-code/pull/80294)

5. **#80241 — fix: [BUG] Console scrolling to top when Claude adds text**  
   Props to an autonomous agent contribution. Resolves scroll‑jump behaviour that loses user position.  
   [PR](https://github.com/anthropics/claude-code/pull/80241)

6. **#80229 — docs: fix 1 broken link via archive.org**  
   Another dead link repaired (similar to #80294).  
   [PR](https://github.com/anthropics/claude-code/pull/80229)

7. **#80196 — fix: Auto‑compact never triggers despite “100% context used”**  
   Addresses a bug where context compaction fails to fire even when the statusline reports full context.  
   [PR](https://github.com/anthropics/claude-code/pull/80196)

8. **#80195 — fix: Instantly hitting usage limits with Max subscription**  
   Likely a rate‑limiting or limits‑accounting bug for Max plan users.  
   [PR](https://github.com/anthropics/claude-code/pull/80195)

9. **#80112 — Make devcontainer firewall init resilient to DNS resolution failures**  
   Prevents transient DNS failures from aborting the entire devcontainer firewall setup.  
   [PR](https://github.com/anthropics/claude-code/pull/80112)

10. **#80008 — Add twilight plugin: spec‑first design/implement skills with durable focus stack**  
    Experimental PR demonstrating a strategy for design‑then‑implement workflows with a focus stack. Marked as requiring significant modification.  
    [PR](https://github.com/anthropics/claude-code/pull/80008)

## Feature Request Trends

- **Cross‑session context sharing** (#13843, 99 👍): Users strongly want to carry planning from Claude.ai into Claude Code without re‑explaining.
- **Desktop ↔ CLI feature parity** (#71726, #80407, #78933): Desktop users expect the same mid‑task steering, custom skills, and Remote Control reliability that CLI offers.
- **Agent session lifecycle management** (#66202, 9 👍): Ability to dismiss or mark completed background agent sessions.
- **Model plan‑mode variants** (#80359): With OpusPlan existing, users want a `FablePlan` for token‑efficient planning tasks.
- **Documentation gaps** (#80398, #80397, #80396): Multiple reports about missing or misleading docs on skills frontmatter, `context: fork` behaviour, and subagent naming restrictions.

## Developer Pain Points

- **Permissions system unreliability** — #39523 (bypass permissions never works, 9‑month meta) and #50842 (browser extension silently denies domains without approval UI) show systemic trust/control issues.
- **Task/Todo tool inconsistency** — Tools that vanish mid‑session (#80401), are missing in CLI vs Desktop (#80213), or regress silently (#80210) break structured workflows.
- **Fable model behaviour** — Hallucinated “verified” states (#80348), contradictory availability messages (#80382), and false danger classifiers on internal agent messages (#80406) erode confidence in newer models.
- **Cross‑platform regressions** — macOS Filesystem extension (#80002), Windows webview unresponsive (#80403), Windows event‑loop starvation after sleep (#80404), and Linux OAuth loop (#77966) indicate platform‑specific testing gaps.
- **Auto‑compact & memory management** — Issues like #80196 (compact never triggers) and #80405 (long assistant text blocks lost from transcripts during interrupts) point to ongoing challenges with context management.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# Codex Community Digest – 2026-07-23

## Today’s Highlights
Four Rust client alpha releases (v0.146.0-alpha.1 through alpha.4) landed in rapid succession, signalling continued iteration on the CLI’s native surface. Meanwhile, the community remains vocal about resource leaks and process management – two long-running issues around MCP zombie processes and file-descriptor exhaustion with “Too many open files” remain top-of-mind. A new bug report about Codex Ultra mode “wasting usage” without producing work is also drawing attention.

## Releases
- **rust-v0.146.0-alpha.1 / .2 / .3 / .4** – Four sequential alpha releases of the Rust-based Codex client. No detailed changelogs were provided; these appear to be iterative internal builds. Developers using the Rust CLI should update to the latest to benefit from ongoing fixes.

## Hot Issues (10 Noteworthy)
1. [#28969 – Add setting to disable auto-resolve in 60 seconds for questions](openai/codex Issue #28969) (53 comments, 151 👍) – A heavily upvoted request for user control over automatic resolution timing. Community frustration with premature timeouts is clear.
2. [#12491 – MCP child processes not reaped after task completion – 1300+ zombies, 37GB memory leak](openai/codex Issue #12491) (27 comments) – A severe resource leak in the Codex.app GUI that leaves zombie processes and massive memory consumption. Remains open after five months.
3. [#21639 – Hooks no longer run after Codex Desktop update](openai/codex Issue #21639) (23 comments) – A regression breaking custom hooks in the desktop app, affecting automation workflows.
4. [#25319 – Scope Codex VS Code chats to the current workspace/project](openai/codex Issue #25319) (17 comments, 47 👍) – A popular enhancement request for project-scoped chat history in the IDE extension.
5. [#27597 – Codex IDE extension fails to load in VS Code Remote-SSH](openai/codex Issue #27597) (16 comments) – Blocks remote development for users relying on SSH workspaces.
6. [#22428 – Windows Desktop sandbox fails with setup refresh failed / CreateProcessAsUserW failed](openai/codex Issue #22428) (15 comments) – Persistent Windows sandbox startup failure, affecting sandbox-dependent users.
7. [#26984 – MCP stdio servers leak pipe fds + orphan child processes → cumulative EMFILE](openai/codex Issue #26984) (14 comments) – A companion to #12491, affecting CLI users with file-descriptor exhaustion under long-running sessions.
8. [#23200 – Support headless remote Linux hosts for Codex mobile without requiring desktop app](openai/codex Issue #23200) (13 comments, 42 👍) – Strong demand for mobile-to-Linux-server workflows.
9. [#27458 – Codex appears to timeout while waiting for user input](openai/codex Issue #27458) (12 comments, 43 👍) – A timeout bug that prevents interactive workflows; high reaction count.
10. [#33778 – Windows Codex desktop app spawns hundreds of taskkill.exe and conhost.exe during local tool execution](openai/codex Issue #33778) (8 comments) – A performance-killing process storm on Windows, causing system-wide lag.

## Key PR Progress (10 Important)
1. [#34852 – Wake sleeping threads for queued agent mail](openai/codex PR #34852) – Fixes idle threads not waking when agent work arrives; critical for multi-agent reliability.
2. [#34851 – Use batch metadata for plugin app summaries](openai/codex PR #34851) – Improves plugin loading performance by batching metadata requests, with fallback to cache on batch failure.
3. [#34850 – Disable image generation for Free-plan accounts](openai/codex PR #34850) – Prevents Free-tier users from accessing image generation tool, aligning with subscription gating.
4. [#34849 – Cache remote plugin catalogs by scope](openai/codex PR #34849) – Adds disk caching for plugin catalogs (3h TTL), reducing network overhead on repeated plugin listing.
5. [#31817 – Update models.json](openai/codex PR #31817) – Automated refresh of model definitions, keeping the client in sync with OpenAI’s model roster.
6. [#34847 – Use Guardian model limits for review sessions](openai/codex PR #34847) – Ensures Guardian review uses correct context-window and compaction limits when the reviewed model differs from the parent.
7. [#34846 – Allow custom providers to opt into standalone web search](openai/codex PR #34846) – Exposes `supports_standalone_web_search` flag for custom model providers, enabling web search in non-default setups.
8. [#34845 – Track multi-agent mode in world state](openai/codex PR #34845) – Makes multi-agent instructions durable across history changes without re-emitting setup hints.
9. [#34840 – Add persisted thread pinning to the app server](openai/codex PR #34840) – Lets users pin threads; includes filtering and pagination support – a direct response to workspace organization requests.
10. [#34839 – Preserve user input when MCP startup is interrupted](openai/codex PR #34839) – Prevents loss of user input if interrupt occurs while MCP tools are still starting – a subtle but important user-experience fix.

## Feature Request Trends
- **Workspace-scoped chat history** – Multiple issues ask for per-project or per-workspace isolation of conversations in the IDE extension and desktop app.
- **Headless/remote Linux control** – Strong desire to use Codex mobile as a control layer for always-on Linux servers without requiring a desktop app intermediary.
- **Better rate-limit visibility** – Users on Plus accounts are confused by disappearing daily limits and unclear weekly usage displays.
- **User-configurable auto-resolution** – The ability to disable or adjust the 60-second auto-resolve timer for questions is a top-voted request.

## Developer Pain Points
- **Process and resource leaks** – MCP servers leave orphaned child processes and leak file descriptors across both desktop (GUI) and CLI, leading to crashes and memory bloat.
- **Windows-specific instability** – A disproportionate number of bugs affect Windows: sandbox failures, excessive `taskkill.exe` spawning, token exchange errors, and WSL path mismatches.
- **Regression in hooks and extensions** – Updates frequently break existing hooks or IDE extension functionality (e.g., Remote-SSH, GitHub Codespaces), eroding trust in stable releases.
- **Silent behavior changes** – Users report that prerelease modes (e.g., “Code mode”) are shipped silently in stable extensions, breaking long-running MCP calls and burning token quotas.
- **Confusing plan-mode violations** – Agents ignoring plan-mode restrictions and modifying files, undermining the safety guarantees of planning workflows.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*