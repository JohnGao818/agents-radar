# OpenClaw Ecosystem Digest 2026-06-16

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-16 03:40 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-16

## Today's Overview

OpenClaw is experiencing a sustained high level of activity, with **500 issues** and **500 pull requests** updated in the last 24 hours. The community remains deeply engaged: 481 issues are open, 19 were closed, and 87 PRs were merged or closed. A new beta release, `v2026.6.8-beta.2`, shipped today, focusing on richer and more robust Telegram and WhatsApp channel delivery. Security and stability topics dominate the discussion, with several high-severity bugs and feature requests receiving significant commentary. The project shows strong momentum in cross-platform expansion, channel reliability, and tool safety.

---

## Releases

**New release:** `v2026.6.8-beta.2` — openclaw 2026.6.8-beta.2

### Highlights
- **Telegram** can now send structured rich text including tables, lists, expandable blockquotes, and preserved intentional line breaks.
- **WhatsApp** channel delivery is less brittle (details in release notes).
- Prompt-preserving CLI backend delivery for Telegram.
- Retired native draft migration (replaced by richer handling).
- Safer rich-media handling (likely preventing the media loss bugs seen in earlier versions).

No breaking changes or migration notes have been explicitly documented for this beta.

---

## Project Progress

Today **87 PRs were merged or closed**. Notable closed PRs from the top list include:

- [#91208](https://github.com/openclaw/openclaw/pull/91208) *(closed)* — **fix #91047: Plugin session-extension registry not pinned** – prevents plugin extension loss after agent/subagent plugin-load churn. Improves session stability.

Several other high-impact PRs remain open (see sections below) but moved closer to merge. The closing of #91208 is a key stability win for plugin-heavy users.

---

## Community Hot Topics

The most-commented and most-reacted issues highlight three core community concerns: **cross-platform availability**, **security**, and **session reliability**.

| Issue | Comments | 👍 | Topic |
|-------|----------|----|-------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | 109 | 79 | Linux/Windows Clawdbot Apps – users want desktop parity with macOS/iOS/Android |
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | 32 | 1 | Text between tool calls leaks to messaging channels – a critical UX bug |
| [#9443](https://github.com/openclaw/openclaw/issues/9443) | 25 | 2 | Prebuilt Android APK releases – barrier to entry for Android users |
| [#32473](https://github.com/openclaw/openclaw/issues/32473) | 17 | 5 | Control UI requires HTTPS/localhost – Docker/VPS users blocked |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) | 17 | 0 | Signal daemon restart race condition – orphaned processes, message loss |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) | 17 | 0 | Tiered bootstrap file loading – token budget optimization request |

**Underlying needs:** The community is clearly pushing for (1) broader OS support outside the Apple ecosystem, (2) tighter security boundaries to prevent agent output from leaking internal processing, and (3) better session and sandbox isolation for multi-agent scenarios.

---

## Bugs & Stability

Several high-severity bugs were reported or updated today. Ranked by impact:

1. **Critical – Text between tool calls leaks to messaging channels**  
   [#25592](https://github.com/openclaw/openclaw/issues/25592) (P1, impact:security, impact:message-loss) – The agent’s internal processing output (error handling, narration) is sent to Slack, iMessage, etc. as visible messages. **No fix PR found yet** in the top list, but a related PR [#85403](https://github.com/openclaw/openclaw/pull/85403) *fix(telegram): suppress message-tool reply previews* addresses a similar Telegram-side issue.

2. **Control UI requires device identity (HTTPS/localhost)**  
   [#32473](https://github.com/openclaw/openclaw/issues/32473) (P1, regression, impact:security) – VPS/Docker users cannot access the UI without HTTPS or localhost. **No linked fix PR** observed.

3. **Signal daemon stop() race condition on SIGUSR1 restart**  
   [#22676](https://github.com/openclaw/openclaw/issues/22676) (P1, impact:crash-loop, impact:message-loss) – Orphaned processes and send failures on gateway restart. **No linked fix PR** observed.

4. **Agent replies to previous message instead of current**  
   [#32296](https://github.com/openclaw/openclaw/issues/32296) (P1, impact:session-state, impact:message-loss) – Session context confusion. **No linked fix PR**.

5. **”Cannot convert undefined or null to object” with google-vertex/gemini-3.1**  
   [#38327](https://github.com/openclaw/openclaw/issues/38327) (P1, regression) – Breaks Gemini model usage after upgrade to 2026.3.2. **No linked fix PR**.

6. **Bootstrap files in agentDir silently ignored**  
   [#29387](https://github.com/openclaw/openclaw/issues/29387) (P1, impact:session-state, impact:security) – Per-agent bootstrap files are not loaded. **No linked fix PR**.

7. **Multiple Docker/Sandbox volume mount bugs**  
   [#31331](https://github.com/openclaw/openclaw/issues/31331) (P1, impact:session-state, impact:security) – Workspace cannot bind in Docker-with-Docker. **No linked fix PR**.

Several other P1/P2 bugs were also updated today, including avatar rendering issues, Feishu media loss, and session key reuse problems. The volume of **open P1 issues with no fix PR** suggests a backlog that maintainers are actively triaging but have not yet resolved.

---

## Feature Requests & Roadmap Signals

The community has submitted numerous feature requests, many carrying the `impact:security` label. The most prominent:

- **Masked Secrets** ([#10659](https://github.com/openclaw/openclaw/issues/10659)) – allow agents to *use* API keys without *seeing* them. High community demand (👍4).
- **Private network fetch opt-in** ([#39604](https://github.com/openclaw/openclaw/issues/39604)) – `tools.web.fetch.allowPrivateNetwork` (👍9 – highest reaction count in requests).
- **Slack Block Kit support** ([#12602](https://github.com/openclaw/openclaw/issues/12602)) – richer Slack messages.
- **Post-subagent completion extension hook** ([#22358](https://github.com/openclaw/openclaw/issues/22358)) – for structured trajectory recording.
- **Memory Trust Tagging** ([#7707](https://github.com/openclaw/openclaw/issues/7707)) – prevent memory poisoning.
- **Tiered bootstrap loading** ([#22438](https://github.com/openclaw/openclaw/issues/22438)) – token budget optimization.

**Prediction for next release:** The beta already ships richer Telegram/WhatsApp delivery. Likely the next stable will incorporate a subset of these security-oriented features—masked secrets (high interest) and private network opt-in (easy to implement). The Slack Block Kit and memory tagging may take longer due to scope.

---

## User Feedback Summary

Real pain points voiced in today’s issue updates:

- **“I can't find how to solve this”** – multiple users struggling with HTTPS requirement for control UI (Docker/VPS).
- **“This is a significant UX problem”** – tool-call text leakage into channels breaks trust.
- **“Bootstrap files are silently ignored”** – per-agent configuration not working as documented.
- **“No precompiled APK”** – barrier for Android users who cannot compile from source.
- **“Token waste on full tool schemas”** – advanced users want fine-grained control over context size.
- **“Duplicate messages in A2A communication”** – confusion in multi-agent setups.

Overall satisfaction is tempered by these regressions and gaps, but the active community and rapid release cycle (new beta today) indicate strong maintenance and responsiveness.

---

## Backlog Watch

Several important items have been open for months without a fix PR:

- **#75** (Jan 2026) – Linux/Windows Clawdbot Apps – **109 comments**, massive community support, no PR attached.
- **#25592** (Feb 2026) – Text between tool calls leaks – critical security bug, no fix PR.
- **#22676** (Feb 2026) – Signal daemon race condition – P1, impact:crash-loop, no PR.
- **#10687** (Feb 2026) – Dynamic model discovery (OpenRouter) – maintainer-tagged, no PR.
- **#22438** (Feb 2026) – Tiered bootstrap loading – feature request with 17 comments, no PR.
- **#14785** (Feb 2026) – Reduce tool schema token overhead – 7 comments, no PR.

**PRs needing maintainer attention:**
- [#93265](https://github.com/openclaw/openclaw/pull/93265) – `feat(onboard): streamline setup with agent-assisted configuration` – large PR, ready for maintainer look.
- [#93276](https://github.com/openclaw/openclaw/pull/93276) – `fix(plugins): stop tool-discovery loads from clearing active providers` – waiting on author.
- [#85403](https://github.com/openclaw/openclaw/pull/85403) – `fix(telegram): suppress message-tool reply previews` – needs screenshot proof.

These items represent the most significant gaps between community demand and maintainer capacity. The project’s health is strong, but the backlog of unaddressed P1 bugs and high-profile feature requests may strain community goodwill if left unattended for much longer.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is maturing rapidly, driven by two leading reference implementations: **OpenClaw** (core reference, generic personal AI) and **Hermes Agent** (NousResearch’s agent framework). Both projects are experiencing high community engagement, but they address different layers of the stack. OpenClaw prioritizes channel delivery reliability and cross-platform desktop coverage, while Hermes Agent focuses on multi-agent orchestration, provider diversity, and desktop IDE-like UX. Critical shared challenges include session isolation, tool-call leakage, and context-window optimization. The ecosystem shows clear demand for security-hardened deployments, hybrid remote+local execution, and better error transparency.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| Issues updated (24h) | 500 | 50 |
| PRs updated (24h) | 500 | 50 |
| Issues open/active | 481 | 43 |
| Issues closed (24h) | 19 | 7 |
| PRs merged/closed (24h) | 87 | 5 |
| Latest release | v2026.6.8-beta.2 (today) | v0.16.0 (2026-06-05) |
| Release cadence | Weekly betas | ~Bi-weekly |
| Health score* | **B+** (high activity, but large P1 bug backlog) | **B** (critical regressions, slower PR throughput) |

*Health score based on issue closure rate, severity of open P1s, PR merge velocity, and release freshness.

## 3. OpenClaw’s Position

**Advantages vs. peers:**
- **Channel richness**: Telegram/WhatsApp delivery with structured text (tables, lists, blockquotes) – Hermes Agent focuses on channels like Discord/Telegram but lags in rich formatting.
- **Plugin stability**: Recent fix for plugin session-extension registry pinning (#91208) reduces agent churn; Hermes Agent has no equivalent plugin architecture.
- **Community scale**: OpenClaw’s issue/PR volume is **10× higher** than Hermes Agent, indicating a larger contributor base and broader user adoption.
- **Release velocity**: Beta shipped today shows rapid iteration; Hermes Agent last released 11 days ago with no new release in 24h.

**Technical approach differences:**
- OpenClaw is channel-first (delivery, rich media, CLI backend), while Hermes Agent is orchestration-first (DAG TaskGraph, Kanban workers, A2A bus).
- OpenClaw uses a plugin-based session registry; Hermes Agent uses a monolithic session model with SQLite backend.

**Community size comparison:** OpenClaw’s 109-comment issue #75 (Linux/Windows apps) vs Hermes Agent’s 50-comment issue #7237 (truncation) suggests OpenClaw’s user base is more vocal and likely larger.

## 4. Shared Technical Focus Areas

| Focus Area | Projects Affected | Specific Needs |
|------------|-------------------|----------------|
| **Cross-platform desktop apps** | OpenClaw, Hermes Agent | Linux/Windows parity (OpenClaw #75); macOS Electron compilation failures (Hermes #40187) |
| **Session isolation & security** | OpenClaw, Hermes Agent | Tool-call text leakage (OpenClaw #25592), concurrent session cross-contamination (Hermes #46303) |
| **Gateway reliability** | OpenClaw, Hermes Agent | Signal daemon race (OpenClaw #22676), Telegram freeze after 409 (Hermes #40691) |
| **Context window optimization** | OpenClaw, Hermes Agent | Tiered bootstrap files (OpenClaw #22438), skill list bloat vector routing (Hermes #22620) |
| **OAuth/API key security** | OpenClaw, Hermes Agent | Masked secrets (OpenClaw #10659), Anthropic OAuth rejection (Hermes #46675) |
| **Error transparency** | Hermes (primary), OpenClaw | Kanban worker protocol violations (Hermes #27178); OpenClaw’s “cannot convert undefined” error (#38327) |

Both projects are actively addressing **security-hardened agent execution** and **smarter context management**, but Hermes Agent shows more advanced work on orchestration and provider diversity.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary focus** | Channel delivery, plugin stability, cross-platform desktop | Multi-agent orchestration, provider diversity, desktop IDE UX |
| **Target users** | End users needing reliable messaging + personal AI on any OS | Developers building custom agent workflows with multi-model backends |
| **Architecture** | Plugin-based session registry, CLI backend, rich text pipelines | DAG TaskGraph, Kanban workers, SQLite session store, Electron desktop |
| **Channel support** | Telegram (rich), WhatsApp, Slack, iMessage, Signal | Discord, Telegram, Feishu, Slack (basic), Kanban |
| **Provider support** | Gemini, Vertex, OpenRouter (dynamic) | Many providers (Anthropic, OpenAI, Minimax, Fusion, MoA) |
| **Release maturity** | Beta (frequent, experimental) | Stable v0.16.0 (but regressions) |
| **Community size (inferred)** | Larger (10× activity) | Smaller but highly engaged |
| **Key strength** | Rich messaging & plugin isolation | Orchestration & model management |

**Conclusion:** OpenClaw is better for users who want a stable personal assistant across multiple messaging platforms; Hermes Agent is better for developers building complex, multi-agent systems with controlled context.

## 6. Community Momentum & Maturity

- **Rapid iteration tier**: **OpenClaw** – weekly beta releases, 87 PRs merged/closed in 24h, high community churn on features. Strong momentum but risk of burnout due to P1 backlog.
- **Stabilizing tier**: **Hermes Agent** – slower PR throughput (5 merged/closed in 24h), but deeper architecture work (orchestration, multi-provider). Recent v0.16.0 regression suggests need for stabilization before major features.

Both projects are **actively maintained** with engaged communities. OpenClaw shows higher raw activity, but Hermes Agent’s large open PRs (DAG TaskGraph, Fusion presets) indicate substantial feature development in progress.

## 7. Trend Signals

Five key industry trends extracted from community feedback:

1. **Security-first agent execution**  
   Both communities demand masked secrets (OpenClaw #10659), private network fetch opt-in (OpenClaw #39604), and memory trust tagging (OpenClaw #7707). Tool-call leakage is the top security concern.

2. **Hybrid deployment (remote reasoning + local tools)**  
   Hermes Agent’s #18715 (15 👍) and OpenClaw’s control UI HTTPS requirement (#32473) signal a need for agents that can offload reasoning to cloud while keeping sensitive tool execution local.

3. **Context window optimization as a product differentiator**  
   Token budgets (bootstrap tiering), lazy skill routing, and vector-based context management are recurring themes. Developers see this as the next frontier for agent performance.

4. **Cross-platform desktop parity (beyond macOS/iOS)**  
   OpenClaw #75 (109 comments) and Hermes Agent #40187 (Electron compilation failures) show that Linux/Windows support is no longer optional. Users expect the same rich experience on all major OSes.

5. **Gateway reliability and error transparency**  
   Opaque failures (Kanban protocol violations, Signal race conditions, Telegram freezes) erode trust. Both communities are pushing for better logging, retry logic, and user-visible error messages.

**Value for AI agent developers:** These trends emphasize that the next wave of agent platforms will focus on **security boundaries**, **context efficiency**, and **cross-platform reach**. Developers should prioritize integration with private network access controls, token budget management, and robust gateway error handling to meet user expectations.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-06-16

## 1. Today’s Overview

Hermes Agent saw high activity over the past 24 hours, with **50 issues** and **50 pull requests** updated. Of those, **43 issues remain open/active** and **7 were closed**; on the PR side, **45 are open** and **5 were merged or closed**. No new releases were published. The project is actively addressing a wide range of bugs – from desktop compilation failures and gateway freezes to Kanban protocol violations and database corruption on Windows – while also advancing several large feature branches for orchestration, multi-provider support, and UI/UX improvements. Community engagement remains strong, with several issues attracting double-digit comments and reactions.

## 2. Releases

**No new releases** were created in the last 24 hours. The latest referenced version is **v0.16.0 (2026-06-05)**.

## 3. Project Progress – Merged/Closed PRs

Five PRs were merged or closed today. Notable among the top-ranked PRs:

- **[#46958] – Hide hosted dashboard update controls** (closed)  
  Hides the dashboard's built-in update controls when running in a container, and adds a `can_update_hermes` API endpoint for conditional rendering.  
  https://github.com/NousResearch/hermes-agent/pull/46958

The remaining four merged/closed PRs are not listed in the top 20 but likely address smaller bug fixes or documentation updates. The project continues to push forward on multiple fronts, with significant open PRs for orchestration (DAG TaskGraph, #12436), MoA virtual provider (#46081), Fusion presets (#46094), and desktop UI improvements (#46959).

## 4. Community Hot Topics

The following issues and PRs generated the most discussion and reactions:

- **[#7237] – [Bug]: Response truncated due to output length limit** (closed, 50 comments, 6 👍)  
  Users report that Hermes Agent truncates long-form responses mid-stream, breaking CLI and gateway messaging.  
  https://github.com/NousResearch/hermes-agent/issues/7237

- **[#40187] – [Bug]: hermes update / hermes desktop fails to compile desktop app on macOS** (open, 8 comments)  
  Compilation fails at the Electron-builder stage, blocking macOS desktop deployment.  
  https://github.com/NousResearch/hermes-agent/issues/40187

- **[#22620] – Feature Request: Skill list bloat causes massive context window inflation – need vector-based skill routing or lazy loading** (open, 5 comments)  
  Users propose smarter skill management to prevent prompt size explosion.  
  https://github.com/NousResearch/hermes-agent/issues/22620

- **[#18715] – Support remote Hermes agent with local tool execution** (open, 4 comments, 15 👍)  
  A highly upvoted request for splitting agent reasoning from local tool execution.  
  https://github.com/NousResearch/hermes-agent/issues/18715

- **[#27178] – Kanban worker reports 'protocol_violation' when agent ends turn with text response** (open, 4 comments)  
  Users frustration with opaque Kanban worker failures.  
  https://github.com/NousResearch/hermes-agent/issues/27178

**Underlying needs:** The community is asking for better error reporting (especially in Kanban), improved handling of long responses, more flexible deployment (remote agent + local tools), and smarter context management for skill-heavy sessions.

## 5. Bugs & Stability

Several high-severity bugs were reported or active in the last 24 hours, ranked by priority:

### P1 – Critical
- **[#46675] – Max OAuth requests rejected as third‑party (HTTP 400) due to single‑underscore `mcp_` tool-name prefix**  
  Blocking all API calls when using Anthropic OAuth. No fix PR identified.  
  https://github.com/NousResearch/hermes-agent/issues/46675

- **[#47002] – `SessionDB.__init__` crashes on SQLite without trigram tokenizer (v0.16.0 regression)**  
  New regression breaks SQLite builds lacking the optional trigram FTS5 tokenizer.  
  https://github.com/NousResearch/hermes-agent/issues/47002

- **[#40691] – Telegram Gateway freezes after polling conflict recovery**  
  Gateway stops processing all messages after a 409 conflict, requiring manual restart.  
  https://github.com/NousResearch/hermes-agent/issues/40691

### P2 – High
- **[#46303] – Concurrent sessions cross‑contaminate (shared memory injection + shared git worktree)**  
  No isolation between concurrent Desktop sessions.  
  https://github.com/NousResearch/hermes-agent/issues/46303

- **[#42682] – Curator‑archived bundled skills marked as user‑modified, blocking updates**  
  Skills sync bug prevents official updates from being applied.  
  https://github.com/NousResearch/hermes-agent/issues/42682

- **[#46934] – Stale `resume_pending` sessions bypass idle reset, causing context bleed after gateway restart**  
  Zombie sessions persist after gateway crash.  
  https://github.com/NousResearch/hermes-agent/issues/46934

- **[#46979] – Desktop Run History empty for agent cron jobs (v0.16.0 regression)**  
  Regression in the Desktop UI blocking run history display.  
  https://github.com/NousResearch/hermes-agent/issues/46979

- **[#46917] – Beings cannot respond with silence: forced response even when zero output is desired**  
  System produces placeholder responses like `(silence)` when none is wanted.  
  https://github.com/NousResearch/hermes-agent/issues/46917

**Fix PRs in progress:**  
- [#47007] – Force DELETE journal mode on Windows to prevent WAL corruption (P1)  
- [#47010] – Allow manual models for custom endpoints in Desktop (P2)  
- [#47008] – Add `cdn.discordapp.com` to trusted private‑IP hosts (P2)  
- [#47013] – Keep `CREATE_NO_WINDOW` on Windows MCP spawns (P2)  
- [#46985] – Surface real worker error instead of bare "protocol violation" in Kanban (P3)  

https://github.com/NousResearch/hermes-agent/pull/47007  
https://github.com/NousResearch/hermes-agent/pull/47010  
https://github.com/NousResearch/hermes-agent/pull/47008  
https://github.com/NousResearch/hermes-agent/pull/47013  
https://github.com/NousResearch/hermes-agent/pull/46985  

## 6. Feature Requests & Roadmap Signals

The following user-requested features gained traction:

- **[#18715] – Support remote Hermes agent with local tool execution** (15 👍)  
  High demand for hybrid deployment models. Likely to be prioritized in a future release.  
  https://github.com/NousResearch/hermes-agent/issues/18715

- **[#22620] – Skill list bloat: vector‑based skill routing or lazy loading**  
  Directly impacts agent performance on long‑running sessions.  
  https://github.com/NousResearch/hermes-agent/issues/22620

- **[#46097] – Desktop font size setting** (2 👍)  
  Simple UI quality‑of‑life request.  
  https://github.com/NousResearch/hermes-agent/issues/46097

- **[#46839] – Chinese user installation support**  
  Highlights need for proxy‑aware installer or mirror support.  
  https://github.com/NousResearch/hermes-agent/issues/46839

**Roadmap signals from open PRs:**  
- **Orchestration / Multi‑agent**: PR #12436 (*DAG TaskGraph + delegate bridge + A2A bus*) is a large addition (open since April).  
- **Provider expansion**: PR #36286 (*minimax-cn-oauth* for China region) and PR #46094 (*Fusion presets*) broaden supported backends.  
- **UI polish**: PR #46959 (*composer model selector, per‑model presets*) and PR #46081 (*MoA as virtual provider*) indicate focus on user‑friendly model management.  

https://github.com/NousResearch/hermes-agent/pull/12436  
https://github.com/NousResearch/hermes-agent/pull/36286  
https://github.com/NousResearch/hermes-agent/pull/46094  
https://github.com/NousResearch/hermes-agent/pull/46959  
https://github.com/NousResearch/hermes-agent/pull/46081  

**Prediction:** The next minor release (v0.17.0) will likely include the orchestration package (DAG/A2A), better multi‑provider support, and the desktop UI improvements currently in review.

## 7. User Feedback Summary

Real user pain points expressed in the past 24 hours:

- **Desktop stability on macOS**: Installation/update fails at Electron‑builder stage (#40187).  
- **Database corruption on Windows**: Frequent "session not found" after abnormal shutdown (#47002, #47007).  
- **Gateway reliability**: Telegram adapter freezes after conflict (#40691); Discord pushes excessive notifications (#47004); Feishu code‑block truncation (#46941).  
- **Kanban confusion**: Workers exit with unhelpful "protocol violation" messages (#27178, #46593, #46985).  
- **Session isolation**: Concurrent sessions leak memory and git state across workspaces (#46303).  
- **Model selection UX**: Desktop dropdown silently fails with custom endpoints (#40480, #46961).  
- **Forced responses**: Users want the ability to have an agent remain silent when appropriate (#46917).  
- **Chinese users**: Installation fails behind GFW; request for proxy support (#46839).  
- **Long responses**: Truncation error still a problem despite being closed (#7237).  

Satisfaction signals are sparse; most feedback is centered around bugs and missing features. The high volume of activity suggests an engaged but demanding user base.

## 8. Backlog Watch

Several important issues and PRs have remained unanswered or unmerged for extended periods, requiring maintainer attention:

- **[#16511] – fix(approval): use per‑process UUID as default session key (P1, open since April 27)**  
  Security fix for cross‑session state leaks – still open for over a month.  
  https://github.com/NousResearch/hermes-agent/pull/16511

- **[#10707] – fix(cli): honor config base_url mirror for explicit openrouter provider (P2, open since April 16)**  
  Simple configuration fix that has been waiting for over two months.  
  https://github.com/NousResearch/hermes-agent/pull/10707

- **[#12436] – feat(orchestration): DAG TaskGraph + delegate bridge (open since April 19)**  
  Major feature PR with no recent maintainer activity.  
  https://github.com/NousResearch/hermes-agent/pull/12436

- **[#46675] – Max OAuth requests rejected as third‑party (P1, reported June 15)**  
  No PR yet, blocks Anthropic OAuth users entirely.  
  https://github.com/NousResearch/hermes-agent/issues/46675

- **[#40691] – Telegram Gateway freezes after polling conflict recovery (P1, reported June 6)**  
  Still open without a fix PR.  
  https://github.com/NousResearch/hermes-agent/issues/40691

These items represent both critical stability issues and promising feature work that would benefit from maintainer review and prioritization.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*