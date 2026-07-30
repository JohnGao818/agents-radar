# OpenClaw Ecosystem Digest 2026-07-30

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-30 01:59 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-30

## 1. Today’s Overview
The OpenClaw project remains extremely active, with **500 issues and 500 pull requests updated in the last 24 hours**. Of these, 448 issues are open/active and 52 were closed; 402 PRs are open and 98 were merged or closed. No new releases were published. Activity is dominated by high‑severity bugs (P1 often tagged `diamond lobster` or `platinum hermit`) around Codex integration, OAuth authentication, memory/cache performance, subagent message delivery, and cron reliability. Many issues carry `clawsweeper:needs-maintainer-review` or `clawsweeper:needs-product-decision` labels, indicating a significant backlog of decisions and reviews. The project is clearly under heavy community usage, but stability and maintenance responsiveness remain pressing concerns.

## 2. Releases
No new releases were published for the period covered. The latest available version remains **2026.7.1** (as seen in issue #109017). Users are encouraged to check the [OpenClaw releases page](https://github.com/openclaw/openclaw/releases) for future updates.

## 3. Project Progress
Despite the absence of a new release, **98 pull requests were merged or closed today**. Notable closed PRs (from the top‑30 list) include:

- **#116151** (closed) – `fix(agents): throw CompactionError when summarization fails entirely` – improves compaction reliability.
- **#116167** (closed) – `fix: serialize hosted Swift release tests` – resolves test contention.
- **#116162** (closed) – `fix(daemon): prevent duplicate systemd gateway ownership` – addresses upgrade‑related service conflicts.

Several high‑impact closed issues also reflect progress:
- **#95515** (closed, P0) – *Upgrade 2026.6.8→2026.6.9 corrupts email channel config* – was a release‑blocker, now resolved.
- **#87665** (closed) – *Discord‑originated subagent tasks default to done_only, leaving channel stuck on typing indicator*.
- **#92374** (closed) – *Plugin `message_sending` hooks silently bypassed on channel agent‑reply delivery paths*.
- **#79375** (closed) – *Upgrade leaves stale user‑level systemd unit, dueling services kill each other*.
- **#69943** (closed) – *Session‑memory hook persists raw chat‑template tokens causing self‑reinforcing poisoning loop*.
- **#43454** (closed) – *Feature Request: Gateway lifecycle hooks* – has been implemented and closed.

These fixes show the team is actively addressing critical regressions and long‑standing feature requests.

## 4. Community Hot Topics

### Most Active Issues (by comment count)
| Issue | Comments | Summary |
|-------|----------|---------|
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | 18 | Codex PreToolUse native hook relay spawns CPU‑bound `openclaw-hooks` processes, stalls gateway RPC. **(P1, diamond lobster)** |
| [#86996](https://github.com/openclaw/openclaw/issues/86996) | 15 | Active Memory + Codex app‑server path causes long response latency, hook timeouts, startup aborts. **(P1, diamond lobster)** |
| [#39476](https://github.com/openclaw/openclaw/issues/39476) | 13 | A2A sessions_send causes duplicate messages when target agent calls back. **(P1, platinum hermit, stale)** |
| [#90354](https://github.com/openclaw/openclaw/issues/90354) | 11 | Feature request: bounded/validated append semantics for pre‑compaction memory flush. **(P2, diamond lobster)** |
| [#91363](https://github.com/openclaw/openclaw/issues/91363) | 10 | Isolated cron jobs consistently fail with “LLM request failed” / timeouts. **(P1, platinum hermit, 6👍)** |

### Top Reacted Issues
- **#91363** (6👍) – cron failures – strong user demand for a fix.
- **#90361** (3👍) – *memory_search “index metadata is missing”* – a regression with community traction.
- **#81061** (3👍) – *pre‑routing interception hook* – feature request for inbound message routing.

### Underlying Needs
The community is most vocal about:
- **Codex integration stability** (#91009, #86996) – CPU spikes, OAuth refresh failures, mid‑turn aborts.
- **Cron/automation reliability** (#91363, #89095) – isolated runs timeout without notification.
- **Memory search performance** (#90361, #92633, #112196) – timeouts, missing indexes, sync errors.
- **Subagent message delivery** (#39476, #90944, #92433) – duplicate or dropped completions.

These topics indicate users rely heavily on multi‑agent workflows, scheduled automation, and long‑term memory, and are hitting real production pain points.

## 5. Bugs & Stability

Today’s most severe bug reports (P1, often with `impact:message-loss` or `impact:crash-loop`):

| Issue | Title | Severity | Fix PR exists? |
|-------|-------|----------|----------------|
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex PreToolUse native hook relay CPU‑bound, stalls gateway | P1, diamond lobster | No PR linked |
| [#86996](https://github.com/openclaw/openclaw/issues/86996) | Active Memory + Codex latency, hook timeouts, event‑loop stalls | P1, diamond lobster | No PR linked |
| [#91363](https://github.com/openclaw/openclaw/issues/91363) | Isolated cron fails – “LLM request failed” | P1, platinum hermit | No PR linked |
| [#86215](https://github.com/openclaw/openclaw/issues/86215) | Codex OAuth refresh wedge – hours without alerting | P1, platinum hermit | No PR linked |
| [#89278](https://github.com/openclaw/openclaw/issues/89278) | Codex OAuth refresh succeeds but cron/heartbeat fail with 10s timeout | P1, platinum hermit | No PR linked |
| [#112423](https://github.com/openclaw/openclaw/issues/112423) | SQLite transcript cleanup blocks gateway event loop | P1, silver shellfish | No PR linked |
| [#91456](https://github.com/openclaw/openclaw/issues/91456) | Telegram DM lane guarded after send timeout | P1, diamond lobster | No PR linked |
| [#87756](https://github.com/openclaw/openclaw/issues/87756) | Lobster workflow hangs on nested /tools/invoke when prompt‑launched | P1, platinum hermit | No PR linked |
| [#92433](https://github.com/openclaw/openclaw/issues/92433) | Subagent completion silently dropped | P1, platinum hermit | No PR linked |
| [#89315](https://github.com/openclaw/openclaw/issues/89315) | Gateway heap grows unbounded, killed by cgroup OOM | P1, silver shellfish | No PR linked |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | Leaks unreaped hook/tool child processes – zombie accumulation | P1, diamond lobster | No PR linked |
| [#115908](https://github.com/openclaw/openclaw/issues/115908) | Transcript projection livelock under sustained writes, stalls thread | P1, silver shellfish | No PR linked |

Many of these issues lack linked fix PRs, indicating they are still in investigation or require product decisions. Some have companion PRs (e.g., #116166 addresses request timeouts but not specific issues yet). The P0 regression (#95515) was closed, signaling a successful hotfix.

## 6. Feature Requests & Roadmap Signals

The most requested features visible in today’s data:

| Issue | Title | Potential for Next Version |
|-------|-------|----------------------------|
| [#90354](https://github.com/openclaw/openclaw/issues/90354) | Bounded/validated append semantics for pre‑compaction memory flush | **High** – directly improves compaction safety, multiple PRs nearby |
| [#81061](https://github.com/openclaw/openclaw/issues/81061) | Pre‑routing inbound message interception hook | **Medium** – addressed in closed #43454 but re‑requested; could be merged |
| [#88154](https://github.com/openclaw/openclaw/issues/88154) | Slack Modal Support for Interactive Workflows | **Medium** – aligns with UI improvements in PR #114853 |
| [#8299](https://github.com/openclaw/openclaw/issues/8299) | Config option to suppress sub‑agent announce | **Medium** – common request, simple config change |
| [#13219](https://github.com/openclaw/openclaw/issues/13219) | Per‑model usage logging for cost tracking | **High** – requested since February, high user value |
| [#85461](https://github.com/openclaw/openclaw/issues/85461) | Capture image‑generation provider usage metadata | **Low** – nice‑to‑have, no linked PR |
| [#91259](https://github.com/openclaw/openclaw/issues/91259) | Drop redundant agent‑id scoping from memory collection names | **Medium** – cleanup, linked PR open |

The bounded append semantics (#90354) and per‑model logging (#13219) are most likely to appear in a near‑term release given community demand and available implementation patterns. The feature for suppressing sub‑agent announce (#8299) is also frequently mentioned and would be simple to implement.

## 7. User Feedback Summary

### Common Pain Points
- **Performance degredation** – users report CPU spikes from Codex hooks (#91009), unbounded heap growth (#89315), and event‑loop stalls (#112423, #115908).
- **Authentication headaches** – Codex OAuth refresh failures (#86215, #89278) and provider model catalog staleness (#109017) cause service interruptions.
- **Cron and automation unreliability** – isolated jobs fail silently (#91363), subagent run timeouts do not notify parent (#89095), and “failed” notifications fire during hot reloads (#90595).
- **Message loss and delivery issues** – duplicate messages via A2A (#39476), dropped subagent completions (#92433), and Telegram lane guards (#91456).
- **Channel‑specific problems** – Feishu missing text sanitization (#90684), Discord typing indicator stuck (#87665 closed), Mattermost edits not waking agents (#97316 PR), and Windows CLI regressions (#91144, #105528).
- **Upgrade friction** – stale systemd units (#79375 closed), email config corruption (#95515 closed), and missing stderr in launchd (#90711).

### Satisfaction Signals
- Issues that have been closed steadily (52 in 24h) indicate that maintainers are responsive.
- Several high‑profile bugs (email corruption, systemd conflicts, Discord typing indicator) have been resolved.
- Community engagement is high, with 6👍 on #91363 and 3👍 on #90361, showing users actively advocate for fixes.

### Dissatisfaction Signals
- Many P1 items remain open for weeks (some since May–June) with no fix PR linked, suggesting bandwidth constraints.
- The `clawsweeper:needs-product-decision` label appears on ~40% of top issues, implying organizational delays.
- Users report that after upgrades, previously working features break (e.g., DeepSeek V4 Flash #88657), eroding trust.

## 8. Backlog Watch

The following long‑standing Items require maintainer attention:

### Issues
| Issue | Age | Priority | Reason for Watch |
|-------|-----|----------|------------------|
| [#39476](https://github.com/openclaw/openclaw/issues/39476) | Since 2026-03-08 | P1, platinum hermit | Stale A2A duplicate messages – impacts multi‑agent workflows, no PR. |
| [#8299](https://github.com/openclaw/openclaw/issues/8299) | Since 2026-02-03 | P2, off‑meta tidepool | Feature request to suppress sub‑agent announce – simple, high demand, stale. |
| [#13219](https://github.com/openclaw/openclaw/issues/13219) | Since 2026-02-10 | P2, off‑meta tidepool | Per‑model usage logging – popular, linked PR exists but stalled. |
| [#52526](https://github.com/openclaw/openclaw/issues/52526) | Since 2026-03-22 | P2, diamond lobster | `agent --json` returns pre‑hook text – affects plugin developers. |
| [#69086](https://github.com/openclaw/openclaw/issues/69086) | Since 2026-04-19 | P2, diamond lobster | session‑history guard too broad in attempt‑execution – blocks retries. |
| [#81061](https://github.com/openclaw/openclaw/issues/81061) | Since 2026-05-12 | P2, diamond lobster | Pre‑routing inbound message hook – linked PR open but needs product decision. |

### Pull Requests
| PR | Age | Status | Reason for Watch |
|----|

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent Open-Source Ecosystem

**Date:** 2026-07-30  
**Scope:** OpenClaw (core reference, GitHub) and Hermes Agent (Nous Research, GitHub)  
**Audience:** Technical decision-makers and developers

## 1. Ecosystem Overview

The personal AI agent open-source landscape is maturing rapidly, driven by community demand for autonomous task execution, multi-agent coordination, and long-term memory. Two major reference implementations—OpenClaw and Hermes Agent—illustrate different architectural philosophies: OpenClaw as a monolithic, plugin-heavy core with deep Codex integration; Hermes Agent as a modular, desktop-first platform with a strong emphasis on test hermeticity and platform portability. Both projects face similar scaling challenges around memory management, OAuth reliability, and message delivery, but their development velocities and community engagement patterns diverge significantly—OpenClaw shows extremely high issue/PR volume but a heavy backlog of unresolved P1s, while Hermes Agent demonstrates tighter CI discipline and faster issue closure rates.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|---|---|---|
| Issues updated (last 24h) | 500 total (448 open, 52 closed) | 50 total (32 open, 18 closed) |
| PRs updated (last 24h) | 500 total (402 open, 98 merged/closed) | 50 total (35 open, 15 merged/closed) |
| New releases (last 24h) | None (latest: 2026.7.1) | None (latest: v0.19.0, 2026-07-20) |
| P1 open bugs | ~11+ (Codex, OAuth, cron, memory) | 2 (distribution_owned, possibly 1 closed) |
| “Needs product decision” labels | ~40% of top issues | ~30% of open issues |
| Test suite pass rate | Not reported | 22,588 passing (fully hermetic) |
| **Health score** (qualitative) | **Medium:** High activity but severe stability concerns; decision backlog | **High:** Balanced throughput, rigorous testing, fast closure |

**Key observations:**  
- OpenClaw’s issue/PR volume is 10× higher than Hermes Agent, but its closure rate is proportionally lower (52 vs 18 issues closed; 98 vs 15 PRs).  
- Hermes Agent’s CI pipeline is more mature, with a single batch fixing 12 external PRs and achieving full hermetic test isolation.  
- Both projects lack recent releases, indicating either a stabilization phase or internal bottlenecks.

## 3. OpenClaw’s Position

**Advantages over peers:**  
- Largest community footprint: 500 daily interactions signal broad deployment and active bug reporting.  
- Deep Codex integration for model-agnostic multi-agent workflows; many features (pre-tool-use hooks, subagent routing) are unique.  
- Rich plugin ecosystem with channel connectors (Discord, Telegram, Slack, Feishu, Mattermost).  
- Advanced memory compaction and session history features (bounded append semantics, compaction error handling).

**Technical approach differences:**  
- OpenClaw employs a **gateway-centric architecture** with subagent dispatch via A2A protocol, while Hermes Agent uses a **desktop-first profile system** with Kanban boards and delegated profiles.  
- OpenClaw’s memory model relies on active memory + Codex app-server path, leading to CPU-bound hook processes and event-loop stalls. Hermes Agent uses simpler SQLite-based state.db/kanban.db, suffering platform-specific filesystem corruption.  
- OpenClaw’s release cadence is slower (weeks between major releases) vs Hermes Agent’s more frequent minor releases (~v0.19.0 late July).

**Community size comparison:**  
- OpenClaw appears to have a larger user base given 448 open issues and heavy commenting (top issue 18 comments).  
- Hermes Agent’s community is smaller but more concentrated on desktop/CLI workflows, with notable feature requests (Kanban integration, RPM throttling) indicating a developer-heavy audience.

## 4. Shared Technical Focus Areas

Both projects, despite different architectures, show converging requirements:

| Focus Area | OpenClaw | Hermes Agent |
|---|---|---|
| **OAuth token refresh reliability** | Multiple P1s (#86215, #89278 – Codex OAuth wedge, timeout) | #44799 – Codex OAuth refresh chain during idle cooldown |
| **Memory / state database corruption** | #90361 (index metadata missing), #112423 (SQLite transcript cleanup blocking) | #68545 (macOS virtiofs corruption), #53819 (Kanban DB concurrent write) |
| **Multi-agent message delivery** | #39476 (A2A duplicate messages), #92433 (dropped subagent completions) | #73771 (MEDIA dedup drops re-send), #18659 (skill commands cleared on scan failure) |
| **Cron / scheduled task reliability** | #91363 (LLM request failed), #89095 (subagent run timeouts) | (Not explicitly reported, but similar concern in event-loop closure #60197) |
| **Platform portability** | Discord, Telegram, Feishu, Windows CLI regressions (#91144, #105528) | macOS APFS, virtiofs, Linux ZFS, Windows Desktop updater (#74267) |
| **Developer tooling & test stability** | Few test-focused PRs; CI backlog | Large batch of 12 hermetic test PRs merged today |

**Underlying need:** Both projects must invest in **zero-downtime authentication**, **cross-platform filesystem resilience**, and **guaranteed message delivery** for production use cases.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|---|---|---|
| **Target users** | Self-hosters, power users, multi-agent orchestrators | Desktop-centric developers, CLI enthusiasts, small teams |
| **Primary interface** | CLI + channel integrations (Discord, Telegram, Slack) | Desktop app + CLI + SSH remote mode |
| **Architecture style** | Monolithic gateway with plugins; Codex-native hooks | Modular profile system; managed runtime + Kanban board |
| **Memory management** | Active memory + Codex summarization; pre-compaction flush | SQLite-based state.db/kanban.db; per-session session DB |
| **Testing discipline** | Moderate; many open bugs without linked PRs | Strong; hermetic test suite, CI pipeline hardening |
| **Community engagement** | High-volume issue reporting but decision backlog | Smaller, more focused discussions; faster resolution |
| **Feature set maturity** | Broad: email, Slack, Telegram, subagents, cron, hooks | Narrower: focus on desktop, Kanban, delegation, telemetry |
| **Key differentiator** | **Deep Codex integration & multi-agent A2A protocol** | **Desktop-first experience & test reliability** |

**Takeaway:** OpenClaw is better suited for complex multi-agent automations across channels; Hermes Agent excels for individual developers who want a stable, portable desktop assistant.

## 6. Community Momentum & Maturity

**Activity tiers:**  
- **Tier 1 (Very High):** OpenClaw – 500 daily actions, but **growing pains** in stability and decision-making.  
- **Tier 2 (High):** Hermes Agent – 50 daily actions, but **disciplined iteration** with rapid PR merging.

**Rapidly iterating:** Both projects are iterating, but OpenClaw’s high PR count (402 open) suggests many contributions awaiting review, whereas Hermes Agent closed 15 PRs today, indicating a tighter feedback loop.

**Stabilizing:**  
- OpenClaw is in a **stabilization phase** – many P1 bugs unresolved, no new release, but key regressions (email config, systemd units) recently closed.  
- Hermes Agent appears **more stable** – its test suite is hermetic; P1 bugs are rare and quickly addressed (#60197 closed). The focus on platform-specific filesystem fixes indicates work toward broader compatibility.

**Maturity indicators:**  
- Hermes Agent has a more formal release process (v0.19.0 tagged 10 days ago) and author attribution pipeline.  
- OpenClaw relies on community-driven labeling (`clawsweeper` tiers) but lacks structured release notes for recent progress.

## 7. Trend Signals

From combined community feedback, five industry-level trends emerge:

1. **Codex dependency becomes double-edged sword.** Both projects struggle with OAuth refresh and hook performance when using Codex. Users demand **autonomous fallback** when the Codex integration fails (e.g., switch to local model or retry with exponential backoff).

2. **Multi-agent coordination is the next frontier.** OpenClaw’s A2A duplicate/dropped messages and Hermes Agent’s delegation profiles (#71727) show users want reliable subagent orchestration without message loss. Expect standardized protocols (e.g., agent-to-agent handshake) to emerge.

3. **Filesystem portability is critical for production.** SQLite corruption on APFS, virtiofs, ZFS is a recurring pain. Projects will adopt **configurable journal modes** and **FUSE-based workarounds**.

4. **Desktop CLI integration is undervalued.** Hermes Agent’s Kanban board request (16👍) and OpenClaw’s Slack/Modal support (#88154) signal that users want richer visual workflows, not just chat interfaces. **Desktop-first assistants** may differentiate from pure CLI tools.

5. **Telemetry and cost tracking are missing.** Per-model usage logging (#13219 in OpenClaw) and RPM-based throttling (#7489 in Hermes Agent) indicate a growing need for observability in production—both for budgeting and debugging.

**Strategic value for AI agent developers:** Invest in **resilient authentication**, **cross-platform file I/O**, **guaranteed message delivery**, and **desktop visual components**. The ecosystems are still early; projects that solve these pain points will capture the most mindshare.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-30

## Today’s Overview

The Hermes Agent project saw **high activity** in the last 24 hours: 50 issues updated (32 open, 18 closed) and 50 pull requests updated (35 open, 15 merged/closed). No new releases were published. The bulk of merged PRs (12 in a single batch) focused on **test-stability, hermeticity, and platform-specific fixes**, indicating a strong push to harden the CI pipeline and eliminate flaky tests. Meanwhile, several **P1/P2 bugs** were reported in configuration handling, desktop remote mode, and platform compatibility, keeping the maintainers busy on critical regressions. Overall, the project remains actively maintained with a healthy blend of new features, bug squashing, and infrastructure improvements.

## Releases

No new releases (latest: none reported). The last known version is **v0.19.0** (tagged 2026-07-20).

## Project Progress

Fifteen pull requests were closed or merged today, with the most notable being a **test-stability backlog land** (#74517) that salvaged 12 external contributions and achieved a full suite of 22,588 passing tests. Key merged PRs include:

- **Test hermeticity and robustness**
  - `fix(honcho): network-hermetic unit tests + lazy async writer start` (#67576) – prevents silent writes to production Honcho instances.
  - `test: guard browser and Keychain side effects` (#35464) – stops real OAuth windows or Keychain reads during local test runs.
  - `fix(test): importlib.reload isolation leak in test_web_server.py` (#39038) – resolves suite-order-dependent failures.
  - `fix(test): fail-closed kanban write guard` (#69385) – protects user’s real `~/.hermes` from accidental pollution.
  - `fix(test): patch _launch_configured_cwd in completion tests` (#70148) – makes path-filter tests hermetic.
  - `fix(tests): hermetic env must disable lazy pip installs` (#43782) – prevents intermittent proxy timeout failures.
  - `fix(test): hermetic env-detection tests` (#71393) – fixes container and macOS shell detection.
  - `test: fix flaky blocking-approval E2E poll under CI load` (#63522) – removes time-sensitive race.
  - `test: assert SessionDB timeout without wall-clock` (#69176) – deflakes cron DB timeout test.
  - `test: scope session.create close_race orphan-cleanup assert to own session key` (#46189) – avoids false positives.
  - `fix(session): resolve runtime state DB path for test isolation` (#11875) – ensures `HERMES_HOME` overrides are honored.
- **Infrastructure**
  - `chore(release): map jethachan@gmail.com to jethac in AUTHOR_MAP` (#63560) – unblocks PR attribution checks.

These changes collectively improve developer experience, CI reliability, and platform portability.

## Community Hot Topics

The most active discussions (by comment count) highlight persistent pain points with configuration, filesystem compatibility, and desktop integration:

| Issue | Comments | Topic |
|-------|----------|-------|
| [#71298](https://github.com/NousResearch/hermes-agent/issues/71298) *[OPEN]* | 13 | **Providers vs custom_providers dual storage** – CLI/GUI mismatch and model version stuck in profile. Labeled P2, needs repro. |
| [#69551](https://github.com/NousResearch/hermes-agent/issues/69551) *[OPEN]* | 12 | **Desktop SSH remote mode broken with non-default profile** – token-path validation resolves against profile-scoped `HERMES_HOME` while client hardcodes `~/.hermes/desktop-ssh`. P2, needs decision. |
| [#41222](https://github.com/NousResearch/hermes-agent/issues/41222) *[OPEN]* | 9 (+16 👍) | **Feature Request: Integrate Kanban Board into Desktop App** – users want to avoid switching between CLI and desktop for multi-agent workflows. |
| [#60197](https://github.com/NousResearch/hermes-agent/issues/60197) *[CLOSED]* | 8 | **RuntimeError: Event loop is closed during /exit** – MCP server tasks emit ignored exceptions. P1, fixed in pending PR? (closed without merge?) |
| [#53819](https://github.com/NousResearch/hermes-agent/issues/53819) *[OPEN]* | 7 | **Kanban DB corruption under high concurrent-worker load** – SQLite writes from multiple workers need serialization. P3, needs decision. |
| [#68545](https://github.com/NousResearch/hermes-agent/issues/68545) *[CLOSED]* | 6 | **state.db corruption on macOS virtiofs** – `checkpoint_fullfsync` gated on `sys.platform == "darwin"`, missing in Linux containers. P2. |
| [#7489](https://github.com/NousResearch/hermes-agent/issues/7489) *[OPEN]* | 6 (+5 👍) | **RPM-based pre-emptive throttling using x-ratelimit headers** – proposal to avoid expensive 429 retry loops. P3. |
| [#73771](https://github.com/NousResearch/hermes-agent/issues/73771) *[CLOSED]* | 5 | **Session-wide MEDIA dedup silently swallows explicit “send it again” requests** – Telegram/other platforms affected. P2. |
| [#73109](https://github.com/NousResearch/hermes-agent/issues/73109) *[CLOSED]* | 5 | **Successful managed-runtime repair leaves stale venv (1.1 GB)** – no cleanup mechanism. P3. |
| [#44799](https://github.com/NousResearch/hermes-agent/issues/44799) *[OPEN]* | 5 | **Codex OAuth refresh chain not maintained during idle cooldown** – refresh token expires. P2. |
| [#18659](https://github.com/NousResearch/hermes-agent/issues/18659) *[OPEN]* | 5 | **scan_skill_commands clears all skills on scan failure** – all 90+ slash commands lost silently. P2, needs decision. |

Underlying needs: users are demanding **configuration consistency** (no dual storage), **platform-agnostic filesystem support** (APFS, ZFS, virtiofs), **better desktop integration** (Kanban, profile switching), and **resource cleanup** (stale venv, OAuth token refresh). The high upvotes on the Kanban feature (#41222) signal strong community desire for a richer desktop experience.

## Bugs & Stability

**Critical and High-severity bugs reported or updated today:**

- **[P1] (#74373)** *[OPEN]* – `distribution_owned` does not constrain profile distribution copy/update payload, potentially allowing unintended profile overwrites. No fix PR yet.
- **[P1] (#60197)** *[CLOSED]* – `Event loop is closed during /exit` (MCP server shutdown). Closed without merge? Needs verification.
- **[P2] (#71298)** *[OPEN]* – Providers vs custom_providers dual storage causes CLI/GUI mismatch. Needs repro data.
- **[P2] (#69551)** *[OPEN]* – Desktop SSH remote mode broken with non-default profile. Needs decision.
- **[P2] (#74267)** *[OPEN]* – Windows Desktop updater falsely detects running Hermes processes, blocking update. Reproducible after reboot.
- **[P2] (#74345)** *[OPEN]* – `hermes meet install` upgrades `websockets` unconditionally, breaking the project’s own pin (websockets==15.0.1). Immediate compatibility issue.
- **[P2] (#71498)** *[CLOSED]* – APFS CoW + SQLite WAL incompatibility causes disk I/O errors on macOS. Fix merged? (closed, likely fixed in #71498 or follow-up).
- **[P2] (#67165)** *[CLOSED]* – cua-driver macOS ScreenCaptureKit returns zero display count despite permissions OK. Fix merged.
- **[P2] (#73771)** *[CLOSED]* – MEDIA dedup drops re-send requests. Fix merged.

Several open bugs have **associated fix PRs** in flight:
- For #70679 (desktop global remote mode hides profile switcher), PR [#74500](https://github.com/NousResearch/hermes-agent/pull/74500) proposes a fix (refresh profiles on gateway ready).
- For #73109 (stale venv), likely a cleanup PR is expected.
- For #68545 (macOS virtiofs corruption), the issue is closed, implying a fix has been merged (e.g., configurable journal mode from #57820).

Overall, the project has been actively addressing filesystem-corruption bugs (SQLite on APFS, ZFS, virtiofs) through configurable journal mode and fallbacks.

## Feature Requests & Roadmap Signals

Notable feature requests and open PRs that hint at future direction:

| Feature | Status | Comments |
|---------|--------|----------|
| **Kanban Board integration into Desktop** [#41222](https://github.com/NousResearch/hermes-agent/issues/41222) | OPEN, P3, 16 👍 | High community demand; could be a candidate for next release given desktop focus. |
| **RPM-based pre-emptive throttling** [#7489](https://github.com/NousResearch/hermes-agent/issues/7489) | OPEN, P3, 5 👍 | Would reduce 429 retry loops; likely to be implemented with the new telemetry work. |
| **Named delegation profiles** [#71727](https://github.com/NousResearch/hermes-agent/issues/71727) | OPEN, P3 | Prevents incoherent model/endpoint pairs for subagents. |
| **Account-wide GitHub pull requests dashboard** [#62352](https://github.com/NousResearch/hermes-agent/issues/62352) | OPEN, P3 | Enhances desktop coding workflow. |
| **Opt-in per-turn waterfall tracing** PR [#65329](https://github.com/NousResearch/hermes-agent/pull/65329) | OPEN | Telemetry for debugging agent calls; needs decision on activation mechanism. |
| **Host-enforced turn gate extension point** PR [#74529](https://github.com/NousResearch/hermes-agent/pull/74529) | OPEN | Adds plugin-owned provider registration with lease enforcement. |
| **Re-add Vercel AI Gateway provider** PR [#74518](https://github.com/NousResearch/hermes-agent/pull/74518) | OPEN | Modernized revert of #33067; expands provider ecosystem. |
| **Desktop profile refresh on global remote** PR [#74500](https://github.com/NousResearch/hermes-agent/pull/74500) | OPEN | Fixes #70679, enhances remote multi-profile support. |

Given the volume of desktop-related fixes and features, the next release (v0.20.0 likely) will probably include:
- Kanban board desktop integration (if prioritised)
- Turn tracing and telemetry
- Vercel AI Gateway provider
- Continued robustness for SQLite across platforms.

## User Feedback Summary

Real user pain points captured in today’s dataset:

- **Configuration confusion**: Users report that `providers` and `custom_providers` in `config.yaml` are independently stored and inconsistently displayed, leading to model version being stuck (#71298).
- **Desktop remote mode unusable with profiles**: SSH remote mode fails when a non-default profile is active, making remote usage effectively single-profile (#69551).
- **Platform-specific filesystem corruption**: Multiple reports of `state.db`/`kanban.db` corruption on macOS (APFS, virtiofs), Linux (ZFS), and even on

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*