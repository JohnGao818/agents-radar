# OpenClaw Ecosystem Digest 2026-06-18

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-18 03:33 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-18

## 1. Today’s Overview

Activity remains very high: 500 issues and 500 pull requests were updated in the last 24 hours. Of those, 20 issues were closed and 90 PRs were merged or closed, indicating a healthy rate of resolution. No new releases were published today. The project shows strong community engagement with numerous high-discussion issues, but a large backlog of open items (480 open issues, 410 open PRs) suggests maintainer bandwidth is stretched. Security, session-state integrity, and message-loss bugs continue to dominate the most active threads.

## 2. Releases

No new releases today.

## 3. Project Progress

Ninety PRs were merged or closed in the last 24 hours. Notable examples among the top-scored PRs include:

- **fix(agents): parallelize MCP server connections in bundle-tools** (#94382, closed) — reduces session startup latency by connecting MCP servers concurrently instead of sequentially.
- **fix(gateway): strip oversized config payload from config.get tool result details** (#94392, open but probably soon merged) — prevents 100KB middleware limit violations.
- **fix(compaction): increase compaction retry aggregate timeout from 60s to 300s for large sessions** (#94403, open) — accommodates ~200K token sessions where model calls take >60s.
- **fix(sandbox): pre-create materialized skills directory to avoid root:root ownership** (#94395, open) — resolves Docker permission issues.
- **fix(cli): reject present-but-invalid --timeout on status/health fast path** (#92996, open) — corrects CLI command-line argument handling.

Several smaller fixes landed for Telegram, Matrix, outbound channel plugins, memory-search config, and TUI display.

## 4. Community Hot Topics

The following issues and PRs have generated the most discussion and reactions:

- **#25592 – Text between tool calls leaks to messaging channels** (32 comments, P1, security)  
  A critical UX and security problem where internal agent processing output (error handling, narration) appears in Slack/iMessage. The issue carries high-impact labels: security, message-loss. No associated fix PR yet.  
  [Issue #25592](https://github.com/openclaw/openclaw/issues/25592)

- **#88838 – Track core session/transcript SQLite migration via accessor seam** (30 comments, P0)  
  A strategic tracking issue for a branch-by-abstraction migration to SQLite for session state. This is the highest-priority item (P0) and reflects a major architectural effort to avoid a high-risk rewrite.  
  [Issue #88838](https://github.com/openclaw/openclaw/issues/88838)

- **#9443 – Request: Prebuilt Android APK releases** (25 comments, P2)  
  User requests prebuilt APK for the Android companion app. No action taken since February; still open and maintainer-reviewed.  
  [Issue #9443](https://github.com/openclaw/openclaw/issues/9443)

- **#32473 – Control UI requires device identity (use HTTPS or localhost)** (17 comments, 5👍, P2)  
  Regression where control UI fails on remote hosts without HTTPS. High engagement suggests many users affected.  
  [Issue #32473](https://github.com/openclaw/openclaw/issues/32473)

- **#22676 – Signal daemon stop() race condition on SIGUSR1 restart** (17 comments, P1)  
  Process management bug causing orphaned processes and send failures. Linked PR open (#?).  
  [Issue #22676](https://github.com/openclaw/openclaw/issues/22676)

- **#22438 – Tiered bootstrap file loading** (17 comments, P2)  
  Enhancement to reduce LLM token waste by loading bootstrap files per context. Strong community interest.  
  [Issue #22438](https://github.com/openclaw/openclaw/issues/22438)

Underlying needs span three major themes: **security/privacy** (message leaks, credential exposure), **session reliability** (migration, routing, process management), and **usability gaps** (APK builds, onboarding, configuration complexity).

## 5. Bugs & Stability

Several critical and high-priority bugs were reported or updated today. They are ranked by severity:

| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| **P0** | [#88838](https://github.com/openclaw/openclaw/issues/88838) | Session/transcript SQLite migration (tracking issue – not a bug per se but highest priority) | N/A (tracking) |
| **P1** | [#25592](https://github.com/openclaw/openclaw/issues/25592) | Text between tool calls leaks to messaging channels (security, message loss) | No |
| **P1** | [#22676](https://github.com/openclaw/openclaw/issues/22676) | Signal daemon stop() race condition – orphaned processes, send failures | Yes (linked PR open) |
| **P1** | [#29387](https://github.com/openclaw/openclaw/issues/29387) | Bootstrap files in agentDir silently ignored (session-state, security) | No |
| **P1** | [#31331](https://github.com/openclaw/openclaw/issues/31331) | Docker + Sandbox cannot workspaceAccess at all (security, session-state) | No |
| **P1** | [#38327](https://github.com/openclaw/openclaw/issues/38327) | "Cannot convert undefined or null to object" with google-vertex/gemini-3.1-pro-preview | No |
| **P1** | [#41165](https://github.com/openclaw/openclaw/issues/41165) | Telegram DMs still routed to agent:main:main after fix (message-loss) | Yes (linked PR open) |
| **P1** | [#41744](https://github.com/openclaw/openclaw/issues/41744) | Feishu read image tool loses media before final outbound payload | Yes (linked PR open) |
| **P1** | [#86215](https://github.com/openclaw/openclaw/issues/86215) | Codex OAuth refresh failures can wedge agent for hours (session-state, message-loss) | No |
| **P1** | [#39476](https://github.com/openclaw/openclaw/issues/39476) | A2A sessions_send creates duplicate messages (session-state, message-loss) | Yes (linked PR open) |
| **P1** | [#31583](https://github.com/openclaw/openclaw/issues/31583) | `exec` tool does not inherit `skills.entries.*.env` environment variables | No |
| **P2** | [#43747](https://github.com/openclaw/openclaw/issues/43747) | Memory management chaos – inconsistent chunking and storage across users | No |
| **P2** | [#41201](https://github.com/openclaw/openclaw/issues/41201) | Control UI avatar broken image (regression) | No |

A regression pattern is evident: several bugs were introduced in recent updates (e.g., #32473, #38327, #41201, #31583), suggesting test coverage or CI gaps.

## 6. Feature Requests & Roadmap Signals

The following user-requested features have high engagement and align with ongoing project themes:

- **Tiered bootstrap file loading** (#22438) – likely to land soon given its 17 comments and product-decision labels.
- **Masked secrets** (#10659) – addresses a core security need; multiple security-related issues reference this.
- **Configurable streaming watchdog timeout** (#68596) – 8👍, P2 – many users with reasoning models are affected.
- **Slack Block Kit support** (#12602) – 0👍 but active discussion; important for enterprise use.
- **Per-agent cost budget enforcement** (#42475) – operational necessity for multi-tenant deployments.
- **Session snapshots (save/load)** (#13700) – 0👍 but discussed; could become a major quality-of-life feature.
- **Pre-response enforcement hooks** (#13583) – 2👍, for high-stakes workflows (finance, security).
- **Post-subagent completion extension hook** (#22358) – 1👍, useful for trajectory logging.
- **Distributed Agent Runtime** (#42026) – 3👍, ambitious RFC to split gateway and runtime.

**Prediction for next minor release (2026.4.x):** Given the activity around bootstrapping, session migration, and compaction, expect the SQLite migration tracking (#88838) to produce the first PRs, along with possible inclusion of tiered bootstrap and masked secrets if maintainer resources allow.

## 7. User Feedback Summary

- **Pain Points (most frequently reported):**
  - *Security/Leakage: Agents leaking internal processing text to public channels (#25592, #29387, #10659).*
  - *Session Reliability: Memory inconsistencies (#43747), bootstrap files ignored (#29387), OAuth refresh hangs (#86215), duplicate messages in A2A (#39476).*
  - *Deployment friction: No prebuilt Android APK (#9443), missing memory setup in onboarding wizard (#16670), broken control UI on non-localhost (#32473), Docker sandbox issues (#31331).*
  - *Performance: Tool schema token overhead (~3500 tok/session, #14785), streaming watchdog timeouts (#68596).*

- **Use Cases:**
  - Multi-agent group chats with natural-language rule learning (#41366).
  - CRM summaries and database queries via Slack Block Kit (#12602).
  - Session state preservation across `/new` resets (#40418) and branch conversations (#13700).
  - Backup/restore for environment migration (#13616, #40786).
  - Global-scale deployment via AWS (#13597) and distributed architecture (#42026).

- **Satisfaction Indicators:**
  - Users express frustration with regressions and missing core features, but the volume of high-quality feature requests (some with RFCs) demonstrates strong investment in the project.
  - The high number of 👍 on bug reports (e.g., #32473 with 5👍, #29387 with 5👍) indicates many users share the same issues.

## 8. Backlog Watch

The following high-importance issues and PRs have been open for an extended period without clear maintainer action or are stuck in review/pending:

| Item | Created | Comments | Status | Notes |
|------|---------|----------|--------|-------|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) Text leakage | Feb 24 | 32 | Needs maintainer review, security review, product decision | No fix PR; one of the most discussed issues overall. |
| [#9443](https://github.com/openclaw/openclaw/issues/9443) Android APK | Feb 5 | 25 | Needs maintainer review, product decision | Stale for months; user expectations unmet. |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) Masked secrets | Feb 6 | 13 | Needs maintainer review, security review | Essential for security; no movement. |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) Memory trust tagging | Feb 3 | 12 | Needs product decision, security review | Unresolved for 4.5 months. |
| [#6731](https://github.com/openclaw/openclaw/issues/6731) Safe/unsafe ClawdBot | Feb 2 | 12 | Needs security review | Ambitious proposal with no traction. |
| [#41375](https://github.com/openclaw/openclaw/pull/41375) fix(hooks): deliver internal hook replies | Mar 9 | — | Waiting on author, needs real behavior proof | PR from March still pending author response. |
| [#41299](https://github.com/openclaw/openclaw/pull/41299) fix: add separator between metadata and user message | Mar 9 | — | Needs proof, merge-risk labels | Stale; affects message parsing. |
| [#41067](https://github.com/openclaw/openclaw/pull/41067) Fix dashboard chat recovery | Mar 9 | — | Needs proof, high risk labels | Critical for web UI; stalled. |
| [#40874](https://github.com/openclaw/openclaw/pull/40874) iOS Liquid Glass UI | Mar 9 | — | Waiting on author, proof: screenshot | Feature PR with no recent activity. |
| [#40782](https://github.com/openclaw/openclaw/pull/40782) fix(feishu): use union_id for @mention | Mar 9 | — | Automerge armed but still open | Despite automerge label, hasn’t merged. |
| [#11665](https://github.com/openclaw/openclaw/issues/11665) Webhook hook sessions multi-turn | Feb 8 | 8 | Needs product decision, security review | Documented feature doesn’t work. |
| [#13751](https://github.com/openclaw/openclaw/issues/13751) Feishu plugin permissions | Feb 11 | 6 | Needs security review, P1 | High severity but no resolution in 4+ months. |

These items represent either **security-critical gaps**, **core feature regressions**, or **long-standing enhancement requests**

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## 1. Ecosystem Overview
The personal AI assistant open‑source landscape is maturing rapidly, with two major reference implementations—OpenClaw and Hermes Agent—driving innovation in agent runtime, messaging gateway, and desktop user experience. Both projects exhibit intense community activity, with hundreds of issues and PRs updated daily. The dominant themes across the ecosystem are security (preventing internal processing leaks to public channels), session reliability (state persistence, OAuth stability), and deployment flexibility (prebuilt mobile apps, remote client‑only setups). Interoperability standards like MCP and A2A are becoming critical differentiators, while architectural migrations (e.g., SQLite for session state) signal a shift toward more robust, maintainable foundations.

## 2. Activity Comparison

| Project      | Issues Updated (24h) | Issues Open | PRs Updated (24h) | PRs Open | Latest Release | Health Score* |
|--------------|-----------------------|-------------|-------------------|----------|----------------|--------------|
| **OpenClaw** | 500                   | 480         | 500               | 410      | None today     | **Moderate** – high velocity but large backlog; maintainer bandwidth stretched |
| **Hermes Agent** | 50                 | 46          | 50                | 47       | None today     | **Good** – responsive triage, smaller backlog, active feature development |

*Health Score combines throughput, resolution rate, and backlog depth. OpenClaw resolves ~18% of PRs daily, Hermes ~6%, but Hermes has a much lower absolute backlog.

## 3. OpenClaw’s Position
**Advantages:** OpenClaw operates at an order‑of‑magnitude larger scale (500 vs 50 issues/PRs updated daily), indicating a broader contributor base and more extensive deployment surface. Its focus on session‑state integrity (SQLite migration, compaction timeouts) and message‑loss prevention positions it as the more enterprise‑grade reference implementation for high‑reliability agent backends. The project also addresses critical security issues like text leakage between tool calls (#25592) and credential exposure (#10659), which are fundamental to trust in multi‑channel deployments.

**Technical approach differences:** OpenClaw emphasizes core runtime architecture (parallel MCP connections, oversized payload stripping, Docker sandbox fixes) over end‑user features. Hermes Agent invests more in desktop UX (system tray, Kanban board, electron builds) and interoperability (A2A, LUMEN binary protocol, OTLP observability). OpenClaw’s community is larger but also more burdened by a backlog of 480 open issues and 410 open PRs, which may delay roadmap items like the SQLite migration.

## 4. Shared Technical Focus Areas
Both projects are converging on several critical requirements:

| Focus Area | OpenClaw Evidence | Hermes Agent Evidence |
|------------|-------------------|------------------------|
| **Session reliability & state persistence** | SQLite migration (#88838 P0), compaction timeout increase (#94403), message‑loss bugs (#25592, #39476) | Session ↔ workspace binding (#48190), vision fallback chain broken (#27555), “Summarizing thread” stale status (#48098) |
| **Security & privacy** | Text leakage to messaging channels (#25592), credential exposure (#10659), bootstrap files ignored (#29387) | Disabled memory tools can be bypassed (#48181), agent modifies own skills (#32497), OAuth billing header missing (#48176) |
| **Deployment friction** | Android APK requests (#9443), Docker sandbox issues (#31331), control UI broken on remote hosts (#32473) | Windows installer fails (#46260), desktop build cache invalidation (#47917), custom endpoint onboarding hard‑fails (#47006) |
| **Interoperability (MCP / A2A)** | MCP server connection parallelization (#94382), A2A sessions duplicate messages (#39476) | A2A protocol support (#514, most upvoted), LUMEN binary MCP transport (#47740) |
| **Observability & monitoring** | Config streaming watchdog timeout (#68596) | OTLP observability plugin (#48184), install‑method stamping for Docker (#48188) |

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary focus** | Core agent runtime, gateway, session state integrity | Desktop experience, user‑facing features, interoperability protocols |
| **Target users** | Developers, system administrators, self‑hosters | End‑users, desktop power users, multi‑channel (WhatsApp, Discord) enthusiasts |
| **Architecture philosophy** | Monolithic reference with SQLite migration in progress; strong emphasis on security hardening and bug fixing | Modular with many third‑party plugins (OTLP, LUMEN, new skills); rapid feature iteration alongside bug fixes |
| **Community engagement style** | High issue volume with many “stuck” items needing maintainer attention; lower per‑issue comment depth | Higher per‑issue engagement (e.g., #514 with 22 comments, 18 👍); maintainers respond quickly with same‑day fix PRs |
| **Release cadence** | No recent release; large backlog suggests next release may be delayed | No recent release but steady PR flow indicates active development toward next version |
| **Notable strengths** | Enterprise‑grade session management, broad language support (Telegram, Matrix, Feishu) | Desktop native features (tray, Kanban, OTLP), cutting‑edge protocols (A2A, LUMEN) |

## 6. Community Momentum & Maturity
- **Tier 1 – Rapid iteration with scaling pains:** OpenClaw sees intense activity but struggles with maintainer throughput. 480 open issues and 410 open PRs, coupled with critical P0/P1 bugs lacking fix PRs (#25592, #29387), suggest the project is in a *growth phase* where core infrastructure improvements (SQLite migration) are needed to stabilize.
- **Tier 2 – Sustainable feature‑driven development:** Hermes Agent exhibits a healthier issue‑to‑maintainer ratio. Despite a smaller absolute number of contributions, its triage is prompt (fix PRs created same day for many bugs), and feature requests like A2A receive strong community backing. The project appears to be *stabilizing* while introducing ambitious new capabilities.
- **Stabilizing signals:** Both projects have no new releases today, but Hermes shows more forward‑looking feature PRs (LUMEN, OTLP, new skills). OpenClaw is still heavily in bug‑fix mode.

## 7. Trend Signals
- **Security as table stakes:** The high volume of security‑labeled issues (leakage, credential exposure, tool bypass) indicates that internal agent processing must never be visible to external channels. This is a non‑negotiable requirement for production deployments.
- **Interoperability is the next frontier:** A2A protocol support is the most upvoted feature across both ecosystems. Developers expect agents to communicate and coordinate autonomously, not just via MCP tool calls. LUMEN binary compression further suggests performance‑sensitive multi‑agent setups are coming.
- **Desktop client‑only architecture emerges:** Hermes Agent’s #38602 (18 👍) and OpenClaw’s prebuilt APK demand (#9443) signal a shift from all‑in‑one agents to separable frontends. Users want a thin client that connects to a remote runtime—critical for cloud, corporate, or low‑resource environments.
- **Observability becomes bundled:** OpenTelemetry plugins and streaming watchdog timeouts show that operators need visibility into agent behavior, especially for long‑running reasoning sessions. This will likely become a standard requirement for any agent platform.
- **Session persistence is a universal pain:** Both projects have multiple issues around memory inconsistencies, bootstrap files being ignored, and state loss. Users expect agents to remember context reliably across resets and restarts—a foundational capability that is still being hardened.
- **Value for AI agent developers:** Those building on either ecosystem should prioritize security hardening (leak prevention, credential masking) and session reliability (persistent state, compaction) before adding features. Investing in interoperability (MCP, A2A) and observability will future‑proof integrations. Desktop and mobile deployment flexibility is essential for user adoption beyond developer sandboxes.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-18

## Today’s Overview

Hermes Agent saw very high activity on June 18, with 50 issues and 50 pull requests updated in the last 24 hours. Of these, 46 issues remain open and 4 were closed; on the PR side, 47 are open and 3 merged/closed. New issue creation and PR submission are both intense, indicating an active community and responsive development cycle. No new releases were published today, but the sustained feature and bug-fixing effort suggests a solid pipeline toward the next version.

## Releases

*No new releases today.*  
*Latest stable remains the previous version (not specified in data).*

## Project Progress

Three pull requests were merged or closed today:

- **PR #43051** – [fix(approval): honor glob command allowlist entries](https://github.com/NousResearch/hermes-agent/pull/43051)  
  *Closed.* Ensures manual `command_allowlist` entries are matched as text patterns (including globs like `podman *`) for permanent approvals.

- **PR #48084** – [bug(desktop): `electronDist` path mismatch](https://github.com/NousResearch/hermes-agent/pull/48084)  
  *Closed as duplicate.* Desktop build path issue already covered by #47276.

- **PR #48149** – [Bug: gh CLI authentication fails with 401/Blocked](https://github.com/NousResearch/hermes-agent/pull/48149)  
  *Closed.* Environment variable authentication issue resolved.

Additionally, several open PRs show meaningful feature progress:
- **PR #48184** – OTLP observability plugin (OpenTelemetry) added as third bundled plugin.
- **PR #47740** – LUMEN binary protocol transport for MCP servers (32–80% wire compression).
- **PR #47576** – Four new optional skills: graphify, ui-ux-pro-max, impl-validator, suede-promo.
- **PR #48180** – Linux `computer_use` backend added.
- **PR #47140** – Z.AI GLM Coding Plan provider with `glm-5.2` model.

## Community Hot Topics

Four issues stand out for high comment counts and/or reaction volume:

1. **Issue #514** ([A2A Protocol Support](https://github.com/NousResearch/hermes-agent/issues/514))  
   *22 comments, 18 👍* – Long-running feature request for Google’s Agent-to-Agent protocol. The community strongly desires inter-agent discovery and communication (complementary to MCP). This remains the most upvoted open feature.

2. **Issue #38602** ([Desktop Client-Only Installation](https://github.com/NousResearch/hermes-agent/issues/38602))  
   *6 comments, 18 👍* – Users want a thin-client desktop app that connects to a remote Hermes runtime, not bootstrapping a local agent. High reaction count indicates broad need.

3. **Issue #47917** ([Desktop build fails after update](https://github.com/NousResearch/hermes-agent/issues/47917))  
   *8 comments* – Electron binary cache invalidation causing build failures on subsequent updates. Affects Windows/macOS users who rely on the desktop app.

4. **Issue #27555** ([Vision fallback_chain silently broken](https://github.com/NousResearch/hermes-agent/issues/27555))  
   *7 comments* – P1 bug: `_resolve_single_provider` passes wrong kwargs, making the entire vision fallback chain return `None` without any error message.

**Underlying needs:**  
- **Interoperability** – A2A (and related standards) is a top request; users want agents to cooperate seamlessly.  
- **Deployment flexibility** – Remote client-only setups for corporate or cloud-hosted Hermes instances.  
- **Stability** – Desktop build reliability is a persistent pain point.  
- **Transparency** – Silent failures (like the vision bug) erode trust; users want clear error reporting.

## Bugs & Stability

### P1 — Critical

| Issue | Description | Status |
|-------|-------------|--------|
| [#27555](https://github.com/NousResearch/hermes-agent/issues/27555) | Vision fallback chain is silently broken (wrong kwargs) | Open, no fix PR yet |
| [#48176](https://github.com/NousResearch/hermes-agent/issues/48176) | Anthropic OAuth requests rejected HTTP 400 (missing billing header) | Open, **PR #48177** provides fix |

### P2 — High

| Issue | Description | Fix PR |
|-------|-------------|--------|
| [#47917](https://github.com/NousResearch/hermes-agent/issues/47917) | Desktop build fails after update (electronDist cache) | None yet |
| [#46260](https://github.com/NousResearch/hermes-agent/issues/46260) | Windows installer fails at desktop stage (npm install exit code 1) | None yet |
| [#32497](https://github.com/NousResearch/hermes-agent/issues/32497) | Agent modifies its own skills/system prompts during unrelated tasks | None yet |
| [#48181](https://github.com/NousResearch/hermes-agent/issues/48181) | Security: disabled `memory` toolsets can be bypassed via late injection | None yet |
| [#48167](https://github.com/NousResearch/hermes-agent/issues/48167) | Gateway GUI start button does nothing (CLI works) | None yet |
| [#48161](https://github.com/NousResearch/hermes-agent/issues/48161) | Chinese IME input not displayed until next keypress (Windows) | None yet |
| [#48150](https://github.com/NousResearch/hermes-agent/issues/48150) | `strip_markdown` eats Markdown bullet lists and asterisks (plain text gateways) | None yet |
| [#48133](https://github.com/NousResearch/hermes-agent/issues/48133) | Gateway timestamp strip fails on Windows multi-word timezone names | None yet |

### P3 — Moderate

- [#47006](https://github.com/NousResearch/hermes-agent/issues/47006) – Custom-endpoint onboarding wizard hard-fails on endpoints not exposing `/v1/models` (e.g., Cohere).
- [#41808](https://github.com/NousResearch/hermes-agent/issues/41808) – Dashboard Chat tab React error #301 (maximum update depth) on Tailscale IP connections.
- [#40692](https://github.com/NousResearch/hermes-agent/issues/40692) – macOS Desktop composer becomes extremely laggy after 30+ exchanges.
- [#48098](https://github.com/NousResearch/hermes-agent/issues/48098) – Desktop keeps showing stale “Summarizing thread” status after compaction resumes.

**Today’s fix PRs for reported bugs:**  
- [#48177](https://github.com/NousResearch/hermes-agent/pull/48177) – Sends Claude Code billing-attribution block on OAuth requests (fixes #48176).  
- [#48186](https://github.com/NousResearch/hermes-agent/pull/48186) – Fixes WSL clipboard paste (image detection failure).  
- [#48185](https://github.com/NousResearch/hermes-agent/pull/48185) – Detects macOS app-bundle Chrome for browser availability gate.  
- [#48178](https://github.com/NousResearch/hermes-agent/pull/48178) – XML-escapes launchd plist values to prevent format string injection.  
- [#48188](https://github.com/NousResearch/hermes-agent/pull/48188) – Scopes install-method stamp to code tree, fixing Docker + host shared config updates.  
- [#48145](https://github.com/NousResearch/hermes-agent/pull/48145) – Strips `_comment` keys from ComfyUI workflows to avoid HTTP 500.  

## Feature Requests & Roadmap Signals

### High Community Interest (likely next version)

- **A2A Protocol Support** ([#514](https://github.com/NousResearch/hermes-agent/issues/514)) – Most upvoted feature; groundwork may already be in progress.  
- **Desktop Client-Only Installation** ([#38602](https://github.com/NousResearch/hermes-agent/issues/38602)) – 18 👍; would enable remote Hermes setups.  
- **System Tray Support** ([PR #48163](https://github.com/NousResearch/hermes-agent/pull/48163)) – Close to tray instead of quit (Windows/Linux).  
- **Kanban Board View in Desktop** ([#48159](https://github.com/NousResearch/hermes-agent/issues/48159)) – Already exists in web UI and CLI; missing from Electron app.  
- **Session ↔ Workspace Binding** ([#48190](https://github.com/NousResearch/hermes-agent/issues/48190)) – Record cwd, repo, and restore on resume.  
- **OTLP Observability Plugin** ([PR #48184](https://github.com/NousResearch/hermes-agent/pull/48184)) – Third observability plugin (OpenTelemetry) added today.  
- **LUMEN Binary Protocol for MCP** ([PR #47740](https://github.com/NousResearch/hermes-agent/pull/47740)) – 32–80% compression, multi-agent sharing.

### Additional Signals

- **CLI Auto-Queue Mode** ([#13072](https://github.com/NousResearch/hermes-agent/issues/13072)) – Smart interrupt and crash recovery in `hermes chat`.  
- **OpenAI Responses API verbosity** ([#20203](https://github.com/NousResearch/hermes-agent/issues/20203)) – Control terse vs. expansive responses.  
- **Desktop Command Center for Gateway** ([#48189](https://github.com/NousResearch/hermes-agent/issues/48189)) – Start/Stop/Install buttons for messaging gateway.  
- **Per-subagent model overrides** ([PR #12794](https://github.com/NousResearch/hermes-agent/pull/12794)) – Allows routing individual subagents with different models.  
- **Z.AI GLM Coding Plan provider** ([PR #47140](https://github.com/NousResearch/hermes-agent/pull/47140)) – New provider and model (`glm-5.2`).

## User Feedback Summary

**Pain Points (explicit or inferred):**  
- Windows installation continues to be problematic: `npm install` errors, “Access Denied” on auto-update, Chinese IME input lag.  
- Desktop build reliability is fragile – Electron cache invalidation after updates frustrates developers.  
- Silent failures (vision fallback, Markdown stripping) lead to hard-to-debug issues.  
- Custom endpoint onboarding is too restrictive – many SaaS endpoints don’t expose `/v1/models`.  
- Agent self-modification of skills (**#32497**) is a major trust concern for power users.  
- Gateway GUI “Start” button not working for some users (Windows, specific network conditions).  

**Satisfaction Indicators:**  
- Rapid community engagement on feature requests (A2A, client-only desktop) with many 👍 and constructive comments.  
- Users are actively contributing PRs for new capabilities (OTLP, LUMEN, system tray, new skills).  
- Issues are being triaged and responded to promptly (many with maintainer labels, fix PRs created same day).  

**Use Cases Highlighted:**  
- Multi-channel Discord with separate personas per channel (**#48175**).  
- WhatsApp group sending via Hermes Skill on Termux (**#47477**).  
- Remote Hermes usage via Tailscale/limited networks.  
- Docker-backed gateways sharing config with macOS Desktop host.  

## Backlog Watch

Issues and PRs that are important but have been open for a while without a resolution:

| Item | Created | Last Updated | Notes |
|------|---------|--------------|-------|
| [#514](https://github.com/NousResearch/hermes-agent/issues/514) | 2026-03-06 | 2026-06-17 | A2A protocol – most upvoted, no maintainer assignment visible. Needs prioritization. |
| [#8359](https://github.com/NousResearch/hermes-agent/issues/8359) | 202

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*