# AI CLI Tools Community Digest 2026-06-09

> Generated: 2026-06-09 02:45 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: Claude Code vs. OpenAI Codex
**Date:** 2026-06-09

---

## 1. Ecosystem Overview

The AI CLI development tools ecosystem is entering a phase of **mature differentiation**, where both major players—Anthropic's Claude Code and OpenAI's Codex—ship weekly releases while facing growing user expectations around reliability and parity. Community engagement remains high, with both tools seeing 50+ active issues daily, but the nature of complaints is shifting: users are less excited about new features and more vocal about **consistency bugs, platform-specific regressions, and missing automation surfaces**. Claude Code leads in raw customization surface (skills, plugins, hooks, MCP), while Codex is closing the gap with its own hook system and desktop-first workflow enhancements. The emerging competitive battleground is **hybrid local/cloud workflows**, cross-platform stability, and MCP tool permission management.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Issues Updated (24h)** | 50+ (estimated) | ~25-30 (from 10 hot issues + background) |
| **Hot Issues Tracked** | 10 noteworthy | 10 noteworthy |
| **Open PRs** | 5 (1 merged, 4 active) | 10 (all active/merged) |
| **Releases Today** | v2.1.169 (stable) | rust-v0.138.0 (stable) + v0.139.0-alpha.1 |
| **Top Issue Engagement** | #63060 (79 comments, 30 👍) – API credit errors | #26892 (76 comments, 28 👍) – gpt-5.5 model not found |
| **Highest Feature Request** | #30154 (165 👍) – Multi-window Desktop | #25144 (65 👍) – Disable auto .txt conversion |

**Key Takeaway:** Claude Code has higher raw community engagement volume (more issues and comments), but Codex is shipping more PRs per day and maintaining parallel stable/alpha release trains. Both have a comparable "peak complaint" intensity.

---

## 3. Shared Feature Directions

The following requirements appear across **both** communities, indicating cross-cutting user needs:

| Shared Need | Claude Code Evidence | OpenAI Codex Evidence |
|---|---|---|
| **Multi-window / multi-session UI** | #30154 (165 👍) – Desktop multi-window, tabs | #25144 (65 👍) – better prompt management; #23218 – clear context between tasks |
| **Conversation/state branching** | #32631 (30 👍) – fork/merge/tree navigation | Goal API improvements in PR #26953 (persisted goals) |
| **Automation surface (hooks/plugins)** | Plugin ecosystem (PRs #65286, #65619); hooks in `--safe-mode` | #21753 (15 👍) – Full Claude Code hook parity requested |
| **Local→cloud hybrid workflows** | #66373 (new) – local-to-cloud handoff | #8758 (closed, delivered) – image gen; desktop handoff via `/app` |
| **Image support** | Narrower (MCP tools for Chrome) | Delivered in 0.138.0 – local image attachments + standalone gen |
| **Windows/WSL performance** | No equivalent issue cited | #25715 (36 👍) – WSL slow; #26149 (16 👍) – `/mnt/c` scanning |
| **macOS resource issues** | #5674 (36 👍) – ECONNRESET | #25719 (20 👍) – `syspolicyd` CPU runaway |
| **MCP tool approval UX** | #61044 – broken approval UI in Routines | #24135 – non-interactive MCP approval in `codex exec` |

**Insight:** The shared pain points are in **platform stability** (Windows/macOS), **session management** (branching, clearing, multi-window), and **automation maturity** (hooks, MCP approvals). Neither tool has solved the "long-running agent without context corruption" problem well.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary Focus** | Deep customization (plugins, skills, hooks, MCP servers) | Desktop-first UX, image generation, `/app` handoff |
| **Target User** | Power developers building custom agent pipelines | Broader developer audience, including non-CLI desktop users |
| **Release Cadence** | ~weekly stable, no alpha/beta channel visible | Dual-track: stable + alpha releases (e.g., 0.138.0 stable, 0.139.0-alpha.1) |
| **Telemetry & Observability** | OTLP support (though #66401 reports macOS gaps) | Performance spans in PR #27094, analytics in PR #27103 |
| **Model Ecosystem** | Opus 4.x family; reports of CLI vs Desktop model mismatch (#66410) | GPT-5.5 listed but broken (#26892); stronger model availability confusion |
| **Plugin/Extension Model** | MCP servers + custom `plugin.json` manifests; ecosystem growth visible | Hooks via injected providers (PR #27101); less mature plugin system |
| **Security Model** | `--safe-mode` for troubleshooting; symlink hardening (PR #66171) | Guardian auto-review (PR #27062, #27109); `--dangerously-bypass-*` flags |
| **Standout Feature** | `/cd` command preserves prompt cache across directories | Image generation + `/app` desktop handoff |

**Key Difference:** Claude Code is **extensibility-first**—its community builds plugins, MCP servers, and skills. Codex is **desktop-integration-first**—image gen, `/app` window handoff, and WSL support matter more. Claude Code suffers from feature bloat (many moving parts = more bugs), while Codex has fewer hooks but more consistent shipping.

---

## 5. Community Momentum & Maturity

| Indicator | Claude Code | OpenAI Codex |
|---|---|---|
| **Community Size** | Larger raw activity (50+ issues/24h, 165 👍 top request) | Smaller but vocal (65 👍 top request, 76 comments on blocker) |
| **Iteration Speed** | Steady weekly stable releases; fewer PRs/day | Faster release cadence (alpha + stable parallel); 10 PRs today |
| **Bug Recurrence** | High: #5674 ECONNRESET (9 months), #27897 Cowork VM (months) | Moderate: #21671 `/compact` regression fixed; #26880 fsmonitor fixed quickly |
| **Feature Maturity** | Plugin/hook ecosystem maturing; `/cd` and `--safe-mode` show polish | Desktop integration maturing; hooks still chasing parity |
| **Observability for Enterprise** | OTLP support exists but buggy (#66401) | Better telemetry instrumentation visible (spans, analytics, cached tokens) |
| **Windows Support** | Poor – Cowork VM broken on Insider | Poor – WSL extreme slowness, GitHub OAuth fail |

**Verdict:** Claude Code has **more community momentum** (higher engagement, richer requests), but Codex is **shipping faster** with fewer regressions per release. Claude Code's community is more invested (higher upvote counts on issues), suggesting deeper dependency on the tool. Codex's community skews toward desktop/WSL users facing platform-specific friction.

---

## 6. Trend Signals for Developers

### Emerging Industry Trends from Community Feedback

1. **Model transparency is breaking trust.** Both communities report confusion between CLI/Desktop model selections (#66410 in Claude Code, #26892 in Codex). Developers need **deterministic model routing** and clear versioning—especially as context windows grow (1M in Claude Code) and model families multiply. **Action:** If evaluating tools, prioritize those that expose the exact model ID and context window in the session header.

2. **MCP/hook permissions are the new "sudo."** Across both tools, MCP tool approval is broken, undocumented, or dangerous (Claude Code #61044, Codex #24135). As agentic workflows expand, the **permission model becomes the critical bottleneck** for production deployment. **Action:** Demand a documented, auditable permission model before building automated pipelines on either tool.

3. **Hybrid local/cloud is the next must-have.** Claude Code's #66373 (local→cloud handoff) and Codex's `/app` desktop bridge point to a clear trend: developers want to start sessions locally and escalate to cloud execution. Neither tool has a seamless story here. **Action:** Watch for both tools to ship bidirectional handoff within 2-3 releases.

4. **Performance on non-macOS platforms is neglected.** Both tools have open, months-old performance bugs on Windows (Claude Code Cowork VM, Codex WSL) and macOS (Claude Code ECONNRESET, Codex `syspolicyd`). This suggests both teams prioritize macOS/Linux as primary targets. **Action:** Windows/WSL users should budget extra friction; consider containerized workflows to mitigate.

5. **Observability is becoming a requirement, not a nice-to-have.** Claude Code's OTLP (#66401) and Codex's performance spans (PR #27094) and cached token analytics (PR #27103) show both teams investing in telemetry. **Action:** Choose the tool with the better telemetry story if you need to monitor agent costs and performance at scale—currently Codex has more visible instrumentation.

6. **The "long agent" problem is unsolved.** Conversation branching (#32631 in Claude Code), context clearing (#23218 in Codex), and context loss on upgrade (#66406) all stem from the same root cause: **sessions are fragile and linear**. Neither tool has a robust session persistence model. **Action:** Plan for session corruption; build checkpoint/restore workflows externally.

### Recommendation for Decision-Makers

- **Choose Claude Code if** you need deep customization (plugins, skills, MCP servers), have a macOS/Linux team, and can tolerate more bugs in exchange for richer extensibility.
- **Choose OpenAI Codex if** you need desktop integration, image generation, faster release cadence, and better telemetry—and your team is willing to accept fewer hooks and current model availability issues.
- **Avoid both for production Windows/WSL workflows** until platform-specific performance bugs are resolved.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

**Data snapshot:** 2026-06-09 | **Source:** github.com/anthropics/skills (official Skills repository)

---

## 1. Top Skills Ranking

The following Pull Requests have generated the most discussion (sorted by comment count). All remain **open** as of this report.

### #1 – Document Typography Skill (`document-typography`)
[PR #514](https://github.com/anthropics/skills/pull/514) | Author: PGTBoos | Created: 2026-03-04

Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. The skill targets a universal frustration for anyone using Claude to produce polished output. Discussion highlights include proposals to extend the skill to cover table formatting and hyphenation rules.

---

### #2 – ODT / OpenDocument Skill (`odt`)
[PR #486](https://github.com/anthropics/skills/pull/486) | Author: GitHubNewbie0 | Created: 2026-03-01

Enables the creation, filling, reading, and conversion of ISO-standard ODF files (.odt, .ods). The conversation focused on whether to include LibreOffice macro execution and the complexity of template placeholders. The skill is seen as a gateway for enterprise users stuck in Microsoft Office–only environments.

---

### #3 – Frontend Design Skill Clarity Improvement
[PR #210](https://github.com/anthropics/skills/pull/210) | Author: justinwetch | Created: 2026-01-05

A rewrite of the existing `frontend-design` skill to ensure every instruction is actionable within a single conversation. The debate centered on balancing prescriptive rules with creative freedom. Several reviewers requested visual output examples.

---

### #4 – Skill Quality & Security Analyzers
[PR #83](https://github.com/anthropics/skills/pull/83) | Author: eovidiu | Created: 2025-11-06

Two meta-skills that evaluate other skills across structure, documentation, and security dimensions. Discussion highlights include tooling integration (automated CI checks) and potential false-positive concerns.

---

### #5 – PDF Case‑Sensitivity Fix
[PR #538](https://github.com/anthropics/skills/pull/538) | Author: Lubrsy706 | Created: 2026-03-06

Corrects 8 case‑sensitive file references in `skills/pdf/SKILL.md` that break on case‑sensitive file systems. Minimal controversy but high practical impact for Linux/macOS users. The conversation touched on broader cross‑platform consistency in the repository.

---

### #6 – Skill‑Creator YAML Validation
[PR #539](https://github.com/anthropics/skills/pull/539) | Author: Lubrsy706 | Created: 2026-03-06

Adds a pre‑parse check in `quick_validate.py` to catch unquoted `description` fields containing colons. The PR triggered a conversation about extending validation to other YAML frontmatter fields and integrating linting into the skill creation workflow.

---

### #7 – DOCX Tracked Change ID Collision Fix
[PR #541](https://github.com/anthropics/skills/pull/541) | Author: Lubrsy706 | Created: 2026-03-06

Prevents document corruption when the DOCX skill adds tracked changes to files with existing bookmarks. The root cause (`w:id` collision in OOXML) was well explained; community feedback highlighted the need for a general ID generation strategy for all OOXML skills.

---

### #8 – SAP Predictive Analytics Skill (`SAP-RPT-1-OSS`)
[PR #181](https://github.com/anthropics/skills/pull/181) | Author: amitlals | Created: 2025-12-28

Uses SAP’s open‑source tabular foundation model for predictive analytics on business data. Discussion focused on model availability, API authentication patterns, and whether the skill should also cover data extraction from SAP S/4HANA.

---

## 2. Community Demand Trends

From the most‑commented Issues (24 total exceeding 2 comments), three clear demand vectors emerge:

| Demand Vector | Key Issues | Signal |
|---------------|------------|--------|
| **Org‑wide skill management** | [#228](https://github.com/anthropics/skills/issues/228) (13 comments) – enable direct sharing, shared libraries. [#492](https://github.com/anthropics/skills/issues/492) (7 comments) – namespace security audit needed. | Strong enterprise push for governance and collaboration beyond single‑user `.skill` files. |
| **Tooling / Developer Experience stability** | [#556](https://github.com/anthropics/skills/issues/556) (11 comments) – `run_eval.py` 0% trigger rate. [#1169](https://github.com/anthropics/skills/issues/1169) (2 comments) – recall always 0% in optimization loop. [#202](https://github.com/anthropics/skills/issues/202) (8 comments) – `skill-creator` needs rewrite. | Community is hitting hard‑to‑diagnose bugs in skill development and evaluation toolchain. |
| **Skill packaging & portability** | [#189](https://github.com/anthropics/skills/issues/189) (6 comments) – duplicate skills from overlapping plugins. [#1220](https://github.com/anthropics/skills/issues/1220) (2 comments) – multi‑file preload. [#1156](https://github.com/anthropics/skills/issues/1156) (2 comments) – per‑skill portability labels. | Users want clear contracts for skill composition, versioning, and cross‑project reuse. |

Minor but notable themes: **agent governance** ([#412](https://github.com/anthropics/skills/issues/412)), **Bedrock compatibility** ([#29](https://github.com/anthropics/skills/issues/29)), and **MCP exposure of Skills** ([#16](https://github.com/anthropics/skills/issues/16)).

---

## 3. High‑Potential Pending Skills

These active‑comment PRs have not yet merged but show signs of imminent landing or strong community interest:

- **[PR #1140 – agent‑creator skill + multi‑tool evaluation fix](https://github.com/anthropics/skills/pull/1140)**  
  Meta‑skill to build task‑specific agent sets. Addresses evaluation stability and Windows support. Closes #1120.

- **[PR #723 – testing‑patterns skill](https://github.com/anthropics/skills/pull/723)**  
  Covers full testing stack (unit, React, integration, E2E) with Testing Trophy philosophy. High demand for better testing guidance.

- **[PR #568 – ServiceNow platform skill](https://github.com/anthropics/skills/pull/568)**  
  Broad support for ITSM, ITOM, SecOps, ITAM, FSM, and IntegrationHub. Enterprise users eagerly awaiting a single‑source skill for ServiceNow.

- **[PR #444 – AURELION skill suite (kernel, advisor, agent, memory)](https://github.com/anthropics/skills/pull/444)**  
  Structured cognitive framework plus persistent memory. The four‑skill bundle is ambitious; discussion centers on overlap with existing memory/context skills.

- **[PR #190 – n8n builder + debugger skills](https://github.com/anthropics/skills/pull/190)**  
  Two production‑tested skills for building and debugging n8n workflows. Includes a bonus FAF‑expert skill. Community feedback is positive, with requests for MCP support.

- **[PR #363 – feature‑dev workflow fix (TodoWrite overwrite bug)](https://github.com/anthropics/skills/pull/363)**  
  Addresses a bug where quality‑review and summary phases are skipped. Essential for anyone using the `/feature-dev` workflow in anger.

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for robust, enterprise‑grade developer tooling and lifecycle management (evaluation, sharing, security, packaging) rather than new domain skills themselves.**

---

# Claude Code Community Digest — 2026-06-09

## Today's Highlights
Anthropic shipped **v2.1.169** with a `--safe-mode` flag for troubleshooting customizations and a new `/cd` command to move sessions without cache loss. Community activity remains high, with **50+ issues updated in 24 hours** — bug reports around model consistency between CLI and desktop/app extensions, OTLP telemetry gaps, and MCP permission gaps dominate. The most popular feature request (**#30154**, multi-window Desktop) continues to gather steam (165 👍).

---

## Releases
**[v2.1.169](https://github.com/anthropics/claude-code/releases/tag/v2.1.169)** – *June 9, 2026*
- **`--safe-mode` flag** (and `CLAUDE_CODE_SAFE_MODE` env var) — starts Claude Code with all customizations (CLAUDE.md, plugins, skills, hooks, MCP servers) disabled, intended for troubleshooting.
- **`/cd` command** — moves a session to a new working directory without breaking the prompt cache, enabling seamless context-preserving directory switches.

---

## Hot Issues (10 Noteworthy)

1. **[#63060 – [BUG] API Error: Usage credits required for 1M context](https://github.com/anthropics/claude-code/issues/63060)** – 79 comments, 30 👍  
   Users hitting credit errors when attempting 1M-context sessions. High discussion volume; may indicate billing edge cases or API rate limiting.

2. **[#30154 – [FEATURE] Multi-window support in Claude Code Desktop](https://github.com/anthropics/claude-code/issues/30154)** – 55 comments, 165 👍  
   The #1 community request: opening multiple windows in a single Desktop app instance. Current single-window/sidebar design limits multitasking.

3. **[#5674 – [BUG] Persistent ECONNRESET Errors on macOS](https://github.com/anthropics/claude-code/issues/5674)** – 41 comments, 36 👍  
   Long-standing network issue on macOS causing connection drops; not reproducible on Windows/Linux. High frustration among Mac users.

4. **[#27897 – [BUG] Cowork VM broken on Windows 11 Insider (MSIX)](https://github.com/anthropics/claude-code/issues/27897)** – 35 comments, 14 👍  
   EXDEV rename bug in v1.1.4010 makes Cowork VM unusable on Windows 11 Insider builds. Regression that has persisted for months.

5. **[#29573 – [BUG] Claude creating file limit filesystem bug on long sessions](https://github.com/anthropics/claude-code/issues/29573)** – 16 comments, 22 👍  
   Filesystem limits hit after long or many sessions, potentially crashing user workflows. Under-reported but serious.

6. **[#32631 – [FEATURE] Conversation Branching (fork, merge, tree navigation)](https://github.com/anthropics/claude-code/issues/32631)** – 9 comments, 30 👍  
   Full spec for improving `/fork` into true branching with merge and tree navigation. Consolidates several older locked issues.

7. **[#43255 – [BUG] Claude in Chrome MCP tools: "Navigation to this domain is not allowed"](https://github.com/anthropics/claude-code/issues/43255)** – 13 comments, 7 👍  
   Regression in v1.0.66 for Chrome MCP tools – all domains blocked. Impacting web automation workflows.

8. **[#61044 – [BUG] MCP tool calls in CCR Routines fail with "requires approval" — no UI shown](https://github.com/anthropics/claude-code/issues/61044)** – 6 comments, 3 👍  
   MCP approvals broken in Routines mode; reconnect doesn't help. Blocks automated pipelines.

9. **[#66373 – [FEATURE] CLI command to hand off local session to cloud (inverse of `--teleport`)](https://github.com/anthropics/claude-code/issues/66373)** – 2 comments (brand new, June 9)  
   Request for a `local→web` handoff. Shows growing interest in hybrid local/cloud workflows.

10. **[#66410 – [BUG] Desktop app shows non-1M Opus 4.8 while CLI says 1M for same session](https://github.com/anthropics/claude-code/issues/66410)** – 1 comment (June 9)  
   Model inconsistency between CLI and Desktop app for the same session. A sign of broader model selection bugs (see #66403, #66407).

---

## Key PR Progress (5 Total)

1. **[#65286 – fix(plugins): add missing plugin.json manifest for plugin-dev](https://github.com/anthropics/claude-code/pull/65286)**  
   Adds the missing manifest so the `plugin-dev` plugin can be discovered and installed normally. Small but important for plugin ecosystem health.

2. **[#65619 – fix(plugins): align frontend-design author with marketplace entry](https://github.com/anthropics/claude-code/pull/65619)** *(Closed)*  
   Fixes malformed author/email fields in `frontend-design` plugin manifest. Clean merge that resolves #61785.

3. **[#66372 – fix(devcontainer): detect Docker daemon failures via $LASTEXITCODE](https://github.com/anthropics/claude-code/pull/66372)**  
   Fixes a PowerShell try/catch bug that silently ignores Docker daemon failures. Now reports correctly when Docker Desktop is not running.

4. **[#26914 – docs: add rules frontmatter paths syntax examples and validation hook](https://github.com/anthropics/claude-code/pull/26914)** *(Closed)*  
   Adds example files and a PostToolUse hook to validate `paths:` syntax in rules frontmatter – preventing silent failures that have confused users.

5. **[#66171 – [#64582] [BUG] extensibility.py follows symlinks in project-controlled gui](https://github.com/anthropics/claude-code/pull/66171)**  
   Addresses security concern where `extensibility.py` follows symlinks in GUI-controlled project directories. Includes reproduction guide and hardening.

---

## Feature Request Trends

Examining all open issues reveals three dominant feature directions:

- **Multi-window / multi-session UI** – #30154 (165 👍) and related requests for tabs, folders, and concurrent session views in both Desktop and CLI.
- **Conversation branching and state management** – #32631 (30 👍) outlines full fork/merge/tree navigation; #66373 asks for local→cloud handoff; multiple issues request CLI commands to better manage long-running agents.
- **Per-agent configuration** – Several bugs (#66402, #66403, #66407) point to the inability to set per-agent model/effort without global side effects. #66352 requests user-level skill discovery for cross-agent workflows.
- **Custom keybindings and UI actions** – #66399 (open settings.json via keybinding) and #66398 (cursor visibility) highlight desire for deeper TUI customization.

---

## Developer Pain Points

- **MCP permission inconsistencies** – Issues #61044, #64521, #66380: MCP tool approvals configured on claude.ai are not honored in CLI; Routines mode shows no approval UI; policy enforcement windows undocumented. This is a recurring frustration for teams building automated pipelines.
- **Model and context mismatches** – #66410, #66403, #66407, #66404: The CLI, Desktop app, and VSCode extension disagree on the selected model (Opus 4.6 vs 4.8, 1M vs non-1M). Updates can silently change the model in Cowork spaces.
- **Context loss on upgrade** – #66406: Clicking "software upgrade" during an active session destroys context; no resume mechanism.
- **Network stability (macOS)** – #5674: ECONNRESET errors persist for over 9 months on Mac, while Windows/Linux are unaffected.
- **Telemetry not emitted** – #66401: OTLP metrics/logs silently dropped on macOS TUI despite correct env vars, complicating observability for enterprise deployments.
- **Tool output corruption** – #66396: Japanese text in large tool outputs becomes corrupted and fabricated on Windows, a localization/encoding bug.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-09

## Today's Highlights

Codex desktop and CLI saw two notable improvements: the `/app` command can now hand off directly to a permanent desktop window on macOS and Windows, and local image attachments as well as standalone image generation are now supported. However, the community is sharply focused on a broken model – `gpt-5.5` is listed as available but all requests fail with a 404, affecting both Desktop and CLI users (Issue #26892, 76 comments). A long-standing request to disable automatic conversion of long pasted prompts into `.txt` attachments has drawn 65 👍 and 52 comments (Issue #25144).

## Releases

- **rust-v0.138.0 (stable)** – New `/app` command can hand off the CLI thread into Codex Desktop on macOS and native Windows; Windows workspace launches can now open directly into Desktop. Local image attachments and standalone image generation added.
- **rust-v0.139.0-alpha.1** – First alpha for the next minor version.
- **rust-v0.138.0-alpha.7 / .alpha.8** – Pre-release iterations of the stable 0.138.0 line.

## Hot Issues (10 Noteworthy)

1. **[#26892 – gpt-5.5 model not found (OPEN)](https://github.com/openai/codex/issues/26892)**  
   Model metadata shows `gpt-5.5` as available, but actual API calls return 404 “Model not found”. Affects both Desktop and CLI on all platforms. 76 comments, 28 👍.

2. **[#25144 – Option to disable automatic long-prompt → .txt conversion (OPEN)](https://github.com/openai/codex/issues/25144)**  
   Users want a toggle to prevent Codex App from converting long pasted prompts into `.txt` attachments. High demand (65 👍, 52 comments).

3. **[#25203 – GitHub OAuth callback fails on Windows (OPEN)](https://github.com/openai/codex/issues/25203)**  
   “Unable to find Electron app” error when connecting GitHub from Codex Desktop on Windows. 37 comments, 21 👍.

4. **[#25715 – WSL agent environment extremely slow (OPEN)](https://github.com/openai/codex/issues/25715)**  
   Codex Desktop becomes unusably slow when using WSL as the agent environment. 36 comments, 36 👍.

5. **[#21671 – `/compact` fails with unknown `service_tier` parameter (CLOSED)](https://github.com/openai/codex/issues/21671)**  
   Regression in 0.129.0: `/compact` returns an API parameter error. Root cause and fix still being debated (25 comments).

6. **[#8758 – Image generation from Codex (CLOSED)](https://github.com/openai/codex/issues/8758)**  
   Long-running feature request to generate images natively within Codex. Now closed–likely delivered in 0.138.0’s image support. 55 👍.

7. **[#24675 – Stale app connector link after reauth (OPEN)](https://github.com/openai/codex/issues/24675)**  
   Codex Desktop keeps using a stale connector link until the local cache is manually cleared. 21 comments.

8. **[#25719 – macOS `syspolicyd` / `trustd` CPU runaway (OPEN)](https://github.com/openai/codex/issues/25719)**  
   Codex Desktop triggers persistent high CPU usage from macOS security daemons. 20 comments, 20 👍.

9. **[#26149 – Windows + WSL repeatedly scans `.codex/.tmp/plugins` over `/mnt/c` (OPEN)](https://github.com/openai/codex/issues/26149)**  
   Causing severe per-command latency. 10 comments, 16 👍.

10. **[#21753 – Full Claude Code Hook Parity (OPEN)](https://github.com/openai/codex/issues/21753)**  
    Umbrella request for 29+ hooks to match Claude Code’s automation surface. 11 comments, 15 👍.

## Key PR Progress (10 Important)

1. **[#27094 – Add spans to `build_tool_router`](https://github.com/openai/codex/pull/27094)**  
   Adds performance tracing to the tool router, which averages ~113ms per call. Enables future optimizations.

2. **[#27101 – Load user instructions through an injected provider](https://github.com/openai/codex/pull/27101)**  
   Removes implicit `$CODEX_HOME` dependency from `codex-core`, making embedders responsible for user instructions.

3. **[#26880 – Preserve fsmonitor for worktree Git reads](https://github.com/openai/codex/pull/26880)**  
   Fixes a performance bug where Codex forced `core.fsmonitor=false` on internal Git commands, causing full scans in large repos.

4. **[#27109 – Add Guardian catalog diagnostics metadata](https://github.com/openai/codex/pull/27109)**  
   Provides request-level evidence when `codex-auto-review` is missing from the client-side model catalog, aiding debugging.

5. **[#27062 – Retry transient Guardian review failures](https://github.com/openai/codex/pull/27062)**  
   Auto Review (Guardian) now retries transient session failures, reducing false permission prompts.

6. **[#25704 – Normalize Codex images for Responses strict mode](https://github.com/openai/codex/pull/25704)**  
   Feature-flagged strict mode for the Responses API: converts local/data URL images before sending to `/responses`.

7. **[#27039 – Add detached async command hooks](https://github.com/openai/codex/pull/27039)**  
   Enables hooks configured with `async: true` to run non-blocking, delivering results on a later user turn.

8. **[#27103 – Report cached input tokens for v2 compaction](https://github.com/openai/codex/pull/27103)**  
   Adds `cached_input_tokens` to compaction analytics, giving visibility into prompt-cache usage for v2 compaction.

9. **[#27105 – Refresh account plan from usage](https://github.com/openai/codex/pull/27105)**  
   Treats the plan returned by `/usage` as authoritative, fixing stale plan data after plan changes.

10. **[#26953 – Add dedicated Python SDK goal operations](https://github.com/openai/codex/pull/26953)**  
    Exposes a goal API in the Python SDK that matches how the TUI drives persisted goals, enabling true goal-based workflows.

## Feature Request Trends

The most requested directions, distilled from top issues:

- **Automation surface parity** – Users want Claude Code-level hooks (Issue #21753, 15 👍) and an Agent View in the TUI (Issue #22321, 9 👍).
- **UI/UX polish** – Disable automatic .txt conversion (Issue #25144, 65 👍), allow use of externally created worktrees (Issue #12863, 8 👍), and support multiple accounts (Issue #12029, 43 👍).
- **Platform integration** – Native image generation (now delivered in 0.138.0), improved Computer Use browser controls (Issue #25271, #23222), and seamless clearing of context between tasks (Issue #23218).
- **Non-interactive tool usage** – Ability to approve MCP tool calls in `codex exec` without the dangerous `--dangerously-bypass-*` flag (Issue #24135).

## Developer Pain Points

Recurring frustrations from the community:

- **Windows + WSL performance** – Two separate issues (#25715, #26149) detail extreme slowness due to WSL-related scanning and process creation. Combined 52 👍 and 46 comments.
- **Model availability confusion** – `gpt-5.5` being listed but unusable (#26892) is the top complaint, with a secondary report of GPT-5.5 xhigh stalling on Bedrock (#26860).
- **Authentication on Windows** – GitHub OAuth fails (#25203) and stale app connectors (#24675) force manual cache clearing.
- **macOS resource leaks** – Crashpad dumps growing to 5 GB (#25921) and `syspolicyd`/`trustd` CPU runaway (#25719) affect daily use.
- **Regression sensitivity** – The `/compact` `service_tier` regression (#21671) and the removal of core.fsmonitor (#26880 before fix) show that even minor changes can have outsized impact on developer workflows.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*