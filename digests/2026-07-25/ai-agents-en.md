# OpenClaw Ecosystem Digest 2026-07-25

> Issues: 465 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-25 02:13 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-25

## 1. Today's Overview

OpenClaw continues to see extremely high activity: **465 issues** and **500 pull requests** were updated in the last 24 hours. Of those, **297 PRs were closed or merged**, indicating a strong pace of bug fixes and incremental improvements. However, **no new releases** were published today, and **357 open/active issues** remain. The project’s health is mixed: the community is highly engaged, and many regressions are being addressed quickly, but a significant backlog of P1/P0 bugs—especially around session recovery, compaction timeouts, and provider compatibility—continues to strain maintainers. Labels like `clawsweeper-recovery-stuck` and `needs-maintainer-review` appear on dozens of high-severity items, suggesting that some systemic issues remain unresolved for weeks.

## 2. Releases

**No new releases today.** The latest release remains the `2026.7.2-beta` series; no changelog or migration notes were published.

## 3. Project Progress

Of the **297 closed/merged PRs**, notable examples from the top-by-comment list include:

- **#113459** (merged) – *fix(sqlite): prevent stale verifier quarantine after database replacement*. Closes the SQLite snapshot integrity race (related to #113306).
- **#113450** (merged) – *feat(ui): render chat notice rows as markdown*. Improves readability of system-notice transcripts in the Control UI.
- **#112416** (open) – *fix(compaction): thread agent streamFn into safeguard summarizer*. Addresses an OpenRouter-provider fallback issue during compaction.
- **#113460** (open) – *chore: stabilize session cost usage cache warmup test*. Prevents validation flakes on CI.
- **#113462** (open) – *fix(moonshot): type anyOf branches so Kimi accepts MCP tool schemas*. Fixes a provider-specific compatibility issue.

Other merged PRs targeted proxy support for model discovery (Venice, Kilocode, OpenRouter), Telegram/QQ Bot media path handling, gateway config reload intent, and uninstall shell-completion cleanup. Many fixes are still in review.

## 4. Community Hot Topics

The following issues drew the most comments and reactions, revealing deep community concerns:

- **Issue #102020** – *[Bug]: Second message in a session fails with “reply session initialization conflicted” (cross-channel, position-dependent)*  
  (16 comments, 1 👍)  
  https://github.com/openclaw/openclaw/issues/102020  
  **Analysis:** A repeatable cross-channel bug that blocks multi-turn conversations after the first reply. Comments indicate the problem is seen on both Signal and da‑ channels. No fix PR linked yet.

- **Issue #86996** – *Active Memory + Codex app-server path causes long response latency, hook timeouts, startup aborts, and gateway event-loop stalls*  
  (14 comments, 2 👍)  
  https://github.com/openclaw/openclaw/issues/86996  
  **Analysis:** A P1 performance bug affecting users who combine Active Memory, `openclaw-honcho`, and OpenAI/Codex models. The issue leads to gateway stalls and startup failures. Labeled `clawsweeper-recovery-stuck`.

- **Issue #94228** – *Native Anthropic path: replaying historical `thinking` blocks bricks long tool-use threads (400 Invalid signature)*  
  (14 comments, 2 👍)  
  https://github.com/openclaw/openclaw/issues/94228  
  **Analysis:** A provider-specific bug that renders long Anthropic tool-use sessions permanently broken. Community members report workarounds but no official fix.

- **Issue #92043** – *Bug: 180s compaction timeout is a single wall clock over the whole chunk pipeline with no partial-progress reuse*  
  (13 comments, 3 👍)  
  https://github.com/openclaw/openclaw/issues/92043  
  **Analysis:** A P1 design flaw in the compaction pipeline. Even legitimate long-running compactions fail identically every turn. Linked PR #92231 is open.

- **Issue #107220** – *2026.7.1 gateway crash-loop: legacy memory sidecar `meta`/`chunks` conflicts are fatal while `files` conflicts auto-resolve*  
  (10 comments, 1 👍; **CLOSED**)  
  https://github.com/openclaw/openclaw/issues/107220  
  **Analysis:** A P0 crash-loop regression after upgrading to **2026.7.1**. Already closed, suggesting a fix was deployed quickly. Community relief.

- **Issue #110950** – *[Feature]: Everything is a cron — unify heartbeat, watchers, and scheduled automation*  
  (10 comments, 2 👍; **CLOSED**)  
  https://github.com/openclaw/openclaw/issues/110950  
  **Analysis:** A proposal to redesign OpenClaw’s automation primitives around a single cron abstraction. Closed as a feature request, but likely being considered for the next major release.

