# OpenClaw Ecosystem Digest 2026-06-06

> Issues: 469 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-06 02:47 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-06

## 1. Today's Overview

The project is highly active with **469 issues** and **500 pull requests** updated in the last 24 hours. 131 issues were closed and 137 PRs were merged or closed, indicating steady maintenance and community involvement. No new releases were published. Persistent regressions (especially around the OpenAI ChatGPT Responses transport and the Coding Agent) continue to generate heated discussion, while the community actively proposes features such as tiered bootstrap loading and per-agent memory-wiki vaults. Several high-priority fixes are in the review pipeline, and the ClawSweeper automation is merging minor patches.

## 2. Releases

**None today.** The latest release remains the previously tagged version (no new releases reported in the data).

## 3. Project Progress

Over the past 24 hours, **137 PRs have been closed or merged**. Notable examples include:

- **#90815** (closed) – Fix macOS node mode silent self-reconnect ([PR](https://github.com/openclaw/openclaw/pull/90815))  
- **#90816** (closed) – Fix memory-core adapter default model identity check ([PR](https://github.com/openclaw/openclaw/pull/90816))  
- **#90736** (closed) – macOS node mode WebSocket session fix ([PR](https://github.com/openclaw/openclaw/pull/90736))  
- **#90773** (closed) – Keep auto-compaction appends owned during prompt lock release ([PR](https://github.com/openclaw/openclaw/pull/90773))  
- **#90772** (closed) – Guard routing fix ([PR](https://github.com/openclaw/openclaw/pull/90772))  
- **#90620** (closed) – Preserve live Twilio streams in stale reaper for voice calls ([PR](https://github.com/openclaw/openclaw/pull/90620))

