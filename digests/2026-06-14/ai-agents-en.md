# OpenClaw Ecosystem Digest 2026-06-14

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-14 03:37 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-14

---

## 1. Today’s Overview

The OpenClaw project is experiencing extremely high activity: **500 issues and 500 pull requests updated in the last 24 hours**, with **400 open/active issues** and **213 merged/closed PRs** on the same day. Two new beta releases (v2026.6.7 and v2026.6.8) landed, focusing on richer channel delivery for Telegram and WhatsApp, tighter Slack integration, and more robust media handling. Despite this momentum, the project faces a deepening backlog of critical stability issues — several high-severity memory leaks, session state corruption, and silent data loss bugs remain unresolved for weeks or months. Community engagement is strong, with diamond-lobster–rated issues drawing 10–19 comments each, but many important features and security concerns await product decisions.

---

## 2. Releases

Two new beta versions were published:

### v2026.6.8-beta.1 (2026-06-08)
- **Highlights:**
  - Telegram channel delivery enhanced: structured rich text (tables, lists, expandable blockquotes), prompt-preserving CLI backend delivery, retired native draft migration, safer rich-media boundaries.
  - WhatsApp channel delivery richer and less brittle.
- No breaking changes or migration notes were documented.

### v2026.6.7-beta.1 (2026-06-07)
- **Highlights:**
  - Same-channel Slack finals persist in transcripts.
  - Top-level `image` message-tool sends attached media.
  - Expandable Telegram blockquotes and spool handling improvements.
  - Silent replies, progress drafts, and paged action results across Slack, Telegram, and outbound media.
- No breaking changes or migration notes documented.

---

## 3. Project Progress

Today saw **213 merged or closed PRs**. Notable fixes that advanced:

- **iOS Safari chat layout**: PR [#92855](https://github.com/openclaw/openclaw/pull/92855) (clownfish repair) and original [#63644](https://github.com/openclaw/openclaw/pull/63644) fix viewport handling and input zoom on iPhone.
- **Memory-core reindex bug**: PR [#92850](https://github.com/openclaw/openclaw/pull/92850) reset `lastMetaSerialized` so byte-identical reindex still writes `__meta`.
- **Slug generator error handling**: PR [#92854](https://github.com/openclaw/openclaw/pull/92854) rejects provider/auth error payloads that were being turned into memory filenames.
- **ACP server compatibility**: PR [#92853](https://github.com/openclaw/openclaw/pull/92853) accepts MCP date-string `protocolVersion` (e.g., `"2025-11-25"`) from VS Code 1.113+ and Cursor.
- **Tailscale JSON parse resilience**: PR [#92849](https://github.com/openclaw/openclaw/pull/92849) repairs the earlier fix to preserve parse errors for malformed JSON while handling noisy valid output.
- **Feishu thread routing**: PR [#73958](https://github.com/openclaw/openclaw/pull/73958) (still open) preserves `root_id` for group reply routing without forcing `thread_id`.
- **MCP protocol version**: PR [#56176](https://github.com/openclaw/openclaw/pull/56176) (closed today) accepts `protocolVersion` date strings in the ACP server.
- **Config hot-reload polling fallback**: PR [#92852](https://github.com/openclaw/openclaw/pull/92852) (open) adds polling mode when inotify watcher exhausts retries.

Several smaller fixes (e.g., heartbeat delivery, Mattermost thread context, control UI) also advanced but remain open.

---

## 4. Community Hot Topics

The most active discussions (by comment count and reactions) reveal deep concerns around session reliability, data loss, and security:

- **[Bug] Feishu monitor state leak** (#48183, 19 comments) — Memory leak in `httpServers` Map during monitor cleanup. Closed stale.
- **[Bug] Subagent completion silently lost** (#44925, 19 comments, 👍1) — No retry, no notification, no auto-restart on timeout. Still open with P1 severity.
- **[Feat] Centralized filename encoding** (#48788, 18 comments) — Proposal for multi-encoding Content-Disposition handling across all channels. Still open, needs product decision.
- **[Bug] gh-issues skill prompt injection** (#45740, 13 comments, 👍1) — Untrusted issue body injected directly into sub-agent prompts. Open, needs security review.
- **[Bug] Cron scheduled trigger contaminates global state** (#90991, 13 comments, 👍1) — Transient system-wide overload failures. Closed after fix.
- **[Bug] Steer mode not injecting mid-turn** (#48003, 12 comments, 👍2) — Queued messages don’t interrupt active main session turn. Open.
- **[Bug] Embedded-run session state leak** (#48573, 12 comments) — Zombie agents persist after parent termination. Closed stale.
- **[Feat] Per-agent cost budget enforcement** (#42475, 12 comments, 👍1) — Gateway-level daily/monthly spend caps. Open for months.
- **[Bug] Feishu read image tool loses media** (#41744, 12 comments) — Image attachment lost before final outbound payload. Open.
- **[Bug] Heartbeat/Cron stale timestamp** (#44993, 11 comments) — “Current time” not refreshing between runs. Open.
- **[Feat] Memory trust tagging by source** (#7707, 11 comments) — Prevent memory poisoning attacks. Open since Feb 3.
- **[Bug] Write tool lacks append mode** (#40001, 11 comments, 👍1) — Cron sessions overwrite shared files. Open.
- **[Bug] Discord leaks internal tool-call traces** (#44905, 10 comments, 👍1) — `NO_REPLY`, `commentary`, raw JSON visible to users. Open.
- **[Bug] Multi-agent orchestration unstable** (#43367, 10 comments, 👍1) — Config overwrites, session-lock failures, detached child work. Open.

**Underlying needs**: Operators are demanding better session isolation, robust subagent orchestration, transparent failure handling (fast-fail vs. silent timeout), and security hardening against prompt injection and data leakage.

---

## 5. Bugs & Stability

Multiple critical and high-severity bugs remain unresolved. Ranked by severity based on labels and community impact:

### P0 — Critical (ongoing crashes / data loss)
- **Gateway memory leak** (#91588, 10 comments, P0) — RSS grows from 350 MB to 15.5 GB over 2–3 days, causing OOM kills. No fix PR linked. **Most urgent.**

### P1 — High (session state corruption, message loss, crashes)
- **Subagent completion silently lost** (#44925, open) — Three failure patterns with no retry or notification.
- **Steer mode not injecting mid-turn** (#48003, open) — Queued messages wait until turn ends.
- **Session write-lock timeouts block subagent lanes** (#86538, open) — Delivery/lifecycle failures.
- **Codex app-server turns go silent** (#85251, open) — Embedded run wedges for 360s default recovery.
- **Feishu HTTP proxy breaks tenant_access_token** (#48949, open) — Channel unusable behind proxy.
- **tools.elevated.enabled breaks exec routing** (#46786, open) — All exec calls routed to gateway host instead of sandbox.
- **OpenAI Codex errors leak into user chat** (#44910, open) — Unwrapped error messages in Telegram.
- **Discord leaks internal tool-call traces** (#44905, open) — Security and message loss.
- **Feishu read image tool loses media** (#41744, open) — Attachment dropped before delivery.
- **Multi-agent orchestration unstable** (#43367, open) — Config overwrites, session-lock failures.
- **Session hangs on compaction timeout** (#43661, open) — Duplicate message sends every ~10 min.

### P2 — Medium (regressions, behavior bugs)
- **Heartbeat/Cron stale timestamp** (#44993, open) — No fix PR.
- **Early abort response templates not populated** (#45314, open) — Template variables missing.
- **OPENCLAW_HOME nested directory** (#45765, open) — Regression for Linux users.
- **Control UI avatar not displaying** (#41201, open) — Broken image loading.
- **Telegram DMs still land in agent:main:main** (#41165, open) — Session pollution.
- **Cron jobs silently time out instead of fast-fail** (#45494, open) — Regression on API errors.
- **Write tool lacks append mode** (#40001, open) — Silent data loss in cron.
- **gh-issues prompt injection** (#45740, open) — Security: untrusted issue body injected into prompt.
- **Feishu monitor state memory leak** (#48183, closed stale) — Not fixed; closed due to staleness.

**Regression patterns**: Several bugs are marked as regressions (e.g., #44993, #41201, #45494, #45765, #38327), indicating recent changes may have introduced instability. The project should prioritize root-cause analysis of these regression waves.

---

## 6. Feature Requests & Roadmap Signals

Notable feature requests with high community engagement (reactions or prolonged discussion) that are likely to influence the next release:

| Issue | Title | Engagement | Likely Priority |
|-------|-------|------------|-----------------|
| #42475 | Per-agent cost budget enforcement at gateway | 12 comments, 👍1 | **High** — Prevents runaway spend, operator pain point |
| #45608 | Pre-reset agentic memory flush for `/new` | 10 comments, 👍4 | **High** — Preserves memory across sessions |
| #40418 | Automated session memory preservation & synthesis | 7 comments, 👍1 | **Medium** — Continuous learning across resets |
| #7707 | Memory trust tagging by source | 11 comments, 👍1 | **Medium** — Security against memory poisoning |
| #42840 | MathJax/LaTeX support in Control UI | 7 comments, 👍6 | **Medium** — High reaction count, niche but passionate |
| #45758 | YAML config file format support | 7 comments, 👍2 | **Low** — Nice-to-have, but major config rewrite |
| #40786 | `.gitignore`-like exclude patterns for backup CLI | 7 comments, 👍1 | **Low** — Backup ergonomics |
| #48874 | Multi-session architecture (shared LLM, isolated sessions) | 7 comments | **Low** — Major architecture change, RFC stage |
| #39979 | Path-scoped RWX permissions for exec and file tools | 7 comments | **Medium** — Security hardening |
| #45565 | Route gateway lifecycle warnings to dedicated channel | 7 comments, 👍1 | **Low** — Noise reduction |

**Prediction**: The next minor release (2026.7.x) will likely include cost budgets (#42475) and pre-reset memory flush (#45608), as both have clear user demand and relatively contained implementation scope. The multi-session architecture (#48874) is too large for immediate inclusion. Memory trust tagging (#7707) may see a prototype due to security concerns around prompt injection.

---

## 7. User Feedback Summary

Real user pain points expressed in the latest issues and PRs:

- **Silent data loss**: Several users report that subagent results, cron file writes, and shared workspace files disappear without warning (#44925, #40001, #43661). “No retry, no notification” is a recurring sentiment.
- **Memory leaks and OOM crashes**: The gateway memory leak (#91588) forces users into repeated restart cycles. “RSS grows from 350MB to 15.5GB” indicates fundamental resource management issues.
- **Session state confusion**: Users are frustrated by zombie subagents (#48573), stale timestamps (#44993), and main sessions that become unresponsive after subagent completion (#47975). “I never see any of our memory is managed in same way” (#43747) reflects inconsistency.
- **Channel routing problems**: Discord leak of internal tool calls (#44905) and Telegram DMs polluting the main session (#41165) break user trust. “These should never be visible to end-users.”
- **Configuration and upgrade pain**: `OPENCLAW_HOME` nesting (#45765), EBUSY on Windows update (#40540), and WebSocket URL clearing gateway token (#41545) indicate testing gaps on non-Linux platforms.
- **Performance degradation**: Control UI becoming progressively stuck (#45698) and iOS Safari layout regressions (#63644) show frontend stability concerns.
- **Positive feedback**: The new Telegram rich text and WhatsApp improvements in the latest releases are acknowledgment of user requests for better channel formatting. Some users express satisfaction via emoji reactions (👍 on feature requests).

---

## 8. Backlog Watch

Several important issues and PRs have been open for weeks or months without maintainer action or product decision. These require attention to avoid further user friction:

### Critical / High-severity issues lacking resolution
| Issue | Created | Days Open | Labels | Notes |
|-------|---------|-----------|--------|-------|
| #91588 — Gateway memory leak (P0) | 2026-06-09 | 5 | P0, diamond lobster | No fix PR; OOM kills daily |
| #7707 — Memory trust tagging | 2026-02-03 | 131 | P2, security | Needs product decision and security review |
| #42475 — Cost budget enforcement | 2026-03-10 | 96 | P2 | Needs maintainer review |
| #40001 — Write tool append mode | 2026-03-08 | 98 | P1 | Needs product decision; data loss risk |
| #40418 — Session memory preservation | 2026-03-09 | 97 | P2 | Needs security review |
| #40786 — Backup exclude patterns | 2026-03-09 | 97 | P2 | Needs product decision |
| #41744 — Feishu read image loss | 2026-03-10 | 96 | P1 | Needs maintainer review |
| #43367 — Multi-agent orchestration | 2026-03-11 | 95 | P1 | Needs product decision |
| #43661 — Session hangs on compaction | 2026-03-12 | 94 | P1 | Needs product decision |
| #44925 — Subagent completion lost | 2026-03-13 | 93 | P1 | Needs maintainer review |
| #45740 — gh-issues prompt injection | 2026-03-14 | 92 | P2, security | Needs security review |
| #46786 — Elevated exec routing break | 2026-03-15 | 91 | P1 | No fix PR yet |
| #48003 — Steer mode mid-turn

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs Hermes Agent

## 1. Ecosystem Overview
The personal AI assistant and agent open-source landscape is experiencing explosive growth, with two major reference implementations showing contrasting maturity profiles. OpenClaw, as the core reference project, operates at a massive scale with hundreds of daily contributions but grapples with critical stability and resource management issues. Hermes Agent, a younger but highly active project, recently crossed a major feature milestone (Web UI Gateway) and is rapidly absorbing community contributions, though it faces platform-specific bugs and memory reliability challenges. Both projects share a common trajectory toward richer channel integrations, automated memory management, and security hardening, but differ significantly in community size, release cadence, and technical debt burden.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| Issues updated (24h) | 500 | 50 |
| PRs updated (24h) | 500 | 50 |
| Open/Active Issues | ~400 | 47 |
| Merged/Closed PRs (today) | 213 | 2 (issues closed) |
| Open PRs | Not specified (many) | 48 |
| New releases (today) | 2 beta (v2026.6.7, v2026.6.8) | None |
| Health Score (qualitative) | **Moderate** – high activity but critical P0 memory leak, multiple P1 regressions, and significant backlog (90+ days open for key issues) | **Good** – active community, major feature delivered, but several P2 bugs and platform-specific stability gaps |

**Interpretation:** OpenClaw’s raw activity is an order of magnitude higher, but its health is strained by unresolved critical issues and a growing backlog. Hermes Agent shows balanced activity with fewer unresolved problems, though its issue count is much smaller.

## 3. OpenClaw’s Position

**Advantages vs. peers:**
- **Core reference status** – OpenClaw is the de facto standard for AI agent architecture; its releases define the ecosystem’s baseline.
- **Channel breadth** – Mature support for Telegram, WhatsApp, Slack, Mattermost, Feishu, Discord, and more. Hermes Agent covers fewer channels (Telegram, WeChat, Matrix, GitHub Copilot) but is catching up.
- **Release velocity** – Two beta releases in two days; Hermes Agent has none today. OpenClaw is iterating faster.
- **Community scale** – 500 daily contributors vs. 50 for Hermes; larger pool of potential fixes and features.

**Technical approach differences:**
- **Memory management** – OpenClaw uses a monolithic gateway with known memory leaks (RSS from 350MB to 15.5GB). Hermes Agent focuses on context compression and memory consolidation (auto-dream) but also suffers from retry loops and orphan sessions.
- **Orchestration** – OpenClaw has complex multi-agent orchestration (subagents, steer mode, session locking) but these are unstable. Hermes uses delegation models and simpler tool-calling bursts.
- **Configuration** – OpenClaw uses YAML and hot-reload; Hermes uses TOML and separate provider/API key handling, but both face configuration complexity complaints.

**Community size comparison:** OpenClaw’s issue/PR volume (500 each daily) dwarfs Hermes’ 50, indicating roughly 10x the contributor base. However, Hermes’ community is more focused and has higher per-issue engagement (e.g., 8 comments, 5 👍 for auto-dream).

## 4. Shared Technical Focus Areas

Both projects reveal common emerging requirements:

| Focus Area | OpenClaw | Hermes Agent | Common Need |
|------------|----------|--------------|-------------|
| **Memory / Context Management** | Memory leak (#91588), session state corruption, compaction hangs | Auto-dream (#10771), retry loops (#42405), orphan sessions | Reliable long-term memory, transparent failure handling |
| **Rich Channel Delivery** | Telegram rich text, WhatsApp media, Slack finals | Telegram Bot API 10.1 rich messages (#44428), WhatsApp voice notes | Support for modern messaging APIs (tables, LaTeX, collapsible) |
| **Security & Data Leakage** | Prompt injection (#45740), internal tool-call leaks (#44905) | Credential env var confusion, OAuth issues | Sandboxed execution, end-user message filtering |
| **Platform Stability (Windows/Non-UTF-8)** | `OPENCLAW_HOME` nesting, EBUSY on update | Windows GBK encoding crashes, Docker path issues | Cross-platform testing and locale-aware configuration |
| **Session Isolation** | Zombie subagents, session lock failures, thread routing | Context compression interruption, orphan sessions | Predictable session lifecycle and resource cleanup |
| **Cost / Rate Control** | Per-agent cost budgets (#42475) | Credit spike on resume (#45783) | Gateway-level spend limits and rate-limit transparency |

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary Target User** | Enterprise operators, multi-channel deployment teams | Individual developers and power users seeking local first-class experience |
| **Feature Focus** | Channel breadth, subagent orchestration, robust MCP/ACP protocol compliance | Desktop/TUI experience, Web UI, memory automation (auto-dream), emerging gateways (WeChat, Matrix) |
| **Technical Architecture** | Monolithic core with heavy memory footprint; separate gateway process; complex session locking | More modular; lighter memory profile; uses delegation and model routing; open PRs indicate occasional monolithic mega-PRs (#45925) |
| **Release Strategy** | Rapid beta releases (2 per day) with breaking changes not always documented | Slower, milestone-driven releases (e.g., Web UI Gateway closed after long demand) |
| **Key Differentiator** | **Scale and integration depth** – dozens of channels, hundreds of daily contributors | **User experience polish** – Web UI, auto-scroll, sound cues, planning consultant feature |
| **Security Posture** | Several known vulnerabilities (prompt injection, data leakage) with no immediate fixes | Fewer exposure points but OAuth/credential handling gaps |

## 6. Community Momentum & Maturity

- **Activity Tiers:**
  - **Tier 1 (Hyperactive / Fragile):** OpenClaw – very high code churn, but critical bugs persist; community is vocal about pain points. The project is maturing rapidly but accumulating technical debt.
  - **Tier 2 (Active / Stable-ish):** Hermes Agent – steady contributor growth, fewer blockers, major feature delivered. Shows signs of stabilization with higher per-issue resolution satisfaction.

- **Rapid Iteration:** OpenClaw is in a “beta firehose” mode, pushing multiple releases per day. This indicates a team or core maintainer prioritizing velocity over quality assurance.
- **Stabilizing:** Hermes Agent exhibits a slower, more deliberate cadence. Closure of #501 (Web UI) marks a stabilization milestone.

- **Community Health Indicators:**
  - OpenClaw: 10–19 comments per hot issue, but many “closed stale” without fix. Diamond-lobster labels attract engagement but don’t guarantee action.
  - Hermes Agent: Fewer but more targeted discussions, higher reaction counts relative to comments (e.g., 5 👍 on 8 comments for auto-dream). Suggests a community that votes with emojis but trusts maintainers to act.

## 7. Trend Signals

Cross-project community feedback reveals several industry trends valuable for AI agent developers:

1. **Rich Messaging as a Competitive Must-Have** – Both projects receive intense demand for Telegram Bot API 10.1 features (tables, LaTeX, collapsible). Developers expect agents to produce native-platform formatted output, not plain text.

2. **Memory Management Is the #1 Pain Point** – Silent data loss, context compression failures, retry loops, and orphan sessions are common across both projects. Users want transparent, predictable, and automated memory lifecycle management – ideally with user-inspectable “memory logs.”

3. **Security Hardening Is Urgent but Underresourced** – Prompt injection, internal tool-call leaks, and credential exposure are repeatedly reported. Only Hermes Agent shows active PRs addressing some issues; OpenClaw’s security backlog (e.g., #45740 open for 92 days) signals a gap. Expect community forks or commercial wrappers to prioritize security.

4. **Cross-Platform Compatibility Is Still Underserved** – Windows (especially non-UTF-8 locales like Chinese) and Docker environments cause disproportionate bugs. Developers targeting enterprise or non-Linux users must invest in CI testing across locales.

5. **Cost Management Will Drive Adoption** – Both projects have requests for per-agent cost budgets and credit spike warnings. As LLM usage scales, operators need granular financial controls – this is likely a near-term feature priority for all agent frameworks.

6. **Web UI vs. CLI/TUI: A False Dichotomy** – Hermes Agent’s Web UI Gateway closure (after 14 comments and long demand) shows that users want both. OpenClaw’s lack of a web UI is a growing disadvantage. Expect all serious agent projects to offer a web interface soon.

**Recommendation for developers:** Invest in robust memory management with transparent error reporting, prioritize Telegram rich message support, and ensure your agent works out-of-the-box on Windows (especially GBK locales). Consider integrating cost budgets as a first-class feature.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-14

## Today’s Overview

Hermes Agent shows **extremely high community activity** with 50 issues and 50 pull requests updated in the last 24 hours. Of those, 47 issues remain open/active and 48 PRs are still open, indicating a thriving stream of contributions and discussion. The most notable milestone is the closure of the **Web UI Gateway** feature request (#501), which was the project’s single most-commented issue and a long-requested capability. Meanwhile, the community is heavily engaged around Telegram Bot API 10.1 rich messages (two feature requests filed today), memory consolidation, and several stability bugs affecting desktop/TUI, Windows, and WeChat gateway users. No new releases were published today; the project continues to incorporate changes through ongoing PR merges.

## Releases

*None — no new releases today.*

## Project Progress

Two pull requests were merged or closed today. While the specific merged/closed PRs are not detailed in the top items, three issues were closed:

- **#501** [CLOSED] — **Web UI Gateway** — a major feature milestone, now implemented.
- **#44927** [CLOSED] — **Desktop auto-scroll opt-in** — closed as duplicate; related feature likely merged elsewhere.
- **#44942** [CLOSED] — **skill-update backup corruption bug** — fix merged; follow-up to earlier issues.

The closure of these items signals steady forward movement on both feature development and bug fixing. The large number of open PRs suggests a high merge cadence is expected soon.

## Community Hot Topics

| Issue/PR | Title | Comments | 👍 | Analysis |
|----------|-------|----------|----|----------|
| [`#501`](https://github.com/NousResearch/hermes-agent/issues/501) [CLOSED] | Web UI Gateway — Local Browser-Based Interface | 14 | 1 | **Most discussed item.** Community strongly advocated for a web UI alongside CLI and gateways. Now delivered. |
| [`#10771`](https://github.com/NousResearch/hermes-agent/issues/10771) [OPEN] | Automatic Memory Consolidation ("Auto Dream") | 8 | 5 | **High demand.** Users want periodic cleanup of stale dates and deduplication, inspired by Claude Code. |
| [`#44428`](https://github.com/NousResearch/hermes-agent/issues/44428) [OPEN] | Support Telegram Bot API 10.1 Rich Messages | 5 | 3 | **Urgent due to Telegram’s API change** – rich formatting (tables, LaTeX, collapsible) is now available but not yet integrated. Two related issues filed today (`#45864`, `#45854`). |
| [`#23975`](https://github.com/NousResearch/hermes-agent/issues/23975) [OPEN] | Context compression interrupted by gateway messages | 5 | 0 | **Core stability issue** – users hitting fallback markers when compression is interrupted, leading to degraded conversation quality. |
| [`#19344`](https://github.com/NousResearch/hermes-agent/issues/19344) [OPEN] | Planning Consultant — model-initiated frontier-model review | 4 | 0 | **Power-user feature request** – cost-efficient users want ability to invoke a stronger model via `/consult` for complex decisions. |

Underlying needs:  
- **Rich formatting parity** with Telegram’s latest API is a recurring theme (3 issues today).  
- **Memory management** (auto-dream, retry loops) is a top pain point.  
- **Context compression reliability** directly impacts user trust in long conversations.

## Bugs & Stability

### Critical / High Severity (P2)

| Issue | Description | Fix PR Present? |
|-------|-------------|-----------------|
| [`#23975`](https://github.com/NousResearch/hermes-agent/issues/23975) | Context compression interrupted by gateway messages → fallback summary marker | None identified yet |
| [`#44666`](https://github.com/NousResearch/hermes-agent/issues/44666) | `api_key_env` silently ignored in custom provider config → auth fails | None identified yet |
| [`#43586`](https://github.com/NousResearch/hermes-agent/issues/43586) | `key_env` ignored in model block → sends `no-key-required` → 401 | None identified yet |
| [`#31155`](https://github.com/NousResearch/hermes-agent/issues/31155) | `delegation.model` override ignored – subagents always inherit parent model | None identified yet |
| [`#42405`](https://github.com/NousResearch/hermes-agent/issues/42405) | Memory at capacity triggers zero-match retry loop → silent hang | None identified yet |
| [`#45783`](https://github.com/NousResearch/hermes-agent/issues/45783) | Tool call burst on session resume → massive credit spikes | None identified yet |
| [`#45813`](https://github.com/NousResearch/hermes-agent/issues/45813) | GitHub Copilot provider always returns HTTP 400 | None identified yet |
| [`#45674`](https://github.com/NousResearch/hermes-agent/issues/45674) | `hermes mcp list` crashes with `AttributeError` on string entries | None identified yet |
| [`#45792`](https://github.com/NousResearch/hermes-agent/issues/45792) | Docker container doesn’t understand its environment (config paths) | None identified yet |
| [`#45860`](https://github.com/NousResearch/hermes-agent/issues/45860) | Three Windows installation bugs (missing hermes.exe, etc.) | None identified yet |
| [`#45931`](https://github.com/NousResearch/hermes-agent/issues/45931) | WeChat gateway polling hangs + encoding issues on Chinese Windows | None identified yet |
| [`#45932`](https://github.com/NousResearch/hermes-agent/issues/45932) | Message gateway fails to start due to GBK decoding error | None identified yet |

### Medium / Low Severity (P3)

| Issue | Description |
|-------|-------------|
| [`#42366`](https://github.com/NousResearch/hermes-agent/issues/42366) | Desktop chat does not auto-scroll; input prompt disappears during output |
| [`#45834`](https://github.com/NousResearch/hermes-agent/issues/45834) | Duplicate patch files applied twice from global and profile patches directories |
| [`#45877`](https://github.com/NousResearch/hermes-agent/issues/45877) | Cron background review blocks read-only tools (read_file, search_files) |
| [`#45921`](https://github.com/NousResearch/hermes-agent/issues/45921) | Workspace directory selection button missing if too many directories |
| [`#45493`](https://github.com/NousResearch/hermes-agent/issues/45493) | Matrix: agent’s own thread-initial message lost from next-turn context |
| [`#42228`](https://github.com/NousResearch/hermes-agent/issues/42228) | Desktop compressed sessions appear in "No workspace" due to null `cwd` |

Several fix PRs are already in flight to address related issues. For example:

- [`#45938`](https://github.com/NousResearch/hermes-agent/pull/45938) — keeps overflow stream chunks editable during gateway responses.
- [`#45934`](https://github.com/NousResearch/hermes-agent/pull/45934) — refreshes Weixin poll session after transport failures.
- [`#45937`](https://github.com/NousResearch/hermes-agent/pull/45937) — fixes UTF-8 decoding in dashboard SPA for Windows GBK locales.
- [`#45936`](https://github.com/NousResearch/hermes-agent/pull/45936) — fixes desktop model switch rollback.
- [`#45681`](https://github.com/NousResearch/hermes-agent/pull/45681) — surfaces broken CA bundles with clear error messages.
- [`#45868`](https://github.com/NousResearch/hermes-agent/pull/45868) — distinguishes config references from mutations in skills.
- [`#24395`](https://github.com/NousResearch/hermes-agent/pull/24395) — fixes `hermes auth remove` suppression logic.
- [`#45800`](https://github.com/NousResearch/hermes-agent/pull/45800) — converts WhatsApp voice notes to Opus on the fly.

## Feature Requests & Roadmap Signals

**Likely to land in the next version:**

1. **Telegram Bot API 10.1 Rich Messages** — Three issues today (`#44428`, `#45864`, `#45854`) with strong community interest. A PR `#22532` (clarify prompts) and `#45800` (voice notes) touch Telegram infrastructure; a dedicated PR `#45933` makes rich replies opt-in, suggesting cautious rollout.
2. **Automatic Memory Consolidation (Auto Dream)** (`#10771`) — 5 👍, high engagement. A natural candidate for next minor release given community demand.
3. **Desktop auto-scroll toggle** (`#44927` closed as duplicate) — likely already in progress; TUI improvements PR `#42922` (OpenTUI) may include it.

**Emerging signals:**

- **Planning Consultant** (`#19344`) — model-initiated frontier-model review via `/consult` – could become a power-user plugin.
- **WhatsApp Cloud API message templates** (`#45935`) – from a real production use case.
- **Linear gateway AgentSession integration** (PR `#40739`) – shows enterprise interest.
- **Completion cues / desktop sound** (PR `#42480`) – polish feature for desktop UX.

## User Feedback Summary

**Satisfaction signals:**
- The Web UI Gateway closure addresses a major gap compared to competitors (Claude, ChatGPT).
- Multiple contributors are actively submitting PRs (43 PRs from AIalliAI bundled in a mega branch `#45925`), indicating a healthy open-source ecosystem.

**Common pain points expressed:**
- **Windows / non-UTF-8 locale issues** are a recurring theme (`#45931`, `#45932`, `#45860`) – multiple users on Chinese Windows report crashes.
- **Desktop TUI usability** – no auto-scroll, missing scrollbar, input prompt disappearing (`#42366`, `#45921`).
- **Memory and context compression reliability** – retry loops, orphan sessions, interrupted compression cause silent failures or degraded quality.
- **Configuration complexity** – `api_key_env` and `key_env` inconsistencies frustrate users trying to set up custom providers.
- **Docker environment** – mounting home directory does not match container paths (`#45792`).
- **Copilot and MCP integration** – broken OAuth and listing errors (`#45813`, `#45674`).

Overall, the community is active and constructive, but stability issues on Windows, Docker, and the memory subsystem are the most frequently voiced blockers.

## Backlog Watch

| Item | Type | Created | Last Updated | Why It Needs Attention |
|------|------|---------|--------------|------------------------|
| [`#10771`](https://github.com/NousResearch/hermes-agent/issues/10771) Auto Dream | Feature request | 2026-04-16 | 2026-06-13 | High demand (5 👍), 8 comments but no assignee or milestone. |
| [`#19245`](https://github.com/NousResearch/hermes-agent/issues/19245) session_search empty after crash – orphaned session JSON | Bug (P2) | 2026-05-03 | 2026-06-13 | Affects memory reliability; no fix PR yet. |
| [`#22417`](https://github.com/NousResearch/hermes-agent/issues/22417) ThinkCheck 3.0 showcase | Showcase | 2026-05-09 | 2026-06-14 | Community innovation but no maintainer response. |
| [`#23975`](https://github.com/NousResearch/hermes-agent/issues/23975) Context compression interrupted by gateway messages | Bug (P2) | 2026-05-11 | 2026-06-13 | Core stability issue; 5 comments, no PR. |
| [`#31155`](https://github.com/NousResearch/hermes-agent/issues/31155) delegation.model override ignored | Bug (P2) | 2026-05-23 | 2026-06-14 | Blocks multi-model workflows; no fix. |
| [`#33907`](https://github.com/NousResearch/hermes-agent/issues/33907) Orphan sessions from context compression | Bug (P2) | 2026-05-28 | 2026-06-13 | Related to #19245; data loss risk. |
| [`#17480`](https://github.com/NousResearch/hermes-agent/pull/17480) Codex usage credentials from auth fallbacks | PR (P2) | 2026-04-29 | 2026-06-14 | Open for 46 days; important for Codex integration. |
| [`#21774`](https://

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*