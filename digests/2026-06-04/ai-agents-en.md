# OpenClaw Ecosystem Digest 2026-06-04

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-04 03:31 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-04

## 1. Today’s Overview

OpenClaw is experiencing sustained high activity with **500 issues and 500 pull requests updated in the last 24 hours**. Among those, **383 issues remain open/active** and **401 PRs are open**, while **117 issues and 99 PRs were closed or merged** over the same window. Three new releases landed — `v2026.6.2-beta.1`, `v2026.6.1`, and `v2026.6.1-beta.3` — all focused on recovery, stability, and plugin-safety improvements. Despite the pace, the project continues to carry a significant regression burden, with several P1 bugs reported across channels, session state, and the Codex app‑server. Maintainer attention remains split between fixing recent regressions and moving forward with infrastructure improvements (SQLite session migration, operator install policies). Overall project health is **moderately stable but visibly strained** by the volume of open regressions.

## 2. Releases

Three releases were published (most recent first):

- **[v2026.6.2-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.2-beta.1)** —  
  **Highlights**: Plugin and skill installs now use an **operator install policy** instead of the legacy dangerous‑code scanner path. The change surfaces clearer diagnostics in the doctor, CLI, ClawHub, and troubleshooting pages for all install types (package, archive, source, upload, marketplace). No breaking changes or migration notes were indicated.

