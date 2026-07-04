# OpenClaw Ecosystem Digest 2026-07-04

> Issues: 332 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-04 02:32 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-07-04

## Today’s Overview

OpenClaw remains intensely active, with **332 issues** and **500 PRs** updated in the past 24 hours. Of those, **95 issues were closed** and **59 PRs were merged/closed**, reflecting a healthy rate of progress despite a large backlog. The project is currently in a heavy bug-fixing and hardening phase, with many P1‑rated issues covering security, session state, and message loss. No new releases were cut today; the last public release was `v2026.6.11`. The sheer volume of open work (237 open issues, 441 open PRs) suggests the core team may be stretched, but the high closure rate demonstrates strong operational momentum.

## Releases

No new releases today.

## Project Progress

Today’s merged/closed PRs include:

- **#48942** (closed): `test(gateway): consolidate deriveSessionTitle tests into dedicated module` – Improves test organisation and prevents heartbeat polls from overwriting user‑set session titles.
- **#99759** (closed): `fix(providers): resolve ClawRouter auth-profile models` – Fixes model catalog resolution when the proxy key lives in an auth profile; clears stale catalogs on refresh.

Closed issues among the top 50 include:

- **#6731** – Safe/unsafe ClawdBot feature request (closed after discussion, likely superseded by other permission work).
- **#75593** – Subagents list still empty after spawn (closed, appears fixed).
- **#98528** – Tool output returns empty after first call per turn on `v2026.6.11` (regression, closed as fixed).
- **#97871** – Agent `--local` hangs with local providers (closed, likely fixed or needs‑info resolved).

These closures indicate targeted regression fixes and test improvements are reaching the main branch.

## Community Hot Topics

The most discussed issues this week (by comment count) focus on reliability and security:

- **#25592** (33 comments) – *Text between tool calls leaks to messaging channels*. A major UX/security concern: internal processing acknowledgments and error messages often appear as visible chat messages. Users strongly support a solution that suppresses “noise” text.

- **#99551** (14 comments) – *Codex worker runaway hardening sprint*. After an incident, this tracker issue outlines the need to prevent uncontrolled resource consumption by Codex workers. It is a high‑priority umbrella.

- **#73148** (14 comments) – *Image tool: opaque “Failed to optimize image” when sharp is not installed*. Causes frustrating silence for users on minimal environments.

- **#12602** (13 comments) – *Slack Block Kit support for agent messages*. High demand from Slack‑centric teams for richer interactive responses (CRMs, dashboards, etc.).

- **#10659** (13 comments) – *Masked Secrets – Prevent agent from accessing raw API keys*. Strong consensus that credentials should be usable but not readable by the agent.

- **#92043** (11 comments) – *180s compaction timeout fails on legitimate long compactions*. A performance bug that can permanently stall sessions with long histories.

- **#98416** (11 comments) – *Published dist missing reentrancy guard* – a critical regression in `v2026.6.11`.

The underlying needs are clear: users expect **no‑leak agent outputs**, **graceful handling of missing dependencies**, **richer delivery formats**, and **stronger security boundaries** around secrets.

## Bugs & Stability

**Critical/P1 regressions and reliability bugs** reported in the last 24 hours:

| Issue | Summary | Severity | Fix PR / Status |
|-------|---------|----------|-----------------|
| #98416 | Missing reentrancy guard in published dist – reply session initialisation conflict | 🔴 Regression, message‑loss | No dedicated PR yet, linked to #98236? |
| #98528 | Tool output (exec, web_fetch, web_search) returns empty after first call per turn (v2026.6.11) | 🔴 Regression | **Closed** (fix merged) |
| #92043 | 180s compaction timeout fails identically each turn – no partial progress reuse | 🔴 Performance stall, message‑loss | #92043 open, no fix PR yet |
| #90361 | Intermittent `memory_search` "index metadata is missing" – likely search/reindex race | 🟠 Regression, session‑state | #90361 open, local hotfix exists |
| #92241 | Gateway holds stale module import paths after update/rollback – messages silently dropped | 🟠 Regression, message‑loss | #92241 open |
| #97871 | Agent `--local` hangs with Ollama/LM Studio (while capability model succeeds) | 🟠 Symptom, crash‑loop | **Closed** |
| #99241 | Tool outputs render as `(see attached image)` placeholders – agent blinded | 🟠 Message‑loss | #99241 open |

