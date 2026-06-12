# OpenClaw Ecosystem Digest 2026-06-12

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-12 03:34 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-06-12

## 1. Today’s Overview
OpenClaw remains in an intense development cycle with **500 issues** and **500 pull requests** updated in the last 24 hours. The project currently has **471 open issues** and **378 open PRs**, reflecting sustained community engagement and active maintainer review. A new pre-release (`v2026.6.6-beta.2`) landed today, focusing on security boundaries across transcripts, sandbox, MCP, and other sensitive subsystems. Despite high churn, the backlog continues to grow — many issues and PRs are tagged with `needs-maintainer-review` or `needs-product-decision`, indicating a need for faster triage.

## 2. Releases
### **v2026.6.6-beta.2** (released 2026-06-12)
**Highlights** (from official changelog):
- Substantially tighter security boundaries across:
  - Transcript handling
  - Sandbox binds
  - Host environment inheritance
  - MCP stdio
  - Codex HTTP access
  - Native search policy
  - Elevated sender checks
  - Deleted-agent ACP bypasses
  - Loopback tools
  - Discord moderation
  - Teams group actions
- Core `exec` tool hardening.

No explicit breaking changes or migration notes were published. Users upgrading from stable should test workflows involving sandbox, MCP, and cross-channel moderation.

