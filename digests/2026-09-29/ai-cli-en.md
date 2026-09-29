# AI CLI Tools Community Digest 2026-09-29

> Generated: 2026-09-29 03:57 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool AI CLI Ecosystem Comparison — 2026-09-29

## 1. Ecosystem Overview

Both Claude Code and OpenAI Codex shipped releases in the window, but community attention is dominated less by new features than by **reliability, data integrity, and platform-specific regressions**. Claude Code’s v2.1.284 introduces Sonnet 5.5 as the default Sonnet model while facing a Linux freeze regression tied to sandbox glob expansion. Codex’s rust-v0.158.0 focuses on TUI copy/paste and MCP OAuth, but copy/paste regressions from 0.157.0 and Windows desktop failures remain highly visible. Across both communities, MCP/plugin authentication, cross-surface session continuity, usage observability, and Windows/macOS deployment quality are emerging as platform-level requirements. The ecosystem is iterating quickly, but users are increasingly version-pinning and treating silent data loss or broken core workflows as trust-damaging events.

---

## 2. Activity Comparison

| Tool | Issues in Digest Window | PRs in Digest Window | Release Status | Dominant Themes |
|---|---:|---:|---|---|
| **Claude Code** | 10 hot issues + 5 watchlist; trend analysis cites 30 surfaced issues | 6 PRs updated in last 24h | **v2.1.284** stable; Sonnet 5.5 default; Linux freeze regression #98023 | Data integrity, desktop performance, cross-surface Skills sync, agent compaction |
| **OpenAI Codex** | 10 hot issues | 10 key PRs + 2 notable = 12 | **rust-v0.158.0** stable; **0.160.0-alpha.3/.2**, **0.159.0-alpha.13** | Windows desktop regressions, copy/paste breakage, MCP OAuth, console window spam |

**Data note:** Counts reflect items explicitly listed in the provided 24h digests, not full tracker totals. Claude Code’s PR queue is notably thin; Codex shows higher PR throughput and alpha cadence.

---

## 3. Shared Feature Directions

| Direction | Claude Code Evidence | Codex Evidence | Shared Need |
|---|---|---|---|
| **Cross-surface/session continuity** | Skills sync Desktop ↔ CLI #20697 (157 👍), mobile-started Desktop sessions #96867, session-history portability #98051 | Remote Control macOS/iOS failures #36946/#40558, password SSH login #44446, clear-context command #19829 | Unified session, skill, and context identity across CLI, desktop, web, mobile, and remote hosts |
| **MCP/plugin lifecycle & auth** | User-scope MCP shadowing plugin server #98035 | OAuth client-secret support in 0.158.0; Supabase MCP reauth #13852; plugin manifest cache PRs #49099/#49100 | Predictable conflict resolution and reliable OAuth/token refresh for MCP and plugins |
| **TUI/input ergonomics** | Enter now interrupts instead of queueing #93239; theme polish #73837; glob-expander freeze #98023 | Copy/paste regressions #47996, #48125, #49092; X11 primary selection PR #49112; copy-on-select in 0.158.0 | Terminal conventions must be stable, configurable, and cross-emulator consistent |
| **Data integrity

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights
**Data as of 2026-09-29.** Note: PR comment counts are `undefined` in the supplied snapshot, so the PR ranking below uses related Issue discussion volume, update recency, and issue-linked clusters as attention proxies. All top-20 PRs shown are **OPEN**; none are marked merged or draft.

## 1. Top Skills

---

# Claude Code Community Digest — 2026-09-29

Source: [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)

---

## 1. Today's Highlights

