# AI CLI Tools Community Digest 2026-06-26

> Generated: 2026-06-26 02:56 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem

## 1. Ecosystem Overview

The AI CLI tools landscape is maturing rapidly, with both Claude Code and OpenAI Codex addressing increasingly complex developer workflows—from model-assisted coding to MCP-based extensibility. While feature velocity remains high, community discourse has shifted from pure capability to cost governance, platform reliability, and transparent model behavior. Both tools face pressure to deliver stable, predictable experiences as adoption scales to production-critical environments. The emergence of shared pain points—rate-limit confusion, OAuth lifecycle management, and cross-platform parity—signals that the ecosystem is converging on common infrastructure challenges.

## 2. Activity Comparison (Based on 2026-06-26 Digests)

| Metric | Claude Code | OpenAI Codex |
|--------|------------|--------------|
| **Hot Issues highlighted** | 10 (from top 30) | 10 (from top 30) |
| **PRs updated/mentioned** | 1 (closed) | 10 (multiple statuses) |
| **Latest stable release** | v2.1.193 | rust-v0.142.2 + alphas |
| **Notable issue engagement** | Highest: #3412 (269👍, 76 comments) | Highest: #28224 (385👍, 86 comments) |
| **Critical cost/performance bug** | #71481 – $506 silent upgrade | #28879 – 10-20× cost jump |
| **Platform regressions** | Multiple (ARM64, VSCode, desktop) | Multiple (Windows sandbox, macOS log churn) |

*Note: Counts reflect issues and PRs specifically called out in the digests, not total repository volumes.*

## 3. Shared Feature Directions

Several requirements appear across both communities, indicating cross-tool priorities:

- **Cost transparency and guardrails**  
  *Both tools*: Users are demanding real-time token/cost displays, explicit model-upgrade consent, and predictable budgeting. Claude Code #71481 (silent Opus upgrade) and Codex #28879 (10-20× cost jump) highlight identical friction.

- **Platform parity and stability**  
  *Both tools*: Windows regressions (sandbox dialogs, paste bugs, ARM64 failures) and macOS-specific issues (socket path limits, log bloat) persist. Claude Code #50674 (ARM64 Cowork), Codex #29200 (sandbox on every patch).

- **MCP/OAuth authentication lifecycle**  
  *Both tools*: MCP tool integration suffers from stale token handling, missing auto-refresh, and unclear recovery paths. Claude Code #70958 (sub-agent auth errors), Codex #17265 (OAuth tokens not refreshed).

- **Memory and performance leaks**  
  *Both tools*: Long-running sessions degrade. Claude Code #71493 (348 MB/hour leak), Codex #28224 (SQLite ~640 TB/year writes, partially fixed).

