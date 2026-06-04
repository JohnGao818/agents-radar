# AI CLI Tools Community Digest 2026-06-04

> Generated: 2026-06-04 03:31 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developers Ecosystem  
**Date**: 2026-06-04 | **Sources**: Claude Code & OpenAI Codex Community Digests

---

## 1. Ecosystem Overview

The AI CLI tools landscape is dominated by two major players—Claude Code (Anthropic) and OpenAI Codex—each serving overlapping but distinct developer audiences. Both ecosystems are actively shipping releases and handling high-volume community feedback, with reliability, billing transparency, and session management emerging as top cross-cutting concerns. While Claude Code focuses on deep agent orchestration and VS Code integration, Codex leans into enterprise features (managed policies, sandbox security, TUI polish). The community energy is high on both sides, but the nature of complaints differs: Claude users report silent data loss and agent quality regressions, while Codex users are most frustrated by token burn rates and authentication friction.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Hot issues highlighted today** | 10 | 10 |
| **Top issue engagement** | 173 comments (billing bug) | 597 comments (token burn) |
| **PRs updated in last 24h** | 4 (2 open, 2 closed) | 10 (all open, plus related stack) |
| **Release today** | v2.1.162 (patch) | rust‑v0.137.0 + alpha pre‑release |
| **Feature request with most 👍** | 116 👍 (session continuation) | 133 👍 (Windows installer) |
| **Unique pain points listed** | ~12 distinct categories | ~8 distinct categories |

*Note: Issue/PR counts are those specifically featured in each digest; total repository volumes are larger.*

---

## 3. Shared Feature Directions

Several requirements appear across both tool communities, indicating industry-wide developer needs:

- **Session & resource limits** – Both communities demand graceful continuation after hitting token/session limits.  
  *Claude: #13354 (116👍), Codex: #14593 (597 comments)*
- **Windows platform parity** – Both face Windows-specific issues. Claude users report installation bugs and path-casing duplicates; Codex users demand a standalone `.exe` installer.  
  *Claude: #59883, #65237; Codex: #13993*
- **Data retention transparency** – Silent loss of session history bothers users on both sides.  
  *Claude: #59248 (transcript deletion), Codex: #23979 (conversation history missing)*
- **Cost predictability** – Unexpected token consumption spikes erode trust.  
  *Claude: #41617 (2-3x token usage), Codex: #14593 (token burn)*