Other progress includes open PRs with proofs that address session stability, sandbox skills materialization for Docker, and reasoning tag stripping (e.g., #90051, #90798, #90811).

## 4. Community Hot Topics

Issues with the highest engagement (by comment count and reactions):

- **#22438** – *Feat: Tiered bootstrap file loading for progressive context control*  
  [Issue](https://github.com/openclaw/openclaw/issues/22438) — 17 comments, 0 reactions  
  *Need:* Reduce LLM token waste by loading bootstrap files on demand instead of every session.

- **#62505** – *[Bug]: Coding Agent never completes anything (worked in 2026.4.2 and earlier)*  
  [Issue](https://github.com/openclaw/openclaw/issues/62505) — 14 comments, 1 reaction  
  *Need:* Critical regression affecting all coding tasks; community is pressing for a fix.

- **#76562** – *High CPU, extreme control-plane RPC latency, and unstable polling after upgrade*  
  [Issue](https://github.com/openclaw/openclaw/issues/76562) — 13 comments, 5 reactions  
  *Need:* Performance regression after minor upgrades; gateway becomes nearly unusable.

- **#78308** – *Channel-mediated approval for MCP tool calls (consent envelope)*  
  [Issue](https://github.com/openclaw/openclaw/issues/78308) — 12 comments, 1 reaction  
  *Need:* Security – let MCP tools opt into the same approval workflow as shell-exec.

- **#90083** – *OpenAI ChatGPT Responses transport fails with invalid_provider_content_type for gpt-5.4/gpt-5.5*  
  [Issue](https://github.com/openclaw/openclaw/issues/90083) — 12 comments, 3 reactions  
  *Need:* Urgent bug blocking users on latest OpenAI models.

- **#63829** – *Per-agent memory-wiki vault configuration*  
  [Issue](https://github.com/openclaw/openclaw/issues/63829) — 9 comments, 9 reactions (most 👍)  
  *Need:* Multi-agent setups need isolated knowledge wikis per agent.

## 5. Bugs & Stability

Several high-severity bugs and regressions were reported or discussed today.

| Severity | Issue | Summary | Fix PR exists? |
|----------|-------|---------|----------------|
| **P1** | [#62505](https://github.com/openclaw/openclaw/issues/62505) | Coding Agent never completes (regression from 2026.4.2) | Not linked in data |
| **P1** | [#76562](https://github.com/openclaw/openclaw/issues/76562) | High CPU / RPC latency after upgrade to 2026.4.29+ | No linked PR |
| **P1** | [#90083](https://github.com/openclaw/openclaw/issues/90083) | OpenAI ChatGPT Responses transport broken for gpt-5.4/5.5 | No linked PR |
| **P1** | [#87756](https://github.com/openclaw/openclaw/issues/87756) | Lobster workflow hangs on nested /tools/invoke when launched from prompt | No linked PR |
| **P1** | [#90325](https://github.com/openclaw/openclaw/issues/90325) | Matrix channel dispatch broken in v2026.6.1 (TypeError) | No linked PR |
| **P1** | [#90466](https://github.com/openclaw/openclaw/issues/90466) | memory-core dreaming uses deleted session files, writes fallback | No linked PR |
| **P2** | [#90072](https://github.com/openclaw/openclaw/issues/90072) | Cron state silently wiped during SQLite migration to 2026.6.1 | Closed as fixed? (closed without merge) |
| **P2** | [#77012](https://github.com/openclaw/openclaw/issues/77012) | WebChat session transcript overwritten on every turn (5.2 regression) | No linked PR |
| **P1** | [#72031](https://github.com/openclaw/openclaw/issues/72031) | `image` tool fails for Bedrock with `requireApiKey` | No linked PR |

Many other bugs (e.g., #90711, #67417, #90783) remain open but with lower comment counts. The **Coding Agent (#62505)** and **OpenAI transport (#90083)** are the most impactful, affecting core functionality for a large user base.

## 6. Feature Requests & Roadmap Signals

The community is actively requesting enhancements that suggest future roadmap priorities:

- **Tiered bootstrap file loading (#22438)** – Would significantly reduce token consumption for power users. Likely in next minor release given PR #90819 (pinning plugin workspace) addresses related performance.
- **Channel-mediated MCP approval (#78308)** – Strong security rationale; similar to existing shell-exec approval.
- **Per-agent memory-wiki vault (#63829)** – High demand (9 👍). Would enable true multi-agent isolation.
- **Hide/collapse Workspace rail in WebChat (#90246)** – UX improvement; low effort, high value.
- **Model picker agent runtimes (#90328)** – Already has an open PR, so likely shipped soon.
- **Session max duration/token caps (#64463)** – Cost control for runaway sessions.

PRs that are being actively worked on:  
- #78441 (Forward toolsAllow from sessions_spawn) – open, ready for maintainer look.  
- #90811 (Stabilize user-turn serialization to preserve prompt cache) – open, needs real-behavior proof.  
- #85155 (Avoid provider swaps in model alias guidance) – open, ready for maintainer look.

## 7. User Feedback Summary

User sentiment is mixed – **dissatisfaction** with regressions is loud:

- "Coding Agent just doesn't do anything… vague status updates and apologies" (#62505)
- "CPU pinned near 100%… control-plane RPC latency extreme" (#76562)
- "Cron state silently wiped… only 1 of 45 jobs survived" (#90072)
- "WebChat transcript overwritten every turn – all previous messages gone" (#77012)
- "Matrix channel handler crashes on every inbound message" (#90325)

**Positive signals**: The community actively proposes solutions (tiered bootstrap, MCP approval, per-agent vaults). Users appreciate the approval workflow concept and want it extended. The ClawSweeper automation is making small merges efficiently, but major regressions remain unaddressed.

## 8. Backlog Watch

Several important issues and PRs have been open for weeks or months without maintainer resolution:

- **#22438** – Tiered bootstrap (17 comments, opened Feb 2026) – needs product decision.
- **#14785** – Reduce tool schema token overhead ~3500 tok/session (opened Feb) – needs maintainer review.
- **#43015** – message.send schema overexposes poll/components (opened Mar) – linked PR open but not merged.
- **#61005** – Android onboarding "Connect" button inactive when offline (opened Apr, 5 reactions) – no PR.
- **#63101** – Feishu channel config validation fails after upgrade (opened Apr) – linked PR open.
- **#62985** – Telegram multi-account config error (opened Apr) – linked PR open.
- **#58818** – Guarantee last N raw messages in agent context (opened Apr) – needs product decision.
- **#58730** – exec() sandbox isolation (opened Apr) – needs multiple reviews.

These items represent pain points that, if resolved, would greatly improve stability and user trust. The maintainer team is encouraged to prioritise **P1 regressions (#62505, #76562, #90083)** over new features, given the volume of complaints.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs Hermes Agent

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is experiencing a bifurcation between foundational core frameworks and user-facing agent deployments. Both OpenClaw and Hermes Agent demonstrate strong community engagement, with OpenClaw acting as a reference implementation for agent routing, memory, and transport layers, while Hermes focuses on polished desktop, mobile, and gateway integrations with internationalisation at the forefront. The ecosystem is marked by a tension between rapid feature iteration and stability regressions—users across both projects report frustration with critical path failures (coding agents, transport compatibility, reconnect logic) even as new features like MCP tool approval and i18n support gain traction. Maintainers face increasing pressure to balance upstream model API changes (OpenAI, Anthropic) with backward compatibility for self-hosted deployments.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| Issues updated (24h) | 469 | 50 |
| PRs updated (24h) | 500 | 50 |
| Issues closed (24h) | 131 | not specified (~49 open) |
| PRs merged/closed (24h) | 137 | 21 |
| Release today? | None | v0.16.0 (yesterday) |
| Community health score | **Moderate** – high volume but 6+ P1 regressions blocking core workflows | **High** – strong release cadence but 2 P1 bugs and multiple P2 stability issues |
| Contributors (recent) | Not specified (open core) | 170 community contributors in v0.16.0 |

**Interpretation:** OpenClaw operates at roughly 10x the raw activity volume, but a disproportionate share reflects bug triage and regression management. Hermes, despite lower volume, shows a cleaner signal-to-noise ratio with focused feature delivery and a polished major release.

## 3. OpenClaw's Position

**Advantages:**
- **Scale of community engagement** – 469 issues and 500 PRs in 24h indicates a very large user/contributor base, far exceeding Hermes in raw participation.
- **Technical depth** – Unique constructs like tiered bootstrap loading (#22438), per-agent memory-wiki vaults (#63829), and channel-mediated MCP approval (#78308) demonstrate architectural ambition beyond what Hermes currently targets.
- **Transport breadth** – Support for Twilio, Matrix, Telegram, Feishu, OpenAI Responses, and MCP tools gives it a wider integration surface.

**Technical approach differences:**
- OpenClaw is a **core reference stack** – its architecture emphasises modular memory, session routing, and configurable context loading. Hermes is a **shippable product** with a unified desktop/TUI/CLI experience.
- OpenClaw’s “ClawSweeper” automation merges minor patches autonomously, indicating a more DevOps-driven release pipeline, while Hermes relies on manual PR review cycles.

**Community size comparison:** OpenClaw’s activity volume (469 issues, 500 PRs) suggests a community 5–10x larger than Hermes (50 issues, 50 PRs), though the per-issue severity is higher for OpenClaw.

**Weakness:** Regression velocity is causing user frustration – 6 P1 bugs block core functionality (Coding Agent complete failure, OpenAI transport broken, Matrix dispatch crashes). Hermes has fewer P1 issues and a more recent successful release.

## 4. Shared Technical Focus Areas

Both projects exhibit converging requirements across the following domains:

| Focus Area | OpenClaw Signals | Hermes Signals | Common Need |
|------------|-----------------|----------------|-------------|
| **Context/token waste reduction** | Tiered bootstrap loading (#22438), prompt cache preservation (#90811) | Compression evidence fabrication guard (#40260), context preservation on failure (#26051) | Smarter context management to reduce LLM costs and improve reliability |
| **Multi-agent isolation** | Per-agent memory-wiki vaults (#63829), session max duration caps (#64463) | Cron scheduler context bleed (#39886) | Isolated state, memory, and configuration per agent/profile |
| **MCP tool permission model** | Channel-mediated approval (#78308) | Shell-exec approval already exists; `/approvals` slash command requested (#39425) | Standardised user-in-the-loop approval for tool invocations |
| **Transport/adapter resilience** | Twilio stream reaper fix (#90620), Matrix dispatch crash (#90325) | QQ Bot reconnect loop (#31101), LINE media crash (#34233), MCP dead-after-outage (#38488) | Graceful reconnection and message handling for third-party platforms |
| **Internationalisation** | Not explicitly present | Japanese (#40219), Portuguese (#40239), Chinese IME fixes (#40146), i18n framework merged (#35277) | Growing demand for non-English UX |
| **Security/secret handling** | MCP consent envelope (#78308) | Secret redaction modifies command execution (#40139), CVE dependencies (#40176) | Secure credential handling and dependency hygiene |

**Key insight:** The most pressing shared requirement is **context reliability** – both communities are actively pushing for solutions that prevent LLM token waste, preserve prompt caches, and eliminate fabricated or stale information. This suggests a maturing awareness that raw model capacities are not the bottleneck; intelligent resource management is.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary target user** | Developers building custom agent systems, self-hosters, integrators | End-users seeking a ready-to-use desktop/CLI agent, i18n-first users |
| **Delivery model** | Reference implementation + core library; no unified binary | Shippable desktop app (Electron), TUI, gateway plugins |
| **Architecture emphasis** | Modular memory-wiki, routing, multi-transport, agent-to-agent communication | Unified session context, compression, MCP server integration, profile system |
| **Release cadence** | Continuous (ClawSweeper merges minor patches); major versions less frequent | Major milestones (v0.16.0 “Surface Release”); versioned with changelogs |
| **Community contribution style** | High-volume issue/PR triage; driver for stability patches | Smaller but highly engaged; 170 contributors in one release |
| **Feature risk profile** | High regression risk – frequent breakage in core paths (Coding Agent, OpenAI transport) | Moderate – desktop/UI bugs dominate; core agent logic more stable |
| **i18n status** | No reported i18n support | Actively building Japanese, Chinese, Portuguese; TUI/CLI already partially localised |

**Summary:** OpenClaw is the **platform builder’s choice** – broader integration surface, deeper customisation, but at the cost of stability. Hermes is the **end-user’s choice** – polished, localised, and more reliable, but with a narrower integration scope.

## 6. Community Momentum & Maturity

| Tier | Project | Characteristics |
|------|---------|-----------------|
| **Rapid iteration (volatile)** | OpenClaw | 469 issues/500 PRs daily, 6+ P1 regressions, no new release. Community is highly active but frustrated. Growth is organic but chaotic. |
| **Rapid iteration (stable)** | Hermes Agent | 50 issues/50 PRs daily, clean v0.16.0 release, 2 P1 bugs under active fix. Strong product momentum with controlled pace. |

**Assessment:**
- **OpenClaw** is in a **hypergrowth-but-stabilisation phase** – activity volume suggests a large installed base, but the project is struggling to contain regressions. The maintainer team should treat the current state as a firefighting crisis that erodes user trust.
- **Hermes** is in a **consolidation phase** after a massive release – focus is shifting to bug fixing, i18n, and platform polish. The community is enthusiastic but smaller, with a higher ratio of feature contributors to bug reporters.

**Maturity signals:**
- OpenClaw has more backlog items (some open since February 2026) and a higher ratio of unresolved P1 issues → **lower maturity / higher technical debt**.
- Hermes has a cleaner backlog, a released major version, and active PR review for its top P1 bugs → **higher maturity per unit of community size**.

## 7. Trend Signals for AI Agent Developers

1. **Context optimization is the new frontier** – Both communities are investing heavily in reducing LLM token waste (bootstrap loading, compression guards, prompt cache preservation). Developers should prioritise tooling for selective context injection and cache-aware session management over raw model capability upgrades.

2. **Multi-agent isolation is becoming table stakes** – With OpenClaw’s per-agent vaults and Hermes’ profile-scoped memory, the ecosystem is converging on a model where each agent profile has independent knowledge stores and session state. Developers building agent platforms should bake this in from day one.

3. **MCP tool approval is not optional** – Both projects are adding user-in-the-loop workflows for tool invocations. The community expects security boundaries between agents and external tools, especially for shell execution and data-sensitive APIs. Build approval frameworks that are channel-agnostic (web, chat, API).

4. **Transport resilience is the #1 reliability pain point** – From Twilio streams to QQ Bot WebSocket loops, adapter instability is the dominant source of user frustration. Investing in standardised reconnect backoff, heartbeat monitoring, and idempotent message handling yields high user satisfaction returns.

5. **i18n is a growth lever** – Hermes’ explicit investment in Japanese, Portuguese, and Chinese (backed by community translators) signals untapped demand in non-English markets. Even if core logic remains English-first, localising TUI/CLI and configuring locale-aware formatting opens significant user acquisition opportunities.

6. **Model API evolution exposes architectural debt** – OpenClaw’s breakage with gpt-5.4/5.5 and Hermes’ need for schema sanitizers (#40232) illustrate that hardcoding provider-specific transport logic is fragile. A provider abstraction layer with fallback handling is increasingly necessary.

7. **Self-hosted deployment remains dominant** – Both projects’ bug reports frequently reference Docker, VPS, Tailscale, and SQLite. Developers targeting this audience must optimise for low-resource environments and offline-capable architectures (cron, local gateway, local file systems).

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-06

## Today’s Overview

Hermes Agent continues its rapid development cadence with **50 issues and 50 PRs updated in the last 24 hours**, reflecting a very high level of community and maintainer activity. One new release landed yesterday – **v0.16.0 (The Surface Release)** – a massive milestone encompassing 874 commits, 542 merged PRs, and contributions from 170 community contributors. The project is currently processing a wide range of bug reports (especially around desktop platform compatibility, IME input, and remote gateway connectivity) alongside feature requests for internationalisation and enhanced platform integration. The open/active issue count of 49 out of 50 indicates that most reports are still being triaged, while 21 PRs were merged or closed today, signalling strong momentum in bug fixing and feature delivery.

## Releases

**v2026.6.5 — Hermes Agent v0.16.0 (The Surface Release)**  
*Released 2026-06-05*  
- Since v0.15.2: 874 commits, 542 merged PRs, 1,962 files changed, +205,216 / -46,217 lines  
- 399 issues closed (2 P0, 62 P1, 16 security-tagged)  
- 170 community contributors (including co-authors)  

No explicit breaking changes or migration notes were included in the provided release notes, but given the scale of changes, downstream users should review the full changelog for any deprecations.

## Project Progress

Today **21 PRs were closed or merged**, with several notable integrations:

- **Codex profile builder web flow** (#40254) — adds a multi-step dashboard for creating agent profiles (model, MCP servers, skills).
- **Vision tool retry fix** (#32297) — stops retrying non-retryable 4xx image download errors, eliminating wasted API calls.
- **OpenRouter model ID documentation** (#40087) — clarifies fallback best practices for provider model renaming.
- **Line platform adapter fix** (#34233) — resolves inbound media crashes by mapping LINE message types to standard gateway enums.
- **i18n framework merge** (#35277) — consolidates Chinese localization (CLI/TUI) into a clean branch ready for mainline.

Active PRs that advanced today include:
- **Compression evidence fabrication guard** (#40260) — addresses a high-severity P1 bug (#40201) by adding critical evidence re-grounding checks after context compression.
- **Desktop remote gateway file operations** (#40258) — allows file browse/upload to work when the desktop client is connected to a remote backend (VPS over tailscale).
- **ACP OAuth bearer forwarding** (#40257) — enables end‑to‑end user identity propagation through ACP to the LLM provider.

## Community Hot Topics

The most active discussions (by comment count) highlight strong interest in cross‑platform compatibility and internationalisation:

| Issue/PR | Title | Comments | 🏷 Labels |
|----------|-------|----------|-----------|
| [#37505](https://github.com/NousResearch/hermes-agent/issues/37505) | macOS DMG arm64-only fails on Intel Macs | 5 | type/bug, P3 |
| [#40219](https://github.com/NousResearch/hermes-agent/issues/40219) | Add Japanese language support (i18n) | 4 | type/feature, comp/tui, P3 |
| [#31101](https://github.com/NousResearch/hermes-agent/issues/31101) | QQ Bot adapter silent reconnect loop | 4 | type/bug, comp/gateway, platform/qqbot, P2 |
| [#40146](https://github.com/NousResearch/hermes-agent/issues/40146) | Send button not switching from voice when typing Chinese (IME) | 3 | type/bug, comp/tui, P3 |
| [#40239](https://github.com/NousResearch/hermes-agent/issues/40239) | Add Portuguese (pt-BR) language support | 2 | type/feature, P3 |
| [#40260](https://github.com/NousResearch/hermes-agent/pull/40260) | Fix: prevent post‑compression evidence fabrication | (new) | PR targeting P1 bug |
| [#34233](https://github.com/NousResearch/hermes-agent/pull/34233) | Fix LINE inbound media crashes | (new) | type/bug, comp/gateway, P3 |

The underlying needs are clear:
- **Support for non‑English users** – Japanese, Portuguese, and better Chinese IME handling.
- **Platform resilience** – QQ Bot, LINE, and MCP server reconnection after transient outages.
- **Desktop UX parity** – Intel Mac & Windows IME behaviour, remote gateway file access.

## Bugs & Stability

### P1 (Highest Severity)
| Issue | Description | Fix PR |
|-------|-------------|--------|
| [#39886](https://github.com/NousResearch/hermes-agent/issues/39886) | Cron scheduler context bleed: profile-job context leaks into non‑profile job, causing “Script not found” | – |
| [#40201](https://github.com/NousResearch/hermes-agent/issues/40201) | Post‑compression synthesis fabricates source-backed findings without re‑grounding | [#40260](https://github.com/NousResearch/hermes-agent/pull/40260) in progress |

### P2 (High Severity)
| Issue | Description | Fix PR |
|-------|-------------|--------|
| [#31101](https://github.com/NousResearch/hermes-agent/issues/31101) | QQ Bot WebSocket enters endless silent reconnect loop | – |
| [#38412](https://github.com/NousResearch/hermes-agent/issues/38412) | Desktop remote gateway `/api/ws` always returns 4403 for packaged Electron | – |
| [#38488](https://github.com/NousResearch/hermes-agent/issues/38488) | MCP server permanently dead after transient outage – requires gateway restart | – |
| [#38963](https://github.com/NousResearch/hermes-agent/issues/38963) | Hermes desktop startup fails: “no git???” on Windows | – |
| [#40139](https://github.com/NousResearch/hermes-agent/issues/40139) | Secret redaction modifies actual command execution (e.g. `printf`, `sed`) instead of masking only display | – |
| [#40145](https://github.com/NousResearch/hermes-agent/issues/40145) | Windows desktop Chinese input truncation (CJK IME) | – |
| [#40176](https://github.com/NousResearch/hermes-agent/issues/40176) | Pinned Python deps with known CVEs (urllib3, python-multipart, PyJWT, idna) | – |
| [#40225](https://github.com/NousResearch/hermes-agent/issues/40225) | Feishu approval buttons always return “Unauthorized” in DM | – |
| [#26051](https://github.com/NousResearch/hermes-agent/pull/26051) | Fix: preserve context on compression failures (PR open since May 15) | – |

### P3 (Medium/Low Severity)
Numerous P3 bugs were reported, mostly around desktop UI (e.g., [#40226](https://github.com/NousResearch/hermes-agent/issues/40226) – Chinese IME breaks composer, [#40250](https://github.com/NousResearch/hermes-agent/issues/40250) – terminal escape sequences consuming first characters, [#40215](https://github.com/NousResearch/hermes-agent/issues/40215) – remote gateway config error). Many of these are likely dependencies of ongoing i18n and desktop refactoring efforts.

## Feature Requests & Roadmap Signals

The following user‑requested features are likely candidates for the next minor release (v0.16.x or v0.17.0):

- **Japanese and Traditional Chinese desktop locale** – PR [#40114](https://github.com/NousResearch/hermes-agent/pull/40114) already submitted; high community demand.
- **Portuguese (pt-BR) language support** – backend locale already exists (`locales/pt.yaml`); desktop extension seems straightforward.
- **`/approvals` slash command** – to toggle `manual` / `smart` / `off` mid‑session (issue [#39425](https://github.com/NousResearch/hermes-agent/issues/39425); has 1 👍).
- **Telegram clarify choice buttons** – render human‑readable labels instead of bare numbers (issue [#40259](https://github.com/NousResearch/hermes-agent/issues/40259)).
- **ACP OAuth bearer forwarding** – already implemented in PR [#40257](https://github.com/NousResearch/hermes-agent/pull/40257).
- **Gateway health per‑platform** – expose QQBot/LINE etc. adapter status (issue [#40199](https://github.com/NousResearch/hermes-agent/issues/40199)).
- **Schema sanitizer for strict backends** – strip invalid property key characters (issue [#40232](https://github.com/NousResearch/hermes-agent/issues/40232)).

These align with the project’s stated direction of “The Surface Release” – polishing UI, i18n, and platform integrations.

## User Feedback Summary

**Strong satisfaction with core agent architecture** – A Chinese user (#40251) posted a heartfelt thank‑you note praising Hermes’ skill/memory/session_search system as a “truly learnable AI agent” and “genius” design. This reflects deep adoption by power users.

**Frustration around desktop cross‑platform support** – Multiple users reported being unable to run Hermes Desktop on Intel Macs (#37505, #38227) and encountering Chinese IME breakage on Windows (#40146, #40226, #40245). The remote gateway WebSocket error (#38412) also blocks remote‑first workflows.

**Reliability concerns** – Two P1 bugs (cron context leak, compression fabrication) and several P2 reconnection issues (QQ Bot, MCP) indicate that stability in edge cases remains a pain point.

**Translators eager to contribute** – The Portuguese language issue (#40239) garnered a 👍, and the Japanese i18n issue (#40219) has active discussion, showing community willingness to localise.

## Backlog Watch

Several high‑impact items have been open for an extended period without clear resolution:

| Issue/PR | Created | Priority | Notes |
|----------|---------|----------|-------|
| [#9553](https://github.com/NousResearch/hermes-agent/issues/9553) – `reward_functions_library.py` doc error | 2026-04-14 | P3 | Low‑priority documentation fix, but left unresolved for 53 days. |
| [#26051](https://github.com/NousResearch/hermes-agent/pull/26051) – Preserve context on compression failures | 2026-05-15 | P2 | Important stability improvement; still open after 22 days. |
| [#34233](https://github.com/NousResearch/hermes-agent/pull/34233) – Fix LINE inbound media | 2026-05-29 | P3 | Awaiting review/merge for 8 days. |
| [#35277](https://github.com/NousResearch/hermes-agent/pull/35277) – i18n Chinese localization merge | 2026-05-30 | P3 | Large PR with 16 files; needs maintainer approval. |
| [#38488](https://github.com/NousResearch/hermes-agent/issues/38488) – MCP server never reconnects after outage | 2026-06-03 | P2 | No fix PR yet; affects reliability of external tool integrations. |
| [#40176](https://github.com/NousResearch/hermes-agent/issues/40176) – Pinned Python deps with CVEs | 2026-06-05 | P2 | Security‑sensitive; no patch PR has been submitted. |

Maintainer attention is recommended for the P2 security and reliability issues, and for merging the long‑standing i18n and context‑preservation PRs to reduce community frustration.

---

*All links refer to the [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) repository on GitHub.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*