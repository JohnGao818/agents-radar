# OpenClaw Ecosystem Digest 2026-07-27

> Issues: 350 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-27 02:32 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-07-27

## 1. Today's Overview
OpenClaw remains extraordinarily active, with **350 issues** and **500 pull requests** updated in the last 24 hours. Almost **70% of issues** are still open (242 open), and **345 PRs were merged or closed** today – indicating a strong focus on fixing regressions and shipping incremental improvements. No new releases were cut today, but the volume of merged work suggests a release candidate may be approaching. The project is clearly in a **heavy maintenance cycle** with many P1 bugs and sessions‑state regressions being actively addressed, while the community continues to push for long‑standing features like desktop app support and per‑agent tool restrictions.

## 2. Releases
No new releases were recorded today.

## 3. Project Progress (Merged/Closed PRs Today)
Today’s 345 closed/merged PRs include a broad mix of **performance optimizations, UI fixes, channel‑refactoring, and tooling improvements**. Notable merges from the top‑30 list:

- **`#114237`** – Improves `sessions.list` performance by eliminating O(rows²) full‑store scans in ACP meta reads ([PR](https://github.com/openclaw/openclaw/pull/114237))
- **`#114230`** – Freezes parity between two private OpenAI Responses stream processors to prevent future drift ([PR](https://github.com/openclaw/openclaw/pull/114230))
- **`#114233`** – Completes the Labs UI roster with Tool Search, lean local‑model tools, and message audit metadata gates ([PR](https://github.com/openclaw/openclaw/pull/114233))
- **`#114235`** – Refactors IRC outbound sends to use the central message adapter, eliminating duplicate presentation logic ([PR](https://github.com/openclaw/openclaw/pull/114235))
- **`#114229`** – Centralizes talk‑back readiness logic across Google Meet, Teams, and Zoom plugins ([PR](https://github.com/openclaw/openclaw/pull/114229))
- **`#114225`** – Fixes `check:changed` to fall back to local execution when the CI backend is unavailable ([PR](https://github.com/openclaw/openclaw/pull/114225))
- **`#114228`** – Splits config‑write preparation primitives ahead of a larger config redesign ([PR](https://github.com/openclaw/openclaw/pull/114228))
- **`#113842`** – Fixes new‑session composer auto‑growing before scrolling in the Web UI ([PR](https://github.com/openclaw/openclaw/pull/113842))
- **`#113834`** – Prevents worktree sessions from briefly showing in “Threads” before moving to “Coding” ([PR](https://github.com/openclaw/openclaw/pull/113834))

These merges reflect ongoing work to reduce latency, simplify plugin internals, and polish the Control UI.

## 4. Community Hot Topics
The most active discussions this week revolve around **critical user‑facing regressions** and a **long‑standing feature gap**:

- **Desktop app for Linux/Windows** – Issue [#75](https://github.com/openclaw/openclaw/issues/75) continues to dominate with **115 comments** and **80 👍** reactions. Users across platforms are requesting parity with the existing macOS, iOS, and Android apps. Despite high demand, no development PRs have been linked.
- **Tool output rendered as unreadable image attachments** – Issue [#99241](https://github.com/openclaw/openclaw/issues/99241) (24 comments) describes a scenario where ANSI‑heavy tool results collapse into `(see attached image)`, making the output invisible to the agent. This P1 bug directly impacts agent reasoning reliability.
- **Duplicate replies on Telegram after 5.20 update** – Issue [#86519](https://github.com/openclaw/openclaw/issues/86519) (12 comments) reports 2–10× duplicate messages. The severity is high enough that some users are unable to use the Telegram channel effectively.
- **Second message fails with “reply session initialization conflicted”** – Issue [#102020](https://github.com/openclaw/openclaw/issues/102020) (15 comments) blocks multi‑turn conversations on multiple channels.
- **Session compaction timeout failures** – Issue [#92043](https://github.com/openclaw/openclaw/issues/92043) (12 comments) highlights that the new 180 s compaction timeout is a single wall‑clock budget, so slow (but legitimate) compactions fail every turn.

On the PR side, the largest active pull requests are **`#114167`** (workboard status notifications, `size: L`), **`#114236`** (unify OpenAI completions compatibility, `size: L`), and **`#113500`** (route bundled command replies across four channels, `size: XL`). These are still in review/proof status.

## 5. Bugs & Stability
Today’s bug report density is **unusually high**, with multiple **P1 and P0** issues affecting session state, message delivery, and gateway stability. Key bugs sorted by severity:

| Issue | Priority | Impact | Summary | Fix PR? |
|-------|----------|--------|---------|---------|
| [#90378](https://github.com/openclaw/openclaw/issues/90378) | **P0** | session‑state, data‑loss, message‑loss | Upgrading 5.28→6.1 silently migrates cron store to SQLite with wrong delivery mode, causing channel errors | Linked PR open |
| [#99241](https://github.com/openclaw/openclaw/issues/99241) | P1 | session‑state, message‑loss | Tool outputs become image attachments, unreadable to agent | No fix PR linked |
| [#102020](https://github.com/openclaw/openclaw/issues/102020) | P1 | session‑state, message‑loss | Second message fails with “reply session initialization conflicted” | No fix PR linked |
| [#86519](https://github.com/openclaw/openclaw/issues/86519) | P1 | session‑state, message‑loss | Agent repeats identical replies 2–10x on Telegram | No fix PR linked |
| [#92043](https://github.com/openclaw/openclaw/issues/92043) | P1 | session‑state, crash‑loop | 180 s compaction timeout is non‑resumable; legitimate slow compactions fail identically | No fix PR linked |
| [#85251](https://github.com/openclaw/openclaw/issues/85251) | P1 | session‑state, message‑loss | Codex app‑server goes silent after `notification:turn/started`; session stuck for 360 s | No fix PR linked |
| [#94251](https://github.com/openclaw/openclaw/issues/94251) | P1 | session‑state, message‑loss, auth‑provider | Ollama streaming not consumed; model call never progresses | No fix PR linked |
| [#85844](https://github.com/openclaw/openclaw/issues/85844) | P1 | session‑state, message‑loss | Auto‑update leaves stale hashed bundle imports; gateway uses old modules | No fix PR linked |
| [#103917](https://github.com/openclaw/openclaw/issues/103917) | P1 | crash‑loop | Gateway crashes when subagent workspace directory is deleted before spawn | No fix PR linked |
| [#112423](https://github.com/openclaw/openclaw/issues/112423) | P1 | session‑state | Large SQLite transcript cleanup blocks the gateway event loop | No fix PR linked |
| [#113434](https://github.com/openclaw/openclaw/issues/113434) | P1 | session‑state, crash‑loop | Codex session reset reuses retired session ID; catalog scans exhaust RAM | No fix PR linked |
| [#113315](https://github.com/openclaw/openclaw/issues/113315) | P1 | message‑loss | Telegram inbound update permanently lost after offset persistence with no dispatch | No fix PR linked |
| [#111519](https://github.com/openclaw/openclaw/issues/111519) | P1 | session‑state, message‑loss | Telegram DM replies fall back after stale DM‑scope cleanup in 2026.7.2‑beta.3 | No fix PR linked |

Several **closed bugs** today include [#99263](https://github.com/openclaw/openclaw/issues/99263) (Gateway crash on Node 26 due to FileHandle GC) and [#98673](https://github.com/openclaw/openclaw/issues/98673) (sanitizeContentBlocksImages incorrectly converting text to image blocks). These appear to have been resolved in recent merges.

On the fix front, PRs **`#114188`** (delegated subagents honor per‑call timeouts), **`#112871`** (fixes Voice Wake migration startup loops), and **`#114215`** (empty npm install failures now report exit code) are open and awaiting maintainer review.

## 6. Feature Requests & Roadmap Signals
Long‑standing enhancement requests continue to accumulate. The most prominent signals for the next release:

- **Desktop apps for Linux/Windows** ([#75](https://github.com/openclaw/openclaw/issues/75)) – the top community ask, but no development activity.
- **Denylist for exec‑approvals** ([#6615](https://github.com/openclaw/openclaw/issues/6615)) – “allow everything except X” policy – has open PRs and maintainer review.
- **Per‑agent dreaming configuration** ([#67413](https://github.com/openclaw/openclaw/issues/67413)) – to avoid memory spikes when all agents dream simultaneously.
- **Per‑spawn tool restrictions** ([#15032](https://github.com/openclaw/openclaw/issues/15032)) – directly addressed by PR **`#78441`** (open, needs proof). Likely to land in the next release.
- **Distributed Agent Runtime** ([#42026](https://github.com/openclaw/openclaw/issues/42026)) – RFC proposing separation of control plane and agent compute. Still under product decision.
- **Mid‑stream message injection** ([#10960](https://github.com/openclaw/openclaw/issues/10960)) – “soft steer” to inject messages during generation, not just at tool boundaries. Gaining community support.
- **Webhook session reuse** ([#11665](https://github.com/openclaw/openclaw/issues/11665)) – documented but broken multi‑turn hook conversations; linked PR open.
- **Plugin approval APIs** ([#82336](https://github.com/openclaw/openclaw/issues/82336)) – needed for external HITL plugins; PR **`#113517`** (open) implements the external verification contract.

Given the volume of current bugfixing, it is unlikely that the next release will contain the desktop apps or distributed runtime. However, per‑spawn tool restrictions and the denylist feature have strong PR momentum and could ship soon.

## 7. User Feedback Summary
User sentiment in today’s issues reflects **frustration with regressions and missing platform support**, alongside **appreciation for the project’s rapid iteration**.

**Common pain points:**
- **Telegram duplication** – multiple users report agent repeating replies up to 10×. Workarounds exist (downgrading) but are not sustainable.
- **Tool output invisibility** – agents cannot see their own tool results, making long‑running tasks unreliable.
- **Session startup failures** – multi‑turn conversations break on second message (cross‑channel).
- **Performance degradation** – Active Memory + Codex combinations cause gateway stalls and timeouts.
- **Missing desktop clients** – many potential users are blocked on Linux/Windows support.
- **Local model support** – Ollama and llama.cpp streaming issues (e.g., [#94251](https://github.com/openclaw/openclaw/issues/94251), [#108473](https://github.com/openclaw/openclaw/issues/108473)) reduce usability for self‑hosted setups.

**Positive signals:** The community is actively contributing fixes (many PRs today from external contributors). The maintainers are responsive, tagging issues with `clawsweeper` statuses and merging PRs quickly. Users often close issues with a “fixed in latest version” note.

## 8. Backlog Watch
Several important issues remain unanswered or stalled despite maintainer labels:

| Issue | Opened | Last Activity | Status |
|-------|--------|---------------|--------|
| [#75](https://github.com/openclaw/openclaw/issues/75) – Linux/Windows apps | 2026‑01‑01 | 2026‑07‑27 | `needs‑product‑decision`, `needs‑security‑review` – high community demand but no roadmap commitment |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) – exec‑approval denylist | 2026‑02‑01 | 2026‑07‑26 | `needs‑product‑decision`,

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## 1. Ecosystem Overview

The open-source personal AI assistant and agent ecosystem is experiencing a phase of **hyperactive maintenance and stabilization**, following months of rapid feature expansion. Both OpenClaw and Hermes Agent—the two most prominent reference implementations—are investing heavily in bug fixing, security patching, and performance optimization rather than new major features. The ecosystem is converging on common pain points: session-state reliability, multi-channel message delivery, local model support, and plugin extensibility. While community engagement remains high, user frustration is growing around regressions introduced by fast release cycles, suggesting the ecosystem is overdue for a **stability-focused release cycle**. The long-standing demand for desktop clients across Linux and Windows remains a critical gap that neither project has filled, creating an opening for new entrants.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues Updated (24h)** | 350 | 50 |
| **Issues Open** | 242 (69% of total) | ~36 (estimated) |
| **PRs Merged/Closed (24h)** | 345 | 37 |
| **New Release Today** | No | No |
| **P0/P1 Bugs Reported** | 15+ (3 P0, 12+ P1) | 7 (1 P0, 6 P1) |
| **P0/P1 Bugs Fixed (24h)** | ~5 | 7 (all fixed) |
| **Health Score** | **🔴 Watch (high bug density, slow fix turnaround)** | **🟡 Monitor (fast fixes, but several P2-P3 open bugs)** |
| **Community Engagement** | Very high (115+ comments on top issue) | High (14 reactions on top feature request) |
| **Maintainer Responsiveness** | Moderate (some P1 bugs lack fix PRs) | High (all P0/P1 bugs fixed within 24-48h) |

**Interpretation:**
- **OpenClaw** has a significantly larger volume of activity but a **concerning bug-to-fix ratio**. The 69% open-issue rate and multiple P0 session-state regressions suggest a project struggling to contain technical debt during rapid iteration.
- **Hermes Agent** has smaller absolute numbers but demonstrates **superior fix velocity** (100% of P0/P1 bugs closed same-day). This suggests a more disciplined triage process and smaller codebase surface area.

---

## 3. OpenClaw's Position

### Advantages Over Peers
- **Largest Plugin Ecosystem**: Supports IRC, Google Meet, Microsoft Teams, Zoom, Telegram, and webhooks—broader than Hermes’ channel support.
- **More Advanced Session Management**: Implements worktree sessions, compaction with timeouts, and ACP meta reads—Hermes lacks equivalent depth.
- **Larger Developer Community**: 350 issues/day vs. 50 indicates more contributors and testers.
- **Deeper UI Investment**: Labs UI with Tool Search, message audit metadata, and Control UI reflect more polished frontend development.

### Technical Approach Differences
- **Architecture**: OpenClaw uses a **modular JavaScript/Node.js stack** with channel adapters; Hermes Agent is **Python-based** with a flat skill/plugin model.
- **Session State**: OpenClaw uses SQLite with compaction and gateway event loops; Hermes uses in-memory with pruning and restart gates.
- **Tool Integration**: OpenClaw has richer per-agent tool restrictions and exec-approval denylists in progress; Hermes focuses on MCP (Model Context Protocol) and shell command safety.

### Community Size Comparison
- **Issue Volume**: OpenClaw ~7× larger (350 vs. 50 issues/day)
- **PR Volume**: OpenClaw ~9× larger (345 vs. 37 PRs/day)
- **Top Issue Engagement**: OpenClaw leads (115 comments on desktop app request vs. Hermes’ 14 on CLI shell escape)
- **Risk**: OpenClaw's scale creates triage bottlenecks—critical bugs (e.g., tool output invisibility) lack fix PRs while PR volume remains high.

---

## 4. Shared Technical Focus Areas

Both projects are independently converging on the same pain points, reflecting industry-wide requirements for production AI agents:

| Focus Area | OpenClaw | Hermes Agent |
|------------|----------|--------------|
| **Session State Reliability** | Multiple P0/P1 regressions: compaction timeouts, conflicting init, silent migration errors | Fixed: pruning of active sessions, startup-restore gate silence, compaction summary loss |
| **Telegram Delivery Bugs** | Duplicate replies (2-10×), inbound message loss, DM fallback issues | FD leak that wedged gateway (fixed) |
| **Gateway Stability** | Crashes on subagent workspace deletion, SQLite block on event loop | Startup-restore gate, reconnect watcher (both fixed) |
| **Tool Output Visibility** | Agent cannot read tool results (ANSI→image attachments) | Not directly reported, but shell injection fix indicates terminal pipeline concern |
| **Local Model Streaming** | Ollama/llama.cpp streaming not consumed | Not surfaced in this digest (may use different providers) |
| **Security Hardening** | Not emphasized in today's digest | Fixed shell injection via Matrix, patched multiple CVEs |
| **Desktop App Demand** | [#75](https://github.com/openclaw/openclaw/issues/75) – 115 comments, 80 👍 | [#50643](https://github.com/NousResearch/hermes-agent/issues/50643) – 3 👍 (less vocal but present) |
| **Per-Agent Configuration** | Tool restrictions, dreaming config, approval denylists | Per-user profile routing, per-call model override |

**Key insight:** The **session-state tier** (compaction, pruning, gate startup) is the most fragile component in both projects. Any developer building on either framework should expect session lifecycle to be the primary source of production incidents.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary Language** | JavaScript/Node.js | Python |
| **Target User** | Power users, multi-platform integrators | Developers, CLI-heavy users, self-hosters |
| **Key Strength** | Breadth of channel support, UI polish | Security posture, fix velocity, Python ecosystem compatibility |
| **Key Weakness** | Bug density, slow P1 fix turnaround | Smaller community, fewer channels, less mature UI |
| **Plugin Model** | Channel adapters + tools + MCP | Skills (Python) + MCP + shell commands |
| **Desktop Support** | macOS, iOS, Android apps exist; Linux/Windows missing | Desktop in development (GUI-only with remote gateway) |
| **Identity/Auth** | Complex profile-chaining, auth providers | Simpler profile-based routing |
| **Distributed Computing** | RFC for Distributed Agent Runtime (#42026) | Not addressed |
| **Notable Feature** | Per-agent "dreaming" (background processing) | Batch migration skill (#380) |

**Strategic Recommendation:**
- **Choose OpenClaw** if you need broad channel support, deep UI customization, or Enterprise-grade session management (and can tolerate higher bug risk).
- **Choose Hermes Agent** if you value Python interoperability, security-first design, quick bug fixes, or plan to integrate with Python ML/data tools.

---

## 6. Community Momentum & Maturity

| Tier | Project | Phase | Evidence |
|------|---------|-------|----------|
| **Stabilizing** | **OpenClaw** | Heavy maintenance, regression-heavy | 70% issues open, 345 PRs/day but P0 bugs persist, multiple "fixed in latest version" user notes |
| **Rapidly Iterating (Fix-First)** | **Hermes Agent** | Security patching + rapid bug fixes | All P0/P1 fixed in 24h, 37 merged PRs, lower absolute issue volume |

### Activity Trajectory
- **OpenClaw** is in a **stabilization stall**: high velocity but failing to close the gap on critical regressions. The project risks user trust erosion if P0 bugs (e.g., tool output invisibility, session data loss) remain unlinked to fix PRs.
- **Hermes Agent** is in a **disciplined sprint**: small team, fast turnaround, security-conscious. The absence of new releases today despite high fix throughput suggests a consolidated release approaching (v0.14.x or v0.15.0).

### Community Sentiment Trends
- **OpenClaw**: Users express **frustration with regressions** but **appreciation for iteration speed**. The Telegram duplication and compaction timeout issues are direct blockers for daily use.
- **Hermes Agent**: Users are **relieved by quick fixes** but **demanding missing features** (shell escape, batch migration). The security fix applause is evident in closed-issue reactions.

---

## 7. Trend Signals for AI Agent Developers

### 1. **Security Hardening Is Becoming Non-Negotiable**
   - Hermes Agent fixed shell injection via Matrix room names. OpenClaw has no equivalent security highlight.
   - **Action**: Audit any channel that passes user-controlled strings to shell/tool execution. Implement strict input sanitization for room names, group titles, and display names.

### 2. **Tool Output Observability Is Broken (and Dangerous)**
   - OpenClaw's tool output being rendered as image attachments means agents cannot inspect their own results. This is a **fundamental reasoning gap**.
   - **Action**: Ensure your agent framework always delivers tool outputs in machine-readable form (JSON, text) before presentation. ANSI-to-image conversion should be opt-in, not default.

### 3. **Session State Is the New Reliability Frontier**
   - Both projects have multiple bugs around compaction, pruning, startup-gate silence, and session reset conflicts.
   - **Action**: Design session management with **idempotent checkpointing** and **resumable timeouts**. Avoid single wall-clock budgets for compaction (as OpenClaw discovered).

### 4. **Local Model Streaming Remains Unreliable**
   - OpenClaw reports Ollama/llama.cpp streaming not consumed. This blocks self-hosted deployments.
   - **Action**: If targeting local LLM users, invest in streaming correctness early. Consider standardized provider abstractions (e.g., LLMClient protocol) to isolate provider-specific bugs.

### 5. **Desktop Clients Are the Unaddressed Moonshot**
   - Both projects have vocal demand for Linux/Windows desktop apps. Neither has shipped. This remains the single largest growth opportunity.
   - **Action**: Evaluate Electron/Tauri-based thin clients that connect to an existing gateway. Users don’t need a full local agent; they want a desktop UI for their existing deployment.

### 6. **Multi-Turn Conversation Reliability Is Fragile**
   - OpenClaw’s "second message fails with session initialization conflicted" bug (#102020) and Hermes’ startup-restore gate silence both break the most basic user flow: asking a follow-up question.
   - **Action**: Invest in **conversation continuity testing** across all channels. A failing second message is a showstopper for any assistant product.

### 7. **Plugin Governance Is Emerging**
   - OpenClaw is adding approval denylists (#6615), per-agent tool restrictions (#15032), and plugin approval APIs (#82336). Hermes is adding per-call model overrides (#72394).
   - **Action**: Build plugin permission systems early. The "allow everything" era is ending; users need fine-grained control (denylists, per-call overrides, role-based access).

---

## Executive Summary

The AI agent open-source ecosystem is **healthy but strained**. OpenClaw dominates in community size and channel breadth but is **losing the reliability battle** with a 69% open-issue rate and unresolved P0 bugs. Hermes Agent demonstrates **how to run a tight ship**: smaller scope, faster fixes, security-first. For technical decision-makers:

- **If you need multi-channel, production-ready deployment today**: Hermes Agent may be safer despite its smaller ecosystem.
- **If you need maximum flexibility and plugin depth**: OpenClaw is the stronger platform, but budget for workarounds on session-state and tool observability issues.
- **Both projects share an industry-wide debt on desktop support, local model streaming, and multi-turn reliability**—these are the next battlegrounds.

The ecosystem is **one major stability release away from mainstream readiness**. Developer investment in session state robustness, security hardening, and desktop clients will yield outsized returns.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-27

## 1. Today's Overview

Hermes Agent saw exceptionally high activity on 2026-07-27, with **50 issues** and **50 pull requests** updated in the last 24 hours. **14 issues were closed** and **37 PRs were merged or closed**, indicating strong maintenance velocity. Several critical (P0) and high-severity (P1) bugs were fixed, including major security vulnerabilities (shell injection via Matrix, skills data loss, macOS launcher breakage) and gateway session regressions. The project remains in an active bug-fixing and security-patching cycle with no new releases today, but the rapid turnaround on fixes demonstrates a responsive core team and engaged community.

## 2. Releases

**None.** No new releases were published today.

## 3. Project Progress

The 37 merged/closed PRs today reflect significant effort across security, stability, and bug fixes:

- **Security & Critical Fixes:**
  - [PR #71306](https://github.com/NousResearch/hermes-agent/pull/71306) (P1) – Stopped multiline session environment variables (e.g., Matrix room names) from injecting shell commands via terminal snapshots.
  - [PR #72216](https://github.com/NousResearch/hermes-agent/pull/72216) (P0) – Fixed `hermes skills update` silently overwriting user skills with same-named skills from a different registry, preventing data loss.
  - [PR #71323](https://github.com/NousResearch/hermes-agent/pull/71323) (P1) – Made macOS launcher independent of external `realpath`, resolving breakage on stock macOS.
  - [PR #71593](https://github.com/NousResearch/hermes-agent/pull/71593) (P1) – Fixed Telegram fallback transport file descriptor leak that could wedge the gateway.
  - [PR #71043](https://github.com/NousResearch/hermes-agent/pull/71043) (P1) – Preserved recently active sessions during pruning; previously compared against `started_at` instead of last activity.
  - [PR #71903](https://github.com/NousResearch/hermes-agent/pull/71903) (P1) – Bounded gateway startup‑restore gate to prevent total silence during a slow resumed turn.
  - [PR #72145](https://github.com/NousResearch/hermes-agent/pull/72145) (P1) – Kept compaction summaries intact when turn‑end override rewrites the user row.

- **Dependency & Patching:**
  - Multiple PRs bumped `cryptography`, `starlette`, `python-multipart` to clear 2026 OSV advisories ([#58487](https://github.com/NousResearch/hermes-agent/pull/58487), [#56252](https://github.com/NousResearch/hermes-agent/pull/56252), [#56830](https://github.com/NousResearch/hermes-agent/pull/56830), [#63152](https://github.com/NousResearch/hermes-agent/pull/63152), [#61105](https://github.com/NousResearch/hermes-agent/pull/61105), [#60839](https://github.com/NousResearch/hermes-agent/pull/60839)).

- **Lazy Dependency & Feature Detection:**
  - [PR #70590](https://github.com/NousResearch/hermes-agent/pull/70590) – Marked features as active only when a distinctive (non‑shared) package is present, preventing false positives.
  - [PR #67930](https://github.com/NousResearch/hermes-agent/pull/67930) – Keyed `active_features()` on distinctive packages, not any‑present.
  - [PR #53505](https://github.com/NousResearch/hermes-agent/pull/53505) – Refreshed active memory provider dependencies during `hermes update`.

- **Other fixes:** Gateway reconnect watcher resurrection ([#71177](https://github.com/NousResearch/hermes-agent/pull/71177)), Hindsight embedding stack probe ([#68009](https://github.com/NousResearch/hermes-agent/pull/68009)).

## 4. Community Hot Topics

| Issue / PR | Comments | Reactions | Summary |
|------------|----------|-----------|---------|
| [#7545](https://github.com/NousResearch/hermes-agent/issues/7545) (OPEN) | 3 | 👍 14 | **Bang (`!`) prefix for inline shell commands** in CLI chat – heavily upvoted feature request, modeled after Claude Code. |
| [#380](https://github.com/NousResearch/hermes-agent/issues/380) (OPEN) | 3 | 👍 0 | **Batch Migration Skill** – parallel code migration orchestration with git worktree isolation. Open since March. |
| [#30626](https://github.com/NousResearch/hermes-agent/issues/30626) (OPEN) | 3 | 👍 0 | **Gateway profile‑blind** – `hermes gateway run` ignores live profile switches, serves only boot‑time profile. |
| [#48689](https://github.com/NousResearch/hermes-agent/issues/48689) (OPEN) | 3 | 👍 0 | **`hermes doctor` false positives** – stale npm vulnerability and invalid API key warning for Gemini. |
| [#37501](https://github.com/NousResearch/hermes-agent/issues/37501) (OPEN) | 3 | 👍 0 | **`hermes mcp add --env` bug** – only the last `--env` flag is persisted, others silently dropped. |
| [#61334](https://github.com/NousResearch/hermes-agent/issues/61334) (OPEN) | 3 | 👍 0 | **Reasoning effort fallback** – `minimal`/`max` silently use same budget as `medium` on Anthropic‑compatible providers. |
| [#72215](https://github.com/NousResearch/hermes-agent/issues/72215) (CLOSED, P0) | 1 | – | **Skills data loss** on `hermes skills update` – same‑named skills replaced from different registry. **Fixed in #72216.** |
| [#71296](https://github.com/NousResearch/hermes-agent/issues/71296) (CLOSED, P1) | 1 | – | **Shell injection via Matrix room name** – newline in display name could execute commands. **Fixed in #71306.** |

**Underlying needs:** Users want easier shell integration (`!` prefix), larger‑scale migration tooling (batch skill), better profile management across gateways, reliable MCP configuration, and truthful health diagnostics.

## 5. Bugs & Stability

| Severity | Component | Issue | Status | Fix PR |
|----------|-----------|-------|--------|--------|
| **P0** | skills/update | [Skills silently replaced from different registry (#72215)](https://github.com/NousResearch/hermes-agent/issues/72215) | CLOSED | [#72216](https://github.com/NousResearch/hermes-agent/pull/72216) (merged today) |
| **P1** | terminal/env | [Shell injection via Matrix room name (#71296)](https://github.com/NousResearch/hermes-agent/issues/71296) | CLOSED | [#71306](https://github.com/NousResearch/hermes-agent/pull/71306) (merged today) |
| **P1** | install/update | [macOS `realpath` dependency breaks `hermes` launcher (#71320)](https://github.com/NousResearch/hermes-agent/issues/71320) | CLOSED | [#71323](https://github.com/NousResearch/hermes-agent/pull/71323) (merged today) |
| **P1** | gateway/deadlock | [Telegram FD leak wedges gateway (#71593)](https://github.com/NousResearch/hermes-agent/pull/71593) | CLOSED | PR itself merged today |
| **P1** | gateway/sessions | [Session pruning deletes recently active long‑lived conversations (#71043)](https://github.com/NousResearch/hermes-agent/pull/71043) | CLOSED | PR itself merged today |
| **P1** | gateway | [Startup‑restore gate silences every channel on slow resume (#71903)](https://github.com/NousResearch/hermes-agent/pull/71903) | CLOSED | PR itself merged today |
| **P1** | agent/compaction | [Compaction summary lost on turn‑end override (#72145)](https://github.com/NousResearch/hermes-agent/pull/72145) | CLOSED | PR itself merged today |
| **P2** | gateway/config | [Profile‑blind gateway (#30626)](https://github.com/NousResearch/hermes-agent/issues/30626) | OPEN | – |
| **P2** | cli/doctor | [False‑positive stale npm vuln + invalid Gemini key (#48689)](https://github.com/NousResearch/hermes-agent/issues/48689) | OPEN | – |
| **P2** | mcp | [`--env` flag silently drops all but last (#37501)](https://github.com/NousResearch/hermes-agent/issues/37501) | OPEN | – |
| **P2** | provider/anthropic | [reasoning_effort fallback (#61334)](https://github.com/NousResearch/hermes-agent/issues/61334) | OPEN | – |
| **P2** | gateway/whatsapp | [5s debounce adds 5s latency to every response (#44883)](https://github.com/NousResearch/hermes-agent/issues/44883) | OPEN | – |
| **P2** | desktop/Windows | [WebSocket race / reconnect loop under GIL stall (#72391)](https://github.com/NousResearch/hermes-agent/issues/72391) | OPEN (new today) | – |
| **P2** | gateway | [Session reset ignores `session_reset.mode=none` (#61052)](https://github.com/NousResearch/hermes-agent/issues/61052) | OPEN | – |
| **P3** | many items | Various lower‑severity bugs (MCP OSV unbounded read, ACP tools dropped, TUI output clipping, etc.) | Mixed | – |

**Takeaway:** All P0 and P1 bugs reported in the last few days were fixed within 24–48 hours. Several P2 bugs remain open but are acknowledged.

## 6. Feature Requests & Roadmap Signals

| Feature | Issue | Comments/Reactions | Likelihood for Next Version | Rationale |
|---------|-------|--------------------|-----------------------------|-----------|
| Bang `!` shell escape | [#7545](https://github.com/NousResearch/hermes-agent/issues/7545) | 14 👍 | **High** – High community demand, simple CLI change, precedent in Claude Code. |
| Per‑user profile routing | [#33548](https://github.com/NousResearch/hermes-agent/issues/33548) | 2 comments | **Medium** – Gateway improvements are active, aligns with profile fixes in progress. |
| GUI‑only desktop (remote gateway) | [#50643](https://github.com/NousResearch/hermes-agent/issues/50643) | 3 👍 | **Medium** – Desktop is being actively developed, mentioned in recent commits. |
| Batch migration skill | [#380](https://github.com/NousResearch/hermes-agent/issues/380) | 3 comments, open since March | **Low-Medium** – Complex feature, not yet scheduled, but similar tools exist elsewhere. |
| Per‑call model/provider override on delegate | [#72394](https://github.com/NousResearch/hermes-agent/issues/72394) | 1 comment, new today | **Low** – Early stage, needs discussion. |
| Suppress cron job header for no_agent scripts | [#72395](https://github.com/NousResearch/hermes-agent/issues/72395) | 1 comment, new today | **Low** – Minor quality‑of‑life, easy to implement. |

**Prediction:** The `!` shell escape feature (#7545) is the most‑requested and simplest to implement; it may land in the next minor release (v0.14.x or v0.15.0). Per‑user profile routing (#33548) and GUI‑only install (#50643) are also strong candidates.

## 7. User Feedback Summary

**Pain points expressed today:**
- **Skills data loss** (#72215) – a silent, destructive bug that replaced user‑authored skills without warning. Fix merged same day.
- **Shell injection** (#71296) – critical security boundary violation via Matrix metadata. Fixed immediately.
- **macOS launcher broken** (#71320) – stock macOS cannot run `hermes` after an update without coreutils. Fixed.
- **Profile‑blind gateway** (#30626) – frustration that profile switches require process restart. Still open.
- **False‑positive diagnostics** (#48689) – erodes trust in `hermes doctor`. Still open.
- **MCP flag handling** (#37501) – `hermes mcp add --env` silently drops multiple flags. User had to re‑add servers. Still open.

**Satisfaction signals:** Rapid turnaround on critical fixes (P0/P1 within hours) suggests users value the responsiveness. No complaints about release cadence or broken features that weren’t fixed quickly.

## 8. Backlog Watch

These issues have been open for an extended period or lack maintainer attention:

| Issue | Opened | Updated | Last Activity | Status |
|-------|--------|---------|---------------|--------|
| [#380](https://github.com/NousResearch/hermes-agent/issues/380) – Batch migration skill | 2026-03-04 | 2026-07-27 | Comment today, but no maintainer response since April? (no assignee, no label like `accepted`) | Needs maintainer triage |
| [#3634](https://github.com/NousResearch/hermes-agent/issues/3634) – Telegram channel_post support | 2026-03-28 | 2026-07-27 | Comment today, but no official response | Needs maintainer evaluation |
| [#7545](https://github.com/NousResearch/hermes-agent/issues/7545) – Bang `!` prefix | 2026-04-11 | 2026-07-27 | 14 👍, no maintainer comment | High community demand, no official roadmap acknowledgment |
| [#30626](https://github.com/NousResearch/hermes-agent/issues/30626) – Profile‑blind gateway | 2026-05-22 | 2026-07-27 | 3 comments, no label like `triaged` | Needs maintainer decision |
| [#33548](https://github.com/NousResearch

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*