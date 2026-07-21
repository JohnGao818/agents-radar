# AI CLI Tools Community Digest 2026-07-21

> Generated: 2026-07-21 02:14 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: Claude Code vs OpenAI Codex (2026-07-21)

## Ecosystem Overview

The AI CLI tools ecosystem is maturing rapidly, with both Claude Code and OpenAI Codex addressing performance, security, and user experience under growing workloads. Claude Code’s latest release (v2.1.216) fixes a quadratic slowdown in long sessions, while the community rallies around multi-account switching and data-retention reliability. OpenAI Codex is investing heavily in infrastructure—per-environment permission profiles, Windows sandboxing, and optimized polling—against a backdrop of urgent rate-limit transparency concerns. Both tools face similar pain points around cost transparency, platform coverage, and session persistence, but their engineering emphases diverge: Claude Code prioritizes interactive feature depth, Codex focuses on secure, scalable backend mechanics.

## Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Hot issues tracked** | 10 (top: 668 👍) | 10 (top: 802 👍) |
| **PRs updated (24h)** | 7 | 10 |
| **Latest release** | v2.1.216 (notable fix: quadratic slowdown) | `rust-v0.145.0-alpha.25/27` (no detailed changelog) |
| **Community engagement signal** | 668 👍 on multi‑account switching | 802 👍 on Linux desktop app |
| **Data‑loss / regression bugs** | Chat JSONL deletion (#62272) | Rate‑limit cost spike (#28879, 358 👍) |
| **Release cadence** | Stable release today | Two alpha bumps, no stable release |

## Shared Feature Directions

| Requirement | Appears in Claude Code | Appears in OpenAI Codex | Common Motivation |
|---|---|---|---|
| **Session persistence / background execution** | SSH session survival after client disconnect (#49790, 29 👍) | Headless remote Linux hosts for mobile (#23200, 42 👍) | Long‑running workflows over unreliable connections |
| **Permission & sandbox granularity** | `sandbox.filesystem.disabled` setting; folder trust issues (#69066) | Per‑environment permission profiles (#34398); Windows sandboxing (#34423) | Enterprise security, multi‑user environments |
| **Cost / rate‑limit transparency** | Fable 5 incorrect plan usage (#79341) | Rate‑limit cost spike on gpt‑5.5 (#28879, 358 👍) | Surprise billing, budget management |
| **Cross‑platform desktop & terminal UX** | Text selection broken in VSCode (#61021) | Windows 11 freezes (#20214); Ctrl‑B sidebar conflict (#10749) | Core editing workflows hindered by UI regressions |
| **Skill composability / agent orchestration** | Agent unable to invoke `/code-review` from custom skills (#79023) | MultiAgentV2 audit trail broken (#28058) | Advanced automation, debugging compound workflows |
| **Accessibility / hands‑free** | TTS read‑aloud PR (#79620) | Not explicitly surfaced | Inclusivity, multitasking use cases |

## Differentiation Analysis

Claude Code emphasizes **user‑facing feature requests**—multi‑account switching, branch‑aware diff, text‑to‑speech, and skill composition. Its community shows strong interest in personal productivity enhancements and session management (SSH persistence). The tool’s pain points cluster around data integrity (chat JSONL deletion) and agent harness bugs (random text insertion under high concurrency).

OpenAI Codex, by contrast, is doubling down on **infrastructure hardening**—per‑environment permission profiles, explicit proxy resolution, buffered exec yields, and Windows sandboxing. Its community’s top demand (Linux desktop app) signals a gap in platform coverage that Claude Code may already fill (no equivalent demand observed). Codex users are more vocal about rate‑limit cost spikes, background polling waste, and platform stability on Windows—issues that affect **deploy‑scale usage** and budget predictability.

Target user divergence: Claude Code’s “Cowork VM” and skill composition point toward pair‑programming and team coding workflows. Codex’s managed‑network profiles and multi‑agent encryption suggest an enterprise/security‑focused audience needing audit trails and compliance.

## Community Momentum & Maturity

- **Claude Code** demonstrates higher release momentum with a stable, well‑documented fix today. Its community is self‑organizing (recovery scripts for data loss, prototype TTS hooks). The top feature request (multi‑account, 668 👍) is well‑defined but lacks official response—a sign of pending prioritization.
- **OpenAI Codex** shows rapid PR throughput (10 merged in 24h) but weak release communication (alpha versions without changelogs). The 802‑thumbs‑up Linux desktop issue remains unaddressed for a long time, indicating a strategic choice to postpone platform expansion. The #28879 rate‑limit regression (358 👍) is the most urgent unresolved community pain.
- **Maturity signals**: Codex’s permission profile system and sandboxing are more advanced; Claude Code’s data‑loss bug and agent concurrency issues suggest younger infrastructure. Both communities are highly active and technically sophisticated.

## Trend Signals

1. **Cost governance is the new bottleneck.** As models scale, users demand real‑time rate‑limit visibility and predictable billing—Claude Code’s plan‑usage confusion and Codex’s 10–20× cost spike are top pain points.
2. **Platform parity remains unfinished business.** The Linux desktop request is the #1 Codex feature (802 👍) with no resolution; Windows stability is a recurring theme in both tools.
3. **Session persistence becomes table‑stakes.** Developers expect CLI assistants to survive network drops and support mobile/remote controls—both tools’ communities are asking for `tmux`‑like reliability.
4. **Security granularity moves into the mainstream.** Per‑environment permission profiles, sandboxed execution, and proxy isolation are no longer enterprise‑only—they’re becoming core CLI features.
5. **Composable agents face interoperability hurdles.** Both tools report bugs where skills cannot invoke other skills or where audit trails break in multi‑agent setups—signs that orchestration layers are still immature.
6. **Accessibility is emerging as a community‑driven feature.** Claude Code’s TTS hook was built by the community and gained enough traction for a PR; expect similar demands across tools as usage diversifies.

| Trend | Claude Code Signal | OpenAI Codex Signal |
|---|---|---|
| Cost transparency | Plan‑vs‑usage confusion (#79341) | Rate‑limit cost spike (#28879) |
| Platform parity | Text selection broken (VSCode) | Linux app #1, Windows freezes |
| Session persistence | SSH resume (#49790) | Headless host control (#23200) |
| Security granularity | sandbox.filesystem.disabled (#69066) | Per‑environment profiles (#34398) |
| Agent composability | Skill invocation regression (#79023) | MultiAgent audit trail broken (#28058) |
| Accessibility | TTS PR (#79620) | Not yet surfaced |

*Reference value for developers*: Both tools are converging on infrastructure needs (security, cost transparency, session resilience) but differ in domain emphasis—Claude Code for interactive pair programming, Codex for orchestrated enterprise deployments. Monitoring their respective community traction (especially #28879 and #11023) will indicate where the next major platform investments will land.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data from github.com/anthropics/skills | Snapshot: 2026-07-21*

---

## 1. Top Skills Ranking

The most-discussed Pull Requests reveal intense community focus on **tooling reliability** and **skill quality**, alongside novel domain-specific skills. All remain open.

**1. Skill Creator Fixes (#1298) — MartinCajiao**
- **Functionality:** Fixes `run_eval.py` to report accurate recall (was stuck at 0% on all queries). Addresses Windows stream reading, trigger detection flakiness, and parallel worker bugs. Directly enables the description-optimization loop to function.
- **Discussion:** References #556 (12 comments) and 10+ independent reproductions of the recall=0% bug. The criticality has made this the most-watched PR — without it, no skill description can be empirically improved.
- **Status:** Open | [PR #1298](https://github.com/anthropics/skills/pull/1298)

**2. Document Typography (#514) — PGTBoos**
- **Functionality:** Prevents orphan words, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses typographic issues that users rarely report but affect every document Claude produces.
- **Discussion:** Broad community appeal — typographic quality is a universal pain point. No major controversy, but strong implicit demand evident from sustained comment activity.
- **Status:** Open | [PR #514](https://github.com/anthropics/skills/pull/514)

**3. Self-Audit (v1.3.0) (#1367) — YuhaoLin2005**
- **Functionality:** Two-phase output audit: mechanical file verification (do all claimed files exist?) followed by four-dimension reasoning quality gate in damage-priority order. Universal across projects and models.
- **Discussion:** Recent (late June) but highly active. Represents a new category — skills that audit other skills' outputs. The "reasoning quality gate" concept has sparked further proposals (#1385).
- **Status:** Open | [PR #1367](https://github.com/anthropics/skills/pull/1367)

**4. Testing Patterns (#723) — 4444J99**
- **Functionality:** Comprehensive testing skill covering Testing Trophy philosophy, AAA pattern, React Testing Library, mocking, and E2E with Playwright. Designed to make Claude a capable testing partner across the full stack.
- **Discussion:** Community interest reflects the perennial difficulty of getting LLMs to write good tests. The skill's structured coverage of "what to test vs. what NOT to test" has been well-received.
- **Status:** Open | [PR #723](https://github.com/anthropics/skills/pull/723)

**5. Frontend-Design Clarity (#210) — justinwetch**
- **Functionality:** Revises the existing frontend-design skill for clarity and actionability. Ensures every instruction is followable within one conversation and steers behavior without being overly prescriptive.
- **Discussion:** Highlights community frustration with existing skills that read like documentation rather than executable instructions. Related to #202 (skill-creator should be updated to best practice).
- **Status:** Open | [PR #210](https://github.com/anthropics/skills/pull/210)

**6. Pyxel Retro Game Development (#525) — kitao**
- **Functionality:** Skill for the Pyxel retro game engine and its MCP server. Covers write → run-and-capture → inspect → iterate workflow. Aimed at pixel-art/8-bit game creation with Python.
- **Discussion:** Creator of Pyxel (kitao) submitted the PR, lending authority. Longest-running open PR with sustained updates through July 2026. A niche but passionate use case.
- **Status:** Open | [PR #525](https://github.com/anthropics/skills/pull/525)

**7. Quality & Security Analyzers (#83) — eovidiu**
- **Functionality:** Two meta-skills: `skill-quality-analyzer` (structure, documentation, examples, testability — 5 dimensions) and `skill-security-analyzer` (expression injection, path traversal, tool abuse, privilege escalation). The first systematic approach to skill quality assurance.
- **Discussion:** Early submission (Nov 2025) but still open. Demonstrates demand for meta-skills that evaluate other skills — a sign of ecosystem maturation.
- **Status:** Open | [PR #83](https://github.com/anthropics/skills/pull/83)

**8. SAP-RPT-1-OSS Predictor (#181) — amitlals**
- **Functionality:** Skill for SAP's open-source tabular foundation model. Enables predictive analytics on SAP business data directly via Claude.
- **Discussion:** Enterprise-focused. Unusual in that it wraps an external ML model rather than guiding Claude's behavior. Represents the "skill as model adapter" pattern.
- **Status:** Open | [PR #181](https://github.com/anthropics/skills/pull/181)

---

## 2. Community Demand Trends

The Issues tab reveals five clear demand clusters:

| Demand Cluster | Key Issues | Sentiment |
|---|---|---|
| **Trust & Security Boundaries** | #492 (43 comments) — Community skills under `anthropic/` namespace impersonate official skills. Users risk granting elevated permissions unintentionally. | Urgent concern |
| **Organizational Skill Sharing** | #228 (14 comments) — No built-in way to share skills within an org. Current workflow: download .skill → send via Slack → manual upload. | High demand |
| **Tooling Reliability (skill-creator)** | #556 (12), #1169 (3), #1061 (3), #62 (10) — 0% recall bug, Windows incompatibility, encoding crashes. The skill-creation pipeline is fragile. | Critical blocker |
| **New Skill Domains** | #1329 (9) — compact-memory (symbolic notation for agent state); #412 (6) — agent-governance (safety patterns for AI agents); #1385 (3) — reasoning quality gate pipeline | Emerging interest |
| **Duplicate/Clutter in Plugin Distribution** | #189 (6) — `document-skills` and `example-skills` install identical content, causing duplicates in context window. | Quality-of-life friction |

**Notable:** The tooling reliability cluster (#556, #1061, #1169) is the most painful — it blocks *everyone* from improving skill descriptions. The security concern (#492) has the most comments and is still open, suggesting unresolved architectural questions about namespace governance.

---

## 3. High-Potential Pending Skills

These active PRs have strong community engagement and address clear pain points — likely to merge soon:

- **Fix: run_eval.py on Windows (#1099) — joshuawowk**  
  Directly unblocks Windows users of skill-creator. Fixes subprocess pipe reading and encoding. Complements #1050 (gstreet-ops) which addresses the PATHEXT issue.  
  [PR #1099](https://github.com/anthropics/skills/pull/1099)

- **Fix: YAML unquoted characters (#539, #361) — Lubrsy706, Mr-Neutr0n**  
  Two independent PRs solving the same problem: silent YAML parsing failures when `description` contains `:`. #539 adds pre-parse validation; #361 adds UTF-8 byte-length checks. Convergence suggests a merge-ready fix pattern.  
  [PR #539](https://github.com/anthropics/skills/pull/539) | [PR #361](https://github.com/anthropics/skills/pull/361)

- **Fix: DOCX w:id collision (#541) — Lubrsy706**  
  Fixes document corruption when tracked changes collide with existing bookmarks in OOXML. A targeted, correct fix for a reportable bug.  
  [PR #541](https://github.com/anthropics/skills/pull/541)

- **Color Expert (#1302) — meodai**  
  Self-contained color expertise covering naming systems (ISCC-NBS, Munsell, XKCD, RAL, etc.) and color space selection (OKLCH for scales, OKLAB for gradients, CAM16 for appearance). Author is a well-known color systems expert (meodai/color-names).  
  [PR #1302](https://github.com/anthropics/skills/pull/1302)

- **ODT Support (#486) — GitHubNewbie0**  
  Adds OpenDocument format creation, template filling, and ODT→HTML conversion. Addresses LibreOffice/ISO standard document workflows.  
  [PR #486](https://github.com/anthropics/skills/pull/486)

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is *not* for novel skill domains — it is for a reliable, cross-platform skill-development toolchain** (skill-creator fixes dominate 4 of the top 10 PRs and 3 of the most active issues), followed by trust-layer infrastructure (namespace security, org-wide sharing), indicating the ecosystem is past the "invention" phase and entering an "industrialization" phase where tooling reliability and governance determine adoption velocity.

---

# Claude Code Community Digest — 2026-07-21

## Today's Highlights

A performance‑critical fix lands in v2.1.216, eliminating a quadratic slowdown that affected long sessions with multi‑second stalls and slow resumes. The community’s top‑voted feature request (668 👍) for multi‑account profile switching in Claude Desktop remains the most active discussion, while a data‑loss bug where chat JSONLs are silently deleted despite high `cleanupPeriodDays` continues to draw attention with a recovery script now available for macOS Time Machine users.

## Releases

**v2.1.216** — [Release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.216)

- **`sandbox.filesystem.disabled` setting** — lets you skip filesystem isolation while retaining network egress control.
- **Fix: quadratic message normalization slowdown** — corrected an O(n²) cost that caused multi‑second stalls and slow session resumes in long conversations.
- **Fix: [truncated – likely authentication]** — the changelog entry reads “Fixed au” in the provided data; details may appear in the full release notes.

## Hot Issues

1. **[#18435 – Multi‑account profile switching in Claude Desktop](https://github.com/anthropics/claude-code/issues/18435)** — 148 comments, 668 👍. The most‑requested feature: easy switching between multiple Claude accounts. No official response yet.

2. **[#23626 – Diff comparison against branches other than main](https://github.com/anthropics/claude-code/issues/23626)** — 33 comments, 95 👍. Users want `/diff` to work with any branch, not only the default.

3. **[#62272 – Chat JSONLs deleted despite high `cleanupPeriodDays`](https://github.com/anthropics/claude-code/issues/62272)** — 18 comments. Data‑loss bug triggered on updates/restarts. A community recovery script for macOS Time Machine is available.

4. **[#61021 – Text selection broken in VSCode terminal](https://github.com/anthropics/claude-code/issues/61021)** — 12 comments. Recent changes made selecting and copying text difficult; affects productivity.

5. **[#64592 – Cowork VM service not running on Windows 11](https://github.com/anthropics/claude-code/issues/64592)** — 12 comments. Workaround: manually enable Virtual Machine Platform. Extends closed cluster of related reports.

6. **[#69829 – Random “hello” text insertion under high concurrent agent load](https://github.com/anthropics/claude-code/issues/69829)** — 11 comments. Reproducible with 20+ agents on macOS; below 20 agents works fine.

7. **[#49790 – SSH remote session should survive client disconnect](https://github.com/anthropics/claude-code/issues/49790)** — 10 comments, 29 👍. Users want persistent remote sessions that can be reconnected after network drops.

8. **[#60848 – Ambiguous “Don’t ask me again” in session resume prompt](https://github.com/anthropics/claude-code/issues/60848)** — 8 comments, 13 👍. The option is unclear whether it silences the resume prompt permanently or just for the current session.

9. **[#79341 – Fable 5 incorrectly requires usage credits on Max 20x plan](https://github.com/anthropics/claude-code/issues/79341)** — 5 comments, 8 👍. Mid‑session auto‑switch to Opus 4.8 despite unused Fable weekly allowance.

10. **[#79023 – Agent unable to invoke `/code-review` skill from custom skills](https://github.com/anthropics/claude-code/issues/79023)** — 4 comments, 10 👍. Regression in v2.1.215 breaks programmatic skill composition.

## Key PR Progress

1. **[#79620 – Text‑to‑speech read‑aloud hook for accessibility](https://github.com/anthropics/claude-code/pull/79620)** — Implements a multi‑platform TTS hook (Piper, `say`, PowerShell) that reads responses aloud. Addresses the feature request in #79542.

2. **[#79387 – Error message when `edit-issue-labels.sh` called without label args](https://github.com/anthropics/claude-code/pull/79387)** — Makes silent exit code 1 visible with a stderr message. Fixes #69913.

3. **[#66650 – Use full author name in `pr-review-toolkit` plugin manifest](https://github.com/anthropics/claude-code/pull/66650) — CLOSED** — Corrects author name to “Daisy Hollman” for consistency across bundled plugins.

4. **[#1 – Create SECURITY.md](https://github.com/anthropics/claude-code/pull/1) — CLOSED** — Long‑standing security policy document; closed now (likely superseded).

5. **[#74722 – Conventional Branch naming in `/commit-push-pr`](https://github.com/anthropics/claude-code/pull/74722)** — Adds an optional `conventional` argument to create branches per the Conventional Branch 1.0.0 spec.

6. **[#79385 – Honor any user’s thumbs‑down, not just the issue author’s](https://github.com/anthropics/claude-code/pull/79385)** — Fixes the auto‑close‑duplicates bot to respect all thumbs‑down reactions, matching its own documentation.

7. **[#78532 – GCP gateway: optional internal ALB + PG16 Cloud SQL fix](https://github.com/anthropics/claude-code/pull/78532)** — Fixes Terraform example failures when deploying PG16+ (defaults to ENTERPRISE_PLUS) and adds internal ALB support.

*Note: Only 7 PRs were updated in the last 24 hours; all are listed above.*

## Feature Request Trends

- **Multi‑account management** (#18435, 668 👍) — Users want to switch between multiple Anthropic accounts within Claude Desktop, likely for work/personal separation or team workflows.
- **Session persistence over SSH** (#49790, 29 👍) — Demand for remote sessions that survive client disconnection and allow reconnection (like `tmux`).
- **Branch‑aware diff** (#23626, 95 👍) — The ability to compare changes against any git branch, not just `main`.
- **Accessibility / hands‑free** (#79542, #79620) — Text‑to‑speech output for reading responses aloud, driven by community prototypes.
- **Localhost proxy exception** (#76653, 9 👍) — Allow `ANTHROPIC_BASE_URL` pointing to loopback proxies while keeping Remote Control enabled.
- **Skill composability** (#79023, #79560) — Users want built‑in skills (especially `/code-review`) to be invocable from other skills, which is currently blocked by `disable-model-invocation`.

## Developer Pain Points

1. **Data loss from chat deletion** (#62272) — Despite user‑configured retention settings, chat JSONLs are deleted on updates/restarts, forcing reliance on Time Machine recovery.

2. **Text selection in VSCode terminal** (#61021) — A recent change broke copy‑paste, a core editing workflow.

3. **Cowork VM service failures on Windows** (#64592, #62116) — Fresh installations and Home editions lack fallback paths; manual enabling of VMP is required.

4. **Agent harness bugs** (#69829, #78782) — Random text insertion under high concurrency and background tasks never resuming subagents.

5. **Crediting and model switching confusion** (#79341, #75055) — Fable 5 incorrectly charging usage credits on Max plans, and workflow agents inheriting expensive models without override.

6. **Permission and trust inconsistencies** (#69066, #79612, #78273) — Un‑canonicalized paths on Windows create duplicate entries that reset folder trust; parent‑dir trust skips the dialog but still requires MCP approval; file overwrite without confirmation causes irreversible data loss.

7. **Hook and MCP tool resolution** (#79616, #79621) — `PostToolUse` hooks not reaching Claude in VSCode, and background subagents unable to find MCP tools even with exact names.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-21

## Today's Highlights
The community is rallying around two major pain points: a suspected **cost-spike regression** in `gpt-5.5` rate limits (Issue #28879, 358 👍) that has users burning 5-hour budgets in 2-3 prompts, and the enduring demand for a **native Linux desktop app** (Issue #11023, 802 👍). Meanwhile, the engineering team landed a dense batch of infrastructure PRs today—**per-environment permission profiles**, **Windows sandboxing in the exec server**, and **buffered code-mode exec**—all aimed at tightening security, proxy handling, and developer experience.

## Releases
- **[`rust-v0.145.0-alpha.27`](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.27)**: Alpha release with no detailed changelog.
- **[`rust-v0.145.0-alpha.25`](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.25)**: Alpha release with no detailed changelog.

*Note: Both releases lack descriptive notes; likely minor version bumps on the way to a stable `0.145.0`.*

## Hot Issues
*10 noteworthy issues form the core of today's community discussion:*

1. **[#28879 – Rate-limit cost per token jumped ~10-20x](https://github.com/openai/codex/issues/28879)** (208 comments, 358 👍)  
   *Critical.* Users report `gpt-5.5` on the Plus plan draining the 5-hour budget in 2-3 prompts. Session logs show `limit-% consumed per token` spiking 10-20× since June 16. No official response yet—this is the top community concern today.

2. **[#11023 – Linux desktop app](https://github.com/openai/codex/issues/11023)** (181 comments, 802 👍)  
   *Highest-voted feature request overall.* Linux users cite macOS power-consumption issues and need a native app for workstations. The sheer vote count signals a persistent gap in platform coverage.

3. **[#20214 – Windows 11 freezes/stutters](https://github.com/openai/codex/issues/20214)** (60 comments, 68 👍)  
   Frequent UI freezes on Windows 11 Pro despite ample RAM (32 GB) and CPU (Ryzen 5 5600). Multiple duplicates exist—this is a recurring platform stability complaint.

4. **[#13733 – Background process polling wastes tokens](https://github.com/openai/codex/issues/13733)** (31 comments, 29 👍)  
   Each `write_stdin` poll triggers a full API round-trip with complete conversation history. Burns tokens proportional to history size × poll count, especially painful during long builds.

5. **[#28058 – Encrypted messages break task audit trail](https://github.com/openai/codex/issues/28058)** (24 comments, 99 👍)  
   Regression after #26210: encrypted MultiAgentV2 messages remove readable task audit trails. Concerns about debugging multi-agent workflows and transparency.

6. **[#31836 – Projects Sort By broken](https://github.com/openai/codex/issues/31836)** (23 comments, 26 👍)  
   `Sort By Last updated` only sorts tasks within project groups, not the projects themselves. A UX bug that frustrates users with many projects.

7. **[#24287 – UI stuck in Thinking; Stop fails](https://github.com/openai/codex/issues/24287)** (16 comments, 5 👍)  
   Desktop app accepts prompts but hangs in "Thinking" state; Stop button doesn't work; the turn becomes invisible after restart. Pro users report this as a workflow killer.

8. **[#26633 – Automations ignore timezone for RRULE](https://github.com/openai/codex/issues/26633)** (15 comments, 3 👍)  
   Desktop automations treat `BYHOUR` as UTC even when `DTSTART;TZID=Europe/Paris` is set. Critical for users relying on Codex automations for scheduled tasks.

9. **[#31969 – Unsupported parameter 'reasoning.summary'](https://github.com/openai/codex/issues/31969)** (14 comments, 8 👍)  
   `reasoning.summary` not supported with `gpt-5.3-codex-spark` model. Suggests a model-parameter compatibility gap that breaks certain configurations.

10. **[#23200 – Headless remote Linux hosts for mobile](https://github.com/openai/codex/issues/23200)** (12 comments, 42 👍)  
    Requests that Codex mobile support always-on Linux servers without requiring the desktop app to stay online. A natural extension for SSH-based DevOps workflows.

## Key PR Progress
*10 significant pull requests merged or updated today:*

1. **[#34441 – Add buffered code-mode exec yields](https://github.com/openai/codex/pull/34441)**  
   Sets default `yield_time_ms` for code-mode `exec` to 30 seconds (up from 10). Reduces token waste from rapid polling during long-running commands.

2. **[#34438 – Increase patch approval test timeout](https://github.com/openai/codex/pull/34438)**  
   Raises wait time for patch approval events to 15 seconds. Improves test reliability for approval flows.

3. **[#34436 – Honor managed permission profiles in proxy resolution](https://github.com/openai/codex/pull/34436)**  
   Fixes a gap where `requirements.toml` permission profiles were not applied to network proxy resolution. Tightens security for managed environments.

4. **[#34435 – Resolve outbound proxy routes explicitly](https://github.com/openai/codex/pull/34435)**  
   Ensures consistent proxy behavior by resolving system proxy discovery upfront, avoiding blocking and inconsistent fallback across transports.

5. **[#34434 – Support catalog messages for non-request approval policies](https://github.com/openai/codex/pull/34434)**  
   Adds model-catalog approval message variants for `never` and `unless_trusted` policies. Improves UX for approval policy feedback.

6. **[#34398 – Support per-environment permission profiles](https://github.com/openai/codex/pull/34398)**  
   Lets each environment optionally override the thread `PermissionProfile`. Covers shell, exec, patch, filesystem, and managed-network decisions. Landmark for flexible sandboxing.

7. **[#34431 – Optimize remote compaction history handling](https://github.com/openai/codex/pull/34431)**  
   Reduces CPU/memory overhead during remote compaction by estimating token counts once and avoiding unnecessary cloning when tracing is disabled.

8. **[#34423 – Support Windows sandboxing in the exec server](https://github.com/openai/codex/pull/34423)**  
   Enables sandboxed process launch through the exec server on Windows. Adds native process launcher with PTY/pipe backends and sandbox session selection.

9. **[#34417 – Enrich app/read connector metadata](https://github.com/openai/codex/pull/34417)**  
   Adds `iconUrlDark`, `distributionChannel`, `installUrl`, and `pluginDisplayNames` to experimental `app/read` connector. Better plugin display support.

10. **[#30235 – Kill timed-out Git status process groups](https://github.com/openai/codex/pull/30235)**  
    Fixes zombie Git wrappers by running `git status --porcelain` in its own process group and killing the group on timeout. Prevents hung Git processes from blocking the worktree.

## Feature Request Trends
The community's most-requested directions are clear:

1. **Linux desktop app** — #11023 remains the undisputed #1 feature (802 👍). Users want native Linux support for power-efficient, long-running development sessions.
2. **Headless remote hosts** — #23200 (42 👍) asks for Codex mobile to control always-on Linux servers independently of the desktop app. This aligns with SSH-centric DevOps workflows.
3. **Rate limit/cost transparency** — #32726 (2 comments, 1 👍) asks for exact expiration timestamps on reset cards, but the broader sentiment from #28879 shows users want real-time rate-limit visibility and predictable cost accounting.
4. **Shared ChatGPT–Codex context** — #32519 (5 comments) proposes bidirectional task handoff between ChatGPT mobile and Codex desktop, reflecting users who ideate on mobile and execute on desktop.
5. **Timezone-aware automations** — #26633 (15 comments) shows users deeply rely on RRULE scheduling and expect proper timezone handling for global workflows.

## Developer Pain Points
Recurring frustrations cluster around these themes:

- **Rate-limit regressions** — #28879 is the most urgent: unexplained 10-20× cost-per-token spikes on `gpt-5.5` that drain daily budgets in minutes. No official acknowledgment yet.
- **Windows stability** — #20214, #33711, #33737, #34025, #34305, and #34351 all describe freeze/stutter/Disk 100% issues on Windows 10/11, often tied to Defender, sandbox scanning, or recursive FSEvents watchers.
- **Polling waste** — #13733 (background process polling) and #31401 (TUI idle after turn) point to inefficient token usage that burns credits without user benefit.
- **UI/UX regressions** — #24287 (stuck "Thinking" state), #10749/#33977 (Ctrl-B sidebar conflict on macOS), and #28055 ("Invite a Friend" misclick) show the desktop app still has rough edges in interactions.
- **Plugin/extension quirks** — #31553 (VS Code extension stopped auto-including context after update) and #21244 (history intermittently hides local chats) indicate instability in the IDE extension, particularly on Windows/remote containers.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*