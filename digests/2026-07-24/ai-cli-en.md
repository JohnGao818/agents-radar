# AI CLI Tools Community Digest 2026-07-24

> Generated: 2026-07-24 02:16 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools — 2026-07-24

## 1. Ecosystem Overview

The AI CLI tools landscape is entering a **consolidation phase** where reliability and predictable behavior are overtaking raw feature velocity as the primary community concern. Both Claude Code and OpenAI Codex are experiencing distinct but parallel stability pressures: Claude Code battles persistent network-layer failures (ECONNRESET) across platforms, while Codex faces severe Windows-specific resource exhaustion bugs. Despite these challenges, both toolchains continue to ship incremental improvements, and the community demand for **multi-session orchestration, context transparency, and MCP/extension lifecycle management** is converging across both ecosystems. The day’s digests reveal that neither tool has yet solved the fundamental tension between agent autonomy and system stability at scale.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Hot Issues (high-traffic)** | 10 | 10 |
| **Total Issues Updated (24h)** | ~20–30 (estimated from digest scope) | ~100 |
| **PRs Updated (24h)** | 4 | 10 |
| **New Releases** | None | 2 (rust-v0.146.0-alpha.5, rust-v0.146.0-alpha.3.1) |
| **P0/Critical Issues** | 0 explicitly designated | 2 (#34879 CPU saturation, #34260 WMI exhaustion) |
| **Longest-running open issue** | #5674 (ECONNRESET, since Aug 2025) | #20214 (Windows freeze/stutter, 3 months) |

Codex exhibits **substantially higher operational velocity** — 100 issues and 10 PRs touched in 24 hours versus Claude Code’s quieter cadence. This reflects a difference in release strategy: Codex’s continuous-delivery alpha pipeline generates constant churn (and regression risk), while Claude Code appears to batch changes or maintain a slower, perhaps more stable, release rhythm.

---

## 3. Shared Feature Directions

Three requirements appear across *both* communities, indicating genuine market demand:

### Multi-Session Orchestration & Remote Control
- **Claude Code**: #29006 (114 👍) — remote control of one session from another or from the desktop app
- **Codex**: #13036 (multi-chat display) — users want parallel, side-by-side sessions; #22220 — telemetry for context compaction across sessions
- **Common pattern**: Single-threaded sessions are increasingly insufficient for complex workflows. Both communities want to run, monitor, and coordinate multiple agent sessions simultaneously.

### MCP / Extension Lifecycle & Identification
- **Claude Code**: #41836 (24 👍) — per-conversation identifiers for MCP servers; #80016 — extensions handshake but tools never dispatch
- **Codex**: #20883, #19858 — project-scoped MCP process pools instead of per-session spawning; recurring leaks on Windows
- **Common pattern**: MCP/extension processes are treated as stateless, single-use resources, but real-world usage demands persistent, identifiable, and scoped service instances.

### Context & Compaction Transparency
- **Claude Code**: PDF token optimization (#80449); general cost-awareness sentiment
- **Codex**: #22220 (12 👍) — telemetry for compaction decisions; #35032 — compaction leaves ~80% full context, wasting quota
- **Common pattern**: Users on metered plans (Pro, Max) are demanding visibility into token consumption, compaction triggers, and per-turn budgets. Cost control is a first-class concern, not an operations afterthought.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary pain point** | Network reliability (ECONNRESET, connection drops) | Windows system-level resource exhaustion (WMI, process leaks) |
| **Feature emphasis** | Model access management (Fable 5 entitlements); Terminal UI refinements; multi-session in desktop app | Sandbox integrity (writable roots, patch reliability); Guardian/review pipeline; plugin attribution |
| **Target user** | Developer comfortable with CLI/TUI, multi-platform macOS/Linux/WSL | Developer deep in IDE (VSCode) and remote Windows workflows; security-conscious teams |
| **Release philosophy** | Slower, batched; transparent feature requests | Continuous-delivery alpha stream; higher churn, faster feedback |
| **Technical approach** | Focus on agent-model interaction (per-conversation state, MCP identifiers) | Focus on process model, sandboxing, and system-level resource governance |
| **Major unaddressed risk** | Fable 5 billing bugs eroding trust in Max plan value | Windows stability undermining adoption on the dominant desktop OS |

Claude Code’s community is more **model-and-session-centric** — the top requests revolve around how the agent interacts with the model, manages conversations, and controls multiple instances. Codex’s community is more **infrastructure-and-sandbox-centric** — the top issues concern process lifecycle, file-system access patterns, and security review pipelines. This likely reflects their respective architectural heritages: Claude Code emerged from an API-product mindset, while Codex evolved from an IDE-plugin background.

---

## 5. Community Momentum & Maturity

### Activity Velocity
- **Codex** is significantly more active: ~100 issues updated daily versus Claude Code’s ~20–30. The 10 PRs in 24h (vs. 4) and continuous alpha releases indicate a team under pressure to stabilize a rapidly-shipping product.
- **Claude Code** shows stable, focused community engagement — 10 hot issues, high-vote feature requests (114 👍 for #29006), but lower daily churn. This suggests either a more mature product with fewer regression cycles, or a slower development cadence.

### Community Sentiment
- **Claude Code**: Users are *persistent but frustrated* — issues like #5674 have been open for **11 months** without resolution. The Fable 5 billing bugs (#79337, #80382) are creating a trust deficit around plan value.
- **Codex**: Users are *vocal and urgent* — the P0 designation on #34879 and the rapid escalation of #34260 (filed 4 days ago, already 28 comments) show a community that expects fast fixes. The high volume of automation PRs (copyberry[bot]) suggests an engineering team leaning into automation to manage regression volume.

### Maturity Signals
- Claude Code’s community articulates **well-scoped, conceptually mature feature requests** (per-conversation MCP IDs, OpenTelemetry git worktree info) — this indicates a user base that has deeply integrated the tool.
- Codex’s community is still battling **foundational reliability issues** (process leaks, UI stutter, sandbox brokenness on Windows) — the product feels earlier in its lifecycle on that platform.

---

## 6. Trend Signals

### Signal 1: Model Entitlement & Metering Is a Trust Erosion Point
Both Fable 5 access confusion (Claude Code) and context-compaction inefficiency (Codex) point to **unreliable billing and quota logic** undermining user trust. For prosumers and teams, unpredictable overage or denied access to advertised features is a dealbreaker. Expect tools to invest heavily in *entitlement verification transparency* in the near term.

### Signal 2: Single-Device, Single-Session Is No Longer Sufficient
The cross-tool demand for remote session control (#29006, 114 👍) and multi-chat displays (#13036) signals that advanced users want **agent farms, not single assistants**. The industry is moving toward orchestrated, multi-agent workflows — but neither tool has a production-grade solution yet.

### Signal 3: Windows Remains the Achilles’ Heel
Codex’s three top issues are Windows-specific resource exhaustion bugs. Claude Code’s ECONNRESET issue (#5674) is macOS-only. As enterprise adoption grows on Windows, tools that cannot deliver reliable Windows experiences (especially on WSL and VSCode) will face an adoption ceiling.

### Signal 4: Context Visibility Is Becoming a Cost-Control Interface
Users on metered plans increasingly treat context consumption as a **financial metric**. Compaction telemetry (#22220), per-turn token budgets, and manual compaction controls are moving from “nice-to-have” to “must-have” for power users managing monthly cost exposure.

### Signal 5: PR Velocity ≠ Stability
Codex’s 10 PRs/day reflects a high-bandwidth engineering operation, but the simultaneous P0 Windows regressions suggest that **shipping velocity is outpacing quality assurance**. Claude Code’s slower cadence may correlate with fewer acute regressions, but also slower resolution of chronic issues (11-month-old ECONNRESET bug). Each tool faces a different point on the stability-velocity tradeoff curve.

---

## Conclusion

For technical decision-makers: **Claude Code** offers a more stable multi-platform experience with a mature feature-set, but carries unresolved network reliability risk on macOS and growing model-access trust issues. **OpenAI Codex** ships faster and shows stronger momentum in security/sandbox innovation, but is currently unstable on Windows — a critical gap for enterprise deployments. Neither tool has solved multi-session orchestration at scale, but both communities are actively demanding it. The near-term strategic fork is clear: *reliability vs. velocity*, with the winner likely determined by which team can stabilize its respective platform weakness first.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report (as of 2026-07-24)

---

## 1. Top Skills Ranking

The following open pull requests represent the most-discussed Skill submissions, based on community comment activity. All remain open; none have been merged yet.

### #1298 — Fix `run_eval.py`: Improve Recall Detection  
**Functionality:** Repairs the core evaluation script used by skill-creator to measure how often a skill triggers. Fixes Windows stream reading, trigger detection, and parallel worker issues.  
**Discussion highlights:** Addresses the widely-reported recall=0% bug (#556, confirmed by 10+ users). Critical for the description-optimization loop to work.  
**Status:** Open, last updated 2026-06-23.  
[GitHub PR](https://github.com/anthropics/skills/pull/1298)

### #514 — Add `document-typography` Skill  
**Functionality:** Enforces typographic quality control on generated documents—prevents orphan words, widow paragraphs, and numbering misalignment common in AI output.  
**Discussion highlights:** Users note that these issues affect virtually every Claude-generated document; demand for automated polish is strong.  
**Status:** Open, last updated 2026-03-13.  
[GitHub PR](https://github.com/anthropics/skills/pull/514)

### #1367 — Add `self-audit` Skill (Reasoning Quality Gate v1.3.0)  
**Functionality:** Mechanical file verification plus a four-dimension reasoning audit before delivery, prioritized by damage severity. Works across any project and model.  
**Discussion highlights:** Follows a proposal issue (#1385) for a full quality-gate pipeline; early adopters praise its structured approach to catching reasoning failures.  
**Status:** Open, last updated 2026-07-02.  
[GitHub PR](https://github.com/anthropics/skills/pull/1367)

### #723 — Add `testing-patterns` Skill  
**Functionality:** Comprehensive coverage of the full testing stack—unit (AAA pattern), React (Testing Library), E2E (Playwright), and testing philosophy (Trophy model).  
**Discussion highlights:** Addresses a clear gap: the skills repo had no dedicated testing skill. Community members debated scope and overlap with existing testing-related skills.  
**Status:** Open, last updated 2026-04-21.  
[GitHub PR](https://github.com/anthropics/skills/pull/723)

### #525 — Add `pyxel` Skill for Retro Game Development  
**Functionality:** Wraps the Pyxel MCP server to enable turn-based retro/pixel-art game creation with Python—write, run, capture, inspect, iterate.  
**Discussion highlights:** Received sustained interest due to the novelty of game development support and the unique MCP integration. Author is the original Pyxel creator.  
**Status:** Open, last updated 2026-07-15.  
[GitHub PR](https://github.com/anthropics/skills/pull/525)

### #1302 — Add `color-expert` Skill  
**Functionality:** Self-contained color expertise for any task—covers naming systems (ISCC-NBS, Munsell, RAL, etc.), color spaces with usage tables (OKLCH, OKLAB, CAM16), and practical selection guidance.  
**Discussion highlights:** Niche but highly valued by designers and data-viz practitioners; the PR has remained active with incremental improvements.  
**Status:** Open, last updated 2026-07-21.  
[GitHub PR](https://github.com/anthropics/skills/pull/1302)

### #486 — Add `odt` Skill (OpenDocument Support)  
**Functionality:** Create, fill, read, and convert OpenDocument Format files (.odt, .ods). Includes template filling and ODT-to-HTML conversion.  
**Discussion highlights:** Strong demand from LibreOffice users; questions about ODF standard compliance and cross-platform rendering.  
**Status:** Open, last updated 2026-04-14.  
[GitHub PR](https://github.com/anthropics/skills/pull/486)

---

## 2. Community Demand Trends

From the most-commented issues, several clear demand directions emerge:

- **Security & Trust Boundaries** (Issue #492, 43 comments) — The community is deeply concerned about community skills distributed under the `anthropic/` namespace creating a false sense of trust. Demand for official vs. community skill labeling, sandboxing, and permission auditing is high.

- **Enterprise Collaboration** (Issue #228, 14 comments) — Users want org-wide skill sharing without manual file transfer. The request for a shared skill library or direct sharing link within Claude.ai is consistent.

- **Skill-Creator Toolchain Reliability** (Issues #556, #202, #1169, #1061) — A cluster of issues around the skill-creation/optimization tooling: recall=0% bugs, Windows compatibility, encoding panics, and subprocess errors. The community urgently needs the evaluation loop to work correctly before they can trust skill optimization.

- **New Skill Directions** —  
  - **Agent Governance** (Issue #412): Safety patterns for AI agent systems (policy enforcement, threat detection, audit trails).  
  - **Compact Agent Memory** (Issue #1329): Symbolic notation for long-running agent state to reduce context waste.  
  - **Reasoning Quality Pipelines** (Issue #1385): Multi-gate verification (pre-task calibration, adversarial review, delivery verification).  
  - **MCP Integration** (Issue #16): Exposing Skills as MCP servers to standardize API interfaces.

- **Platform Compatibility** — A recurring theme is extending Claude Skills to AWS Bedrock (Issue #29) and fixing Windows-specific failures (Issue #1061).

---

## 3. High-Potential Pending Skills

These active-comment PRs are not yet merged but show high likelihood of landing soon based on momentum and community interest:

- **`skill-creator` Bug Fixes** (multiple PRs: #1298, #1099, #1050, #1323, #362, #361, #539, #538, #541) — A concentrated wave of fixes from several contributors. The sheer volume indicates the maintainers are actively working on stabilizing the skill-creation pipeline. Likely to be merged as a batch.

- **`self-audit` (#1367)** — Strong conceptual backing from issue #1385; the author has already produced a working implementation with detailed reasoning gates.

- **`testing-patterns` (#723)** — Clear demand, well-defined scope, and no blocking objections. Could be merged as-is or with minor refinements.

- **`color-expert` (#1302)** — High-quality, self-contained skill with continued updates through July 2026.

- **`pyxel` (#525)** — Unique value proposition; maintained by the library's original author, which increases confidence in accuracy.

- **`document-typography` (#514)** — Solves a universal pain point; low controversy.

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is for **reliable, secure, and platform-compatible skill creation tooling** — not just new Skill content, but a trusted pipeline that makes it safe and easy for anyone to build, test, and share high-quality Skills across Windows, Linux, and enterprise environments.

---

# Claude Code Community Digest — 2026-07-24

**Prepared for AI developer tooling technical audience**

---

## Today's Highlights

No new releases shipped in the last 24 hours. The community remains focused on two major themes: **network stability** (persistent ECONNRESET and "connection closed mid-response" errors across macOS, Linux, and WSL) and **Fable 5 access confusion** for Max plan subscribers. Users are also pushing for better **multi-session tooling**, including a remote control feature for the desktop app and per-conversation identifiers in MCP.

---

## Releases

*None in the last 24 hours.*

---

## Hot Issues (10 of note)

### 1. Persistent ECONNRESET Errors on macOS
**#5674** — 50 comments, 47 👍  
[Issue link](https://github.com/anthropics/claude-code/issues/5674)  
A long-standing (since Aug 2025) bug causing connection drops on macOS only, while Windows/Linux on the same network work fine. High community pain, still open with a repro available.

### 2. Fable 5 Prompts ‘Usage Credits Required’ on Max Plan
**#79337** — 40 comments, 12 👍  
[Issue link](https://github.com/anthropics/claude-code/issues/79337)  
Since Fable 5 became standard on Max plans (2026-07-20), users are downgraded to Opus 4.8 and told they need credits. Indicates a billing/entitlement check bug.

### 3. Enable Remote Control for Claude Code Sessions in Desktop App
**#29006** — 35 comments, 114 👍  
[Issue link](https://github.com/anthropics/claude-code/issues/29006)  
Top-voted feature request: allow one desktop session to remotely control another (e.g., headless agent orchestration). Community clearly wants multi-session orchestration.

### 4. API Error: Connection Closed Mid-Response (WSL/VSCode)
**#69415** — 33 comments, 65 👍  
[Issue link](https://github.com/anthropics/claude-code/issues/69415)  
Frequent disconnections in VSCode on WSL that make the tool unusable. Related to #69336 (Linux) and #5674.

### 5. No Session/Conversation Identifier Sent to MCP Servers
**#41836** — 14 comments, 24 👍  
[Issue link](https://github.com/anthropics/claude-code/issues/41836)  
MCP servers cannot distinguish concurrent sessions, preventing per-conversation state. Limiting for multi-session workflows.

### 6. VSCode Session Rename Doesn’t Sync Terminal Tab
**#37628** — 11 comments, 14 👍  
[Issue link](https://github.com/anthropics/claude-code/issues/37628)  
Renaming via sidebar doesn't update terminal tab; next message overwrites custom name. Minor but irritating for heavy VSCode users.

### 7. Opus 4.7/4.8 Token Usage Regression (2–3×)
**#64961** — 10 comments, 5 👍  
[Issue link](https://github.com/anthropics/claude-code/issues/64961)  
Users report dramatically higher token consumption and more frequent disconnects after a recent update. Affects cost-sensitive workflows.

### 8. Claude Desktop (Windows): Filesystem Extension Handshake Succeeds But Tools Not Dispatched
**#80016** — 9 comments, 0 👍  
[Issue link](https://github.com/anthropics/claude-code/issues/80016)  
Re-opened bug from #22299: extensions connect but tool calls never execute. Reinstall doesn't fix.

### 9. Conversation Rendered Multiple Times in Terminal (Windows TUI)
**#49985** — 8 comments, 22 👍  
[Issue link](https://github.com/anthropics/claude-code/issues/49985)  
Duplicated conversation output in terminal TUI under Windows. High annoyance for terminal-heavy users.

### 10. Fable 5 Contradictory Availability Messages for Max Plan
**#80382** — 3 comments, 0 👍 (new today)  
[Issue link](https://github.com/anthropics/claude-code/issues/80382)  
Another Fable 5 billing glitch: shows conflicting availability messages to Max users. Likely related to #79337.

---

## Key PR Progress (4 items)

### #41611 — Add the Missing Source to Claude Code (OPEN)
[PR link](https://github.com/anthropics/claude-code/pull/41611)  
Author: tornikeo — Adds a missing source reference to the codebase. Unclear from summary; open since March 2026.

### #42604 — Remove "Retro-Futuristic" Recommendation from Frontend Design Skill (CLOSED)
[PR link](https://github.com/anthropics/claude-code/pull/42604)  
Author: TechyHaroon — Closes with a playful note; likely a documentation or configuration change.

### #80508 — Fix: Paginate Comments and Reactions in auto-close-duplicates (OPEN)
[PR link](https://github.com/anthropics/claude-code/pull/80508)  
Author: Serhii-Leniv — Fixes #80506. The auto-close duplicate script only reads 30 comments/reactions due to missing pagination, causing missed duplicate detection. Important for maintainers.

### #80495 — Fix: Stop Parsing /ralph-loop Prompt Text as Shell Code (OPEN)
[PR link](https://github.com/anthropics/claude-code/pull/80495)  
Author: Serhii-Leniv — Fixes #16037. The `/ralph-loop` custom command substitutes user prompt literally into shell execution, breaking for everyday users. Affects Windows/git-bash.

**Note:** Only 4 PRs were updated in the last 24h; no further items to list.

---

## Feature Request Trends

Based on enhancement-labeled issues and high-vote items:

- **Remote session control** (#29006, 114 👍) — ability to control one session from another or from the desktop app. Likely the most desired feature.
- **Syntax highlighting in VS Code chat panel** (#64968, 21 👍). Recurring request; code blocks rendered as plain text.
- **Per-conversation MCP identifiers** (#41836, 24 👍). Essential for multi-session and stateful MCP servers.
- **OpenTelemetry git worktree info** (#80745, new). Users want telemetry to include branch/worktree context for team monitoring.
- **PDF token optimization** (#80449, new). Suggestion to avoid sending both text and image rendering from PDFs to reduce cost.

---

## Developer Pain Points

Recurring themes from recent high-traffic bugs:

- **Network reliability** — ECONNRESET (#5674) and "connection closed mid-response" (#69415, #69336) affect all platforms. Users report making the tool unusable for any real work.
- **Fable 5 billing glitches** — Multiple reports (#79337, #79341, #80382) of Max plan users being incorrectly denied access to the new model. Creates trust issues around plan features.
- **Auto-updater inefficiency** (#79942) — Every running session downloads a full 265 MB binary independently; no cross-session lock. Wasteful for multi-session workflows.
- **MCP extension failures** (#80016, #76040) — Extensions handshake but tools never dispatch; JSON Schema $ref resolution fails.
- **TUI rendering bugs** (#49985 — duplicated output; #64474 — empty Bash tool output expanded; #77242 — question text missing from AskUserQuestion dialog). Degraded experience in terminal mode.
- **Non-reproducible authorization bypass** (#73739) — AutoMode task classifier blocks an operation, but the main agent still executes it. Security concern if confirmed.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-24

## Today’s Highlights

Two new Rust alpha releases landed, but the community’s attention is consumed by a wave of **critical Windows stability regressions**. A P0 CPU-saturation bug on launch (#34879) and an unbounded `taskkill.exe`/WMI-exhaustion loop (#34260) have generated urgent discussion alongside a persistent high-volume freeze-and-stutter report (#20214) that remains unresolved after months. With **~100 issues updated in the last 24 hours** and a flood of automation PRs from copyberry[bot], the project is clearly in a high-velocity stabilization cycle.

---

## Releases

Two incremental Rust alpha builds were published:

- **[rust-v0.146.0-alpha.5](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.5)** — Latest alpha, likely hotfixes from the previous release cycle. No changelog beyond version bump.
- **[rust-v0.146.0-alpha.3.1](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.3.1)** — Minor patch on the `.3` line.

No detailed release notes were included — these appear to be continuous-delivery snapshots.

---

## Hot Issues

1. **[#20214 — Codex App frequently freezes/stutters on Windows 11 Pro](https://github.com/openai/codex/issues/20214)**  
   The longest-running and most-upvoted open issue (75 comments, 72 👍) describes persistent UI stutter on a well-resourced Ryzen 5/32 GB machine. Community frustration is high; no fix has been shipped in the three months since filing.

2. **[#34260 — unbounded taskkill.exe/conhost.exe cleanup storm exhausts WMI](https://github.com/openai/codex/issues/34260)**  
   A severe Windows process-management bug: Codex spawns hundreds of `taskkill.exe` processes, each with a `conhost.exe`, that collectively exhaust the WMI provider quota and lock the system. 28 comments, 9 👍; filed only four days ago and already urgent.

3. **[#34879 — [P0 regression] Windows desktop launch saturates all CPU cores via WmiPrvSE](https://github.com/openai/codex/issues/34879)**  
   Filed yesterday, this reports that launching Codex (build 26.715.10079.0) spikes all 32 logical processors to 100% immediately. Complements #34260 in describing Windows system-level resource abuse.

4. **[#4003 — Patched files have mixed line endings on Windows](https://github.com/openai/codex/issues/4003)**  
   A long-standing bug (27 comments, 71 👍) — Codex does not respect existing file line endings when applying patches on Windows. Quietly frustrating for developers who maintain consistent `.gitattributes`.

5. **[#30712 — Codex injects split writable roots, causing `apply_patch` to fail on Windows](https://github.com/openai/codex/issues/30712)**  
   11 comments, 12 👍. The safe edit path is broken in the sandbox, forcing agents to fall back to PowerShell for writes. A sandbox reliability blocker.

6. **[#35032 — Auto-compaction completes but leaves context ~80% full, forcing repeat cycles](https://github.com/openai/codex/issues/35032)**  
   A detailed report about context compaction being ineffective in long-running tool-heavy threads. Leaves only ~20% runway before the next compaction — effectively wastes usage quota.

7. **[#22220 — Conversation Compaction Telemetry / Context Health](https://github.com/openai/codex/issues/22220)**  
   Feature request (19 comments, 12 👍) asking for visibility into when and why compaction happens. Users want to see token counts per turn, compaction frequency, and health indicators. Strong community backing.

8. **[#27284 — SSH remote project shows “No chats” while remote threads exist in state DB](https://github.com/openai/codex/issues/27284)**  
   A data-visibility bug on macOS when connecting to remote Linux hosts. Chats exist in the state database but the UI shows nothing. Affects remote workflow reliability.

9. **[#19891 — “For coding” view hides edited file names behind aggregate summaries](https://github.com/openai/codex/issues/19891)**  
   A UX regression: after an update, the code-review view collapsed individual file edits into opaque summaries. 8 comments, 8 👍 from developers who need diff clarity.

10. **[#33786 — Completed large thread is fully replayed every few seconds, causing system-wide input stutter](https://github.com/openai/codex/issues/33786)**  
    A Windows performance bug where long threads replay completely on a timer, creating UI stutter. 4 comments, 2 👍 — but a clear reproduction that points to a rendering or state-reconciliation issue.

---

## Key PR Progress

1. **[#35063 — Track deferred tool namespaces in world state](https://github.com/openai/codex/pull/35063)**  
   Adds a `deferred_tool_world_state` feature that exposes deferred tool namespaces to the model. Disabled by default; foundational for multi-step tool orchestration.

2. **[#35065 — Avoid duplicating deferred sources in tool search](https://github.com/openai/codex/pull/35065)**  
   Optimization: when `DeferredToolWorldState` is active, the tool search description already advertises sources — this PR stops redundant listing, saving context tokens.

3. **[#35054 — Allow disabling the update_plan tool](https://github.com/openai/codex/pull/35054)**  
   Configuration-driven control: adds `tools.update_plan.enabled` (default on) so users or organizations can opt out of the re-planning tool.

4. **[#35049 — Register the Guardian V2 feature flag](https://github.com/openai/codex/pull/35049)**  
   Adds `GuardianV2` to the feature registry and configuration schema, disabled by default. Part of the next-generation approval/review pipeline.

5. **[#35036 — Preserve Windows sandbox proxy settings in guardian sessions](https://github.com/openai/codex/pull/35036)**  
   Fix for Windows: Guardian review commands were discarding proxy-port configuration, breaking sandboxed review on Windows. A direct response to Windows sandbox friction.

6. **[#35034 — Route environment registry requests through the shared HTTP client](https://github.com/openai/codex/pull/35034)**  
   Noise-environment registry requests now follow the exec-server’s outbound proxy policy without leaking registry URLs in diagnostics. Security + correctness.

7. **[#35033 — Expose Browser Use requirements through the app server](https://github.com/openai/codex/pull/35033)**  
   Parses `browser_use.disable_auto_review` from layered config and exposes it via the `configRequirements/read` endpoint. Enables per-user browser automation control.

8. **[#35031 — Enforce writer ownership for thread archive and deletion](https://github.com/openai/codex/pull/35031)**  
   Data-race fix: archive and delete operations must acquire paginated writer ownership. Prevents corruption when multiple processes touch the same thread.

9. **[#35029 — Preserve plugin attribution across command approvals](https://github.com/openai/codex/pull/35029)**  
   Plugin metadata (`plugin_id`, `script_path`) is now propagated through delegated approvals and guardian reviews. Stronger audit trail for plugin-originated commands.

10. **[#35020 — Attribute command executions to trusted plugin scripts](https://github.com/openai/codex/pull/35020)**  
    Shell and unified-exec commands are resolved against trusted plugin roots, adding `pluginId` and `scriptPath` fields to execution events. Improves security visibility.

---

## Feature Request Trends

Three major themes dominate open feature requests:

- **Context management & transparency** — Users want telemetry on conversation compaction (#22220), visibility into token budgets per turn, and the ability to manually trigger or block compaction. Related issue #13036 (multi-chat display) suggests developers want to run parallel side-by-side sessions, which makes compaction behavior even more critical.
- **MCP process lifecycle improvements** — Multiple requests (#20883, #19858) ask for project-scoped MCP process pools instead of per-session spawning. MCP server leaks are a recurring pain point, especially on Windows.
- **Sandbox and permission control** — After starting a desktop session with full access, some users experience downgraded permissions when continuing from mobile (#30485). There is also demand for better sandbox writable-root configuration (#30712) and explicit controls for the “update_plan” tool (#35054 style).

---

## Developer Pain Points

The single loudest pattern this week is **Windows desktop stability**. Three of the top-10 issues by comment count are direct Windows crash/hang/livelock reports (#34879, #34260, #33786), and #20214 has been open for three months. The common thread is **WMI and process-management exhaustion** — `taskkill.exe`, `WmiPrvSE`, and `conhost.exe` leaks. Developers on AMD Ryzen hardware with ample RAM are seeing the worst symptoms.

Other recurring frustrations:

- **apply_patch sandbox reliability** — Mixed line endings (#4003) and split writable roots (#30712) force agents to bypass the sandbox with PowerShell, reducing safety guarantees.
- **Session state and data loss** — Post-update history mapping loss (#26157), “No chats” on remote projects (#27284), and stale subagents in the cache (#25179) undermine trust in long-running agent workflows.
- **Performance regressions from context replay** — Full thread replay on timer (#33786) and ineffective compaction (#35032) waste both system resources and usage quota, a double hit for paying Pro users.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*