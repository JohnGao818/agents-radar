# OpenClaw Ecosystem Digest 2026-06-17

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-17 03:40 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-06-17

## 1. Today's Overview
OpenClaw continues to show extremely high community activity with **500 issues** and **500 PRs** updated in the last 24 hours. Of these, **466 issues remain open/active**, while **91 PRs were merged or closed** today, reflecting a healthy but heavily loaded development pipeline. A new release **v2026.6.8** landed, bringing improvements to Telegram and WhatsApp channel delivery. The project is clearly under intense use and scrutiny, with many stability and message‑delivery bugs being reported and fixed in parallel.

## 2. Releases
**New release:** `v2026.6.8` – [openclaw 2026.6.8](https://github.com/openclaw/openclaw/releases/tag/v2026.6.8)

### 2026.6.8 Highlights
- **Richer channel delivery:** Telegram and WhatsApp are less brittle.
  - Telegram now renders structured text with tables, lists, expandable blockquotes, preserved intentional line breaks, and CLI‑backed replies.
  - WhatsApp now honors configured ACP bindings.
  - Referenced issues: #92679, #931 (partial release notes shown).

No breaking changes or migration notes were published with this release.

## 3. Project Progress
Today **91 PRs were merged or closed**. Notable closed/merged PRs from the top 30 list include:

| PR | Description | Labels |
|----|-------------|--------|
| [#68936](https://github.com/openclaw/openclaw/pull/68936) | Autofix: add PR review autofix pipeline + Windows daemon | scripts, size: XL |
| [#70630](https://github.com/openclaw/openclaw/pull/70630) | fix(telegram): keep no‑visible direct turns silent | channel: telegram, size: XS, P2 |
| [#93301](https://github.com/openclaw/openclaw/pull/93301) | fix(skill‑workshop): add Global/Selected‑agent scope toggle to Control UI | app: web‑ui, gateway, size: L, P2 |
| [#93821](https://github.com/openclaw/openclaw/pull/93821) | fix(qmd): strip mcporter daemon startup logs from stdout before JSON.parse | extensions: memory‑core, size: XS, P1 |
| [#93822](https://github.com/openclaw/openclaw/pull/93822) | fix(slack): forward identity (username/icon) to chat.update for edited messages | channel: slack, size: XS, P2 |
| [#93890](https://github.com/openclaw/openclaw/pull/93890) | feat(telegram): export sender isBot field to agent context | channel: telegram, size: XS |
| [#93896](https://github.com/openclaw/openclaw/pull/93896) | docs(gateway): add agent runtime boundary documentation | docs, gateway, size: XS |

Additionally, several high‑priority PRs remain open but show active work (e.g., #93866, #93840, #93848, #93832). The overall pace suggests steady progress on both urgent fixes and feature work.

## 4. Community Hot Topics
Most active issues and PRs by comment count and reactions:

| Issue | Title | Comments | 👍 | URL |
|-------|-------|----------|----|-----|
| #75 | [Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) | 109 | 79 | [openclaw/openclaw Issue #75](https://github.com/openclaw/openclaw/issues/75) |
| #44925 | [Subagent completion silently lost — no retry, no notification, no auto‑restart on timeout](https://github.com/openclaw/openclaw/issues/44925) | 19 | 1 | [openclaw/openclaw Issue #44925](https://github.com/openclaw/openclaw/issues/44925) |
| #22676 | [Signal daemon stop() race condition on SIGUSR1 restart](https://github.com/openclaw/openclaw/issues/22676) | 17 | 0 | [openclaw/openclaw Issue #22676](https://github.com/openclaw/openclaw/issues/22676) |
| #32296 | [Agent replies to previous message instead of current message (session context confusion)](https://github.com/openclaw/openclaw/issues/32296) *(closed)* | 16 | 1 | [openclaw/openclaw Issue #32296](https://github.com/openclaw/openclaw/issues/32296) |
| #58450 | [Agent can promise a later follow‑up without starting any actual follow‑up action](https://github.com/openclaw/openclaw/issues/58450) | 15 | 3 | [openclaw/openclaw Issue #58450](https://github.com/openclaw/openclaw/issues/58450) |
| #68596 | [Configurable streaming watchdog timeout threshold](https://github.com/openclaw/openclaw/issues/68596) | 14 | 8 | [openclaw/openclaw Issue #68596](https://github.com/openclaw/openclaw/issues/68596) |

**Underlying needs:** Users are demanding **reliable agent behavior** — subagent orchestration must not lose results, session context must stay aligned, and streaming must handle long‑thinking models gracefully. The high reaction count for #75 (Linux/Windows apps) shows strong desire for broader platform support, and #68596 indicates frustration with current streaming watchdog limits.

## 5. Bugs & Stability
Critical and high‑severity bugs reported or updated today:

| Issue | Severity | Impact | Summary | Fix PR? |
|-------|----------|--------|---------|---------|
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | P1 | message‑loss, session‑state | Subagent completion silently lost on timeout – no retry, no notification | label: linked‑pr‑open |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) | P1 | crash‑loop, message‑loss | Signal daemon race condition causes orphaned processes and send failures | label: linked‑pr‑open |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | P1 | session‑state, message‑loss | Coding Agent never completes (regression since 2026.4.2) | label: linked‑pr‑open |
| [#63216](https://github.com/openclaw/openclaw/issues/63216) | P1 | session‑state, message‑loss | Repeated hard resets despite high reserveTokensFloor | no linked PR |
| [#67777](https://github.com/openclaw/openclaw/issues/67777) | P1 | session‑state, message‑loss | Subagent completion delivery lost on timeout/drain/orphan prune | no linked PR |
| [#64810](https://github.com/openclaw/openclaw/issues/64810) | P1 | message‑loss | Heartbeat/system events swallow in‑progress replies in Telegram topics | label: linked‑pr‑open |
| [#65161](https://github.com/openclaw/openclaw/issues/65161) | P2 | session‑state, message‑loss | Heartbeat isolated mode: cadence stalls, mislabels exec‑events, heavy Context | no linked PR |
| [#73148](https://github.com/openclaw/openclaw/issues/73148) | P1 | message‑loss | Image tool fails with opaque error when sharp is not installed – no fallback | no linked PR |

Many of these have associated PRs (marked `linked‑pr‑open`), indicating active resolution. The cluster of P1 bugs around subagent completion and session state suggests a systemic reliability gap in the async orchestration layer.

## 6. Feature Requests & Roadmap Signals
Top feature requests from the last 24h:

| Issue | Feature | Votes | Link | Likely next version? |
|-------|---------|-------|------|----------------------|
| #75 | Linux/Windows Clawdbot Apps | 79 | [Issue #75](https://github.com/openclaw/openclaw/issues/75) | Long‑standing, help wanted – uncertain, but high demand |
| #39604 | Add `tools.web.fetch.allowPrivateNetwork` | 9 | [Issue #39604](https://github.com/openclaw/openclaw/issues/39604) | High chance – small config change, security‑controlled |
| #63829 | Per‑agent memory‑wiki vault configuration | 9 | [Issue #63829](https://github.com/openclaw/openclaw/issues/63829) | Medium – frequently requested for multi‑agent setups |
| #68596 | Configurable streaming watchdog timeout | 8 | [Issue #68596](https://github.com/openclaw/openclaw/issues/68596) | High – directly addresses user pain with long‑thinking models |
| #81061 | Pre‑routing inbound message hook (`before_route_inbound_message`) | 3 | [Issue #81061](https://github.com/openclaw/openclaw/issues/81061) | Low – complex architectural change |

**Prediction:** v2026.6.9 or v2026.7 will likely include `allowPrivateNetwork` and a configurable streaming watchdog threshold, as both are relatively targeted changes that solve well‑understood user problems. Per‑agent memory‑wiki may take more design iteration.

## 7. User Feedback Summary
Common pain points expressed across today’s issues and comments:

- **Silent failures** – Subagent completions, message deliveries, and task continuations can fail without any user‑visible error (e.g., #44925, #58450, #67777, #92460).
- **Session context confusion** – Agents reply to wrong messages, repeat previous content, or lose conversation alignment (#32296, #69118, #84383).
- **Streaming instability** – Watchdog warnings and incomplete turns force users to manually resend messages (#68596, #88657).
- **Missing platform support** – #75 (Linux/Windows apps) continues to be the most upvoted issue, showing strong demand behind macOS and iOS coverage.
- **Configuration friction** – Several reports highlight confusing or incorrect config handling: nested directories (#45765), Telegram token replacement crash (#67366), installer hang (#73814).
- **Accessibility gaps** – Screen readers announce every token during streaming (#65538).

On the positive side, users are actively deploying OpenClaw for coding agents, multi‑agent orchestration, and channel bridging (Telegram, Discord, Feishu). The high volume of reports indicates both deep engagement and urgency for stability improvements.

## 8. Backlog Watch
Long‑standing or stuck issues and PRs that require maintainer attention:

| Item | Age | Status | Summary |
|------|-----|--------|---------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | Created Jan 1, 2026 | Open, P2, help wanted | Linux/Windows apps – highest‑voted issue, no fix PR |
| [#11665](https://github.com/openclaw/openclaw/issues/11665) | Created Feb 8, 2026 | Open, P2 | Webhook hook sessions should reuse existing session for multi‑turn support |
| [#40001](https://github.com/openclaw/openclaw/issues/40001) | Created Mar 8, 2026 | Open, P1 | Write tool lacks append mode – cron sessions destroy shared files |
| [#54155](https://github.com/openclaw/openclaw/issues/54155) | Created Mar 25, 2026 | Open, P1 | Gateway memory leak 389MB → 14.7GB over 4 days – no linked fix |
| [#85651](https://github.com/openclaw/openclaw/pull/85651) | Created May 23, 2026 | Open, P1, needs proof | Context‑pressure‑aware continuation (large PR, waiting for real‑behavior proof) |

Many other issues carry labels `clawsweeper:needs-maintainer-review` or `clawsweeper:needs-product-decision`, indicating they are blocked on maintainer triage. The project would benefit from a dedicated triage cycle to unblock these items, especially those affecting reliability (e.g., #54155 memory leak, #40001 data loss).

---
*Generated from OpenClaw GitHub data for 2026-06-17. All links point to openclaw/openclaw.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Personal Assistant Open-Source Ecosystem

**Date:** 2026-06-17  
**Analyst:** Senior AI Agent Ecosystem Analyst

---

## 1. Ecosystem Overview

The open-source personal AI assistant landscape is experiencing a phase of intense maturation and scaling pressure. Both OpenClaw and Hermes Agent show high community engagement, but the character of their activity diverges significantly: OpenClaw is dealing with the scale pains of a rapidly growing user base (500 daily issues, 91 PRs merged), while Hermes Agent operates at a more controlled cadence (50 daily issues, 4 PRs merged) with deeper architectural debates. Across both projects, the dominant user demands center on **reliable task execution**, **multi-platform delivery fidelity**, and **multi-tenant isolation** for production deployments. The ecosystem is bifurcating into two tiers: high-throughput community projects absorbing broad use cases, and more architecturally focused projects serving developer and enterprise needs. Neither project has yet solved the core reliability challenges around subagent orchestration, streaming stability, and context management, suggesting these remain the key unsolved problems in the category.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues updated (24h)** | 500 | 50 |
| **Open/active issues** | 466 | ~45 |
| **PRs updated (24h)** | 500 | 50 |
| **PRs merged/closed (24h)** | 91 | 4 |
| **New releases (24h)** | v2026.6.8 | None |
| **P1/P2 critical bugs open** | 8+ | 2+ |
| **Health score** | **High churn, moderate stability risk** | **Healthy iteration, lower throughput** |

**Health assessment**: OpenClaw exhibits higher raw activity and faster fix velocity, but the volume of open P1 bugs (particularly around subagent silent failures) indicates systemic reliability gaps. Hermes Agent shows more stable hygiene with fewer critical issues, though its lower throughput may reflect a smaller community or more selective maintainer attention.

---

## 3. OpenClaw's Position

**Advantages over peers:**
- **Community scale**: 10x the daily issue/PR volume of Hermes Agent, indicating a larger user base and contributor pool.
- **Delivery breadth**: v2026.6.8 delivers structured text rendering for Telegram (tables, lists, blockquotes) and WhatsApp ACP binding – features no competitor has matched fully.
- **Fix velocity**: 91 merged PRs in 24 hours demonstrates responsive maintenance, even if many are small (XS size).
- **Long-standing demand validation**: Issue #75 (Linux/Windows apps) with 79 👍 signals untapped platform expansion potential.

**Technical approach differences:**
- OpenClaw appears more **monolithic and script-driven** (notable: "Autofix" pipeline PR with Windows daemon, mcporter daemon logs in stdout).
- Hermes Agent leans toward **modular architecture** (two-phase context management debate, per-profile git credentials, real-time voice as gateway plugin).
- OpenClaw's bug profile suggests heavier reliance on community-contributed fixes; Hermes Agent has more design-led feature PRs.

**Community size comparison:**
- OpenClaw's 500 daily updates vs. Hermes Agent's 50 suggests approximately 10x the community engagement. However, OpenClaw's open issue backlog (466) is also 10x larger, implying a less curated or more overwhelmed triage process.

---

## 4. Shared Technical Focus Areas

| Emerging Requirement | Seen In | Specific User Needs |
|---------------------|---------|---------------------|
| **Subagent orchestration reliability** | **Both** | Silent completion loss (OpenClaw #44925), no retry/notification on timeout; Hermes tool-call corruption (#6841) |
| **Telegram rendering fidelity** | **Both** | Bullet lists broken (Hermes #6388), table+bullet double render (Hermes #47048); OpenClaw v2026.6.8 addressed tables & lists but issues persist |
| **Streaming instability** | **Both** | Watchdog timeouts (OpenClaw #68596, 8👍); reasoning stream correct but final answer dumped (Hermes #47116) |
| **Multi-tenant/multi-profile isolation** | **Both** | Memory hooks bypass tenant isolation (Hermes #34352); per‑agent memory‑wiki vault config requested (OpenClaw #63829) |
| **Memory leak / resource exhaustion** | **Both** | Gateway memory leak 389MB→14.7GB (OpenClaw #54155, P1); desktop model picker hides custom providers after session (Hermes #47042, indicative of state issues) |
| **Cross-platform desktop support** | **Both** | OpenClaw #75 (Linux/Windows apps, 79👍); Hermes #46320 (duplicate model switcher on desktop), #47327 (Chinese user: desktop fails to read third-party models) |

**Key insight**: Reliability of async agent-to-agent communication (subagent completion, tool calls) is the #1 unmet need across both projects. No project yet handles this gracefully.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Target users** | Power users, channel bridgers, agent orchestration builders | Developers, multi-agent system operators, enterprise deployments |
| **Primary use case** | Multi-platform chat delivery (Telegram, WhatsApp, Slack, Signal) with structured content | Multi-tenant isolation, custom model integration, voice interaction |
| **Technical architecture** | Script-heavy, community-fix driven, broader channel support | Modular, design-debate heavy, smaller but more opinionated feature set |
| **Release cadence** | Frequent patch releases (v2026.6.8 today) | Slower, fewer releases but focused on architectural gains |
| **Language/community** | Primarily English, high volume of small contributions | Mix of English and Chinese (notable #47327), fewer but deeper contributions |
| **Unique strengths** | Telegram/WhatsApp structured delivery, autofix pipeline | Multi-tenant memory isolation work, real-time voice TTS, per-profile credentials |
| **Unique weaknesses** | Systemic silent failures in subagent orchestration, high open issue count | Tool-call corruption P1 bug unaddressed for 2+ months, slower fix velocity |

**Architecture verdict**: Hermes Agent is building toward **enterprise-grade isolation** (multi-tenant hooks, per-profile git creds, two-phase context management). OpenClaw is optimizing for **end-user feature breadth and rapid community iteration**. These are complementary rather than competing strategies.

---

## 6. Community Momentum & Maturity

**Activity tiers (based on 24h data):**

| Tier | Projects | Characteristics |
|------|----------|-----------------|
| **High churn / rapid iteration** | OpenClaw | 500 daily items, 91 merged PRs, new release. High contributor throughput but also high bug count. |
| **Healthy cadence / architectural focus** | Hermes Agent | 50 daily items, 4 merged PRs, no release. Fewer but deeper changes. |

**Maturity signals:**
- **OpenClaw**: High engagement but low stability signal. The existence of a "Clawsweeper" label for maintainer review suggests a triage bottleneck. v2026.6.8 release shows shipping discipline despite chaos.
- **Hermes Agent**: Higher bar for PR acceptance (4 merged vs 91). Active architectural debates (two-phase context, multi-tenant) indicate a mature design culture. However, the P1 tool-call corruption bug (#6841, 2+ months old) is a worrying gap.

**Prediction**: OpenClaw will stabilize its orchestration layer within 2-3 patch releases, improving reliability but likely continuing its high-velocity model. Hermes Agent may see a major "stability release" soon that addresses the P1 tool-call bug and multi-tenant isolation.

---

## 7. Trend Signals

**For AI agent developers**, the following industry trends emerge from community feedback:

1. **Subagent orchestration is the new bottleneck**: Both projects report silent failures in agent-to-agent task completion. This suggests that LLM-as-orchestrator patterns are failing in production, and developers need **observability, retry, and notification primitives** for subagent workflows.

2. **Streaming APIs are under pressure**: Watchdog timeouts (OpenClaw #68596) and "reasoning streaming correct but final answer dumped" (Hermes #47116) indicate that current streaming architectures assume deterministic, fast model response. Long-thinking models (e.g., chain-of-thought, reasoning models) are breaking these assumptions. **Configurable streaming timeouts** will become a baseline requirement.

3. **Multi-tenant readiness is a production blocker**: Hermes #34352 (memory hooks bypass isolation) is a direct impediment to multi-agent deployments. Developers building internal tools or SaaS-like agent services need **tenant-aware memory, credential, and context boundaries**.

4. **Desktop platform demand is real and underserved**: OpenClaw #75 (79👍) and Hermes's desktop model-picker regressions (#47042, #46320) show that mobile-first (iOS/macOS) reach is insufficient. Linux/Windows desktop support is a **differentiator candidate**.

5. **Voice as a first-class interaction mode is emerging**: Hermes's real-time voice PR (#47330) and streaming TTS dispatcher (#47588) signal that **voice is no longer an add-on** but a core modality being designed into agent frameworks. Developers should plan for voice-native agent interfaces.

6. **Telegram is the stress test for rendering fidelity**: Both projects struggle with Telegram's MarkdownV2 rendering. Telegram power users are early adopters of AI agents, and **Telegram UX quality is a proxy for overall platform maturity**. Developers investing in chat-based agent deployment should prioritize Telegram rendering first.

7. **Silent failures are the top user frustration**: Across both projects, users consistently express helplessness when agents "promise follow-ups without starting them" (OpenClaw #58450), "lose subagent results without notification" (#44925), or "log MCP errors only at DEBUG" (Hermes #31246). **Observability and user-facing error communication** are critical UX gaps in current agent frameworks.

**Recommendation for developers evaluating these projects**: Choose OpenClaw if you need broad channel delivery and can tolerate a higher bug surface. Choose Hermes Agent if multi-tenant isolation and architectural soundness are your priority. Both projects will likely converge on similar reliability improvements in the next 2-3 months, with OpenClaw driven by community pressure and Hermes by design iteration.

---

*Data sourced from OpenClaw and Hermes Agent GitHub community digests for 2026-06-17. Health scores are qualitative assessments based on issue volume, severity distribution, and fix velocity.*

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-17

## Today's Overview
Hermes Agent continues to see very high activity, with **50 issues and 50 pull requests updated in the last 24 hours**. Of these, 5 issues were closed (including 3 bug fixes) and 4 PRs were merged/closed. No new releases were published today. The project is in a healthy, fast-paced development cycle, with significant attention on **multi-tenant isolation**, **platform-specific rendering bugs** (Telegram, Feishu, Signal), and **credential/authentication reliability**. Several long-standing design discussions (e.g., two-phase context management, custom provider model discovery) are still active, indicating ongoing architectural evolution.

## Releases
**None** in the last 24 hours.

## Project Progress
- **Merged/Closed PRs (4 total)**: Notable among the closed PRs is [#28981](https://github.com/NousResearch/hermes-agent/pull/28981) (fix: exclude `.stash` directory from skill scanning), which addresses a skill indexing bug. Several closed issues confirm bug fixes landed: [#26599](https://github.com/NousResearch/hermes-agent/issues/26599) (P1 – Codex `extra_headers` rejection) and [#46789](https://github.com/NousResearch/hermes-agent/issues/46789) (P2 – desktop segfaults on macOS) are resolved.
- **Closed Issues (5)**: In addition to the above, [#46320](https://github.com/NousResearch/hermes-agent/issues/46320) (duplicate desktop model switcher) and [#47529](https://github.com/NousResearch/hermes-agent/issues/47529) (duplicate Slack feature) were closed as duplicates, indicating ongoing refinement of the issue tracker.
- **Feature Progress**: Several open PRs with no comments yet are advancing key capabilities, including real-time voice conversation ([#47330](https://github.com/NousResearch/hermes-agent/pull/47330)), Mattermost channel discovery ([#47593](https://github.com/NousResearch/hermes-agent/pull/47593)), and per-profile git credential provisioning ([#47598](https://github.com/NousResearch/hermes-agent/pull/47598)).

## Community Hot Topics
The most active discussions (by comment count) reveal user frustration and feature demands:

| Issue/PR | Comments | Topic |
|----------|----------|-------|
| [#34352 – Multi-Tenant Hermes Problem](https://github.com/NousResearch/hermes-agent/issues/34352) | 7 | Memory hooks bypass tenant isolation |
| [#6388 – Telegram MarkdownV2 bullet escape](https://github.com/NousResearch/hermes-agent/issues/6388) | 6 | Bullet lists rendered as escaped `\-` |
| [#47327 – 桌面端无法读取第三方模型](https://github.com/NousResearch/hermes-agent/issues/47327) | 4 | Chinese user: desktop fails to read third-party models |
| [#31246 – MCP silent failure](https://github.com/NousResearch/hermes-agent/issues/31246) | 3 | MCP errors logged only at DEBUG, invisible to users |
| [#10011 – Auto-discover models from custom endpoints](https://github.com/NousResearch/hermes-agent/issues/10011) | 3 (👍3) | Feature request: model picker should auto-detect models |

The **multi-tenant problem** (#34352) is a core architectural discussion – the user has a production fix and is advocating for upstreaming changes to make tenant isolation possible without forking core. The Telegram rendering bug (#6388) is a long-standing UX issue (opened April 9) that continues to draw attention, with 1 👍 indicating user impact.

## Bugs & Stability
Several new bugs were reported in the last 24 hours. Ranked by severity (P1 highest):

- **P1**: [#6841 – Hermes tool-calling pipeline can corrupt tool names and JSON arguments](https://github.com/NousResearch/hermes-agent/issues/6841) – still open, 3 👍, affects generic tool-call path. A fix PR [#20766](https://github.com/NousResearch/hermes-agent/pull/20766) (P1 security, Tirith fail-open) is also still open.
- **P2** (new today):
  - [#47515 – `hermes config set` coerces "on"/"off" to booleans](https://github.com/NousResearch/hermes-agent/issues/47515) – corrupts enum string settings.
  - [#47509 – MCP discovery failures invisible at INFO log level](https://github.com/NousResearch/hermes-agent/issues/47509) – similar to #31246.
  - [#47048 – Telegram table+bullet double render](https://github.com/NousResearch/hermes-agent/issues/47048) – final reply overlaps streamed message.
  - [#47116 – Reasoning streaming correct but final answer dumped all at once](https://github.com/NousResearch/hermes-agent/issues/47116) – CLI UX regression.
  - [#47042 – Desktop model picker hides custom providers](https://github.com/NousResearch/hermes-agent/issues/47042) – regressed after update.
- **P3** (new today): [#47504 – Profile name dialogs accept uppercase then warn](https://github.com/NousResearch/hermes-agent/issues/47504), [#47154 – Dashboard file browser HTTP 500 on dangling symlinks](https://github.com/NousResearch/hermes-agent/issues/47154).

**Fix PRs exist** for several bugs: [#47597](https://github.com/NousResearch/hermes-agent/pull/47597) (Qwen tool result strings), [#47596](https://github.com/NousResearch/hermes-agent/pull/47596) (Feishu card parsing), [#47594](https://github.com/NousResearch/hermes-agent/pull/47594) (send_message cross-loop crash), and [#46722](https://github.com/NousResearch/hermes-agent/pull/46722) (WeCom duplicate instances). These indicate responsive development.

## Feature Requests & Roadmap Signals
- **Two-Phase Context Management** ([#513](https://github.com/NousResearch/hermes-agent/issues/513), created March 6) – user proposes cheaper pruning before full compaction, inspired by Kilocode. Still open with 2 comments; likely candidate for next minor release.
- **Auto-discover models** ([#10011](https://github.com/NousResearch/hermes-agent/issues/10011)) – 3 👍, high user demand for custom provider integration.
- **Per-profile git credentials** ([#47598](https://github.com/NousResearch/hermes-agent/pull/47598)) – new feature PR, indicating roadmap focus on multi-profile environment management.
- **Real-time Voice** ([#47330](https://github.com/NousResearch/hermes-agent/pull/47330)) – major feature landing as a gateway platform plugin, addressing Option C from issue #35750.
- **Streaming TTS dispatcher** ([#47588](https://github.com/NousResearch/hermes-agent/pull/47588)) – provider-agnostic streaming TTS, suggests expanded voice capabilities.

Predictions for next version: **Multi-tenant memory isolation** (#34352) is highly active and may be prioritized if the external fix is upstreamed. **Telegram rendering fixes** and **MCP error visibility** are low-hanging UX improvements likely to land soon.

## User Feedback Summary
- **Pain Points**:
  - **Multi-tenant isolation**: Memory operations bypass hooks entirely – a blocker for production deployments with isolated contexts. (#34352)
  - **Telegram MarkdownV2 rendering**: Bullet lists broken, tables double-rendered – poor user experience for Telegram power users. (#6388, #47048)
  - **Desktop model picker**: Custom providers hidden, model override lost on session resume. (#47042, #46320)
  - **Email subject hardcoded**: No way to set subject for outbound emails. (#46947)
  - **Credential detection drift**: 18 provider overlays missing `extra_env_vars` causing authentication failures. (#47361)
- **Satisfaction**: High community engagement (50+ items updated daily) suggests active user base. Several closed bugs indicate maintainers address reported issues quickly. Positive reactions (👍) on feature requests show enthusiasm for improvements.
- **Use Cases**: Emerging patterns include **multi-agent systems** (multi-tenant), **local model integration** (Gemma 4 via Ollama #45924), **voice interaction** (new PR #47330), and **enterprise platforms** (Mattermost, WeCom, QQ Bot).

## Backlog Watch
The following important issues/PRs have been open for extended periods without maintainer response or resolution:

| Item | Created | Priority | Age | Notes |
|------|---------|----------|-----|-------|
| [#513 – Two-Phase Context Management](https://github.com/NousResearch/hermes-agent/issues/513) | 2026-03-06 | Feature | 3+ months | No maintainer comments; design proposal still waiting for triage. |
| [#6841 – Tool-call corruption](https://github.com/NousResearch/hermes-agent/issues/6841) | 2026-04-09 | **P1** | 2+ months | High severity with 3 👍; no linked PR or assignee visible. |
| [#20766 – Tirith fail-open security fix](https://github.com/NousResearch/hermes-agent/pull/20766) | 2026-05-06 | **P1** | 1+ month | Open PR for security issue; no recent updates or merge. |
| [#35424 – Fallback activation notice buffered](https://github.com/NousResearch/hermes-agent/pull/35424) | 2026-05-30 | P2 | 2.5 weeks | PR open, no comments from maintainers. |
| [#39806 – Stale-state guard for background review](https://github.com/NousResearch/hermes-agent/pull/39806) | 2026-06-05 | P3 | 12 days | No review activity. |

The **P1 tool-call corruption bug** (#6841) is the most concerning backlog item – it directly impacts reliability of all tool use and has no visible movement. The security PR (#20766) also warrants attention given its severity label.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*