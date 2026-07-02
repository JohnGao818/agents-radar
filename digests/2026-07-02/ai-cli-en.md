# AI CLI Tools Community Digest 2026-07-02

> Generated: 2026-07-02 02:52 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools – 2026-07-02

## 1. Ecosystem Overview

The AI CLI tools landscape is maturing rapidly, with both Anthropic’s Claude Code and OpenAI’s Codex pushing new capabilities while grappling with production‑scale stability challenges. Claude Code shipped a major release featuring browser integration and a dedicated data‑visualization skill, but is inundated with safety‑filter false‑positive reports that undermine trust. Codex is deep into a Rust port of its CLI, focusing on Git security hardening and multi‑agent communication improvements, though Windows‑specific bugs and a missing `/undo` command dominate its community discussion. Both tools face shared pressure to improve context retention, plugin/MCP reliability, and platform consistency, while their respective communities are vocal—suggesting high usage but also high expectations for production readiness.

## 2. Activity Comparison

| Metric                     | Claude Code (anthropics/claude-code)       | OpenAI Codex (openai/codex)                    |
|----------------------------|--------------------------------------------|-----------------------------------------------|
| **Notable Issues (today)** | 10 (90 comments, ~68 total reactions)      | 10 (259 comments, ~514 total reactions)       |
| **PRs (notable changes)**  | 2 (1 doc fix merged, 1 incomplete draft)   | 10 (all substantive, likely merged or in review) |
| **Releases (latest)**      | 1 stable release (v2.1.198, with changelog) | 2 alpha releases (rust v0.143.0-alpha.32/.33, no visible changelogs) |

Codex shows significantly higher community engagement (more comments and reactions on its top issues) and a much higher volume of active PRs, though Claude’s single release is more feature‑rich and better documented. Claude’s 15+ duplicate safety‑filter reports from one user alone are not counted as “notable issues” but indicate systemic noise.

## 3. Shared Feature Directions

Both communities are demanding improvements in several overlapping areas:

