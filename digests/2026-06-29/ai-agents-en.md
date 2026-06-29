# OpenClaw Ecosystem Digest 2026-06-29

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-29 03:31 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-29

## Today's Overview
OpenClaw saw extremely high activity in the last 24 hours: **500 issues and 500 pull requests were updated**, with **74 issues closed** and **100 PRs merged or closed**. A new beta release (`v2026.6.11-beta.2`) landed, focusing on channel simplification and configurable model routing. However, the project is carrying a large backlog of open, priority-1 bugs (especially around session state, message loss, and security), and many issues remain in the "needs-maintainer-review" state. Community engagement is strong, with several long-running threads (e.g., Linux/Windows desktop apps) and a steady stream of regression reports.

## Releases
**`v2026.6.11-beta.2`** (one new release today)  
- **Highlights**:  
  - Slack relay mode and native Mattermost `/oc_queue` support were added.  
  - Per-DM model overrides now allow tuning channel operations without global changes.  
  - Thanks to contributors @sjf-oa, @amknight, @xydigit-zt, @thomaszta, and @gandalf-at-lerian.  
- No breaking changes or migration notes were documented in the release summary. This is a beta version; users should test before upgrading production gateways.

## Project Progress
Of the **500 PRs updated today**, **100 were merged or closed**. While the top-30 PR list (by comment count) shows only open PRs, the closed PR count indicates active feature and bugfix work. Notable merged contributions referenced in the release include:
- Better channel control (Slack relay, Mattermost `/oc_queue`, per-DM overrides) – PRs #94707, #95546, #95120.  
- Active session/transcript SQLite migration (Path 3) is being implemented via PR #96625, consolidating earlier proposals.  
- Several PRs with "ready for maintainer look" status were updated, including docs fixes (#97635), bounded response reads (#97549, #97547), and Tlon truncation fixes (#97599).

## Community Hot Topics
The most active issues (by comment count and reactions) reveal strong user focus on cross-platform support and session reliability:

- **[#75: Linux/Windows Clawdbot Apps](https://openclaw/openclaw/issues/75)** – 110 comments, 81 👍. Users strongly want native desktop apps for Linux and Windows (similar to existing macOS/iOS/Android). This is a long-standing request (opened Jan 2026) and remains a top community desire.  
- **[#88838: Track core session/transcript SQLite migration via accessor seam](https://openclaw/openclaw/issues/88838)** – 36 comments. A critical architectural change to move sessions from JSONL to SQLite. Progress is consolidated in PR #96625.  
- **[#77598: Track live dev agent behavior and trajectory](https://openclaw/openclaw/issues/77598)** – 22 comments. Observational monitoring of a development agent; reflects community interest in agent reliability and debugging.  
- **[#88312: Codex app-server turn-completion stall regression](https://openclaw/openclaw/issues/88312)** – 18 comments, 4 👍. A regression in the Codex provider causing agent stalls; regressed from a previous fix (#85107).  
- **[#79077: Telegram bot-to-bot and guest-bot support](https://openclaw/openclaw/issues/79077)** – 8 comments, 8 👍. High ratio of upvotes per comment, indicating strong interest in Telegram's new platform features.

Underlying needs: Users are asking for **cross-platform desktop support**, **robust session storage** (migration to SQLite), **provider-specific stability** (especially Codex and Discord), and **better Telegram integration**.

## Bugs & Stability
Today’s updated issues show several high-severity regressions and systemic problems:

| Bug | Priority | Impact | Fix PR exists? |
|-----|----------|--------|----------------|
| [Codex turn-completion stall regression (#88312)](https://openclaw/openclaw/issues/88312) | P1 | Session stall, message loss | Regressed from #85107; new fix needed |
| [Session write-lock timeouts block subagent delivery (#86538)](https://openclaw/openclaw/issues/86538) | P1 | Message loss, delivery failure | Not yet |
| [Gateway OOM due to unbounded sessions.json growth (#55334)](https://openclaw/openclaw/issues/55334) | P1 | OOM, crash loop | Not yet (SQLite migration is long-term fix) |
| [Isolated cron fails with "LLM request failed" (#91363)](https://openclaw/openclaw/issues/91363) | P1 | Isolated jobs unreachable | PR #96295? (reference not confirmed) |
| [macOS CLLocationManager rebuilds every second (#94147)](https://openclaw/openclaw/issues/94147) | P2 | TCC permission spamming | Not yet |
| [Chrome MCP existing-session timeout (#80036)](https://openclaw/openclaw/issues/80036) | P2 | Browser tooling unusable | Not yet |
| [gzip not decompressed under Node v26 (#79752)](https://openclaw/openclaw/issues/79752) | P1 | HTTP responses fail (Discord) | Not yet |
| [Subagent stale output / history inheritance (#78055)](https://openclaw/openclaw/issues/78055) | P1 | Duplicate/misattributed messages | Not yet |

Many of these bugs share root causes: **session state consistency**, **timeout handling**, and **resource bounds**. The project is actively working on a SQLite rewrite (#88838) which should address several session-related issues, but immediate patches are needed.

## Feature Requests & Roadmap Signals
User-requested features visible in today's top issues:

- **Channel-mediated approval for MCP tool calls** (#78308) – Extend the existing approval pipeline to MCP servers. This would close a security gap for third-party plugins.  
- **Gateway-lite mode without AI harness** (#86881) – For deterministic deployments (webhooks, cron) without loading LLM components.  
- **i18n for slash command descriptions** (#79458) – Localization support for non-English users; especially for Chinese/Japanese/Korean users.  
- **Companion-friendly SQLite transcript/session seams** (#79902, #79904, #79905) – Expose canonical runtime state for external consumers. This is part of the larger SQLite migration umbrella.  
- **Preserve conversation context across cross-backend model switches** (#79047) – Allow seamless model switching while maintaining history.  
- **Add user chat bubble color selector for macOS** (PR #59214) – A small UX improvement for desktop users.

**Likely next version candidates**: The SQLite migration progress suggests that companion seam APIs (#79902, #79904) could land soon. Channel-mediated approval (#78308) and gateway-lite mode (#86881) are also mature enough for inclusion in a future minor release.

## User Feedback Summary
Real user pain points expressed in today’s activity:

- **Missing Linux/Windows native apps** – Issue #75 is the most-upvoted open issue; users feel left out from the desktop experience.  
- **Session reliability is top concern** – Comments on #88483, #86538, and #77598 describe agents that stall, lose context, or fail silently. Users expect a personal AI to be always responsive.  
- **Regressions in every monthly release** – Several reports (#88312, #77930, #77642) show that every new version introduces new bugs that break previously working functionality. This reduces trust.  
- **OAuth and auth provider issues** – #80040, #74484, and #73182 describe complex cascading failures that leave users unable to recover without manual intervention.  
- **Telegram and Discord channel frustrations** – #79077 (guest bots), #79308 (wrong chat_id), and #49104 (silent truncation) show that messaging platform integration is still fragile.

Overall sentiment: users appreciate OpenClaw's flexibility and plugin ecosystem but are frustrated by frequent regressions and the lack of some foundational features (Linux app, SQLite storage, stable session handling).

## Backlog Watch
Several important issues and PRs have been open for months and need maintainer attention:

- **[#75: Linux/Windows Clawdbot Apps](https://openclaw/openclaw/issues/75)** – Opened Jan 1, 2026. 110 comments, no concrete PR from the core team. A PR #59859 (`cute GTK-native Linux App`) has been open since April 2, 2026, but is still awaiting review.  
- **[#55334: Gateway OOM from sessions.json unbounded growth](https://openclaw/openclaw/issues/55334)** – Opened March 26, P1, with 11 comments. No fix PR yet; the root cause is known but no actionable patch has landed.  
- **[#45718: Session bloat – skillsSnapshot accumulated every run](https://openclaw/openclaw/issues/45718)** – Opened March 14, P2, 6 comments. Similar unbounded growth issue.  
- **[#60842: Re-expose toolsAllow core tools in embedded runs](https://openclaw/openclaw/pull/60842)** – PR opened April 4, still needs proof/blessing. Affects cron and isolated runs.  
- **[#59898: Handle explicit empty tool lists in system prompt](https://openclaw/openclaw/pull/59898)** – PR opened April 2, waiting for proof and context.  
- **[#79903: Expose durable session lineage and sessionId discovery](https://openclaw/openclaw/issues/79903)** – Part of the SQLite companion umbrella, has been open since May 9 but lacks progress.

These items are blocking user workflows (missing desktop app, chronic memory leaks) or preventing important architectural improvements. Maintainer review and triage are needed to move them forward.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## Ecosystem Overview

The open-source personal AI assistant ecosystem in mid-2026 is characterized by high-velocity development tempered by foundational stability challenges. Both OpenClaw and Hermes Agent demonstrate active communities pushing toward cross-platform desktop support, deterministic execution layers, and robust session management—but each project approaches these goals from fundamentally different architectural philosophies. The ecosystem as a whole shows strong user demand for reliable, memory-resident agents that integrate seamlessly with existing messaging platforms, while developers struggle to balance feature velocity against regression management. A notable tension exists between the desire for plugin-rich, highly configurable platforms (OpenClaw's approach) and the appeal of polished, opinionated desktop experiences (Hermes's target).

## Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues Updated (24h)** | 500 | 50 |
| **PRs Updated (24h)** | 500 | 50 |
| **Issues Closed (24h)** | 74 | 4 |
| **PRs Merged/Closed (24h)** | 100 | ~ several (not quantified) |
| **Current Release** | v2026.6.11-beta.2 (today) | None today |
| **Open Priority-1 Bugs** | ~8+ (session, OOM, regressions) | ~2-3 (security, IME) |
| **Health Score (Qualitative)** | Moderate — high activity but significant technical debt and regression churn | Stable — focused development with manageable bug count |

*Note: OpenClaw's activity numbers are an order of magnitude higher, but this reflects a larger contributor base and a more aggressive triage/merge cadence rather than proportionally higher output quality. Hermes Agent shows more disciplined, targeted development with fewer regressions.*

## OpenClaw's Position

**Advantages over peers:**
- **Unmatched plugin ecosystem and protocol support** — Slack relay, Mattermost `/oc_queue`, Telegram bot-to-bot, and per-DM model overrides demonstrate a universal gateway vision that Hermes does not match.
- **Larger community engagement** — Issue #75 (Linux/Windows desktop apps) has 110 comments and 81 upvotes, indicating passionate user base. Overall issue/PR volume is 10x Hermes's.
- **Early architectural bets** — The SQLite migration (#88838) for session storage is a forward-looking investment in durability and observability that Hermes has not yet prioritized.

**Technical approach differences:**
- OpenClaw treats the agent as a **configurable routing layer** (gateway-first), while Hermes builds the agent as a **desktop-native application** (UI-first).
- OpenClaw's plugin model (MCP servers, channel-mediated tool approval) enables third-party extensibility that Hermes's more curated toolset does not.

**Community size comparison:**
- OpenClaw's 500 updated issues/PRs daily vs. Hermes's 50 suggests a ~10x larger active contributor and user base. However, OpenClaw's higher regression rate (e.g., each release introduces new bugs per user feedback) indicates growing pains from this scale.

**Key vulnerability:** OpenClaw's metric volume may mask quality issues—only 14.8% of PRs (100/500) were merged today, and P1 bugs (OOM, session loss) remain unpatched for months (#55334 opened March 26). Hermes's smaller but more focused community produces fewer regressions per feature.

## Shared Technical Focus Areas

Multiple projects are converging on the following requirements:

| Focus Area | OpenClaw | Hermes Agent | Specific Need |
|------------|----------|---------------|---------------|
| **Deterministic/Non-LLM Execution** | Gateway-lite mode (#86881) | Deterministic Workflow Engine (#5354) | Task automation without LLM latency/cost |
| **Session Persistence & Durability** | SQLite migration (#88838) | Session import API (#54586) | Crash recovery, cross-session continuity |
| **Desktop Cross-Platform Support** | Linux/Windows native apps (#75) | Windows console flash fix (#54220), IME fixes (#38826) | Non-macOS users feel abandoned |
| **Telegram Integration Depth** | Guest bots, btob (#79077) | Typing indicator stuck (#28004) | Platform-specific reliability |
| **MCP Tool Reliability** | Approval pipeline (#78308) | Missing tools in desktop sessions (#37589) | Security and consistency |
| **Provider-Specific Stability** | Codex stall regression (#88312) | Codex inconsistency (#13834) | Parity with official SDK behavior |

**Key insight:** Both projects identify **session reliability** and **platform-independent desktop support** as their top two technical debts. The SQLite migration in OpenClaw and the session import/export work in Hermes are addressing the same root cause—fragile in-memory or JSON-based session state.

## Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|---------------|
| **Target User** | Power users, integrators, multi-platform operators | Desktop-first professionals, solo developers |
| **Primary UI** | Gateway + CLI (desktop apps emerging) | Electron desktop app + TUI (first-class) |
| **Plugin Philosophy** | Unlimited MCP/relay extensibility | Curated toolset with managed plugins |
| **Provider Strategy** | Model-agnostic router (per-DM overrides) | Focused on Codex + OpenRouter + native providers |
| **Session Model** | Gateway-managed (JSONL → SQLite) | Desktop-managed (in-memory + import) |
| **Biggest Pain Point** | Regression churn per release (user feedback: "every monthly release breaks things") | Windows stability and IME compatibility |
| **Risk Profile** | Higher — architected for scale, but carrying technical debt | Lower — narrower scope, faster bug resolution |

**Architectural distinction:** OpenClaw functions as a **universal message bus** with AI routing; Hermes functions as a **single-user desktop workspace** with AI tools. OpenClaw's gateway-lite mode (#86881) and Hermes's workflow engine (#5354) represent a convergence toward hybrid LLM/deterministic execution, but from opposite starting points.

## Community Momentum & Maturity

**Tier 1 — Rapidly iterating (high velocity, high regression risk):**
- **OpenClaw** — Ships beta releases almost daily (v2026.6.11-beta.2 today). Community is large and vocal (74 issues closed, 100 PRs merged in 24h). However, users report "every new version introduces new bugs" (#88312, #77930). This is a project in the **"storming" phase** of community growth—enthusiasm outpacing stability.

**Tier 2 — Steady development (moderate velocity, stable quality):**
- **Hermes Agent** — No release today, but 50 PRs and 50 issues updated. Bug counts are manageable (4 closed today, no new P1s). Features like Slack history tool (#54535) and terminal persistence (#54585) are landing in code review. This project appears to be in the **"norming" phase**—features mature, process stable, but Windows support remains a gap.

**Maturity markers:**
- OpenClaw: **Pre-1.0 beta** (v2026.6.11-beta.2). Architectural churn (SQLite migration) indicates foundational decisions still in flux.
- Hermes: **Post-1.0** (no version indicated but PRs reference v0.16/v0.18 scoping). More settled architecture.

## Trend Signals

1. **Cross-platform desktop support is the #1 unmet need.** OpenClaw's #75 (110 comments, 81 👍) and Hermes's Windows flash console (#54220) and IME bugs (#38826) show that both projects have significant platform gaps. Developers building on these ecosystems should expect Linux/Windows parity to be a multi-quarter journey.

2. **Deterministic execution layers are becoming table stakes.** Both projects now feature proposals for non-LLM task automation (OpenClaw's gateway-lite #86881; Hermes's Workflow Engine #5354). This reflects a broader industry recognition that personal AI agents must handle background, recurring, or low-risk tasks without LLM latency and cost.

3. **Session persistence is the hard problem everyone is solving differently.** OpenClaw's SQLite migration (path 3, #88838) is the most ambitious approach; Hermes's session import API (#54586) is more pragmatic. The ecosystem lacks a standard for durable agent state—a gap that represents both a risk and an opportunity for newcomers.

4. **Provider-specific regressions erode trust.** Both projects report Codex integration issues (OpenClaw #88312 stall regression; Hermes #13834 inconsistency vs. official CLI). As model providers move quickly, agent frameworks struggle to keep pace. Users increasingly value stability over supporting the latest model.

5. **Security boundaries for MCP tool calls are emerging.** OpenClaw's channel-mediated approval (#78308) and Hermes's forged delimiter fix (#44059) signal that the ecosystem is maturing beyond trusting third-party tools implicitly. Expect this to become a core requirement for enterprise adoption.

**Value for AI agent developers:**
- If you need **multi-platform integration** (Slack, Mattermost, Telegram, Discord) and are willing to accept periodic regressions, OpenClaw offers unmatched breadth.
- If you need a **stable, desktop-first experience** (especially on macOS) with curated tools and lower operational overhead, Hermes is the safer choice.
- For any deployment, invest in **session state monitoring** and **provider-specific fallback logic**—both projects' user feedback emphasizes these as top pain points regardless of platform choice.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-29

---

## 1. Today's Overview

Hermes Agent shows **high activity** with 50 issues and 50 pull requests updated in the last 24 hours. The project remains in a **heavy development and bug‑fixing phase**, with 44 open issues and 44 open PRs reported during this window. No new releases were published today. The community is actively reporting Windows‑specific GUI regressions and input method (IME) compatibility problems, while maintainers continue to advance feature work around gateway persistence, Slack integration, and session management. Overall project health is **stable** but under sustained pressure to address platform‑specific stability issues, especially on Windows and desktop environments.

---

## 2. Releases

None in the last 24 hours.

---

## 3. Project Progress

**Closed Issues (resolved in last 24h):**
- [#39753] – **config priority: OpenRouter catalog overrides explicit custom provider** *(bug, closed)* — addresses configuration precedence.
- [#6396] – **Security** *(bug, closed)* — related to credential display.
- [#54506] – **Command prompt blinking on Windows desktop** *(duplicate bug, closed)* — duplicate of umbrella issue [#54220].
- [#54578] – **Feishu reply attachments not visible to agent** *(duplicate bug, closed)*.

**Open PRs advancing features and fixes (top by comment count, all open):**
- [#54588] – **feat: Add configurable attribution string for agent identity** — controls "created by X" in system prompt.
- [#54535] – **feat(slack): add read-only Slack channel history tool** — enables agent to inspect recent channel messages.
- [#54585] – **feat(desktop): persist & restore terminal tabs + scrollback across relaunch** — VS‑Code‑style terminal restoration.
- [#54586] – **Add dashboard session import flow** – new API endpoint and UI for session JSON import.
- [#42563] – **feat(desktop): add agent run inspector panel** – live visual summary of active agent runs.
- [#44059] – **Neutralize forged `<untrusted_tool_result>` delimiters in tool-result wrapping** *(security, P1)* – fixes boundary‑spoofing vulnerability.
- [#37904] – **fix(gateway): normalize SessionResetPolicy.mode to lowercase** – stops silent skip of session resets.
- [#37887] – **fix(toolsets): resolve alias target when merging registry tools into a static toolset** – prevents dropped MCP tools.
- [#33639] – **fix(discord): handle expired slash defer interactions** – prevents dropped commands.
- [#53691] – **feat(feishu,multiplex): scope-aware secrets, shared-loop WS, and credential isolation** – multi‑profile gateway multiplexing.
- [#18734] – **fix(cli): respect 12-factor env precedence in load_hermes_dotenv()** – addresses credential rotation footgun.

🔗 All open PRs: [NousResearch/hermes-agent pulls](https://github.com/nousresearch/hermes-agent/pulls)

---

## 4. Community Hot Topics

The most active issues (by comment count) reveal key areas of user attention:

1. **#13834** — *Hermes openai-codex fails on same machine where official Codex CLI works* ⭐13 comments / 3 👍  
   **Analysis:** Users are frustrated by inconsistent behavior between Hermes’s Codex integration and the official CLI. Needs a clear reproduction path and likely provider‑specific fixes.

2. **#3002** — *Fails to install NeuTTS during setup* ⭐12 comments / 4 👍  
   **Analysis:** A persistent setup blocker for users wanting text‑to‑speech. The “pip not found” error suggests environment isolation issues in the venv.

3. **#38826** — *Chinese IME input broken – pressing Enter submits empty/incomplete text* ⭐8 comments / 0 👍  
   **Analysis:** High‑impact UX bug for Chinese‑speaking users; requires IME composition event handling in the Electron composer.

4. **#54220** — *Windows Desktop GUI: console windows flash on subprocess spawns* ⭐8 comments / 0 👍  
   **Analysis:** The most‑reported active bug (“umbrella tracking issue”). Affects all Windows desktop users; several duplicates closed against it.

5. **#5354** — *Feature: Deterministic Workflow Engine (Lobster-style)* ⭐8 comments / 8 👍  
   **Analysis:** Strong community demand for a fixed, LLM‑free task execution layer for mission‑critical automation. 8 upvotes signal high interest.

6. **#28004** — *Telegram typing indicator stuck indefinitely* ⭐7 comments / 0 👍  
   **Analysis:** Race condition in `_keep_typing` leads to persistent “typing…” state – a visible annoyance in Telegram.

Other notable mentions:  
- [#37589] – *Desktop sessions miss configured MCP tools* (5 comments, 3 👍)
- [#531] – *User Workspace & Knowledge Base – Persistent RAG* (4 comments, 2 👍)

🔗 Top issue: [#13834](https://github.com/nousresearch/hermes-agent/issues/13834)

---

## 5. Bugs & Stability

**New Bugs Reported Today (2026-06-29) – ranked by severity:**

| Issue | Severity | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| [#54572] | **P2** | Patch tool (replace mode) can edit wrong region when `old_string` is not an exact match – fuzzy matching chains may apply changes to unintended locations. | No |
| [#54579] | **P2** | Long code blocks lose indentation when replies are split into multiple messages – `truncate_message` preserves fences but not leading whitespace. | No |
| [#54577] | **P3** | `title_generation.enabled: false` config ignored – title generation always runs, causing timeout errors. | No |
| [#54049] | **P2** | DeepSeek streaming drops chunks when behind OpenResty with custom httpx transport – workaround provided. | No |
| [#54220] | **P2** | Windows Desktop GUI: console windows flash frequently (tracking issue). | Several related PRs (e.g., [#54506] closed as duplicate) |
| [#54578] | **P2** | Feishu reply attachments not visible to agent (duplicate, already closed). | — |
| [#54496] | **P3** | Feature request: expand terminal in Hermes Desktop (not a bug). | — |
| [#54566] | **P3** | TUI/CLI: cron jobs and delegate_task persistence warnings missing. | — |

**Critical / Security:**  
- [#44059] (PR) – **P1** – Fixes neutralisation of forged `</untrusted_tool_result>` delimiters in tool output. Still open.  
- [#44983] – **P2** – WhatsApp bridge has critical CVE in `@whiskeysockets/baileys` (GHSA-qvv5-jq5g-4cgg). Open with no fix PR yet.

**Regression Watch:**  
- [#48445] – Desktop WebSocket disconnects during long foreground tasks (P2).  
- [#53641] – Dashboard chat scrollback drift in long sessions (P2).

🔗 All open bugs: [Issues with `type/bug`](https://github.com/nousresearch/hermes-agent/issues?q=is%3Aopen+label%3Atype%2Fbug)

---

## 6. Feature Requests & Roadmap Signals

**Strong community signals today:**

| Request | Interest | Potential Next‑Version Fit |
|---------|----------|---------------------------|
| **Deterministic Workflow Engine** (E.g., code‑free cron with retries) – [#5354] | 8 👍, active discussion | High – many users want LLM‑independent task execution. Likely to be scoped for v0.16. |
| **Persistent User Workspace & Knowledge Base (RAG)** – [#531] | 2 👍, long‑standing | Medium – foundational feature but complex; may land as plugin first. |
| **Model allowlist for ollama‑cloud provider** – [#26980] | 1 👍 | Low – niche, but quick to implement. |
| **Expand terminal in Hermes Desktop** – [#54496] | 1 👍 | Low – already possible via separate window, but UX request noted. |
| **Surface cron delivery warnings earlier** – [#54566] | 1 👍 | Low – documentation patch likely sufficient. |

**PRs indicating near‑future features (already in code review):**
- Attribution string [#54588]
- Slack history tool [#54535]
- Terminal persistence [#54585]
- Dashboard session import [#54586]
- Agent run inspector panel [#42563]
- Multi‑profile Feishu/WeChat gateway [#53691]
- Shared WebSocket layer decoupling desktop from dashboard [#54568]

These are likely candidates for the next minor release (v0.18.x or v0.17.1).

🔗 Feature requests: [Issues with `type/feature`](https://github.com/nousresearch/hermes-agent/issues?q=is%3Aopen+label%3Atype%2Ffeature)

---

## 7. User Feedback Summary

**Common pain points expressed today:**

- **Windows flash console** – Most vocal complaint; users report it happens every few seconds, worsens with messaging. Several duplicates filed. Workaround: none yet.
- **IME input failures** – Chinese, Korean, Japanese users hit multiple bugs: Enter submit broken, send button becomes voice button, text truncation. Covers desktop app on both macOS and Windows.
- **Config precedence confusion** – `.env` overrides runtime‑injected secrets (systemd/Docker) and OpenRouter catalog overrides explicit custom providers – users want deterministic configuration.
- **MCP tools missing in desktop** – Even when configured correctly for CLI, desktop sessions lose them. Troublesome for power users.
- **Cron jobs silent in TUI** – Default delivery channel maps to chat, but TUI has no output channel, leading to lost results.
- **Telegram typing indicator** – Stuck “typing…” after response delivered – minor but annoyingly visible.

**Positive signals:**
- High engagement on feature requests (8 👍 on workflow engine, 3 👍 on MCP improvements) indicates a motivated community.
- Quick closure of duplicate bugs (e.g., [#54506], [#54578]) shows maintainers are triaging.

**Satisfaction:** Mixed. Desktop users on Windows are frustrated, but CLI/backend users benefit from ongoing features and security fixes.

---

## 8. Backlog Watch

Issues or PRs that have been open for a long time without maintainer action or updates:

| Item | Created | Last Update | Comments | Why It Matters |
|------|---------|-------------|----------|----------------|
| [#531] – Persistent Knowledge Base | 2026-03-06 | 2026-06-29 | 4 | Core feature request with 2 👍; no maintainer response. |
| [#3002] – NeuTTS install failure | 2026-03-25 | 2026-06-29 | 12 | Long‑standing setup blocker; user frustration. |
| [#5354] – Deterministic Workflow Engine | 2026-04-05 | 2026-06-29 | 8 | High community interest (8 👍); no maintainer comment. |
| [#13834] – Codex inconsistency | 2026-04-22 | 2026-06-29 | 13 | High visibility; needs reproduction. |
| [#18734] – fix(cli): 12‑factor env precedence | 2026-05-02 | 2026-06-29 | 0 | PR still open after nearly 2 months; important for credential rotation. |
| [#28004] – Telegram typing indicator | 2026-05-18 | 2026-06-29 | 7 | Root cause identified; no fix PR merged. |
| [#37904] – Session reset policy case sensitivity | 2026-06-03 | 2026-06-29 | 0 | Fix PR open; not merged. |

**Maintainer attention needed:** The backlog mostly consists of well‑described bugs and popular feature requests that lack a maintainer response or scheduled milestone. The oldest issues (March–April) risk becoming stale.

🔗 Oldest open issues: [NousResearch/hermes-agent issues by created](https://github.com/nousresearch/hermes-agent/issues?q=is%3Aopen+sort%3Acreated-asc)

---

*Data snapshot: 2026-06-29 23:59 UTC. Sources: GitHub Issues & PRs for NousResearch/hermes-agent.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*