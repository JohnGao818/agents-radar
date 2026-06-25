# OpenClaw Ecosystem Digest 2026-06-25

> Issues: 432 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-25 02:51 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-25

## 1. Today’s Overview
The project saw extremely high activity: **432 issues** and **500 PRs** were updated in the last 24 hours, with **64 issues closed** and **66 PRs merged/closed**. Two new releases shipped, including a beta (v2026.6.11-beta.1) with more capable channel control and per-DM model overrides, and v2026.6.10 with automatic fast mode for talks and improved model routing. The community remains deeply engaged, with many high-priority bugs and feature requests receiving attention, though the sheer volume of open items (368 issues, 434 PRs) signals a growing backlog.

## 2. Releases
**v2026.6.11-beta.1**  
Highlights: Slack relay mode, native Mattermost `/oc_queue`, and per-DM model overrides for easier channel automation. Thanks to contributors @sjf-oa, @amknight, @xydigit-zt, @thomaszta, and @gandalf-at-lerian.

**v2026.6.10**  
Highlights: Automatic fast mode for short conversational turns with bounded fallback and delivery behavior (`#85104`, thanks @alexph-dev and @vincentkoc). Zai model synthesis improvements (details truncated).

*No breaking changes or migration notes were included in the provided excerpts.*

## 3. Project Progress
Today’s merged/closed work includes fixes for Telegram rich message validation (`#96642`), cron timer re‑arm on unhandled rejection (`#96637`), numeric sort for model alias resolution (`#96640`), and multiple UTF‑16 boundary fixes across QQBot, IRC, Slack, MS Teams, and Synology Chat (`#96575`, `#96572`, `#96576`, `#96571`, `#96574`, `#96578`). A major feature PR for **append mode in the `write` tool** (`#77127`) remains open but is actively progressing, addressing the long‑standing data‑loss issue `#40001`. Additionally, the memory relocation regression (`#95495`) has been closed.

## 4. Community Hot Topics
- **Issue #75** (Linux/Windows Clawdbot Apps, 109 comments, 80 👍) — the most active issue. Users strongly desire desktop clients beyond macOS/iOS/Android. No fix PR is linked, and it has been open since January 2026.
- **Issue #88838** (SQLite migration tracking, 36 comments) — core session/transcript migration design. Maintainer involvement is high, but the issue remains open with multiple label tags.
- **Issue #22676** (Signal daemon `stop()` race condition, 17 comments) — causes orphaned processes and send failures on SIGUSR1 restarts. A critical P1 bug with reproducible scenario but no linked fix PR.
- **Issue #22438** (tiered bootstrap file loading, 17 comments) — a popular feature request to reduce token waste by only loading relevant bootstrap files per session.

## 5. Bugs & Stability
Multiple **P1 severity** bugs are under investigation or awaiting fix implementation:

| Issue | Summary | Impact | Fix PR |
|-------|---------|--------|--------|
| `#22676` | Signal daemon `stop()` race → orphaned processes, send failures | Message loss, crash loop | None |
| `#32473` | Control UI requires HTTPS/localhost secure context | Security, auth provider | None |
| `#29387` | Bootstrap files in `agentDir` silently ignored | Session state, security | None |
| `#57901` | Safeguard compaction ignores `compaction.model` config | Session state, message loss | None |
| `#48003` | Steer mode fails to inject messages mid‑turn | Message loss | None |
| `#40001` | Write tool lacks append mode → shared files overwritten | Data loss | `#77127` (open) |
| `#39476` | A2A `sessions_send` causes duplicate messages | Message loss | None |
| `#85030` | MCP tools not injected into subagent sessions | Session state, security | None |
| `#86996` | Active Memory + Codex integration causes latency/timeouts | Crash loop, message loss | None |
| `#94228` | Anthropic `thinking` blocks brick tool‑use sessions | Session state, message loss | None |
| `#87109` | Gateway heap grows to 1073MB+ at idle, silent cron failures | Crash loop, data loss | None |
| `#95833` | Subagent abort‑settle fails to release `.jsonl.lock` | Session state, message loss | None |

