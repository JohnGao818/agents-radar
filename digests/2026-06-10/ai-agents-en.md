# OpenClaw Ecosystem Digest 2026-06-10

> Issues: 443 | PRs: 483 | Projects covered: 2 | Generated: 2026-06-10 02:58 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-10

## Today's Overview
OpenClaw shows exceptionally high activity with 443 issues and 483 pull requests updated in the last 24 hours. Of those, 130 PRs were merged or closed, and 2 new releases were published. The project remains in a rapid iteration phase, with major focus on channel delivery correctness (stripping thinking scaffolding, fixing message leaks), Codex compatibility, and memory system reliability. The community is heavily engaged, reporting regressions and contributing fixes across Windows, Linux, and mobile platforms.

---

## Releases
Two new releases were published today:
- **v2026.6.5** (stable)
- **v2026.6.5-beta.6** (beta)

### Highlights (both releases)
- **QQBot**: The model's reasoning/thinking scaffolding (e.g., `<thinking>` tags) is now stripped before native delivery, preventing raw internal thought from leaking into channel replies. (#89913, #90132) Thanks @openperf.
- **MCP tool results**: `resource_link`, `resource`, `audio`, malformed images, and future types are now coerced to safe formats.

No breaking changes or migration notes are listed, suggesting these are incremental improvements.

---

## Project Progress
Several features and fixes advanced through merged/closed PRs today:

