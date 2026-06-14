# AI CLI Tools Community Digest 2026-06-14

> Generated: 2026-06-14 03:37 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# AI CLI Tools Ecosystem Cross-Comparison Report — 2026-06-14

## 1. Ecosystem Overview

The AI CLI tools landscape is experiencing divergent maturation paths. Claude Code's community is pushing toward plugin extensibility, session persistence, and UX customization—signs of a platform reaching production maturity. OpenAI Codex is locked in a cross-platform stabilization sprint, with heavy investment in Windows/WSL infrastructure and recurring safety-layer friction eroding user trust. Both tools share mounting community frustration around permission-system reliability and tool-use hallucination, while diverging sharply on integration philosophy and target-user focus.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Sourced Issues (last 24h)** | 10 hot issues | 10 hot issues |
| **Sourced PRs (last 24h)** | 3 (1 substantial, 2 trivial/stale) | 10 (all active infrastructure PRs) |
| **Releases (last 24h)** | None | 2 alpha releases (`v0.140.0-alpha.18/.19`, no changelogs) |
| **Community engagement (top issue)** | #24726: 52 comments, 159 👍 | #24391: 52 comments, 26 👍 (CLOSED) |
| **Critical-severity bugs** | Session data loss (#66734), bypass permissions regressions (#37253, #36497) | Windows app non-launchable (#27979), macOS malware alerts (#24246) |
| **Signal-to-noise in PRs** | Low (1 meaningful PR, rest trivial) | High (coordinated cross-platform stack from core team) |

**Takeaway:** Codex is iterating faster on infrastructure (10 active PRs, 2 releases), but Claude Code's community engagement per issue is higher (159 upvotes vs 26 for top issues). Claude Code's PR activity is a weak point—only one community contribution worth noting.

---

## 3. Shared Feature Directions

Both communities independently request similar capabilities, suggesting genuine industry demand:

| Shared Requirement | Claude Code Signal | OpenAI Codex Signal | Implications |
|---|---|---|---|
| **IDE integration parity** | #47166 (JetBrains plugin demanded), #24726 (VS Code auto-attach opt-out) | N/A (Codex lacks official VS Code/JetBrains extensions) | Claude Code users expect first-class IDE support; Codex has not yet entered this conversation |
| **Memory / session lifecycle hooks** | #47023 (official hooks for compact/event interception) | #20204 (PreToolUse hook coverage inconsistent) | Both communities want programmable middleware for observability, memory, and security |
| **Windows & cross-platform reliability** | WSL-specific regression (#36497) | #24391, #27979, #28086 (Windows sandbox failures, app launch, WSL agent) | Windows support remains immature in both tools; Codex is investing heavily, Claude Code is reacting |
| **Tool-use reliability & hallucination** | #67847, #68332 (fabricated `tool_use` blocks) | #28015, #27817 (false-positive safety flags blocking legitimate work) | Both face trust deficits when tool execution deviates from user intent |
| **Rate-limit / billing transparency** | Implicit (no direct issue) | #28118 (rate-limit reset redemption in TUI) | Only Codex has surfaced this as a feature request; likely latent demand in Claude Code |

**Notable divergence:** Claude Code's community focuses heavily on **terminal UX customization** (themes, input highlighting, sound effects)—uniquely absent from Codex discourse.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary user persona** | Power developers, CLI-first users, JetBrains/VS Code practitioners | Enterprise/regulated users, cross-platform teams, Windows-first organizations |
| **Plugin/extensibility** | Plugin system exists and is used (#68239 per-project theme plugin); community building on it | Hook system exists but incomplete (#20204); plugin auth routing still maturing |
| **Safety approach** | Permission prompts for internal paths—trust erosion due to bypass regression | Aggressive safety flags with false positives—users blocked from finance/devops work |
| **Deployment model** | Local TUI + VS Code extension + remote control | CLI + Desktop app (Windows/macOS) + app-server + remote environments |
| **Session persistence** | JSONL transcript with critical data-loss bug (#66734) | Side-chat ephemeral (#26227), session model less documented |
| **Model behavior** | Opus 4.8 tool hallucination reports; subagent reasoning effort config requested | SSE fallback performance regression; computer-use approval denied despite permissions |
| **Community tone** | Feature requests and UX complaints from experienced users | Infrastructure bugs and safety-policy frustration from mixed-skill users |

**Strategic insight:** Claude Code is evolving into a **customizable developer platform** (plugins, themes, memory hooks), while Codex is focused on **reliable enterprise deployment** (cross-OS, sandbox, auth). These are complementary but distinct market positions.

---

## 5. Community Momentum & Maturity

| Indicator | Claude Code | OpenAI Codex |
|---|---|---|
| **Community size (by engagement)** | Higher upvote counts (159 on top issue); broader feature request diversity | More commented issues (52 comments on top); narrower infrastructure focus |
| **Iteration velocity** | Low (no releases last 24h, 1 meaningful PR) | High (2 alpha releases, 10 active PRs, coordinated team pushes) |
| **Maturity signals** | Plugin system being used; UX customization demands indicate power users; data-loss bug indicates production adoption | Cross-platform PR stacks show systematic investment; fragmented release quality indicates immaturity |
| **Developer tooling** | VS Code extension exists; JetBrains request is 2nd hottest issue | No IDE extensions; app-server and remote environments are primary interfaces |
| **Bug severity landscape** | Session data loss (critical), permission regression (trust-eroding), hallucination (confidence-shaking) | App non-launchable (critical), security false positives (trust-eroding), sandbox regression (reliability-shaking) |

**Assessment:** Claude Code has a more mature community (higher signal, broader use cases) but slower iteration. Codex is iterating faster but producing more alpha-quality releases and fragile Windows builds. Neither tool is fully production-stable.

---

## 6. Trend Signals

1. **Agent trust deficit is the dominant meta-theme.** Both communities report tool fabrication (#67847, #68332 in Claude; false safety flags in Codex). Users cannot trust tools to execute correctly without verification—a fundamental barrier to autonomous agent adoption.

2. **Permission systems are failing at scale.** bypassPermissions regressions (Claude) and false-positive safety checks (Codex) are the #1 pain points by comment volume. Users want predictable, opt-out-able guardrails, not unpredictable interruption.

3. **Extensibility is the next competitive differentiator.** Claude Code's plugin hook for themes (#68239) and memory lifecycle hooks (#47023) show a platform play. Codex's incomplete hook coverage (#20204) and pragmatic plugin dedup (#27607) suggest slower platform investment.

4. **Windows support remains a blueprint-quality gap.** Codex is actively building hermetic Wine test harnesses (#28120), remote environment `cwd` handling (#28146, #28152), and process lifecycle tests (#28135). Claude Code treats WSL regressions reactively. For any organization with mixed-OS teams, Codex's infrastructure investment is a stronger signal.

5. **Safety fatigue is real.** Codex's cybersecurity false positives (finance, DevOps) and Claude's internal-path permission spam are driving users to seek bypass mechanisms—undermining the very safety controls these tools were designed to enforce.

6. **Rate-limit and billing transparency is emerging as a UX surface area.** Codex's rate-limit redemption feature (#28118) is the first explicit request; expect Claude Code to follow as adoption scales and API costs become more visible to end users.

---

**Bottom line for decision-makers:** Choose Claude Code if your team prioritizes CLI-first power-user workflows, plugin extensibility, and IDE integration, and you can tolerate session-persistence risk. Choose OpenAI Codex if cross-platform reliability (especially Windows) and enterprise sandbox compliance are non-negotiable, and you can manage safety-fatigue among users. Neither tool is ready for fully autonomous production deployment without human verification overhead.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

**Data as of 2026-06-14** | Source: [github.com/anthropics/skills](https://github.com/anthropics/skills)

---

## 1. Top Skills Ranking

The following pull requests represent the most-discussed skill submissions (sorted by comment count, all currently **open**). Each describes a new or substantially improved Skill for the Claude Code ecosystem.

### #1 – 🏆 `document-typography` skill
**PR #514** ([link](https://github.com/anthropics/skills/pull/514))  
*Author: PGTBoos | Created: 2026-03-04*  
A typographic quality-control skill that prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. The PR argues these issues affect every document Claude produces, making it a high-impact utility. Discussion highlights the universality of the problem and requests for additional typographic rules.

### #2 – `ODT` skill (OpenDocument text creation and template filling)
**PR #486** ([link](https://github.com/anthropics/skills/pull/486))  
*Author: GitHubNewbie0 | Created: 2026-03-01*  
Adds full support for `.odt` and `.ods` files—creation, template filling, reading, and conversion to HTML. Important for LibreOffice/OpenOffice users. The community has debated whether this should be merged with the existing DOCX skill or remain separate.

### #3 – Improved `frontend-design` skill
**PR #210** ([link](https://github.com/anthropics/skills/pull/210))  
*Author: justinwetch | Created: 2026-01-05*  
A revision of the existing frontend-design skill to improve clarity, actionability, and internal coherence. The goal is to ensure every instruction is Claude-executable within a single conversation. Comments focus on the balance between specificity and flexibility.

### #4 – `skill-quality-analyzer` & `skill-security-analyzer` meta-skills
**PR #83** ([link](https://github.com/anthropics/skills/pull/83))  
*Author: eovidiu | Created: 2025-11-06*  
Two meta-skills that evaluate other skills across structure/documentation, security, and quality dimensions. The quality analyzer uses a five-dimension scoring system (20% each). Discussion centered on whether meta-skills should live in a separate namespace and how to avoid evaluation loops.

### #5 – SAP-RPT-1-OSS predictor skill
**PR #181** ([link](https://github.com/anthropics/skills/pull/181))  
*Author: amitlals | Created: 2025-12-28*  
Leverages SAP’s open-source tabular foundation model (released at TechEd 2025) for predictive analytics on SAP business data. Attracted enterprise users; discussion focused on API key management and security implications of running predictive models via Claude Code.

### #6 – `testing-patterns` skill
**PR #723** ([link](https://github.com/anthropics/skills/pull/723))  
*Author: 4444J99 | Created: 2026-03-22*  
Covers the full testing stack: philosophy (Testing Trophy model), unit testing (AAA pattern), React component testing, and edge cases. Community asked for expanded coverage of integration testing and mocking strategies.

### #7 – AURELION skill suite (kernel, advisor, agent, memory)
**PR #444** ([link](https://github.com/anthropics/skills/pull/444))  
*Author: Chase-Key | Created: 2026-02-21*  
Four skills from the AURELION ecosystem: a structured cognitive framework (5-floor thinking templates), an advisor for professional knowledge management, and memory/agent capabilities. The breadth of the suite sparked discussion on skill modularity and namespace collisions.

---

## 2. Community Demand Trends

Analysis of the top Issues reveals several clear directions the community is most eagerly awaiting:

- **Org-wide skill sharing & governance** – Issue [#228](https://github.com/anthropics/skills/issues/228) (14 comments, 7 👍) requests native sharing within organizations. Users currently rely on manual `.skill` file transfers. A related security concern [#492](https://github.com/anthropics/skills/issues/492) (7 comments) highlights trust-boundary abuse when community skills appear under the `anthropic/` namespace.

- **Reliable skill evaluation & description optimization** – Issues [#556](https://github.com/anthropics/skills/issues/556) (12 comments) and [#1169](https://github.com/anthropics/skills/issues/1169) (3 comments) report that `run_eval.py` consistently returns 0% recall for all queries. This breaks the core optimization loop for skill descriptions. The community urgently wants a fix to enable data-driven skill improvement.

- **Enterprise / security skills** – Issue [#412](https://github.com/anthropics/skills/issues/412) (6 comments) proposes an `agent-governance` skill with policy enforcement and audit trails. Issue [#1175](https://github.com/anthropics/skills/issues/1175) discusses security for SharePoint Online document handling. Demand is rising for skills that enforce safety patterns and enterprise access controls.

- **Windows compatibility** – Issues [#1061](https://github.com/anthropics/skills/issues/1061) and earlier reports document multiple subprocess, encoding, and pipe failures on Windows. The skill-creator toolchain is effectively unusable on Windows, creating a significant barrier for a large segment of potential contributors.

- **MCP integration** – Issue [#16](https://github.com/anthropics/skills/issues/16) (4 comments) requests exposing Skills as Model Context Protocol endpoints, allowing deterministic API-like interaction with Claude. This would unlock tool composition and external system integration.

- **Multi-file skill bundling** – Issue [#1220](https://github.com/anthropics/skills/issues/1220) (2 comments) asks for inline bundling of reference files so all supporting materials are delivered within the skill context, reducing fragmentation.

---

## 3. High-Potential Pending Skills

The following skill PRs are **open**, actively discussed, and likely to land in the near future:

| Skill | PR | Description | Created | Comments (approx.) |
|-------|----|-------------|---------|-------------------|
| `document-typography` | [#514](https://github.com/anthropics/skills/pull/514) | Typographic quality control for AI-generated documents | 2026-03-04 | High (top of list) |
| `ODT` (OpenDocument) | [#486](https://github.com/anthropics/skills/pull/486) | Create, fill, read, convert `.odt`/`.ods` files | 2026-03-01 | High |
| `skill-quality-analyzer` + `skill-security-analyzer` | [#83](https://github.com/anthropics/skills/pull/83) | Meta-skills for evaluating other skills | 2025-11-06 | High |
| `SAP-RPT-1-OSS predictor` | [#181](https://github.com/anthropics/skills/pull/181) | Predictive analytics using SAP tabular foundation model | 2025-12-28 | Moderate |
| `agent-creator` | [#1140](https://github.com/anthropics/skills/pull/1140) | Meta-skill for creating task-specific agent sets | 2026-05-15 | Moderate |
| `testing-patterns` | [#723](https://github.com/anthropics/skills/pull/723) | Full testing stack guidance | 2026-03-22 | Moderate |
| `codebase-inventory-audit` | [#147](https://github.com/anthropics/skills/pull/147) | Orphaned code / unused files / documentation gaps | 2025-12-16 | Moderate |
| `shodh-memory` | [#154](https://github.com/anthropics/skills/pull/154) | Persistent memory system for cross-conversation context | 2025-12-19 | Moderate |
| `AURELION skill suite` | [#444](https://github.com/anthropics/skills/pull/444) | Cognitive framework + memory + advisor + agent | 2026-02-21 | Moderate |

All appear non-controversial in terms of scope; the primary blockers are code review bandwidth and the resolution of toolchain bugs (especially `run_eval.py` recall issues) that affect evaluation of new skills.

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand at the Skills level is for robust document-format handling (typography, ODT, PDF) combined with meta-skills for quality assurance and security validation, driven by a pressing need to fix the broken skill-evaluation toolchain and enable enterprise-grade governance and sharing.**

---

# Claude Code Community Digest — 2026-06-14

## Today’s Highlights

No new releases today. The community is vocal about persistent permission‑system bugs (bypassPermissions still prompting on internal paths), a serious session data‑loss bug in the latest installer builds, and growing demand for customizable IDE integrations (especially a real JetBrains plugin). A promising community PR adds per‑project theme settings via a plugin hook.

## Releases

*(No new releases in the last 24 hours.)*

---

## Hot Issues (10 noteworthy)

1. **[#24726 – VS Code extension: add setting to disable auto-attach of open file/selection](https://github.com/anthropics/claude-code/issues/24726)**  
   *52 comments · 159 👍*  
   Users want to opt out of the automatic file-attach behavior in the VS Code sidebar. High engagement shows this is a significant UX friction point for many.

2. **[#47166 – JetBrains needs a real Claude Code plugin](https://github.com/anthropics/claude-code/issues/47166)**  
   *23 comments*  
   The existing JetBrains integration is considered insufficient; the community is asking for a first‑class AI Assist interface similar to the VS Code extension.

3. **[#47023 – Expose compact/session lifecycle hooks for external memory layers](https://github.com/anthropics/claude-code/issues/47023)**  
   *22 comments · 4 👍*  
   A proposal to provide official hooks for compact & session events so that external memory solutions (knowledge graphs, markdown stores) don’t need to re‑implement transcript interception. Ties together five separate memory‑related issues.

4. **[#29937 – Terminal rendering corruption in tmux](https://github.com/anthropics/claude-code/issues/29937)**  
   *17 comments · 38 👍*  
   Text overlaps and overwrites previous output in tmux on Linux. A persistent rendering bug affecting power users who rely on tmux.

5. **[#8504 – Disable or customize user input background highlighting](https://github.com/anthropics/claude-code/issues/8504)**  
   *12 comments · 18 👍*  
   Request to allow disabling or styling the highlighted background of the user input area in the TUI. A long‑standing accessibility and aesthetic concern.

6. **[#37253 – bypassPermissions mode still prompts for edits to ~/.claude/ files](https://github.com/anthropics/claude-code/issues/37253)**  
   *11 comments · 8 👍*  
   Despite setting `bypassPermissions`, edits to `~/.claude/commands/` and `~/.claude/rules/` trigger confirmation dialogs. Undermines the purpose of the bypass setting.

7. **[#43083 – Configurable reasoning effort level for subagents](https://github.com/anthropics/claude-code/issues/43083)**  
   *10 comments · 22 👍*  
   Users want to set `low/medium/high` reasoning effort when dispatching subagents, not just choose the model. High upvote ratio indicates strong demand.

8. **[#36497 – .claude/skills/ edit permission prompts (regression in v2.1.79)](https://github.com/anthropics/claude-code/issues/36497)**  
   *9 comments · 11 👍*  
   A regression causes permission prompts on `.claude/skills/` files even though docs say they are exempt. Affects users on WSL.

9. **[#28379 – Slash commands not supported in /remote-control UI](https://github.com/anthropics/claude-code/issues/28379)**  
   *8 comments · 44 👍*  
   When using remote control from claude.ai/code or mobile, slash commands like `/clear` are sent as regular messages. High upvote count shows many use remote control and expect parity.

10. **[#66734 – Session JSONL rewritten to metadata‑only stub – data loss](https://github.com/anthropics/claude-code/issues/66734)**  
    *3 comments*  
    A critical bug where session transcripts are truncated to metadata only, permanently losing all user/assistant messages. Affects sessions since the native installer migration (v2.1.168–170). Low comment count but extremely high severity.

---

## Key PR Progress

Only three PRs were updated in the last 24 hours. The sole substantial contribution is:

- **[#68239 – feat: add project‑theme plugin for per‑project theme settings](https://github.com/anthropics/claude-code/pull/68239)**  
  *Open · by 12britz*  
  Adds a `SessionStart` plugin hook that reads `theme` / `color` from `.claude/settings.json` and applies them automatically. Closes #43216 (per‑project persistent color request). A clean example of the plugin system being used to solve a long‑standing user need.

The other two PRs are trivial: [#1](https://github.com/anthropics/claude-code/pull/1) is a long‑closed SECURITY.md addition, and [#58673](https://github.com/anthropics/claude-code/pull/58673) appears to be a spam/test PR.

---

## Feature Request Trends

The most prominent feature directions visible in today’s issues:

- **IDE integration parity** – High demand for a real JetBrains plugin (#47166) and finer control over VS Code behavior (disable auto‑attach #24726, status line customization #21867).
- **Memory & session lifecycle hooks** – Several issues request official hooks for compact/event interception so external memory layers can be built without workarounds (#47023, linked to five other memory issues).
- **Subagent & agent team control** – Configurable reasoning effort (#43083) and better inbox message handling in agent teams (#50779) show users want more fine‑grained control over autonomous agents.
- **Remote control feature parity** – Slash commands and other local‑mode features are missing from `/remote-control` (#28379); popularity suggests remote usage is growing.
- **Terminal and UI customization** – Hiding token counter/version (#21867), disabling input highlighting (#8504), sound effects toggle (#59970), and per‑project themes (#68239 PR) all point to a desire for a less cluttered, more personalizable terminal experience.
- **Desktop app UX polish** – Project recents removal, re‑rooting sessions (#68350), and SSH config cache reload (#68334) indicate the desktop app is gaining adoption but still lacks basic management features.

---

## Developer Pain Points

Recurring frustrations and high‑frequency bug reports:

- **Permission system regression** – Multiple reports (##37253, #36497, #53888) confirm `bypassPermissions` does not fully exempt internal paths like `.claude/commands/` or `.claude/skills/` from permission prompts. This erodes trust in the setting’s contract.
- **Session data loss** – Issue #66734 details a session JSONL being rewritten to a stub, losing all conversation history. A “data‑loss” label with high severity; no fix yet.
- **Model hallucination & tool confabulation** – Issues #67847 and #68332 describe Opus 4.8 fabricating tool executions (no `tool_use` blocks) and reporting fake results. Another report (#64048) describes Claude creating prompt‑injection content before reading a file. These shake confidence in the tool‑use reliability.
- **Terminal rendering bugs** – tmux corruption (#29937) and CJK mojibake when copying from fullscreen renderer (#66269) continue to affect Linux/macOS users.
- **Silent failures** – Gateway model discovery silently fails when auth comes from `apiKeyHelper` (#56675); expired model trial bricks the session with no auto‑fallback (#68218). Both leave users stuck without clear error messages.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-14

## Today's Highlights

Two new Rust alpha releases (v0.140.0-alpha.18 and .19) landed with no changelog detail, but the repo’s real action is in a fresh wave of Windows cross‑platform infrastructure PRs and sustained user frustration with false‑positive safety flags. The most‑commented issue (52 replies) is closed: a sandbox‑setup bug in CLI 0.133.0 that broke Windows users for weeks. Meanwhile, a coordinated PR stack from the `anp‑oai` team targets hermetic Wine test harnesses, remote environment `cwd` handling, and process‑handle invariants—signaling a serious push to stabilize Windows + WSL execution inside app‑server.

## Releases

- [`rust-v0.140.0-alpha.19`](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.19) — bare release tag, no changelog.
- [`rust-v0.140.0-alpha.18`](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.18) — bare release tag, no changelog.

Both published within the last 24 hours. No breaking changes or feature notes.

## Hot Issues (10 Noteworthy)

1. **[#24391 — Windows sandbox: spawn setup refresh fails on Codex CLI 0.133.0](https://github.com/openai/codex/issues/24391)** (CLOSED, 52 comments)  
   A long‑running blocker for Windows CLI users—`spawn` setup refresh started failing after the 0.133.0 update. The 52‑comment thread and 26 👍 indicate a widespread outage that appears to have been resolved.

2. **[#27979 — Windows Codex App no longer opens after update](https://github.com/openai/codex/issues/27979)** (OPEN, 18 comments)  
   The June‑12 app update (build 26.609.4994.0) leaves the app completely non‑launchable on some Windows 11 machines. Users cannot even see the About dialog. High urgency.

3. **[#28015 — False positive cybersecurity safety check blocks normal repo maintenance](https://github.com/openai/codex/issues/28015)** (OPEN, 15 comments)  
   Codex CLI repeatedly flags routine DevOps tasks (git push, dependency audits) as security risks, interrupting paid sessions. User reports the session was doing “ordinary local DevOps hygiene.”

4. **[#27817 — False positive cybersecurity flag on authorized finance/tax work](https://github.com/openai/codex/issues/27817)** (OPEN, 15 comments)  
   A normal personal‑finance conversation was flagged and redirected to “Trusted Access for Cyber” program. This repeats the theme of oversensitive safety checks (same reporter as #28015).

5. **[#24428 — Codex responds too slowly](https://github.com/openai/codex/issues/24428)** (OPEN, 14 comments, 25 👍)  
   Performance regression since late May, especially when falling back from WebSocket to SSE. The high number of thumbs‑up shows broad agreement.

6. **[#24246 — macOS “Malware Blocked” alert for Codex helper](https://github.com/openai/codex/issues/24246)** (OPEN, 11 comments, 9 👍)  
   macOS repeatedly shows “codex contains malware” alerts for the helper process. The exact trigger isn’t captured, causing user distrust on Apple Silicon.

7. **[#20204 — Inconsistent PreToolUse hook coverage across tool handlers](https://github.com/openai/codex/issues/20204)** (OPEN, 10 comments)  
   Only `shell`, `unified_exec`, `apply_patch`, and `mcp` emit hook events; other tools are invisible. This breaks custom hook‑based tooling and security‑audit pipelines.

8. **[#26158 — Windows sandbox regression in CLI 0.138.0](https://github.com/openai/codex/issues/26158)** (CLOSED, 10 comments, 5 👍)  
   `CreateProcessAsUserW` fails post‑0.132.0. Users forced to rollback. Closed, but another Windows sandbox regression in a short span raises reliability concerns.

9. **[#18896 — macOS Computer Use approval denied via MCP even after granting permissions](https://github.com/openai/codex/issues/18896)** (OPEN, 8 comments)  
   Screen Recording + Accessibility permissions granted, yet `list_apps` works but subsequent actions are blocked. Severe for macOS users depending on Computer Use.

10. **[#28086 — Windows app WSL agent fails to find bundled CLI](https://github.com/openai/codex/issues/28086)** (OPEN, 5 comments)  
    App‑server in WSL mode launches the wrong `codex.exe` (Windows binary) instead of the Linux CLI, breaking agent startup.

## Key PR Progress (10 Important)

1. **[#28151 — pipeline Windows targets separately](https://github.com/openai/codex/pull/28151)** (OPEN)  
    Breaks the Windows release matrix into per‑target pipelines so ARM64 packaging doesn’t wait for x64. Should reduce release latency.

2. **[#28146 — preserve remote environment cwd](https://github.com/openai/codex/pull/28146)** (OPEN)  
    Fixes app‑server rejecting or rewriting Windows cwds when the execution host is Linux. Critical for cross‑OS remote‑environment correctness.

3. **[#28152 — render remote environment cwd natively](https://github.com/openai/codex/pull/28152)** (OPEN)  
    Ensures the model‑visible `<environment_context>` shows correct Windows path syntax (e.g., `C:\Windows` instead of `/C:/windows`).

4. **[#28148 — add managed Amazon Bedrock login and logout](https://github.com/openai/codex/pull/28148)** (OPEN)  
    Adds account RPCs for Bedrock credential management. Provider‑scoped auth is maturing, although runtime reloading is deferred.

5. **[#28122 — exec‑server honors remote environment cwd and shell](https://github.com/openai/codex/pull/28122)** (OPEN)  
    Enables Windows process execution inside exec‑server with the correct cwd and native shell—paving the way for proper `remote_env_windows` tests.

6. **[#27607 — Dedupe plugin MCPs by app declaration name](https://github.com/openai/codex/pull/27607)** (CLOSED)  
    Hides duplicate plugin MCP servers when an App declaration already exists. Part of the ongoing plugin auth‑routing cleanup.

7. **[#28118 — feat(tui): add rate‑limit reset redemption to /usage](https://github.com/openai/codex/pull/28118)** (OPEN)  
    Adds CLI command to view/redeem personal rate‑limit reset credits. Backed by server‑side support in #28143.

8. **[#28120 — bazel: add PowerShell to Wine test harness](https://github.com/openai/codex/pull/28120)** (OPEN)  
    Adds x86_64 PowerShell into the hermetic Wine CI environment. Enables realistic cross‑OS integration tests.

9. **[#28135 — test process handle reuse after exit](https://github.com/openai/codex/pull/28135)** (OPEN)  
    Enforces the app‑server contract that a `processHandle` becomes reusable once the process exits. Part of a comprehensive test suite for process lifecycle.

10. **[#27953 — load app‑bundled internal hooks from Codex Desktop](https://github.com/openai/codex/pull/27953)** (OPEN, code‑reviewed)  
    Forces bundled plugin hooks to be trusted, hides them from review UI, and retains telemetry. Tightens security for first‑party plugins.

## Feature Request Trends

- **Cross‑platform parity**: Multiple issues and PRs target Windows sandbox, WSL integration, macOS TCC permissions, and computer‑use approval. Users expect identical reliability across OSes.
- **Safety‑check tuning**: False positives around cybersecurity flags (finance, repo maintenance) are the top user frustration. A trend toward “trusted access” programs is emerging, but users want fewer interruptions for legitimate work.
- **Side‑chat persistence**: [#26227](https://github.com/openai/codex/issues/26227) requests that side chats be preserved as child threads instead of being ephemeral—a common ask for long‑running sessions.
- **Rate‑limit transparency**: [#28118](https://github.com/openai/codex/pull/28118) responds to demand for visible reset credits and redemption flow in the CLI.
- **Spellcheck configuration**: [#25431](https://github.com/openai/codex/issues/25431) (13 👍) asks for an on‑off switch for spellcheck in the Windows app—a small UX win with broad appeal.

## Developer Pain Points

- **False‑positive safety interruptions** (3 high‑comment issues this week alone)—users are blocked from routine work and finance tasks, losing trust in the safety layer.
- **Windows sandbox fragility** —regressions in CLI 0.133.0 and 0.138.0 forced rollbacks; app updates leave Windows builds non‑launchable.
- **Performance degradation** —slow responses (especially SSE fallback) and memory churn on long threads remain unresolved.
- **macOS malware scares** —the “Malware Blocked” dialog erodes confidence and may push users to disable security features.
- **Inconsistent hook coverage** —tool hooks are opt‑in, making it impossible to build reliable security or observability tooling on top of Codex.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*