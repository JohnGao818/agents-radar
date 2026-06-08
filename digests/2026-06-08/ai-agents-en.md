# OpenClaw Ecosystem Digest 2026-06-08

> Issues: 295 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-08 03:36 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-08

## 1. Today’s Overview

OpenClaw is in a period of extremely high activity. In the last 24 hours, 295 issues were updated (180 open/active, 115 closed) and 500 pull requests were updated (333 open, 167 merged/closed). No new releases were published today. The community is actively submitting and discussing bugs and feature requests, with a strong focus on session stability, security boundaries, and channel-specific reliability (Feishu, Discord, Telegram, Slack). Several long-standing “diamond lobster” rated issues remain open, indicating persistent pain points that require maintainer attention.

## 2. Releases

*No new releases were published on 2026-06-08.*

## 3. Project Progress

167 pull requests were merged or closed today, though the top 30 by comment count are predominantly still open or in review. Notable closed PRs include:

- [#87219 – fix(agents): resolve inbound media read refs](https://github.com/openclaw/openclaw/pull/87219) (merged)  
  Closes #87203, allows managed inbound media references through the host read workspace guard and normalizes `media://inbound/...` paths.

- [#88234 – Feishu dispatch: TypeError - Cannot read properties of undefined (reading 'run')](https://github.com/openclaw/openclaw/issues/88234) (closed)  
  A crash in Feishu message dispatch was fixed.

- [#68113 – Mattermost slash commands return 503 "not yet initialized"](https://github.com/openclaw/openclaw/issues/68113) (closed)  
  A v2026.4.15 regression that broke slash commands was resolved.

Several other closed stale issues and PRs (e.g., #73802, #70330, #70164, #69778) show ongoing cleanup of channel‑specific regressions and gateway restart issues.

Key **open** PRs pushing forward improvements:

- [#89659 – fix(feishu): retry on send rate-limit errors (230020/230006)](https://github.com/openclaw/openclaw/pull/89659) – adds retry logic for Feishu send errors.
- [#90101 – feat: add runtime self context config and tool](https://github.com/openclaw/openclaw/pull/90101) – first config-backed slice of the runtime/offload/scale effort.
- [#91308 – feat(xai): add realtime voice provider](https://github.com/openclaw/openclaw/pull/91308) – adds xAI as a Talk realtime voice provider.
- [#78441 – feat(subagents): forward toolsAllow from sessions_spawn](https://github.com/openclaw/openclaw/pull/78441) – allows tool allowlists for subagent spawns.
- [#90328 – Expose model picker agent runtimes](https://github.com/openclaw/openclaw/pull/90328) – adds `agentRuntime` metadata to model listings for the WebUI.

## 4. Community Hot Topics

The most active discussions are around stability, security, and session management.

- **Text leakage between tool calls** ([#25592](https://github.com/openclaw/openclaw/issues/25592), 27 comments, 👍1)  
  P1, diamond lobster. Agent‑generated text between tool calls is sent to messaging channels, breaking UX. Needs product and security review. Stale since February.

- **Core session/transcript SQLite migration** ([#88838](https://github.com/openclaw/openclaw/issues/88838), 18 comments, 👍1)  
  P2. A plan to migrate session state to SQLite via branch‑by‑abstraction. Maintainer-led.

- **Regression: Codex app-server turn-completion stall** ([#88312](https://github.com/openclaw/openclaw/issues/88312), 14 comments, 👍3)  
  P1, regression of #84076. Multi‑tool agent turns stall after 2026.5.27 update. Needs live repro and product decision.

- **Bootstrap files in agentDir silently ignored** ([#29387](https://github.com/openclaw/openclaw/issues/29387), 14 comments, 👍5)  
  P1, security and session impact. Per‑agent `agentDir` bootstrap `.md` files are not loaded; only the shared workspace directory works. Users frustrated.

- **Cron scheduled trigger contaminates global runtime state** ([#90991](https://github.com/openclaw/openclaw/issues/90991), 13 comments, 👍1)  
  P1. Cron triggers cause system‑wide overload failures. Needs live repro.

- **Post-subagent completion extension hook** ([#22358](https://github.com/openclaw/openclaw/issues/22358), 12 comments, 👍1)  
  P2, diamond lobster. Request for a hook after subagent completion to generate structured trajectory files.

- **`exec` tool does not inherit skill environment variables** ([#31583](https://github.com/openclaw/openclaw/issues/31583), 12 comments, 👍2)  
  P1, regression. Skills‑configured `env` vars not passed to `exec` subprocesses, preventing secret injection.

- **Write tool lacks append mode – isolated cron sessions destroy shared files** ([#40001](https://github.com/openclaw/openclaw/issues/40001), 11 comments, 👍1)  
  P1. Overwrites shared workspace files instead of appending. Linked PR open.

## 5. Bugs & Stability

Several high‑severity bugs were reported or updated today:

| Issue | Severity | Summary | Fix PR Exists? |
|-------|----------|---------|---------------|
| [#91283](https://github.com/openclaw/openclaw/issues/91283) | P3, **security** | `minSecurity` rank order inverted (`full` treated as most restrictive). Session override clamped incorrectly. | No |
| [#91212](https://github.com/openclaw/openclaw/issues/91212) | P1 | `delivery-recovery` starts before channel transport ready, causing message loss on gateway restart. | No |
| [#90639](https://github.com/openclaw/openclaw/issues/90639) | P1 | `compaction.mode: "safeguard"` allows sessions to grow to context ceiling, then forces /new; no in-channel recovery on Slack. | [#90641](https://github.com/openclaw/openclaw/pull/90641) (open, preserves assistant boundary replies) |
| [#90428](https://github.com/openclaw/openclaw/issues/90428) | P1, **regression** | `exec` tool triggers SIGTERM gateway restart on WSL2 with Node 24. | No |
| [#88312](https://github.com/openclaw/openclaw/issues/88312) | P1, **regression** | Multi‑tool turns stall on Codex app‑server after 2026.5.27. (Regression of #84076, which was fixed by #85107.) | No |
| [#91212](https://github.com/openclaw/openclaw/issues/91212) | P1 | Delivery recovery fails after gateway restart because channel WebSocket not reconnected. | No |
| [#87326](https://github.com/openclaw/openclaw/issues/87326) | P1 | Telegram streaming: intermediate text blocks between tool calls lost; only final block visible. | No |
| [#74586](https://github.com/openclaw/openclaw/issues/74586) | P1 | Active‑memory plugin aborts `memory_search` tool calls, classifies as timeout. | No |
| [#64664](https://github.com/openclaw/openclaw/issues/64664) | P2 | In‑flight approvals lost on gateway restart; stale callback buttons show confusing error. | No |

Several stale high‑impact bugs also remain open from February/March 2026, e.g., #25592 (text leakage), #29387 (bootstrap ignored), #31583 (env inheritance), #40001 (write overwrite). These indicate a significant backlog of core reliability issues.

## 6. Feature Requests & Roadmap Signals

New and active feature requests suggest the community is pushing for:

- **Gateway‑lite mode** ([#86881](https://github.com/openclaw/openclaw/issues/86881)) – deterministic deployments without AI harness. Could land in a future minor release.
- **Topic‑session families** ([#90916](https://github.com/openclaw/openclaw/issues/90916)) – multiple named context lanes per assistant. P2, needs product decision.
- **Bounded/validated append for pre‑compaction memory flush** ([#90354](https://github.com/openclaw/openclaw/issues/90354)) – guardrails against oversized noisy memory writes.
- **Configurable `session.resetPrompt`** ([#45501](https://github.com/openclaw/openclaw/issues/45501)) – replace hardcoded startup message. P2, needs review.
- **Slack tool‑level progress** ([#33413](https://github.com/openclaw/openclaw/issues/33413)) – dynamic status text instead of static “is typing…”. P2, queueable.
- **Cumulative context usage in `/usage` footer** ([#40215](https://github.com/openclaw/openclaw/issues/40215)) – show remaining window per model.

The active PRs on runtime self‑context (#90101) and xAI voice (#91308) point toward upcoming infrastructure improvements and provider expansion.

## 7. User Feedback Summary

Real user pain points captured from issues and comments:

- **Text leakage** (#25592): “Internal processing output fails… leaks to messaging channel” – severe UX and security issue.
- **Bootstrap file ignorance** (#29387): “Only workspace directory files are injected” – forces workarounds for multi‑agent setups.
- **Sandbox workspace read‑only** (#37634): “Tools that need to write to workspace fail” – users want `workspaceAccess: "none"` to still allow writing.
- **Approval lost on restart** (#64664): “unknown or expired approval id” – confusing for users who see stale buttons.
- **Cron overload** (#90991): “Transient system‑wide overload failures” – intermittent but disruptive.
- **Symbolic link not followed** (#38622): “Workspace file injection shows `[MISSING]` for symlinks” – breaks shared personality files.
- **Compaction safeguard frustration** (#90639): “Session ends with no recovery – forces manual reset” – users on recommended config get stuck.
- **Dreaming feature gaps** (#70005): “Summaries disconnected from meaningful events” – quality of life improvement desired.

Satisfaction signals: Several reported bugs were closed promptly (Mattermost, Feishu dispatch), and the community is actively contributing detailed reproduction steps and proposed fixes.

## 8. Backlog Watch

Long‑unanswered important issues that need maintainer attention:

| Issue | Age | Status | Why It Matters |
|-------|-----|--------|---------------|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | Feb 24, 2026 (3.5 months) | Open, P1, needs product & security review | Text leakage affects all messaging channels; diamond‑lobster severity. |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) | Feb 28, 2026 | Open, P1, needs review | Bootstrap file ignorance blocks multi‑agent customization. |
| [#22358](https://github.com/openclaw/openclaw/issues/22358) | Feb 21, 2026 | Open, P2, needs decision | Post‑subagent hook would unlock many automation use cases. |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) | Mar 2, 2026 | Open, P1, linked PR open | Secret injection regression – high security impact. |
| [#40001](https://github.com/openclaw/openclaw/issues/40001) | Mar 8, 2026 | Open, P1, linked PR open | Write tool overwrites shared files; data loss in cron. |
| [#37634](https://github.com/openclaw/openclaw/issues/37634) | Mar 6, 2026 | Open, P1, needs review | Sandbox workspace read‑only blocks core workflows. |
| [#38622](https://github.com/openclaw/openclaw/issues/38622) | Mar 7, 2026 | Open, P1, linked PR open | Symlinks broken in workspace injection – affects shared configs. |
| [#45501](https://github.com/openclaw/openclaw/issues/45501) | Mar 13, 2026 | Open, P2, needs review | Configurable reset prompt – commonly requested. |
| [#75025](https://github.com/openclaw/openclaw/pull/75025) | Apr 30, 2026 | Open, P2 | Stale timestamp fix for cron – long‑standing nit. |
| [#46303](https://github.com/openclaw/openclaw/pull/46303) | Mar 14, 2026 | Open, P1 | Inbound message loss on SIGUSR1 reload – affects multiple channels. |

The sheer volume of stale high‑severity items suggests the maintainer team may need to allocate dedicated backlog‑reduction sprints.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## 1. Ecosystem Overview

The open‑source personal AI assistant and agent landscape is experiencing explosive growth, driven by demand for multi‑channel deployment, multi‑agent orchestration, and robust security boundaries. Two major reference implementations—**OpenClaw** (core framework) and **Hermes Agent** (Nous Research’s agent platform)—each serve distinct yet overlapping needs. Both projects are in hyper‑active development cycles, with hundreds of issues and pull requests updated daily. The ecosystem is maturing rapidly, but backlogs of high‑severity bugs (especially around session stability, memory management, and platform‑specific crashes) signal that maintainers must balance feature velocity with reliability.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues updated (last 24h)** | 295 (180 open, 115 closed) | 50 (33 open, 17 closed) |
| **PRs updated (last 24h)** | 500 (333 open, 167 merged/closed) | 50 (46 open, 4 merged/closed) |
| **New releases** | None | None |
| **Health score** ⚠️ | **High activity, significant backlog** — 60% open issues, 66% open PRs; many “diamond lobster” P1s open for months | **Responsive, fast closure** — 34% open issues, but only 8% of PRs merged today; maintainers close P1s within ~11 days |

*Interpretation: OpenClaw has a vastly larger contributor base and broader scope, but carries a heavier maintenance debt. Hermes Agent is smaller but more agile, with quicker turnaround on critical bugs.*

## 3. OpenClaw’s Position

**Advantages vs. peers:**
- **Scale & breadth:** 295 issues and 500 PRs in one day dwarfs Hermes’ numbers, reflecting a larger community and broader integration surface (Feishu, Discord, Telegram, Slack, Mattermost, WhatsApp).
- **Deep security model:** Diamond‑lobster ratings, `minSecurity` rank order, and workspace guards show a mature security architecture.
- **Core reference:** OpenClaw is explicitly the “core reference” implementation; many downstream projects (including Hermes) fork or migrate from it.

**Technical approach differences:** OpenClaw focuses on channel‑specific reliability (e.g., Feishu dispatch retry, Telegram streaming fixes) and session state migration to SQLite via branch‑by‑abstraction. Hermes leans into desktop UX, A2A protocol, and plugin‑based extensibility.

**Community size:** OpenClaw’s raw issue/PR count indicates a community many times larger than Hermes’. However, Hermes’ community is highly engaged on a smaller set of high‑impact features (A2A received 18 reactions).

## 4. Shared Technical Focus Areas

Both projects are investing in overlapping pain points:

| Requirement | OpenClaw | Hermes Agent |
|-------------|----------|--------------|
| **Multi‑agent orchestration** | Subagent tool allowlists (PR #78441), post‑subagent hooks (issue #22358) | A2A protocol plugin (PR #41711), Kanban board (PR #41756), “send to all” broadcast (PR #39474) |
| **Memory & session management** | SQLite session migration (#88838), compaction safeguard (#90639), bounded append (#90354) | Bounded memory with in‑turn consolidation (PR #41755), Honcho KV cache fix (#13631) |
| **Security hardening** | Text leakage (#25592), minSecurity inversion (#91283), env variable inheritance (#31583) | V4A guards, ACP reads, API auth, Discord mention control (PR #41754) |
| **Platform stability** | WSL2 SIGTERM crash (#90428), macOS update stuck (#41737) | Windows gateway watchdog (PR #41761), macOS launchctl fallback (#41676) |
| **Message delivery reliability** | Delivery recovery on restart (#91212), Telegram streaming loss (#87326) | Compression desync (#34089), DM session isolation (PR #41764) |

*These shared focus areas confirm that the ecosystem still lacks robust solutions for production‑grade agent reliability, and users across projects are hitting the same walls.*

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Target user** | Developers building multi‑channel, multi‑model agent systems | End‑users and developers who want a desktop‑first agent experience with built‑in Kanban and A2A |
| **Primary architecture** | Modular plugin‑based core with channel adapters; SQLite for session state | Desktop app (Electron) + gateway; plugin system (A2A, Kanban); memory consolidation in‑turn |
| **Channel support** | Broad: Feishu, Discord, Telegram, Slack, Mattermost, WhatsApp | Narrower: Discord, WhatsApp, Codex; desktop UI as primary interface |
| **Feature emphasis** | Security boundaries, session lifecycle, tool execution env, cron reliability | Multi‑agent interoperability (A2A), desktop UX (preview tabs, sidebar overlays), memory management |
| **Release pace** | No releases today; many stale high‑severity issues suggest slower stabilization | No releases today, but features land quickly via PRs; P1 bugs fixed in days |
| **Community contribution model** | Large external contributor pool; many PRs from community with detailed repro steps | Mix of core team and external devs; feature PRs often from community (e.g., #41761 by `iamlukethedev`) |

**Key takeaway:** OpenClaw is the “operating system” for agent infrastructure; Hermes is the “application layer” that targets end‑user productivity and multi‑agent studios.

## 6. Community Momentum & Maturity

**Activity Tiers:**

- **Tier 1 (Extremely High Activity):** Both projects are in a rapid iteration cycle. OpenClaw processes 500+ PRs daily; Hermes 50+. Neither shows signs of slowing.
- **Stabilization signs:** OpenClaw has a long tail of “diamond lobster” issues (e.g., text leakage open since February) indicating that some core problems are not yet resolved. Hermes closes P1s within 11 days on average (e.g., #34089), suggesting a more focused stabilization effort.
- **Feature velocity:** Hermes is shipping major features (A2A plugin, Kanban, broadcast) almost daily. OpenClaw’s open PRs include several infrastructure upgrades (runtime self‑context, xAI voice provider) but many are not yet merged.

**Maturity assessment:** OpenClaw is more mature in scope but carries technical debt; Hermes is younger but faster to iterate and ship.

## 7. Trend Signals

From community feedback and issue discussions across both projects, several industry‑wide trends emerge:

1. **Multi‑agent orchestration is the top demand.** A2A protocol (Hermes #514, 18 👍) and subagent tool allowlists (OpenClaw #78441) show that developers want agents that can discover and communicate with each other autonomously.

2. **Security and data leakage are non‑negotiable.** Text leakage between tool calls (#25592) and cron identity leakage (#10769) are high‑severity concerns that undermine trust in production deployments.

3. **Platform‑specific reliability remains a weak spot.** Windows gateway crashes, macOS update freezes, and WSL2 signal handling issues are recurring themes. Users expect cross‑platform parity.

4. **Memory management is a constant challenge.** Both projects are developing bounded memory, compaction safeguards, and in‑turn consolidation to prevent context overflow and data loss.

5. **Real‑time voice and multimodal are expanding.** OpenClaw’s addition of xAI realtime voice (PR #91308) and Hermes’ vision tool compatibility fixes (Xiaomi, Azure) signal provider diversification.

6. **Desktop and GUI integration is a growth vector.** Hermes’ Kanban board, preview tabs, and “send to all” broadcast reflect a shift from pure CLI/API agents to visual, collaborative interfaces.

**Value for AI agent developers:** These trends highlight the need to invest in robust session persistence, multi‑agent protocol support, and cross‑channel reliability before scaling to production. The ecosystem is still converging on standards—A2A being the most promising—and early adopters who contribute to these efforts will shape the next generation of agent infrastructure.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-08

## 1. Today's Overview
Hermes Agent saw extremely high activity today, with **50 issues** and **50 pull requests** updated in the last 24 hours. Of those, **33 issues remain open**, **17 were closed**, and **46 PRs are still open** with only **4 merged/closed**. No new releases were published. The community is deeply engaged on the long‑anticipated A2A (Agent‑to‑Agent) protocol implementation, which finally saw its first PR today. At the same time, a wave of bug reports — many at P2 severity — landed, particularly around gateway stability on Windows and macOS, DM session isolation, and vision tool compatibility with non‑OpenAI providers. The project is in a **rapid iteration cycle** with significant contributions from both core team and external developers.

## 2. Releases
None today.

## 3. Project Progress
**Merged/Closed PRs (4 total):**
- [PR #39474](https://github.com/NousResearch/hermes-agent/pull/39474) (closed) – **feat(desktop):** “send to all” broadcast across profiles, enabling simultaneous prompt delivery to every active profile from the profile rail.
- [PR #40726](https://github.com/NousResearch/hermes-agent/pull/40726) (closed) – **fix(migration):** adds warning‑only preflight checks for cron scanner and workflow cleanup during OpenClaw → Hermes migration.
- [PR #41610](https://github.com/NousResearch/hermes-agent/pull/41610) (closed) – **fix(nous):** single‑provider Nous setups now re‑probe during rate‑limit cooldown, recovering as soon as capacity frees up rather than waiting for worst‑case `reset_at`.

**Closed Issues (17 total) — highlights:**
- [#34089](https://github.com/NousResearch/hermes-agent/issues/34089) (P1) – conversation compression desync between agent and gateway (fixed, tests added in PR #41727).
- [#13631](https://github.com/NousResearch/hermes-agent/issues/13631) – Honcho auto‑injected context breaking KV cache (closed).
- [#33169](https://github.com/NousResearch/hermes-agent/issues/33169) – Kanban SQLite corruption with concurrent gateway/dashboard processes (closed).
- [#32064](https://github.com/NousResearch/hermes-agent/issues/32064) – bounded memory fix: durable unlimited user memory with retrieval (closed).
- [#27918](https://github.com/NousResearch/hermes-agent/issues/27918) – OpenAI Codex GPT‑5.5 context length correction to 1M (closed).
- [#25176](https://github.com/NousResearch/hermes-agent/issues/25176) – Multi‑Agent Communication Channel feature request (closed, superseded by A2A plugin).
- [#10769](https://github.com/NousResearch/hermes-agent/issues/10769) – cron job identity leakage (closed).
- [#32671](https://github.com/NousResearch/hermes-agent/issues/32671) – delegate tool ignoring persistent config (closed).
- [#15275](https://github.com/NousResearch/hermes-agent/issues/15275) – TUI spawning duplicate MCP serve processes (closed).
- [#35186](https://github.com/NousResearch/hermes-agent/issues/35186) – memory deletion permanent with no archive bridge (closed).
- [#38974](https://github.com/NousResearch/hermes-agent/issues/38974) – macOS update stuck (closed).
- [#40383](https://github.com/NousResearch/hermes-agent/issues/40383) – Yuanbao adapter 5‑sec shutdown delay (closed).

**Key feature advances today (via open PRs):**
- **A2A protocol plugin** ([PR #41711](https://github.com/NousResearch/hermes-agent/pull/41711)) – consolidates all A2A work into a single plugin with zero core edits.
- **Kanban integration into desktop app** ([PR #41756](https://github.com/NousResearch/hermes-agent/pull/41756)) – adds a right‑sidebar Kanban tab and slash command.
- **Memory in‑turn consolidation** ([PR #41755](https://github.com/NousResearch/hermes-agent/pull/41755)) – bounded memory now tells the model to consolidate and retry in the same turn.
- **Windows gateway watchdog** ([PR #41761](https://github.com/NousResearch/hermes-agent/pull/41761)) – Scheduled Task auto‑respawn to keep cron running.
- **DM session isolation** ([PR #41764](https://github.com/NousResearch/hermes-agent/pull/41764)) – isolates DM sessions by `user_id` when `chat_id` is absent.
- **Desktop preview tab system** ([PR #41762](https://github.com/NousResearch/hermes-agent/pull/41762)) – routes explicit‑link previews through file tabs.
- **MCP subprocess timeouts** ([PR #41758](https://github.com/NousResearch/hermes-agent/pull/41758)) – adds timeouts to four `subprocess.run()` calls.
- **Security hardening** ([PR #41754](https://github.com/NousResearch/hermes-agent/pull/41754)) – covers V4A guards, ACP reads, API auth, Discord mentions, webhook idempotency.
- **Desktop sidebar hover overlays** ([PR #41670](https://github.com/NousResearch/hermes-agent/pull/41670)) – collapsed sidebars float back on hover.

## 4. Community Hot Topics
| Item | Comments | Reactions | Summary |
|------|----------|-----------|---------|
| [#514](https://github.com/NousResearch/hermes-agent/issues/514) – A2A Protocol Support | 20 | 👍18 | Most‑discussed issue, requesting Google’s A2A standard for inter‑agent discovery and communication. PR [#41711](https://github.com/NousResearch/hermes-agent/pull/41711) opened today. |
| [#6653](https://github.com/NousResearch/hermes-agent/issues/6653) – OpenAI Codex Reauth Loop | 4 | 0 | Switching between local and OpenAI Codex across profiles triggers unnecessary re‑auth. Still open. |
| [#34089](https://github.com/NousResearch/hermes-agent/issues/34089) – Compression Desync (P1) | 4 | 0 | Critical desync between agent working memory and gateway routing, causing silent message loss. Now closed with tests PR #41727. |
| [#13631](https://github.com/NousResearch/hermes-agent/issues/13631) – KV Cache Invalidation | 4 | 1 | Honcho context rebuilds break prompt caching every N turns. Closed. |

**Analysis:** The community is **strongly pushing for agent‑to‑agent interoperability** — the A2A request (#514) has the highest engagement and now has a comprehensive plugin PR. Authentication stability (#6653) and memory management (#13631) are also recurring pain points. The speed at which issues like #34089 (P1) were fixed and tests added shows the maintainers are responsive to severe bugs.

## 5. Bugs & Stability
**Newly reported bugs today (June 8) ranked by severity:**

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#41676](https://github.com/NousResearch/hermes-agent/issues/41676) | **P2** | macOS launchctl fallback gateway not recognized as healthy → repeated restarts | No |
| [#41662](https://github.com/NousResearch/hermes-agent/issues/41662) | **P2** | Windows gateway cron scheduler dies with gateway crash; `os.kill(pid,0)` broken | [PR #41761](https://github.com/NousResearch/hermes-agent/pull/41761) |
| [#41660](https://github.com/NousResearch/hermes-agent/issues/41660) | **P2** | WhatsApp send fails with bare phone number (missing `@s.whatsapp.net` JID suffix) | No |
| [#41669](https://github.com/NousResearch/hermes-agent/issues/41669) | **P3** | Desktop app Gateway mode cannot attach files (file not found) | No |
| [#41686](https://github.com/NousResearch/hermes-agent/issues/41686) | **P3** | `terminal_tool.py:_get_env_config()` crashes with `FileNotFoundError` when CWD removed | No |
| [#41737](https://github.com/NousResearch/hermes-agent/issues/41737) | **P3** | Linux desktop update freezes at 100% (Electron main process never exits) | No |
| [#39685](https://github.com/NousResearch/hermes-agent/issues/39685) | **P3** | Xiaomi vision fast path returns multimodal results → 400 error, session poisoned | No |
| [#39750](https://github.com/NousResearch/hermes-agent/issues/39750) | **P3** | Azure Foundry vision with `api_mode: responses` routes wrong → 401 | No |
| [#41688](https://github.com/NousResearch/hermes-agent/issues/41688? Not listed but multiple) | – | (Issue #41728 fix for `hermes_time.reset_cache` also a doc bug) | [PR #41728](https://github.com/NousResearch/hermes-agent/pull/41728) |

**Recent high‑severity fixed issues:**
- [#34089](https://github.com/NousResearch/hermes-agent/issues/34089) (P1) – conversation compression desync **fixed and tested**.
- [#15275](https://github.com/NousResearch/hermes-agent/issues/15275) (P2) – duplicate MCP subprocesses **closed**.
- [#10769](https://github.com/NousResearch/hermes-agent/issues/10769) – cron identity leakage **closed**.

## 6. Feature Requests & Roadmap Signals
**Top requests from today’s data:**

| Request | Issue/PR | Likely Next Version? |
|---------|----------|----------------------|
| A2A Protocol Support | [#514](https://github.com/NousResearch/hermes-agent/issues/514) → [PR #41711](https://github.com/NousResearch/hermes-agent/pull/41711) | ✅ **High** – plugin already drafted. |
| Kanban Board in Desktop | [#41222](https://github.com/NousResearch/hermes-agent/issues/41222) → [PR #41756](https://github.com/NousResearch/hermes-agent/pull/41756) | ✅ **High** – implementation submitted. |
| YAML frontmatter as key‑value table in Markdown preview | [#41701](https://github.com/NousResearch/hermes-agent/issues/41701) | **Medium** – small UX improvement. |
| Auto‑open preview attachments for explicit‑link sources | [#41702](https://github.com/NousResearch/hermes-agent/issues/41702) | **Medium** – aligns with desktop tab system PR. |
| “Send to all” broadcast across profiles | [PR #39474](https://github.com/NousResearch/hermes-agent/pull/39474) | ✅ Already merged today. |
| Clipboard set + macOS PyObjC acceleration | [PR #41757](https://github.com/NousResearch/hermes-agent/pull/41757) | **Medium** – new tool enhancement. |
| `on_session_title` plugin hook | [PR #41752](https://github.com/NousResearch/hermes-agent/pull/41752) | **Medium** – plugin developer feature. |
| Session provenance metadata for ACP compression rotation | [PR #41724](https://github.com/NousResearch/hermes-agent/pull/41724) | **Low/Medium** – ACP protocol refinement. |

**Future signals:** The community wants more multi‑agent orchestration tools (A2A, Kanban, broadcast). Desktop UX improvements (preview, file tabs, overlays) also appear frequently. Memory management continues to be refined (in‑turn consolidation PR #41755). No major architectural shifts are visible beyond the A2A plugin.

## 7. User Feedback Summary
- **Pain points (reported in issues):**
  - Re‑authentication loops when switching OpenAI Codex profiles (#6653) cause workflow interruptions.
  - Conversation compression silently loses messages (#34089) – critical for production agents.
  - Memory char limits force permanent deletion of entries with no archive (#35186) – fixed.
  - Cron job identity leakage between tasks (#10769) – fixed.
  - Windows and macOS gateway instability (#41676, #41662) – partial fixes incoming.
  - File attachment broken in Gateway mode (#41669).
  - Desktop update freezes on Linux (#41737).
- **Positive signals:**
  - High engagement on feature requests (A2A: 18 reactions) shows users want to build multi‑agent systems.
  - Many issues get closed quickly (e.g., #34089 P1 closed in 11 days).
  - External contributors are filing well‑structured issues with reproduction steps and even fix PRs (e.g., #41662 fixed by PR #41761 from community member `iamlukethedev`).
- **Use cases shared:**
  - Multi‑agent anime production studio (#25176) – creative team orchestration.
  - Kanban for multi‑agent workflow management (#41222).
  - Writing assistant clusters reporting compression bugs (#34089 from `claramiai/writer_ai`).

## 8. Backlog Watch
- **Issue #514** (A2A Protocol) – While the PR is open, the issue itself has been open since March 6. With today’s PR, it’s effectively addressed, but maintainer review is needed to close it.
- **Issue #6653** (OpenAI Codex reauth loop) – Open since April 9, last updated today but still without a fix. Notable because it affects a core provider.
- **Issue #24911** (Webhooks option missing in setup wizard) – Open since May 13, no comments from maintainers. Blocking users who want to configure GitLab webhooks via the wizard.
- **Issue #39685** (Xiaomi vision 400) – Open since June 5, no PR yet. Affects a growing provider ecosystem.
- **Issue #39750** (Azure Foundry vision 401) – Similar, still open.
- **Issue #41669** (Desktop attachment in Gateway mode) – Reported today, no response yet.
- **Issue #41686** (Terminal tool CWD crash) – No response yet.

**Maintainer attention needed:**  
- The **#24911** webhooks wizard gap is a long‑standing documentation/integration issue that blocks a setup path mentioned in

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*