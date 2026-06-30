# OpenClaw Ecosystem Digest 2026-06-30

> Issues: 376 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-30 02:55 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-30

## 1. Today’s Overview

OpenClaw sustained extremely high activity over the last 24 hours, with **376 issues updated** (317 open, 59 closed) and **500 pull requests touched** (444 open, 56 merged/closed). No new releases were cut. The project is in a heavy development and triage cycle — many bugs are being actively reported and patched, but the sheer volume of open issues (especially P1 regressions) suggests the codebase is under stability pressure. The highest-comment issues center on session write‑lock contention, silent message drops, and embedded‑run latency, indicating core infrastructure pain points.

## 2. Releases

**No new releases** — the last published version remains `2026.6.8` (based on issue references). No breaking changes or migration notes to report this period.

## 3. Project Progress

**56 pull requests were merged or closed** in the last 24 hours. Notable resolved issues from the top‑comment list:

- **#81525* *[Bug] media‑understanding silently routes images → closed* — a validation bug that sent images to models without checking their vision capability is now fixed.
- **#88548* *GitHub Copilot static model list → closed* — the provider now correctly uses live entitlement discovery instead of a stale default list.
- **#95500* *Plugin model provider (opencode‑go) resolution in cron → closed* — isolated cron sessions can now find plugin‑defined models.
- **#16896* *Right‑click reply in Dashboard webchat → closed* — a long‑standing UX enhancement was finally merged.