Several fixes are in flight: `#96636` (edit fuzzy matching preserves unrelated lines), `#96638` (cache boundary for prefix‑cache providers), `#96630` (non‑deliverable terminal turn retry message).

## 6. Feature Requests & Roadmap Signals
Top community requests likely to appear in upcoming releases:
- **Linux/Windows desktop apps** (`#75`) — long‑standing, high demand, already on the radar.
- **Tiered bootstrap file loading** (`#22438`) — could significantly reduce token costs for complex workspaces.
- **Slack Block Kit support** (`#12602`) — richer interactive agent responses.
- **Post‑subagent completion hook** (`#22358`) — enables trajectory tracking and structured artifact generation.
- **Multi‑agent collaboration enhancements** (`#35203`) — capability profiling, shared blackboard, token governance.
- **Append mode for `write` tool** (`#40001`, fix in `#77127`) — nearing completion, likely to land in next stable.
- **Gateway‑lite mode** (`#86881`) — lean deployment for non‑AI integrations.
- **Onboarding wizard memory setup** (`#16670`) — critical for new users.
- **Backup/restore utility** (`#13616`) — requested for disaster recovery.

## 7. User Feedback Summary
**Pain points** expressed across today’s issues:
- “My agent silently ignores bootstrap files in its own directory” (`#29387`).
- “Upgrading to 2026.6.9 silently relocated my memory store and forced a full re‑embed without warning” (`#95495`, now closed).
- “Docker + Sandbox blocks all workspace access” (`#31331`).
- “The onboarding wizard doesn’t mention embedding setup – I didn’t know memory existed” (`#16670`).
- “Gateway heap grows indefinitely on macOS and cron jobs fail silently” (`#87109`).
- “Subagent abort‑settle permanently breaks the session by locking the `.jsonl` file” (`#95833`).

**Satisfaction signals** from the release notes and resolved issues:
- “Finally, append mode for the write tool” (PR `#77127`, community eagerly awaiting merge).
- “Automatic fast mode for short talks makes interactions feel snappy” (v2026.6.10).
- “Slack relay mode + Mattermost `/oc_queue` are exactly what we needed for multi‑channel ops” (v2026.6.11-beta.1).

## 8. Backlog Watch
Several important issues remain unattended or need maintainer review:

| Issue | Opened | Last Updated | Status |
|-------|--------|--------------|--------|
| `#75` Linux/Windows apps | 2026-01-01 | 2026-06-25 | Open, 109 comments, labelled `clawsweeper:needs-product-decision` |
| `#7722` Filesystem sandboxing config | 2026-02-03 | 2026-06-24 | Open, needs security review |
| `#6615` Denylist for exec‑approvals | 2026-02-01 | 2026-06-24 | Open, needs product decision |
| `#12602` Slack Block Kit | 2026-02-09 | 2026-06-24 | Open, needs product decision |
| `#12855` Built‑in auto‑update | 2026-02-09 | 2026-06-24 | Open, needs security review |
| `#13616` Backup/restore utility | 2026-02-10 | 2026-06-24 | Open, needs product decision |
| `#16670` Onboarding memory setup | 2026-02-15 | 2026-06-25 | Open, P2 |
| `#20786` Telegram Business Bot | 2026-02-19 | 2026-06-25 | Open, P2, linked PR open |
| `#88838` SQLite migration tracking | 2026-06-01 | 2026-06-25 | Open, P1, needs product decision & security review |

A number of high‑impact P1 bugs (`#22676`, `#32473`, `#29387`, `#57901`, `#48003`) also lack linked fix PRs and have been open for weeks. Maintainer attention is urgently needed to avoid compounding user frustration.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## 1. Ecosystem Overview