- **iOS/iPadOS Control Surfaces** (#91557, merged) – iPad now has a sidebar/navigation model, dedicated iPad destinations, and responsive phone control hub. Connected surfaces for Workboard, Skill Workshop, and settings.
- **Codex Context-Engine Compaction** (#91590, merged) – Keeps owning context-engine compaction primary for queued budget compaction when Codex/native harness is also selected. Stops stale Codex thread-bootstrap runs.
- **Cron Disabled Wake Fallback** (#91811, merged) – One-shot cron jobs now queue a heartbeat request instead of marking the run as skipped when the heartbeat is disabled.
- **iMessage Inbound Startup Diagnostics** (#91785, merged) – Privacy-safe logs when inbound rows are dropped for echo/reflection reasons.
- **iMessage Outbound Send Transport** (#91783, merged) – Adds `channels.imessage.sendTransport` with per-account overrides (`auto`, `bridge`, or `applescript`). Stops monitor final replies from reusing the long-lived watch RPC client.
- **Bug Fix: OpenAI ChatGPT Responses Transport** (#90083, closed) – Fixed `invalid_provider_content_type` error for `gpt-5.4`/`gpt-5.5`.

---

## Community Hot Topics
The most active issues and PRs by comment count reveal deep user pain points:

1. **#[25592](https://github.com/openclaw/openclaw/issues/25592) — Text Between Tool Calls Leaks to Channels** (29 comments, open)
   - **Summary**: Internal processing text (error handling, acknowledgments) is routed to messaging channels as visible messages.
   - **Need**: Message privacy and UX – users don't want to see internal scaffolding. This is the #1 most-discussed issue, labeled `impact:security` and `impact:message-loss`.

2. **#[90083](https://github.com/openclaw/openclaw/issues/90083) — ChatGPT Responses Transport Fails with `invalid_provider_content_type`** (16 comments, closed)
   - **Need**: Compatibility with the newest GPT-5.x models. Fixed in today's release.

3. **#[32296](https://github.com/openclaw/openclaw/issues/32296) — Agent Replies to Previous Message (Session Context Confusion)** (15 comments, open)
   - **Need**: Correct conversational flow – responses must match the current user message, not the previous one.

4. **#[88312](https://github.com/openclaw/openclaw/issues/88312) — Codex Turn-Completion Stall Regression** (15 comments, open)
   - **Need**: Reliability of Codex-backed runs; multi-tool agent turns stall after 2026.5.27.

5. **#[87307](https://github.com/openclaw/openclaw/issues/87307) — Matrix Thread Replies Sent as Normal Replies** (14 comments, open)
   - **Need**: Platform-specific delivery semantics – Matrix threads must preserve threading.

Other hot topics include RISC-V compatibility (#54253), Docker sandbox workspace mounting (#31331), and Discord internal tool-call leaks (#44905).

---

## Bugs & Stability
Numerous regressions and stability issues were reported or updated today. Ranked by severity:

### Critical / High Impact
- **Session Context Confusion** (#32296) – Agent replies to wrong message. Fix PR not yet available.
- **Text Leaks Between Tool Calls** (#25592) – Internal text goes to channels. No fix PR yet; security concern.
- **Codex Turn-Completion Stall** (#88312) – Regression from 2026.5.27 preventing multi-tool turns from completing. Open.
- **Matrix Thread Regression** (#87307) – Replies sent as normal messages; `/status` and `/model` commands silent. Open.
- **Windows Local Model Blocks Gateway Event Loop** (#86599, closed) – Fixed: trivial infer runs took ~4 minutes.
- **Embedded Session Takeover Error** (#86508) – `EmbeddedAttemptSessionTakeoverError` during Discord runs after status text disappears. Open.
- **Heartbeat PendingFinalDelivery Stuck** (#83184) – Blocks subsequent heartbeats. Open.
- **WhatsApp Session Stalls on Long Model Calls** (#84569) – Incomplete turns, reply never delivered. Open.
- **Gateway Heap Grows Unbounded (OOM)** (#89315) – Killed by cgroup OOM on long-running Linux deployments. Open.
- **Telegram Infinite Retry Loop** (#56096) – `sendChatAction` retries every ~3s with no backoff, making bot unresponsive. Open.
- **Agent Tool Failure Infinite Loop** (#55694) – Chinese report of repeated message spam after tool failure.

### Medium Impact
- **Steer Mode Not Injecting Mid-Turn** (#48003) – User messages queued until turn completes instead of at tool boundaries. Open.
- **Discord Leaks Internal Tool-Call Traces** (#44905) – `NO_REPLY`, raw JSON, commentary exposed. Open.
- **Active Memory + Codex Latency** (#86996) – Long response times, hook timeouts, startup aborts. Open.
- **Docker Sandbox Workspace Access** (#31331) – `/workspace` bind mount issues in Docker-outside-of-Docker setups. Open.
- **Browser Control Server Hang** (#53399) – `npx chrome-devtools-mcp` spawn stuck inside Gateway process. Open.
- **Memory Search Abort** (#74586) – AM embedded run aborts `memory_search` calls, classifies as timeout despite model completion. Open.
- **Backup Tmp Files Left on Timeout** (#50442) – Large `.tmp` files cause disk space exhaustion. Open.

### Low Impact (P2/P3)
- Feishu card JSON rendered as plain text (#53486); config drop on HOME change (#54634); sessions_history duplicates (#85669, closed); TTS ElevenLabs ignored (#52186); Live docs ahead of release (#48920); whitespace in config directory (#44599, closed); etc.

---

## Feature Requests & Roadmap Signals
Community requests point toward better configurability and user-facing feedback:

- **Per-channel / per-group model overrides** (#53638) – 5 comments, 2 👍. Likely to be addressed as it aligns with existing multi-channel architecture.
- **Persistent task-status surface for long runs** (#52640) – 7 comments

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem

*Generated from community digests of OpenClaw and Hermes Agent (2026-06-10)*

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is in a phase of rapid, high-velocity iteration driven by large, engaged communities. Two dominant reference implementations—**OpenClaw** (the core reference agent) and **Hermes Agent** (by Nous Research)—are both hyperactive, but with markedly different development cadences and community dynamics. The ecosystem is heavily focused on channel delivery correctness, model provider compatibility, memory system reliability, and user-facing privacy (preventing internal scaffolding from leaking to end-users). Both projects receive hundreds of daily contributions, yet also accumulate hundreds of open bugs, indicating that stability is still secondary to feature expansion and platform coverage.

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | PRs Merged/Closed (24h) | Releases Today | Health Score* |
|---|---|---|---|---|---|
| **OpenClaw** | 443 | 483 | 130 | 2 (stable + beta) | 7/10 |
| **Hermes Agent** | 50 | 50 | 3 | 0 | 5/10 |

*Health Score (1–10, subjective): based on release cadence, issue resolution rate, merge velocity, and community responsiveness. OpenClaw’s high merge throughput and rapid releases offset its large bug backlog. Hermes Agent’s slower merge velocity and no releases today lower its score despite active discussion.

## 3. OpenClaw’s Position

OpenClaw is the primary reference implementation and community ground truth. Its advantages include:

- **Community size & velocity**: >8× the daily issue/PR volume of Hermes Agent, indicating a much larger contributor base and user footprint.
- **Technical approach**: Architectural focus on channel delivery correctness (stripping thinking tags, avoiding message leaks) and memory system compaction. OpenClaw’s codebase shows heavy investment in platform-specific transport layers (iMessage, Matrix, QQ Bot, WhatsApp, Telegram, Discord).
- **Stability trade-offs**: Rapid iteration leads to frequent regressions (e.g., Codex turn-completion stall, Matrix thread breakage, gateway OOM). However, the project consistently ships multiple releases per week, including beta channels for risk-tolerant adopters.

Compared to Hermes Agent, OpenClaw feels more like an infrastructure project—its users are developers integrating agents into diverse channels—while Hermes focuses more on end-user experience (dashboard, desktop, bundled skills).

## 4. Shared Technical Focus Areas

Both projects are converging on several critical requirements:

| Requirement | OpenClaw | Hermes Agent |
|---|---|---|
| **Message privacy** – prevent internal scaffolding from leaking to channels | #25592, #44905, #90083 (fixed) | #43121 (cron session invisibility), #7507 (Matrix quoting) |
| **Model provider compatibility** – support latest GPT, Gemini, and regional providers | Fixed `invalid_provider_content_type` for GPT-5.x | Vision support gap for Gemini 2.x, Volcengine request |
| **Platform diversity** – Matrix, Telegram, Discord, iMessage, WeChat, etc. | iMessage send transport, Matrix thread fix, WhatsApp stalls | WeChat Silk voice, Matrix PLATFORM_HINTS, Telegram command menu |
| **Cron/job scheduling reliability** – background tasks not stalling | Cron disabled wake fallback (#91811) | Cron sessions invisible in Desktop (#43121), cron security fix (#43223) |
| **Memory and context management** – avoid stalls, OOM, timeout | Codex turn-completion stall (#88312), memory search abort (#74586) | Stale-stream retry without fallback (#43211), token counters restore (#43050) |

Both projects are also receiving strong community demand for **per-channel/per-group model overrides** (OpenClaw #53638) and **per-tool enable/disable** (Hermes Agent #31375)—pointing to a need for more granular configuration at the integration level.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|---|---|---|
| **Primary target user** | Developers building multi-channel agent deployments | End-users and power users running a personal AI desktop/dashboard |
| **Feature emphasis** | Channel transport correctness, memory compaction, Codex compatibility | Bundled skills, provider expansion, Kanban workflow, desktop UX |
| **Release philosophy** | Rapid, incremental (2 releases/day, including betas) | Slower, feature-gated (last release days ago, no new release today) |
| **Bundled skills / plugins** | Not highlighted; community focuses on core transport | Heavy investment: 15 new bundled skills in progress (Linear, Spotify, 1Password, etc.) |
| **Platform support** | Windows, Linux, macOS, iOS/iPadOS (control surfaces) | Linux (Termux fix), macOS (desktop crash reported), Docker (OIDC issue) |
| **Community engagement** | Very high; multiple open issues with 15–29 comments | Moderate; top issues have 3–4 comments, lower discussion depth |

## 6. Community Momentum & Maturity

**OpenClaw** is in **hyper-iteration mode** – 130 PRs merged in a single day, two releases cut, and a massive issue tracker that is actively triaged but not keeping pace with incoming bugs. The community is highly engaged, but the constant regressions suggest that maturity is still months away. It is the riskier but more feature-rich choice for early adopters.

**Hermes Agent** is **stable-ish but slower** – only 3 PRs merged today, no release. The community is actively filing bugs and feature requests, but maintainer responsiveness appears delayed for older items (e.g., #13107, #7507). The project is growing its skill ecosystem, which may accelerate adoption once stability improves.

Both projects share a common pattern: **high community enthusiasm outpacing maintainer capacity**, leading to growing backlogs and occasional community frustration.

## 7. Trend Signals

Several industry trends emerge from the community feedback:

- **Privacy-by-design is non-negotiable**: Users won’t tolerate internal agent reasoning (thinking tags, tool-call traces) leaking to public channels. This is the #1 pain point across both ecosystems.
- **Multi-platform is table stakes**: Support for iMessage, Matrix, WeChat, QQ, Discord, Telegram, and WhatsApp is no longer optional—it’s expected. Platform-specific quirks (threading, voice messages, command menus) are top issues.
- **Model provider fragmentation is accelerating**: Developers need support for GPT-5.x, Gemini 2.x, Volcengine, and local providers. A single-provider dependency is increasingly seen as a limitation.
- **Agent workflow maturity is demanded**: Kanban review transitions, cron job visibility, and persistent task status surfaces show that users want agents to manage long-running, structured work, not just Q&A.
- **Desktop + mobile convergence**: OpenClaw’s iPad control surfaces and Hermes’ desktop app crashes both signal that the ecosystem is moving beyond terminal/CLI to native GUI experiences.
- **Bundled skills as competitive advantage**: Hermes’ aggressive addition of 15+ skills suggests that out-of-the-box utility is becoming a differentiator. OpenClaw may need to follow suit to retain developer mindshare.

**For AI agent developers, the key takeaway** is that even the most advanced reference implementations are still wrestling with fundamental reliability (stalls, OOM, message leaks). Investing in channel-specific transport hardening and privacy-safe scaffolding management will yield immediate value, while waiting for the ecosystem to stabilise before adopting bleeding-edge features.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-06-10

## 1. Today's Overview

Project activity remains very high, with **50 issues** and **50 pull requests** updated in the last 24 hours. The majority of issues are open (48), reflecting an active community reporting bugs and proposing features – only 2 issues were closed. Similarly, PRs are predominantly open (47), with only 3 merged or closed today. A single security patch was merged during the day. No new releases were cut. The project is in a heavy feature‑request and bug‑fixing phase, with significant contributions around platform support, tooling, and bundled skills.

## 2. Releases

**No new releases today.** The latest published version remains the previously released Hermes Agent (dashboard 0.16.0 and desktop 0.15.1 are mentioned in issues). No migration notes or changelogs are available for today.

## 3. Project Progress

Three PRs were closed/merged today:

- **PR #43223** `[CLOSED, P1, security]` – Fixes cron strict‑scanning of script‑injected output in no‑skills jobs, preventing false positive alerts on innocuous data.  
  [View PR](https://github.com/NousResearch/hermes-agent/pull/43223)

No other merges were observed in the top 20 PR snapshot, suggesting the bulk of progress is still in review or pending.

Noteworthy open PRs that advanced today include:
- **#40377** (Termux/PRoot support via `UV_LINK_MODE=copy`)
- **#43046** (re‑validate PGID ownership before killing orphaned MCP process groups)
- **#43050** (restore token counters on session.resume for Desktop)
- **#43051** (honor glob command allowlist entries)
- **#43091** (avoid consuming skipped manual cron triggers)
- **#43164** (prefer managed Chromium over Snap wrapper)
- **#43167** (force‑include pinned sessions in sidebar)
- **#43249** (improve Matrix PLATFORM_HINTS)

These span fixes for Linux compatibility, MCP lifecycle, gateway UI, command approval, cron scheduling, browser tooling, and messaging platform hinting.

## 4. Community Hot Topics

The most discussed issues (by comment count) reveal a strong interest in **platform integration** and **configuration flexibility**:

1. **#13107** – *Feature request: support command description override via config.yaml* (4 comments)  
   Users want per‑locale command descriptions for Telegram/Discord bots.  
   [Issue](https://github.com/NousResearch/hermes-agent/issues/13107)

2. **#29331** – *feat: add Volcengine (火山引擎) as built-in provider* (3 comments, 1 👍)  
   A ByteDance provider is requested with an existing integration guide.  
   [Issue](https://github.com/NousResearch/hermes-agent/issues/29331)

3. **#42086** – *fix(vision): support gemini-2.5 and gemini-2.0 in _supports_media_in_tool_results* (3 comments)  
   Gemini 2.x model families lack vision support detection, causing silent failures.  
   [Issue](https://github.com/NousResearch/hermes-agent/issues/42086)

4. **#43042** – *Desktop file browser ENOENT: session.info CWD overwrite ignores local filesystem* (3 comments)  
   A regression in remote gateway mode where the sidebar flashes correct data then resets to “UNREADABLE”.  
   [Issue](https://github.com/NousResearch/hermes-agent/issues/43042)

5. **#42896** – *Kanban review status exists but has no first-class request-review transition* (3 comments)  
   Workers cannot formally move tasks into review, breaking the Kanban workflow.  
   [Issue](https://github.com/NousResearch/hermes-agent/issues/42896)

The underlying needs are clear: better multi‑platform i18n support, expanded provider networks (Volcengine, Gemini 2.x), and more mature Kanban lifecycle management.

## 5. Bugs & Stability

Several impactful bugs were reported today, many with corresponding fix PRs already in flight.

**High severity (P1–P2):**
- **#43211** (P2) – Stale stream errors silently retry on the same provider instead of triggering runtime fallback.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/43211) – No fix PR yet.
- **#43121** (labeled P3, but described as “Critical”) – Cron sessions in Desktop render only the user prompt; tool calls and LLM responses are invisible until gateway restart.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/43121) – No fix PR yet.
- **#43242** (P3) – Desktop app crash on macOS 26.5.1: Fatal process out of memory (V8 CodeRange) on startup.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/43242) – No fix PR.

**Medium severity (P2–P3) with active fix PRs:**
- **#43042** – Remote gateway file browser ENOENT → fix PR #43050 (token counters) partially addresses the UI display, but root cause may require more.
- **#42084** – WeChat Silk voice messages not converted to WAV for STT.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/42084) – PRs unclear, but a known gap.
- **#42780** – `HERMES_DASHBOARD_PUBLIC_URL` not respected for OIDC callback in Docker.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/42780) – No fix PR yet.
- **#41744** – `auxiliary.title.enabled: false` config is ignored; title generation always runs.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/41744) – No fix PR.
- **#42962** – Desktop session does not refresh after update from Telegram gateway.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/42962) – PR #43050 likely related.
- **#43245** – Models ignore PTY terminal tool when needing sudo, trying alternative unsafe methods.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/43245) – No fix PR.
- **#43122** – Messaging provider icons (Matrix, Slack) not dark‑UI friendly.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/43122) – No fix PR.
- **#43196** – Dashboard wedges (SIGKILL required) in persistent service mode due to two PTY/Chat tab bugs.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/43196) – No fix PR.

The **#43223** security fix for cron was merged today, addressing a vulnerability in script‑injected output scanning.

## 6. Feature Requests & Roadmap Signals

The most significant feature requests indicate the community is pushing for:

- **Provider expansion** – Volcengine (#29331), local provider overlay alias (#43052), You.com web backend (PR #13314).
- **Config granularity** – Per‑tool enable/disable (#31375), command description override (#13107), configurable Telegram command menu (PR #43162).
- **Workflow improvements** – First‑class Kanban review transition (#42896), inline “Reply & unblock” for blocked tasks (#43216), context selection as a separate engine concern (#36765).
- **Plugin/hook expansion** – `transform_api_request` full‑payload hook (PR #43241), shell‑hook parent_session_id (#42939), ephemeral API‑message transformation (#20307).
- **Bundled skills** – Three PRs (#43166, #43169, #43172) collectively add **15 new bundled skills** (Linear, Spotify, 1Password, GitHub PR tools, Hindsight Memory, Paperclip AI, bioinformatics, etc.), signaling a push toward a richer out‑of‑the‑box experience.

**Prediction for next release:** Given the volume and maintainer engagement (many PRs are reviewed), we may see these features land soon: Volcengine provider, per‑tool enable/disable, and the new bundled skills. The Kanban review transition and Matrix reply quoting are also strong candidates.

## 7. User Feedback Summary

**Pain points expressed:**
- **i18n/locale** – Hardcoded English command descriptions alienate non‑English users (#13107).
- **Platform gaps** – WeChat voice messages unsupported (#42084), Matrix reply quoting clunky (#7507), Telegram command menu not configurable (PR #43162).
- **UI/UX regressions** – Desktop token stats show 0% (#42989, #43050), multi‑line user messages clipped (#42992), session refresh broken (#42962), dark‑theme icon invisibility (#43122).
- **Stability** – Desktop crash on macOS (#43242), dashboard wedges when run as service (#43196), stale‑stream silent retry without fallback (#43211).
- **Configuration surprises** – `auxiliary.title.enabled` ignored (#41744), `protocol_violation` hardcoded failure_limit=1 too aggressive (#42924), `execute_code` still prompts in YOLO mode (#42921).
- **Remote/gateway issues** – File browser ENOENT (#43042), OIDC callback URL ignored (#42780), cron sessions invisible in Desktop (#43121).

**Satisfaction signals:**
- Likely positive reaction to the merged Termux fix (PR #40377) and the cron security fix (#43223).
- The large number of bundled skill PRs suggests users desire more ready‑made capabilities – a sign of a maturing ecosystem.

## 8. Backlog Watch

The following issues and PRs have remained open for an extended period without significant maintainer response, risking community frustration:

- **#13107** (2026-04-20) – Command description override – 4 comments, no maintainer reply.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/13107)
- **#7507** (2026-04-11) – Matrix reply quoting – 2 comments, 1 👍, no maintainer reply.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/7507)
- **#20307** (2026-05-05) – Plugin hook for ephemeral API‑message transformation – 1 comment, no maintainer reply.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/20307)
- **#31375** (2026-05-24) – Per‑tool enable/disable – 2 comments, 1 👍, no maintainer reply.  
  [Issue](https://github.com/NousResearch/hermes-agent/issues/31375)
- **PR #13314** (2026-04-21) – You.com web backend – no comments from maintainers, still open.  
  [PR](https://github.com/NousResearch/hermes-agent/pull/13314)

These items represent valuable contributions that could stall without maintainer guidance or triage. Prioritising them would improve community trust and reduce duplicated effort.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*