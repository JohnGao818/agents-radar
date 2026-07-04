# AI CLI Tools Community Digest 2026-07-04

> Generated: 2026-07-04 02:32 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date: 2026-07-04**

---

## 1. Ecosystem Overview

The AI CLI tools landscape shows two major platforms—Claude Code and OpenAI Codex—both at different stages of maturity but converging on similar pain points around security, session reliability, and model behavior consistency. Claude Code is shipping frequent patch releases (two in 24 hours) with community feedback dominating the roadmap, while Codex is pushing substantial security infrastructure via Git sandboxing PRs alongside a Rust-based CLI alpha. Both communities are experiencing friction from recent behavioral changes—Claude Code's AskUserQuestion timeout redesign and Codex's GPT-5.5 perceived regression—indicating that user trust in model reliability remains fragile. The broader trend points toward growing demand for multi-account support, configurable autonomy levels, and hardening against session/cache leakage as these tools become embedded in production workflows.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Hot Issues (noteworthy)** | 10 | 10 |
| **PRs in digest period** | 7 (5 unique + 2 closed duplicates) | 10 |
| **Release status (24h)** | 2 patch releases (v2.1.200, v2.1.201) | 1 alpha release (rust-v0.143.0-alpha.35) |
| **Top issue engagement** | #73125: 111 comments, 354 👍 | #30224: 68 comments, 22 👍 |
| **Highest community demand** | #65697 (Linux Desktop, closed): 495 👍 | #30364 (GPT-5.5 regression): 53 👍 |
| **Security-related PRs** | 1 (#74021: schema fix) | 6 (Git sandboxing PRs #30848–#31072) |

Both tools show roughly equivalent issue volume, but Claude Code generates significantly higher community engagement per issue (111 vs 68 max comments) and stronger upvote signals (495 vs 53 max 👍). Codex has more active PRs, particularly from first-party engineers focusing on security hardening.

---

## 3. Shared Feature Directions

Several requirements span both tool communities:

- **Multi-account / workspace isolation**: Both Claude Code (#36151, 415 👍) and Codex (#26338, +8 👍) see demand for switching between accounts or repositories without credential conflicts or session cross-contamination. Claude Code reports actual session leakage (#74066); Codex has related workspace separation asks.

- **Configurable timeouts and autonomy**: Claude Code's new AskUserQuestion idle timeout (#73105, 27 👍) and Codex's approval prompt fatigue (#30898) both reflect user desire for granular control over when the tool waits vs. proceeds. The community pushback against enforced timeouts is consistent across both ecosystems.

- **Git integration flexibility**: Claude Code requests diff comparison against arbitrary branches (#23626, 78 👍). Codex requests multi-repository workspace support (#26338). Both indicate that single-branch, single-repo assumptions limit real-world use.

- **Security and secret handling**: Claude Code's repeated requests for automatic `.env`/`.ssh` redaction and Codex's extensive Git sandboxing PR series both prioritize preventing the tool from exposing sensitive data in untrusted repositories.

- **Linux / cross-platform support**: Claude Code's closed-but-highly-upvoted Linux desktop request (#65697, 495 👍) and Codex's Windows sandbox failures (#30009) show that platform-specific gaps still limit adoption in heterogeneous environments.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Release cadence** | Frequent patch releases (2–3x/week), targeting UX regressions | Slower alpha cycle, bulk security PRs from first-party engineers |
| **Primary user pain** | Session reliability and behavioral regressions (AskUserQuestion, hallucinated turns, resume failures) | Model degradation (GPT-5.5) and sandbox instability (Windows) |
| **Community role** | Strong feature demand signals (upvote-heavy, active commentary on UX design) | More passive; issues track bugs, but PRs are primarily internal |
| **Security posture** | Reactive: responding to leakage reports, schema edge cases | Proactive: systematic Git transport/filter hardening (6 PRs) |
| **Target user** | Individual developers and small teams; Linux CLI heavy | Enterprise and Pro users; Windows/macOS App users |
| **Technical focus** | Conversation flow control, permission modes, session management | Git sandboxing, authentication routing, rate-limit infrastructure |

Claude Code is more developer-ergonomics-focused, iterating rapidly on user workflow feedback. Codex is investing heavily in infrastructure security and reliability, suggesting an enterprise-first deployment strategy.

---

## 5. Community Momentum & Maturity

**Claude Code** has the more active and vocal community. Its open issues generate 2–5× more upvotes and 2× more comments than comparable Codex issues. The 495 👍 on the closed Linux request demonstrates sustained demand despite the tool's existing CLI support. However, the volume of session/cache leakage reports (#74066, #72274, #73675) suggests maturity gaps in state management that could undermine trust if not addressed.

**OpenAI Codex** appears more internally-driven, with many PRs from OpenAI engineers rather than community contributions. The alpha release (rust-v0.143.0-alpha.35) indicates ongoing architectural work, but the lack of changelog details and slow resolution of long-standing issues (#7291, 9 months open) may frustrate users. The GPT-5.5 regression reports (#30364, #30137) are a significant concern given the tool's core value proposition.

Both tools are iterating rapidly but in different dimensions: Claude Code on UX surface area, Codex on backend security. Neither appears fully mature for mission-critical production use, given the open issues around session reliability, model consistency, and platform support.

---

## 6. Trend Signals

Several industry-relevant patterns emerge from today's digests:

- **Security hardening is becoming table stakes**: Codex's six Git sandboxing PRs and Claude Code's cross-workspace leakage reports indicate that AI CLI tools must defend against repository-injected attacks. Developers evaluating these tools should assess whether sandboxing of Git hooks, filters, and configuration extends to their workflows.

- **Model behavior regressions erode trust quickly**: Both communities show immediate backlash when model quality changes unexpectedly (Claude Code's hallucinated turns, Codex's GPT-5.5 clustering). Tool maintainers must prioritize deterministic behavior and transparent model versioning.

- **User autonomy vs. AI autonomy is unresolved**: Claude Code's reversal on AskUserQuestion auto-continue and Codex's approval prompt fatigue show that the industry has not settled on the right default balance. Expect this to remain a hot topic as tools gain more file-system and network access.

- **Session and cache isolation is underbuilt**: With multiple reports of cross-account contamination (Claude Code) and context compaction losing state (Codex), state management is a weak point. Tools that solve session isolation cleanly will have a competitive advantage for enterprise adoption.

- **Cross-platform parity is still aspirational**: Linux demand for Claude Code and Windows sandbox failures for Codex suggest that developers in heterogeneous environments should test tools on their primary platform before committing to a workflow.

**Bottom line for technical decision-makers**: Claude Code offers a more responsive, community-shaped experience with faster UX iteration but carries session reliability risk. Codex offers stronger infrastructure security but slower issue resolution and ongoing model quality concerns. Both tools should be evaluated under realistic multi-session, multi-repository workflows before production adoption.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data snapshot: 2026-07-04 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

*Note: All PRs display `Comments: undefined` in the source data, so ranking is based on cross-referenced issue activity and discussion depth inferred from PR descriptions and linked issues.*

**#1 — `skill-creator` fix suite (multiple PRs)**
- **PRs:** #1298, #1323, #1099, #1050, #362, #361, #539  
- **Functionality:** The `skill-creator` meta-skill (used to author and optimize other skills) has a critical bug: `run_eval.py` always reports 0% recall, making the description-optimization loop optimize against noise. Multiple contributors (MartinCajiao, Polluelo978, joshuawowk, gstreet-ops, Mr-Neutr0n, Lubrsy706) have submitted fixes addressing: trigger detection logic, Windows subprocess/encoding crashes, YAML parsing failures, and Unicode byte-length panics.
- **Discussion highlights:** The root cause (#556) has 12 comments and 7 👍 from affected users. Issue #1169 confirms the bug is reproducible on literal slash-command queries. The community is actively debugging across Windows and macOS, with multiple partial fixes in flight.
- **Status:** All open. #1298 (by MartinCajiao) is the most comprehensive fix, also addressing parallel workers and Windows stream reading.

**#2 — `document-typography` (#514)**
- **Author:** PGTBoos  
- **Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents — common typographic issues affecting every document Claude generates.
- **Discussion highlights:** Addresses a universal pain point users rarely articulate. The skill is self-contained and targets a clear, measurable quality improvement.
- **Status:** Open since 2026-03-04.

**#3 — `skill-quality-analyzer` + `skill-security-analyzer` (#83)**
- **Author:** eovidiu  
- **Functionality:** Meta-skills that evaluate other skills across five dimensions (Structure & Documentation, Trigger Precision, etc.) and scan for security vulnerabilities. Proposes a standardized quality scoring system.
- **Discussion highlights:** Represents an early attempt at skill governance — predating the broader security/trust conversation that later emerged in Issue #492.
- **Status:** Open since 2025-11-06.

**#4 — `ODT` skill (#486)**
- **Author:** GitHubNewbie0  
- **Functionality:** Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Triggers on mentions of ODT, ODS, LibreOffice, or requests for open-source document formats.
- **Discussion highlights:** Addresses a clear gap — LibreOffice/ODF support is absent from the official document-skills collection. The community has interest in cross-format interoperability.
- **Status:** Open since 2026-03-01.

**#5 — `testing-patterns` (#723)**
- **Author:** 4444J99  
- **Functionality:** Comprehensive testing skill covering the Testing Trophy model, unit testing (AAA pattern), React component testing (Testing Library), E2E testing (Playwright), and testing anti-patterns.
- **Discussion highlights:** Broader than typical skills — essentially a testing methodology guide embedded as a skill. High potential for developer workflow impact.
- **Status:** Open since 2026-03-22.

**#6 — `self-audit` / output verification (#1367)**
- **Author:** YuhaoLin2005  
- **Functionality:** Two-stage audit: mechanical file verification (all claimed outputs exist) followed by four-dimension reasoning quality audit (correctness, completeness, consistency, clarity) in damage-severity priority order. Universal across projects and tech stacks.
- **Discussion highlights:** Most recent major skill submission (2026-06-28). Addresses a fundamental trust gap in AI-generated outputs.
- **Status:** Open, very recently updated (2026-07-02).

**#7 — `color-expert` (#1302)**
- **Author:** meodai  
- **Functionality:** Self-contained color expertise covering naming systems (ISCC-NBS, Munsell, XKCD, RAL, Ridgway, CSS), color spaces with "what to use when" guidance, and accessibility.
- **Discussion highlights:** Narrow but deep domain expertise. Leverages the author's existing color knowledge library.
- **Status:** Open since 2026-06-10.

---

## 2. Community Demand Trends

From the most-active Issues, the community's highest-priority demands cluster into four themes:

**🔒 Security & Trust Boundary (Issue #492 — 34 comments, 2 👍)**
The top-voted issue. Community skills distributed under `anthropic/` namespace create impersonation risk. Users may grant elevated permissions to unverified community skills. This is the most urgent governance conversation — demand for: official verification badges, namespace separation, permission-scope manifests, and a trust model for skill distribution.

**🏢 Organization-Wide Collaboration (Issue #228 — 14 comments, 7 👍)**
Skills cannot be shared organizationally within Claude.ai. Users must manually download `.skill` files and distribute via Slack/Teams. Demand for: shared skill libraries, direct sharing links, team-level management, and enterprise deployment workflows.

**🔧 Skill-Creator Reliability (Issue #556 — 12 comments, 7 👍; Issue #1169 — 3 comments)**
The `skill-creator` meta-skill is fundamentally broken — `run_eval.py` reports 0% recall on all queries, making the optimization loop worthless. This blocks anyone from authoring or improving skills effectively. Highest operational priority for the skill ecosystem.

**📋 Skill Discovery & Deduplication (Issue #189 — 6 comments, 9 👍)**
`document-skills` and `example-skills` plugins install identical content, causing duplicates. Demand for: clear separation of plugin scopes, deduplication logic, and proper skill categorization.

**Emerging demand signals:**
- **Agent governance patterns** (Issue #412 — 6 comments): Policy enforcement, threat detection, trust scoring for AI agent systems — no existing skill covers this.
- **Compact agent memory** (Issue #1329 — 8 comments): Symbolic notation for compact agent state representation, avoiding context bloat from prose-style memory.
- **MCP/skill interop** (Issue #16): Expose skills as MCP tools for standardized API signaling.
- **SharePoint/enterprise security** (Issue #1175): Access control patterns for skills operating on enterprise document systems.

---

## 3. High-Potential Pending Skills

These open PRs have active community engagement and are likely to land soon:

| Skill | PR | Author | Why It May Land Soon |
|-------|-----|--------|---------------------|
| **skill-creator fix (comprehensive)** | [#1298](https://github.com/anthropics/skills/pull/1298) | MartinCajiao | Fixes the blocker bug (#556) with thorough analysis; multiple community confirmations |
| **self-audit (v1.3.0)** | [#1367](https://github.com/anthropics/skills/pull/1367) | YuhaoLin2005 | Recently updated (Jul 2); fills a clear trust gap; well-structured proposal |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | 4444J99 | Broad developer appeal; no competing skill exists |
| **sensory (macOS automation)** | [#806](https://github.com/anthropics/skills/pull/806) | AdelElo13 | Novel approach (AppleScript instead of screenshot-based CU); addresses macOS-native demand |
| **ODT skill** | [#486](https://github.com/anthropics/skills/pull/486) | GitHubNewbie0 | Fills a clear gap in document format support; no equivalent in official collection |
| **DOCX tracked-change fix** | [#541](https://github.com/anthropics/skills/pull/541) | Lubrsy706 | Fixes document corruption; small, well-scoped change with clear reproduction |

**Critical path blockers:**
The `skill-creator` fix PRs (#1298, #1323, #1099) are blocking all other skill development — without a working evaluation loop, no one can optimize skill descriptions. The community may coalesce around a single fix, likely #1298 as the most comprehensive.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for tooling reliability and trust governance — a stable, trustworthy, and collaborative skill authoring and distribution infrastructure — even more than for individual domain-specific skills.**

The data reveals a layered priority:
1. **Foundation broken:** `skill-creator` is non-functional (0% recall bug), blocking all skill optimization.
2. **Trust unaddressed:** No namespace verification, permission model, or security review process for community skills.
3. **Collaboration absent:** No org-wide sharing, no discovery mechanism, no deduplication.
4. **Then, domain skills:** Only once the above are resolved does the community fully benefit from skills like testing-patterns, ODT, color-expert, or self-audit.

The most impactful contribution to the ecosystem right now is not a new skill — it's a working `skill-creator` and a trust/verification framework for skill distribution.

---

# Claude Code Community Digest — 2026-07-04

## Today’s Highlights
Two patch releases shipped in the last 24 hours: **v2.1.201** (Sonnet 5 harness reminder change) and **v2.1.200** (AskUserQuestion no longer auto-continues by default, permission mode defaults to Manual). The community is reacting strongly to the new AskUserQuestion idle timeout – 111 comments on a single bug report – and several session‑leakage reports are raising security eyebrows. The long‑running request for a native Linux desktop build (495 👍) was closed, but the underlying demand remains.

## Releases
**v2.1.201** – Claude Sonnet 5 sessions no longer use the mid‑conversation system role for harness reminders.

**v2.1.200** – Two behavioral changes:
- `AskUserQuestion` dialogs no longer auto‑continue by default; users must opt into an idle timeout via `/config`.
- The “default” permission mode has been changed to **Manual** across the CLI, `--help`, VS Code, and JetBrains. `--permission-mode manual` and `"defaultMode": "manual"` are now accepted.

## Hot Issues (10 noteworthy)
1. **[#36151 – Multi‑account switching in Claude Mobile](https://github.com/anthropics/claude-code/issues/36151)**  
   *Comments: 116 | 👍: 415* – A long‑standing feature request for account switching without shared email. High community demand; still open.

2. **[#73125 – AskUserQuestion: “No response after 60s” bug](https://github.com/anthropics/claude-code/issues/73125)**  
   *Comments: 111 | 👍: 354* – After the v2.1.200 change, users report that the 60‑second timeout fires even when they intend to respond, causing unintended progress. Labelled `bug` and already the top‑voted open issue.

3. **[#19673 – False “You’ve hit your limit” at 84% usage](https://github.com/anthropics/claude-code/issues/19673)**  
   *Comments: 101 | 👍: 75* – Persistent rate‑limiting false positive affecting users in Asia. Still open after six months.

4. **[#65697 – [CLOSED] Official Claude Desktop for Linux](https://github.com/anthropics/claude-code/issues/65697)**  
   *Comments: 51 | 👍: 495* – Closed as “invalid” (moved to another tracker?), but 495 upvotes show huge demand for native Linux support.

5. **[#23626 – Diff comparison against branches other than main](https://github.com/anthropics/claude-code/issues/23626)**  
   *Comments: 24 | 👍: 78* – Users want to compare diffs against arbitrary branches, not just `main`. Still open.

6. **[#70315 – Hallucinated turns with stop_reason=null (re‑report)](https://github.com/anthropics/claude-code/issues/70315)**  
   *Comments: 12 | 👍: 0* – A recurring bug where the model invents fake user/system turns. User reports it’s still present in v2.1.186 despite being auto‑closed as duplicate.

7. **[#74060 – Cloud web session hangs indefinitely after init](https://github.com/anthropics/claude-code/issues/74060)**  
   *Comments: 3 – New today.* – Sessions on claude.ai/code spin forever after initialization. No response to any message.

8. **[#74023 – Settings resolution broken in subdirectory launches](https://github.com/anthropics/claude-code/issues/74023)**  
   *Comments: 3* – `.claude/settings.json` resolves against literal `cwd`, not git root, silently dropping project settings when launched from a subdirectory.

9. **[#73105 – Make AskUserQuestion timeout configurable](https://github.com/anthropics/claude-code/issues/73105)**  
   *Comments: 6 | 👍: 27* – Following the v2.1.200 change, users request a configurable timeout or restore indefinite wait.

10. **[#74066 – Potential session/cache leakage between workspaces](https://github.com/anthropics/claude-code/issues/74066)**  
    *Comments: 1 – New today.* – User reports session cross‑contamination: a Claude session on an enterprise workspace suddenly started building a Minecraft temple as if from another account.

## Key PR Progress (7 total, all covered)
1. **[#74021 – fix(security‑guidance): allow null findings in StructuredOutput schema](https://github.com/anthropics/claude-code/pull/74021)** – Prevents schema rejection when the model finds no vulnerabilities and returns `null` instead of `[]`. Observed in 31 review sessions across 7 repos.

2. **[#74010 – enhance(feature‑dev): add system design patterns, edge cases, and operational context](https://github.com/anthropics/claude-code/pull/74010)** – New `code‑architect` steps for system design pattern analysis and operational context, improving architectural guidance.

3. **[#74009 – fix(plugin‑dev): use “asks to” in skill descriptions](https://github.com/anthropics/claude-code/pull/74009)** – Completes a consistency fix across plugin‑dev skills; two remaining files now match the standard phrasing.

4. **[#74007 – [CLOSED] enhance(feature‑dev): … (duplicate of #74010)](https://github.com/anthropics/claude-code/pull/74007)** – Identical to #74010; closed in favour of the newer PR.

5. **[#73999 – [CLOSED] fix(plugin‑dev): use “asks to” … (duplicate of #74009)](https://github.com/anthropics/claude-code/pull/73999)** – Identical to #74009; closed.

6. **[#42701 – fix init‑firewall.sh crash from ipset repeated IPs](https://github.com/anthropics/claude-code/pull/42701)** – Prevents devcontainer launch failure when a domain resolves to duplicate IPs by adding the `-exist` switch to `ipset`.

7. **[#66854 – [OPEN] “toekn”](https://github.com/anthropics/claude-code/pull/66854)** – Title appears to be a typo; no summary provided. Likely a draft or test PR.

## Feature Request Trends
- **Account & authentication** – Multi‑account switching (#36151, 415 👍) and cross‑workspace session isolation remain top wants.
- **Linux support** – Native desktop build (#65697) was closed but received 495 👍, indicating strong community demand.
- **Git integration** – Ability to diff against any branch (#23626) and more flexible branch comparison.
- **Configurable timeouts** – The new AskUserQuestion timeout (#73105) has sparked requests for adjustable idle behaviour.
- **Secret redaction** – Automatic redaction of likely‑secret files (e.g. `.env`, `.ssh`) continues to be raised, with contributions offered (#65122, #59296).

## Developer Pain Points
- **AskUserQuestion regressions** – The v2.1.200 change that stops auto‑continue has caused widespread confusion and workflow breaks (#73125, #73105). Many want the old indefinite‑wait behaviour restored or made configurable.
- **Session & credential leakage** – Multiple reports this week of cross‑session data contamination (#74066, #72274) and persistent ghost sessions (#73675). Security concerns are growing.
- **Hallucinated turns** – The bug where Claude invents fake user/system turns persists across versions (#70315), forcing users to fall back to Opus 4.8.
- **Settings resolution** – Launching Claude Code from a subdirectory silently ignores project settings (#74023), a subtle but painful misconfiguration.
- **Resume failures** – Session resume breaks with “undefined is not an object” (#74059) and stale session indexes (#74043) hinder productivity.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-04

## Today’s Highlights
A new Rust-based CLI alpha (0.143.0-alpha.35) shipped with no visible feature changes. The community remains vocal about model-behavior regressions, especially GPT-5.5 token clustering and perceived intelligence drops. Several security-focused pull requests from OpenAI engineers (bookholt-oai) target Git sandboxing to prevent repository-controlled filters and transports from executing during patch operations — a substantial hardening effort.

## Releases
- **rust-v0.143.0-alpha.35** — [Release](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.35). No changelog details provided beyond the version bump.

## Hot Issues (10)
1. **[#30224](https://github.com/openai/codex/issues/30224)** — “This model is not supported when using X-OpenAI-Internal-Codex-Responses-Lite.”  
   *68 comments, 22 👍* — A persistent error affecting multiple users, especially on Windows and with GPT-5.5. The community suspects a backend routing mismatch.

2. **[#7291](https://github.com/openai/codex/issues/7291)** — VS Code extension fails to revert changes.  
   *47 comments, 16 👍* — Long-standing (since Nov 2025) but still open. Users report that undo operations simply do not work in the extension.

3. **[#30364](https://github.com/openai/codex/issues/30364)** — GPT-5.5 reasoning-token clustering at 516/1034/1552 – degraded performance on complex tasks.  
   *37 comments, 53 👍* — Highly upvoted. The anomaly suggests the model is hitting artificial boundaries, reducing reasoning depth. Many users echo the observation.

4. **[#20214](https://github.com/openai/codex/issues/20214)** — Codex App freezes/stutters on Windows 11 Pro despite sufficient resources.  
   *27 comments, 40 👍* — Affecting Plus users with high-end hardware. No fix yet; community suspects rendering or IPC bottlenecks.

5. **[#30009](https://github.com/openai/codex/issues/30009)** — `apply_patch` fails with Windows sandbox error.  
   *20 comments, 4 👍* — File edits via tool calls crash on Windows when sandbox is active. Blocks critical workflow for Pro users.

6. **[#25792](https://github.com/openai/codex/issues/25792)** — Context compaction forgets AGENTS rules; progress jumps from 97% back to 42%.  
   *12 comments* — Long-running task reliability issue. The automatic compaction discards agent instructions.

7. **[#30595](https://github.com/openai/codex/issues/30595)** — macOS CLI incorrectly routes ChatGPT-authenticated requests to Responses-Lite.  
   *11 comments* — Auth routing bug: same account works on Windows but fails on macOS CLI.

8. **[#30406](https://github.com/openai/codex/issues/30406)** — GPT-5.5 fails with Responses-Lite error while GPT-5.4 works in the same app.  
   *10 comments, 2 👍* — Model-specific regression after a recent app update.

9. **[#26429](https://github.com/openai/codex/issues/26429)** — Computer Use plugin disappears after Codex Desktop restart.  
   *9 comments, 3 👍* — Plugin becomes unavailable until manual re-enable.

10. **[#30137](https://github.com/openai/codex/issues/30137)** — “significant reduction in intelligence. feels like gpt 5.5 got downgraded to 5.3.”  
    *6 comments, 2 👍* — Anecdotal but echoed in other threads; the community suspects a recent model update or configuration change.

## Key PR Progress (10)
1. **[#30848](https://github.com/openai/codex/pull/30848)** — Block selected executable Git filters before patch application.  
   *Security: prevents repository-controlled clean/smudge filters from running during patching.*

2. **[#31072](https://github.com/openai/codex/pull/31072)** — Bind patch application to guarded Git configuration.  
   *Ensures validated config is reused across child processes, preventing re-execution with untrusted settings.*

3. **[#31071](https://github.com/openai/codex/pull/31071)** — Authorize included Git configuration sources before patch operations.  
   *Handles `include.path` and `includeIf` recursion.*

4. **[#31070](https://github.com/openai/codex/pull/31070)** — Authorize primary Git configuration sources before patch operations.  
   *Validates environment-driven config files (HOME, XDG, Windows profile) before patching.*

5. **[#31069](https://github.com/openai/codex/pull/31069)** — Bind Git configuration environment for patch operations.  
   *Prevents reading different `GIT_CONFIG_*` env vars per child process.*

6. **[#30395](https://github.com/openai/codex/pull/30395)** — Expose rate-limit reset credit details (`app-server`).  
   *New v2 endpoint returns available credits, expiry times, and consumption support.*

7. **[#30488](https://github.com/openai/codex/pull/30488)** — Show reset details in redemption picker (CLI).  
   *UI enhancement: users can now see credit expiry and select which credit to redeem.*

8. **[#30850](https://github.com/openai/codex/pull/30850)** — Block selected Git filters before staging patch paths.  
   *Prevents Git from recursing into unvalidated directories during `git add`.*

9. **[#31058](https://github.com/openai/codex/pull/31058)** — Retry model capacity errors with jittered backoff.  
   *`[code finalized]` – Retries HTTP 503 (capacity) up to 3 times (30s, 2m, 5m) to reduce user-facing failures.*

10. **[#30982](https://github.com/openai/codex/pull/30982)** — Allow extension-managed Apps authentication.  
    *Enables third-party extensions to authenticate with the Codex app, opening the door for richer plugin integration.*

## Feature Request Trends
- **Multi-repository workspaces** — [#26338](https://github.com/openai/codex/issues/26338) (+8 👍) requests support for parent folders containing multiple Git repos.  
- **Per-subagent model selection** — [#14039](https://github.com/openai/codex/issues/14039) (+12 👍) asks for the ability to assign different models/providers/profiles to spawned subagents.  
- **File viewer UX improvements** — [#22095](https://github.com/openai/codex/issues/22095) (+2 👍) wants scroll preservation and Page Up/Down support in the app’s file viewer.  
- **Real-time sync between App and Client** — [#31062](https://github.com/openai/codex/issues/31062) (+0 👍 but recent) requests bidirectional live state sync.

## Developer Pain Points
- **Windows sandbox instability** — Issues like [#30009](https://github.com/openai/codex/issues/30009), [#29413](https://github.com/openai/codex/issues/29413), and [#30435](https://github.com/openai/codex/issues/30435) highlight broken patch application, WSL+CWD failures, and Computer Use unavailability on Windows.  
- **GPT-5.5 regression** — Multiple reports ([#30364](https://github.com/openai/codex/issues/30364), [#30137](https://github.com/openai/codex/issues/30137)) suggest the model has degraded in reasoning quality, with token boundary artifacts and a “downgraded” feel.  
- **Context compaction losing progress** — [#25792](https://github.com/openai/codex/issues/25792) and [#31033](https://github.com/openai/codex/issues/31033) show that automatic context compaction can roll back task state, frustrating long sessions.  
- **Approval prompt fatigue** — [#30898](https://github.com/openai/codex/issues/30898) and [#30821](https://github.com/openai/codex/issues/30821) note that full-access mode and approved command prefixes still trigger approval dialogs, breaking unattended workflows.  
- **Authentication/routing confusion** — The “X-OpenAI-Internal-Codex-Responses-Lite” error ([#30224](https://github.com/openai/codex/issues/30224), [#30406](https://github.com/openai/codex/issues/30406), [#30595](https://github.com/openai/codex/issues/30595)) is affecting multiple platforms and models, likely a backend gateway misconfiguration.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*