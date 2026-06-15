# OpenClaw Ecosystem Digest 2026-06-15

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-15 03:51 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-06-15

## 1. Today's Overview
OpenClaw activity remains intense, with 500 issues and 500 PRs updated in the last 24 hours (427 open / 73 closed issues; 421 open / 79 merged/closed PRs). A new beta release (`v2026.6.8-beta.1`) landed today, focusing on Telegram and WhatsApp delivery robustness. However, the project continues to face a wave of P1 regressions—duplicate message delivery, session takeover errors, silent truncation, and cron reliability issues—that have drawn sustained community attention. Despite high churn, the maintainer team is actively reviewing PRs and closing both bugs and feature integrations.

## 2. Releases
**New release: [v2026.6.8-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.8-beta.1)**  
Highlights:  
- **Telegram**: structured rich text (tables, lists, expandable blockquotes), prompt-preserving CLI backend delivery, safer rich-media boundaries.  
- **WhatsApp**: richer channel delivery with fewer brittle edge cases.  
- Retired native draft migration for Telegram.

No explicit breaking changes or migration notes are listed; existing agents are expected to upgrade without manual intervention.

## 3. Project Progress
In the last 24 hours, 79 PRs were merged or closed. Notable among the top-30 most-commented PRs:

- **Merged/closed PRs visible in the snapshot**:  
  - [#93148](https://github.com/openclaw/openclaw/pull/93148) – `fix(telegram): record every sent message in the SQLite db` (restores sent-message persistence).  
  - [#93147](https://github.com/openclaw/openclaw/pull/93147) – `feat(cron): add edit dry-run preview` (clean replacement for earlier attempts).  
  - [#93135](https://github.com/openclaw/openclaw/pull/93135) – `fix(cron): fail closed on unavailable-tool self-debug in cron delivery` (prevents misleading “I can’t use the tool” responses).

- **Open PRs nearing completion** (automerge armed or maintainer-reviewed):  
  - [#92318](https://github.com/openclaw/openclaw/pull/92318) – `fix(cron): require explicit message target proof` (strengthens cron delivery accounting).  
  - [#87298](https://github.com/openclaw/openclaw/pull/87298) – `test: add temp directory helper guidance` (cleanup sufficiency scanner replacement).  
  - [#93109](https://github.com/openclaw/openclaw/pull/93109) – `test(qa): embed profile scorecard evidence` (improves test transparency).

- **Feature advances**:  
  - [#93125](https://github.com/openclaw/openclaw/pull/93125) – `feat(compaction): add compaction.fallbacks: string[]` (ordered model fallback chain for summarization).  
  - [#88750](https://github.com/openclaw/openclaw/pull/88750) – `feat(context-engine): pass runtime settings into lifecycle` (Codex/Forge integration).

The release itself represents the most significant merged feature bundle.

## 4. Community Hot Topics
The most active discussions (by comment count) reveal three core pain points:

| Issue | Title | Comments | 👍 | Underlying Need |
|-------|-------|----------|---|-----------------|
| [#85888](https://github.com/openclaw/openclaw/issues/85888) | Cron jobs consistently fail with MiniMax 503 overload during early morning | 12 | 1 | Better cron scheduling resilience / rate-limit handling |
| [#84516](https://github.com/openclaw/openclaw/issues/84516) | Codex app-server: long agent replies silently truncated at ~1000-1100 chars | 11 | 2 | Message delivery integrity / no silent data loss |
| [#86996](https://github.com/openclaw/openclaw/issues/86996) | Active Memory + Codex app-server causes long latency, hook timeouts, startup aborts | 9 | 1 | Performance under complex feature combinations |
| [#86519](https://github.com/openclaw/openclaw/issues/86519) | Agent repeats identical replies 2-10x on Telegram after 5.20 update | 9 | 1 | Regression user trust |
| [#86508](https://github.com/openclaw/openclaw/issues/86508) | EmbeddedAttemptSessionTakeoverError during Discord runs | 9 | 4 | Session concurrency safety |
| [#85103](https://github.com/openclaw/openclaw/issues/85103) | Model fallback chain not triggered on provider-wide quota exhaustion | 9 | 1 | Robust failover |

**Reactions**: The highest 👍 count appears on [#91016](https://github.com/openclaw/openclaw/issues/91016) (5 👍) – a Chinese user reporting DeepSeek prompt cache failure costing ~$6/hour, plus [#86508](https://github.com/openclaw/openclaw/issues/86508) (4 👍). Community is most vocal about session takeover errors and cache inefficiency.

**Underlying need**: Users expect deterministic, lossless message delivery regardless of channel, time of day, or provider outages. The recurring `EmbeddedAttemptSessionTakeoverError` and silent truncation patterns indicate a systemic session-state / locking weakness.

## 5. Bugs & Stability
**Critical regressions (P1, many cross-referenced)**:

- **Duplicate replies** – [#86519](https://github.com/openclaw/openclaw/issues/86519), [#88951](https://github.com/openclaw/openclaw/issues/88951), [#87068](https://github.com/openclaw/openclaw/issues/87068) (Telegram, WhatsApp, general). Duplicates range 2–10× per user message. Workaround exists (rollback to 5.12), but no fix PR in top-30.
- **Session takeover errors** – [#86508](https://github.com/openclaw/openclaw/issues/86508), [#85103](https://github.com/openclaw/openclaw/issues/85103), [#84569](https://github.com/openclaw/openclaw/issues/84569), [#83251](https://github.com/openclaw/openclaw/issues/83251), [#86845](https://github.com/openclaw/openclaw/issues/86845). The `EmbeddedAttemptSessionTakeoverError` cluster suggests a race condition in the embedded prompt lock.
- **Silent truncation / message loss** – [#84516](https://github.com/openclaw/openclaw/issues/84516) (Codex truncation), [#86047](https://github.com/openclaw/openclaw/issues/86047) (interrupted turns), [#83184](https://github.com/openclaw/openclaw/issues/83184) (heartbeat delivery stuck).
- **Cron reliability** – [#85888](https://github.com/openclaw/openclaw/issues/85888) (MiniMax overload), [#45494](https://github.com/openclaw/openclaw/issues/45494) (silent timeouts on API errors), [#86861](https://github.com/openclaw/openclaw/issues/86861) (rate-limit regression).
- **Memory leak** – [#87109](https://github.com/openclaw/openclaw/issues/87109) (heap grows to 1GB+ on macOS, cron jobs fail silently).
- **Auth/OAuth** – [#86215](https://github.com/openclaw/openclaw/issues/86215) (Codex OAuth refresh wedges), [#77467](https://github.com/openclaw/openclaw/issues/77467) (MiniMax refresh not implemented).

**New bugs today** (created 2026-06-15 in the PR list, likely many more not in top-50): [#93152](https://github.com/openclaw/openclaw/issues/93152) (ancestor context file walk security), [#93151](https://github.com/openclaw/openclaw/issues/93151) (GBK encoding on Chinese Windows). Both have fix PRs.

**Existing fix PRs**:  
- [#93110](https://github.com/openclaw/openclaw/pull/93110) addresses [#92460](https://github.com/openclaw/openclaw/issues/92460) – cron delivery route lease store.  
- [#93127](https://github.com/openclaw/openclaw/pull/93127) – apply factory denylist to `sessions_yield` tool.

**Overall stability**: The project is in a “regression fire” state post-5.20, but the maintainer team is actively reviewing and merging hotfixes.

## 6. Feature Requests & Roadmap Signals
**User-requested features with active discussion**:

- **Gateway-lite mode** – [#86881](https://github.com/openclaw/openclaw/issues/86881) (7 comments): an optional mode without AI harness for pure channel gateways and cron scheduling. High potential for next release if maintainer priority aligns.
- **Stream mode slash command** – [#74077](https://github.com/openclaw/openclaw/issues/74077) (5 comments, stale but updated today): per-chat `/stream` control without restarting gateway. Moderate likelihood given UX improvement.
- **Heading-aware memory chunking** – [#44395](https://github.com/openclaw/openclaw/issues/44395) (5 comments, opened 2026-03-12): semantic chunking for memory search. Still open with no fix PR – may be on the back burner.
- **Image generation usage metadata** – [#85461](https://github.com/openclaw/openclaw/issues/85461) (6 comments): capture cost/usage from image providers. Lightweight feature with existing PRs in other areas.

**Roadmap predictions**: The v2026.6.8-beta.1 release already includes major Telegram/WhatsApp improvements. The next minor release (2026.6.x stable) will likely prioritize cron delivery hardening (multiple PRs in progress) and compaction fallbacks (PR #93125). The Gateway-lite mode may appear as an opt-in feature if demand rises.

## 7. User Feedback Summary
**Pain points** (extracted from issue comments and reactions):

- “Agent replies duplicated 2–10 times on Telegram after 5.20” – **dissatisfaction** with recent regression; some users rolled back to 5.12.
- “Session takeover error: session file changed while embedded prompt lock was released” – **frustration** with concurrency bugs; the error is cryptic and `doctor --fix` does not help.
- “Cron jobs fail silently during MiniMax overload” – **reliability gap**; users rely on cron for business processes.
- “DeepSeek prompt cache broken after upgrade, cost spikes ~$6/hour” – **financial impact**; the bug (#91016) has high 👍 but no fix yet.
- “Memory leak to 1GB+, cron jobs fail under pressure” – **resource stability** concern on macOS.

**Satisfaction signals**:
- Positive reactions to the new beta release (Telegram formatting, WhatsApp delivery) – “richer and less brittle”.
- Multiple PRs with “automerge armed” and “ready for maintainer look” indicate efficient workflow and user confidence in the team.

**Use cases**: AI agents in Telegram/Discord/WhatsApp groups, cron-scheduled background tasks, voice-call agents, and multi-provider fallback chains. These are core to OpenClaw’s value proposition.

## 8. Backlog Watch
**Issues needing maintainer attention** (long open, no recent activity, or awaiting product decision):

| Issue | Created | Comments | Impact | Why it’s stuck |
|-------|---------|----------|--------|----------------|
| [#45494](https://github.com/openclaw/openclaw/issues/45494) | 2026-03-13 | 8 | Cron API error handling | Needs product decision; fix shape unclear |
| [#74077](https://github.com/openclaw/openclaw/issues/74077) | 2026-04-29 | 5 | Stream per-session | Needs maintainer review and product decision |
| [#44395](https://github.com/openclaw/openclaw/issues/44395) | 2026-03-12 | 5 | Memory chunking | No PR; needs product decision |
| [#77467](https://github.com/openclaw/openclaw/issues/77467) | 2026-05-04 | 5 | MiniMax OAuth refresh | Needs maintainer review; source repro available |
| [#83184](https://github.com/openclaw/openclaw/issues/83184) | 2026-05-17 | 8 | Heartbeat stuck delivery | Linked PR open; awaiting merge |

**Old PRs waiting for review** (marked “waiting on author” or “needs proof”):

- [#45901](https://github.com/openclaw/openclaw/pull/45901) (2026-03-14) – Session directory permissions.
- [#45465](https://github.com/openclaw/openclaw/pull/45465) (2026-03-13) – Cron lifecycle hooks.
- [#41067](https://github.com/openclaw/openclaw/pull/41067) (2026-03-09) – Dashboard chat recovery.
- [#39102](https://github.com/openclaw/openclaw/pull/39102) (2026-03-07) – Per-agent A2A allowlist.

These PRs address security, reliability, and feature completeness but have not progressed for months. They represent missed opportunities for the project to reduce technical debt.

---

*Data snapshot taken from [github.com/openclaw/openclaw](https://github.com/openclaw/openclaw) on 2026-06-15. Issues and PRs listed are the top items by comment count in the last 24h; total activity includes 500 updates in each category.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs Hermes Agent

## 1. Ecosystem Overview

The open-source personal AI agent ecosystem is maturing rapidly, with two major reference implementations—OpenClaw and Hermes Agent—driving divergent architectural philosophies while converging on shared reliability challenges. Both projects have passed the experimental phase and are now grappling with production-scale issues: session concurrency, multi-channel delivery guarantees, provider fallback chains, and credential security. Community activity remains intense across both codebases, indicating strong developer investment but also growing pains from rapid feature expansion outpacing stability hardening. The ecosystem is bifurcating between a “gateway-first” approach (OpenClaw) focused on rich channel delivery and a “security-first” approach (Hermes) prioritizing sandboxed execution and provider transparency.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues (24h)** | 500 updated (427 open / 73 closed) | 100 updated (84 open / 16 closed) |
| **PRs (24h)** | 500 updated (421 open / 79 merged/closed) | ~50 updated (8 merged/closed) |
| **Release Status** | Beta v2026.6.8-beta.1 (today) | No release in last 24h |
| **Critical Bugs** | 7+ P1 regressions (duplicates, session takeover, silent truncation, cron failures, memory leak) | 3 P1 bugs (cron orphan, Matrix E2EE exhaustion, security exfiltration) |
| **Health Score** | 5/10 — Regression fire state; high throughput but stability compromised | 6/10 — Responsive but has critical cron data loss and security gaps |
| **Maintainer Responsiveness** | High — hotfixes merged same day; active review queue | High — security fixes open within hours; closed 16 issues today |

**Health Score Note**: OpenClaw’s raw throughput is 5× Hermes, but the proportion of regressions to fixes is higher. Hermes shows fewer regressions but has a more concerning unresolved P1 cron orphan issue (21 days without maintainer reply).

## 3. OpenClaw's Position

**Advantages**:
- **Channel delivery maturity**: Beta release today delivers structured rich text (tables, lists, blockquotes) to Telegram and richer WhatsApp formatting—features Hermes lacks natively.
- **Community scale**: 5× the daily issue/PR churn of Hermes, indicating a larger user base and more diverse ecosystem integrations (cron, compaction fallbacks, context engine).
- **CI/merging velocity**: 79 PRs merged/closed in 24 hours vs 8 for Hermes. The project processes contributions at industrial scale.
- **Feature depth**: Compaction fallbacks (#93125), context engine runtime settings (#88750), and gateway-lite mode (#86881) show architectural ambition beyond channel translation.

**Technical approach differences**:
- OpenClaw uses an **embedded prompt lock** system that has revealed systemic race conditions (the `EmbeddedAttemptSessionTakeoverError` cluster). This is a high-risk design for concurrency.
- Hermes uses a **profile-based gateway architecture** with s6 process supervision and separate log/run directories per profile, which isolates failures but introduces lifecycle bugs (doomed resident gateways, root-owned log parents).
- OpenClaw prioritizes **channel richness** over isolation; Hermes prioritizes **cross-platform security** (sandboxed `read_file`, Termux support, macOS temp paths).

**Community size comparison**: OpenClaw’s 500 daily updates vs Hermes’ 100 suggests roughly 5× the contributor base. However, OpenClaw’s higher regression rate implies either more aggressive feature shipping or less rigorous pre-merge testing.

## 4. Shared Technical Focus Areas

The following requirements emerge independently across both projects, indicating ecosystem-wide priorities:

| Requirement | OpenClaw | Hermes Agent |
|-------------|----------|--------------|
| **Cron delivery hardening** | #85888 (MiniMax overload), #93110 (route lease fix), #92318 (explicit target proof) | #32091 (silent orphan cron jobs, P1, open 21 days) |
| **Silent message truncation** | #84516 (Codex 1000-1100 char truncation), #86047 (interrupted turns) | #7237 (output length limit, closed today after 46 comments) |
| **Session concurrency / takeover safety** | #86508 (EmbeddedAttemptSessionTakeoverError), 5+ cross-referenced issues | #46303 (concurrent session cross-contamination) |
| **Provider fallback chain reliability** | #85103 (fallback not triggered on quota exhaustion), #93125 (compaction fallbacks) | #44560 (model.options blocks on sync HTTP calls → WebSocket timeout) |
| **OAuth / credential refresh** | #86215 (Codex OAuth refresh wedges), #77467 (MiniMax refresh unimplemented) | #46427 (GH_TOKEN leak prevention), #46411/#46413 (credential exfiltration from sibling profiles) |
| **Memory/prompt context safety** | Not explicitly an issue | #31584 (memory injection as attack vector; treat as background context) |

**Underlying pattern**: Both projects struggle with **state consistency across asynchronous boundaries**—cron triggers, session handoffs, provider API failures, and OAuth token lifecycles. The community demands deterministic, lossless behavior under all failure modes.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary focus** | Multi-channel delivery (Telegram, WhatsApp, Discord) with rich formatting | Security, cross-platform desktop, and provider transparency |
| **Target user** | Power users running AI agents in group chats; cron automation for business workflows | Desktop-first users; security-conscious developers; multi-provider setups |
| **Architecture** | Embedded prompt lock + SQLite sent-message persistence; monolithic agent runtime | Profile-based gateway isolation; s6 process supervision; TUI + desktop apps |
| **Key differentiator** | **Channel richness**: Tables, blockquotes, expandable lists on Telegram | **Security depth**: `read_file` guards against credential exfiltration, Termux TIRITH support, macOS temp path awareness |
| **Weakness** | Race conditions in prompt lock cause session takeover errors; duplicate replies erode trust | Cron orphan data loss; Matrix E2EE exhaustion; Intel Macs unsupported |
| **Community tone** | “Regression fire” — high churn, vocal about financial impact (DeepSeek cache bug costing $6/hr) | “Responsive but gaps” — privacy backlash over Parallel.ai routing; long-unanswered P1 |
| **Feature roadmap signal** | Gateway-lite mode, compaction fallbacks, heading-aware memory chunking | Claude subscription OAuth, Kanban epoch workflows, unified appearance system |

**Strategic implication**: OpenClaw is betting that **delivery reliability** is the moat; Hermes is betting that **security and provider neutrality** will win enterprise/security-sensitive users. Their weaknesses are mirror images: OpenClaw’s concurrency bugs vs Hermes’ silent data loss in cron.

## 6. Community Momentum & Maturity

**Activity tier**:
- **Tier 1 (Rapid iteration)**: OpenClaw — 500 daily updates, beta releases, many hotfixes merged within hours. Despite regressions, the project is not stalling.
- **Tier 2 (Steady growth)**: Hermes Agent — 100 daily updates, no release today but consistent merge velocity. Security responses are fast; UX requests take longer.

**Maturity indicators**:

| Maturity Signal | OpenClaw | Hermes Agent |
|-----------------|----------|--------------|
| **Release cadence** | Weekly beta; next stable likely within 30 days | Irregular; last release pre-dates today |
| **Backlog aging** | 5+ issues open >3 months (#45494, #74077, #44395) | 1 P1 open 21 days (#32091); 2+ features open >2 months (#25267, #12020) |
| **Regression trend** | Increasing post-5.20; duplicate reply bug affects core trust | Stable but with isolated critical gaps (cron, security) |
| **Maintainer bandwidth** | Stretched but effective — high throughput | Focused on security fixes; UX featurization slower |

**Stabilization timeline**:
- **OpenClaw** will likely stabilize in 4-6 weeks as compaction fallbacks, cron lease fixes, and session lock hardening merge. The v2026.6.8-beta.1 is a positive signal for channel quality.
- **Hermes** needs to address the P1 cron orphan (data loss risk) and Matrix E2EE exhaustion before it can be considered production-grade for automation. Claude OAuth integration (#25267) could be a major growth catalyst.

## 7. Trend Signals

The following industry trends emerge from cross-project community feedback, valuable for AI agent developers and platform builders:

### 1. Multi-channel delivery is now table stakes, not differentiation
OpenClaw’s rich-text Telegram beta and Hermes’ Matrix E2EE fixes show that users expect **lossless, deterministic delivery** across all channels. Silent truncation (both projects) and duplicate replies (OpenClaw) are immediate trust-breakers.

### 2. Provider neutrality is becoming a hard requirement
Both communities reject opaque third-party routing without consent:
- Hermes: #45058 (Parallel.ai silent routing) with 15 👍 and privacy backlash.
- OpenClaw: #85103 (fallback not triggered on quota exhaustion) — users want control over which provider handles overflow.
**Signal**: Expect a “provider routing manifesto” or explicit opt-in UX pattern in both roadmaps.

### 3. Cron automation is the unsung killer use case—and the most fragile
Both projects have critical cron bugs (orphan jobs in Hermes, MiniMax overload in OpenClaw). Users are running business processes on cron; silent failures are unacceptable. **Developers should invest in cron observability, delivery receipts, and explicit target-proofing** regardless of framework choice.

### 4. Credential security concerns are escalating beyond OAuth
Hermes’ security issues (#46411, #46413, #46427) reveal that credential exfiltration across sibling profiles is a real attack vector. OpenClaw’s Chinese user reporting $6/hr cost due to prompt cache failure (#91016) shows that **cost management and security are converging**—users need both isolation and transparency.

### 5. Cross-platform desktop support is fragmented
Hermes supports macOS (ARM-only, no Intel), Windows (WSL bash issues), and Linux; OpenClaw has no explicit desktop offering. **Intel Mac users and Windows power users are underserved**, creating an opportunity for projects that can deliver consistent CLI/TUI/Tauri-based experiences.

### 6. Concurrent session isolation is an unsolved design problem
Both projects exhibit concurrency bugs: OpenClaw’s `EmbeddedAttemptSessionTakeoverError` (prompt lock race) and Hermes’ #46303 (cross-contamination of memory and git worktrees). **Session isolation will be a major architectural battleground** — expect either lock-free designs (actor model) or heavier containerization (per-session Docker/Firecracker).

### 7. User-requested “lite” modes signal infrastructure fatigue
OpenClaw’s gateway-lite mode (#86881) and Hermes’ request for configurable status bars and hide-unconfigured-providers (#46304) indicate that **power users want to strip features they don’t use**, not accumulate more complexity. The market is shifting from “more features” to “lean, reliable core with optional extensions.”

---

**Recommendation for developers evaluating these projects**:
- **Choose OpenClaw** if channel richness and cron automation are primary, and your team can tolerate a regression-prone codebase while contributing to session-lock fixes.
- **Choose Hermes Agent** if security, provider transparency, and desktop UX matter more, but be prepared to patch the cron orphan bug or work around it.
- **Watch both projects** for convergence on session isolation and provider routing transparency—these will define the ecosystem’s next architectural standard.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-15

## 1. Today’s Overview

The Hermes Agent project continues to see intense community activity, with a combined **100 issues and pull requests** updated in the last 24 hours (84 open, 16 closed). While no new releases were cut today, the volume of merged fixes and feature PRs signals sustained momentum. The community is particularly focused on **security hardening** (credential exfiltration across profiles), **platform stability** (WebSocket timeouts, s6 Docker lifecycle bugs), and **user-requested UX improvements** (configurable status bar, `Keep` option for base URLs, hide unconfigured providers). Several regressions introduced in recent merges are now being addressed, indicating a high-velocity but responsive development cycle.

## 2. Releases

None today.

## 3. Project Progress

### Merged / Closed PRs Today (8 of 50 PRs updated were closed)

- [#46291 – fix(s6): make profile gateway log parent writable](https://github.com/NousResearch/hermes-agent/pull/46291) – Fixes s6-log deadlocks for late-added profile gateways.
- [#39840 – fix(ui-tui): stabilize embedded dashboard chat gateway](https://github.com/NousResearch/hermes-agent/pull/39840) – Prevents crash when embedded `/chat` loads before gateway transport is ready.
- [#46399 – fix(terminal): fall back to .env for env_passthrough in local backend](https://github.com/NousResearch/hermes-agent/pull/46399) – Mirrors Docker fallback logic to local backend.
- [#46438 – fix(send_message): support Telegram rich messages](https://github.com/NousResearch/hermes-agent/pull/46438) – Adds opt-in fast path for Telegram Bot API rich Markdown.

**Corresponding closed issues** include:
- [#7237 – [Bug]: Error: Response truncated due to output length limit](https://github.com/NousResearch/hermes-agent/issues/7237) – *Closed after 46 comments.*
- [#38963 – [Setup]: hermes desktop strat fail, it say no git???](https://github.com/NousResearch/hermes-agent/issues/38963)
- [#45058 – web_search/web_extract silently routes to Parallel.ai without user opt-in](https://github.com/NousResearch/hermes-agent/issues/45058) – *Privacy/opt-in concern closed with merged fix?*
- [#45865 – [Feature]: Add ability to remove provider accounts](https://github.com/NousResearch/hermes-agent/issues/45865)
- [#36515 – Improve test coverage: plugins/web/parallel/provider.py](https://github.com/NousResearch/hermes-agent/issues/36515)
- [#45258 – [Bug]: gateway per-profile log/run leaves logs/gateways/ parent root-owned](https://github.com/NousResearch/hermes-agent/issues/45258)
- [#46419 – Chat WebSocket close-error banners are hardcoded English, bypassing i18n](https://github.com/NousResearch/hermes-agent/issues/46419)
- [#45963 – [Bug]: `profile create` auto-starts a doomed resident gateway for every new profile in s6 container](https://github.com/NousResearch/hermes-agent/issues/45963)

## 4. Community Hot Topics

### Most Active Issues (by comments / reactions)

- [#7237 – Response truncated due to output length limit](https://github.com/NousResearch/hermes-agent/issues/7237) – 46 comments, 6 👍. *Closed today; long-standing frustration with truncated long-form responses across all platforms.*
- [#25267 – Claude Agent SDK model provider with subscription OAuth (Codex-style)](https://github.com/NousResearch/hermes-agent/issues/25267) – 7 comments, 21 👍. *Strong demand for Claude integration that reuses existing subscription instead of separate API billing.*
- [#45058 – web_search/web_extract silently routes to Parallel.ai](https://github.com/NousResearch/hermes-agent/issues/45058) – 7 comments, 15 👍. *Privacy backlash over default routing change; community wants explicit opt-in.*
- [#31584 – Treat memory-context as background context, not authoritative user-message content](https://github.com/NousResearch/hermes-agent/issues/31584) – 6 comments. *Safety/security concern: memory injection can be misused; proposed design change.*
- [#44560 – model.options handler blocks on synchronous per-provider HTTP calls causing WebSocket timeout](https://github.com/NousResearch/hermes-agent/issues/44560) – 5 comments. *Performance bug affecting multi-provider setups.*

### Top PRs (by recent activity)

- [#46292 – fix(s6): persist profile gateway desired state](https://github.com/NousResearch/hermes-agent/pull/46292) – Addresses container restart drift.
- [#44107 – Unify dashboard appearance and chat skins](https://github.com/NousResearch/hermes-agent/pull/44107) – Broad UX consolidation; open for review.
- [#46422 – fix(workflows): harden token permissions](https://github.com/NousResearch/hermes-agent/pull/46422) – CI security hardening.
- [#46346 – fix: refresh OpenCode Go model catalog](https://github.com/NousResearch/hermes-agent/pull/46346) – Fallback model picker fixes.

**Underlying needs**: The community is pushing for **better model provider integration** (Claude subscription re-use), **transparent defaults** (no silent routing), **performance under multiple providers**, and **configurable UI** (skins, status bar, provider visibility).

## 5. Bugs & Stability

### Critical / P1

- [#46310 – [Bug]: send_message Matrix (media) path reconnects + re-inits E2EE per message – exhausts recipient one-time keys and silently drops messages under burst](https://github.com/NousResearch/hermes-agent/issues/46310) – *P1, Matrix media bug; No fix PR yet.*
- [#32091 – Cron jobs created from a profile-scoped agent session go to a jobs.json the gateway never reads (silent orphan)](https://github.com/NousResearch/hermes-agent/issues/32091) – *P1, open since May 25; severe data loss.*

### High / P2

- [#44560 – model.options handler blocks on synchronous per-provider HTTP calls causing WebSocket timeout](https://github.com/NousResearch/hermes-agent/issues/44560) – *Open, no fix PR.*
- [#46303 – Concurrent sessions cross-contaminate (shared memory injection + shared git worktree)](https://github.com/NousResearch/hermes-agent/issues/46303) – *Open, reported today; isolation regression.*
- [#46411 – Security: read_file can exfiltrate credential stores from sibling profiles](https://github.com/NousResearch/hermes-agent/issues/46411) – **Fix PR #46417 exists** (extends `read_file` guard).
- [#46413 – Security: Desktop file preview can read Hermes credential stores](https://github.com/NousResearch/hermes-agent/issues/46413) – *Open, no fix PR yet.*
- [#45963 – [Bug]: `profile create` auto-starts doomed resident gateway in s6 container (zombie tokens)](https://github.com/NousResearch/hermes-agent/issues/45963) – *Closed with PR #46291?*
- [#45258 – [Bug]: gateway per-profile log/run leaves parent root-owned → s6-log loops](https://github.com/NousResearch/hermes-agent/issues/45258) – *Closed with PR #46291.*
- [#46427 – fix: prevent copilot from leaking into model picker via GH_TOKEN](https://github.com/NousResearch/hermes-agent/pull/46427) – *Open PR fixing unexpected Copilot provider appearance.*

### Medium / P3

- [#46090 – Agent becoming extremely slow for basic tasks](https://github.com/NousResearch/hermes-agent/issues/46090) – *Open, needs reproduction.*
- [#46265 – SimpleX adapter silently drops all DM replies](https://github.com/NousResearch/hermes-agent/issues/46265) – *Open.*
- [#46332 – [Windows] Cron jobs with .sh scripts fail because WSL bash is picked over Git Bash](https://github.com/NousResearch/hermes-agent/issues/46332) – *Open.*
- [#46320 – Desktop: bottom-left model switcher lacks global toggle; resuming session overwrites model override](https://github.com/NousResearch/hermes-agent/issues/46320) – *Open.*
- [#46419 – Chat WebSocket close-error banners hardcoded English, bypassing i18n](https://github.com/NousResearch/hermes-agent/issues/46419) – *Closed, presumably via PR.*
- [#46412 – fix(file_tools): don't treat macOS temp/scratch paths as sensitive](https://github.com/NousResearch/hermes-agent/pull/46412) – *Open PR fixing file write blocking on macOS.*
- [#46410 – fix(tirith): support Termux musl auto-install](https://github.com/NousResearch/hermes-agent/pull/46410) – *Open PR for mobile security tool.*

## 6. Feature Requests & Roadmap Signals

### Likely to land in next release (high attention / PRs exist)

- **Claude subscription OAuth** (#25267, 21 👍) – Strong demand, design discussion ongoing; could be accompanied by a model provider plugin refactor.
- **Remove provider accounts in UI** (#45865) – Simple UX fix, likely to be merged soon.
- **Configurable TUI status bar (fields, layout, skin)** (#13490) – Appeals to power users and skin authors.
- **Hiding unconfigured providers from model switcher** (#46304) – Low risk, high QoL.
- **Fallback session stickiness configurable (`fallback_model.sticky`)** (#23094) – Requested for more predictable fallback behavior.

### Emerging signals

- **GBrain as memory provider plugin** (#46253) – Indicates interest in external semantic memory backends.
- **x86_64 macOS build** (#42199, 4 comments) – Intel Mac users are left out; could be addressed if build infrastructure grows.
- **`/api/appearance` unification** (PR #44107) – Suggests a broader theming/layout system is underway.
- **Kanban epoch callback for spiral workflows** (PR #46360) – Points toward more sophisticated autonomous workflows.

## 7. User Feedback Summary

### Pain Points (direct quotes or paraphrases)

- “Response truncated due to output length limit” – long-form tasks break mid-stream; affects CLI, Telegram, Discord, Slack (#7237, closed).
- “No way to disconnect a provider account in the UI” – once connected, users feel trapped (#45865).
- “Intel Macs cannot run the Desktop App” – DMG is ARM64 only, no Rosetta fallback (#42199).
- “Silent routing to Parallel.ai without opt-in” – trust violated; users demand explicit consent for third-party services (#45058).
- “Concurrent Desktop sessions cross-contaminate memory and git worktrees” – no isolation is a reliability risk (#46303).
- “Agent extremely slow for basic tasks” – potential context bloat; no diagnose tool (#46090).
- “SimpleX DMs are dropped silently” – zero feedback on failure (#46265).
- “Matrix E2EE reconnects per message causing key exhaustion” – bursts cause silent message loss (#46310).

### Satisfaction signals

- Quick turnaround on security issues: multiple fix PRs opened same day as bug reports (e.g., #46417, #46427, #46421).
- Community members actively writing PRs for feature requests (e.g., unified appearance PR #44107, kanban epoch PR #46360).
- Closed issues with high comment counts indicate responsive maintainers.

## 8. Backlog Watch

### Long-unanswered / Unresolved Important Issues

- [#32091 – Cron job silent orphan (P1, opened May 25)](https://github.com/NousResearch/hermes-agent/issues/32091) – No maintainer response in 21 days; cron is core functionality for automation users.
- [#25267 – Claude subscription OAuth (P3, opened May 13, 21 👍)](https://github.com/NousResearch/hermes-agent/issues/25267) – No official comment from maintainers despite high demand.
- [#12020 – Disable `hermes.tool.progress` output (P3, opened Apr 18)](https://github.com/NousResearch/hermes-agent/issues/12020) – Affects frontend compatibility; no resolution in 2 months.
- [#13490 – Configurable TUI status bar (P3, opened Apr 21)](https://github.com/NousResearch/hermes-agent/issues/13490) – Open for 55 days; a prominent UX enhancement.
- [#31584 – Memory-context as background context (P2, opened May 24)](https://github.com/NousResearch/hermes-agent/issues/31584) – Security/reliability design discussion still open.

### PRs Awaiting Review

- [#44107 – Unify dashboard appearance and chat skins](https://github.com/NousResearch/hermes-agent/pull/44107) – Large PR with UX implications, open since Jun 11.
- [#46360 – Kanban epoch callback for spiral workflows](https://github.com/NousResearch/hermes-agent/pull/46360) – New feature for autonomous workflows; may benefit from maintainer feedback.

**Maintainer attention recommended** for the P1 orphan cron bug (#32091) and the widely-upvoted Claude OAuth feature (#25267) to sustain community engagement.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*