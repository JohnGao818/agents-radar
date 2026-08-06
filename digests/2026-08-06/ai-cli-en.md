# AI CLI Tools Community Digest 2026-08-06

> Generated: 2026-08-06 02:09 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: Claude Code vs. OpenAI Codex
**Coverage date: 2026-08-06**

## 1. Ecosystem Overview

Both major AI CLI tools shipped stable updates on the same day — Claude Code v2.1.223 and OpenAI Codex rust-v0.146.1 — while the industry converges on a shared set of integration challenges: MCP lifecycle reliability, session/history portability, and Windows desktop stability. Issue-tracker sentiment shows the bar has shifted from "can the model write code" to "can the tooling be trusted at scale," with silent data loss, permission fatigue, and state corruption dominating complaints in both communities. The two projects are also differentiating sharply in architecture: Claude Code leans into policy-controlled agent workflows (plugins, hooks, marketplaces) while Codex invests in a cross-platform desktop/TUI runtime with thread-rollout persistence and multi-agent orchestration.

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| Latest stable release | v2.1.223 (today) | rust-v0.146.1 (today) |
| Pre-release channel | None reported today | rust-v0.147.0-alpha.6.5 / .10 / .11 / .12 / .13 |
| Hot issues featured | 10 | 10 (1 closed) |
| PRs active/merged (24h) | 5 active, 0 merged | ~19 merged |
| Top issue engagement | 46 👍 — session URLs in commits should be opt-in (#66504) | 373 👍 — restore `/undo` (#9203) |
| Dominant issue theme | Silent MCP parameter loss; desktop crashes | Windows desktop instability; missing `/undo` |

## 3. Shared Feature Directions

- **MCP reliability & lifecycle** — both. Claude: parameters silently dropped after long values (#72228) and absorbed by tag-grammar parser (#84362). Codex: zombie MCP child processes / 37 GB leak (#12491), tools discovered but not exposed to Desktop threads (#19425), handshake deadlock fixed in #37168.
- **Session & history continuity** — both. Claude: `--continue` cannot find `-p` sessions (#82536); session-URL injection into git metadata should be opt-in (#66504). Codex: conversation history vanishes after updates despite data in `state_5.sqlite` (#23979); legacy rollout migration to paginated history (#37175, #37157).
- **Permission & safety controls** — both. Claude: browser "Always allow" persists as `duration:"once"` (#74715); `pretooluse` hook now fails closed on exceptions (#84364). Codex: approval mode silently reverts to `on-request` (#32862); Guardian circuit-breaker for cyber-capable models (#37190); `/undo` demand (#9203).
- **Windows desktop stability** — both. Claude: GPU-process crash kills the app (#83744), 5-hour usage-limit crash requires reinstall (#83403). Codex: `taskkill.exe`/WMI storms with 40–50% idle CPU (#33776), Sysmon reinstallation and BSODs (#31035).
- **Context & model-behavior transparency** — both. Claude: Opus 4.8 tone and 5.0 coherence complaints (#77136). Codex: text-log attachment triggers persistent "Request blocked" state (#32177).

## 4. Differentiation Analysis

- **Focus**: Claude Code optimizes for terminal-native, Git-centric agent workflows — hooks, slash commands, marketplace governance (now with `owner/*` wildcards). Codex targets a broader desktop-first surface: GUI app, TUI, threads, rollouts, and world-state orchestration for multi-agent sessions.
- **Target users**: Claude's community skews toward CLI/CI power users and plugin consumers; Codex's skews toward desktop app users, with Windows-specific complaints dominating its tracker.
- **Technical approach**: Claude runs on Bun, ships thin releases, and grows capability through a marketplace/plugin model (marketplace expanding 14→27 plugins in PR #41661). Codex is Rust-based, merges large architectural PRs in daily batches (rollout migration, tool-namespace reservation, session-source propagation), and gates cyber-capable models with dedicated Guardian policies.
- **Safety posture**: Claude hardening the *boundary*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-08-06 | Source: github.com/anthropics/skills*

> Note: The dataset snapshot did not include per-PR comment counts; PR ordering reflects the comment-sorted export of 50 PRs.

## 1. Top Skills Ranking
The most-discussed PRs, combining new Skill submissions and critical fixes to the skill-creator toolchain. All remain open.

1. **skill-creator eval reliability fix** ([#1298](https://github.com/anthropics/skills/pull/1298)) — The highest-attention PR. Fixes `run_eval.py`'s systemic `recall=0%` failure (10+ independent reproductions of issue #556): installs the eval artifact as a real skill, repairs Windows stream reading, trigger detection, and parallel workers. The description-optimization loop was effectively optimizing against noise.

2. **document-typography** ([#514](https://github.com/anthropics/skills/pull/514)) — Typographic quality control for generated documents: orphan word wrap (1–6 words spilling to the next line), widow headings stranded at page bottom, and numbering misalignment — problems affecting every document Claude generates.

3. **ODT skill** ([#486](https://github.com/anthropics/skills/pull/486)) — OpenDocument text creation, template filling, and ODT/ODS→HTML conversion, covering LibreOffice and ISO-standard formats for users requesting open-source document output.

4. **frontend-design clarity overhaul** ([#210](https://github.com/anthropics/skills/pull/210)) — Revises the frontend-design skill so every instruction is actionable within a single conversation and specific enough to steer behavior without over-constraining.

5. **skill-quality-analyzer + skill-security-analyzer** ([#83](https://github.com/anthropics/skills/pull/83)) — Meta-skills for the marketplace: evaluate any Claude Skill across structure/documentation (20%), examples, resources, and security dimensions.

6. **testing-patterns** ([#723](https://github.com/anthropics/skills/pull/723)) — Comprehensive testing skill: Testing Trophy philosophy, what-to-test vs. not, AAA unit-test patterns, and React component testing with Testing Library.

7. **color-expert** ([#1302](https://github.com/anthropics/skills/pull/1302)) — Self-contained color expertise: naming systems (ISCC-NBS, Munsell, RAL, Ridgway…), a color-space "what to use when" table (OKLCH for scales, CAM16…).

8. **self-audit** ([#1367](https://github.com/anthropics/s

---

# Claude Code Community Digest — 2026-08-06

## Today's Highlights

Claude Code shipped **v2.1.223**, adding owner-wildcard marketplace controls (`owner/*`) and a warning for workflow agents, forked skills, slash commands, and resumed background work. The hottest community topics are silent MCP parameter loss, browser permission loops, and desktop stability crashes. A new PR also fixes a security-sensitive `pretooluse` hook failure mode by making it fail closed.

## Releases

### v2.1.223
- Added `"owner/*"` wildcard support for `strictKnownMarketplaces` and `blockedMarketplaces` managed settings, letting users allow/block all marketplace repos under a GitHub org.
- Added a warning when workflow agents, forked skills, slash commands, or resumed background agents are involved.

## Hot Issues

1. **[Feature] Session URL appended to commit messages and PR descriptions by default — should be opt-in** — [#66504](https://github.com/anthropics/claude-code/issues/66504)  
   High-community-interest feature request with **46 👍 and 12 comments**. Users want session links in git metadata, but not silently by default.

2. **[Bug] Claude Opus 4.8’s language is toxic/unpleasant; Opus 5.0 incoherent** — [#77136](https://github.com/anthropics/claude-code/issues/77136)  
   Strongly worded model-behavior complaint with 8 comments and 8 👍. Likely to draw maintainer attention to model output quality and tone controls.

3. **[Bug] Claude Desktop crashes near 5-hour usage limit, then requires full reinstall** — [#83403](https://github.com/anthropics/claude-code/issues/83403)  
   Severe reliability issue on Desktop. 7 comments; no workaround other than reinstalling.

4. **[Bug] `--continue` cannot find sessions created by `-p` (interactive resume)** — [#82536](https://github.com/anthropics/claude-code/issues/82536)  
   Session continuity regression affecting print-mode users trying to resume interactively. 7 comments.

5. **[Bug] MCP tool calls silently drop parameters emitted after a long parameter value** — [#72228](https://github.com/anthropics/claude-code/issues/72228)  
   Has a repro and 5 comments. Servers receive partial argument sets, leading to silent data loss.

6. **[Bug] Bundled ugrep balloons to 9–14 GB RSS on a bounded-interval BRE** — [#83342](https://github.com/anthropics/claude-code/issues/83342)  
   Agent grep calls transparently route to bundled ugrep and can consume massive memory. 4 comments.

7. **[Bug] Claude Desktop Windows — GPU process crash kills the whole app** — [#83744](https://github.com/anthropics/claude-code/issues/83744)  
   GPU process exitCode `101457950` takes down the entire desktop app. 4 comments.

8. **[Bug] "Always allow" for Claude-in-Chrome site permissions persists as `duration:"once"`** — [#74715](https://github.com/anthropics/claude-code/issues/74715)  
   Approved-sites list stays empty and permission prompts repeat for every browser action. 4 comments.

9. **[Bug] Foreground task returns "[Request interrupted by user for tool use]" with no user interrupt** — [#78915](https://github.com/anthropics/claude-code/issues/78915)  
   Spurious interruption string appears on macOS CLI subagent dispatches. 3 comments; cross-linked to related input-consumption bugs.

10. **[Bug] Tag-grammar tool-call parser silently absorbs parameter blocks on mismatched close tags** — [#84362](https://github.com/anthropics/claude-code/issues/84362)  
    Newly re-raised issue measuring **6.2% silent field loss** on parameter-rich MCP calls. Related to #72228 and previously closed #44826.

## Key PR Progress

Only **5 PRs** were active in the last 24 hours; all are listed here.

1. **[fix(scripts)] Allow any user to prevent auto-close with thumbs down** — [#84365](https://github.com/anthropics/claude-code/pull/84365)  
   Fixes #79146 by matching the dedupe bot’s behavior: any user’s thumbs-down can prevent issue auto-close.

2. **[fix(hookify)] Fail closed on exceptions in pretooluse hook** — [#84364](https://github.com/anthropics/claude-code/pull/84364)  
   Security fix: exceptions such as `ImportError` now exit with `permissionDecision: 'deny'` instead of allowing the gated tool to execute.

3. **[Plugins] Add 14 Revolutionary Claude Code Plugins** — [#41661](https://github.com/anthropics/claude-code/pull/41661)  
   Large marketplace expansion adding 14 plugin directories and updating `marketplace.json` to 27 plugins. Open since March; needs maintainer review.

4. **[fix(code-review)] Respect --comment flag for GitHub posting** — [#16929](https://github.com/anthropics/claude-code/pull/16929)  
   Fixes #16606 so `/code-review` outputs to the terminal by default and only posts to GitHub when `--comment` is explicitly passed.

5. **[fix] Workaround for self-signed certificate error in Cowork** — [#84138](https://github.com/anthropics/claude-code/pull/84138)  
   Fixes #24470: Claude Code’s Bun-based runtime doesn’t load system certificates on macOS, causing spurious self-signed certificate errors in PostToolUse hooks.

## Feature Request Trends

Across open issues, feature requests cluster into four directions:

- **Opt-in metadata and transcript control** — e.g. session URLs in commits/PRs should be opt-in ([#66504](https://github.com/anthropics/claude-code/issues/66504)); transcripts should be project-portable while scratch files stay local ([#81946](https://github.com/anthropics/claude-code/issues/81946)).
- **Browser permission and security controls** — persistent site permissions ([#74715](https://github.com/anthropics/claude-code/issues/74715), [#84355](https://github.com/anthropics/claude-code/issues/84355)), and reliable cross-machine device identification for connected browsers ([#77605](https://github.com/anthropics/claude-code/issues/77605)).
- **UI/UX configurability** — disabling or rebinding the left-arrow detach-to-background gesture ([#84348](https://github.com/anthropics/claude-code/issues/84348)).
- **Web/mobile CLI parity** — slash-command typeahead is still missing on mobile/web Claude Code ([#56204](https://github.com/anthropics/claude-code/issues/56204)).

## Developer Pain Points

- **Silent tool-call data loss** — MCP parameters are being dropped or absorbed in multiple parser paths ([#72228](https://github.com/anthropics/claude-code/issues/72228), [#84362](https://github.com/anthropics/claude-code/issues/84362)).
- **Permission-prompt fatigue** — Claude-in-Chrome repeatedly prompts on every browser action despite allow rules ([#74715](https://github.com/anthropics/claude-code/issues/74715), [#84355](https://github.com/anthropics/claude-code/issues/84355)).
- **Session continuity problems** — interactive resume fails after `-p` ([#82536](https://github.com/anthropics/claude-code/issues/82536)), and default session-URL injection irritates users ([#66504](https://github.com/anthropics/claude-code/issues/66504)).
- **Desktop instability** — Windows GPU crashes and usage-limit crashes require full reinstalls ([#83403](https://github.com/anthropics/claude-code/issues/83403), [#83744](https://github.com/anthropics/claude-code/issues/83744)).
- **Billing/usage attribution confusion** — users report incorrect model attribution in the usage panel ([#84359](https://github.com/anthropics/claude-code/issues/84359)), phantom extra charges ([#84358](https://github.com/anthropics/claude-code/issues/84358)), and rate-limit downgrades triggered by legitimate security testing ([#84340](https://

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-06

## 1. Today's Highlights

The Codex team shipped a stable patch (rust-v0.146.1) that tightens automatic-review defaults for cyber-capable models and explains permission changes in the terminal UI, alongside a burst of 0.147.0-alpha releases. Community attention remains heavily focused on Windows desktop stability — GPU-process crashes, `taskkill.exe`/WMI storms, and Sysmon-related BSODs — while the long-running `/undo` feature request (#9203) continues to dominate with 373 👍. On the engineering side, a wave of merged PRs lands significant architecture work around rollout migration, tool-namespace reservation, MCP handshake timeouts, and world-state orchestration.

## 2. Releases

| Version | Summary |
|---|---|
| [rust-v0.146.1](https://github.com/openai/codex/releases/tag/rust-v0.146.1) | Bug-fix release: applies safer automatic-review defaults for cyber-capable models and surfaces permission-change explanations in the terminal interface (backport of [#37057](https://github.com/openai/codex/pull/37057)). |
| rust-v0.147.0-alpha.6.5 / .10 / .11 / .12 / .13 | Alpha releases; no detailed changelogs published in the last 24h. |

## 3. Hot Issues

1. **[#9203 — Please make "/undo" back](https://github.com/openai/codex/issues/9203)** · 70 comments · 373 👍
   The highest-demand community feature. Users want `/undo` restored after Codex unintentionally deletes non-tracked files or modifies uncommitted work. Extreme 👍 count signals strong consensus for session-safety tooling.

2. **[#12491 — Codex.app GUI: MCP child processes not reaped — 1300+ zombies, 37GB memory leak](https://github.com/openai/codex/issues/12491)** · 32 comments
   MCP child processes accumulate after task completion in the GUI wrapper, causing zombie-process buildup and severe memory exhaustion. Highlights a lifecycle-management gap in the app-server MCP layer.

3. **[#33776 — ChatGPT.exe spawns hundreds of taskkill.exe/conhost.exe processes](https://github.com/openai/codex/issues/33776)** · 30 comments · 27 👍
   Windows desktop triggers WMI failure storms and DWM degradation via runaway `taskkill.exe`/`conhost.exe` spawns (287+ observed). Pairs with #34929, suggesting a systemic Windows process-manager problem.

4. **[#19425 — Custom stdio MCP server tools not exposed to Desktop threads](https://github.com/openai/codex/issues/19425)** · 29 comments
   `tools/list` discovers custom MCP tools, but they never reach Desktop threads or `tool_search`. Users report it as a regression in `0.124.0-alpha.2`, pointing to an exposure-layer bug in the app server.

5. **[#23979 — Local project conversation history missing after update](https://github.com/openai/codex/issues/23979)** · 26 comments
   Desktop update caused conversation histories to vanish from the UI, even though data remains in `state_5.sqlite` and rollout JSONL files. Data-preservation concern resonates with the rollout-migration PRs in flight.

6. **[#25178 — Windows Computer Use screenshot fails on Win10 22H2](https://github.com/openai/codex/issues/25178)** · 23 comments · 12 👍
   `get_window_state` fails at `SetIsBorderRequired` with `0x80004002` on Windows 10, blocking all screenshot-based Computer Use flows while non-screenshot actions work.

7. **[#31035 — Windows reinstall/start SysmonDrv v13.22; WinDbg points to SysmonDrv.sys BSODs](https://github.com/openai/codex/issues/31035)** · 23 comments
   Codex Desktop appears to reinstall Sysmon even after forced uninstall, followed by kernel crashes. A serious trust/safety concern for the Windows sandbox implementation.

8. **[#37002 — Unable to install after clicking Update in the Codex app](https://github.com/openai/codex/issues/37002)** · 20 comments
   Fresh report (Aug 5) of update-path installation failure — likely affects users on older macOS. Rapid comment growth suggests a widespread update regression.

9. **[#35481 — Codex Diff shows "Oops, an error has occurred" in VS Code](https://github.com/openai/codex/issues/35481)** · 18 comments · 49 👍 · **CLOSED**
   VS Code extension diff view broken on Windows; now closed (fix landed), but the high 👍 count shows how many users depend on inline diff review.

10. **[#32177 — Text-log attachment can trigger "Request blocked" and poison subsequent turns](https://github.com/openai/codex/issues/32177)** · 14 comments · 16 👍
    Attaching a plain-text log to a Desktop thread causes a hard "Request blocked" state that persists across subsequent turns. Signal-integrity bug with high annoyance factor for debugging workflows.

## 4. Key PR Progress

1. **[#37191 — Preserve legacy semantics during rollout migration](https://github.com/openai/codex/pull/37191)** · Merged
   Ensures legacy rollouts with rollbacks, compaction checkpoints, and subagent history copies don't change visible conversation or model context when migrated to paginated history.

2. **[#37190 — Interrupt cyber model turns after one Guardian denial](https://github.com/openai/codex/pull/37190)** · Merged
   Adds a circuit-breaker policy for cyber-specialty models, interrupting after the first Guardian denial while retaining existing thresholds for other models.

3. **[#37189 — Track multi-agent usage hints in world state](https://github.com/openai/codex/pull/37189)** · Merged
   Persists multi-agent usage instructions in world state so resumed sessions survive configuration changes or pre-tracking history.

4. **[#37188 — Reserve the `tool_search` namespace for the search tool](https://github.com/openai/codex/pull/37188)** · Merged
   Removes namespace tools named `tool_search` before registering the built-in search tool; records collisions for strict handling. Addresses namespace-confusion bugs like [#32101](https://github.com/openai/codex/issues/32101).

5. **[#37175 — Add legacy rollout migration to paginated history](https://github.com/openai/codex/pull/37175)** · Merged
   Introduces `LocalThreadStore::migrate_rollouts` with dry-run/apply modes, throughput limiting, and per-rollout outcomes — the infrastructure behind the history-preservation fixes.

6. **[#37168 — Bound remote MCP handshake HTTP requests](https://github.com/openai/codex/pull/37168)** · Merged
   Fixes a deadlock where a timed-out streamable HTTP MCP handshake left the serial executor blocked; now tracks the remaining init deadline.

7. **[#37166 — Keep textarea cursors and rendering inside the viewport](https://github.com/openai/codex/pull/37166)** · Merged
   Reserves continuation rows for full-width logical lines and clips overflowing spaces — a TUI polish fix for cursor drift and mask rendering.

8. **[#37157 — Harden named session lookup in the TUI](https://github.com/openai/codex/pull/37157)** · Merged
   Shares exact-name candidate lookup between resume/archive commands, prefers valid SQLite names, and validates rollout identity/collection/source. Directly relevant to history-disappearance reports.

9. **[#37151 — Coalesce concurrent Git status scans](https://github.com/openai/codex/pull/37151)** · Merged
   Shares a single in-flight `git status --porcelain` across concurrent workspace metadata requests for the same repo root — a meaningful perf win for large-resume workloads (cf. #32309).

10. **[#37167 — Expose session sources to MCP contributors](https://github.com/openai/codex/pull/37167)** · Merged
    Propagates each thread's `SessionSource` through MCP setup/resolution so thread-scoped MCP servers resolve correctly in Desktop contexts.

Other notable merges: [#37178](https://github.com/openai/codex/pull/37178) (image transparency metadata), [#37177](https://github.com/openai/codex/pull/37177) (explicit skill selection moved to skills crate), [#37174](https://github.com/openai/codex/pull/37174) (centralized skill invocation helpers), [#37169](https://github.com/openai/codex/pull/37169) (plugin skill snapshot tests into core), [#37162](https://github.com/openai/codex/pull/37162) (host skill roots via skills extension), [#37156](https://github.com/openai/codex/pull/37156) (remote env readiness tests), [#37154](https://github.com/openai/codex/pull/37154) (Azure Key Vault for macOS notarization), [#37149](https://github.com/openai/codex/pull/37149) (orchestrator skills via world state), [#37147](https://github.com/openai/codex/pull/37147) (provisioned env state tracking).

## 5. Feature Request Trends

- **Session safety / undo**: The `/undo` demand (#9203) is the clearest signal — users need recovery from destructive file operations on non-git-tracked or uncommitted work.
- **History & thread persistence**: Multiple issues (#23979, #35481, #37175) revolve around conversation history surviving updates, migrations, and UI refreshes.
- **MCP reliability & lifecycle**: Custom MCP servers being discovered but not exposed (#19425), zombie processes (#12491), and OAuth flow failures (#34684) point to MCP as a top integration priority.
- **Windows desktop stability**: A cluster of issues demands fixing the Windows process manager, sandbox driver behavior, GPU/browser crashes, and input lag (see Pain Points below).
- **Context/compaction transparency**: Users want fewer surprise "Request blocked" states and more reliable compaction (#32177, #32533, #31375, #33493).

## 6. Developer Pain Points

- **Windows app is the dominant complaint surface**: runaway `taskkill.exe`/`conhost.exe` spawning with 40–50% idle CPU (#34929), WMI storms and DWM degradation (#33776), and Sysmon reinstallation causing BSODs (#31035).
- **In-app browser/GPU crashes on Windows**: Multiple reports of `vk_swiftshader.dll` Code Integrity blocks taking down the whole desktop session (#35352, #35411, #35566, #35635) — all closed, indicating recent fixes, but the pattern was severe.
- **MCP process leaks**: Zombie children and multi-GB memory growth after tasks complete (#12491) — a reliability blocker for MCP-heavy workflows.
- **Sandbox & permission regressions**: Approval mode silently reverting to `on-request` (#32862), escalated commands inheriting restricted network policy (#15309),

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*