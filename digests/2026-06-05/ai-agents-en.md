# OpenClaw Ecosystem Digest 2026-06-05

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-05 03:25 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-05

## 1. Today’s Overview

Project activity remains extremely high, with 500 issues and 500 pull requests updated in the last 24 hours. Of these, 351 issues are open/active, 149 closed, while on the PR side 397 are still open and 103 were merged or closed. No new releases were published today. The volume suggests a community in full production use, with many reports pointing to regressions after the recent `2026.5.22`–`2026.6.1` upgrades and ongoing migrations (SQLite, Codex runtime). Several critical P1 bugs have surfaced, many with clear reproduction steps but lacking associated fix PRs, indicating a backlog of unresolved stability issues.

## 2. Releases

*(No new releases today.)*

## 3. Project Progress

103 pull requests were merged or closed in the last 24 hours. Among the most notable from the top‑30 list:

- **#90304** (closed): Added a `memory.qmd.rerank` toggle to allow QMD query mode without reranking – a user‑requested feature.
- **#90527** (closed): Introduced `ReplyPayload.origin` metadata to tag cron‑driven payloads, helping channel adapters distinguish scheduler sends from assistant replies.
- **#89483** (open, AI‑assisted): Persists agent‑run error replies in chat history so Control UI does not lose them after a refresh – merged to improve WebChat reliability.
- **#90399** (open): Fixes missing `content‑type` header on ChatGPT Responses SSE streams, addressing a recent OpenAI transport regression.
- **#90389** (open): Anchors Mattermost slash command state on `globalThis` to fix the persistent `503 “not yet initialized”` error reported in #68113.
- **#90060** (open): Preserves unrelated lines during fuzzy text matching in edit operations, fixing a subtle content corruption bug.

These merged/open PRs signal active progress on the Codex‑to‑Pi runtime parity, SQLite migration, and improved error handling across channel integrations.

## 4. Community Hot Topics

The most active issues (by comment count) reflect deep frustrations with connectivity, session state, and provider compatibility:

