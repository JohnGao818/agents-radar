# AI CLI Tools Community Digest 2026-06-25

> Generated: 2026-06-25 02:51 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date:** 2026-06-25 | **Analyst:** Senior Technical Analyst, AI Developer Tools

---

## 1. Ecosystem Overview

The AI CLI tools landscape in mid-2026 is characterized by rapid iteration cycles, with both Claude Code and OpenAI Codex shipping multiple releases weekly while communities surface increasingly sophisticated concerns. The dominant themes across both ecosystems are **persistent memory across sessions**, **transparent billing and rate-limit telemetry**, and **multi-agent reliability**—indicating the user base has moved beyond initial novelty to demand production-grade stability. Several cross-cutting issues suggest the industry is converging on shared architectural patterns (MCP, world-state snapshots, credential brokering) while diverging in execution philosophy. The most striking signal is a growing **trust deficit**: from Claude Code's model-perception degradation to Codex's cost-multiplier bug, users are actively questioning whether tool providers are optimizing for their success or for platform economics.

---

## 2. Activity Comparison

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Hot Issues (noteworthy)** | 10 | 10 |
| **PRs (last 24h)** | 5 | 10 |
| **Releases (last 24h)** | 2 (v2.1.191, v2.1.190) | 4 (3 alpha + 1 stable) |
| **Top Issue Engagement** | #36151: 106 comments, 372 👍 | #28879: 135 comments, 269 ❤️ |
| **Critical Security Fixes** | 2 (command injection in plugin) | 0 (infrastructure-focused) |
| **Community Sentiment** | Concerned about token burn, model quality | Frustrated by rate-limit billing, Windows perf |

**Key observation:** Codex shows double the PR activity (10 vs 5) and faster release cadence (4 vs 2 releases), but Claude Code's community engagement per issue is significantly higher—indicating a smaller but more vocal user base.

---

## 3. Shared Feature Directions

Requirements appearing across **both** communities:

| Requirement | Claude Code Signal | OpenAI Codex Signal |
|---|---|---|
| **Persistent memory / session context** | #47023 (hooks for external memory), #14227, #32627 | #29833–#29837 (WorldState persistence stack) |
| **Customizable TUI status bar** | Implied by multiple "status" requests | #17827 (token usage, rate limits, git branch) |
| **Multi-account / workspace switching** | #36151 (372 👍, mobile + desktop) | #25749 (account recovery lockout) |
| **Rate-limit / billing transparency** | #42249 (token quota depletion) | #28879, #22220 (compaction telemetry) |
| **Subagent lifecycle reliability** | #64605 (worktree isolation broken) | #24389, #25870 (`close_agent` hangs) |
| **MCP server / OAuth integration** | #70723, #70728 (server connection issues) | #29017–#29021 (OAuth refresh stack), #29924 |

**Signal:** Both communities are converging on a **stateful, observable, multi-account agent runtime**—neither tool fully delivers this today.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary focus** | Security, data integrity, model quality | Infrastructure, MCP, multi-agent orchestration |
| **Target user** | Individual developers, macOS power users | Enterprise teams, Windows users, managed environments |
| **Release strategy** | Conservative (2 patches/day, high stability bar) | Aggressive (3+ alphas/day, feature-heavy) |
| **Security posture** | Proactive (CRITICAL PRs for command injection) | Reactive (credential broker, OAuth enums) |
| **Community pain** | Model degradation perception, data loss | Rate-limit cost bugs, Windows regressions |
| **Unique strengths** | Cowork (pair programming), `/rewind` after `/clear` | WorldState persistence, Ultra reasoning mode |
| **Unique weaknesses** | iCloud file corruption, orphaned exe on Windows | 640 TB/year logging projection, ghost `.git` dirs |

**Key insight:** Claude Code prioritizes **predictability and safety** (even adding `/rewind` to undo `/clear`), while Codex prioritizes **capability expansion** (OAuth stacks, Ultra reasoning, skill lifecycle). This maps to different risk profiles for adopters.

---