- **Context retention & memory** – Claude users report cross‑session context loss (#72745) and token‑wasteful reinjection (#72997); Codex users struggle with agents replying to stale messages (#8648). Both groups want persistent operational memory.
- **Plugin/MCP reliability** – Claude’s GitHub MCP plugin returns malformed JSON‑RPC (#64654); Codex’s Meta Ads server OAuth fails (#24103). Authentication and payload validation are recurring pain points.
- **Undo / rollback** – Codex’s #9203 (312 👍) explicitly demands `/undo`; Claude lacks a dedicated undo feature but similar sentiment appears in requests for configurable tool timeouts and session recovery.
- **Approval & safety‑filter controls** – Claude’s flood of AUP false positives (own‑website audits, port scanning) and Codex’s `--dangerously‑bypass‑approvals` not working (#14345) indicate users need granular trust policies, not binary blocks.
- **Platform stability** – Both see Windows‑specific crashes (Claude P0 message loss #73118, Codex blank‑screen crash #29320) and macOS desktop regressions (Claude file viewer #72423, Codex SIGTRAP #29000).
- **Performance & token efficiency** – Claude’s harness re‑injects duplicate context blocks; Codex has TUI latency regressions (#16335). Users are cost‑conscious at scale.

## 4. Differentiation Analysis

| Dimension                | Claude Code                                       | OpenAI Codex                                      |
|--------------------------|---------------------------------------------------|---------------------------------------------------|
| **Feature focus**        | Desktop/IDE integration, agent orchestration, dataviz | CLI infrastructure, Rust port, Git safety hardening |
| **Target users**         | Broader: developers, designers, security auditors, data analysts | Primarily developers, especially those using Windows, CI pipelines, and complex Git workflows |
| **Technical approach**   | Browser extension (Chrome), OS notifications, harness‑based agent context | Rust re‑implementation, multi‑agent communication logging, structured Git status refusal |
| **Recent stability**     | Regressions in desktop file viewer, login browser, and VSCode message queuing | Regressions in Windows app crashes, sandbox bypass, and TUI responsiveness |
| **Community dynamics**   | High emotional reaction to safety restrictions; many duplicate issue reports | Highly focused on one critical feature (undo) and platform‑specific bugs; more PR contributions |

Claude differentiates by shipping visible user‑facing capabilities (Chrome extension, `/dataviz`) and aiming for a broader developer‑adjacent audience. Codex differentiates through deep engineering investment in security and cross‑platform compatibility, but its a lack of visible feature velocity (silent alpha releases) may frustrate users expecting tangible improvements.

## 5. Community Momentum & Maturity

- **OpenAI Codex** has a more active and vocal community (259 comments vs 90 on top issues, 514 total reactions vs 68). Its PR count (10) is five times higher than Claude’s (2), indicating substantial development throughput. However, the focus on Rust port and safety hardening suggests the CLI is still in a transition phase—alpha releases with no changelogs signal that stability is not yet guaranteed.
- **Claude Code** has a large but more reactive community—safety‑filter false positives generate many duplicate reports, and the P0 bug on Windows/VSCode suggests uneven quality control. The single stable release with detailed changelog and new features shows a more product‑oriented cadence, but the volume of regression reports indicates a maturing product dealing with edge cases from rapid expansion.

Neither tool is fully “mature” in a production sense; both suffer from platform‑specific regressions and missing critical features (context memory, undo). Codex has higher developer contribution velocity; Claude has higher feature velocity.

## 6. Trend Signals

From today’s community feedback, several industry‑wide signals emerge for AI CLI tool developers:

1. **Trust & safety are the top friction points** – Aggressive AUP enforcement (Claude) and ineffectual bypass options (Codex) show that binary approval models don’t work for legitimate security work or automation. Expect demand for **configurable policy levels** (e.g., “trusted projects”, “domain allowlists”, “security‑research mode”).
2. **Context is the new memory** – Both communities explicitly call for cross‑session context retention. As agents handle longer tasks, stateless sessions become untenable. Cloud‑sync’d memory or diff‑based context updates will become table stakes.
3. **Windows remains the Achilles’ heel** – Codex’s issue tracker is dominated by Windows crashes, line‑ending problems, Defender interference, and sandbox failures. Claude’s P0 bug on Windows/VSCode reinforces this. AI CLI tools that nail Windows compatibility will gain a significant differentiation.
4. **MCP/plugin ecosystems need governance** – Broken JSON‑RPC payloads and OAuth failures suggest that the plugin API layer is still fragile. Standardisation of protocol versions, error codes, and testing harnesses will be critical as the ecosystem grows.
5. **Undo/rollback is a non‑negotiable safety net** – Codex’s 312‑👍 plea makes clear that users will not trust AI‑driven file modifications without a reliable revert mechanism. This is a fundamental UX requirement, not a nice‑to‑have.
6. **Token efficiency is becoming a first‑class concern** – Users are actively measuring and complaining about wasted tokens (Claude’s 1.2M injected context, Codex’s TUI lag). Future tools will need to transparently report token usage and offer configurable compression strategies.

**Bottom line for decision‑makers:** Both tools are viable but still in beta for production use. Claude offers richer features for broader audiences but risks trust erosion from safety overreach. Codex provides a more developer‑focused, security‑conscious foundation but lacks visible feature momentum and essential undo functionality. Choose Claude for breadth and rapid feature rollout; choose Codex for deep Git workflows and Windows environment stability—but monitor both closely for the regressions and missing features highlighted today.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot: 2026-07-02 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The most-discussed Skill proposals by community attention reflect a strong focus on **infrastructure reliability** and **document quality tooling**.

| # | Skill | Functionality | Discussion Highlights | Status |
|---|-------|---------------|----------------------|--------|
| 1 | **skill-creator: run_eval.py fix** [#1298](https://github.com/anthropics/skills/pull/1298) | Repairs the evaluation pipeline that reports 0% recall for every skill description due to missing eval artifact installation, Windows stream reading bugs, and broken trigger detection | Central fix for issue #556 (12 comments, 7 👍) and #1169 (3 comments). The most consequential PR — without it, the description optimization loop optimizes against noise | **Open** (since June 10) |
| 2 | **document-typography** [#514](https://github.com/anthropics/skills/pull/514) | Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents — issues affecting every document Claude produces | Well-received quality-of-life improvement; addresses a pain point users rarely articulate but universally encounter | **Open** (since March 4) |
| 3 | **testing-patterns** [#723](https://github.com/anthropics/skills/pull/723) | Covers full testing stack with Testing Trophy philosophy, AAA pattern, React Testing Library, and test naming conventions | Comprehensive scope; fills a clear gap in the skills collection for production-grade testing guidance | **Open** (since March 22) |
| 4 | **ODT skill** [#486](https://github.com/anthropics/skills/pull/486) | Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods) — LibreOffice/ISO standard documents | Responds to demand for open-source document formats alongside existing PDF/DOCX skills | **Open** (since March 1) |
| 5 | **self-audit** [#1367](https://github.com/anthropics/skills/pull/1367) | Mechanical file verification + four-dimension reasoning quality gate for AI output before delivery | Newest high-activity PR; universal approach (any stack, any model) with verifiable step checks | **Open** (since June 28) |
| 6 | **color-expert** [#1302](https://github.com/anthropics/skills/pull/1302) | Self-contained color knowledge: naming systems (ISCC-NBS, Munsell, XKCD), color spaces with usage tables | Niche but authoritative — contributors noted the skill's production-grade reference tables | **Open** (since June 10) |
| 7 | **sensory (macOS automation)** [#806](https://github.com/anthropics/skills/pull/806) | Native macOS automation via `osascript`/AppleScript with two-tier permission system; alternative to screenshot-based computer use | Distinctive approach to GUI automation; permission model thoughtfully designed | **Open** (since March 29) |
| 8 | **SAP-RPT-1-OSS predictor** [#181](https://github.com/anthropics/skills/pull/181) | Predictive analytics on SAP business data using SAP's open source tabular foundation model | Enterprise-focused; early addition (December 2025) with ongoing community interest | **Open** (since Dec 28) |

> **Note:** All top PRs remain open. The community discusses improvements before merging — a healthy pattern for skill quality.

---

## 2. Community Demand Trends

From Issues, three clear demand clusters emerge:

### 🔧 Skill Developer Tooling (highest urgency)
- **run_eval.py / optimization loop reliability** — Issues [#556](https://github.com/anthropics/skills/issues/556) (12 comments, 7 👍) and [#1169](https://github.com/anthropics/skills/issues/1169) expose that the core evaluation pipeline is broken on Windows and reports 0% recall universally. Multiple contributors have independently reproduced the bug.
- **Windows compatibility** — Issue [#1061](https://github.com/anthropics/skills/issues/1061) (3 comments) details three Unix-first assumptions blocking native Windows usage.

### 🏢 Organization & Trust Infrastructure
- **Org-wide skill sharing** — Issue [#228](https://github.com/anthropics/skills/issues/228) (14 comments, 7 👍) demands direct sharing links instead of manual .skill file distribution. The highest-reacted feature request.
- **Trust boundary & namespace security** — Issue [#492](https://github.com/anthropics/skills/issues/492) (34 comments, 2 👍) warns that community skills distributed under the `anthropic/` namespace create impersonation risks. The most-discussed issue overall.
- **Duplicate skill deduplication** — Issue [#189](https://github.com/anthropics/skills/issues/189) (6 comments, **9 👍**) — the highest thumbs-up per comment ratio — reveals identical skills when installing `document-skills` and `example-skills` plugins.

### 🚀 New Skill Categories Requested
- **Agent governance/safety** — Issue [#412](https://github.com/anthropics/skills/issues/412) proposes policy enforcement, threat detection, and trust scoring patterns for AI agent systems.
- **Compact memory for agents** — Issue [#1329](https://github.com/anthropics/skills/issues/1329) proposes symbolic notation for long-running agent state management.
- **SharePoint Online document handling** — Issue [#1175](https://github.com/anthropics/skills/issues/1175) raises security and context-window concerns for enterprise document processing.
- **MCP integration** — Issue [#16](https://github.com/anthropics/skills/issues/16) requests exposing Skills as Model Context Protocol endpoints.

---

## 3. High-Potential Pending Skills

These PRs have active comments and are likely to land soon:

| Skill PR | Why It's Close | Key Details |
|----------|----------------|-------------|
| **[#1298 — run_eval.py fix](https://github.com/anthropics/skills/pull/1298)** | Addresses the single biggest blocker for the entire skill-creator workflow. Multiple contributors collaborating | Fixes install, Windows pipes, trigger detection, parallel workers |
| **[#1323 — run_eval trigger detection](https://github.com/anthropics/skills/pull/1323)** | Companion fix to #1298; catches the case where real skill name is missed | Target recall=0% bug from a different angle |
| **[#1099 — Windows subprocess fix](https://github.com/anthropics/skills/pull/1099)** | Directly resolves issue #1061's WinError 10038 | 1-line fix unlocking Windows compatibility |
| **[#1050 — Windows encoding + PATHEXT](https://github.com/anthropics/skills/pull/1050)** | Two 1-line fixes for Windows `claude.cmd` invocation | Complements #1099; same author ecosystem |
| **[#1367 — self-audit](https://github.com/anthropics/skills/pull/1367)** | Very recent (June 28); rapid updates (July 2). Mechanical-file-before-reasoning approach resonates | v1.3.0 already; universal applicability |
| **[#1302 — color-expert](https://github.com/anthropics/skills/pull/1302)** | Self-contained, authoritative; low review friction | Weeks-old but no blocking issues reported |

These pending PRs cluster around **two themes**: fixing the skill development pipeline (5 PRs) and high-quality domain-specific skills (2 PRs).

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is not for new Skills, but for reliable tooling to create, evaluate, and trust Skills — with the skill-creator's broken evaluation pipeline being the single bottleneck blocking the entire ecosystem from scaling.**

---

# Claude Code Community Digest — 2026-07-02

## Today's Highlights

Anthropic shipped **v2.1.198** making Claude in Chrome generally available and introducing `/dataviz` for chart/dashboard design guidance. The community is **flooded with safety-filter and AUP false-positive reports** — user `sworrl` alone filed over a dozen issues today, all describing session-halted blocks on legitimate work (own-website audits, drone protocol RE, port-scanning scripts). Meanwhile, a P0 bug on Windows/VSCode (pending user messages lost on disconnect) and a desktop file-viewer regression on macOS signal rough edges in the latest desktop experience.

## Releases

### [v2.1.198](https://github.com/anthropics/claude-code/releases/tag/v2.1.198)
- **Claude in Chrome** — browser extension now GA; enables in-page contextual coding.
- **Background agent notifications** — `claude agents` sessions that need input or finish now fire `agent_needs_input` / `agent_completed` hooks via the OS `Notification` API.
- **`/dataviz` skill** — new slash command provides guidance on chart selection, dashboard layout, and design best practices.

## Hot Issues (10 Noteworthy)

1. **[#50674](https://github.com/anthropics/claude-code/issues/50674) — Cowork fails on ARM64 (Snapdragon X) despite passing readiness check**  
   *Comments: 34 · 👍 0*  
   Long-standing bug (since April) blocking Copilot-like cowork mode on newer Windows-on-ARM hardware. Community frustration is audible.

2. **[#63469](https://github.com/anthropics/claude-code/issues/63469) — API 400 "messages[1].role must be either 'user' or 'assistant', but got 'system'"**  
   *Comments: 19 · 👍 8*  
   Regression in v2.1.156 that breaks tool calls when a system message is injected. High repro rate, high emoji count.

3. **[#45942](https://github.com/anthropics/claude-code/issues/45942) — Remote Control: "Always allow" permission from Android app breaks tool calls**  
   *Comments: 13 · 👍 16*  
   Critical for mobile + WSL workflows. "Allow once" works, "Always allow" returns internal error. High reaction signal.

4. **[#64654](https://github.com/anthropics/claude-code/issues/64654) — plugin:github:github MCP fails with HTTP 400 — malformed JSON-RPC payload**  
   *Comments: 12 · 👍 34*  
   GitHub MCP plugin broken by missing `jsonrpc` version tag. Top emoji count of all open issues — heavily affects CI/GitHub-centric teams.

5. **[#64630](https://github.com/anthropics/claude-code/issues/64630) — Claude on macOS does not use default browser for login**  
   *Comments: 8 · 👍 7*  
   Auth flow opens wrong browser (often Safari instead of Chrome/FF). Small UX annoyance amplifying with desktop app adoption.

6. **[#73118](https://github.com/anthropics/claude-code/issues/73118) — P0: long agent turns block queued user messages; pending messages lost on disconnect**  
   *Comments: 0 · 👍 0*  
   Filed today on Windows + VS Code. User cannot interrupt long-running agent turns; pending messages are discarded if connection drops. Critical for interactive use.

7. **[#72423](https://github.com/anthropics/claude-code/issues/72423) — Desktop file viewer blocks files in `permissions.additionalDirectories`**  
   *Comments: 1 · 👍 3*  
   Regression on macOS: agent can read files but desktop viewer refuses. Breaks workflow for multi-directory projects.

8. **[#72997](https://github.com/anthropics/claude-code/issues/72997) — Harness re-injects identical context blocks (task-list snapshots ×15, tool-schema delta ×2)**  
   *Comments: 1 · 👍 0*  
   Token-waste issue: harness sends verbatim context blocks multiple times per session (~1.2M injected tokens observed). Cost and latency concern.

9. **[#72745](https://github.com/anthropics/claude-code/issues/72745) — Quality regression: no cross-session context retention**  
   *Comments: 1 · 👍 0*  
   Systematic loss of operational memory between sessions on same task. Repeated failures and rework.

10. **[#67120](https://github.com/anthropics/claude-code/issues/67120) — Undocumented timezone- and endpoint-dependent variation in system-prompt date line**  
    *Comments: 1 · 👍 0*  
    Anomalous behavior in the `Today's date is …` prompt state — varies with API endpoint and system TZ, invisible to static analysis.

## Key PR Progress (2 PRs in total)

1. **[#72866](https://github.com/anthropics/claude-code/pull/72866) — docs: fix Github -> GitHub typo in README**  
   *Author: Manuelnuel098*  
   Clean docs-only fix. Low impact but welcomed.

2. **[#72543](https://github.com/anthropics/claude-code/pull/72543) — Create Cha**  
   *Author: sanpingli62-web*  
   Incomplete/unreviewed. Appears to be a draft or placeholder. No meaningful description.

## Feature Request Trends

- **Configurable `AskUserQuestion` timeouts** — multiple users (issues #62657, #73105) want the tool to stop auto-continuing after ~60 seconds. Indefinite wait or user-defined timeout preferred.
- **Cross-session memory/context retention** — #72745 and related reports demand persistent operational memory so recurring tasks don't restart from scratch.
- **Context-waste reduction** — #72997's analysis of duplicate token injection aligns with broader community calls for diff-based context updates rather than full re-injection of unchanged blocks.
- **Security/audit workflow enablement** — the flood of false-positive complaints (cyber/aup) from sworrl and others implicitly requests either a "trusted domain" bypass or improved discrimination of legitimate security work from malicious activity.

## Developer Pain Points

1. **Safety-filter / AUP false positives** — The top issue category today. User `sworrl` filed 15+ duplicates showing blocks on own-website audits, drone RE, port-scanning scripts, and cloud IAM analysis. Each halted the session with no easy override. Community frustration is high and Anthropic has not yet acknowledged the pattern publicly.

2. **Plugin/MCP reliability** — The GitHub MCP plugin (#64654) breaking on malformed JSON-RPC, the ARM64 cowork failure (#50674), and the Android remote-control permission bug (#45942) all point to insufficient testing across platforms and plugin APIs.

3. **Desktop app regressions** — macOS file viewer blocking `additionalDirectories` (#72423), login browser mismatch (#64630), and the pending-message loss on VS Code (#73118) indicate the desktop and IDE integrations are maturing unevenly.

4. **Token waste & cost** — The harness re-injection bug (#72997) and the system-prompt timezone variation (#67120) highlight underlying infrastructure issues that silently inflate token consumption.

*Generated from GitHub data for `anthropics/claude-code` — 2026-07-02*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-02

## Today’s Highlights
Two Rust-based alpha releases (v0.143.0-alpha.32 and .33) landed without visible changelogs, while the project focused on hardening Git safety checks and improving multi-agent communication logging. A long‑standing Windows line‑ending bug finally received a fix PR, and the most‑upvoted issue this week remains the missing `/undo` command (312 👍).

## Releases
- **rust‑v0.143.0‑alpha.32** — No additional details.
- **rust‑v0.143.0‑alpha.33** — No additional details.

*Both are part of the ongoing Rust port of the CLI. No behavior changes are documented in the release notes.*

## Hot Issues (10 noteworthy)

1. **[#8648](https://github.com/openai/codex/issues/8648) — Agent replies to earlier messages instead of latest**  
   *71 comments, 55 👍*  
   A critical context‑handling bug where Codex loses track of conversation order, especially in long threads. Community reports this makes multi‑turn sessions unreliable.

2. **[#9203](https://github.com/openai/codex/issues/9203) — Please bring back `/undo`**  
   *54 comments, 312 👍*  
   The highest‑voted open issue. Users rely on `/undo` to revert unintended file modifications/deletions; its removal has caused significant workflow disruption.

3. **[#29320](https://github.com/openai/codex/issues/29320) — Windows app shows “Something went wrong” after update**  
   *28 comments, 2 👍*  
   A blank‑screen crash on Windows 11 25H2 after the latest MSIX update (26.616.6631.0). No workaround yet, affecting multiple users.

4. **[#4003](https://github.com/openai/codex/issues/4003) — Patched files have mixed line endings on Windows**  
   *22 comments, 66 👍*  
   A long‑standing compatibility issue: Codex ignores the existing line‑ending style (LF vs. CRLF), causing Git diffs to break. A fix is now in PR #30882.

5. **[#29000](https://github.com/openai/codex/issues/29000) — CLI crashes with SIGTRAP on Intel macOS (CLOSED)**  
   *20 comments, 16 👍*  
   Closed as fixed after investigation confirmed a regression in v0.141.0. Users on Intel Macs should upgrade to v0.142+.

6. **[#14345](https://github.com/openai/codex/issues/14345) — Directories not trusted even with `--dangerously‑bypass‑approvals‑and‑sandbox`**  
   *15 comments, 21 👍*  
   A sandbox regression that forces approval prompts for trusted directories, breaking automated workflows. Community frustration is high.

7. **[#16335](https://github.com/openai/codex/issues/16335) — TUI/CLI performance regression from v0.116 to v0.117**  
   *15 comments, 7 👍*  
   Interactive CLI responsiveness degraded noticeably; users report multi‑second lag after every command.

8. **[#30009](https://github.com/openai/codex/issues/30009) — `apply_patch` fails with Windows sandbox error**  
   *14 comments, 2 👍*  
   File edits through the Windows app fail with a sandbox‑related crash. The error blocks all patch operations.

9. **[#20880](https://github.com/openai/codex/issues/20880) — App silently creates empty `~/Documents/Codex` on every launch**  
   *10 comments, 31 👍*  
   A minor but pervasive annoyance: an empty folder appears in the user’s Documents directory even when no project is opened.

10. **[#24103](https://github.com/openai/codex/issues/24103) — Official Meta Ads MCP fails OAuth login**  
    *10 comments, 2 👍*  
    MCP integration is a key use case, but the Meta Ads server returns `invalid_client_metadata` before the OAuth flow even starts, blocking social‑media toolchains.

## Key PR Progress (10 important changes)

1. **[#30887](https://github.com/openai/codex/pull/30887) — Speed up reverse history search**  
   Rewrites history access to batch‑read entries instead of fetching one at a time, dramatically reducing latency for large `history.jsonl` files.

2. **[#30882](https://github.com/openai/codex/pull/30882) — Preserve line endings when applying patches**  
   Fixes the long‑standing Windows CRLF issue (#4003) by detecting and maintaining each file’s existing line‑ending style.

3. **[#30850](https://github.com/openai/codex/pull/30850) — Block selected Git filters before staging**  
   Prevents repository‑configured Git filters from executing during patch staging, closing a potential code‑execution sink.

4. **[#30854](https://github.com/openai/codex/pull/30854) — Block selected merge drivers before three‑way patch application**  
   Similar hardening for `git apply --3way` to avoid running unsafe merge drivers from the repo’s config.

5. **[#30848](https://github.com/openai/codex/pull/30848) — Block executable Git filters before patch application**  
   Adds guard against `clean`, `smudge`, and `process` filters during `apply`/`preflight`/`revert`.

6. **[#30863](https://github.com/openai/codex/pull/30863) — Report structured Git status refusals**  
   Converts the binary “unavailable” status into a structured reason, making workspace‑change detection safer and more debuggable.

7. **[#30880](https://github.com/openai/codex/pull/30880) — Detect Codex installs managed by Vite+**  
   Adds support for the upcoming Vite+ package manager, including detection and proper `vp install` updates.

8. **[#30879](https://github.com/openai/codex/pull/30879) — Handle mixed‑case URLs in Windows command safety**  
   Fixes a case‑sensitivity bug where uppercase/mixed‑case HTTP(S) schemes in PowerShell commands were not blocked.

9. **[#30867](https://github.com/openai/codex/pull/30867) — Consolidate multi‑agent v2 communication sends**  
   Unifies direct messages, follow‑ups, and spawn messages into a single outbound path, simplifying added lifecycle logging.

10. **[#30876](https://github.com/openai/codex/pull/30876) — Support interleaved response items**  
    Enables reasoning summaries and final‑answer events to be delivered concurrently, reducing perceived latency in longer responses.

## Feature Request Trends
- **Undo/rollback** (#9203) – the most requested single feature, with 312 👍.
- **Windows app improvements** (#21074, #13673) – custom install location and smoother installation.
- **Rate‑limit transparency** (#30686, #30726) – users want clear visibility into “bankable reset credits” and why some accounts see resets while others do not.
- **MCP reliability** (#24103, #29857) – authentication and silent cancellation of MCP tool calls need fixes.
- **Enhanced `/fast` command** (#30800) – users want `/fast` to be handled internally rather than sent as chat text.

## Developer Pain Points
- **Windows‑specific bugs** dominate the issue tracker: app crashes (#29320, #30884), sandbox failures (#30009, #29413), mixed line endings (#4003), TUI escape‑sequence leakage (#28869), and Defender high CPU (#30527).
- **Context loss in long conversations** (#8648) remains a top frustration, as agents respond to stale messages.
- **Performance regressions** (#16335, #26869) in both TUI and app‑server continue to appear after each minor release.
- **Sandbox bypass not working** (#14345) harms automated/CI workflows that rely on `--dangerously‑bypass‑approvals`.
- **Missing features** like `/undo` and reliable MCP OAuth flow make the tool less trustworthy for production use.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*