**Today’s new fix PRs** (opened in last 24h) that target stability:

- **#99516** – `fix(runtime): guard JSON.stringify against circular tool output` – prevents crashes on circular references.
- **#99747** – `fix: protect uncovered cleanup window in runCodexAppServerAttempt` – prevents resource leaks in Codex app‑server.
- **#99164** – `fix(agents): classify Anthropic refusal and OpenAI content_filter as failover-eligible` – enables fallback when providers return safety refusals.
- **#98236** – `refactor: flip sessions and transcripts to sqlite storage` – large refactor to eliminate race‑prone JSONL files.

The project is actively addressing multiple regressions, but some high‑impact bugs (compaction timeout, memory index race) still lack a committed fix.

## Feature Requests & Roadmap Signals

The most‑upvoted feature requests reveal strong community priorities:

- **#10659** (Masked Secrets, 4 👍) – Expected in a near‑term release given the security focus and PM attention.
- **#12602** (Slack Block Kit, 0 👍 but 13 comments) – High engagement; likely to appear once core stability improves.
- **#12678** (Capability‑based permissions for skills/tools) – Complements the permission manifest (#12219) and the denylist request (#6615).
- **#35203** (Multi‑Agent Collaboration: capability profiling, shared blackboard, layered memory) – An ambitious RFC; unlikely in the next minor release but signals future architecture.
- **#13616** (Backup/restore utility for config, cron, sessions) – Common request for production deployments.
- **#12855** (Built‑in auto‑update with schedule/confirmation) – Could appear in the next maintenance release.
- **#9986** (Model fallback on context length exceeded) – Small change that improves user experience greatly.