## 5. Community Momentum & Maturity

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Issue engagement depth** | High: 5.4 avg comments/issue | Moderate: 2.8 avg comments/issue |
| **Feature request persistence** | High: #10238 open since Oct 2025 | Moderate: #17827 open since April 2026 |
| **Windows support maturity** | Low: orphaned exe, rendering stutter | Moderate: proxy support, but I/O regressions |
| **Security community trust** | Higher: acknowledged injection fixes | Lower: rate-limit bug unaddressed |
| **Documentation gap** | Model behavior transparency (#68780) | Compaction telemetry (#22220) |

**Verdict:** Claude Code has a **more engaged but smaller** community; Codex has **higher throughput with spreading dissatisfaction**. Codex's rate-limit bug (#28879) risks eroding trust faster than any feature gain can offset. Claude Code's token-consumption concerns (#42249) similarly threaten adoption.

---

## 6. Trend Signals for Developers

### 🔴 Critical Watch Items
1. **Rate-limit cost explosion (both ecosystems)** — #28879 (Codex, 10–20× cost jump) and #42249 (Claude Code, quota drained in minutes) suggest systemic billing bugs or silent consumption changes. **Implication:** Always monitor per-request token consumption; trust but verify provider billing.
2. **Model quality degradation controversy** — #68780 (Claude Code Opus 4.8) and general community suspicion. **Implication:** Pin model versions where possible; treat model updates as breaking changes.
3. **Data loss via iCloud/optimized storage** — #32637 (Claude Code Cowork + iCloud). **Implication:** Avoid running AI agents on cloud-synced directories; use local temp workspaces.

### 🟡 Emerging Patterns
4. **MCP becomes the standard integration layer** — Both tools are building OAuth, credential brokering, and lifecycle hooks around MCP. **Implication:** Invest early in MCP-compatible tooling; avoid proprietary integrations.
5. **World-state persistence as competitive moat** — Codex's #29833–#29837 stack is ahead of Claude Code's request-based approach (#47023). **Implication:** Session continuity is a differentiator; tools that lose context on resume will lose users.
6. **Windows remains second-class** — Both tools suffer Windows-specific regressions (orphaned procs, I/O floods, Defender conflicts). **Implication:** For Windows-heavy teams, expect higher manual oversight; evaluate per-platform deployment.
7. **Accessibility pressure is rising** — Claude Code's #69998–#70000 screen-reader issues signal regulatory or community-driven demand. **Implication:** Tools without accessibility investment will face adoption barriers in enterprise and education.

### 🟢 Tactical Recommendations
- **For cost-sensitive teams:** Implement token-usage dashboards externally; do not rely on built-in telemetry.
- **For multi-agent workflows:** Prefer Codex's WorldState persistence (resume/fork) over naive subagent spawning.
- **For security-critical environments:** Claude Code's injection fixes and Cowork isolation model offer stronger guarantees today.
- **For Windows users:** Expect 2–3 months latency before parity; consider macOS or Linux for production agent workloads.

---

**Bottom line:** The AI CLI tool market is rapidly maturing but fragmenting along philosophical lines—Claude Code prioritizes *safety and predictability*, Codex prioritizes *capability and velocity*. Neither is production-ready for all scenarios. Developers should evaluate based on their risk tolerance for cost spikes, data loss, and platform-specific regressions rather than raw feature counts.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-06-25 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following pull requests have garnered the most community discussion and attention. All are currently **open** and under review.

### #1 – skill-creator Fix (run_eval 0% recall bug)
**PR #1298** – [View on GitHub](https://github.com/anthropics/skills/pull/1298)  
**Author:** MartinCajiao | **Updated:** 2026-06-23  
**Functionality:** Fixes the core evaluation script (`run_eval.py`) that was always reporting 0% recall, making the entire skill description optimization loop (used by `run_loop.py` and `improve_description.py`) work against noise. The fix installs the eval artifact as a real skill, corrects Windows stream reading, trigger detection, and parallel worker behavior.  
**Discussion highlights:** References issue #556 (10+ independent reproductions). The high comment count reflects the criticality of this fix for anyone using the skill creator tool. Community members have been blocked on skill iteration because the evaluation pipeline was broken.

### #2 – Document Typography Skill
**PR #514** – [View on GitHub](https://github.com/anthropics/skills/pull/514)  
**Author:** PGTBoos | **Updated:** 2026-03-13  
**Functionality:** Adds a skill that enforces typographic quality control on generated documents—catches orphan words, widow paragraphs, and numbering misalignment. Designed to be triggered automatically whenever Claude produces a document.  
**Discussion highlights:** Strong positive reception; users note these issues affect every document Claude generates. The skill addresses a universal pain point in AI-generated content.

### #3 – ODT Skill (OpenDocument Support)
**PR #486** – [View on GitHub](https://github.com/anthropics/skills/pull/486)  
**Author:** GitHubNewbie0 | **Updated:** 2026-04-14  
**Functionality:** Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods). Supports LibreOffice documents and ISO standard formats.  
**Discussion highlights:** Community demand for non-proprietary document formats. The skill fills a gap in the existing document-skills collection (which covered only PDF, DOCX, etc.).

### #4 – Frontend-Design Skill Improvement
**PR #210** – [View on GitHub](https://github.com/anthropics/skills/pull/210)  
**Author:** justinwetch | **Updated:** 2026-03-07  
**Functionality:** Revises the existing frontend-design skill for clarity, actionability, and internal coherence. Ensures instructions are specific enough to steer Claude behavior without being overly prescriptive.  
**Discussion highlights:** The PR addresses a common criticism that many skills read more like developer documentation than operational instructions. Sets a standard for skill quality.

### #5 – Skill Quality & Security Analyzers (Meta-Skills)
**PR #83** – [View on GitHub](https://github.com/anthropics/skills/pull/83)  
**Author:** eovidiu | **Updated:** 2026-01-07  
**Functionality:** Adds two meta-skills—`skill-quality-analyzer` (evaluates structure, documentation, readability, completeness, actionability) and `skill-security-analyzer` (audits skills for privilege escalation, prompt injection, dangerous capabilities).  
**Discussion highlights:** These tools aim to improve the overall skill ecosystem quality. The community has debated appropriate security analysis methodology and the risk of false positives.

### #6 – Testing Patterns Skill
**PR #723** – [View on GitHub](https://github.com/anthropics/skills/pull/723)  
**Author:** 4444J99 | **Updated:** 2026-04-21  
**Functionality:** Comprehensive skill covering the full testing stack: testing philosophy (Testing Trophy model), unit testing patterns, React component testing with Testing Library, end-to-end patterns, and what *not* to test.  
**Discussion highlights:** Addresses a high-demand area—developers want Claude to generate robust test suites. The breadth of coverage is appreciated; some discussion around keeping the skill focused to avoid token bloat.

### #7 – AppDeploy Skill
**PR #360** – [View on GitHub](https://github.com/anthropics/skills/pull/360)  
**Author:** avimak | **Updated:** 2026-05-04  
**Functionality:** Enables Claude to deploy and manage web applications via AppDeploy—full-stack deployment, lifecycle management, environment variables, and HTTPS.  
**Discussion highlights:** The first skill to integrate a third-party deployment platform. Discussions center on security implications and whether Claude should have deployment capabilities by default.

### #8 – Skill-Creator YAML Validation Fix
**PR #539** – [View on GitHub](https://github.com/anthropics/skills/pull/539)  
**Author:** Lubrsy706 | **Updated:** 2026-04-16  
**Functionality:** Adds pre-parse validation to detect unquoted `description` fields containing colons, which silently break YAML parsing and cause truncated descriptions.  
**Discussion highlights:** This fix (and related PRs #361, #362) addresses a common source of skill misbehavior. High engagement from contributors encountering the same silent failures.

---

## 2. Community Demand Trends

Analysis of the top 15 issues by comment volume reveals three dominant demand themes:

### 🔒 Trust & Security Boundaries (Issue #492 – 17 comments)
**Issue #492** ([link](https://github.com/anthropics/skills/issues/492)) – Community skills distributed under the `anthropic/` namespace create a trust vulnerability. Users may grant elevated permissions to skills they believe are official. This has sparked a broader debate about namespace governance, permission scoping, and the need for a skill signing or verification mechanism.

### 🏢 Organizational & Enterprise Features (Issue #228 – 14 comments)
**Issue #228** ([link](https://github.com/anthropics/skills/issues/228)) – Request for org-wide skill sharing directly within Claude.ai, rather than manual file transfer. This is the top upvoted feature request (👍7) and reflects growing enterprise adoption. Also related: Issue #1175 (SharePoint/SPO security concerns) highlights demand for enterprise-grade access control in skills.

### 🔧 Skill-Creator Reliability (Issues #556, #1169, #1061 – 12, 3, 3 comments)
**Issues #556** ([link](https://github.com/anthropics/skills/issues/556)), **#1169** ([link](https://github.com/anthropics/skills/issues/1169)), **#1061** ([link](https://github.com/anthropics/skills/issues/1061)) – The `run_eval.py` script consistently reports 0% recall, making the optimization loop useless. Multiple users reproduced the bug on both Windows and Linux. This is the single biggest blocker for the skill creator workflow. Companion issues also report Windows compatibility failures (subprocess, encoding, pipe handling). The community is eager for a stable skill development experience.

#### Emergent Skill Directions (new work areas proposed in Issues)
- **Agent Governance** (Issue #412, 6 comments) – Safety patterns for AI agent systems: policy enforcement, threat detection, trust scoring, audit trails.
- **Compact Memory** (Issue #1329, 4 comments) – Symbolic notation for compact agent state to reduce context window usage in long-running agents.
- **MCP Exposure** (Issue #16, 4 comments) – Exposing skills as Model Context Protocol endpoints to make them interoperable with other AI tools and platforms.
- **Skill Duplication** (Issue #189, 6 comments) – A structural issue where `document-skills` and `example-skills` plugins contain identical content, wasting context. Community wants clear separation of concerns.

---

## 3. High-Potential Pending Skills

These open PRs have active discussions and recent updates, suggesting near-term merge potential:

| PR | Skill | Last Update | Why Hot |
|----|-------|-------------|---------|
| [#1298](https://github.com/anthropics/skills/pull/1298) | skill-creator eval fix | 2026-06-23 | Core blocker for all skill creators; multiple maintainers engaged |
| [#1323](https://github.com/anthropics/skills/pull/1323) | skill-creator trigger detection fix | 2026-06-23 | Companion fix – real skill name not being detected |
| [#1099](https://github.com/anthropics/skills/pull/1099) | skill-creator Windows pipe fix | 2026-05-24 | Addresses Windows subprocess crash |
| [#1050](https://github.com/anthropics/skills/pull/1050) | skill-creator Windows PATHEXT + encoding fix | 2026-05-24 | Two 1-line fixes resolving Windows compatibility |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns skill | 2026-04-21 | High demand; comprehensive coverage |
| [#514](https://github.com/anthropics/skills/pull/514) | document-typography skill | 2026-03-13 | Universal appeal; clean implementation |
| [#486](https://github.com/anthropics/skills/pull/486) | ODT skill | 2026-04-14 | Fills gap in document format support |
| [#360](https://github.com/anthropics/skills/pull/360) | AppDeploy deployment skill | 2026-05-04 | Early mover in deployment integration |

The skill-creator fixes (#1298, #1323, #1099, #1050) are likely to land first as they are critical infrastructure. The new skills may follow as the evaluation pipeline stabilizes.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, cross-platform skill development toolchain** – the top PRs and issues overwhelmingly center on fixing `run_eval.py` and the skill-creator loop rather than on new skill functionality, indicating that the ecosystem's growth is currently bottlenecked by tooling stability, not by lack of creative skill ideas.

---

# Claude Code Community Digest — 2026-06-25

## Today’s Highlights
A new patch release (v2.1.191) brings long-requested `/rewind` support after `/clear` and fixes several agent lifecycle bugs. The community is vocally concerned about extreme token consumption on macOS, suspected model degradation of Opus 4.8, and persistent data-loss risks from Cowork on iCloud. A flurry of accessibility issues also entered the tracker, signalling renewed focus on Windows screen-reader support.

## Releases
Two releases landed in the last 24 hours:

- **v2.1.191** — Adds `/rewind` capability to resume conversations after `/clear`. Fixes scroll-position jumping during streaming and prevents background agents from resurrecting after being stopped.
- **v2.1.190** — Bug fixes and reliability improvements only.

## Hot Issues (10 noteworthy)

1. **[#36151 – Multi-account switching in Claude Mobile app](https://github.com/anthropics/claude-code/issues/36151)**  
   💬 106 comments | 👍 372  
   *Why it matters:* Users with multiple accounts (personal/work) want seamless switching without shared email. High engagement reflects broad demand across mobile and desktop.

2. **[#10238 – Add support for subdirectories in skills](https://github.com/anthropics/claude-code/issues/10238)**  
   💬 45 comments | 👍 159  
   *Why it matters:* Organisations with large skill libraries need folder hierarchies. This feature request has been open since Oct 2025 and remains a top‑voted enhancement.

3. **[#47023 – Expose compact/session lifecycle hooks for external memory layers](https://github.com/anthropics/claude-code/issues/47023)**  
   💬 33 comments | 👍 4  
   *Why it matters:* Five separate issues ask for persistent memory. This proposal offers a clean hook‑based solution that the community could build on.

4. **[#42249 – Extreme token consumption – quota depleted in minutes](https://github.com/anthropics/claude-code/issues/42249)**  
   💬 26 comments | 👍 17  
   *Why it matters:* Normal usage draining daily quotas in under an hour is a critical cost and usability problem. Several users report the same pattern.

5. **[#68780 – Opus 4.8 reasoning degradation and performance regression](https://github.com/anthropics/claude-code/issues/68780)**  
   💬 10 comments | 👍 14  
   *Why it matters:* Users perceive a sharp drop in Opus 4.8 quality, with one threatening legal action. This mirrors earlier cycles where model updates caused visible nerfs.

6. **[#32637 – Cowork destroys user files when reorganising iCloud‑offloaded documents](https://github.com/anthropics/claude-code/issues/32637)**  
   💬 6 comments | 👍 1  
   *Why it matters:* **Data loss** – Cowork copies 0-byte stubs and then `rm -rf`s the originals. Even though closed, it highlights a dangerous class of bugs on macOS with Optimised Storage.

7. **[#62107 – Cowork scheduled tasks leave orphaned claude.exe on Windows](https://github.com/anthropics/claude-code/issues/62107)**  
   💬 5 comments | 👍 1  
   *Why it matters:* Memory accumulation from background tasks degrades Windows workstation performance over time.

8. **[#64605 – Chip‑spawned task runs on primary checkout instead of fresh worktree](https://github.com/anthropics/claude-code/issues/64605)**  
   💬 5 comments | 👍 1  
   *Why it matters:* Breaks the documented isolation contract for agent worktrees, risking dirty state on `main`.

9. **[#69829 – Random "hello" text insertion in agent harness under high load (20+ agents)](https://github.com/anthropics/claude-code/issues/69829)**  
   💬 5 comments | 👍 0  
   *Why it matters:* A bizarre concurrency bug that corrupts the agent’s output – likely a terminal input race condition.

10. **[#69998 – Screen reader: permission dialogs do not receive focus (NVDA on Windows)](https://github.com/anthropics/claude-code/issues/69998)**  
    💬 4 comments | 👍 0  
    *Why it matters:* Part of a broader accessibility initiative (#69996). Blind users are effectively blocked from approving file/shell actions.

## Key PR Progress (only 5 PRs updated in last 24h)

- [#70634 – fix: handle server rate limiting during normal usage](https://github.com/anthropics/claude-code/pull/70634)  
  Closes #70631. Adds resilience for API rate limits during routine operation.

- [#70633 – fix: Handle rate limiting headers for Anthropic API](https://github.com/anthropics/claude-code/pull/70633)  
  Closes #70630. Interprets `Retry-After` headers from Anthropic to avoid hammering the API.

- [#70582 – fix: sanitize subprocess call in llm.py](https://github.com/anthropics/claude-code/pull/70582)  
  **Severity: CRITICAL** – Fixes a command‑injection vulnerability in the security‑guidance plugin. Detected by a multi‑agent scanner.

- [#66854 – PR titled “toekn” (no description)](https://github.com/anthropics/claude-code/pull/66854)  
  Unclear intent; likely an accidental or spam submission.

- [#70538 – fix: sanitize subprocess call in gitutil.py](https://github.com/anthropics/claude-code/pull/70538)  
  **Severity: CRITICAL** – Another security fix in the same plugin, preventing shell injection via git commands.

## Feature Request Trends

- **Persistent memory / external memory layers** – Multiple issues (#47023, #14227, #32627, etc.) ask for a way to retain context across sessions. The community is building ad‑hoc solutions (markdown, knowledge graphs) and wants official hooks.
- **Skill organisation** – The long‑running #10238 for subdirectory support in skills shows that power users need structure for large skill sets.
- **Multi‑account and multi‑workspace switching** – #36151 and similar requests highlight the need for account/profile management.
- **Model behaviour transparency** – Issues like #70575 and #68780 demand clear release notes when model capabilities change, and the ability to pin model versions.
- **Accessibility** – Three new issues (#69998–70000) from a single reporter cover screen‑reader support for dialogs, generation status, and navigation. This is a nascent but important trend.

## Developer Pain Points

- **Excessive token consumption** (#42249) – Quota burn that feels disproportionate to the work done. Several developers report having to switch models or limit sessions.
- **Model quality regressions** (#68780, #70575) – Opus 4.8 is perceived as “dumb” after recent updates; users feel the model is dynamically throttled or swapped out without notice.
- **Data loss and file corruption** (#32637, #64605) – Cowork and agent worktrees can destroy or misplace user files, especially on macOS iCloud and Windows.
- **Windows stability and memory leaks** (#62107, #67406) – Orphan processes, rendering stutter, and invisible cursors degrade the Windows experience.
- **MCP server issues** (#70723, #70728) – Remote OAuth servers show “Connected” but register zero tools; image generation servers fail to load on Windows.
- **Concurrency bugs** (#69829, #64036) – Random text insertions and stale status classification in FleetView under heavy agent use.
- **Sandbox permission fatigue** (#70711) – Permission prompts fire even for sandbox‑allowed paths, training users to add broad exceptions that defeat the security model.
- **Tool‑call parsing failures** (#66400, #68719) – Intermittent malformed XML from the model wastes time and breaks automation.

---

*Data source: [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# 🧠 OpenAI Codex Community Digest — 2026-06-25

## 1️⃣ Today's Highlights

A severe **rate-limit cost bug** on `gpt-5.5` (Issue #28879) continues to dominate community attention, with 135 comments and 269 reactions—users report their 5-hour budget draining in 2–3 prompts after June 16. In positive news, the team merged three PRs that **eliminate ~85% of excessive SQLite feedback logs** (Issue #28224) which were projected to write up to 640 TB/year. Meanwhile, a flood of **Windows performance complaints** around persistent disk I/O and system lag suggests new regressions in the latest desktop builds.

---

## 2️⃣ Releases

Three alpha releases of the Rust client (`0.143.0-alpha.13` through `0.143.0-alpha.15`) landed, but no changelogs are provided. The stable `rust-v0.142.1` adds **opt-in Windows system proxy support** (PAC, WPAD, static proxies, and bypass rules) for authentication flows. This is a focused fix for enterprise users relying on corporate proxy infrastructure.

---

## 3️⃣ Hot Issues (Top 10 by Importance)

1. **#28879 — Rate-limit cost per token jumped 10–20× on Plus plan**  
   🔗 https://github.com/openai/codex/issues/28879  
   The most urgent open bug. Users on `gpt-5.5` report their 5-hour budget burns in 2–3 prompts. Session logs confirm the per-token consumption multiplier increased drastically around June 16. *No official response yet—community is demanding an investigation.*

2. **#28224 — SQLite feedback logs could write ~640 TB/year**  
   🔗 https://github.com/openai/codex/issues/28224  
   The author reports this **successfully closed** after three merged PRs cut 85% of logs. A cautionary tale about logging volume—and a sign the team is responsive to I/O performance issues.

3. **#25749 — No phone number recovery path for legacy MFA**  
   🔗 https://github.com/openai/codex/issues/25749  
   Users with an inaccessible legacy phone number are locked out entirely with no recovery flow. 62 comments, 37 👍—a long-standing UX failure for account recovery.

4. **#17827 — Customizable status line (TUI)**  
   🔗 https://github.com/openai/codex/issues/17827  
   Request for a Claude Code-style status bar showing token usage, model name, rate limits, git branch, etc. 76 👍 and still open since April—popular feature request with no movement.

5. **#22220 — Conversation Compaction Telemetry**  
   🔗 https://github.com/openai/codex/issues/22220  
   Users want visibility into when/why compaction happens, what’s being dropped, and context window health. 18 comments reflect a desire for transparency in long sessions.

6. **#25667 — macOS app leaves ~965 MB of code_sign_clone directories per launch**  
   🔗 https://github.com/openai/codex/issues/25667  
   Each app launch leaves behind ~965 MB of unreclaimed disk space. 13 comments point to a persistent cleanup bug on macOS.

7. **#24389 / #25870 — `close_agent` hangs for hours on unresponsive subagents**  
   🔗 https://github.com/openai/codex/issues/24389  
   🔗 https://github.com/openai/codex/issues/25870  
   Two related reports of multi-agent flows hanging indefinitely when a subagent reaches a terminal state (completed/interrupted) but remains listed as live. Both indicate reliability gaps in the subagent lifecycle.

8. **#29463 — Windows app writes TRACE websocket logs despite `RUST_LOG=warn`**  
   🔗 https://github.com/openai/codex/issues/29463  
   Log verbosity settings are ignored on Windows; TRACE websocket logs flood SQLite continuously. Reduces SSD lifespan and causes persistent writes.

9. **#29911 / #29858 — Windows app creates empty `.git` directories, triggering Defender CPU spikes**  
   🔗 https://github.com/openai/codex/issues/29911  
   🔗 https://github.com/openai/codex/issues/29858  
   Codex creates empty `.git` or `.agent` directories in non-Git workspaces, causing `git.exe` spawning loops and 100% CPU from Windows Defender. Two separately filed symptoms of the same root class.

10. **#29955 — Quota drained instantly: 100 credits → 0% in 1 message**  
    🔗 https://github.com/openai/codex/issues/29955  
    Newest rate-limit report (filed today). Pro*5 user had their full budget consumed by a single message. Likely related to #28879—suggests the bug is spreading to higher-tier plans.

---

## 4️⃣ Key PR Progress (Top 10)

1. **#29899 — Add Ultra reasoning effort**  
   🔗 https://github.com/openai/codex/pull/29899  
   Introduces a single user-facing “Ultra” reasoning mode that combines maximum reasoning with proactive multi-agent delegation. Simplifies the UX by merging two separate settings. *Not yet merged.*

2. **#29017–#29021 — MCP OAuth refresh serialization (5-PR stack)**  
   🔗 https://github.com/openai/codex/pull/29017  
   🔗 https://github.com/openai/codex/pull/29018  
   🔗 https://github.com/openai/codex/pull/29019  
   🔗 https://github.com/openai/codex/pull/29020  
   🔗 https://github.com/openai/codex/pull/29021  
   A coordinated set of changes to prevent race conditions during OAuth refresh of MCP servers. Serializes login/logout, refresh transactions, and rereads persisted credentials. *Core infrastructure for MCP reliability.*

3. **#29965 — Refresh selected skill context at runtime**  
   🔗 https://github.com/openai/codex/pull/29965  
   Allows turn-input contributors to append bounded context after runtime preparation. Enables skill catalogs and instructions to refresh dynamically while preserving precedence. *Enhances skill lifecycle flexibility.*

4. **#29960 — Activate selected executor skills atomically**  
   🔗 https://github.com/openai/codex/pull/29960  
   Freezes selected executor skill declarations per resolved root and publishes them with capability generations. Covers atomic publication, fork, and cold-resume lifecycle behaviors.

5. **#29833 / #29835 / #29837 — WorldState persistence stack (3 PRs)**  
   🔗 https://github.com/openai/codex/pull/29833  
   🔗 https://github.com/openai/codex/pull/29835  
   🔗 https://github.com/openai/codex/pull/29837  
   Makes `WorldState` snapshots serializable, persists them in rollouts, and replays them on resume/fork. Fixes a long-standing gap where resume lost the exact diff baseline. *Critical for session continuity.*

6. **#29959 — Conditional Codex home dotenv**  
   🔗 https://github.com/openai/codex/pull/29959  
   Adds conditional `.env.*` overlays under `CODEX_HOME`. Lexicographic loading with TCP condition evaluation. *Enables environment-specific config without manual switching.*

7. **#29752 — Integrate experimental credential broker**  
   🔗 https://github.com/openai/codex/pull/29752  
   Adds an integration layer so child processes can opt into a proxy-owned credential broker. Preserves brokered values across shell snapshots while removing proxy-scoped dummy values on exit. *Security improvement for managed environments.*

8. **#29924 — Represent MCP authentication with an enum**  
   🔗 https://github.com/openai/codex/pull/29924  
   Replaces `use_chatgpt_auth` boolean with a proper `enum` distinguishing OAuth and ChatGPT-session flows. Enables a first-party trust boundary for credential forwarding.

9. **#28529 — Support OAuth for HTTP MCP servers from selected executor plugins**  
   🔗 https://github.com/openai/codex/pull/28529  
   Routes OAuth bootstrap and refresh through the executor’s network boundary, enabling executor-only MCP servers to complete discovery and login.

10. **#29919 — TUI support for buffer experience**  
    🔗 https://github.com/openai/codex/pull/29919  
    A closed PR with no further details—likely a prelim PR for TUI buffering improvements. *Worth watching for future TUI enhancements.*

---

## 5️⃣ Feature Request Trends

- **Customizable status line / TUI widgets** (#17827) — Strong demand for real-time visibility into token usage, rate limits, model name, git branch, and context window. Modeled after Claude Code’s status bar.
- **Conversation compaction telemetry** (#22220) — Users want insight into when/why compaction happens and what context is dropped. A request for transparency in long-running sessions.
- **Multi-agent lifecycle reliability** (implied across #24389, #25870) — Hanging subagents and lack of timeout/force-close mechanisms are driving requests for more robust agent lifecycle management.
- **Per-session rate-limit awareness** (#28879 fallout) — Users want in-app dashboards showing real-time token consumption, budget burn rate, and per-request cost breakdown.

---

## 6️⃣ Developer Pain Points

| Category | Key Issues | Frequency |
|---|---|---|
| **Rate-limit / billing bugs** | #28879, #29955, #29760, #29948, #29961 | Very High (5+ reports this week) |
| **Windows performance regressions** | #28855, #29177, #29436, #29281, #29543, #29463, #29821, #29832, #29911, #29858 | Very High (>10 reports; disk I/O, input lag, ghost `.git` dirs) |
| **Multi-agent hang / lifecycle** | #24389, #25870 | Moderate (2 distinct reports of `close_agent` hanging for hours) |
| **macOS cleanup bugs** | #25667 (≈1 GB unreclaimed per launch) | Low (1 report, but high severity per launch) |
| **Logging verbosity ignored** | #29463 (TRACE writes despite `RUST_LOG=warn`) | Moderate (Windows-specific; SSD endurance issue) |
| **Account recovery lockout** | #25749 (legacy phone number, no recovery path) | Low (but critically blocking for affected users) |

### 🛑 Immediate Action Items for OpenAI
1. **Investigate and fix rate-limit cost multiplier bug** (#28879) — This is the #1 community concern, causing real financial harm to paying users.
2. **Triage Windows I/O regressions** — Multiple reports of 400+ GB/day writes, ghost `.git` directories, and kernel-pool growth point to a root cause in the latest desktop build.
3. **Improve subagent hang resilience** — Two separate issues show `close_agent` can block indefinitely, which is untenable for multi-agent workflows.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*