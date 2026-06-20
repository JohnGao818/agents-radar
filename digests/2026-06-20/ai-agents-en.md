# OpenClaw Ecosystem Digest 2026-06-20

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-06-20 02:56 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-06-20

## 1. Today's Overview
The OpenClaw project is experiencing **extremely high activity**, with 500 issues and 500 pull requests updated in the last 24 hours. Of these, 452 issues remain open/active and 48 were closed, while 457 PRs are still open and 43 were merged or closed. One new beta release (`v2026.6.9-beta.1`) shipped today focusing on Telegram delivery fidelity. The issue tracker reveals several **critical stability problems**, including a severe gateway memory leak (P0), silent data loss in the memory-core Dreaming pipeline (P0), and multiple regressions across channel integrations (Telegram, Matrix, Slack). Community engagement is strong, with several high-comment threads on session migration, model fallback chains, and session isolation failures.

---

## 2. Releases
**New release: [v2026.6.9-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.9-beta.1)**  
- **Highlights:**  
  - Richer Telegram delivery: now sends rich HTML, preserves markdown and sticker paths, renders progress drafts and command output faithfully, and fixes mention and spooled handler routing.  
  - No breaking changes or migration notes are documented in the release summary.

---

## 3. Project Progress
**43 PRs merged/closed in the last 24 hours**, including several important fixes:

- **[#94656](https://github.com/openclaw/openclaw/pull/94656) (merged):** Adds a direct text delivery fallback for subagent completions, preventing silent message loss when the requester session is inactive.  
- **[#95139](https://github.com/openclaw/openclaw/pull/95139) (merged):** Fixes Ollama `/think` menu to show all thinking levels for live-discovered models.  
- **[#95157](https://github.com/openclaw/openclaw/pull/95157) (merged):** Corrects macOS version reporting for Darwin 25+ (macOS 26 Tahoe) by using `sw_vers` instead of kernel version.  
- **[#93794](https://github.com/openclaw/openclaw/pull/93794) (closed):** Fixes Telegram Web support regression introduced in v2026.6.8 (high community reaction: 8 👍).  

Other active PRs in review or awaiting proof include fixes for Anthropic socket keep‑alive failures, Matrix MiniMax reasoning tags, session naming migration, and Telegram approval message cleanup.

---

## 4. Community Hot Topics
The most-engaged issues (by comment count) reflect deep user concerns about **session state, memory management, and channel reliability**:

| Issue | Title | Comments | 👍 | Underlying Need |
|-------|-------|----------|----|-----------------|
| [#88838](https://github.com/openclaw/openclaw/issues/88838) | Track core session/transcript SQLite migration via accessor seam | 31 | 1 | Safe migration strategy without full rewrite |
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | Critical: Gateway Memory Leak — RSS 350MB → 15.5GB causing OOM crashes | 13 | 1 | System stability under sustained use |
| [#85333](https://github.com/openclaw/openclaw/issues/85333) | `openclaw doctor --fix` 4-5x slower (55s → 229s+) | 13 | 1 | Performance regression in diagnostic tool |
| [#63829](https://github.com/openclaw/openclaw/issues/63829) | Per-agent memory-wiki vault configuration | 10 | 9 | Multi‑agent isolation for knowledge stores |
| [#85103](https://github.com/openclaw/openclaw/issues/85103) | Model fallback chain not triggered on provider-wide quota exhaustion | 10 | 1 | Reliable model chaining on provider failure |
| [#85030](https://github.com/openclaw/openclaw/issues/85030) | MCP tools not injected into subagent sessions | 8 | 3 | Tool availability in spawned agents |
| [#84903](https://github.com/openclaw/openclaw/issues/84903) | Single stalled agent session blocks entire Gateway event loop | 8 | 2 | Session isolation / resource containment |
| [#92043](https://github.com/openclaw/openclaw/issues/92043) | 180s compaction timeout fails identically every turn for long histories | 8 | 1 | Configurable compaction deadlines with partial reuse |
| [#92460](https://github.com/openclaw/openclaw/issues/92460) | Isolated cron completion drops explicit delivery.channel | 8 | 1 | Reliable cron result delivery |

The community is demanding **more granular configuration (per‑agent memory, per‑channel models)**, **better failure isolation**, and **faster diagnostic tools**. The high number of reactions on [#63829](https://github.com/openclaw/openclaw/issues/63829) (9 👍) signals strong interest in per-agent memory vaults.

---

## 5. Bugs & Stability
**Critical (P0) issues with active discussion:**

- **[#91588](https://github.com/openclaw/openclaw/issues/91588) (P0, open):** Gateway memory leak – RSS grows from 350 MB to 15.5 GB over days, causing repeated OOM kills. No fix PR identified yet.  
- **[#84882](https://github.com/openclaw/openclaw/issues/84882) (P0, open):** `memory-core` Dreaming pipeline silently deletes daily memory files (`memory/YYYY-MM-DD.md`). **Data loss bug** with high severity. Linked PR open but needs info.  

**High-severity (P1) regressions and stability bugs:**

- **[#90325](https://github.com/openclaw/openclaw/issues/90325) (P1):** Matrix channel dispatch crashes with `TypeError: Cannot read properties of undefined (reading 'run')` after v2026.6.1 update.  
- **[#93794](https://github.com/openclaw/openclaw/issues/93794) (closed, P1):** Telegram Web messages unsupported after v2026.6.8 – **resolved** in today’s release.  
- **[#84903](https://github.com/openclaw/openclaw/issues/84903) (P1):** A single stalled agent session blocks the entire Gateway event loop – session isolation failure.  
- **[#90711](https://github.com/openclaw/openclaw/issues/90711) (P1):** `launchd` plist hardcodes `StandardErrorPath` to `/dev/null`, hiding all gateway stderr since 5.28.  
- **[#90840](https://github.com/openclaw/openclaw/issues/90840) (P1):** Subagent raw output delivered to chat user instead of parent summary (regression).  
- **[#93905](https://github.com/openclaw/openclaw/issues/93905) (P1):** `/usage` no longer works in Telegram after v2026.6.8.  

**Other notable bugs:**

- [#94269](https://github.com/openclaw/openclaw/issues/94269) (P2): Z.ai static catalog models resolve without `baseUrl`, causing fallthrough to OpenAI API.  
- [#93807](https://github.com/openclaw/openclaw/issues/93807) (P2): `web_fetch` ignores `NO_PROXY` env variable when `useTrustedEnvProxy` is enabled.  
- [#78640](https://github.com/openclaw/openclaw/issues/78640) (P1, Windows): EPERM errors on memory index reindex persist despite previous fixes.  

Several bugs have **open fix PRs** (e.g., [#92460](https://github.com/openclaw/openclaw/issues/92460) linked to [PR #94656](https://github.com/openclaw/openclaw/pull/94656), [#93905](https://github.com/openclaw/openclaw/issues/93905) possibly related to upcoming Telegram fixes).

---

## 6. Feature Requests & Roadmap Signals
**High-demand features posted recently or with strong community support:**

| Issue | Title | 👍 | Likely near-term inclusion |
|-------|-------|----|----------------------------|
| [#63829](https://github.com/openclaw/openclaw/issues/63829) | Per-agent memory-wiki vault configuration | 9 | **High** – 10 comments, actively discussed, aligns with multi‑agent growth |
| [#53638](https://github.com/openclaw/openclaw/issues/53638) | Per-channel / per-group / per-DM model override | 2 | **Medium** – long-standing (Mar 24), multiple linked PRs open |
| [#90916](https://github.com/openclaw/openclaw/issues/90916) | Topic-session families for isolated context lanes | 1 | **Medium** – new feature area, fits chat-native assistant use cases |
| [#46656](https://github.com/openclaw/openclaw/issues/46656) | Webchat inline button support | 1 | **Medium** – parity with Telegram, needed for Control UI |
| [#90354](https://github.com/openclaw/openclaw/issues/90354) | Bounded/validated append semantics for pre-compaction memory flush | 1 | **High** – directly related to memory data loss bug [#84882](https://github.com/openclaw/openclaw/issues/84882) |
| [#91455](https://github.com/openclaw/openclaw/issues/91455) | Documentation update for Kubernetes deployment | 1 | **Low** – doc improvement, not functionality |

Per-agent memory vaults ([#63829](https://github.com/openclaw/openclaw/issues/63829)) and bounded memory append ([#90354](https://github.com/openclaw/openclaw/issues/90354)) are strong candidates for the next release given the ongoing memory reliability crises.

---

## 7. User Feedback Summary
Real pain points expressed through issues and comments:

- **Memory leaks and OOM crashes** ([#91588](https://github.com/openclaw/openclaw/issues/91588)): “RSS grows from ~350 MB at startup to 15.5 GB over 2-3 days” – operator frustration with repeated crash-restart cycles.  
- **Silent data loss** ([#84882](https://github.com/openclaw/openclaw/issues/84882)): “Dreaming step silently deletes daily memory files” – users shocked by lost conversations.  
- **Degraded diagnostic tool** ([#85333](https://github.com/openclaw/openclaw/issues/85333)): “`openclaw doctor --fix` went from 55s to 229s+” – explicit performance regression complaint.  
- **Channel regressions** ([#90325](https://github.com/openclaw/openclaw/issues/90325), [#93794](https://github.com/openclaw/openclaw/issues/93794)): Updates breaking previously working Telegram Web and Matrix – users express “worked before, now fails”.  
- **Session isolation failure** ([#84903](https://github.com/openclaw/openclaw/issues/84903)): “A single stalled agent session blocks the entire Gateway” – critical for multi-user deployments.  
- **Model fallback unreliability** ([#85103](https://github.com/openclaw/openclaw/issues/85103)): “Quota exhaustion not triggering fallback chain” – frustration with service disruption during peak usage.  

Positive feedback is scarce in the raw data, but the Telegram rich delivery improvements ([v2026.6.9-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.9-beta.1)) are likely to improve satisfaction for Telegram power users.

---

## 8. Backlog Watch
Issues that have been open for several weeks without maintainer resolution or clear progress:

| Issue | Created | Last Update | Comments | Status |
|-------|---------|-------------|----------|--------|
| [#46656](https://github.com/openclaw/openclaw/issues/46656) (P2) | 2026-03-14 | 2026-06-19 | 6 | Needs maintainer review / product decision |
| [#53638](https://github.com/openclaw/openclaw/issues/53638) (P2) | 2026-03-24 | 2026-06-19 | 6 | Needs maintainer review / product decision |
| [#63829](https://github.com/openclaw/openclaw/issues/63829) (P1) | 2026-04-09 | 2026-06-20 | 10 | Needs security review + product decision |
| [#85027](https://github.com/openclaw/openclaw/issues/85027) (P1) | 2026-05-21 | 2026-06-20 | 5 | Needs info from reporter |
| [#85333](https://github.com/openclaw/openclaw/issues/85333) (P1, stale) | 2026-05-22 | 2026-06-19 | 13 | Needs live repro |
| [#85334](https://github.com/openclaw/openclaw/issues/85334) (P2, stale) | 2026-05-22 | 2026-06-19 | 6 | Source repro available, linked PR open |
| [#84882](https://github.com/openclaw/openclaw/issues/84882) (P0) | 2026-05-21 | 2026-06-20 | 6 | Needs info from maintainer (silent data loss) |

The P0 memory data loss bug ([#84882](https://github.com/openclaw/openclaw/issues/84882)) and the P1 gateway memory leak ([#91588](https://github.com/openclaw/openclaw/issues/91588)) are the most urgent items requiring maintainer attention. Several long-standing feature requests ([#46656](https://github.com/openclaw/openclaw/issues/46656), [#53638](https://github.com/openclaw/openclaw/issues/53638)) need a product decision to move forward.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: OpenClaw vs. Hermes Agent

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is experiencing explosive growth and increasing operational maturity. Both OpenClaw and Hermes Agent are shipping weekly releases, with hundreds of community contributors actively shaping roadmaps through issue-tracker engagement. The ecosystem is bifurcating: some projects prioritize multi-agent orchestration and memory persistence (OpenClaw), while others focus on desktop-native experiences and channel expansion (Hermes Agent). A shared theme across both communities is the tension between feature velocity and stability—users demand both new capabilities *and* reliable foundations, and both projects are grappling with regression-prone release cycles. The critical mass of community contributions (245 for Hermes Agent in v0.17.0 alone, 43+ PRs merged daily for OpenClaw) signals that this space has moved beyond hobbyist tinkering into serious infrastructure territory.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|--------|----------|--------------|
| **Issues updated (24h)** | 500 | 50 |
| **Open issues** | 452 | ~40-45 (estimated) |
| **PRs updated (24h)** | 500 | 50 |
| **Open PRs** | 457 | ~45 (estimated) |
| **Latest release** | v2026.6.9-beta.1 (today) | v0.17.0 (yesterday) |
| **Release type** | Minor beta (patch) | Major release (1,475 commits) |
| **Release focus** | Telegram delivery fix | "The Reach Release" — stability + channels |
| **P0/P1 bugs (open)** | ~12 critical | ~8 critical |
| **Data loss bugs** | 1 (P0, confirmed) | 0 (confirmed) |
| **Contributor momentum** | 43 PRs merged/closed in 24h | 800+ PRs merged since v0.16.0 |
| **Health score** | **Moderate** — high activity but firefighting regressions | **Strong** — post-release stabilization, fewer critical incidents |

**Health score rationale:** OpenClaw's extreme activity volume masks a structural issue—nearly as many open issues as closed, with two P0 data-loss/memory-leak bugs unaddressed. Hermes Agent shows healthier ratios: fewer open items relative to throughput, a major release behind them, and no confirmed data-loss issues.

---

## 3. OpenClaw's Position

**Advantages:**
- **Scale:** By far the larger project by raw activity (10x the daily issue/PR volume of Hermes Agent). This reflects both a larger install base and more aggressive development.
- **Memory architecture:** Pioneering the "Dreaming" pipeline for long-term memory persistence, though currently plagued by a P0 data loss bug (#84882). When stable, this is a genuine competitive moat.
- **Multi-agent orchestration:** Per-agent memory vaults (#63829) and subagent delegation (#94656) indicate deeper multi-agent infrastructure than Hermes Agent.
- **Channel depth:** Telegram integration is more granular (rich HTML, markdown, sticker paths, spooled handler routing) than Hermes Agent's approach.

**Technical approach differences:**
- OpenClaw uses SQLite for session/transcript storage with migration seams (#88838); Hermes Agent appears more abstracted.
- OpenClaw's gateway event loop is a single point of failure (#84903 shows a stalled session blocks everything), whereas Hermes Agent's gateway design seems more process-isolated.
- OpenClaw's diagnostic tool (`openclaw doctor --fix`) has regressed 4-5x in performance (#85333), suggesting technical debt in the CLI toolchain.

**Community size comparison:**
OpenClaw's community is demonstrably larger (500 daily updates vs. 50 for Hermes Agent), but this comes with signal-to-noise costs. The community is actively frustrated—critical bugs go unaddressed, and users report "worked before, now fails" across multiple channels. Hermes Agent has fewer users but higher satisfaction per contributor (245 contributors for a major release vs. widespread complaint volume in OpenClaw).

---

## 4. Shared Technical Focus Areas

| Focus Area | OpenClaw Signal | Hermes Agent Signal | Implication |
|------------|----------------|---------------------|-------------|
| **Memory reliability** | P0 data loss (#84882), bounded append semantics (#90354) | Context compression causes repetition (#49307) | Both projects struggle with memory as a first-class concern |
| **Model provider compatibility** | Ollama think levels (#95139), Z.ai fallthrough (#94269) | Gemma 4 broken (#45924/#49297), Cerebras reasoning echo (#34760) | Every provider integration is fragile; no project has "just works" for all models |
| **Credential/secret isolation** | Not yet a major topic | Zero-knowledge proxy daemon (#4656, 79 days open) | Emerging security-consciousness; Hermes Agent is leading here |
| **Session/channel isolation** | Single stalled session blocks gateway (#84903) | Only WhatsApp sessions indexed (#49361) | Both need better resource containment and session visibility |
| **Channel reliability** | Matrix crash (#90325), Telegram Web regression (#93794) | Telegram silent hang (#49369), WhatsApp Docker fail (#36641) | Channel integrations are fragile and regression-prone for both |
| **Diagnostic tooling** | `doctor --fix` 4x slower (#85333) | CLI plugin filters broken (#23802) | Both have neglected their CLI/developer tooling |

**Emerging requirement:** Both projects need a **provider-agnostic model fallback chain** that works reliably across quota exhaustion, API changes, and new model releases. OpenClaw has a fallback chain feature (#85103) that doesn't trigger properly; Hermes Agent doesn't appear to have one yet.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|-----------|----------|--------------|
| **Core identity** | Reference implementation for multi-agent, memory-persistent AI | Desktop-first personal AI assistant with broad channel reach |
| **Primary user** | Operators running multi-user, multi-agent deployments | Individual users, desktop power users, Docker operators |
| **Architecture style** | Monolithic gateway with per-channel adapters; SQLite-backed | Desktop app with gateway mode; plugin architecture for channels |
| **Release philosophy** | Continuous beta: patch releases every 1-2 days | Major version releases with consolidation (v0.16.0 → v0.17.0) |
| **Key technical bet** | "Dreaming" pipeline for autonomous memory compaction | Desktop-native UX with voice wake word, dashboard plugins |
| **Weakest link** | Memory pipeline reliability; gateway OOM crashes | Provider compatibility; credential management |
| **Channel priority** | Telegram (deepest), Matrix, Slack | WhatsApp, Signal, Telegram, Desktop app |
| **Multi-agent story** | Strong — per-agent vaults, subagent delegation, session isolation (broken) | Weak — delegate task model overrides ignored (#49332) |
| **Security posture** | Not a highlighted theme | Zero-knowledge proxy daemon (#4656) indicates growing security focus |
| **Windows support** | EPERM errors on memory reindex (#78640) | Node/npm path management broken (#49242), Kanban cleanup broken (#49374) |

**Notable gap:** OpenClaw has no desktop application; Hermes Agent has no multi-agent memory isolation equivalent to OpenClaw's vault system. Both are incomplete mirrors of each other's strengths.

---

## 6. Community Momentum & Maturity

**Activity tiers:**

- **Tier 1 (Extreme):** OpenClaw — 500 issues/PRs daily, 452 open issues. This is either "hypergrowth with strong community" or "maintainers overwhelmed." The bug-to-fix ratio suggests the latter.
- **Tier 2 (High):** Hermes Agent — 50 issues/PRs daily with healthier closed/open ratios. Post-major-release stabilization in progress.
- **Tier 3 (Emerging):** Not captured in this data, but likely includes smaller projects (e.g., AutoGPT, SuperAGI) with lower activity.

**Rapid iteration signals:**

- **OpenClaw:** Shipping beta releases daily. Hotfix branches are active. The project is clearly in "move fast and break things" mode.
- **Hermes Agent:** Just shipped a major release with 1,475 commits. The team is likely in stabilization mode for the next 1-2 weeks.

**Stabilization indicators:**

- **OpenClaw:** Multiple community members reporting regressions ("worked before, now fails"). Data loss bug (#84882) is a showstopper. **Not yet stable.**
- **Hermes Agent:** v0.17.0 closed 300+ issues. Reopened Gemma 4 bug is a regression concern but isolated to one provider. **Approaching stability.**

**Maturity assessment:**
Both projects are in **early majority adoption** phase — enough users to generate significant feedback, not enough to force rigorous quality gates. Neither has a formal regression test suite mentioned in the digests. This is a systemic risk across the ecosystem.

---

## 7. Trend Signals

**1. Memory is the new frontier, but it's broken everywhere.**
Both projects have memory-related bugs (OpenClaw: data loss in Dreaming pipeline; Hermes Agent: context compression causing repetition). Users want persistent, reliable memory that doesn't silently corrupt or lose data. This is the single highest-value area for AI agent developers: solve memory reliability, and you win the ecosystem.

**2. Provider agnosticism is a myth.**
Every major model provider (Ollama, Gemma 4, Cerebras, Bedrock, Z.ai) breaks in both projects. The industry needs a **provider compatibility testing standard** — something akin to web browser standards for LLM providers. Until then, every integration is a bespoke maintenance burden.

**3. Channel fragmentation is real and expensive.**
Both projects support 3-5+ channels, and every channel update introduces regressions in others. Telegram Web regressions, Matrix crashes, WhatsApp Docker failures — these are not isolated incidents. Developers should **specialize in fewer channels** rather than chasing feature parity across all platforms.

**4. Security is becoming table stakes.**
Hermes Agent's zero-knowledge proxy daemon (#4656) is the strongest signal: operators want credential isolation from the host OS. This will become a requirement for any project targeting CI/CD or multi-tenant deployments within 6 months.

**5. Desktop-native UX is a growing wedge.**
Hermes Agent's desktop app (with `/goal` support, file browser, dashboard plugins) contrasts with OpenClaw's CLI-only approach. As AI assistants move from "chat interface" to "OS-integrated agent," desktop experiences will differentiate projects in the next 1-2 quarters.

**6. Community patience for regressions is thinning.**
OpenClaw's feedback is increasingly frustrated: "RSS grows from 350 MB to 15.5 GB," "worked before, now fails," "a single stalled agent blocks everything." Users who adopted early are now hitting production walls. The next release cycle for any project must prioritize **stability over features** to retain trust.

**7. Multi-agent orchestration is still immature.**
Both projects struggle with something as basic as "make one agent call another without breaking everything." OpenClaw's session isolation failure (#84903) and Hermes Agent's delegate model override being ignored (#49332) show that distributed agent architectures are not yet production-ready outside of carefully managed demos.

---

**Recommendation for technical decision-makers:**
- **If you need a stable, single-user desktop assistant today:** Hermes Agent v0.17.0 is the safer choice, but test your specific model providers thoroughly before committing.
- **If you need multi-user, multi-agent memory infrastructure:** OpenClaw has the architecture you want but cannot yet deliver reliably. Monitor #84882 (data loss) and #91588 (OOM leaks) for resolution before deploying.
- **If you are building tooling for this ecosystem:** Focus on **provider compatibility testing frameworks**, **memory validation tools**, and **credential isolation solutions** — these are the three highest-value gaps shared by both projects.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — June 20, 2026

## Today's Overview
Project activity remains high with 50 issues and 50 PRs updated in the last 24 hours, alongside a major v0.17.0 release pushed yesterday (June 19). The release, named “The Reach Release,” consolidates over 1,475 commits, 800 merged PRs, and contributions from 245 community contributors — signalling strong momentum. Today’s update shows a healthy mix of new features (e.g., project tree, OAuth connect), urgent bug fixes (P1 grade), and ongoing community discussion around credential security, model provider compatibility, and desktop–gateway integration. The project clearly prioritizes both core agent stability and ecosystem expansion.

## Releases
**New Release: v0.17.0 (v2026.6.19)**  
- **Commits since v0.16.0:** ~1,475  
- **Merged PRs:** ~800  
- **Files changed:** 1,693 (235,390 insertions, 50,730 deletions)  
- **Issues closed:** 300+  
- **Community contributors:** 245  

**Summary:** v0.16.0 established the Hermes desktop footprint; v0.17.0 (“The Reach Release”) extends that foundation with major stability improvements, expanded provider support, and deepened platform integration (particularly WhatsApp and Signal). Breaking changes are not detailed in the truncated changelog, but the sheer number of changes suggests operators should review migration notes in the [release page](https://github.com/NousResearch/hermes-agent/releases/v2026.6.19).  

*No new release was tagged today (June 20).*

## Project Progress — Merged/Closed PRs Today
Several PRs were merged/closed in the last 24h, contributing to stability and feature completeness:

| PR | Description | Impact |
|----|-------------|--------|
| [#49375](https://github.com/NousResearch/hermes-agent/pull/49375) (closed) | Fix delegate: route Bedrock subagents through converse mode | Prevents incorrect wire format for Bedrock delegation |
| [#43970](https://github.com/NousResearch/hermes-agent/pull/43970) (closed) | Fix `_add_path_candidate` crash on `~user` expanduser `RuntimeError` | Eliminates silent agent failure when tool‑call contains `~` in non‑path contexts |
| [#40498](https://github.com/NousResearch/hermes-agent/pull/40498) (closed) | Add opt‑in `image_edit` tool | Extends `image_gen` toolset with editing capabilities |
| [#49260](https://github.com/NousResearch/hermes-agent/issues/49260) (closed) | Live adapter delivers silently for Signal cron jobs | Critical fix ensuring messages reach users |
| [#43476](https://github.com/NousResearch/hermes-agent/issues/43476) (closed) | Desktop `/goal` swallowed — missing `command.dispatch` handler | Improves goal‑setting UX in desktop app |
| [#39281](https://github.com/NousResearch/hermes-agent/issues/39281) (closed) | Hermes fails with Gemma 4 on Ollama backend | Resolved token‑limit related truncation (though reopened as #49297) |

## Community Hot Topics
The most actively discussed issues and PRs (by comment count and reactions) reveal key community concerns:

- **[#4656](https://github.com/NousResearch/hermes-agent/issues/4656) — Credential proxy daemon** (11 comments, 1 👍)  
  Users are pushing for a zero‑knowledge HTTP/HTTPS broker to isolate agent credentials from the host OS. This reflects growing security‑consciousness among operators running Hermes in multi‑tenant or CI environments.

- **[#45924](https://github.com/NousResearch/hermes-agent/issues/45924) — Gemma 4 12B model crash** (5 comments, 1 👍)  
  Repeated reports of Hermes failing even on a simple “hello” with Gemma 4 on Ollama, despite the same model working standalone. The community suspects a provider‑side marshalling issue.

- **[#39281](https://github.com/NousResearch/hermes-agent/issues/39281) — Gemma 4 truncation** (4 comments)  
  Closed but reopened as [#49297](https://github.com/NousResearch/hermes-agent/issues/49297), indicating the fix was incomplete.

- **[#36641](https://github.com/NousResearch/hermes-agent/issues/36641) — WhatsApp bridge fails after Docker recreate** (3 comments)  
  Affects users relying on Docker‑based deployments; dependency re‑installation fails on container restart.

- **[#49297](https://github.com/NousResearch/hermes-agent/issues/49297) — Gemma 4 still broken after v0.17.0** (3 comments)  
  User explicitly re‑opened the issue because they believe closed issues are unseen. Maintainer attention needed.

- **[#23802](https://github.com/NousResearch/hermes-agent/issues/23802) — CLI filters out entry‑point discovered plugins** (3 comments, 1 👍)  
  Plugin installation/deployment friction for operators who install Hermes plugins via pip.

- **[#47868](https://github.com/NousResearch/hermes-agent/issues/47868) — Strict providers reject leaked `timestamp` metadata** (3 comments, 1 👍)  
  Gateway mode sends schema‑foreign fields causing 400 errors; impacts cross‑provider compatibility.

**Underlying needs**: The community is asking for:
- Better credential isolation and secret management.
- Rock‑solid Ollama/LLM provider compatibility (especially with newer models like Gemma 4).
- Reproducible Docker setups.
- Cleaner plugin installation flows.

## Bugs & Stability
**P1 (Critical) – New/Updated Today**

| Bug | Issue | Fix PR? |
|-----|-------|---------|
| Session index only tracks WhatsApp – CLI sessions invisible | [#49361](https://github.com/NousResearch/hermes-agent/issues/49361) | Not yet |
| Telegram gateway silent hang during startup (no init timeout) | [#49369](https://github.com/NousResearch/hermes-agent/issues/49369) | PR [#49369](https://github.com/NousResearch/hermes-agent/pull/49369) (open) |
| Context compression causes answer repetition + instruction loss | [#49307](https://github.com/NousResearch/hermes-agent/issues/49307) | PR [#49381](https://github.com/NousResearch/hermes-agent/pull/49381) (open) |
| Live adapter delivers silently for Signal cron jobs (closed as fixed) | [#49260](https://github.com/NousResearch/hermes-agent/issues/49260) | Already closed |

**P2 (High) – New/Updated Today**

| Bug | Issue | Fix PR? |
|-----|-------|---------|
| `delegate_task` model override ignored – subagents use wrong model | [#49332](https://github.com/NousResearch/hermes-agent/issues/49332) | Not yet |
| `auxiliary.vision provider=auto` does not inherit `base_url`/`api_key` | [#48991](https://github.com/NousResearch/hermes-agent/issues/48991) | Not yet |
| File browser doesn’t follow profile switch (race condition) | [#49293](https://github.com/NousResearch/hermes-agent/issues/49293) | Not yet |
| `execute_code` consent gate does not recognise explicit chat consent in desktop GUI | [#49283](https://github.com/NousResearch/hermes-agent/issues/49283) | Not yet |
| Desktop GUI ‘Start Gateway’ button has no effect | [#49345](https://github.com/NousResearch/hermes-agent/issues/49345) | Not yet |
| Windows WhatsApp gateway should prefer Hermes‑managed Node/npm | [#49242](https://github.com/NousResearch/hermes-agent/issues/49242) | Not yet |
| CLI `--global` model switch does not persist `base_url`/`api_mode` | [#25106](https://github.com/NousResearch/hermes-agent/issues/25106) | PR [#49360](https://github.com/NousResearch/hermes-agent/pull/49360) (open) |

**P3 (Medium) – Notable New Bugs**

- Chinese punctuation input jumps to settings screen ([#49326](https://github.com/NousResearch/hermes-agent/issues/49326))  
- Unconditional Raft CLI warning logged even when disabled ([#49336](https://github.com/NousResearch/hermes-agent/issues/49336))  
- Kanban worker process trees not killed on Windows timeout ([#49374](https://github.com/NousResearch/hermes-agent/pull/49374) – fix open)

**Regression Watch:** The Gemma 4 issue (#45924/#49297) persists across v0.17.0, indicating an incomplete fix. The context compression bug (#49307) is critical and has a dedicated PR (#49381) in review.

## Feature Requests & Roadmap Signals
Today’s issue and PR landscape reveals several features that are strongly desired and have active implementation traction:

| Feature | Issue/PR | Community Signal | Likely for Next Release? |
|---------|----------|-----------------|--------------------------|
| Credential proxy daemon (zero‑knowledge) | [#4656](https://github.com/NousResearch/hermes-agent/issues/4656) | 11 comments, oldest pending feature | High – flagship security feature |
| First‑class Project entity (replacing git‑branch workspace) | [#49037](https://github.com/NousResearch/hermes-agent/pull/49037) | New PR, backend‑authoritative session tree | Likely |
| Voice wake word for Hermes Desktop | [#49383](https://github.com/NousResearch/hermes-agent/issues/49383) | New, no activity yet | Possible – early signal |
| Zulip platform adapter | [#49229](https://github.com/NousResearch/hermes-agent/issues/49229) | Superseded by PR #3335 | Already in core |
| Honcho OAuth connect (passwordless memory provider) | [#44335](https://github.com/NousResearch/hermes-agent/pull/44335) | Open PR, one‑click desktop flow | Likely |
| Desktop dashboard plugins parity with web | [#49363](https://github.com/NousResearch/hermes-agent/issues/49363) | New, low comments | Possible |
| GLM‑5.x reasoning support in OpenCodeGo profile | [#49279](https://github.com/NousResearch/hermes-agent/issues/49279) | 1 comment, niche | Unlikely in next minor |

**Prediction:** The credential proxy daemon (#4656) and first‑class projects (#49037) are the strongest roadmap signals. Both address operator pain points (security, workspace organisation) and have existing community buy‑in.

## User Feedback Summary
**Pain Points (explicitly reported):**
- **Model compatibility:** Multiple users report Gemma 4 (Ollama) broken after v0.17.0 – “even just saying hello causes an error” (#45924). One user explicitly feels closed issues are ignored (#49297).
- **Credential management:** Users want secrets isolated from the host to prevent exfiltration, especially in CI/multi‑tenant setups (#4656).
- **Docker/stability:** WhatsApp bridge dependencies fail on container recreate (#36641); Telegram gateway silently hangs (#49369).
- **Desktop GUI quirks:** `/goal` swallowed, file browser not following profile switches, “Start Gateway” button dead, Chinese punctuation triggers settings page.
- **Windows support:** Node/npm path management inadequate (#49242); Kanban worker process tree cleanup broken (#49374).
- **Session management:** Only WhatsApp sessions appear in index – CLI/TUI sessions invisible (#49361).

**Satisfaction indicators:**
- The release v0.17.0 was warmly received (245 contributors, 800 merged PRs).
- Users are actively contributing features (OAuth connect, Zulip adapter, execution receipts).
- The “Reach Release” name suggests maintainers are proud of the scope.

**Dissatisfaction signals:**
- Re‑opening of Gemma 4 bug indicates fix regression.
- Several open P1/P2 bugs with no fix PR assigned may erode trust.

## Backlog Watch
Issues and PRs that have been open for an extended period (14+ days) with no recent maintainer action or that are high‑impact:

| Item | Age | Status | Why It Matters |
|------|-----|--------|----------------|
| [#4656](https://github.com/NousResearch/hermes-agent/issues/4656) — Credential proxy daemon | 79 days | Open, 11 comments | Top‑voted feature request, no maintainer response |
| [#23802](https://github.com/NousResearch/hermes-agent/issues/23802) — CLI filters plugins installed via entry points | 40 days | Open, 3 comments | Blocks plugin ecosystem adoption |
| [#25106](https://github.com/NousResearch/hermes-agent/issues/25106) — `--global` model switch doesn’t persist `base_url`/`api_mode` | 38 days | Open, 1 comment | Causes silent config corruption for custom providers |
| [#29433](https://github.com/NousResearch/hermes-agent/pull/29433) — Catch `RuntimeError` from `Path.expanduser()` | 31 days | Open PR | Fixes a crash affecting all tool‑call paths; supersedes closed #43970 |
| [#34760](https://github.com/NousResearch/hermes-agent/pull/34760) — Strip `reasoning_content` echo for Cerebras | 22 days | Open PR | Fixes multi‑turn tool use on Cerebras models |
| [#46199](https://github.com/NousResearch/hermes-agent/issues/46199) — Request for portable/isolated Windows deployment docs | 6 days | Open, 1 comment | Security‑conscious users need official guidance |

**Maintainer action needed:** The credential proxy (#4656) and CLI plugin filter (#23802) are longstanding, high‑impact issues that shape the project’s perception. The PR #29433 (expanduser fix) is a small but important stability patch that should be merged quickly. The Cerebras PR (#34760) also blocks a specific provider user base.

---

*Digest generated from GitHub data for 2026-06-20.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*