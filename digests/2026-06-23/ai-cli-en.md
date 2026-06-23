# AI CLI Tools Community Digest 2026-06-23

> Generated: 2026-06-23 02:50 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools  
**Date:** 2026-06-23  
**Data Sources:** Claude Code Community Digest, OpenAI Codex Community Digest  

---

## 1. Ecosystem Overview

The AI CLI tools landscape is maturing rapidly, with both Claude Code and OpenAI Codex shipping daily releases while confronting growing pains in reliability, transparency, and cross-platform support. Community conversations have pivoted from raw capability to operational trust—users are laser-focused on cost predictability, data persistence, and sandbox stability. Both tools are investing heavily in plugin/MCP infrastructure and usage accounting, but divergent release cadences and community priorities reveal distinct strategic emphases. The day’s activity underscores that user trust is now the primary competitive battleground.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Recent release** | v2.1.186 (stable) | rust-v0.142.0 (stable) + 2 alphas |
| **Hot issues in digest** | 10 (10 open) | 10 (9 open, 1 closed) |
| **PRs listed in digest** | 4 (all open) | 10 (mix of open/merged) |
| **Highest-upvoted issue** | #17968 (87👍, JSONC support) | #28879 (239👍, rate-limit cost jump) |
| **Most commented issue** | #60226 (45 comments) | #28879 (121 comments) |
| **Data-loss reports** | 3 (Windows blank screen, missing messages, macOS history loss) | 2 (Crashpad dumps, SQLite log churn; no direct data loss) |
| **Cross-platform regressions** | Windows white screen, iOS crash, macOS auth redirect | Windows sandbox fail, macOS SQLite log churn, Windows fan/GPU spike |
| **PR velocity (24h)** | Low (4 PRs, no major feature PRs in review) | High (10 PRs; active backport and feature work) |

**Summary:** OpenAI Codex shows higher activity volume and a more complex release pipeline, but Claude Code’s community is equally engaged on critical bugs (especially data loss). Codex’s most viral issue has 3x the upvotes of Claude’s top feature request, indicating a sharper acute pain point.

---

## 3. Shared Feature Directions

- **Plugin & MCP Ecosystem Improvements**  
  *Both tools* are iterating on plugin authentication (Claude added `mcp login` CLI commands; Codex reorganized plugin sections and improved MCP server identity). Both communities want better plugin discovery, cross-platform reliability, and seamless sharing between desktop and CLI.

- **Configuration with Comments / Transparency**  
  *Claude* explicitly requests JSONC for `settings.json` (87👍). *Codex*’s analogous need is real-time per-token cost visibility and breakdowns of quota consumption. Both trends reflect user demand for human-readable, documented configuration and auditability.

- **Cross-Platform Parity**  
  *Claude*: Windows data-loss and blank screen, macOS auth redirect, iOS crash. *Codex*: Windows sandbox fails, idle CPU/GPU spikes, macOS SQLite log churn. Both communities report that Windows users feel like second-class citizens, and CLI vs. desktop consistency remains fragile.

- **Resource Efficiency**  
  *Claude*: Windows Defender race causing `EBUSY` on plugin install, MCP fleet memory leaks on Windows. *Codex*: SQLite log bloat (~640 TB/year partially fixed, but residual churn persists), Crashpad dumps growing +5GB/day. Users want background processes that don’t silently drain disk or battery.

