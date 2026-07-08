# AI CLI Tools Community Digest 2026-07-08

> Generated: 2026-07-08 02:21 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date:** 2026-07-08  
**Scope:** Claude Code (Anthropic) vs. OpenAI Codex

---

## 1. Ecosystem Overview

The AI CLI tools landscape is maturing rapidly, with both Claude Code and OpenAI Codex entering phases of incremental refinement punctuated by critical reliability and cost-transparency challenges. Claude Code is navigating a **cost crisis** from unexplained 3–5× token consumption spikes, while Codex is shipping infrastructure improvements (atomic thread lifecycle, remote plugins) but facing model-specific regression concerns with GPT-5.5 reasoning-token clustering. Both communities share overlapping demands for usage observability, stable session management, and lifecycle hook parity. The tension between feature velocity and operational stability is the defining dynamic of this ecosystem today.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Hot Issues (active)** | 10 tracked | 10 tracked |
| **Comments on top issue** | 53 (#41506) | 156 (#30364) |
| **Total 👍 on top issue** | 26 | 252 |
| **Open PRs updated today** | 2 (both docs-only) | 10+ (many functional) |
| **Releases today** | **2 patch releases** (v2.1.203, v2.1.204) | **1 minor + 2 alpha releases** (rust-v0.143.0, alpha.38/39) |

**Key observation:** Codex has significantly more PR velocity and community engagement on its top issue, while Claude Code is shipping at a higher patch-release cadence with more breadth of reported bugs across Windows and UX categories.

---

## 3. Shared Feature Directions

Both communities are demanding the same capabilities, though with tool-specific naming:

| Common Need | Claude Code | OpenAI Codex |
|-------------|-------------|--------------|
| **Usage/cost transparency** | #33978: built-in `claude usage` command (10+ related issues) | Implicit via #30364 token clustering investigation |
| **Stable session resume** | #38029: abnormal token burn on resume; #75496/75497: TUI freezes | #25792: context compaction corruption losing AGENTS rules |
| **Hook / lifecycle automation** | Existing hook system; #21753 is missing from Claude's digest but implied by parity demand | #21753: 29 missing lifecycle hooks (Claude Code parity) |
| **UI accessibility** | #50543: independent font size scaling | #28726: code-server sidebar freeze |
| **Remote connection reliability** | Windows SSH woes (#75499) | #22857: SSH key auth improvements |
| **Plugin / marketplace UX** | #45810: disabled update button | Remote plugins enabled by default in v0.143.0 |

The **strongest cross-tool signal** is the demand for **cost and usage transparency**. Both communities are experiencing opaque consumption behavior (Claude Code: token spikes; Codex: reasoning-token clustering) and lack the tooling to diagnose it. This is a systemic gap in the category.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|-----------|-------------|--------------|
| **Primary pain point** | **Cost/billing surprises** (top 3 issues are cost-related) | **Model behavior regression** (GPT-5.5 token clustering) |
| **Community's trust posture** | Guarded — silent billing changes (#28927) eroded confidence | Pragmatic — focused on feature parity and infrastructure |
| **Editor UX emphasis** | VS Code terminal integration (#61021), JetBrains (#75498) | code-server, remote SSH, cross-platform app-server |
| **Safety/security posture** | Safety filter false positives (3 "cyber" blocks today); OAuth RFC violation (#42765) | Explicit memory writability control (#19195); authentication improvements |
| **Platform maturity** | Broader Windows-specific issues (Advisor unavailable, installation failures) | More mature cross-platform support, but macOS/Windows post-update crashes persist |
| **PR activity focus** | Docs-only today (minor typo, clarification) | **Deep infrastructure**: atomic thread lifecycle, plugin migration, syscall optimization, SQLite degraded mode |

**Takeaway:** Claude Code's community is **cost- and trust-focused**, reacting to perceived billing regressions. Codex is **infrastructure- and performance-focused**, rebuilding core systems while managing model-specific bugs. Claude Code has more surface-level UX complaints; Codex has deeper architectural churn.

---

## 5. Community Momentum & Maturity

| Indicator | Claude Code | OpenAI Codex |
|-----------|-------------|--------------|
| **Community engagement depth** | Moderate — top issue has 53 comments, 26 👍 | **Very high** — #30364 has 156 comments, 252 👍 |
| **Issue diversity** | Broad: billing, Windows, UX, safety, security | Focused: model behavior (#30364 dominates), hooks, atomic lifecycle |
| **Release maturity** | **Stable patch cadence** (2 patches/day) | **Rapid alpha/minor cadence** (3 releases/day) |
| **Core team visibility** | Low (only 2 docs PRs) | **High** (12+ PRs from winston-openai, deep Cargo.toml changes) |
| **Developer ecosystem** | Plugin marketplace exists but buggy (disabled update) | Remote plugins ship by default; npm marketplace sources |

**Assessment:** Codex is iterating faster at the **infrastructure layer** with visible core-team investment in thread lifecycle, plugin systems, and syscall optimization. Claude Code's community is more vocal about **operational pain** (cost, Windows regressions) but seeing less deep engineering response in the past 24 hours. Claude Code's **market maturity** looks higher in terms of stable releases, but its **innovation velocity** appears lower than Codex's current cycle.

---

## 6. Trend Signals

1. **Token consumption transparency is the #1 unmet need.** Both tools have communities in the dark about how and why tokens are consumed. A `claude usage` or `codex usage` built-in is the single highest-value feature gap across the ecosystem.

2. **Model-specific behavior changes are undermining trust.** GPT-5.5 reasoning-token clustering (Codex #30364) and Opus 4.8 safety filter false positives (Claude Code #75504) show that underlying model updates directly impact CLI tool reliability. Developers want **model behavior observability**, not just feature releases.

3. **Windows support is still an afterthought.** Claude Code has 5+ Windows-specific active issues; Codex has Git Bash and `exec_command` failures. The ecosystem is macOS/Linux-first, and Windows developers are experiencing friction disproportionately.

4. **Lifecycle hooks are becoming table stakes.** Codex's #21753 (29 hooks for parity with Claude Code) signals that **automation surfaces** are now expected. Tools without deep hook systems will struggle in CI/CD and multi-agent orchestration use cases.

5. **Session durability is a reliability bottleneck.** Both tools have reports of sessions corrupting (Claude: resume token burn; Codex: context compaction losing AGENTS rules). **Stable long-running sessions** are critical for developer adoption but remain fragile.

6. **Cost-control UX is immature.** Claude Code's false overage alarms (#39678), silent billing changes (#28927), and unexplained spikes (#41506) suggest that **usage limits and billing displays are not rigorously tested**. As these tools move from free tiers to paid plans, billing UX will become a competitive differentiator.

7. **Plugin ecosystems are accelerating.** Codex enabled remote plugins by default with npm sources. Claude Code has a marketplace but it's buggy. The **plugin model is winning**, and the tool that offers the most reliable, discoverable plugin ecosystem will gain developer mindshare.

---

**Bottom line for technical decision-makers:** If cost predictability and Windows reliability are your constraints, Claude Code's current turbulence warrants caution before scaling usage. If you need deep infrastructure reliability, lifecycle automation, and are willing to ride a fast-alpha cadence, Codex's current investment cycle suggests strong forward momentum — but monitor GPT-5.5 regression closely. For both tools, **invest in session monitoring and token auditing** until built-in transparency ships.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data snapshot: 2026-07-08 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The most-discussed pull requests reveal where community attention is concentrated—largely around **core tooling fixes** and **format-specific document skills**.

### #1 – skill-creator: fix run_eval.py (PR #1298) | **OPEN**
**Functionality**: Addresses the critical `run_eval.py` bug where every skill description reports `recall=0%` regardless of content—rendering the description-optimization loop useless. Fixes include installing the eval artifact as a real skill, Windows stream handling, trigger detection, and parallel worker logic.
**Discussion highlights**: References 10+ independent reproductions (#556) and multiple downstream scripts (`run_loop.py`, `improve_description.py`) that consume broken signals. This is the single highest-urgency item in the repository.
**Status**: Open | 🔗 [View PR](https://github.com/anthropics/skills/pull/1298)

### #2 – Add document-typography skill (PR #514) | **OPEN**
**Functionality**: Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Covers universal typographic issues that appear in every Claude output.
**Discussion highlights**: Community recognized pain—users rarely ask for typography fixes but consistently receive documents with orphaned lines and stranded section headers.
**Status**: Open | 🔗 [View PR](https://github.com/anthropics/skills/pull/514)

### #3 – fix(pdf): case-sensitive file references (PR #538) | **OPEN**
**Functionality**: Corrects 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where uppercase file references (`REFERENCE.md`, `FORMS.md`) point to actual lowercase files. Breaks on case-sensitive filesystems (Linux, macOS).
**Discussion highlights**: Highlights systemic issue—cross-platform file reference hygiene in the skills repository.
**Status**: Open | 🔗 [View PR](https://github.com/anthropics/skills/pull/538)

### #4 – Add ODT skill (PR #486) | **OPEN**
**Functionality**: OpenDocument text creation, template filling, and ODT-to-HTML conversion. Covers `.odt`, `.ods`, `.odf` and LibreOffice document workflows.
**Discussion highlights**: Addresses a clear format gap—users producing open-source or ISO-standard documents had no dedicated skill.
**Status**: Open | 🔗 [View PR](https://github.com/anthropics/skills/pull/486)

### #5 – Improve frontend-design skill (PR #210) | **OPEN**
**Functionality**: Revises the existing frontend-design skill for clarity, actionability, and single-conversation coherence.
**Discussion highlights**: Focused on making every instruction something Claude can actually follow within one turn—steering behavior without human-in-the-loop.
**Status**: Open | 🔗 [View PR](https://github.com/anthropics/skills/pull/210)

### #6 – Add skill-quality-analyzer and skill-security-analyzer (PR #83) | **OPEN**
**Functionality**: Two meta-skills: quality analysis across five dimensions (structure, documentation, etc.) and security analysis for community skills.
**Discussion highlights**: Meta-skills for the skills ecosystem itself—enables automated review of new submissions.
**Status**: Open | 🔗 [View PR](https://github.com/anthropics/skills/pull/83)

### #7 – fix(docx): tracked change w:id collision (PR #541) | **OPEN**
**Functionality**: Prevents document corruption when DOCX skill adds tracked changes to documents with existing bookmarks. Root cause: `w:id` is a shared ID space in OOXML; hardcoded low IDs collide with existing bookmarks.
**Discussion highlights**: Highlights the complexity of formatting skills—OOXML internals require careful namespace management.
**Status**: Open | 🔗 [View PR](https://github.com/anthropics/skills/pull/541)

---

## 2. Community Demand Trends

Analysis of top Issues (sorted by comments) reveals clear demand clusters:

| Demand Cluster | Key Issue(s) | Comments | 🔗 |
|---|---|---|---|
| **Security & Trust Boundaries** | #492 – Community skills under `anthropic/` namespace enable impersonation | 34 | [Issue #492](https://github.com/anthropics/skills/issues/492) |
| **Enterprise Sharing & Org Management** | #228 – Org-wide skill sharing in Claude.ai | 14 | [Issue #228](https://github.com/anthropics/skills/issues/228) |
| **Core Tooling Reliability** | #556 – `run_eval.py` 0% trigger rate; #1169 – recall=0% on every iteration | 12+3 | [Issue #556](https://github.com/anthropics/skills/issues/556), [#1169](https://github.com/anthropics/skills/issues/1169) |
| **Windows Compatibility** | #1061 – subprocess PATHEXT, cp1252 encoding, select on pipes | 3 | [Issue #1061](https://github.com/anthropics/skills/issues/1061) |
| **Skill Management & Persistence** | #62 – Skills disappearing after file rename | 10 | [Issue #62](https://github.com/anthropics/skills/issues/62) |
| **Duplicate Content** | #189 – document-skills and example-skills install identical content | 6 | [Issue #189](https://github.com/anthropics/skills/issues/189) |
| **New Skill Proposals** | #1329 – compact-memory (symbolic notation); #412 – agent-governance | 9+6 | [Issue #1329](https://github.com/anthropics/skills/issues/1329), [#412](https://github.com/anthropics/skills/issues/412) |
| **Cross-Platform Access** | #29 – AWS Bedrock compatibility; #16 – Expose Skills as MCPs | 4+4 | [Issue #29](https://github.com/anthropics/skills/issues/29), [#16](https://github.com/anthropics/skills/issues/16) |

**Key takeaways**:
- **Security is the #1 community concern**: The namespace impersonation issue (#492) has the highest engagement by far (34 comments, 2 👍). Community members are actively worried about trust boundaries when installing third-party skills.
- **Tooling reliability dominates**: The `run_eval.py` 0% bug (#556, 12 comments) and its variants (#1169) represent the most impactful functional gap—the description-optimization loop is fundamentally broken.
- **Enterprise features are highly demanded**: Org-wide skill sharing (#228, 14 comments) with 7 upvotes shows strong enterprise interest.
- **Cross-platform support is emerging**: Windows compatibility (#1061) and Bedrock integration (#29) signal demand beyond macOS-first users.

---

## 3. High-Potential Pending Skills

These PRs have active discussion, address clear community pain points, and are likely to land soon:

| Skill | PR | Summary | Why It Matters |
|---|---|---|---|
| **self-audit** (v1.3.0) | [#1367](https://github.com/anthropics/skills/pull/1367) | Mechanical file verification + four-dimension reasoning audit before delivery | Universal output quality gate—works across any project/stack/model |
| **color-expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Color naming systems (ISCC-NBS, Munsell, XKCD, RAL) + color space decision tables | Self-contained color expertise for design/document workflows |
| **sensory** (macOS automation) | [#806](https://github.com/anthropics/skills/pull/806) | Native macOS automation via AppleScript with two-tier permission system | Alternative to screenshot-based computer use—lower latency, higher reliability |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Full testing stack: philosophy, unit testing, React, E2E | Comprehensive test generation—addresses a core developer workflow |
| **Windows fixes** | [#1099](https://github.com/anthropics/skills/pull/1099), [#1050](https://github.com/anthropics/skills/pull/1050) | `run_eval.py` crash on Windows; subprocess encoding bugs | Unblocks Windows users from the skill-creation pipeline |
| **YAML validation** | [#539](https://github.com/anthropics/skills/pull/539), [#361](https://github.com/anthropics/skills/pull/361) | Pre-parse checks for unquoted descriptions with `:`, `#`, `{`, `[` | Prevents silent YAML parsing failures—catches errors before submission |
| **UTF-8 safety** | [#362](https://github.com/anthropics/skills/pull/362) | Replace character-length checks with byte-length validation to prevent Rust panics | Fixes crashes when skills contain multi-byte characters (emoji, CJK) |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, cross-platform skill-creation toolchain**—the `run_eval.py` recall bug (PR #1298, Issue #556, Issue #1169) generates more discussion than any single new skill proposal, indicating that contributors want to *create and iterate on skills* but are blocked by fundamental tooling failures, Windows incompatibility, and YAML parsing fragility, while simultaneously pushing for security hardening (namespace trust boundaries) and enterprise-grade sharing capabilities.

---

# Claude Code Community Digest — 2026-07-08

Powered by [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)

---

## Today’s Highlights

Two new patch releases (v2.1.203, v2.1.204) land fixes for hook streaming in headless sessions and pre‑emptive login‑expiry warnings. However, the community is **dominated by billing and token‑consumption pain**: the longest‑running thread (#41506) reports a 3–5× token spike on the Max plan since late March, and a parallel issue (#38029) links abnormal usage to session resumption. A new bug (#73365) with the Fable 5 advisor “unavailable” on Windows is drawing 31 👍 in just six days.

---

## Releases

Two versions shipped in the last 24 hours:

### [v2.1.204](https://github.com/anthropics/claude-code/releases/tag/v2.1.204)
- Fixed hook events not streaming during `SessionStart` hooks in headless sessions, which could cause remote workers to be idle‑reaped mid‑hook.

### [v2.1.203](https://github.com/anthropics/claude-code/releases/tag/v2.1.203)
- Added a warning when your login is about to expire, so you can re‑authenticate before background sessions are interrupted.
- Added a grey ⏸ badge to the footer when in manual permission mode, making the active mode always visible.
- Added the session’s additional working directories to the UI.

---

## Hot Issues (10 of 30)

| # | Issue | Comments | 👍 | Why it matters |
|---|-------|----------|----|----------------|
| 1 | [#41506](https://github.com/anthropics/claude-code/issues/41506) Max Plan: Token usage increased ~3–5x without configuration change | 53 | 26 | **Cost crisis** – users on the $100/month Max plan report sudden 3–5× usage since late March, with no config change. Uproar is intense. |
| 2 | [#38029](https://github.com/anthropics/claude-code/issues/38029) Abnormal usage consumption on Claude Code session resume | 23 | 33 | **Session resume cost bug** – resuming a session unexpectedly burns extra tokens. 33 👍 shows widespread impact. |
| 3 | [#33978](https://github.com/anthropics/claude-code/issues/33978) Feature request: Built‑in usage analytics command (`claude usage`) | 18 | 10 | **Missing observability** – consolidates 10+ open issues asking for token/usage transparency. |
| 4 | [#39678](https://github.com/anthropics/claude-code/issues/39678) Code Review incorrectly reports overage limit reached when spend is $0/$250 | 16 | 13 | **False billing alarm** – blocks PR reviews despite zero spend, affecting CI workflows. |
| 5 | [#28927](https://github.com/anthropics/claude-code/issues/28927) Silent billing change in v2.1.51: 1M context moved to extra‑usage‑only | 16 | 19 | **Undocumented billing change** – users discovered 1M context was silently moved out of Max plan allocation. |
| 6 | [#45810](https://github.com/anthropics/claude-code/issues/45810) Marketplace update button is disabled/unpressable | 13 | 5 | **Plugin UX bug** – update button greyed out even when a newer version exists. |
| 7 | [#73365](https://github.com/anthropics/claude-code/issues/73365) Advisor always “unavailable” with Fable 5 advisor (Opus 4.8 main) on Windows | 12 | 31 | **Showstopper for new model** – Advisor feature completely broken for Fable 5 users across all sessions. |
| 8 | [#61021](https://github.com/anthropics/claude-code/issues/61021) Can’t select text to copy from VS Code terminal | 10 | 7 | **Core UX regression** – terminal text selection broken in VS Code when Claude Code is running. |
| 9 | [#42765](https://github.com/anthropics/claude-code/issues/42765) OAuth redirect_uri uses `localhost` instead of `127.0.0.1`, violating RFC 8252 | 6 | 17 | **Security RFC violation** – potential man‑in‑the‑middle risk on Linux; many users want it fixed. |
| 10 | [#50543](https://github.com/anthropics/claude-code/issues/50543) macOS desktop app: change font size without scaling the whole UI | 6 | 15 | **Accessibility / ergonomics** – request for independent font size control. |

---

## Key PR Progress

Only two open pull requests were updated in the last 24 hours:

- [#73476](https://github.com/anthropics/claude-code/pull/73476) **docs: fix GitHub capitalization in README** – Minor typo fix (“Github” → “GitHub”). No functional change.
- [#75252](https://github.com/anthropics/claude-code/pull/75252) **docs: clarify plugin MCP configuration scope** – Clarifies that plugin `mcpServers` config is separate from the user’s `~/.claude.json` allow/deny list. Reopened after previous PR was deleted.

---

## Feature Request Trends

The most requested feature directions (distilled from open issues):

1. **Usage transparency** – A built‑in `claude usage` command to see token consumption per session, model, and time period. (#33978 and 10+ related issues)
2. **Cost controls that actually work** – Respect monthly limits (#23579), prevent silent billing changes (#28927), and fix false overage alarms (#39678).
3. **Independent UI scaling** – Ability to change font size without zooming the entire desktop app (#50543, #50543 duplicates).
4. **Offline / stable session resume** – Eliminate the token burn on resume (#38029) and TUI freeze on resume (#75496, #75497).
5. **Plugin marketplace reliability** – Enable update button (#45810) and improve MCP configuration docs (#75252).

---

## Developer Pain Points

Recurring frustrations from today’s issues:

- **Billing transparency & cost surges** – The top two issues (#41506, #38029) both involve unexplained token consumption spikes, with 76 combined 👍. Users feel blindsided by silent billing changes (#28927).
- **Session resume instability** – Multiple reports of terminal freezes on `claude --resume` (Windows: #75497, WSL: #75496) and abnormal token burn (#38029).
- **UI/UX regressions** – Broken text selection in VS Code (#61021), TUI corruption in long iTerm2 sessions (#68461), and unresponsive plugin updates (#45810).
- **Windows-specific woes** – Advisor unavailable (#73365), installation failure (#75485), JetBrains plugin path serialization (#75498), and Dispatch pairing failure (#75499).
- **Safety filter false positives** – Three separate “cyber” false positives today (#75504, #75503, #75491) halting legitimate reverse‑engineering work, indicating a potential oversensitivity in the Opus 4.8 safety layer.
- **Data loss risk** – One report (#75490) of desktop app worktree mechanism wiping gitignored directories from the main working tree.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-07-08

## Today’s Highlights

The `rust-v0.143.0` release landed with remote plugins enabled by default, now supporting npm marketplace sources and richer catalog rows. The community is closely watching Issue #30364, where GPT-5.5’s reasoning-token clustering at fixed boundaries (516/1034/1552) is reported to degrade complex task performance — the thread has 156 comments and 252 👍. Separately, a flurry of 12+ PRs from the core team (winston-openai) achieved atomic thread lifecycle tracking, serializing turn transitions and idle shutdown across the app-server and core crates.

## Releases

- **rust-v0.143.0** – Remote plugins are now enabled by default, with richer catalog rows, npm marketplace sources, and visible remote/local versions. Codex can route authentication and Responses API traffic through macOS and Windows system proxies, including PAC support.
- **rust-v0.143.0-alpha.39 & alpha.38** – Alpha releases with no detailed changelog.

## Hot Issues

1. **#30364** – *GPT-5.5 reasoning-token clustering at 516/1034/1552 degrading performance*  
   Highly upvoted (252 👍) bug report with 156 comments. Pattern appears model-specific and coincides with lower reasoning quality. Community is actively discussing possible misconfiguration in token-budget distribution.

2. **#21753** – *Full Claude Code Hook Parity (29+)*  
   Umbrella tracker (26 comments, 19 👍) for 29 missing lifecycle hooks. The community strongly desires a complete automation surface for every major event, with Codex-native naming.

3. **#12115** – *Dynamically loading nested AGENTS.md*  
   23 comments, 83 👍. Request for on-demand loading of child-directory AGENTS.md, similar to Claude Code’s CLAUDE.md behavior. Rated “top 100 customer” priority.

4. **#28726** – *Codex IDE extension freezes code-server sidebar on desktop Chromium*  
   14 comments. Blocks remote development on code-server; Android works fine, pointing to a browser-specific issue.

5. **#25792** – *Context compaction forgets AGENTS rules: task progress jumps from 97% to 42%*  
   13 comments. Serious reliability bug in long-running tasks – after automatic compaction, agent instructions are lost, causing regressions.

6. **#28969** – *Add setting to disable auto-resolve in 60 seconds for questions*  
   88 👍, 12 comments. Users want control over the forced auto-resolution timeout, especially during complex interactive sessions.

7. **#19195** – *Make Codex memory writability explicit when `memories = true` is enabled*  
   12 comments. Conflicting behavior: feature flag says “memories enabled” but model prompt says “never update memories”. Community requests clear signaling.

8. **#23840** – *Codex Desktop Computer Use MCP initialize times out*  
   11 comments. Same client handshake works from Terminal but fails from Desktop – likely a proxy or environment misconfiguration.

9. **#25127** – *Unable to send message (Windows/macOS)*  
   11 comments. Repeated reports of app being completely unresponsive after update, with minimal diagnostic info. High frustration.

10. **#22857** – *Better key authentication on SSH host remote connections*  
    14 👍, 11 comments. Users on iOS and Desktop want streamlined key-based SSH auth without manual key management.

## Key PR Progress

1. **#31515** – *Add client-only web search result metadata*  
   Bounded URL, title, and snippet metadata for client-facing web search items, persisted in rollout events and exposed through app-server v2 and exec JSONL.

2. **#31466** – *Capture tool search pipeline diagnostics in /feedback*  
   Replaces RUST_LOG diagnostics with an always-on, bounded, per-thread tool-search snapshot, no public API change.

3. **#31482** – *Migrate plugin commands into skills*  
   Moves command-to-skill conversion into `codex-core-plugins` to avoid dependency cycles during plugin installation.

4. **#31503** – *Detect Codex installs managed by pnpm*  
   Fixes the JavaScript shim to handle pnpm global installs so `codex doctor` and update flows report pnpm commands correctly.

5. **#31514** – *Reduce redundant filesystem syscalls*  
   Optimizations: atomic writes reuse the temp file descriptor; directory classification retained from file-search walking; replaces unnecessary `stat` calls.

6. **#31509** – *Support SQLite-disabled degraded mode*  
   Restores `sqlite = false` escape hatch for environments like NFS, skipping database init, recovery, and integrity checks.

7. **#31283** – *Support extension-owned turn items*  
   Adds `codex-extension-items` crate so extensions can own `TurnItem` schemas, starting with standalone image generation.

8. **#29793** – *Resolve app tool file paths in selected environments*  
   Supports app-tool uploads across foreign OSes between app-server and exec-server. (Closed)

9. **#31304 → #31395** (multiple closed PRs) – *Atomic thread lifecycle tracking*  
   Winston-openai’s 12-PR series serializes turn transitions, makes idle shutdown atomic, tracks thread teardown groups, and preserves activity through completion. These lay groundwork for stable long-running sessions.

10. **#31400** – *Claim thread teardown groups atomically*  
    Generalizes teardown coordinator from single `ThreadId` to an operation-owned group, deduplicating claims under one lock.

## Feature Request Trends

- **Hook parity**: The top-requested feature (#21753) aims for full Claude Code-style lifecycle hook coverage (29+ hooks). Community sees hooks as essential for CI/CD, multi-agent orchestration, and custom tooling.
- **Dynamic AGENTS.md loading**: #12115 reflects a persistent desire for hierarchical agent configuration, similar to Claude Code’s on-demand directory-specific files.
- **Memory writability control**: Users want explicit, non-contradictory signaling when `memories = true` is enabled so the model actually writes to memory (#19195).
- **Remote connection improvements**: SSH key authentication (#22857), notification support during remote sessions (#20930), and cross-platform app-server compatibility are recurring themes.
- **Per-user config overrides**: Disabling auto-resolve (#28969) and controlling sandbox profiles (#28715) show demand for fine-grained user settings.

## Developer Pain Points

- **Windows sandbox & MCP reliability**: Multiple bugs report `exec_command` failures with Git Bash (#15016), false “filename too long” errors (#31511), duplicate MCP stdio process pools causing memory bloat (#31499), and inotify watch exhaustion in VS Code (#23574).
- **Context compaction corruption**: #25792 highlights a critical reliability gap: after automatic context compaction, AGENTS rules are lost, causing task progress to regress severely.
- **GPT-5.5 reasoning token clustering**: #30364 suggests the model’s token budget is causing fixed-boundary clustering, degrading complex tasks. Impact broad across Pro and Plus users.
- **App updates break core functionality**: Multiple post-update crashes (e.g., #30608 Computer Use damaged, #29787 app doesn’t restart, #25127 unable to send message) indicate insufficient backward compatibility testing, especially on macOS and Windows.
- **Ghost conversations**: #29868 and #25397 report conversations disappearing or becoming “stale ghosts” that cannot be resumed or archived, eroding user trust.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*