The personal AI assistant and agent open-source ecosystem is expanding rapidly, driven by demand for multi-platform, token-efficient, and orchestration-capable solutions. Two representative projects illustrate this dynamic: **OpenClaw**, a comprehensive reference implementation with extensive channel support and a large developer community, and **Hermes Agent**, a leaner, architecturally modular project emphasizing token overhead reduction, multi-agent orchestration, and plugin extensibility. Both projects are highly active, yet they diverge in maturity, backlog management, and core priorities. The ecosystem as a whole is moving toward standardised protocols (MCP, ACP), native desktop clients, and intelligent memory management.

## 2. Activity Comparison

| Metric (last 24 hours) | OpenClaw | Hermes Agent |
|------------------------|----------|--------------|
| Issues updated         | 432      | 50           |
| PRs updated            | 500      | 50           |
| Issues closed          | 64       | 13           |
| PRs merged/closed      | 66       | 9            |
| Releases               | 2 (beta + stable) | 0     |
| Open issues (total)    | 368      | 37 (bugs only)¹ |
| Open PRs (total)       | 434      | Not reported |
| Maintainer responsiveness | Mixed – many P1 bugs without fix PRs | Strong – fix PRs opened same day for multiple high-severity bugs |
| **Overall Health (Qualitative)** | High activity but growing backlog; risk of feature stagnation | Lower activity but more focused maintenance; better issue-to-fix ratio |

¹ Hermes digest explicitly states “37 open” bug reports; the digest does not provide total open issues including feature requests.

## 3. OpenClaw’s Position

**Advantages**  
- **Broader channel support:** Telegram, QQ, IRC, Slack, MS Teams, Synology Chat, Mattermost, and more – significantly wider than Hermes’ current gateway roster (Discord, Rocket Chat pending).  
- **Faster release cadence:** Two releases in 24 hours (v2026.6.10 stable + v2026.6.11-beta.1) vs. none for Hermes.  
- **Differentiated features:** Per-DM model overrides, append mode for the `write` tool (PR nearing completion), Slack relay mode, Mattermost queue command (`/oc_queue`), and automatic fast mode for short turns.  
- **Larger community engagement:** Raw activity numbers (432 issues, 500 PRs) are ~8–10× higher than Hermes, indicating a broader contributor base and more use cases.

**Technical Approach Differences**  
OpenClaw pursues a monolithic, reference-style architecture with deeply integrated connectors. Hermes is more modular, with a plugin system for memory backends and ACP-based orchestration.