- **Session / Quota Transparency**  
  *Claude*: session limit resets unexpectedly early (#69592). *Codex*: rate-limit cost jumped 10-20x (#28879), Pro subscribers treated as Plus (#29243). Both communities demand clear, predictable enforcement and breakdowns of why their limited budget is consumed.

- **Undo / Recovery Features**  
  *Claude*: `/unclear` command request (31👍) to restore cleared context. *Codex*: No direct analogue, but the token-budget compaction PR (#29521) resets context, which could be seen as a similar “fresh start” mechanic. Data-loss issues amplify the need for recovery mechanisms.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|-----------|-------------|--------------|
| **Primary focus** | Agentic workflow (team management, git integration, `/workflows` agent) | Cost control & plugin ecosystem (/usage credits, /plugins reorganization, rate-limit monitoring) |
| **Target user** | Developer teams using native CLI agents (TUI-centric) | Individual developers & enterprises needing predictable pricing and sandboxed execution |
| **Technical approach** | Monolithic TUI with agent orchestration; MCP as secondary channel | Microservice architecture with Rust backend; plugin-first design; desktop app as first-class client |
| **Pain point intensity** | **Data loss** is the dominant narrative – multiple reports across Windows and macOS erode trust in persistence | **Cost spikes** are the dominant narrative – the rate-limit regression (#28879) is causing immediate financial pain and workflow halts |
| **Community engagement style** | Ugvoted feature requests with long tails (JSONC request since Jan 2026) | Rapidly escalating hot issues with hundreds of reactions and comments (viral anger) |
| **Release maturity** | Stable channel with single version; occasional regressions | Three-channel model (stable, alpha, internal) with frequent merges; more complex patch management |
| **Enterprise readiness** | Weak – data loss and team-management tool regressions (#68721) undermine confidence | Mixed – Pro plan tier mismatches and missing reset credits erode trust, but plugin sharing and usage analytics are maturing |

**Bottom line:** Claude Code doubles down on agent autonomy and TUI power; OpenAI Codex prioritizes cost visibility and plugin extensibility. Each tool’s challenges reflect its core bet – Claude’s data-loss problems threaten its “always on” agent promise; Codex’s cost anomalies threaten its “predictable pricing” value prop.

---

## 5. Community Momentum & Maturity

- **OpenAI Codex** has the higher-velocity, more engaged community in the short term – the rate-limit issue (#28879) attracted 239👍 and 121 comments in days, indicating an active user base that feels heard (or is loud about not being heard). The number of PRs (10 in one digest) and the complex release pipeline suggest a rapidly iterating engineering team. However, the “incomplete fixes” sentiment (e.g., SQLite log fix only partially effective) shows the community is sophisticated and unforgiving.

- **Claude Code** has a slower but more deliberate pulse – only 4 PRs today, but long-standing feature requests (87👍 for JSONC) persist for months. The community is patient but frustrated by regressions that break core workflows (team management, data persistence). Claude’s iOS crash (#70165) and Windows blank screen (#51143) are severe but less viral. The absence of major feature PRs in review is a signal that the team may be focusing on stabilization.

- **Maturity level:** Both tools are past early adopter phase but not yet enterprise-grade. Claude has stronger TUI polish but weaker reliability; Codex has stronger cost infrastructure but weaker cross-platform consistency. Neither tool inspires full confidence in persistence or quota fairness.

---

## 6. Trend Signals

1. **Rate-limit transparency is no longer optional.** Codex’s viral issue and Claude’s session limit complaint indicate that users will not tolerate opaque consumption. Expect both tools to introduce real-time token/cost counters, per-prompt breakdowns, and configurable budget caps.

2. **Data loss erodes trust faster than feature gaps.** Multiple data-loss reports across both tools (Claude: Windows blank screen, missing messages; Codex: Crashpad dumps, log churn) show that users prioritize reliability over new features. Tools that invest in persistence testing and crash recovery will win loyalty.

3. **MCP/plugin ecosystems demand authentication standardization.** Both tools are adding CLI-based MCP login flows. The ecosystem is moving beyond interactive menus toward scriptable, automatable credential management – a prerequisite for CI/CD and SSH environments.

4. **Cross-platform parity is a growing liability.** Windows and macOS regressions appear weekly in both digests. As developer tooling becomes more distributed, teams expect identical behavior across platforms. Tools that neglect Windows (or treat it as secondary) will face exodus.

5. **Community trust is fragile and viral.** A single cost spike (#28879) or data-loss wave can spiral into 100+ comment threads within days. Both teams must prioritize incident communication and root-cause acknowledgment over silent fixes.

6. **Configuration file ergonomics matter.** The JSONC request (Claude, 87👍) and the SQLite log control demands (Codex) signal that developers want to inspect and modify behavior via readable, versioned config files – not just through TUI menus or opaque settings.

**Actionable insight for developers:**  
- If you rely on *cost predictability*, monitor Codex's rate-limit issues closely; consider switching to Fast mode or limiting session length until official fix lands.  
- If you rely on *session persistence and data safety*, hold off on Claude Desktop updates on Windows until blank screen and history-loss bugs are resolved.  
- For *cross-platform teams*, neither tool is fully reliable today – test updates on each OS before rolling out.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-06-23 • Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

### #1 — `skill-creator` Fix: `run_eval.py` 0% Recall Bug
**PR #1298** — *Open* — [View on GitHub](https://github.com/anthropics/skills/pull/1298)

The most-discussed PR in the repository addresses a critical bug where `run_eval.py` (and dependent scripts `run_loop.py` and `improve_description.py`) consistently reports `recall=0%` for every skill description. The root cause spans multiple issues: the eval artifact isn't installed as a real skill, Windows stream reading fails, trigger detection is broken, and parallel workers behave incorrectly. The description-optimization loop—which is supposed to iteratively improve skill descriptions—has been optimizing against noise rather than genuine signal.

> **Discussion highlights:** Referenced across issues #556 and #1169 (15+ combined comments, 10+ independent reproductions). This is widely acknowledged as the single most impactful fix needed for the skill-creator workflow.
> **Status:** Open. Author @MartinCajiao has produced an unusually comprehensive fix spanning the entire eval pipeline.

---

### #2 — `document-typography`: Typographic Quality Control
**PR #514** — *Open* — [View on GitHub](https://github.com/anthropics/skills/pull/514)

A skill that prevents common typographic problems in AI-generated documents: orphan word wrap (1-6 words spilling onto the next line), widow paragraphs (section headers stranded at page bottom), and numbering misalignment. The PR argues these issues affect every document Claude generates, yet users rarely request typographic fixes explicitly.

> **Discussion highlights:** Commenters noted this fills a genuine gap—typographic polish is often overlooked in AI document generation. Some discussion on whether this should be a standalone skill or folded into the existing `document-skills` plugin.
> **Status:** Open, awaiting review.

---

### #3 — `odt`: OpenDocument Text Creation and Template Filling
**PR #486** — *Open* — [View on GitHub](https://github.com/anthropics/skills/pull/486)

Adds comprehensive support for OpenDocument Format files (.odt, .ods), including creation, template filling, and conversion to HTML. Triggers on mentions of "ODT", "ODS", "ODF", "OpenDocument", or "LibreOffice document".

> **Discussion highlights:** Community members highlighted the need for ISO-standard document format support, particularly in European government and enterprise contexts where ODF is mandated. Some debate on scope—whether to include spreadsheet (.ods) support or keep it document-only.
> **Status:** Open.

---

### #4 — `skill-quality-analyzer` and `skill-security-analyzer`: Meta-Skills
**PR #83** — *Open* — [View on GitHub](https://github.com/anthropics/skills/pull/83)

Two meta-skills that analyze other skills: `skill-quality-analyzer` evaluates across five dimensions (Structure & Documentation, Example Quality, Resource Usage, etc.), while `skill-security-analyzer` audits skills for security vulnerabilities. The quality analyzer also includes self-assessment templates.

> **Discussion highlights:** Early interest in tooling that enforces quality standards across the ecosystem. Some concerns about circular evaluation (meta-skills evaluating themselves) and whether quality metrics are well-calibrated.
> **Status:** Open, one of the earliest PRs still pending (since November 2025).

---

### #5 — `testing-patterns`: Full-Stack Testing Skill
**PR #723** — *Open* — [View on GitHub](https://github.com/anthropics/skills/pull/723)

A comprehensive testing skill covering the full stack: Testing Trophy model philosophy, AAA unit testing patterns, React component testing with Testing Library, integration testing, E2E testing, and CI/CD integration. Emphasizes what to test vs. what NOT to test.

> **Discussion highlights:** Strong community support for a testing-focused skill. Some discussion on whether to include language-specific sections (Python vs. JavaScript) or keep it framework-agnostic.
> **Status:** Open.

---

### #6 — `servicenow`: Enterprise ServiceNow Platform Skill
**PR #568** — *Open* — [View on GitHub](https://github.com/anthropics/skills/pull/568)

A broad ServiceNow platform assistant covering ITSM, ITOM, ITAM/SAM Pro, FSM, HRSD/CSM, SPM/PPM, Vulnerability Response, Security Incident Response, CSDM data modeling, and IntegrationHub.

> **Discussion highlights:** Enterprise users expressed strong demand for ServiceNow support, noting it's one of the most common enterprise platforms. Scope concerns about a single skill covering too many domains were raised.
> **Status:** Open.

---

### #7 — `aurelion-kernel/advisor/agent/memory`: Cognitive Framework Suite
**PR #444** — *Open* — [View on GitHub](https://github.com/anthropics/skills/pull/444)

Four skills from the AURELION ecosystem: `aurelion-kernel` (5-floor structured thinking framework), `aurelion-advisor` (domain-specific configuration), `aurelion-agent` (autonomous task execution), and `aurelion-memory` (vector-based persistent memory).

> **Discussion highlights:** The most ambitious multi-skill submission. Generated discussion about skill complexity thresholds and whether frameworks this opinionated belong in the official collection.
> **Status:** Open.

---

## 2. Community Demand Trends

### Trend #1: 🚨 **Reliability and Bug Fixing** *(Highest urgency)*
Issue **#556** (run_eval.py 0% trigger rate, 12 comments) and **#1169** (recall=0% across iterations, 3 comments) together represent the community's most acute pain point. The skill-creator evaluation pipeline is fundamentally broken for a significant portion of users. This is not a feature request—it's a workflow blocker.

### Trend #2: 🔒 **Security and Trust Boundaries**
Issue **#492** (9 comments) raises serious concerns about community skills distributed under the `anthropic/` namespace impersonating official skills. Users want clear provenance and security guarantees before running third-party skills. This intersects with broader conversations about signing, sandboxing, and permission scoping.

### Trend #3: 🏢 **Enterprise and Organizational Features**
Issue **#228** (14 comments, highest-commented) requests org-wide skill sharing without manual file transfer. Issue **#1175** (SharePoint/SPO access control) and **#568** (ServiceNow) reflect enterprise demand for structured, governed AI integration with existing platforms.

### Trend #4: 🪟 **Windows Compatibility**
Issues **#1061** (3 comments) and **#556** document critical Windows failures in skill-creator scripts. Multiple PRs (#1050, #1099, #1298) address Windows-specific `subprocess`, `PATHEXT`, `cp1252 encoding`, and `select` on pipes issues—suggesting a significant Windows user base facing daily friction.

### Trend #5: 🧠 **Agent Governance and Safety Patterns**
Issue **#412** (skill proposal for agent-governance) and **#1329** (compact-memory for agent state) indicate growing interest in patterns for managing long-running agent behavior, context budgeting, and safety guardrails.

---

## 3. High-Potential Pending Skills

| Skill | PR | Comments Activity | Why It May Land Soon |
|-------|----|-------------------|----------------------|
| **`document-typography`** | [#514](https://github.com/anthropics/skills/pull/514) | High initial engagement | Low complexity, clearly scoped, broad applicability to all document outputs |
| **`odt` (OpenDocument)** | [#486](https://github.com/anthropics/skills/pull/486) | Sustained discussion | ISO standard compliance is a blocker for enterprise adoption; clear demand |
| **`testing-patterns`** | [#723](https://github.com/anthropics/skills/pull/723) | Moderate | Well-structured, addresses a universal need, no controversial design choices |
| **`skill-quality-analyzer`** | [#83](https://github.com/anthropics/skills/pull/83) | Low recent activity but high historical | Oldest pending PR; may land as quality gate for future submissions |
| **`servicenow`** | [#568](https://github.com/anthropics/skills/pull/568) | Moderate | Enterprise demand is clear; may need scope reduction to pass review |
| **`frontend-design` (revised)** | [#210](https://github.com/anthropics/skills/pull/210) | Low recent activity | Improvement of existing skill, not a new addition—lower review bar |

---

## 4. Skills Ecosystem Insight

> **The community's most concentrated demand is for skill-creator pipeline reliability (fixing the broken 0% recall bug on Windows and Unix) and enterprise governance features (org-wide sharing, security provenance, and platform integrations like ServiceNow and ODF), reflecting a shift from "what skills can do" to "how skills are managed and trusted at scale."**

---

# Claude Code Community Digest — 2026-06-23

## Today's Highlights

Version 2.1.186 ships CLI-based MCP server authentication and status filtering for the `/workflows` agent. The community is buzzing about a regression that broke native team‑management tools, a long‑standing request for JSONC settings support, and a crop of iOS crashes in the latest app update. Several data‑loss bugs on Windows and macOS continue to draw attention.

---

## Releases

**v2.1.186** — [Release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.186)
- Added `claude mcp login <name>` and `claude mcp logout <name>` for authenticating MCP servers directly from the CLI, bypassing the interactive `/mcp` menu. Supports `--no-browser` stdin redirect for SSH completions.
- Added status filtering (press `f`) to the `/workflows` agent view.

---

## Hot Issues

1. **#60226 – Self-identified blocking gaps do not gate output**  
   *[bug, area:model, area:agent]* — Claude states that its own analysis is unfounded and then proceeds to complete it anyway. Community describes this as a “self‑deception” pattern that undermines trust in agent output. 45 comments, no upvotes.  
   [Link](https://github.com/anthropics/claude-code/issues/60226)

2. **#68721 – TeamCreate/TeamDelete tools no longer surfaced (regression)**  
   *[bug, regression, platform:linux]* — Tools added in v2.1.177 disappeared in v2.1.178. 17 comments, 5 👍. Affects native team workflow.  
   [Link](https://github.com/anthropics/claude-code/issues/68721)

3. **#17968 – Support JSONC format for settings files**  
   *[feature]* — Long‑running request (since Jan 2026) with 87 👍 and 16 comments. Users want comments in `settings.json` without resorting to hacks like `_comment` keys.  
   [Link](https://github.com/anthropics/claude-code/issues/17968)

4. **#36215 – Redirect URI not supported by client (macOS auth)**  
   *[bug, area:auth]* — Authorization flow fails with a redirect‑URI error. 15 comments, no upvotes. Common blocker for macOS users.  
   [Link](https://github.com/anthropics/claude-code/issues/36215)

5. **#51143 – Blank/white screen on Windows Desktop**  
   *[bug, area:desktop]* — Persistent blank screen after launch, cowork unusable. Multiple reinstalls have no effect. 15 comments, 12 👍.  
   [Link](https://github.com/anthropics/claude-code/issues/51143)

6. **#12908 – Conversation history disappeared after update**  
   *[bug, memory, area:ide]* — Update caused total loss of stored session history. 14 comments, 18 👍.  
   [Link](https://github.com/anthropics/claude-code/issues/12908)

7. **#53717 – Windows: message content missing after auto-update**  
   *[bug, data-loss, area:desktop]* — Sessions appear in sidebar but all message content is gone; JSONL files not persisted. 10 comments, 4 👍.  
   [Link](https://github.com/anthropics/claude-code/issues/53717)

8. **#69592 – Session limit resets unexpectedly early**  
   *[question, area:cost]* — User hit a 5‑hour limit far sooner than expected, questioning throttling logic. 6 comments.  
   [Link](https://github.com/anthropics/claude-code/issues/69592)

9. **#39975 – `/unclear` command to undo `/clear`**  
   *[feature, area:tui]* — A simple quality‑of‑life request: restore context after a clear. 5 comments, 31 👍.  
   [Link](https://github.com/anthropics/claude-code/issues/39975)

10. **#70165 – iOS app hard‑crashes opening Remote Control session**  
    *[bug, regression, platform:ios]* — Swift KeyPath metadata stack overflow introduced in version 1.260618.0. 2 comments, 0 👍, but critical for iOS users.  
    [Link](https://github.com/anthropics/claude-code/issues/70165)

---

## Key PR Progress

Only four pull requests were updated in the last 24 hours. All are open.

1. **#70173 – Fix `/clean_gone` detection of `[gone]` branches**  
   `git branch -v` doesn’t show remote‑tracking status; changed to `git branch -vv`. One line fix but resolves silent no‑op.  
   [Link](https://github.com/anthropics/claude-code/pull/70173)

2. **#63686 – Bump stale/autoclose timeouts from 14 to 90 days**  
   Proposes to reduce churn in the issue tracker by extending the inactivity window.  
   [Link](https://github.com/anthropics/claude-code/pull/63686)

3. **#70074 – Fix stale marketplace name in plugin‑dev README**  
   Renames `claude-code-marketplace` to `claude-code-plugins`.  
   [Link](https://github.com/anthropics/claude-code/pull/70074)

4. **#70066 – Update marketplace install docs in plugin‑dev README**  
   Clarifies install command from `cc --plugin-dir` to `claude --plugin-dir`.  
   [Link](https://github.com/anthropics/claude-code/pull/70066)

> *Note:* PR activity is low today. No major feature or bug‑fix PRs are currently in review.

---

## Feature Request Trends

- **Configuration with comments** (✨ 87 👍): JSONC support for `settings.json` is the most‑upvoted feature request.
- **Undo `/clear`** (✨ 31 👍): `/unclear` command to restore cleared context.
- **Client‑side edit preview** (#70188): Allow editing a proposed file change in `$EDITOR` before writing.
- **Configurable git polling** (#70186): `gitPollingIntervalMs` setting to reduce background git activity.
- **Feature parity with Ultracode** (#70190): A vague but recurring desire for more TUI goodies.

---

## Developer Pain Points

- **Data loss after updates** — Multiple reports on Windows (white screen, missing messages, sessions list but no content) and macOS (history gone). Users are frustrated by unreliable persistence.
- **Authentication failures** — Redirect URI errors on macOS, token not written to Keychain, and “Max 5x account cannot be authenticated” on Windows.
- **iOS regression** — Two separate crashes in the latest app update (hard crash on Remote Control session, immediate crash on new code session).
- **Agent self‑contradiction** — #60226 highlights a model bug where Claude knowingly proceeds with flawed reasoning.
- **Session limits** — #69592 suggests quota enforcement may be inconsistent or opaque.
- **Windows Defender race** — Plugin installs fail with `EBUSY` due to real‑time scanning (#67595).
- **Memory / process leaks** — MCP fleets not reaped on Windows session end (#68394).

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-23

A day of intense rate-limit scrutiny, plugin ecosystem maturation, and cross-platform stability fixes. The community remains laser-focused on unexplained quota consumption spikes, while the Codex team pushes forward with MCP infrastructure consolidation, token budget refinements, and Windows sandbox repairs.

---

## Today's Highlights

Rate-limit anomalies dominate the conversation, with Issue #28879 surpassing 120 comments as users report 10-20x cost-per-token increases since mid-June. The team merged critical fixes to reduce SQLite feedback log bloat (~640 TB/year avoided) and shipped rust-v0.142.0 with improved usage credit management and plugin organization. Multiple PRs signal ongoing investment in context window accounting and MCP server identity cleanup.

---

## Releases

### rust-v0.142.0 (stable)
- **`/usage`** now displays and redeems earned usage-limit reset credits, with confirmation dialogs, retry logic, and refreshed availability states ([#28154](https://github.com/openai/codex/issues/28154), [#28793](https://github.com/openai/codex/issues/28793))
- **`/plugins`** reorganizes remote plugins into three sections: OpenAI Curated, Workspace, and Shared with me, with turn-eligible recommendations

### rust-v0.143.0-alpha.1 / alpha.2
- Placeholder releases; no changelog details provided

### rust-v0.142.0-alpha.11 / alpha.12
- Placeholder releases; no changelog details provided

---

## Hot Issues

1. **[#28879](https://github.com/openai/codex/issues/28879) — Rate-limit cost per token jumped 10-20x since June 16**  
   *Status: OPEN | 121 comments | 239 👍*  
   The most viral issue of the week. Users on Plus plan report their 5-hour budget draining in 2-3 prompts on `gpt-5.5`. Session logs confirm `limit-% consumed per token` increased dramatically. Community frustration is high; OpenAI has not yet acknowledged root cause.

2. **[#28224](https://github.com/openai/codex/issues/28224) — SQLite feedback logs writing ~640 TB/year**  
   *Status: CLOSED | 39 comments | 265 👍*  
   Two merged PRs (#29432, #29457) reduce log volume by ~85%. Issue closed today. This was a top community concern for SSD endurance; the resolution is widely celebrated.

3. **[#28982](https://github.com/openai/codex/issues/28982) — Windows sandbox setup fails: "The specified module could not be found"**  
   *Status: OPEN | 29 comments | 9 👍*  
   App version 26.616.3309.0 breaks native sandbox helper on Windows x64. Affects Plus users. Related to #29418 (also open). No fix merged yet.

4. **[#28978](https://github.com/openai/codex/issues/28978) — Desktop app 26.616: new conversations fail with missing `inputSchema`**  
   *Status: OPEN | 20 comments | 24 👍*  
   Fresh conversations in the desktop app fail immediately after auto-update. CLI with identical config works fine, pointing to a desktop-specific MCP regression. Pro users affected.

5. **[#28823](https://github.com/openai/codex/issues/28823) — Usage meter consumes faster than historical comparable sessions**  
   *Status: OPEN | 16 comments*  
   Corroborates #28879 with local telemetry vs. server-side meter mismatch. Suggests a server-side quota accounting regression.

6. **[#25921](https://github.com/openai/codex/issues/25921) — Crashpad dumps grow +5GB/day with no limit**  
   *Status: OPEN | 13 comments | 3 👍*  
   Desktop app continuously generates `.dmp` files in Crashpad/pending. 54,504 files in one day observed. Long-standing issue (since June 2) with no fix.

7. **[#28504](https://github.com/openai/codex/issues/28504) — Pro ($200/month) account missing Codex reset bank and referral entitlements**  
   *Status: OPEN | 6 comments | 6 👍*  
   Pro subscribers not receiving advertised usage-reset credits. Underscores broader rate-limit transparency concerns.

8. **[#29243](https://github.com/openai/codex/issues/29243) — Pro $100 (5x) plan rate-limited as `plus` on Desktop**  
   *Status: OPEN | 5 comments*  
   `access_token` says `plan_type=prolite` but API returns `X-Codex-Plan-Type=plus`. Tier mismatch may cause unexpected quota depletion.

9. **[#29281](https://github.com/openai/codex/issues/29281) — Windows 11: sustained fan noise + GPU/CPU activity while idle**  
   *Status: OPEN | 3 comments | 2 👍*  
   After updating to 26.616.41845, Codex Desktop causes persistent fan noise. Regression likely related to background renderer or crash reporting.

10. **[#29532](https://github.com/openai/codex/issues/29532) — macOS: Persistent SQLite TRACE log churn remains after v0.142.0**  
    *Status: OPEN | 2 comments*  
    Even after the 85% reduction (#29432, #29457), `logs_2.sqlite` continues growing. Community notes the fix is partial; traces from `codex_api::endpoint::responses_websocket` are reduced, but other targets persist.

---

## Key PR Progress

1. **[#29528](https://github.com/openai/codex/pull/29528) — Centralize Codex Apps client handling**  
   Consolidates apps-specific logic (cache helpers, startup, tool conversion) into one location instead of scattering checks across layers. Clean architectural improvement.

2. **[#24092](https://github.com/openai/codex/pull/24092) — Reject unlowered PowerShell AST regions**  
   Security fix: the PowerShell safe-command classifier could be bypassed by code that avoids lowering `EndBlock.Statements`. Prevents execution of unsafe commands on Windows.

3. **[#29526](https://github.com/openai/codex/pull/29526) — core: resolve `view_image` paths in selected environment**  
   Fixes a bug where `view_image` resolved tool paths as host-native, making relative or target-native absolute paths unreliable in foreign execution environments.

4. **[#29527](https://github.com/openai/codex/pull/29527) — core: keep compaction world state aligned with context**  
   Follow-up to #29249. Prevents mid-turn compaction from rendering context from one snapshot while building `WorldState` from another, avoiding environment mismatch bugs.

5. **[#29155](https://github.com/openai/codex/pull/29155) — Expose service tier and reasoning effort in OTEL**  
   Adds `service_tier` and `model_reasoning_effort` to `response.completed` OTEL events. Requested by NVIDIA for measuring Fast mode usage and reasoning effort from CLI logs.

6. **[#29472](https://github.com/openai/codex/pull/29472) — app-server: preserve legacy cwd strings in exec events**  
   Reverts overeager `PathUri` conversion for command lifecycle event cwds. Includes deserialization tests for backwards compatibility with events already on disk.

7. **[#29158](https://github.com/openai/codex/pull/29158) — path-uri: remove legacy path deserialization**  
   Cleans up `PathUri` by removing legacy string deserialization support; replaced by `LegacyAppPathString` for explicit backcompat conversions.

8. **[#29521](https://github.com/openai/codex/pull/29521) — core: reset context for token budget compaction**  
   When token-budget feature is enabled, compaction now behaves like `new_context` tool: fresh window with normal injected context, no prior transcript carried forward. Keeps budget accounting clean.

9. **[#28598](https://github.com/openai/codex/pull/28598) — bazel: right-size Rust test targets**  
   Fixes Bazel's verbose timeout warnings by defaulting Rust tests to `small` size, adding per-target size/shard overrides. Reduces noise in CI.

10. **[#29520](https://github.com/openai/codex/pull/29520) — Scope token-budget accounting to body-after-prefix window**  
    Charges the configured body budget only against growth after the carried harness prefix, while still respecting full model context window as a safety cap.

---

## Feature Request Trends

- **Rate-limit transparency and control**: The dominant community ask. Users want real-time per-token cost visibility, breakdowns of why quotas drain, and the ability to switch between Fast/Deep modes to preserve budget. The `/usage` credit redemption feature in v0.142.0 is a step forward, but many feel it doesn't address the core accounting regression.

- **Plugin and MCP ecosystem improvements**: Strong demand for better plugin discovery (sections in `/plugins` help), local stdio MCP server reliability (especially cross-platform), and Cloudflare affinity support for hosted plugin traffic (#29516). Users want plugin sharing to work seamlessly across desktop and CLI.

- **Cross-platform consistency**: Windows users repeatedly request parity with macOS—sandbox setup, computer-use features, and performance (fan noise, GPU/CPU spikes). The PowerShell AST security fix (#24092) is welcome but Windows-specific regressions continue to erode trust.

- **Resource efficiency**: Ongoing requests to tame disk I/O, SQLite log growth, and crashpad dump accumulation. The partial fix for SQLite logs (#28224) is acknowledged, but users note similar patterns persist (#29532). Real-time monitoring of background processes is desired.

---

## Developer Pain Points

- **Unexplained cost spikes**: The #1 complaint. Developers who rely on Codex for daily workflows cannot predict or control their 5-hour budget consumption. The lack of an official explanation for the June 16 regression (Issue #28879, #28823) is causing users to pause upgrades or switch plans.

- **Sandbox and Windows fragility**: Native sandbox setup consistently fails on Windows (#28982, #29418). MCP desktop app regressions (#28978) break workflows immediately after auto-updates. These create a perception that Windows is a second-class platform.

- **Persistent resource leaks**: Crashpad dump growth (+5GB/day), SQLite log churn despite fixes, and idle GPU/CPU activity on Windows suggest systemic background processes that users cannot control or audit.

- **Plan-tier mismatches**: Multiple Pro subscribers are being treated as Plus at the API level (#29243, #28504). This erodes trust in billing infrastructure and makes debugging quota issues harder.

- **Incomplete fixes**: The SQLite log reduction is celebrated, but Issue #29532 demonstrates that the underlying logging architecture still generates persistent churn. Developers want root-cause resolution, not band-aids.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*