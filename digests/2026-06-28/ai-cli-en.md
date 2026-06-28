# AI CLI Tools Community Digest 2026-06-28

> Generated: 2026-06-28 03:25 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Ecosystem Report: AI CLI Developer Tools
**Date**: 2026-06-28 | **Tools Covered**: Claude Code, OpenAI Codex

---

## 1. Ecosystem Overview

The AI CLI tools landscape shows a mature but **fractured stability picture** in late June 2026. Both Claude Code and OpenAI Codex face unresolved blocking issues—thinking summary rendering and rate-limit cost spikes—that directly impact daily developer productivity. The ecosystem is simultaneously investing heavily in **agent autonomy** (co-working, manual compaction, self-feedback loops) and **cross-platform reliability** (ARM64 Windows, Linux desktop parity). Community engagement remains high, but frustration is mounting around unaddressed root-cause bugs and opaque pricing changes. The MCP protocol continues to be a hotspot for integration work, with both tools investing in OAuth serialization and credential management, suggesting a maturing third-party ecosystem that demands better reliability guarantees.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Releases (24h)** | None | 3 alpha releases (rust-v0.143.0-alpha.27–.29) |
| **Hot Issues (noteworthy)** | 10 | 10 |
| **PRs in flight** | 2 (both minor) | 10+ active (including a 6-PR OAuth stack) |
| **Critical/blocking bugs** | Opus 4.7 thinking summaries (4 duplicates), Cowork ARM64 blocker, Safety classifier outage | Rate-limit cost spike (10–20×), SQLite log churn (partially fixed), GPT-5.5/Responses-Lite incompatibility |
| **Community engagement (top issue)** | #49268 (75 👍, 46 comments) | #28879 (334 👍, 186 comments) |
| **Platform pain points** | Windows ARM64, Git worktree lock pollution | Windows ARM64 sandbox, macOS zombie processes |

**Key observation**: Codex is shipping more aggressively (multiple alphas per day, a large PR stack), while Claude Code is stalled on core bugs with no shipping fixes despite community root-cause analysis. Codex's rate-limit issue has 4× the engagement of Claude's top bug.

---

## 3. Shared Feature Directions

The following requirements emerge across **both** tool communities:

| Requirement | Claude Code | OpenAI Codex | Notes |
|---|---|---|---|
| **File/path exclusion** | Implicit via `.gitignore` issues | Explicit request for `.codexignore` (#2847, 414 👍) | Codex community more vocal; Claude users rely on git-based filtering |
| **OS-level notifications** | VS Code extension (#57230, 14 👍) + CLI/TUI (#67220) | Not explicitly requested, but related attention-surfacing issues exist | Both want to reduce manual polling |
| **MCP stability & credential management** | Instruction handling gaps (#23808, #43474), env var inconsistency (#71924) | OAuth refresh races (#30292–#30296 stack), fd leaks (#26984) | Both investing in serialization and recovery mechanisms |
| **Cross-platform parity** | Windows ARM64 Cowork (#39636, 9 months open) | Linux desktop app (#11023, 650 👍), Windows ARM64 sandbox (#24259) | ARM64 Windows is the common pain point |
| **Usage transparency** | No equivalent | Rate-limit expiry display (#30395 PR) | Codex actively shipping transparency tooling |
| **Agent autonomy/self-improvement** | Self-feedback signals (#71937), manual compaction (#65114) | Non-blocking MCP orchestration (#30399) | Both envision agents that learn and act without human intervention |

**Emerging pattern**: The tension between **agent autonomy** and **user control** is a cross-cutting theme. Communities want configurable confirmation flows (Claude's clickable Yes/No toggle #70622, Codex's per-edit confirmation #24325), while also requesting agents that can self-improve and auto-compact.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary focus** | Agent autonomy, co-working, workflow automation | IDE integration, model flexibility, enterprise policy |
| **Target user** | Power developers comfortable with CLI/TUI and Cowork agent | Broader developer base (VS Code + desktop app) |
| **Technical approach** | Harness-based model orchestration with explicit state management (e.g., `display: "summarized"`) | Rust-based alpha releases with concurrent feature development (OAuth, telemetry, rate-limit tooling) |
| **Key strength** | Cowork agent model (multi-session autonomy) | Model variety (+ GPT-5.5, Responses-Lite) and active PR throughput |
| **Key weakness** | Stalled bug fixes (thinking summaries 2+ months); slow PR pipeline | Opaque pricing changes; SQLite log bloat; Linux gap |
| **Platform maturity** | Strong on macOS/Linux; Windows ARM64 is second-class | macOS-native; Windows ARM64 and Linux are gaps |
| **Community relationship** | Deep technical analysis by users (root cause identified, one-line fixes proposed) | High engagement but less technical community contribution; team drives fixes |

**Strategic divergence**: Claude Code is betting on **agentic workflows** (Cowork, compaction, self-feedback) as the differentiator, while OpenAI Codex is investing in **enterprise readiness** (marketplace policy enforcement, OAuth serialization, rate-limit tooling) and **platform expansion** (Linux desktop remains #1 feature request). Claude's community is more technically engaged (diagnosing harness bugs), while Codex's community is more focused on cost and usability.

---

## 5. Community Momentum & Maturity

| Tool | Community Size Indicators | Iteration Velocity | Developer Sentiment |
|---|---|---|---|
| **Claude Code** | High engagement on specific bugs (75 👍 for thinking summaries); moderate overall | **Low**: No releases in 24h, only 2 minor PRs, critical bugs unaddressed for months | **Frustrated but analytical**: Users root-cause issues but see no fixes; trust is eroding |
| **OpenAI Codex** | Very high engagement (334 👍 on rate-limit bug); larger overall community | **High**: 3 alphas/day, 10+ PRs in flight, coordinated OAuth work | **Agitated but engaged**: Users are vocal about cost spikes, but team is shipping fixes and transparency tooling |

**Maturity assessment**:
- **Claude Code**: Mature tool with a **stagnation risk**. Core features (thinking summaries) remain broken for months. The community's deep technical analysis is a strength, but the lack of shipping velocity suggests organizational bottlenecks or prioritization misalignment.
- **OpenAI Codex**: **Rapidly iterating** but with **stability concerns**. The alpha cadence is impressive, but the silent rate-limit change without communication is a trust deficit. The OAuth PR stack signals investment in core reliability, but the SQLite log fix is incomplete on Windows.

**Conclusion**: Codex has more community momentum and shipping velocity. Claude Code has deeper community technical engagement but is losing credibility due to unaddressed bugs.

---

## 6. Trend Signals

### For Developer Tool Builders

1. **Cost transparency is table stakes**: The Codex rate-limit crisis (10–20× cost spike, no communication) demonstrates that opaque pricing changes can erode trust faster than any feature gap. Expect users to demand **real-time usage dashboards** and **budget caps**.

2. **MCP is the new API boundary**: Both tools are investing in OAuth serialization, credential stores, and concurrent-access handling. The MCP ecosystem is moving from "works on my machine" to **production-grade authentication**. Expect credential management tooling to become a competitive differentiator.

3. **ARM64 Windows is the next platform war**: Both tools have issues on Snapdragon X hardware. As Microsoft pushes ARM64 for Windows, AI CLI tools that ship stable support first will capture early-adopter mindshare.

4. **Agent self-improvement is inevitable**: Multiple feature requests across both tools ask for agents that learn from implicit signals (response resumption, edit patterns) and auto-optimize (compaction, memory updates). The next frontier is **observable, controllable agent autonomy**.

5. **UI configurability is under-invested**: Clickable prompts, custom keybindings, notification channels—users want to shape the interaction model. The one-size-fits-all approach is showing limits as power users demand personalization.

6. **Platform parity is a competitive moat**: Linux desktop (Codex #11023, 650 👍) and Windows ARM64 (both tools) are gaps. The first tool to deliver seamless cross-platform experience (including notifications, sandbox, and performance) will differentiate.

7. **Safety pipeline resilience**: Claude's classifier outage (#69950) blocked all tool calls with no fallback. As these tools become critical infrastructure, **graceful degradation** under safety service failures is a design requirement.

---

*Report generated from community digest data. All issue numbers, comment counts, and reaction counts sourced from GitHub repositories for Claude Code (anthropics/claude-code) and OpenAI Codex (openai/codex).*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-06-28 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

The most-discussed Skill submissions by community engagement, current status:

**#1. [PR #1298] fix(skill-creator): run_eval.py always reports 0% recall**
- **Author:** MartinCajiao | **Status:** Open (Jun 2026)
- **Function:** Fixes the core evaluation pipeline where `run_eval.py` reports `recall=0%` for every skill description, rendering the optimization loop useless. Addresses 10+ independent reproductions (#556). Fixes include installing eval artifacts as real skills, Windows stream reading, trigger detection, and parallel worker logic.
- **Discussion highlights:** Highest-engagement PR. The 0% recall bug has been independently reproduced by multiple community members, making this the most critical blocker for the skill-creator workflow.
- **Link:** [PR #1298](https://github.com/anthropics/skills/pull/1298)

**#2. [PR #514] Add document-typography skill**
- **Author:** PGTBoos | **Status:** Open (Mar 2026)
- **Function:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents — issues affecting every document Claude produces.
- **Discussion highlights:** Strong community resonance. Users note this addresses a persistent quality gap that users rarely explicitly request but universally notice.
- **Link:** [PR #514](https://github.com/anthropics/skills/pull/514)

**#3. [PR #538] fix(pdf): correct case-sensitive file references in SKILL.md**
- **Author:** Lubrsy706 | **Status:** Open (Mar 2026)
- **Function:** Fixes 8 case-sensitivity mismatches (`REFERENCE.md` → `reference.md`, `FORMS.md` → `forms.md`) that break on case-sensitive file systems (Linux/macOS).
- **Discussion highlights:** Simple but high-impact fix. Reveals cross-platform portability gaps in the existing skill collection.
- **Link:** [PR #538](https://github.com/anthropics/skills/pull/538)

**#4. [PR #486] Add ODT skill — OpenDocument text creation and template filling**
- **Author:** GitHubNewbie0 | **Status:** Open (Mar 2026)
- **Function:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Triggers on "ODT", "ODS", "ODF", "OpenDocument", "LibreOffice" mentions.
- **Discussion highlights:** Addresses demand for open-source document format support, complementing existing DOCX/PDF skills.
- **Link:** [PR #486](https://github.com/anthropics/skills/pull/486)

**#5. [PR #210] Improve frontend-design skill clarity and actionability**
- **Author:** justinwetch | **Status:** Open (Jan 2026)
- **Function:** Revises existing frontend-design skill so every instruction is executable within a single conversation, with specific enough guidance to steer behavior without over-constraining.
- **Discussion highlights:** Represents a class of "skill improvement" PRs that refine existing skills rather than adding new ones — a growing community pattern.
- **Link:** [PR #210](https://github.com/anthropics/skills/pull/210)

**#6. [PR #83] Add skill-quality-analyzer and skill-security-analyzer**
- **Author:** eovidiu | **Status:** Open (Nov 2025)
- **Function:** Two meta-skills: quality analysis across structure/documentation/functionality/security/usability dimensions, and security analysis for identifying vulnerabilities in other Claude Skills.
- **Discussion highlights:** Represents the "meta-skill" trend — skills that analyze other skills. Longest-running open PR with sustained interest.
- **Link:** [PR #83](https://github.com/anthropics/skills/pull/83)

**#7. [PR #541] fix(docx): prevent tracked change w:id collision with existing bookmarks**
- **Author:** Lubrsy706 | **Status:** Open (Mar 2026)
- **Function:** Fixes document corruption when DOCX skill adds tracked changes to documents with existing bookmarks. Root cause: shared `w:id` ID space collision.
- **Discussion highlights:** Demonstrates deep OOXML domain expertise from the community. Specific, well-documented fix.
- **Link:** [PR #541](https://github.com/anthropics/skills/pull/541)

**#8. [PR #539] fix(skill-creator): warn on unquoted description with YAML special characters**
- **Author:** Lubrsy706 | **Status:** Open (Mar 2026)
- **Function:** Pre-parse validation in `quick_validate.py` detecting unquoted `description` fields containing `:` that cause silent YAML parsing failures.
- **Discussion highlights:** Duplicated effort with #361 (Mr-Neutr0n) — indicates high community pain point around YAML parsing in skill definitions.
- **Link:** [PR #539](https://github.com/anthropics/skills/pull/539)

---

## 2. Community Demand Trends

From Issue activity (50 total issues, sorted by comments), the most-anticipated new Skill directions:

| Demand Area | Signal | Key Issue |
|-------------|--------|-----------|
| **Organizational skill sharing & governance** | #228 (14 comments, 7 👍) — Users want org-wide skill libraries, direct sharing links, and permission controls | [#228](https://github.com/anthropics/skills/issues/228) |
| **Skill-creator pipeline reliability** | #556 (12 comments, 7 👍) — 0% trigger rate bug; #202 (8 comments) — skill-creator reads like dev docs not operational skill; #1169 (3 comments) — recall=0% on literal slash-command queries | [#556](https://github.com/anthropics/skills/issues/556) |
| **Security & trust boundary** | #492 (23 comments, 2 👍) — Community skills under `anthropic/` namespace enable trust abuse; #1175 (4 comments) — SharePoint document security concerns | [#492](https://github.com/anthropics/skills/issues/492) |
| **Windows compatibility** | #1061 (3 comments, 1 👍) — All three core scripts fail on native Windows (PATHEXT, cp1252 encoding, select on pipes) | [#1061](https://github.com/anthropics/skills/issues/1061) |
| **Duplicate skill installation** | #189 (6 comments, 9 👍) — `document-skills` and `example-skills` plugins install identical content | [#189](https://github.com/anthropics/skills/issues/189) |
| **Memory & persistent context** | #1329 (6 comments) — "compact-memory" proposal for symbolic notation of agent state across conversations | [#1329](https://github.com/anthropics/skills/issues/1329) |
| **Agent governance patterns** | #412 (6 comments) — Safety patterns: policy enforcement, threat detection, trust scoring, audit trails | [#412](https://github.com/anthropics/skills/issues/412) |
| **MCP protocol integration** | #16 (4 comments) — Expose Skills as MCP tools for standardized API surface | [#16](https://github.com/anthropics/skills/issues/16) |
| **AWS Bedrock support** | #29 (4 comments) — Run Skills outside Claude.ai/desktop | [#29](https://github.com/anthropics/skills/issues/29) |

**Emerging themes:** The community is shifting from "what Skills can Claude perform" to "how do we manage, secure, and distribute Skills at scale." Security (#492), governance (#412), and sharing infrastructure (#228) collectively outpace individual skill proposals.

---

## 3. High-Potential Pending Skills

Active-comment PRs not yet merged — these Skill submissions have traction and may land soon:

| PR | Skill | Author | Status | Why Watch |
|----|-------|--------|--------|-----------|
| [#1298](https://github.com/anthropics/skills/pull/1298) | run_eval.py 0% recall fix | MartinCajiao | Open (Jun 2026) | **Highest priority fix** in the repo. Blocks all skill-creator users. Latest update Jun 23. |
| [#1323](https://github.com/anthropics/skills/pull/1323) | run_eval trigger detection fix | Polluelo978 | Open (Jun 2026) | Companion fix to #1298. Addresses same 0% recall from different root cause. Updated Jun 25. |
| [#1099](https://github.com/anthropics/skills/pull/1099) | Windows crash on subprocess pipe | joshuawowk | Open (May 2026) | Windows-blocker fix. Every query recorded as "not triggered." Updated May 24. |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns skill | 4444J99 | Open (Mar 2026) | Comprehensive testing skill (Trophy model, AAA pattern, React, E2E, visual regression). Addresses explicit testing demand gap. |
| [#181](https://github.com/anthropics/skills/pull/181) | SAP-RPT-1-OSS predictor | amitlals | Open (Dec 2025) | Tabular foundation model for SAP business data. Niche but deep enterprise value. |
| [#360](https://github.com/anthropics/skills/pull/360) | AppDeploy skill | avimak | Open (Feb 2026) | Deploy full-stack web apps directly from Claude. Updated May 4 — still active. |

**Momentum pattern:** Three of six high-potential items are Windows/skill-creator infrastructure fixes, not new Skills. The community is currently more focused on repairing the tooling pipeline than adding novel capabilities.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is fixing the skill-creator tooling pipeline** — specifically the 0% recall bug in `run_eval.py` (PRs #1298, #1323, #1099, #1050; Issues #556, #1169, #1061) and Windows cross-platform compatibility (#538, #1099, #1050, Issue #1061) — indicating that until the evaluation loop reliably measures skill trigger rates, the entire community skill creation workflow is operating on noise rather than signal.

---

# Claude Code Community Digest — 2026-06-28

---

## Today's Highlights

The community continues to focus on **Opus 4.7 thinking summary rendering** — three high-engagement issues (#49322, #49268, #49902) remain open with no fix in sight, and a new variant (#59844) now documents the same bug in non-interactive surfaces. **Cowork on ARM64 Windows** (#39636) is still a blocker for Snapdragon X users. Two new feature requests propose agent-invokable compaction and a Claude self-learning signal, signaling growing interest in autonomous agent refinement.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues (10 Noteworthy)

- **[#49322 – Opus 4.7 thinking summaries not rendered in VS Code extension](https://github.com/anthropics/claude-code/issues/49322)**  
  *47 comments, 41 👍* — Original bug: VS Code extension fails to render Opus 4.7 thinking summaries. Reopened multiple times; root cause appears to be the harness not setting `display: "summarized"`. This is the most active bug impacting daily workflows.

- **[#49268 – Thinking summaries missing on Opus 4.7 — harness doesn't set display: "summarized"](https://github.com/anthropics/claude-code/issues/49268)**  
  *46 comments, 75 👍* — Deep technical analysis by the community pinpoints the issue to the API default change for `display` on Opus 4.7. Highest 👍 count among open bugs; developers are waiting for a configuration passthrough.

- **[#39636 – Cowork VM guest kernel never boots on Snapdragon X Plus (ARM64)](https://github.com/anthropics/claude-code/issues/39636)**  
  *32 comments, 9 👍* — A long-running platform blocker for Windows ARM users. Cowork fails to boot consistently, triggering connection timeouts. No resolution in over three months.

- **[#49902 – Duplicate: Opus 4.7 thinking summaries not rendered (VSCode extension 2.1.112)](https://github.com/anthropics/claude-code/issues/49902)**  
  *14 comments, 41 👍* — Confirms the same bug persists on the latest marketplace version and on Linux (WSL2). Demonstrates broad cross-platform impact.

- **[#59844 – `showThinkingSummaries: true` silently no-ops on Opus 4.7 in non-interactive surfaces](https://github.com/anthropics/claude-code/issues/59844)**  
  *10 comments, 6 👍* — Expands the thinking summaries bug to CLI `--print` and SDK use. Community notes a one-line fix exists but hasn't been shipped.

- **[#70622 – Add option to disable clickable Yes/No prompts in terminal](https://github.com/anthropics/claude-code/issues/70622)**  
  *8 comments, 24 👍* — Users report accidental permission approvals/cancellations due to the new clickable prompt UI. Strong demand for a configuration toggle.

- **[#57102 – Stale .git/index.lock left behind in worktrees during normal CLI operation (macOS)](https://github.com/anthropics/claude-code/issues/57102)**  
  *5 comments, 0 👍* — Reproducible bug causing git lock file pollution in worktrees. Low engagement but potentially disruptive for projects with many worktrees.

- **[#65114 – Cowork: give users a manual /compact (user-initiated compaction)](https://github.com/anthropics/claude-code/issues/65114)**  
  *5 comments, 1 👍* — Request for a manual compaction command in Cowork. Auto-compact timing is unpredictable; users want control.

- **[#57230 – VSCode Extension: Add native system/toast notifications when Claude needs attention](https://github.com/anthropics/claude-code/issues/57230)**  
  *4 comments, 14 👍* — Current visual indicators (tab dot, status bar) are insufficient. Users want OS-level notifications for permission prompts and completion.

- **[#69950 – Safety classifier outage blocks ALL Bash/tool calls](https://github.com/anthropics/claude-code/issues/69950)**  
  *2 comments, 0 👍* — Even with low engagement, this is a critical incident: auto-approval mode completely blocked due to classifier unavailability for Opus 4.8. Points to resilience gaps in the safety pipeline.

---

## Key PR Progress

Only two PRs were updated in the last 24 hours:

- **[#71798 – "." (closed)](https://github.com/anthropics/claude-code/pull/71798)** — Likely an accidental or test PR; no meaningful changes.

- **[#68787 – fix(scripts): add error message to edit-issue-labels.sh when called with no label arguments](https://github.com/anthropics/claude-code/pull/68787)** — An open PR improving script robustness. Previously the script exited silently with code 1 when no labels were provided, making CI debugging harder. This PR adds a clear stderr message.

No major feature or bug-fix PRs are in progress this week.

---

## Feature Request Trends

- **Cowork autonomy & notifications** — Several requests target better Cowork user control: manual compaction (#65114), the ability for the agent to invoke compaction itself (#71803), and actionable push notifications for permission prompts (#62458). Users want to stay away from the keyboard without losing workflow.

- **Unified notification system** — Both the CLI/TUI (#67220 for Windows) and VS Code extension (#57230, #65241) lack native OS notifications. The theme crosses all platforms and surfaces.

- **Agent self-feedback & memory** — New idea from (#71937): Claude currently only learns from explicit user corrections. Proposals ask for implicit signal detection (e.g., response resumption rate, user edits) to auto-update memory.

- **Configurability of UI elements** — Beyond clickable prompts (#70622), users want the ability to customize keybindings (#62623) and notification channels.

- **Multi-surface parity** — Issue #71941 highlights frustration with inconsistent feature sets across Claude Code, Cowork, and claude.ai and calls for a clearer roadmap.

---

## Developer Pain Points

- **Opus 4.7 thinking summaries still broken** — Three separate duplicates and a fourth expanded variant show no fix shipped. Community members have identified the root cause and even proposed one-line fixes, but the issue has lingered for over two months. Frustration is high.

- **Cowork platform gaps** — ARM64 Windows (#39636) has been blocked since March. Cowork Dispatch pairing issues (#67303) also persist. These affect early adopters on Microsoft’s new hardware.

- **Safety pipeline brittleness** — The classifier outage (#69950) disabled all tool calls for an extended period. No fallback mechanism exists, leaving users completely blocked.

- **MCP server instruction handling** — Instructions can be missing entirely (#23808, closed) or truncated (#43474). Environment variable `CLAUDE_PROJECT_DIR` is absent on Windows (#71924). These inconsistencies break third-party MCP server interoperability.

- **Git integration regressions** — Stale `.git/index.lock` files in worktrees (#57102) and potential other lock issues are a reliability concern for teams using git worktrees.

- **Windows-specific regressions** — SSL certificate handling broke after 2.1.190 (#71663). Model ID generation for Bedrock produces invalid identifiers (#68005). Windows users continue to face second-class support.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-28

## Today’s Highlights
Three alpha releases (`rust-v0.143.0-alpha.27` through `.29`) rolled out without public changelogs, while the community continues to react to a sharp **10–20× rate-limit cost increase** that has drained Plus accounts in 2–3 prompts. A massive stack of MCP OAuth serialization PRs (10+) landed for review, hinting at a coordinated effort to fix token refresh races and credential persistence. The long-running SQLite log‑amplification bug (#28224) was closed after three merged PRs, though a new report (#30405) suggests the fix is incomplete on Windows.

## Releases
- **rust-v0.143.0-alpha.29** – latest alpha; no feature details.
- **rust-v0.143.0-alpha.28** – intermediary alpha.
- **rust-v0.143.0-alpha.27** – released earlier in the day.

*No changelog or summary was provided for any of the three.*

## Hot Issues (10 selected)
1. **#28879 – Rate-limit cost per token jumped ~10–20x**  
   *(334 👍, 186 comments)* – The most urgent open bug. Plus users report their 5‑hour budget consumed in 2–3 prompts. Session logs show `limit‑% consumed per token` spiked ~June 16. No official response yet.  
   [openai/codex#28879](https://github.com/openai/codex/issues/28879)

2. **#11023 – Codex desktop app for Linux**  
   *(650 👍, 130 comments)* – The highest‑voted open feature. Users cite poor macOS power consumption as a reason for needing Linux support.  
   [openai/codex#11023](https://github.com/openai/codex/issues/11023)

3. **#28224 – SQLite feedback logs write ~640 TB/year**  
   *(400 👍, 93 comments)* – **Closed** after three PRs (#29432, #29457, #294??) reduced log volume by ~85%. Community members noted the fix helped but did not eliminate the problem (see #29532, #30405).  
   [openai/codex#28224](https://github.com/openai/codex/issues/28224)

4. **#2847 – Way to exclude sensitive files**  
   *(414 👍, 79 comments)* – Request for a `.codexignore`/`.aiignore` mechanism at repo and global levels, e.g., to prevent `node_modules` or secrets from being sent to the model.  
   [openai/codex#2847](https://github.com/openai/codex/issues/2847)

5. **#30224 – “This model is not supported” when using Responses-Lite**  
   *(18 👍, 52 comments)* – GPT‑5.5 fails with `X-OpenAI-Internal-Codex-Responses-Lite` on the desktop app; GPT‑5.4 works. Affects Plus/Pro users on Win11.  
   [openai/codex#30224](https://github.com/openai/codex/issues/30224)

6. **#29955 – Quota drained instantly: 100 credits gone after 1 message**  
   *(7 👍, 29 comments)* – Another rate‑limit anomaly. Pro*5 user lost entire 5‑hour limit after one prompt. Likely related to #28879.  
   [openai/codex#29955](https://github.com/openai/codex/issues/29955)

7. **#29532 – macOS SQLite TRACE churn persists after v0.142.0**  
   *(7 👍, 22 comments)* – The partial fix from #29432 helped, but `logs_2.sqlite` still grows rapidly on macOS. Community suspects the WAL mode is not adequately throttled.  
   [openai/codex#29532](https://github.com/openai/codex/issues/29532)

8. **#25744 – macOS accumulates Computer Use / MCP zombie processes**  
   *(3 👍, 8 comments)* – Long‑running sessions leak child processes, causing HID lag and WindowServer stalls. Reproducible with Computer Use enabled.  
   [openai/codex#25744](https://github.com/openai/codex/issues/25744)

9. **#24259 – Windows sandbox intermittently fails with `spawn setup refresh` on ARM64**  
   *(12 👍, 13 comments)* – `codex doctor` passes, but sandbox creation fails. Affects Windows 11 ARM64.  
   [openai/codex#24259](https://github.com/openai/codex/issues/24259)

10. **#26984 – MCP stdio servers leak pipe fds + orphan children → EMFILE**  
    *(1 👍, 7 comments)* – Cumulative file‑descriptor exhaustion after long‑running sessions using MCP stdio servers.  
    [openai/codex#26984](https://github.com/openai/codex/issues/26984)

## Key PR Progress (10 selected)
1. **#30395 – Show usage‑limit reset expiry details**  
   Fetches reset‑credit expiry dates from the backend concurrently, so clients can display when banked resets expire.  
   [openai/codex#30395](https://github.com/openai/codex/pull/30395)

2. **#30334 – Telemetry: log structured tool and inference timing events**  
   Adds dispatch/queue/handler latency breakdowns to JSON logs for operational diagnostics.  
   [openai/codex#30334](https://github.com/openai/codex/pull/30334)

3. **#30269 – Disable Nagle on Rendezvous WebSockets**  
   Reduces latency for exec‑server WebSocket messages by disabling Nagle’s algorithm unconditionally.  
   [openai/codex#30269](https://github.com/openai/codex/pull/30269)

4. **#30294 – Route MCP OAuth recovery through Codex** (stacked)  
   First PR in a 6‑PR stack to serialize shared OAuth stores, login/logout, refresh transactions, and route recovery through Codex’s own auth flow.  
   [openai/codex#30294](https://github.com/openai/codex/pull/30294)

5. **#30292 – Serialize shared MCP OAuth credential stores**  
   Core serialization layer to prevent race conditions when multiple MCP clients read/write the same credential file.  
   [openai/codex#30292](https://github.com/openai/codex/pull/30292)

6. **#30295 – Serialize MCP OAuth login and logout**  
   Ensures atomic transitions between authentication states.  
   [openai/codex#30295](https://github.com/openai/codex/pull/30295)

7. **#30293 – Serialize MCP OAuth refresh transactions**  
   Avoids concurrent token refreshes that could produce stale or conflicting credentials.  
   [openai/codex#30293](https://github.com/openai/codex/pull/30293)

8. **#30296 – Report MCP OAuth auto‑store drift**  
   Logs when persisted credentials differ from in‑memory state, aiding debugging of credential corruption.  
   [openai/codex#30296](https://github.com/openai/codex/pull/30296)

9. **#30327 – Stabilize synthesized call output IDs**  
   Assigns stable IDs to “aborted” synthetic outputs so retries and prompt caching produce consistent conversation history.  
   [openai/codex#30327](https://github.com/openai/codex/pull/30327)

10. **#29691 – Enforce marketplace source policy at runtime**  
    Blocks installed plugins that violate enterprise source policies; filters discovery and snapshot reports accordingly.  
    [openai/codex#29691](https://github.com/openai/codex/pull/29691)

## Feature Request Trends
- **File exclusion (.codexignore)**: Multiple issues (#2847, #24993) request a way to prevent Codex from reading sensitive or irrelevant paths (e.g., `node_modules`, `.env`). The community wants both repo‑local and global ignore files.
- **Linux desktop app**: #11023 remains the most‑voted feature (650 👍). Users cite macOS power drain and performance issues as primary motivators.
- **Per‑edit confirmation**: #24325 requests an opt‑in mode where Codex asks before making each edit, reverting to the earlier interactive behavior.
- **Rate‑limit transparency**: #29618 asks for detailed reset‑credit expiry dates (now addressed by PR #30395).
- **Non‑blocking MCP/subagent orchestration**: #30399 envisions observable, parallel startup for multi‑machine workflows.
- **Thread‐management tools**: #30233 notes that `create_thread` and `fork_thread` are not exposed in the app despite being available server‑side.

## Developer Pain Points
- **Rate‑limit cost spikes** – The #1 pain point. Users on Plus and Pro plans report budget depletion after 1–3 prompts, with no official explanation or rollback. Several duplicate reports (#28879, #29955, #30390).
- **Excessive SQLite log churn** – Even after the #28224 fix, macOS (#29532) and Windows (#30405) users still see high‑frequency TRACE logging. SSD endurance remains a concern.
- **MCP OAuth fragility** – Multiple issues (#27165, #26984, #25744) describe token refresh failures, credential drift, and file‑descriptor leaks. The massive OAuth serialization PR stack suggests the team is aware and acting.
- **Windows sandbox instability** – ARM64 users face `spawn setup refresh` failures (#24259) and `CreateProcessAsUserW` errors (#20570). Blank editor panels on Windows (#21863) also persist.
- **macOS resource leaks** – Computer Use sessions accumulate zombie child processes (#25744), leading to HID lag and potential system‑wide stalls.
- **Auth token invalidation** – Business Plan users (#28672) experience repeated 401 errors and forced phone verification, especially when using dev containers.
- **GPT‑5.5 vs. Responses‑Lite incompatibility** – Users of the desktop app (#30224, #30406) cannot use GPT‑5.5 when the internal lite endpoint is active, forcing a downgrade to GPT‑5.4.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*