| Issue | Comments | Summary |
|-------|----------|---------|
| [#72808](https://github.com/openclaw/openclaw/issues/72808) | 20 | P1: Silent Slack connection loss after days of stable use – bot went dark mid‑demo. |
| [#88838](https://github.com/openclaw/openclaw/issues/88838) | 17 | P2: Tracking the core session/transcript SQLite migration via branch‑by‑abstraction to avoid a large risky rewrite. |
| [#80171](https://github.com/openclaw/openclaw/issues/80171) | 15 (closed) | Codex‑vs‑Pi runtime parity QA harness – closed but referenced by multiple follow‑ups. |
| [#65161](https://github.com/openclaw/openclaw/issues/65161) | 14 | P2: Heartbeat isolated mode regressions – cadence stalls, mislabeled exec‑events, heavy context. |
| [#87307](https://github.com/openclaw/openclaw/issues/87307) | 13 | P1: Matrix thread replies sent as normal replies on `2026.5.22`; `/status` and `/model` silent. |
| [#90083](https://github.com/openclaw/openclaw/issues/90083) | 11 | P1: OpenAI ChatGPT Responses transport fails with `invalid_provider_content_type` for `gpt‑5.4`/`gpt‑5.5` on `2026.6.1`. |
| [#68113](https://github.com/openclaw/openclaw/issues/68113) | 11 | P1: Mattermost slash commands return 503 “not yet initialized” – regression since `2026.4.15`. |

The underlying needs are clear: users expect **reliable long‑running connections** (Slack, Mattermost, Matrix), **glitch‑free session migration** to SQLite, and **compatibility with the latest OpenAI models**. The high comment counts indicate these bugs are widely reproduced and blockers for production deployments.

## 5. Bugs & Stability

Several new high‑severity bugs appeared (or were updated) in the last 24 hours:

| Severity | Issue | Description | Affected Version | Fix PR? |
|----------|-------|-------------|------------------|---------|
| **P1** | [#90083](https://github.com/openclaw/openclaw/issues/90083) | OpenAI ChatGPT Responses transport fails on `gpt‑5.4`/`gpt‑5.5` with `invalid_provider_content_type`. | `2026.6.1` | No |
| **P1** | [#90093](https://github.com/openclaw/openclaw/issues/90093) | Native replay sends encrypted reasoning, causing next turn to fail with `invalid_encrypted_content`. | `2026.6.1` | No |
| **P1** | [#90072](https://github.com/openclaw/openclaw/issues/90072) | Cron state silently wiped during SQLite migration on upgrade to `2026.6.1` – 44 of 45 jobs lost. | `2026.5.28`→`2026.6.1` | No |
| **P1** | [#90082](https://github.com/openclaw/openclaw/issues/90082) | Active‑memory circuit breaker too aggressive; fallback prompt pollutes main session context. | `2026.6.1` | No |
| **P1** | [#90036](https://github.com/openclaw/openclaw/issues/90036) | Session model route drifts from `openai/gpt‑5.5` to `openai‑codex/gpt‑5.5` after native Codex turn. | `2026.6.1` | No |
| **P1** | [#88929](https://github.com/openclaw/openclaw/issues/88929) | Feishu streaming card truncated to last character when card render mode is enabled. | `2026.6.1`? | No |

Notable older regressions still open and without fix PRs:

- [#63216](https://github.com/openclaw/openclaw/issues/63216) – Repeated hard resets on same session despite high `reserveTokensFloor`.
- [#67777](https://github.com/openclaw/openclaw/issues/67777) – Subagent completion delivery lost on timeout/drain/orphan prune.
- [#64810](https://github.com/openclaw/openclaw/issues/64810) – Heartbeat interrupts in‑progress replies in Telegram topic sessions.

**Positive note:** PR #90399 now addresses the missing `content‑type` issue (related to #90083’s root cause) and PR #90389 finally fixes the enduring Mattermost 503 regression (#68113).

## 6. Feature Requests & Roadmap Signals

Several user‑requested enhancements are gaining traction, many with detailed RFC‑style issues:

- **Sensitive data masking** – [#64046](https://github.com/openclaw/openclaw/issues/64046) calls for API keys and secrets to be encrypted/redacted in config files, logs, and UI. Given the security‑focused label (`impact:security`) and diamond‑lobster rating, this is a high‑priority candidate for the next release.
- **Multi‑index embedding memory** – [#63990](https://github.com/openclaw/openclaw/issues/63990) proposes model‑aware failover across embedding providers to avoid vector semantic corruption. Already labelled `P2` with a clear design; likely to be scheduled soon.
- **Anthropic advisor tool** – [#63930](https://github.com/openclaw/openclaw/issues/63930) requests support for Claude’s server‑side advisor tool. As Anthropic releases more server‑side tools, this becomes a competitive differentiator.
- **Control UI plugin contribution slots** – [#71736](https://github.com/openclaw/openclaw/issues/71736) outlines data‑driven UI slots for chat modes, approval cards, input guards – a major SDK expansion that would enable third‑party UI customisation.
- **Discord access list overhaul** – [#69748](https://github.com/openclaw/openclaw/issues/69748) wants role‑based and per‑channel permissions instead of the current `requireMention` / `users` allowlist.

These features align with the ongoing Codex runtime migration and the push toward a more extensible, enterprise‑ready platform.

## 7. User Feedback Summary

Real user pain points captured from the latest issues:

- **“Lost connection mid‑demo”** – tleyden on #72808: a Slack bot that worked for days suddenly went silent, humiliating during a live demo.
- **“44 cron jobs vanished without warning”** – wlassalle724 on #90072: upgrade to `2026.6.1` wiped almost all scheduled jobs with no backup or notification.
- **“Every turn wastes 20‑30% tokens on bootstrap files”** – Ekko‑2xko on #67419: users running budget models are frustrated by context bloat from re‑injected files.
- **“Matrix thread replies regressed to normal replies”** – sibbl on #87307: a breaking change in `2026.5.22` that undermines Matrix group workflows.
- **“QQBot now shows raw `<thinking>` blocks”** – openperf on #90132 (fix PR open): after upgrading to `2026.5.28`, users see unfiltered reasoning content.

Satisfaction signals are rarer but evident in closed issues – e.g., #80171 (Codex parity QA harness) closed after spawning several derivative tracking issues, suggesting the community is engaged in helping improve the runtime transition.

## 8. Backlog Watch

Several important issues have been open for weeks or months without a corresponding fix PR, despite high severity and community demand:

| Issue | Opened | Last Update | Severity | Summary |
|-------|--------|-------------|----------|---------|
| [#72808](https://github.com/openclaw/openclaw/issues/72808) | 2026‑04‑27 | 2026‑06‑04 | P1 | Silent Slack disconnect – no root cause identified |
| [#65161](https://github.com/openclaw/openclaw/issues/65161) | 2026‑04‑12 | 2026‑06‑04 | P2 | Multiple heartbeat‑isolated‑mode regressions |
| [#63216](https://github.com/openclaw/openclaw/issues/63216) | 2026‑04‑08 | 2026‑06‑04 | P1 | Repeated hard resets on same session despite high reserve |
| [#67777](https://github.com/openclaw/openclaw/issues/67777) | 2026‑04‑16 | 2026‑06‑04 | P1 | Subagent completion delivery loss |
| [#68113](https://github.com/openclaw/openclaw/issues/68113) | 2026‑04‑17 | 2026‑06‑04 | P1 | Mattermost slash commands 503 *(fix PR #90389 now open)* |
| [#64046](https://github.com/openclaw/openclaw/issues/64046) | 2026‑04‑10 | 2026‑06‑04 | P1 (impact:security) | Sensitive data in plaintext – no progress |

These issues all carry `clawsweeper:no‑new‑fix‑pr` tags, indicating they are acknowledged but not yet assigned for implementation. The next maintainer sprint should prioritise at least the P1 security and stability items to prevent further erosion of user trust.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report: AI Agent Open-Source Landscape

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing a period of intense production adoption, marked by high community engagement but also significant stability challenges. Both OpenClaw and Hermes Agent show 24-hour activity volumes indicative of large, active user bases—OpenClaw with 500+ issues/PRs and Hermes with 50+ each—suggesting these projects have crossed the chasm from experimental to production deployment. The dominant theme across both ecosystems is the tension between rapid feature iteration and reliability: users are demanding production-grade connection stability, session persistence, and platform-specific integrations, while maintainers are managing complex runtime migrations (Codex-to-Pi in OpenClaw) and security hardening. Community feedback reveals that reliability regressions, especially around connection drops and data loss during upgrades, are the most critical pain points eroding user trust. Both projects are also responding to increasing demand for enterprise features—RBAC, permission tiers, and secure credential handling—indicating a shift from single-user tinkering toward multi-user, multi-platform deployments.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues Updated (24h)** | 500 (351 open, 149 closed) | 50 (38 open, 12 closed) |
| **PRs Updated (24h)** | 500 (397 open, 103 merged/closed) | 50 (44 open, 6 merged/closed) |
| **New Release Today** | No | No |
| **Latest Stable Version** | 2026.6.1 (implied) | v0.15.1 |
| **P1/P0 Bugs Open (24h)** | 6 new P1s, none with fix PRs | 0 P0, ~8 P2s, several with fix PRs |
| **Community Responsiveness** | Issues linger longer; high comment counts (11–20) for critical bugs | Issues closed within hours; maintainer response visible |
| **Health Score** | 🟡 **Moderate** — High volume but significant regressions and unresolved P1s | 🟢 **Strong** — Responsive team, quick closures, proactive security fixes |

**Assessment:** OpenClaw shows 10× the raw activity of Hermes but with a larger unresolved backlog and more severe regressions. Hermes demonstrates better issue-to-resolution velocity despite smaller scale.

## 3. OpenClaw's Position

**Advantages:**
- **Reference implementation status** — As `github.com/openclaw/openclaw`, it serves as the core reference for the ecosystem, attracting the most contributor attention and the broadest channel integration support (Slack, Mattermost, Matrix, Feishu, Discord, QQBot)
- **Aggressive feature velocity** — 103 PRs merged/closed daily indicates a maintainer team capable of absorbing large amounts of community contribution
- **Migration-driven innovation** — The SQLite session migration and Codex-to-Pi runtime parity effort, while painful, positions OpenClaw for a more modular, performant architecture
- **Deep platform-specific support** — Feishu streaming cards, Matrix thread handling, Mattermost slash commands — niche but valuable for enterprise users

**Technical Approach Differences:**
- **Runtime architecture:** OpenClaw is undergoing a major runtime migration (Codex → Pi), creating temporary instability but long-term architectural benefits. Hermes appears more stable with its existing runtime.
- **Session storage:** OpenClaw's SQLite migration (tracked in #88838) is a branch-by-abstraction effort, indicating a legacy storage overhaul. Hermes does not show similar storage migration signals.
- **Channel adapter model:** OpenClaw has a more granular channel adapter system (ReplyPayload.origin metadata, cron state handling) suggesting a platform-first design philosophy.

**Community Size Comparison:**
- OpenClaw's 500 daily issues/PRs vs. Hermes' 50 suggests an order-of-magnitude larger community base
- OpenClaw's issue comment counts (11–20 on top bugs) indicate deeper community engagement and reproduction efforts
- Hermes' faster closure times suggest a smaller but more maintainable community

## 4. Shared Technical Focus Areas

Both projects are converging on several critical requirements, though with different implementation maturity:

| Focus Area | OpenClaw | Hermes Agent |
|------------|----------|--------------|
| **Reliable persistent connections** | Silent Slack disconnect (#72808), Mattermost 503 (#68113) | Slack DM thread breakage (#39527), Desktop app boot-loop (#39505) |
| **Model/provider compatibility** | OpenAI ChatGPT transport fails on gpt-5.4/5.5 (#90083) | OpenRouter key confusion (#39365), model routing presets (PR #39507 draft) |
| **Session state management** | SQLite migration for transcripts (#88838), cron state loss (#90072) | Child session disappearance (#39471), session resume rendering errors (#39469) |
| **Security & credential handling** | Sensitive data masking (#64046) — P1 security, no progress | Docker runs as root (#3969, fixed), aiohttp CVE patching (#39467) |
| **Platform-specific UX** | Feishu streaming truncation (#88929), Matrix thread regression (#87307) | CJK IME input loss (#39457), Desktop app start failures (#39503) |
| **Permission/access control** | Discord access list overhaul (#69748) | RBAC permission tiers (#527) — highest-voted feature |

**Key observation:** Connection reliability and session migration are the two most critical shared pain points, directly impacting production use cases.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary target user** | Production operators, multi-platform deployers, enterprise teams | Individual developers, desktop users, gateway-based multi-user setups |
| **Distribution model** | Self-hosted, container-optional, channel-adapter-centric | Desktop app + CLI + Docker sandbox, gateway-focused |
| **Maturity stage** | Post-MVP with migration pain — high feature surface but regressions | Early production — smaller surface, fewer regressions, faster iteration |
| **Integration depth** | Broad: Slack, Mattermost, Matrix, Feishu, Discord, QQBot | Focused: Slack, Docker sandbox, Desktop app, CLI |
| **Risk profile** | Higher regression risk due to runtime migration; more channels to break | Lower regression risk; desktop-specific bugs but narrower blast radius |
| **Security posture** | Reactive: sensitive data masking still unaddressed (#64046) | Proactive: aiohttp CVE patched, Docker root fixed, RBAC demanded |
| **UI/UX sophistication** | WebChat, Control UI, plugin contribution slots (#71736) | Desktop app (boot-loop issues), TUI (freeze on /reload-mcp) |

**Architecture contrast:** OpenClaw is a **platform infrastructure** project — designed to be the backbone for multiple chat clients. Hermes is a **user-facing agent** — designed to be installed and run directly by an individual or small team. This fundamental difference explains the divergence in bug profiles (channel-specific vs. app-specific) and feature priorities (channel adapters vs. RBAC/Docker).

## 6. Community Momentum & Maturity

**Activity Tiers:**

| Tier | Project | Characteristics |
|------|---------|-----------------|
| **High-Volume, High-Velocity** | OpenClaw | 500+ daily updates, 103 PRs merged/closed, but large unresolved backlog and regressions |
| **High-Responsiveness, Moderate Volume** | Hermes Agent | 50 daily updates, 6 PRs merged, quick issue closure, proactive fixes |

**Iteration Velocity:**
- **OpenClaw** is iterating rapidly but with **destabilizing velocity** — the high merge rate is producing regressions faster than they can be fixed, especially around the Codex-to-Pi migration.
- **Hermes Agent** is iterating at a **sustainable velocity** — frequent small fixes land quickly, and the backlog of open PRs (44 open vs. 6 merged) suggests manageable review throughput.

**Stabilization Signals:**
- OpenClaw: The high number of P1 bugs without fix PRs (6 new in 24h, 5+ older) signals a **stabilization bottleneck**. The next sprint should prioritize these over new features.
- Hermes: The closed P0 security issues (#3969, #9560-sec) and proactive CVE patching (#39467) show a **mature security culture**, though the multi-month RBAC feature (#527) remains unaddressed.

**Maturity Assessment:**
- **OpenClaw**: 🟡 **Scaling pain** — High adoption but struggling with migration-induced regressions. Needs a stabilization release.
- **Hermes Agent**: 🟢 **Healthy growth** — Responsive, secure, with clear feature roadmap. Needs to address the RBAC backlog.

## 7. Trend Signals for AI Agent Developers

1. **Reliability is the #1 barrier to production adoption.** Both projects' most-commented issues involve connection drops (Slack, Mattermost), state loss (cron jobs, sessions), and upgrade data loss. Developers should prioritize idempotent state management, connection health checks, and upgrade rollback support.

2. **Multi-user permission models are becoming essential.** Both communities are demanding RBAC/access tiers. This signals the market maturing beyond single-user assistants toward team deployments. Developers should plan permission systems early, even if not immediately needed.

3. **Model provider diversity creates integration fragility.** OpenClaw's OpenAI transport failures (#90083) and Hermes' OpenRouter confusion (#39365) highlight that provider-specific bugs are a growing source of support burden. Logging model version, provider, and transport metadata will aid debugging.

4. **Docker sandboxing is expected, not optional.** Hermes' Docker-related issues (root security, HOME bridging, container cleanup) show that users expect containerized execution but also secure defaults. OpenClaw doesn't emphasize Docker, but the ecosystem demand is clear.

5. **Desktop apps introduce new failure modes.** Both projects face platform-specific bugs (macOS IME, Windows installers, sleep/wake issues). For any project adding desktop clients, anticipate OS-specific QA costs.

6. **Real-time streaming remains fragile.** Feishu card truncation, SSE header issues, and reasoning content leaks all involve streaming logic. This is a high-complexity area requiring dedicated testing harnesses.

7. **Users are running budget-constrained models.** OpenClaw's "20-30% token waste on bootstrap files" (#67419) indicates users are tuning for cost efficiency, not just capability. Agent developers should expose and minimize overhead token usage.

8. **Security hardening is lagging behind feature development.** Both projects have open security issues (plaintext credentials, excessive Docker capabilities) that users are noticing. This is becoming a competitive differentiator—projects that address it proactively (like Hermes' aiohttp patch) gain trust.

---

**Bottom line for decision-makers:** OpenClaw is the ecosystem's dominant reference platform but is in a painful migration phase; deploy with caution and tested upgrade paths. Hermes Agent offers a more stable, desktop-first experience with better security hygiene, suitable for individual developers and small teams. Both projects validate that the AI agent space is moving from experimental tinkering toward production infrastructure—and the winners will be those who prioritize reliability, security, and multi-user permissions over raw feature count.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-05

## 1. Today’s Overview

The project is experiencing **extremely high activity**, with 50 issues and 50 pull requests updated in the last 24 hours. Of the 50 issues, 38 remain open and 12 were closed; on the PR side, 44 are open and 6 were merged or closed. Despite this volume, **no new release** was published today, leaving the latest official release (v0.15.1) unchanged. The community is actively reporting bugs, proposing features, and submitting fixes — especially around the Desktop app, CLI, gateway authentication, and Docker sandboxes. The large number of open items suggests a growing backlog, but the rapid response (many issues closed within hours) indicates a responsive maintainer team.

## 2. Releases

**No new releases today.** The current latest version remains `v0.15.1`.

## 3. Project Progress

- **6 PRs were merged or closed today.** One notable closed PR visible from the top 20 list is:
  - **[#39518] (fix(install): scrap rebuild venv)** — Fixes a broken venv rebuild step in the installer. [PR link](https://github.com/NousResearch/hermes-agent/pull/39518)
- **12 issues were closed**, including:
  - **[#4876] (Upgrade Node.js 20→22)** — Node 20 LTS EOL work-around completed. [issue link](https://github.com/NousResearch/hermes-agent/issues/4876)
  - **[#39275] (execute_code approval buttons not working)** — Root cause identified and fixed with missing `is_approved` check. [issue link](https://github.com/NousResearch/hermes-agent/issues/39275)
  - **[#39332] (Mac install failure)** — Installer bug resolved. [issue link](https://github.com/NousResearch/hermes-agent/issues/39332)
  - **[#24531] (bare `import grp` lacking platform guard)** — Test fix merged. [issue link](https://github.com/NousResearch/hermes-agent/issues/24531)
  - **[#36279] (Docs: browser console mangling)** — Doc improvement closed. [issue link](https://github.com/NousResearch/hermes-agent/issues/36279)
  - **[#7963] (docker.md missing local LLM guide)** — Doc gap filled. [issue link](https://github.com/NousResearch/hermes-agent/issues/7963)
  - **[#3969] (Docker runs as root with excessive capabilities)** — Security fix closed. [issue link](https://github.com/NousResearch/hermes-agent/issues/3969)
  - **[#39277] (xAI OAuth broken in Docker sandboxes)** — Credential resolution fixed. [issue link](https://github.com/NousResearch/hermes-agent/issues/39277)
  - **[#39367] (CLI 2nd Ctrl+C traceback)** — Cleanup behavior improved. [issue link](https://github.com/NousResearch/hermes-agent/issues/39367)
  - **[#39514] (Website theme low contrast)** — Chinese feedback addressed. [issue link](https://github.com/NousResearch/hermes-agent/issues/39514)

**New PRs opened today** (not yet merged) include:
- **[#39531] (feat(memory): allow disabling built-in memory tool)** — Config option for custom deployments. [PR link](https://github.com/NousResearch/hermes-agent/pull/39531)
- **[#39530] (fix(dashboard): self-heal broken uvicorn bootstrap installs)** — Fixes boot-loop caused by partial `uvicorn` install. [PR link](https://github.com/NousResearch/hermes-agent/pull/39530)
- **[#39528] (fix(skills): accept content fallback in skill_manage)** — Schema robustness. [PR link](https://github.com/NousResearch/hermes-agent/pull/39528)
- **[#39527] (fix(slack): slash commands broken in DM threads)** — Slack session key mismatch resolved. [PR link](https://github.com/NousResearch/hermes-agent/pull/39527)
- **[#39463] (Fix clarify prompt Enter submission)** — TUI interaction fix. [PR link](https://github.com/NousResearch/hermes-agent/pull/39463)
- **[#39467] (chore(deps): bump aiohttp to clear security advisories)** — Critical 9.1 vulnerability patched. [PR link](https://github.com/NousResearch/hermes-agent/pull/39467)

## 4. Community Hot Topics

The most commented issues in the last 24 hours reveal strong community interest in **access control** and **deployment flexibility**:

- **[#527] (Feature: Gateway Permission Tiers — RBAC)** — 10 comments, 2 👍. This feature proposal has been open since March and remains the most engaging issue. Users are asking for role-based access (Owner/Admin/User/Guest) on messenger platforms. The underlying need is multi-user gateway management without granting full command/tool access to everyone. [issue link](https://github.com/NousResearch/hermes-agent/issues/527)
- **[#39492] (Add config option to disable built-in memory tool)** — 3 comments. The user wants to keep external memory providers but hide the global `memory` tool in a multi-user gateway setup. A PR (#39531) was already opened today. [issue link](https://github.com/NousResearch/hermes-agent/issues/39492)
- **[#39365] (Misleading “OpenRouter API key missing” error)** — 3 comments. The real failure was a 401 invalid API_SERVER_KEY, but the Desktop app showed the wrong error message. This is a UX pain point emphasizing the need for clearer error propagation from gateway to client. [issue link](https://github.com/NousResearch/hermes-agent/issues/39365)
- **[#39332] (Mac install failure)** — 3 comments, 1 👍. Quickly closed after community engagement. [issue link](https://github.com/NousResearch/hermes-agent/issues/39332)
- **[#4876] (Upgrade Node.js 20→22)** — 4 comments, 1 👍. Closed after Docker image update. [issue link](https://github.com/NousResearch/hermes-agent/issues/4876)

**Other notable discussions:**
- **[#39505] (Desktop app boot-loop after bootstrap)** — 2 comments, details a crash caused by missing `uvicorn.supervisors` subpackage; a fix PR (#39530) is open. [issue link](https://github.com/NousResearch/hermes-agent/issues/39505)
- **[#39418] (/reload-mcp freezes CLI terminal)** — 1 comment. Session becomes unresponsive after manual `/reload-mcp`. No fix PR yet. [issue link](https://github.com/NousResearch/hermes-agent/issues/39418)

## 5. Bugs & Stability

Today saw a large influx of bug reports, many affecting the **Desktop app and CLI**. Issues are ranked by severity (P2 mostly; no P0 reported today):

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **P2** | [#39505](https://github.com/NousResearch/hermes-agent/issues/39505) | Desktop app boot-loop: `uvicorn` partial install after bootstrap | Yes [#39530](https://github.com/NousResearch/hermes-agent/pull/39530) |
| **P2** | [#39503](https://github.com/NousResearch/hermes-agent/issues/39503) | Desktop app fails to start: `unrecognized arguments: --tui` | No |
| **P2** | [#39418](https://github.com/NousResearch/hermes-agent/issues/39418) | CLI freezes after `/reload-mcp` | No |
| **P2** | [#39489](https://github.com/NousResearch/hermes-agent/issues/39489) | `/stop` command does not clean Docker sandbox containers | No |
| **P2** | [#39457](https://github.com/NousResearch/hermes-agent/issues/39457) | CJK IME input truncation on macOS: Chinese text after English dropped | No |
| **P2** | [#39469](https://github.com/NousResearch/hermes-agent/issues/39469) | Rich MarkupError on session resume (ANSI `_DIM` + `[/]` close tag) | No |
| **P2** | [#39471](https://github.com/NousResearch/hermes-agent/issues/39471) | Branch-like child sessions disappear from `sessions list` when `_branched_from` missing | No |
| **P2** | [#39365](https://github.com/NousResearch/hermes-agent/issues/39365) | Misleading error message on gateway auth failure | No |
| **P3** | [#39529](https://github.com/NousResearch/hermes-agent/issues/39529) | Windows installer fails on restricted networks (SSH/HTTPS both fail) | No |
| **P3** | [#39523](https://github.com/NousResearch/hermes-agent/issues/39523) | Sandbox HOME bridge broken for Keychain/SSH/Git/Python resources | No |
| **P3** | [#39497](https://github.com/NousResearch/hermes-agent/issues/39497) | Desktop app: personality config ignored, app hangs after sleep | No |

**Regression note:** The boot-loop issue (#39505) is a regression introduced by changes in v0.15.1’s bootstrap workflow. The self-heal PR (#39530) is under review.

## 6. Feature Requests & Roadmap Signals

Top user-requested features today, with predictions on next-version inclusion:

- **RBAC Permission Tiers** ([#527](https://github.com/NousResearch/hermes-agent/issues/527)) — High interest, long open. Likely being designed for v0.16.0.
- **Disable built-in memory tool** ([#39492](https://github.com/NousResearch/hermes-agent/issues/39492)) — PR already open (#39531); almost certain for next release.
- **Model routing presets** (PR [#39507](https://github.com/NousResearch/hermes-agent/pull/39507) – draft) — Lightweight model profiles for quick switching. In early draft; may land later.
- **System tray** (PR [#39468](https://github.com/NousResearch/hermes-agent/pull/39468)) — Minimize-to-tray for Windows/Linux. Likely to merge soon.
- **Zip fallback first-class for installer** ([#39529](https://github.com/NousResearch/hermes-agent/issues/39529)) — Network-restricted users want a direct download path.
- **Sandbox HOME bridge** ([#39523](https://github.com/NousResearch/hermes-agent/issues/39523)) — Subprocess tools need HOME-relative resources.
- **Feishu thread attachment fix** ([#39526](https://github.com/NousResearch/hermes-agent/issues/39526)) — Media attachments incorrectly sent to main conversation.
- **OpenClaw skill.md automatic generation** ([#39509](https://github.com/NousResearch/hermes-agent/issues/39509)) — Request for examples of what OpenClaw cannot do.

## 7. User Feedback Summary

**Real pain points expressed today:**

- **Desktop app unreliability:** Multiple users report crashes, boot-loops, freezes, and misleading errors on first launch or after sleep. The boot-loop (#39505) and startup failure (#39503) are particularly frustrating.
- **Gateway/authentication confusion:** A user spent time debugging an “OpenRouter key missing” error when the real cause was an invalid server key (#39365). Another found that `/reload-mcp` makes the CLI completely unresponsive (#39418).
- **Session management gaps:** Child sessions disappearing (#39471) and session resuming breaking rendering (#39469) indicate subtle state management bugs.
- **Chinese IME input loss** on macOS (#39457) — a usability barrier for CJK users.
- **Docker security and cleanup:** The `docker.md` docs now mention host-side LLM connection (#7963 closed), but users still want container cleanup on stop (#39489) and better sandbox HOME bridging (#39523).
- **Feature requests for production deployment:** RBAC (#527) and memory tool disabling (#39492) are clear signs that users are deploying Hermes in multi-user settings and need fine-grained control.

**Satisfaction indicators:**
- Many issues closed quickly (e.g., #39275, #39332, #3969) — maintainers are responsive.
- PRs like #39467 (aiohttp security patch) and #39530 (self-heal) show proactive maintenance.

## 8. Backlog Watch

The following important items have been open for an extended period without resolution or maintainer response:

- **[#527] Gateway Permission Tiers (RBAC)** — Created 2026-03-06, 10 comments, 2 👍. No PR or assignee. This is the single most upvoted feature request and has been dormant for 3 months. [issue link](https://github.com/NousResearch/hermes-agent/issues/527)
- **[#9560] Security: session management and skills guard** — PR opened 2026-04-14 (P0 severity, still open). High-risk vulnerability fix awaiting review. [PR link](https://github.com/NousResearch/hermes-agent/pull/9560)
- **[#22064] fix(api): avoid sweep task leak on startup refusal** — PR opened 2026-05-08 (P2). Prevents orphaned background tasks when API server fails to start. Still open after almost a month. [PR link](https://github.com/NousResearch/hermes-agent/pull/22064)
- **[#24229] fix(bluebubbles): drop participant-address fallback in _resolve_chat_guid** — PR opened 2026-05-12 (P1, privacy leak). Still open. [PR link](https://github.com/NousResearch/hermes-agent/pull/24229)
- **[#30196] fix(gateway): refuse --replace across HERMES_PROFILE mismatch** — PR opened 2026-05-22 (P2).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*