# OpenClaw Ecosystem Digest 2026-06-21

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-21 03:43 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-21

## 1. Today’s Overview

The project experienced very high activity in the last 24 hours, with 500 issues and 500 pull requests updated, and one new release (`v2026.6.9`). The release brings richer Telegram message delivery, but the majority of attention remains on critical bug reports and regressions. 34 PRs were merged or closed, indicating ongoing remediation, yet the volume of open issues (481) and open PRs (466) reflects significant stability and reliability challenges. The community is deeply engaged, with several high-severity issues gathering multiple comments and reactions.

## 2. Releases

**v2026.6.9** ([release link](https://github.com/openclaw/openclaw/releases/tag/v2026.6.9))

- **Richer Telegram delivery**: Messages now include rich HTML, preserve rich markdown and sticker paths, render progress drafts and command output more faithfully, normalize HTML tables safely, and keep mentions and spooled handlers on the correct delivery path. (#93286, #93164, #9…)
- No breaking changes or migration notes are documented in the provided data.

## 3. Project Progress

Out of 34 merged/closed PRs in the last 24h, two notable ones are visible in the top-30 list:

- **#68936** [CLOSED] – *Autofix: add PR review autofix pipeline + Windows daemon* – adds an automated review-comment fix pipeline and a Windows background daemon to supervise the OpenClaw gateway.
- **#84140** [CLOSED] – *chore: format oxfmt-touched files* – applies consistent formatting across the codebase.

Several other PRs are in advanced review stages, ready for maintainer look or in re-review loop:

- **#84450** – *Doctor: expose config audit scrub findings* – structured health findings for historical config scrubs.
- **#95467** – *fix(sessions): keep bound channel identity across non-delivery turns* – P1 fix actively grinding.
- **#94828** – *feat(cli): add skills uninstall command* – new functionality for skill lifecycle management.

## 4. Community Hot Topics

The most active issues (by comment count and reactions) highlight deep reliability concerns:

| Issue | Title | Comments | 👍 | Link |
|-------|-------|----------|---|------|
| #88838 | Track core session/transcript SQLite migration via accessor seam | 31 | 1 | [Issue #88838](https://github.com/openclaw/openclaw/issues/88838) |
| #88312 | [Regression] Codex app-server turn-completion stall | 16 | 4 | [Issue #88312](https://github.com/openclaw/openclaw/issues/88312) |
| #91588 | Critical: Gateway Memory Leak (350MB → 15.5GB, OOM crashes) | 13 | 1 | [Issue #91588](https://github.com/openclaw/openclaw/issues/91588) |
| #85333 | `doctor --fix` 4–5x slower on 2026.5.20 | 13 | 1 | [Issue #85333](https://github.com/openclaw/openclaw/issues/85333) |
| #91363 | Isolated cron fails with “LLM request failed” on model-call-started | 6 | 4 | [Issue #91363](https://github.com/openclaw/openclaw/issues/91363) |

**Underlying needs**: Users are struggling with session reliability (migration, stalls), performance regressions, and infrastructure-level resource leaks. The migration to SQLite (#88838) is a major architectural change, and its incremental approach is being closely tracked. The codex turn-completion stall (#88312) and gateway memory leak (#91588) are breaking critical use cases.

## 5. Bugs & Stability

Several critical bugs and regressions were reported or updated in the last 24h, ranked by severity:

| Severity | Issue | Title | Impact | Fix PR exists? |
|----------|-------|-------|--------|----------------|
| **P0** | #91588 | Gateway memory leak (RSS 350MB → 15.5GB, OOM) | Crash-loop, session-state, message-loss | No linked fix PR |
| **P1** | #88312 | Codex turn-completion stall regression | Session-state, message-loss | Mentioned prior fix #85107 but regression persists |
| **P1** | #85333 | `doctor --fix` 4–5x slower | Session-state, crash-loop | No linked fix PR |
| **P1** | #92201 | Invalid thinking signatures on replay (Anthropic) | Session-state, message-loss, auth-provider | Possibly unresolved |
| **P1** | #86519 | Duplicate Telegram replies (2–10x) | Session-state, message-loss | Reduced but not fully fixed |
| **P1** | #90325 | Matrix channel dispatch broken | Message-loss | No linked fix PR |
| **P1** | #91363 | Isolated cron fails with model-call timeout | Session-state, message-loss, auth-provider | No linked fix PR |
| **P1** | #92460 | Isolated cron announcer drops delivery.channel | Message-loss | Linked fix PR #95352 |
| **P1** | #92415 | `/model` switch never refreshes `this.model` snapshot | Session-state, data-loss, auth-provider | Linked fix PR |
| **P1** | #90639 | Compaction safeguard mode grows to context ceiling | Session-state, message-loss | No linked fix PR |
| **P1** | #90082 | active-memory circuit breaker too aggressive | Session-state, auth-provider | No linked fix PR |
| **P1** | #91009 | Codex PreToolUse hook relay CPU-bound stalls | Crash-loop | Linked fix PR |
| **P1** | #92043 | Compaction timeout (180s) wall clock, no partial reuse | Session-state, crash-loop, message-loss | Linked fix PR |

Many of these still await maintainer review or product decision. The high number of P1 regressions suggests a rigorous testing/release process is needed.

## 6. Feature Requests & Roadmap Signals

The following feature requests reflect community demand and are likely to be prioritized:

- **#90354** – *Add bounded/validated append semantics for pre-compaction memory flush* – guardrails for memory writes (P2, linked PR open).
- **#90916** – *Topic-session families for one assistant across multiple named context lanes* – multi-topic chat with isolated context (P2, linked PR open).
- **#14785** – *Reduce tool schema token overhead (~3,500 tok/session)* – load-on-demand schemas (P2, open since February).
- **#86023** – *Codex long-running sessions should use semantic thread/bootstrap cache ownership* – performance improvement for long sessions (P2, open since May 24).
- **#91455** – *Documentation update for Kubernetes* – better deployment instructions (P3, linked PR open).

From pull requests, the following new features are close to landing:
- **#94828** – `openclaw skills uninstall <slug>` command.
- **#95322** – Persistent session preferences (e.g., `/think --persist`).

Prediction: next minor release will include the skills uninstall command, persistent preferences, and likely the bounded memory flush feature (#90354).

## 7. User Feedback Summary

Common pain points reported in the last 24 hours:

- **Performance regressions**: `doctor --fix` slowdown, gateway memory leak, interactive session perceived slowness.
- **Message delivery failures**: duplicate replies on Telegram, broken Matrix channel, isolated cron not reaching users, delivery recovery failing after restart.
- **Data loss**: messages lost when recovery starts before channel transport is ready (#91212), session compaction growing beyond ceiling (#90639).
- **Incorrect behavior**: subagent completion delivered to user as raw output instead of summary (#90840), internal reasoning leaked to users (#91804), preseeded boot files causing auto-complete (#91931).
- **Configuration issues**: plugins not recognized by config validate (#92884), NO_PROXY ignored (#93807), hardcoded stderr path (#90711).

Satisfaction signals are sparse; the overall tone is frustrated, with several users labeling issues as “critical” and “beta release blocker.” The community is actively reproducing and providing detailed error contexts, which is helping maintainers understand the root causes.

## 8. Backlog Watch

Several important issues and PRs have been open for weeks and still require maintainer decision or review:

| Item | Created | Status | Link |
|------|---------|--------|------|
| **#85333** – `doctor --fix` 4–5x slower (P1) | 2026-05-22 | Needs maintainer review, product decision | [Issue](https://github.com/openclaw/openclaw/issues/85333) |
| **#85334** – `doctor --fix` auto-injects bundled plugin path (P2) | 2026-05-22 | Needs maintainer review, linked PR open | [Issue](https://github.com/openclaw/openclaw/issues/85334) |
| **#84583

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem

*Prepared: 2026-06-21*

---

## 1. Ecosystem Overview

The personal AI assistant / agent open-source landscape is experiencing a surge in production adoption, driven by two prominent reference implementations—OpenClaw and Hermes Agent—both hosting hundreds of daily contributions. The community is grappling with common maturation pains: session reliability, memory and token efficiency, and multi-platform delivery consistency. While both projects share core goals of enabling autonomous, conversational AI agents, they diverge in architectural philosophy (centralized core reference vs. modular, performance-optimized agent) and community maturity. The ecosystem remains highly dynamic, with a clear signal that users expect production-grade reliability from agent frameworks they deploy in real-world workflows.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| Issues updated (last 24h) | 500 | 50 |
| PRs updated (last 24h) | 500 | 50 |
| PRs merged/closed (last 24h) | 34 | 24 |
| New release today? | ✅ v2026.6.9 | ❌ None |
| **Health Score** (1–10) | **4** – high regression count, memory leak (P0), many P1 bugs open | **7** – most P1 bugs have fix PRs, active maintainer response, lower regression noise |
| Open Issues (approximate) | 481 (overall backlog) | Not reported (likely lower) |
| Community engagement signal | High frustration but detailed reproduction; 34 PRs merged | Active contribution (24 PRs merged), users building monitoring dashboards |

*Interpretation: OpenClaw has a significantly larger issue/PR surface but also more instability. Hermes Agent is in a healthier state with focused, fast resolution cycles.*

---

## 3. OpenClaw’s Position

**Advantages vs. peers:**
- **Core reference implementation** – OpenClaw is the canonical open-source agent; its architectural decisions (e.g., SQLite-based session migration, explicit `doctor` diagnostics, subagent lifecycle) set ecosystem direction.
- **Rich Telegram delivery** – v2026.6.9 brings rich HTML, markdown, sticker paths, and spooled handler preservation—a level of platform integration not yet matched by Hermes Agent.
- **Larger community surface** – 500 issues/PRs updated daily indicates a broad install base and intensive field testing (albeit with quality trade-offs).

**Technical approach differences:**
- OpenClaw employs an **accessor seam** for SQLite migration (#88838) and explicit **compaction safeguards**; Hermes Agent uses a more lightweight summary-rotation model.
- OpenClaw’s `doctor` subsystem is a first-class diagnostic tool; Hermes relies on external monitoring (user-built dashboards).
- OpenClaw emphasizes **skill lifecycle** (uninstall command #94828) and **persistent preferences** (#95322); Hermes focuses on token overhead reduction and plugin routing hooks.

**Community size comparison:**
- OpenClaw’s daily activity volume (500 vs 50) suggests a community roughly **10× larger** or at least with a higher churn rate. However, the proportion of critical issues is also higher. Hermes’ per-PR resolution speed is faster (most P1s have linked fix PRs), indicating a tighter maintainer feedback loop.

---

## 4. Shared Technical Focus Areas

Both projects are actively developing in overlapping domains, reflecting common requirements across the ecosystem:

| Focus Area | OpenClaw (issue/PR) | Hermes Agent (issue/PR) |
|------------|----------------------|-------------------------|
| **Token overhead reduction** | #14785 – ~3,500 tok/session load-on-demand schemas | #6839, #4379 – 73% fixed overhead, two-pass injection |
| **Session/data loss prevention** | #88838 (SQLite migration), #90639 (compaction ceiling), #91212 (delivery recovery) | #33618 (/goal state lost), #49925 (transcript loss on rotation) |
| **Multi-platform delivery reliability** | #86519 (Telegram dupes), #90325 (Matrix broken), #91588 (gateway memory leak) | #49930 (Telegram fd leak), #49831 (WhatsApp path bug), #47804 (Feishu env override) |
| **Memory/resource leaks** | #91588 (gateway OOM crash) | #49930 (CLOSE_WAIT), #47826 (Electron zombie timer) |
| **Performance regressions** | #85333 (doctor --fix 4-5x slower) | #49920 (desktop hang after update) |
| **Lazy/on-demand loading** | #14785 (tool schema) | #6839 (tool schema) |
| **Cross-platform session sharing** | Not explicitly requested | #4335 (CLI ↔ Telegram) |
| **Documentation & onboarding** | #91455 (Kubernetes docs) | 12 docs PRs merged, Windows install guide |

*Key insight: Token waste and session reliability are the #1 shared pain points, implying the ecosystem needs a standardized, efficient context management strategy.*

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Target user** | Advanced developers, self-hosters, infrastructure teams | Broader consumer base, multi-platform users, enterprise pilot users |
| **Primary use case** | Autonomous agent with complex session lifecycle, subagent orchestration | Lightweight, fast agent for personal assistants, chat, coding |
| **Architecture** | Monolithic core with explicit subsystems (doctor, codex, skills) | Modular adapter model with heavy emphasis on token optimization |
| **Platform support** | Telegram-first, Matrix, cron; Windows daemon in preview | Telegram, WhatsApp, Feishu, iMessage, Desktop Electron, MCP, VSCode |
| **Release cadence** | Frequent (daily patch releases) but with regression risk | Slower (minor releases), more stable merges |
| **Diagnostic tooling** | Built-in `doctor` (audit, scrub, fix) | Community-driven monitoring dashboards (#4379) |
| **Community engagement style** | High-volume issue reporting, strong reproduction detail, frustrated but persistent | Proactive feature requests with analysis, documentation contributions, faster maintainer response |

**Strategic implication:** OpenClaw is the **ecosystem reference**—it breaks new ground but pays the price in stability. Hermes Agent is the **polished implementer**—adopting proven patterns and optimizing for end-user experience.

---

## 6. Community Momentum & Maturity

**Tier 1 – High iteration, high instability (OpenClaw)**
- Daily release cycle (v2026.6.9 today) reflects rapid feature development, but the P0 memory leak (#91588) and multiple P1 regressions indicate the project is **trading stability for speed**.
- The community is mature in debugging (detailed logs, reproduction steps), but trust is eroded by repeated regressions.
- **Recommendation:** A stabilization sprint (e.g., “bug bash week”) would improve health score significantly.

**Tier 2 – Steady iteration, moderate stability (Hermes Agent)**
- No release today, but 24 PRs merged with clear P1 patches. Documentation and bug fixing dominate over new features.
- Token overhead analysis (#4379, #6839) shows community proactively driving architectural improvements.
- **Recommendation:** Maintain current rate; next minor release (0.18.0) should include lazy tool loading and compression reliability.

**Both projects** show strong contributor sustainment (34 + 24 PRs merged/day), but Hermes Agent demonstrates better bug-to-fix cycle (most P1s have linked PRs). The wider ecosystem would benefit from cross-project collaboration on shared standards (e.g., session migration, token-efficient schema injection).

---

## 7. Trend Signals

From community feedback and issue patterns, the following industry trends are emerging:

- **Token economy is the new latency metric** – Both projects’ most upvoted requests (#6839: 26 comments, #14785: open since Feb) indicate that **token waste** is the primary source of user frustration. AI agent developers must prioritize schema compression, lazy injection, and model call batching to remain competitive.

- **Session continuity as a feature, not a bug fix** – Users expect agents to persist goals, assistant messages, and cross-session context without loss (#33618, #88312). The ecosystem is moving toward **accessor-pattern session stores** (OpenClaw’s SQLite seam) and **semantic cache ownership** (#86023) as first-class design goals.

- **Multi-platform reliability trumps feature count** – Duplicate replies, broken channels, and delivery deadlocks (e.g., #86519, #90325, #49831) are the top complaints. Developers should invest in **adapter integration tests** and **keepalive/heartbeat mechanics** before adding new platforms.

- **Compression is a double-edged sword** – Both projects see issues where compression destroys state (#49925, #90639). The trend is toward **partial reuse, time-bounded compaction** (OpenClaw #92043) and **bounded append semantics** (#90354) rather than wholesale rotation.

- **Developer UX matters** – `doctor --fix` slowdowns (#85333), console flashing on Windows (#49931), and desktop update hangs (#49920) erode trust. **Diagnostic tooling** (OpenClaw’s doctor) and **smooth onboarding** (Hermes’ docs PRs) are emerging as competitive differentiators.

- **Agent autonomy requires explicit config** – Users want control over skill lifecycle (`skills uninstall`), persistent preferences (`/think --persist`), and plugin routing hooks (#41190). The ecosystem is converging on **declarative, user-visible configuration** over implicit behavior.

**Value for AI agent developers:**
- Adopt **lazy tool schema loading** and **context compression with recovery** as non-negotiable architectural features.
- Invest in **cross-platform session continuity** and **diagnostic tools** (like OpenClaw’s doctor) to build user trust.
- Monitor token consumption dashboards (as in #4379) to identify waste before users report it.
- Prioritize **stability sprints** after feature releases to avoid regression fatigue.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-21

## 1. Today’s Overview

The project is in a **high-activity phase**, with 50 issues and 50 PRs updated in the last 24 hours. The community remains focused on **performance optimisation** (token overhead, lazy tool loading), **context compression reliability** (session rotation bugs, lost goals/assistant messages), and **platform‑specific bugs** (WhatsApp, Feishu, Telegram, Windows). No new release was cut today; development effort is concentrated on bug fixes and documentation improvements. The maintainer team merged/closed 24 PRs, including several P1 stability patches for compression and gateway hygiene.

## 2. Releases

**None.** No new version was published on 2026-06-21. The last known version tag remains `v0.17.0` (referenced in an issue comment).

## 3. Project Progress

24 PRs were merged or closed today. Key changes:

- **Compression** — [PR #49928](https://github.com/NousResearch/hermes-agent/pull/49928) (P1) protects the summary call from mid‑flight interrupts; [PR #49925](https://github.com/NousResearch/hermes-agent/pull/49925) (P1) preserves the full transcript when hygiene auto‑compress cannot rotate the session.
- **Security** — [PR #49922](https://github.com/NousResearch/hermes-agent/pull/49922) (P1) stops cross‑session `HERMES_SESSION_*` environment variable leaks into subprocesses.
- **Platform reliability** — [PR #49930](https://github.com/NousResearch/hermes-agent/pull/49930) (P1) applies keepalive limits and TCP keepalive to the Telegram adapter, preventing `CLOSE_WAIT` file descriptor leaks.
- **Windows UX** — [PR #49931](https://github.com/NousResearch/hermes-agent/pull/49931) (P2) bypasses the Git Bash wrapper to eliminate console flashing on Windows.
- **Configuration** — [PR #49921](https://github.com/NousResearch/hermes-agent/pull/49921) (P2) bridges Feishu group rules from `config.yaml` and adds regression tests.
- **Think/Reasoning** — [PR #49143](https://github.com/NousResearch/hermes-agent/pull/49143) (P2) enables the `thinking` parameter for Kimi `/coding` endpoints.
- **Docs** — 12 documentation‑only PRs were merged, covering Windows install, contribution guidelines, skill docs, and antivirus false‑positive guidance (e.g., [PR #49661](https://github.com/NousResearch/hermes-agent/pull/49661), [PR #49444](https://github.com/NousResearch/hermes-agent/pull/49444), [PR #48569](https://github.com/NousResearch/hermes-agent/pull/48569)).

## 4. Community Hot Topics

The most actively discussed issues (by comment count) reveal three major pain points:

- **Token overhead** — [Issue #6839](https://github.com/NousResearch/hermes-agent/issues/6839) (26 comments, 13 👍) proposes two‑pass tool injection to reduce the ~3.5K‑5K tokens wasted on full schema injection per call. A companion analysis [Issue #4379](https://github.com/NousResearch/hermes-agent/issues/4379) (15 comments) shows **73% of every API call is fixed overhead** (~13.9K tokens). Users are clearly seeking a dramatic reduction in token waste.

- **Context compression data loss** — [Issue #33618](https://github.com/NousResearch/hermes-agent/issues/33618) (5 comments) and duplicates (#33907, #48956, #45059) report that persistent `/goal` state and assistant messages vanish after session rotation. The issue is well‑understood (state not migrated), and several fix PRs are now merged but may not cover all edge cases.

- **Plugin routing** — [Issue #41190](https://github.com/NousResearch/hermes-agent/issues/41190) (5 comments, 1 👍) calls for a unified plugin‑accessible hook to override provider/model per turn, reflecting fragmentation in routing logic.

## 5. Bugs & Stability

**P1 bugs identified today (all with open or merged fix PRs):**

| Bug | Component | Impact | Fix Status |
|-----|-----------|--------|------------|
| [Telegram CLOSE_WAIT fd leak](https://github.com/NousResearch/hermes-agent/issues/49930) | Telegram adapter | Long‑running gateway connections exhaust file descriptors | PR #49930 open |
| [Compression summary interrupt](https://github.com/NousResearch/hermes-agent/issues/23975) (related) | Compression | Degraded summaries after mid‑flight interrupt | PR #49928 open |
| [Gateway hygiene transcript loss](https://github.com/NousResearch/hermes-agent/issues/21301) (related) | Gateway | Auto‑compress destroys transcript when rotation fails | PR #49925 open |
| [Cross‑session env leak](https://github.com/NousResearch/hermes-agent/issues/49922) | Terminal subprocess | Session keys leak to other concurrent sessions | PR #49922 open |

**P2/P3 bugs reported today:**

- [Photon iMessage streaming white square](https://github.com/NousResearch/hermes-agent/issues/49793) — cursor artifact in outbound messages.
- [WhatsApp bridge path off‑by‑one](https://github.com/NousResearch/hermes-agent/issues/49831) — fatal error on editable installs.
- [MCP double‑encoded JSON errors](https://github.com/NousResearch/hermes-agent/issues/47867) — actionable errors hidden from model.
- [Desktop Electron `Object has been destroyed` crash](https://github.com/NousResearch/hermes-agent/issues/47826) — zombie timer after window closed.
- [macOS bootstrap fails with spaces in path](https://github.com/NousResearch/hermes-agent/issues/47822) — `HERMES_HOME` with spaces breaks venv entrypoint.
- [Feishu forced enabled by env vars](https://github.com/NousResearch/hermes-agent/issues/47804) — `config.yaml` disabled setting ignored.
- [TTS edge broken on Docker after v2026.6.5](https://github.com/NousResearch/hermes-agent/issues/49747) — lazy install fails due to env var set to 1.
- [Desktop hangs in CONNECTING after update](https://github.com/NousResearch/hermes-agent/issues/49920) — dashboard build fails due to `NODE_ENV=production` stripping devDependencies.
- [NVIDIA NIM model truncation at 50](https://github.com/NousResearch/hermes-agent/issues/49911) — Nemotron, GLM models hidden from dropdown.

## 6. Feature Requests & Roadmap Signals

The community continues to request features that reduce cost and improve flexibility:

| Feature | Issue | Likely Priority |
|---------|-------|-----------------|
| **Lazy tool schema loading** | [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) | High – token waste is a top complaint |
| **Cross‑platform session sharing** (CLI ↔ Telegram) | [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) | Medium – requested by multi‑platform users |
| **i18n/Localization** | [#37543](https://github.com/NousResearch/hermes-agent/issues/37543) | Medium – Chinese community actively contributing |
| **Unified plugin route selector** | [#41190](https://github.com/NousResearch/hermes-agent/issues/41190) | Medium – reduces routing fragmentation |
| **Python 3.14 support** | [#48723](https://github.com/NousResearch/hermes-agent/issues/48723) | Low/Medium – current pin `<3.14` will block Homebrew users |

Given the volume of token‑related issues, the next version (likely 0.18.0) will probably include a two‑pass tool injection mechanism and improved compression reliability. I18n and cross‑platform session sharing may appear in subsequent releases.

## 7. User Feedback Summary

- **Satisfaction**: The community is actively contributing – 24 PRs merged today, and users are building monitoring dashboards ([#4379](https://github.com/NousResearch/hermes-agent/issues/4379)) and detailed bug reports. The project is clearly valued for its extensibility and multi‑platform support.
- **Pain Points**:
  - **Token waste** – “16K tokens per ‘who u?’” ([#13983](https://github.com/NousResearch/hermes-agent/issues/13983)) is a recurring frustration. Users want immediate reductions.
  - **Context compression fragility** – Users frequently lose `/goal` state, assistant messages, and see orphan sessions. Even after fixes, duplicates keep appearing.
  - **Platform configuration quirks** – Feishu env‑var override, WhatsApp path errors, desktop update hangs – these erode trust in a polished consumer experience.
- **Wishlist**: Better model enumeration for local providers ([#30202](https://github.com/NousResearch/hermes-agent/issues/30202)), MCP workflow documentation ([#48325](https://github.com/NousResearch/hermes-agent/pull/48325)), and antivirus false‑positive guidance ([#48439](https://github.com/NousResearch/hermes-agent/pull/48439)).

## 8. Backlog Watch

Several **high‑importance issues** have been open for weeks without a maintainer response or fix:

- **[#6839](https://github.com/NousResearch/hermes-agent/issues/6839) – Lazy tool schema loading** (26 comments, opened Apr 9). The most‑discussed feature request. No assignee or milestone.
- **[#4379](https://github.com/NousResearch/hermes-agent/issues/4379) – Token overhead analysis** (15 comments, opened Apr 1). The user provided a detailed dashboard – no official comment from maintainers.
- **[#4335](https://github.com/NousResearch/hermes-agent/issues/4335) – Cross‑platform session sharing** (3 comments, opened Mar 31). Stale, with no label update or roadmap signal.
- **[#13983](https://github.com/NousResearch/hermes-agent/issues/13983) – 16K token consumption** (5 comments, opened Apr 22). The user is clearly frustrated; no maintainer response.
- **[#49920](https://github.com/NousResearch/hermes-agent/issues/49920) – Desktop hang after update** (opened today, 1 comment). A P2 bug that may affect many Windows users – immediate triage recommended.

**Recommendation**: The maintainer team should explicitly label these with a roadmap milestone or at least a comment acknowledging the issue, especially #6839 and #4379 which dominate community discussion.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*