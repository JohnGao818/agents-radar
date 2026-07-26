# OpenClaw Ecosystem Digest 2026-07-26

> Issues: 341 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-26 02:25 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-26

## Today’s Overview
Activity on the OpenClaw repository remained very high over the past 24 hours, with **341 issues updated** (241 open, 100 closed) and **500 pull requests updated** (277 open, 223 merged/closed). No new releases were published. The project is in a period of intense development and community reporting, but also faces several critical regressions in the 2026.7.1 release line. Maintainers are actively reviewing and merging PRs, with 223 PRs closed/merged today. However, **P0 and P1 bugs** affecting gateway startup, session creation, and core data integrity (SQLite snapshots, config corruption) are prominent, suggesting the current stable channel may need a hotfix release.

## Releases
No new releases today.

## Project Progress
Today **223 pull requests were merged or closed**, reflecting substantial forward momentum. Among the closed PRs visible in the top-30 list:

- **#113971** (`build(lint): adopt stylelint for Control UI CSS`) – introduces CSS linting to prevent styling defects.
- **#113948** (`feat(ui): drag custom sidebar groups between built-in session zones`) – improves Control UI sidebar customization.
- **#113976** (`fix(qwen): enforce Token Plan constraints for direct model refs`) – ensures Qwen Token Plan models maintain required payload constraints.

Open PRs under active review include critical stability fixes:
- **#113959** (fix(sessions): gateway becomes unusable with many sessions) – addresses multi-second SQLite table reloads.
- **#113471** (fix(memory): close previous embedding provider before replacement) – prevents orphaned processes in memory-core.
- **#113654** (fix(logging): keep JSON console output structured across CLI routes) – closes #111906.

Major structural refactors are also in progress: **#113979** (split `acp-spawn.ts`), **#113974** (split QA Lab suite), **#113783** (split Windows task scheduler integration) – all aimed at reducing technical debt.

## Community Hot Topics
Issues with highest engagement (by comment count):

