# AI CLI Tools Community Digest 2026-07-10

> Generated: 2026-07-10 02:37 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date**: 2026-07-10 | **Analysis**: Senior Technical Analyst, AI Developer Tools Ecosystem

---

## 1. Ecosystem Overview

The AI CLI tools landscape is in a high-velocity maturation phase, with both major players shipping weekly releases while grappling with the complexities of multi-agent orchestration, authentication architecture, and flagship model reliability. Claude Code and OpenAI Codex are converging on shared challenges—permission models for agent workflows, MCP integration stability, and session state management—but diverging in their approach to sandboxing, model transparency, and community engagement. The community signals that reliability and developer trust are becoming more critical than raw feature velocity, as premium-tier subscribers increasingly report regressions in flagship models and billing/auth friction that undermines confidence in both platforms.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Notable Issues (today)** | 10 hot issues tracked; 2 top issues exceed 500 👍 combined | 10 hot issues tracked; top issue at 279 👍 |
| **PR Activity (last 24h)** | 3 PRs (all documentation/fixes, same contributor) | 10+ architecturally significant PRs (multi-contributor) |
| **Release Status** | v2.1.206 (stable); quality-of-life and diagnostics | rust-v0.144.0, v0.144.1 (stable); v0.145.0-alpha.1/.2 (pre-release) |
| **Community Reaction Velocity** | Higher per-issue engagement (642 👍 on top issue) | Broader issue distribution; lower max reactions but more issues with PR follow-through |
| **Bug Report Density** | High — multiple model reliability, workflow orchestration, and billing issues | High — usage-limit anomalies, installation gaps, authentication instability |
| **Documentation/Infra Focus** | Low PR throughput; documentation fixes suggest maintenance mode | Higher PR throughput; focused on sandboxing, permission models, and runtime hardening |

**Key Observation**: Claude Code has higher community engagement per issue but lower PR velocity. OpenAI Codex shows stronger development throughput but faces more fragmented community feedback.

---

## 3. Shared Feature Directions

The following requirements appear across **both** communities, indicating industry-wide needs:

| Shared Need | Claude Code Evidence | OpenAI Codex Evidence |
|---|---|---|
| **Multi-agent workflow control** | #73633 (subagent permission inheritance), #71723 (agent protocol switching) | #31662 (restrict subagent environments), #31814 (hidden MultiAgent V2 controls) |
| **MCP/tool integration stability** | #76228 (params serialized as strings), #73544 (custom tools invisible) | #31970 (MCP handshake timeout), #30295/30294 (OAuth recovery routing) |
| **Model selection transparency** | #72871 (see/choose model per routine), #65476 (managed settings for "Default" model) | #31927 (5.6 not available on SSH), #31814 (model auto-hides routing controls) |
| **Session/workspace organization** | #75856 (reorderable groups), #73928 (choose working directory before first message) | #11022 (thread references lost on folder move), #31655 (move workspace roots onto environments) |
| **Authentication & billing robustness** | #5088 (account disabled after payment), #18435/#20131 (multi-account profiles) | #28672 (repeated 401/forced phone verification), #30212/#31601 (usage-limit anomalies) |