A new release (**v2.1.284**) ships **Claude Sonnet 5.5** as the default Sonnet model on the Anthropic API (1M context, $2/$10 per Mtok, $0.20/Mtok cache reads) — but a Linux regression report alleges the same build freezes on first Enter due to the new sandbox glob expander. Meanwhile, the issue tracker is dominated by **data-integrity and desktop-performance problems**: silent 30-day transcript deletion (#62476), stale writes from Cowork's `device_commit_files` (#93482), and the Windows desktop app spawning ~17 `git.exe` per second (#94478). The most-upvoted open request remains cross-surface **Skills sync between Claude Desktop and the Code CLI** (#20697, 157 👍).

---

## 2. Releases

### v2.1.284 (latest)
- **Claude Sonnet 5.5 (`claude-sonnet-5-5`)** added and now the **default Sonnet model** on the Anthropic API — 1M context window, **$2 / $10 per Mtok**, **$0.20/Mtok cache reads**.
- **Auto mode prompt**: new `"Yes, but ask again next time"` answer for reads outside the working directories, giving a middle ground between one-off approval and permanent allowlisting.
- ⚠️ Changelog provided is truncated; no further entries verified.
- ⚠️ **Regression watch:** [#98023](https://github.com/anthropics/claude-code/issues/98023) reports 2.1.284 freezing permanently on first Enter on Linux — the new sandbox glob expander allegedly walks all of `~` synchronously for `~/**/…` `denyRead` patterns (follows symlinks, unbounded memory). 2.1.280 is unaffected. Users with broad `denyRead` globs should hold off or narrow them.

---

## 3. Hot Issues (10 noteworthy)

| # | Issue | Why it matters | Reaction |
|---|-------|----------------|----------|
| 1 | [#91188](https://github.com/anthropics/claude-code/issues/91188) — make auto-memory `MEMORY.md` compaction threshold configurable | Auto-memory loads only the first 200 lines / 25KB of `MEMORY.md`; the compaction reminder threshold is hardcoded and unsuppressable. Long-lived memory files are effectively truncated with no user control. | **58 comments** — highest-activity issue in the window, zero 👍 (debate-heavy) |
| 2 | [#20697](https://github.com/anthropics/claude-code/issues/20697) — Sync Skills between Claude Desktop and Claude Code CLI | Skills authored for one surface are invisible to the other, forcing duplication. This is the highest-signal request for a unified authoring/runtime story. | **157 👍 / 49 comments** — top-voted open enhancement |
| 3 | [#62476](https://github.com/anthropics/claude-code/issues/62476) — transcripts silently deleted after 30 days by default | Silent data loss of conversation history with no obvious warning; `[bug, reproduced]`. Undermines auditability and recall for long-running projects. | 27 👍 / 25 comments |
| 4 | [#94478](https://github.com/anthropics/claude-code/issues/94478) — Windows desktop spawns ~15–20 `git.exe`/sec continuously | ~2M short-lived processes/day per open app; aggravates a kernel pool leak into **~6 GB/day** memory growth. Serious resource-exhaustion bug on Windows. | 4 comments, `has repro`, performance label |
| 5 | [#93482](https://github.com/anthropics/claude-code/issues/93482) — Cowork `device_commit_files` reports success but disk lags one commit | Silent stale writes with fresh mtime — the worst class of data-loss bug because tooling reports success. Windows, `data-loss`. | 15 comments |
| 6 | [#70647](https://github.com/anthropics/claude-code/issues/70647) — native installer produces unsealed macOS app bundle | `ClaudeCode.app` is installed without `_CodeSignature`, so macOS reports it as "damaged and can't be opened." Blocks install for macOS users and enterprise MDM. | 15 comments / 5 👍 |
| 7 | [#98023](https://github.com/anthropics/claude-code/issues/98023) — 2.1.284 freezes on first Enter (sandbox glob expander) | Fresh regression against the release shipping today; makes the TUI unusable on affected Linux configs. | Filed 2026-09-28, already triaged with repro |
| 8 | [#97665](https://github.com/anthropics/claude-code/issues/97665) — subagent compaction drops the preserved segment's tail record | The compaction boundary references a message that never lands in the subagent transcript, and unlike #97316 it is never recovered. Corrupts the agent audit trail. | 2 comments, macOS `area:agents` |
| 9 | [#95601](https://github.com/anthropics/claude-code/issues/95601) — every background agent completion fires two parent-turn events | `SubagentHandback` + a redundant task-notification double-notify the parent turn, skewing orchestration and token accounting for anyone scripting agents. | Linux, 3 👍 |
| 10 | [#93239](https://github.com/anthropics/claude-code/issues/93239) — Enter now interrupts instead of queueing (regression) | Breaks a core input idiom on Windows desktop: users lose the ability to queue prompts while Claude is working. | 4 comments, `regression` |

**Also worth watching:** [#97997](https://github.com/anthropics/claude-code/issues/97997) (Fable weekly usage counted at 20% with zero Fable requests — billing/quota accuracy), [#98017](https://github.com/anthropics/claude-code/issues/98017) (safety classifier blocking legitimate admin-UI generation), [#95276](https://github.com/anthropics/claude-code/issues/95276) (stealth auto-update drops all Remote Control sessions), [#81776](https://github.com/anthropics/claude-code/issues/81776) (`claude --cloud` always bundles, ignoring `/web-setup` and repo binding), [#98052](https://github.com/anthropics/claude-code/issues/98052) (worktree subagents load `CLAUDE.md` and `@imports` twice).

---

## 4. Key PR Progress

Only **6 PRs** were updated in the last 24h — all are covered below (the requested 10 are not available in this window).

1. [#94847](https://github.com/anthropics/claude-code/pull/94847) *(OPEN)* — **diff pane**: only auto-opens on the first Edit/Write/NotebookEdit when there is actually a file to list, instead of opening pre-fetch and showing "No tracked changes" for out-of-repo, ignored, or other-worktree writes. Fixes a persistent empty-pane annoyance.
2. [#98018](https://github.com/anthropics/claude-code/pull/98018) *(CLOSED)* — **mods: revert two changes**, restoring earlier behavior for the `agents-md` and `diff` mods by reverting #96363 and #96364. Signals churn in the mod/plugin layer.
3. [#97952](https://github.com/anthropics/claude-code/pull/97952) *(OPEN)* — **CI security hardening** for the three workflows that call Claude (`claude-issue-triage.yml`, `claude-dedupe-issues.yml`, `claude.yml`): egress-firewall runner and tightened credential handling. Relevant to anyone self-hosting these automations.
4. [#96364](https://github.com/anthropics/claude-code/pull/96364) *(CLOSED, reverted)* — `agents-md`: an auto-paginated whole-file `Read` of a nested `AGENTS.md` no longer counts as delivering it, preventing duplicate attachment on later reads.
5. [#96363](https://github.com/anthropics/claude-code/pull/96363) *(CLOSED, reverted)* — `diff`: pass `--no-color` so forced git colors (`color.ui=always`) don't empty the diff body.
6. [#31204](https://github.com/anthropics/claude-code/pull/31204) *(CLOSED)* — community-submitted interactive canvas AI-learning-roadmap app (React/Vite, localStorage persistence). Closed without merge; notable only as a long-lived community contribution.

**Takeaway:** the PR queue is thin and dominated by internal mod/plugin reverts and CI hardening — no user-facing feature PRs landed in this window.

---

## 5. Feature Request Trends

Distilled from all 30 surfaced issues plus recent release notes:

1. **Configurability of implicit context/memory** — Hardcoded thresholds are the friction point: [#91188](https://github.com/anthropics/claude-code/issues/91188) (MEMORY.md compaction), [#98052](https://github.com/anthropics/claude-code/issues/98052) (CLAUDE.md double-loading via worktrees). Users want knobs, not magic numbers.
2. **Cross-surface continuity** — Skills sync between Desktop and CLI ([#20697](https://github.com/anthropics/claude-code/issues/20697)), starting Desktop Code sessions from mobile ([#96867](https://github.com/anthropics/claude-code/issues/96867)), and session-history portability across machines ([#98051](https://github.com/anthropics/claude-code/issues/98051)).
3. **Data retention transparency & controls** — Explicit opt-in/opt-out around the 30-day transcript purge ([#62476](https://github.com/anthropics/claude-code/issues/62476)) and whether stats rebuilds lose purged history ([#94479](https://github.com/anthropics/claude-code/issues/94479)).
4. **MCP / plugin coexistence** — Let user-scope MCP servers intentionally shadow a plugin's server without a warning, or let plugins opt out ([#98035](https://github.com/anthropics/claude-code/issues/98035), closed).
5. **Cost & quota observability** — Per-model usage attribution that matches actual requests ([#97997](https://github.com/anthropics/claude-code/issues/97997)).
6. **Themeability & TUI polish** — Make markdown code spans honor custom theme overrides ([#73837](https://github.com/anthropics/claude-code/issues/73837)).
7. **Fewer silent model behaviors** — Prose hard-wrapping/max-width capping recurring despite `CLAUDE.md` and memory ([#89274](https://github.com/anthropics/claude-code/issues/89274)).

---

## 6. Developer Pain Points

- **Silent data loss is the #1 trust issue.** Three separate vectors this week: 30-day transcript deletion ([#62476](https://github.com/anthropics/claude-code/issues/62476)), Cowork's stale-but-successful writes ([#93482](https://github.com/anthropics/claude-code/issues/93482)), and the desktop heatmap losing days because only the CLI writes `stats-cache.json` ([#87772](https://github.com/anthropics/claude-code/issues/87772)).
- **The desktop app is a resource sink.** ~17 `git.exe`/sec and ~6 GB/day growth on Windows ([#94478](https://github.com/anthropics/claude-code/issues/94478)), an `EventEmitter` listener leak causing periodic freezes ([#92785](https://github.com/anthropics/claude-code/issues/92785)), and stealth auto-updates killing live Remote Control sessions ([#95276](https://github.com/anthropics/claude-code/issues/95276)).
- **Regressions keep landing in minor releases.** Glob-expander freeze on 2.1.284 ([#98023](https://github.com/anthropics/claude-code/issues/98023)) and Enter-now-interrupts on desktop ([#93239](https://github.com/anthropics/claude-code/issues/93239)). Several reporters explicitly pin "2.1.280 fine" as a workaround — a sign that users are version-pinning to survive.
- **Agent/compaction transcripts are unreliable.** Subagent compaction loses the preserved segment tail ([#97665](https://github.com/anthropics/claude-code/issues/97665)) and duplicate handback events double-fire parent turns ([#95601](https://github.com/anthropics/claude-code/issues/95601)) — painful for anyone automating or auditing multi-agent runs.
- **Installation & platform trust.** The unsealed macOS bundle ([#70647](https://github.com/anthropics/claude-code/issues/70647)) blocks installs outright and is hostile to MDM-managed fleets; a Linux crash on 2.1.261 ([#92307](https://github.com/anthropics/claude-code/issues/92307)) remains open.
- **Model behavior and safety are perceived as opaque.** Safety classifier false positives on ordinary code generation ([#98017](https://github.com/anthropics/claude-code/issues/98017)), Fable 5.1 emitting its final answer as a thinking block so users never see it ([#91939](https://github.com/anthropics/claude-code/issues/91939)), and quota attributed to models never used ([#97997](https://github.com/anthropics/claude-code/issues/97997)).
- **Configuration drift across surfaces.** Settings, skills, and sessions don't travel cleanly between CLI, Desktop, web, and mobile ([#20697](https://github.com/anthropics/claude-code/issues/20697), [#81776](https://github.com/anthropics/claude-code/issues/81776), [#98051](https://github.com/anthropics/claude-code/issues/98051)).

---

*Data note: issue/PR counts reflect items updated within the last 24h as provided; the 6 PRs above are the complete set in that window.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-09-29

## 1. Today's Highlights

The Codex team shipped a copy/paste-focused rust-v0.158.0 release that adds configurable copy-on-select and right-click paste in the fullscreen TUI, Markdown-preserving transcript copies, and support for MCP servers requiring pre-registered OAuth client secrets. Meanwhile, the issue tracker is dominated by a wave of Windows desktop regressions (startup hangs on the loading screen, disappearing projects, and focus-stealing console windows) plus copy/paste breakage across Linux and macOS terminals introduced around CLI 0.157.0.

## 2. Releases (last 24h)

- **[rust-v0.158.0](https://github.com/openai/codex/releases)** — Stable release. Configurable copy-on-select and right-click paste in the fullscreen TUI; copied transcript selections now preserve Markdown formatting (#47639, #47896, #48118). Adds connectivity to MCP servers that require pre-registered OAuth client secrets, including via `codex mcp add --oauth-client…`.
- **rust-v0.160.0-alpha.3 / alpha.2** — Roll-forward alpha builds with no public changelog.
- **rust-v0.159.0-alpha.13** — Incremental alpha build.

Note: the copy/paste work in 0.158.0 lands directly against the highest-engagement regressions below, but the fixes do not appear to cover every affected terminal.

## 3. Hot Issues

1. **[#25220 — [Windows] Bundled plugins (Computer Use, Browser, Chrome, LaTeX) unavailable — copyfile fails on EFS-encrypted WindowsApps](https://github.com/openai/codex/issues/25220)** — 44 comments, 5 👍. Longest-running active thread: Microsoft Store installs fail to copy plugin payloads on EFS-encrypted `WindowsApps`, disabling Computer Use, Browser, Chrome, and LaTeX. High impact because it silently removes core capabilities for Store users.
2. **[#42739 — Local projects disappear from sidebar after Windows desktop update](https://github.com/openai/codex/issues/42739)** — 36 comments. Projects vanish while chats remain in Recents and folders remain on disk; a data-presentation regression rather than data loss, but highly visible and still unresolved since early September.
3. **[#48422 — Windows: visible console windows flash for shell process children on every session/turn](https://github.com/openai/codex/issues/48422)** — 29 comments, 31 👍. The single most-upvoted issue in the current window. Constant console flashing makes Windows CLI sessions unusable for many; closely related to [#44768](https://github.com/openai/codex/issues/44768) and [#48440](https://github.com/openai/codex/issues/48440).
4. **[#13852 — Supabase MCP repeatedly requires reauthentication: OAuth token refresh failed during initialize](https://github.com/openai/codex/issues/13852)** — 24 comments. A six-month-old MCP auth defect that is gaining new attention as OAuth-secured MCP servers become common — directly relevant to the new `--oauth-client-secret` support in 0.158.0.
5. **[#48463 — Windows desktop app stuck on loading screen after update (26.924.2738.0)](https://github.com/openai/codex/issues/48463)** — 20 comments, 2 👍. Bootstrap timeout after the `codex-home` request; corroborated by [#48466](https://github.com/openai/codex/issues/48466), [#48492](https://github.com/openai/codex/issues/48492), and [#48896](https://github.com/openai/codex/issues/48896), forming the largest cluster of the week.
6. **[#44768 — Windows: app-server daemon opens a visible console window for every hook and shell command](https://github.com/openai/codex/issues/44768)** — 18 comments, 7 👍. Shows the shared app-server daemon amplifies the console-window problem across every TUI session sharing `CODEX_HOME`.
7. **[#48125 — "I CANT FUCKING COPY TEXT" (CLOSED)](https://github.com/openai/codex/issues/48125)** — 16 comments, 19 👍. Closed, but its tone captures community frustration over the 0.157.0 copy regression; a strong signal about release-quality expectations for the TUI.
8. **[#47996 — [macOS][CLI 0.157.0] Cmd+C no longer copies selected transcript text in iTerm2](https://github.com/openai/codex/issues/47996)** — 14 comments, 17 👍. Platform-specific counterpart to the Linux reports ([#49092](https://github.com/openai/codex/issues/49092), [#27811](https://github.com/openai/codex/issues/27811)), indicating the regression spans multiple terminal emulators.
9. **[#40558 — [macOS][Remote iOS] Desktop-created active threads fail to load due to active-writer conflict](https://github.com/openai/codex/issues/40558)** — 9 comments, 6 👍. Blocks the Remote Control workflow across desktop and iOS; pairs with [#36946](https://github.com/openai/codex/issues/36946) (Remote Control cannot be enabled on macOS, 8 👍).
10. **[#47041 — GPT-5.6 Sol and GPT-6 Astra reject harmless prompts with `invalid_prompt`](https://github.com/openai/codex/issues/47041)** — 6 comments. Model-behavior regression with a duplicate report at [#43781](https://github.com/openai/codex/issues/43781); false-positive policy rejections erode trust in the default models.

## 4. Key PR Progress

1. **[#49153 — Omit blockquote markers when copying quoted selections in the TUI](https://github.com/openai/codex/pull/49153)** — Stops injecting Markdown `>` markers into plain-text selections; a follow-up to this week's copy fixes.
2. **[#49112 — Add X11 primary selection and middle-click paste support](https://github.com/openai/codex/pull/49112)** — Publishes selections to X11 `PRIMARY` and pastes via middle-click, addressing long-standing Linux copy/paste friction.
3. **[#49105 — Resume unsent TUI input after reconnecting](https://github.com/openai/codex/pull/49105)** — Separates unsent from unconfirmed messages so queued input auto-resumes after reconnect, a reliability win for remote/daemon sessions.
4. **[#49144 — Preserve server reasoning summary and verbosity settings in the TUI](https://github.com/openai/codex/pull/49144)** — Stops local defaults from overriding server-side model settings. Companion to [#49145](https://github.com/openai/codex/pull/49145), which hides these settings in `/status` for server connections.
5. **[#49135 — Treat explicit provider model catalogs as authoritative](https://github.com/openai/codex/pull/49135)** — Prevents bundled/stale models from leaking into providers with `model_catalog_url`, and requires exact model ID matching.
6. **[#49130 — Move content-filter guidance into the shared Responses retry handler](https://github.com/openai/codex/pull/49130)** — Consolidates retry behavior for `content_filter` stops; builds on [#49119](https://github.com/openai/codex/pull/49119), which adds recovery guidance to content-filter retries (relevant to the false-positive reports above).
7. **[#49138 — Expose original error details to turn lifecycle contributors](https://github.com/openai/codex/pull/49138)** — Adds `CodexErrorDetails` to `TurnErrorInput`, surfacing usage-limit reset times and rate-limit snapshots to hooks — useful for teams building observability on top of Codex.
8. **[#49099 — Cache parsed plugin manifests across plugin workflows](https://github.com/openai/codex/pull/49099)** — Shares a manifest cache across marketplace, loading, and capability inspection; reduces repeated parsing and duplicate warnings.
9. **[#49100 — Reuse the HTTP connection pool for remote plugin requests](https://github.com/openai/codex/pull/49100)** — Replaces per-config HTTP clients with a shared, route-aware pool for remote plugin service calls.
10. **[#49102 — Preserve SQLite vacuum modes and surface pool initialization errors](https://github.com/openai/codex/pull/49102)** — Fixes masked `PoolTimedOut` failures during SQLx pool init and avoids blocking auto-vacuum mode changes.

Other notable items: [#49106](https://github.com/openai/codex/pull/49106) adds history pagination ("Show more") to the agent command center, and [#49103](https://github.com/openai/codex/pull/49103) balances Windows Bazel test shards by estimated duration. Most of these PRs are authored by `copyberry[bot]` and merged as CLOSED, indicating an automated/agent-assisted review pipeline.

## 5. Feature Request Trends

- **Session and context control** — [#19829](https://github.com/openai/codex/issues/19829) requests a command to clear context within the current session, motivated by running review skills on fresh context without restarting. Context hygiene remains a top ask.
- **Remote/SSH ergonomics** — [#44446](https://github.com/openai/codex/issues/44446) asks for password-based SSH login in Connections without pre-configuring a private key; adjacent to the Remote Control enablement requests ([#36946](https://github.com/openai/codex/issues/36946), [#40558](https://github.com/openai/codex/issues/40558)).
- **TUI input/output configuration** — The 0.158.0 release notes show the team responding to demand for configurable copy-on-select, right-click paste, and Markdown-preserving copies; lingering issues ([#49092](https://github.com/openai/codex/issues/49092), [#27811](https://github.com/openai/codex/issues/27811)) show coverage is still incomplete per-terminal.
- **MCP authentication maturity** — OAuth client-secret support shipped, but [#13852](https://github.com/openai/codex/issues/13852) shows token refresh reliability is the next expected step.
- **Cross-platform parity** — Repeated requests for Windows/macOS/Linux behavior to match (console suppression, plugin availability, paste semantics) run through nearly every thread.
- **Usage transparency** — [#48296](https://github.com/openai/codex/issues/48296) seeks accurate analytics for Pro weekly resets and Subagent consumption; ties to PR #49138 exposing rate-limit metadata.

## 6. Developer Pain Points

- **Windows desktop is the dominant source of friction.** Startup hangs on the loading screen after recent 26.924.x updates ([#48463](https://github.com/openai/codex/issues/48463), [#48466](https://github.com/openai/codex/issues/48466), [#48492](https://github.com/openai/codex/issues/48492), [#48896](https://github.com/openai/codex/issues/48896)), vanishing Projects ([#42739](https://github.com/openai/codex/issues/42739)), and EFS-related plugin failures ([#25220](https://github.com/openai/codex/issues/25220)) are collapsing into a single "Windows build quality" complaint.
- **Console window spam.** Visible console flashes on every turn, hook, and shell command — especially with the shared app-server daemon — are the most-upvoted pain point ([#48422](https://github.com/openai/codex/issues/48422), [#44768](https://github.com/openai/codex/issues/44768), [#48440](https://github.com/openai/codex/issues/48440)).
- **Copy/paste regressions are cross-platform and emotional.** The 0.157.0 regression broke fundamental terminal workflows on iTerm2, mate-terminal, SSH sessions, and Warp ([#47996](https://github.com/openai/codex/issues/47996), [#48125](https://github.com/openai/codex/issues/48125), [#49092](https://github.com/openai/codex/issues/49092), [#27811](https://github.com/openai/codex/issues/27811)).
- **False-positive content filtering.** GPT-6 Astra / GPT-5.6 Sol rejecting benign prompts as policy violations ([#47041](https://github.com/openai/codex/issues/47041), [#43781](https://github.com/openai/codex/issues/43781)) undermines confidence in default models.
- **Remote Control and multi-device flows remain fragile.** macOS enablement failures, iOS active-writer conflicts, and Android pairing loops ([#36946](https://github.com/openai/codex/issues/36946), [#40558](https://github.com/openai/codex/issues/40558), [#49132](https://github.com/openai/codex/issues/49132)) suggest the remote story is not yet production-ready.
- **Ecosystem/auth plumbing gaps.** MCP OAuth refresh ([#13852](https://github.com/openai/codex/issues/13852)), SSRF/password-auth limits ([#44446](https://github.com/openai/codex/issues/44446)), and CLI platform/package mismatches ([#48366](https://github.com/openai/codex/issues/48366)) add up to a nontrivial setup tax for teams.
- **Long-lived bugs signal triage lag.** Issues opened in March, April, June, and August remain open with active September traffic, reinforcing community perception that Windows and auth fixes are deprioritized relative to release velocity.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*