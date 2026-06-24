# OpenClaw Ecosystem Digest 2026-06-24

> Issues: 190 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-24 02:51 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-24

## 1. Today's Overview

OpenClaw is in a period of **extremely high development activity** with 190 issues updated and 500 PRs updated in the last 24 hours, though no new releases were published today. The project shows a **2.3:1 open-to-closed issue ratio** (140 active vs. 50 closed) and a **11.5:1 open-to-merged PR ratio** (460 open vs. 40 merged/closed), indicating heavy review queues and ongoing work. Key focus areas include session-state integrity, message delivery reliability, provider compatibility (especially Anthropic, OpenAI, DeepSeek, and Ollama), and infrastructure improvements like SQLite migration and SSRF policy. The community is actively engaged, with several P1 issues receiving sustained discussion. Notably, no releases were cut today, suggesting the team is consolidating fixes before the next ship cycle.

## 2. Releases

**No new releases today.** The latest available version remains `2026.6.9` (commit `c645ec4`), with users reporting regressions in that release for Telegram rich messages and Dreams memory promotion.

---

## 3. Project Progress (Merged/Closed Items Today)

**Today's 40 merged/closed PRs show progress across several tracks:**

### Infrastructure & Compatibility
- **[#94949](https://github.com/openclaw/openclaw/pull/94949) (merged)** — `fix(ports): route isPortBusy through checkPortInUse to catch IPv4-only occupants`: Fixes port detection on systems where services bind only to IPv4, preventing premature `forceFreePortAndWait` exits.

### Session & Transcript Management
- **[#92582](https://github.com/openclaw/openclaw/issues/92582) (closed)** — `Bug: doctor falsely warns local memory embeddings are not ready`: False positive in `openclaw doctor` diagnostics corrected.

### Provider-Specific Fixes
- **[#93465](https://github.com/openclaw/openclaw/issues/93465) (closed)** — `bug(acpx): Windows embedded ACPX runtime fails with spawn EINVAL`: Windows ACPX path fixed, unblocking `sessions_spawn(runtime="acp")` on Windows.
- **[#95760](https://github.com/openclaw/openclaw/issues/95760) (closed)** — `[Bug]: Incomplete turn / stream cut mid-tool-calls with NVIDIA Build provider`: Silent zombie session state resolved for NVIDIA Build/GLO models.
- **[#90991](https://github.com/openclaw/openclaw/issues/90991) (closed)** — `Cron scheduled trigger contaminates global runtime state`: System-wide overload failures from cron contamination fixed.

### Session Integrity & Message Delivery
- **[#90404](https://github.com/openclaw/openclaw/issues/90404) (closed)** — `acpx TypeError: Cannot use in operator to search for method in 1`: ACP spawn TypeError resolved.
- **[#76729](https://github.com/openclaw/openclaw/issues/76729) (closed)** — `Feishu replies disappear from webchat after compaction rotation`: Assistant messages dropped during compaction with `truncateAfterCompaction: true` fixed.
- **[#92273](https://github.com/openclaw/openclaw/issues/92273) (closed)** — `Tool Search (mode: "tools") silently breaks pre-compaction memory flush`: Durable memory loss during tool search errors resolved.

### User-Facing Fixes
- **[#90643](https://github.com/openclaw/openclaw/issues/90643) (closed)** — `Discord mention aliases rewrite @handle inside fenced code`: Fence-detector bypass fixed for code blocks containing triple-backtick literals.
- **[#68780](https://github.com/openclaw/openclaw/issues/68780) (closed)** — `Plugin allowlist empty warning is unactionable`: First-time user UX improved for plugin warnings.

### Regression Fixes
- **[#96118](https://github.com/openclaw/openclaw/issues/96118) (closed)** — `[6.9 Regression] Dreaming runs but memory never promotes + Dreams UI shows dash`: `v2026.6.9` regression in memory promotion diagnosed and closed (fix needed in next release).

---

## 4. Community Hot Topics

### Most Commented Issues (Top 3)

| Issue | Comments | Summary |
|-------|----------|---------|
| **[#88838](https://github.com/openclaw/openclaw/issues/88838)** | 35 | Track core session/transcript SQLite migration via accessor seam (P1, diamond lobster). Active since June 1 — community following Path 3 seam-adoption progress. |
| **[#96148](https://github.com/openclaw/openclaw/issues/96148)** | 17 | Track iMessage source-reply latency instrumentation (P2, opened June 23). Performance investigation for message-tool-only turns. |
| **[#92201](https://github.com/openclaw/openclaw/issues/92201)** | 14 | Embedded runner: freshly streamed thinking signatures intermittently invalid on replay (Anthropic) (P1, diamond lobster). Recovery wrapper never fires. |

### Most Reacted Issues

| Issue | 👍 | Summary |
|-------|-----|---------|
| **[#42840](https://github.com/openclaw/openclaw/issues/42840)** | 7 | Feature Request: Add MathJax/LaTeX Support to Control UI |
| **[#94518](https://github.com/openclaw/openclaw/issues/94518)** | 3 | DeepSeek cache hit rate <10% after 6.x upgrade |
| **[#92043](https://github.com/openclaw/openclaw/issues/92043)** | 2 | 180s compaction timeout is a single wall clock with no partial-progress reuse |

### Analysis of Community Needs

The most active threads reveal **three systemic concerns**:

1. **Session/Transcript Data Integrity** — Issues like [#88838](https://github.com/openclaw/openclaw/issues/88838) (35 comments) and [#92201](https://github.com/openclaw/openclaw/issues/92201) (14 comments) reflect anxiety around data loss during compaction, migration, and replay. Users need reliable long-running sessions without silent corruption.

2. **Provider Performance & Caching** — [#96148](https://github.com/openclaw/openclaw/issues/96148) and [#94518](https://github.com/openclaw/openclaw/issues/94518) (👎3) show users deeply invested in prompt caching efficiency, especially for DeepSeek and iMessage latency — suggesting the community is pushing OpenClaw toward production-scale performance.

3. **Newcomer UX** — [#42840](https://github.com/openclaw/openclaw/issues/42840) (👍7, 8 comments) combines a feature request for LaTeX rendering with a recurring theme: users want the chat UI to handle scientific/mathematical content gracefully, a gap that affects both new and power users.

---

## 5. Bugs & Stability

### Critical (P1) Bugs Active Today

| Issue | Impact | Fix PR? | Summary |
|-------|--------|---------|---------|
| **[#92043](https://github.com/openclaw/openclaw/issues/92043)** | session-state, crash-loop | No new PR | 180s compaction timeout is single-wall-clock with no partial-progress reuse; legitimately long compactions fail every turn |
| **[#88870](https://github.com/openclaw/openclaw/issues/88870)** | session-state, message-loss | [#89045](https://github.com/openclaw/openclaw/pull/89045) open | Stuck-session recovery aborts long-but-active agent runs with misleading "Reply operation aborted by user" |
| **[#94228](https://github.com/openclaw/openclaw/issues/94228)** | session-state, message-loss, auth-provider | No PR | Native Anthropic path: replaying historical `thinking` blocks bricks long tool-use threads with 400 "Invalid signature" |
| **[#92201](https://github.com/openclaw/openclaw/issues/92201)** | session-state, message-loss | No PR | Anthropic thinking signatures invalid on replay; recovery wrapper never fires |
| **[#94939](https://github.com/openclaw/openclaw/issues/94939)** | data-loss, message-loss | No PR | 6.x state migration leaves channel conversation-store SQLite empty (0 bytes) — orphans references, breaks MS Teams proactive sends |
| **[#95833](https://github.com/openclaw/openclaw/issues/95833)** | session-state, message-loss | No PR | Subagent abort-settle fails to release `.jsonl.lock`, permanently breaking the session |
| **[#94251](https://github.com/openclaw/openclaw/issues/94251)** | session-state, message-loss, auth-provider | No PR | Ollama remote provider streaming not consumed — model_call:started never progresses |

### High-Severity Regressions

- **[#95554](https://github.com/openclaw/openclaw/issues/95554)** (P2) — Telegram `richMessages` breaks paragraph breaks and table rendering on 2026.6.9
- **[#96118](https://github.com/openclaw/openclaw/issues/96118)** (P2, now closed) — Dreams UI shows dash on 6.9, memory never promotes
- **[#95538](https://github.com/openclaw/openclaw/issues/95538)** (P2) — Telegram `/status` card collapses into one run-on line on 2026.6.9

### Notable Infrastructure Bugs

- **[#92057](https://github.com/openclaw/openclaw/issues/92057)** (P1) — Gateway slow/times out under multi-session load
- **[#85844](https://github.com/openclaw/openclaw/issues/85844)** (P1) — Auto-update leaves stale hashed bundle imports in running gateway
- **[#86034](https://github.com/openclaw/openclaw/issues/86034)** (P2) — Media generation succeeds but completion delivery fails and looks like generation failure

---

## 6. Feature Requests & Roadmap Signals

### Features with Active PRs (Possible for Next Release)

| Feature | Issue/PR | Status | Signals |
|---------|----------|--------|---------|
| **Hosted marketplace feed** | [#96158](https://github.com/openclaw/openclaw/pull/96158), [#96155](https://github.com/openclaw/openclaw/pull/96155), [#96194](https://github.com/openclaw/openclaw/pull/96194) and 6+ stacked PRs | 📣 needs proof (all open) | Large RFC 0009 implementation stack — adds plugin marketplace commands, refresh, telemetry, registry validation |
| **Let compaction providers be MCP servers** | [#96156](https://github.com/openclaw/openclaw/issues/96156) | 3 comments, P2 | Enables any MCP tool to serve as compaction engine, not just registered plugins |
| **Session labeling (/label & /new commands)** | [#93422](https://github.com/openclaw/openclaw/issues/93422) | 3 comments, P2 | Multiple users requesting WebChat session naming for dashboard management |
| **Telegram quote/reply as first-class contract** | [#88032](https://github.com/openclaw/openclaw/issues/88032) | 3 comments, P2 | User had to local-patch quote handling; wants durable inbound contract |
| **Topic-session families** | [#90916](https://github.com/openclaw/openclaw/issues/90916) | 4 comments, P2 | Multiple named context lanes for one assistant with isolated transcripts |

### Popular New Requests

- **[#42840](https://github.com/openclaw/openclaw/issues/42840)** (👍7, 8 comments) — MathJax/LaTeX rendering in Control UI for scientific communication
- **[#92314](https://github.com/openclaw/openclaw/issues/92314)** (👍2, 4 comments) — Workboard card delete/remove API
- **[#93068](https://github.com/openclaw/openclaw/issues/93068)** (👍2, 3 comments) — Global SSRF policy configuration (gateway-level `allowRfc2544BenchmarkRange`)
- **[#96236](https://github.com/openclaw/openclaw/issues/96236)** — iOS Node TestFlight invite (user requesting mobile push notifications)

### Predictions for Next Version

The **marketplace feed stack** (8+ PRs from `giodl73-repo`) is the largest infrastructure addition in flight and likely targets `2026.7.x`. The **compaction-as-MCP** feature addresses a frequent pain point for complex deployments. I also expect a quick `2026.6.10` patch to fix the 6.9 Telegram rich messages regression and the Dreams promotion bug.

---

## 7. User Feedback Summary

### Pain Points (Repeated Across Multiple Issues)

1. **Session/Data Loss** — Numerous P1/P2 bugs describe messages disappearing, compaction failing silently, or sessions entering zombie states. Users feel anxiety about reliability for long-running agents.
2. **Provider Incompatibility Churn** — Multiple reports of models working in `2026.5.26` but breaking in `2026.5.27/28` (DeepSeek V4 Flash, [#88657](https://github.com/openclaw/openclaw/issues/88657)). Users upgrade hesitantly.
3. **Migration Fragility** — `2026.5.x → 2026.6.x` migrations cause orphaned OAuth profiles ([#95136](https://github.com/openclaw/openclaw/issues/95136)), empty SQLite stores ([#94939](https://github.com/openclaw/openclaw/issues/94939)), and stale bundle imports ([#85844](https://github.com/openclaw/openclaw/issues/85844)).
4. **Config Validation Gaps** — Users hit cryptic errors when provider IDs are renamed (e.g., `openai-codex` → `openai`, [#96257](https://github.com/openclaw/openclaw/pull/96257)) or when config options silently break behavior.

### Satisfaction Signals

- **Quick triage responsiveness** — Issues like [#96118](https://github.com/openclaw/openclaw/issues/96118) (6.9 regression) and [#93465](https://github.com/openclaw/openclaw/issues/93465) (Windows ACPX) have active PRs or are already closed within 1–2 days.
- **Structured test migration** — PRs like [#96058](https://github.com/openclaw/openclaw/pull/96058) refactoring tests to shared temp directory helpers show ongoing test infrastructure improvement.
- **Portable use cases emerging** — User requesting iOS node ([#96236](https://github.com/openclaw/openclaw/issues/96236)) and Telegram custom rich message behavior indicate growing demand for OpenClaw as a personal AI assistant.

### Representative User Quote

> *"The model worked without issues in 2026.5.26"* — multiple issue authors describing regressions after version bumps (e.g., [#88657](

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant / Agent Open-Source Ecosystem

## 1. Ecosystem Overview

The open-source personal AI assistant landscape is currently defined by two distinct architectural philosophies: **platform-oriented core reference systems** (OpenClaw) and **end-user-focused agent runtimes** (Hermes Agent). Both projects are experiencing intense development activity, with common pain points around session integrity, provider compatibility churn, and token efficiency. The ecosystem is shifting from single-model assistants toward multi-provider, multi-agent orchestration, while users increasingly demand production-grade reliability (e.g., no silent data loss) and cost-optimized API usage. The emergence of gateway integrations (Telegram, Discord, Feishu) and local model support (Ollama) underscores a broadening user base spanning personal assistants to enterprise deployments.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues updated (24h)** | 190 | 50 |
| **Open / Closed issues** | 140 open / 50 closed | Not specified (50 total updated) |
| **PRs updated (24h)** | 500 | 50 |
| **Open / Merged PRs** | 460 open / 40 merged | ~44 open / 6 merged |
| **Release status** | No release today (latest v2026.6.9 with regressions) | No release today (latest v0.17.0 / 2026.6.19) |
| **Health score (qualitative)** | **Moderate**: high activity but heavy review backlog (11:1 open/merged PRs), multiple P1 regressions | **Concerning**: several critical P1 bugs without fix PRs, maintainer bandwidth appears stretched |

*Note: Hermes digest did not provide absolute open/closed counts; estimates based on 50 total updates and 6 closures.*

## 3. OpenClaw’s Position

**Advantages vs. peers:**
- **Scale**: 3–4× more issues and PRs than Hermes, suggesting a larger developer community and more aggressive feature development.
- **Infrastructure depth**: Unique initiatives like SQLite migration for session/transcript storage (`#88838`), global SSRF policy configuration, and a hosted marketplace feed (8+ stacked PRs) show a platform-building mindset.
- **Provider compatibility breadth**: Explicit support for Anthropic, OpenAI, DeepSeek, Ollama, NVIDIA Build, and others, with dedicated fixes for each (e.g., ACPX runtime on Windows, Anthropic thinking signature issues).

**Technical approach differences:**
- OpenClaw treats the assistant core as a **composable framework** with plugin-based compaction, MCP server integration, and a full command-line toolchain (`openclaw doctor`, session labeling). Hermes focuses on a **runtim-plus-gateway** model with stronger emphasis on token optimization and coding agent orchestration.
- OpenClaw’s architecture leans toward **stateful session management** (compaction, transcription, dreams/memory promotion), whereas Hermes prioritizes **lightweight stateless gateways** (Telegram, desktop) with credential pooling.

**Community size comparison:** OpenClaw’s 190 issues and 500 PRs vs. Hermes’ 50 each indicates roughly 3–4× higher raw engagement. However, Hermes’ high upvote counts on token-related issues (14 👍, 16 👍) suggest a passionate, focused user base.

## 4. Shared Technical Focus Areas

| Focus Area | OpenClaw | Hermes Agent |
|------------|----------|--------------|
| **Session/Data Integrity** | P1 bugs in compaction timeout, message loss, stuck sessions (`#92043`, `#88870`) | P1 credential pool drops (`#19566`), redaction breaking tool calls (`#43083`), Telegram duplication loop (`#48648`) |
| **Provider Compatibility Churn** | DeepSeek cache hit rate drop, Anthropic thinking signature failures, Ollama streaming not consumed | OpenAI-Codex credential pool issues, Vertex AI provider pending, `gpt-5.5` backend errors |
| **Gateway Reliability** | Telegram rich messages regressions (6.9), Feishu replies disappearing, iMessage latency | Telegram typing indicator stuck, infinite message duplication, Docker gateway `.env` stripping |
| **Migration Fragility** | 5.x→6.x migration leaves empty SQLite stores, orphaned OAuth profiles, stale bundle imports | Desktop app reinstall prompts on every launch, profile deletion silently fails |
| **Multi-Agent Orchestration** | Subagent abort-settle lock issues (`#95833`), topic-session families (`#90916`) | Generalized ACP client to orchestrate Claude Code/Cursor (`#5257`) |

**Underlying requirement:** Both communities are demanding **reliable long-running sessions** with zero data loss and **seamless multi-provider failover** — a sign that personal AI assistants are moving from prototypes to production systems.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary focus** | Core reference platform for AI agents (session management, provider abstraction, plugin ecosystem) | Personal AI assistant runtime with coding agent orchestration, gateway integrations, credential management |
| **Target users** | Developers building agent systems, power users who want CLI + WebChat + deep configurability | End users (Telegram, desktop), developers needing lightweight assistant with multi-gateway support |
| **Key architectural strengths** | Stateful session compaction (MCP-based), marketplace feed, SSRF policy, rich dashboard | Token efficiency (lazy schema loading), multi-agent ACP client, credential pooling, billing tracking |
| **Pain points** | Heavy review backlog (460 open PRs), regression-prone releases (`6.9` Telegram/ Dreams bugs) | Unresolved P1 bugs with no fix PRs, maintainer bottleneck, narrower provider coverage |
| **Community engagement style** | High issue/PR volume, structured RFC process (RFC 0009 for marketplace) | Vocal user base on token overhead, strong upvote signals, but slower resolution |

**Key takeaway:** OpenClaw is the **“Linux kernel”** of personal AI agents — broad, infrastructure-heavy, but occasionally unstable. Hermes is the **“Ubuntu”** — more focused on user experience and specific workflows, but with less engineering bandwidth for deep platform-level fixes.

## 6. Community Momentum & Maturity

**Activity tiers:**
- **Rapid iteration with heavy backlog**: OpenClaw (500 PRs updated, 460 open). The 11:1 open-to-merged PR ratio signals that the project is taking in many contributions faster than it can review them, which can lead to code quality debt.
- **High activity but limited throughput**: Hermes Agent (50 PRs updated, 6 merged). The low merge ratio (8:1 open/merged) and multiple P1 bugs without fixes suggest maintainer capacity is a bottleneck.

**Stabilization signals:**
- OpenClaw is consciously consolidating fixes (no release today, multiple regression closures). The active SQLite migration and marketplace RFC indicate a structural cleanup phase.
- Hermes has no release today and several long-standing performance issues (token overhead, credential redaction) without resolved PRs, suggesting a **pre-stabilization phase** where features outpace polish.

**Maturity indicators:**
- Both projects have formal issue triage (P1/P2 labels) and structured community discussion, but OpenClaw shows higher process maturity (RFCs, test infrastructure refactors, migration paths).

## 7. Trend Signals

**Industry trends extracted from community feedback:**

1. **Token cost optimization is the #1 unmet need.** Hermes’ 73% fixed overhead analysis and 14 upvotes on lazy schema loading reflect a pressing demand. OpenClaw does not mention token efficiency, representing a potential gap.

2. **Multi-agent interoperability is becoming table stakes.** Hermes’ ACP client generalization and OpenClaw’s subagent fix point to a future where personal AI assistants must orchestrate other agents (Claude Code, Cursor, etc.) — not just host their own.

3. **Session reliability is non-negotiable.** Both projects have multiple P1 bugs around data loss, message dropping, and stuck sessions. Users expect “set and forget” operation for long-running agents.

4. **Credential and security management is fragile.** Redaction bugs, credential pool drops, and SSRF policy requests show that as assistants gain more tool access, security boundaries are still immature.

5. **Gateway diversity is accelerating.** Telegram, Feishu, iMessage, Discord – users want to interact with their assistant on any platform. Standardizing these gateways (e.g., OpenClaw’s quote/reply contract) will be a differentiator.

**Value for AI agent developers:**
- Focus on **reliable state persistence** (compaction, migration, replay) to differentiate from plugins that lose data.
- Invest in **token-aware tool selection** and **lazy schema loading** to win cost-sensitive and local-model users.
- Build **multi-agent orchestration** capabilities early – the ecosystem will reward composability over monoliths.
- Prioritize **security guardrails** (credential redaction, SSRF, approval gates) to satisfy enterprise adopters.

---

*Generated from 2026-06-24 community digests for OpenClaw and Hermes Agent.*

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-24

## 1. Today's Overview

Hermes Agent saw extremely high activity over the past 24 hours, with **50 issues and 50 pull requests updated**, and **6 PRs merged or closed**. The project remains in a rapid development cycle with substantial community engagement, though no new releases were published today. Bug fixes and feature requests related to token optimization, gateway reliability, and credential management dominated the conversation, while several long-standing performance concerns continue to attract attention.

## 2. Releases

No new releases were published today (last release: v0.17.0 / 2026.6.19, as referenced in issue #51579). No migration notes or breaking changes to report.

## 3. Project Progress

Only a small number of PRs were merged or closed today:

- **#17209** (closed) – Added a generic WSL-to-Windows printer invocation skill.
- **#39118** (closed) – Fixed Termux uv installation triggering Rust source compile; now uses prebuilt binary or skips.
- **#51575** (closed) – Fixed desktop stop-button popup referencing non-existent `/interrupt` command.
- **#51587** (closed) – Reported MCP server tools not surfacing into agent session toolsets; closed as needs-repro.
- Three other PRs were merged/closed (not listed in top 20 but indicated by the 6 total).

No major feature branches or architectural changes were merged today, but several open PRs are progressing (see Feature Requests & Roadmap).

## 4. Community Hot Topics

The most active discussions revolve around **token efficiency** and **multi-agent orchestration**:

- **[#6839 – Lazy Tool Schema Loading](https://github.com/NousResearch/hermes-agent/issues/6839)**  
  *26 comments, 14 👍* – A proposal to reduce token overhead by injecting only relevant tool schemas per call instead of all 50+ tools. Users strongly support this as a major performance win for local models and cost-sensitive deployments.

- **[#4379 – Token Overhead Analysis](https://github.com/NousResearch/hermes-agent/issues/4379)**  
  *15 comments, 0 👍* – Detailed analysis showing 73% of each API call (~13.9K tokens) is fixed overhead, based on real deployment monitoring. Complements #6839 and drives demand for lazy loading.

- **[#5257 – Generalized ACP Client](https://github.com/NousResearch/hermes-agent/issues/5257)**  
  *11 comments, 16 👍* – Proposes extending Hermes' Agent Client Protocol (ACP) client to orchestrate any ACP-compatible coding agent (Claude Code, Cursor, etc.), not just Copilot. Strong community interest in multi-agent workflows.

- **[#19566 – OpenAI-Codex Credential Pool Drops New Credentials](https://github.com/NousResearch/hermes-agent/issues/19566)**  
  *8 comments, 1 👍* – A high-severity bug where newly added credentials can be lost during stale `auth.json` rewrite on rotation. Users report unreliable multi-credential setups.

- **[#43083 – Passwords Redacted but Model Fails on Second Tool Call](https://github.com/NousResearch/hermes-agent/issues/43083)**  
  *8 comments* – A security/functionality bug where redacting credentials from conversation history causes the model to fail when it reads back its own history. Highlights need for more robust redaction design.

**Underlying needs:** Users are demanding **better token management**, **reliable multi-provider/credential support**, and **interoperability with other coding agents**. The project's next major version should address the token overhead crisis to retain local-model users and cost-conscious cloud users.

## 5. Bugs & Stability

Several high-severity bugs were reported or updated today, ranked by priority:

- **[P1] #19566 – Credential pool drops newly added credential** – Critical for multi-key OpenAI deployments. No fix PR yet.
- **[P1] #43083 – Passwords redacted but model fails on second tool call** – Security boundary issue. No fix PR.
- **[P1] #48648 – Infinite Telegram message duplication loop during 4096-char overflow** – Caused by improper streaming handling. No fix PR linked.
- **[P1] #51579 – Docker `gateway run` strips `.env` on every container start** – Regression of #26804, kills Telegram config. No fix.
- **[P2] #38387 – Windows gateway Scheduled Task leaves blank console window** – Due to `uv venv pythonw` redirect misbehavior. No fix.
- **[P2] #28004 – Telegram typing indicator stuck indefinitely** – Race condition in `_keep_typing`. No fix.
- **[P2] #49787 – Desktop app reinstall prompt on every launch despite valid config** – Affects macOS users. No fix.
- **[P2] #50005 – Desktop non-functional on WebSocket disconnect** – No offline mode. No fix.
- **[P2] #47368 – Desktop profile deletion fails silently** – Profile reappears. No fix.
- **[P2] #38146 – Desktop installer fails with 389 TS errors on main** – Build breakage. No fix.
- **[P3] #51045 – Nous Portal `gpt-5.5` returns Azure backend error (500)** – Provider outage. No fix.
- **[P3] #42083 – Payment error detection misses 502/503/504 / UNAVAILABLE** – False negative detection. No fix but a PR may address it.

**Most urgent:** The credential pool bug (#19566) and the Telegram duplication loop (#48648) are likely causing real user pain. No fix PRs exist for either, suggesting maintainer bandwidth is stretched.

## 6. Feature Requests & Roadmap Signals

The following requested features have strong community support and are likely to appear in the next minor/major release:

- **Lazy Tool Schema Loading (#6839)** – Already has a thorough design; would drastically reduce token waste.
- **Generalized ACP Client (#5257)** – Enables Hermes to orchestrate Claude Code, Cursor, etc. Strong upvoted.
- **Multi-model billing tracking (#51607, #51634)** – PR #51634 is already open to track per-model token usage mid-session; likely to be merged soon.
- **Ollama Cloud plugin-based provider (#22648)** – PR open since May; rebased and ready for review.
- **Zulip integration (#3335)** – Stale PR from March, but no recent movement.
- **Vertex AI provider for Gemini (#8427)** – PR open since April; enterprise users interested.
- **Terminal subscription view and billing cleanup (#51639)** – Fresh PR; indicates focus on monetization and user self-service.
- **Feishu improvements and tool-loop guardrails (#49631)** – PR with improvements for Chinese platform users.

**Prediction:** The next version will likely include **lazy tool schema loading** (if accepted), **per-model billing tracking**, and **Ollama Cloud support**. The token overhead issue is the most urgent for the user base.

## 7. User Feedback Summary

- **Pain Points:** 
  - Token overhead is the #1 complaint – users are paying for thousands of wasted tokens per turn.
  - Credential management is fragile (losing keys, redaction breaking tool calls).
  - Telegram gateway suffers from infinite loops and stuck typing indicators.
  - Desktop app has multiple stability issues (profile deletion, reinstall prompts, build failures).
  - MCP tools fail to surface in sessions despite correct configuration.
  - Security: non-shell tools bypass approval gate (#35357).

- **Use Cases:** 
  - Running Hermes as a personal assistant with Telegram/WhatsApp gateways.
  - Multi-agent orchestration (Claude Code + Hermes).
  - Local model usage (Ollama) where token efficiency is critical.
  - Enterprise deployment with multi-key providers (OpenAI Codex pools).

- **Satisfaction:** 
  - Users appreciate the breadth of built-in tools and gateway integrations.
  - The active community and rapid issue triage (many closed today) is positive.
  - However, long-standing high-severity bugs without fix PRs suggest maintainer capacity is limited.

## 8. Backlog Watch

Issues and PRs that have been open for extended periods with no resolution or maintainer activity:

- **[#6839 – Lazy Tool Schema Loading](https://github.com/NousResearch/hermes-agent/issues/6839)** – Created April 9, high activity, no PR yet. Should be a priority.
- **[#4379 – Token Overhead Analysis](https://github.com/NousResearch/hermes-agent/issues/4379)** – Created April 1, data-driven but no assigned milestone.
- **[#5257 – Generalized ACP Client](https://github.com/NousResearch/hermes-agent/issues/5257)** – Created April 5, strong community support, no assignee.
- **[#3335 – Zulip Integration (PR)](https://github.com/NousResearch/hermes-agent/pull/3335)** – Open since March 27, no recent commits. May need rebase or decision.
- **[#8427 – Vertex AI Provider (PR)](https://github.com/NousResearch/hermes-agent/pull/8427)** – Open since April 12, waiting for review.
- **[#19566 – Credential Pool Drops New Credentials](https://github.com/NousResearch/hermes-agent/issues/19566)** – P1, open since May 4, no PR. Risk to production deployments.
- **[#43083 – Password Redaction Bug](https://github.com/NousResearch/hermes-agent/issues/43083)** – P1, open since June 9, no fix. Affects security boundary.

These items either require maintainer prioritization (especially the P1 bugs) or community contribution to move forward. The project health would benefit from addressing at least the token overhead and credential pool issues before the next release.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*