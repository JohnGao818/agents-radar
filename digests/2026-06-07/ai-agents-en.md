# OpenClaw Ecosystem Digest 2026-06-07

> Issues: 296 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-07 03:30 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-07

## 1. Today’s Overview

OpenClaw shows extremely high activity with **296 issues updated** in the last 24 hours (150 open/active, 146 closed) and **500 pull requests updated** (397 open, 103 merged/closed). Two new beta releases (v2026.6.5‑beta.1 and v2026.6.5‑beta.2) were published, focusing on QQBot thinking-strip safety and MCP tool result coercion. The project is under heavy development with a large proportion of merged PRs, indicating a strong fix-forward cadence, but several high‑severity regressions (especially around the 2026.6.1 upgrade) are causing community frustration.

## 2. Releases

**v2026.6.5‑beta.2** and **v2026.6.5‑beta.1** were released in the last 24 hours.

### Highlights (both betas)  
- **QQBot**: Model reasoning/thinking scaffolding (e.g., `<thinking>` tags) is now stripped before delivery, preventing raw cognitive content from leaking into channel replies. (Issues [#89913](https://github.com/openclaw/openclaw/issues/89913), [#90132](https://github.com/openclaw/openclaw/issues/90132))
- **MCP tool results**: The runtime now coerces `resource_link`, `resource`, `audio`, and malformed image fields, adding forward‑compatibility for future MCP extensions.

No breaking changes or migration notes were announced.

## 3. Project Progress — Merged/Closed PRs

Of the 103 merged/closed PRs in the last 24 hours, several notable ones appear in the top‑30 list:

- **[#91073 – fix(openrouter): reconcile streamed generation cost](https://github.com/openclaw/openclaw/pull/91073)** – Merged. Corrects cost accounting for OpenRouter streaming completions.
- **[#91072 – refactor(memory‑wiki): store source sync state in sqlite](https://github.com/openclaw/openclaw/pull/91072)** – Merged. Moves imported‑source checkpoints from JSON to SQLite, improving reliability and capacity management.
- **[#91032 – docs(imessage): require DisableLibraryValidation on modern macOS](https://github.com/openclaw/openclaw/pull/91032)** – Closed/merged. Updates documentation for macOS 26 Tahoe injection gates.
- **[#90978 – docker fix (summary missing)](https://github.com/openclaw/openclaw/pull/90978)** – Closed.

Key areas advanced: **OpenRouter monetization**, **Memory Wiki state management**, **iMessage channel resilience**, and **Feishu rate‑limit retry** (PR [#89659](https://github.com/openclaw/openclaw/pull/89659) still open but progressed).

## 4. Community Hot Topics

Issues and pull requests with the highest engagement (comments and reactions) reveal deep operational pain points.

### Top Issues

1. **[#90083 – OpenAI ChatGPT Responses transport fails with invalid_provider_content_type for gpt‑5.4/gpt‑5.5](https://github.com/openclaw/openclaw/issues/90083)**  
   **14 comments, 3 👍**  
   *User pain*: After upgrading to 2026.6.1, the `openai-chatgpt-responses` transport breaks for newer GPT models with `invalid_provider_content_type`. Users cannot use the latest OpenAI models.  
   *Underlying need*: Critical regression blocking production model use.

2. **[#88312 – [Regression] Codex app‑server turn‑completion stall returns](https://github.com/openclaw/openclaw/issues/88312)**  
   **13 comments, 3 👍**  
   *User pain*: Multi‑tool agent turns fail with “Codex stopped before confirming the turn was complete” starting in 2026.5.27. This is a regression of a previously fixed issue (#84076).  
   *Underlying need*: Reliable Codex agent execution.

3. **[#88929 – Feishu streaming card: abnormal typewriter effect and truncated final content](https://github.com/openclaw/openclaw/issues/88929)**  
   **11 comments, 2 👍**  
   *User pain*: In Feishu channel streaming with card render, replies appear 1-2 characters at a time and final content is truncated to a single character.  
   *Underlying need*: Usable streaming output in Feishu channel.

4. **[#90991 – Cron scheduled trigger contaminates global runtime state](https://github.com/openclaw/openclaw/issues/90991)**  
   **7 comments, 1 👍**  
   *User pain*: A cron trigger causes transient system‑wide overload failures, affecting all sessions.  
   *Underlying need*: Isolated cron execution that does not leak into global state.

### Top Pull Requests (by engagement – few comments, but priority flags)

- **[#89659 – fix(feishu): retry on send rate‑limit errors (P1)](https://github.com/openclaw/openclaw/pull/89659)** – 0 comments but marked P1 and ready for maintainer look. Addresses Feishu send rate‑limiting.
- **[#90101 – feat: runtime self context config and tool (XL, feature showcase)](https://github.com/openclaw/openclaw/pull/90101)** – 0 comments but large PR adding new ability to provide runtime context to the model.
- **[#78441 – feat(subagents): forward toolsAllow from sessions_spawn](https://github.com/openclaw/openclaw/pull/78441)** – 0 comments but long‑running PR (since May) for subagent tool policy.

## 5. Bugs & Stability

Several high‑severity bugs were newly reported or escalated in the last 24 hours, many tied to the 2026.6.1 release. No fix PRs are yet attached to the most critical reports.

### Critical / P1 Regressions

| Issue | Description | Impact | Fix PR |
|-------|-------------|--------|--------|
| [#91018](https://github.com/openclaw/openclaw/issues/91018) | ⚠️ DeepSeek prompt cache broken after upgrade to 2026.6.1 – $6 burned in one hour | $ cost explosion, provider inefficiency | None |
| [#90991](https://github.com/openclaw/openclaw/issues/90991) | Cron trigger contaminates global runtime state causing system‑wide overload | Complete service degradation | None |
| [#90925](https://github.com/openclaw/openclaw/issues/90925) | Subagent announce compaction for Codex/OAuth falls into openai‑responses API‑key route | Agent collaboration broken for OAuth users | None |
| [#90886](https://github.com/openclaw/openclaw/issues/90886) | Gateway hangs at `[gateway] starting...` when configured provider lacks credentials | Startup failure | None |
| [#90083](https://github.com/openclaw/openclaw/issues/90083) | ChatGPT Responses transport fails with `invalid_provider_content_type` for gpt‑5.4/5.5 | Model unusable | None |

### High‑Impact (P1/P2) – Already Open or New

- [#90916](https://github.com/openclaw/openclaw/issues/90916) – Topic‑session families (P2, feature request but also a stability concern for context isolation).
- [#90595](https://github.com/openclaw/openclaw/issues/90595) – Cron run “failed” notifications fire during hot reload, causing alert fatigue (P2).
- [#91042](https://github.com/openclaw/openclaw/issues/91042) – Reply‑context body truncation needs to cover additional JSON paths (P2, follow‑up to previous fix).

### General Stability Observations

The 2026.6.1 upgrade appears to be the root cause of multiple regressions, particularly around **model provider transports** (OpenAI, DeepSeek) and **cron execution** state isolation. The project would benefit from a hot‑fix release targeting these.

## 6. Feature Requests & Roadmap Signals

The community is requesting several forward‑looking features. Based on existing open PRs and maintainer prioritization tags, the following may land in the next minor release:

### Likely to Ship Soon (PRs exist with “ready for maintainer look” or “proof supplied”)

- **Runtime Self Context** (PR [#90101](https://github.com/openclaw/openclaw/pull/90101)) – Config‑backed context that lets the model know its runtime environment. High synergy with offload/cost awareness.
- **Model Picker Agent Runtimes** (PR [#90328](https://github.com/openclaw/openclaw/pull/90328)) – Expose non‑default agent runtimes in the WebUI model picker (e.g., “GPT‑5.5 · OpenAI Codex”).
- **Subagent toolsAllow forwarding** (PR [#78441](https://github.com/openclaw/openclaw/pull/78441)) – Allow parent sessions to restrict subagent tool access.
- **Policy for exec approvals** (PR [#90003](https://github.com/openclaw/openclaw/pull/90003)) – Add redacted policy coverage for the `exec-approvals.json` artifact.

### High‑Demand Features Without Open PRs

- **Topic‑session families** (Issue [#90916](https://github.com/openclaw/openclaw/issues/90916)) – Multiple named context lanes for a single assistant.
- **More local providers** (Issue [#89265](https://github.com/openclaw/openclaw/issues/89265)) – Treat local models as first‑class citizens.
- **Bounded/validated append semantics for pre‑compaction memory flush** (Issue [#90354](https://github.com/openclaw/openclaw/issues/90354)).
- **Gateway‑side circuit breaker for unhealthy sessions** (Issue [#62615](https://github.com/openclaw/openclaw/issues/62615)).

### Strategic Direction Signals

The project is investing heavily in **runtime awareness**, **subagent governance**, and **provider‑agnostic model handling**. The addition of MCP result coercing in the latest betas also suggests growing support for the Model Context Protocol.

## 7. User Feedback Summary

### Pain Points (dissatisfaction)

- **Upgrade horrors**: “Upgrade 2026.6.1 broke DeepSeek prompt cache – $6 burned in one hour” ([#91018](https://github.com/openclaw/openclaw/issues/91018)) is the most visceral. Users are financially impacted.
- **Regression fatigue**: Multiple threads (e.g., [#88312](https://github.com/openclaw/openclaw/issues/88312), [#90083](https://github.com/openclaw/openclaw/issues/90083)) express frustration that previously fixed bugs (Codex stall, ChatGPT transport) have returned.
- **Cron unpredictability**: Cron triggers causing system‑wide overload ([#90991](https://github.com/openclaw/openclaw/issues/90991)) and false failure notifications ([#90595](https://github.com/openclaw/openclaw/issues/90595)) undermine trust in scheduled tasks.

### Satisfaction / Positive Signals

- **QQBot thinking‑strip fix** (in both beta releases) received community thanks (user `@openperf` acknowledged).
- **Feishu retry logic PR** ([#89659](https://github.com/openclaw/openclaw/pull/89659)) addresses a long‑standing rate‑limit issue, appreciated by Feishu channel users.
- **iMessage documentation updates** ([#91032](https://github.com/openclaw/openclaw/pull/91032)) show responsiveness to macOS evolution.

### Use Cases Highlighted

- DeepSeek V4 Flash with prompt cache (cost‑sensitive large‑scale deployment)
- Feishu as a primary channel (especially in Asian markets)
- Codex/OAuth flows (ChatGPT Plus integration)
- Multi‑agent subagent workflows (compaction, announce routing)

## 8. Backlog Watch

Several important issues and PRs have been waiting for maintainer attention for weeks or months. These are tagged with `clawsweeper:needs-maintainer-review` or similar.

### Long‑Standing Issues (created >30 days, P1/P2, no fix)

| Issue | Priority | Created | Summary | Status |
|-------|----------|---------|---------|--------|
| [#49603](https://github.com/openclaw/openclaw/issues/49603) | P1 | 2026‑03‑18 | Orphaned lock files not cleared on

---

## Cross-Ecosystem Comparison

## Cross-Project Comparison Report: OpenClaw & Hermes Agent (2026-06-07)

### 1. Ecosystem Overview
The personal AI assistant/agent open-source ecosystem is experiencing an intense phase of rapid iteration, with projects like **OpenClaw** and **Hermes Agent** showing extremely high activity levels. Both communities are pushing toward production-grade reliability while introducing new capabilities such as Model Context Protocol (MCP) support, subagent orchestration, and multi-channel deployment (QQBot, Feishu, Telegram). However, the breakneck release cadence is causing regression fatigue (especially in OpenClaw) and highlighting gaps in cross-platform stability (especially on macOS in Hermes). Security vulnerabilities are being disclosed and patched transparently, reflecting a maturing approach to safety. Overall, the ecosystem is bifurcating between "platform-like" projects (OpenClaw, focused on provider diversity and enterprise channels) and "personal desktop" projects (Hermes, focused on TUI/plugin UX), with both sharing core concerns around agent autonomy, cost management, and subagent governance.

### 2. Activity Comparison

| Metric                    | OpenClaw                              | Hermes Agent                        |
|---------------------------|---------------------------------------|-------------------------------------|
| **Issues updated (24h)**  | 296 (150 open, 146 closed)            | 50 (38 open, 12 closed)             |
| **PRs updated (24h)**     | 500 (397 open, 103 merged/closed)     | 50 (40 open, 10 merged/closed)      |
| **Releases (24h)**        | 2 beta releases (v2026.6.5-beta.1/2)  | None (latest stable v0.16.0)        |
| **Health Score**          | **Moderate** – high churn; multiple P1 regressions from recent upgrade (2026.6.1) causing cost blowups and transport failures, but strong fix-forward cadence | **Good** – rapid security response (RCE fix, Honcho injection patch); fewer regressions, but minor cross-platform friction and long-standing bugs |

- OpenClaw’s raw volume is ~6x higher on issues and ~10x higher on PRs, indicating a much larger community and/or more automated processes (bots).
- OpenClaw is releasing betas daily, while Hermes is in a more conservative release cycle (no new release today).

### 3. OpenClaw’s Position
**Advantages over peers:**
- **Scale & velocity**: With 500 daily PRs and a massive issue tracker, OpenClaw is clearly the most active project in the ecosystem, attracting a wide contributor base.
- **Provider diversity**: Deep integration with OpenRouter, DeepSeek, ChatGPT Responses, Feishu, QQBot, and MCP. Hermes focuses more on local/TUI providers.
- **Maturity on enterprise channels**: Feishu rate-limit retry, QQBot thinking-strip safety, iMessage macOS 26 injection – shows strong channel support for Asian markets and corporate use.
- **Subagent governance**: PR #78441 (toolsAllow forwarding) and #90101 (runtime self-context) represent advanced agent coordination patterns.

**Technical approach differences:**  
OpenClaw uses a **gateway + memory wiki + SQLite** architecture with heavy emphasis on provider abstraction and MCP integration, while Hermes emphasizes **plugins, kanban-style goals, and TUI/Desktop UX**.

**Community size comparison:**  
OpenClaw’s daily issue/PR volume is 6–10x higher than Hermes, suggesting a much larger user and developer base. However, a proportion of OpenClaw’s closed issues may be automated (bot-triaged). Hermes’ community is smaller but vocal, with detailed bug reports and feature requests.

### 4. Shared Technical Focus Areas
The following concerns are common to both projects, indicating ecosystem-wide priorities:

| Area                | OpenClaw (specifics)                          | Hermes Agent (specifics)                  |
|---------------------|-----------------------------------------------|-------------------------------------------|
| **Subagent delegation** | PR #78441 (toolsAllow forwarding from parent) | PR #40946 (`delegate_task(background=true)`) |
| **Cron/scheduled task stability** | Issue #90991 (cron contaminates global state) | Issue #40801 (cron script-path guard rejection) |
| **Security hardening** | – (no explicit security issues this period, but MCP result coercion suggests input validation) | CVE-grade RCE (TUI gateway), Honcho injection patch |
| **Cost optimization** | Issue #91018 (DeepSeek prompt cache broken, $6/hour) | – (not a major topic in this digest) |
| **Multi-channel streaming** | Feishu streaming truncation (Issue #88929) | Telegram auth bypass (Issue #40863) |
| **macOS compatibility** | iMessage docs update (PR #91032) | Multiple macOS issues: launchd, Intel support, installer spaces |
| **Plugin/Memory state management** | Memory wiki SQLite refactor (PR #91072) | Context-length cache atomic write fix (PR #40919) |

Both projects are investing in **isolation of background tasks**, **secure subagent operations**, and **platform-specific reliability**.

### 5. Differentiation Analysis

| Dimension              | OpenClaw                                     | Hermes Agent                               |
|------------------------|----------------------------------------------|--------------------------------------------|
| **Primary target users**   | Developers building multi-provider, multi-channel agent platforms (enterprise & power users) | Individual users seeking a personal AI desktop/TUI assistant (consumer & power users) |
| **Core architecture**      | Gateway → Provider adapters → Memory wiki → Subagents; MCP-native | Plugin system → Kanban goals → Desktop/TUI → Background delegation |
| **Communication channels** | QQBot, Feishu, iMessage, OpenRouter, ChatGPT, MCP | Telegram, Discord, WhatsApp, CLI/TUI, Web UI |
| **Release cadence**        | Near-daily betas, fast iteration but high regression risk | Slower, more stable releases; security hotfixes |
| **Community engagement**   | Large, diverse, but some frustration with upgrade pain | Smaller but highly detailed bug reports; strong feature requests |
| **Key differentiator**     | **Provider & channel agnosticism** with MCP support | **Desktop UX & plugin extensibility** with goal lifecycle |

OpenClaw is building a **platform for agent engineers**; Hermes is building a **personal assistant for end-users**.

### 6. Community Momentum & Maturity
- **Tier 1 (Rapid iteration, high churn)**: **OpenClaw** – extreme activity, daily releases, but suffers from significant regression issues (e.g., #90083, #90991, #91018). The project is clearly in a “move fast and fix things” phase, with a strong core team but some operational debt.
- **Tier 2 (Steady growth, stability focus)**: **Hermes Agent** – high activity but more controlled; security incidents handled within 24 hours with patches. The community is growing but not yet overwhelmed by regression volume. Long-standing bugs (#6718, #8125) indicate areas needing sprint focus.
- **Overall ecosystem maturity**: Both projects are **pre-stable**; neither has a 1.0 release. OpenClaw’s recent regressions suggest it may be further from a stable milestone, while Hermes’ conservative approach may lead to a 1.0 sooner.

### 7. Trend Signals
The aggregate community feedback across both projects reveals several emerging industry trends valuable for AI agent developers:

1. **MCP as a new standard**: OpenClaw’s MCP result coercion and Hermes’ (implied) lack of MCP focus suggests MCP is becoming a key differentiator for platform projects.
2. **Subagent governance is critical**: Both projects are actively working on restricting subagent tool access (OpenClaw #78441, Hermes #40946) – expect this to be a core security concern.
3. **Cost blowups from regressions**: The DeepSeek prompt cache failure (OpenClaw #91018) and community cost anxiety highlight the need for **cost monitoring and circuit breakers** as first-class features.
4. **macOS fragmentation**: Two separate macOS issues on Hermes (Intel build, launchd regression) plus iMessage doc updates on OpenClaw indicate that Apple’s OS evolution is a major source of friction.
5. **Desktop UX matters for end-user adoption**: Hermes’ desktop bugs (oversized dock icon, WSL IME, scrollbar) show that as agents move beyond CLI, polished UI becomes a competitive advantage.
6. **Background task reliability**: Both projects have open issues with cron/scheduled tasks (OpenClaw #90991, Hermes #6718) – “agent autonomy” requires trustworthy background execution.

**Value for AI agent developers**:  
- Choose OpenClaw if you need **multi-provider, multi-channel deployment** with MCP and are willing to manage daily upgrade risk.  
- Choose Hermes Agent if you prioritize **desktop/TUI experience, plugin extensibility, and a more stable release cycle** for end-user applications.  
- Pay attention to **subagent governance, cost controls, and background isolation** as these will define production-readiness in the coming months.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-07

## 1. Today’s Overview
Hermes Agent saw a very high level of community and development activity over the past 24 hours, with **50 issues updated** (38 open, 12 closed) and **50 pull requests updated** (40 open, 10 merged/closed). No new releases were cut. The traffic was driven by a wave of bug reports on macOS and desktop stability, several security vulnerability disclosures (including an RCE in the TUI gateway and an Honcho memory injection patch), and a burst of feature requests for the `/goal` lifecycle, kanban subscriptions, and desktop UX improvements. The core team responded rapidly, pushing multiple fix PRs and merging several stability patches.

## 2. Releases
No new releases were published today. The latest stable version remains **v0.16.0** (based on recent issues referencing v0.16.0 / main branch). No migration notes to report.

## 3. Project Progress
Today **10 pull requests were merged or closed**. While the full list of merged PRs is not visible in the top-20 data, the closed issues imply several important fixes landed:

- **Windows Unicode logging** (#40432, closed) – Gateway logging on Windows now tolerates Unicode in rotating log handlers.
- **Model display inconsistency** (#40296, closed) – Nous provider model name shown in UI/footer now matches `config.yaml`.
- **Dashboard vision tool rendering** (#22961, closed) – `vision_analyze` results are no longer mislabeled as user messages.
- **QQ bot reconnect loop** (#31193, closed) – 100% CPU spin on reconnect busyloop fixed.
- **CLI input lockup on lazy deps** (#40490, closed) – Bare `input()` under `prompt_toolkit` replaced.
- **Web UI npm install failure** (#38358, closed) – `hermes update` now correctly passes `--workspace web` flag.

Several security-critical fixes were also opened today (see Bugs & Stability), indicating rapid progress on hardening.

## 4. Community Hot Topics
The most active discussions this period revolve around **cross-platform compatibility** and **plugin/system initialization**:

- **#37505** [6 comments] – Hermes Desktop DMG is arm64-only, fails on Intel Macs. Users want a universal (`x86_64+arm64`) binary or at least an Intel-specific build.
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/37505)

- **#27683** [4 comments] – `web_tools.py` silently fails on fresh installs because the plugin discovery step is not called before dispatching search/extract/crawl. Root cause: missing `_ensure_plugins_discovered()` at dispatch sites.
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/27683)

- **#40820** [3 comments] – Desktop installer fails on macOS when the home directory path contains spaces (e.g. external drive). Unquoted shell commands cause breakage.
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/40820)

- **#6718** [3 comments, 1 👍] – Background process auto-notifications (`notify_on_complete`) never deliver to the agent. Users report the agent is not “woken up” after background tasks finish. This bug has been open since April.
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/6718)

Underlying theme: **reliability of core workflows** (web tools, notifications, installer) on diverse platforms is a growing community concern.

## 5. Bugs & Stability
### Critical / P1
- **TUI Gateway RCE via shell.exec denylist bypass** (#36847) – A CVE‑worthy vulnerability that allowed arbitrary command execution. **Fix PR #40939** opened today.
  [Issue](https://github.com/NousResearch/hermes-agent/issues/36847) | [PR](https://github.com/NousResearch/hermes-agent/pull/40939)

- **Honcho memory injection on customer-facing gateways** (#40170) – Operator-level memory from Honcho was auto-injected into WhatsApp, Telegram, Discord, etc., enabling indirect prompt injection. **Fix PR #40967** opened today.
  [PR](https://github.com/NousResearch/hermes-agent/pull/40967)

- **Telegram sender rejection bypass** (#40863) – Messages from unauthorized users were processed before authentication check, wasting resources. **Fix PR #40941** opened today.
  [PR](https://github.com/NousResearch/hermes-agent/pull/40941)

### High / P2
- **macOS 26 launchd domain regression** (#40831) – `hermes gateway start` incorrectly targets `user/<uid>` instead of `gui/<uid>`, breaking gateway startup on macOS 26.5.1.
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/40831)

- **CLI escape sequence leakage** (#40250) – Terminal escape codes at session start cause first 1-3 characters of every response to be silently consumed.
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/40250)

- **Cron script-path guard rejects default-profile scripts** (#40801) – Profile‑scoped jobs cannot reference scripts in `~/.hermes/scripts/`.
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/40801)

- **Context‑length cache corruption** – PR #40919 fixes an atomic write vulnerability in the cache file that could leave it empty after a process kill.
  [PR](https://github.com/NousResearch/hermes-agent/pull/40919)

### Medium / P3 (new today)
- #40944 – Stale “commits behind” count after manual `git pull`.  
- #40937 – macOS Dock icon appears oversized.  
- #40954 – WSL2 Desktop cannot use Windows IME.  
- #40963 – Model selection dropdown height too constrained.

## 6. Feature Requests & Roadmap Signals
Several user-requested features point toward upcoming improvements:

- **Goal lifecycle plugin hooks** (#27777) – Expose `on_goal_set/pause/resume/complete` to plugins. Highly requested for audit and automation.
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/27777)

- **Kanban board‑level event subscriptions** (#40917) – Enable `notify-subscribe` for all cards on a board, not just per‑task. Useful for multi‑agent orchestration.
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/40917)

- **ScoutGate v2** (#40940) – Bind `/goal` authority to lifecycle leases, epochs, and manifests for stronger safety.
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/40940)

- **Structured gateway `/goal` status metadata** (#30577) – Return JSON‑parsable status (e.g., `goal_achieved`, `continuing`, `paused`) for third‑party adapters.
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/30577)

- **Background subagent delegation** – PR #40946 adds `delegate_task(background=true)` to allow async subagents.
  [PR](https://github.com/NousResearch/hermes-agent/pull/40946)

- **Desktop “Keep Tool Calls Expanded” toggle** – PR #40942 addresses a common UX frustration.
  [PR](https://github.com/NousResearch/hermes-agent/pull/40942)

**Prediction**: The next minor release (likely v0.17.0) will ship the security patches (RCE, Honcho injection), the delegation background feature, and the structured goal metadata, along with plugin hook expansions.

## 7. User Feedback Summary
Users are **actively reporting issues** – a sign of a growing, engaged community. Common pain points:

- **macOS gaps**: Intel Macs unsupported (#37505); installer fails with spaces (#40820); launchd domain broken on macOS 26 (#40831); Dock icon oversized (#40937).
- **Plugin/initialization friction**: Web tools fail on fresh install (#27683); mnemosyne plugin not discovered (#40101); cron script paths incorrectly rejected (#40801).
- **Desktop UI quirks**: Sidebar sessions hiding (#38989); remote gateway config not working (#40215); model dropdown too small (#40963); WSL IME broken (#40954).
- **CLI/TUI annoyances**: Escape sequence truncation (#40250); banner version staleness (#40944); background notifications not delivered (#6718).

**Satisfaction signals**: The community trusts the project enough to file detailed bug reports and feature requests. PRs are reviewed and merged quickly. The security disclosures were handled transparently with rapid patches.

## 8. Backlog Watch
Maintainer attention is needed on these long-standing open issues:

- **#6718** – *Background process auto-notifications not delivering* (since 2026-04-09, 3 comments, 1 👍). This blocks a core “agent autonomy” feature.  
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/6718)

- **#8125** – *launchd plist includes session‑specific PATH entries causing false stale refreshes* (since 2026-04-12). Impacts macOS reliability.  
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/8125)

- **#13529** – *Agent Activity API & Emotional State Exposure* (since 2026-04-21). A feature request that could enable rich integrations; no response from maintainers.  
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/13529)

- **#24433** – *“No inference provider configured” in chat despite working `-z` flag* (since 2026-05-12, P1). A user‑blocking bug that remains open with 2 comments.  
  [GitHub](https://github.com/NousResearch/hermes-agent/issues/24433)

**Project health assessment**: Very active, with strong commit velocity and rapid security response. The sheer volume of new issues indicates both a large user base and some maturity gaps in installation/configuration UX. The maintainers are effectively triaging and fixing high‑severity items, but the backlog of non‑critical but long‑standing bugs (#6718, #8125) may need dedicated sprint focus.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*