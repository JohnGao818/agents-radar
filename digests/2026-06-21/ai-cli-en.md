# AI CLI Tools Community Digest 2026-06-21

> Generated: 2026-06-21 03:43 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date:** 2026-06-21 | **Sources:** Claude Code & OpenAI Codex Community Digests

---

## 1. Ecosystem Overview

The AI CLI tools landscape is marked by a clear divergence between stability-focused incrementalism (Claude Code) and rapid, ambition-driven iteration with regressions (OpenAI Codex). Both tool communities are converging on multi-agent orchestration and session continuity as the next frontier, but they approach these capabilities from fundamentally different architectural philosophies—Claude Code emphasizing structured agent hierarchies and plugin extensibility, while Codex pursues unified world-state models and thread-level orchestration primitives. A shared vulnerability is emerging around sandbox and platform-specific reliability, with Windows and mobile gaps becoming prominent pain points across both ecosystems. The week's most salient signal is the tension between community demand for robust multi-agent primitives and the reality of foundational regressions (sandbox metadata, cross-platform binary compatibility) that still dominate day-to-day developer experience.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Hot Issues (Top 10)** | 10 featured issues | 10 featured issues |
| **Total Issue Comments (Top 10)** | ~250 comments | ~306 comments |
| **Total Issue Upvotes (Top 10)** | ~266 👍 | ~668 👍 |
| **PRs in last 24h** | 4 (all fixes/docs) | 10 (3 closed, 7 open; architecture + fixes) |
| **Releases today** | v2.1.185 (minor UX) | None |
| **Critical Regression** | Termux/Android (#50270, 50 days unresolved) | `sandboxPolicy` field bug (#29189+, multiple dupes) |

**Key takeaway:** Codex commands higher community engagement (2.5× total upvotes) and more active PR development, but is currently in a higher-regression phase. Claude Code's lower activity reflects a quieter development cadence, not necessarily lower quality—their regression is older and arguably more damaging to a specific user segment.

---

## 3. Shared Feature Directions

These requirements appear across **both** tool communities, suggesting ecosystem-wide priorities:

| Requirement | Claude Code Signals | OpenAI Codex Signals | Common Need |
|---|---|---|---|
| **Multi-agent / Inter-session Orchestration** | #24798 (18👍), #28300 (A2A protocol), #1770 (parent-child), #65456 | #14923 (thread/* turn/* primitives), #20312, #15299 | Standardized primitives for agent A→agent B communication; task handoff; context sharing |
| **Event-Driven Notifications & Hooks** | #13024 (waiting-for-input hook, 71👍), #28765 (push for task completion, 41👍) | #21166 (Telegram), #20475 (Slack), #11820 (mobile notifications) | External triggers when agents block on input or complete long-running tasks |
| **Sensitive File / Secret Exclusion** | *(less explicit—plugin marketplace focus)* | #2847 (.codexignore proposal, 409👍) — **single most-upvoted issue in either tool** | Mechanism to prevent model from reading secrets, credentials, or dependency trees |
| **Cross-Platform Stability (Windows)** | #14088 (mapped drive history loss), #69706 (401 auth) | #28248 (ACL after crash), #29200 (setup dialog spam), #29117 (permission prompts) | Windows-specific sandbox, filesystem, and auth reliability |
| **Session Continuity / Context Isolation** | #47926 (resume across devices) | #25319 (VS Code workspace scoping, 34👍), #28806 (resume/fork checkpoint) | Per-project context, safe resume across device/workspace boundaries |

**Notable divergence:** Claude Code's community focuses heavily on **notifications** (71👍 for input hooks) and **cross-device** session resumption, while Codex's community is singularly obsessed with **sensitive file exclusion** (409👍—nearly 1.5× the next-highest upvote count across both tools).

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Core Architecture** | Agent hierarchy with defined roles (Cowork, Task tool, parent-child) | World-state consolidation (unified model-visible state), thread-level orchestrator |
| **Primary User Base** | Enterprise teams, multi-developer workflows, plugin/marketplace extension | Individual developers (Plus plan), mobile-first users, VS Code integration |
| **API / Pricing Model** | API-based cost model; retry timeout adjusted today (20s) | Rate-limit token budget (Plus); per-token cost volatility (#28879: 10-20× jump) |
| **Plugin / Extensibility** | Plugin marketplace (hookify system, MCP plugins) with reliability issues (#36431 Telegram drops) | MCP tools (node_repl, browser, computer use) tightly coupled to sandbox metadata |
| **Mobile Support** | iOS notifications requested (#28765, #29438); desktop pty leak bug (#66434) | ChatGPT iOS app connectivity (#22898, mobile offline); mobile-first cross-device pairing |
| **Regressions Today** | Termux/Android: 50-day unresolved native binary incompatibility | sandboxPolicy field bug: <24-hour outbreak affecting macOS *and* Windows, multiple tool surfaces |
| **PR Velocity** | Low (4 PRs/day); majority hookify bugfixes + telemetry | High (10 active PRs); architectural changes (world state, checkpoint resumption) + bugfixes |

**Key insight:** Claude Code is optimizing for **structured multi-agent workflows** with a marketplace ecosystem (similar to VS Code extension model), while Codex is optimizing for **unified execution context** with tight sandbox control. The regressions reflect their respective complexity: Claude's binary incompatibility is a packaging/CI oversight; Codex's sandbox metadata bug is an error in their complex world-state model that cascades across all MCP tools.

---

## 5. Community Momentum & Maturity

| Aspect | Claude Code | OpenAI Codex |
|---|---|---|
| **Community Size (by engagement)** | Smaller but vocal; ~25 avg comments per top issue | Larger (2.5× total upvotes); more duplicate reports indicating broader user base |
| **PR Acceptance Rate** | Low velocity but high quality (4/4 are meaningful fixes) | High velocity but mixed (3 closed + 7 open; architectural PRs still in review) |
| **Regression Management** | Slower to resolve major issues (50-day Termux bug); quiet development weeks | Fast-spreading regressions (sandboxPolicy <24h to multi-issue duplicates); faster response via PRs |
| **Feature Request Sophistication** | High: proposing IPC primitives, A2A protocol, event hooks | High: proposing world-state models, thread/fork primitives, checkpointing |
| **Documentation Quality** | Docs-focused PR today (#69710) | Workspace headline/message API PRs suggest growing administrative UX |

**Assessment:**
- **Claude Code** feels **more mature but slower-moving**—the community is sophisticated (asking for IPC primitives, not just "fix this bug") but the core team's release cadence is measured. The Termux regression is a worrying signal for a tool that clearly *had* a working cross-platform strategy before.
- **OpenAI Codex** feels **higher-energy but more volatile**—the PR velocity and architectural ambition (world state consolidation, checkpoint-based resume) indicate rapid iteration, but the sandboxPolicy bug shows that ambition outpaces testing. The 409-upvote request for `.codexignore` suggests that Codex's *design philosophy* (maximal model visibility) creates a pain point Claude Code doesn't share.

---

## 6. Trend Signals for Developers

### Multi-Agent Is the Dominant Theme (but Not Production-Ready)
Both communities are asking for the same primitives: inter-agent IPC, task handoff, context sharing. However, neither tool has delivered this reliably—Claude Code's `Task` tool parent-child communication (#1770) has been open since June 2025. **Developers should expect multi-agent orchestration to remain a "coming soon" feature for 6-12 months**, and should not bet their architecture on any tool's current multi-agent capabilities.

### Sandbox Security Is Becoming a Differentiator
Codex's #2847 (`.codexignore`) with 409 upvotes is the loudest signal. **Sensitive file exclusion is rapidly becoming table-stakes** for production use of AI CLI tools. Developers evaluating tools should prioritize which sandbox model works for their workflow:
- Claude Code's approach (plugin marketplace, hookify rules) may offer more control but requires configuration.
- Codex's approach (sandbox metadata, protected data mode in #26229) is more opinionated but currently buggy.

### Cost Predictability Is a Growing Concern
Codex's #28879 (10-20× cost jump) is a **red flag for enterprise adoption**—if per-token costs can spike without notice, budget-conscious teams cannot rely on it. Claude Code's price-per-call model (with today's retry timeout adjustment) suggests a different philosophy: stable but potentially more expensive per-task. **Watch for both tools to introduce cost caps or transparency features** in the next 3-6 months.

### Platform-Specific Reliability Is the Hidden Tax
- **Windows:** Both tools have unresolved issues (mapped drives, ACLs, permission spam). Windows users should expect friction and budget extra setup time.
- **Mobile:** Codex has an explicit mobile connectivity failure (#22898); Claude Code lacks mobile CLI entirely.
- **Linux/Non-standard:** Claude Code's Termux/Android bug (#50270) shows that Linux-on-mobile users are effectively abandoned. **If you work on ARM Linux, Chromebook, or alternative platforms, neither tool is reliable today.**

### The "Plugin vs. World-State" Architecture Debate
Claude Code's plugin marketplace (hookify, MCP plugins) suggests a **federated** approach—extensions live outside the core and communicate via defined hooks. Codex's world-state consolidation (#29282, #29249) suggests a **centralized** approach—everything lives in a unified model-visible context. Developers should consider which model fits their stack:
- Federated (Claude Code): More modular, easier to extend, but harder to debug when state gets stale.
- Centralized (Codex): Consistent context, but single point of failure (as the sandboxPolicy bug demonstrates).

### Recommendation for Technical Decision-Makers
- **Choose Claude Code for:** Enterprise teams needing structured multi-agent workflows, plugin extensibility, and stable cross-platform support (as long as you're not on Termux/Android).
- **Choose OpenAI Codex for:** Individual developers who need fast iteration, tight sandbox control, and mobile/desktop pairing—at the cost of higher volatility and current sandbox regressions.
- **Monitor both for:** Inter-session IPC primitives (both communities are converging), cost predictability improvements, and Windows stability gains. Neither tool is mature enough to bet a production pipeline on multi-agent orchestration today.

**Bottom line:** The AI CLI tools ecosystem is in an **adolescent phase**—ambitious architectural visions, community consensus on what's needed (multi-agent, events, security), but foundational reliability issues that still consume most of the energy. The next 6 months will tell us which architecture (federated vs. centralized) scales better, and whether either tool can deliver on multi-agent before a third-party competitor does.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data: github.com/anthropics/skills | Snapshot: 2026-06-21*

---

## 1. Top Skills Ranking

The following Pull Requests have attracted the most discussion and represent the community's current focus areas:

### #514 – Document Typography Skill
**Status:** Open | **Author:** PGTBoos | **Created:** 2026-03-04
**Link:** https://github.com/anthropics/skills/pull/514

A quality-control skill that prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. The author argues these typographic issues affect "every document Claude generates," positioning this as a universal quality layer rather than a niche formatting tool. Discussion centers on whether typography enforcement should be a standalone Skill or baked into existing document-generation Skills. The PR remains open with sustained attention.

### #486 – ODT / OpenDocument Skill
**Status:** Open | **Author:** GitHubNewbie0 | **Created:** 2026-03-01
**Link:** https://github.com/anthropics/skills/pull/486

Adds support for creating, filling, reading, and converting OpenDocument Format files (.odt, .ods). Addresses a significant gap in the document-skills ecosystem, which currently covers PDF, DOCX, and HTML but not LibreOffice's native format. Discussion reflects community interest in enterprise document workflows where ODF compliance is mandated. The PR is open with ongoing refinement of template-filling capabilities.

### #210 – Frontend-Design Skill Clarity Improvements
**Status:** Open | **Author:** justinwetch | **Created:** 2026-01-05
**Link:** https://github.com/anthropics/skills/pull/210

A revision of the existing frontend-design Skill to make instructions more actionable and internally coherent. The key insight: every instruction should be something Claude can actually follow within a single conversation. This PR exemplifies a trend toward Skill-quality meta-improvements rather than new Skill proposals. Discussion has been extensive, suggesting broad agreement that existing Skills need refinement.

### #83 – Meta-Skills: Quality Analyzer & Security Analyzer
**Status:** Open | **Author:** eovidiu | **Created:** 2025-11-06
**Link:** https://github.com/anthropics/skills/pull/83

Proposes two meta-Skills that evaluate other Skills across five dimensions: Structure & Documentation (20%), plus security analysis for community-submitted Skills. This would create a self-regulating quality ecosystem. Despite its early creation date, the PR remains open with active discussion about standardization and governance — possibly held up by decisions on whether to merge into `example-skills` or create a new `meta-skills` directory.

### #538 & #539 – Skill-Creator Tooling Fixes (Case Sensitivity & YAML Parsing)
**Status:** Open | **Author:** Lubrsy706 | **Created:** 2026-03-06
**Link:** https://github.com/anthropics/skills/pull/538 | https://github.com/anthropics/skills/pull/539

Two complementary fixes: one corrects case-sensitive file references in the PDF Skill that break on Linux filesystems; the other adds YAML frontmatter validation for unquoted descriptions containing colons. These are narrow but critical — the YAML issue silently truncates Skill descriptions, making them non-functional. The developer ecosystem is paying close attention because these directly affect Skill submission reliability.

### #1298 – run_eval.py Always Reports 0% Recall
**Status:** Open | **Author:** MartinCajiao | **Created:** 2026-06-10
**Link:** https://github.com/anthropics/skills/pull/1298

A substantial fix for a systemic bug where the skill-creator evaluation pipeline reports `recall=0%` for every description, breaking the description-optimization loop entirely. The root cause spans multiple subsystems: eval artifact installation, Windows stream reading, trigger detection, and parallel worker configuration. Despite being very recent, this PR has attracted immediate attention because the recall bug is blocking all Skill optimization workflows (referenced in Issues #556, #1169).

---

## 2. Community Demand Trends

From the Issues tracker, the community's most vocal demands cluster around four themes:

**Skill Sharing & Distribution (#228, 14 comments, 👍7)**
The highest-engagement Issue requests org-wide skill sharing without manual file transfer. Users want a shared skill library or direct sharing links within Claude.ai. The 14 comments and 7 upvotes reflect real enterprise pain — teams managing 10+ Skills need distribution channels, not file-download workflows.

**Skill-Creator Reliability (#556, 12 comments, 👍7; #1169, 3 comments, 👍1)**
Two Issues document the same core bug: `run_eval.py` always returns 0% trigger rate, making the description optimization loop optimize against noise. This is the single most disruptive bug in the ecosystem — it renders the primary Skill development workflow non-functional. The community is actively reproducing and investigating.

**Security & Trust Boundaries (#492, 7 comments, 👍2)**
Community-submitted Skills under the `anthropic/` namespace create a trust boundary vulnerability. Users may grant elevated permissions to what they believe are official Anthropic Skills. This raises important questions about namespace governance and security labeling that the repository maintainers have not yet addressed.

**Windows Compatibility (#1061, 3 comments)**
Multiple Issues and PRs document Windows-specific failures in skill-creator scripts: `PATHEXT` not honored, `cp1252` encoding conflicts, and pipe/select incompatibilities. The Windows user base is small but vocal, and the issues are well-documented.

---

## 3. High-Potential Pending Skills

These PRs have active discussion and are likely to land soon:

| PR | Skill | Author | Key Feature | Likelihood |
|----|-------|--------|-------------|------------|
| **#723** | testing-patterns | 4444J99 | Full-stack testing coverage (unit, React, E2E) with Testing Trophy philosophy | Medium |
| **#568** | servicenow | Vanka07 | Broad ServiceNow platform assistant (ITSM, ITOM, SecOps, CSDM, IntegrationHub) | Medium-High |
| **#444** | AURELION suite (4 skills) | Chase-Key | Structured cognitive framework + persistent memory for professional knowledge management | Medium |
| **#181** | SAP-RPT-1-OSS predictor | amitlals | Tabular foundation model for enterprise analytics on SAP data | Low-Medium |
| **#335** | masonry-generate-image-and-videos | junaid1460 | AI image/video generation via Masonry CLI (Imagen 3.0, Veo 3.1) | Low |
| **#154** | shodh-memory | varun29ankuS | Persistent context across conversations for AI agents | Medium |

The **ServiceNow skill (#568)** and **testing-patterns (#723)** have the clearest use cases and most refined proposals. The **AURELION suite (#444)** is ambitious but may face merge friction due to its four-skill scope. The **SAP predictor (#181)** and **Masonry media skill (#335)** are domain-specific but well-defined.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *reliable Skill development tooling* — specifically fixing the `run_eval.py` 0% recall bug (PR #1298, Issues #556/#1169) that has broken the entire description-optimization workflow, overwhelming all other Skill feature requests.**

This is a critical finding: the community is not primarily asking for new Skills. They are asking for the *infrastructure to build and test Skills* to work correctly. The recall bug, Windows incompatibilities, and YAML parsing failures together create a development experience where Skill authors cannot validate their work. Until these tooling issues are resolved, the rate of high-quality Skill submissions will remain suppressed.

---

Here is the **Claude Code Community Digest** for **2026-06-21**, based on the GitHub data you provided.

---

# Claude Code Community Digest — 2026-06-21

## Today’s Highlights
The community is increasingly vocal about **multi-agent orchestration and inter-session communication**, with numerous feature requests converging on standardized IPC primitives. A critical **Termux/Android regression** remains unresolved, blocking users on v2.1.113+. Today’s release slims the API stall timeout message but continues a quiet week for features.

## Releases
- **v2.1.185** — *Released 2026-06-21*
  - Changes the streaming stall hint from “No response from API · Retrying in …” to “Waiting for API response · will retry in …”.
  - Triggers retry after **20 seconds of silence** (up from 10 seconds).
  - **Analysis:** A minor UX improvement for users experiencing intermittent API latency, but likely not sufficient for the deeper “No Response from API” regression reported in #69538.

## Hot Issues (Top 10 by Community Impact)
1. **[#50270] Termux/Android completely broken (v2.1.113+)** — *41 comments, 50 👍*  
   The switch from a JS entry point to a native glibc binary (introduced in 2.1.113) renders Claude Code unusable on Android (Termux). The platform reports `android`, not `linux`, and the binary is rejected by the Android kernel. **No fix has shipped.** This remains the single most upvoted open defect.  
   [View Issue](https://github.com/anthropics/claude-code/issues/50270)

2. **[#14088] Chat history not persisting on mapped drives / OneDrive** — *36 comments, 12 👍*  
   Windows users on network or cloud-synced drives lose all conversation history. High frustration given the platform’s widespread enterprise use.  
   [View Issue](https://github.com/anthropics/claude-code/issues/14088)

3. **[#40175] Cowork global instructions silently revert to older version** — *25 comments, 12 👍*  
   Cowork users save global instructions only to see them silently revert. This undermines trust in configuration persistence.  
   [View Issue](https://github.com/anthropics/claude-code/issues/40175)

4. **[#24798] Inter-session communication for multi-Claude workflows** — *37 comments, 18 👍*  
   A long-running feature request for sequencing tasks across parallel sessions. Represents the most consistent community demand this month.  
   [View Issue](https://github.com/anthropics/claude-code/issues/24798)

5. **[#13024] Add hook for when Claude is waiting for user input** — *24 comments, 71 👍*  
   High enthusiasm (71 thumbs-up). Developers want build-system integration or Slack pings when a session blocks on user consent.  
   [View Issue](https://github.com/anthropics/claude-code/issues/13024)

6. **[#28300] Multi-agent collaboration across machines (Agent-to-Agent protocol)** — *29 comments, 0 👍 (but high discourse)*  
   A direct neighbor of #24798, proposing explicit A2A protocol support. Heavy cross-referencing in comments suggests strong latent demand.  
   [View Issue](https://github.com/anthropics/claude-code/issues/28300)

7. **[#36431] Telegram plugin: inbound MCP notifications never delivered** — *19 comments, 31 👍*  
   Outbound works; inbound silently drops. A core integration reliability issue for teams using MCP plugins for notification.  
   [View Issue](https://github.com/anthropics/claude-code/issues/36431)

8. **[#1770] Parent-child agent communication in Task tool** — *14 comments, 25 👍*  
   One of the oldest open feature requests (June 2025). Users want the Agent tool’s spawned tasks to report back or accept interrupts.  
   [View Issue](https://github.com/anthropics/claude-code/issues/1770)

9. **[#28765] Push notifications for completed tasks in remote-control mode** — *14 comments, 41 👍*  
   Strong interest in iOS/desktop push when a long-running task finishes while the app is backgrounded.  
   [View Issue](https://github.com/anthropics/claude-code/issues/28765)

10. **[#66434] Desktop app leaks pseudo-terminals (ptys) until system runs out** — *7 comments, 4 👍*  
    A system-level stability bug: one long-running desktop session can exhaust all available ptys (`forkpty: Device not configured`).  
    [View Issue](https://github.com/anthropics/claude-code/issues/66434)

## Key PR Progress
Only **4 pull requests** were updated in the last 24 hours. Here are the most technically relevant:

1. **[#69727] fix(hookify): match file rules against Write tool content**  
   Fixes a silent fire failure: `event: file` hooks (e.g., “Warn About Debug Code”) never triggered when Claude created a new file via the `Write` tool. Root cause was a field-name inference mismatch (`new_text` vs `content`).  
   [View PR](https://github.com/anthropics/claude-code/pull/69727)

2. **[#69716] fix(workflows): send Statsig event time in milliseconds**  
   `claude-dedupe-issues.yml` sent epoch seconds as a string; Statsig expects milliseconds. The sibling workflow already did it correctly. A small but important fix for internal telemetry accuracy.  
   [View PR](https://github.com/anthropics/claude-code/pull/69716)

3. **[#69698] fix(hookify): use root-relative imports to fix marketplace install**  
   Fixes a module-resolution issue that broke hookify installation from the plugin marketplace.  
   [View PR](https://github.com/anthropics/claude-code/pull/69698)

4. **[#69710] docs: Update plugins README to use recommended install methods**  
    Documentation-only—updates plugin installation instructions away from the deprecated `npm install -g @anthropic-ai/claude-code`.  
    [View PR](https://github.com/anthropics/claude-code/pull/69710)

> *Note: Only 4 PRs were touched in the 24-hour window. The digest highlights all of them as they constitute the full merge/development activity.*

## Feature Request Trends
The dominant themes across all open issues:

1. **Multi-Agent / Multi-Session Orchestration (highest velocity)**  
   - Inter-session communication primitives (#24798, #62153, #62631)  
   - Agent-to-agent protocol across machines (#28300)  
   - Parent-child agent monitoring and task handoff (#1770, #65456)  
   - Session-as-process primitive (spawn/communicate/terminate) (#68996, #65456)  
   - Agent hierarchy dashboard for real-time visualization (#24537, #29438)  

2. **Cross-Device / Cross-Platform Session Continuity**  
   - Resume sessions across devices (#47926)  
   - iOS push notifications for permission approval (#29438) and task completion (#28765)  

3. **Notifications & Event-Driven Architecture**  
   - Hook for when Claude waits for user input (#13024)  
   - Reliable interrupt/notification mechanism for inter-agent messaging (#35072)  
   - Async / event-driven communication as a first-class capability (#55981)  

4. **Plugin & Marketplace Reliability**  
   - Update button in marketplace is non-functional (#45810)  
   - Telegram MCP plugin inbound delivery failure (#36431)  

## Developer Pain Points
Recurring frustrations and high-frequency requests:

- **Termux/Android regression (#50270):** The #1 pain point by both comments and upvotes. No workaround exists since v2.1.113. Community sentiment suggests an official re-architecture or JS fallback is needed.
- **API reliability regressions (#69538):** Intermittent “No Response from API” errors since June 17, with auto-retry causing cumulative slowdown.
- **Cowork global instructions silently revert (#40175):** Breaks team workflows as saved configurations are lost without warning.
- **Background agents die silently on pause/resume (#63023):** No completion notification or work recovery—agents killed by sleep or idle are invisible to the user.
- **No reliable intrA-session IPC (#35072, #48965, #55981):** Community has tried PostToolUse hooks, file-based signaling, and MCP—none provide reliable mid-conversation delivery.
- **Windows platform gaps:** Chat history loss on mapped drives (#14088) and 401 auth errors on Windows (#69706) are repeatedly reported but receive limited engineering attention in recent releases.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-21

## Today's Highlights
A **critical sandboxPolicy metadata bug** in Codex Desktop 26.616 is disrupting Browser Use, Computer Use, and the node_repl MCP tool across all platforms, generating a flood of near-identical reports. Meanwhile, OpenAI engineers are actively merging PRs to consolidate model-visible state into a unified “world state” architecture and to fix the sandbox metadata regression. The developer community continues to push for **exclusion of sensitive files**, **cross‑thread orchestration primitives**, and **inbound event-driven session wake** as top feature priorities.

## Releases
No new releases in the last 24 hours.

## Hot Issues (10 most noteworthy)

1. **[#2847 – A way to exclude sensitive files](https://github.com/openai/codex/issues/2847)**  
   *78 comments, 409 👍*  
   The most‑upvoted open enhancement. Users want a `.codexignore`‑style mechanism (repo‑local and global) to prevent Codex from reading or sending sensitive paths (e.g., secrets, `node_modules/`) to the model. Strong community demand.

2. **[#29189 – `node_repl` fails: `sandboxPolicy` missing in sandbox-state-meta](https://github.com/openai/codex/issues/29189)**  
   *58 comments, 63 👍*  
   The lead bug of today’s regression storm. Codex Desktop 26.616.41845 breaks the bundled node_repl MCP on macOS because `codex/sandbox-state-meta` lacks the `sandboxPolicy` field. Breaks all dependent tools (browser, computer use).

3. **[#18960 – Frequent reconnect loop: WebSocket closed before response.completed](https://github.com/openai/codex/issues/18960)**  
   *50 comments, 35 👍*  
   Long‑running issue with streaming failures in the Codex app. Users report silent disconnections and automatic reconnects that never recover, wasting time and token budgets.

4. **[#28879 – Rate‑limit cost per token jumped 10–20× since June 16](https://github.com/openai/codex/issues/28879)**  
   *39 comments, 81 👍*  
   Plus plan users on `gpt-5.5` see their 5‑hour budget drained in 2–3 prompts. Logs show per‑token consumption increased dramatically. High community frustration and many upvotes.

5. **[#29193 – Windows `node_repl/js` fails with missing `sandboxPolicy`](https://github.com/openai/codex/issues/29193)**  
   *17 comments, 2 👍*  
   Windows‑specific duplicate of #29189. On Windows Codex Desktop the same `codex/sandbox-state-meta: missing field sandboxPolicy` error blocks JavaScript execution.

6. **[#22898 – Mobile shows desktop as offline; Reconnect does nothing](https://github.com/openai/codex/issues/22898)**  
   *14 comments, 40 👍*  
   ChatGPT iOS app cannot connect to a running Codex desktop. Tapping “Reconnect” produces no feedback. Reported by many mobile‑first developers.

7. **[#29205 – Browser/annotation tools fail: missing `sandboxPolicy`](https://github.com/openai/codex/issues/29205)**  
   *12 comments*  
   Another manifestation of the sandboxPolicy regression – this time affecting in‑app browser and annotation tools. Shows how wide the blast radius is.

8. **[#29219 – Desktop ignores `node_repl` args, sends malformed sandbox metadata](https://github.com/openai/codex/issues/29219)**  
   *12 comments, 4 👍*  
   Goes beyond the missing field: the desktop app actively strips or ignores user‑configured sandbox arguments, making it impossible to work around the bug via settings.

9. **[#14923 – Explicit cross‑thread orchestration over `thread/*` and `turn/*` primitives](https://github.com/openai/codex/issues/14923)**  
   *12 comments, 2 👍*  
   A long‑running enhancement request for explicit APIs to coordinate multiple threads (e.g., agent A passes a context to agent B). Still active after three months.

10. **[#25319 – Scope VS Code chats to current workspace/project](https://github.com/openai/codex/issues/25319)**  
    *12 comments, 34 👍*  
    Developers want the Codex VS Code extension to isolate chat history per workspace. Currently all chats are global, causing noise when switching projects.

---

## Key PR Progress (10 important merges & active PRs)

1. **[#29282 – Move live context diffing into world state](https://github.com/openai/codex/pull/29282)** *(open)*  
   Consolidates model‑visible settings diffing from ad‑hoc builders into the typed world state, fixing baseline incompleteness that could cause stale context in multi‑turn sessions.

2. **[#29249 – Migrate environment context to model world state](https://github.com/openai/codex/pull/29249)** *(open, code‑reviewed)*  
   Adds a typed, replayable representation of environment context (first slice of the model world‑state). Integrates with existing initial‑context and settings‑diff paths.

3. **[#29255 – Add configurable token budget compaction reminder](https://github.com/openai/codex/pull/29255)** *(closed)*  
   Introduces a model‑visible prompt before automatic context compaction, giving the agent a chance to wrap up. Addresses feedback that compaction is too abrupt.

4. **[#29259 – Prototype `mcp_history` thread hint injection](https://github.com/openai/codex/pull/29259)** *(closed)*  
   Explores injecting thread hints from MCP history into the initial context without requiring a model tool call – a step toward context‑aware session resumption.

5. **[#28806 – Optimize resume and fork history](https://github.com/openai/codex/pull/28806)** *(open)*  
   Checkpoint‑backed `thread/resume` and copy‑on‑write `thread/fork` dramatically reduce cold history work while preserving fallback for legacy sessions.

6. **[#28232 – Add workspace headline statusline item](https://github.com/openai/codex/pull/28232)** *(open)*  
   New TUI status‑line component showing the active workspace headline, refreshed every 10 seconds. Useful for team‑admin announcements.

7. **[#29001 – Add workspace messages app‑server API](https://github.com/openai/codex/pull/29001)** *(open)*  
   Backend API support for reading/sending workspace‑level messages (e.g., admin broadcasts). Feature‑gated; maps backend 404 to “feature not available”.

8. **[#28801 – Improve thread list and resume RPC paths](https://github.com/openai/codex/pull/28801)** *(open)*  
   Adds a SQLite‑optimized `thread/list` path that reads only list‑relevant fields. Reduces overhead for large thread histories.

9. **[#28366 – Forward app link IDs in approval elicitations](https://github.com/openai/codex/pull/28366)** *(open, code‑reviewed)*  
   Small but important fix: ensures `link_id` is passed in approval requests so desktop approvals can trace back to the exact MCP tool call.

10. **[#26229 – Add protected data mode to core and app server](https://github.com/openai/codex/pull/26229)** *(closed)*  
    Implements core‑owned Protected Data Mode: MCP tool results can mark data as protected, forcing explicit user approval before sending to the model. Merged after several weeks of review.

---

## Feature Request Trends

- **Exclusion of sensitive files** (#2847, plus related issues like #29117 on Windows permission spam): The community continues to request a robust `.codexignore`‑like mechanism to prevent accidental exposure of secrets, credentials, or large dependency trees.
- **Cross‑thread orchestration and event‑driven wake** (#14923, #20312, #15299, #15355): Multiple open issues ask for APIs to launch child threads, pass contexts between agents, and wake idle sessions on external events (file changes, MCP resource pushes, chat mentions).
- **Integration with external communication platforms** (#21166 Telegram, #20475 Slack, #11820 ChatGPT mobile notifications): Developers want Codex agents to receive and respond to messages from chat apps, not just terminal / IDE input.
- **Workspace/context isolation** (#25319 VS Code workspace scoping, #23489 TUI composer background): Users request per‑project thread history and better remote‑terminal compatibility.

---

## Developer Pain Points

1. **`sandboxPolicy` metadata bug** – The single biggest pain point today: a missing field in `codex/sandbox-state-meta` breaks every MCP tool that depends on node_repl. Affects macOS and Windows (mirrored issues #29189, #29193, #29205, #29215, #29219, #29242, #29251). Many duplicates suggest the community quickly identified the regression.
2. **Rate‑limit / cost explosion** – Issue #28879 shows a 10–20× jump in per‑token cost since June 16, draining Plus budgets in 2–3 prompts. No official acknowledgment yet.
3. **Connection reliability** – #18960 (reconnect loop) and #22898 (mobile offline state) point to fragile WebSocket and pairing logic.
4. **Windows‑specific sandbox and ACL failures** – Beyond the sandboxPolicy bug, issues like #28248 (ACLs broken after power outage), #29200 (setup dialog on every `apply_patch`), and #29117 (repeated permission prompts) indicate Windows sandbox stability is behind macOS.
5. **CLI crashes** – #29000 reports SIGTRAP on Intel macOS, and #29223 notes missing `codex_app` tools in 0.142.0‑alpha.1. Developers on non‑Apple Silicon hardware and cutting‑edge builds are hit hardest.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*