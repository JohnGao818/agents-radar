# AI CLI Tools Community Digest 2026-07-03

> Generated: 2026-07-03 02:35 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools  
**Date: 2026-07-03**

---

## 1. Ecosystem Overview

The AI CLI tools market continues to mature, with Anthropic’s Claude Code and OpenAI’s Codex competing as the primary agentic coding assistants. Both tools show high community engagement around **session/usage quota management**, **Windows/corporate environment friction**, and **interactive UX reliability**—indicating that developer trust hinges on predictable resource consumption and robust local-first behavior. While Claude Code is experiencing greater heat over silent data loss and subagent orchestration bugs, Codex is undergoing a security hardening phase with a flurry of sandbox-related PRs. The pace of releases is modest on both sides, suggesting maintainers are prioritizing stability and security over new features.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Hot issues (top 10)** | 789 max comments, 467 👍 | 680 👍 (top), 139 comments |
| **PRs (last 24h)** | 4 (all open, 2 trivial docs) | 10 (mostly security/merge, some merged) |
| **Releases today** | 1 patch (v2.1.199) | 2 minor alpha (no changelogs) |
| **Bug-to-PR ratio** | Very high (many bugs, few fixes) | Moderate (active PRs address critical issues) |
| **Community response time** | No official RC on top issue (#38335) | Closed #28224 with fix; active conversation on #11023 |

**Key takeaway**: Codex shows more active engineering response (merged security PRs) while Claude Code’s community is frustrated by lack of resolution on long-standing bugs.

---

## 3. Shared Feature Directions

Several recurring requirements appear across both communities:

| Requirement | Claude Code | OpenAI Codex |
|-------------|-------------|--------------|
| **Configurable timeout for user prompts** | #73125 (65 comments, 224 👍) – auto-dismiss after 60s while typing | #28969 (74 👍) – add setting to disable 60-second auto-resolve |
| **Session/usage limit transparency** | #38335 (467 👍) – Max plan exhaustion; #21943 (40 👍) – programmatic usage data | #30918/30939 – usage limits draining 5-10x too fast |
| **Windows/corporate reliability** | #72451 – stale DNS; #73696 – PDF tool failures; #73694 – AppX locks | #20214 – freezes on Win11; #29193 – sandboxPolicy missing on Windows Desktop |
| **Silent data loss prevention** | #59248, #41458 – session transcripts deleted without warning | #28224 – SQLite logs consuming SSD endurance (fixed); #28997 – WAL file unbounded growth |
| **Subagent/orchestration correctness** | #69824, #69212 – race conditions, result misrouting | No direct equivalent, but context bug #8648 (wrong message selection) spans similar concerns |
| **Linux native app** | Not a prominent request | #11023 (680 👍) – Linux desktop app (most upvoted) |

Both communities are demanding **user control over model-initiated actions** (timeout, auto-resolve) and **better resource accounting** (quotas, cleanup, logs).

---

## 4. Differentiation Analysis

| Aspect | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Core model** | Anthropic’s Claude (Opus 4.8, Fable, etc.) | OpenAI’s GPT-5.5 (reported regression #24431) |
| **Primary use case** | Multi-turn design/approval flows, subagent orchestration | Automated code generation, Git operations, sandboxed execution |
| **Community pain points** | Session cleanup, subagent fragility, model streaming regressions (#72639) | Windows freezes, log bloat, model regression, Linux desktop absence |
| **Engineering focus** | Bugfix patches, some slash-skill enhancements | Security hardening (Git helper, sandbox, approval flow) |
| **Release cadence** | Occasional patch releases after larger gaps | Frequent alpha releases (e.g., two today), but no stable for Rust client |
| **API/CLI parity** | TUI heavy; programmatic usage data requested | Desktop app vs CLI split; MCP tool parity a recurring theme |

**Distinctive technical approaches**:  
- **Claude Code** emphasizes an **agent-as-workflow** model (subagents, CronCreate, slash skills) but suffers from orchestration fragility.  
- **Codex** invests heavily in **security boundaries** (repo-controlled Git helpers, sandbox validation, approval response hardening)—reflecting a defensive stance against supply-chain attacks.

**Target user persona**:  
- Claude Code power users are **multi-step coding workflow engineers** (design reviews, approval loops, scheduled tasks).  
- Codex heavy users are **platform engineers** needing reliable Git integration and corporate desktop support.

---

## 5. Community Momentum & Maturity

- **Claude Code**: Extremely vocal community with high engagement on a few dominant issues (#38335 alone has 789 comments). However, the low PR throughput (4 PRs, mostly trivial) and lack of official communication on top bugs signal a **maintainer bottleneck**. The community is mature enough to identify deep architectural issues (subagent race conditions, retention logic flaws) but frustrated by slow resolution.

- **OpenAI Codex**: More balanced community–engineering interaction. The SQLite log issue (#28224) was closed after three merged PRs. Security PRs are coming from internal engineers, not just community. But the top feature request (#11023 for Linux desktop) has 680 👍 with no visible commitment. The tool is **undergoing a security maturation phase** (many PRs this week target Git attack vectors), suggesting a focus on enterprise-grade reliability over feature velocity.

**Maturity assessment**:  
| Metric | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| Community activity | High | High |
| Engineering responsiveness | Low (on key bugs) | Medium (security fixes) |
| Release stability | Moderate (regressions common) | Alpha status for Rust client |
| Feature depth | High (subagents, scheduled tasks) | Moderate (core Git, sandbox) |
| Documentation gaps | Acknowledge (#73686, #73690) | Implicit (no major issues) |

---

## 6. Trend Signals

1. **Usage quota transparency is the #1 trust issue** – Both communities report unexplained quota draining (Claude Max plans, Codex Plus limits). Developers cannot monitor or predict costs, eroding confidence in subscription models. Expect third-party monitoring tools and internal API exposure as demand grows.

2. **Silent data loss undermines adoption** – Claude Code’s session cleanup bug and Codex’s log bloat demonstrate that developers will not tolerate opaque data management. Features like selective session pinning, configurable retention, and explicit recovery mechanisms will become table stakes.

3. **Security boundaries are becoming a differentiator** – Codex’s series of Git sandbox PRs (blocking repo-controlled filters, merge drivers, symlink traversal) reflects a broader industry shift toward zero-trust execution in AI coding tools. Claude Code’s lack of similar hardening may become a liability for enterprise use.

4. **Windows/Linux parity remains incomplete** – Both tools show significant friction on Windows (freezes, sandbox failures, file locking) and a strong Linux desktop demand (Codex). Cross-platform reliability is a prerequisite for widespread adoption in heterogeneous development shops.

5. **Model streaming regressions hurt real-time workflows** – Claude Code’s Opus 4.8 stream hang and Codex’s GPT-5.5 degradation indicate that model-side updates can break client-side flows. Developers need better version pinning or regression detection in CLI releases.

6. **Subagent/complex workflow orchestration is still immature** – Claude Code’s subagent race conditions and Codex’s context message misselection show that neither tool reliably handles multi-turn, multi-agent scenarios. Expect convergence on deterministic task graphs and result routing.

---

*Data extracted from public GitHub issues and PRs for anthropics/claude-code and openai/codex as of 2026-07-03.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-07-03 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following Pull Requests attracted the highest community attention (by comment volume and cross-referencing in Issues). All remain **open** as of the snapshot date.

### #1298 — Fix skill-creator run_eval.py (0% recall bug)
**Author:** MartinCajiao | **Status:** Open  
**URL:** https://github.com/anthropics/skills/pull/1298

**Functionality:** Repairs the core evaluation pipeline (`run_eval.py`, `run_loop.py`, `improve_description.py`) which was reporting `recall=0%` for every skill description — effectively making the description-optimization loop optimize against noise. The fix installs the eval artifact as a real skill, corrects Windows stream reading, trigger detection logic, and parallel worker handling.

**Discussion highlights:** Root-cause analysis traced the problem to how `claude -p` subprocesses handle skill invocation. Multiple independent reproductions confirmed the bug (Issue #556 has 10+ confirmations). The PR has been the most active cross-reference point for skill-creator issues.

### #514 — Add document-typography skill
**Author:** PGTBoos | **Status:** Open  
**URL:** https://github.com/anthropics/skills/pull/514

**Functionality:** Prevents typographic defects in AI-generated documents: orphan word wrap (1–6 words on a new line), widow paragraphs (headers stranded at page bottom), and numbering misalignment. Targets a universal pain point in Claude-generated output.

**Discussion highlights:** Strong community resonance — users noted these issues affect every document Claude generates. Technical discussion focused on whether the skill should be presentation-layer only or integrate with specific document formats (PDF, DOCX). Proposal to make it a default companion skill for document-generation workflows.

### #538 — Fix case-sensitive file references in PDF skill
**Author:** Lubrsy706 | **Status:** Open  
**URL:** https://github.com/anthropics/skills/pull/538

**Functionality:** Corrects 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where `REFERENCE.md` and `FORMS.md` were referenced in uppercase but the actual filenames are lowercase. Breaks on case-sensitive filesystems (Linux, macOS with case-sensitive volumes).

**Discussion highlights:** Triggered debate about repository conventions for file naming and whether the skill system should normalize paths. Also surfaced that the PDF skill had multiple undocumented dependencies on sibling files.

### #486 — Add ODT skill (OpenDocument Text)
**Author:** GitHubNewbie0 | **Status:** Open  
**URL:** https://github.com/anthropics/skills/pull/486

**Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Provides templates and HTML conversion. Triggers on mentions of ODT, ODS, ODF, OpenDocument, or LibreOffice.

**Discussion highlights:** Interest from European public-sector users where ODF is a mandated standard. Community requested additional support for ODP (presentations) and template variable injection patterns. Some concern about skill size given the complexity of ODF XML parsing.

### #210 — Improve frontend-design skill clarity
**Author:** justinwetch | **Status:** Open  
**URL:**
https://github.com/anthropics/skills/pull/210

**Functionality:** Revises the frontend-design skill for better clarity, actionability, and internal coherence. Ensures every instruction is executable within a single conversation with specific behavioral guidance.

**Discussion highlights:** Community debate on how prescriptive design skills should be — some argued for strict rules, others for flexible principles. The PR became a reference point for skill-writing philosophy (directive vs. suggestive tone). Authors across other skills began adopting its structural patterns.

### #1367 — Add self-audit skill (v1.3.0)
**Author:** YuhaoLin2005 | **Status:** Open  
**URL:** https://github.com/anthropics/skills/pull/1367

**Functionality:** Universal output-quality gate: mechanical file verification (verify every claimed output exists) followed by four-dimension reasoning audit in damage-severity priority order. Works across any project, tech stack, or model.

**Discussion highlights:** One of the most ambitious meta-skills proposed. Community discussion centered on whether mechanical verification should be mandatory infrastructure rather than a skill. High interest from enterprise users needing delivery guarantees.

---

## 2. Community Demand Trends

Analysis of the top 15 Issues reveals concentrated demand in four directions:

**Skill-Creator Reliability (dominant trend)**
Issues #556, #1169, and #1061 document a systemic bug where `run_eval.py` reports 0% recall across all queries — making the description-optimization loop useless. Multiple independent reproductions confirm this is a platform-specific bug (Windows subprocess handling, `claude -p` skill invocation). This is the community's most urgent technical blocker.

**Trust & Security Boundaries**
Issue #492 (34 comments, highest engagement) exposes a critical vulnerability: community skills distributed under the `anthropic/` namespace impersonate official Anthropic skills, enabling trust boundary abuse. Demand is high for namespace verification, signing, or tiered visibility.

**Windows Compatibility**
Issues #1061, #1169, and several PRs confirm that skill-creator scripts are effectively non-functional on Windows due to `PATHEXT` handling (`claude.cmd` vs `claude`), `cp1252` encoding, and `select()` on pipes. Windows users represent a vocal, blocked segment.

**Org-Wide Skill Distribution**
Issue #228 (14 comments, 7 upvotes) requests native organizational skill sharing — users currently must manually transfer .skill files via Slack/Teams. Demand for shared skill libraries and direct sharing links.

**Secondary themes:** Skill duplicates on plugin installation (#189), governance patterns for AI agent systems (#412), integration with AWS Bedrock (#29), and MCP exposure for skills (#16).

---

## 3. High-Potential Pending Skills

These open PRs have active discussion threads, strong technical foundations, and address clear community needs — suggesting imminent merge:

| PR | Skill | Why It May Land Soon |
|----|-------|---------------------|
| #1298 | run_eval fix | Blocks all skill-creator users; multiple maintainer comments; urgent dependency for #556/#1169 |
| #1367 | self-audit | Universal utility; complete implementation; no external dependencies |
| #1302 | color-expert | Self-contained; references authoritative color systems; low risk of conflicts |
| #723 | testing-patterns | Comprehensive but modular; fills clear gap in current skills collection |
| #806 | sensory (AppleScript) | Niche but well-scoped; macOS automation is a frequently requested capability |
| #1099 | Windows subprocess fix | Duplicate of #1050 but with more detailed reproduction; maintainer momentum building |

**Notable merges already in progress:** Multiple skill-creator fixes (#538, #539, #541) show that repository maintainers are actively processing quality-of-life corrections, which may accelerate the pipeline for feature skills.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, cross-platform skill-development toolchain** — the majority of engagement centers on fixing the `skill-creator` scripts (Windows compatibility, subprocess handling, trigger detection) rather than on any single domain skill, indicating that the ecosystem's growth is bottlenecked by developer-experience reliability rather than by skill-idea scarcity.

---

# Claude Code Community Digest — 2026-07-03

## Today's Highlights

A new patch release (v2.1.199) landed today, improving slash-skill stacking and SSL error handling, but the community remains focused on two persistent fires: a runaway 789-comment thread about abnormally fast Max plan session exhaustion, and a hot 65-comment bug where `AskUserQuestion` dialogs auto-dismiss after 60 seconds even while the user is actively typing. Subagent reliability and silent session cleanup also continue to generate significant discussion.

---

## Releases

**[v2.1.199](https://github.com/anthropics/claude-code/releases/tag/v2.1.199)** — Bugfix and quality-of-life release:
- **Stacked slash-skill invocations**: `/skill-a /skill-b do XYZ` now loads up to 5 leading skills, not just the first.
- **SSL/TLS certificate error handling**: Fixed a class of bugs where TLS-inspecting proxies, missing `NODE_EXTRA_CA_CERTS`, or expired certificates would burn API retries before showing actionable guidance. This should improve first-run experiences behind corporate proxies.

---

## Hot Issues (Top 10 Noteworthy)

1. **[#38335 – Max plan session limits exhausted abnormally fast](https://github.com/anthropics/claude-code/issues/38335)**  
   *789 comments, 467 👍*  
   The single most heated issue on the repo. Users on the Claude Max plan report session quotas burning through in hours instead of days starting March 23. Anthropic hasn’t made a public RC update in months, fueling frustration. Many users suspect a silent policy change or billing bug.

2. **[#73125 – AskUserQuestion: "No response after 60s" while user is typing](https://github.com/anthropics/claude-code/issues/73125)**  
   *65 comments, 224 👍*  
   A critical UI/UX bug affecting multi-step design or approval flows. The 60-second timeout fires while the user is mid-answer, forcing Claude to guess. Multiple duplicates have been filed (e.g. #73490, #73650), indicating high impact.

3. **[#65833 – Scroll wheel sends arrow keys instead of scrolling conversation](https://github.com/anthropics/claude-code/issues/65833)**  
   *30 comments, 53 👍*  
   Regression introduced in v2.1.150. Mouse wheel now cycles through input history instead of scrolling the conversation pane. Users on WSL are most affected; no fix has been shipped yet.

4. **[#59248 – Silent retention cleanup deletes session transcripts](https://github.com/anthropics/claude-code/issues/59248)**  
   *19 comments, 10 👍*  
   Users lose all conversation transcripts from a workspace, including sessions from the previous day, without warning. The cleanup runs on startup regardless of `cleanupPeriodDays` settings.

5. **[#41458 – `cleanupPeriodDays: 99999` ignored – 490 sessions deleted](https://github.com/anthropics/claude-code/issues/41458)**  
   *18 comments, 2 👍*  
   A concrete example of the retention bug: the configuration is overridden, leading to bulk deletion. Points to a deeper issue in the cleanup logic.

6. **[#21943 – Expose subscription usage data via file or API](https://github.com/anthropics/claude-code/issues/21943)**  
   *11 comments, 40 👍*  
   Long-standing feature request (since Jan 2026). Users want programmatic access to session/quotas to build monitoring dashboards or integrate with CI. `/usage` command is insufficient for automation.

7. **[#50911 – `CronCreate` durable:true silently dropped](https://github.com/anthropics/claude-code/issues/50911)**  
   *7 comments, 1 👍*  
   Scheduled tasks with `durable: true` are never persisted to `.claude/scheduled_tasks.json`. All tasks die on session end, breaking workflows that rely on background persistence.

8. **[#69824 – Subagents not awaiting nested subagent results](https://github.com/anthropics/claude-code/issues/69824)**  
   *6 comments, 0 👍*  
   Subagents spawn nested agents but proceed without waiting for results, sometimes fabricating fake completion notifications. Leads to duplicate work and race conditions. Another sign of subagent orchestration fragility.

9. **[#72639 – Opus 4.8 (1M) stream hangs after first chunk](https://github.com/anthropics/claude-code/issues/72639)**  
   *4 comments, 0 👍*  
   Regression in v2.1.154. Large context window streaming stops after the first chunk; v2.1.153 is the last known good version. Affects heavy document analysis or long-context coding sessions.

10. **[#61625 – API Usage Policy false positive on security terminology](https://github.com/anthropics/claude-code/issues/61625)**  
    *5 comments, 2 👍*  
    The Anthropic content classifier incorrectly flags security research terms (e.g., "Krebs", "Black Hat briefings") as policy violations. Blocks legitimate security testing.

---

## Key PR Progress

Only **4 pull requests** were updated in the last 24 hours, indicating a quiet day for community contributions.

| PR | Title | Status | Notes |
|----|-------|--------|-------|
| [#72451](https://github.com/anthropics/claude-code/pull/72451) | fix: remove statsig.anthropic.com from init-firewall.sh | **OPEN** | Fixes devcontainer startup failure when the stale hostname doesn't resolve. Small but important for developer experience on container-based setups. |
| [#73476](https://github.com/anthropics/claude-code/pull/73476) | docs: fix GitHub capitalization in README | **OPEN** | Typo fix: "Github" → "GitHub". No functional impact. |
| [#72543](https://github.com/anthropics/claude-code/pull/72543) | Create Cha | **OPEN** | Empty/incomplete PR with no description. Likely spam or accidental. |
| [#72866](https://github.com/anthropics/claude-code/pull/72866) | docs: fix Github → GitHub typo in README | **OPEN** | Duplicate of #73476. Two PRs for the same doc fix within two days. |

**Observation**: The almost total lack of meaningful PR activity contrasts with the high volume of bug reports. This suggests either (a) the barrier to contributing fixes is high, (b) the issues are primarily server-side or require Anthropic-internal changes, or (c) maintainer bandwidth is limited.

---

## Feature Request Trends

1. **Session & transcript retention control** (multiple issues inc. #59248, #41458, #63842)  
   Users repeatedly ask for selective session pinning/bookmarking, configurable cleanup that is actually respected, and recovery mechanisms. The blunt `cleanupPeriodDays` approach is universally disliked.

2. **Programmatic usage data** (#21943)  
   A consistent ask for API or file-based access to quota/reset timestamps. Currently only available via the interactive `/usage` command.

3. **Timeout configurability for user prompts** (#73691, #73125)  
   The 60-second auto-dismiss is seen as hostile to thoughtful interaction. Users want either a configurable timeout or the ability to disable it entirely.

4. **Subagent orchestration improvements** (#69824, #69212, #69260)  
   Features around result routing, proper await/dependency chains, and hook execution for subagents. The current implementation leaves users with race conditions and unauthorized tool use.

5. **Model guardrail transparency** (#73693)  
   Users in security research request demotion logic that considers context (e.g., self-audit vs. malicious prompt). A false-positive downgrade from Fable to Opus is seen as productivity loss.

6. **Documentation completeness** (#73686, #73690)  
   Multiple docs issues point to gaps in Agent View documentation, particularly around supervisor process behavior and release notes for minor features.

---

## Developer Pain Points

- **Silent data loss**: The session cleanup bug (#59248, #41458) destroys weeks of work with no warning or recovery path. This is the single most alarming issue for power users.
- **AskUserQuestion auto-dismiss**: A direct UX regression that breaks interactive workflows. Developers relying on multi-turn approval loops are forced to work around it with faster typing or scripted responses.
- **Subagent fragility**: Race conditions (#69824), hooks not firing (#69260), and result misrouting (#69212) erode trust in the Agent tool. Users who depend on complex multi-agent orchestrations cannot rely on consistent behavior.
- **Model streaming regressions**: Opus 4.8 stream hangs (#72639) and the scroll wheel regression (#65833) are signs of inadequate regression testing in the release pipeline.
- **Windows/corporate environment friction**: Stale DNS errors (#72451), PDF tool failures (#73696), and AppX file locks (#73694) make Claude Code less portable in enterprise Windows contexts.
- **High session count without root cause**: The Max plan exhaustion bug (#38335) remains the #1 reported issue with no official resolution, undermining trust in Anthropic’s billing and usage tracking.

---

*Data snapshot: 2026-07-03 23:59 UTC. Generated from anthropics/claude-code public GitHub activity in the last 24 hours.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**Community Digest – Wednesday, July 3, 2026**

---

## Today’s Highlights

Two minor Rust alpha releases (v0.143.0-alpha.34/35) land without visible changelogs, while the community focuses on a massive thread requesting a **Linux Codex desktop app** (680 👍) and a high-impact fix to **SQLite feedback logs** that previously could write ~640 TB/year. A series of security‑hardening PRs from OpenAI engineers tightens Git helper execution boundaries, reflecting a broader push to protect against repository‑controlled attacks.

---

## Releases

- **`rust-v0.143.0-alpha.35`** – Patch release (no detail beyond version bump).  
  [GitHub Release](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.35)
- **`rust-v0.143.0-alpha.34`** – Patch release.  
  [GitHub Release](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.34)

---

## Hot Issues (10 selected)

1. **#11023 – Codex desktop app for Linux**  
   [Issue](https://github.com/openai/codex/issues/11023)  
   *139 comments, 680 👍* – The most‑voted request: a native Linux desktop app. Users cite macOS power consumption issues and want to use their Linux workstations. Community engagement is extremely high.

2. **#28224 – SQLite feedback logs can write ~640 TB/year, consuming SSD endurance**  
   [Issue](https://github.com/openai/codex/issues/28224)  
   *129 comments, 419 👍* – Three merged PRs now reduce logs by ~85%, addressing a severe performance and hardware‑wear concern. Closed by the author after the fix was released in 0.142.0.

3. **#8648 – Codex replies to earlier messages instead of latest**  
   [Issue](https://github.com/openai/codex/issues/8648)  
   *73 comments, 55 👍* – A long‑standing agent context bug causing incorrect message selection in multi‑turn conversations. Still open after six months.

4. **#20214 – Codex App freezes/stutters on Windows 11**  
   [Issue](https://github.com/openai/codex/issues/20214)  
   *23 comments, 39 👍* – Reports of freezing despite ample RAM (32 GB) and a modern CPU. Windows users are particularly affected.

5. **#28969 – Add setting to disable the 60‑second auto‑resolve**  
   [Issue](https://github.com/openai/codex/issues/28969)  
   *10 comments, 74 👍* – Strong demand for a configurable timeout on Codex CLI’s automatic question resolution. Very high upvote‑to‑comment ratio.

6. **#24431 – GPT-5.5 performance and reliability significantly worse**  
   [Issue](https://github.com/openai/codex/issues/24431)  
   *8 comments, 14 👍* – Users report GPT‑5.5 failing to fix simple bugs and breaking existing code. Open – may indicate a model‑side regression.

7. **#29193 – Windows node_repl/js fails with missing `sandboxPolicy`**  
   [Issue](https://github.com/openai/codex/issues/29193)  
   *21 comments, 4 👍* – MCP JavaScript execution fails on Windows Desktop due to a missing sandbox‑state field. Blocks many browser/computer‑use workflows.

8. **#28997 – `logs_2.sqlite-wal` grows unbounded (tens of GB)**  
   [Issue](https://github.com/openai/codex/issues/28997)  
   *11 comments, 3 👍* – WAL file for CLI logs can explode in size. Related to #28224 but not yet fully fixed.

9. **#30918 / #30939 – Usage limits draining 5‑10x too fast**  
   [Issues](https://github.com/openai/codex/issues/30939) and [30918](https://github.com/openai/codex/issues/30918)  
   *8 comments combined* – Two concurrent reports that Plus usage limits burn through the 5‑hour window in minutes. High concern for heavy users.

10. **#27552 – Windows: image attachment saved to Temp but not accessible to WSL**  
    [Issue](https://github.com/openai/codex/issues/27552)  
    *8 comments, 6 👍* – Desktop + WSL workspace interop failure: images are placed in Windows Temp, but the Linux sandbox cannot access them.

---

## Key PR Progress (10 selected)

1. **#30963 – Validate approval responses against pending authority**  
   [PR](https://github.com/openai/codex/pull/30963) – Hardens approval flow so an exec response cannot consume a patch waiter. Prevents client‑supplied data from bypassing boundaries.

2. **#30628 – Trust only system PowerShell parsers on Windows**  
   [PR](https://github.com/openai/codex/pull/30628) – Prevents repository‑supplied `powershell.exe` from running before sandbox checks. Security fix.

3. **#30493 – Add configurable multi‑agent mode hint text**  
   [PR](https://github.com/openai/codex/pull/30493) – Enables deployments to replace built‑in mode instructions with a stable policy. Closed (merged).

4. **#30801 – Sanitize exec config summary values**  
   [PR](https://github.com/openai/codex/pull/30801) – Cleans control characters from repo‑controlled values before display. Prevents terminal injection.

5. **#30876 – Support interleaved response items**  
   [PR](https://github.com/openai/codex/pull/30876) – Allows reasoning summaries and final text to be streamed out of order, keeping TUI output correct.

6. **#30837 – Derive effective patch paths through Git**  
   [PR](https://github.com/openai/codex/pull/30837) – Uses Git’s own path resolution for renames, copies, and headers to avoid mismatched safety checks.

7. **#30850 – Block selected Git filters before staging patch paths**  
   [PR](https://github.com/openai/codex/pull/30850) – Prevents `git add` from running repo‑configured filters on unvalidated files.

8. **#30896 – Centralize repository authority for Git helper launches**  
   [PR](https://github.com/openai/codex/pull/30896) – Single scope that decides trusted Git executable, improving performance and security on Windows.

9. **#30854 – Block selected merge drivers before three‑way patch application**  
   [PR](https://github.com/openai/codex/pull/30854) – Avoids custom merge‑driver execution when using `git apply --3way`.

10. **#30844 – Confine staged patch paths to the parent worktree**  
    [PR](https://github.com/openai/codex/pull/30844) – Prevents symlink / submodule traversal during staging, closing a privilege‑escalation vector.

---

## Feature Request Trends

- **Linux desktop app** remains the #1 ask by a wide margin (issue #11023, 680 👍).  
- **Configurable CLI auto‑resolve timeout** (#28969, 74 👍) shows strong demand for user‑control over model‑initiated actions.  
- **First‑class Computer Use in CLI** (#20851, 9 👍) continues to be requested as an alternative to the desktop‑only plugin.  
- **Worktree selection** (issue #22316) and **worktree UI improvements** (#10704) highlight users wanting more flexible Git integration from the app.  
- **MCP tool exposure parity** between desktop and CLI is a recurring theme (issues #30486, #30343).  
- **Image generation timeouts** (#29645) and **multi‑agent mode configuration** (PR #30493) round out the recent requests.

---

## Developer Pain Points

- **Windows reliability** – Frequent freezes (#20214), blank VS Code panels (#21863), sandbox/MCP failures (#29193, #30486, #27552), temperature spikes (#30055), and silent exits (#30962) make Windows the most problematic platform.
- **Usage limit drain** – Multiple reports (#30918, #30939) of limits burning 5–10x faster than expected, affecting Plus subscribers heavily.
- **Log bloat** – SQLite logs consuming tens of GB (#28997) and wear on SSDs (#28224, now partially fixed) frustrate terminal users.
- **Context / conversation bugs** – Agent replying to the wrong message (#8648) remains unresolved for over six months.
- **Model regressions** – GPT‑5.5 degradation (#24431) sparks concern about reliability of the primary model.
- **CLI usability** – Auto‑resolve annoyance (#28969) and Windows paste‑execute confusion (#13729) show room for polish.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*