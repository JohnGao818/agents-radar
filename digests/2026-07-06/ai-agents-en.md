# OpenClaw Ecosystem Digest 2026-07-06

> Issues: 500 | PRs: 500 | Projects covered: 2 | Generated: 2026-07-06 02:47 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest – 2026-07-06

**Generated from GitHub data (openclaw/openclaw) — last 24 hours**

---

## 1. Today’s Overview

Activity remains at a very high level: **500 issues** and **500 pull requests** were updated in the past 24 hours, with **328 PRs merged or closed** and **77 issues resolved**. One new beta release (`v2026.7.1-beta.2`) shipped, bringing **GPT-5.6 model family support** and a new external harness attachment command. Despite strong forward momentum, the project carries a heavy bug backlog — several **P0/P1 regressions** and **security-rated issues** remain open, and the community continues to press for long-standing features like Linux/Windows desktop apps and prebuilt Android APKs. The maintainer review queue is congested, with many popular issues labelled `clawsweeper:needs-maintainer-review` lingering for weeks.

---

## 2. Releases

### v2026.7.1-beta.2

- **Highlights:**
  - **OpenAI GPT-5.6 support** – OpenClaw now recognizes the GPT-5.6 model family across catalog, capability, and runtime selection paths ([#98333](https://github.com/openclaw/openclaw/issue/98333), thanks @steipete-oai).
  - **External harness attachment** – `openclaw attach` launches an external harness against an existing Gateway session.

- **Breaking changes / migration notes:** none provided in the release data.

---

## 3. Project Progress

**328 PRs were merged or closed today** – a sign of high development throughput. Among the most notable closed PRs:

- **[#68936](https://github.com/openclaw/openclaw/pull/68936) (CLOSED)** – **Autofix: add PR review autofix pipeline + Windows daemon.** A large (~785 line) pipeline that uses Claude Agent SDK to automatically address PR review comments, plus a Windows background daemon to run the loop and supervise the OpenClaw gateway.
- **[#100563](https://github.com/openclaw/openclaw/pull/100563) (CLOSED)** – **fix: warn when active transcript byte guard is inactive.** Resolves a silent configuration trap where `maxActiveTranscriptBytes` could be set but ignored unless `truncateAfterCompaction` was also enabled.
- **[#93972](https://github.com/openclaw/openclaw/pull/93972) (CLOSED)** – **fix(slack): keep agent identity on edited messages.** Edited Slack messages now preserve custom `username` and icon overrides – a regression fix for a long-standing UX complaint.

**Closed issues** (notable):
- **[#98239](https://github.com/openclaw/openclaw/issue/98239) (CLOSED)** – `[Bug]: /pair qr can change gateway.bind and break Tailscale Serve webchat` – a P1 security/state bug resolved.
- **[#48045](https://github.com/openclaw/openclaw/issue/48045) (CLOSED)** – `[Bug]: Browser tool silently discards downloads and throws "Download is starting" error when using CDP connection`.
- **[#96704](https://github.com/openclaw/openclaw/issue/96704) (CLOSED)** – `[Bug]: Managed browser cookies never persist to disk (in-memory only)` – refiled from stale issue #15645, now closed (likely fixed in a recent PR).

---

## 4. Community Hot Topics

The most active issues and PRs reveal strong demand for **cross-platform support**, **better tool reliability**, and **ecosystem maturity**.

| Issue / PR | Comments | Description |
|---|---|---|
| [#75](https://github.com/openclaw/openclaw/issue/75) – [OPEN] | **110** | Linux/Windows Clawdbot Apps – the single most-requested feature (👍 81). | 
| [#9443](https://github.com/openclaw/openclaw/issue/9443) – [OPEN] | **26** | Prebuilt Android APK releases – P0, ux-release-blocker. | 
| [#92201](https://github.com/openclaw/openclaw/issue/92201) – [OPEN] | **20** | Embedded runner: freshly streamed thinking signatures intermittently invalid on replay (Anthropic); recovery wrapper never fires. | 
| [#48788](https://github.com/openclaw/openclaw/issue/48788) – [OPEN] | **18** | Centralized filename encoding utility for multi-encoding Content-Disposition handling (Fix after Feishu fix). | 
| [#63918](https://github.com/openclaw/openclaw/issue/63918) – [OPEN] | **17** | Cron agent sends `thinking=none` to OpenAI GPT-5-nano even when configured `thinking=minimal`. |
| [#98416](https://github.com/openclaw/openclaw/issue/98416) – [OPEN] | **16** | v2026.6.11 published dist missing reentrancy guard – reply session initialization conflicted. |
| [#50090](https://github.com/openclaw/openclaw/issue/50090) – [OPEN] | **15** | Community Skill Development & ClawHub – the gap between promise and practice. |

**Underlying needs:** Users want a **first-class desktop experience** (Linux, Windows, prebuilt Android APK), **reliable streaming** (Anthropic thinking signatures, cron LLM parameters), and a **thriving skill ecosystem** (ClawHub). The high comment count on #75 and #50090 shows these are passionate, long-term blockers for adoption.

---

## 5. Bugs & Stability

Several high-severity bugs remain open or were newly reported. Listed by severity:

### P0 / Release-blocker
| Issue | Description | Fix status |
|---|---|---|
| [#9443](https://github.com/openclaw/openclaw/issue/9443) | Prebuilt Android APK releases missing – P0 ux-release-blocker | No linked fix PR |
| [#48920](https://github.com/openclaw/openclaw/issue/48920) | Live Docs are ahead of release (e.g., `IsolatedSessions` heartbeat config documented but not in v2026.3.13) | No linked fix PR |

### P1 / High impact
| Issue | Description | Fix status |
|---|---|---|
| [#92201](https://github.com/openclaw/openclaw/issue/92201) | Embedded runner: Anthropic thinking signatures invalid on replay; recovery wrapper broken | `clawsweeper:no-new-fix-pr` |
| [#98416](https://github.com/openclaw/openclaw/issue/98416) | v2026.6.11 missing reentrancy guard causes reply session init conflict | `clawsweeper:fix-shape-clear` (likely fixed in future) |
| [#48003](https://github.com/openclaw/openclaw/issue/48003) | Steer mode does not inject messages mid-turn for main sessions | `clawsweeper:linked-pr-open` (PR pending) |
| [#54155](https://github.com/openclaw/openclaw/issue/54155) | Gateway memory leak: 389MB → 14.7GB over 4 days | No linked fix PR |
| [#63918](https://github.com/openclaw/openclaw/issue/63918) | Cron agent sends `thinking=none` to models that only accept `minimal` | `clawsweeper:not-repro-on-main` |
| [#64810](https://github.com/openclaw/openclaw/issue/64810) | Heartbeat / async system events interrupt and swallow in-progress replies in Telegram topics | `clawsweeper:needs-live-repro` |
| [#29387](https://github.com/openclaw/openclaw/issue/29387) | Bootstrap files in `agentDir` silently ignored – only workspace directory files loaded | `clawsweeper:linked-pr-open` (PR pending) |

### Security-rated (P1/P2)
- [#45740](https://github.com/openclaw/openclaw/issue/45740) – `gh-issues` skill injects untrusted issue body directly into sub-agent prompt (P2)
- [#10659](https://github.com/openclaw/openclaw/issue/10659) – Masked Secrets: agent can see raw API keys (P1)
- [#7707](https://github.com/openclaw/openclaw/issue/7707) – Memory Trust Tagging by Source (P2)
- [#7722](https://github.com/openclaw/openclaw/issue/7722) – Filesystem Sandboxing Config (P2)
- [#50739](https://github.com/openclaw/openclaw/issue/50739) – System events cannot bypass congested queues for reliable alerts (P2)

**Newly fixed / closed bugs today:** #98239 (`/pair qr` Tailscale breakage), #48045 (CDP downloads), #96704 (browser cookies persistence). Several P1 memory and session-state bugs remain without a clear fix PR, which is a concern for production users.

---

## 6. Feature Requests & Roadmap Signals

### Most active community requests
| Issue | Description | Age |
|---|---|---|
| [#75](https://github.com/openclaw/openclaw/issue/75) | Linux/Windows Clawdbot Apps | Since 2026-01-01 |
| [#9443](https://github.com/openclaw/openclaw/issue/9443) | Prebuilt Android APK releases | Since 2026-02-05 |
| [#50090](https://github.com/openclaw/openclaw/issue/50090) | Community Skill Development & ClawHub ecosystem | Since 2026-03-19 |
| [#10659](https://github.com/openclaw/openclaw/issue/10659) | Masked Secrets: Prevent agent from seeing raw API keys | Since 2026-02-06 |
| [#35203](https://github.com/openclaw/openclaw/issue/35203) | Multi-Agent Collaboration: Capability Profiling + Shared Blackboard + Layered Memory + Token Cost Governance | Since 2026-03-05 |
| [#60572](https://github.com/openclaw/openclaw/issue/60572) | Multi-Slot Memory Architecture | Since 2026-04-03 |
| [#13700](https://github.com/openclaw/openclaw/issue/13700) | Session snapshots – save/load context checkpoints | Since 2026-02-10 |
| [#33975](https://github.com/openclaw/openclaw/issue/33975) | Fallback approval mode + model attribution in messages | Since 2026-03-04 |
| [#50199](https://github.com/openclaw/openclaw/issue/50199) | Skill Priority Configuration | Since 2026-03-19 |
| [#45565](https://github.com/openclaw/openclaw/issue/45565) | Route gateway lifecycle warnings to dedicated channel | Since 2026-03-14 |

### Prediction for next minor release
Given the **P0 label** on #9443 (prebuilt Android APK) and the fact that Android source already exists in `apps/android`, it is likely that the **next stable release will include prebuilt APK artifacts**. Additionally, the release of `v2026.7.1-beta.2` with GPT-5.6 support suggests that **OpenAI GPT-5.6 will be fully stable** in the imminent stable release. The **multi-slot memory** (#60572) and **masked secrets** (#10659) have seen renewed activity and may land in the `2026.7.x` cycle.

---

## 7. User Feedback Summary

- **Cross-platform frustration:** The top-voted issue (#75, 👍 81) and #9443 (P0) show that users on Linux, Windows, and Android feel underserved. Comments describe manual builds as “a significant barrier to entry.”
- **Reliability concerns:** Several users reported feeling **betrayed by silent failures** – e.g., cron jobs hallucinating output instead of erroring (#49876), messages lost on Discord attachment size limits (#99021), and cookies not persisting (#96704). These erode trust in production use.
- **Security awareness growing:** The push for **masked secrets** (#10659), **filesystem sandboxing** (#7722), and **memory trust tagging** (#7707) shows a mature user base concerned about prompt injection and credential leakage.
- **Skill ecosystem gap:** Users are enthusiastic about the ClawHub vision (#50090) but find the current implementation “wide gap between promise and practice.” Community-maintained skills lack publishing, installation, and discovery polish.
- **Satisfaction with speed:** The new GPT-5.6 support and high PR merge rate are seen as positive signals. One user noted: “The team is shipping fast, but the bugs pile up just as fast.”

---

## 8. Backlog Watch

Several important issues and PRs have been languishing without maintainer action for months. They are labelled with `clawsweeper:needs-maintainer-review` and/or `clawsweeper:no-new-fix-pr`.

### Stale high-value issues
| Issue | Title | Opened | Labels |
|---|---|---|---|
| [#75](https://github

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent Open-Source Ecosystem
**Date:** 2026-07-06 | **Analysis Period:** Last 24 Hours

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is bifurcating into two distinct tiers: high-throughput core reference implementations and leaner, platform-focused agents. OpenClaw and Hermes Agent represent the two poles—one a massive, fast-moving core with heavy bug debt, the other a more measured project prioritizing platform reliability and feature completeness. Both projects are shipping code daily, but the divergence in scale, bug density, and community expectations is becoming structural. The market is demanding cross-platform desktop experiences, MCP ecosystem maturity, and security hardening, while the maintainer bottleneck remains the dominant constraint on progress across both projects.

---

## 2. Activity Comparison

| Metric | OpenClaw | Hermes Agent |
|---|---|---|
| **Issues Updated (24h)** | 500 | 50 |
| **PRs Updated (24h)** | 500 | 50 |
| **PRs Merged/Closed (24h)** | 328 | 20 |
| **Issues Resolved (24h)** | 77 | 13 |
| **Release Today** | ✅ v2026.7.1-beta.2 | ❌ None |
| **Open P0/P1 Bugs** | 8+ (incl. memory leak, streaming, docs) | 4 (incl. stream loop, Ollama context, reconnect) |
| **Top Issue Community Demand** | 81 👍 (Linux/Windows desktop apps) | 41 👍 (Claude subscription OAuth) |
| **Health Score (Analyst Estimate)** | **Medium-High** – rapid iteration but heavy bug backlog and maintainer bottleneck | **High** – steady cadence, fewer regressions, better bug closure rate relative to volume |

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **First-mover on GPT-5.6 support** – ships model family integration ahead of Hermes, signaling tighter OpenAI partnership.
- **Massive merge throughput** – 328 PRs closed in 24 hours vs. Hermes' 20; engineering velocity is an order of magnitude higher.
- **Broader community engagement** – top issue has 81 👍 (vs. Hermes' 41), and 110 comments on the desktop apps request indicate a larger, more vocal user base.
- **Richer skill/plugin ecosystem ambition** – ClawHub vision, memory architectures, multi-agent collaboration features.

**Technical Approach Differences:**
- OpenClaw is **gateway-centric** with a heavy plugin/skill system; Hermes is **agent-focused** with MCP transport as primary extension mechanism.
- OpenClaw uses a "clawweeper" triage system for bug classification; Hermes uses salvage PR workflows and more manual maintainer coordination.
- OpenClaw's `attach` command and external harness support indicate a **developer toolchain orientation**; Hermes leans toward **end-user desktop/TUI UX**.

**Community Size Comparison:**
- OpenClaw: 500 issues/500 PRs updated daily → roughly **10x Hermes activity volume**.
- Hermes: 50/50 daily, but with higher closure ratios relative to volume (13/50 issues closed vs. 77/500 for OpenClaw).

**Key Vulnerability:** OpenClaw's bug density is proportionally higher. The P0/P1 list includes a memory leak (389MB→14.7GB), streaming signature failures, and cron parameter bugs—issues that erode production trust. Hermes, with fewer features, has fewer critical regressions.

---

## 4. Shared Technical Focus Areas

Both projects are converging on the same pain points, indicating industry-level requirements:

| Requirement | OpenClaw | Hermes Agent |
|---|---|---|
| **Cross-platform desktop apps** | #75 (81 👍) – Linux/Windows clawdbot apps; P0 Android APK | Windows desktop install reliability fixes (#59304, #59230); desktop-first UX |
| **MCP reliability** | MCP transport improvements in backlog | #38488 fix: MCP reconnection after transient outages; timeout fixes |
| **Security hardening** | Masked secrets (#10659), filesystem sandboxing (#7722), memory trust tagging | Feishu/WhatsApp oversized body patch (#54935); profile secret scoping (#59315) |
| **Streaming reliability** | #92201 – Anthropic thinking signatures invalid on replay | #58962 – "Stream stale" loop with OpenAI providers |
| **Skill/plugin ecosystem maturity** | #50090 – ClawHub publishing/installation gap | Plugin hook signature mismatches (#59262) |
| **Local model support** | (less emphasis) | #43900 – Ollama context caps; #42961 – cwd config ignored |

**Key Insight:** Cross-platform desktop support and MCP resilience are the two highest-urgency shared needs. Security hardening is maturing from feature request to active patching.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent |
|---|---|---|
| **Target User** | Developers, integrators, multi-agent orchestrators | End-users, desktop-centric workflows, Claude power users |
| **Primary Interface** | Gateway + CLI + web chat | Desktop app + CLI + TUI |
| **Extension Model** | Skills/plugins with ClawHub ecosystem | MCP servers + plugins |
| **Scale Ambition** | Massive – multi-agent collaboration, layered memory, token governance | Lean – practical UX, platform integration (Windows, reverse proxy) |
| **Risk Profile** | High velocity, high bug debt – "shipping fast, bugs pile up" | Moderate velocity, fewer regressions – "stability over breadth" |
| **Community Demand Signal** | Cross-platform frustration (81 👍) | Claude subscription OAuth (41 👍) – users want to avoid API fees |
| **Maturity Signal** | Persistent `clawsweeper:needs-maintainer-review` tagged issues → bottleneck | Better close ratio; salvage PR culture → cleaner backlog |

---

## 6. Community Momentum & Maturity

**Activity Tiers:**

| Tier | Project | Characteristics |
|---|---|---|
| **Tier 1: Hyperactive** | OpenClaw | 500+ daily updates; beta releases; heavy bug churn; maintainer bottleneck |
| **Tier 2: Very Active** | Hermes Agent | 50–100 daily updates; steady cadence; focused regression fixes; high closure efficiency |

**Rapid Iteration vs. Stabilization:**
- **OpenClaw** is in rapid iteration mode with beta releases. The priority is feature velocity (GPT-5.6, external harness, autofix pipelines) over bug reduction. This is appropriate for a core reference but risky for production dependents.
- **Hermes** is stabilizing – fewer new features, more salvage fixes, and desktop/Windows reliability improvements. The closure of long-running issues like `model_switch` tool (#16525) signals roadmap completion rather than expansion.

**Bottleneck Analysis:**
- OpenClaw has **hundreds** of issues tagged `clawsweeper:needs-maintainer-review`, some weeks old. The top-voted feature (#75) has been open since January 2026.
- Hermes has a more manageable queue but still has PR #2637 (quick shell command) open for months – a sign of selective prioritization.

---

## 7. Trend Signals

**1. Cross-platform is the new baseline.**
Both projects face intense pressure for Linux/Windows/Android support. Users on non-macOS platforms are increasingly vocal. Projects that fail to deliver desktop apps risk losing adoption to competitors (e.g., Claude Desktop, Copilot).

**2. Reliability trumps features.**
Community feedback across both projects shows growing fatigue with silent failures (cron hallucinations, lost messages, cookie persistence). Users want production-grade agents that fail loudly and recover gracefully. The "ship fast, fix later" model is hitting diminishing returns.

**3. Security is becoming a purchase criterion.**
Masked secrets, filesystem sandboxing, and memory trust tagging are moving from "nice to have" to "must have." Agentic systems that handle credentials, files, and long-term memory will face scrutiny from enterprise adopters.

**4. Autonomous model routing is in demand.**
Both communities want agents that can self-select models based on task complexity. OpenClaw's multi-agent collaboration features and Hermes' `model_switch` tool (now implemented) signal a trend toward **intelligent routing** rather than manual model selection.

**5. Claude ecosystem lock-in anxiety.**
Hermes' #25267 (Claude subscription OAuth, 41 👍) reveals user desire to decouple from API pricing. This suggests growing demand for **provider-agnostic agent frameworks** that can work with subscription models or local models.

**6. MCP is the extension protocol of choice.**
Both projects treat MCP as the primary extension mechanism. Reliability fixes (reconnection timeouts, permanent abandonment) indicate MCP is transitioning from experimental to production-critical infrastructure.

**Value for AI Agent Developers:**
- Invest in **cross-platform desktop builds** – this is the #1 adoption blocker.
- Prioritize **MCP resilience** – retry logic, timeouts, reconnection semantics are table stakes.
- Build **autonomous model routing** – agents that choose models dynamically will differentiate your product.
- Implement **credential masking** early – retrofitting security is expensive.
- Watch **Claude OAuth support** – if Hermes implements it, expect pressure on all competitors to follow.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-06

## Today's Overview

Project activity remains **very high**: 50 issues and 50 pull requests were updated in the last 24 hours. Of these, 13 issues and 20 PRs were closed/merged, indicating sustained development velocity. No new releases were published today, but a large batch of salvage PRs (many by @teknium1) addresses long-standing bugs across the gateway, MCP transport, desktop, and CLI. Community engagement is strong, particularly around the request for Claude subscription OAuth support (#25267, 41 👍) and the new model-switch tool idea (#16525). The project is actively fixing regressions and stability issues while rolling out features for multiplex profiles, approval routing, and desktop shortcuts.

---

## Releases

**None** — No new releases were tagged on 2026-07-06.

---

## Project Progress

### Merged / Closed PRs (from top-20 list)

- **[PR #59304](https://github.com/NousResearch/hermes-agent/pull/59304)** `[CLOSED]` — fix(install): guard Windows desktop installs against broken web_server (salvage of #59230). Merged after syntax-checking `web_server.py` before install completion; auto-rollback on parse failure.
- **[PR #59230](https://github.com/NousResearch/hermes-agent/pull/59230)** `[CLOSED]` — Original fix for Windows desktop installs: prevents a successful install when `web_server.py` contains syntax errors.

Both PRs improve the **Windows desktop installation reliability** and are merged today.

### Issues closed (13 total; selected notable)

- **[#16525](https://github.com/NousResearch/hermes-agent/issues/16525)** `[CLOSED]` — Feature: Expose `model_switch` as an agent-callable tool. This long-running request (since April) was resolved, enabling autonomous complexity-based routing.
- **[#38488](https://github.com/NousResearch/hermes-agent/issues/38488)** `[CLOSED]` — Bug: MCP server permanently gives up after transient backend outage. A fix was applied to allow reconnection without gateway restart.
- **[#57129](https://github.com/NousResearch/hermes-agent/issues/57129)** `[CLOSED]` — Bug: MCP client permanently abandons server after 5 failed reconnects. Closed as duplicate of #38488, indicating a systematic fix.
- **[#24097](https://github.com/NousResearch/hermes-agent/issues/24097)** `[CLOSED]` — Bug: MCP OAuth login hard timeout at 40s. Fixed – per-server `connect_timeout` is now respected.
- **[#59257](https://github.com/NousResearch/hermes-agent/issues/59257)** `[CLOSED]` — Bug: Desktop-first commits silently degrading CLI/TUI – session title lost on exit. Fix merged.
- **[#54935](https://github.com/NousResearch/hermes-agent/issues/54935)** / **[#54940](https://github.com/NousResearch/hermes-agent/issues/54940)** `[CLOSED]` — Security: Feishu/WhatsApp webhook oversized body buffering before 413 check. Patched.

---

## Community Hot Topics

### Most commented issues

| Issue | Comments | 👍 | Summary |
|-------|----------|----|---------|
| [#16525](https://github.com/NousResearch/hermes-agent/issues/16525) | 9 | 5 | Feature: model_switch as agent-callable tool (now closed) |
| [#34390](https://github.com/NousResearch/hermes-agent/issues/34390) | 9 | 0 | Feature: dashboard `--allowed-hosts` flag for reverse-proxy/Tailscale |
| [#25267](https://github.com/NousResearch/hermes-agent/issues/25267) | 9 | **41** | Feature: Claude Agent SDK model provider with subscription OAuth (Codex-style) — **highest demand** |
| [#43900](https://github.com/NousResearch/hermes-agent/issues/43900) | 8 | 0 | Bug: Ollama local models silently capped at 4096-token context |
| [#42961](https://github.com/NousResearch/hermes-agent/issues/42961) | 8 | 0 | Bug: terminal.cwd config ignored for local backend |

**Underlying needs:**
- **#25267** reveals a strong user desire to use Claude without paying both subscription and API fees. This is the most upvoted request and may drive future provider integration work.
- **#16525** (now closed) addressed a demand for autonomous agent routing — many users want their agent to self-select the right model for the task.
- **#34390** reflects growing use of Hermes behind reverse proxies; users want to safely expose the dashboard via Tailscale or Nginx.

### Active PRs (no comment count available, but high engagement through reactions)

- **[PR #2637](https://github.com/NousResearch/hermes-agent/pull/2637)** `[OPEN]` — "Add quick shell command feature (!cmd)" — oldest open PR, still awaiting merge. Users want non-LLM shell execution.
- **[PR #59309](https://github.com/NousResearch/hermes-agent/pull/59309)** — fix(agent): recover leaked clarify JSON envelopes — addresses local model failure mode.
- **[PR #59315](https://github.com/NousResearch/hermes-agent/pull/59315)** — fix(gateway): read platform env overrides through the profile secret scope — security improvement for multiplex mode.

---

## Bugs & Stability

### P1 (Critical)
- **[PR #59313](https://github.com/NousResearch/hermes-agent/pull/59313)** (open) — fix(desktop/windows): pre-write update marker before quit dwell to prevent backend respawn. Windows desktop updates can brick if the renderer respawns the backend during the update hand-off. Patch available in this open PR.
- **[PR #59230](https://github.com/NousResearch/hermes-agent/pull/59230)** (closed), **[#59304](https://github.com/NousResearch/hermes-agent/pull/59304)** (closed) — Windows installs broken by syntax errors in `web_server.py`. Now fixed.

### P2 (High)
- **[#58962](https://github.com/NousResearch/hermes-agent/issues/58962)** `[OPEN]` — Sessions permanently stuck in "Stream stale" loop with OpenAI-compatible provider. No fix PR identified yet. Affects retries after timeout. 🚩
- **[#43900](https://github.com/NousResearch/hermes-agent/issues/43900)** `[OPEN]` — Ollama local models capped at 4096-token context despite GGUF metadata showing larger context. PR needed.
- **[#42961](https://github.com/NousResearch/hermes-agent/issues/42961)** `[OPEN]` — `terminal.cwd` config ignored for local backend. Process cwd used instead.
- **[#59224](https://github.com/NousResearch/hermes-agent/issues/59224)** `[OPEN]` — CLI `/resume` listing hides Desktop and WebUI sessions (only shows source="cli").
- **[#59272](https://github.com/NousResearch/hermes-agent/issues/59272)** `[OPEN]` — QQAdapter.connect() misses `is_reconnect` parameter, causing TypeError on reconnect. Fix PR **[#59317](https://github.com/NousResearch/hermes-agent/pull/59317)** open.
- **[#57129](https://github.com/NousResearch/hermes-agent/issues/57129)** `[CLOSED]` — MCP client abandons server after 5 reconnects – duplicate of #38488 (now fixed).
- **[#41556](https://github.com/NousResearch/hermes-agent/issues/41556)** `[OPEN]` — Desktop app sends file path instead of image data when pasting images.
- **[#54147](https://github.com/NousResearch/hermes-agent/issues/54147)** `[OPEN]` — `hermes chat -m <model>` uses stale `api_mode` from config default → 404 on opencode-go.

### P3 (Medium/Low)
- **[#59262](https://github.com/NousResearch/hermes-agent/issues/59262)** `[OPEN]` — Plugin `transform_terminal_output` hook signature mismatch warns on every gateway message.
- **[#59244](https://github.com/NousResearch/hermes-agent/issues/59244)** `[OPEN]` — Background memory review ignores configured memory provider (only writes legacy memory).
- **[#38669](https://github.com/NousResearch/hermes-agent/issues/38669)** `[OPEN]` — Web UI chat scrollbar cannot scroll to bottom.
- **[#38419](https://github.com/NousResearch/hermes-agent/issues/38419)** `[OPEN]` — Desktop app "Prompt snippets" submenu clipped inside attachment menu container.
- **[#10943](https://github.com/NousResearch/hermes-agent/issues/10943)** `[OPEN]` — Model repeatedly hits max output tokens when continuing prompts (Chinese user).

### Regression Watch
- **[#59257](https://github.com/NousResearch/hermes-agent/issues/59257)** `[CLOSED]` — Desktop-first commits degraded CLI/TUI: session title lost on exit. Now fixed, but indicates risk of cross-platform regressions.

---

## Feature Requests & Roadmap Signals

### High Demand / Likely in Next Version

| Issue | 👍 | Description | Likelihood |
|-------|----|-------------|------------|
| [#25267](https://github.com/NousResearch/hermes-agent/issues/25267) | 41 | Claude subscription OAuth support | Medium – requires new provider integration |
| [#16525](https://github.com/NousResearch/hermes-agent/issues/16525) | 5 | Model-switch tool (now closed/implemented) | Done |
| [#59308](https://github.com/NousResearch/hermes-agent/issues/59308) | 

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*