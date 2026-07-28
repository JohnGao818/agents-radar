# OpenClaw Ecosystem Digest 2026-07-28

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-28 02:07 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

## OpenClaw Project Digest — 2026-07-28

### 1. Today’s Overview
The OpenClaw project remains highly active, with **500 issues** and **500 pull requests** updated in the last 24 hours (242 open issues, 258 closed; 284 open PRs, 216 merged/closed). No new releases were published. Activity is concentrated on urgent stability fixes, major architectural refactors (e.g., transcript runtime removal, default agent removal), and a coordinated rename of “cron” to “Automations” across the product surface. Several P0 and P1 bugs – including a critical memory leak (RSS grows to 15.5 GB) and a SQLite migration blocker – are under active investigation, indicating a period of intense maintenance.

### 2. Releases
No new releases were published on 2026-07-28.

### 3. Project Progress
Out of **216 merged/closed PRs** today, several represent meaningful forward progress:

- **Matrix end-to-end encryption support** – [#114856](openclaw/openclaw PR #114856) (closed) adds encrypted messaging.
- **Overlapping process fix** – [#114845](openclaw/openclaw PR #114845) (closed) prevents scoped processes from surviving replacement.
- **UI theming improvement** – [#114812](openclaw/openclaw PR #114812) (closed) matches ClickClack discussion sidebars to host themes.
- **Active-memory config fix** – [#103614](openclaw/openclaw PR #103614) (closed) accepts `thinking: "max"` in plugin metadata.
- **Nextcloud Talk alias preservation** – [#113432](openclaw/openclaw PR #113432) (closed) fixes room aliases across upgrades.
- **Open PRs advancing features** – Notable open PRs include the “cron → Automations” rename stack ([#114841](openclaw/openclaw PR #114841), [#114852](openclaw/openclaw PR #114852), [#114853](openclaw/openclaw PR #114853), [#114854](openclaw/openclaw PR #114854), [#114855](openclaw/openclaw PR #114855)), and the removal of the stored default agent ([#114388](openclaw/openclaw PR #114388)), which will eliminate a class of ownership bugs.

### 4. Community Hot Topics
The most active discussions this cycle are centered on platform gaps, security, and session reliability:

- **[#75: Linux/Windows Clawdbot Apps](openclaw/openclaw Issue #75)** – 115 comments, 80 👍  
  Long-standing request for desktop apps beyond macOS/iOS/Android. Community clearly wants parity and a unified agent experience.
- **[#7707: Memory Trust Tagging by Source](openclaw/openclaw Issue #7707)** – 22 comments  
  Proposes trust-level metadata for memory entries to prevent poisoning attacks. Indicates growing concern over security of ingested content.
- **[#91588: Critical Gateway Memory Leak](openclaw/openclaw Issue #91588)** – 21 comments, P0  
  RSS grows from 350 MB to 15.5 GB over days, causing OOM crashes. Highly upvoted and actively discussed by users experiencing the same.
- **[#102020: Second Message Session Fail](openclaw/openclaw Issue #102020)** – 16 comments (closed)  
  A cross-channel bug where the first message works but the second fails. Resolution suggests a recent fix landed.
- **[#10659: Masked Secrets to Prevent API Key Leaks](openclaw/openclaw Issue #10659)** – 15 comments, 4 👍  
  Strong community support for a system that hides raw credentials from the agent, directly addressing prompt injection risk.

**Underlying needs**: Users demand cross-platform availability, stronger security sandboxing, and reliable session continuity. The volume of comments on memory and session bugs indicates operational stability is the top immediate concern.

### 5. Bugs & Stability
Multiple high-severity bugs were reported or updated today:

| Severity | Issue | Title | Fix PR? |
|----------|-------|-------|---------|
| **P0** | [#91588](openclaw/openclaw Issue #91588) | Gateway memory leak → OOM (RSS 350MB → 15.5GB) | No fix PR yet |
| **P0** | [#109867](openclaw/openclaw Issue #109867) (closed) | SQLite migration creates index before column, blocks startup | Closed, likely fixed |
| **P1** | [#113306](openclaw/openclaw Issue #113306) | SQLite snapshot restore lacks crash/identity guarantees | No fix PR |
| **P1** | [#113434](openclaw/openclaw Issue #113434) | Codex session.reset reuses retired session ID, RAM exhaustion | No fix PR |
| **P1** | [#113323](openclaw/openclaw Issue #113323) | LLM idle timeout aborts reasoning-token streaming | No fix PR |
| **P1** | [#87109](openclaw/openclaw Issue #87109) | Gateway heap grows to 1073MB+ at idle, cron silent failures | No fix PR |
| **P1** | [#85251](openclaw/openclaw Issue #85251) | Codex session wedges after `notification:turn/started` | No fix PR |
| **P1** | [#86519](openclaw/openclaw Issue #86519) | Duplicate replies on Telegram (regression from 5.20) | No fix PR |
| **P1** | [#94251](openclaw/openclaw Issue #94251) | Ollama streaming not consumed – chat sessions stuck | No fix PR |
| **P1** | [#87756](openclaw/openclaw Issue #87756) | Lobster workflow hangs on nested `/tools/invoke` | No fix PR |

Several fix PRs are in flight for related issues: e.g., [#112370](openclaw/openclaw PR #112370) addresses concurrent draft updates, [#111126](openclaw/openclaw PR #111126) fixes agent exit code on failures, and [#111955](openclaw/openclaw PR #111955) preserves Slack tables. However, the *Gatekeeper* memory leak (#91588) and the *Codex session* problems remain without an upstream fix, suggesting they require deeper architectural changes.

### 6. Feature Requests & Roadmap Signals
The issue tracker reveals a clear roadmap toward **security-first design** and **cross-platform expansion**:

- **Security & sandboxing** – [#10659 Masked Secrets](openclaw/openclaw Issue #10659), [#7722 Filesystem Sandboxing](openclaw/openclaw Issue #7722), [#6615 Exec-Approvals Denylist](openclaw/openclaw Issue #6615), [#12219 Skill Permission Manifest](openclaw/openclaw Issue #12219) all aim to restrict agent capabilities and prevent credential theft.
- **Multi-platform clients** – [#75 Linux/Windows Clawdbot Apps](openclaw/openclaw Issue #75) remains the top-voted feature (80 👍). Likely to be prioritized once session stability is addressed.
- **Observability & fallback** – [#9016 Expose OpenRouter Cost](openclaw/openclaw Issue #9016), [#9986 Context Length Fallback](openclaw/openclaw Issue #9986), and [#6599 Test Fallback Command](openclaw/openclaw Issue #6599) indicate a push for better cost transparency and reliability.
- **User experience** – [#9637 TUI Accessibility (disable emojis)](openclaw/openclaw Issue #9637), [#10118 TUI Multiline Input](openclaw/openclaw Issue #10118), [#7476 WhatsApp Stickers](openclaw/openclaw Issue #7476) show demand for refined interfaces.
- **Platform renames** – The active PR stack renaming “cron” to “Automations” (#114841–#114855) suggests a product identity consolidation likely to land in the next beta.

**Predictions**: One or more of the security features (masked secrets, filesystem sandboxing) are likely candidates for the next minor release given the high number of “needs-security-review” labels. The automations rename is almost certain for `2026.7.x`.

### 7. User Feedback Summary
Real user pain points surfaced in the last 24 hours:

- **“Second message fails”** – Users on both Signal and daemon channels report a consistent initialization conflict after the first turn (closed #102020). This undermines trust in basic chat.
- **“Agent repeats replies 2–10x on Telegram”** – A regression from the 5.20 update that persists (though reduced) in 5.22. Users explicitly call it a “regression.”
- **“Cron runs silent failure”** – Jobs that correctly produce no output are marked as errors ([#76159](openclaw/openclaw Issue #76159)), and memory pressure causes cron tasks to fail without notification ([#87109](openclaw/openclaw Issue #87109)). Frustration with opaque “error” statuses is high.
- **“Approval buttons become stale after restart”** – Telegram approval prompts show “unknown or expired approval id” after gateway restart ([#64664](openclaw/openclaw Issue #64664), closed). Users find this confusing and would prefer a persistent approval queue.
- **“Webhook sessions don’t support multi-turn”** – Despite documentation promising `sessionKey` for multi-turn, it is not implemented (#11665). Users who rely on webhook integrations are blocked.
- **“No way to remove paired gateway on iOS”** – The “Forget Gateway” button does nothing (#114082, fixed by #114083). A basic usability gap.

**Satisfaction indicators**: The high volume of closed bugs (258 in 24h) suggests that maintainers are responsive, and duplicate issues are being resolved. The existence of a “needs-product-decision” label indicates thoughtful triage. However, the shear number of open P0 and P1 bugs (many without fix PRs) points to a system under strain.

### 8. Backlog Watch
Several important issues and PRs have been waiting for maintainer attention for months:

- **[#75 – Linux/Windows Clawdbot Apps](openclaw/openclaw Issue #75)** – Opened Jan 2026, 115 comments. Despite high community interest, no assignee or milestone. The “clawsweeper:needs-product-decision” label suggests a strategic decision has not been made.
- **[#7707 – Memory Trust Tagging](openclaw/openclaw Issue #7707)** – Feb 2026, still in “needs-maintainer-review”. Security-critical but no progress.
- **[#10659 – Masked Secrets](openclaw/openclaw Issue #10659)** – Feb 2026, also “needs-maintainer-review” and “needs-product-decision”. Could become a liability if exploits continue.
- **[#6615 – Exec-Approvals Denylist](openclaw/openclaw Issue #6615)** – Feb 2026, 10 comments, 8 👍. Has an open linked PR (#? not listed) but still waiting.
- **[#8299 – Suppress Sub-Agent Announce](openclaw/openclaw Issue #8299)** – Feb 2026, 8 comments. Simpler feature that would improve multi-agent workflows.
- **[#114388 – Remove Stored Default Agent PR](openclaw/openclaw PR #114388)** – Opened today but touches many areas and is a breaking change. Needs careful maintainer review before merging.
- **[#82572 – Persist Followup Queues Across Gateway Restarts](openclaw/openclaw PR #82572)** – Open since May 2026 (2+ months). Addresses a regular complaint from users who lose messages after restarts. Yet to be merged.

These items represent gaps in maintainer bandwidth or unresolved product direction. If the team can triage the backlog of “needs-product-decision” issues, it would accelerate delivery of key features like multisession webhooks and credential protection.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent Open-Source Ecosystem
**Analysis Date:** 2026-07-28 | **Source:** Community Digests for OpenClaw & Hermes Agent

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is entering a **stability and hardening phase**, with both major projects—OpenClaw and Hermes Agent—operating at high velocity but facing similar growing pains around session reliability, cross-platform parity, and security sandboxing. Activity has shifted from pure feature acceleration toward urgent bug triage, with both projects collectively processing over **550 issues and 550 PRs** in a single day. The ecosystem is bifurcating: OpenClaw pursues a broad, multi-protocol platform strategy (Matrix, Nextcloud, Telegram, iOS), while Hermes Agent concentrates on desktop-native experiences (macOS, Windows, Linux) with deep LLM provider integrations. Both projects signal a maturing community that demands production-grade stability before further feature expansion.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|---|---|---|
| **Issues Updated (24h)** | 500 (242 open, 258 closed) | 50 (42 open, 8 closed) |
| **PRs Updated (24h)** | 500 (284 open, 216 merged/closed) | 50 (39 open, 7 merged/closed) |
| **New Releases Today** | None | None |
| **P0/P1 Bugs (open)** | 9 high-severity | 4 P1, several P2/P3 |
| **Fix PRs for High-Severity Bugs** | 0 for P0 memory leak; partial coverage | 2–3 fix PRs open |
| **Community Engagement (avg comments/top issue)** | ~115 (top issue) | ~13 (top issue) |
| **Health Signal** | **Under strain**: high bug volume, low fix coverage for critical issues | **Stable iteration**: lower volume, focused fixes, faster PR cycle |

**Summary**: OpenClaw operates at ~10× the raw volume but carries more unresolved critical bugs. Hermes Agent shows tighter triage discipline with fewer open issues and quicker PR-to-merge cycles.

---

## 3. OpenClaw's Position

**Advantages over peers:**
- **Broader protocol surface**: Matrix E2EE, Nextcloud Talk, Telegram, Slack, Signal—OpenClaw supports more chat platforms than Hermes Agent’s Discord/Slack/Feishu focus.
- **Larger community engagement**: 115 comments on the Linux/Windows desktop request (#75) vs. Hermes’ peak of 13 comments. OpenClaw’s user base is more vocal and organized.
- **Ambitious architecture refactors**: Active removal of stored default agents and transcript runtime indicates willingness to break backward compatibility for long-term correctness.
- **Security feature pipeline**: Memory trust tagging (#7707), masked secrets (#10659), filesystem sandboxing (#7722)—a more comprehensive security roadmap than Hermes Agent’s current scope.

**Technical approach differences:**
- OpenClaw uses a **gateway-based session architecture** (separate gateway process with session multiplexing), which is powerful but generates memory leak and session lifecycle bugs (P0 15.5GB RSS leak).
- Hermes Agent uses a **profile-scoped session model** with tighter integration into the desktop app’s state management.
- OpenClaw’s “cron → Automations” rename suggests a broader product identity shift; Hermes Agent maintains more conventional naming.

**Community size comparison:**
- OpenClaw: 500 issues updated/day, 500 PRs, major feature requests with 80+ upvotes, 115-comment threads.
- Hermes Agent: 50 issues, 50 PRs, peak comment count of 13. OpenClaw’s community is roughly **10× more active** by raw engagement metrics.

---

## 4. Shared Technical Focus Areas

Both projects are independently converging on the same pain points, validating these as ecosystem-wide requirements:

| Focus Area | OpenClaw Signals | Hermes Agent Signals |
|---|---|---|
| **Session Reliability** | #102020 second-message fail; #85251 session wedge after notification; #113306 session reset RAM exhaustion | #72971 wrong session after switch; #72016 missing activity watchdog; #72905 screenshot kills session |
| **Cross-Platform Desktop Parity** | #75 Linux/Windows Clawdbot apps (115 comments, top request) | #61396 macOS arm64 terminal failure; #40146 Windows IME; #72970 slow startup on Windows |
| **Security & Credential Protection** | #10659 masked secrets; #7707 memory trust tagging; #6615 exec-approvals denylist | #73037 guard profile secret scope; #73043 normalize MSYS paths; #67607 NeMo Relay observability |
| **Gateway/Platform-Specific Reliability** | #86519 duplicate Telegram replies; #113432 Nextcloud alias fixes; #64664 stale approval buttons | #26037 Feishu loss of context; #72975 interrupt silently no-ops; #73009 Slack event fallback logging |
| **Observability & Diagnostics** | #9016 expose OpenRouter cost; #9986 context length fallback | #67607 NeMo Relay metrics; #48689 `hermes doctor` false positives |
| **Session State Pollution** | Cron silent failures (#87109), overlapping processes (#114845) | Test sessions leaking into production state.db (#50681) |

**Takeaway**: The ecosystem is converging on a **“reliability core”** : session lifecycle management, credential sandboxing, and cross-platform compatibility are non-negotiable for agent adoption.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|---|---|---|
| **Target User** | Power users, self-hosters, multi-platform workflow builders | Desktop-first users, LLM power users, developer tooling consumers |
| **Primary Interface** | Chat apps (Telegram, Signal, Matrix, Nextcloud) + mobile | Desktop app (macOS/Windows) + CLI/TUI |
| **Architecture** | Gateway multiplexer + session pool; cron/automations engine | Profile-scoped sessions; deep LLM provider integration (OpenAI, Copilot subscriptions) |
| **Security Approach** | Layered permissions (masked secrets, sandbox, trust tagging) | Secret scope guards, verification nudges, no broad sandboxing yet |
| **Innovation Vector** | Platform breadth (Matrix E2EE, Nextcloud, 10+ adapters) | Desktop UX (pet overlays, wake-words, theme parity, cold-start perf) |
| **Risk Profile** | High architectural churn (transcript removal, default agent removal, cron rename); potential breakage | Incremental fixes; lower risk of regressions; focused, small PRs |
| **Observability** | Cost transparency, context length fallback (emerging) | NeMo Relay metrics, lifecycle events, shared-metrics (merged today) |

**Key insight**: OpenClaw is building a **universal agent platform** that routes through any chat interface; Hermes Agent is building a **personal desktop co-pilot** with a polished native app. These are complementary visions serving different adoption patterns.

---

## 6. Community Momentum & Maturity

**Activity Tiers:**

| Tier | Projects | Characteristics |
|---|---|---|
| **Rapidly Iterating (High Churn)** | OpenClaw | 500 issues/day, 500 PRs/day, large architectural refactors, many open P0/P1 bugs without fixes. Volatile but productive. |
| **Stabilizing (Focused Polish)** | Hermes Agent | 50 issues/day, 50 PRs/day, incremental fixes, lower bug severity. More predictable release cycle. |

**Maturity Indicators:**
- **OpenClaw**: 258 bugs closed in 24 hours shows high maintainer responsiveness; but the P0 memory leak (#91588) remains unfixed after community escalation (21 comments). The “needs-product-decision” label on 5+ major features suggests unresolved strategic direction.
- **Hermes Agent**: 7 PRs merged today vs. 0 for OpenClaw (in terms of feature/content, though OpenClaw merged 216). Hermes shows tighter merge discipline. The Dvorak keyboard fix (#46369) resolved by a community contributor signals healthy contributor onboarding.

**Prediction**: OpenClaw will likely ship a stabilization release within 2–3 weeks focusing on memory leaks and session lifecycle. Hermes Agent may ship a minor release next week with wake-word support and desktop perf improvements.

---

## 7. Trend Signals

**Key industry trends extracted from community feedback:**

1. **Agent trust is the #1 emerging concern.** Both projects see strong community demand for credential protection (masked secrets, trust tagging, sandboxed execution). This is not a niche request—it’s rising to P0/P1 priority.

2. **Session reliability is table stakes.** Users across both projects report first-message-succeeds/second-message-fails patterns. The ecosystem has not solved session lifecycle management for multi-turn interactions—this is a fundamental gap that undermines adoption for production use.

3. **Cross-platform parity is a competitive moat.** OpenClaw’s #1 feature request (115 comments) is desktop apps for Linux/Windows. Hermes Agent’s most active bugs are macOS/Windows-specific. The project that delivers unified desktop + mobile + chat experience will win broad deployment.

4. **Observability is becoming a feature, not a tool.** Exposing cost (OpenRouter), diagnostics (`hermes doctor`), and metrics (NeMo Relay) to end users signals a shift from “agent as black box” to “agent as transparent service.” Users want to understand why the agent behaved a certain way.

5. **Security-by-design is being demanded, not optional.** Prompt injection via memory (#7707), credential leaks through API keys (#10659), and sandbox escapes are active community concerns. The projects that implement defense-in-depth early will have a structural advantage.

**Value for AI agent developers:**
- Build session recovery into agent frameworks from day one—do not treat sessions as ephemeral.
- Invest in credential sandboxing before feature expansion; the community is already penalizing projects that leak credentials.
- Prioritize cross-platform testing (Windows IME, macOS permissions, Linux terminal compatibility) as a differentiator.
- Expose agent decision transparency (cost, context usage, lifecycle events) as a user-facing feature—users are demanding it.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-07-28

## 1. Today's Overview

Hermes Agent saw very high activity over the past 24 hours, with **50 issues** and **50 pull requests** updated across the project. Of those, 42 issues remain open and 39 PRs are still in progress. No new releases were cut today, but the community and core team are clearly focused on stability and polish: the majority of updates touch the desktop app, session state, gateway message delivery, and cross-platform compatibility (macOS, Windows, CJK locales). A mix of P1/P2 bug reports and user-visible feature PRs (wake‑word support, pet overlay animation, desktop performance fixes) indicates a project balancing rapid iteration with increasing production‑grade demands.

## 2. Releases

*No new releases today.*

## 3. Project Progress

Seven pull requests were **merged or closed** today (6 merged, 1 withdrawn):

- **#73038** – fix(desktop): show a check on the active theme and color mode in ⌘K  
  ✅ Restores the active‑row indicator in the command palette theme picker.

- **#73040** – feat(desktop): right‑click parity for cron, webhooks, and profile rows  
  ✅ Follow‑up to #72987, adding right‑click context menus to overlay panels and sidebar cron rows.

- **#73041** – fix(desktop): keep the active tab and the “+” in view when the tab strip scrolls  
  ✅ Prevents new session tabs from appearing off‑screen.

- **#73024** – perf(desktop): cut renderer cold start by keeping shiki/mermaid off the boot path  
  ✅ Reduces cold‑start time by deferring 22 MB of code (syntax highlighting, diagram rendering) that was inlined into the entry chunk.

- **#73009** – fix(slack): never lose an inbound event without a trace  
  ✅ Adds a log‑everywhere fallback so valid `@mention` events are always recorded, even if the router silently drops them.

- **#67607** – feat(observability): integrate NeMo Relay runtime and shared metrics  
  ✅ Large feature merge: Hermes now ships lifecycle events through a profile‑scoped Relay binding, with a local exporter and the first shared‑metrics vertical slice.

- **#72919** – Withdrawn by author (type/security, tool/skills).

**Notable open PRs advancing today** (still in review):  
- **#73008** – feat(discord): add durable thread run lifecycle  
- **#73043** – fix(gateway): normalize MSYS drive paths in MEDIA tag parsing on Windows  
- **#73037** – fix(cron): guard profile secret scope with multiplex check  
- **#73039** – fix(agent): persist before emitting verify‑on‑stop / pre_verify nudge answers  
- **#73035** – fix(desktop): let a typed message answer past a clarify prompt  
- **#73033** – fix(desktop): stop GlyphSpinner React churn  
- **#73034** – fix(gateway): recognise JSON NO_REPLY envelope in response filters  
- **#73036** – fix(compression): preserve history across bounded passes

## 4. Community Hot Topics

The most active discussions this week (by comment count) reveal three core pain points:

| Issue | Comments | Summary |
|-------|----------|---------|
| [#67600](https://github.com/NousResearch/hermes-agent/issues/67600) | 13 | **Desktop session sidebar empty for `default` profile only.** Named profiles work fine. Backend confirms rows are served. Users are blocked from using the default profile. |
| [#48689](https://github.com/NousResearch/hermes-agent/issues/48689) | 6 | **`hermes doctor` reports stale npm vulnerability and false‑positive Gemini API key error.** False alarms erode trust in the diagnostics tool. |
| [#61396](https://github.com/NousResearch/hermes-agent/issues/61396) | 5 | **macOS arm64 terminal fails to start** because `node‑pty`’s spawn‑helper loses the execute bit in the app bundle. Affects all Desktop users on Apple Silicon. |
| [#40146](https://github.com/NousResearch/hermes-agent/issues/40146) | 4 | **Desktop send button doesn’t switch from voice when typing Chinese (IME composition).** CJK users are forced to commit text before sending. |
| [#26037](https://github.com/NousResearch/hermes-agent/issues/26037) | 4 | **Feishu gateway loses parent context when replying to image messages.** `_fetch_message_text()` returns empty for non‑text content. |
| [#68339](https://github.com/NousResearch/hermes-agent/issues/68339) | 4 | **Mixed‑batch tool execution interacts with `TOOL_USE_ENFORCEMENT_GUIDANCE`**, causing early‑session front‑loading of tool calls. Community members report observable behavior shifts after commit `348e9912f`. |

**Underlying needs**: Users depend on the default profile for first‑run experience; diagnostic false‑positives reduce confidence; platform‑specific issues (macOS, Windows IME, CJK) highlight demand for locale and OS parity.

## 5. Bugs & Stability

**High‑severity (P1) bugs reported today:**

- [#72975](https://github.com/NousResearch/hermes-agent/issues/72975) **Interrupt/abort silently no‑ops when `force_close_tcp_sockets()` returns 0** (OpenAI client). The request stays alive for minutes. **No fix PR yet.**  
- [#72016](https://github.com/NousResearch/hermes-agent/issues/72016) **Gateway sessions lack activity watchdog** – agent loop stalls silently. **Closed as fixed** by a previous commit.

**P2 bugs with ongoing investigation:**

- [#72971](https://github.com/NousResearch/hermes-agent/issues/72971) **Desktop GUI: `prompt.submit` sends to wrong session after session switch while model response is slow** – messages appear in the wrong conversation. No fix PR yet.  
- [#72905](https://github.com/NousResearch/hermes-agent/issues/72905) **Screenshot in tool message permanently kills a session** – HTTP 422 is never classified; two provider signatures missing from `_MULTIMODAL_TOOL_CONTENT_PATTERNS`. OpenRouter sessions become permanently broken. No fix PR yet.  
- [#68339](https://github.com/NousResearch/hermes-agent/issues/68339) Mixed‑batch tool execution behavior shift (still open, needs‑repro & needs‑decision).  
- [#67629](https://github.com/NousResearch/hermes-agent/issues/67629) **`search_files` fails on absolute Windows paths** due to MSYS path rewriting.  
- [#50681](https://github.com/NousResearch/hermes-agent/issues/50681) **pytest sessions leak into production state.db** – 187 test‑created fake sessions polluted the real database.  

**P3 bugs (many with fixes in progress):**

- [#61396](https://github.com/NousResearch/hermes-agent/issues/61396) macOS terminal spawn failure – **a fix PR (#73038) is open** but the issue remains open.  
- [#40146](https://github.com/NousResearch/hermes-agent/issues/40146) Windows IME composition – no fix PR yet.  
- [#70719](https://github.com/NousResearch/hermes-agent/issues/70719) File‑mutation verifier footer fires on arg‑missing patch calls (noisy overclaim).  
- [#69107](https://github.com/NousResearch/hermes-agent/issues/69107) `prompt.submit` truncate rejects valid ordinals when TUI and web client collide.

**Today’s P2 fix PRs** that address related stability issues:  
- [#73039](https://github.com/NousResearch/hermes-agent/pull/73039) – persist messages before emitting verify‑on‑stop answers.  
- [#73035](https://github.com/NousResearch/hermes-agent/pull/73035) – let typed messages answer past a clarify prompt.  
- [#73034](https://github.com/NousResearch/hermes-agent/pull/73034) – recognise JSON NO_REPLY envelope.  
- [#73036](https://github.com/NousResearch/hermes-agent/pull/73036) – preserve history across bounded compression passes.

## 6. Feature Requests & Roadmap Signals

Several user‑requested features indicate the project’s direction:

| Request | Description | Likely next‑version candidate |
|---------|-------------|-------------------------------|
| [#65735](https://github.com/NousResearch/hermes-agent/issues/65735) | **Support multiple OpenAI/Copilot subscriptions** – allow switching when rate‑limited. | High user demand; implementation already on main (#65735 closed). |
| [#70509](https://github.com/NousResearch/hermes-agent/pull/70509) | **On‑device wake words** with open‑vocabulary phrases and multi‑profile voice routing (CLI/TUI/Desktop). | Large feature; PR open for 4 days, actively reviewed. |
| [#67325](https://github.com/NousResearch/hermes-agent/issues/67325) | **Detect generated skill documentation drift** without CI mutation. | Needed for project hygiene; may land in next minor release. |
| [#29483](https://github.com/NousResearch/hermes-agent/issues/29483) | **Render Slack progress drafts as plan cards** – replace repetitive status lines with compact, scannable cards. | Community +1s; could be a mid‑term goal. |
| [#33489](https://github.com/NousResearch/hermes-agent/issues/33489) | **BlueBubbles adapter: group chat filtering** (`IGNORE_GROUP_CHATS` or `ALLOWED_CHATS`). | Awaiting decision; niche but valuable for iMessage users. |
| [#72986](https://github.com/NousResearch/hermes-agent/pull/72986) | **Desktop pet overlay: drag‑run animation and floor roaming**. | Polish feature; merged today? (PR open). |
| [#73008](https://github.com/NousResearch/hermes-agent/pull/73008) | **Discord durable thread run lifecycle** – run‑started marker, explicit terminal status. | Important for Discord reliability; high likelihood of merging. |

**Prediction**: The next version will likely include the NeMo Relay observability merge (#67607), wake‑word support (#70509), and the collection of desktop fixes (theme indicator, tab scrolling, cold‑start perf). The multiple‑subscription feature for OpenAI (#65735) is already closed as “implemented‑on‑main”.

## 7. User Feedback Summary

**Pain points voiced by the community:**

- **Desktop “default” profile broken** – multiple users report the session sidebar is completely empty after an update. Backend is healthy but frontend fails.  
- **`hermes doctor` false alerts** – stale npm vulnerability warnings and invalid Gemini API key errors erode trust. Users want a silent “all clear” when no real issues exist.  
- **Keyboard layout discrimination** – Dvorak users cannot use keyboard shortcuts (#46369, closed today with a fix that respects `event.key`).  
- **CJK input on Windows** – IME composition is unsupported, forcing Chinese, Japanese, and Korean users to commit text before seeing the send button.  
- **Windows file paths** – `search_files` and `MEDIA:` tags break under MSYS/Git Bash, requiring workarounds.  
- **Session state pollution** – test sessions leaking into production database is a recurring complaint (#50681).  
- **Slow startup on Windows** – optional skill provenance backfill adds seconds to CLI startup (#72970, closed as duplicate but root cause acknowledged).

**Positive signals**: Users are filing detailed, well‑reproduced bug reports and contributing fix PRs (e.g., Dvorak layout fix, candidate fixes for MSYS paths, Slack event logging). The community engagement is healthy, with

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*