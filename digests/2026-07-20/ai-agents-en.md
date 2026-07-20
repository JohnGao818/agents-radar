# OpenClaw Ecosystem Digest 2026-07-20

> Issues: 345 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-20 02:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-20

---

## 1. Today's Overview

OpenClaw is experiencing extremely high activity, with **345 issues** and **500 pull requests** updated in the last 24 hours. The project maintains a strong pulse: 231 open issues and 353 open PRs indicate continuous development, while 147 PRs have been merged or closed in the same period. No new releases were published today, but the volume of merged fixes and ongoing feature work suggests a build-up toward an upcoming stable release. Community engagement is robust, with several long-running discussions on platform support, security hardening, and agent reliability continuing to attract attention.

---

## 2. Releases

No new releases recorded for 2026-07-20. The latest release remains earlier versions (e.g., v2026.7.1, v2026.7.2-beta.3), with several regression bugs reported against them (see Bugs & Stability below).

---

## 3. Project Progress

Of the **147 merged/closed PRs** in the last 24 hours, the project saw progress across multiple areas:

- **Agent tooling & reliability** – Notable merged/closed PRs include:
  - [#111364](https://github.com/openclaw/openclaw/pull/111364) (closed) – Fix escape code leakage in exec output when escape sequences span stream chunks.
  - [#108075](https://github.com/openclaw/openclaw/issues/108075) (closed) – Regression fix for LLM provider rejecting request schema/tool payload in v2026.7.1.
  - [#89954](https://github.com/openclaw/openclaw/issues/89954) (closed) – Telegram `getUpdates` 409 cascade fix.
  - [#97970](https://github.com/openclaw/openclaw/issues/97970) (closed) – Gateway bind auto-fill conflict with auth.mode:none.

- **Security hardening** – Several PRs merged to bound file reads and enforce size limits (e.g., #111588, #111586, #109793, #109880), addressing potential resource exhaustion.

- **Localization & infrastructure** – Multi-PR foundation series (#111541–#111545) for localization convergence is in review.

- **CI/Dependencies** – Automated dependency bumps (#110263) and bounded timeout additions for subprocess calls (#111580, #111166, #111176) improve stability in CI and embedded environments.

---

## 4. Community Hot Topics

The following issues and pull requests have generated the highest discussion and reaction volume:

| Item | Comments | Reactions | Description |
|------|----------|-----------|-------------|
| [#75 – Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) | 114 | 80 👍 | Long-standing request for desktop app parity across platforms. |
| [#7707 – Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707) | 17 | – | Tag memory entries by origin to prevent poisoning attacks. |
| [#10659 – Masked Secrets](https://github.com/openclaw/openclaw/issues/10659) | 14 | 4 👍 | Prevent agents from reading raw API keys. |
| [#13583 – Pre-response enforcement hooks](https://github.com/openclaw/openclaw/issues/13583) | 14 | 2 👍 | Hard gates for mandatory tool-call/policy rules. |
| [#94846 – Cron agentTurn delivery bug](https://github.com/openclaw/openclaw/issues/94846) | 12 | 1 👍 | Recovered tool error misclassified as fatal in cron workflows. |
| [#109490 – Codex turn interruption](https://github.com/openclaw/openclaw/issues/109490) | 11 | 1 👍 | Client-delegated dynamic tools cause agent turn to stop prematurely. |
| [#79077 – Telegram guest/bot-to-bot modes](https://github.com/openclaw/openclaw/issues/79077) | 11 | 8 👍 | Support for Telegram May 2026 platform features. |
| [#6615 – Denylist for exec-approvals](https://github.com/openclaw/openclaw/issues/6615) | 8 | 8 👍 | Allow “allow everything except X” policies. |

**Underlying needs:**  
The hot topics reflect three core community demands:  
1. **Platform coverage** – Users need CLI/desktop apps beyond macOS (Linux, Windows).  
2. **Security & trust** – Agents must be protected from memory poisoning, secret leakage, and untrusted integrations.  
3. **Deterministic control** – High-stakes workflows (finance, ops) require hard enforcement hooks rather than soft prompt-based rules.

---

## 5. Bugs & Stability

Multiple high-severity bugs were reported or updated today. The table below ranks them by reported impact:

| Issue | Priority | Impact | Description | Fix PR? |
|-------|----------|--------|-------------|---------|
| [#109490](https://github.com/openclaw/openclaw/issues/109490) | P1 | Message loss | Codex turns interrupted after client-delegated tool result (`terminate:true`) – promised work never executes. | No specific PR yet |
| [#92076](https://github.com/openclaw/openclaw/issues/92076) | P1 | Message loss | Subagent completion fails when requester session is inactive and transcript locked. | No |
| [#70024](https://github.com/openclaw/openclaw/issues/70024) | P1 | Message loss | Channel stop timeout leaves channel permanently dead with stale store entries. | No (linked PR open) |
| [#102006](https://github.com/openclaw/openclaw/issues/102006) | P1 | Crash-loop / wedge | Exec tool aborted run wedges subsequent exec calls in same session (regression from #94412). | No |
| [#108580](https://github.com/openclaw/openclaw/issues/108580) | P1 | Auth-provider | Cron tool schema incompatible with llama.cpp grammar-constrained tool calling (regression v2026.7.1). | Linked PR #108580? |
| [#111519](https://github.com/openclaw/openclaw/issues/111519) | P1 | Message loss | Telegram DM replies fall back after stale DM-scope cleanup in v2026.7.2-beta.3. | No |
| [#83337](https://github.com/openclaw/openclaw/issues/83337) | P1 | Silent channel failure | Plugin/core version drift after upgrade causes silent failure. | No |
| [#99910](https://github.com/openclaw/openclaw/issues/99910) | P1 | Crash-loop | Memory Dreaming run pegs gateway event loop for ~10 min; short-term recall never persists. | No |
| [#94846](https://github.com/openclaw/openclaw/issues/94846) | P2 | Message loss | Cron isolated agentTurn skips delivery after recovered early tool error misclassified as fatal. | PR #111574 (fix for nonzero exit classification) |
| [#111506](https://github.com/openclaw/openclaw/issues/111506) | P2 | Session-state | Rapid-fire requests cause session lock contention on heavy contexts (LM Studio backend). | No |

**Notable regressions:**  
Multiple P1 regressions stem from the v2026.7.1 release (tool schema changes, Telegram DM scope cleanup, state stream wedge). The community is actively reporting these, and maintainers appear to be triaging with `clawsweeper:needs-maintainer-review` and `linked-pr-open` labels.

---

## 6. Feature Requests & Roadmap Signals

The following accepted or highly-discussed features indicate likely near-term development targets:

| Issue | Summary | Likelihood for Next Release |
|-------|---------|-----------------------------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | Linux/Windows Clawdbot Apps | Moderate – long-running but no recent fix PRs; P2 priority. |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | Memory Trust Tagging by Source | High – security-critical P2 with strong community support. |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | Masked Secrets (agent cannot see API keys) | High – P1 security, multiple upvotes, linked to secret management. |
| [#13583](https://github.com/openclaw/openclaw/issues/13583) | Pre-response enforcement hooks | Moderate – P2 but addresses a hard requirement for enterprise use. |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) | Denylist support for exec-approvals | Moderate – P2, 8 upvotes, complements existing allowlist. |
| [#110950](https://github.com/openclaw/openclaw/issues/110950) | “Everything is a cron” – unify heartbeat/watchers/automation | Low – conceptual proposal, P2, authored by maintainer (steipete), but early stage. |
| [#12219](https://github.com/openclaw/openclaw/issues/12219) | Skill Permission Manifest (skill.yaml) | Moderate – P2 security, aligns with current security hardening trend. |
| [#78963](https://github.com/openclaw/openclaw/issues/78963) | WhatsApp listen-only/hooks-only mode | Low – P2, niche use case for archival/ETL. |
| [#99583](https://github.com/openclaw/openclaw/issues/99583) | Intelligent Session Auto-Titling | Low – P3, but aligns with UX improvements. |

**Prediction:** The next release is likely to include at least one of the security-focused features (Memory Trust Tagging or Masked Secrets) along with fixes for the most critical regressions. The “Everything is a cron” proposal may influence future architecture but is unlikely in the immediate next version.

---

## 7. User Feedback Summary

Users express both satisfaction with the platform’s capability and frustration with stability and missing features. Key themes:

- **Pain points:**
  - **Session reliability** – Multiple reports of lost messages, hung agents, and dead channels (#109490, #92076, #70024, #102006).
  - **Security gaps** – Memory poisoning, readable secrets, and untrusted skill permissions are top concerns (#7707, #10659, #12219).
  - **Platform availability** – Linux/Windows users are still waiting for native apps (#75).
  - **Tool deficiencies** – Browser tool requires CSS selectors (#44431), exec tool has escape code and wedge issues (#93139, #102006), cron tool schema limits local model compatibility (#108580).
  - **Configuration friction** – Version drift causes silent failures (#83337), missing fields get auto-filled incorrectly (#97970).
  - **UX friction** – Multi-line input in TUI, vague context overflow messages, subagent announce suppression (#10118, #9409, #8299).

- **Positive signals:**
  - Feature requests with high upvote counts (8–80) show active, engaged user base.
  - Rapid issue triage (231 open / 345 updated) indicates maintainers are responsive.
  - Multiple pull requests merging daily suggests a healthy development cycle.

---

## 8. Backlog Watch

The following long-standing issues and PRs have not seen meaningful progress and may need maintainer attention:

| Item | Created | Last Updated | Comments | Status |
|------|---------|--------------|----------|--------|
| [#75 – Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) | 2026-01-01 | 2026-07-19 | 114 | Open, P2, needs maintainer review |
| [#7707 – Memory Trust Tagging](https://github.com/openclaw/openclaw/issues/7707) | 2026-02-03 | 2026-07-19 | 17 | Open, P2, needs security review |
| [#10659 – Masked Secrets](https://github.com/openclaw/openclaw/issues/10659) | 2026-02-06 | 2026-07-19 | 14 | Open, P1, needs security review |
| [#13583 – Pre-response enforcement hooks](https://github.com/openclaw/openclaw/issues/13583) | 2026-02-10 | 2026-07-19 | 14 | Open, P2, needs security review |
| [#6599 – `/models test-fallback`](https://github.com/openclaw/openclaw/issues/6599) | 2026-02-01 | 2026-07-19 | 6 | Open, P3, needs product decision |
| [#7524 – groupScope option](https://github.com/openclaw/openclaw/issues/7524) | 2026-02-02 | 2026-07-19 | 5 | Open, P2, needs product decision |
| [#82540 – WeChat hot-reload accounts](https://github.com/openclaw/openclaw/pull/82540) | 2026-05-16 | 2026-07-20 | – | Open PR, P1, needs proof |
| [#8355 – Streaming TTS for voice calls](https://github.com/openclaw/openclaw/issues/8355) | 2026-02-03 | 2026-07-19 | 5 | Open, P2, needs live repro |
| [#9016 – OpenRouter cost exposure](https://github.com/openclaw/openclaw/issues/9016) | 2026-02-04 | 2026-07-19 | 5 | Open, P2, needs maintainer review |
| [#9986 – Trigger fallback on context length exceeded](https://github.com/openclaw/openclaw/issues/9986) | 2026-02-05 | 2026-07-19 | 5 | Open, P2, needs product decision |
| [#111176 – Timeout for channel docs find](https://github.com/openclaw/openclaw/pull/111176) | 2026-07-19 | 2026-07-20 | – | Open PR, P3, needs PR context |

These items have been open for months (5–7 months) and have accumulated comments without resolution. They represent valuable features or potential stability improvements that could unblock community workflows. Maintainers should prioritize triage, especially for P1 issues with security impact.

---

*Data snapshot as of 2026-07-20 23:59 UTC. Generated from OpenClaw GitHub repository metadata.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## 1. Ecosystem Overview

The open-source personal AI assistant and agent ecosystem is entering a phase of rapid maturation, characterized by a tension between feature velocity and production reliability. Both OpenClaw and Hermes Agent demonstrate vibrant community engagement with hundreds of daily contributions, yet both face similar structural challenges around session state consistency, streaming reliability, and security hardening. The landscape is bifurcating: large reference implementations like OpenClaw are building toward stable releases with broad platform support, while more focused projects like Hermes Agent are refining UX and provider compatibility for specific desktop-centric users. Neither project has released a stable version this week, indicating that the ecosystem is still in a pre-1.0 refinement cycle, with regression management consuming significant maintainer bandwidth.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| Issues updated (24h) | 345 | 50 |
| PRs updated (24h) | 500 | 50 |
| Open issues | 231 | 45 |
| Open PRs | 353 | ~44 |
| Merged/closed PRs (24h) | 147 | 6 |
| Releases today | None | None |
| P1 bugs (active) | 8 | ~5 |
| Health score (subjective) | High velocity, moderate instability | Moderate velocity, good resolution rate |

OpenClaw operates at an order-of-magnitude larger scale, with 10× the daily issue/PR volume. However, it also carries a larger absolute bug backlog, with multiple P1 regressions from its recent v2026.7.1 release. Hermes Agent shows a cleaner resolution ratio (6 PRs merged for 50 updated) and fewer high-severity open bugs, suggesting a more controlled release cadence.

## 3. OpenClaw's Position

OpenClaw holds several structural advantages over Hermes Agent:

- **Broader platform ambition**: OpenClaw explicitly targets Linux/Windows desktop parity (issue #75, 114 comments), while Hermes Agent's desktop support is macOS-primary with community gaps.
- **Deeper security architecture**: Features like Memory Trust Tagging (#7707), Masked Secrets (#10659), and Pre-response enforcement hooks (#13583) demonstrate a more mature security-first design philosophy. Hermes Agent's security posture is reactive (credential redaction PRs).
- **Larger community base**: 114 reactions on a single platform parity issue vs. Hermes Agent's highest at ~7 comments on active bugs. OpenClaw's community is both larger and more vocal.

However, OpenClaw's complexity creates a higher regression surface. Its v2026.7.1 introduced multiple P1 regressions (tool schema breaking local LLMs, Telegram DM scope cleanup issues). Hermes Agent, with a narrower scope and smaller codebase, appears to have fewer cross-cutting regression vectors.

## 4. Shared Technical Focus Areas

Both projects are converging on four critical requirements:

1. **Session state reliability** – Both projects have P1 bugs around session lifecycle: OpenClaw's channel stop timeouts (#70024) and session lock contention (#111506); Hermes Agent's stale-route recovery causing cost escalation (#67781) and daily session reset failures. **Underlying need**: deterministic session teardown and recovery semantics.

2. **Streaming connection stability** – OpenClaw reports escape code leakage across stream chunks (#111364); Hermes Agent reports Cloudflare `keepalive_expiry` breakage (#67012). **Underlying need**: robust stream chunk handling irrespective of network intermediaries.

3. **Provider schema compatibility** – OpenClaw's cron tool schema breaks llama.cpp grammar-constrained tool calling (#108580); Hermes Agent's LM Studio context_length is stuck at 64K (#30178). **Underlying need**: standardized tool schemas that work across local and cloud LLM providers.

4. **Deterministic control hooks** – OpenClaw's #13583 (pre-response enforcement) and #6615 (denylist for approvals) mirror Hermes Agent's need for hard gating in enterprise workflows. **Underlying need**: policy enforcement that is not prompt-dependent.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Feature focus** | Agent tooling (exec, cron, memory systems), multi-platform CLI/desktop | Chat UI/UX, desktop-first, provider streaming, config-bridge |
| **Target user** | Power users and developers building complex agent workflows | End-users and administrators managing personal/team chat agents |
| **Technical architecture** | Monolithic agent runtime with heavy tool coupling (exec, cron, memory dreaming) | Gateway-based modular architecture with provider abstraction |
| **Security posture** | Proactive: designing trust tagging, secret masking, enforcement hooks | Reactive: fixing credential leaks, redacting SDK logs |
| **Platform coverage** | macOS, Linux/Windows in demand (#75) | macOS primary; desktop UI instability reports |
| **Community maturity** | Longest-running feature requests (6+ months) accumulate without resolution | Faster issue triage, but smaller absolute volume |

OpenClaw is building a **platform for agent developers** (exec tools, cron, permission manifests). Hermes Agent is building a **user-facing chat application** (streaming quality, desktop rendering, provider switching). These are complementary rather than competitive, with OpenClaw likely serving as infrastructure for projects that would use Hermes Agent as a front-end.

## 6. Community Momentum & Maturity

**Tier 1 – Rapid Iteration (High risk/high reward):**  
**OpenClaw** shows the highest raw activity but is experiencing "growth pain" – 147 PRs merged daily suggests a team racing toward stability, but 8 active P1 regressions from the latest release indicate quality assurance may not be keeping pace with feature development. The project is in a **build-up phase**, accumulating features and fixes toward an upcoming stable release.

**Tier 2 – Steady Stabilization:**  
**Hermes Agent** demonstrates a healthier feature-to-fix ratio. With 6 PRs merged and only ~5 P1 bugs active, it appears to be in a **consolidation phase**. Community feedback (streaming bugs, desktop UI inconsistencies) suggests it is nearing desktop-application maturity but needs to address provider-specific regression patterns.

**Maturity indicators:** Neither project has a 1.0 stable release. OpenClaw's oldest open issues (6+ months) without maintainer attention (#75, #7707) suggest significant technical debt. Hermes Agent's LM Studio bug (#30178, 2 months stale) indicates similar prioritization challenges.

## 7. Trend Signals

Five industry trends emerge from cross-project community feedback:

1. **Deterministic security is non-negotiable** – Users in both communities demand hard enforcement (pre-response hooks, denylists) over soft prompt-based controls. This is the #1 signal for enterprise adoption readiness.

2. **Session trust is the new authentication** – Memory poisoning (#7707), secret leakage (#10659), and provider state inheritance (#44585, #67781) represent a new class of security vulnerabilities unique to AI agents. Traditional authentication models (OAuth, API keys) are insufficient.

3. **Multi-platform reachability is table stakes** – The 114-comment thread on OpenClaw's Linux/Windows apps (#75) and Hermes Agent's desktop UI bugs indicate that macOS-only or CLI-only agents will lose market share. Users expect cross-platform parity (including Telegram, Feishu, Mattermost).

4. **Provider streaming resilience is a differentiator** – Both projects struggle with streaming failures under Cloudflare, custom gateways, and local LLMs. Users are abandoning agents that drop messages mid-stream. This is the reliability equivalent of "5 nines" for the AI agent space.

5. **User trust is eroding from cost surprises** – $12 in unnecessary API calls from a session reset bug (#67781) and billing surprises from cron tool behavior (#94846) show that users are acutely cost-sensitive. Agents that cannot explain or control their API consumption face churn.

**Value for AI agent developers:** The data strongly suggests that the next wave of successful agent frameworks will prioritize (a) deterministic security hooks, (b) session trust and memory provenance, (c) robust cross-provider streaming, and (d) transparent cost attribution. OpenClaw leads on (a) and (b); Hermes Agent leads on (c) through its gateway architecture. Neither has fully solved (d), presenting an opportunity for differentiation.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-07-20

## 1. Today’s Overview
The Hermes Agent project is experiencing very high activity with 50 issues and 50 pull requests updated in the last 24 hours. Of these, 5 issues were closed and 6 PRs were merged/closed, indicating steady resolution of reported problems. The open/active issue count (45) suggests a healthy backlog of community-reported bugs and feature requests being actively investigated. No new releases were published today, but the sheer volume of updates—especially around session state, streaming compatibility, and desktop UI—signals a project in continuous, community-driven refinement.

## 2. Releases
None. The latest release remains earlier versions; no new release notes are available for this date.

## 3. Project Progress
Six pull requests were merged or closed today, covering a range of fixes and minor features. Notable merged/closed PRs include:
- **#64613** – `fix(gateway): retry transient lifecycle notifications` – improves reliability of restart and home-channel notifications.
- **#67822** – `fix(desktop): render fenced file lists as code blocks` – corrects markdown rendering in the desktop app.
- **#67818** – `perf(desktop): virtualize the review-pane diff` – eliminates full-Shiki freezes on large diffs.
- **#67819** – `fix(feishu): redact SDK credentials from logs` – security hardening.
- **#67810** – `fix(mattermost): honor reply_mode from config.yaml` – config bridge fix.
- **#67811** – `fix(cli): clear plugin state on removal` – prevents stale plugin entries.

Additionally, several open PRs advanced (e.g., #65544 CJK FTS index, #62660 topic-aware compaction) but remain under review.

## 4. Community Hot Topics
The most active discussions highlight three recurring pain points:

- **Streaming reliability with Cloudflare/OpenRouter** – [#67012](https://github.com/NousResearch/hermes-agent/issues/67012) (7 comments) reports that a `keepalive_expiry=20` change breaks streaming for OpenRouter users behind Cloudflare. The commit that introduced the regression is identified, and a fix is being sought.
- **Worker exit without `kanban_complete`** – [#46593](https://github.com/NousResearch/hermes-agent/issues/46593) (6 comments) describes a protocol-violation bug where kanban workers exit cleanly without calling completion callbacks, causing task blocks. The root cause (boto3 `converse_stream` failure) is known but a fix is pending.
- **MCP tool re-registration** – [#67187](https://github.com/NousResearch/hermes-agent/issues/67187) (5 comments) concerns a parked server that reconnects but fails to re-register its tools, breaking downstream workflows. The community is actively reproducing and discussing a fix.

These issues share a common theme: **state consistency across sessions, streaming connections, and tool lifecycles**—a critical area for reliability in AI agent frameworks.

## 5. Bugs & Stability
Several new bugs were reported today, ranked by priority:

**Critical (P2):**
- **Telegram fails to connect** – [#67817](https://github.com/NousResearch/hermes-agent/issues/67817): `HTTPXRequest.do_request` read-only error, likely version incompatibility. *No fix PR yet.*
- **Daily session reset resurrected by stale-route recovery** – [#67781](https://github.com/NousResearch/hermes-agent/issues/67781): A Telegram session survived its 4 AM reset, costing ~$12 in unnecessary API calls. **Fix PR [#67816](https://github.com/NousResearch/hermes-agent/pull/67816) addresses related Telegram group allowlist issues.**
- **Desktop first-message with file attachment aborted by drift race** – [#67783](https://github.com/NousResearch/hermes-agent/issues/67783) and fix PR [#67813](https://github.com/NousResearch/hermes-agent/pull/67813) align foreground delivery with cua-driver 0.9.0.
- **Anthropic model picker missing `claude-sonnet-5`** – [#67815](https://github.com/NousResearch/hermes-agent/issues/67815): CLI works but desktop app does not list it. *No fix PR.*
- **Messages disappear after switching provider mid-conversation** – [#67651](https://github.com/NousResearch/hermes-agent/issues/67651): Cmd+R restores them; likely a UI state sync bug. *No fix PR.*
- **Desktop files panel auto-opens on new session** – [#67286](https://github.com/NousResearch/hermes-agent/issues/67286): persistent UI annoyance reported by multiple users (duplicate of #66059 and #66917). *No dedicated fix PR, but #67822 touches related rendering.*

**Moderate (P3):**
- **Interface zoom setting resets** – [#60693](https://github.com/NousResearch/hermes-agent/issues/60693): 110% zoom intermittently reverts to 100%. *No fix PR.*
- **Online documentation out of date** – [#67278](https://github.com/NousResearch/hermes-agent/issues/67278): `custom_providers` → `providers` change not reflected. *No fix PR.*
- **LM Studio per-model context_length broken** – [#30178](https://github.com/NousResearch/hermes-agent/issues/30178): regressed to 64K in v0.14.0, still open since May. *No fix PR.*

**Fixes with PRs today:**
- [#67813](https://github.com/NousResearch/hermes-agent/pull/67813) – computer_use alignment with cua-driver 0.9.0 (fixes #67783).
- [#67812](https://github.com/NousResearch/hermes-agent/pull/67812) – new-chat file attachment race (fixes #64789? likely).
- [#67814](https://github.com/NousResearch/hermes-agent/pull/67814) – raises vulnerable dependency floors.
- [#67816](https://github.com/NousResearch/hermes-agent/pull/67816) – Telegram group allowlist fallback (related to #67781).

## 6. Feature Requests & Roadmap Signals
Several feature requests were filed today, pointing toward upcoming priorities:

- **Lifecycle hooks as a shared runtime contract** – [#67798](https://github.com/NousResearch/hermes-agent/issues/67798): Proposes moving event hooks from gateway-owned to runtime-owned, affecting CLI, TUI, cron, and desktop surfaces. This is a broad architectural change likely to be discussed for the next major release.
- **VOICEVOX TTS provider** – [#67803](https://github.com/NousResearch/hermes-agent/issues/67803): A request to add Japanese TTS support, indicating growing internationalization needs.
- **Custom API session sources** – PR [#67820](https://github.com/NousResearch/hermes-agent/pull/67820) adds a header to accept custom session sources, enabling third-party integrations to appear in the desktop sidebar. This is close to merging.
- **Disable persistent context-window caching for volatile providers** – [#65905](https://github.com/NousResearch/hermes-agent/issues/65905): A safety feature for providers with dynamic model catalogs.

Predictions for next release: The lifecycle hook change (#67798) is still in discussion, but the custom session source PR (#67820) and the cua-driver alignment PRs (#67813, #67809) have high priority and may land soon. The VOCEVOX request, while valued, is likely lower priority.

## 7. User Feedback Summary
Users are actively reporting and discussing concrete pain points:

- **Streaming and provider-specific breakages** – Several users (evandroid, icatw, Adolanium) are frustrated by regressions in streaming reliability, especially with Cloudflare/OpenRouter and custom API gateways. The community has traced root causes to specific commits, which speeds up resolution.
- **Desktop UI inconsistencies** – Multiple reports of the files panel auto-opening (#66059, #66917, #67286), messages disappearing (#67651), and zoom resets (#60693) suggest that desktop session state management and UI reactivity are under strain.
- **Session state and billing surprises** – Users like sw5813 and twe-cloud experienced unexpected cost accumulation due to session reset failures or inherited provider state. This erodes trust and is prioritized as P2.
- **Documentation gaps** – The outdated `custom_providers` documentation (#67278) points to a need for more rigorous docs sync with code changes.

Overall sentiment is engaged but demanding – the community is providing detailed bug reports and reproduction steps, which is a sign of healthy, invested users.

## 8. Backlog Watch
The following important issues and PRs have remained open without maintainer comment or fix for an extended period:

- **#30178** – LM Studio context_length broken since v0.14.0 (filed 2026-05-22). No maintainer response. Models always show 64K regardless of config. **Severity: P3, but affects local LM Studio users significantly.**
- **#37352** – Feature request for `hermes skills lint` (2026-06-02). No maintainer activity. Would improve skill authoring tooling.
- **#39136** – Stale `hermes dashboard --tui` processes accumulate (2026-06-04). 3 comments, 1 reaction, no maintainer response. Affects upgrades.
- **#53861** – macOS gateway stays down after update due to launchd deferral (2026-06-27). 2 comments, no resolution. P2 severity but may affect macOS users.
- **#44585** – (Closed) Cron inherited paid provider state – was P1 at filing, closed with a fix, but similar issues (#67781) continue to occur, suggesting the fix may be incomplete.

These items indicate areas where maintainer attention is needed to prevent user frustration and to stabilize core functionality.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*