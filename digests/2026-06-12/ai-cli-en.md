# AI CLI Tools Community Digest 2026-06-12

> Generated: 2026-06-12 03:34 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools (2026-06-12)

## 1. Ecosystem Overview

The AI CLI tools ecosystem is in a phase of rapid iteration and growing community engagement, with both Claude Code and OpenAI Codex shipping multiple updates daily. Developer sentiment is shaped by persistent platform friction—especially around Windows and ARM64 support, billing inconsistencies, and data loss—while feature demands converge on multi-account management, dynamic project context loading, and reliable sandbox execution. The two tools are diverging in architectural philosophy: Claude Code invests heavily in a feature-rich TUI and local VM sandbox (Cowork), while Codex is doubling down on remote execution via encrypted transports and sub-agent orchestration. Overall, the ecosystem is maturing but still struggles with regressions across updates, signaling that user trust is fragile and requires deliberate investment in stability and transparency.

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Releases today** | 2 patch releases (v2.1.173, v2.1.174) | 5 Rust alpha builds (0.140.0-alpha.8–.13) |
| **Issues updated (24h)** | 50 issues updated | 10 hot issues highlighted (many more active) |
| **Noteworthy issues (10 selected)** | 10 issues (1 open 5+ months) | 10 issues (1 closed after 197 comments) |
| **Key PRs in digest** | 10 PRs (some automated bounty PRs) | 10 PRs (infrastructure and features) |
| **Top voted feature (👍)** | Multi‑account switching: 581 👍 | Linux desktop app: 551 👍 |
| **Documentation gaps** | Undocumented hooks and UI panels | Missing recovery path for lost histories |

Both tools exhibit similar community engagement volume. Claude Code’s digest explicitly counts 50 updated issues in 24h; Codex’s digest selects 10, but the issue tracker is equally active. Codex leads in release cadence today (5 builds vs. 2), though these are alpha versions without per-release changelogs.

## 3. Shared Feature Directions

The following requirements appear across both tool communities, indicating industry-wide developer needs:

- **Multi‑account / cross‑workspace switching**  
  - Claude Code: #18435 (581 👍) – switch personal/work accounts in Desktop  
  - Codex: #27742 (new) – phone verification exemption for paying users, reflecting desire for smoother multi-account handling  

- **Linux desktop app**  
  - Codex: #11023 (551 👍) – long-standing demand for native Linux UI  
  - Claude Code: No equivalent Linux desktop request (Claude Code already runs on Linux via TUI)  

