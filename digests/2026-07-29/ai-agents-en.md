# OpenClaw Ecosystem Digest 2026-07-29

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-29 02:10 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-07-29

## 1. Today’s Overview
The project saw **very high activity**: 500 issues and 500 pull requests were updated in the last 24 hours, with 267 PRs merged/closed and 275 issues resolved. A new beta release **v2026.7.2-beta.5** shipped with major state‑safety improvements (quarantine store, crash‑recoverable SQLite snapshots, schema‑upgrade data‑loss protection). Despite this, several **P0/P1 blockers** remain open—most critically a memory leak that can exhaust 15.5 GB of RAM over days. Community engagement is strong: the oldest open feature request (#75, Linux/Windows apps) has 115 comments and 80 👍, indicating sustained demand for cross‑platform support.

---

## 2. Releases
**New release:** [v2026.7.2-beta.5](https://github.com/openclaw/openclaw/releases/tag/v2026.7.2-beta.5)  
**Highlights (2026.7.2):**
- **State safety and recovery**: quarantine store for corrupt databases, crash‑recoverable SQLite snapshots, durable filesystem publication, rejection of schema‑upgrade data loss, and rollback‑writer snapshot recovery.
- No explicit breaking changes or migration notes were announced; the release is labelled beta.

*Note: No other new versions were released today.*

---

## 3. Project Progress (Merged/Closed PRs Today)
267 PRs were merged or closed. Notable merges include:

- [#115483](https://github.com/openclaw/openclaw/pull/115483) – Refactor: remove duplicate runtime, plugin, and chat paths (size XL, by maintainer steipete).
- [#115481](https://github.com/openclaw/openclaw/pull/115481) – Fix sandbox provisioning failures exhausting model fallbacks.
- [#115480](https://github.com/openclaw/openclaw/pull/115480) – Hide credential profiles from model labels in Control UI.
- [#115477](https://github.com/openclaw/openclaw/pull/115477) – Preview model picker interactions live (UI responsiveness fix).
- [#115472](https://github.com/openclaw/openclaw/pull/115472) – Keep microphone picker background neutral when Talk is unavailable.
- [#115422](https://github.com/openclaw/openclaw/pull/115422) – Restore subagent completion delivery on CLI runtimes.
- [#114441](https://github.com/openclaw/openclaw/pull/114441) – Fix completed cron jobs stuck behind slower batch runs.
- [#114439](https://github.com/openclaw/openclaw/pull/114439) – Keep agent selection aligned across session switches (size XL).
- [#114436](https://github.com/openclaw/openclaw/pull/114436) – Derive agent core‑files list from canonical workspace set.

These address performance, UI consistency, sandbox reliability, and subagent lifecycle bugs.

---

## 4. Community Hot Topics (Highest Engagement)

| Issue | Title | Comments | 👍 | Underlying Need |
|-------|-------|----------|----|----------------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | Linux/Windows Clawdbot Apps | 115 | 80 | Native clients for non‑Apple platforms; feature parity with macOS |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | Memory Trust Tagging by Source | 23 | 0 | Protect against memory‑poisoning attacks from untrusted content |
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | Gateway Memory Leak (P0) | 20 | 1 | Severe stability: RSS grows from 350 MB to 15.5 GB |
| [#96857](https://github.com/openclaw/openclaw/issues/96857) | Tool text outputs become “(see attached image)” placeholders (closed) | 15 | 4 | Agent blindness to normal command output |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | Masked Secrets (P1) | 14 | 4 | Prevent credential leaks and prompt‑injection extraction |
| [#115326](https://github.com/openclaw/openclaw/issues/115326) | Crash‑loop breaker persists after recovery (new today) | 12 | 0 | Discord/WhatsApp permanently suppressed; documented recovery fails |
| [#11665](https://github.com/openclaw/openclaw/issues/11665) | Webhook sessions reuse (multi‑turn support) | 11 | 0 | SessionKey does not work as documented |

The community is most vocal about **cross‑platform support**, **security hardening**, and **core stability** (memory leaks, crash loops). The memory leak (#91588) is a P0 that directly impacts production deployments.

---

## 5. Bugs & Stability

### Critical / P0
- **[#91588](https://github.com/openclaw/openclaw/issues/91588)** – Gateway memory leak: RSS from 350 MB to 15.5 GB over days → OOM crashes. *No fix PR yet*; still open.
- **[#115326](https://github.com/openclaw/openclaw/issues/115326)** – Crash‑loop breaker permanently suppresses Discord/WhatsApp; documented recovery (`channels.start`) fails with WebSocket 1006. *Opened today, no fix PR yet.*

### Severe / P1
- **[#113434](https://github.com/openclaw/openclaw/issues/113434)** – Codex `sessions.reset` reuses retired session ID; file scans exhaust Gateway RAM. *Open.*
- **[#78562](https://github.com/openclaw/openclaw/issues/78562)** – Repeated tool‑loop context overflows cause successive auto‑compactions (v2026.5.5). *Open.*
- **[#77012](https://github.com/openclaw/openclaw/issues/77012)** – WebChat session transcript overwritten every turn (regression). *Closed today; likely fixed.*
- **[#102268](https://github.com/openclaw/openclaw/issues/102268)** – Silent empty tool results after large tool result in Sonnet 5. *Open.*
- **[#114137](https://github.com/openclaw/openclaw/issues/114137)** – Visible channel turns dispatch with no queued reply; final text never delivered. *Open.*

### Regressions
- [#111519](https://github.com/openclaw/openclaw/issues/111519) – Telegram DM replies fall back after stale DM‑scope cleanup (beta.3 regression). *Closed? Actually open but marked with fix PR.*
- [#115001](https://github.com/openclaw/openclaw/issues/115001) – Hybrid memory search returns spurious 1.0 similarity scores (FTS LIKE‑fallback bug). *Open, filed today.*
- [#74378](https://github.com/openclaw/openclaw/issues/74378) – CLI commands stay alive as node.exe processes on Windows. *Open.*

Several P1 issues remain without associated fix PRs, suggesting maintainer bandwidth is stretched.

---

## 6. Feature Requests & Roadmap Signals
Top user‑requested features that are likely to land in the next release(s):

- **[Masked Secrets](https://github.com/openclaw/openclaw/issues/10659)** (P1) – Prevent agents from seeing raw API keys. High security impact; raised by multiple users.
- **[Denylist for exec‑approvals](https://github.com/openclaw/openclaw/issues/6615)** – Complement existing allowlist. 8 👍, clear use case.
- **[Filesystem sandboxing config](https://github.com/openclaw/openclaw/issues/7722)** – `tools.fileAccess` restrictions. 4 👍.
- **[Trigger model fallback on context length exceeded](https://github.com/openclaw/openclaw/issues/9986)** – Currently only API errors trigger fallback.
- **[Mid‑stream message injection](https://github.com/openclaw/openclaw/issues/10960)** – “Soft steer” during model generation.
- **[Dynamic model discovery for OpenRouter](https://github.com/openclaw/openclaw/issues/10687)** – Needed for fast‑moving catalogs.

Additionally, the long‑standing [#75](https://github.com/openclaw/openclaw/issues/75) (Linux/Windows apps) continues to generate strong demand but has not seen recent activity from maintainers.

**Predictions:** The next minor version (2026.7.3 or 2026.8) will likely include Masked Secrets, exec‑approval denylist, and possibly dynamic model discovery, as these have linked PRs or maintainer review.

---

## 7. User Feedback Summary

### Pain Points
- **Stability:** Memory leaks and crash‑loops are the top frustrations. One user reported “Our agent’s main session silently rolled over on three occasions” ([#106403](https://github.com/openclaw/openclaw/issues/106403)).
- **Missing features:** Linux/Windows apps, Control UI regression (missing Skill Proposals/Dreaming pages), sticker support in WhatsApp.
- **Regressions in beta:** Telegram DM loss, WebChat transcript overwrite, sandbox provisioning failures.
- **LLM integration:** Local reasoning models aborted due to idle timeout, llama.cpp tool‑calling broken by cron regex.

### Positive Sentiment
- User in [#73537](https://github.com/openclaw/openclaw/issues/73537) says: “We've been running it as a family and business assistant … it has genuinely become part of our daily workflow. Really appreciate the work you and the team put into this.”
- Several PRs are merged quickly by maintainers, showing responsiveness.

### Overall Sentiment
The user base is enthusiastic but growing increasingly vocal about reliability and missing cross‑platform support. The beta.5 release addresses data safety, but production users are still encountering crash‑loop and memory issues.

---

## 8. Backlog Watch
Issues and PRs that have been open for months without resolution, needing maintainer attention:

| Item | Created | Age | Status | Notes |
|------|---------|-----|--------|-------|
| [#75](https://github.com/openclaw/openclaw/issues/75) – Linux/Windows apps | Jan 2026 | ~7 months | Open, P2, 115 comments | No assignee; clawsweeper labels indicate stuck review |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) – Memory trust tagging | Feb 2026 | ~6 months | Open, P2 | Needs product decision & security review |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) – Masked secrets | Feb 2026 | ~6 months | Open, P1 | Linked PR open; still needs maintainer review |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) – Exec‑approval denylist | Feb 2026 | ~6 months | Open, P2 | Linked PR open; awaits review |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) – Filesystem sandboxing | Feb 2026 | ~6 months | Open, P2 | Needs maintainer review & live repro |
| [#8299](https://github.com/openclaw/openclaw/issues/8299) – Suppress sub‑agent announce | Feb 2026 | ~6 months | Open, P2 | Stuck; needs product decision |
| [#9986](https://github.com/openclaw/openclaw/issues/9986) – Fallback on context length | Feb 2026 | ~6 months | Open, P2 | Needs product decision |
| [#75165](https://github.com/openclaw/openclaw/pull/75165) – Composable termination algebra | Apr 2026 | ~4 months | Open, P2 | “Ready for maintainer look” but not merged |
| [#95847](https://github.com/openclaw/openclaw/pull/95847) – Subagent completion credit | Jun 2026 | ~1 month | Open, P1 | Needs proof; high merge risk |
| [#114151](https://github.com/openclaw/openclaw/pull/114151) – Per-turn tool narrowing | Jul 2026 | 3 days | Open, P2 | Needs proof |

The backlog shows a cluster of **security‑related enhancements** (memory tagging, masked secrets, sandboxing, denylist) that are all stalled on maintainer review or product decisions. These have been open for over six months and represent a significant gap in the security posture. The maintainer team may need to prioritize these to reduce risk surface.

---

*Generated from GitHub data on 2026-07-29. All links point to the official OpenClaw repository: [github.com/openclaw/openclaw](https://github.com/openclaw/openclaw).*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs Hermes Agent

## Ecosystem Overview

The open-source personal AI assistant ecosystem in mid-2026 is characterized by rapid iteration and maturing production requirements. Both OpenClaw and Hermes Agent demonstrate strong community engagement, but reveal different phases of the lifecycle: OpenClaw is stabilizing a core reference architecture with state-safety guarantees, while Hermes Agent is expanding feature surface area (OAuth, RBAC, undo/redo) with heavier triage burdens. Across both projects, users consistently demand cross-platform support, memory reliability, and security hardening — indicating that the ecosystem is moving from experimental deployment to production-grade expectations. Maintainer bandwidth appears stretched in both communities, with critical stability bugs persisting despite high commit activity.

## Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues updated (24h)** | 500 (275 resolved) | 50 (0 resolved) |
| **PRs updated (24h)** | 500 (267 merged/closed) | 50 (8 merged/closed) |
| **Current release** | v2026.7.2-beta.5 (today) | v0.8.x (no new release) |
| **PR merge rate** | ~53% | ~16% |
| **P0/P1 open bugs** | 10+ (1 P0 memory leak, multiple P1s) | 12+ (all P2, but high severity) |
| **Top community issue engagement** | 115 comments (cross-platform), 80 👍 | 17 comments (RBAC), 10 👍 |
| **Health score (qualitative)** | 7/10 — high throughput but critical P0 open | 5/10 — low closure rate, no bug fixes resolved |

## OpenClaw's Position

**Advantages over peer:**
- **Scale and velocity:** 10× the issue/PR throughput of Hermes Agent. 267 PRs merged vs 8 in the same 24-hour window.
- **Release discipline:** Ships regular beta releases with clear changelogs and safety features (quarantine store, crash-recoverable SQLite, schema-upgrade data-loss protection).
- **Production-oriented:** State-safety infrastructure (rollback-writer snapshots, durable publication) indicates focus on deployment reliability.
- **Community size:** The oldest feature request (#75, Linux/Windows apps) has 115 comments and 80 👍 — far surpassing any single Hermes discussion.

**Technical approach differences:**
- OpenClaw follows a **core-reference architecture** with a single main repository (OpenClaw/openclaw) and centralized governance.
- Heavier emphasis on **state integrity and crash recovery** — Hermes has no equivalent of the quarantine store or schema-upgrade rejection.
- **Memory leak severity higher** (P0, 15.5 GB growth) but being actively tracked with detailed analysis; Hermes has multiple memory-related bugs (process spawn leak, session growth) but none yet escalated to P0.

**Community size comparison:**
- OpenClaw’s top issue engagement (115 comments) is 6.8× Hermes’s top (17 comments).
- OpenClaw’s feature request 👍 count (80) is 8× Hermes’s top (10 👍).
- Indicates significantly larger user base and/or more vocal community.

## Shared Technical Focus Areas

Requirements emerging across both projects (all apply to both unless noted):

| Priority | Requirement | OpenClaw Signal | Hermes Signal |
|----------|-------------|-----------------|---------------|
| **Critical** | Memory leak / unbounded growth fixes | P0 gateway leak, session RAM exhaustion | Desktop process spawn leak, session turn accumulation |
| **Critical** | Crash-loop recovery & circuit breaker | P0 #115326 — permanent Discord/WhatsApp suppression | P2 #73163 — WSL VM crash, P2 #73779 — Feishu WebSocket crash |
| **High** | Cross-platform support (Linux/Windows) | #75 — 115 comments, 80 👍 | #70544 — Windows Smart App Control block |
| **High** | Security hardening: credential masking | #10659 — masked secrets (P1) | #26977 — prompt injection scanning misses |
| **High** | Session / memory management reliability | #113434 — session ID reuse, webhook sessions | #73297 — memory rollback after /reset, #73775 — session poison |
| **Medium** | Tool calling reliability | #102268 — silent empty tool results | #8993 — unstable tool calling, hallucination |
| **Medium** | Exec-approval and sandboxing | #6615 denylist, #7722 filesystem sandboxing | RBAC (#527) overlaps in access control |
| **Medium** | UI/UX polish for multi-turn | #115477 — model picker live preview | #59308 — archive shortcut, #41302 — dual-column chat |

**Key insight:** No single project leads on all shared requirements. OpenClaw is stronger on state safety and recovery; Hermes is earlier on RBAC and UI customization. Both need memory management and cross-platform support.

## Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Core strength** | State safety, crash recovery, data durability | Feature velocity, platform integration breadth (Telegram, Feishu, iMessage, Gemini) |
| **Target user** | Production operators, family/business assistants | Advanced power users, multi-platform deployers |
| **Architecture** | Centralized core reference, heavy on SQLite/FTS | Distributed: desktop app, gateway, sidecar services |
| **Release cadence** | Regular betas with changelogs | Sporadic — last release v0.8.x (no date) |
| **Security posture** | Masked secrets, sandboxing in backlog | RBAC in discussion, trust tagging not started |
| **Community engagement** | High volume on old issues (Linux/Windows veteran demand) | High volume on fresh bugs, lower closure rate |
| **Unique features** | Quarantine store, schema-upgrade protection | Gemini OAuth, undo/redo, iMessage integration, Kanban dashboards |
| **Platform focus** | macOS-centric with Linux/Windows gap | Cross-platform from start (WSL, Podman, Windows, macOS) |

OpenClaw is the **stability-and-safety reference**; Hermes is the **feature-expansion innovator**. Each fills a different ecosystem niche: OpenClaw for those needing a reliable core agent, Hermes for those wanting broad platform reach and cutting-edge integrations.

## Community Momentum & Maturity

**Tier 1: Rapid iteration with stabilization focus**
- **OpenClaw** — Very high activity, regular releases, but major open P0/P1 bugs suggest maintenance is outpacing QA. The 267 PRs merged today indicate significant contributions, but the memory leak (#91588) and crash-loop blocker (#115326) remain unresolved, undermining reliability gains.

**Tier 2: Active triage with feature expansion**
- **Hermes Agent** — Moderate activity, low bug-fix resolution (0 issues closed, 8 PRs merged), heavy triage load. Bug counts indicate many users running into regressions (tool calling, session management, platform-specific crashes). No new release today suggests maintainers are in a development sprint rather than stabilization mode.

**Maturity assessment:**
- OpenClaw is more **mature** (state-safety infrastructure, beta releases, larger community).
- Hermes Agent is more **volatile** (higher bug resolve rate required, earlier in lifecycle).

## Trend Signals

From community feedback across both projects, the following industry trends are emerging:

1. **Cross-platform is not optional.** Both projects see strong demand for Linux/Windows support (OpenClaw #75; Hermes #70544, #73163). The ecosystem is leaving pure-macOS roots.

2. **Memory management is the #1 production blocker.** Leaks, unbounded growth, and session poisoning are recurring across both projects. Developers scaling from single-user to multi-session deployments are hitting resource exhaustion.

3. **Security hardening is moving from nice-to-have to must-have.** Masked secrets (#10659), RBAC (#527), exec-approval denylists (#6615), and trust tagging (#7707) all reflect a user base that has moved past prototyping to real-world credential handling.

4. **Tool-calling reliability remains unsolved.** Both projects report hallucinations, empty results, and retry loops (#8993, #102268, #73388). This is a fundamental LLM integration challenge that no open-source agent has fully addressed.

5. **State safety features are becoming a differentiation point.** OpenClaw’s quarantine store and crash-recoverable snapshots signal that users care about data integrity during crashes — a concern that will grow as agents become always-on.

6. **Platform-specific integration bugs are rising.** WSL crash (#73163), Windows Smart App Control (#70544), Feishu WebSocket crash (#73779), Telegram session growth (#73775) — as agents expand to more platforms, the surface area for edge cases grows faster than maintainer capacity.

**Value for AI agent developers:** Focus on memory management, cross-platform compatibility, and secret masking as the top three infrastructure investments. Tool-calling reliability is the highest-impact user experience gap. State safety (crash recovery, data durability) is emerging as a competitive differentiator for production deployments.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-29

## Today's Overview

Hermes Agent saw high community activity over the last 24 hours with 50 active issues and 50 PRs receiving updates. Notably, **all 50 issues remain open** (no resolved bugs), and **8 out of 50 PRs were merged or closed** — a modest closure rate of 16%. No new releases were cut. The project is in a **heavy triage and development phase**, with users reporting critical stability regressions (unbounded process growth, session memory rollback, platform-specific crashes) while contributors push forward feature branches (RBAC, undo/redo, Gemini OAuth, local iMessage). The volume of open items and the presence of several high-severity bugs suggest maintainers are stretched, but the community is actively engaged in both reporting and fixing.

## Releases

None over the reporting period.

## Project Progress

**8 pull requests were merged or closed today.** The top two by engagement were:
- **#73780 (CLOSED)** — `fmt(js): npm run fix auto-fix` — auto-generated formatting clean-up, squash-merged after CI pass.
- **#73698 (CLOSED)** — `perf(desktop): kill sidebar + overlay render churn from hot store subscriptions` — a performance improvement for desktop rendering, merged after addressing three independent churn sources.

Other closed PRs (not shown in top 20) likely include minor fixes and documentation updates. No major feature PRs were merged.

## Community Hot Topics

The most active discussions, ranked by comment count:

| Issue # | Title (abbreviated) | Comments | 👍 | Link |
|---------|---------------------|----------|---|------|
| #527 | Feature: Gateway Permission Tiers — RBAC (Owner/Admin/User/Guest) | 17 | 10 | [Issue #527](https://github.com/NousResearch/hermes-agent/issues/527) |
| #58619 | Bug: Hermes Desktop spawns unbounded serve processes on reconnection | 6 | 0 | [Issue #58619](https://github.com/NousResearch/hermes-agent/issues/58619) |
| #8993 | Bug: Tool calling unstable / frequent hallucination and empty responses (v0.8.0) | 4 | 3 | [Issue #8993](https://github.com/NousResearch/hermes-agent/issues/8993) |
| #62975 | Bug: Node sidecar dep (NPM) error on Podman install | 4 | 0 | [Issue #62975](https://github.com/NousResearch/hermes-agent/issues/62975) |
| #26977 | Bug: Context and skill scanners miss multi-word instruction-override variants | 3 | 0 | [Issue #26977](https://github.com/NousResearch/hermes-agent/issues/26977) |
| #73163 | Bug: `_build_wsl_interop_paths` scrapes all /mnt/ paths → Plan 9 overload → WSL VM crash | 3 | 0 | [Issue #73163](https://github.com/NousResearch/hermes-agent/issues/73163) |
| #46917 | Bug: Beings cannot respond with silence; forced response even when zero output desired | 3 | 0 | [Issue #46917](https://github.com/NousResearch/hermes-agent/issues/46917) |

**Underlying needs:** The community is demanding **stability and configurability** — granular access control (RBAC), reliable tool calling, install compatibility (Podman, WSL), and better handling of edge cases (silence, prompt injection). The high 👍 count on #527 indicates strong desire for multi-role gateway permissions.

## Bugs & Stability

Several critical and high-priority bugs were reported or updated today. **No fix PRs are yet linked to these issues.** Ordered by severity (P2 first):

- **P2 — #58619**: Hermes Desktop spawns unbounded `serve` processes on reconnection; old processes are never cleaned up. With sustained API errors, processes accumulate at ~1 per 15–30 minutes. **Potential resource exhaustion.**
- **P2 — #73163**: `_build_wsl_interop_paths` scrapes all `/mnt/` paths on WSL, causing Plan 9 filesystem overload and VM crash. Root cause identified with AI assistance; fix suggested.
- **P2 — #73368**: `hermes status` on macOS does not warn when launchd gateway service is unloaded, leading to silent downtime.
- **P2 — #73297**: Memory rollback after `/reset` — FTS write not flushed before session invalidation; agent loads outdated memory.
- **P2 — #73388**: Agent repeatedly retries `tool_search`/`tool_describe` on non-deferred MCP tools instead of calling them directly.
- **P2 — #73775** (new today): Long-lived Telegram sessions grow unbounded (353+ turns) with no rotation, eventually poisoning every request. **Session management failure.**
- **P2 — #73777** (new today): Retry loop treats empty content from Anthropic API as retryable, burning 35–40 seconds per occurrence with no diagnostic.
- **P2 — #73779** (new today): Feishu WebSocket receive loop crashes with `Future attached to a different loop` in multiplex mode; gateway silently stops receiving.
- **P2 — #46917**: Forced response when zero output is desired – beings cannot remain silent.
- **P2 — #70153**: Persisted `/model` override rehydrates wrong `api_mode` after gateway restart (wrong client type for opencode-go models).

**P3 bugs also updated**: #62975 (Node sidecar Podman), #26977 (prompt injection scanning), #21685 (provider plugin integration gaps), #71585 (MCP guardrail never fires), #70236 (preview URL error), #70544 (Windows Smart App Control block), #43129 (Langfuse zero cost), #6212 (Telegram dumps context on fresh start), #26714 (Telegram cron context injection), #5214 (locked config.yaml handling), #69905 (custom provider /models probe hangs on 401).

## Feature Requests & Roadmap Signals

Features requested or advanced via PRs:

- **#527** — RBAC for gateway platforms (Owner/Admin/User/Guest). Likely to be prioritized given community interest.
- **#59308** — Keyboard shortcut for archiving sessions in Desktop.
- **#41302** — Dual-column chat bubble layout toggle.
- **#33852** — Kanban dashboard deep links for tasks.
- **#8714** — Configurable Python interpreter for cron pre-scripts.
- **#7344** — Expose live agent context to plugin tool handlers.
- **#15793** — AI assistant for Hermes documentation.

**Active PRs hinting at next version:**
- **#71473** — Google Gemini OAuth provider with device-code login (P3 feature).
- **#47017** — Reversible half-turn `/undo` + `/redo` across CLI, gateway, TUI (P3, long open).
- **#22037** — `hermes update` reconciling local branches (install/update area).
- **#33302** — Suggest next goals in default SOUL profile.
- **#56023** — Local iMessage mode for Photon platform.
- **#73559** — Terminal webhook delivery metadata.
- **#62866** — Support `local_server` STT provider.
- **#10635** — Unblock `execute_code` for subagents.

**Prediction for next release (v0.8.x / v0.9.0):** Expect inclusion of Gemini OAuth, local iMessage, `/undo`/`/redo`, and critical bug fixes around session management and tool calling reliability. RBAC is likely further out but gaining momentum.

## User Feedback Summary

**Common pain points:**
- “Tool calling unstable” (#8993) — v0.8.0 regression causing hallucinations and empty responses; users frustrated with web_search and FireCrawl.
- “Process leak in Desktop” (#58619) — reconnection logic spawns processes unbounded; heavy API usage worsens.
- “Silence not respected” (#46917) — users want agents to truly remain silent when instructed.
- “Podman install breaks” (#62975) — permissions errors on Node sidecar despite SELinux disabled.
- “Memory rollback after reset” (#73297) — Telegram users losing recent memory due to flush timing.
- “Session grows forever” (#73775) — 24/7 Telegram deployment hit 353 turns; every subsequent request poisoned.
- “Documentation is thorough but hard to navigate” (#15793) — community requests an AI assistant for docs to speed up lookups.

**Satisfaction signals:** Users praise documentation depth (#15793) and the project’s ambition (“tech is incredible”). The active reporting of edge cases shows a dedicated user base that relies on Hermes for production-like scenarios.

## Backlog Watch

Issues and PRs that have been open for extended periods and may require maintainer attention:

| Item | Age (approx.) | Status | Why stalled? |
|------|---------------|--------|--------------|
| #527 (RBAC) | 4+ months (Mar 6) | Open, needs-decision | High engagement, but no maintainer decision. |
| #8993 (Tool calling unstable) | 3.5 months (Apr 13) | Open, needs-repro | Reproducibility not confirmed; users continue to report. |
| #26977 (Prompt injection scanning) | 2.5 months (May 16) | Open | No movement; heuristic gap persists. |
| #11185 (Email thread context fix) | 3+ months (Apr 16) | PR open | Not yet merged. |
| #47017 (Undo/redo) | 1.5 months (Jun 16) | PR open | Large surface area; may need more review. |
| #22037 (Update branch reconciliation) | 2.5 months (May 8) | PR open | Awaits approval. |

**Recommendation:** Maintainers should prioritize triage of #527 (community demand) and #58619/#73163 (stability risks). Several open PRs address long-standing user pain points (email threading, undo/redo, update reliability) and would reduce backlog if merged.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*