# OpenClaw Ecosystem Digest 2026-06-28

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-28 03:25 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-06-28

## 1. Today’s Overview

OpenClaw remains highly active with 500 issues and 500 pull requests updated in the last 24 hours. However, only 13 issues were closed and 40 PRs merged/closed, indicating a large and growing backlog. The project faces significant stability challenges: several critical memory leaks (P0/P1), persistent agent response failures, and regression in coding tasks dominate the open issue list. Community demand for per-agent configuration and multi-agent enhancements continues to rise, but many feature requests remain stalled in maintainer review. The absence of a new release (latest remains 2026.4.x) suggests focus is on bug fixing and internal refactoring rather than shipping new versions.

## 2. Releases

**No new releases** — the latest version remains the 2026.4.x series (e.g., 2026.4.14, 2026.4.2). No releases were published today.

## 3. Project Progress

40 pull requests were merged or closed today, addressing several high-priority issues:

- **Lock contention fixes**: [#95833](https://github.com/openclaw/openclaw/issues/95833) (subagent abort-settle `.jsonl.lock` leak) and [#95915](https://github.com/openclaw/openclaw/issues/95915) (heap not released on embedded run abort) were both closed, resolving persistent session-breaking lock issues.
- **Telegram streaming improvement**: [#96317](https://github.com/openclaw/openclaw/pull/96317) adds `appendMode` to preserve message history during streaming updates, fixing a common user complaint.
- **Memory index performance**: [#96184](https://github.com/openclaw/openclaw/pull/96184) prevents large legacy memory indexes from stalling and restarting.
- **Speculative optimization PRs**: A batch of micro-optimizations from contributor `ly-wang19` (e.g., [#97206](https://github.com/openclaw/openclaw/pull/97206), [#97205](https://github.com/openclaw/openclaw/pull/97205), [#97207](https://github.com/openclaw/openclaw/pull/97207)) reduce unnecessary allocations in memory-core and talk processing.
- **Major refactoring open**: [#96625](https://github.com/openclaw/openclaw/pull/96625) (flip sessions and transcripts to SQLite storage) is a large XL‑sized PR still awaiting author; if merged, it will fundamentally change storage architecture.

## 4. Community Hot Topics

The most active issues (by comment count, 15 comments each) reveal deep user frustration:

- **#58450** ([🐚 platinum hermit](https://github.com/openclaw/openclaw/issues/58450)) — “Agent can promise a later follow-up without starting any actual follow-up action” (3 👍). The agent ends a turn by saying it will follow up but never does. This is a **trust-breaking UX bug** that has been open since March 31 without a fix PR.
- **#92201** ([🦞 diamond lobster](https://github.com/openclaw/openclaw/issues/92201)) — “Embedded runner: freshly streamed thinking signatures intermittently invalid on replay (Anthropic); recovery wrapper never fires”. This causes silent message loss in Slack and Telegram integrations.
- **#91588** ([P0, 🐚 platinum hermit](https://github.com/openclaw/openclaw/issues/91588)) — “Critical: Gateway Memory Leak — RSS grows from 350MB to 15.5GB over days”. The most severe stability issue, with 14 comments and widespread impact.
- **#65161** ([🐚 platinum hermit](https://github.com/openclaw/openclaw/issues/65161)) — “Heartbeat isolated mode: cadence stalls, ‘heartbeat last’ mislabels exec‑events”. A regression in isolated mode first reported April 12.
- **#62505** ([🦞 diamond lobster](https://github.com/openclaw/openclaw/issues/62505)) — “Coding Agent never completes anything (worked in 2026.4.2 and earlier)”. A major regression blocking coding workflows.

**Most reacted issue**: [#63829](https://github.com/openclaw/openclaw/issues/63829) (Per‑agent memory-wiki vault configuration) with 9 👍, reflecting strong multi-agent demand.

**PRs with high activity**: Several PRs carry the `mantis: telegram-visible-proof` label (e.g., [#75469](https://github.com/openclaw/openclaw/pull/75469), [#71839](https://github.com/openclaw/openclaw/pull/71839), [#96625](https://github.com/openclaw/openclaw/pull/96625)), indicating user-driven testing for Telegram channel improvements.

## 5. Bugs & Stability

The project has multiple critical and high‑severity bugs without fix PRs:

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | **P0** | Gateway memory leak (350 MB → 15.5 GB) causing OOM crashes | No |
| [#63216](https://github.com/openclaw/openclaw/issues/63216) | **P1** | Repeated hard context-overflow resets on same session, even with high compaction headroom | No |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | **P1** | Coding agent never completes tasks (regression) | No (linked PR open, but no fix merged) |
| [#92201](https://github.com/openclaw/openclaw/issues/92201) | **P1** | Invalid thinking signatures on replay, recovery never fires | No |
| [#55334](https://github.com/openclaw/openclaw/issues/55334) | **P1** | `sessions.json` unbounded growth → gateway OOM | No |
| [#65161](https://github.com/openclaw/openclaw/issues/65161) | **P1** | Heartbeat cadence stalls in isolated mode | No |
| [#67419](https://github.com/openclaw/openclaw/issues/67419) | **P2** | Bootstrap files re-injected every turn, wasting 20–30% tokens | No |
| [#66443](https://github.com/openclaw/openclaw/issues/66443) | **P1** | Overflow recovery duplicates `role=user` messages, amplifying transcript growth | No |

Two subagent lock issues were closed today ([#95833](https://github.com/openclaw/openclaw/issues/95833), [#95915](https://github.com/openclaw/openclaw/issues/95915)), but the underlying systemic lock‑contention pattern remains a concern. New today: [#97234](https://github.com/openclaw/openclaw/pull/97234) aims to fix proxy `NO_PROXY` matching, addressing a proxy regression.

## 6. Feature Requests & Roadmap Signals

Several high-demand features continue to await maintainer decisions:

- **Per-agent memory‑wiki vault** ([#63829](https://github.com/openclaw/openclaw/issues/63829), 9 👍) — demanded for multi-agent isolation.
- **Per-agent TTS/STT overrides** ([#66252](https://github.com/openclaw/openclaw/issues/66252)) — enables multi-language agent setups.
- **Anthropic advisor tool support** ([#63930](https://github.com/openclaw/openclaw/issues/63930)) — would unlock beta server‑side tooling.
- **MathJax/LaTeX in Control UI** ([#42840](https://github.com/openclaw/openclaw/issues/42840), 7 👍) — important for scientific/technical users.
- **Multi-agent collaboration enhancement** ([#35203](https://github.com/openclaw/openclaw/issues/35203)) — ambitious RFC for capability profiling, blackboard, token governance.

**Likely next‑version inclusions**: The SQLite storage refactor ([#96625](https://github.com/openclaw/openclaw/pull/96625)) is the largest PR open; if it lands, it will fix many session‑management bugs. The wait‑for‑result hook endpoint ([#67433](https://github.com/openclaw/openclaw/pull/67433)) appears close to merge. Per‑agent web_fetch SSRF policy ([#67421](https://github.com/openclaw/openclaw/pull/67421)) has a maintainer‑approved proof.

## 7. User Feedback Summary

**Pain points expressed directly by users:**

- **Memory leaks** are the top frustration — multiple reports of OOM crashes after days of uptime (e.g., [#91588](https://github.com/openclaw/openclaw/issues/91588), [#54155](https://github.com/openclaw/openclaw/issues/54155)). Users say “requires periodic forced restarts”.
- **Agent unreliability**: “Coding Agent never completes anything” ([#62505](https://github.com/openclaw/openclaw/issues/62505)) and “agent promises follow-up but doesn’t start” ([#58450](https://github.com/openclaw/openclaw/issues/58450)) erode trust.
- **Hardcoded paths** in code ([#51429](https://github.com/openclaw/openclaw/issues/51429)) — a Chinese speaker reports `/Users/wangtao` hardcoded into a release, causing workspaces to be created in an unrelated home directory. This is a **quality‑assurance failure**.
- **Token waste**: Users note that 20–30% of context is consumed by re‑injected bootstrap files ([#67419](https://github.com/openclaw/openclaw/issues/67419)), increasing costs.
- **Regressions**: Several users report features that worked in 2026.4.2 and earlier are now broken (coding agent, Discord routing, Chrome extension relay).

**Satisfaction signals**: The high number of feature requests (e.g., per‑agent config, TTS/STT overrides) indicates a committed user base that wants to customize OpenClaw. The large volume of contributed PRs from community members also shows engagement.

## 8. Backlog Watch

The following important issues and PRs have been awaiting maintainer review or product decision for extended periods (3+ months) with no fix PR or resolution:

| Item | Age (since) | Status |
|------|-------------|--------|
| [#58450](https://github.com/openclaw/openclaw/issues/58450) | 2026-03-31 | Platinum hermit, needs maintainer review + product decision |
| [#65161](https://github.com/openclaw/openclaw/issues/65161) | 2026-04-12 | Platinum hermit, needs maintainer review + live repro |
| [#57326](https://github.com/openclaw/openclaw/issues/57326) | 2026-03-29 | Diamond lobster, needs maintainer review + security review |
| [#53628](https://github.com/openclaw/openclaw/issues/53628) | 2026-03-24 | Diamond lobster, needs maintainer review + product decision |
| [#57901](https://github.com/openclaw/openclaw/issues/57901) | 2026-03-30 | Diamond lobster, linked PR open but needs product decision |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | 2026-04-07 | Diamond lobster, regression with linked PR open but no maintainer decision |
| [#63015](https://github.com/openclaw/openclaw/pull/63015) | 2026-04-08 | Open PR, status “needs proof” — small fix for WhatsApp attachments |
| [#67433](https://github.com/openclaw/openclaw/pull/67433) | 2026-04-15 | Open PR, “needs proof” — waitForResult hook endpoint, important for API users |

The most worrying are the **five “platinum hermit” issues** (highest internal severity) that have been open for months without a fix branch — these represent fundamental architecture bugs (follow‑up promises, heartbeat stalls, overflow recovery, multi‑agent context blur, and gateway crash from Playwright). The project appears to be bottlenecked on maintainer capacity for both bug triage and product decisions.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs Hermes Agent
**Date: 2026-06-28**

## 1. Ecosystem Overview
The open‑source personal AI agent ecosystem is bifurcating into two dominant archetypes: foundational infrastructure projects (like OpenClaw) that provide core agent runtime and multi‑agent orchestration, and end‑user oriented platforms (like Hermes Agent) that prioritize usability, cloud sync, and rapid bug fixing. Both projects are actively maintained, but their health trajectories diverge sharply—OpenClaw struggles under a growing backlog of critical stability bugs, while Hermes Agent demonstrates high throughput in closing pervasive issues. A shared demand for per‑agent configuration, provider failover, and cloud sync indicates the community expects production‑grade reliability and multi‑device workflows.

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| Issues updated (24h) | 500 | 50 |
| Issues closed (24h) | 13 | 38 |
| PRs updated (24h) | 500 | 50 |
| PRs merged/closed (24h) | 40 | 18 |
| Latest release | 2026.4.x (no new) | v0.13.0 (no new) |
| Critical open bugs (P0/P1) | 7+ (no fix PRs) | 1 (fix PR open) |
| Community engagement (top issue 👍) | 9 👍 | 14 👍 |
| **Health Score** (subjective) | 🟡 **Concerning** — high volume but low closure rate, maintainer bottleneck | 🟢 **Healthy** — high closure rate, responsive maintainers |

## 3. OpenClaw’s Position

**Advantages vs. peers:**
- Larger community engagement (500 issues/PRs vs 50) suggests broader adoption and contributor base.
- Core reference implementation status (github.com/openclaw/openclaw) attracts upstream feature proposals (e.g., multi‑agent collaboration RFC, per‑agent memory‑wiki vault).
- Deep integration with Telegram and Slack, plus extensive memory/indexing features not present in Hermes.

**Technical approach differences:**
- OpenClaw emphasises persistent memory (SQLite storage refactor, wiki vaults, large memory indexes) and agent‑to‑agent communication.
- Hermes Agent focuses on provider rotation, credential management, and gateway resilience—less on in‑agent memory.

**Community size comparison:**
- OpenClaw’s 500 updated issues vs Hermes’ 50 indicates at least 10× the raw activity, but much of it is unresolved. The platial hermit severity (5 issues open >3 months) signals structural maintenance debt.

## 4. Shared Technical Focus Areas

Both projects face converging requirements:

- **Agent reliability**: OpenClaw’s “coding agent never completes” (#62505) and “agent promises follow‑up” (#58450) mirror Hermes’ closed “tool calls freeze” (#28834) and “repeated tool loops” (#30408). Users across both projects demand deterministic task completion.
- **Provider failover & credential rotation**: OpenClaw has lock contention causing session aborts; Hermes just closed credential pool rotation (#53913) and stale stream timeout (#25689). Both need robust fallback mechanisms.
- **Memory leaks**: OpenClaw’s P0 gateway memory leak (#91588) and unbounded `sessions.json` (#55334) echo Hermes’ closed “gateway SIGTERM flap” (#29092). Memory pressure is a top‑tier concern.
- **Streaming & message integrity**: OpenClaw’s invalid thinking signatures (#92201) and telegram streaming fix (#96317) parallel Hermes’ closed “Anthropic streaming hang” (#28161) and “tool result contamination” (#27033).
- **Per‑agent configuration**: Both have high‑upvoted requests for per‑agent memory vaults (OpenClaw #63829) and per‑slot reasoning effort (Hermes #53932).

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Primary focus** | Core agent runtime, multi‑agent orchestration, memory/index | User‑facing platform, gateway resilience, desktop/cloud sync |
| **Target users** | Developers building custom agents; power users who self‑host | End‑users and operators; multi‑device workflows |
| **Architecture** | Monorepo with heavy memory subsystem; SQLite migration in progress | Modular gateway + CLI + desktop app; provider abstraction layer |
| **Community dynamics** | High noise‑to‑signal ratio; maintainer bottleneck stifles bug resolution | High throughput; maintainers close bugs within same day |
| **Key feature differentiators** | Wiki vaults, memory‑core, heartbeat isolation, per‑agent TTS/STT overrides | Cloud sync (top request), Mixture‑of‑Agents, `/findout` slash command, Olympus dashboard plugin |
| **Operational maturity** | Barely stable; “requires periodic forced restarts” (user quote) | Production‑ready; most critical bugs closed within 24h |

## 6. Community Momentum & Maturity

- **Rapid iteration tier**: **Hermes Agent** — 38 issues closed and 18 PRs merged in 24 hours, including multiple P1 fixes. The project is actively stabilising and adding new capabilities (TTS endpoint, dashboard, slash commands). Product‑focused.
- **Stabilization tier**: **OpenClaw** — high activity but low closure rate. The backlog of 5 platinum‑hermit issues (oldest >3 months) indicates the team is fire‑fighting rather than shipping. The lack of a release suggests internal refactoring (SQLite storage) before any new version. Community trust is eroding (e.g., “Coding Agent never completes anything”).
- **Maturity assessment**: Hermes is closer to a polished product; OpenClaw remains a powerful but brittle framework.

## 7. Trend Signals

Extracted from community feedback and cross‑project patterns:

1. **Cloud sync is inevitable**: Hermes’ top‑upvoted issue (#20510, 14 👍) and OpenClaw’s lack of a similar feature signal that multi‑device agent users expect seamless configuration roams.
2. **Agent reliability > new features**: Both projects’ most urgent complaints are about agents failing to complete tasks (OpenClaw #62505, #58450; Hermes #30408, #28834). Until fundamental execution guarantees are met, feature requests will remain secondary.
3. **Token waste is a cost driver**: OpenClaw’s bootstrap‑file re‑injection (#67419) wasting 20–30% of context per turn mirrors Hermes’ closed context replay bug (#27156). Efficiency improvements are a competitive differentiator.
4. **Multi‑agent orchestration is still nascent**: OpenClaw’s ambitious RFC (#35203) for capability profiling and token governance shows the ecosystem is early. No project ships production‑grade multi‑agent collaboration yet.
5. **Provider diversity creates failure points**: Hermes’ massive closed‑bug list includes multiple provider‑specific issues (Anthropic, OpenAI, Discord, Telegram). Modular provider abstraction is critical for long‑term stability.

**For AI agent developers**: Prioritise agent reliability and token efficiency above new bells and whistles. Invest in provider‑agnostic fallback layers and consider cloud sync as a non‑negotiable expectation for end users.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-28

## 1. Today's Overview
The project saw very high activity on June 28, with **50 issues** and **50 pull requests** updated in the last 24 hours. Of those, **38 issues were closed** and **18 PRs were merged or closed**, indicating a strong focus on bug fixing and feature delivery. Despite no new releases, the community continued to submit both critical bug reports and thoughtful feature proposals. The closing of several P1 bugs and the introduction of multiple new capabilities suggest the project is healthy and responsive to user needs.

## 2. Releases
**No new releases today.** The latest stable version remains v0.13.0 (v2026.5.7), with approximately 496 commits on main beyond that tag.

## 3. Project Progress
Today’s merged/closed PRs and the large number of closed issues reflect substantial progress across the codebase. Key highlights include:

- **Credential pool rotation fix**: PR [#53913](https://github.com/NousResearch/hermes-agent/pull/53913) (closed) ensures long-lived sessions restore a live credential instead of a stale revoked key, addressing long-standing token exhaustion issues.
- **Systemd double-load fix**: PR [#53954](https://github.com/NousResearch/hermes-agent/pull/53954) (closed) resolves profile override conflicts when Hermes is launched via `python -m hermes_cli.main` under systemd.
- **Test suite deflake**: PR [#53945](https://github.com/NousResearch/hermes-agent/pull/53945) (closed) widens a timing assertion in `run_agent` tests to prevent CI flakiness.
- **Multiple critical bugs closed**: Issues such as the Anthropic streaming hang ([#28161](https://github.com/NousResearch/hermes-agent/issues/28161)), gateway SIGTERM flap ([#29092](https://github.com/NousResearch/hermes-agent/issues/29092)), `active_provider` override of config ([#29285](https://github.com/NousResearch/hermes-agent/issues/29285)), HTTP 400 tool result contamination ([#27033](https://github.com/NousResearch/hermes-agent/issues/27033)), and the PEP 668 lazy‑backend failure ([#30594](https://github.com/NousResearch/hermes-agent/issues/30594)) were all closed today, indicating that the corresponding fixes landed.

## 4. Community Hot Topics
The most engaged discussions and highly upvoted items reveal strong user interest in usability and cross‑device workflows:

- **[#20510 – Cloud Sync for Hermes Configurations](https://github.com/NousResearch/hermes-agent/issues/20510)**  
  *7 comments, 14 👍*  
  The single most upvoted open issue. Users want to sync `~/.hermes/` across devices. This is a clear indication that multi‑device power‑users are a growing segment.

- **[#36970 – Desktop Remote‑Client Onboarding](https://github.com/NousResearch/hermes-agent/issues/36970)**  
  *5 comments, 3 👍*  
  The macOS Desktop app currently requires a fresh Hermes install. Users ask for a way to connect the native client to an existing backend without bootstrapping a second instance.

- **[#53932 – MoA Reference Slots `reasoning_effort`](https://github.com/NousResearch/hermes-agent/issues/53932)**  
  *2 comments (opened today)*  
  A power‑user requests per‑slot reasoning effort control in the Mixture‑of‑Agents preset, enabling fine‑grained cost/quality trade‑offs.

- **[#53949 – Desktop Build Overwrites Source File](https://github.com/NousResearch/hermes-agent/issues/53949)**  
  *1 comment (opened today)*  
  Developer pain point: `npm run build` minifies the source `main.cjs` in place, breaking source‑tree readability.

## 5. Bugs & Stability
Today’s bug activity was intense, with many P1 issues closed and a handful of new problems reported. Below is a severity‑ranked summary:

| Severity | Issue / Bug | Status | Fix PR? |
|----------|-------------|--------|---------|
| **P1 (Critical)** | Anthropic streaming hangs via `_replace_primary_openai_client` ([#28161](https://github.com/NousResearch/hermes-agent/issues/28161)) | **Closed** | Yes – likely in today’s batch |
| **P1** | Gateway services enter SIGTERM flap loop ([#29092](https://github.com/NousResearch/hermes-agent/issues/29092)) | **Closed** | Yes |
| **P1** | `auth.json` silently overrides `config.yaml` provider ([#29285](https://github.com/NousResearch/hermes-agent/issues/29285)) | **Closed** | Yes |
| **P1** | Full test suite broken on main ([#27004](https://github.com/NousResearch/hermes-agent/issues/27004)) | **Closed** | Yes |
| **P1** | Tool result contamination causes persistent HTTP 400 loop ([#27033](https://github.com/NousResearch/hermes-agent/issues/27033)) | **Closed** | Yes |
| **P1** | Outbound chat messages bypass redact_sensitive_text ([#23810](https://github.com/NousResearch/hermes-agent/issues/23810)) | **Closed** | Yes |
| **P1** | Stale stream timeout does not trigger fallback_providers ([#25689](https://github.com/NousResearch/hermes-agent/issues/25689)) | **Closed** | Yes |
| **P1** | Agent tool calls freeze mid‑execution ([#28834](https://github.com/NousResearch/hermes-agent/issues/28834)) | **Closed** | Yes |
| **P1** | Repeated tool loops and broken final responses to Telegram ([#30408](https://github.com/NousResearch/hermes-agent/issues/30408)) | **Closed** | Yes |
| **P1** | Discord adapter silent zombie after outage ([#26656](https://github.com/NousResearch/hermes-agent/issues/26656)) | **Closed** | Yes |
| **P1** | Gateway kills agent during `clarify` ([#27564](https://github.com/NousResearch/hermes-agent/issues/27564)) | **Closed** | Yes |
| **P1** | Telegram gateway never delivers tool results ([#27230](https://github.com/NousResearch/hermes-agent/issues/27230)) | **Closed** | Yes |
| **P1** | Gateway shutdown hang (PID file race) ([#14128](https://github.com/NousResearch/hermes-agent/issues/14128)) | **Closed** | Yes |
| **P1** | Image routing failure locks entire message queue ([#21160](https://github.com/NousResearch/hermes-agent/issues/21160)) | **Closed** | Yes |
| **P1** | Discard image attachments mixed with non‑PNG/JPEG/WEBP ([#25935](https://github.com/NousResearch/hermes-agent/issues/25935)) | **Closed** | Yes |
| **P1** | Config normalization overwrites user values ([#27354](https://github.com/NousResearch/hermes-agent/issues/27354)) | **Closed** | Yes |
| **P2** | Stale stream errors retry same provider, not fallback ([#43211](https://github.com/NousResearch/hermes-agent/issues/43211)) | **Closed** | Yes |
| **P2** | Credential pool refresh loop prevents fallback on 401s ([#26080](https://github.com/NousResearch/hermes-agent/issues/26080)) | **Closed** | Yes |
| **P2** | Session resume replays prior context ([#27156](https://github.com/NousResearch/hermes-agent/issues/27156)) | **Closed** | Yes |
| **P2** | Subagent tool delegation inconsistent ([#21658](https://github.com/NousResearch/hermes-agent/issues/21658)) | **Closed** | Yes |
| **P2** | `_restore_primary_runtime` bypasses credential pool ([#25205](https://github.com/NousResearch/hermes-agent/issues/25205)) | **Closed** | Yes |
| **P3 (New today)** | Desktop build script overwrites source file ([#53949](https://github.com/NousResearch/hermes-agent/issues/53949)) | **Open** | None yet |
| **P3** | QQAdapter fails on reconnect (`is_reconnect` kwarg) ([#53948](https://github.com/NousResearch/hermes-agent/issues/53948)) | **Open** | PR [#53948](https://github.com/NousResearch/hermes-agent/pull/53948) open |
| **P3** | Session info not reporting per‑session provider override ([#53947](https://github.com/NousResearch/hermes-agent/issues/53947)) | **Open** | PR [#53947](https://github.com/NousResearch/hermes-agent/pull/53947) open |
| **P2** | Stale background processes block session reset ([#29177](https://github.com/NousResearch/hermes-agent/issues/29177)) | **Open** | PR [#53942](https://github.com/NousResearch/hermes-agent/pull/53942) open |

The rapid closure of so many P1/P2 bugs is a strong sign of maintainer responsiveness. However, the new bugs reported today (especially the desktop build pollution) could frustrate developers.

## 6. Feature Requests & Roadmap Signals
Several user‑submitted features point toward upcoming capabilities:

- **Cloud Sync** ([#20510](https://github.com/NousResearch/hermes-agent/issues/20510)) – The 14 upvotes make this the top community demand. Expect it to be prioritised for the next release.
- **Desktop Remote‑Client Onboarding** ([#36970](https://github.com/NousResearch/hermes-agent/issues/36970)) – Would enable pairing native Desktop clients to existing backends; likely follows cloud sync.
- **MoA Per‑Slot `reasoning_effort`** ([#53932](https://github.com/NousResearch/hermes-agent/issues/53932)) – A power‑user request to tune cost/quality per reference model.
- **OpenAI‑compatible TTS Endpoint** (PR [#42568](https://github.com/NousResearch/hermes-agent/pull/42568)) – Open since June 9, adds `/v1/audio/speech` to the gateway API. Still open, but a clear signalling of audio integration.
- **Olympus Dashboard Plugin** (PR [#53951](https://github.com/NousResearch/hermes-agent/pull/53951)) – A read‑only agent workstation monitor (profiles, sessions, Kanban, etc.), indicating a push toward observability.
- **`/findout` Slash Command** (PR [#53889](https://github.com/NousResearch/hermes-agent/pull/53889)) – Hard‑routed pipeline prompt across all interfaces; adds a powerful debugging/analysis command.
- **Hermes Agents Dashboard** (PR [#53946](https://github.com/NousResearch/hermes-agent/pull/53946)) – CLI MVP for managing multi‑agent teams.

Given the volume and quality of open feature PRs, the next version is

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*