- **Dynamic / on‑demand project configuration loading**  
  - Claude Code: Users want `CLAUDE.md` to be loaded per-subdirectory (indirectly via #3412 pasted text review)  
  - Codex: #12115 (67 👍) – dynamic loading of nested `AGENTS.md` to reduce upfront context  

- **Platform reliability (ARM64, Windows sandbox)**  
  - Claude Code: #39636 – Cowork VM fails on ARM64 Windows; #29045 – heavy Hyper‑V VM overhead  
  - Codex: #26477, #26896 – sandbox setup failures on Windows 11 Enterprise  

- **Data preservation after updates**  
  - Claude Code: #40175 – Cowork global instructions silently revert to older version  
  - Codex: #20741 – desktop chat histories disappeared after update  

- **Billing and account glitches**  
  - Claude Code: #64928, #67409 – gift codes consumed, billing errors cause account downgrade  
  - Codex: #20161 (closed) – phone verification blocks paying users  

- **Terminal / input handling regressions**  
  - Claude Code: #65833 – scroll wheel sends arrow keys; #10375 – focus escape sequences  
  - Codex: #22085 – Git processes causing high CPU on Windows (input polling)  

## 4. Differentiation Analysis

| Aspect | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Primary interface** | Rich TUI with inline images proposal, scroll acceleration settings | Primarily VS Code extension + Rust CLI; Linux desktop app requested |
| **Sandbox / execution model** | Local Hyper‑V VM (Cowork) – resource-heavy, unreliable on ARM64 | Remote execution via Noise‑encrypted transport (exec-server) – multi‑platform focus |
| **Safety / policy enforcement** | Safety classifier false positives causing silent model downgrades (#66728) | Guardian system with stream‑disconnect classification (#27537) and capacity exhaustion handling (#27540) |
| **Sub‑agent architecture** | Not prominently featured; focus on single‑agent with tool use | Emphasizes sub‑agent workflows – Guardian approval, thread history builder, sub‑agent UI regressions |
| **Plugin ecosystem** | MCP server SIGTERM kills (#40207), WebSearch tool broken (#67756) | MCP client handshake failures (#6020) blocking all tool‑using workflows |
| **Config file standard** | `CLAUDE.md` – single file at project root | `AGENTS.md` – supports multiple environments (PR #27696) |
| **Release cadence & communication** | Daily stable patches with changelogs; community digest | Frequent alpha builds without changelogs; heavy automated CI |
| **Community engagement style** | Active issue voting (581 👍 top), bounty PRs via NVIDIA AI | Long‑standing feature requests (551 👍), closed issues after 197 comments |

**Key differentiators:**  
- Claude Code is optimizing for a local-first, TUI-rich experience with a focus on real-time collaboration (Cowork) and model selection flexibility (multiple plan tiers).  
- Codex is architecting for remote execution at scale (Noise transport, multi‑environment `AGENTS.md`, Guardian capacity management) and is more tied to the VS Code ecosystem.

## 5. Community Momentum & Maturity

**Claude Code** exhibits intense community momentum:
- 50 issues updated in 24 hours, with the top feature request (multi‑account, 581 👍) untouched for 5 months – indicating high demand but slower official response.
- Two stable patch releases per day with detailed changelogs signal a mature release process.
- Automated bounty PRs (NVIDIA AI, REAPR tool) are flooding the PR queue, raising questions about quality control and genuine contribution.
- Cowork/sandbox bugs on ARM64 and macOS 26 indicate growing platform heterogeneity that the community is vocal about.

**OpenAI Codex** shows similarly high engagement:
- Five alpha releases in one day point to fast backend iteration, but lack of per-release notes reduces transparency.
- Long-lived issues (#11023, 551 👍) receive no recent official updates – a risk for retaining community trust.
- PRs focus on infrastructure (Noise transport, Guardian improvements, secret storage) rather than user-facing features.
- Phone verification debacle (#20161) closed after 197 comments – a cautionary tale about authentication friction.

**Maturity assessment:** Both tools are past early adoption, now dealing with scale-related friction (platform compatibility, billing, data loss). Claude Code has more predictable stable releases; Codex is iterating faster but with less polished communication.

## 6. Trend Signals

From the community feedback, several industry trends are shaping the future of AI CLI tools:

1. **Multi-account and profile management is non-negotiable.**  
   Developers increasingly need to switch between personal, work, and enterprise accounts. The #1 feature request on both platforms.

2. **Linux desktop is the next frontier for user interface.**  
   Codex’s 551 👍 for a Linux desktop app contrasts with Claude Code’s TUI-first approach that already runs on Linux. Expect Linux-first features to become a competitive differentiator.

3. **Dynamic context loading will replace monolithic config files.**  
   Both communities want `CLAUDE.md` / `AGENTS.md` to be loaded lazily from subdirectories to avoid context bloat and improve model precision.

4. **Sandbox/VMs are causing more pain than value for local users.**  
   Heavyweight Hyper‑V VMs (Claude Code’s Cowork) and Windows sandbox failures (both tools) are driving users toward remote execution or demanding lightweight alternatives.

5. **Token and credit waste is a silent productivity killer.**  
   Background polling sending full conversation history (Codex #13733) and silent model downgrades mid-task (Claude Code #66728) erode trust in cost predictability.

6. **Billing transparency and account recovery remain weak points.**  
   Gift codes consumed without extension, phone verification blocking paying users, and histories lost after updates – all destroy user confidence.

7. **AI-assisted bug fixing is generating noise.**  
   Automated PRs (NVIDIA AI, REAPR) are becoming common, but often produce duplicate or low-quality fixes. The community needs better review processes to maintain codebase health.

**Recommendation for developers:** Prioritize stability over feature velocity. Invest in cross-platform sandbox testing (especially ARM64 Windows and macOS 26), implement robust data backup/restore, and provide clear communication on model downgrades and billing changes. The communities are loyal but increasingly vocal about regressions – now is the time to harden the core experience.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Date:** 2026-06-12 (data as of 2026-06-12)  
**Source:** [github.com/anthropics/skills](https://github.com/anthropics/skills)

---

## 1. Top Skills Ranking

The following Pull Requests represent the most-discussed Skill proposals or improvements in the official repository. All remain open as of this report.

### 1.1 `#1046` – Triple Skill Bundle: Frontend Design, AI Experience Consultant, Automation Workflows Builder
**Functionality:** Adds three new community skills: `frontend-design`, `ai-experience-consultant`, and `automation-workflows-builder`. Each targets a distinct domain—UI/UX guidance, AI-product consulting, and multi-step workflow automation.  
**Discussion highlights:** Community interest in expanding beyond technical skills into strategic/consultative areas. The bundle approach reduces repo churn.  
**Status:** Open  
[🔗 PR #1046](https://github.com/anthropics/skills/pull/1046)

### 1.2 `#514` – Document Typography Skill
**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI‑generated documents. Addresses pervasive formatting issues across all document types.  
**Discussion highlights:** High engagement—users report these problems affect nearly every generated document. Requests for integration with existing DOCX/PDF skills.  
**Status:** Open  
[🔗 PR #514](https://github.com/anthropics/skills/pull/514)

### 1.3 `#486` – ODT Skill (OpenDocument Text Creation & Conversion)
**Functionality:** Enables creation, filling, reading, and conversion of `.odt`/`.ods` files following the ISO-standard OpenDocument format. Compatible with LibreOffice.  
**Discussion highlights:** Interest in open‑source document formats; users want interoperability with government/enterprise systems that mandate ODF.  
**Status:** Open  
[🔗 PR #486](https://github.com/anthropics/skills/pull/486)

### 1.4 `#83` – Meta Skills: skill-quality-analyzer & skill-security-analyzer
**Functionality:** Two meta-skills for evaluating other skills: quality analysis across structure, documentation, and examples; security analysis for trust boundaries and privilege escalation.  
**Discussion highlights:** Strong support for tooling that helps skill authors improve their submissions. Related to broader concerns about skill safety (#492).  
**Status:** Open  
[🔗 PR #83](https://github.com/anthropics/skills/pull/83)

### 1.5 `#181` – SAP-RPT-1-OSS Predictor Skill
**Functionality:** Uses SAP’s open‑source tabular foundation model for predictive analytics on SAP business data. Targets enterprise users needing no‑code forecasting.  
**Discussion highlights:** Niche but passionate audience. Technical discussion about model integration and data privacy.  
**Status:** Open  
[🔗 PR #181](https://github.com/anthropics/skills/pull/181)

### 1.6 `#1140` – Agent Creator Skill & Multi‑Tool Evaluation Fix
**Functionality:** Adds `agent-creator` meta-skill for composing task-specific agent sets, plus critical stability fixes in evaluation scripts and Windows path handling.  
**Discussion highlights:** Addresses the highly‑upvoted issue #1120. Includes multiple cross‑platform fixes, indicating high maintenance value.  
**Status:** Open  
[🔗 PR #1140](https://github.com/anthropics/skills/pull/1140)

### 1.7 `#723` – Testing Patterns Skill
**Functionality:** Comprehensive coverage of testing philosophy (Trophy model), unit testing (AAA), React Testing Library, end‑to‑end testing, and performance testing.  
**Discussion highlights:** Broad interest from web developers. Requests to extend to backend testing patterns.  
**Status:** Open  
[🔗 PR #723](https://github.com/anthropics/skills/pull/723)

### 1.8 `#806` – Sensory Skill (macOS Automation via AppleScript)
**Functionality:** Teaches Claude to use `osascript` for native macOS automation, bypassing screenshot‑based computer use. Two‑tier permission system (direct app scripting + Accessibility API).  
**Discussion highlights:** Enthusiasm for native desktop automation; privacy/security concerns about Accessibility permissions.  
**Status:** Open  
[🔗 PR #806](https://github.com/anthropics/skills/pull/806)

---

## 2. Community Demand Trends

From the most‑commented Issues, the community’s strongest demands fall into these categories:

| Trend | Evidence | Key Issues |
|-------|----------|------------|
| **Skill distribution & sharing** | #228 (14 comments, 👍7) requests org‑wide sharing; #492 (7 comments) flags trust‑boundary risks in the `anthropic/` namespace | [#228](https://github.com/anthropics/skills/issues/228), [#492](https://github.com/anthropics/skills/issues/492) |
| **Tooling reliability** | #556 (12 comments, 👍7) documents `run_eval.py` 0% recall bug; #1061 (3 comments) reports Windows subprocess failures; #1169 (2 comments) confirms same bug persists | [#556](https://github.com/anthropics/skills/issues/556), [#1061](https://github.com/anthropics/skills/issues/1061), [#1169](https://github.com/anthropics/skills/issues/1169) |
| **Governance & safety** | #412 (4 comments) proposes `agent-governance` skill; #1175 (3 comments) raises SharePoint permission concerns | [#412](https://github.com/anthropics/skills/issues/412), [#1175](https://github.com/anthropics/skills/issues/1175) |
| **Platform expansion** | #29 (4 comments) requests Bedrock integration; #16 (4 comments) asks to expose skills as MCPs | [#29](https://github.com/anthropics/skills/issues/29), [#16](https://github.com/anthropics/skills/issues/16) |
| **Skill authorship improvements** | #202 (8 comments) demands a rewritten `skill-creator`; #1220 (2 comments) requests multi‑file bundling | [#202](https://github.com/anthropics/skills/issues/202), [#1220](https://github.com/anthropics/skills/issues/1220) |

**Most‑requested new skill directions** emerging from Issues and PR activity: workflow automation, test generation, document quality assurance, enterprise data integration (SAP, ODT), and agent governance.

---

## 3. High‑Potential Pending Skills

These open PRs have active discussion and are likely to land soon based on recent updates and criticality:

- **#1298 – Fix `run_eval.py` 0% recall** (updated 2026-06-11)  
  Directly addresses the #556 blocker that makes skill evaluation useless. Multiple contributors involved.  
  [🔗 PR #1298](https://github.com/anthropics/skills/pull/1298)

- **#1050 – Windows subprocess + encoding fixes** (updated 2026-05-24)  
  Two‑line fix for `PATHEXT` and pipe encoding, unblocking Windows users running `run_loop.py`.  
  [🔗 PR #1050](https://github.com/anthropics/skills/pull/1050)

- **#1099 – Fix `run_eval.py` crash on Windows** (updated 2026-05-24)  
  Fixes `WinError 10038` that causes 0% recall on Windows. Complementary to #1050.  
  [🔗 PR #1099](https://github.com/anthropics/skills/pull/1099)

- **#723 – Testing Patterns Skill** (updated 2026-04-21)  
  High community interest; ready for final review.  
  [🔗 PR #723](https://github.com/anthropics/skills/pull/723)

- **#806 – Sensory Skill (macOS)** (updated 2026-04-02)  
  Unique native‑automation capability; permission‑model discussion nearly resolved.  
  [🔗 PR #806](https://github.com/anthropics/skills/pull/806)

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for robust meta-tooling (skill evaluation, creation, and cross‑platform compatibility) and specialized skills that address concrete quality gaps—typography, document formats, testing, and native OS automation—rather than abstract workflow templates.**

---

# Claude Code Community Digest — 2026-06-12

## Today's Highlights

Two patch releases (v2.1.173 and v2.1.174) shipped with fixes for scroll acceleration, model picker display, Fable 5 naming, and Windows sandbox warnings. Community activity is intense: 50 issues updated in 24h, with the top-voted feature request (multi-account switching, 581 👍) still open after 5 months, and a new scroll wheel regression (#65833) quickly gaining attention. A cluster of Cowork/sandbox bugs on ARM64 Windows and macOS 26 signals growing platform friction.

## Releases

**[v2.1.174](https://github.com/anthropics/claude-code/releases/tag/v2.1.174)**  
- Added `wheelScrollAccelerationEnabled` setting to disable mouse‑wheel scroll acceleration in fullscreen mode.  
- Fixed `/model` picker so Opus appears as its own row on Max/Team Premium/Enterprise plans, and Sonnet on Pro/Team plans (previously the model family that Default resolves to was hidden).

**[v2.1.173](https://github.com/anthropics/claude-code/releases/tag/v2.1.173)**  
- Fixed Fable 5 model names with `[1m]` suffix not being normalized (1M context is now stripped automatically).  
- Fixed spurious “sandbox dependencies missing” startup warning on Windows when sandbox was enabled in settings.

## Hot Issues (10 Noteworthy)

1. **[#18435 – Add multi‑account management in Claude Desktop](https://github.com/anthropics/claude-code/issues/18435)**  
   *581 👍, 113 comments*  
   The community’s most‑requested feature: switch between multiple Claude accounts/profiles. Still open after five months with no official response.

2. **[#3412 – Allow viewing/editing pasted text before submission](https://github.com/anthropics/claude-code/issues/3412)**  
   *266 👍, 74 comments*  
   macOS dictation users hit collapsed “Pasted” blocks they cannot review. A long‑standing a11y gap.

3. **[#10375 – Focus‑reporting escape sequences injected into input](https://github.com/anthropics/claude-code/issues/10375)**  
   *30 👍, 27 comments*  
   `[I`/`[O` sequences appear when using mouse/modifiers in WezTerm. Affects many terminal users.

4. **[#39636 – Cowork VM never boots on Snapdragon X Plus (ARM64)](https://github.com/anthropics/claude-code/issues/39636)**  
   *9 👍, 27 comments*  
   Connection timeout every attempt on ARM64 Windows — a blocker for new hardware users.

5. **[#29045 – Claude Desktop spawns 1.8 GB Hyper‑V VM for chat‑only use](https://github.com/anthropics/claude-code/issues/29045)**  
   *54 👍, 25 comments*  
   Even when not using Cowork, a heavy Hyper‑V VM is launched. Concerns over resource waste.

6. **[#65833 – Scroll wheel now sends arrow keys instead of scrolling](https://github.com/anthropics/claude-code/issues/65833)**  
   *16 👍, 14 comments*  
   Regression in v2.1.150: mouse scroll cycles input history instead of scrolling conversation. Affects WSL users.

7. **[#40175 – Cowork global instructions silently revert to older version](https://github.com/anthropics/claude-code/issues/40175)**  
   *10 👍, 21 comments*  
   After saving, global instructions sometimes revert — data loss in critical workflow config.

8. **[#66728 – Safety classifier false positive forces mid‑task model downgrade](https://github.com/anthropics/claude-code/issues/66728)**  
   *0 👍, 9 comments*  
   Fable 5 → Opus 4.8 downgrade during PR review‑reply when syscall/ABI content is flagged. Silent model switch breaks workflows.

9. **[#40207 – Claude Code sends SIGTERM to all healthy stdio MCP servers after 10‑60s](https://github.com/anthropics/claude-code/issues/40207)**  
   *4 👍, 10 comments*  
   Strace evidence shows healthy MCP servers killed without error. Shrinking timeout over session.

10. **[#67756 – WebSearch tool broken: internal model claude‑haiku‑4‑5 not found](https://github.com/anthropics/claude-code/issues/67756)**  
    *0 👍, 1 comment*  
    Freshly reported in v2.1.174. WebSearch fails because an internal Haiku model endpoint is missing.

## Key PR Progress (10)

1. **[#67753 – fix(ralph‑wiggum): case‑insensitive completion promise matching](https://github.com/anthropics/claude-code/pull/67753)**  
   Uses `tr` for portable case‑insensitive matching of completion promises. Prevents false negatives when Claude outputs different casing.

2. **[#67722 – [BUG] Claude autonomously ran background scripts calling a paid external](https://github.com/anthropics/claude-code/pull/67722)**  
   Open PR addressing an autonomous action bug. Proposes a GitHub Actions deduplication workflow.

3. **[#67699 & #67697 – Automated NVIDIA AI fixes for “Claude autonomously ran background scripts”](https://github.com/anthropics/claude-code/pull/67699)**  
   Two identical `/bounty` PRs by mkcash using NVIDIA AI to fix #67654. Raises questions about automated bounty farming.

4. **[#67599 – Fix false‑positive cybersecurity flag on content‑moderation discussion](https://github.com/anthropics/claude-code/pull/67599)**  
   Automated fix via REAPR tool for #67557. Addresses API error when discussing legitimate moderation topics.

5. **[#61956 – Correct state file path in ralph‑wiggum help.md](https://github.com/anthropics/claude-code/pull/61956)**  
   Closed. Fixes a documentation path mismatch that would break plugin setup.

6. **[#50301 – Add flappy‑claude terminal game plugin](https://github.com/anthropics/claude-code/pull/50301)**  
   Closed. A fun `/flappy‑claude` slash command using pure Python curses — community contribution merged.

7. **[#54551 – Proposal: inline image rendering in the TUI](https://github.com/anthropics/claude-code/pull/54551)**  
   Closed. Feature proposal for rendering images in Claude Code TUI (only client missing inline images). Links to tracking issue #54546.

8. **[#41695 & #41694 – PermissionDenied hook example with retry and audit logging](https://github.com/anthropics/claude-code/pull/41695)**  
   Two identical closed PRs adding example for the undocumented `PermissionDenied` hook. Demonstrates retry and logging.

9. **[#64489 – Updated example file](https://github.com/anthropics/claude-code/pull/64489)**  
   Minor update to example file. Still open.

10. **[#67409 – [baobao] [BUG] Account downgraded due to billing error](https://github.com/anthropics/claude-code/pull/67409)**  
    Open bounty PR ($200) via NVIDIA AI to fix billing downgrade issue #67407.

## Feature Request Trends

- **Multi‑account/profile switching** (#18435, 581 👍) remains the #1 community ask — users want to switch between personal/work accounts in the Desktop app.
- **Pasted text review** (#3412, 266 👍) — users demand ability to inspect/edit content pasted from dictation or other sources before submission.
- **Inline image rendering in TUI** (#54551) — Claude Code is the only Claude client that cannot display images inline.
- **Scroll wheel behavior** — multiple issues (#65833, #67766) show users expect predictable scrolling, not arrow‑key emulation.
- **Cowork/sandbox improvements** — requests for lighter VM footprint (#29045), ARM64 support (#39636), and reliable global instructions (#40175).

## Developer Pain Points

1. **Silent model downgrades** (#66728) — safety classifier false positives force downgrade from Fable 5 to Opus without clear notification, breaking long‑running tasks.
2. **Cowork VM instability** — ARM64 Windows (#39636), macOS 26 networking entitlements (#66870), and DNS resolution failures (#67739) make the sandbox unreliable across platforms.
3. **MCP server reliability** — SIGTERM kills (#40207), streaming JSON parser corruption (#67765), and missing Haiku model for WebSearch (#67756) erode trust in the plugin ecosystem.
4. **Billing and account glitches** — gift codes silently consumed (#64928), subscriptions not extended (#67750), and account downgrades due to billing errors (#67409) cause frustration.
5. **TUI rendering regressions** — scroll wheel broken (#65833), tab‑indented code not displayed (#67763), focus escape sequences injected (#10375) — each patch risks breaking terminal UX.
6. **Documentation gaps** — new VS Code usage panel (#67746) and PermissionDenied hooks (#41695) undocumented, forcing users to reverse‑engineer features.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-12

## Today's Highlights

A flurry of Rust alpha releases (0.140.0-alpha.8 through .13) landed today, signaling active backend iteration. The community remains engaged on long-standing pain points: a closed phone‑verification bug (#20161) garnered 197 comments and 121 👍, while a Linux desktop app feature request (#11023) continues to attract attention with 551 👍. On the PR front, the team is advancing critical infrastructure for remote execution (Noise transport, environment metadata) and polishing sub‑agent and Guardian workflows.

## Releases

Five **rust‑v0.140.0‑alpha** builds were published in the last 24 hours:  
- `0.140.0-alpha.13`, `0.140.0-alpha.11`, `0.140.0-alpha.10`, `0.140.0-alpha.9`, `0.140.0-alpha.8`  
- No individual changelogs were provided; these are likely incremental patches or version bumps from automated CI.

## Hot Issues (10 selected)

1. **#20161 (CLOSED) – Phone number verification doesn’t work**  
   *Sistem-Pack* — 197 comments, 121 👍  
   A critical authentication bug that broke SSO workflows by forcing phone verification on users who never added a phone. Closed after extensive community outcry.  
   [Link](https://github.com/openai/codex/issues/20161)

2. **#11023 (OPEN) – Codex desktop app for Linux**  
   *Suhaibinator* — 105 comments, 551 👍  
   The most‑voted feature request on the board. Users want a native Linux app to avoid power‑management issues on Mac and to leverage high‑performance Linux desktops.  
   [Link](https://github.com/openai/codex/issues/11023)

3. **#3567 (CLOSED) – Undo does not work on Windows**  
   *Polinarium* — 58 comments, 29 👍  
   A VS Code extension bug where full‑agent edits cannot be undone. Closed after a long discussion, but many Windows users still experience related issues.  
   [Link](https://github.com/openai/codex/issues/3567)

4. **#6020 (OPEN) – MCP client handshaking failure**  
   *kirso* — 42 comments, 27 👍  
   All MCP servers fail with “connection closed: initialize response” on Pro subscriptions using GPT‑5. Blocks any tool‑using workflow via MCP.  
   [Link](https://github.com/openai/codex/issues/6020)

5. **#20741 (OPEN) – Desktop project chat histories disappeared after update**  
   *GGBondBlueWhale* — 38 comments, 14 👍  
   After a recent app update, macOS users lost all project‑level conversation history. No data recovery path documented.  
   [Link](https://github.com/openai/codex/issues/20741)

6. **#13733 (OPEN) – Background process polling wastes tokens**  
   *jitlabs-sg* — 27 comments, 22 👍  
   Each `write_stdin` poll during long‑running builds sends the full conversation history, burning credits. Community demands smarter incremental polling.  
   [Link](https://github.com/openai/codex/issues/13733)

7. **#12115 (OPEN) – Dynamically loading nested `AGENTS.md`**  
   *kszlim* — 20 comments, 67 👍  
   Users want on‑demand loading of `AGENTS.md` from subdirectories, similar to Claude Code’s `CLAUDE.md`. Currently all `AGENTS.md` files are loaded upfront.  
   [Link](https://github.com/openai/codex/issues/12115)

8. **#22085 (CLOSED) – Windows: Git processes cause high CPU**  
   *azsama* — 12 comments, 17 👍  
   After a recent update, Codex spawns thousands of Git for Windows processes per minute, rendering machines unusable. Closed but workaround unclear.  
   [Link](https://github.com/openai/codex/issues/22085)

9. **#27205 (OPEN) – CLI `followup_task` encrypted parameter error**  
   *cowwoc* — 9 comments, 5 👍  
   `Invalid Value: 'tools'. Function ... declares encrypted parameters but is not configured` — a model‑compatibility regression on gpt‑5.4 with CLI 0.138.0.  
   [Link](https://github.com/openai/codex/issues/27205)

10. **#17991 (OPEN) – Windows Summary tab shows false PR errors for WSL repos**  
    *tompw89* — 8 comments, 0 👍  
    The desktop app’s Summary tab incorrectly reports GitHub CLI/PR errors and logs `ENOENT` on `.git` paths when working with WSL‑based repositories.  
    [Link](https://github.com/openai/codex/issues/17991)

## Key PR Progress (10 selected)

1. **#27751 – Expose Bedrock credential source in `account/read`**  
   *celia-oai* — Allows the UI to distinguish Codex‑managed Bedrock keys from user‑supplied AWS credentials, simplifying account‑state rendering.  
   [Link](https://github.com/openai/codex/pull/27751)

2. **#27504 – Add secret auth storage configuration**  
   *celia-oai* — Workaround for Windows Credential Manager’s 2,560‑byte blob limit; introduces an encrypted local secrets backend with a configurable selection layer.  
   [Link](https://github.com/openai/codex/pull/27504)

3. **#27750 – Add incremental thread history changes**  
   *wiltzius-openai* — New `ThreadHistoryBuilder` APIs that coalesce repeated rollout item changes, reducing overhead when syncing thread state.  
   [Link](https://github.com/openai/codex/pull/27750)

4. **#27723 – Preserve user goal evidence in approval review**  
   *fchen-oai* — Stores canonical goal objectives as separate “user‑provided goal” evidence in Guardian approval, excluding metadata and duplicates.  
   [Link](https://github.com/openai/codex/pull/27723)

5. **#27537 – Preserve Guardian stream‑disconnect classification**  
   *kbazzi* — Distinguishes infrastructure failures (e.g., websocket reset) from policy denials, so transient disconnects are not reported as false rejections.  
   [Link](https://github.com/openai/codex/pull/27537)

6. **#26245 – exec‑server: default remote transport to Noise**  
   *viyatb-oai* — Ties the Noise authenticated‑encryption transport to executor registration and runtime startup, securing remote harness ↔ executor traffic.  
   [Link](https://github.com/openai/codex/pull/26245)

7. **#27540 – Treat Guardian capacity exhaustion as unavailable**  
   *kbazzi* — After retry budget exhaustion due to `server_is_overloaded`, marks the session as unavailable instead of silently failing.  
   [Link](https://github.com/openai/codex/pull/27540)

8. **#25866 – fix(apply‑patch): handle CRLF gracefully**  
   *dylan-hurd-oai* — Adds a disabled‑by‑default flag to preserve CRLF line endings when applying patches, preventing unwanted changes to Windows‑style files.  
   [Link](https://github.com/openai/codex/pull/25866)

9. **#27696 – Load `AGENTS.md` from all bound environments**  
   *anp-oai* — Extends multi‑environment support: the model now sees `AGENTS.md` files from every bound environment, not just the primary one.  
   [Link](https://github.com/openai/codex/pull/27696)

10. **#27702 (CLOSED) – Parallelize release code generation**  
    *tamird* — Switches from single codegen unit to four units, using ThinLTO to cut the critical‑path build time without sacrificing binary size.  
    [Link](https://github.com/openai/codex/pull/27702)

## Feature Request Trends

- **Linux desktop app** (#11023, 551 👍) – Dominant demand for a native Linux GUI, driven by dissatisfaction with Mac power consumption and desire for Linux performance.
- **Multi‑repo support** (#11956) – Users want to point Codex at multiple directories/repos (like Claude Code) to handle cross‑service changes seamlessly.
- **Dynamic `AGENTS.md` loading** (#12115, 67 👍) – On‑demand loading of project‑guidance files from subdirectories to reduce upfront context bloat.
- **Phone verification exemption for paying users** (#27742) – Long‑time subscribers request removal of mandatory phone verification, citing privacy and friction.
- **Remote app‑server thread orchestration** (#25482) – Ability to list/manage threads created on an SSH host from the Desktop UI, enabling mixed local/remote workflows.
- **Better Windows sandbox and UAC handling** – Multiple issues (#26477, #26896) request fixes for sandbox setup and permission elevation on Windows 11 Enterprise.

## Developer Pain Points

- **Forced phone verification** (#20161, 197 comments) – Even users without a phone number were blocked, causing account lockouts and significant backlash.
- **Data loss after app updates** (#20741) – Chat histories disappearing without backup or restore path.
- **Token / credit waste** (#13733) – Polling loops during background processes dramatically inflate API usage, affecting both Pro and Enterprise users.
- **Windows performance degradation** (#22085, #20567) – Uncontrolled Git process spawning and high CPU after updates.
- **Windows sandbox failures** (#26477, #26896, #27633) – Persistent `CreateProcessAsUserW`, `os error 740`, and missing dependencies on Windows 11.
- **MCP client unreliability** (#6020) – All‑or‑nothing handshake failures block tool‑based workflows.
- **macOS V8 crashes after system updates** (#27358) – `SIGTRAP` in V8 due to hardened‑runtime entitlement issues.
- **Sub‑agent UI regressions** (#27350) – Blank transcript pane after spawning subagents, reducing visibility into multi‑agent sessions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*