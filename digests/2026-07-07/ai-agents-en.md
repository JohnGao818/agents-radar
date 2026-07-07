# OpenClaw Ecosystem Digest 2026-07-07

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-07 02:42 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-07-07

## 1. Today's Overview
The project remains in a high-activity state with **500 issues and 500 pull requests updated in the last 24 hours**. Among them, **398 issues are open/active** and **102 are closed**, while **298 PRs are open** and **202 have been merged or closed**. No new releases were published today. The community is deeply engaged in both bug triage and feature discussion, with several long-standing high-priority items (#75, #25592) continuing to attract heavy commentary. Patch contributions are flowing steadily, addressing regressions, platform gaps, and infrastructure hardening.

## 2. Releases
No new releases today.

## 3. Project Progress
In the last 24 hours **202 pull requests were merged or closed**. Notable advances include:

- **Anthropic thinking budget fix** – PR [#101283](https://github.com/openclaw/openclaw/pull/101283) ensures explicit `thinkingBudgetTokens: 0` disables thinking instead of being overridden by default 1024.
- **Temp workspace security fix** – PR [#101246](https://github.com/openclaw/openclaw/pull/101246) fixes a `/tmp` permission corruption issue (`0o1777` → `0o0700`) during `skills install/update`.
- **CJK-friendly emphasis parsing** – PR [#101229](https://github.com/openclaw/openclaw/pull/101229) improves bold/italic rendering for Chinese, Japanese, and Korean text across all channels.
- **Codex app-server floor raised** – PR [#101221](https://github.com/openclaw/openclaw/pull/101221) bumps the minimum Codex app-server version to `0.142.5`, removes dead compat code, and fixes deferred sub-agent steering.
- **Discord outbound delivery resilience** – PR [#101024](https://github.com/openclaw/openclaw/pull/101024) clears recovery state on connect-phase errors, preventing permanent message drops after network outages.
- **Android CI reform** – PR [#101275](https://github.com/openclaw/openclaw/pull/101275) enables `ktlintCheck` to prevent formatting drift on Android code.
- **SSRF guard for OpenAI Realtime** – PR [#86526](https://github.com/openclaw/openclaw/pull/86526) adds fake-IP range handling for proxy stacks like Clash/Surge.

## 4. Community Hot Topics
The most active issues by comment count (≥25 comments) reveal key areas of community concern:

- **Issue #75** (110 comments) – [Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75). Users continue to demand first-class desktop support for non-macOS platforms. The 81 👍 reactions underscore broad interest.
- **Issue #25592** (33 comments) – [Text between tool calls leaks to messaging channels](https://github.com/openclaw/openclaw/issues/25592). A diamond-lobster-rated security / UX bug: internal processing text (errors, acknowledgements) is broadcast to Slack, iMessage, etc. No fix PR linked yet, but the community is actively discussing scoping.
- **Issue #9443** (27 comments, closed) – [Prebuilt Android APK releases](https://github.com/openclaw/openclaw/issues/9443). Closed, but the desire for easy Android installs remains a recurring theme.
- **Issue #98416** (20 comments, closed) – [v2026.6.11 missing reentrancy guard in published dist](https://github.com/openclaw/openclaw/issues/98416). The missing commit `d2da8c79d9` caused session initialization conflicts; now fixed.

Other heavily discussed topics include:
- **Tiered bootstrap loading** (#22438, 17 comments) – progressive context control to save tokens.
- **Signal daemon race condition** (#22676, 17 comments) – orphaned processes on restart.
- **Per-agent memory-wiki vaults** (#63829, 12 comments) – multi-agent isolation for knowledge stores.
- **Allow private network access** (#39604, 13 comments) – opt-in `web_fetch` to reach internal addresses.

## 5. Bugs & Stability
Several critical and high-severity bugs remain open or were discussed today:

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#43661](https://github.com/openclaw/openclaw/issues/43661) | **P0** | Session hangs when compaction times out, causing duplicate message sends. No recovery. | No linked PR |
| [#98416](https://github.com/openclaw/openclaw/issues/98416) | P1 (closed) | Missing reentrancy guard in `v2026.6.11` – `commitReplySessionInitialization` conflict. | Fixed (commit present in source) |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) | **P1** | Signal daemon race on SIGUSR1: orphaned processes and send failures. | No linked PR |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | **P1** | `"Cannot convert undefined or null to object"` with `google-vertex/gemini-3.1-pro-preview` since v2026.3.2. | No linked PR |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) | **P1** | `exec` tool does not inherit `skills.entries.*.env` – regression. | No linked PR |
| [#43747](https://github.com/openclaw/openclaw/issues/43747) | **P2 (regression)** | Memory management chaos across users – inconsistent chunking/embedding and storage behavior. | No linked PR |
| [#38439](https://github.com/openclaw/openclaw/issues/38439) | **P2 (regression)** | Webchat avatar endpoint `/avatar/{agentId}` returns 404 even with valid `IDENTITY.md`. | No linked PR |
| [#96857](https://github.com/openclaw/openclaw/issues/96857) | Unranked | Tool text outputs degrade to `(see attached image)` placeholders, making the agent blind to normal output. | No linked PR |

Several P1 bugs have no associated fix PR yet, indicating that maintainer attention or product decisions are pending.

## 6. Feature Requests & Roadmap Signals
The community submitted and voted on many feature requests this cycle. Likely candidates for upcoming releases include:

- **Linux/Windows Clawdbot Apps** (#75) – the top-voted request (81 👍). Given sustained interest, a Linux/Win App beta may be on the mid-term roadmap.
- **Per-agent cost budgets** (#42475) – daily/monthly spending caps at gateway level, a common ops need.
- **Tiered bootstrap file loading** (#22438) – to reduce token waste in large workspaces.
- **Per-agent memory-wiki vaults** (#63829) – multi-agent isolation for knowledge.
- **Pre-response enforcement hooks** (#13583) – mandatory tool-call gates for high-stakes workflows.
- **Post-subagent completion hook** (#22358) – automated trajectory logging.
- **Durable natural-language rule learning** (#41366) – persistent rules across sessions and agents.
- **MathJax/LaTeX support in Control UI** (#42840) – academic and scientific users.
- **Distributed agent runtime** (#42026) – split control plane from compute, an ambitious RFC.

The next minor release (2026.7.x) will likely incorporate some of the simpler config-driven features (tiered bootstraps, per-agent budgets) alongside ongoing stability fixes.

## 7. User Feedback Summary
User sentiment is a mix of enthusiasm for the project’s capabilities and frustration with stability and missing platform support:

- **Pain points**: Lack of prebuilt Android APK (#9443), no Linux/Windows apps (#75), message leakage (#25592, #96857), session compaction hang (#43661), memory inconsistency (#43747), avatar regression (#38439), and telegram direct message routing bugs (#41165).
- **Workflow friction**: Users report multi-agent orchestration is unstable (#43367), cron sessions overwrite shared files (#40001), and subagent lifecycle lacks observability (#38626, #43454).
- **Positive signals**: High engagement on feature requests (81 👍 for Linux/Windows, 11 👍 for private network access) suggests a willing and invested user base. The closure of several high-impact bugs (#98416, #9443) indicates the maintainers are responsive to critical issues.

## 8. Backlog Watch
Several important issues and PRs have been open for weeks or months without maintainer assignment or fix progress:

| Item | Age | Priority | Status |
|------|-----|----------|--------|
| [#75](https://github.com/openclaw/openclaw/issues/75) – Linux/Windows Apps | Since 2026-01-01 | P2 (labelled) | Needs maintainer review & product decision; high community demand. |
| [#25592](https://github.com/openclaw/openclaw/issues/25592) – Text leaks to channels | Since 2026-02-24 | P1 | No fix PR; needs security review and product decision. |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) – Signal daemon race | Since 2026-02-21 | P1 | No linked PR; needs maintainer review. |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) – Bootstrap files ignored in agentDir | Since 2026-02-28 | P1 | Needs maintainer review & product decision. |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) – exec tool env inheritance regression | Since 2026-03-02 | P1 | Needs security review and product decision. |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) – Vertex/Gemini null crash | Since 2026-03-06 | P1 (regression) | Needs live repro and maintainer review. |
| [#43661](https://github.com/openclaw/openclaw/issues/43661) – Session compaction hang | Since 2026-03-12 | **P0** | Needs product decision and live repro; critical for stability. |
| [#74131](https://github.com/openclaw/openclaw/pull/74131) – Harden subagent lifecycle | Since 2026-04-29 | P2 | Open PR awaiting maintainer look, despite being ready. |
| [#90239](https://github.com/openclaw/openclaw/pull/90239) – Session history family lookup | Since 2026-06-04 | P2 | Open PR, ready for maintainer, but no review yet. |
| [#95832](https://github.com/openclaw/openclaw/pull/95832) – Twilio voice-call regions IE1/AU1 | Since 2026-06-22 | P2 | Open with sufficient proof, pending maintainer review. |

These items represent the most significant accumulated technical debt and unaddressed user needs. The sheer volume of open issues (398) suggests the maintainer team may be bandwidth-constrained, or that product decisions are blocking many pull requests from merging.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs Hermes Agent
## Personal AI Assistant Open-Source Ecosystem — 2026-07-07

---

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is experiencing a bifurcation between monolithic reference implementations (OpenClaw) and specialized, modular agents (Hermes Agent). Both projects show sustained high activity, with the community increasingly demanding desktop platform parity, provider compatibility, and operational controls like cost budgets and RBAC. The ecosystem is maturing beyond proof-of-concept into production deployment, as evidenced by the volume of bug reports centered on reliability (session hangs, message leaks, cron delivery failures). Interoperability with proprietary API providers and self-hosted backends remains a critical friction point, with both projects investing heavily in provider-specific workarounds. The total combined issue volume (>550 open issues across both projects) suggests maintainer bandwidth is the primary bottleneck to further ecosystem acceleration.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Total Open Issues** | 398 | 36 |
| **Issues Updated (24h)** | 500 | 50 |
| **Open Pull Requests** | 298 | ~50 (est.) |
| **PRs Merged/Closed (24h)** | 202 | 7 |
| **New Releases Today** | 0 | 0 |
| **P0/P1 Open Bugs** | 7 (including 1 P0) | 1 (P3 primary; P1 resolved today) |
| **Longest-Standing Unresolved Issue** | #75 — 188 days (Linux/Windows apps) | #14980 — 74 days (WhatsApp timeout) |
| **Community Engagement Signal** | 81 👍 on #75 (Linux/Windows) | 10 👍 on #42187 (Codex UX, now closed) |
| **Health Score** | **Moderate** — high output but critical stability gaps remain | **Strong** — lower volume but higher fix velocity for P1 issues |

**Observations:**
- OpenClaw operates at ~10× the raw volume of Hermes, but maintains a proportionally larger backlog (398 vs 36 open issues). The 202 PRs merged in 24 hours indicates high merge throughput, but does not fully offset the accumulation rate.
- Hermes resolves P1 bugs quickly (both #59202 and #58818 closed same day), while OpenClaw has 7 P0/P1 bugs without linked fix PRs, several weeks old.
- Hermes shows stronger triage discipline: 14 issues closed in 24h vs 102 for OpenClaw, but against a much smaller base.

---

## 3. OpenClaw's Position

**Advantages vs Peers:**
- **Reference implementation status**: OpenClaw is the "core reference" for the ecosystem, with broader platform coverage (Discord, Signal, Telegram, iMessage, Slack, Webchat, Twilio, Slack, Teams) — likely 2-3× more integrations than Hermes.
- **Larger contributor base**: 500 issues/PRs updated in 24h vs 50 for Hermes suggests a significantly larger development community.
- **CJK emphasis handling** (PR #101229) and **SSRF guard for proxy stacks** (PR #86526) indicate attention to non-English markets and security-hardened deployment, areas where Hermes has less visible investment.

**Technical Approach Differences:**
- OpenClaw appears more **monolithic**: a single repo managing agents, skills, memory management, platform bridges, and build tooling. This creates integration benefits but also cascading regression risks (e.g., #43747 — memory management chaos across users).
- Hermes is more **modular**, with clear boundaries between gateway, agent core, desktop, and provider adapters. This is reflected in Hermes having separate issues for desktop (cross-tab leaks, provider routing) vs core (MoA hanging, cron reliability).

**Community Size Comparison:**
- OpenClaw's issue engagement (110 comments on #75, 33 on #25592) versus Hermes' (11 comments on #527) suggests a community roughly **5-10× larger** by active participation.
- OpenClaw's user base skews toward **enterprise/self-hosters** requesting Linux/Windows apps and cost controls. Hermes' community appears more **hobbyist/NAS-focused** (WhatsApp timeout, Photon iMessage, desktop config issues).

---

## 4. Shared Technical Focus Areas

These requirements are emerging across **both** projects, indicating ecosystem-wide gaps rather than project-specific concerns:

| Requirement | OpenClaw | Hermes Agent |
|-------------|----------|--------------|
| **Desktop platform parity** | #75 — Linux/Windows apps (81 👍) | #59305 — desktop tab leaks; #52401 — macOS cross-profile leak; #58498 — provider routing ignored |
| **Provider compatibility** | #38327 — Vertex/Gemini null crash (P1) | #59386 — strict OpenAI backend HTTP 400; Tencent TokenHub missing models (#59923) |
| **Message leakage / security** | #25592 — internal text leaks to channels (P1) | #52401 — cross-profile data leak; #59925 — ZWJ threat scanner fix |
| **Cron job reliability** | (implied by session compaction #43661) | #59924 — orphan cron processes; #59921 — cron history pruning; #58818 — dropped messages during restart |
| **Memory management** | #43747 — inconsistent chunking across users (P2) | #25061 — pre-turn memory health hook (feature request) |
| **Cost/budget controls** | #42475 — per-agent cost budgets (feature request) | N/A explicitly, but RPM throttling (#7489) addresses cost via rate limits |

**Key Takeaway**: The ecosystem still lacks robust **platform abstraction layers**. Both projects are writing provider-specific workarounds (Tencent, Google Vertex, OpenAI strict mode) rather than treating all backends uniformly. This suggests a market opportunity for a standardized provider compatibility layer or middleware.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary Target User** | Enterprise/advanced self-hoster; multi-agent orchestration at scale | Hobbyist/small-team; single-agent deployments with rich integrations |
| **Core Architecture** | Monolithic — single repository for all components | Modular — separate concerns for gateway, desktop, core, providers |
| **Agent Orchestration** | First-class multi-agent; subagent lifecycle, per-agent vaults (#63829) | Simpler single-agent focus; MoA (Mixture-of-Agents) via delegation |
| **Platform Coverage** | Broad (Discord, Slack, Signal, Telegram, iMessage, Webchat, Twilio) | Focused (Telegram, WhatsApp, Photon iMessage, Desktop, CLI) |
| **Desktop Experience** | None (macOS-only for Clawdbot) — #75 | Dedicated Electron-based desktop app (with i18n, tab management) |
| **Security Framework** | SSRF guards, permission systems, fake-IP handling | MCP OAuth (global state elimination), RBAC proposal (#527), threat scanner |
| **Language/Locale Support** | CJK emphasis rendering (#101229) | 15-language i18n system (#38846) — broader but less deep |
| **Release Cadence** | Frequent (minor releases ~monthly) | Less structured (no releases recorded today) |
| **Community Governance** | Active triage but backlog growing; product decisions blocking PRs | Tighter triage; faster P1 resolution but fewer contributors |

**Strategic Insight**: OpenClaw is the **"generalist platform"** — broader scope, larger community, but suffering from maintainer bandwidth constraints. Hermes is the **"specialist tool"** — more focused UX, faster bug fixes, but smaller integration surface.

---

## 6. Community Momentum & Maturity

### Activity Tiers

**Tier 1: Rapid Iteration — OpenClaw**
- 500 issues/PRs updated daily, 202 PRs merged in 24h
- Critical P0 bug (#43661 — session compaction hang) unresolved for 117 days
- 398 open issues indicates **velocity outpacing capacity** — the project is iterating fast but accumulating debt
- High community enthusiasm (81 👍 for desktop apps) but **frustration visible** in stability complaints

**Tier 2: Steady Maturation — Hermes Agent**
- 50 issues/PRs updated daily, 7 PRs merged
- Fast P1 resolution cycle (issues closed same day as reported)
- 36 open issues is manageable; backlog is modest
- Community engaged but smaller; feature requests are targeted (RBAC, cron UX)

### Maturity Assessment

| Criterion | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **API Stability** | Moderate — regression in `exec` tool env (#31583) | Moderate — provider schema changes cause breakage |
| **Documentation** | Not directly assessed, but closing #9443 (APK) suggests onboarding friction | Not directly assessed |
| **Security Posture** | Evolving — SSRF guard, temp workspace fix, but text leakage (#25592) is serious | Improving — threat scanner, MCP OAuth cleanup, gateway classification |
| **Release Reliability** | Mixed — v2026.6.11 shipped missing reentrancy guard (#98416) | No releases recorded; likely rolling/continuous delivery |

---

## 7. Trend Signals for AI Agent Developers

### From Community Feedback

1. **Provider Divergence is the Top Pain Point**
   Both projects invest heavily in provider-specific workarounds (Vertex, Tencent, OpenAI strict mode, Google Antigravity). This signals that **API uniformity does not exist** even among "OpenAI-compatible" backends. Developers should budget for per-provider testing and abstraction layers.

2. **"Reliability > Features"**
   The highest-voted issues are not about new capabilities but about **stability and completeness**: desktop parity (81 👍), prebuilt binaries, message delivery guarantees. Users are willing to trade features for a system that "just works." The session compaction hang (P0, 117 days unresolved) is a systemic risk for any team relying on OpenClaw.

3. **Multi-Agent is Hard**
   OpenClaw's subagent lifecycle (#43367, #38626, #43454) and Hermes' MoA reference hanging (#59928) indicate that **nested agent calls remain fragile**. Developers should expect race conditions, orphan processes, and observability gaps when orchestrating multiple agents.

4. **Self-Hosters Need Ops Tooling**
   Cost budgets (#42475), RPM throttling (#7489), cron history management (#59921), and job reliability (both projects) point to a **maturation of deployment operations**. AI agents are moving from "cool demo" to "managed service" in the self-hosted context.

5. **Progressive Loading / Token Optimization**
   OpenClaw's tiered bootstrap loading (#22438) and Hermes' memory health hook (#25061) both address **context window efficiency**. As real-world workspaces grow, managing token budgets programmatically (rather than relying on LLM instruction) is becoming essential.

6. **Non-English Markets Matter**
   OpenClaw's CJK fix (#101229) and Hermes' 15-language i18n (#38846) signal that the ecosystem is **globalizing**. Developers who ignore locale-specific rendering (e.g., ZWJ emoji in threat scanners) will encounter community backlash.

7. **Permission Models are Oversimplified**
   Both projects have binary auth models that users find insufficient for family/team deployments. RBAC proposals (Hermes #527) and private network access controls (OpenClaw #39604) suggest the ecosystem is outgrowing the "single user, single agent" paradigm.

### Value for Decision-Makers

- **If scaling to enterprise multi-agent deployments**: OpenClaw offers broader integration and orchestration features, but budget for stability engineering and expect to contribute fixes for P0/P1 bugs.
- **If building a reliable single-agent system**: Hermes Agent provides tighter triage discipline and faster bug resolution, but with a narrower integration surface.
- **For platform/tooling builders**: The provider compatibility pain point is a clear market opportunity. A unified provider abstraction layer (think "LIBS for AI backends") would serve both projects' communities.
- **For contributors**: OpenClaw has a larger surface area for impactful contributions (particularly the stalled P1/P0 bugs), while Hermes has easier onboarding for first-time contributors (trivial fixes like #12232 / IMAP username are 2.5 months stale).

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-07

## Today's Overview

The project is in a **high-activity state** with 50 issues and 50 pull requests updated in the last 24 hours. Of those, 14 issues were closed and 7 PRs were merged or closed, indicating meaningful progress despite the large open backlog (36 open issues remain). No new releases were published today. The community is actively reporting bugs and requesting enhancements, particularly around gateway permissions, provider compatibility, and desktop stability. A cluster of Codex OpenAI auto-compaction notice duplication issues has been resolved, while several P1/P2 bugs in gateway connectivity and cron delivery remain open with ongoing PR fixes.

## Releases

No new releases were recorded on this date.

## Project Progress

**Merged/Closed PRs (7 total today):**

| # | Topic | Summary |
|---|-------|---------|
| #59930 | Kanban substrate hardening | Added periodic integrity re-probes and defense-in-depth for SQLite page corruption (closed, likely merged). |
| (5 additional closed PRs not in top-20 list) | Various fixes | Including bug fixes in gateway shutdown forensics, process group handling, and credential handling. |

Notable open PRs advancing key features include:
- **#59935** – Fix TUI session persistence to avoid stale state DB handles.
- **#59934** – Honor `NO_PROXY` CIDR ranges in agent proxy resolution.
- **#59933** – Recognize official remotes with embedded credentials in update system.
- **#59932** – Clear xterm terminal buffer on `/reset` command in dashboard.
- **#59926** – Add `default=[]` to `delegate_task` schema for strict OpenAI backends (fixing #59386).
- **#59925** – Exempt ZWJ emoji sequences from invisible Unicode flag in threat scanner.
- **#59923** – Add live-fetch for Tencent TokenHub provider models (currently only shows 1 of 58).
- **#59924** – Fix cron orphan processes and error message on script timeout.
- **#59928** – Add timeout to `Future.result()` in MoA reference gathering to prevent indefinite hangs.
- **#59921** – Add CLI commands to prune/clear cron execution history.
- **#59920** – Inherit global proxy config in browser engine.
- **#54325** – Eliminate global `_oauth_port` race condition in MCP OAuth callback flow.
- **#57419** – Classify planned service restarts in gateway to avoid false crash detection.
- **#38846** – Add 15-language i18n system for Desktop UI.

## Community Hot Topics

### Top issues by engagement (comments + reactions):

1. **#527 – Gateway Permission Tiers (Role-Based Access Control)**  
   *11 comments, 6 👍* – Proposes moving from binary auth to tiered permissions (Owner/Admin/User/Guest) for messenger platforms. High community interest in granular control.

2. **#55416 – Photon iMessage: persistent RST_STREAM code 2**  
   *6 comments* – Service outage reported: gRPC stream dies repeatedly after ~90s. P3 severity but critical for users relying on iMessage.

3. **#59386 – `delegate_task` schema causes HTTP 400 on strict OpenAI backends**  
   *5 comments* – Non-retryable crash when using custom provider. Fix PR #59926 already open.

4. **#50530 – Google antigravity legacy integration issues (P2)**  
   *5 comments* – Summarizes three remaining P2 bugs after connectivity fix: sub-agent crashes, forced re-auth, session breakpoints.

5. **#14980 – WhatsApp bridge npm install timeout too short (60s) on container startup**  
   *5 comments, 3 👍* – Affects NAS users; timeout is hardcoded and fails on slower systems.

6. **#42187 – Codex gpt-5.5 autoraise notice shown once per gateway session (CLOSED)**  
   *3 comments, 10 👍* – Highly voted UX improvement; now resolved.

7. **#47241/#46786/#54432 – Codex gpt-5.5 auto-compaction notice duplicates (CLOSED)**  
   Several duplicates all closed today, indicating successful deduplication fix.

### Underlying needs:
- Users want **finer-grained access control** for multi-user gateways (family, teams).
- **Reliability of third-party integrations** (Photon, WhatsApp, Google Antigravity) remains a pain point.
- **Provider compatibility** with strict OpenAI backends is a frequent sticking point.

## Bugs & Stability

### Severe bugs reported today (ranked):

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **P1** | #59202 (CLOSED) | Telegram gateway `connect()` hangs indefinitely on container boot – asyncio.timeout not firing. | Resolved (closed 2026-07-07) |
| **P1** | #58818 (CLOSED) | Planned restart fires while cron delivery in-flight, message silently dropped. | Resolved |
| **P1** | #14980 (OPEN) | WhatsApp bridge npm install timeout (60s) too short on slow systems (Unraid). | None yet |
| **P2** | #59386 (OPEN) | `delegate_task` schema causes HTTP 400 on strict OpenAI backends. | #59926 open |
| **P2** | #59305 (OPEN) | Desktop chat tabs leak messages across sessions – cross-tab content mixing. | Needs repro |
| **P2** | #52401 (OPEN) | Desktop macOS cross-profile data leak: non-default profile shows default's sessions/crons. | None |
| **P2** | #58498 (OPEN) | Desktop ignores OpenAI Codex provider, routes through Nous Portal (CLI works). | None |
| **P2** | #50530 (OPEN) | Google Antigravity: sub-agent crashes, forced re-auth, session breakpoints. | None |
| **P2** | #59896 (OPEN) | DaemonThreadPoolExecutor breaks on Python 3.14 – `AttributeError` due to CPython internal change. | None |
| **P3** | #59890 (OPEN) | Kanban task event notifications never delivered – 18 subscriptions, 0 deliveries. | None |
| **P3** | #44299 (OPEN) | Explicit auxiliary vision config blocks native vision on providers like Xiaomi MiMo. | None |
| **P3** | #49978 (OPEN) | Desktop PageUp when input focused breaks layout (sidebar squeezed, blank space). | None |
| **P3** | #37338 (OPEN) | Skill metadata audit finds broken `related_skills`, stale names, empty directories. | None |

### Regressions:
- No explicit regressions flagged, but the DaemonThreadPoolExecutor issue (#59896) is a forward-compatibility bug for Python 3.14.

## Feature Requests & Roadmap Signals

### Notable feature requests from today’s data:

| Issue | Feature | Likely inclusion in next release? |
|-------|---------|-----------------------------------|
| #527 | **Gateway Permission Tiers (RBAC)** – Owner/Admin/User/Guest roles for messengers. | High demand, but complex. Candidate for v0.19+ |
| #25061 | **Pre-turn memory health hook** – Auto-compact memory via programmatic logic instead of unreliable LLM instructions. | Low-hanging fruit; could land in next minor release. |
| #37352 | **`hermes skills lint` command** – Validate SKILL.md frontmatter. | Already partially built; PRs possible soon. |
| #47652 | **Perseus context engine integration** – Live context resolution framework. | Early-stage; needs maintainer review. |
| #12232 | **IMAP username config** – Support non-email IMAP usernames (like SMTP already does). | Trivial; likely merged quickly. |
| #7489 | **RPM-based pre-emptive throttling** – Avoid 429s by reading `x-ratelimit` headers. | Ongoing discussion; not yet implemented. |

### Roadmap signals:
- Multiple PRs today address **cron job reliability** (#59921, #59924, #59922, #59930), suggesting a focus on cron stability.
- **Desktop improvements** continue: i18n (#38846), tab leaks (#59305), proxy inheritance (#59920), command exclusions (#59931).
- **Provider compatibility** is a recurring theme – Tencent TokenHub, strict OpenAI backends, Google Antigravity.
- **Security enhancements**: MCP OAuth global elimination (#54325), gateway restart classification (#57419), threat scanner ZWJ fix (#59925).

## User Feedback Summary

### Pain points (frequently mentioned):

- **Timeout issues**: WhatsApp bridge npm install (60s too short), Cron delivery lost during restart, MoA reference hanging.
- **Provider-specific breaks**: OpenAI strict backends reject optional array fields; Tencent shows only 1 of 58 models; Google Antigravity has multiple P2 bugs.
- **Desktop reliability**: Cross-tab message leaks, cross-profile data leak, Codex provider bypass, layout breakage on PageUp.
- **Photom iMessage outage** (RST_STREAM) causing complete service failure for some users.
- **Notification failures**: Kanban task events never delivered to originating conversation.

### Satisfaction signals:

- **Codex duplicate notice issues** (#42187, #47241, #46786, #54432) all closed today – users who voted (up to 10 👍) will see improved UX.
- **Quick fixes** for `delegate_task` schema (#59926) and ZWJ threat scanner (#59925) show responsive development.
- **High engagement** on permission tiers (#527) indicates users are actively investing in shaping the project.

## Backlog Watch

### Issues needing maintainer attention (long-unanswered / unresolved):

| Issue | Age | Problem | Stale? |
|-------|-----|---------|--------|
| #14980 | Since 2026-04-24 | WhatsApp npm timeout – 3 months without fix. | High impact, no response. |
| #7489 | Since 2026-04-11 | RPM throttling – 3 months, no implementation. | Low urgency, but popular. |
| #12232 | Since 2026-04-18 | IMAP username config – 2.5 months, trivial fix. | Low complexity, ignored. |
| #37338 | Since 2026-06-02 | Skill metadata audit – 5 weeks, no follow-up. | Impacts built-in skills. |
| #25061 | Since 2026-05-13 | Memory health hook – 2 months, no assignee. | Good candidate for new contributor. |
| #47652 | Since 2026-06-17 | Perseus integration – 20 days, no maintainer comment. | Needs triage. |

### PRs needing review:

| PR | Age | Size | Description |
|----|-----|------|-------------|
| #34561 | Since 2026-05-29 | Large | Signal message editing via timestamps – 5 weeks open, no merge. |
| #54325 | Since 2026-06-28 | Medium | MCP OAuth global elimination – 9 days, no merge. |
| #38846 | Since 2026-06-04 | Large | 15-language i18n – 33 days, no merge. |
| #57419 | Since 2026-07-03 | Medium | Gateway restart classification – 4 days, pending review. |

**Key takeaway**: The project is actively addressing high-severity bugs (P1) quickly, but medium-priority feature PRs and long-standing issues remain in backlog without maintainer response. The growing number of provider-specific compatibility requests suggests a need for a more structured test matrix or compatibility documentation.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*