- **Agent reliability** – Tasks marked complete without verification (Claude #60177) and stalled reasoning turns (Codex #24260) signal quality regression concerns.
- **Authentication friction** – Phone/account lockouts and billing bugs affect both.  
  *Claude: #5088 (account disabled after payment), Codex: #25837, #25820 (phone verification)*

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|-----------|-------------|--------------|
| **Primary user** | Agent-heavy developers, CI/CD integrators | Enterprise teams, sandboxed workflows |
| **Top feature emphasis** | Agent state visibility, plugins (Socratic mentor), VS Code extension | TUI keyboard enhancements, managed MITM CA, prompt hooks |
| **Hot UI focus** | LaTeX rendering in VS Code, notification system | Windows-native installer, semi-transparent sidebar fix, searchable menus |
| **Unique pain points** | Parallel tool call cascading failures, remote reconnect drops, false disk full on macOS | Spawn refresh failures on ARM64 Windows, phone number change block |
| **Enterprise alignment** | Max plan billing issues, credential-guard plugin | Credit limit visibility, admin-managed config bundles, EDU workspaces |
| **Plugin/extensibility** | Plugins as hooks (PreToolUse); collab and credential-guard already merged | Prompt hooks system in early PRs; plugin persistence lost on restart |
| **Architecture** | Native builds with embedded search; remote control for mobile | Native Rust TUI + sandbox; MITM CA trust management |

Claude Code currently emphasizes **agent observability** (new `waitingFor` field, structured orchestration requests) and **developer productivity** (VS Code integration), while Codex invests in **enterprise security** (CA bundles, background terminal APIs) and **TUI polish** (keybindings, compact status items). The communities reflect these priorities: Claude’s feature requests lean toward scientific/math support and agent design patterns; Codex’s toward cross-platform portability and authentication flow fixes.

---

## 5. Community Momentum & Maturity

- **OpenAI Codex** has the highest single-issue engagement (597 comments on #14593), suggesting a vocal, persistent user base. The number of open PRs (10 featured) and multiple interlocking changes (MITM CA stack) indicate **rapid engineering iteration**, but the burning token-bug remains unresolved. The community is active but frustrated with long-standing authentication and platform issues.

- **Claude Code** shows a broader spread of pain points (12 categories vs 8) and more feature requests with high upvotes (session continuation 116👍, LaTeX 93👍). The release cadence (v2.1.162 today) is steady. The PR list is smaller but includes a merged plugin and a diagnostic script for a recurring bug. The community appears **mature and feature-hungry**, with clear demands for agent reliability and data control.

Both tools are **actively maintained** and **shipping weekly**. Codex may be iterating faster on infrastructure (PR stack density), while Claude Code is moving on user-facing features and bug fixes with slightly lower PR volume.

---

## 6. Trend Signals

For technical decision-makers and developers, these community signals suggest where the industry is heading:

1. **Token usage transparency is mandatory** – Both communities penalize opaque cost increases. AI CLI tools must expose per-session token breakdowns and allow users to set budgets or pause on limit.
2. **Session continuity is non-negotiable** – Hard stops after limits are unacceptable. Graceful continuation (with cost warnings) will be table stakes.
3. **Data retention policies need opt-in** – Silent deletion of transcripts erodes trust. Tools should provide retention controls, backup options, and clear notifications.
4. **Platform-specific bugs are a competitive edge** – Windows, macOS ARM, and mobile support are becoming differentiators. Neglecting any platform risks user churn.
5. **Agent testing quality must improve** – Users report tasks marked complete without verification. Integrated testing frameworks (CI hooks, self-check assertions) will become a differentiator.
6. **Extensibility is maturing** – Both tools are investing in plugin/hook systems (credential scanning, Socratic mentoring, prompt hooks). Expect more third-party plugin ecosystems to emerge.
7. **Parallel execution reliability** – Cascading failures in parallel tool calls (Claude #22264) and sandbox spawn failures (Codex #24259) point to a need for **robust retry and isolation** mechanisms in AI agent loops.

*These trends mirror broader industry shifts toward cost-aware, reliable, and transparent AI tooling.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-06-04 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following Pull Requests commanded the most community attention (by comment activity and engagement). All remain **open** and under active development.

| # | Skill | Description | Discussion Highlights | Status |
|---|-------|------------|----------------------|--------|
| 514 | **document–typography** | Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. | Addresses a universal pain point – every Claude-generated document suffers from these issues. High practical value for professional output. | Open |
| 486 | **ODT (OpenDocument)** | Enables creation, filling, reading, and conversion of `.odt`/`.ods` files with template support. | Bridges a major gap – LibreOffice/OpenOffice users now have native skill support. Discussion focused on scope creep and security of file parsing. | Open |
| 210 | **frontend‑design (improvement)** | Revises the existing frontend-design skill to be more actionable and coherent within a single conversation. | Community feedback demanded more concrete, step-by-step instructions. The PR aims to make the skill steer Claude’s behavior without vagueness. | Open |
| 83 | **skill‑quality‑analyzer & skill‑security‑analyzer** | Two meta‑skills: one evaluates skill structure/docs, the other audits security (prompt injection, secret exposure). | First‑of‑kind meta‑skills; stirs debate on whether quality/security checks should be part of the core tooling rather than a skill. | Open |
| 1140 | **agent‑creator** | Meta‑skill that generates task-specific agent sets; also fixes multi‑tool evaluation and adds Windows support. | Addresses fundamental issue #1120 about agent composition. Gain traction as a “skill for making skills” – high potential for ecosystem growth. | Open |
| 723 | **testing‑patterns** | Comprehensive skill covering testing trophy model, unit tests, React Testing Library, integration, and E2E. | One of the most requested skill categories. Discussion centers on balancing breadth vs. depth and avoiding duplication with existing skills. | Open |
| 568 | **ServiceNow** | Broad platform assistant covering ITSM, ITOM, SecOps, ITAM, CSDM, IntegrationHub and more. | Marks enterprise appetite – ServiceNow is a major platform. Questions about maintainability and whether it should be split into sub‑skills. | Open |
| 154 | **shodh‑memory** | Persistent memory system for AI agents, maintaining context across conversations via `proactive_context` calls. | High interest in agent memory solutions. Concerns about performance and interference with Claude's native context window. | Open |

> **Note:** Several high‑comment PRs focused on bug fixes and tooling (e.g., #538, #539, #541 – case‑sensitivity and ID collision fixes; #1099, #1050 – Windows subprocess fixes). These are not new skills but critical for ecosystem stability.

---

## 2. Community Demand Trends (from Issues)

**Top 5 most‑commented Issues reveal where the community wants the Skills ecosystem to grow:**

| Issue | Demand Area | Comments | 👍 |
|-------|-------------|----------|----|
| #228 – Org‑wide skill sharing | **Enterprise sharing & governance** – users want a shared skill library or direct sharing links instead of manual file transfer. | 13 | 7 |
| #556 – `run_eval.py` never triggers skills | **Tooling reliability** – the evaluation script is broken for many users (0% trigger rate), blocking skill optimization. | 9 | 6 |
| #492 – Namespace trust boundary abuse | **Security & trust** – community skills under `anthropic/` namespace impersonate official ones; need better provenance. | 7 | 2 |
| #189 – Duplicate skills from plugins | **Installation hygiene** – `document‑skills` and `example‑skills` plugins install identical content; need deduplication. | 6 | 8 |
| #202 – skill‑creator best practices | **Skill‑creator quality** – the meta‑skill reads like docs, not an operational instruction; needs rewrite for token efficiency. | 8 | 1 |

**Emerging themes from lower‑comment issues:**
- **Windows compatibility** – multiple PRs and issues (#1099, #1050, #556) report subprocess crashes, encoding bugs, and `claude.cmd` handling.
- **Multi‑file skill references** – #1220 requests inline bundling of reference files to avoid context window fragmentation.
- **Agent governance** – #412 proposes a safety pattern skill for AI agent systems (policy enforcement, threat detection, audit trails).

**Overall trend:** The community is shifting from “create any skill” to “create reliable, shareable, and secure skills for enterprise use.”

---

## 3. High‑Potential Pending Skills (Active‑Comment PRs Likely to Land Soon)

These open PRs have sustained recent activity and address clear community needs:

- **#1140 – agent‑creator** (updated 2026-06-02) – Directly solves the meta‑skill gap; includes critical bug fixes for evaluation and Windows.
- **#363 – feature‑dev workflow fix** (updated 2026-06-03) – Repairs `TodoWrite` overwriting that skips quality review phases – a subtle but impactful workflow bug.
- **#486 – ODT skill** (updated 2026-04-14) – High demand from LibreOffice/ODF communities; discussion is converging on scope.
- **#568 – ServiceNow skill** (updated 2026-04-23) – Enterprise users are actively testing; refinements expected.
- **#723 – testing‑patterns skill** (updated 2026-04-21) – Strong initial framework; community feedback on what testing libraries to prioritize.
- **#190 – n8n‑builder & n8n‑debugger** (updated 2026-05-18) – Adds two automation/nocode skills; active discussion on `faf‑expert` scope.
- **#154 – shodh‑memory** (updated 2026-03-03) – Long‑running PR with persistent interest; author recently added performance benchmarks.

---

## 4. Skills Ecosystem Insight

> **The community’s most concentrated demand is for skills that turn Claude from a general assistant into a reliable, enterprise‑ready document, workflow, and agent platform** – with parallel urgency for the tooling (evaluation, security, sharing) needed to sustain that growth at scale.

---

*All links: `https://github.com/anthropics/skills/pull/{number}` for PRs, `https://github.com/anthropics/skills/issues/{number}` for issues.*

---

# Claude Code Community Digest — 2026-06-04

## Today’s Highlights

A new patch release v2.1.162 ships with improved agent state visibility and dedicated search tools for native builds. Community attention remains focused on a high-profile billing issue where the Claude Code Max plan payment disabled accounts (#5088), and a long-running feature request to allow session continuation after hitting limits (#13354). Remote control reliability and silent data loss from transcript retention cleanup are also top community concerns today.

## Releases

**v2.1.162** (latest, ~24h old)
- `claude agents --json` now includes a `waitingFor` field that shows what a waiting session is blocked on (e.g. a permission prompt) — improves observability for headless/CI workflows.
- `--tools` now correctly provides dedicated Grep/Glob search tools on native builds with embedded search; previously these names were silently ignored.

[Release link](https://github.com/anthropics/claude-code/releases/tag/v2.1.162)

## Hot Issues (10 selected)

| Issue | Title | Comments | 👍 | Why it matters |
|-------|-------|----------|----|----------------|
| [#5088](https://github.com/anthropics/claude-code/issues/5088) | Account Disabled After Payment for Claude Code Max 5x Plan | 173 | 58 | Critical billing bug: payment immediately disables access. High visibility, likely Anthropic on-call priority. |
| [#13354](https://github.com/anthropics/claude-code/issues/13354) | [FEATURE] Continue when the session limit reached | 56 | 116 | Top-voted feature request: users want to keep working after hitting limits rather than hard-stopping. |
| [#34255](https://github.com/anthropics/claude-code/issues/34255) | Remote Control: automatic reconnection doesn't work | 48 | 86 | Connection drops silently with no recovery on macOS/iOS – breaks remote workflows. |
| [#16446](https://github.com/anthropics/claude-code/issues/16446) | [FEATURE] LaTeX rendering in VS Code plugin | 33 | 93 | Strong demand for scientific/math support in the popular VS Code extension. |
| [#22264](https://github.com/anthropics/claude-code/issues/22264) | Sibling tool call errored: parallel calls cascade-fail | 33 | 61 | If one parallel tool call fails, all siblings are cancelled; forces wasteful retries. |
| [#41617](https://github.com/anthropics/claude-code/issues/41617) | Excessive token consumption after recent updates (Max plan) | 18 | 19 | Users on Max plans report 2-3x token usage for the same tasks – cost concerns. |
| [#59248](https://github.com/anthropics/claude-code/issues/59248) | Silent retention cleanup deletes session transcripts | 12 | 4 | No opt-in, warning, or recovery; users lose full conversation histories. Linked to [#62476](https://github.com/anthropics/claude-code/issues/62476). |
| [#63396](https://github.com/anthropics/claude-code/issues/63396) | CLI builds invalid request after context ops → 400 Error | 7 | 4 | Context compaction, `/clear`, or model switch can render a session permanently wedged. |
| [#60177](https://github.com/anthropics/claude-code/issues/60177) | Claude marks tasks done without testing (Opus 4.x) | 7 | 1 | Patterns of premature completion – 12 days, 51 commits still broken. Quality regression. |
| [#65237](https://github.com/anthropics/claude-code/issues/65237) | Project picker shows duplicate Recent rows due to path-casing | 3 | 0 | New UI bug on case-insensitive APFS – duplicates clutter the project picker. |

## Key PR Progress (all 4 updated in last 24h)

| PR | Title | Status | Summary |
|----|-------|--------|---------|
| [#65223](https://github.com/anthropics/claude-code/pull/65223) | Spelling: Fix typo in security guidance plugin | **Closed** | Corrects "reqwest" → "request" in a plugin text. Small but clean. |
| [#61691](https://github.com/anthropics/claude-code/pull/61691) | Add diagnostic script for GitHub connector showing 'Connected' but no tools | Open | PowerShell script to diagnose and repair a recurring Windows Cowork bug (related to [#61682](https://github.com/anthropics/claude-code/issues/61682)). |
| [#62099](https://github.com/anthropics/claude-code/pull/62099) | Add credential-guard plugin for hardcoded secret detection | Open | PreToolUse hook scans Write/Edit/Bash for 20+ credential patterns before content is written. Addresses [#62095](https://github.com/anthropics/claude-code/issues/62095). |
| [#22919](https://github.com/anthropics/claude-code/pull/22919) | feat(plugins): add collab plugin for Socratic mentoring mode | **Closed** | Transforms Claude into a mentor asking guiding questions instead of writing code. Already merged. |

## Feature Request Trends

The most-requested feature directions from recent issues:

1. **Session limit continuation** ([#13354](https://github.com/anthropics/claude-code/issues/13354), 116 👍) — Allow a seamless way to continue working past token/session limits rather than hard-stopping.
2. **LaTeX rendering in VS Code** ([#16446](https://github.com/anthropics/claude-code/issues/16446), 93 👍) — Critical for academic, scientific, and math-heavy workflows.
3. **Structured orchestration as a first-class agent behaviour** ([#64767](https://github.com/anthropics/claude-code/issues/64767)) — Users want predefined orchestration patterns (DAG, pipeline, parallel-map) rather than letting agents self-organise.
4. **Notification system for VS Code** ([#65242](https://github.com/anthropics/claude-code/issues/65242)) — Toast/sound signals for limit resets, task completions, or session events when the editor is in the background.
5. **Agent design guidance in documentation** ([#42873](https://github.com/anthropics/claude-code/issues/42873)) — More structured docs around agent design patterns for the bundled `/claude-api` skill.

## Developer Pain Points

Recurring frustrations visible across the issue tracker:

- **Silent data loss** — Session transcripts deleted after 30 days with no opt-in or warning ([#59248](https://github.com/anthropics/claude-code/issues/59248), [#62476](https://github.com/anthropics/claude-code/issues/62476)). Context compaction can also wedge sessions permanently ([#63396](https://github.com/anthropics/claude-code/issues/63396)).
- **Billing & cost unpredictability** — Account disabled after payment ([#5088](https://github.com/anthropics/claude-code/issues/5088)), excessive token consumption after updates ([#41617](https://github.com/anthropics/claude-code/issues/41617)), and session limits burning through all tokens twice in one day ([#65249](https://github.com/anthropics/claude-code/issues/65249)).
- **Remote control reliability** — Automatic reconnection does not work; connection drops silently ([#34255](https://github.com/anthropics/claude-code/issues/34255)), and mobile-to-desktop messaging is read-only in practice ([#62284](https://github.com/anthropics/claude-code/issues/62284)).
- **Parallel tool call fragility** — One failing sibling cancels all parallel calls, forcing wasteful retries ([#22264](https://github.com/anthropics/claude-code/issues/22264)).
- **Context limit UX failure** — No progressive warnings, misleading error messages, cascade failure in compaction ([#64850](https://github.com/anthropics/claude-code/issues/64850)).
- **Agent quality regressions** — Claude marks tasks done without testing ([#60177](https://github.com/anthropics/claude-code/issues/60177)), ignores instructions ([#57200](https://github.com/anthropics/claude-code/issues/57200)), and background subagents die on transient rate limits instead of retrying ([#65222](https://github.com/anthropics/claude-code/issues/65222)).
- **Platform-specific issues** — Windows Store installation breaks `/desktop` command ([#59883](https://github.com/anthropics/claude-code/issues/59883)), false "disk full" errors on macOS ([#65251](https://github.com/anthropics/claude-code/issues/65251)), and Vietnamese character input unsupported in terminal ([#65250](https://github.com/anthropics/claude-code/issues/65250)).
- **Performance degradation** — Recent builds (v2.1.161) showing 10-30x slower execution for UI tasks ([#65236](https://github.com/anthropics/claude-code/issues/65236)).

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-04

## Today’s Highlights
Two releases landed (rust‑v0.137.0 and a companion alpha), bringing TUI keyboard enhancements and enterprise credit‑limit visibility. Community outcry remains loudest around a long‑standing token‑burning bug (#14593) that has accumulated nearly 600 comments. On the engineering side, a major stack of PRs is laying groundwork for managed MITM CA bundles, and a new prompt‑hooks system is taking shape across several interlocking changes.

## Releases
- **rust‑v0.137.0** – Adds F13–F24 keybindings, paste support in searchable menus, and a compact reasoning‑only status/title item in the TUI. Enterprise and admin flows now display monthly credit limits and can apply cloud‑managed config bundles, including support for EDU workspaces.  
- **rust‑v0.137.0‑alpha.5** – Tagged as a pre‑release; no detailed changelog provided.

## Hot Issues (Top 10 by community attention)
1. **[Burning tokens very fast](https://github.com/openai/codex/issues/14593)** – #14593 (597 comments, 262 👍). A long‑running rate‑limit bug that continues to frustrate Business users on Windows. Community thread shows no clear resolution yet.
2. **[Standalone Windows installer (`codex‑setup.exe`)](https://github.com/openai/codex/issues/13993)** – #13993 (61 comments, 133 👍). High demand from users blocked by Microsoft Store policies, corporate restrictions, or offline environments.
3. **[Disable automatic conversion of long pasted prompts into .txt attachments](https://github.com/openai/codex/issues/25144)** – #25144 (49 comments, 56 👍). Users want control over how Codex handles lengthy pastes; automatic conversion breaks structured input.
4. **[Silent hiding of project conversations outside the global recent‑50 window](https://github.com/openai/codex/issues/21128)** – #21128 (19 comments, 16 👍). A design flaw that makes the Desktop app unreliable as a working memory for real projects.
5. **[gpt‑5.5 xhigh turn stalled 30 minutes before first output](https://github.com/openai/codex/issues/24260)** – #24260 (16 comments, 9 👍). Disconcerting “Thinking” state with no progress indicator for half an hour.
6. **[Conversation history missing after update](https://github.com/openai/codex/issues/23979)** – #23979 (15 comments, 3 👍). Data still exists in SQLite but UI loses access; users on macOS affected by 26.519.22136.
7. **[Windows sandbox intermittently fails with `spawn setup refresh`](https://github.com/openai/codex/issues/24259)** – #24259 (12 comments, 9 👍). ARM64 Windows 11 users hit a non‑deterministic sandbox launch failure despite healthy diagnostics.
8. **[Semi‑transparent sidebar causes transparent/undrawn regions on Windows](https://github.com/openai/codex/issues/25249)** – #25249 (12 comments, 0 👍). Maximized window rendering bug; cosmetic but visually severe.
9. **[Cannot change phone number for login](https://github.com/openai/codex/issues/25837)** – #25837 (11 comments). Users moving countries are locked out of paid accounts; no UI to update the SMS phone number.
10. **[CLI login blocked by phone verification rate limit — Pro subscriber](https://github.com/openai/codex/issues/25820)** – #25820 (5 comments). Another authentication pain point; affects CLI users who cannot reach the phone verification endpoint.

## Key PR Progress (Top 10 by engineering significance)
1. **[Sign macOS release artifacts with Azure Key Vault](https://github.com/openai/codex/pull/26252)** – Moves Developer ID keys behind OIDC/Key Vault, improving security without breaking the notarisation pipeline.
2. **[Load platform MITM CA roots](https://github.com/openai/codex/pull/26285)** + **[Materialize child MITM CA bundles](https://github.com/openai/codex/pull/26286)** + **[Prepare managed child MITM CA env](https://github.com/openai/codex/pull/25888)** – Three‑PR stack to give sandboxed processes correct CA trust without inherited overrides, a critical security and networking fix.
3. **[Add app‑server background terminal process APIs](https://github.com/openai/codex/pull/26041)** – Experimental v2 endpoints so Codex Apps can correctly list/terminate terminals associated with a thread, replacing fragile process‑tree heuristics.
4. **[Gate terminal visualization instructions in TUI](https://github.com/openai/codex/pull/26013)** – New `TerminalVisualizationInstructions` feature flag (default off) to keep TUI instructions from confusing users until ready.
5. **[Propagate auth session logging ID in ChatGPT login](https://github.com/openai/codex/pull/26276)** – Adds a correlation key so login failures can be traced back to auth service without fuzzy matching.
6. **[Optimize external agent session detection](https://github.com/openai/codex/pull/26291)** – Internal performance improvement for agent session lifecycle.
7. **[Add prompt hooks](https://github.com/openai/codex/pull/24634)** + **[Expose prompt hooks to clients](https://github.com/openai/codex/pull/26268)** – Core infrastructure for user‑definable prompt handlers that run as side requests without interfering with main conversation state.
8. **[Add metadata‑only thread catalog subscriptions](https://github.com/openai/codex/pull/26009)** – Lets sidebar clients keep a small, up‑to‑date thread list without resuming every thread, reducing overhead.
9. **[Load plugin hooks without other plugin capabilities](https://github.com/openai/codex/pull/26272)** – Cuts `hooks/list` latency by ~100 ms by skipping unnecessary plugin skill/MCP loading.
10. **[Allow disabling session store and load in code mode](https://github.com/openai/codex/pull/26284)** – Gives code‑mode consumers control over session persistence, useful for stateless or ephemeral workflows.

## Feature Request Trends
- **Windows‑native installer** (#13993) – Strong push for a standalone `.exe` to bypass Microsoft Store and corporate policy barriers.
- **User control over automatic transformations** (#25144) – Requests to disable automatic paste‑to‑file conversion, suggesting a desire for more predictable input handling.
- **Multi‑account OAuth rotation** (#9648) – Power users want to manage multiple ChatGPT accounts and automatically fail‑over when one hits rate limits.
- **Clipboard & text‑handling improvements** (#12200 clean copy for multiline, #2379 undo/redo typing, #25465 headless clipboard reader) – Developers need better support for copying structured output and working in environments without a GUI.

## Developer Pain Points
- **Rate‑limiting / token burn** (#14593) remains the single most commented issue, with Business users feeling their credits disappear too quickly.
- **Phone‑based authentication** (#25837, #25828, #25820) is a recurring blocker, especially for CLI users and those who have changed countries.
- **Windows sandbox instability** (#24259, #22428, #25366, #26158) – A cluster of failures with `spawn setup refresh` and `os error 740` plagues Windows 11 users, forcing many to roll back CLI versions.
- **Conversation history issues** (#21128, #23979) – Silent loss or hiding of older chats undermines trust in the Desktop app as a persistent workspace.
- **Plugin persistence & configuration** (#26296, #25758, #25813) – Computer Use and Browser plugins are repeatedly removed on restart or overwritten by the app, requiring manual reinstallation.
- **Stalled reasoning turns** (#24260) – Long “Thinking” pauses with no feedback erode user confidence in model responsiveness.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*