# AI CLI Tools Community Digest 2026-06-19

> Generated: 2026-06-19 03:55 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date:** 2026-06-19

## 1. Ecosystem Overview

The AI CLI tools landscape is maturing rapidly, with both Claude Code and OpenAI Codex shipping frequent releases while grappling with scaling pains. User communities are converging around shared demands for cost transparency, sandbox stability, and IDE-agnostic support, even as each tool pursues distinct technical architectures. Platform-specific regressions—particularly on Windows and macOS—remain the most common source of friction, while MCP (Model Context Protocol) integration has emerged as a critical reliability frontier. Overall, the ecosystem is shifting from raw capability demonstration to production-grade reliability, multi-user workflow support, and enterprise cost governance.

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Hot issues tracked** | 10 | 10 |
| **Total comments (hot issues)** | ~227 | ~297 |
| **👍 on hot issues** | ~278 | ~210 |
| **PRs in progress / merged** | 4 (1 merged, 1 closed) | 10 (0 merged, all open/active) |
| **New release today** | v2.1.183 | rust-v0.141.0 + 3 alpha builds |
| **Active regression reports** | Multiple (config, API, MCP) | Multiple (permission loops, WAL bloat) |
| **Longest-running unresolved issue** | #26302 – 4 months (UI lag) | #25719 – weeks (CPU runaway) |

**Assessment:** Both projects maintain high release cadences. Codex shows more concurrent PR activity (10 vs 4), while Claude Code has higher total upvote weight on its top issues, indicating broad community pain. Codex resolved the long-standing #20161 phone-verification bug today; Claude Code fixed its lock workflow after 53 consecutive failures.

## 3. Shared Feature Directions

The following requirements appear across both tool communities, suggesting industry-wide developer expectations:

- **Cost control & transparency:** Both communities demand granular usage analytics (Claude Code: #38350 session inflation, #20944 context opt-out; Codex: #28879 rate-limit spikes, #28997 disk bloat). Users are increasingly sensitive to opaque billing.
- **Sandbox & permission reliability:** Frequent permission loops (Codex #28988), destructive command blocking (Claude Code 2.1.183), and sandbox ACL corruption (Codex #15777) signal that secure execution environments remain brittle.
- **IDE-agnostic support:** JetBrains plugin demand (Claude Code #47166) and WSL failures (Codex #16815) show users want toolchain flexibility beyond VSCode and standard terminals.
- **MCP stability:** Both tools face MCP tool-call hangs (Claude Code #69487, Codex #28978) and authentication issues (Claude Code #69324), indicating the protocol needs client-side timeouts and better error handling.
- **Configuration persistence:** Regressions in /config dialogs (Claude Code #69466) and global vs project-scoped settings (Codex #14601) highlight the need for more robust, isolated configuration.

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|-----------|-------------|--------------|
| **Primary focus** | Safe auto-mode, team management, terminal UX | Remote executors, encryption, cross-platform sandbox |
| **Target user** | Individual developers and small teams (vocal about cost) | Enterprise and power users (Pro Max, Plus plans) |
| **Technical approach** | CLI-first with VSCode integration; Git safety gating | Rust-based with relay channels, MITM proxy, indexed search |
| **Release cadence** | Frequent patch releases; fewer open PRs | Alpha/beta gateways; high PR throughput |
| **Community size** | Larger engagement (higher 👍 counts, 62 comments top issue) | Higher comment count (200+ on #20161) but narrower base |
| **Pain point distribution** | macOS TUI regressions, cost inflation, MCP hangs | Windows instability, macOS CPU runaway, billing unpredictability |
| **Unique differentiators** | Team management tools (team create/delete), JetBrains demand | Noise relay encryption, indexed web search, cross-platform executors |

## 5. Community Momentum & Maturity

- **Claude Code** shows a more vocal, higher-engagement user base with cost concerns dominating. The tool appears to have wider adoption among individual developers, as evidenced by the 62-comment session usage issue. Its slower PR throughput (4 PRs vs 10) suggests a more conservative, safety-focused development cycle. The JetBrains plugin demand and team-management regression indicate growing enterprise interest.
- **OpenAI Codex** demonstrates faster iteration (3 alpha releases today) and deeper engineering investments (10 open PRs covering encryption, search, and sandbox hardening). However, its community is more concentrated on platform-specific bugs (Windows, macOS) and billing shocks. The closure of #20161 after 200+ comments signals improved maturity in authentication flows.
- **Overall maturity:** Both tools are past the hype phase and into production scaling. Codex's cross-platform executor support and encrypted relays suggest a more infrastructure-oriented roadmap; Claude Code's Git safety and team tools point toward workflow governance.

## 6. Trend Signals for Developers

1. **Safety as a feature, not an afterthought.** Claude Code's blocking of destructive Git commands in auto-mode (v2.1.183) sets a new baseline for responsible agent behavior. Expect other tools to follow with guardrails.
2. **MCP protocol standardization is urgent.** Across both tools, unstable MCP integrations undermine trust. Developers should monitor for client-side timeout defaults and better error propagation.
3. **Cost observability is the top adoption blocker.** With Codex Plus plans draining budgets in 2–3 prompts and Claude Code sessions inflating without warning, tools that provide real-time token accounting and session caching controls will win enterprise trust.
4. **Windows remains the weakest link.** Six distinct Windows-specific issues in Codex (WSL, Git refs, sandbox ACL, UI flickering, AV false positives, registry keys) and three in Claude Code (MSIX config, UI lag, rate limits) show that cross-platform parity is still a major engineering investment.
5. **Config isolation and portability are rising.</strong> Users want project-scoped trusted levels, provider base URLs, and `.config` files that travel with the repo. This mirrors the DevOps shift to infrastructure-as-code and environment reproducibility.
6. **Conversation management is an emerging requirement.** Requests for `/merge` commands, cross-project conversation moves, and session-name sync across devices (Claude Code) indicate that developers want to treat AI sessions like version-controlled artifacts—searchable, shareable, and portable.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data compiled from github.com/anthropics/skills — 2026-06-19 snapshot*

---

## 1. Top Skills Ranking

The following pull requests represent the most-discussed Skill submissions based on comment volume and community engagement. All remain **open** as of the snapshot date.

### #1 — Document Typography Skill
**PR #514** · [View on GitHub](https://github.com/anthropics/skills/pull/514)
- **Functionality:** Prevents orphan word wrap (1–6 words spilling to next line), widow paragraphs (section headers stranded at page bottom), and numbering misalignment in AI-generated documents. Addresses a universal pain point in every document Claude produces.
- **Discussion highlights:** The PR summary explicitly identifies these as problems "affecting every document Claude generates." Community interest is driven by the skill's broad applicability—any user producing long-form content benefits immediately.
- **Status:** Open (created 2026-03-04, last updated 2026-03-13). Author: @PGTBoos.

### #2 — ODT (OpenDocument) Skill
**PR #486** · [View on GitHub](https://github.com/anthropics/skills/pull/486)
- **Functionality:** Enables creation, template filling, and conversion of OpenDocument Format files (.odt, .ods). Triggered by mentions of "ODT," "ODS," "LibreOffice," or open-format document requests.
- **Discussion highlights:** Addresses a significant gap in document-format coverage. The ISO-standard format is widely used in government and European enterprise contexts, making this a highly requested compliance-oriented skill.
- **Status:** Open (created 2026-03-01, last updated 2026-04-14). Author: @GitHubNewbie0.

### #3 — Frontend-Design Skill Clarity Overhaul
**PR #210** · [View on GitHub](https://github.com/anthropics/skills/pull/210)
- **Functionality:** Revises the existing frontend-design skill to improve clarity, actionability, and internal coherence. Ensures every instruction is executable within a single conversation with specific behavioral guidance.
- **Discussion highlights:** The community is pushing for skills that are *operational* rather than *educational*. This PR exemplifies the shift: users want Claude to *do*, not *explain*. The skill-quality distinction (actionable vs. verbose) is a recurring theme across multiple PRs and issues.
- **Status:** Open (created 2026-01-05, last updated 2026-03-07). Author: @justinwetch.

### #4 — Skill Quality & Security Analyzers (Meta-Skills)
**PR #83** · [View on GitHub](https://github.com/anthropics/skills/pull/83)
- **Functionality:** Two meta-skills for evaluating and auditing other skills. The *skill-quality-analyzer* scores across five dimensions (structure, documentation, examples, resource usage, code quality). The *skill-security-analyzer* audits for prompt injection, data exfiltration risks, and unauthorized tool access.
- **Discussion highlights:** As the skills ecosystem grows, the community recognizes the need for quality assurance and security tooling. These meta-skills directly address concerns raised in Issue #492 about trust boundaries and namespace impersonation.
- **Status:** Open (created 2025-11-06, last updated 2026-01-07). Author: @eovidiu.

### #5 — SAP-RPT-1-OSS Predictive Analytics Skill
**PR #181** · [View on GitHub](https://github.com/anthropics/skills/pull/181)
- **Functionality:** Integrates SAP's open-source tabular foundation model (SAP-RPT-1-OSS, Apache 2.0 license) for predictive analytics on SAP business data. Targets the enterprise analytics workflow.
- **Discussion highlights:** This skill taps into the enterprise demand for Claude to interact with specialized ML models. The SAP ecosystem is a major enterprise touchpoint, and this PR signals community desire for industry-specific model orchestration skills.
- **Status:** Open (created 2025-12-28, last updated 2026-03-16). Author: @amitlals.

### #6 — Testing-Patterns Skill
**PR #723** · [View on GitHub](https://github.com/anthropics/skills/pull/723)
- **Functionality:** Covers the full testing stack: Testing Trophy philosophy, AAA pattern for unit tests, React Testing Library patterns, integration testing strategies, and E2E testing guidance. Explicitly documents what *not* to test.
- **Discussion highlights:** Testing is a perennial developer need. The skill's comprehensive scope (philosophy through implementation) and focus on anti-patterns received positive community attention.
- **Status:** Open (created 2026-03-22, last updated 2026-04-21). Author: @4444J99.

### #7 — ServiceNow Platform Skill
**PR #568** · [View on GitHub](https://github.com/anthropics/skills/pull/568)
- **Functionality:** Broad ServiceNow platform assistant covering ITSM, ITOM, ITAM/SAM Pro, FSM, HRSD, CSM, SPM, Vulnerability Response, Security Incident Response, CSDM, and IntegrationHub.
- **Discussion highlights:** One of the most ambitious enterprise skill submissions, spanning nearly the entire ServiceNow product suite. The breadth reflects community demand for platform-level rather than narrow scripting-focused skills.
- **Status:** Open (created 2026-03-08, last updated 2026-04-23). Author: @Vanka07.

### #8 — AURELION Cognitive Framework Suite (4 Skills)
**PR #444** · [View on GitHub](https://github.com/anthropics/skills/pull/444)
- **Functionality:** Four skills from the AURELION ecosystem: *kernel* (5-floor structured thinking templates), *advisor* (domain-adaptive reasoning), *agent* (autonomous task orchestration), and *memory* (persistent context management).
- **Discussion highlights:** Cognitive framework skills represent a growing category where users teach Claude structured reasoning patterns. The suite approach (multiple interdependent skills) sparked discussion about skill composition and dependency management.
- **Status:** Open (created 2026-02-21, last updated 2026-05-06). Author: @Chase-Key.

---

## 2. Community Demand Trends

Analysis of the most-discussed Issues reveals five high-demand direction areas:

### 📡 Organizational Skill Sharing & Distribution
**Issue #228** (14 comments, 7👍) — [View on GitHub](https://github.com/anthropics/skills/issues/228)
The top-voted issue overall. Users want org-wide skill libraries and direct sharing links. Current workflow (download .skill file → Slack → manual upload) is a barrier to enterprise adoption. Related: Issue #189 (6 comments) reports duplicate skills when installing both `document-skills` and `example-skills` plugins, indicating distribution management pain.

### 🔐 Security & Trust Boundary Management
**Issue #492** (7 comments, 2👍) — [View on GitHub](https://github.com/anthropics/skills/issues/492)
Community skills distributed under the `anthropic/` namespace create a trust-boundary vulnerability where users may grant elevated permissions to impersonating skills. This intersects with PR #83 (skill-security-analyzer) as a proposed solution. A security-first stance is emerging as a community priority.

### 🐛 Skill-Creator Tooling Reliability (Cross-Platform)
**Issues #556, #1169, #1061** — collectively 18+ comments
The `run_eval.py` evaluation loop returns 0% recall on every iteration (Issues #556, #1169), making the description-optimization loop unusable. Windows compatibility failures (Issue #1061) affect subprocess spawning, encoding, and pipe handling. **This is the single most-reported functional blocker** — multiple independent reproductions confirm the bug. Multiple PRs (#1298, #1099, #1050, #361, #362) attempt fixes, indicating this is the community's most active debugging effort.

### 🧠 Agent Governance & Safety Patterns
**Issue #412** (6 comments) — [View on GitHub](https://github.com/anthropics/skills/issues/412)
Proposal for an *agent-governance* skill teaching Claude policy enforcement, threat detection, trust scoring, and audit trails for AI agent systems. The community recognizes that as skills grow more autonomous, safety guardrails become essential. Related: Issue #1175 discusses security concerns with SharePoint Online document handling via skills.

### 🪟 Windows Compatibility
**Issues #1061, #1099, #1050** — 3+ related issues
Native Windows Python 3.14 encounters three distinct failures: missing `PATHEXT` handling, `cp1252` encoding mismatches, and `select` on pipes. The skill-creator toolchain is effectively Unix-only today, excluding a significant user base. Multiple PRs target this, making it one of the most actively addressed infrastructure gaps.

### 📘 Documentation & Onboarding
**Issue #452** (referenced in PR #509) — [View on GitHub](https://github.com/anthropics/skills/pull/509)
The repository scores 25% on GitHub's community health metrics. PR #509 adds `CONTRIBUTING.md` addressing this gap, covering skill anatomy, best practices, validation, and the submission checklist. The community signals that low documentation quality is a barrier to contribution.

---

## 3. High-Potential Pending Skills

These active PRs show sustained community engagement and are likely to merge soon based on discussion momentum and fix-criticality:

| PR | Skill | Author | Why It's Likely to Land |
|----|-------|--------|------------------------|
| **#1298** | fix(skill-creator): run_eval.py recall=0% + Windows fixes | @MartinCajiao | Directly addresses the #1 reported bug (Issues #556, #1169). Multiple reproductions, clear root cause, comprehensive fix (artifact installation, stream reading, trigger detection, parallel workers). |
| **#361** | Detect unquoted YAML special characters | @Mr-Neutr0n | Fixes silent YAML parsing failures in description fields. Intersects with #539 (duplicate effort). The bug causes truncated or misparsed skill descriptions. High priority for reliability. |
| **#362** | Fix skill-creator UTF-8 panic | @Mr-Neutr0n | Prevents Rust panics on multi-byte characters by switching to byte-length validation. A correctness fix that prevents silent failures. |
| **#723** | testing-patterns skill | @4444J99 | No blocking issues; comprehensive scope; directly useful to developers. Likely to merge as-is or with minor revisions. |
| **#538** | fix(pdf): case-sensitive file references | @Lubrsy706 | Fixes 8 case-sensitivity mismatches that break on case-sensitive filesystems. Simple, correct, unblocking for Linux/macOS users. |
| **#541** | fix(docx): tracked change ID collision | @Lubrsy706 | Prevents document corruption when tracked changes interact with existing bookmarks. A correctness fix with clear root cause (shared `w:id` namespace). |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is at the intersection of enterprise document workflows and skill-ecosystem reliability** — users are simultaneously pushing for production-grade document skills (typography, OpenDocument, ServiceNow) while struggling with fundamental tooling failures (YAML parsing bugs, 0% recall evaluation loops, Windows incompatibility) that undermine the skill development pipeline itself.

---

# Claude Code Community Digest — 2026-06-19

## Today’s Highlights

Version 2.1.183 rolls out critical safety improvements for auto mode, blocking destructive `git` commands unless explicitly requested. Meanwhile, the community is reporting fresh friction: a `/config` dialog regression in 2.1.181 that discards all changes, API rate-limit errors striking multiple platforms, and a lingering MCP tool-call hang without client‑side timeout. A long‑standing issue around inflated session usage (#38350) continues to gather attention, and the demand for JetBrains IDE support (#47166) remains vocal.

## Releases

**v2.1.183** — *just released*  
Improved auto‑mode safety:  
- Destructive `git` commands (`reset --hard`, `checkout -- .`, `clean -fd`, `stash drop`) are now blocked when you did not ask to discard local work.  
- `git commit --amend` is blocked when the commit was not made by the agent this session.  

[Full release](https://github.com/anthropics/claude-code/releases/tag/v2.1.183)

## Hot Issues (10 noteworthy)

1. **[#38350 – Abnormal / inflated rate limit / session usage](https://github.com/anthropics/claude-code/issues/38350)**  
   *62 comments, 42 👍*  
   Users on macOS report sessions consuming far more tokens than expected, making the tool expensive. High community engagement suggests this is a top‑tier cost concern.

2. **[#53915 – API Error: Server is temporarily limiting requests (rate limited)](https://github.com/anthropics/claude-code/issues/53915)**  
   *57 comments, 19 👍*  
   Windows and VSCode users hit server‑side rate limits even when within their own usage caps. A fresh duplicate (#69484) was filed today, confirming the issue is ongoing.

3. **[#26302 – Severe UI lag and mouse stutter on Windows (Desktop app)](https://github.com/anthropics/claude-code/issues/26302)**  
   *43 comments, 37 👍*  
   A performance regression introduced in Desktop 1.1.3189. Still unfixed after four months, this remains the most‑upvoted Windows bug in the repo.

4. **[#68721 – Team‑management tools (TeamCreate/TeamDelete) regression in 2.1.178](https://github.com/anthropics/claude-code/issues/68721)**  
   *15 comments, 5 👍*  
   Native team tools disappeared after bumping from 2.1.177. Marked as a regression on Linux; affects multi‑user workflows.

5. **[#47166 – JetBrains plugin request](https://github.com/anthropics/claude-code/issues/47166)**  
   *25 comments, 1 👍*  
   Community clamors for a first‑class JetBrains interface. Marked as duplicate, but the demand is clear: many developers want Claude Code outside VSCode.

6. **[#20944 – Setting to disable automatic IDE selection context](https://github.com/anthropics/claude-code/issues/20944)**  
   *16 comments, 58 👍*  
   Users want to opt out of context being automatically collected from the IDE environment, citing cost and privacy concerns.

7. **[#69358 – No response from API (2.1.181 constant failures)](https://github.com/anthropics/claude-code/issues/69358)**  
   *3 comments, 12 👍*  
   A fresh regression on Linux where the tool stops receiving API responses entirely. Rapid upvotes indicate widespread impact.

8. **[#69466 – `/config` dialog completely non‑functional (regression in 2.1.181)](https://github.com/anthropics/claude-code/issues/69466)**  
   *2 comments, 0 👍*  
   Settings changes do not persist; pressing Enter toggles the option instead of saving. Escape discards all changes. Affects macOS users.

9. **[#69487 – MCP tool call wedges indefinitely without client‑side timeout](https://github.com/anthropics/claude-code/issues/69487)**  
   *1 comment, 0 👍*  
   A single stalled MCP tool call can block the entire session. No default timeout exists for MCP tool calls in the CLI.

10. **[#68711 – Terminal text display corruption resolved only by window resize](https://github.com/anthropics/claude-code/issues/68711)**  
    *3 comments, 4 👍*  
    Text garbling in iTerm2 and Warp on macOS. Consistent reproduction reported.

## Key PR Progress (4 PRs)

- **[#69470 (closed) – Fix lock‑closed‑issues workflow](https://github.com/anthropics/claude-code/pull/69470)**  
  Switches from offset pagination to search API, fixing the stale‑issue lock workflow that had been failing for 53 consecutive days (since April 27).  
- **[#68673 (open) – Fix pagination break condition](https://github.com/anthropics/claude-code/pull/68673)**  
  Corrects the pagination loop to stop when a page is not full, not only when empty. Likely affects batch operations.  
- **[#23972 (open) – Hookify plugin: Python 3.8 compat & cwd‑independent rule loading](https://github.com/anthropics/claude-code/pull/23972)**  
  Adds `from __future__ import annotations` for Python 3.8 and fixes rule loading that was broken when the plugin ran from outside the project directory.  
- **[#45553 (open) – Resolve duplicate IPs](https://github.com/anthropics/claude-code/pull/45553)**  
  No description provided; appears to address duplicate IP handling in some internal tooling.

## Feature Request Trends

- **IDE‑agnostic expansion** — The strongest signal is the repeated call for a proper JetBrains plugin (#47166). Users want Claude Code integrated into their preferred IDE, not just VSCode.  
- **Cost transparency and control** — Requests to disable automatic IDE context (#20944), to add skill invocation analytics (#35319), and to manage session caching (#47098) all point to a growing sensitivity around token/wallet usage.  
- **Accessibility** — A built‑in text‑to‑speech option (#58429) was proposed, reflecting demand for hands‑free and blind‑user support.  
- **Desktop workflow improvements** — Launching a Code session from a specific folder via CLI or deep link (#54614) and sorting project groups by recency (#55225) are small but frequently echoed quality‑of‑life requests.  
- **Mobile‑desktop sync** — Several issues (#36151, #69485) touch on multi‑account switching and session‑name sync between mobile and desktop apps.

## Developer Pain Points

1. **Server‑side rate limiting** — Multiple reports (#53915, #69358, #69484) describe the tool being throttled even when personal usage limits are not exceeded. Confusing error messages and platform‑specific triggers (Windows, Linux) are common.  
2. **MCP instability** — MCP tools auto‑injecting and failing with 401s (#69324), tool calls hanging without timeout (#69487), and MCP tools not surfacing on mobile (#69365) create reliability gaps.  
3. **API & session cost inflation** — The inflated session usage bug (#38350) and cache‑miss behaviour (#47098) frustrate users who feel charged for work they did not request.  
4. **Display and TUI regressions** — Text corruption (#68711), keyboard scrolling broken (#48435), text selection issues in VSCode (#61021), and a general rendering regression flagged across many versions after 2.1.153 (#69486) degrade the terminal experience.  
5. **Configuration persistence** — `/config` dialog not saving changes (#69466) and the Windows MSIX config file pointing to the wrong location (#26073) are basic workflow blockers.  
6. **Shell‑compatibility issues** — The Bash tool emits non‑zsh syntax on macOS (#67146), causing silent failures when `SHELL=zsh`.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-19

## Today’s Highlights
The team shipped **rust-v0.141.0** with end-to-end encrypted Noise relay channels and cross-platform executor support, alongside three alpha releases paving the way for v0.142.0. Community attention remains fixed on **macOS CPU runaway** (Issue #25719) and a **rate‑limit cost spike** on Plus plans (Issue #28879). Several high‑impact Windows sandbox and permission regressions landed in the last 24 hours, while the prolific **#20161 phone‑verification bug** was finally closed after 200+ comments.

---

## Releases
- **[rust-v0.141.0](https://github.com/openai/codex/releases)**  
  *New Features*  
  - Remote executors now use authenticated, end-to-end encrypted Noise relay channels (#26242, #26245).  
  - Cross‑platform remote execution preserves executor‑native working directories, shells, and filesystem permission paths across app‑server and exec‑server boundaries.  

- **rust-v0.142.0-alpha.1 / .2 / .3**  
  Tagged without description; likely incremental internal builds leading to v0.142.0 stable.

---

## Hot Issues (Top 10 by Community Impact)

1. **#20161 – Phone number verification doesn't work** ([CLOSED](https://github.com/openai/codex/issues/20161))  
   ⚡ 201 comments | 125 👍  
   After SSO login on a new device, users are forced to enter a phone number they never added. Closed after weeks of debugging – a major authentication fix.

2. **#25719 – macOS `syspolicyd` / `trustd` CPU and memory runaway** ([OPEN](https://github.com/openai/codex/issues/25719))  
   33 comments | 40 👍  
   Codex Desktop repeatedly triggers system security daemons, causing persistent high CPU. Affects Apple Silicon Macs; still unresolved.

3. **#14601 – Configuration pollution: separate `trusted_level` from `config.toml`** ([OPEN](https://github.com/openai/codex/issues/14601))  
   15 comments | 43 👍  
   Trusted‑level prompts pollute the global config. Community strongly supports moving this setting to a per‑project file.

4. **#28988 – Full Access mode keeps asking for permission (26.614.11602)** ([OPEN](https://github.com/openai/codex/issues/28988))  
   9 comments | 6 👍  
   Recent macOS update introduces infinite permission loops in Full Access mode. Reproduced by Pro Max users.

5. **#16815 – Windows WSL agent fails with “AbsolutePathBuf deserialized without a base path”** ([OPEN](https://github.com/openai/codex/issues/16815))  
   9 comments | 7 👍  
   Switching agent environment to WSL breaks task creation. Affects Windows Business subscribers.

6. **#28879 – Rate‑limit cost per token jumped 10–20× since June 16** ([OPEN](https://github.com/openai/codex/issues/28879))  
   5 comments | 4 👍  
   Plus plan users on gpt‑5.5 see their 5‑hour budget drained in 2–3 prompts. No official explanation yet.

7. **#28997 – `logs_2.sqlite-wal` grows unbounded to tens of GB** ([OPEN](https://github.com/openai/codex/issues/28997))  
   6 comments  
   CLI’s WAL file on Linux consumes disk space indefinitely. Observed on v0.140.0; no auto‑cleanup.

8. **#28978 – Desktop app 26.616: new conversations fail with “missing field `inputSchema`”** ([OPEN](https://github.com/openai/codex/issues/28978))  
   3 comments | 5 👍  
   MCP configurations that work via CLI break on the desktop app after auto‑update. High urgency for MCP users.

9. **#28676 – Computer Use plugin fails on Windows (`@oai/sky` subpath not exported)** ([OPEN](https://github.com/openai/codex/issues/28676))  
   5 comments  
   Bootstrap fails before `sky.list_apps()`. Node package exports error from bundled runtime.

10. **#28241 – Codex turn‑diff tree refs break libgit2‑based Git clients** ([OPEN](https://github.com/openai/codex/issues/28241))  
    7 comments  
    After using Codex, Git clients (e.g., GitHub Desktop) fail due to malformed refs. Windows users affected.

---

## Key PR Progress

1. **[#29006 – Preserve skill descriptions outside model context](https://github.com/openai/codex/pull/29006)**  
   Stops truncating skill descriptions to 1024 chars in metadata, keeping full text for non‑model consumers while trimming only the context fragment sent to the model.

2. **[#28787 – Code‑mode: introduce transport‑neutral session runtime](https://github.com/openai/codex/pull/28787)**  
   Extracts session ownership into a transport‑neutral `SessionRuntime`, preparing cells and shared state for separate‑process transport.

3. **[#29035 – Optimize filesystem thread listing](https://github.com/openai/codex/pull/29035)**  
   Avoids parsing rollout summaries early when filtering threads by `SessionMeta` fields, significantly speeding up interactive queries in large directories.

4. **[#28683 – Track starting environments in snapshots](https://github.com/openai/codex/pull/28683)**  
   Behind a `deferred_executor` feature, allows session startup to proceed while remote environments are still connecting, avoiding delays.

5. **[#29026 – Avoid skill filesystem scans on cache hits](https://github.com/openai/codex/pull/29026)**  
   Skips `cwd` ancestor walking and `.agents/` checks when the skills snapshot is already cached – reduces per‑turn latency.

6. **[#28489 – Add indexed web search mode](https://github.com/openai/codex/pull/28489)**  
   Introduces `web_search = "indexed"` alongside existing modes, using a gated hosted index for faster, privacy‑aware search.

7. **[#28707 – Abort turns when rollout budgets expire](https://github.com/openai/codex/pull/28707)**  
   Propagates shared rollout‑budget exhaustion as a `TurnAborted` error, preventing runaway token consumption across threads.

8. **[#29014 – Honor startup custom CA bundles with managed MITM](https://github.com/openai/codex/pull/29014)**  
   Ensures custom `SSL_CERT_FILE` overrides are merged with the managed proxy’s generated bundle instead of being replaced.

9. **[#29013 – Protect managed MITM CA private keys from sandboxed commands](https://github.com/openai/codex/pull/29013)**  
   Moves the CA private key out of the shared‑user‑readable proxy directory, enforcing sandbox isolation.

10. **[#29022 – Support protected resource OAuth discovery](https://github.com/openai/codex/pull/29022)**  
    Aligns preflight and login OAuth discovery implementations, making plugin install work on servers that require protected‑resource metadata.

---

## Feature Request Trends
- **Config isolation**: Multiple requests to separate project‑scoped settings (trusted levels, provider base URLs) from a single global `config.toml` (see #14601, #28902).
- **Conversation management**: Users want to move conversations between projects (#24519) and merge context from parallel sessions via a `/merge` command (#29031).
- **Provider flexibility**: Calls for configurable `base_url` for Amazon Bedrock (#28902) and better cross‑provider thread resumption (#15219).
- **Better subagent UX**: Subagent notifications that confuse the model (#24225) and missing `inputSchema` in MCP tools (#28978) highlight demand for cleaner agent integration.

---

## Developer Pain Points
- **Windows instability**: The most frequently reported OS; issues span WSL agent failure (#16815), Chrome plugin registry keys (#24040), Git ref corruption (#28241), sandbox ACL corruption (#15777), missing sandbox helper module (#28982), transparent taskbar icons (#26809), UI flickering (#29029), and AV false positives (#28971).
- **macOS performance regressions**: Repeated `syspolicyd`/`trustd` CPU spikes (#25719, #28583) and Full Access permission loops (#28988) degrade daily use on Apple Silicon.
- **Rate‑limit unpredictability**: Unexplained 10–20× cost jumps (#28879) and hard resets instead of banked resets (#28811) erode trust in the billing system.
- **Disk & memory bloat**: Unbounded SQLite WAL growth (#28997) and log‑file accumulation force manual cleanup.
- **Sandbox permission loops**: Frequent “ask every time” dialogues even after approval (#28988), especially after updates.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*