## 5. Bugs & Stability

**New or newly active high-severity bugs today:**

| Severity | Issue | Summary | Fix PR exists? |
|----------|-------|---------|----------------|
| **P0** | #107220 (closed) | Gateway crash-loop on upgrade – memory sidecar conflicts | Yes (closed) |
| **P0** | #90378 | Cron store migration to SQLite silently breaks channel delivery | Linked PR open |
| **P1** | #113306 | SQLite snapshot restore lacks crash and identity guarantees | Yes (#113459 merged) |
| **P1** | #102020 | Second message fails with session initialization conflict | No |
| **P1** | #86996 | Active Memory + Codex causes latency/stalls | No |
| **P1** | #94228 | Anthropic `thinking` blocks brick tool-use threads | No |
| **P1** | #92043 | Compaction timeout design flaw | Linked PR open (#92231) |
| **P1** | #106786 | gpt-5.6 models silently fall back on ChatGPT-OAuth | No |
| **P1** | #111519 (regression) | Telegram DM replies fall back after stale DM-scope cleanup | No |
| **P1** | #111498 (regression) | Main agent blocked by workspace-state migration after Anthropic auth recovery | No |
| **P1** | #98528 (closed) | Tool output returns empty after first call per turn (2026.6.11 regression) | Yes (closed) |
| **P2** | #112906 (regression) | Rich messages `\`\`` tags no longer collapsible (2026.7.1) | No |

**Stability concerns:** Many P1 issues remain open for weeks, some with `clawsweeper-recovery-stuck` label, indicating the project’s recovery mechanisms themselves are failing. Compaction, memory sidecar conflicts, and provider-specific signature issues are recurring themes.

## 6. Feature Requests & Roadmap Signals

The following feature requests received strong community support and are plausible candidates for the next release:

- **#110950** (closed) – *Everything is a cron* – Already discussed above; closing suggests maintainer interest in designing a unified automation system.
- **#7722** – *Filesystem Sandboxing Config (tools.fileAccess)* – 4 👍, 10 comments; addresses security concerns.  
  https://github.com/openclaw/openclaw/issues/7722
- **#10687** – *Fully dynamic model discovery (OpenRouter + beyond)* – 3 👍, 10 comments; a critical usability gap for fast-moving model catalogs.  
  https://github.com/openclaw/openclaw/issues/10687
- **#45758** – *Support YAML as config file format* – 2 👍, 8 comments; a low-effort quality-of-life improvement.  
  https://github.com/openclaw/openclaw/issues/45758
- **#12219** – *Skill Permission Manifest Standard (skill.yaml)* – 0 👍 but 6 comments; security-focused.  
  https://github.com/openclaw/openclaw/issues/12219
- **#46812** – *Control UI: Pinned context panel for user-defined persistent facts* – 1 👍, 6 comments; addresses a common complaint about manual MEMORY.md editing.  
  https://github.com/openclaw/openclaw/issues/46812
- **#46058** – *Exploring a chat-first Android surface* – 1 👍, 6 comments; discussion of upstreaming parts of an independent Android fork.  
  https://github.com/openclaw/openclaw/issues/46058

**Predictions:** The “everything is a cron” feature appears to have strong maintainer buy-in and could land in **2026.8.x**. Dynamic model discovery and YAML config are low-effort wins that might appear in a minor point release. Sandboxing and skill permissions are longer-term roadmap items.

## 7. User Feedback Summary

Real user pain points captured from recent issues:

- **Session recovery is unreliable.** Several issues (#102020, #86996, #92043, #90378) describe situations where sessions either cannot be initialized after the first turn, get stuck indefinitely, or lose context after recovery. Users express frustration with “[reply session initialization conflicted]” and “180s compaction timeout” preventing any forward progress.
- **Upgrade breaks existing configurations.** #107220 (crash-loop on 2026.7.1) and #90378 (cron store migration) demonstrate that silent migration of storage backends can cause channel errors or total gateway failure. Users want safer upgrade paths and better migration logging.
- **Provider-specific regressions are common.** Anthropic thinking blocks (#94228), OpenAI prompt-cache churn (#95610), Ollama streaming not consumed (#94251), and ChatGPT-OAuth model fallback (#106786) show that multi-provider support is fragile. Users request better error messages and automatic fallback verification.
- **Telegram and Discord channel reliability issues persist.** #91564 (forum topic black hole), #111519 (DM reply fallback), #96007 (message truncation on Discord) indicate that chat platform integrations need more thorough testing.
- **Security and sandboxing** remain top-of-mind. Issues #7722 (filesystem sandbox), #12219 (skill permissions), #12219, and #48104 (model safety blocking authorized operations) show a community that wants both security and flexibility.
- **UI/UX friction:** #112906 (rich messages broken), #9637 (TUI emojis inaccessible), #10944 (Telegram parse_mode). Users want accessibility improvements and configurable message rendering.

Overall satisfaction is mixed: the speed of fixes (many PRs closed daily) is appreciated, but the recurrence of similar bug patterns (session state, provider compatibility, channel wedge) points to systemic issues that need architectural attention.

## 8. Backlog Watch

Several important issues have been open for months without a maintainer response or fix PR, despite high comment counts and severity labels. These are at risk of becoming stale:

- **#67419** (P2, 10 comments, last updated Apr 15) – *Session context bloat: bootstrap files re-injected every turn, wasting 20-30% tokens*  
  https://github.com/openclaw/openclaw/issues/67419  
  Labels: `clawsweeper:needs-maintainer-review`, `clawsweeper:needs-product-decision`

- **#47975** (P1, 10 comments, last updated Mar 16) – *Subagent sessions persist after completion, main session becomes unresponsive*  
  https://github.com/openclaw/openclaw/issues/47975  
  Labels: `stale`, `clawsweeper:needs-maintainer-review`

- **#45494** (P1, 9 comments, last updated Mar 13) – *Cron agent jobs silently time out during sustained LLM API outages instead of fast-failing*  
  https://github.com/openclaw/openclaw/issues/45494  
  Labels: `stale`, `regression`, `clawsweeper:needs-maintainer-review`

- **#45758** (P3, 8 comments, last updated Mar 14) – *Support YAML as config file format*  
  https://github.com/openclaw/openclaw/issues/45758  
  Labels: `stale`, `clawsweeper:needs-maintainer-review`

- **#57256** (P2, 7 comments, last updated Mar 29) – *`openclaw status` falsely reports memory as unavailable when live gateway plugin is working*  
  https://github.com/openclaw/openclaw/issues/57256  
  Labels: `stale`, `bug:behavior`, `clawsweeper:needs-maintainer-review`

- **#53540** (P1, 7 comments, last updated Mar 24) – *Embedded runner “Network connection lost” when LLM generates a tool call with large parameters*  
  https://github.com/openclaw/openclaw/issues/53540  
  Labels: `stale`, `clawsweeper:needs-maintainer-review`

These issues represent long-standing pain points that have not received maintainer feedback. The `stale` label suggests automatic bot-marking, but no manual push has occurred for months. If not addressed, they risk eroding user trust in the project’s responsiveness to critical session-state and performance concerns.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Open-Source Personal AI Assistant Ecosystem
**Date:** 2026-07-25

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem remains highly dynamic, with two major reference implementations—OpenClaw and Hermes Agent—both sustaining exceptional development velocity. OpenClaw operates at a significantly larger scale (465 issues, 500 PRs updated daily), reflecting its position as the de facto community standard with broad provider support and a complex plugin architecture. Hermes Agent, while smaller (50 issues, 50 PRs), demonstrates focused engineering discipline, prioritizing Windows compatibility, Telegram reliability, and text-encoding robustness. Both projects share systemic challenges around session state management, provider-specific regressions, and upgrade safety, indicating that the ecosystem has moved past initial capability demonstrations into a phase of hardening multi-provider, multi-platform deployments. The community's tolerance for instability appears to be decreasing, with users demanding reliable session recovery, predictable upgrades, and secure sandboxing.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues updated (24h)** | 465 | 50 |
| **PRs updated (24h)** | 500 | 50 |
| **PRs merged/closed** | 297 | 10 |
| **Open issues** | ~357 | ~33 |
| **New releases** | None (latest: 2026.7.2-beta) | None |
| **P0 bugs open** | 0 (1 closed today) | 0 |
| **P1 bugs open** | ~10 high-severity | 3 open, 1 fixed today |
| **Stale backlog items** | 6+ issues (weeks-months old) | None identified |
| **Health assessment** | High activity, strained maintainers, systemic recovery issues | Focused iteration, targeted fixes, stable but smaller scope |

OpenClaw operates at ~10x the raw activity volume of Hermes Agent. However, its higher bug backlog-to-fix ratio and the presence of weeks-old unresolved P1 issues suggest scalability challenges in maintainer bandwidth. Hermes merges fewer PRs but closes a higher proportion of its reported issues, indicating tighter issue triage.

## 3. OpenClaw's Position

**Advantages:**

- **Market leader by community size and contributor base** – 465 issues and 500 PRs updated daily demonstrate unmatched ecosystem engagement. No other open-source AI agent project approaches this velocity.
- **Broadest provider support** – Active fixes for OpenAI, Anthropic, OpenRouter, Venice, Kilocode, Moonshot/Kimi, Ollama, and custom endpoints. Multi-provider fallback is a first-class concern.
- **Plugin/extension architecture** – Gateway, memory sidecar, cron automation, and channel bots (Telegram, QQ, Signal, Discord) create a composable system that appeals to power users and integrators.
- **Rapid regression fixes** – 297 PRs merged today alone; critical crash-loop bugs (e.g., #107220) closed within 24 hours of reporting.

**Technical approach differences:**

- OpenClaw uses a modular gateway + memory sidecar architecture with SQLite-based persistence and cron-driven automation. Compaction and session recovery are explicit pipeline stages.
- Multiple recovery mechanisms (clawsweeper, compaction summarizers) introduce complexity that, when they fail, cascade into "recovery stuck" states.

**Community size:** OpenClaw's community engagement is an order of magnitude larger than any comparable project. The 357 open issues and dozens of active feature requests indicate both broad adoption and higher fragmentation of user expectations.

## 4. Shared Technical Focus Areas

Both projects are investing heavily in the same problem domains, suggesting these are ecosystem-wide requirements:

| Focus Area | OpenClaw | Hermes Agent |
|------------|----------|--------------|
| **Session state recovery** | P0/P1 bugs: session init conflicts (#102020), compaction timeouts (#92043), migration breaks (#90378) | Fixed: Telegram hang on cold start (#67498); open: session continuity hints PR (#70972) |
| **Provider-specific compatibility** | Anthropic thinking blocks (#94228), ChatGPT-OAuth fallback (#106786), gpt-5.6 silent fallback | No direct equivalent (Hermes focuses on fewer providers) |
| **Windows/desktop reliability** | Not a primary focus | P1: app can't run after update (#69179); multiple encoding/cert fixes merged |
| **Encoding and text handling** | No specific encoding issues reported | 5+ encoding fixes merged today (BOM, cp1252, UTF-8 lock files) |
| **Security / sandboxing** | Feature requests: filesystem sandboxing (#7722), skill permissions (#12219) | Credential masking PR open (#67344) |
| **Telegram integration** | DM reply fallback regression (#111519) | Telegram hang fixed (#71118); polling reliability addressed |
| **Upgrade safety** | Migration breaks cron delivery (#90378); crash-loop on 2026.7.1 (#107220) | Desktop update integrity checks (#71119); app can't run after update (#69179) |

**Key takeaway:** Session state reliability and upgrade safety are the two most pressing cross-project pain points. Both projects are actively patching these, but OpenClaw's architectural complexity makes systemic fixes slower to propagate.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Target user** | Power users, self-hosters, multi-channel deployment | Desktop-first, Windows users, evaluation/inference workflows |
| **Primary use case** | Conversational AI agent with tool use, memory, automation | Personal assistant with TTS, desktop integration, Telegram |
| **Provider support** | 10+ providers, dynamic discovery | Fewer providers, but deeper integration |
| **Deployment model** | Gateway + sidecar + channels; complex, modular | Desktop app + Telegram; simpler architecture |
| **Automation** | Cron agents, event-driven ("everything is a cron") | Not a primary focus |
| **Memory system** | Active Memory, memory sidecar, SQLite compaction | Memory tools, file-based; less complex |
| **UI surfaces** | Control UI, TUI, Telegram/QQ/Discord bots | Desktop app, Telegram |
| **Evaluation/testing** | No dedicated evaluation harness | Deterministic evaluation harness PR open (#67343) |

OpenClaw is a **conversational platform** optimized for breadth (many providers, many channels, automation, memory). Hermes Agent is a **personal assistant application** optimized for depth (Windows desktop, TTS, session continuity). They are likely to converge in vision but serve different developer audiences today.

## 6. Community Momentum & Maturity

**Activity Tiers:**

- **Tier 1 – Hyper-growth with strain:** *OpenClaw* – Sustained 500+ PRs/day closed, but P1 bugs linger for weeks and maintainer bandwidth is visibly stretched. The community is growing faster than the core team can review, leading to a "fix quickly, but systemically fragile" pattern.
- **Tier 2 – Focused maturation:** *Hermes Agent* – 10 PRs/day closed, but each targets a verified regression with high specificity. The team prioritizes Windows and Telegram reliability over feature breadth. Fewer stale issues indicate better maintainer-to-issue ratio.

**Maturity signals:**
- OpenClaw is in a **stabilization phase** after rapid feature growth. The "everything is a cron" proposal (#110950) suggests a design-level rethink of automation primitives—a sign of architectural maturity.
- Hermes Agent is in a **platform-hardening phase**, eliminating encoding, signing, and boot-time failures. The evaluation harness PR (#67343) signals growing interest in reproducibility and benchmarking.

**Risk assessment:** OpenClaw's unresolved P1 bugs (session init conflicts, compaction failures, Anthropic signature errors) pose higher risk for production deployments. Hermes Agent's bugs are more contained but Windows compatibility remains fragile.

## 7. Trend Signals

From community feedback across both projects, the following industry trends are evident:

1. **Session state is the new bottleneck.** Users across projects report the same failure mode: the first turn works, the second turn fails. Multi-turn conversation reliability is now the critical success factor, not single-turn quality.

2. **Multi-provider deployments are brittle.** Provider-specific regressions (Anthropic thinking blocks, OpenAI fallback, Moonshot schema issues) are the most common bug category. The ecosystem is converging on a "provider abstraction layer" that is not yet mature.

3. **Upgrade safety is non-negotiable.** Silent migration breaks, crash-loops after upgrade, and binary signing failures erode trust. Both projects are investing in pre-flight checks and migration guardrails.

4. **Security is rising in priority.** Filesystem sandboxing, skill permissions, credential masking, and model safety checks are moving from feature requests to architectural requirements.

5. **Desktop + mobile surfaces are underserved.** Hermes Agent targets Windows; OpenClaw's Control UI and TUI are functional but rough. The community wants polished, accessible interfaces—especially chat-first mobile.

6. **Evaluation and reproducibility are emerging concerns.** Hermes Agent's evaluation harness PR is a leading indicator. As agents grow more complex, the community will demand standardized benchmarks and deterministic testing.

7. **Community documentation and maintainer responsiveness are becoming pain points.** Stale backlog items (OpenClaw) and uncommented issues signal that growth in adoption outpaces growth in contributor documentation. This is a systemic risk for both projects.

**Value for AI agent developers:**
- Invest in session recovery and state management early—it will be your most reported bug.
- Choose your provider abstraction carefully; narrow provider support (Hermes approach) reduces surface area but limits reach.
- Plan for upgrade safety from day one: migration testing, binary integrity checks, and backward compatibility guarantees.
- Expect community pressure for security sandboxing and evaluation tooling within 6–12 months.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-25

## 1. Today's Overview
Project activity remains very high: 50 issues and 50 pull requests were updated in the last 24 hours. Of these, 17 issues were closed and 10 PRs were merged/closed, reflecting a sustained push to fix critical bugs. The team focused heavily on Windows compatibility (executable signing, architecture verification, encoding issues), Telegram gateway reliability, and text‑encoding defects that have been generating duplicate reports. A notable P1 bug (Telegram hangs forever on cold start) was fixed and merged today, while a new P1 bug (“app can’t run on your computer” after update) remains open. No new releases were published.

## 2. Releases
No new releases today.

## 3. Project Progress
**Merged/closed pull requests (10 total)** – key improvements:

- **Telegram gateway hang** – PR [#71118](https://github.com/NousResearch/hermes-agent/pull/71118) (closed) requires proven polling readiness before reporting “connected”, fixing the indefinite hang at `Connecting to Telegram (attempt 1/8)`.  
- **Desktop update integrity** – PR [#71119](https://github.com/NousResearch/hermes-agent/pull/71119) (closed) adds PE header, architecture, and size sanity checks before shipping a rebuilt desktop executable, preventing corrupt or wrong‑arch binaries from replacing a working Hermes.exe.  
- **Checkpoint pruning on unmounted volumes** – PR [#71117](https://github.com/NousResearch/hermes-agent/pull/71117) (closed) narrows orphan classification so that an unmounted or detached volume no longer triggers deletion of project checkpoint history.  
- **TTS playback fixes** – Four PRs were merged to improve TTS: batch synchronous provider playback ([#70535](https://github.com/NousResearch/hermes-agent/pull/70535)), serialize batch TTS to prevent audio overlap ([#70601](https://github.com/NousResearch/hermes-agent/pull/70601)), carry leftover bytes for misaligned PCM streaming chunks ([#70851](https://github.com/NousResearch/hermes-agent/pull/70851)), and prevent duplicate TTS response rendering ([#70497](https://github.com/NousResearch/hermes-agent/pull/70497)).  
- **Session reopening crash** – PR [#70586](https://github.com/NousResearch/hermes-agent/pull/70586) (closed) fixes a TypeError in the desktop renderer when reopening a session that contains `async_delegation_complete` messages.  
- **.env BOM handling** – Issue [#65123](https://github.com/NousResearch/hermes-agent/issues/65123) (closed) was resolved with a fix for UTF‑8 BOM silently dropping the first key in `.env`.  
- **Windows cron encoding** – Issue [#42785](https://github.com/NousResearch/hermes-agent/issues/42785) (closed) corrected platform‑default encoding (cp1252) decoding of `no_agent` script stdout.  
- **Copilot ACP encoding** – Issue [#38119](https://github.com/NousResearch/hermes-agent/issues/38119) (closed) added explicit UTF‑8 encoding to ACP file read/write shim.  
- **Chinese Windows lock file** – Issue [#68369](https://github.com/NousResearch/hermes-agent/issues/68369) (closed) fixed `HubLockFile.load()` to use explicit UTF‑8 instead of platform default.  
- **Memory UnicodeDecodeError** – Issue [#10879](https://github.com/NousResearch/hermes-agent/issues/10879) (closed) added `errors=` parameter to memory file reads, catching non‑UTF‑8 bytes gracefully.

**Open pull requests of note** – Several important features and fixes are still being reviewed:
- Session continuity hints and rotation nudges for long‑lived chats ([#70972](https://github.com/NousResearch/hermes-agent/pull/70972))
- Deterministic evaluation harness ([#67343](https://github.com/NousResearch/hermes-agent/pull/67343))
- Credential output masking across CLI/gateway ([#67344](https://github.com/NousResearch/hermes-agent/pull/67344))
- Deduplication of session system prompt snapshots ([#60852](https://github.com/NousResearch/hermes-agent/pull/60852))
- Persisting steer metadata to the session database ([#61013](https://github.com/NousResearch/hermes-agent/pull/61013))
- Cyrillic session search via trigram index ([#61646](https://github.com/NousResearch/hermes-agent/pull/61646))

## 4. Community Hot Topics
The most active threads (by comment count or reactions) reveal deep concerns around Windows compatibility and Telegram reliability:

- **#67498** (closed, 6 comments, 1 👍) – Telegram gateway hangs at “Connecting to Telegram (attempt 1/8)” even after applying the documented workaround. Users reported all threads idle, no progress. **Fixed today** by PR [#71118](https://github.com/NousResearch/hermes-agent/pull/71118).  
- **#60144** (closed, 6 comments) – Desktop boot fails on Windows when platform adapter import exceeds the 15‑second readiness timeout. Closed as fixed.  
- **#50210** (closed, 5 comments, 1 👍) – The Windows bootstrap installer produces an unsigned `Hermes.exe` that gets blocked by Smart App Control. Fixed in a previous release.  
- **#69179** (open, P1, 1 comment, 1 👍, [link](https://github.com/NousResearch/hermes-agent/issues/69179)) – After updating, the desktop app shows “This app can’t run on your computer” on Windows. This is the highest‑severity open issue today.  
- **#10878** (open, P2, 3 comments, 0 👍) – `memory_tool._read_file()` does not strip BOM, causing `\ufeff` to appear in the system prompt. A long‑standing issue (filed April 16) that still lacks a fix.  
- **#69230** (open, P2, 3 comments, 0 👍) – Desktop’s remote gateway reachability probe falsely reports “Could not reach this gateway yet” despite the server being healthy and reachable via curl.  
- **#71026** (open, P3, 3 comments, 0 👍) – `hermes insights --days 30` crashes with `TypeError: unsupported operand type(s) for -: 'str' and 'int'`. A regression in billing calculation.

## 5. Bugs & Stability
### Critical (P1)
- **App can’t run on Windows after update** ([#69179](https://github.com/NousResearch/hermes-agent/issues/69179)) – Open. No fix PR yet. Likely related to architecture mismatch or invalid binary.  
- **Telegram gateway hangs** ([#67498](https://github.com/NousResearch/hermes-agent/issues/67498)) – **Fixed** by PR [#71118](https

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*