The merged PRs span multiple areas: **fixes to Discord slash‑command deployment** (#75961 merged context?), **Matrix crypto bootstrap hardening** (#97181), **Telegram target parsing** (#97823), **proxy NO_PROXY matching** (#97713), and **cron empty‑reply handling** (#95725). A **large pipeline PR** (#93342) aims to normalize provider→channel streaming grammar across all channels.

## 4. Community Hot Topics

The most discussed issues (by comment count) reveal where users are hurting the most:

| Issue | Title | Comments | 👍 |
|-------|-------|----------|----|
| [#86538](https://github.com/openclaw/openclaw/issues/86538) | Session write‑lock timeouts block subagent delivery lanes | 18 | 1 |
| [#80319](https://github.com/openclaw/openclaw/issues/80319) | QA tool‑defaults suite conflates Codex‑native tools with OpenClaw dynamic tool parity | 17 | 1 |
| [#74586](https://github.com/openclaw/openclaw/issues/74586) | AM embedded run aborts memory_search tool calls; classifies as timeout despite model completion | 11 | 3 |
| [#80520](https://github.com/openclaw/openclaw/issues/80520) | Telegram messages silently dropped, no sendMessage logged | 11 | 3 |
| [#79077](https://github.com/openclaw/openclaw/issues/79077) | Support for Telegram bot‑to‑bot and guest‑bot modes | 8 | 8 |
| [#91363](https://github.com/openclaw/openclaw/issues/91363) | Isolated cron consistently fails with “LLM request failed” on model‑call‑started phase | 8 | 5 |
| [#94518](https://github.com/openclaw/openclaw/issues/94518) | DeepSeek cache hit rate <10% after 6.x upgrade – boundary‑aware caching breaks prefix matching | 6 | 8 |

**Underlying needs**:  
- **Reliability of session state** – write‑lock timeouts and silent message drops erode trust in the platform.  
- **Parity between runtimes** – the QA suite highlights inconsistencies between Codex and OpenClaw’s own tool execution.  
- **Provider‑specific regressions** – DeepSeek cache degradation and MiniMax usage field inversions show that recent “boundary‑aware” changes broke real‑world provider behavior.  
- **Telegram ecosystem growth** – users strongly desire the new Telegram bot features (guest bots, bot‑to‑bot) from the May 2026 Telegram release.

## 5. Bugs & Stability

**High‑severity bugs active in the last 24 hours** (ranked by label and impact):

| Issue | Severity | Impact | Fix PR? |
|-------|----------|--------|---------|
| [#86538](https://github.com/openclaw/openclaw/issues/86538) | 🦞 Diamond Lobster (P1) | Session write‑lock timeouts block subagent lanes | Linked PR open (#86572) |
| [#91363](https://github.com/openclaw/openclaw/issues/91363) | 🐚 Platinum Hermit (P1) | Cron jobs fail before LLM invocation (“model‑call‑started” phase) | None yet |
| [#77642](https://github.com/openclaw/openclaw/issues/77642) | 🐚 Platinum Hermit (P1) | Duplicate answers + synthetic “missing tool result” errors (5.3 regression) | Needs live repro |
| [#97877](https://github.com/openclaw/openclaw/issues/97877) | 🦞 Diamond Lobster (P1) | Empty‑error‑retry blocked by `hadPotentialSideEffects` – silent failure on transient 5xx after tool call | **Fix PR #97966** (just opened today) |
| [#80520](https://github.com/openclaw/openclaw/issues/80520) | 🦐 Gold Shrimp (P1) | Telegram messages silently dropped | Needs info |
| [#82070](https://github.com/openclaw/openclaw/issues/82070) | 🐚 Platinum Hermit (P1) | CLI ~14s cold‑start regression after 2026.5.12 | Needs live repro |
| [#95121](https://github.com/openclaw/openclaw/issues/95121) | 🦐 Gold Shrimp (P2) | Codex OAuth/appserver turns spend ~28s after prompt.submitted for tiny replies | Needs live repro |
| [#81917](https://github.com/openclaw/openclaw/issues/81917) | 🐚 Platinum Hermit (P2) | Dashboard logs bare URL despite token auto‑auth; can hang on Linux/KDE | Needs maintainer review |
| [#82662](https://github.com/openclaw/openclaw/issues/82662) | 🐚 Platinum Hermit (P2) | Isolated cron agentTurn fails with “setup timed out before runner start” – all fallback models exhausted | Needs product decision |
| [#87058](https://github.com/openclaw/openclaw/issues/87058) | 🦞 Diamond Lobster (P1) | Android node connects but advertises zero commands + onboarding connect‑nonce retry race | Needs maintainer review |

**Regression trends**: Many bugs are marked **“worked before, now fails”** (e.g., #77642, #81484, #82020, #81934), suggesting that recent large refactors (especially around session management and provider abstraction) have introduced subtle breakage. The **#97877** fix is particularly critical — it unblocks transient error recovery for any session that has used tools.

## 6. Feature Requests & Roadmap Signals

Top feature requests from the last 24 hours (by community engagement):

| Issue | Feature | 👍 | Likely in next version? |
|-------|---------|----|------------------------|
| [#79077](https://github.com/openclaw/openclaw/issues/79077) | Telegram bot‑to‑bot & guest‑bot support | 8 | High – Telegram announced features May 2026, community strongly wants it. |
| [#81061](https://github.com/openclaw/openclaw/issues/81061) | Pre‑routing inbound message hook (`before_route_inbound_message`) | 3 | Medium – would enable channel bridging/proxying. |
| [#80213](https://github.com/openclaw/openclaw/issues/80213) | Skill author‑defined setup hook (`setup.script`) | 4 | Medium – closes gap between install kinds and needed post‑install steps. |
| [#81913](https://github.com/openclaw/openclaw/issues/81913) | Stable plugin SDK surface for installed skill workflows | 1 | Medium – aligns with ongoing SDK stabilization (#80188). |
| [#82450](https://github.com/openclaw/openclaw/issues/82450) | Linear Persistent Workspace Mode for blind users | 1 | Low – niche but high‑impact accessibility request. |
| [#81960](https://github.com/openclaw/openclaw/issues/81960) | Allow onboarding to configure multiple providers/models | 0 | Low – nice‑to‑have for initial setup. |

**Prediction**: The next minor release (2026.6.10 or 2026.7.0) will likely include:
- Fixes for the **session write‑lock timeout** (#86538) and **empty‑error‑retry** (#97877) — both have linked PRs.
- **Telegram bot‑to‑bot / guest‑bot** support (#79077) given the external deadline.
- **DeepSeek cache hit rate** fix (#94518) — high user pain.
- Continued work on the **normalized provider→channel grammar** (#93342), which is a large architectural change.

## 7. User Feedback Summary

From the top 50 issues, user sentiment reveals:

- **Frustration with silent failures** – “Telegram messages silently dropped” (#80520), “user never receives a reply” (same), “sessions_spawn fails with missing scope” (#77807). Users expect explicit error feedback.
- **Performance regressions** – Cold‑start delays (#82070), 10‑17s latency for multi‑agent setups (#80607), 28s extra for tiny replies (#95121). The “auth stage” taking 10‑15s synchronously (#75782) is a recurring complaint.
- **Accessibility praise and pain** – A blind user (#82450) calls OpenClaw “one of the most powerful AI work interfaces I have ever used,” but requests a linear workspace mode. This shows the core experience is strong for screen‑reader users, but workspace navigation needs improvement.
- **Provider‑specific letdowns** – DeepSeek cache hit rate drop (#94518) and MiniMax usage inversion (#81156) erode trust in caching/metering.
- **Desire for parity** – Multiple reports compare Codex runtime vs. OpenClaw embedded‑run behavior (e.g., #80319, #77642). Users want consistent tool execution across runtimes.

## 8. Backlog Watch

Issues and PRs that have been open for weeks or months and still need maintainer attention:

| Item | Created | Last Update | Status | Why Stalled |
|------|---------|-------------|--------|-------------|
| [#75782](https://github.com/openclaw/openclaw/issues/75782) (P1) | 2026-05-01 | 2026-06-29 | Needs product decision + live repro | “Auth” stage takes 10‑15s – no fix PR yet, maintainers divided on approach. |
| [#80131](https://github.com/openclaw/openclaw/issues/80131) (P2) | 2026-05-10 | 2026-06-29 | Needs product decision + live repro | Per‑request auth (5.5s) and tool bundling (8.9s) dominate TTFT – large perf win possible. |
| [#80286](https://github.com/openclaw/openclaw/issues/80286) (P2) | 2026-05-10 | 2026-06-29 | Needs product decision | `sessions --json` missing subagent metadata – blocks monitoring tooling. |
| [#80188](https://github.com/openclaw/openclaw/issues/80188) (P2) | 2026-05-10 | 2026-06-29 | Needs product decision + security review | SDK follow‑up for host‑owned structured plugin inference – foundational for plugin ecosystem. |
| [#12581](https://github.com/openclaw/openclaw/pull/12581) (PR) | 2026-02-09 | 2026-06-30 | Waiting on author | Session prune lifecycle event – long‑dormant PR, may need revival. |
| [#36630](https://github.com/openclaw/openclaw/pull/36630) (PR) | 2026-03-05 | 2026-06-30 | Needs proof | Bidirectional Signal quote‑reply – stalled for months despite being size XL. |
| [#79077](https://github.com/openclaw/openclaw/issues/79077) (P2) | 2026-05-07 | 2026-06-29 | Needs live repro + security review | Telegram bot‑to‑bot – popular but blocked on security review. |

**Recommendation**: The project maintainers should prioritize the P1 backlog items (#75782, #80131) and the Telegram v2 feature (#79077) to address the most painful user experience gaps and external API changes.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## 1. Ecosystem Overview

The open-source personal AI assistant and agent ecosystem is entering a phase of intense scaling and stabilization. Both OpenClaw and Hermes Agent are experiencing high contribution volumes, but the character of their activity diverges: OpenClaw is under stability pressure from rapid feature accretion and provider abstraction refactors, while Hermes Agent is consolidating after a feature push, with a narrower set of high-priority bugs and user-experience gaps. Community engagement remains strong across both projects, with users demanding reliable session persistence, provider-agnostic configuration, and cross-platform continuity. The ecosystem overall is moving from proof-of-concept toward production reliability, with security boundaries and credential management emerging as critical hygiene concerns.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|---|---|---|
| **Issues updated (24h)** | 376 (317 open, 59 closed) | 50 (49 open, 1 closed) |
| **PRs touched (24h)** | 500 (444 open, 56 merged/closed) | 50 (46 open, 4 merged/closed) |
| **Open issue/PR ratio** | ~1.1:1 (balanced) | ~1.1:1 (balanced) |
| **Release status** | No new release; last: 2026.6.8 | No new release; last: 0.16.x implied from PRs |
| **Health signal** | Heavy development with stability pressure; 9 active P1 bugs, many "worked before, now fails" regressions | Active maintenance with bug consolidation; 2 P1 bugs open >1 month, 46 open PRs suggest maintainer bottleneck |
| **Community engagement (top issue comments)** | 18 comments (write-lock contention) | 10 comments (TUI macOS crash) |

**Verdict:** OpenClaw operates at ~7–8× the raw activity volume of Hermes Agent, but a significant portion of that volume is triage and regression management. Hermes Agent has a tighter, more focused contribution pattern with proportionally fewer emergencies.

## 3. OpenClaw’s Position

- **Advantages vs. peers:**
  - **Scale and velocity:** 376 issues and 500 PRs in 24 hours dwarfs Hermes Agent’s volume, indicating a larger contributor base and broader ecosystem adoption.
  - **Platform reach:** Active maintenance across Discord, Matrix, Telegram, and CLI demonstrates a multi-channel strategy that Hermes Agent (desktop + TUI + Telegram) does not fully match.
  - **Architectural ambition:** The normalized provider→channel streaming grammar (PR #93342) and boundary-aware caching (though broken) represent deeper platform investments than Hermes Agent’s current feature set.

- **Technical approach differences:**
  - OpenClaw emphasizes a plugin and skill ecosystem with formalized provider abstraction; Hermes Agent focuses on a more monolithic agent experience with cron loops and session continuity.
  - OpenClaw’s triage load is heavier (9 P1 bugs vs. 2 P1 for Hermes Agent), suggesting a more aggressive release cadence that trades stability for feature velocity.

- **Community size comparison:**
  - OpenClaw’s top issues attract 8–18 comments and up to 8 reactions; Hermes Agent’s top issues attract 5–10 comments and up to 6 reactions. Both have healthy communities, but OpenClaw’s engagement volume is 2–3× larger.

## 4. Shared Technical Focus Areas

The following requirements are emerging across *both* projects, often with independent implementations:

| Focus Area | OpenClaw signals | Hermes Agent signals |
|---|---|---|
| **Session state reliability** | Write-lock timeouts (#86538), silent message drops (#80520) | Gateway TUI mid-turn exit (#27282), session state splitting on model switch (#53611) |
| **Provider-agnostic configuration** | DeepSeek cache degradation (#94518), MiniMax usage inversion (#81156) | `reasoning_effort` silently dropped for custom providers (#55276), hardcoded temperature (#17565) |
| **Telegram integration maturity** | Bot-to-bot/guest-bot support (#79077), rich table rendering fixes | Cronjob table rendering broke (now fixed in #53632), cross-platform session continuity (#54981) |
| **Security / credential boundaries** | (Not prominent in top issues) | Symlink credential bypass (#55367), stale `os.environ` credential pool (#20591) |
| **Tool execution parity across runtimes** | QA suite conflation of Codex-native vs. OpenClaw dynamic tools (#80319) | Embedded-run vs. gateway tool behavior differences (ongoing) |

**Notable:** None of these focus areas are unique to one project. The industry is converging on a shared set of reliability, configuration, and parity concerns.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|---|---|---|
| **Primary feature focus** | Multi-channel, provider-abstracted agent platform with plugin ecosystem | Desktop + TUI agent with cron loops, session persistence, and code-aware workflows |
| **Target users** | Platform builders, channel integrators, skill developers | Individual power users, developers using TUI/CLI, and desktop workflow enthusiasts |
| **Architecture emphasis** | Normalized provider→channel grammar, boundary-aware caching, skill-author hooks | Loop contracts (`#21172`), background review, embedded agent browser (PR #55364) |
| **Key differentiator** | Breadth: first-class support for many channels and provider integrations | Depth: session continuity, credential safety, and IDE-like agent experiences |
| **UI/UX maturity** | Dashboard webchat, CLI, multi-platform; accessibility praise from blind users | Desktop app with scroll-regression complaints; TUI reliability gaps on macOS and Windows |
| **Stability posture** | Triage-heavy with many P1 regressions; rapid fix cycle | Fewer but older P1 bugs; slower response but lower incident density |

**Takeaway:** OpenClaw is a platform play — it aims to be the infrastructure layer for AI agents across any channel. Hermes Agent is a productivity tool — it optimizes for a single-user, code-centric workflow with strong session control.

## 6. Community Momentum & Maturity

**Tier 1 — High momentum, rapid iteration:**
- **OpenClaw:** Extremely high activity, but at the cost of stability. The project is iterating at a pace that introduces regressions faster than they can be resolved. The backlog of 444 open PRs signals that the maintainer team is stretched. This is a project in its hypergrowth phase, where feature velocity is prioritized over polish.

**Tier 2 — Active consolidation, bug-focused:**
- **Hermes Agent:** Steady, lower-volume activity with a clear emphasis on bug fixing and user-experience refinement. Two P1 bugs aging over a month is a concern, but the overall incident density is lower. The project appears to be stabilizing after a feature push (likely 0.16.x).

**Maturity indicators:**
- OpenClaw has clear release numbering (2026.6.x) and a formal severity taxonomy (Diamond Lobster → Gold Shrimp). Hermes Agent lacks a visible release cadence in the digest.
- Both projects have active maintainer presence (PRs respond within hours to days), but OpenClaw’s response is more diffuse across many issues.

## 7. Trend Signals

From community feedback and cross-project patterns, the following trends are relevant for AI agent developers:

1. **Reliability trumps features in enterprise adoption.** Users in both ecosystems are far more vocal about silent failures (dropped messages, unacknowledged errors) than about missing features. AI agent platforms that cannot guarantee delivery and error transparency will struggle in production deployments.

2. **Provider abstraction is a double-edged sword.** Both projects are investing in provider-agnostic layers (normalized grammar, boundary-aware caching), but these abstractions are introducing subtle regressions (DeepSeek cache, MiniMax metering, custom provider credential resolution). Developers should expect a 2–3 release stabilization period after any major provider abstraction overhaul.

3. **Security boundaries are under-architected.** Hermes Agent’s symlink credential bypass and stale environment variable issues are early warnings. As agents gain access to files, credentials, and sensitive memory, the industry needs declarative permission models (immutable skills, file access policies) — not just opt-in approval dialogs.

4. **Session persistence is the new table stakes.** Loop contracts (Hermes Agent) and session write-lock fixes (OpenClaw) both point to the same need: agents must maintain reliable, long-lived sessions across restarts, channel switches, and model switches. Without this, complex multi-step workflows break.

5. **Telegram is emerging as the critical non-desktop channel.** Both projects have significant Telegram-specific issues and feature requests. AI agent developers targeting consumer deployment should prioritize Telegram integration quality over other messaging platforms.

6. **Normalized tool execution across runtimes is a hard problem.** OpenClaw’s QA suite versus Codex comparisons and Hermes Agent’s embedded versus gateway behavior differences reveal that tool behavior varies unpredictably across execution contexts. Standardizing this is a prerequisite for composable agent systems.

---

*Report based on community digest data for 2026-06-30. Activity metrics reflect 24-hour rolling window only.*

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-30

## 1. Today's Overview

Hermes Agent remains highly active, with **50 issues** and **50 pull requests** updated in the last 24 hours. The repository currently carries **49 open issues** (including several high‑priority bugs) and **46 open PRs**, indicating a large maintenance and feature pipeline. Only **1 issue** and **4 PRs** were closed or merged today, suggesting a buildup of change requests. No new releases were cut; the project appears to be in a consolidation and bug‑fixing phase. Community engagement is strong, with several long‑running discussions attracting double‑digit comments and reactions.

## 2. Releases

*None.* No new releases were published on this date.

## 3. Project Progress

**Merged/closed today:** 4 pull requests and 1 issue.

- **PR [#55363](https://github.com/NousResearch/hermes-agent/pull/55363)** *(closed)* – Fix desktop session list refresh on profile scope changes.
- **Other closed PRs** – The remaining 3 closed PRs are not shown in the top‑20 list; likely minor fixes or dependabot updates.
- **Issue [#53632](https://github.com/NousResearch/hermes-agent/issues/53632)** *(closed)* – Cronjob‑breaking rich table rendering in Telegram was fixed.

Additionally, a **P1 bug** ([#53611](https://github.com/NousResearch/hermes-agent/pull/53611)) addressing session state splitting on model switch remains open but received updates today—an important fix for billing and context continuity.

## 4. Community Hot Topics

Most active discussions (by comment count):

- **[#27282](https://github.com/NousResearch/hermes-agent/issues/27282) (10 comments)** – *[P1] Gateway exits mid‑turn with stdin EOF in `--tui` mode on macOS.* Users report this occurs even without Byterover, suggesting a broader TUI session‑state bug. The author suspects a general variant of #14036.

- **[#21172](https://github.com/NousResearch/hermes-agent/issues/21172) (6 comments)** – *[Feature] First‑class Loop Contract for cron‑backed agent loops.* The issue references Boris Cherny’s workflow shift to persistent sessions, and requests declarative budget/stop/refresh controls. This has broad support (+6 👍) and is trending as a design priority.

- **[#37527](https://github.com/NousResearch/hermes-agent/issues/37527) (5 comments)** – *Desktop chat mouse‑wheel scroll‑up snaps back down.* Users find this especially frustrating because manual scrollbar dragging works, pointing to a scroll‑event handling regression.

- **[#17565](https://github.com/NousResearch/hermes-agent/issues/17565) (5 comments, 6 👍)** – *Configurable temperature parameter.* Hardcoded temperature causes hallucinations and inflexibility; 6 upvotes indicate strong demand.

- **[#32207](https://github.com/NousResearch/hermes-agent/issues/32207) (5 comments)** – *`/clear` command freezes terminal on Windows/WSL.* A critical usability bug for Windows users.

- **[#55276](https://github.com/NousResearch/hermes-agent/issues/55276) (3 comments)** – *`reasoning_effort` silently dropped for custom/ZAI providers.* Affects users of alternative model APIs.

**Underlying needs:** The community is demanding (1) session persistence and cross‑platform continuity, (2) better configuration control over model parameters, (3) reliability fixes for TUI and desktop UI, and (4) stronger security boundaries around credentials and skills.

## 5. Bugs & Stability

**New bugs reported today (P2 severity or higher):**

| Issue | Severity | Description | Fix PR exists? |
|-------|----------|-------------|----------------|
| [#55367](https://github.com/NousResearch/hermes-agent/issues/55367) | **P2** (security) | ACP auto‑approve ignores symlinks to sensitive files – credentials can be edited without prompting. | Yes ([#55368](https://github.com/NousResearch/hermes-agent/pull/55368)) |
| [#55369](https://github.com/NousResearch/hermes-agent/issues/55369) | **P2** | Union `integer\|string` tool args drop leading zeros (“007” becomes 7). | Yes ([#55370](https://github.com/NousResearch/hermes-agent/pull/55370)) |
| [#55088](https://github.com/NousResearch/hermes-agent/issues/55088) | **P2** | HTTP session delete leaves transcript/dump files on disk (cleanup incomplete). | No linked PR yet |
| [#54937](https://github.com/NousResearch/hermes-agent/issues/54937) | **P2** | `background_review` cross‑profile memory contamination via dynamic `HERMES_HOME`. | No |
| [#55202](https://github.com/NousResearch/hermes-agent/issues/55202) | **P2** | `HERMES_SESSION_KEY` / `HERMES_SESSION_ID` missing or stale in gateway/Desktop tools. | No |
| [#55224](https://github.com/NousResearch/hermes-agent/issues/55224) | **P2** | Responses auto‑truncation drops leading compaction summaries (loss of context). | No |

**Ongoing high‑priority bugs updated today:**

- **[#27282](https://github.com/NousResearch/hermes-agent/issues/27282) (P1)** – TUI gateway mid‑turn exit on macOS. Stale for over a month.
- **[#20591](https://github.com/NousResearch/hermes-agent/issues/20591) (P1)** – Credential pool reads stale `os.environ` instead of fresh `.env`. Test says correct, code does not match.

**Stability signals:** Several security‑boundary bugs (symlinks, credential injection) and session‑state bugs surfaced today. The desktop scroll snap (P2) and `/clear` freeze (P2) remain unresolved. Overall bug response seems active (two fix PRs submitted today for new bugs), but P1 issues are aging.

## 6. Feature Requests & Roadmap Signals

**Top user‑requested features (based on activity and upvotes):**

- **[#17565](https://github.com/NousResearch/hermes-agent/issues/17565) (6 👍)** – Configurable temperature – unlikely to ship next because it requires provider‑level API changes but is heavily demanded.
- **[#31684](https://github.com/NousResearch/hermes-agent/issues/31684)** – `compress_context` command – includes contributed patches; may land soon.
- **[#25083](https://github.com/NousResearch/hermes-agent/issues/25083)** – Immutable/protected skills – critical for safety and governance; likely to appear in next minor release.
- **[#21172](https://github.com/NousResearch/hermes-agent/issues/21172)** – Loop Contract – high‑profile feature request from Claude Code community; roadmap implications.
- **[#55039](https://github.com/NousResearch/hermes-agent/issues/55039)** – Per‑depth subagent model routing – sophisticated cost‑tapering delegation; longer‑term.
- **[#54981](https://github.com/NousResearch/hermes-agent/issues/54981)** – Cross‑platform session continuity (Desktop ↔ Telegram) – a top user experience gap.

**Prediction for next version (0.17.x):** Likely includes at least one of: temperature configuration, protected skills, or the `compress_context` command. The embedded agent browser PR ([#55364](https://github.com/NousResearch/hermes-agent/pull/55364)) is a large new feature that may land in a later release.

## 7. User Feedback Summary

**Pain points expressed today:**

- *Desktop scroll‑up snapping* (#37527) makes reading long threads frustrating.
- *`/clear` freezes on Windows* (#32207) forces terminal restart.
- *Credential pool misbehavior* (#20591) breaks authentication when using .env files.
- *TTS playback delays mic activation by 7‑8 seconds* (#51265) – voice workflow broken.
- *Cronjob tables render broken in Telegram* (#53632, now closed) – rich message formatting still fragile.
- *Agent ignores memory/skills rules* (#49764) – reliability of self‑regulation questioned.
- *Bundled hermes‑agent skill is too monolithic* (#51387) – update drift and loading costs.

**Satisfaction signals:** The “Embedded agent browser” PR (#55364) was warmly received (though comment data missing), and contributions continue across many areas.

## 8. Backlog Watch

High‑priority issues with long‑standing maintainer attention need:

| Issue | Age | Priority | Why it matters |
|-------|-----|----------|----------------|
| [#27282](https://github.com/NousResearch/hermes-agent/issues/27282) | 44 days (May 17) | **P1** | TUI gateway crash on macOS – core functionality broken. Unanswered for 6 weeks. |
| [#20591](https://github.com/NousResearch/hermes-agent/issues/20591) | 55 days (May 6) | **P1** | Credential pool prefers stale `os.environ` – authentication security gap. No PR. |
| [#13489](https://github.com/NousResearch/hermes-agent/issues/13489) | 70 days (Apr 21) | **P3** | ACP custom provider credential resolution fails. Low priority but old. |
| [#38065](https://github.com/NousResearch/hermes-agent/issues/38065) | 27 days (Jun 3) | **P3** | No DeepSeek option in desktop app. Request ignored. |

**Concern:** Two P1 bugs have been open for over a month without a merged fix. The TUI and credential pool issues impact core user experience and security. The backlog of open PRs (46) suggests maintainer bottleneck despite high contribution volume.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*