**Prediction for next version (v2026.7.x)**: Likely includes Masked Secrets, Slack Block Kit (partial), and auto‑update. The large SQLite session migration (#98236) may land if merge risk assessments pass.

## User Feedback Summary

**Pain points expressed:**

- *“Internal processing output leaks to Slack – my agents look broken.”* (#25592)
- *“`Failed to optimize image` on every image – no hint that `sharp` is missing.”* (#73148)
- *“Onboarding never asked for embedding provider – memory doesn’t work out of the box.”* (#16670)
- *“OAuth refresh failures wedge the agent for hours without alerting.”* (#86215)
- *“Tool schemas cost 3500 tokens per session – wasted context.”* (#14785)
- *“TUI doesn’t support multi‑line input – Shift+Enter needed.”* (#10118)
- *“No emoji/unicode toggle for screenreaders.”* (#9637)

**Positive signals:**

- Users appreciate the high velocity of fixes (many closed issues today: tool output regression, local‑provider hang).
- Community members are contributing substantial PRs (SQLite refactor, onboarding overhaul, iOS setup flow).
- The “ClawSweeper” automated fix‑bot (#75469) is actively closing stability gaps.

**Satisfaction trend:** The community remains engaged and constructive, but frustration with regressions in the latest release (`v2026.6.11`) is palpable. The number of open P1 bugs (15+) suggests quality gates should be tightened before the next release.

## Backlog Watch

Issues and PRs that appear stuck or in need of maintainer attention:

| Item | Age | Status | Reason for watch |
|------|-----|--------|------------------|
| #12602 (Slack Block Kit) | 2026-02-09 (5 months) | `needs‑maintainer‑review`, `needs‑product‑decision` | High community interest but no PR or decision. |
| #10659 (Masked Secrets) | 2026-02-06 (5 months) | Same tags | Critical security feature; may need a product sponsor. |
| #16670 (Memory in onboarding) | 2026-02-15 (4.5 months) | `needs‑maintainer‑review`, `needs‑product‑decision` | Low‑effort improvement, arguably a bug. |
| #6615 (Denylist for exec‑approvals) | 2026-02-01 (5 months) | Similar tags + `needs‑security‑review` | 7 👍 – strong community support. |
| PR #61960 (i18n docs postprocess) | 2026-04-06 (3 months) | `waiting on author` | Stalled; may need rebase or renewed attention. |
| PR #75469 (heartbeat starvation fix) | 2026-05-01 (2 months) | `needs proof` | ClawSweeper bot contribution – seems close but missing evidence. |
| PR #98236 (SQLite session storage) | 2026-06-30 (4 days) | `waiting on author` (flagged) | Large refactor with high merge risk; maintainer review critical. |

Maintainers should prioritise reviewing the high‑risk PRs (#98236, #73399) and unblocking the long‑standing Slack Block Kit and Masked Secrets requests to sustain community trust.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Agent Ecosystem

## 1. Ecosystem Overview

The personal AI agent open-source landscape in mid-2026 is characterized by rapid iteration on core reliability while expanding platform integrations. Both OpenClaw and Hermes Agent show intense community engagement, with daily issue volumes exceeding 50 per project, signaling strong adoption but also straining maintainer capacity. The ecosystem is shifting from experimental prototyping to production-grade hardening, with security boundaries (secret isolation, credential multiplexing), session state durability, and cross-platform authentication emerging as universal pain points. A clear tension exists between feature velocity and regression stability, with both projects accumulating high-severity bugs in recent releases that erode user trust. The community is self-organizing around contributor-driven fixes and automated bot triage, suggesting the ecosystem is maturing but still lacks systematic quality gates.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues updated (24h)** | 332 | 50 |
| **Issues closed (24h)** | 95 | 3 |
| **Open issues** | 237 | 47 |
| **PRs updated (24h)** | 500 | 50 |
| **PRs merged/closed (24h)** | 59 | 7 |
| **Open PRs** | 441 | 43 |
| **Last release** | v2026.6.11 (23 days ago) | v0.18.0 (implied, older) |
| **Health score** | 🟡 Moderate | 🟢 Good |

**Health score rationale:** OpenClaw's closure rate (29% of issues, 12% of PRs) is lower despite higher absolute volume, and 15+ P1 bugs remain open. Hermes has a smaller backlog but a similarly low closure percentage (6% issues, 14% PRs). Both projects are bottlenecked on maintainer review capacity relative to community input volume.

## 3. OpenClaw's Position

**Advantages:**
- **Largest community scale** by an order of magnitude (332 daily issues vs. 50 for Hermes), providing broader testing coverage and faster bug discovery
- **Higher fix velocity:** 59 PRs merged/closed in 24h demonstrates strong operational momentum despite backlog
- **Security maturity:** Dedicated automated fix bot (ClawSweeper) and active P1 regression triage
- **Reference implementation status:** Acts as de facto specification for the ecosystem, attracting more contributor PRs (including large refactors like SQLite session migration)

**Technical approach differences:**
- OpenClaw employs a **heavyweight core** with a native TUI, multi-provider gateway, and SQLite-based session storage (migrating from JSONL)
- Hermes is **lighter-weight**, relying on Docker deployment and platform-specific gateways (Telegram, Discord, Desktop app)
- OpenClaw focuses on **protocol-level features** (compaction, memory search indexing, reentrancy guards), while Hermes emphasizes **platform integration** (Telegram callbacks, Linear plugin, WhatsApp groups)

**Community size comparison:** OpenClaw's issue count is ~7× Hermes', suggesting a 5-10× larger user base. However, Hermes' community is more engaged per-issue (higher comment density on feature requests), indicating a smaller but more vocal power-user segment.

## 4. Shared Technical Focus Areas

| Focus Area | Projects Affected | Specific Needs Expressed |
|------------|-------------------|--------------------------|
| **Secret/key isolation** | OpenClaw (#10659), Hermes (#48441, #57955) | Agents should use credentials without reading them; tool output must not leak tokens |
| **Session state reliability** | OpenClaw (#92043 compaction stall, #90361 index race), Hermes (#58010 `/resume` crash) | Crash-safe persistence, no silent data loss under contention |
| **OAuth token lifecycle** | OpenClaw (#86215 refresh failures), Hermes (#12058, #48534) | Gateway-specific auth propagation, refresh retry with backoff, User-Agent overrides |
| **Missing dependency handling** | OpenClaw (#73148 sharp missing), Hermes (#57905 cua-driver Windows) | Graceful error messages instead of opaque failures |
| **Rich message formatting** | OpenClaw (#12602 Slack Block Kit), Hermes (#40173 Telegram channel_profiles) | Interactive responses beyond plaintext (CRMs, dashboards, per-chat routing) |
| **Multi-provider failover** | OpenClaw (#99164 Anthropic failover classification), Hermes (implied in model config) | Provider-agnostic fallback on safety refusals or context length exceeded |

**Emerging pattern:** Both communities are demanding **security-by-default** where secrets and write-protected files are never exposed to agent reasoning loops, and **graceful degradation** when dependencies or providers fail.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Target user** | Power users, self-hosters, enterprise deployments | Individual developers, Slack/Telegram-centric teams, Docker users |
| **Primary deployment** | Native binary + TUI | Docker container + platform gateways |
| **Feature emphasis** | Core agent reliability, session management, tool security | Platform integration (Telegram, Discord, Linear, Desktop), callbacks |
| **Architecture** | Monolithic core with plugin tools | Modular gateway multiplexer with profile-based routing |
| **Memory strategy** | Search-indexed memory with compaction | Hindsight memory with multi-bank routing (proposed) |
| **UI complexity** | Full TUI with multi-line input issues (#10118) | Desktop app with WebSocket loop, platform-specific UIs |
| **Release cadence** | Frequent point releases (v2026.x.x) | Semantic versioning (v0.18.x) – slower, more conservative |
| **Community contribution style** | Large refactors (SQLite migration) + automated bot fixes | Smaller, targeted PRs (Telegram callbacks, OAuth fixes) |

**Key insight:** OpenClaw is optimizing for **technical robustness** (session durability, memory consistency), while Hermes is optimizing for **platform reach** and **configuration flexibility**. This reflects different stages: OpenClaw is hardening a mature core, Hermes is still building out core integrations.

## 6. Community Momentum & Maturity

**Activity tiers:**

| Tier | Characteristic | OpenClaw | Hermes |
|------|---------------|----------|--------|
| **Velocity** | Issues/PRs per day | Very high (300+) | High (50+) |
| **Closure rate** | % of items resolved daily | Moderate (29% issues, 12% PRs) | Low (6% issues, 14% PRs) |
| **Feature iteration** | New features merged | Moderate (test consolidation, auth fixes) | Moderate (Telegram callbacks, achievements export) |
| **Stability phase** | Bug-fixing vs. feature-building | **Heavy bug-fixing** (15+ P1 bugs) | **Mixed** (critical bugs + new features) |
| **Backlog aging** | Issues >2 months unresolved | 5+ items in "needs-maintainer-review" | 6+ items, oldest 4 months |

**Momentum assessment:**
- **OpenClaw** is rapidly iterating but in a **stability crisis** – the large number of regressions in v2026.6.11 suggests quality gates are insufficient. The community remains engaged and contributing, but maintainer attention is fragmented across too many fronts.
- **Hermes** is growing steadily with manageable backlog, but OAuth token handling and credential isolation are recurring friction points that could limit enterprise adoption. The smaller community scale may actually be an advantage for focused triage.

**Prediction:** Hermes will likely ship its next release (v0.19.0) sooner than OpenClaw's next major release, despite OpenClaw's higher velocity, because OpenClaw's regression burden is heavier.

## 7. Trend Signals

**Industry trends extracted from community feedback:**

1. **Agent output hygiene is non-negotiable** (OpenClaw #25592, Hermes #48441). Users expect internal processing messages (acknowledgments, error traces, tool status) to be suppressed from downstream channels. This is both a security concern (secret leakage in logs) and a UX concern (agents appearing "broken"). Expect agent frameworks to adopt explicit output filtering layers.

2. **Credential isolation is the new perimeter** (OpenClaw #10659, Hermes #57955). As agents gain tool access (files, APIs, databases), the threat model shifts from "user can't access secrets" to "agent can't expose secrets." Masked secrets and path-based write protection are becoming baseline requirements, not nice-to-haves.

3. **Cross-platform authentication remains unsolved** (OpenClaw #86215, Hermes #12058, #48534). OAuth token exchange fails unpredictably across gateways (Telegram vs. CLI vs. Desktop), with User-Agent blocking and Cloudflare challenges as common blockers. Expect deep integration with identity providers to become a differentiator.

4. **Session state durability is a trust metric** (OpenClaw #92043 compaction stall, Hermes #58010 `/resume` crash). Users equate reliable session state with agent competence. Compaction timeouts, index races, and silent commit failures erode trust faster than feature gaps.

5. **Configuration discoverability is a hidden UX burden** (Hermes #12188 Docker docs, OpenClaw #16670 embedding provider). Users consistently report frustration with opaque configuration and poor onboarding flows. Expect "setup wizards" and environment-variable-first config to become table stakes.

6. **Graceful dependency handling separates production from hobby** (OpenClaw #73148 sharp missing, Hermes #57905 cua-driver). Inconsistent or missing optional dependencies should produce actionable error messages, not silent failures or placeholder images.

7. **Predictive performance matters** (Hermes #57903 GIL busy-polling, OpenClaw #14785 tool schema token cost). Users are sensitive to wasted CPU cycles, token budgets, and blocked event loops. Efficient async patterns and token-aware caching will be competitive advantages.

**Value for AI agent developers:**
- **Invest in output hygiene early** – implement a suppression layer for internal messages before shipping to production
- **Default to masked secrets** – make credential non-readability the default, not an opt-in feature
- **Prefer synchronous OAuth refresh with retry** – unreliable auth is the top complaint in both communities
- **Prioritize session crash recovery** – users trust agents that survive restarts without data loss
- **Provide Docker-first configuration** – environment variables over CLI commands for repeatable setups

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-04

## 1. Today’s Overview

The project shows **very high activity** with 50 issues and 50 pull requests updated in the last 24 hours. Of these, 3 issues were closed and 7 PRs were merged or closed, while the vast majority remain open (47 issues, 43 PRs). No new releases were published today. The pulse is driven by a mix of **critical bug reports**—especially around session state corruption, OAuth token handling, and multiplexed gateway credential isolation—and **feature requests** spanning platform integrations (Linear, Feishu, Telegram), memory enhancements, and desktop UI improvements. Security concerns continue to surface, with several reports about plaintext secret leakage and bypass of write-protection mechanisms. The community is highly engaged, filing detailed reproduction steps and even contributing draft fixes.

## 2. Releases

**None** in the latest data. The last tagged release appears to be v0.18.0 (implied from environment strings in issues). No migration notes or changelogs today.

## 3. Project Progress

Seven pull requests were merged or closed today. Notable ones include:

- **#58012** – *feat(achievements): add export endpoint and agent summary* – Implements the first part of the achievements export workstream, allowing agents to surface progress programmatically.
- **#57999** – *feat(telegram): add external callback handlers* – Adds prefix-based callback data dispatch to local scripts, configurable through `telegram.extra.callback_handlers`.
- **#56074** – *fix: reset in-memory OpenRouter catalog cache on `/model --refresh`* – Stops stale model lists from persisting after a refresh command.
- Additional merges (not shown in top 20) likely include minor fixes for session search and MCP handshake compatibility.

These indicate steady progress on **platform extensibility** (Telegram callbacks, Linear agent PR #57734 is still open but advancing) and **quality-of-life fixes** for configuration refresh and achievement visibility.

## 4. Community Hot Topics

The most active discussions (by comment count and reactions) reveal recurring needs:

- **#7269** ([WhatsApp groups & `require_mention` per-user filtering](https://github.com/NousResearch/hermes-agent/issues/7269)) – 5 comments. User wants the bot to reply to group mentions without whitelisting all members, but still restrict non-mention messages.
- **#12058** ([OpenAI Codex OAuth works in CLI but fails on Telegram gateway](https://github.com/NousResearch/hermes-agent/issues/12058)) – 5 comments. Gateway-specific authentication isolation remains a pain point.
- **#48441** ([Terminal session snapshots leak .env secrets to disk](https://github.com/NousResearch/hermes-agent/issues/48441)) – 5 comments, 1 reaction (closed as security). Important fix merged earlier; community appreciates the response.
- **#12188** ([Setting model config in Docker via environment variables](https://github.com/NousResearch/hermes-agent/issues/12188)) – 5 comments, 2 reactions. Users want to avoid entering the container for `hermes model` commands.
- **#40173** ([Telegram `channel_profiles` for per-chat routing](https://github.com/NousResearch/hermes-agent/issues/40173)) – 3 comments, 3 reactions. A popular feature request (👍) to support multiple agent personalities in a single bot.

**Underlying need:** The community heavily desires **multiplexing and credential isolation** across gateways and profiles, as well as **easier configuration** (Docker, environment variables). Security concerns around tool-generated output (terminal, file operations) are flagged frequently.

## 5. Bugs & Stability

Several **new bugs reported today** (2026-07-04) are ranked by severity:

| Issue | Description | Severity | Fix PR exists? |
|-------|-------------|----------|----------------|
| #58010 | `/resume` crashes with `TypeError` because `AsyncSessionDB` coroutines are not awaited in `slash_commands.py` | **P1** (session state broken) | No |
| #58009 | Tool output > ~1KB silently replaced with `<<ccr:...>>` content reference tags – breaks all tools | **P2** (data loss) | No |
| #57928 | Telegram file attachments dropped when used with `/steer`, `/goal`, `/subgoal` commands | **P2** (message delivery broken) | No |
| #57903 | Async LLM calls busy-poll the GIL, blocking Desktop WebSocket loop – fixed in draft PR #57933 | **P2** (desktop performance) | Yes (#57933) |
| #57905 | `computer_use` on Windows fails to discover windows due to wrong field parsing (cua-driver 0.7.0) | **P2** (platform-specific) | No |
| #57923 | Agent entered an infinite loop again – needs repro, but pattern known | **P2** (stability) | No |
| #57967 | `hermes kanban create` returns task ID before COMMIT – silent loss under contention | **P3** (data integrity race) | No |
| #57955 | Terminal tool bypasses SOUL.md write-protection via `sed -i` – security bypass | **P3** (security boundary) | No |
| #57986 | `/journey` crashes when skill frontmatter is not a dict | **P3** (usability) | No |

Also notable from recent days:
- **#54675** (P2, open): Multiplexed gateway uses default profile’s bot token for all secondary profiles – credential isolation broken.
- **#48441** (closed): Terminal snapshot plaintext secret leak – fix merged.
- **#48534** (P1, open): Anthropic OAuth token exchange fails with 404 due to User-Agent block.

**Trend:** Repeated issues around **OAuth token handling** (Anthropic, OpenAI Codex) and **gateway multiplexing** suggest these are the project’s most fragile subsystems. Desktop-specific bugs (Windows console flashes, session wrong project) are also accumulating.

## 6. Feature Requests & Roadmap Signals

**Recently merged/closed features:**
- #58012 – Achievements export endpoint.
- #57999 – Telegram external callback handlers.

**Open high-interest feature requests:**
| Issue | Description | Potential next version inclusion |
|-------|-------------|----------------------------------|
| #624 | Automatic session title generation (inspired by DeerFlow) – lightweight LLM call after first exchange | **Likely** – non-breaking, small code footprint |
| #17790 | Configurable Discord voice inactivity timeout | **Likely** – simple config variable |
| #31776 | Multi-bank routing for Hindsight memory tools | **Possible** – requires memory provider refactoring |
| #40173 | Telegram `channel_profiles` to route per-chat to different Hermes profiles | **High community demand** (3 👍) – but touches profile multiplexing |
| #46337 | UI for local STT/TTS and media generation providers in Hermes Desktop | **Likely** – desktop UX is active area |
| #50668 | Telegram cron delivery should optionally create fresh DM topic per execution | **Possible** – cron workflow improvement |
| #57973 | Expose per-model MoA usage accounting (privacy-safe) | **Possible** – telemetry feature |
| #54588 (PR) | Configurable attribution string for agent identity | Already in review – could ship soon |

**Predictions for next release (v0.19.0):** Based on community activity and PRs in flight, expect improvements to **multiplex credential isolation** (#57563 PR is large, fixing BWS/OAuth hijack), **Telegram callback support**, **Anthropic OAuth retry** (#58014 PR), and **desktop session management fixes**. The Linear Agent platform plugin (#57734) may also land.

## 7. User Feedback Summary

**Pain points expressed by users:**
- *“I would not like to allow all users as a general configuration, but is interesting reply to members of a group without explicit permission.”* (#7269) – Permission granularity is insufficient for group chats.
- *“The documentation for Docker compose is rather lackluster.”* (#12188) – Configuration discoverability is poor; users forced to `exec` into containers.
- *“I'm seeing what looks like a gateway-specific auth issue with openai-codex.”* (#12058) – Authentication is not uniformly propagated across platforms.
- *“The Save button now flushes the live contentEditable editor … matching the already-safe Enter/submit path.”* (PR #58018) – Desktop editor race conditions affect daily use.
- *“Silent commit failure under gateway contention”* (#57967) – Data loss without any error message erodes trust.
- *“Terminal tool lacks protected-file path validation … bypasses SOUL.md write-protection.”* (#57955) – Security boundaries are incomplete for power users.

**Satisfaction signals:** Fast turnaround on security issues (e.g., #48441 was addressed quickly), active community contributing PRs (#58019, #58014, etc.), and detailed bug reports indicate a healthy, engaged user base.

## 8. Backlog Watch

Several important open issues have not received maintainer responses or have been dormant for weeks:

| Issue | Age | Comments | Reason for attention |
|-------|-----|----------|----------------------|
| #7269 | 3 months (since April 10) | 5 | WhatsApp group permission design – likely requires architectural discussion |
| #624 | 4 months (since March 7) | 4 | Lightweight feature with high value – no roadmap commitment |
| #12058 | 2.5 months (since April 18) | 5 | Gateway-specific OAuth regression – affects real deployments |
| #6347 | 3 months (since April 9) | 2 | Anthropic OAuth refresh fails with Cloudflare 403 – no resolution |
| #25106 | 1.5 months (since May 13) | 3 | CLI model switch persist bug – impacts all manual model changes |
| #31776 | 1.5 months (since May 25) | 4 | Memory multi-bank feature – limited traction but high utility |
| #40173 | 1 month (since June 5) | 3 | Popular feature (3 👍) – no maintainer response |

**Recommendation:** The project would benefit from **explicit triage responses** on these older issues, even if only to set expectations about priority or request more information. The number of long-unanswered feature requests and bugs suggests the maintainers may be overwhelmed by the sheer volume of incoming issues (50/day). Consider labeling issues that need “maintainer review” or “good first issue” to distribute load.

---

*Data source: GitHub data for NousResearch/hermes-agent as of 2026-07-04, limited to top 30 issues and top 20 PRs updated in last 24h.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*