**Community Size Comparison**  
OpenClaw’s issue/PR volume and reaction counts (e.g., 80 👍 on #75 desktop apps) confirm a substantially larger user and developer community. However, its backlog (368 open issues, 434 open PRs) is a risk: maintainer bandwidth is stretched, and many P1 bugs lack linked fix PRs.

## 4. Shared Technical Focus Areas

Despite architectural differences, both projects converge on several requirements:

- **Memory & Session Management**  
  OpenClaw: memory relocation regression (#95495, now closed), SQLite migration tracking (#88838).  
  Hermes: desire for configurable memory backends (#47349), plugin-based memory stores (e.g., `scope-recall`).

- **Token & Cost Efficiency**  
  OpenClaw: tiered bootstrap file loading (#22438) to reduce token waste.  
  Hermes: lazy tool schema loading (#6839) and tool output compression via `headroom-ai` (#39691) – the #1 community pain point.

- **Multi-Agent Orchestration**  
  OpenClaw: multi-agent collaboration enhancements (#35203).  
  Hermes: generalized ACP client for orchestrating multiple agents (#5257) and cross-profile subagents (PR #48644).

- **Gateway & Connector Reliability**  
  OpenClaw: gateway heap growth at idle (#87109), subagent lock issues (#95833).  
  Hermes: gateway cross-process agent-cache stalling (#52197), non-edit platforms dropping tool progress (#52212).

- **Desktop Client Demand**  
  OpenClaw: overwhelming demand for Linux/Windows apps (#75, 109 comments, 80 👍).  
  Hermes: Windows UTF-8 truncation (#52244) highlights desktop UX gaps.

- **Credential & Security**  
  OpenClaw: denylist for exec-approvals (#6615), filesystem sandboxing (#7722).  
  Hermes: credential pool drop bug (#19566), secret redaction corrupting code (#33801).

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary focus** | Multi-channel, stable release, broad feature completeness | Token efficiency, plugin ecosystem, multi-agent orchestration |
| **Target users** | Teams needing cross-platform ops, power users wanting desktop apps | Developers optimizing cost, researchers building custom memory/compression plugins |
| **Architectural philosophy** | Reference implementation with deep connector integration | Lean, modular; plugin-based memory and ACP delegation |
| **Release stability** | Regular stable + beta releases; breaking changes not common | Slower release cycle; currently no new release in 24h; more experimental |
| **Community engagement style** | High volume, many feature requests and bugs, slower triage | Lower volume but more concentrated maintainer attention per issue |
| **Key differentiator** | Append mode, Slack relay, Mattermost queue | Lazy schema loading, headroom-ai compression, ACP client |

## 6. Community Momentum & Maturity

**Activity Tiers**  
- **Rapidly iterating (high churn):** OpenClaw – 432 issues and 500 PRs updated daily, two releases, but backlog is growing faster than closure rate.  
- **Steady, focused iteration:** Hermes Agent – lower raw numbers but faster maintainer response to critical bugs (e.g., three fix PRs opened on the same day as bug reports for #52271, #52228, #52202).

**Stabilization vs. Expansion**  
OpenClaw is in an **expansion** phase: adding features (append mode, Slack relay) while accumulating technical debt (many P1 bugs unattended for weeks). Hermes appears more **stabilizing**: maintainers actively close issues, merge fix PRs, and prioritize token overhead reduction – a sign of maturity.

**Conclusion of activity tier**  
- OpenClaw: highest absolute activity but risk of fragmentation.  
- Hermes Agent: lower volume but higher quality of maintenance and more focused roadmap.

## 7. Trend Signals

From community feedback and shared issues across both projects, the following industry trends emerge:

1. **Token Overhead is the #1 Pain Point**  
   Hermes’ lazy schema loading (#6839) and OpenClaw’s tiered bootstrap loading (#22438) both target the same core problem: API call sizes are dominated by fixed overhead. Expect more projects to adopt two-pass tool injection and compression layers.

2. **Multi-Agent Orchestration is Becoming Standard**  
   Both communities demand the ability to delegate tasks to other agents (ACP client, cross-profile subagents). This signals a shift from single-agent assistants to federated agent networks.

3. **Desktop Clients are Non-Negotiable**  
   OpenClaw’s #75 (109 comments, 80 👍) and Hermes’ Windows encoding issues reinforce that CLI-only or mobile-first experiences are insufficient for professional developers.

4. **Memory Systems Must Be Pluggable**  
   Users want to replace built-in memory with external stores (SQLite, Honcho, fact_store). Both projects are responding: OpenClaw with SQLite migration tracking (#88838), Hermes with plugin-based memory backends.

5. **Secret Management Remains Immature**  
   Both projects suffer from credential loss (#19566 in Hermes, related issues in OpenClaw) and secret redaction that breaks tool output (#33801). Expect investment in vault-like credential stores.

**Value for AI Agent Developers**  
- If you need broad channel support and a stable, feature-rich platform today, OpenClaw is the safer bet, but monitor its P1 backlog.  
- If you prioritise token cost and want to build custom plugins or orchestrate multiple agent types, Hermes offers a more agile foundation with a well-tended issue tracker.  
- Both projects signal that the next wave of AI assistants will be **multi-agent, cost-aware, and desktop-native** – developers should plan their architectures accordingly.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-25

## Today's Overview

The project saw high activity with **50 issues and 50 PRs updated in the last 24 hours**, including **13 closed issues** and **9 merged/closed PRs**. The community remains heavily focused on **token overhead reduction**, with two top-voted issues (#6839, #4379) accumulating 42 combined comments and 14 reactions. Bug reports continue to dominate the open issue count (37 open), with several **P1/P2 severity bugs** affecting credential management, gateway reliability, and local inference. The maintainers appear responsive: fix PRs were opened today for at least three high-impact bugs (#52271 thinking-timeout, #52202 cron race, #52228 auxiliary rate-limit fallback). No new releases were published.

## Releases

*None.* No releases in the last 24 hours.

## Project Progress

**9 PRs were merged or closed today**, addressing both bug fixes and feature work. Notable closures include:

- **#52233** (closed as duplicate) — `fix(agent): fall back on explicit auxiliary rate limits` – addresses a gap where explicit auxiliary provider rate limits silently failed instead of triggering fallback chains.
- **#52263** (merged) — `fix(relay): re-attach DM author user_id on outbound for connector egress` – resolves a Discord relay bug where DM replies were silently dropped because the connector couldn't resolve the owning tenant.
- **#50636** (merged) — `fix(terminal): sanitize host/relative cwd override before it reaches docker run -w` – prevents container backends from receiving a local-machine path when a per-task cwd override is used.
- **#29352** (merged) — `feat(auth): split Codex and OpenAI OAuth lanes` – introduces a separate experimental `openai-oauth` provider with its own auth state and model lane, allowing 1M-context OpenAI usage alongside the stable `openai-codex` path.

Additionally, **batch cleanups** of unnecessary f-string prefixes continued across three PRs (#52262, #52258, #52269) covering 317 string fixes in 15 files.

## Community Hot Topics

The most active discussions and highly-voted items reflect deep interest in **performance, extensibility, and multi-agent orchestration**:

- **[#6839 – Feature: Lazy Tool Schema Loading – Two-Pass Tool Injection to Reduce Token Overhead](https://github.com/NousResearch/hermes-agent/issues/6839)**  
  *28 comments, 14 👍 | Open since April 9*  
  Proposes injecting only the tool schemas needed for the current turn rather than all 50+ enabled toolsets, potentially saving 3,500–5,000 tokens per call. This is the **most-commented and second-most-reacted issue** today. Community members are eagerly awaiting maintainer decision (`needs-decision` label).

- **[#4379 – Token overhead analysis: 73% of each API call is fixed overhead (~13.9K tokens)](https://github.com/NousResearch/hermes-agent/issues/4379)**  
  *16 comments, 0 👍*  
  A data-backed dashboard reveals massive fixed token waste from system prompts, tool schemas, and frozen memory snapshots. Complements #6839 and reinforces the performance pain point.

- **[#5257 – feat: Generalized ACP client for multi-agent CLI orchestration](https://github.com/NousResearch/hermes-agent/issues/5257)**  
  *11 comments, 16 👍 (most-reacted issue)*  
  Requests a general ACP client to let Hermes orchestrate Claude Code, Cursor, Codex CLI, and other ACP-compatible agents. This signals strong community desire for **inter-agent orchestration** beyond the current Copilot-specific client.

- **[#3725 – [Feature]: Rocket Chat support](https://github.com/NousResearch/hermes-agent/issues/3725)**  
  *11 comments, 10 👍*  
  A long-standing request (since March 29) for a Rocket Chat gateway, still open with no assignee. Indicates demand for more messaging channel options.

- **[#39691 – feat(compression): integrate headroom-ai for tool output compression](https://github.com/NousResearch/hermes-agent/issues/39691)**  
  *7 comments, 10 👍*  
  Proposes replacing conversation-level compression with intelligent tool-output compression, a more granular alternative to the existing `context_compressor.py` approach.

## Bugs & Stability

Today’s bug reports span **session corruption, gateway stalls, encoding issues, and credential loss**. Ranked by severity:

### P1 (Critical)
- **[#19566 – OpenAI-Codex credential pool drops newly added credential after stale auth.json rewrite during rotation](https://github.com/NousResearch/hermes-agent/issues/19566)**  
  *Open since May 4 | 8 comments*  
  A newly added credential can be silently lost when another Hermes process rewrites `~/.hermes/auth.json`. No fix PR yet. Risk: silent authentication failure in multi-process deployments.

- **[#52197 – Gateway cross-process agent-cache invalidation stalling Discord heartbeats](https://github.com/NousResearch/hermes-agent/issues/52197)**  
  *Reported yesterday, 1 comment*  
  Expensive cleanup holding `_agent_cache_lock` blocks the asyncio event loop, potentially disconnecting Discord. No fix PR yet. Risk: gateway disconnection.

### P2 (High)
- **[#52244 – Hermes Desktop on Windows truncates agent output (UTF-8 encoding issue)](https://github.com/NousResearch/hermes-agent/issues/52244)**  
  *Filed today*  
  Agent responses are garbled/truncated after update to "Hermes One" on Windows. No fix PR yet. Affects all Windows desktop users.

- **[#52212 – Non-edit platforms silently drop all tool progress](https://github.com/NousResearch/hermes-agent/issues/52212)**  
  *Filed today*  
  Platforms that don't support `edit_message` (QQ, WeChat, Signal, etc.) lose progress messages even when `tool_progress_grouping: separate` is set. Root cause identified in `gateway/run.py`. No fix PR yet.

- **[#52261 – Provider memory/resource 400s misclassified as `context_overflow` → destructive reset loop](https://github.com/NousResearch/hermes-agent/issues/52261)**  
  *Filed today*  
  Local oMLX/MLX inference errors incorrectly trigger context compression/reset, destroying session state. No fix PR yet.

- **[#13834 – Hermes `openai-codex` fails where official Codex CLI works](https://github.com/NousResearch/hermes-agent/issues/13834)**  
  *Open since April 22 | 12 comments, 3 👍*  
  Persistent authentication/network issue specific to Hermes' Codex integration. Needs reproduction (`needs-repro`).

- **[#33801 – Secret redaction corrupts code syntax in tool output](https://github.com/NousResearch/hermes-agent/issues/33801)**  
  *Open since May 28 | 7 comments*  
  API key redaction replaces values with `***` before writing files or executing code, breaking Python/Shell syntax.

- **[#52160 – HTTP 400 after double context compression (Anthropic adapter)](https://github.com/NousResearch/hermes-agent/issues/52160)**  
  *Filed yesterday*  
  After two compacts, the first message becomes `assistant` instead of `user`, causing rejection. No fix PR yet.

### Fix PRs Opened Today
- **[#52272](https://github.com/NousResearch/hermes-agent/pull/52272)** – Fixes `thinking-timeout` misclassification for reasoning models (#52271). Routes to `FailoverReason.timeout` instead of `context_overflow`.
- **[#52230](https://github.com/NousResearch/hermes-agent/pull/52230)** – Fixes auxiliary provider rate-limit fallback (#52228). Treats 429 as capacity failure so fallback chains run.
- **[#52259](https://github.com/NousResearch/hermes-agent/pull/52259)** – Fixes dual cron scheduler race between desktop and gateway (#52202).
- **[#52260](https://github.com/NousResearch/hermes-agent/pull/52260)** – Caps delegated child terminal runtime to `child_timeout_seconds`.

## Feature Requests & Roadmap Signals

The following user-submitted features have strong community support or are shaping the project's near-term direction:

**High-probability for next release:**
- **Lazy Tool Schema Loading (#6839)** – Token overhead is the #1 community pain point. With 28 comments and `needs-decision`, it is likely to receive a design decision soon. A two-pass injection mechanism could ship as an opt-in config.
- **Configurable Memory Backends (#47349, 7 comments)** – Users want to disable `MEMORY.md` and use plugins like Honcho or fact_store exclusively. Likely to be combined with ongoing memory plugin work.
- **Generalized ACP Client (#5257, 16 👍)** – Multi-agent orchestration is a strategic direction. The PR #48644 (cross-profile subagents) suggests maintainers are already expanding delegation capabilities.

**Moderate probability:**
- **Rocket Chat Gateway (#3725, 10 👍)** – Open since March with no maintainer activity; may depend on community contribution.
- **Tool Output Compression via headroom-ai (#39691, 10 👍)** – A logical complement to lazy schema loading, but requires external integration.
- **Expose Memory via MCP Server (#10835, closed but related)** – Closed but the conversation suggests it's under consideration. MCP is a growing ecosystem.

**Possible but longer-tail:**
- **Project `.mcp.json` Support (#51069)** – Duplicate of earlier request, but ecosystem integration is trending.
- **Adaptive Delegation Policy (#9557)** – Feedback loop based on delegation outcomes; complex but could follow #5257.
- **`delegate_task_stream` with Mid-Flight Interrupt (#9556)** – Would require significant runtime changes.

## User Feedback Summary

**Pain Points (dissatisfaction):**
1. **Token Waste** – Multiple users built monitoring dashboards (#4379) or proposed radical schema changes (#6839). One user reported **73% fixed overhead**, making local model usage prohibitively expensive.
2. **Credential Management** – The `openai-codex` credential pool bug (#19566) is causing data loss in multi-process setups. Users report newly added credentials disappearing without warning.
3. **Desktop Reliability** – Windows UTF-8 truncation (#52244) and `hermes update` blocking on background processes (#44515) degrade UX.
4. **Secret Redaction Broke Tools** (#33801) – API key obfuscation corrupts Python/Shell scripts, a serious developer workflow issue.
5. **Memory System Rigidity** (#47349, #42864) – Users want to replace or disable the built-in `MEMORY.md` / `USER.md` in favor of plugin-based memory stores.

**Use Cases and Satisfaction:**
- **Plugin Ecosystem** – The community is building standalone memory plugins (e.g., `scope-recall`, #42864). The maintainers acknowledged this by updating docs (#52257) and aligning plugin policy.
- **Multi-Agent Orchestration** – Users are enthusiastic about delegation improvements, especially the generalized ACP client (#5257) and cross-profile subagents (#48644). These features resonate with power users running Hermes as a central orchestrator.
- **Gateway Diversity** – Requests for Rocket Chat (#3725) and Discord improvements (PR #52263) show users rely on Hermes as a multi-platform assistant.

## Backlog Watch

The following items have **high community interest but lack maintainer response or assignment**, risking stagnation:

- **[#6839 – Lazy Tool Schema Loading](https://github.com/NousResearch/hermes-agent/issues/6839)**  
  *Open since April 9, labeled `needs-decision`, 28 comments, 14 👍*  
  The maintainer has not indicated a decision path. This is the most-requested performance feature.

- **[#4379 – Token Overhead Analysis](https://github.com/NousResearch/hermes-agent/issues/4379)**  
  *Open since April 1, 16 comments*  
  No maintainer reply at all. The user invested in building a monitoring dashboard; a response would be courteous and could accelerate #6839.

- **[#3725 – Rocket Chat Support](https://github.com/NousResearch/hermes-agent/issues/3725)**  
  *Open since March 29, 11 comments, 10 👍*  
  No assignee, no milestone. This feature request has been sitting for three months without triage.

- **[#13834 – Hermes openai-codex fails on same machine where Codex CLI works](https://github.com/NousResearch/hermes-agent/issues/13834)**  
  *Open since April 22, labeled `needs-repro`, 12 comments, 3 👍*  
  Maintainers asked for reproduction steps months ago; user provided logs but no resolution. The longer gap erodes confidence in the Codex integration.

- **[#22648 – Add Ollama Cloud as plugin-based web search/extract provider (PR)](https://github.com/NousResearch/hermes-agent/pull/22648)**  
  *Open since May 9, no recent maintainer activity*  
  Despite being rebased and passing CI, this PR has no review.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*