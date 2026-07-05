# OpenClaw Ecosystem Digest 2026-07-05

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-05 02:42 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-05

## 1. Today's Overview

OpenClaw is experiencing extremely high activity: **500 issues** and **500 pull requests** were updated in the last 24 hours, with **460 open/active issues** and **343 open PRs**. The project merged or closed **157 PRs** today, demonstrating strong forward momentum despite a heavy bug load. No new releases were published, but the community is actively discussing critical reliability and security concerns. The most pressing topics center on silent subagent failures, message loss across channels, and gaps in policy enforcement — signaling that the project is in a phase of rapid iteration to address core stability while expanding ecosystem features.

## 2. Releases

*None* — no new versions were cut today.

## 3. Project Progress

Today’s merged/closed PRs (157 total) include several impactful fixes:

- **TUI reliability** – PR [#100117](https://github.com/openclaw/openclaw/pull/100117) (closed) fixes an unnecessary `async` boundary in `EmbeddedTuiBackend.handleAgentEvent` that caused swallowed exceptions.
- **Policy classification** – PR [#99686](https://github.com/openclaw/openclaw/pull/99686) (closed) introduces structured `policy.fixRecommendation` metadata, classifying doctor fixes as automatic, review-required, or manual.
- **CLI completion fixes** – Multiple PRs ([#99491](https://github.com/openclaw/openclaw/pull/99491), [#99431](https://github.com/openclaw/openclaw/pull/99431), [#99427](https://github.com/openclaw/openclaw/pull/99427), [#99419](https://github.com/openclaw/openclaw/pull/99419)) resolve missing command alias tab-completion for all four supported shells.
- **Agents: spill-file preservation** – PR [#100135](https://github.com/openclaw/openclaw/pull/100135) (closed) preserves live exec spill-file pointers through history elision and handles `web_fetch` output truncation.
- **Feishu channel improvements** – PR [#99936](https://github.com/openclaw/openclaw/pull/99936) (closed) prevents reasoning placeholder leaks in mention-only messages; PR [#98320](https://github.com/openclaw/openclaw/pull/98320) (open) improves media reply fallback.
- **OpenShell sandbox env config** – PR [#96073](https://github.com/openclaw/openclaw/pull/96073) (open) adds non-secret environment variable passthrough for sandbox creation.
- **Memory dreaming scoping** – PR [#100057](https://github.com/openclaw/openclaw/pull/100057) (open) adds an optional agent allowlist for memory-core dreaming sweeps.

Key open PRs nearing completion include the **assistant cross-conversation memory** feature ([#100140](https://github.com/openclaw/openclaw/pull/100140), size XL), **onboarding streamline** ([#93265](https://github.com/openclaw/openclaw/pull/93265)), and **smart watch deferral** to avoid crash-loops mid-rebuild ([#99972](https://github.com/openclaw/openclaw/pull/99972)).

## 4. Community Hot Topics

The most active discussions center on **reliability, security, and missing UX polish**:

| Issue | Comments | 👍 | Underlying Need |
|-------|----------|---|----------------|
| [Subagent completion silently lost (#44925)](https://github.com/openclaw/openclaw/issues/44925) | 20 | 1 | Reliable sub‑agent orchestration with retry/notification on timeout |
| [Centralized filename encoding utility (#48788)](https://github.com/openclaw/openclaw/issues/48788) | 18 | 1 | Proper multi‑encoding Content‑Disposition handling across channels |
| [Signal daemon restart race (#22676)](https://github.com/openclaw/openclaw/issues/22676) | 17 | 0 | Prevent orphaned processes and port conflicts on SIGUSR1 restart |
| [Control UI device identity (#32473)](https://github.com/openclaw/openclaw/issues/32473) – *closed* | 17 | 5 | Secure access to control UI without HTTPS/localhost |
| [Community Skill Development & ClawHub (#50090)](https://github.com/openclaw/openclaw/issues/50090) | 15 | 2 | A viable skill ecosystem – documentation, testing, and discoverability gaps |
| [Safeguard compaction model mismatch (#57901)](https://github.com/openclaw/openclaw/issues/57901) | 14 | 1 | Compaction config ignored; uses session model instead |
| [Steer mode mid-turn injection (#48003)](https://github.com/openclaw/openclaw/issues/48003) | 14 | 3 | Messages queued mid‑turn not injected until turn completes |
| [gh-issues skill prompt injection (#45740)](https://github.com/openclaw/openclaw/issues/45740) | 14 | 1 | Untrusted GitHub issue bodies injected directly into sub‑agent prompts (security risk) |
| [CLI-backed helper path bypass (#57326)](https://github.com/openclaw/openclaw/issues/57326) | 13 | 1 | Remaining code paths still bypass proper CLI dispatch for certain models |
| [XDG_CONFIG_HOME not processed (#53628)](https://github.com/openclaw/openclaw/issues/53628) | 13 | 1 | Environment variable not expanded when installing skills |

The community is clearly demanding **defense in depth** — users want silent failures to become loud, multi-channel encoding to be robust, and all security boundaries (prompt injection, scope stripping, bot allowlisting) to be enforced mechanically rather than by convention.

## 5. Bugs & Stability

**Critical (P0)**:
- [#99594](https://github.com/openclaw/openclaw/issues/99594) – Cloud instance falsely shows "out of credits" with $109 balance and active Pro plan. **Fix**: being investigated; no linked PR yet.
- [#48920](https://github.com/openclaw/openclaw/issues/48920) – Live docs reference `IsolatedSessions` not yet in released version. **Fix**: none; documentation/release alignment.

**High (P1)**:
- **Subagent silent loss** ([#44925](https://github.com/openclaw/openclaw/issues/44925)) – Multiple failure modes (E31, E42, E45) where results vanish without retry or notification. Has linked open PR.
- **Signal daemon restart race** ([#22676](https://github.com/openclaw/openclaw/issues/22676)) – Orphaned processes and port/ lock conflicts on SIGUSR1. Open PR linked.
- **Steer mode not injecting mid-turn** ([#48003](https://github.com/openclaw/openclaw/issues/48003)) – Messages queued until turn end; root cause in `KeyedAsyncQueue`. Open PR exists.
- **CLI-backed helper paths bypass** ([#57326](https://github.com/openclaw/openclaw/issues/57326)) – Some paths still go through embedded/API provider instead of `runCliAgent()`. No fix PR linked.
- **Cron sessions hallucinate** ([#49876](https://github.com/openclaw/openclaw/issues/49876)) – LLM fabricates output on tool failure instead of failing cleanly. Security/trust issue. No linked PR.
- **Force reply to originating channel** ([#54531](https://github.com/openclaw/openclaw/issues/54531)) – Responses visible in UI but not delivered to Telegram/Discord/WhatsApp. Open PR?
- **Orphaned lock files** ([#49603](https://github.com/openclaw/openclaw/issues/49603)) – Lock files not cleared when PID matches current process on gateway restart. Open PR.
- **ACP parent session stuck** ([#52249](https://github.com/openclaw/openclaw/issues/52249)) – Parent session remains non-responsive after child completes. Root cause in relay logic. No fix PR.
- **Session lane starvation** ([#54488](https://github.com/openclaw/openclaw/issues/54488)) – Followup drain blocks inbound dispatch for 20-30 min. No linked PR.

**Moderate (P2)** – many, including:
- Memory management chaos ([#43747](https://github.com/openclaw/openclaw/issues/43747)) – inconsistent chunking/embedding across users.
- Hardcoded workspace path ([#51429](https://github.com/openclaw/openclaw/issues/51429)) – `/Users/wangtao` hardcoded and merged.
- Feishu media reply fallback ([#98311](https://github.com/openclaw/openclaw/issues/98311)) – closed by PR #98320 today.

**Regression patterns** – several issues marked "regression" in the top 50, including #32473 (closed), #43747, #45494 (cron timeout), #45765 (OPENCLAW_HOME nesting), and #51396 (scope stripping). This suggests recent releases introduced unintended side effects that are being actively reported.

## 6. Feature Requests & Roadmap Signals

Today’s top feature-oriented discussions point to several priorities that could land in the next minor release:

| Feature | Issue | Likelihood |
|---------|-------|------------|
| **Community Skill Development & ClawHub** – documentation, testing, discoverability | [#50090](https://github.com/openclaw/openclaw/issues/50090) | High – ecosystem growth is strategic |
| **Pre-response enforcement hooks** – hard gates for mandatory tool calls | [#13583](https://github.com/openclaw/openclaw/issues/13583) | Medium – security-critical, but requires architectural change |
| **WhatsApp backfill after reconnection** | [#50093](https://github.com/openclaw/openclaw/issues/50093) | Medium – common pain point for WhatsApp users |
| **Filesystem sandboxing config** (`tools.fileAccess`) | [#7722](https://github.com/openclaw/openclaw/issues/7722) | High – popular request (4 👍), clear use case |
| **Skill priority configuration** | [#50199](https://github.com/openclaw/openclaw/issues/50199) | Medium – overlapping skill selection |
| **Gateway lifecycle hooks** (onSubagentComplete, etc.) | [#43454](https://github.com/openclaw/openclaw/issues/43454) | Medium – enables external automation |
| **Configurable mediaLocalRoots** for image tool | [#47856](https://github.com/openclaw/openclaw/issues/47856) | High – blocks iMessage attachment use |
| **System event priority/bypass-queue mode** | [#50739](https://github.com/openclaw/openclaw/issues/50739) | Medium – reliability for alerts |
| **YAML config support** | [#45758](https://github.com/openclaw/openclaw/issues/45758) | Low – nice-to-have, no maintainer traction |

A notable open PR today — **[feat: let assistants remember across private conversations (#100140)](https://github.com/openclaw/openclaw/pull/100140)** — proposes a major memory scoping change. If merged, it would allow personal assistants to share context across Telegram DMs, WebUI, TUI, etc., which addresses a very common user desire.

## 7. User Feedback Summary

**Pain points (frequent complaints):**
- **Silent failures** – “Subagent completion silently lost” (#44925), “Cron sessions deliver hallucinated output” (#49876), “No retry, no notification, no auto-restart” – trust is eroded.
- **Message loss** – Across Telegram (#44925, #51628), WhatsApp (#50093), Discord (#54931) – users report replies never delivered or duplicated.
- **Configuration drift** – “Run clawdbot doctor --fix” on every startup (#50561); `openclaw status` falsely reports memory unavailable (#57256).
- **Hardcoded paths** – A Chinese user discovered that `/Users/wangtao` was hardcoded into the codebase and merged (#51429) – a serious quality signal.
- **Memory inconsistency** – Multiple users report memory chunking/embedding behavior differs across installations (#43747).
- **Documentation out of sync** – Live docs reference features not yet released (#48920); PR #100142 aims to rewrite docs grounded in current source.

**Positive signals:**
- High engagement with feature requests (e.g., 4 👍 on filesystem sandboxing, 3 👍 on steer mode fix, 5 👍 on control UI issue).
- Community members filing detailed bug reports with reproduction steps – indicates a invested user base.
- Several first-time contributors submitting PRs (e.g., #100117, #99431, #99427) – healthy open-source pipeline.

**Unmet expectations:**
- Users expect “safe” fixes to be auto-applied (#50561).
- Users expect skill development to be as easy as writing a `SKILL.md` but find the gap between promise and reality wide (#50090).

## 8. Backlog Watch

Issues and PRs that have been open for extended periods without maintainer response, despite high importance:

| Item | Opened | Last Update | Status |
|------|--------|-------------|--------|
| [Filesystem Sandboxing (#7722)](https://github.com/openclaw/openclaw/issues/7722) – P2, 4 👍, needs product decision | Feb 3 | Jul 5 | Awaiting maintainer review |
| [Pre-response enforcement hooks (#13583)](https://github.com/openclaw/openclaw/issues/13583) – P2, 2 👍, security | Feb 10 | Jul 4 | Awaiting maintainer review |
| [Signal daemon restart race (#22676)](https://github.com/openclaw/openclaw/issues/22676) – P1, 17 comments, linked PR open | Feb 21

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw & Hermes Agent

**Date: 2026-07-05**  
**Prepared for: Technical decision-makers and AI agent developers**

---

## 1. Ecosystem Overview

The open‑source personal AI assistant ecosystem is experiencing a surge in both adoption and refinement. Projects like OpenClaw and Hermes Agent are evolving from proof‑of‑concept agents into production‑grade platforms, with communities demanding reliability, security, and multi‑channel support. Competition is driving rapid iteration on core stability (silent failure elimination, message delivery guarantees) and ecosystem expansion (skills, memory backends, new messaging channels). The landscape is splitting between broad, feature‑rich reference platforms (OpenClaw) and streamlined, opinionated assistants (Hermes Agent), both responding to the same underlying user needs: trustworthy autonomy and seamless integration with daily tools.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues updated (24h)** | ~500 | ~50 |
| **Pull requests updated (24h)** | ~500 | ~50 |
| **Open/active issues** | 460 | *Not reported explicitly* |
| **Open pull requests** | 343 | *Not reported explicitly* |
| **PRs merged/closed (24h)** | 157 | 8 |
| **New releases today** | 0 | 0 |
| **Critical (P0) bugs** | 2 | 2 (Python 3.14 crash, Telegram token leak) |
| **Health assessment** | High activity, heavy bug load; some resolutions advancing | Lower activity but faster triage; critical bugs being fixed within hours |

*Both projects show strong community engagement. OpenClaw’s scale is an order of magnitude larger, but it also carries a proportionally larger stability debt.*

---

## 3. OpenClaw’s Position

**Advantages over peers:**
- **Ecosystem breadth**: Supports Feishu, Discord, Telegram, WhatsApp, WebUI, TUI, and CLI – far more channels than Hermes Agent.
- **Advanced orchestration**: Sub‑agent management, cross‑conversation memory (PR #100140), memory dreaming sweeps, and policy enforcement hooks.
- **Community size**: 500 issues vs Hermes’ 50; 460 open issues indicate a massive user base filing reports and feature requests.
- **Active contribution pipeline**: 157 PRs merged today, including first‑time contributors – a healthy open‑source funnel.

**Technical approach differences:**
- OpenClaw uses a **multi‑agent architecture** with sub‑agents, ACP (Agent Communication Protocol), and a dedicated TUI/embedded backend.
- It employs **policy‑driven fixes** (`policy.fixRecommendation` metadata) and **secret‑scoped configuration** (non‑secret passthrough in sandbox).
- Memory management is more complex: chunking/embedding across users, dreaming, and allowlisting.

**Community size comparison:**
- OpenClaw’s issue tracker alone dwarfs Hermes’ (500 vs 50 updates/day). This suggests a community at least 5–10× larger, but also a higher noise‑to‑signal ratio.
- OpenClaw has **157 merged PRs/day** vs Hermes’ 8 – reflecting a larger team or more contributors.

---

## 4. Shared Technical Focus Areas

The following requirements emerged across both projects:

| Requirement | OpenClaw | Hermes Agent |
|-------------|----------|--------------|
| **Silent failure elimination** | Subagent loss (#44925), cron hallucination (#49876) | Background session context bug (#47268, now fixed) |
| **Multi‑platform messaging** | Feishu, Discord, Telegram, WhatsApp | Rocket Chat (#3725), WhatsApp setup wizard (#58041) |
| **Memory & context persistence** | Cross‑conversation memory (#100140), memory dreaming scoping (#100057) | Standalone memory provider `scope‑recall` (#42864), per‑session workspace (#40297) |
| **Security & prompt injection** | gh‑issues skill injection (#45740), steer‑mode injection (#48003) | Telegram token leak (#58594), credential pool confusion (#40960) |
| **Sandboxing & file access** | Filesystem sandboxing config (#7722), OpenShell env passthrough (#96073) | Tool‑result compaction (#58610) |
| **Desktop/TUI polish** | Embedded TUI reliability (#100117), smart‑watch deferral (#99972) | Per‑session workspace (#40297), emoji picker (#58617), unbounded process spawning (#58619) |
| **Documentation alignment** | Live docs reference unreleased features (#48920) | `AGENTS.md` rewrite to compact bootloader (#58605) |
| **Skill ecosystem** | ClawHub documentation and discoverability (#50090) | Skill instruction enforcement (#58569), redundant skill confusion (#27103) |

**Key insight:** *Both communities are converging on the same pain points – message loss, hallucination, misconfigured error handling, and ecosystem friction. These are not project‑specific issues but industry‑wide challenges for autonomous agents.*

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Target user** | Power users, developers building custom agent workflows | Personal assistant for daily productivity, desktop‑first |
| **Architecture** | Multi‑agent (sub‑agents, ACP, gateway, sidecar) | Simpler single‑agent back‑end with modular adapters (Anthropic, Codex, etc.) |
| **Channel support** | Extensive (Feishu, Telegram, Discord, WhatsApp, TUI, WebUI) | Moderate (Telegram, Desktop, WebUI, TUI); Rocket Chat requested |
| **Memory model** | Complex: per‑user chunking, dreaming, allowlists, cross‑conversation | Simpler: `scope‑recall` plugin, per‑session workspace |
| **Policy & security** | Formal policy classification (auto, review, manual) + enforcement hooks | Basic credential management; no apparent policy engine |
| **Release cadence** | Rapid changes (157 PRs/day) but no release today | Fewer changes but more stable; critical bugs fixed within hours |
| **Community engagement** | Very high – lots of bugs but also lots of fixes | Moderate – focused discussions, quicker triage |

**Bottom line:** *OpenClaw is the “Android of AI agents” – open, flexible, but sometimes messy. Hermes Agent is the “macOS” – opinionated, polished, but with a narrower scope.*

---

## 6. Community Momentum & Maturity

**Activity tiers (based on issue/PR volume and update frequency):**
- **Rapid iteration / high churn:** **OpenClaw** – 500 issues/day, 157 PRs merged. Heavy bug backlog indicates fast growth but also instability. Signal: the project is in a “quantity over quality” phase, aggressively adding features while fixing regressions.
- **Steady maturation:** **Hermes Agent** – 50 issues/day, 8 PRs merged. Lower volume but higher resolution rate for critical bugs. Signal: the project is stabilizing after a growth spurt, focusing on reliability and usability.

**Stabilization signals:**
- OpenClaw: Multiple regression tags (#32473, #43747, #45494), suggesting recent releases broke previously working features.
- Hermes Agent: Quick closure of session‑context bug (#47268) and emoji picker (#58617); active development on Python 3.14 compatibility.

**Community health:**
- Both projects have first‑time contributors, detailed bug reports, and invested users.
- OpenClaw’s backlog includes items open for months without maintainer response (e.g., #7722, #13583), indicating capacity strain.
- Hermes Agent’s top feature request (#3725, Rocket Chat) has been open since March without official response – similar neglect pattern.

---

## 7. Trend Signals for AI Agent Developers

The combined community feedback reveals several industry‑wide trends:

1. **Trust is the #1 adoption barrier.** Users are vocal about silent failures, hallucinated outputs, and message loss. Projects that cannot provide *guaranteed delivery* and *auditable failure modes* will lose trust. Expect agent orchestration frameworks to adopt circuit‑breakers, retry‑with‑notification, and “fail loud” policies.

2. **Multi‑channel is table stakes.** Users want a single agent that works across Telegram, WhatsApp, Discord, Slack, Rocket Chat, Feishu, and email. A project supporting only one or two channels will struggle to gain traction.

3. **Memory persistence without fragmentation.** Cross‑conversation memory (OpenClaw’s #100140) and standalone memory providers (Hermes’ `scope‑recall`) point to a demand for *unified, user‑controlled memory* that works across devices and sessions.

4. **Security must be mechanical, not conventional.** Prompt injection in GitHub issues (#45740), token leaks in logs (#58594), and un‑sandboxed file access (#7722) are being discovered the hard way. Future agents will need **policy‑enforced boundaries** (e.g., “this skill cannot access the filesystem”) and **outbound request sanitization**.

5. **Sandboxed execution is non‑negotiable.** Both communities are pushing for filesystem sandboxing, environment passthrough controls, and tool‑result compaction. Developers should plan for a future where agents run in lightweight containers or WASM runtimes.

6. **Self‑diagnosis and auto‑repair.** Users expect `doctor --fix` to actually fix things (#50561), not just report issues. Agents that can self‑heal (e.g., auto‑restart, lock‑file cleanup, recompute missing memory indices) will reduce operational burden.

7. **Skill ecosystem needs investment.** OpenClaw’s ClawHub (#50090) and Hermes’ confusion with redundant skills (#27103) highlight that simply allowing third‑party skills is not enough – discoverability, testing frameworks, and conflict resolution are required for a healthy ecosystem.

**Value for AI agent developers:**
- **Invest early in observability**: structured logging, failure classification, and retry policies.
- **Design for multi‑channel from day one**: abstract transport layer to add channels without core changes.
- **Make memory a first‑class concept**: user‑scoped, sandboxed, exportable.
- **Treat security as a product feature**, not an afterthought: enforce policy mechanically, not through documentation.
- **Plan for ecosystem growth**: skills should be versioned, tested, and conflict‑detectable.

---

*Report generated from 2026-07-05 community digests. Data reflects single‑day snapshot; long‑term trends may vary.*

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-05

## Today’s Overview

Activity remains **high** with 50 issues and 50 pull requests updated in the last 24 hours. The community is engaged across feature requests, bug reports, and code contributions. No new releases were published today, but the project is moving quickly on multiple fronts: **8 issues were closed** (including a critical background-review session‑context bug) and **8 PRs were merged/closed** (test isolation, warning gating, documentation cleanup). Several high‑priority bugs — including a Python 3.14 compatibility crash and a Telegram token leak — already have fix PRs open. The overall project health appears **robust**, with active triage and a steady stream of community‑driven enhancements.

## Releases

*None today.*

## Project Progress

The following pull requests were merged or closed today, reflecting concrete progress:

| PR | Description | Status |
|----|-------------|--------|
| [#58613](https://github.com/NousResearch/hermes-agent/pull/58613) | **Fix:** Isolate Anthropic adapter tests from macOS Keychain credentials. | **Closed** |
| [#58618](https://github.com/NousResearch/hermes-agent/pull/58618) | **Fix:** Gate Codex gpt‑5.5 autoraise warning with a configurable toggle. | **Closed** |
| [#58605](https://github.com/NousResearch/hermes-agent/pull/58605) | **Docs:** Shrink `AGENTS.md` to a compact bootloader, route detail to canonical docs. | **Closed** |

Additionally, issues [#47268](https://github.com/NousResearch/hermes-agent/issues/47268) (background‑review session context bug) and [#58617](https://github.com/NousResearch/hermes-agent/issues/58617) (macOS emoji picker not accepted in TUI) were closed, indicating active bug squashing.

## Community Hot Topics

The most discussed and reacted‑to issues highlight strong demand for **multi‑platform messaging** and **desktop usability** improvements:

- **[#3725 – Rocket Chat support](https://github.com/NousResearch/hermes-agent/issues/3725)**  
  *13 comments, 12 👍* – users clearly want Rocket Chat as a first‑class message channel. The request is marked **P3** but has been open since March.

- **[#42864 – `scope-recall` standalone memory provider](https://github.com/NousResearch/hermes-agent/issues/42864)**  
  *6 comments* – a community‑built memory plugin seeks official recognition. Signals interest in modular, auditable memory backends.

- **[#40297 – Desktop: per‑session workspace selection](https://github.com/NousResearch/hermes-agent/issues/40297)**  
  *5 comments, 9 👍* – users want to switch project directories mid‑session, not only at launch. A quality‑of‑life gap for long‑lived desktop use.

- **[#47268 – Background review shares session context](https://github.com/NousResearch/hermes-agent/issues/47268)**  
  *3 comments* – this bug caused premature 11–77 character responses. Now closed; community engagement helped identify the root cause (shared session ID).

- **[#40960 – Credential pool exhaustion gives misleading 401](https://github.com/NousResearch/hermes-agent/issues/40960)**  
  *3 comments* – a real pain point for heavy users: empty API keys from exhausted pools produce confusing “401 Unauthorized” instead of a proper quota error.

- **[#56004 – Qwen3.6 / vLLM: prior‑turn thinking context lost](https://github.com/NousResearch/hermes-agent/issues/56004)**  
  *3 comments, 2 👍* – multi‑turn reasoning is broken when using Qwen with vLLM; the `preserve_thinking` flag is stripped on replay.

**Underlying needs:** Users are pushing for broader platform coverage (Rocket Chat, WhatsApp), better session state management (workspace, context isolation), and robust multi‑turn reasoning across different model providers.

## Bugs & Stability

The following bugs were reported or updated today, sorted by estimated severity:

| Severity | Issue | Description | Fix PR Open? |
|----------|-------|-------------|--------------|
| **High** | [#58596](https://github.com/NousResearch/hermes-agent/issues/58596) | `DaemonThreadPoolExecutor` crashes on **Python 3.14** (removed internal `_initializer`/`_initargs`). Breaks all concurrent features. | [#57459](https://github.com/NousResearch/hermes-agent/pull/57459) |
| **High** | [#58594](https://github.com/NousResearch/hermes-agent/issues/58594) | **Telegram bot tokens leaked** in transport error logs (token in URL path). | [#58594](https://github.com/NousResearch/hermes-agent/pull/58594) |
| **Medium** | [#58581](https://github.com/NousResearch/hermes-agent/issues/58581) | `vision_analyze` auxiliary fallback not working with DeepSeek primary model – first call fails 400. | None yet |
| **Medium** | [#57948](https://github.com/NousResearch/hermes-agent/issues/57948) | `vision_analyze` first call returns 400 when main model lacks vision support; second call succeeds. | None yet |
| **Medium** | [#58619](https://github.com/NousResearch/hermes-agent/issues/58619) | Desktop spawns unbounded `serve` processes on reconnection – no `--replace` flag cleanup. | None yet |
| **Low** | [#58404](https://github.com/NousResearch/hermes-agent/issues/58404) | Desktop chat sessions incorrectly tagged as “TUI”, receiving terminal‑specific guidance. | None yet |
| **Low** | [#58617](https://github.com/NousResearch/hermes-agent/issues/58617) | macOS emoji picker input silently dropped in TUI. | **Closed** (no PR, likely quick fix) |

Other notable bugs:  
- [#58569](https://github.com/NousResearch/hermes-agent/issues/58569) – Agent loads skills but treats instructions as advisory (duplicate of #54256).  
- [#58620](https://github.com/NousResearch/hermes-agent/issues/58620) – Cron tick `lock_fd` can leak file descriptors on lock contention (PR #58620 open).  
- [#58622](https://github.com/NousResearch/hermes-agent/issues/58622) – Gateway proxy SSE buffer unbounded memory growth (PR #58622 open).  
- [#58609](https://github.com/NousResearch/hermes-agent/issues/58609) – Anthropic adapter tests not isolated from macOS Keychain (fixed in PR #58613, closed today).

## Feature Requests & Roadmap Signals

Several feature ideas landed today, pointing toward **provider expansion** and **desktop polish** in upcoming releases:

- **[#58603](https://github.com/NousResearch/hermes-agent/issues/58603) / [#58606](https://github.com/NousResearch/hermes-agent/pull/58606) – Groq & Cerebras providers** – proposed addition of two free‑tier OpenAI‑compatible endpoints. Already has a PR.
- **[#58571](https://github.com/NousResearch/hermes-agent/issues/58571) – Eden AI provider** – multi‑provider aggregator (25+ upstreams). Low effort, high value.
- **[#58041](https://github.com/NousResearch/hermes-agent/issues/58041) – `hermes whatsapp setup` wizard** – one‑command WhatsApp configuration (currently 4+ manual steps).
- **[#49383](https://github.com/NousResearch/hermes-agent/issues/49383) – Voice wake word “Hey Hermes”** – hands‑free invocation for Desktop.
- **[#58370](https://github.com/NousResearch/hermes-agent/issues/58370) – Fable copilot** – expensive model only for critical planning/review checkpoints (closed as feature idea).
- **[#58610](https://github.com/NousResearch/hermes-agent/pull/58610) – Compact large tool results behind handles** – reduces history size by storing full artifacts out‑of‑band.
- **[#57051](https://github.com/NousResearch/hermes-agent/pull/57051) – Aurora dark frosted‑glass dashboard theme** – new visual style for Hermes Web UI.

**Predictions for next release:** The provider additions (Groq, Cerebras, possibly Eden AI) are low‑risk and already have PRs, so they are likely candidates. The Telegram token leak fix (#58594) and Python 3.14 compatibility (#57459) are critical and will almost certainly be included. The per‑session workspace (#40297) may be further out.

## User Feedback Summary

**Pain points expressed today:**

- Multiple users report **misleading error codes** when credential pools are exhausted (#40960) – a debugging nightmare.
- **Desktop‑as‑TUI** misclassification confuses session guidance (#58404).
- **Vision fallback failures** with DeepSeek (#58581, #57948) frustrate users who rely on multi‑modal pipelines.
- **Session context sharing** between background review and main loop (#47268, now fixed) caused premature truncated responses – a reliability issue.
- **Model switching changes behavior** dramatically and redundant skills confuse results (#27103).

**Use‑case signals:**

- Strong desire for **messaging platform diversity** (Rocket Chat #3725, WhatsApp #58041, Telegram integration already exists).
- **Memory and skill management** is a recurring theme: standalone memory providers (#42864), skill instruction enforcement (#58569).
- **Desktop app maturity** is a growing focus: workspace selection, reconnection cleanup, voice wake word, tray minimization (#58621).

**Overall sentiment** remains positive – users are actively contributing features, reporting bugs constructively, and engaging in design discussions. The rapid response to critical bugs (e.g., Python 3.14 crash, Telegram token leak) shows maintainer responsiveness.

## Backlog Watch

The following issues have gone **weeks without maintainer interaction** yet have significant community engagement or importance:

| Issue | Created | Comments | Last Updated | Why Watch |
|-------|---------|----------|--------------|-----------|
| [#3725](https://github.com/NousResearch/hermes-agent/issues/3725) – Rocket Chat support | 2026‑03‑29 | 13 | 2026‑07‑05 | Long‑standing top‑voted feature request; no official response. |
| [#42864](https://github.com/NousResearch/hermes-agent/issues/42864) – `scope-recall` memory provider | 2026‑06‑09 | 6 | 2026‑07‑05 | RFC show‑and‑tell awaiting maintainer decision. |
| [#40297](https://github.com/NousResearch/hermes-agent/issues/40297) – Desktop per‑session workspace | 2026‑06‑06 | 5 | 2026‑07‑05 | Popular desktop improvement; no triage label. |
| [#27103](https://github.com/NousResearch/hermes-agent/issues/27103) – Redundant skills, model switching deviation | 2026‑05‑16 | 3 | 2026‑07‑05 | Unresolved behavioral inconsistency. |
| [#34143](https://github.com/NousResearch/hermes-agent/issues/34143) – Profile Codex auth ignores global credentials | 2026‑05‑28 | 2 | 2026‑07‑05 | Auth reliability issue, may affect enterprise users. |
| [#31874](https://github.com/NousResearch/hermes-agent/issues/31874) – Web UI process D‑state, Gateway crashes (Chinese) | 2026‑05‑25 | 1 | 2026‑07‑05 | Detailed multi‑problem report from

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*