**Takeaway**: The industry is converging on the need for **granular, inheritable permission models** for multi-agent systems, **robust MCP authentication** (especially OAuth recovery), and **transparent model selection** that survives across environments (local, remote, containerized).

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Primary Focus** | Context management & directory navigation; `CLAUDE.md` trimming diagnostics (`/doctor`); multi-account profile switching | Sandboxing & permission-model refactors; exec-server hardening; usage-limit credit system |
| **Target Users** | Power users with complex project contexts; teams sharing `CLAUDE.md` files; Max plan subscribers needing billing reliability | Enterprise/containerized environments; Pro/Business users needing sandbox trust; multi-environment executors |
| **Technical Approach** | Community-driven issue prioritization; smaller, incremental releases (v2.1.x patch stream); CLI-first with Desktop companion | Systematic architectural changes (PR stacks like #30295/#30294); pre-release alpha channels; Rust-based backend with exec-server isolation |
| **Model Reliability** | Opus 4.8 issues (#67606 confabulation, #64774 unparseable tool calls) — flagship model showing regression | GPT-5.5 reasoning-token clustering (#30364) — suspected server-side allocation issue affecting complex tasks |
| **Installation Friction** | Minimal reported issues; `/cd` path suggestions reduce typing friction | Homebrew cask missing binary (#31906); standalone install metadata handling issues |
| **Community Contribution Velocity** | Low PR throughput (3 docs/fixes today); high issue engagement | Higher PR throughput (10+ architectural PRs); more structured contribution pattern |

**Differentiation Signal**: Claude Code is optimizing for **user experience polish** and **context hygiene**, while OpenAI Codex is investing in **sandbox trust boundaries** and **runtime reliability** for enterprise-scale deployments.

---

## 5. Community Momentum & Maturity

### Claude Code
- **Maturity Level**: Maturing but facing trust issues. High community engagement (642 👍 on multi-account profile issue) indicates a passionate, invested user base that expects premium reliability.
- **Iteration Velocity**: Moderate. Weekly patches (v2.1.206) but low PR throughput suggests a smaller core team or prioritization of bug fixes over feature development.
- **Risk Signals**: The Opus 4.8 model reliability issues (#67606, #64774) are serious for a premium-tier product. Confabulation of user messages is a trust-and-safety concern that could drive users to competitors.
- **Strength**: Strong community feature requests with clear signal; the `/doctor` diagnostic shows responsiveness to context-file hygiene needs.

### OpenAI Codex
- **Maturity Level**: Rapidly iterating with architectural ambition. The pre-release alpha channels (v0.145.0-alpha) and systematic sandboxing PRs suggest a team comfortable with breaking changes.
- **Iteration Velocity**: High. Multiple releases, significant PR stacks, and multiple contributors signal a well-resourced development organization.
- **Risk Signals**: Usage-limit anomalies (#30212, #31601) erode trust in the billing model. The single Homebrew cask issue (#31906) affects first-impression reliability for new macOS users.
- **Strength**: Architectural depth in sandboxing (permission profile intersection in URI space, bounding exec-server frame sizes) positions Codex well for enterprise compliance requirements.

**Community Maturity Comparison**: Claude Code has a **louder, more organized community** with higher per-issue reaction counts, suggesting deeper grassroots investment. OpenAI Codex has a **broader, more distributed community** with higher development throughput, suggesting stronger institutional backing.

---

## 6. Trend Signals

### For Technical Decision-Makers

1. **Flagshship Model Reliability is a Top-3 Concern** — Both platforms show flagship model regressions (Opus 4.8 confabulation, GPT-5.5 reasoning-token clustering). If you are deploying AI CLI tools in production, **test against multiple model versions** and consider fallback strategies to older, more stable models.

2. **Multi-Agent Orchestration is Still Proof-of-Concept** — Both platforms have multi-agent capabilities, but both also have critical bugs (permission inheritance, silent protocol switches, hidden routing controls). Do not yet rely on sub-agent workflows for production-critical tasks without extensive testing.

3. **Sandboxing & Permission Models Are Becoming Baseline Requirements** — OpenAI Codex's systematic investments (exec-server frame bounds, URI-space permission intersection, workspace root refactoring) signal that **enterprise compliance** is driving architecture decisions. Expect all major tools to follow this trajectory.

4. **MCP Integration Fragility is a Cross-Platform Issue** — Both communities report MCP handshake timeouts, parameter serialization regressions, and authentication gaps. The MCP ecosystem is still immature; **vendor lock-in risk is higher than usual**.

5. **Billing and Authentication Flow Resilience is Underinvested** — Both platforms have zero-trust incidents (account disabled after payment, usage-limit anomalies, repeated forced phone verification). For enterprise deployments, **plan for alternative authentication pathways** and monitor billing status programmatically.

6. **Context Management is Becoming a Differentiator** — Claude Code's `/doctor` diagnostic and directory path suggestions, combined with community demand for session organization (#75856), indicate that **managing AI context (not just generating code) is a growing UX concern**. Developers should evaluate how each tool handles long-running sessions, shared context files, and workspace organization.

7. **Platform-Specific Gaps Matter for First Impressions** — OpenAI Codex's Homebrew cask issue and Claude Code's Windows Advisor regression (#73365) highlight that **operating system parity is still not guaranteed**. For teams with heterogeneous development environments, test across your target platforms before committing.

### Reference Value for Developers

| If you need... | Consider Claude Code for... | Consider OpenAI Codex for... |
|---|---|---|
| Multi-account/profile switching | Strong community demand; likely incoming | Not a prominent community priority |
| Enterprise sandbox compliance | Less mature; community-led | Active architectural investment |
| Context file hygiene | `/doctor` diagnostic, `CLAUDE.md` focus | No equivalent feature |
| Model selection transparency | Growing demand (#72871) | Hidden routing controls (negative signal) |
| Stable multi-agent workflows | Permission inheritance bugs (#73633) | Subagent environment restrictions (#31662) |
| macOS installation reliability | Minimal reported issues | Homebrew cask gap (#31906) |

---

**Bottom Line**: Both tools are shipping weekly but experiencing growing pains as they scale from "demo-quality" to "production-quality" developer tools. Claude Code leads on community engagement and context-management UX; OpenAI Codex leads on sandboxing architecture and development velocity. Neither is enterprise-grade on all dimensions today, but the rate of improvement suggests either could achieve that status within 6-12 months.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-07-10 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following new Skill proposals have drawn the most community attention (by comments/engagement). All are currently **open**.

| Skill | Author | Created | Functionality | Discussion Summary |
|-------|--------|---------|---------------|-------------------|
| **[document-typography](https://github.com/anthropics/skills/pull/514)** | PGTBoos | 2026-03-04 | Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI‑generated documents. Addresses common typographic issues Claude introduces. | Strong interest from developers producing long‑form documents; debate over whether to bundle with existing document skills. |
| **[ODT](https://github.com/anthropics/skills/pull/486)** | GitHubNewbie0 | 2026-03-01 | Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Includes template filling and ODT‑to‑HTML parsing. | Requested by LibreOffice users and enterprise teams; discussion on dependency management for ODF libraries. |
| **[frontend-design (improved)](https://github.com/anthropics/skills/pull/210)** | justinwetch | 2026-01-05 | Revises the existing frontend‑design skill for clarity, actionability, and single‑conversation usability. | Community agreed the original skill was too vague; PR refines concrete instructions and removes ambiguous guidance. |
| **[skill-quality-analyzer + skill-security-analyzer](https://github.com/anthropics/skills/pull/83)** | eovidiu | 2025-11-06 | Two meta‑skills: quality analysis (structure, documentation, examples, tests, YAML) and security analysis (prompt injection, data exfiltration, privilege escalation). | Early meta‑skill proposal sparked debate about scoping and false positives; maintainers have requested benchmarks. |
| **[testing-patterns](https://github.com/anthropics/skills/pull/723)** | 4444J99 | 2026-03-22 | Comprehensive testing skill covering unit, React, integration, E2E, snapshot, visual regression, and performance testing. Based on the Testing Trophy model. | Well‑received, but some reviewers want a shorter, more trigger‑focused version. |
| **[self-audit](https://github.com/anthropics/skills/pull/1367)** | YuhaoLin2005 | 2026-06-28 | Audits AI output before delivery: mechanical file verification followed by four‑dimension reasoning quality gate. Universal across projects and models. | Very recent; early commentary praises the structured verification step. |
| **[SAP-RPT-1-OSS predictor](https://github.com/anthropics/skills/pull/181)** | amitlals | 2025-12-28 | Wraps SAP’s open‑source tabular foundation model for predictive analytics on SAP business data. | Niche but high‑value for enterprise users; discussions on API key management and model size. |
| **[color-expert](https://github.com/anthropics/skills/pull/1302)** | meodai | 2026-06-10 | Color expertise skill covering naming systems (ISCC‑NBS, Munsell, RAL, etc.), color spaces (OKLCH, OKLAB, CAM16), and accessibility contrast. | Designers and data‑viz developers actively testing it; requests to add color‑blind simulation. |

---

## 2. Community Demand Trends

Based on the most‑commented issues, the community’s most‑anticipated new directions are:

| Direction | Key Issue(s) | What the Community Wants |
|-----------|--------------|--------------------------|
| **Skill sharing & organization** | [#228](https://github.com/anthropics/skills/issues/228) | Org‑wide skill libraries, direct sharing links, and a centralised marketplace within Claude.ai. |
| **Security & trust boundaries** | [#492](https://github.com/anthropics/skills/issues/492) | Clearer namespace separation between official and community skills; permission‑audit tooling. |
| **Agent governance & safety** | [#412](https://github.com/anthropics/skills/issues/412) | Policy enforcement, threat detection, trust scoring, and audit trails for AI agents. |
| **MCP integration** | [#16](https://github.com/anthropics/skills/issues/16) | Expose Skills as MCP servers for interoperable tool use across different AI platforms. |
| **Windows compatibility** | [#1061](https://github.com/anthropics/skills/issues/1061), [#556](https://github.com/anthropics/skills/issues/556) | Fix subprocess handling, encoding, and pipe reading in skill‑creator scripts so they work on native Windows. |
| **Skill‑creator reliability** | [#556](https://github.com/anthropics/skills/issues/556), [#1169](https://github.com/anthropics/skills/issues/1169) | Eliminate the persistent `recall=0%` bug that renders the optimisation loop ineffective. |
| **Compact agent memory** | [#1329](https://github.com/anthropics/skills/issues/1329) | Symbolic notation for compact agent state to reduce context usage in long‑running sessions. |

---

## 3. High‑Potential Pending Skills

The following Skill PRs have active discussion and are likely to merge soon:

- **[testing-patterns](https://github.com/anthropics/skills/pull/723)** – updated 2026-04-21. Could land after streamlining per reviewer feedback.
- **[self-audit](https://github.com/anthropics/skills/pull/1367)** – updated 2026-07-02. Very recent; strong early interest and clear scope.
- **[color-expert](https://github.com/anthropics/skills/pull/1302)** – updated 2026-06-12. Awaiting final tweaks (color‑blind simulation).
- **[skill-quality-analyzer + skill-security-analyzer](https://github.com/anthropics/skills/pull/83)** – updated 2026-01-07. Long‑running but maintainers are evaluating benchmarks; may merge as example skills.
- **[document-typography](https://github.com/anthropics/skills/pull/514)** – updated 2026-03-13. Close to consensus; could be merged with minor formatting adjustments.

---

## 4. Skills Ecosystem Insight

The community’s most concentrated demand is for **reliable, production‑ready skill‑creator tooling** (fixes for the `recall=0%` bug, Windows support, and YAML parsing) – without these, the entire skill development pipeline delivers no signal – while simultaneously pushing for **practical quality‑focused Skills** (typography, testing patterns, output auditing, and security analysis) that solve real‑world document and code defects.

---

# Claude Code Community Digest — 2026-07-10

## Today's Highlights

Claude Code shipped **v2.1.206** with quality-of-life improvements to directory navigation and a new `/doctor` check for trimming overly verbose `CLAUDE.md` files. The community remains fixated on multi-account management (two issues in the top 5 by reaction count) and a critical billing block affecting Max 5x subscribers. A flurry of bugs around **Opus 4.8 model reliability**, **agent workflow retry behavior**, and **MCP parameter serialization** dominated new reports.

## Releases

### [v2.1.206](https://github.com/anthropics/claude-code/releases/tag/v2.1.206)
- **`/cd` now includes directory path suggestions** — mirrors the autocomplete behavior already available in `/add-dir`, reducing manual typing for navigation.
- **New `/doctor` diagnostic** — checks if `CLAUDE.md` files checked into version control contain content Claude could derive directly from the codebase, and proposes trimming. Helps teams keep context files lean and focused on non-derivable knowledge.
- **`/commit-push-pr` auto-allows `git push`** — removes the permission prompt for pushing to the repository's configured remote, streamlining the most common commit-to-PR workflow.

## Hot Issues (10 notable picks)

1. **[#5088 — Account Disabled After Payment for Claude Code Max 5x Plan](https://github.com/anthropics/claude-code/issues/5088)**
   *180 comments, 59 👍* — Payment goes through, but the account is immediately locked out of both code and claude.ai. No resolution surfaced; billing/oncall label. Critical for Max subscribers.

2. **[#18435 — Multi-account profile switching in Desktop app](https://github.com/anthropics/claude-code/issues/18435)**
   *126 comments, 642 👍* — Highest-reacted open issue. Users with separate personal/professional or API/subscription accounts must fully re-authenticate to switch. Community clearly wants profile-native switching.

3. **[#73365 — Advisor always "unavailable" on Windows (Fable 5 / Opus 4.8)](https://github.com/anthropics/claude-code/issues/73365)**
   *47 comments, 91 👍* — Cross-session regression blocking Windows users from the Advisor feature. Duplicate-labeled but the volume suggests a real platform-specific gap.

4. **[#20131 — Multi-Account Profile Support (CLI)](https://github.com/anthropics/claude-code/issues/20131)**
   *37 comments, 96 👍* — Companion to #18435 but focused on the terminal CLI. Single-auth constraint is a regular complaint among power users juggling billing models.

5. **[#20944 — Disable Automatic IDE Selection Context](https://github.com/anthropics/claude-code/issues/20944)**
   *20 comments, 67 👍* — Users want the ability to stop Claude from auto-sensing IDE context (cursor selection, open files) when they don't need it, citing cost and noise.

6. **[#67606 — Opus 4.8 confabulates user messages and fabricates "prompt injection" narratives](https://github.com/anthropics/claude-code/issues/67606)**
   *12 comments* — Two independent sessions with JSONL evidence. The model invents user messages, a fake prompt-injection story, and falsified host facts. Serious trust-and-safety concern for the flagship model.

7. **[#28379 — Slash commands not processed in `/remote-control` UI](https://github.com/anthropics/claude-code/issues/28379)**
   *11 comments, 51 👍* — Remote sessions from claude.ai/code or mobile forward `/clear`, `/compact` etc. as plain text. Blocks remote power use.

8. **[#64774 — Opus 4.8 emits unparseable tool calls at ~1.5% rate](https://github.com/anthropics/claude-code/issues/64774)**
   *6 comments* — Structured output fails 1.5% of the time with `claude-opus-4-8`; no failures on `opus-4-7` or `sonnet-4-6`. Points to a regression in the model's tool-call grammar.

9. **[#71723 — Agent `name` parameter silently switches to teammate protocol, losing results](https://github.com/anthropics/claude-code/issues/71723)**
   *6 comments* — A subtle behavioral bug: passing a `name` in sessions with team config causes background agents to take a teammate code path, discarding their results.

10. **[#73633 — Workflow subagents don't inherit `permissions.allow` from `settings.local.json`](https://github.com/anthropics/claude-code/issues/73633)**
    *5 comments, 5 👍* — Multi-agent workflows (e.g., `deep-research`) spawn subagents that ignore project-level allow-rules, prompting for tool permissions on every call. Defeats the purpose of permission pre-approval.

## Key PR Progress

Only 3 PRs were updated in the last 24 hours, all opened by the same contributor and all documentation or small fixes:

1. **[#76029 — docs(plugin-dev): use flat format in .mcp.json example](https://github.com/anthropics/claude-code/pull/76029)**
   Fixes a docs example that wrapped `.mcp.json` inside an `mcpServers` object (a `plugin.json` concept). Now shows the correct flat format, resolving confusion reported in #63694.

2. **[#76028 — docs(plugin-dev): fix stale marketplace name in README](https://github.com/anthropics/claude-code/pull/76028)**
   The `plugin-dev` README referenced an incorrect marketplace package name (`plugin-dev@claude-code-marketplace` instead of the canonical `claude-code-marketplace` scope). Fixes #70064.

3. **[#76023 — fix: detect GitHub Actions CI using directory test](https://github.com/anthropics/claude-code/pull/76023)**
   The SessionStart hook example tested `.github/workflows` with `-f` (regular file), but it's always a directory on disk. GitHub Actions CI detection was therefore always false-positive. Switched to `-d`.

## Feature Request Trends

1. **Multi-Account & Profile Management** — #18435 (642 👍) and #20131 (96 👍) dominate the reaction board. The community wants seamless switching between personal/professional accounts in both Desktop and CLI. The fact that both remain open suggests a non-trivial auth architecture change is needed.

2. **Session & Workspace Organization** — #75856 (reorderable groups, folder-linked shared context) and #73928 (choose working directory before first message in Desktop) reflect a maturing user base that needs session lifecycle controls beyond single-session workflows.

3. **Model Selection Transparency** — #72871 (see/choose model per routine) and #65476 (managed settings for "Default" model label in picker) show demand for finer-grained control over which model powers which task, particularly in enterprise/proxy deployments.

## Developer Pain Points

- **Model reliability erodes trust**: #67606 (confabulation of fake user messages) and #64774 (1.5% unparseable tool calls) both target Opus 4.8, the premium tier. If the flagship model is less reliable than its predecessors, users paying for Max are getting a degraded experience.
- **Agent & workflow orchestration fragility**: #71723 (agent name silently switches protocol), #73633 (permission inheritance broken for subagents), and #70475 (no retry on transient server errors) reveal that the multi-agent system, while powerful, has edge cases that lose work or force re-runs.
- **Billing/auth friction**: #5088 (account disabled after successful payment) is a zero-trust incident for paying Max 5x subscribers. Combined with #76237 (Fable 5 missing from `/model` after re-login), authentication and subscription state management appear prone to hard failures.
- **Tool and MCP integration regressions**: #76228 (MCP params serialized as strings — a regression) and #73544 (custom connector tools invisible in new conversations) suggest the MCP/tool infrastructure has ongoing quality issues after recent Desktop releases.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-10

## Today’s Highlights
A flurry of sandboxing and permission-model refactors landed in the `main` branch, alongside critical bug fixes in the CLI’s macOS Homebrew cask and standalone install scripts. The community remains intensely focused on two themes: unexplained usage-limit depletion and the impact of GPT‑5.5 reasoning‑token clustering on complex task performance.

## Releases
- **rust‑v0.144.1** – Patch release fixing standalone installs when GitHub returns compact or reordered release metadata, and ensuring macOS packages expose the `code-mode` host alongside the `codex` executable. Also includes a fallback when the companion host binary is unavailable.
- **rust‑v0.144.0** – Introduces usage‑limit reset credits with type/expiration display and the ability to choose which credit to redeem. Adds a `writes` app‑approval mode that allows declared read‑only actions while prompting for writes. MCP tools can now request authentication interactively.
- Pre‑release builds **v0.145.0‑alpha.1** and **v0.145.0‑alpha.2** are also available with no detailed changelog.

## Hot Issues (Top 10 by Community Attention)

1. **#30364** – **GPT‑5.5 reasoning‑token clustering at 516/1034/1552**  
   *Open, 179 comments, 279 👍* – Community analysis shows `gpt‑5.5` responses disproportionately land at fixed reasoning‑token boundaries, coinciding with degraded performance on complex tasks. Many suspect a server‑side allocation issue.  
   [GitHub](https://github.com/openai/codex/issues/30364)

2. **#2153** – **ChatGPT integration (closed)**  
   *Closed, 42 comments, 150 👍* – Longstanding request to move Codex sessions into ChatGPT for brainstorming and web search, then bring results back. Closure may indicate the feature is being absorbed into the merged ChatGPT/Codex app.  
   [GitHub](https://github.com/openai/codex/issues/2153)

3. **#31906** – **Homebrew cask missing `codex-code-mode-host`**  
   *Open, 8 comments, 33 👍* – `codex` 0.144.0 installed via Homebrew fails with “failed to spawn code-mode host” because the supporting binary is not bundled. Affects all commands.  
   [GitHub](https://github.com/openai/codex/issues/31906)

4. **#11022** – **Thread references lost when project folders are moved**  
   *Open, 19 comments, 48 👍* – Moving a project directory makes all conversation threads inaccessible. Users want a migration/update mechanism for thread references.  
   [GitHub](https://github.com/openai/codex/issues/11022)

5. **#30212** – **Usage limit depleted abnormally (5‑hour allowance in 1 hour)**  
   *Open, 10 comments, 9 👍* – Pro subscriber reports that the 20x usage allowance is consumed far faster than expected, with no excessive active work. Suggests a counting or back‑off bug.  
   [GitHub](https://github.com/openai/codex/issues/30212)

6. **#28672** – **Business Codex: repeated 401 / forced phone verification**  
   *Open, 9 comments* – Two‑seat Business account in US/Ubuntu dev container gets OAuth token revocations after a few messages, requiring repeated phone verification. Makes Codex unusable for enterprise users in containers.  
   [GitHub](https://github.com/openai/codex/issues/28672)

7. **#31814** – **GPT‑5.6 Sol hides MultiAgent V2 subagent routing controls**  
   *Open, 7 comments, 9 👍* – The new model auto‑selects MultiAgent V2 and sets `hide_spawn_agent_metadata` to `true`, removing routing knobs that users relied on. Workaround needed.  
   [GitHub](https://github.com/openai/codex/issues/31814)

8. **#31601** – **Usage‑limit reset failed, quota is gone**  
   *Open, 6 comments, 3 👍* – User attempted a reset that failed, leaving zero quota. Indicates a gap in reset‑failure handling.  
   [GitHub](https://github.com/openai/codex/issues/31601)

9. **#31970** – **Slack/Atlassian MCP handshake timeout after update**  
   *Open, 2 comments* – Built‑in `codex_apps` connectors fail with a 30‑second timeout on MCP startup after a desktop update. Previously working connectors now broken.  
   [GitHub](https://github.com/openai/codex/issues/31970)

10. **#31927** – **GPT‑5.6 not available on remote SSH projects**  
    *Open, 3 comments* – Pro users note that the 5.6 model family only appears in local projects, not when connected via Remote SSH.  
    [GitHub](https://github.com/openai/codex/issues/31927)

## Key PR Progress (Top 10 by Architectural Impact)

1. **#31976** – **Retry previous‑model compaction with selected model**  
   Automatic retry on compaction errors that may be due to model availability or capacity. Shares retry logic across remote implementations.  
   [GitHub](https://github.com/openai/codex/pull/31976)

2. **#31782** – **Bound stdio JSON‑RPC frame size**  
   Adds a 64 MiB ceiling on `BufReader::lines()` to prevent runaway frame retention from a misbehaving exec‑server.  
   [GitHub](https://github.com/openai/codex/pull/31782)

3. **#31781** – **Bound executor‑controlled HTTP response buffering**  
   Further hardens sandbox trust boundaries by limiting per‑frame and total buffered response data from the remote exec‑server.  
   [GitHub](https://github.com/openai/codex/pull/31781)

4. **#31919** – **Preserve empty workspace roots in exec‑server**  
   Fixes a bug where empty root lists were silently replaced with the sandbox cwd, breaking callers that intentionally selected no workspace roots.  
   [GitHub](https://github.com/openai/codex/pull/31919)

5. **#31975** – **Sandboxing: intersect foreign permission profiles in URI space**  
   Prevents host‑OS reinterpretation of foreign paths by performing permission‑profile intersection in URI space rather than via the coordinator host OS.  
   [GitHub](https://github.com/openai/codex/pull/31975)

6. **#31951** – **Assume all bundled models support reasoning summaries**  
   Removes the no‑op override `model_supports_reasoning_summaries = false`, simplifying config and making custom models consistent with the catalog.  
   [GitHub](https://github.com/openai/codex/pull/31951)

7. **#31960** – **Add URI permission transforms**  
   Generic merge helpers and URI‑native normalization for sandbox permissions, enabling remote/executor callers to preserve URI semantics.  
   [GitHub](https://github.com/openai/codex/pull/31960)

8. **#31662** – **Allow restricting subagent environments**  
   Adds optional `environment_ids` to `spawn_agent`, letting parent turns limit which execution environments child agents can access.  
   [GitHub](https://github.com/openai/codex/pull/31662)

9. **#31655** – **Move workspace roots onto environments**  
   Removes the thread‑global workspace‑root state and stores roots inside execution environments, fixing a source of `cwd`/root divergence that caused remote‑sandbox context issues.  
   [GitHub](https://github.com/openai/codex/pull/31655)

10. **#30295 / #30294 (stack)** – **Serialize and route MCP OAuth recovery through Codex**  
    Two‑PR stack that implements OAuth login/logout serialization and routes recovery through the Codex app, adding interactive authentication for MCP tools.  
    [PR #30295](https://github.com/openai/codex/pull/30295), [PR #30294](https://github.com/openai/codex/pull/30294)

## Feature Request Trends
- **ChatGPT deep integration** (#2153) – The desire to fluidly move between Codex CLI and a web‑based UI for research/brainstorming remains the most‑voted feature request, now possibly being addressed by the merged ChatGPT/Codex desktop app.
- **Thread/project portability** (#11022) – Several requests (19 comments, 48 👍) ask for the ability to move or rename project folders without losing conversation threads.
- **Default Plan mode** (#13942) – Users want a config option to start CLI sessions in Plan mode rather than the default interactive mode.
- **Expand reasoning by default** (#3248) – In IDEs (VS Code), a setting to always expand thinking/working segments without manual clicking is repeatedly requested (21 👍).
- **Model availability parity** – Multiple issues (#31927, #29663) highlight frustration that newer models (5.6) are not accessible in remote SSH or certain container environments.

## Developer Pain Points
- **Usage‑limit anomalies** – Several reports (#30212, #31601, #31450) describe quota being consumed faster than expected or reset failures leaving zero balance. The new credit‑type UI in v0.144.0 may help, but the underlying counting bugs persist.
- **Installation & binary gaps** – The Homebrew cask missing `codex-code-mode-host` (#31906) and standalone‑install metadata handling (#31913‑related) continue to trip up new users.
- **Authentication instability** – Enterprise/Business users in containerized environments (#28672) face repeated token revocations and forced phone verification, making Codex unusable.
- **MCP integration fragility** – Handshake timeouts (#31970) and Chrome extension connectivity differences between terminal and app-bundled executables (#31980) erode trust in the MCP ecosystem.
- **Stale state after hard shutdown** – #31982 reports that Codex resumes from a checkpoint older than the current VCS state when killed abruptly, risking overwritten work. This is especially painful for long‑running agent sessions.
- **MultiAgent V2 transparency** – #31814 warns that hidden subagent controls reduce user oversight, and the community is pushing for configuration overrides.

*Digest generated from `github.com/openai/codex` activity on 2026-07-10.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*