- **[v2026.6.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.1)** and **[v2026.6.1-beta.3](https://github.com/openclaw/openclaw/releases/tag/v2026.6.1-beta.3)** —  
  **Highlights**: Agents and CLI‑backed runtimes recover more cleanly from interrupted tool calls, stale session bindings, compaction handoffs, and media‑delivery retries. Channels and mobile delivery (Telegram, WhatsApp, iMessage, Slack) are steadier. The beta.3 release is identical in scope to the stable v2026.6.1.

No breaking changes or migration steps were documented in the provided release notes.

## 3. Project Progress

Over the past 24 hours, **99 pull requests were merged or closed**. Notable fixes from the top‑comment PRs include:

- **[PR #90123](https://github.com/openclaw/openclaw/pull/90123)** (closed) — `fix(auto-reply): count message tool sends as delivery`. Ensures `message_tool_only` auto‑reply runs are correctly tracked as delivered.
- **[PR #88890](https://github.com/openclaw/openclaw/pull/88890)** (closed) — `fix #87768: [Bug]: push to talk mac os companion app hard codes thinking low`. Adds a regression test to preserve explicit `thinking` overrides in macOS voice sends.
- **[PR #87965](https://github.com/openclaw/openclaw/pull/87965)** (closed) — `fix(whatsapp): restart channel when a per-account config field changes`. Fixes a bug where disabling a WhatsApp account didn’t tear down the running provider.
- **[PR #88020](https://github.com/openclaw/openclaw/pull/88020)** (closed) — `fix: REPLAY_INVALID_RE missing Anthropic 'Invalid signature in thinking block'`. Added the missing error matcher so sessions with expired thinking signatures can recover with a retry instead of hard failing.

On the open side, several PRs are nearing maintainer review (e.g., **[#90051](https://github.com/openclaw/openclaw/pull/90051)** — strip reasoning tags from chat replies, **[#90110](https://github.com/openclaw/openclaw/pull/90110)** — add Claude Haiku 4.5 static catalog entry, **[#90137](https://github.com/openclaw/openclaw/pull/90137)** — strip thinking signatures after compaction). These indicate steady progress on agent message cleanup and provider compatibility.

## 4. Community Hot Topics

The most commented issues and PRs reveal strong community focus on **session state reliability** and **recent regressions**:

- **[Issue #88838](https://github.com/openclaw/openclaw/issues/88838)** (17 comments, 👍1) — “Track core session/transcript SQLite migration via accessor seam”. The community is actively discussing a phased approach to migrate from file‑based session storage to SQLite, aiming to avoid a single high‑risk rewrite. This is a long‑term infrastructure improvement.

- **[Issue #65161](https://github.com/openclaw/openclaw/issues/65161)** (14 comments, 👍1) — “Heartbeat isolated mode: cadence stalls, ‘heartbeat last’ mislabels exec-events …”. Users report multiple heartbeat‑related regressions in isolated mode, including stalled cadence and misidentified events. The issue has been open since April 12, indicating a persistent pain point.

- **[Issue #67035](https://github.com/openclaw/openclaw/issues/67035)** (14 comments) — “2026.4.14 Windows chat UI regression: input text swallowed, streamed replies often invisible”. Closed, but the high engagement highlights the impact of UI regressions on the Windows user base.

- **[Issue #88312](https://github.com/openclaw/openclaw/issues/88312)** (12 comments, 👍2) — “[Regression] 2026.5.27: Codex app-server turn-completion stall returns”. A P1 bug that reappeared after a previous fix. The community is eager for a permanent resolution.

- **[Issue #67288](https://github.com/openclaw/openclaw/issues/67288)** (11 comments, 👍1) — “amazon-bedrock-mantle lacks config.discovery.enabled gate”. Users want configurable discovery to avoid unnecessary IAM token discovery on every request.

- **[Issue #68113](https://github.com/openclaw/openclaw/issues/68113)** (11 comments, 👍3) — “Mattermost slash commands return 503 "not yet initialized" in v2026.4.15”. A regression in a popular enterprise channel.

Underlying needs: users are frustrated by regressions that break production workflows (Channels, UI, Codex). They want faster fixes and better testing around session state, heartbeat, and network channels.

## 5. Bugs & Stability

The project is contending with several high‑severity bugs:

**P1 (Critical)**
- [Issue #88312](https://github.com/openclaw/openclaw/issues/88312) — Codex turn‑completion stall (regression, no fix PR yet).
- [Issue #86214](https://github.com/openclaw/openclaw/issues/86214) — Codex client closes mid‑turn during large SQLite logs (no fix PR).
- [Issue #87310](https://github.com/openclaw/openclaw/issues/87310) — Stale diagnostic tool_call survives recovery, re‑blocks sessions (no fix PR).
- [Issue #81484](https://github.com/openclaw/openclaw/issues/81484) — Discord guild reply regression: malformed payloads and loops (no fix PR).
- [Issue #63216](https://github.com/openclaw/openclaw/issues/63216) — Repeated hard resets on same session key despite high reserveTokensFloor (no fix PR).
- [Issue #68113](https://github.com/openclaw/openclaw/issues/68113) — Mattermost slash commands 503 (stale, no fix PR).
- [Issue #88020](https://github.com/openclaw/openclaw/issues/88020) — Closed with fix; session recovery now handles expired thinking signatures.
- [Issue #86811](https://github.com/openclaw/openclaw/issues/86811) — WebChat dashboard freezes during tool calls (closed with #86811? Not listed as merged, but closed).

**P2 (High)**
- [Issue #86215](https://github.com/openclaw/openclaw/issues/86215) — Codex OAuth refresh failures can wedge an agent for hours (no fix PR).
- [Issue #77467](https://github.com/openclaw/openclaw/issues/77467) — MiniMax Portal OAuth cannot auto‑refresh (no fix PR).
- [Issue #67735](https://github.com/openclaw/openclaw/issues/67735) — WebChat does not honor identityLinks (no fix PR).
- [Issue #63998](https://github.com/openclaw/openclaw/issues/63998) — Session transcript doomloop leads to OOM (no fix PR, stale).

Many of these bugs have been open for weeks with no linked fix PR. The volume of P1 regressions suggests the project’s testing and release process may need stronger regression gates.

## 6. Feature Requests & Roadmap Signals

Several feature requests garnered community attention:

- **[Issue #72741](https://github.com/openclaw/openclaw/issues/72741)** — “Standard Interface for External Security and Guardrail Checks”. Users want a consistent, documented way to integrate third‑party security checks. This is likely to be prioritised given the growing enterprise adoption and security concerns.

- **[Issue #63990](https://github.com/openclaw/openclaw/issues/63990)** — “Multi-index embedding memory with model-aware failover”. With single‑embedding models being a production risk, this feature would allow resilient provider failover without corrupting vector spaces.

- **[Issue #71142](https://github.com/openclaw/openclaw/issues/71142)** — “Configurable upload size limit for Control UI”. A simple UI enhancement that would benefit Power users uploading larger media.

- **[Issue #64438](https://github.com/openclaw/openclaw/issues/64438)** — “Remote Reranker Endpoint Support”. Adds remote reranker APIs for improved memory search.

- **[Issue #76159](https://github.com/openclaw/openclaw/issues/76159)** — “Per-job acceptSilentStop flag”. Useful for cron jobs that intentionally produce no output but are currently flagged as errors.

**Prediction for next release**: The SQLite session migration (tracked in #88838) is likely to begin landing behind feature flags. The operator install policy from v2026.6.2‑beta.1 may be promoted to stable. Security‑focused features like the standard guardrail interface (#72741) may enter planning.

## 7. User Feedback Summary

**Pain points** expressed across issues and PR comments:
- **Session state volatility** – Users report lost responses, hard resets, and context bloat. E.g., [#67419](https://github.com/openclaw/openclaw/issues/67419) (bootstrap files re‑injected every turn wasting 20–30% tokens), [#63216](https://github.com/openclaw/openclaw/issues/63216) (hard resets despite high token floor).
- **Regression fatigue** – Several high‑profile bugs (Codex stall, Windows UI, Mattermost, Discord) have reappeared after previous fixes, eroding trust in release stability.
- **Channel‑specific issues** – Telegram, Discord, Mattermost, Feishu, and WebChat all have open bugs affecting message delivery or rendering.
- **OAuth management** – MiniMax and Codex OAuth refresh failures leave agents unusable for hours without clear alerting.
- **Tool execution integrity** – Ping‑pong loops survive circuit breakers ([#64500](https://github.com/openclaw/openclaw/issues/64500)), stale tool_call blocks persist ([#87310](https://github.com/openclaw/openclaw/issues/87310)), and tool access for subagents is broken ([#85030](https://github.com/openclaw/openclaw/issues/85030)).

**Satisfaction signals**: The community appreciates the release cadence and the operator install policy improvement. Several PRs receive positive reactions and timely maintainer reviews.

## 8. Backlog Watch

The following important issues and PRs have gone stale or lack maintainer action:

- **[Issue #65161](https://github.com/openclaw/openclaw/issues/65161)** — Heartbeat isolated mode cadence stalls (open since April 12, no fix PR). Multiple users affected; needs product decision.
- **[Issue #63216](https

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem

**Date:** 2026-06-04  
**Analyst:** Senior Ecosystem Analyst

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is experiencing intense activity driven by two distinct architectural philosophies: OpenClaw's agent-first, channel-integrated platform and Hermes Agent's desktop-centric, modular gateway approach. Both projects show high community engagement (50–500 issues/PRs daily) but face divergent maturity challenges—OpenClaw struggles with regression fatigue across its vast channel surface area, while Hermes Agent contends with Windows stability and security hardening gaps. The ecosystem is bifurcating: one path emphasizes production channel reliability and session state management, the other prioritizes desktop UX polish and gateway extensibility. Cross-platform stability remains the single largest pain point across both communities, with Windows and macOS users disproportionately affected.

---

## 2. Activity Comparison

| Metric                    | OpenClaw                                        | Hermes Agent                                    |
|---------------------------|-------------------------------------------------|-------------------------------------------------|
| **Issues Updated (24h)**  | 500                                             | 50                                              |
| **Open Issues**           | 383                                             | 44                                              |
| **Closed Issues (24h)**   | 117                                             | 6                                               |
| **PRs Updated (24h)**     | 500                                             | 50                                              |
| **Open PRs**              | 401                                             | 48                                              |
| **Merged/Closed PRs(24h)**| 99                                              | 2                                               |
| **Releases (today)**      | 3 (v2026.6.2-beta.1, v2026.6.1, v2026.6.1-beta.3)| 0                                               |
| **Critical/High Bugs**    | 7 P1 open, multiple regressions                 | 1 P0, 2 P1, 4 P2 (security-rated)              |
| **Health Score**          | Moderate – strained by regression volume        | High velocity – but with systemic Windows issues|

**Interpretation:** OpenClaw operates at ~10x the raw throughput of Hermes Agent, reflecting a larger development team and broader community. However, its regression burden (6+ P1 bugs unresolved) suggests scaling pains. Hermes Agent's smaller issue volume but higher proportion of security-critical bugs (CVSS 8.0–9.3) indicates a project still building its security posture. Both projects are release-heavy in different ways: OpenClaw pushes stable releases frequently, while Hermes Agent shows no release today despite 8+ fix PRs submitted—implying a pending patch release may be imminent.

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Release cadence:** 3 releases in a single day demonstrates mature CI/CD and rapid iteration capability.
- **Channel breadth:** Telegram, WhatsApp, iMessage, Slack, Discord, Mattermost, Feishu, WebChat—coverage far exceeds Hermes Agent's primarily Slack/WeCom focus.
- **Session state infrastructure:** SQLite migration planning (#88838) indicates architectural foresight for scalability, absent in Hermes Agent's current state.
- **Plugin ecosystem maturity:** Operator install policy (v2026.6.2-beta.1) replaces dangerous-code scanner with safer, policy-driven installs—a security architecture step ahead of Hermes Agent's current file-execution vulnerabilities.

**Technical Approach Differences:**
- OpenClaw is **agent-first**: sessions, tool calls, heartbeat isolation, and compaction are central abstractions. Hermes Agent is **gateway-first**: its architecture revolves around MCP servers, `/claude` commands, and multi-profile routing.
- OpenClaw uses a **Codex app-server** model for enterprise deployments; Hermes Agent emphasizes **desktop standalone** with remote gateway optionality.

**Community Size Comparison:**
- OpenClaw's 500 daily issue/PR updates vs. Hermes Agent's 50 suggests a ~10x larger contributor base. OpenClaw community engagement is more distributed (dozens of high-comment threads), while Hermes Agent's engagement clusters around a few critical issues (accessibility, Windows breakage).
- Both communities show strong contributor altruism: Hermes Agent's `benbarclay` submitted six salvage PRs in one day; OpenClaw's PR volume indicates many contributors fixing their own encountered issues.

**Risk:** OpenClaw's regression volume erodes trust. Hermes Agent can learn from OpenClaw's release gating failures.

---

## 4. Shared Technical Focus Areas

| Shared Need                    | OpenClaw Evidence                              | Hermes Agent Evidence                          |
|--------------------------------|------------------------------------------------|------------------------------------------------|
| **Windows stability**          | Windows UI regression (#67035)                 | Windows update bricks (#37881, #38407)         |
| **Session state reliability**  | Hard resets (#63216), SQLite migration (#88838)| Workspace memory (#38552) – feature request    |
| **Gateway/Channel auth hardening** | Mattermost 503 (#68113), Slack stability      | Slack approval bypass (#38068), gateway fail-open (#38638) |
| **Multi-modal delivery**       | Media delivery retries (v2026.6.1)             | Mermaid rendering (#38654), streaming (#38641) |
| **Desktop app polish**         | WebChat dashboard freezes (#86811)             | Unfocusable composer (#38314), scrollbar bugs (#38669), system tray (#38007) |
| **Tool execution integrity**   | Stale tool_call (#87310), ping-pong loops (#64500) | Blind .py execution (#38674), computer_use issues (#38664) |

**Emerging ecosystem requirement:** **Security-by-default for third-party integrations.** Both projects have open security vulnerabilities in channel/gateway adapters (Mattermost, Slack, custom adapters). The community is demanding standard guardrail interfaces (OpenClaw #72741) and explicit allowlists (Hermes Agent #38638).

---

## 5. Differentiation Analysis

| Dimension                | OpenClaw                                          | Hermes Agent                                      |
|--------------------------|---------------------------------------------------|---------------------------------------------------|
| **Primary user**         | Enterprise/production – channels, sessions, Codex | Developer/enthusiast – desktop, TUI, gateway       |
| **Architecture**         | Agent-in-the-loop with persistent session state   | Gateway MCP routing with ephemeral statelessness  |
| **Deployment model**     | Cloud/app-server (Codex), Docker, local           | Desktop standalone, Docker, terminal (TUI)         |
| **Channel coverage**     | 10+ channels (Telegram, WhatsApp, iMessage, etc.) | Slack, WeCom, Matrix (in progress)                 |
| **Security posture**     | Policy-driven installs, active regressions        | Multiple authorization bypasses, P0 path traversal |
| **Accessibility**        | No explicit accessibility focus                   | VoiceOver request (#26689) – unmet, high engagement|
| **Release philosophy**   | Frequent stable + beta (3 releases today)         | Infrequent releases (none today despite 8+ fixes)  |
| **Community size**       | Large (~500 daily interactions)                   | Smaller (~50 daily interactions) but passionate    |

**Key insight:** OpenClaw targets **reliability at scale** but struggles to maintain it. Hermes Agent targets **desktop-first power users** but sacrifices cross-platform polish and security fundamentals. Neither project has fully addressed accessibility, which may limit adoption in regulated enterprise environments.

---

## 6. Community Momentum & Maturity

**Tier 1: High Maturity, Scaling Pains**  
*OpenClaw* — Rapid iteration (3 releases/day), architectural vision (SQLite migration, operator policies), but regression backlog erodes trust. Community is large, engaged, and vocal about production quality. Maturity is high in infrastructure design but low in regression prevention.

**Tier 2: Rapidly Iterating, Unstable Core**  
*Hermes Agent* — High velocity on bug fixes (8 PRs in one day), strong contributor community (`benbarclay` salvages), but Windows update pipeline is broken, security vulnerabilities are being reported faster than fixed (P0 skill_view traversal unaddressed). Maturity is moderate in feature work but low in platform stability.

**Maturity Signals:**
- **OpenClaw** is stabilizing around session state (SQLite migration) and install security (operator policy). If they resolve regressions, they could enter a "stable core" phase.
- **Hermes Agent** is still discovering its architectural boundaries—accessibility, security, and cross-platform issues indicate the project is in a "feature growth before stabilization" phase.
- Both projects have **unaddressed critical bugs** (OpenClaw: Codex stall #88312, Discord #81484; Hermes Agent: skill_view traversal #38643) that could trigger emergency patch releases.

---

## 7. Trend Signals

**1. Enterprise Readiness Demands Are Outpacing Security Posture**  
Both projects face authorization bypass, path traversal, and channel-specific exploits. The market is demanding standard guardrail interfaces (OpenClaw #72741) and explicit allowlists (Hermes Agent #38638). **Value for developers:** Invest in third-party adapter security testing; policy-driven installs are becoming baseline.

**2. Desktop Parity Is the New Minimum Viable Experience**  
Windows and macOS users are reporting systemic update breakage (Hermes Agent #37881, #38407; OpenClaw #67035). Desktop is no longer a secondary client—it's the primary interface for many power users. **Value for developers:** Test update pipelines separately; invest in desktop CI across all three platforms.

**3. Session State Reliability Separates Amateurs from Professionals**  
OpenClaw's SQLite session migration and Hermes Agent's workspace memory requests signal that **stateless sessions are no longer acceptable** for production AI assistants. Persistent, resilient state management with compaction and recovery is becoming table stakes. **Value for developers:** Prioritize session serialization/deserialization correctness; implement heartbeat-based monitoring.

**4. Multi-Modal Delivery Is Fragmented but Converging**  
Both projects are building streaming/progressive reply capabilities (OpenClaw: media retries; Hermes Agent: WeCom streaming #38641, Mermaid rendering #38654). Markdown-to-rich-delivery pipelines are emerging as a cross-cutting concern. **Value for developers:** Abstract rendering/streaming into a dedicated "delivery layer" to avoid per-channel bugs.

**5. Contributor Sustainability Is a Silent Risk**  
Hermes Agent's reliance on a single contributor (`benbarclay`) for six salvage PRs in one day highlights bus-factor risk. OpenClaw's regression volume suggests maintainers are stretched. **Value for ecosystem:** Invest in automated regression testing and release gating to reduce manual triage burden.

**6. Accessibility Is an Untapped Market**  
Hermes Agent's VoiceOver request (#26689) has 8 comments and zero maintainer response—but accessibility compliance (WCAG, Section 508) is becoming a procurement requirement in European and enterprise markets. **Value for developers:** Early investment in screen-reader support and keyboard navigation can differentiate projects in regulated verticals.

---

**Bottom Line:** Both OpenClaw and Hermes Agent are building foundational AI agent infrastructure, but from different architectural starting points. OpenClaw's breadth and release discipline offer production-level capability at the cost of instability; Hermes Agent's desktop focus and community passion offer innovation velocity at the cost of security maturity. The ecosystem as a whole is converging on session state reliability, cross-platform stability, and security-by-default as the next battlegrounds.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-04

## 1. Today's Overview
Project activity remains very high with **50 issues** and **50 pull requests** updated in the last 24 hours. The ratio of open to closed items (44 open issues, 48 open PRs) indicates a maintenance-heavy phase rather than a release push — no new releases were created today. Windows- and macOS-specific bugs dominate the issue tracker, alongside several security reports rated Critical/High by submitters. Community engagement is robust, with 8 comments on the long-running accessibility request and multiple contributors submitting patches for desktop and gateway stability.

## 2. Releases
**None.** No new versions were published today.

## 3. Project Progress
Two pull requests were closed/merged today:
- **[#38665](https://github.com/NousResearch/hermes-agent/pull/38665) — `test(docker): make tty-passthrough probe robust to container boot-log noise`**  
  A test-only fix that prevents false failures in container TTY passthrough tests by filtering out s6 boot‑log output before parsing PTY column counts.
- **[#38593](https://github.com/NousResearch/hermes-agent/pull/38593) — `refactor(web): unify main-slot model assignment base_url/context handling`**  
  Extracts duplicated provider/base_url/context_length reconciliation logic into a single helper, reducing future drift risk between `POST /api/model/set` and the profile‑model writer.

Six issues were closed, including:
- [#37827](https://github.com/NousResearch/hermes-agent/issues/37827) (Windows setup error) — closed without merge (likely user support case).
- [#37792](https://github.com/NousResearch/hermes-agent/issues/37792) (MCP 401 Unauthorized) — closed, presumably fixed or resolved.
- [#38070](https://github.com/NousResearch/hermes-agent/issues/38070) (Docker/Unraid UID handling) — closed as follow-up to #32559 but notes a remaining root cause.

No major feature milestones were merged today; the focus was on bug fixes and refactoring.

## 4. Community Hot Topics
- **[#26689](https://github.com/NousResearch/hermes-agent/issues/26689) — Accessibility improvements for blind VoiceOver users**  
  *8 comments, 0 reactions.* First opened 2026-05-16. The user (a totally blind macOS user) describes severe screen‑reader friction in the current UX. No maintainer response is visible. This has become the most‑commented open issue, indicating strong latent demand for inclusive design.

- **[#37881](https://github.com/NousResearch/hermes-agent/issues/37881) — `hermes update` bricks Windows install (venv rebuild failure)**  
  *3 comments, 1 👍.* A P1 bug causing total software breakage on Windows after `hermes update`. The user reports `pyvenv.cfg` missing and `ModuleNotFoundError`. Fix is not yet submitted.

- **[#38156](https://github.com/NousResearch/hermes-agent/issues/38156) — TUI passes host launch cwd into Docker terminal sessions on Windows**  
  *2 comments, 2 👍.* A P2 bug that leaks host working directory into Docker containers. High community interest.

- **[#30230](https://github.com/NousResearch/hermes-agent/issues/30230) — Gateway hits macOS fd limit (256)**  
  *3 comments.* A long-standing resource exhaustion bug for users running multiple profiles/MCP servers.

- **[#38068](https://github.com/NousResearch/hermes-agent/issues/38068) — Slack approval buttons ignore authorization**  
  *2 comments.* Self-assessed CVSS 8.0/8.6 (High). Duplicate of #38069 PR. Critical security concern for Slack integrations.

**Underlying needs:** Users are demanding better cross‑platform stability (Windows, macOS), security hardening for gateway integrations, and fundamental usability for assistive technology. Desktop app polish (tray icon, profile switcher) also surfaces repeatedly.

## 5. Bugs & Stability
Today’s reports span P0 to P3. Ranked by severity:

| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| **P0** | [#38643](https://github.com/NousResearch/hermes-agent/issues/38643) | `skill_view` name traversal — attacker can read files outside trusted skills directory | No |
| **P1** | [#38652](https://github.com/NousResearch/hermes-agent/issues/38652) | Infinite auto‑reset loop on OpenRouter/Nous output‑cap errors | Yes: [#38667](https://github.com/NousResearch/hermes-agent/pull/38667) |
| **P1** | [#37881](https://github.com/NousResearch/hermes-agent/issues/37881) | Windows `hermes update` bricks venv, leaves `ModuleNotFoundError` | No |
| **P2** | [#38638](https://github.com/NousResearch/hermes-agent/issues/38638) | Gateway own‑policy adapters fail open without allowlists (CVSS 9.1/9.3) | No |
| **P2** | [#38068](https://github.com/NousResearch/hermes-agent/issues/38068) | Slack approval buttons bypass authorization (CVSS 8.0/8.6) | Yes: [#38069](https://github.com/NousResearch/hermes-agent/pull/38069) |
| **P2** | [#38407](https://github.com/NousResearch/hermes-agent/issues/38407) | Windows Desktop app fails after update: incomplete git checkout + cache mismatch | No |
| **P2** | [#38662](https://github.com/NousResearch/hermes-agent/issues/38662) | `/claude` gateway command passes unsupported `--acp --stdio` flags to Claude Code CLI | No |
| **P2** | [#38674](https://github.com/NousResearch/hermes-agent/issues/38674) | Blindly executes all `.py` files in CWD (e.g. `setup.py` from echomind) | No |
| **P2** | [#38580](https://github.com/NousResearch/hermes-agent/issues/38580) | `requests==2.33.0` missing `_types.py` on aarch64 (Jetson) | No |
| **P3** | [#30230](https://github.com/NousResearch/hermes-agent/issues/30230) | macOS fd limit (256) — OSError Too many open files | No |
| **P3** | [#38650](https://github.com/NousResearch/hermes-agent/issues/38650) | `hermes dump` reports MCP servers as “failed” despite successful discovery | No |
| **P3** | [#38314](https://github.com/NousResearch/hermes-agent/issues/38314) | Desktop composer becomes unfocusable until restart | No |
| **P3** | [#38669](https://github.com/NousResearch/hermes-agent/issues/38669) | Web UI chat scrollbar cannot scroll to bottom | No |

**Notable fix PRs submitted today:**
- [#38667](https://github.com/NousResearch/hermes-agent/pull/38667) fixes the infinite reset loop (P1) by parsing OpenRouter error format.
- [#38664](https://github.com/NousResearch/hermes-agent/pull/38664) fixes three `computer_use` issues with local/custom vision models.
- [#38666](https://github.com/NousResearch/hermes-agent/pull/38666) fixes cron jobs on Windows with `pythonw.exe` + non-UTF-8 locales (closes #38633).
- [#38668](https://github.com/NousResearch/hermes-agent/pull/38668) salvages fallback to `pip` when `uv` is unavailable (memory setup).
- [#38655](https://github.com/NousResearch/hermes-agent/pull/38655) fixes Docker chown of gateway install tree on UID remap.
- [#38672](https://github.com/NousResearch/hermes-agent/pull/38672) re‑wires sudo/secret callbacks on daemon threads.
- [#38649](https://github.com/NousResearch/hermes-agent/pull/38649) promotes `markdown` to core dependency for Matrix rich delivery.
- [#38677](https://github.com/NousResearch/hermes-agent/pull/38677) salvages a batch of six desktop bug fixes (IME, attachments, scroll, etc.).
- [#38631](https://github.com/NousResearch/hermes-agent/pull/38631) fixes persistent needs‑input indicator and UI redesign.
- [#38675](https://github.com/NousResearch/hermes-agent/pull/38675) allows desktop remote dashboard WebSocket origins in legacy token mode.

## 6. Feature Requests & Roadmap Signals
Top user‑requested features today:

- **[#26689](https://github.com/NousResearch/hermes-agent/issues/26689) — Accessibility for blind users (VoiceOver)**  
  Likely to gain traction if maintainers respond; not yet assigned.
- **[#38552](https://github.com/NousResearch/hermes-agent/issues/38552) — Automated Workspace Memory**  
  Agent remembers directory purposes across sessions. Potential synergy with existing memory tools.
- **[#38602](https://github.com/NousResearch/hermes-agent/issues/38602) — Desktop client-only installation**  
  Users want thin‑client mode with remote Hermes backend. Strong desktop integration signal.
- **[#37713](https://github.com/NousResearch/hermes-agent/issues/37713) — Remote gateway profile switcher in Desktop UI**  
  Already has 1 👍. Likely to be implemented given multiple desktop PRs today.
- **[#38007](https://github.com/NousResearch/hermes-agent/issues/38007) — System tray support**  
  Keep app running in background on window close. 1 👍.
- **[#38671](https://github.com/NousResearch/hermes-agent/issues/38671) — True remote workspace/file browser**  
  Desktop currently mixes local and remote filesystem.
- **[#38654](https://github.com/NousResearch/hermes-agent/issues/38654) — Mermaid diagram rendering in markdown preview**  
- **[#38640](https://github.com/NousResearch/hermes-agent/issues/38640) — Launch on startup for Windows**  
- **[#38641](https://github.com/NousResearch/hermes-agent/issues/38641) — WeCom adapter streaming/progressive replies**  
  Also has a PR [#38660](https://github.com/NousResearch/hermes-agent/pull/38660) submitted today.

**Prediction for next version:** Desktop system tray support and profile switcher are low‑hanging fruit likely to land soon. The P0/P1 security fixes (skill_view traversal, Slack auth bypass) may force an emergency patch release. WeCom streaming and Mermaid rendering could appear in a minor release.

## 7. User Feedback Summary
- **Windows dissatisfaction:** Three distinct “update broke my install” reports (##37881, #38407, #38618) indicate a systemic Windows update pipeline issue. Users are blocked from using the app after update.
- **macOS friction:** VoiceOver accessibility (#26689) and fd limit (#30230) show the platform is underserved.
- **Desktop app reliability:** Reports of unfocusable composer (#38314), scrollbar bugs (#38669), and missing system tray (#38007) suggest UI QA gaps.
- **Security concerns:** Two critical/gateway‑wide authorization bypass reports (##38068, #38638) signal that enterprise Slack and custom adapter users need urgent hardening.
- **Positive signals:** Users are actively contributing features (YouPet WeCom bridge #38678, Concentrate AI provider #38403) and bug ﬁx PRs (multiple salvages by `benbarclay`). High community engagement in a single day indicates a dedicated user base.

## 8. Backlog Watch
- **[#26689](https://github.com/NousResearch/hermes-agent/issues/26689)** (P3 feature, accessibility) — opened 2026-05-16, no maintainer comment. With 8 comments and no response, this is the longest neglected high‑engagement issue.
- **[#30230](https://github.com/NousResearch/hermes-agent/issues/30230)** (P2 bug, macOS fd limit) — opened 2026-05-22, 3 comments, no fix. Likely affects many macOS users running multiple profiles.
- **[#38643](https://github.com/NousResearch/hermes-agent/issues/38643)** (P0 security, skill_view traversal) — reported today, needs immediate triage. No PR yet.
- **[#38638](https://github.com/NousResearch/hermes-agent/issues/38638)** (P2 security, gateway fail‑open) — also reported today, no PR. High CVSS score.
- **PRs from `benbarclay`** (##38649, #38655, #38668) have no assigned reviewer. These are salvage PRs that fix important cross‑platform bugs; maintainer review is needed to merge.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*