## 3. Project Progress
**Merged/closed PRs today (approx. 122):**
- **Fixed cron edit field loss:** PRs [#92304](https://github.com/openclaw/openclaw/pull/92304) (closed) and [#92295](https://github.com/openclaw/openclaw/pull/92295) (closed) prevent `cron edit --cron <expr>` from silently stripping `schedule.tz` and `schedule.staggerMs`.
- **Dashboard history projection fix:** PR [#92312](https://github.com/openclaw/openclaw/pull/92312) (closed) and its clean replacement PR [#92328](https://github.com/openclaw/openclaw/pull/92328) (open) fix toolCall-only assistant messages hiding recent user context, and suppress prompt persistence for exec-approval follow-ups.
- **Autofix pipeline + Windows daemon:** PR [#68936](https://github.com/openclaw/openclaw/pull/68936) (closed) adds a new PR review autofix pipeline and a Windows background daemon to supervise the gateway.
- **OpenAI Responses messages collapse:** PR [#92300](https://github.com/openclaw/openclaw/pull/92300) (open) collapses cumulative message snapshots for Bedrock Mantle GPT-5.x model family to reduce noise.
- **Feishu and iMessage bug fixes:** PRs [#92172](https://github.com/openclaw/openclaw/pull/92172) and [#92170](https://github.com/openclaw/openclaw/pull/92170) (both open) fix bilingual fallback and `actions.reply=false` respect for Feishu and iMessage channels.

**Feature advances (open PRs):**
- **Claude bridge app-server harness** ([#86655](https://github.com/openclaw/openclaw/pull/86655)) – first-class Anthropic model support with native tool execution and extended thinking.
- **Subagent execution backend placement** ([#84758](https://github.com/openclaw/openclaw/pull/84758)) – `sessions_spawn` now accepts optional placement requests.
- **Subagent `toolsAllow` forwarding** ([#78441](https://github.com/openclaw/openclaw/pull/78441)) – allowlist propagation from parent to spawned agents.
- **iFlow Search external provider** ([#92213](https://github.com/openclaw/openclaw/pull/92213)) – new web search provider for onboarding.
- **Memory query fix** ([#91691](https://github.com/openclaw/openclaw/pull/91691)) – prevents empty-string `expectedModel` in memory index resolution.

## 4. Community Hot Topics
| Issue | Comments | Reactions | Summary |
|-------|----------|-----------|---------|
| [#75](https://github.com/openclaw/openclaw/issues/75) – Linux/Windows Clawdbot Apps | 109 | 79 👍 | High demand for desktop apps on missing platforms; oldest open issue (Jan 1, 2026). |
| [#9443](https://github.com/openclaw/openclaw/issues/9443) – Prebuilt Android APK releases | 25 | 2 👍 | User Lysen (via AI assistant) requests official Android builds. |
| [#32473](https://github.com/openclaw/openclaw/issues/32473) – Control UI requires HTTPS/localhost | 17 | 5 👍 | Regression affecting VPS/Docker setups with Brave key configuration. |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) – Tiered bootstrap file loading | 17 | 0 | Feature request to reduce token waste from full bootstrap loading. |
| [#32296](https://github.com/openclaw/openclaw/issues/32296) – Agent replies to previous message | 15 | 1 👍 | Session context confusion/regression. |
| [#39604](https://github.com/openclaw/openclaw/issues/39604) – `tools.web.fetch.allowPrivateNetwork` | 13 | 9 👍 | Strong demand for opt-in private network access in `web_fetch`. |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) – Masked Secrets | 13 | 4 👍 | Need for API key visibility protection against prompt injection. |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) – Denylist support for exec-approvals | 7 | 7 👍 | “Allow everything except X” policy requested. |

**Analysis:** The community is heavily focused on security (secret masking, private network access, HTTS requirements), cross-platform support (Linux/Windows apps, Android APKs), and session quality (context confusion, bootstrap loading). The oldest issue (#75) continues to have the highest engagement, indicating strong frustration with platform gaps.

## 5. Bugs & Stability
**Critical/High-severity bugs reported recently (open):**
- **Cron failures with MiniMax 503 overload** ([#85888](https://github.com/openclaw/openclaw/issues/85888)) – intermittent but consistent early-morning failures; manual runs succeed – suggests scheduling issue rather than API health.
- **Claude CLI session reset on every turn in group channels** ([#69118](https://github.com/openclaw/openclaw/issues/69118)) – `groupIntro` drift causes full session reset each turn.
- **Isolated cron “LLM request failed”** ([#91363](https://github.com/openclaw/openclaw/issues/91363)) – model requests never reach provider; high impact for users relying on cron.
- **Duplicate message content** ([#88951](https://github.com/openclaw/openclaw/issues/88951)) – regression after 2026.5.27 update; affects all messages.
- **Multi-agent orchestration instability** ([#43367](https://github.com/openclaw/openclaw/issues/43367)) – concurrent config overwrites, session-lock failures, detached child work.
- **`exec` tool env variable inheritance broken** ([#31583](https://github.com/openclaw/openclaw/issues/31583)) – regression; `skills.entries.*.env` not passed to subprocesses.
- **Docker + sandbox workspace access broken** ([#31331](https://github.com/openclaw/openclaw/issues/31331)) – internal vs. host path mismatch.

**Regressions noted:**
- [#32473](https://github.com/openclaw/openclaw/issues/32473) – control UI HTTPS requirement regression.
- [#38327](https://github.com/openclaw/openclaw/issues/38327) – “Cannot convert undefined or null to object” with Google Vertex/Gemini models after 2026.3.2.
- [#38439](https://github.com/openclaw/openclaw/issues/38439) – avatar endpoint 404 regression.

**Fix PRs in flight:**
- [#92300](https://github.com/openclaw/openclaw/pull/92300) – fixes duplicate message snapshots for Bedrock Mantle models.
- [#92113](https://github.com/openclaw/openclaw/pull/92113) – fixes custom provider auth failure with `secretref-managed` apiKey.
- [#92294](https://github.com/openclaw/openclaw/pull/92294) – fixes `exec` tool unavailability in isolated cron on Codex runtime.

## 6. Feature Requests & Roadmap Signals
**Top community-requested features likely to land in next releases:**
- **Masked Secrets** ([#10659](https://github.com/openclaw/openclaw/issues/10659)) – strong security need; may align with ongoing security hardening in `v2026.6.6-beta.2`.
- **`tools.web.fetch.allowPrivateNetwork`** ([#39604](https://github.com/openclaw/openclaw/issues/39604)) – high 👍; low technical risk; could appear in next minor.
- **Tiered bootstrap loading** ([#22438](https://github.com/openclaw/openclaw/issues/22438)) – addresses token waste; already has linked PR open.
- **Exec approvals denylist** ([#6615](https://github.com/openclaw/openclaw/issues/6615)) – complements existing allowlist; simple config change.
- **Filesystem sandboxing via config** ([#7722](https://github.com/openclaw/openclaw/issues/7722)) – `tools.fileAccess` with allow/deny paths – adjacent to security work.
- **Multi-agent enhancement RFC** ([#35203](https://github.com/openclaw/openclaw/issues/35203)) – capability profiling, shared blackboard, token governance – likely a longer-term roadmap item.
- **Cross-channel visibility in TUI** ([#40678](https://github.com/openclaw/openclaw/issues/40678)) – broken by recent TUI isolation fix; users want opt-in mirroring.

**Predictions:** The next stable release (possibly `v2026.6.x`) will likely include masked secrets, private network fetch flag, cron edit field preservation, and the Claude bridge harness (PR #86655) given its size and maintainer interest.

## 7. User Feedback Summary
**Pain points:**
- **Session context confusion** is a recurring theme (#32296, #69118, #41165) – agents responding to wrong messages or resetting mid-conversation, especially in group channels.
- **Cron job reliability** is poor under load or with certain providers (#85888, #91363) – failures that don’t reproduce manually cause frustration.
- **Configuration complexity** – users report difficulties with HTTPS requirements, Docker/Sandbox integration, and env variable inheritance.
- **Missing platform support** – Linux/Windows desktop apps and official Android builds are the longest-standing feature gap.
- **Data loss** – write tool overwriting files (#40001) and message duplication (#88951) erode trust.

**Satisfaction signals:**
- Active community engagement (500 issues/PRs daily) indicates high usage.
- Positive reactions on security features (masked secrets, private network) show appreciation for hardening.
- Many PRs are opened by first-time contributors, suggesting a healthy open-source ecosystem.
- The new Claude bridge harness and subagent placement features demonstrate continuous innovation.

## 8. Backlog Watch
**Long-unanswered important issues (created > 3 months ago, still open, no maintainer action):**
- [#75](https://github.com/openclaw/openclaw/issues/75) – Linux/Windows apps (Jan 1) – 109 comments, no product decision despite being oldest.
- [#6731](https://github.com/openclaw/openclaw/issues/6731) – safe/unsafe ClawdBot (Feb 2) – 12 comments, no maintainer review.
- [#13616](https://github.com/openclaw/openclaw/issues/13616) – backup/restore utility (Feb 10) – 8 comments, no product decision.
- [#7707](https://github.com/openclaw/openclaw/issues/7707) – memory trust tagging by source (Feb 3) – 7 comments, no maintainer review.
- [#13610](https://github.com/openclaw/openclaw/issues/13610) – native secrets management integration (Feb 10) – 7 comments, no product decision.

**Stale but important PRs needing maintainer attention:**
- [#78441](https://github.com/openclaw/openclaw/pull/78441) – subagent toolsAllow forwarding (May 6) – marked `ready for maintainer look` but still open.
- [#87504](https://github.com/openclaw/openclaw/pull/87504) – skill workshop agent_end hook timeout fix (May 28) – ready for review.
- [#85664](https://github.com/openclaw/openclaw/pull/85664) – wire read coding tool into HTTP /tools/invoke (May 23) – ready for review.
- [#18889](https://github.com/openclaw/openclaw/pull/18889) – agent and tool lifecycle hooks (Feb 17) – no maintainer action for 4 months.

**Recommendation:** Maintainers should prioritize triaging issues and PRs tagged `needs-product-decision` and `needs-maintainer-review` to prevent community fatigue. The top-voted issues (#75, #39604, #6615) and high-profile bugs (#32296, #85888) should receive official product decisions or status updates within the next week.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is experiencing an intense maturation phase, characterized by high-velocity development cycles, growing security consciousness, and a widening gap between core reference implementations and specialized forks. Both OpenClaw and Hermes Agent show daily activity volumes that exceed most enterprise SaaS products—500+ issues/PRs and 50+ issues/PRs respectively—indicating genuine mass adoption rather than speculative development. The ecosystem is converging on a shared set of infrastructure concerns (MCP integration, sandbox security, session management) while diverging in target user profiles and architectural philosophy. Community demand is shifting from "can it work" to "can it work securely, reliably, and cross-platform," with long-standing platform gaps (Linux/Windows desktop apps, Android builds) becoming the most vocal pain points.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues updated (24h)** | 500 | 50 |
| **Open issues** | 471 | ~40-50 (estimated) |
| **PRs updated (24h)** | 500 | 50 |
| **Open PRs** | 378 | ~10-15 (estimated) |
| **Merged/closed PRs (24h)** | ~122 | 10 |
| **Current release** | v2026.6.6-beta.2 | None today (last: prior) |
| **Release cadence** | Weekly beta, monthly stable | Irregular, ~2-3 weeks |
| **Health score** | 6/10 — High churn, growing backlog, triage bottleneck | 8/10 — Fast fix cycle, PRs matching bugs, active maintainer response |

**Key observation:** OpenClaw has ~10x the raw activity volume but also shows clear triage debt (many `needs-maintainer-review` labels). Hermes Agent demonstrates higher fix velocity relative to bug reports—most P2 bugs already have matching fix PRs.

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Reference implementation status:** OpenClaw is the upstream core; Hermes Agent and other forks track it. This creates a "standards carrier" role for MCP, sandbox, and tool execution semantics.
- **Community scale:** ~10x larger contributor base, enabling faster feature development (Claude bridge harness, subagent orchestration, multi-agent RFC) and broader provider support.
- **Security leadership:** Beta.2's security hardening across 11 subsystems (transcript handling, sandbox binds, MCP stdio, loopback tools, etc.) sets the baseline for the entire ecosystem.

**Technical approach differences:**
- **Modularity vs. polish:** OpenClaw exposes more configuration surface (tiered bootstrapping, denylist policies, placement requests) at the cost of setup complexity. Hermes Agent prioritizes out-of-box experience with opinionated defaults.
- **Orchestration depth:** OpenClaw's subagent placement (`sessions_spawn` with placement requests), toolsAllow forwarding, and lifecycle hooks PRs (waiting 4 months) indicate a multi-agent architecture ambition that Hermes Agent has not matched.
- **Security philosophy:** OpenClaw is adding perimeter-style hardening (boundaries, elevation checks, ACP bypass prevention). Hermes Agent focuses on credential management (`.env` propagation to MCP) and billing safeguards.

**Community size comparison:** OpenClaw's 471 open issues vs. Hermes Agent's ~40 implies either a larger user base or higher per-user issue creation rate. The 109-comment Linux/Windows app issue (open since Jan 1) suggests platform demand that Hermes Agent has partially addressed through its desktop-first approach.

## 4. Shared Technical Focus Areas

The following requirements appear independently across both projects, indicating ecosystem-wide priorities:

| Requirement | OpenClaw | Hermes Agent | Analysis |
|-------------|----------|--------------|----------|
| **MCP integration reliability** | MCP stdio security hardening, MCP server failed banner false-positives | MCP credential/env propagation, MCP server connect timing | MCP is now a critical integration point; both projects are hardening it after initial MVP |
| **Cron scheduling reliability** | MiniMax 503 failures, "LLM request failed" errors, TZ/staggerMs field loss | Paid provider state inheritance after pause, Discord delivery "Session is closed" | Cron remains brittle across providers; community needs scheduling guarantees before trusting agents with autonomous tasks |
| **Cross-platform parity** | Linux/Windows apps (#75, oldest open issue, 109 comments) | Linux/WSL setup incompleteness, Windows terminal output, PowerShell fallback | Users expect identical experience regardless of OS; Android builds also emerging as demand |
| **Session context quality** | Context confusion (#32296), groupIntro drift (#69118), message duplication (#88951) | Desktop crash on unexpected data (#44562), undo broken on Windows (#44543) | Both projects struggle with session state integrity, especially across channels and desktop reconnects |
| **Security hardening** | Masked secrets, private network fetch, exec approval denylist | Credential pool exhaustion backoff, secret-env propagation | Security is moving from "nice-to-have" to table-stakes for self-hosted AI assistants |

**Notable divergence:** OpenClaw focuses on sandbox/filesystem boundaries; Hermes Agent focuses on credential lifecycle and billing controls.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Target user** | Self-hosting developers, power users, multi-agent orchestrators | Desktop-first individual users, enterprise BYOD, casual deployers |
| **Core strength** | Security boundaries, subagent orchestration, provider breadth | Desktop UX, rapid bug fixes, agent autonomy (model_switch tool) |
| **Architecture** | Modular core + plugins; heavy configuration (JSON/YAML) | Monolithic but extensible; opinionated defaults |
| **Release strategy** | Weekly betas, security-focused stable releases | Irregular but responsive; patches critical bugs within days |
| **Community communication** | Issue-driven with backlog friction | PR-driven with active maintainer triage |
| **Multi-agent support** | Advanced: placement requests, toolsAllow forwarding, lifecycle hooks (in-progress) | Not a priority; focus on single-agent reliability |
| **Provider strategy** | Broad support (MiniMax, Bedrock Mantle, Claude bridge) | Narrow but deep (Gemma 4, Codex GPT-5.5, custom provider caching) |
| **Desktop experience** | TUI-focused, WebUI second-class | First-class desktop client (Electron/native) |

**Strategic implication:** OpenClaw is positioning as the Kubernetes of personal AI agents—complex but powerful. Hermes Agent is positioning as the macOS of personal AI agents—polished but limited.

## 6. Community Momentum & Maturity

| Tier | Projects | Characteristics |
|------|----------|----------------|
| **Rapid iteration** | OpenClaw | 500 daily updates, weekly releases, growing backlog. 122 PRs merged today alone. Still in discovery phase for multi-agent architecture. Triage bottleneck is the primary risk. |
| **Stabilization** | Hermes Agent | 50 daily updates, 10 PRs merged, fix PRs appear within days of bug reports. Desktop UX bugs are being polished (RTL support, tool row interactions). Moving toward production readiness. |
| **Nascent** | (not covered in this analysis) | Projects with <10 daily issues/PRs, irregular releases, single-contributor maintenance |

**Maturity indicators:**
- OpenClaw: Security hardening as a dedicated release theme → signals production readiness push
- Hermes Agent: P1 billing bug still open → indicates insufficient testing on state persistence paths
- Both: Long-standing feature requests (platform support, secret management) with no resolution → ecosystem immaturity

## 7. Trend Signals

**For developers building on/open-source AI agent infrastructure:**

1. **Security is becoming a differentiator, not an afterthought.** OpenClaw's 11-subsystem security hardening in a single beta release signals that the market has moved past "first make it work" to "first make it safe." The strong community reaction to masked secrets (#10659, 13 reactions) and private network access (#39604, 9 reactions) confirms users are deploying these tools in sensitive contexts.

2. **MCP is the new "curl for AI."** Both projects treat MCP integration as a core reliability challenge, not a feature. Expect MCP to become the universal plugin interface for AI agents, with competition shifting from "do you support MCP" to "how robust is your MCP runtime."

3. **Agent autonomy vs. human oversight tension.** Hermes Agent's model_switch tool (#16525) and OpenClaw's exec approval denylist (#6615) represent competing philosophies: empower agents to self-select tools/models vs. build granular control surfaces. Developers should prepare for both models to coexist.

4. **Cron reliability is the canary in the coal mine.** If agents cannot reliably execute scheduled tasks, they cannot be trusted with unsupervised operation. Both projects' cron bugs suggest the entire ecosystem is 6-12 months from production-grade scheduling.

5. **Platform parity is a retention risk.** The oldest and most-voted issues across both projects are platform gaps (Linux/Windows desktop, Android). Users who cannot run agents on their preferred platform will abandon the ecosystem. This is a structural issue that no amount of feature development can fix.

6. **Session state management remains unsolved.** Message duplication, context confusion, group channel resets, and desktop crashes on unexpected data all point to a fundamental architectural challenge: agents need reliable session persistence across channels, reconnects, and multi-turn interactions. This is the "distributed state" problem of the AI agent era.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-06-12

## 1. Today's Overview
The project saw very high activity with 50 issues and 50 PRs updated in the last 24 hours. Of these, 8 issues were closed and 10 PRs were merged or closed. No new releases were published. The community is deeply engaged, reporting a wide range of bugs (especially around desktop client, MCP integration, and provider compatibility) and proposing features like TTS enhancements, cron timezone support, and a model‑switch tool. Several P2‑severity bugs have matching fix PRs already up, indicating a fast response cycle. Overall, the project is in an active development and stabilisation phase with strong contributor momentum.

## 2. Releases
*No new releases were published today.*

---

## 3. Project Progress
**Merged/closed PRs today** (10 total, representative highlights):
- [#44627 – fix(desktop): move tool-row copy control into expanded body](https://github.com/NousResearch/hermes-agent/pull/44627) – Fixes accidental copy activation when clicking the disclosure caret on tool/command rows.
- [#44625 – fix: show codex gpt-5.5 autoraise notice once](https://github.com/NousResearch/hermes-agent/pull/44625) – Adds configurable notice frequency to avoid repeated banner pop‑ups.
- [#44067 – feat: add Rust-backed install manager and bootstrap orchestration](https://github.com/NousResearch/hermes-agent/pull/44067) – New `hermes-manager` for install metadata, lite uninstall, and checksum validation.

**Notable open PRs that address critical bugs** (likely to merge soon):
- [#44577 – fix(model-switch): cache custom provider model discovery](https://github.com/NousResearch/hermes-agent/pull/44577) – Prevents model.options WebSocket timeout by caching HTTP calls.
- [#44578 – fix(dashboard): add PowerShell fallback for process detection on Windows 11](https://github.com/NousResearch/hermes-agent/pull/44578) – Fixes `hermes dashboard --status` and `--stop` on Windows.
- [#44628 – fix(desktop): list markers and quote border follow RTL message direction](https://github.com/NousResearch/hermes-agent/pull/44628) – Follow‑up to the RTL direction fix, ensures list/quote chrome matches text direction.

These PRs show the team is actively addressing the most impactful community‑reported issues.

---

## 4. Community Hot Topics
The most active discussions and reacted topics:

| Issue | Comments | Reactions | Topic & analysis |
|-------|----------|-----------|------------------|
| [#38240](https://github.com/NousResearch/hermes-agent/issues/38240) | 11 | 0 | **Skills index stale/degraded** – Automated probe failure; the skills hub build may be silently failing, causing stale documentation. |
| [#16525](https://github.com/NousResearch/hermes-agent/issues/16525) | 7 | 👍3 | **Expose model_switch as agent-callable tool** – Users want agents to autonomously route tasks based on complexity, not rely on slash commands. High demand signal. |
| [#37812](https://github.com/NousResearch/hermes-agent/issues/37812) (closed) | 7 | 👍4 | **Approvals not rendering in Desktop GUI** – When `approvals.mode: manual`, confirmation prompts didn’t show. Closed with fix; high satisfaction that this was addressed. |
| [#44532](https://github.com/NousResearch/hermes-agent/issues/44532) (closed) | 4 | 0 | **`hermes setup` incomplete on Linux/WSL** – Setup didn’t configure tools API as on macOS. Closed, presumably fixed. |
| [#39901](https://github.com/NousResearch/hermes-agent/issues/39901) | 3 | 0 | **TUI/CLI banner shows MCP servers as “failed” during async connect** – Cosmetic but confusing; servers actually connect fine after a few seconds. |
| [#44562](https://github.com/NousResearch/hermes-agent/issues/44562) | 3 | 0 | **Frontend crash: tapClientLookup Index out of bounds** – Desktop GUI crashes when tools return unexpected data, requiring a reload. |

**Underlying community needs**:
- **Agent autonomy** – The model_switch tool (#16525) would let the agent decide which model to use per task, a clear power‑user request.
- **Reliability of MCP connections** – Banner false‑negatives (#39901) and credential/env propagation (#44548) indicate friction when integrating external servers.
- **Linux/WSL parity** – Multiple Linux‑specific bugs (#44532, #44567, #16425) show the community expects equal experience across platforms.

---

## 5. Bugs & Stability
**P1 (critical spend/billing risk)**
- [#44585](https://github.com/NousResearch/hermes-agent/issues/44585) – Cron jobs can inherit a temporary paid provider state and continue billing after pause/stop. No fix PR yet; urgent.

**P2 (functional break, blocking work)**
- [#44560](https://github.com/NousResearch/hermes-agent/issues/44560) – `model.options` handler blocks on synchronous HTTP calls, causing WebSocket timeout. **Fix PR** [#44577](https://github.com/NousResearch/hermes-agent/pull/44577) open.
- [#44580](https://github.com/NousResearch/hermes-agent/issues/44580) – `hermes update` reports success when desktop rebuild silently fails. No fix PR yet.
- [#44581](https://github.com/NousResearch/hermes-agent/issues/44581) – Desktop folder attach (drag‑and‑drop/copy‑paste) fails. No fix PR yet.
- [#33597](https://github.com/NousResearch/hermes-agent/issues/33597) – Docker restart persists gateway as stopped, preventing s6 auto‑start. No maintainer response visible.
- [#44499](https://github.com/NousResearch/hermes-agent/issues/44499) – Desktop agent ignores configured BrowserOS MCP and uses built‑in browser tools. No fix PR yet.
- [#16425](https://github.com/NousResearch/hermes-agent/issues/16425) – Windows local terminal commands complete without returning output. Open for 6 weeks.
- [#44541](https://github.com/NousResearch/hermes-agent/issues/44541) – Cron delivery to Discord fails with “Session is closed” after reconnect.
- [#40344](https://github.com/NousResearch/hermes-agent/issues/40344) – WebUI profile state.db not created for new profiles; session data leaks to main `state.db`.

**P3 (annoyance or edge case)**
- [#44562](https://github.com/NousResearch/hermes-agent/issues/44562) – tapClientLookup crash (fix in [#44630](https://github.com/NousResearch/hermes-agent/pull/44630) open).
- [#44543](https://github.com/NousResearch/hermes-agent/issues/44543) – `/undo` slash command does not work in Desktop on Windows.
- [#39765](https://github.com/NousResearch/hermes-agent/issues/39765) – HTTP 307 on DeepSeek API calls.
- [#40544](https://github.com/NousResearch/hermes-agent/issues/40544) – Desktop inline edit submits on Enter during IME composition.
- [#41693](https://github.com/NousResearch/hermes-agent/issues/41693) – tapClientLookup crash causing “Reload window” error screen.
- [#43883](https://github.com/NousResearch/hermes-agent/issues/43883) – `web.backend=anysearch` silently ignored, falls back to ddgs (unusable in China).

Many P2 bugs already have matching fix PRs, indicating rapid triage. The P1 billing issue and the P2 gaps (folder attach, Docker restart, Windows terminal) still need attention.

---

## 6. Feature Requests & Roadmap Signals
**High‑demand features** (based on reactions and engagement):
- [#16525](https://github.com/NousResearch/hermes-agent/issues/16525) – **Agent‑callable model_switch tool** (3👍). Likely candidate for next minor release given active discussion.
- [#19863](https://github.com/NousResearch/hermes-agent/issues/19863) – **Telegram table formatting via Mini Apps** (2👍). Underexplored but requested.
- [#44150](https://github.com/NousResearch/hermes-agent/issues/44150) (closed) – **Native RTL support**. Closed after PR [#44596](https://github.com/NousResearch/hermes-agent/pull/44596) merged; follow‑up [#44628](https://github.com/NousResearch/hermes-agent/pull/44628) refines list markers.
- [#44548](https://github.com/NousResearch/hermes-agent/issues/44548) – **Propagate `.hermes/.env` to MCP subprocesses**. Friction point for credential management.

**Features already in open PRs that point to the next version**:
- Auto‑TTS toggle in composer ([#43845](https://github.com/NousResearch/hermes-agent/pull/43845))
- Exponential backoff for credential pool exhaustion ([#43856](https://github.com/NousResearch/hermes-agent/pull/43856))
- Gemma 4 reasoning token normalisation ([#43950](https://github.com/NousResearch/hermes-agent/pull/43950))
- Configurable hindsight prefetch timeout ([#43998](https://github.com/NousResearch/hermes-agent/pull/43998))
- Cron `CRON_TZ=` prefix for DST‑aware scheduling ([#44629](https

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*