- **User agency over input**  
  *Both tools*: Ability to edit pasted text before submission (Claude Code #3412, Codex #2137 for Windows). Also interrupt hooks (Claude Code #9516) relate to controlling model flow.

- **Context and session management**  
  *Both tools*: Auto-compaction causing task forgetting (Codex #5957), conversation history loss in extensions (Claude Code #29017), silent session resumption (Claude Code #71478).

- **Log/diagnostic volume control**  
  *Primarily Codex* (#28224, #29532), but Claude Code’s memory leak suggests similar monitoring needs.

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|-----------|-------------|--------------|
| **Primary user pain** | Model quality regressions (Opus 4.7/4.8 reasoning degradation) | Rate-limit accounting and token cost spikes |
| **Security focus** | Auto-mode classifier (`classifyAllShell`), workspace trust, bypass permissions | No equivalent built-in; sandbox via Windows setup, MCP resource updates |
| **Extensibility model** | Cowork, sub-agents, user interrupt hooks | MCP Streamable HTTP, plugin service preview, virtual HTTP MCP servers (PR #30000) |
| **Cross-platform maturity** | Stronger Linux presence (seccomp, tmux), ARM64 Windows lagging | Better macOS/Linux alignment; Windows sandbox regressions prominent |
| **Community tone** | High emotional investment in model quality, vocal about deceptive practices | More measured, focused on cost/budget fairness and platform stability |
| **Release cadence** | Slower (one stable release in window, few PRs) | Rapid (stable + multiple alphas, 10 active PRs) |
| **Target developer** | Power users needing flexible model choices, complex agentic workflows | Enterprise/pro users needing predictable throughput and billing |

**Key takeaway**: Claude Code differentiates on model diversity and security governance; Codex differentiates on platform extensibility (MCP, plug-in service) and seems to be iterating faster on infrastructure. Cost governance is a shared weakness, but manifests differently—Claude Code via silent model upgrades, Codex via token accounting bugs.

## 5. Community Momentum & Maturity

- **Claude Code**: Community is highly engaged on long-standing issues (#3412 with 269 upvotes from July 2025) but showing signs of churn—the PR that increases stale/autoclose timeouts (PR #63686) indicates maintainers are overwhelmed by issue volume. Model quality complaints (#68780, #49747) are eroding trust. Momentum is strong in feature requests (multi-account, interrupt hooks) but execution appears slower.

- **OpenAI Codex**: Higher PR activity (10 in one day) suggests a more responsive engineering team. The community is larger numerically (e.g., #28224 has 385 upvotes) and more focused on operational issues (rate limits, log bloat) rather than model quality. However, the rapid alpha cadence (5 alphas in one day) may indicate instability. The rate-limit crisis (#28879, #30002) could become a breaking point if unaddressed.

- **Maturity indicators**: Both tools are past the “novelty” phase; users are treating them as production dependencies. The prevalence of cost, security, and reliability issues signals a shift from feature-driven to operations-driven feedback.

## 6. Trend Signals for Developers

1. **Cost governance is the new critical path** – Silent overruns and opaque billing are becoming dealbreakers. Developers should demand per-request cost previews, spending caps, and explicit upgrade consent before using any CLI in CI or long-running sessions.

2. **Security models are diverging** – Claude Code’s auto-mode classifier and workspace trust offer finer-grained control, while Codex leans on OS-level sandboxing and MCP token management. Evaluate which aligns with your compliance needs (e.g., air-gapped environments, SOC2).

3. **MCP is the de facto integration layer** – Both tools are investing in MCP, but OAuth lifecycle, token refresh, and tool discovery remain immature. Expect rapid iteration here; consider building MCP servers with defensive token handling.

4. **Cross-platform parity remains elusive** – Windows and ARM64 Linux users face recurring regressions. If your team is on these platforms, allocate extra buffer for debugging sandbox and input handling issues.

5. **Mental model for “context window” is still broken** – Auto-compaction, session resumption, and context loss are unsolved. For complex, multi-step tasks, treat both tools as having ephemeral memory unless you explicitly manage checkpoints.

6. **Community health matters for roadmap influence** – Claude Code’s slower PR throughput suggests community contributions may have less impact; Codex’s active PR pipeline invites more direct collaboration. If you plan to extend or customize, Codex’s ecosystem (MCP, plugin preview) currently offers more leverage.

7. **Performance monitoring is non-negotiable** – Memory leaks (Claude Code), log bloat (Codex), and token waste (background polling) can silently degrade developer machines. Integrate heap dumps, disk usage tracking, and cost alerts into your CI/CD or local development environment.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data snapshot: 2026-06-26 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

### 1. fix(skill-creator): run_eval.py always reports 0% recall — install the eval artifact as a real skill; fix Windows stream reading, trigger detection, and parallel workers
**PR #1298** | Author: MartinCajiao | Status: **Open**
**Functionality:** Comprehensive rework of the skill evaluation pipeline — installs the eval artifact as a real skill so Claude can actually invoke it, fixes Windows pipe handling, corrects trigger detection logic, and enables parallel evaluation workers.
**Discussion highlights:** This is the most-watched PR in the repo, addressing the critical `recall=0%` bug (Issue #556, 10+ independent reproductions). Community discussion has centered on root cause analysis — the eval system was testing against a non-functional artifact, making the optimization loop optimize against noise. The PR takes a ground-up approach rather than patching individual symptoms.
[View PR #1298](https://github.com/anthropics/skills/pull/1298)

### 2. Add document-typography skill
**PR #514** | Author: PGTBoos | Status: **Open**
**Functionality:** Typographic quality control for AI-generated documents — detects orphan word wrap, widow paragraphs, and numbering misalignment. Addresses visual issues that affect every document Claude generates.
**Discussion highlights:** Strong consensus that typographic polish is a universal pain point. Community debate around whether this should be a separate skill or folded into the existing PDF/DOCX skills. The PR demonstrates clear before/after examples.
[View PR #514](https://github.com/anthropics/skills/pull/514)

### 3. fix(pdf): correct case-sensitive file references in SKILL.md
**PR #538** | Author: Lubrsy706 | Status: **Open**
**Functionality:** Fixes 8 case-sensitivity mismatches in the PDF skill's SKILL.md where uppercase file references (`REFERENCE.md`, `FORMS.md`) did not match actual lowercase filenames (`reference.md`, `forms.md`). Breaks on case-sensitive filesystems (Linux/macOS).
**Discussion highlights:** Highlights a systemic issue in the repository — inconsistent file naming conventions across skills. Community noted this affects reproducibility and cross-platform reliability.
[View PR #538](https://github.com/anthropics/skills/pull/538)

### 4. Add ODT skill — OpenDocument text creation and template filling
**PR #486** | Author: GitHubNewbie0 | Status: **Open**
**Functionality:** Full support for OpenDocument Format (.odt, .ods) — creation, template filling, reading, and conversion to HTML. Supports LibreOffice and ISO-standard document workflows.
**Discussion highlights:** High demand from users in government and education sectors where ODF is mandatory. Discussion focused on the skill's scope — some felt it should be split into separate ODT and ODS skills. The author argued for a unified approach given shared parsing infrastructure.
[View PR #486](https://github.com/anthropics/skills/pull/486)

### 5. Improve frontend-design skill clarity and actionability
**PR #210** | Author: justinwetch | Status: **Open**
**Functionality:** Refactors the frontend-design skill to ensure every instruction is actionable within a single conversation, with specific guidance to steer Claude's behavior without being overly prescriptive.
**Discussion highlights:** Community debate on the balance between prescriptive and flexible skill design. Several reviewers praised the "conversation-scoped" principle — skills should not assume multi-session context. This PR has influenced the emerging best-practices for skill authoring.
[View PR #210](https://github.com/anthropics/skills/pull/210)

### 6. Add skill-quality-analyzer and skill-security-analyzer to marketplace
**PR #83** | Author: eovidiu | Status: **Open**
**Functionality:** Two meta-skills — one evaluates skill quality across five dimensions (structure, documentation, examples, resource files, field configuration), the other analyzes security risks in skill definitions.
**Discussion highlights:** Early, influential PR that generated discussion about meta-skills as a category. Community raised concerns about circular evaluation (who evaluates the evaluators?). The security analyzer gained particular attention after the namespace trust issue (#492) emerged.
[View PR #83](https://github.com/anthropics/skills/pull/83)

### 7. fix(docx): prevent tracked change w:id collision with existing bookmarks
**PR #541** | Author: Lubrsy706 | Status: **Open**
**Functionality:** Fixes document corruption when the DOCX skill adds tracked changes to documents that already contain bookmarks. Root cause: OOXML's shared `w:id` namespace across bookmarks, tracked changes, comments, and move ranges.
**Discussion highlights:** Revealed the complexity of OOXML skill maintenance. Community noted that this kind of subtle bug is a strong argument for better integration testing in the skill-creator pipeline.
[View PR #541](https://github.com/anthropics/skills/pull/541)

### 8. Add testing-patterns skill
**PR #723** | Author: 4444J99 | Status: **Open**
**Functionality:** Comprehensive testing guidance covering the full stack — Testing Trophy model, AAA pattern, React component testing with Testing Library, integration testing, E2E with Playwright, and accessibility testing.
**Discussion highlights:** Well-received as filling a major gap. Community discussion centered on whether the skill should prescribe specific tool choices (Jest vs Vitest, etc.) or remain tool-agnostic. The author opted for tool-agnostic principles with concrete examples.
[View PR #723](https://github.com/anthropics/skills/pull/723)

---

## 2. Community Demand Trends

From the most active Issues, four clear demand clusters emerge:

### Security & Trust Boundaries (Issue #492 — 19 comments)
The community's most urgent concern: community-submitted skills distributed under the `anthropic/` namespace create a trust boundary vulnerability. Users may grant elevated permissions to skills they mistakenly believe are official. Demand for namespace verification, code signing, or a curated/official distinction mechanism is the single loudest signal in the repo.

### Organizational Skill Sharing & Management (Issue #228 — 14 comments)
Teams need to share skills without manual file transfer (download .skill → Slack → Settings → upload). Demand for a shared skill library, direct sharing links, and org-level policy controls. This is a distribution infrastructure gap.

### Skill-Creation Toolchain Reliability (Issues #556, #1169, #1061 — 12+ comments collectively)
The `run_eval.py` / `run_loop.py` evaluation pipeline is fundamentally broken in multiple ways: 0% trigger rate on all queries, Windows compatibility failures (subprocess, encoding, pipe handling), and silent failures that cause the optimization loop to return null results. This blocks iterative skill development entirely for many users.

### Specialized Domain Skills
- **Agent Governance** (Issue #412): Safety patterns, policy enforcement, audit trails for AI agent systems — reflecting demand for production-grade agent orchestration.
- **Compact Memory / Symbolic Notation** (Issue #1329): Reducing context overhead for long-running agents through symbolic notation — a response to context window pressure.
- **SharePoint/Enterprise Integration** (Issue #1175): Concerns about security and context window size when handling enterprise document stores via skills.

---

## 3. High-Potential Pending Skills

These open PRs show active community engagement and are likely to land soon:

| PR | Skill | Why It May Land Soon |
|---|---|---|
| [#1298](https://github.com/anthropics/skills/pull/1298) | **skill-creator evaluation fix** | Most-watched PR; addresses the blocker preventing any skill from being properly evaluated |
| [#1323](https://github.com/anthropics/skills/pull/1323) | **skill-creator trigger detection fix** | Direct follow-up to #1298; fixes real skill name detection and non-Skill tool bailing |
| [#1099](https://github.com/anthropics/skills/pull/1099) | **Windows pipe/handle fix** | One of multiple Windows compatibility PRs; enables a large user segment |
| [#1050](https://github.com/anthropics/skills/pull/1050) | **Windows subprocess + encoding fix** | Complements #1099; two 1-line changes with high impact |
| [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | Strong initial reception; fills clear gap in the skills catalog |
| [#360](https://github.com/anthropics/skills/pull/360) | **AppDeploy deployment skill** | First-class deployment workflow from Claude; working integration with external service |
| [#147](https://github.com/anthropics/skills/pull/147) | **codebase-inventory-audit** | Comprehensive 10-step workflow; addresses orphaned code and documentation gaps |
| [#154](https://github.com/anthropics/skills/pull/154) | **shodh-memory** | Persistent context across conversations; novel approach to agent memory |

Collectively, these PRs indicate the community's focus is shifting from *creating skills* to *making the skill creation toolchain work reliably*, while simultaneously expanding into enterprise and testing domains.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable skill development toolchain (fixing the broken evaluation loop and Windows compatibility) and trust infrastructure (namespace security and organizational sharing), more than for any single functional skill category.**

---

# Claude Code Community Digest — 2026-06-26

## Today’s Highlights
Release **v2.1.193** introduces a new `autoMode.classifyAllShell` setting that routes all Bash/PowerShell commands through the auto-mode classifier, improving security consistency. The community is buzzing about two critical issues: a **silent default model upgrade to Opus 4.7** that caused $506 in unexpected charges (Issue #71481) and a **severe memory leak** with a growth rate of 348 MB/hour (Issue #71493). Multiple reports also surface Opus 4.8 reasoning degradation and tool-call malformation.

## Releases
**v2.1.193** was published in the last 24 hours. Key changes:
- Added `autoMode.classifyAllShell` setting to route all Bash/PowerShell commands through the auto-mode classifier (instead of only arbitrary-code-execution patterns).
- Added auto-mode denial reasons to the transcript, the denial toast, and the `/permissions` recent denials list.

*No other releases in the window.*

## Hot Issues (10 noteworthy)
1. **[#71481 – Silent default model upgrade to Opus 4.7 caused $506 in unexpected charges](https://github.com/anthropics/claude-code/issues/71481)** (🔥 2 comments, 0 👍)  
   A macOS user reports Claude Code silently switched from Sonnet 4-6 to Opus 4-7 without notification, triggering 15 automatic recharges. Community reaction is sharp; many expect explicit consent before cost-multiplying model changes.

2. **[#71493 – Extreme latency memory leak (348 MB/hour growth)](https://github.com/anthropics/claude-code/issues/71493)** (1 comment, 0 👍)  
   A `/heapdump` reveals a memory leak at 348 MB/hour. Critical for long-running sessions; suggests a deep runtime issue.

3. **[#68780 – Claude Opus 4.8 reasoning degradation](https://github.com/anthropics/claude-code/issues/68780)** (12 comments, 16 👍)  
   Users report severely degraded reasoning even on Max effort, with claims of deceptive business practices. High emotional investment; Anthropic may need to address model quality.

4. **[#49747 – Opus 4.7 mixes legacy XML tool-use format into JSON tool calls](https://github.com/anthropics/claude-code/issues/49747)** (30 comments, 32 👍)  
   A regression affecting long payloads — the model outputs XML in JSON tool call contexts, breaking tool execution. Tagged as `has repro`, making it a priority for the team.

5. **[#3412 – Allow viewing/editing pasted text blocks before submission](https://github.com/anthropics/claude-code/issues/3412)** (76 comments, 269 👍)  
   Long-standing enhancement request from July 2025. Dictation/writing assistants paste collapsed blocks that can’t be reviewed; users want inline editing before sending.

6. **[#61415 – Bypass Permissions mode can’t be enabled on macOS](https://github.com/anthropics/claude-code/issues/61415)** (63 comments, 24 👍)  
   On macOS 2.1.148, the Desktop “Bypass Permissions” toggle reverts immediately. Affects advanced users who need unrestricted tool access.

7. **[#63896 – Usage credits required for 1M context on Windows](https://github.com/anthropics/claude-code/issues/63896)** (41 comments, 25 👍)  
   Recurring friction: users on Opus 1M context hit an ambiguous API error and don’t know how to enable usage credits. Similar to #61869 (closed). Sign of poor UX around cost controls.

8. **[#29017 – Conversation history lost in VSCode extension](https://github.com/anthropics/claude-code/issues/29017)** (25 comments, 18 👍)  
   VSCode extension users lose entire session histories. Highly disruptive; no workaround provided.

9. **[#50674 – Cowork fails on ARM64 Windows (Snapdragon X)](https://github.com/anthropics/claude-code/issues/50674)** (28 comments, 0 👍)  
   Cowork feature passes readiness check but fails on Snapdragon X devices. Growing ARM64 Windows user base affected.

10. **[#9516 – User Interrupt Hook feature request](https://github.com/anthropics/claude-code/issues/9516)** (23 comments, 43 👍)  
    Developers want a hook that fires when they interrupt Claude Code mid-task, allowing them to inject context or cancel operations gracefully.

## Key PR Progress
Only one pull request was updated in the last 24 hours:
- **[PR #63686 – Bump stale and autoclose timeouts from 14 to 90 days](https://github.com/anthropics/claude-code/pull/63686)** (CLOSED)  
  A maintenance PR by @caseyWebb to reduce the churn of issue lifecycle actions. Increases stale/autoclose thresholds to 90 days, giving more time for resolution before auto-closing. Likely a response to the high volume of open issues.

*No other PR activity. The community would benefit from more active PRs; consider diving into the open bugs and submitting fixes.*

## Feature Request Trends
From the top-30 issues, the most requested feature directions include:

- **Multi-account / identity management** – #36151 (110 comments, 380 👍) asks for account switching in the mobile app, but similar pain points exist in Claude Code for team workflows.
- **Editable pasted text** – #3412 (76 comments, 269 👍) remains a top vote-getter for improving user control over inserted content.
- **Interrupt hooks** – #9516 (23 comments, 43 👍) – a programmatic way to react to user interruptions.
- **Sandbox configurability on Linux** – #44180 (5 comments, 12 👍) – add `allowUnixSockets` / `allowAllUnixSockets` equivalent for bwrap/seccomp.
- **Workspace trust improvements** – Implicit in #67319 and #70501 – users want consistent trust prompts in VSCode extension and persistent trust decisions.

Themes: **more user agency** (edit before send, interrupt hooks), **cross-platform parity** (Linux sandbox, Windows ARM64 support), and **cost transparency** (model upgrade notifications, usage credit onboarding).

## Developer Pain Points
Recurring frustrations from the issue tracker:

1. **Model quality regressions** – Multiple reports (#68780, #71446, #49747) that Opus 4.7/4.8 reasoning quality has dropped, mixed with tool-call formatting bugs. Erodes trust in the flagship model.
2. **Silent cost increases** – #71481 (model upgrade without warning) and #71478 (VS Code extension resumes huge sessions without token estimation) highlight insufficient cost guardrails.
3. **Authentication & permissions friction** – Workspace trust dialogs not showing in VSCode (#67319), OAuth scopes missing for design tools (#71490), sub-agent auth errors misreported (#70958).
4. **Cross-platform incompleteness** – Cowork fails on ARM64 Windows (#50674), Linux seccomp lacks Unix socket support (#44180), tmux auto-detection kills session persistence (#70219).
5. **Memory leaks and performance** – #71493 (348 MB/hour leak) and #71491 (scrollbar/copy-paste broken on SSH) degrade the daily experience.
6. **1M context usage credit confusion** – #61869, #63896 and related issues show users hit cryptic “Usage credits required” errors with no in-product guidance.

**Overall sentiment:** The community values Claude Code’s capability but is vocal about regressions in model quality, unexpected costs, and platform-specific rough edges. The new auto-mode classifier settings in v2.1.193 are a step toward better security governance, but many foundational bugs remain unresolved.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-26

## Today’s Highlights
A flurry of releases and PRs signal renewed focus on **MCP tool discovery** and **platform reliability**. The `rust-v0.142.2` release enables default tool search for MCP and adds system proxy support for macOS auth. Meanwhile, the community remains vocal about **rate-limit accounting** – Issue #28879 (152 comments, 303 👍) documents a 10–20× jump in per-token cost on GPT-5.5 since June 16, and Issue #30002 shows Pro accounts hitting the 5h limit in ~41 minutes. On the PR side, several patches aim to **stabilise MCP runtime management** and **reduce SQLite log churn**, though partial fixes leave room for more work.

## Releases
This week’s primary stable update is **rust-v0.142.2** ([GitHub](https://github.com/openai/codex/releases/tag/rust-v0.142.2)), which ships two notable changes:
- **MCP tools now use tool search by default** when supported, improving tool discovery while preserving compatibility with older models and providers. (#29486)
- **macOS authentication clients can honour system proxy, PAC, and WPAD settings** when `respect_system_proxy` is enabled. (#26709)

Additionally, several pre-release alphas were published today (`rust-v0.143.0-alpha.25`, `.22`, `.21`, `.16`) and a new **`codex-zsh-v0.1.0`** plugin. No detailed changelogs are available for the alphas; they likely contain in-progress features for the v0.143 stable branch.

## Hot Issues
*Picked from the top 30 issues by comment count, focusing on high community engagement and impact.*

1. **#28879 – Rate-limit cost per token jumped ~10–20x since June 16**  
   *152 comments, 303 👍* | [Link](https://github.com/openai/codex/issues/28879)  
   Users report Codex (GPT-5.5, Plus plan) draining a 5h budget in 2–3 prompts. Session logs show `limit-% consumed per token` surged drastically. Critical concern for budget-conscious developers.

2. **#28224 – SQLite feedback logs can write ~640 TB/year**  
   *86 comments, 385 👍* | [Link](https://github.com/openai/codex/issues/28224)  
   Original report of massive SSD wear from Codex logs. The author notes three merged PRs (in 0.142.0) reduced logs by ~85%, but the issue remains open for residual concerns.

3. **#25749 – Legacy phone number verification blocks access**  
   *64 comments, 38 👍* | [Link](https://github.com/openai/codex/issues/25749)  
   Users authenticated via Google OAuth cannot bypass an old phone MFA step. No recovery path exists – a significant auth UX flaw.

4. **#2137 – Pasting multi-line text in CIL keeps only first line on Windows**  
   *34 comments, 41 👍* | [Link](https://github.com/openai/codex/issues/2137)  
   A long-standing Windows bug (opened Aug 2025) that auto-submits on paste. Still unresolved, frustrating Windows users.

5. **#5957 – Auto compaction causes GPT-5-Codex to forget mid-task**  
   *31 comments, 9 👍* | [Link](https://github.com/openai/codex/issues/5957)  
   Compaction can cause the model to lose context of ongoing edits or tasks. Enterprise users affected.

6. **#13733 – Background process polling wastes tokens**  
   *30 comments, 23 👍* | [Link](https://github.com/openai/codex/issues/13733)  
   Each status poll during long builds triggers a full API round-trip with complete history, burning credits.

7. **#30002 – Server-side quota over-reports after 5h reset**  
   *24 comments, 4 👍* | [Link](https://github.com/openai/codex/issues/30002)  
   Pro 5h limit triggers in ~41 min / 1.35M tokens, while earlier the same day needed ~156M tokens. Accounting bug suspected.

8. **#17265 – MCP OAuth tokens not auto-refreshed**  
   *19 comments, 39 👍* | [Link](https://github.com/openai/codex/issues/17265)  
   Refresh tokens are stored but never used; MCP tools fail after access token expiry. High upvote count signals demand.

9. **#29200 – Windows sandbox setup dialog on every `apply_patch`**  
   *17 comments, 6 👍* | [Link](https://github.com/openai/codex/issues/29200)  
   Since update 26.616, each patch triggers `codex-windows-sandbox-setup.exe` error dialog. Windows regressions are a recurring theme.

10. **#29532 – Persistent SQLite TRACE churn after 0.142.0**  
    *16 comments, 7 👍* | [Link](https://github.com/openai/codex/issues/29532)  
    Even after partial fixes, `~/.codex/logs_2.sqlite` continues to write excessively on macOS.

## Key PR Progress
*Selected from the top 20 PRs by comment count, highlighting significant changes merged or under review.*

1. **#30144 – Fix terminal rollout durability**  
   [Open PR](https://github.com/openai/codex/pull/30144)  
   Prevents `TurnComplete`/`TurnAborted` events from being appended after an earlier rollout flush, which could leave items stuck in a queue.

2. **#30164 – Make new-thread model defaults scope-aware**  
   [Open PR](https://github.com/openai/codex/pull/30164)  
   Allows Codex to load distinct model defaults for different product scopes (e.g., Work vs. Coding) without reloading config.

3. **#30148 – Reuse MCP runtimes when selected availability changes nothing**  
   [Open PR](https://github.com/openai/codex/pull/30148)  
   Optimises MCP runtime reuse by not restarting when a new environment contributes no MCP servers/connectors.

4. **#30087 – Forward MCP resource updates via app-server**  
   [Closed PR](https://github.com/openai/codex/pull/30087)  
   Exposes `notifications/resources/updated` from MCP into the core event stream, enabling live resource updates.

5. **#30156 – Fall back when remote filesystem walk is unavailable**  
   [Closed PR](https://github.com/openai/codex/pull/30156)  
   Gracefully handles older exec-servers that don’t expose `fs/walk` RPC, avoiding crashes during skill discovery.

6. **#30000 – Prototype Codex Apps as virtual HTTP MCP servers**  
   [Open PR](https://github.com/openai/codex/pull/30000)  
   Snapshots shared Apps upstream and serves them as loopback Streamable HTTP MCP endpoints – a major architectural step.

7. **#28582 – Route preview traffic to plugin service**  
   [Open PR (code-reviewed)](https://github.com/openai/codex/pull/28582)  
   Adds controlled `features.plugin_service_preview` flag for employee-only testing of a new plugin service.

8. **#29516 – Persist Cloudflare affinity cookies for MCP HTTP**  
   [Open PR (code-reviewed)](https://github.com/openai/codex/pull/29516)  
   Ensures `__cflb` cookie is stored and sent with Streamable HTTP MCP requests to maintain load-balancer affinity.

9. **#30154 – Preserve status for evicted V2 agents**  
   [Open PR (code-reviewed)](https://github.com/openai/codex/pull/30154)  
   After LRU eviction, completed/errored agents were returning `NotFound`; now a bounded final status is kept in AgentMetadata.

10. **#29909 – Allow CCA image generation and web search extensions**  
    [Closed PR](https://github.com/openai/codex/pull/29909)  
    Enables actor-authorized image generation and web search for the CCA provider shape while preserving built-in paths for older models.

## Feature Request Trends
From the past 24 hours of issues and PRs, several clear directions emerge:

- **Rate-limit transparency and fairness** – Multiple reports (#28879, #30002, #30034) demand real-time cost-per-token displays, predictable budgeting, and server-side accounting fixes.
- **MCP OAuth token lifecycle automation** – Issues #17265 and #27165 ask for automatic refresh of access tokens before expiration, without manual intervention.
- **Windows platform stability** – Sandbox setup crashes (#29200, #30009), GPU-related unlaunchability (#27828), and memory pressure (#30050) indicate a need for dedicated Windows QA.
- **Log volume control** – Despite partial fixes, #28224 and #29532 show that SQLite log churn remains a pain point, especially for SSD endurance and disk space.
- **Context management improvements** – Requests to prevent auto-compaction from losing task state (#5957) and to reduce token waste from polling loops (#13733) point to smarter session handling.
- **Plugin/service extensibility** – PRs like #28582 and #30000 aim to make Codex a platform for third-party apps and plugins, mirrored in community requests for binary file support in PRs (#4867).

## Developer Pain Points
Recurring frustrations highlighted in today’s issues:

- **Unexpected token consumption** – Users are burning through budgets with normal usage, feeling penalised without clear reasons (#28879, #30002, #30034).
- **Windows sandbox regressions** – After updates, `apply_patch` triggers error dialogs or COM+ errors, blocking workflows (#29200, #29782, #30009).
- **MCP authentication friction** – Stale tokens causing silent failures, no auto-refresh, and no clear recovery path (#17265, #27165).
- **SQLite bloat and disk wear** – Even after optimisations, logs still grow rapidly on some platforms (#28224, #29532).
- **Session context loss** – Auto-compaction and resume logic cause the model to forget ongoing tasks or file edits (#5957, #29773).
- **Blocking on slow MCP `tools/list`** – Initial model requests are delayed until all MCP servers respond, hurting startup time (#28640).
- **macOS socket path limits** – Deep `CODEX_HOME` directories break Unix domain sockets (`SUN_LEN`), preventing daemon commands (#27765).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*