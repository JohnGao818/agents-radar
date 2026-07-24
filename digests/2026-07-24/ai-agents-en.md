# OpenClaw Ecosystem Digest 2026-07-24

> Issues: 312 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-24 02:16 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-24

## Today’s Overview

OpenClaw remains extremely active, with **312 issues** and **500 pull requests** updated in the last 24 hours. Of these, **217 issues are open** (117 closed) and **314 PRs are open** (186 merged/closed). No new releases were tagged today, but the project shows continued heavy development and community engagement. The high volume of issues and PRs suggests both a growing user base and an active maintainer team, though the backlog of stale items (many tagged `needs-maintainer-review`) indicates that triage capacity may be stretched.

## Releases

*None today.*  
The last published release remains `2026.7.2-beta.3` (as referenced in issue #111519). No release notes or changelog updates to report.

## Project Progress

**186 pull requests were merged or closed in the last 24 hours,** advancing several areas:

- **Matrix channel support** – PR [#113199](https://github.com/openclaw/openclaw/pull/113199) (closed) adds rendering for spoilers, underline, and native tables.
- **Sessions & typing indicators** – PR [#113173](https://github.com/openclaw/openclaw/pull/113173) (closed) introduces a suggestion queue and typing indicator for multi‑user sessions.
- **WhatsApp reactions** – PR [#113178](https://github.com/openclaw/openclaw/pull/113178) (closed) fixes reaction delivery to active DMs and groups.
- **Gateway without systemd** – PR [#112386](https://github.com/openclaw/openclaw/pull/112386) (closed) adds detection for non‑systemd Linux environments.
- **iOS UI** – PR [#113057](https://github.com/openclaw/openclaw/pull/113057) (open) renders assistant media attachments on iOS.

Several open PRs with high activity are nearing completion:
- [#110250](https://github.com/openclaw/openclaw/pull/110250) – signed sharded catalog consumption (feeds)
- [#101981](https://github.com/openclaw/openclaw/pull/101981) – signed ClawHub default feed trust
- [#112863](https://github.com/openclaw/openclaw/pull/112863) – improved Signal server setup guide
- [#113201](https://github.com/openclaw/openclaw/pull/113201) – refactoring embedded attempt terminal outcomes

## Community Hot Topics

The most active discussions (by comment count) highlight persistent reliability and usability concerns:

| Issue | Comments | Topic |
|-------|----------|-------|
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | 22 | Subagent completion silently lost – no retry, no notification |
| [#102020](https://github.com/openclaw/openclaw/issues/102020) | 15 | Second message fails with “reply session initialization conflicted” |
| [#94228](https://github.com/openclaw/openclaw/issues/94228) | 14 | Anthropic native path: thinking blocks brick long tool-use sessions |
| [#92043](https://github.com/openclaw/openclaw/issues/92043) | 13 | 180s compaction timeout breaks long histories without partial reuse |
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | 10 | Gateway fails to start after update to 2026.7.1 (P0 regression) |
| [#110950](https://github.com/openclaw/openclaw/issues/110950) | 9 (closed) | Proposal to unify all automation around a single cron job primitive |

The underlying needs are clear: **reliability of agent orchestration** (subagent completion, session state, compaction), **cross‑channel consistency** (Telegram DM fallback, Discord MCP access), and **upgrade safety** (silent migration of cron stores, gateway startup). Many of these issues carry `P1` severity and have `clawsweeper:needs-maintainer-review` tags, indicating maintainer attention is needed.

## Bugs & Stability

**P0 (Release‑blocking)**
- [#108435](https://github.com/openclaw/openclaw/issues/108435) – Gateway fails to start after update to `2026.7.1` (`Error: gateway did not start on 127.0...`). Labeled `regression`. No fix PR yet.
- [#90378](https://github.com/openclaw/openclaw/issues/90378) – Upgrade 5.28→6.1: cron store silently migrates to SQLite, new jobs get wrong delivery mode. Linked PR open.
- [#108580](https://github.com/openclaw/openclaw/issues/108580) – Cron tool schema incompatible with llama.cpp grammar‑constrained tool calling (2026.7.1 regression). Linked PR open.

**P1 (Critical)**
- [#44925](https://github.com/openclaw/openclaw/issues/44925) – Subagent completion silently lost on timeout. Labeled `diamond lobster`.
- [#94228](https://github.com/openclaw/openclaw/issues/94228) – Anthropic thinking blocks cause permanent `Invalid signature` 400 errors. Linked PR open.
- [#92043](https://github.com/openclaw/openclaw/issues/92043) – Compaction timeout (180s wall clock) repeats failures every turn. Labeled `diamond lobster`.
- [#102020](https://github.com/openclaw/openclaw/issues/102020) – Second message fails with initialization conflict (cross‑channel).
- [#98435](https://github.com/openclaw/openclaw/issues/98435) – MCP loopback transport does not auto‑reconnect after gateway restart; `recovered=1` is misleading.
- [#111519](https://github.com/openclaw/openclaw/issues/111519) – Telegram DM replies fall back after stale DM‑scope cleanup (regression in beta.3).

**P2 (Significant)**
- [#67419](https://github.com/openclaw/openclaw/issues/67419) – Session context bloat: bootstrap files re‑injected every turn wasting 20‑30% tokens.
- [#8299](https://github.com/openclaw/openclaw/issues/8299) – No config option to suppress sub‑agent announce.
- [#102081](https://github.com/openclaw/openclaw/issues/102081) – Exec allowlist never auto‑executes on macOS (darwin).
- [#91799](https://github.com/openclaw/openclaw/issues/91799) – Discord agents cannot access MCP tools (works via CLI).

Many P1/P0 issues have linked pull requests (e.g., #108580, #90378, #94228) or `clawsweeper:fix-shape-clear` labels, suggesting active work.

## Feature Requests & Roadmap Signals

Several popular feature requests could land in the next minor release:

| Issue | Topic | Likely priority |
|-------|-------|-----------------|
| [#110950](https://github.com/openclaw/openclaw/issues/110950) | Unify heartbeat, watchers, and scheduled automation under cron | High – closed by maintainer, RFC exists |
| [#8299](https://github.com/openclaw/openclaw/issues/8299) | Config option to suppress sub‑agent announce | Medium – many upvotes, workaround unreliable |
| [#87325](https://github.com/openclaw/openclaw/issues/87325) | Azure Foundry GPT Realtime Talk support | Medium – enterprise demand |
| [#38520](https://github.com/openclaw/openclaw/issues/38520) | Pre‑compaction agent notification and deferral | Medium – addresses data loss |
| [#38568](https://github.com/openclaw/openclaw/issues/38568) | Inject context window percentage into system prompt | Medium – easy win, high utility |
| [#42651](https://github.com/openclaw/openclaw/issues/42651) | Memory MVP: ingestion CLI/skill surface | High – part of memory roadmap |
| [#42648](https://github.com/openclaw/openclaw/issues/42648) | Memory write pipeline with classification/dedupe | High – part of memory roadmap |
| [#12219](https://github.com/openclaw/openclaw/issues/12219) | Skill permission manifest standard (`skill.yaml`) | Medium – security demand |
| [#7524](https://github.com/openclaw/openclaw/issues/7524) | `groupScope` option to consolidate group sessions into main | Medium – user request |
| [#45390](https://github.com/openclaw/openclaw/issues/45390) | Session TTL / max lifetime for automatic rotation | Medium – prevents bloat |
| [#41418](https://github.com/openclaw/openclaw/issues/41418) | Global `--dry-run` mode to preview tool calls | Low – nice to have |

The memory system (#42651, #42648) and the automation unification (#110950) are most likely to ship in the next version, as they have explicit roadmap references and ongoing PRs.

## User Feedback Summary

**Common pain points expressed by users:**
- **Silent failures** – subagent completions disappear, tool results go empty, sessions freeze with no error. Multiple reports of “permanent silence” after update.
- **Context bloat** – bootstrap files consumed 20‑30% of tokens every turn; no way to limit session lifetime.
- **Upgrade regressions** – every minor version introduces new breaking changes (cron store migration, gateway startup, schema incompatibility).
- **Cross‑channel inconsistency** – Discord MCP access, WhatsApp image handling, Telegram DM fallback all have distinct bugs.
- **Lack of observability** – no test command for fallback chain, no compaction notification, `doctor` reports conflicting status.

**Positive signals:**
- Active community contributing fixes and features (e.g., Matrix, Signal, iOS, localization).
- High number of PRs merged daily indicates rapid iteration.
- Users are deploying at scale (multi‑agent, self‑hosted production) and providing detailed field reports (e.g., #41372 with 25 findings).

**Satisfaction/dissatisfaction:**
- Dissatisfaction centers on stability – many “worked before, now fails” labels.
- Satisfaction with the project’s ambition and pace – users continue to invest in self‑hosted setups despite the rough edges.

## Backlog Watch

The following important issues and PRs have been open for extended periods and still lack maintainer review or a clear path forward:

**Stale Issues (no maintainer review for weeks/months)**
- [#94228](https://github.com/openclaw/openclaw/issues/94228) – Anthropic thinking blocks brick tool-use (since June 17)
- [#92043](https://github.com/openclaw/openclaw/issues/92043) – Compaction timeout repeats (since June 10)
- [#90378](https://github.com/openclaw/openclaw/issues/90378) – Cron store migration silent (since June 4)
- [#8299](https://github.com/openclaw/openclaw/issues/8299) – Sub‑agent announce suppression (since February)
- [#87325](https://github.com/openclaw/openclaw/issues/87325) – Azure Foundry support (since May 27)
- [#42820](https://github.com/openclaw/openclaw/issues/42820) – Feishu message tool polluted by poll schema (since March 11)
- [#6599](https://github.com/openclaw/openclaw/issues/6599) – `/models test-fallback` command (since February)
- [#38520](https://github.com/openclaw/openclaw/issues/38520) – Pre‑compaction notification (since March)
- [#48579](https://github.com/openclaw/openclaw/issues/48579) – Context pruning “off” not preventing compactions (since March)
- [#43374](https://github.com/openclaw/openclaw/issues/43374) – All LLM API calls time out simultaneously (since March)
- [#42273](https://github.com/openclaw/openclaw/issues/42273) – `backup create` stalls on large installations (since March)

**Stale Pull Requests needing review**
- [#92307](https://github.com/openclaw/openclaw/pull/92307) – Warn on exec security clamping (since June 12, `ready for maintainer look`)
- [#91078](https://github.com/openclaw/openclaw/pull/91078) – Sandbox fs bridge fix for Codex exec-server (since June 7, `ready for maintainer look`)
- [#95384](https://github.com/openclaw/openclaw/pull/95384) – Prevent plugins being skipped after upgrade (since June 20, `needs proof`)
- [#106015](https://github.com/openclaw/openclaw/pull/106015) – SQLite migration recovery report emoji corruption (since July 13, `needs proof`)
- [#83933](https://github.com/openclaw/openclaw/pull/83933) – Fix cron `deleteAfterRun` and counters (since May 19, `needs proof`)

These items represent significant unresolved stability and usability gaps. Their age suggests maintainer bandwidth is a bottleneck. Community contributions that include test coverage and reproduction steps (e.g., #92307, #91078) are more likely to be acted upon.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Open-Source AI Agent Ecosystem

## 1. Ecosystem Overview

The open-source personal AI assistant landscape is characterized by rapid iteration and high community engagement, with two major reference implementations—OpenClaw and Hermes Agent—driving development. Both projects share common pain points around reliability (silent failures, session state corruption, upgrade regressions) while diverging in architectural focus: OpenClaw is a broad, channel-integration-first platform, while Hermes Agent emphasizes desktop UI and managed authentication flows. The ecosystem as a whole is maturing from experimental to production-grade, with users demanding reliability, observability, and backward compatibility alongside new features. Community feedback consistently prioritizes stability over feature velocity, despite the high cadence of contributions.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues Updated (24h)** | 312 | 50 |
| **Open Issues** | 217 | ~39 (estimate from 50 updated, 11 closed) |
| **PRs Updated (24h)** | 500 | 50 |
| **PRs Merged/Closed (24h)** | 186 | 5 |
| **New Release Today** | No | No |
| **Health Score** | 7/10 – High throughput, triage bottleneck | 6/10 – Focused fixes, critical P1 regressions |

**Key Takeaway:** OpenClaw exhibits an order of magnitude higher activity volume, but this masks a growing stale-backlog problem. Hermes Agent has lower volume but achieves higher closure ratios per issue—suggesting more focused maintainer triage.

## 3. OpenClaw’s Position

**Advantages:**
- **Community scale:** 6x more issues and 10x more PRs than Hermes Agent, indicating larger user base and contribution pool.
- **Integration breadth:** Native support for Matrix, Signal, WhatsApp, Telegram, Discord, and Feishu—Hermes Agent focuses heavily on Telegram and desktop.
- **Feature depth:** Memory roadmap (ingestion CLI, write pipeline), cron unification proposal, and signed catalog consumption are well-documented and actively developed.
- **PR throughput:** 186 merges/closure in 24 hours demonstrates high maintainer capacity despite triage bottlenecks.

**Technical Approach Differences:**
- OpenClaw uses a **modular gateway architecture** with fallback chains and multi-channel session management, while Hermes Agent relies on a **desktop-first GUI** with OAuth-based provider onboarding.
- OpenClaw’s **sub-agent orchestration model** (with silent failure issues) contrasts with Hermes Agent’s **Mixture-of-Agents (MoA)** implementation—two different scalability strategies.
- OpenClaw has deeper **LLM provider integration** (Anthropic thinking blocks, llama.cpp grammar constraints), whereas Hermes Agent focuses on **Nous provider OAuth** and Claude subscription support.

**Community Size Comparison:**
- OpenClaw’s issue count (217 open) vs Hermes Agent’s (~39 open) suggests roughly **5x user base**, though triangulation with GitHub stars would be needed for precision.
- Hermes Agent has stronger **desktop UI community** (repeated UX bugs generate high comment counts), while OpenClaw’s community is more **devops/self-hosting oriented** (deployment scripts, backup tooling).

## 4. Shared Technical Focus Areas

| Focus Area | OpenClaw | Hermes Agent | Consensus Need |
|------------|----------|--------------|----------------|
| **Session state reliability** | #102020: reply initialization conflict; #44925: subagent silent loss | #66875: tab navigation breaks session selection | **Cross-project priority: session persistence and recovery** |
| **Context compaction/management** | #92043: 180s compaction timeout; #67419: bootstrap bloat | #14694: anti-thrashing compression disabled (P1, 3 months stale) | **Automated, configurable context pruning with user notification** |
| **Authentication/OAuth stability** | #108435: gateway fails after upgrade (P0) | #70401: unbounded 401 retry loop (P1) | **Graceful degradation, self-healing retry, and clear error paths** |
| **Cross-channel consistency** | #111519: Telegram DM fallback; #91799: Discord MCP access | #69314: Telegram gateway CLOSE_WAIT storm | **Uniform message delivery semantics across platforms** |
| **Upgrade safety** | #90378: cron store silent migration; #108580: schema incompatibility | #70473: plugin callbacks invalidated after update | **Zero-downtime migrations, rollback support, changelog emphasis** |
| **Observability** | #6599: test-fallback command; #38520: compaction notification | #45148: profile-scoped analytics broken | **CLI/API introspection for debugging and monitoring** |

**Notable:** Both projects have **P1/P0 bugs open for >3 weeks** without maintainer resolution, indicating industry-wide capacity constraints.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary interface** | CLI + gateway (multi-channel) | Desktop GUI + Telegram gateway |
| **Target user** | DevOps/self-hoster running multi-agent systems | Desktop power user wanting managed assistant |
| **Agent orchestration** | Sub-agent model (hierarchical, silent failures) | MoA (mixture-of-agents, toggleable) |
| **LLM provider focus** | Broad: Anthropic, llama.cpp, Azure, GPT-RT | Narrow: Nous, Claude (planned), MoA reference models |
| **Unique features** | Memory MVP, cron unification, signed catalogs | Automatic backup (most-voted), in-session navigation sidebar |
| **Architecture** | Modular gateway with fallback chains, SQLite/persistence | Desktop app with OAuth + plugin lifecycle |
| **Maturity indicator** | Stale backlog of 10+ issues >1 month old | 3 P1 bugs open >1 month (e.g., #14694) |
| **Community voice** | “Reliability above all” – silent failures dominate complaints | “Give me my state back” – backup is #1 feature request |

**Strategic Implication:** OpenClaw is positioned as the **“Linux of AI agents”**—flexible, hackable, demanding technical expertise. Hermes Agent aims for **“macOS-like usability”**—polished desktop experience with managed integrations. Both are valid, but their diverging UX philosophies lead to different failure modes.

## 6. Community Momentum & Maturity

**Activity Tiers:**

- **Tier 1 – Rapidly iterating:** OpenClaw (186 PRs merged/24h). Despite backlog, maintainer throughput is exceptional. The project is actively shipping fixes for Matrix, WhatsApp, iOS, and core infrastructure.
- **Tier 2 – Focused iteration:** Hermes Agent (5 PRs merged/24h). Lower volume but higher closure ratio. The team is systematically closing MoA features and addressing P1 bugs, suggesting a stabilizing phase.

**Stabilization Signals:**
- OpenClaw: MoA features closed, memory roadmap RFC exists, but P0/P1 release-blocking bugs (gateway startup, cron schema) remain unmerged.
- Hermes Agent: Desktop UI regressions (session switching, websocket storms) persist without fix PRs. The P1 anti-thrashing issue (#14694) has been open for 3 months—a concerning indicator.

**Critical Stability Risk:** Both projects have **P0/P1 issues without clear resolution path** that could block the next release:
- OpenClaw: #108435 (gateway fail-to-start regression, no fix PR)
- Hermes Agent: #70401 (OAuth retry loop, no direct fix)

## 7. Trend Signals

**For AI Agent Developers:**

1. **Reliability is the new feature.** Community feedback across both projects explicitly prioritizes “permanent silence free” sessions over new integrations. Silent failures (subagents, tool results, authentication) erode user trust faster than any feature addition can restore it.

2. **Context management is the scaling bottleneck.** Compaction timeouts, token bloat from bootstrap files, and session lifetime limits are the #1 technical debt area. Developers building agent frameworks should invest in **observable, user-configurable, and predictive** context pruning—not just wall-clock-time timeouts.

3. **Cross-platform parity is table stakes.** Users expect identical agent behavior across Telegram, Discord, WhatsApp, and desktop UI. Inconsistencies (MCP access, DM fallback, image handling) generate disproportionate frustration. The next wave of agent adoption will require **channel-agnostic protocol semantics**.

4. **Backup and state persistence are non-negotiable.** Hermes Agent’s #12238 (19 upvotes) and OpenClaw’s memory roadmap signal that users treat agent state as valuable data they cannot afford to lose. Developers should bake export/import and versioned storage into core architecture from day one.

5. **Upgrade safety is the hidden churn factor.** Both projects report significant regression pain after “minor” updates. The ecosystem needs **canary deployment patterns, schema migration validation, and rollback documentation**—not just bug-fix volume.

6. **Observability tools are underdeveloped.** Neither project offers a comprehensive “what just happened” debug command. The absence of compaction notifications, fallback test commands, and session state introspection suggests this is a gap the whole ecosystem will need to address as deployments scale.

**Bottom Line for Decision-Makers:** The open-source AI agent ecosystem is building fast but breaking too often. If you need **production-grade reliability today**, invest in observability tooling and upgrade testing. If you want **short-term feature breadth**, embed a sub-agent pattern or MoA layer. But plan for the cross-cutting reliability tax—it’s coming for both projects.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-24

## 1. Today’s Overview
Hermes Agent saw exceptionally high activity in the last 24 hours: **50 issues** and **50 pull requests** were updated, with 11 issues closed and 5 PRs merged or closed. The project remains in an intense bug-fixing and feature-development cycle without a new release today. Desktop UI regressions, OAuth authentication retry loops, and plugin lifecycle issues dominate the current bug landscape, while long-standing feature requests (e.g., automatic backup, in-session navigation) continue to attract strong community support. Despite the high volume, several critical bugs received targeted fix PRs, indicating active maintainer triage.

## 2. Releases
*No new releases today.*

## 3. Project Progress
Only one PR was closed (merged or otherwise) among the top 20:
- **[#70471 – fix(tests): prevent auth_gate.py from leaking state to subsequent test files](https://github.com/NousResearch/hermes-agent/pull/70471)** – merged: adds an auto-cleanup fixture so `test_dashboard_auth_gate.py` does not pollute later test runs.

Several important bugs from previous days were closed as issues (indicating fixes were merged or otherwise resolved):
- **Empty/whitespace text blocks causing HTTP 400 on Anthropic** – [#69512](https://github.com/NousResearch/hermes-agent/issues/69512) (closed)
- **MoA reference models fabricating tool execution** – [#61452](https://github.com/NousResearch/hermes-agent/issues/61452) (closed as duplicate, likely addressed elsewhere)
- **MoA enable/disable toggle** – [#59707](https://github.com/NousResearch/hermes-agent/issues/59707) (closed – feature delivered)
- **MoA privacy filter** – [#59959](https://github.com/NousResearch/hermes-agent/issues/59959) (closed)
- **MoA progress indicator** – [#59546](https://github.com/NousResearch/hermes-agent/issues/59546) (closed)

## 4. Community Hot Topics
The most active discussions (by comment count) reveal deep user engagement with UI reliability and feature gaps:

- **#66875 – [Bug]: Latest session does not switch after tab navigation**  
  8 comments | [Link](https://github.com/NousResearch/hermes-agent/issues/66875)  
  *Underlying need:* Desktop sidebar state consistency when switching away from chat and back. High frustration with the “stuck on non-chat page” behavior.

- **#69314 – [Bug]: Telegram gateway behind HTTP proxy enters CLOSE_WAIT retry storm**  
  7 comments | [Link](https://github.com/NousResearch/hermes-agent/issues/69314)  
  *Underlying need:* Reliable message delivery over proxy setups. The permanent degraded state forces full container restarts.

- **#12238 – [Feature]: Built-in Automatic Backup & Version Control (~/.hermes)**  
  6 comments, **19 👍** | [Link](https://github.com/NousResearch/hermes-agent/issues/12238)  
  *Underlying need:* Users are afraid of losing learned agent state, conversation history, and skills. The high reaction count signals strong demand.

- **#49978 – [Bug]: PageUp input focus breaks page layout**  
  6 comments, 2 👍 | [Link](https://github.com/NousResearch/hermes-agent/issues/49978)  
  *Underlying need:* Desktop UI stability under standard keyboard interactions (PageUp/Down). Duplicate reports [#52235](https://github.com/NousResearch/hermes-agent/issues/52235) confirm it’s a common pain point.

- **#69551 – [Bug]: Desktop SSH remote mode broken with non-default profile**  
  5 comments | [Link](https://github.com/NousResearch/hermes-agent/issues/69551)  
  *Underlying need:* Profile-scoped `HERMES_HOME` not honoured by the SSH client – a critical path for remote multi-profile users.

## 5. Bugs & Stability
| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| **P1** | [#70401](https://github.com/NousResearch/hermes-agent/issues/70401) | OAuth credential pool enters unbounded 401 retry loop, ignores stop signals (Nous provider) | No direct fix; [#70465](https://github.com/NousResearch/hermes-agent/pull/70465) addresses stale OAuth on ACP sessions, possibly related |
| **P2** | [#70424](https://github.com/NousResearch/hermes-agent/issues/70424) | Desktop: clicking chat from Kanban/Artifacts does not return to chat – forced to New Session | No |
| **P2** | [#69930](https://github.com/NousResearch/hermes-agent/issues/69930) | Desktop GUI websocket reconnect-cycles every 30–45s; detached sessions accumulate | No |
| **P2** | [#70473](https://github.com/NousResearch/hermes-agent/issues/70473) | Git plugin updates invalidate callbacks loaded by running gateway | Yes: [#70474](https://github.com/NousResearch/hermes-agent/pull/70474) |
| **P3** | [#70400](https://github.com/NousResearch/hermes-agent/issues/70400) | Desktop missing window controls on WSLg | No |
| **P3** | [#70444](https://github.com/NousResearch/hermes-agent/issues/70444) | Project list reorders when entering/exiting chat | No |
| **P3** | [#70346](https://github.com/NousResearch/hermes-agent/issues/70346) | Dashboard chat switcher goes stale – no live refresh | No |
| **P3** | [#70450](https://github.com/NousResearch/hermes-agent/issues/70450) | Relative timestamps should show exact time on hover (labeled “bug”) | No |

**Regressions & stability risks**: The P1 OAuth retry loop is a self-sustaining resource exhaustion bug that requires external process kill. The desktop websocket disconnect storm (P2) is also high-impact for heavy users.

## 6. Feature Requests & Roadmap Signals
Top user-requested features likely to influence the next release:

- **Automatic Backup & Version Control** (#12238, 19 👍) – oldest open feature request with huge support. Predicting inclusion in v0.20.0 if capacity allows.
- **In-session message navigation sidebar** (#69532, 2 comments, Chinese UI) – mirrors DeepSeek’s side panel for long conversations.
- **Optional Cursor Models billing via standalone plugin** (#70140) – a niche but strategic request for Cursor Pro subscribers.
- **MoA progress indicator** (#59546) – already closed; likely shipped or about to ship.
- **MoA privacy filter** (#59959) – closed, presumably implemented.

The large PR **[#65982 – claude-agent-sdk provider](https://github.com/NousResearch/hermes-agent/pull/65982)** (25 sweeper tags, P3) is a significant new feature that could land soon, bringing Claude subscription OAuth as a first-class provider.

## 7. User Feedback Summary
- **Frustration**: Desktop session switching UX is a recurring pain point – users report being “stuck” on non-chat pages or having to click “New Session” as a workaround. Websocket instability and profile-scope bugs undermine trust in desktop mode.
- **Reliability**: Proxy-backed gateways (Telegram) and OAuth authentication loops are the most critical reliability complaints today. Users expect self-healing or clearer error messages.
- **Desired improvements**: The overwhelming vote for backup (#12238) indicates that agent state persistence is a top priority. The MoA enhancements (toggle, progress, privacy) were well received – their closure suggests responsiveness to community wishes.
- **Satisfaction signals**: Rapid bug fixes (e.g., Anthropic empty text blocks) show the team is listening, but the high volume of open P1/P2 bugs may dampen overall satisfaction for power users.

## 8. Backlog Watch
Long-standing or critical items that still need maintainer attention:

| Issue | Opened | Updated | Severity / Popularity | Why it matters |
|-------|--------|---------|-----------------------|----------------|
| [#14694 – Anti-thrashing compression permanently disabled](https://github.com/NousResearch/hermes-agent/issues/14694) | 2026-04-23 | 2026-07-24 | P1, 4 comments | No recovery mechanism after thrash; session-level auto-compression stays broken until restart. |
| [#12238 – Automatic Backup & Version Control](https://github.com/NousResearch/hermes-agent/issues/12238) | 2026-04-18 | 2026-07-24 | 19 👍 | Highest community demand, no official response or assignment. |
| [#52669 – System prompt hardcodes ~/.hermes instead of HERMES_HOME](https://github.com/NousResearch/hermes-agent/issues/52669) | 2026-06-25 | 2026-07-24 | P3, 1 👍 | Blocks clean multi-profile setups and non-standard installations. |
| [#45148 – /analytics?profile=custom doesn’t work](https://github.com/NousResearch/hermes-agent/issues/45148) | 2026-06-12 | 2026-07-24 | P3, 3 comments | Profile-scoped analytics is broken or misleading; no PR yet. |
| PR [#65982 – claude-agent-sdk provider](https://github.com/NousResearch/hermes-agent/pull/65982) | 2026-07-16 | 2026-07-24 | P3, 25 sweeper tags | Large feature PR, possibly awaiting final review; marked `needs-decision`. |

Despite high activity, these items have not seen any maintainer assignment or milestone movement in over a month (or in the case of #14694, three months). They represent the most persistent gaps in the user experience.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*