- **#7707** [OPEN] *Feature Request: Memory Trust Tagging by Source* (21 comments, 0 👍)  
  [openclaw/openclaw Issue #7707](https://github.com/openclaw/openclaw/issues/7707)  
  *Underlying need:* Memory poisoning prevention – users want a trust-level system to block malicious instructions hidden in untrusted content (web pages, third-party skills).

- **#78308** [OPEN] *Channel-mediated approval for MCP tool calls (consent envelope)* (15 comments, 1 👍)  
  [openclaw/openclaw Issue #78308](https://github.com/openclaw/openclaw/issues/78308)  
  *Underlying need:* MCP tools that mutate external state (email, vault) need the same `/approve` pipeline as shell execs; users demand a standard opt-in mechanism.

- **#113306** [OPEN] *SQLite snapshot restore lacks end-to-end crash and identity guarantees* (13 comments)  
  [openclaw/openclaw Issue #113306](https://github.com/openclaw/openclaw/issues/113306)  
  *Underlying need:* Data safety – snapshot operations can report success without durable directory linkage or proper identity guard, risking silent data loss.

- **#108435** [OPEN] *Gateway fails to start w/ error* (11 comments, 2 👍)  
  [openclaw/openclaw Issue #108435](https://github.com/openclaw/openclaw/issues/108435)  
  *Underlying need:* Regression blocking all gateway operation on 2026.7.1.

- **#67419** [OPEN] *Session context bloat: bootstrap files re-injected every turn* (10 comments, 2 👍)  
  [openclaw/openclaw Issue #67419](https://github.com/openclaw/openclaw/issues/67419)  
  *Underlying need:* Token waste – 20-30% of context consumed by static files re-injected each turn; users want a smarter cache/retention strategy.

## Bugs & Stability
Several critical and high-severity bugs were reported or updated today. Ordered by priority:

| Issue | Priority | Summary | Fix PR? |
|-------|----------|---------|---------|
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | P0 | **Gateway fails to start** on 2026.7.1 (systemd, Ollama, manual launch). Regression. | No linked PR |
| [#109145](https://github.com/openclaw/openclaw/issues/109145) | P0 | **Gateway HTTP server listens but does not accept connections** (v2026.7.1-beta.5). | None |
| [#113466](https://github.com/openclaw/openclaw/issues/113466) | P1 | `/new` and `/reset` **do not actually create a new session** in 2026.7.1-2. | None |
| [#113306](https://github.com/openclaw/openclaw/issues/113306) | P1 | **SQLite snapshot restore lacks crash guarantees** – can report success without durable links, risking data loss. | None |
| [#112423](https://github.com/openclaw/openclaw/issues/112423) | P1 | **Large SQLite transcript cleanup blocks gateway event loop** – archival I/O on main thread. | None |
| [#113315](https://github.com/openclaw/openclaw/issues/113315) | P1 | **Telegram inbound update permanently lost** after offset persistence without dispatch. | None |
| [#112906](https://github.com/openclaw/openclaw/issues/112906) | P2 | **Rich messages regression** – ` ` tags no longer collapse (broken in v2026.7.1). Regression. | None |
| [#95515](https://github.com/openclaw/openclaw/issues/95515) | P0 | **Upgrade 2026.6.8→2026.6.9 corrupts email channel config** with spurious `groupAllowFrom` field. | No linked PR |
| [#112423](https://github.com/openclaw/openclaw/issues/112423) | P1 | **Gateway heap grows to 1073MB+ at idle on macOS** – cron jobs fail silently. | None |

**No fix PRs were found linked to these P0/P1 bugs in the top-30 PR list.** This indicates that maintainers may be focusing on other improvements before addressing these regressions, or the fixes are still in development.

## Feature Requests & Roadmap Signals
High-interest feature requests updated today:

- **#7707** – Memory Trust Tagging by Source (security, 21 comments)  
- **#78308** – Channel-mediated approval for MCP tool calls (security, 15 comments)  
- **#15032** – Per-spawn tool restrictions for sub-agents (security, 7 comments)  
- **#38520** – Pre-compaction agent notification & deferral (reliability, 6 comments)  
- **#12219** – Skill Permission Manifest Standard (`skill.yaml`) (security, 5 comments)  
- **#9016** – Expose OpenRouter usage cost to agent runtime (observability, 6 comments)  
- **#9986** – Trigger model fallback on context length exceeded (reliability, 6 comments)  
- **#10944** – Telegram `parseMode` config (UX, 6 comments)  
- **#8724** – Per-model generation timeout (UX, 6 comments)  
- **#9637** – TUI emoji/unicode accessibility (UX, 6 comments)  
- **#7476** – WhatsApp sticker send support (platform, 6 comments)

**Likely candidates for next minor release:**  
- **#78308** (MCP consent envelope) – already has a pattern test and community consensus, and addresses a current security gap.  
- **#7707** (memory trust tagging) – heavily discussed, but likely requires design approval.  
- **#9016** (cost tracking) – relatively simple to implement and repeatedly requested.  

**Longer-term roadmap signals:**  
- Sandboxing (filesystem, skill permissions) and sub-agent tool restrictions point toward a **least-privilege agent security model** that may span multiple releases.

## User Feedback Summary
- **Pain points:** Users report chronic memory bloat (heap 1073MB+ #87109), session context waste (20-30% tokens, #67419), regressions in basic features like `/new`, rich messages, and gateway startup. Telegram users experience silent message loss (#91564, #113315). Cron jobs can fail silently (#77109) and isolated cron lanes leak (#89766).  
- **Use cases:** Security-conscious users are pushing for memory poisoning protection (trust tagging), MCP tool approval pipelines, and sandboxed file access.  
- **Satisfaction indicators:** Several feature requests received multiple 👍 (#7722 filesystem sandboxing: 4, #10687 dynamic model discovery: 3, #95515 upgrade corruption: 1). However, the large number of open issues and repeated “regression” tags suggest frustration with recent release stability.  
- **Voice of the community:** Users often refer to prior issues (#108435 references earlier similar bugs), indicating a need for more rigorous regression testing before release.

## Backlog Watch
Issues and PRs that remain open for an extended period and lack maintainer attention:

- **#7707** (Memory Trust Tagging, created Feb 3) – needs maintainer review, product decision, security review.  
- **#78308** (MCP tool call approval, created May 6) – similarly blocked on maintainer review.  
- **#67419** (Session bloat, created Apr 15) – marked “needs-maintainer-review” and “recovery-stuck”.  
- **#10687** (Dynamic model discovery, created Feb 6) – tagged “needs-live-repro”, has not progressed.  
- **#15032** (Per-spawn tool restrictions, created Feb 12) – open with no recent maintainer activity.  
- **#38520** (Pre-compaction notification, created Mar 7) – “needs-security-review” and “recovery-stuck”.  
- **#12219** (Skill Permission Manifest, created Feb 9) – “needs-security-review”, open since February.  

- **PR #90831** (Tooltips for Reasoning/Thinking dropdowns, created Jun 6) – stale, still needs proof of real behavior.  
- **PR #111422** (fix(cron): detect `===DONE_ERR===`, Jul 19) – open and waiting for proof.

These items represent **long-unresolved community needs** (especially around security and reliability) that could accelerate churn if left unaddressed.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent
**Date:** 2026-07-26 | **Scope:** Personal AI Assistant / Agent Open-Source Ecosystem

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing a dual dynamic: rapid feature iteration alongside growing pains in stability and security. Both OpenClaw and Hermes Agent serve as core infrastructure projects for building autonomous agents, yet they operate at different scales and maturity levels. The ecosystem is consolidating around three major requirements: **security-by-design** (trust tagging, consent pipelines, sandboxing), **cross-platform reliability** (particularly Windows), and **context efficiency** (token waste, session state consistency). While both projects show high activity, the community is signaling increasing frustration with regressions in stable channels and unaddressed security gaps.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues Updated (24h)** | 341 | 50 |
| **Open Issues** | 241 | 47 |
| **PRs Updated (24h)** | 500 | 50 |
| **PRs Merged/Closed (24h)** | 223 | 12 |
| **New Releases** | None | None |
| **Health Score** | **Moderate** – regressions slowing adoption | **Stable** – Windows regressions cause friction |

**Note:** OpenClaw’s volume is roughly **6–7× higher** than Hermes Agent across all activity metrics, reflecting significantly larger community size and maintenance burden. However, OpenClaw shows a higher ratio of critical (P0/P1) bugs without linked fix PRs, indicating a potential **stability bottleneck**.

---

## 3. OpenClaw’s Position

**Advantages:**
- **Larger community & contributor base** – 341 issues + 500 PRs/day vs. 50 each for Hermes, implying broader testing surface and faster feature velocity when stable.
- **Deeper architectural foundations** – Formalized security proposals (Skill Permission Manifest, Memory Trust Tagging, MCP consent envelopes) indicate a more systematic approach to agent security than Hermes.
- **Token Plan enforcement** (#113976) – Demonstrates tighter integration with model-level constraints, useful for enterprise deployments.

**Technical Approach Differences:**
- OpenClaw is heavier on **structural refactors** (splitting Windows task scheduler, splitting test suites) to reduce technical debt, while Hermes focuses on **incremental UI/UX patches**.
- OpenClaw uses **SQLite snapshots** and a complex gateway architecture; Hermes relies on a lighter **PTY + Node TUI** stack with simpler state management.

**Community Size Comparison:**
- OpenClaw: ~3.4× more issues, ~10× more PRs per day. Lower barrier to entry (more triaged issues) but higher noise ratio.
- Hermes: More focused discussions, higher signal-to-noise, but slower feature delivery.

---

## 4. Shared Technical Focus Areas

| Requirement | Projects | Details |
|-------------|----------|---------|
| **Security consent pipelines** | OpenClaw (#78308), Hermes (#71509) | Both building approval mechanisms for MCP tool calls and delegate credential preservation |
| **Memory/context protection** | OpenClaw (#7707), Hermes (implied) | Trust tagging to prevent poisoning; session context bloat mitigation |
| **Cross-platform (Windows) stability** | OpenClaw (P0 gateway startup), Hermes (P1 boot loop #71226) | Both suffering on Windows; distinct root causes (OpenClaw: systemd/gateway, Hermes: WebSocket/update chain) |
| **Session state reliability** | OpenClaw (#113466, /new fails), Hermes (#62726, cross-tab bleed) | Both have session creation/consistency bugs; user workflows disrupted |
| **Configuration complexity** | OpenClaw (#95515, config corruption), Hermes (#71298, dual providers) | Both plagued by dual-storage or migration issues |

**Key Insight:** Security (consent, trust) and session reliability are the **two biggest cross-project pain points**. Neither project has fully solved them, suggesting an ecosystem-wide opportunity.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Target Users** | Developers, power users, enterprise | End users, tinkerers, desktop-first |
| **Core Use Case** | Agent orchestration, multi-session, MCP tool gateways | Personal desktop assistant, chat + skills |
| **Architecture** | Gateway-centric, SQLite heavy, modular plugin system | PTY-based, browser dashboard, TUI + desktop |
| **Feature Focus** | Security manifests, sandboxing, cost tracking, Token Plan | UI/UX polish, Telegram/LINE integration, composer improvements |
| **Primary Weakness** | Regression-prone stable releases, memory bloat | Windows friction, slower feature velocity, smaller ecosystem |

**Summary:**
- **OpenClaw** = the **systems/security-first** reference implementation for complex agent orchestration.
- **Hermes** = the **UX-first** personal assistant, prioritizing desktop integration and platform connectivity.

---

## 6. Community Momentum & Maturity

| Tier | Project | Characteristics |
|------|---------|-----------------|
| **Tier 1 – Rapid Iteration** | OpenClaw | 500 PRs/day, major structural refactors underway, but **stability regressions** risk alienating users. Mature codebase with active debt reduction. |
| **Tier 2 – Steady Iteration** | Hermes Agent | 50 PRs/day, responsive to Windows bugs (codex fix, composer scope), but slower on backlog. More predictable release cadence. |

**Maturity Assessment:**
- **OpenClaw** is more mature architecally (formal security specs, split modules) but less mature in release quality (P0 regressions not yet patched).
- **Hermes** is less architecturally complex but more **stable in user-facing behavior** (fewer unlinked P0/P1 bugs).

**Trend:** Both projects are **growing**, but OpenClaw risks **churn** (users leaving due to regressions) if hotfix releases aren't shipped soon. Hermes risks **feature fatigue** (users frustrated by Windows-only bugs and slow backlog).

---

## 7. Trend Signals for AI Agent Developers

The community feedback from these two projects surfaces several industry trends:

### 1. Security becomes the #1 differentiator
- **Memory trust tagging**, **MCP consent envelopes**, **skill manifests**, and **credential preservation** are not edge cases—they are *baseline requirements*. Any agent framework that ships without these will face community pushback.

### 2. Windows is a first-class platform
- Both projects have **critical Windows-specific bugs** (boot loops, FileNotFound errors, WebSocket disconnects). Developers targeting enterprise must invest in Windows parity; the signal is loud.

### 3. Context budgeting is non-negotiable
- OpenClaw’s #67419 (20-30% token waste on static files) and Hermes’s implicit context issues signal that **token efficiency** is the next performance bottleneck for agent scaling. Caching, deduplication, and progressive context injection are must-haves.

### 4. Session state is the new "state management"
- Multi-tab bleed, `/new` failures, and context length mismatches show that **session identity and lifecycle handling** are poorly understood patterns in the new agent paradigm. This is a white-space opportunity for frameworks.

### 5. Dual config paths kill UX
- OpenClaw (#95515) and Hermes (#71298) both have **conflicting configuration sources** (email channels, providers vs. custom_providers). Unified configuration APIs (YAML-based, versioned, validated) are an immediate UX win.

### Value for Developers:
- **If building an agent product**, prioritize **session reliability** and **consent UX** over advanced features.
- **If contributing to either project**, focus on **Windows compatibility** and **config simplification**—these are high-impact, low-competition areas.
- **If choosing a framework**, OpenClaw offers deeper security abstractions but higher regression risk; Hermes offers simpler deployment but slower innovation. Hybrid approaches (e.g., OpenClaw backend + Hermes-style desktop UI) remain unexploited.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-26

## 1. Today's Overview

Hermes Agent saw a high level of activity on 2026-07-26, with **50 issues** and **50 pull requests** updated in the past 24 hours. Among those, only **3 issues were closed** and **12 PRs were merged/closed**, indicating a day dominated by active triage and ongoing development rather than batch releases (no new releases were published). The project continues to attract significant community engagement, particularly around stability concerns on **Windows**, session-state consistency, and credential/provider configuration. The volume of open issues (47) relative to closed ones highlights an increasing backlog, though the steady stream of fix PRs suggests a responsive maintainer team.

## 2. Releases

*None — no new versions were published today.*

## 3. Project Progress

Today’s merged/closed PRs (12 total) addressed several critical areas:

- **Dashboard stability** – PR [#71625](https://github.com/nousresearch/hermes-agent/pull/71625) fixed a startup failure where the browser dashboard reported “Chat unavailable: 1” when the embedded PTY couldn’t prepare its Node TUI runtime.
- **Windows compatibility** – PR [#71696](https://github.com/nousresearch/hermes-agent/pull/71696) resolved a `FileNotFoundError` when launching `codex` on Windows (missing `.exe` suffix), and PR [#71692](https://github.com/nousresearch/hermes-agent/pull/71692) removed a misleading `GetNativeSystemInfo` probe that caused trouble under WoA emulation.
- **Session-consistent model picker** – PR [#71601](https://github.com/nousresearch/hermes-agent/pull/71601) kept the Desktop model picker checkmark aligned with the live session state, preventing stale model indicators.
- **Cron/failure classification** – PR [#71494](https://github.com/nousresearch/hermes-agent/pull/71494) fixed misleading provider-error summaries for script-only cron jobs (no agent). PR [#70977](https://github.com/nousresearch/hermes-agent/pull/70977) (still open) proposes a similar fix.
- **Delegate credential preservation** – PR [#71509](https://github.com/nousresearch/hermes-agent/pull/71509) preserved a parent’s fixed proxy credential when delegating to subagents, preventing unauthorized fallback to provider-default pools.
- **Desktop UI polish** – PR [#71688](https://github.com/nousresearch/hermes-agent/pull/71688) clarified the inherited profile gateway description on Desktop, and PR [#71664](https://github.com/nousresearch/hermes-agent/pull/71664) made skills referenceable anywhere in the Desktop composer (not just at position 0). A TUI parity PR [#71697](https://github.com/nousresearch/hermes-agent/pull/71697) was opened for the same fix.

## 4. Community Hot Topics

The most discussed issues this week revolve around **time awareness**, **rendering bugs**, and **session state**:

- **Turn-level live time context** – Issue [#10421](https://github.com/nousresearch/hermes-agent/issues/10421) (13 comments, 9 👍) requests reliable “now” / “today” awareness at each turn instead of only session-level. This is a long-standing usability gap; many workflows (scheduling, day-aware chat) are blocked without it.
- **MarkdownV2 bullet list breakage on Telegram** – Issue [#6388](https://github.com/nousresearch/hermes-agent/issues/6388) (7 comments) describes how LLM-generated `- item` lists become `\-` after Telegram MarkdownV2 escaping. A root cause in `gateway/platforms/…` has been identified, but no fix PR yet.
- **Dashboard cross-tab session bleed + /new hang** – Issue [#62726](https://github.com/nousresearch/hermes-agent/issues/62726) (7 comments) reports two correlated bugs: session content leaking between browser tabs and `/new` commands requiring a full container restart. This is a high-impact usability bug for multi-tab users.
- **Providers vs. custom_providers dual storage** – Issue [#71298](https://github.com/nousresearch/hermes-agent/issues/71298) (6 comments) highlights a configuration mismatch between CLI and Desktop GUI when using both `providers` and `custom_providers`. The discrepancy leads to inconsistent model version information and profile confusion.
- **Desktop Windows boot loop** – Issue [#71226](https://github.com/nousresearch/hermes-agent/issues/71226) (5 comments, P1) describes a catastrophic failure where Hermes Desktop on Windows 11 enters a reset cycle after a recent update. No immediate fix merged, but a PR [#71692](https://github.com/nousresearch/hermes-agent/pull/71692) addresses a related Windows update probe that may be connected.

## 5. Bugs & Stability

Several high-severity bugs were reported or updated today; fixes are in progress for many.

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **P1** | [#71226](https://github.com/nousresearch/hermes-agent/issues/71226) | Desktop boot loop on Windows: WebSocket connects then immediately disconnects, triggering renderer reset cycle | No direct fix yet; related PR [#71692](https://github.com/nousresearch/hermes-agent/pull/71692) addresses a probe that may contribute |
| **P2** | [#62726](https://github.com/nousresearch/hermes-agent/issues/62726) | Dashboard cross-tab session bleed + `/new` hang requiring full restart | No fix PR |
| **P2** | [#71298](https://github.com/nousresearch/hermes-agent/issues/71298) | Providers vs. custom_providers dual storage causes CLI/GUI mismatch + stuck model version | No fix PR |
| **P2** | [#63177](https://github.com/nousresearch/hermes-agent/issues/63177) | `search_files` returns 0 results on Windows with absolute paths (rg + MSYS_NO_PATHCONV conflict) | No fix PR |
| **P2** | [#67140](https://github.com/nousresearch/hermes-agent/issues/67140) | Background skill-review prompt conflicts with shared curator write guard | No fix PR |
| **P2** | [#71491](https://github.com/nousresearch/hermes-agent/issues/71491) | Hermes Cloud connection mode on Windows: desktop never initiates sign-in, loops on 401 no_cookie | No fix PR |
| **P2** | [#63717](https://github.com/nousresearch/hermes-agent/issues/63717) | Comprehensive Windows update failure chain (7 correlated root causes) | PR [#71692](https://github.com/nousresearch/hermes-agent/pull/71692) addresses one cause |
| **P2** | [#48659](https://github.com/nousresearch/hermes-agent/issues/48659) | Photon sidecar files missing from wheel/sdist (install-sidecar fails) | No fix PR |
| **P3** | [#65123](https://github.com/nousresearch/hermes-agent/issues/65123) (CLOSED) | UTF-8 BOM in `.env` silently drops first key | Closed as fixed? No details |
| **P3** | [#45448](https://github.com/nousresearch/hermes-agent/issues/45448) | Dashboard Channels page doesn't show env-var configured platforms | No fix PR |

**Notable regressions:** The Windows boot loop (#71226) appears to be a regression between commits `2c1a38a` (good) and `07e97d2` (bad) – bisect is needed.

## 6. Feature Requests & Roadmap Signals

The community continues to push for improvements in **context awareness**, **platform integration**, and **skill management**:

- **Turn-level time context** (#10421) – a clear user need that is likely to be implemented soon given its popularity (9 👍) and the explicit feature request.
- **Curator adoption path for legacy local skills** (#67139) – would allow users to opt unmanaged skills into curator management. Duplicate status may indicate maintainers are considering it.
- **LINE budget-aware slow delivery** (PR [#71656](https://github.com/nousresearch/hermes-agent/pull/71656)) – adds `slow_response_mode: auto_push` for LINE and respects monthly quotas. Could ship in next release.
- **Skills referenceable anywhere in composer** (PRs [#71664](https://github.com/nousresearch/hermes-agent/pull/71664) and [#71697](https://github.com/nousresearch/hermes-agent/pull/71697)) – already merged for Desktop, TUI in progress, expected in next version.
- **Post-auth message hooks** (PR [#71541](https://github.com/nousresearch/hermes-agent/pull/71541)) – generic hooks for Discord/Telegram ingress, enabling custom logging or delivery logic.
- **ai& provider** (PR [#71690](https://github.com/nousresearch/hermes-agent/pull/71690)) – new bundled provider for open frontier models via OpenAI-compatible endpoint.
- **Local STT documentation** (#56989) – users want fully local voice transcription (MLX + CUDA) to avoid external APIs.
- **Dependency update** (PR [#71694](https://github.com/nousresearch/hermes-agent/pull/71694)) – routine npm update.

**Prediction for next version:** Turn-level time context (#10421) and the composer skill fixes are strong candidates, along with LINE slow delivery and the ai& provider integration.

## 7. User Feedback Summary

Real user pain points this week:

- **Windows users frustrated**: Multiple reports of Desktop boot loops, update failures, and platform-specific bugs (codex launch, `search_files`, `GetNativeSystemInfo` misbehavior). Windows is clearly the platform with the most friction.
- **Configuration confusion**: Users report difficulty with dual `providers`/`custom_providers` storage (#71298), silent BOM key drops (#65123), and ACP model/provider flag routing (#27186). These suggest the configuration system is overcomplicated and error-prone.
- **Multi-tab workflow broken**: The cross-tab session bleed (#62726) disrupts anyone using multiple browser tabs or windows simultaneously – a common power-user scenario.
- **IMAP/Gmail users impacted**: The Email gateway marking messages as read (#42997) is a significant annoyance for email integration users.
- **iMessage streaming artifacts**: Photon/iMessage streaming still shows white squares (#49793), affecting user visual experience.
- **Positive signals**: The quick response to fix the Windows codex launch (#71696) and composer skill scope (#71664) shows the team listens to urgent bug reports. The addition of new providers (ai&) broadens model choice.

## 8. Backlog Watch

Several important issues have remained open for extended periods without maintainer response or progress:

| Issue | Created | Comments | Summary | Note |
|-------|---------|----------|---------|------|
| [#20721](https://github.com/nousresearch/hermes-agent/issues/20721) | 2026-05-06 | 1 | Skill prompting too strict, causes excessive re-reads (P2) | Needs triage; affects efficiency for GPT-5.5 users |
| [#27186](https://github.com/nousresearch/hermes-agent/issues/27186) | 2026-05-17 | 2 | ACP `/model --provider <named custom provider>` still re-routed by model auto-detection (P2) | Long-standing control override bug |
| [#31043](https://github.com/nousresearch/hermes-agent/issues/31043) | 2026-05-23 | 4 | CLI `/new` does not refresh `context_compressor.context_length` after provider config changes (P3) | Session state lag persists |
| [#11515](https://github.com/nousresearch/hermes-agent/issues/11515) | 2026-04-17 | 2 | ACP session cwd used for tool execution but not for project context discovery (P2) | Inconsistency in ACP |
| [#42997](https://github.com/nousresearch/hermes-agent/issues/42997) | 2026-06-09 | 3 | Email gateway IMAP polling marks unread messages as read (P3) | Gmail users affected |
| [#52581](https://github.com/nousresearch/hermes-agent/issues/52581) | 2026-06-25 | 1 | Relay passthrough_forward buffered deliveries never acked (duplicate agent turns on reconnect) (P3) | Potentially serious for delivery reliability |

These issues deserve maintainer attention to prevent them from stalling community trust in the project’s responsiveness.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*