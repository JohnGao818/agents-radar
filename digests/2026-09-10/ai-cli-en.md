# AI CLI Tools Community Digest 2026-09-10

> Generated: 2026-09-10 02:51 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report — AI CLI Developer Tools
**Digest date: 2026-09-10 | Tools in scope: Claude Code, OpenAI Codex**

> **Data caveats:** Scope is limited to the two digests supplied. Claude Code discloses an explicit 24h issue volume (50); Codex does not, so its issue figure is a floor derived from items surfaced in the digest. Comment and 👍 counts are point-in-time snapshot values.

---

## 1. Ecosystem Overview

Both flagship CLIs shipped on the same day with opposite emphases: Claude Code shipped **governance** (v2.1.267's `maxEffortLevel` effort ceiling and fresh system-prompt rendering), while Codex shipped **capability and surface area** (rust-v0.154.0 with GPT-6-Astra in the model picker/Bedrock catalogs plus experimental worktree isolation). The two communities nonetheless converge on the same unresolved fundamentals: **cost/quota transparency**, **session-state durability**, and **Windows as the dominant failure surface**. A striking asymmetry in the day's activity is Claude Code's 50 updated issues against only 3 PRs, versus Codex's ~14 merged/closed PRs largely driven by automation — suggesting Codex's pipeline is currently more throughput-oriented while Claude Code's issue backlog is outgrowing its visible fix rate. Credential-rotation races under concurrent sessions appear independently in both ecosystems, indicating an architectural pattern rather than isolated incidents.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|---|---|---|
| **Issues updated (24h)** | **50** (disclosed) | Not disclosed; **≥14** surfaced (10 hot + 4 watchlist) |
| **Top issue engagement** | #85891 — 93 comments, 👍225 (always-on-top window) | #25178 — 54 comments, 👍23; #21653 — 👍83 (highest vote) |
| **PRs updated (24h)** | **3** (2 open, 1 closed same-day) | **14** merged/closed (10 key + 4 additional), mostly `copyberry[bot]` |
| **Issue:PR ratio** | ~17:1 (backlog-heavy) | Not computable (issue total undisclosed) |
| **Release status** | **1 stable**: v2.1.267 — no alphas noted | **1 stable + 3 alphas**: rust-v0.154.0; 0.154.0-alpha.6.1/10.2/11 |
| **Release theme** | Effort-level governance (`maxEffortLevel`), `--system-prompt-snapshot off` | GPT-6-Astra in picker + Bedrock; `--worktree` / `/worktree` isolation |
| **Dominant bug cluster** | Windows Cowork/Desktop regression (Plan9 mounts, sandbox, hangs, VM runtime) | Windows Computer Use + session/rollout durability |
| **Notable same-day severity** | Quota cluster (#93068/#93100/#93243) | #44363 compaction destroying transcripts; #44386 cached-input replay draining Plus |

**Reading the table:** Claude Code's engagement is concentrated in a few very high-traffic threads (225 upvotes on a single issue), while Codex's momentum shows up in release/PR cadence rather than issue volume.

---

## 3. Shared Feature Directions

Requirements appearing in **both** communities:

| Direction | Claude Code evidence | Codex evidence |
|---|---|---|
| **Cost / effort / quota control** | `maxEffortLevel` (v2.1.267); 5-hour limits hit in minutes (#93068, #93100); "monthly" behaving daily (#93243); subagents defaulting to a different model (#80902); `code-review` ignoring `--level low` (#92436) | Restore 5-hour limit or explicit Ultra budgets (#34822); cached-input replay per tool call draining Plus usage (#44386) |
| **Session-state durability & isolation** | Worktree lock held by dead PID (#93231); background-session git rules lacking precedence (#87996) | Compaction rewrites rollouts in place, destroying transcripts (#44363); resume reusing rollout ordinals freezing history (#43142); empty history after migration (#44033) |
| **Credential / OAuth rotation races** | Keychain `claudeAiOauth` wiped by concurrent Desktop sessions (#88583); same class in remote MCP OAuth (#91641) | Rotated refresh token lost on MCP shutdown (#41133); remote-control sessions bound to auth owner (#44341, PR) |
| **Windows parity & stability** | KB5124008 breaking Plan9 shares (#92984); sandbox not mounting (#92977); sessions hang (#92921); VM runtime never verifying (#93238) | Computer Use screenshot failure (#25178); Chrome URL resolution (#25271); app launch failure (#42501); process/memory leaks (#29079); Remote Control 503 (#44384) |
| **Reducing permission / safety friction** | Quoted-character warning on ordinary commands (#27957); site permissions ignored by built-in browser (#91495) | False-positive `content_filter` interruptions on literary text (#43969) and JPEG XL probe (#44380) |
| **MCP / plugin lifecycle correctness** | GitHub connector missing from `/mcp` (#29415); four shipped plugin agents fail YAML frontmatter (#91871); validator false-flagging (#83803 → PR #89404) | Duplicate `mcp__*` namespace hard-fails a thread (#44378); OAuth failures reported in MCP status snapshots (#44359, PR) |
| **UI observability & ergonomics** | Chat panel font size (#34196, 👍87); expose context window + cost to local tools (#92853) | Multi-line status line (#21653, 👍83); escape returns focus to composer (#44360, PR) |
| **Remote / cross-device session control** | Start new remote session from mobile with device picker (#91815); reopen a routine's session (#76841) | Remote Control enrollment/relay reliability (#44384); auth-owner binding (#44341) |

**Tool-exclusive directions:** Claude Code — Desktop app configurability (simultaneous spellchecker languages #88502), privacy-preserving feedback without session history (#89874). Codex — image-generation model selector (#43965), expanded model access (Astra on Linux #42868, custom providers #44378), experimental voice conversations (#44331).

---

## 4. Differentiation Analysis

**Feature focus**
- **Claude Code:** governance and operational control. `maxEffortLevel` works as an **org/team-side ceiling across every provider (Bedrock, Vertex, Foundry)** — an enterprise administrative primitive, not a user preference. Adjacent work (mods API renames, telemetry hardening ensuring third-party providers send nothing, `sec-default`/`diff`/`telemetry` plugin modules) points at a plugin/extension ecosystem being formalized under policy.
- **Codex:** capability breadth and session mechanics. Model-catalog expansion (GPT-6-Astra, Bedrock), worktree-based isolated/forked sessions, MCP protocol-version awareness, voice as an experimental flag. Day-one transcripts for #44363/#44386 show the community stress-testing new surfaces immediately.

**Target users**
- **Claude Code:** teams and organizations standardizing on a CLI across providers, plugin/agent authors, VS Code users, and Desktop/Cowork (incl. Windows sandbox) operators. Pain points skew toward **entitlement, quotas, and multi-session credential correctness** — the concerns of paying orgs.
- **Codex:** individual developers on Plus/Pro tiers, TUI-centric users, Windows desktop users, and MCP/hosted-app integrators. Pain points skew toward **model capacity, local state durability, and platform bugs**.

**Technical approach**
- **Claude Code** addresses problems through **configuration surfaces** — settings, per-model overrides, CLI flags,

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights — as of 2026-09-10

**Data caveat:** PR comment counts are recorded as `undefined` in the provided export. The PR ranking below uses the source’s comment-sorted order as a proxy for attention/discussion volume. Issue comment counts are available and used directly.

## 1. Top Skills Ranking

| Rank | Skill / PR | Functionality | Discussion Highlight | Status |
|---|---|---|---|---|
| 1 | **[skill-creator eval fix — PR #1298](https://github.com/anthropics/skills/pull/1298)** | Fixes `run_eval.py` reporting `recall=0%` for all skill descriptions; also fixes Windows stream reading, trigger detection, and parallel workers. | Tied to [Issue #556](https://github.com/anthropics/skills/issues/556), with 10+ independent reproductions. The description-optimization loop is effectively optimizing against noise. | Open |
| 2 | **[document-typography skill — PR #514](https://github.com/anthropics/skills/pull/514)** | Adds typographic quality control for generated documents: orphan word wrap, widow paragraphs, numbering misalignment. | Argues these issues affect every Claude-generated document, even when users do not explicitly ask for typographic quality. | Open |
| 3 | **[scnet-hpc skill — PR #1615](https://github.com/anthropics/skills/pull/1615)** | Adds profile-based SSH and Slurm workflows for operating SCNet HPC clusters. | Covers connection, partitions,

---

# Claude Code Community Digest — 2026-09-10

Source: [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)

---

## 1. Today's Highlights

- **v2.1.267 ships effort-level governance**: a new `maxEffortLevel` cap (global or per-model) plus `--system-prompt-snapshot off` for fresh system prompts per request — a direct answer to long-running cost/effort complaints (e.g. [#92436](https://github.com/anthropics/claude-code/issues/92436)).
- **Windows Cowork is the dominant stability story**: a KB5124008 regression breaks all Plan9 shares ([#92984](https://github.com/anthropics/claude-code/issues/92984)), sandbox mounting fails ([#92977](https://github.com/anthropics/claude-code/issues/92977)), sessions hang after the first message ([#92921](https://github.com/anthropics/claude-code/issues/92921)), and VM runtime downloads never verify ([#93238](https://github.com/anthropics/claude-code/issues/93238)).
- **Cost and quota confusion is escalating**: multiple reports of 5-hour limits hit within minutes and "monthly" spend limits behaving as daily ([#93068](https://github.com/anthropics/claude-code/issues/93068), [#93100](https://github.com/anthropics/claude-code/issues/93100), [#93243](https://github.com/anthropics/claude-code/issues/93243)).

---

## 2. Releases

### v2.1.267
- **`maxEffortLevel` setting** — configurable at the top level or per model under `modelSettings`. Caps the reasoning effort level on **every provider, including Bedrock, Vertex, and Foundry**. Users may still explicitly select a lower level, so this acts as an org/team-side ceiling rather than a hard lock.
- **`--system-prompt-snapshot off`** — renders the system prompt fresh on every request instead of using a cached snapshot. Useful for prompt experimentation and for workflows where dynamic context must not be frozen at session start.

No other releases in the last 24h.

---

## 3. Hot Issues

1. **[#85891](https://github.com/anthropics/claude-code/issues/85891) — Windows 11 Desktop window is always-on-top, no way to disable** (OPEN, 93 comments, 👍 225)
   The single highest-engagement thread in the dataset. The window stays drawn above focused apps with no in-app toggle; explicitly framed as the Windows counterpart to #66516. Volume of reaction suggests this is a daily workflow blocker, not a cosmetic nit.

2. **[#92984](https://github.com/anthropics/claude-code/issues/92984) — Cowork: all Plan9 shares fail after Windows KB5124008** (OPEN, 32 comments, 👍 15)
   `Plan9 mount failed: invalid argument` across every share; **uninstalling the KB fixes it**. A clean external-regression signature with a reproducible bisect — high-signal for triage.

3. **[#27957](https://github.com/anthropics/claude-code/issues/27957) — Disable "Command contains quoted characters in flag names" warning** (OPEN, 27 comments, 👍 74)
   Fires on completely ordinary commands like `git commit -m "message"`. Long-lived (open since February) and highly upvoted — permission-prompt fatigue in its purest form.

4. **[#34196](https://github.com/anthropics/claude-code/issues/34196) — VS Code extension: font size setting for chat panel** (OPEN, 14 comments, 👍 87)
   Highest 👍-to-comment ratio here: the chat panel uses a smaller font than the editor with no way to change it. Accessibility/ergonomics gap in the most-used IDE surface.

5. **[#44380](https://github.com/anthropics/claude-code/issues/44380) — Channel messages don't wake idle sessions (`--channels` plugin)** (OPEN, 13 comments, 👍 6)
   Inbound Telegram messages render in the terminal but don't interrupt an idle REPL — the session waits on keyboard input. Breaks the core promise of the channels plugin for event-driven workflows.

6. **[#29415](https://github.com/anthropics/claude-code/issues/29415) — GitHub connector missing from `/mcp` despite appearing in settings** (OPEN, 12 comments, 👍 14)
   GitHub is connected at claude.ai but shows no state at all in the CLI, while 19 other connectors sync fine. Indicative of connector-state divergence between web and CLI.

7. **[#92977](https://github.com/anthropics/claude-code/issues/92977) — Cowork local sandbox not mounting after Desktop 1.49585.0.0** (OPEN, 9 comments, 👍 1)
   Marked duplicate but part of the same Windows Cowork failure cluster as #92984 — evidence that the regression spans multiple subsystems, not just Plan9.

8. **[#88583](https://github.com/anthropics/claude-code/issues/88583) — `claudeAiOauth` wiped from Keychain by concurrent Desktop session race** (OPEN, 7 comments, 👍 3)
   Concurrent Desktop sessions racing the **single-use refresh token** cause the winner's rotated credential to be clobbered (`expiresAt:0`). The author explicitly distinguishes this from prior corruption reports by identifying the writer — a strong root-cause writeup.

9. **[#92007](https://github.com/anthropics/claude-code/issues/92007) — `/model opusplan` fails with "Unsupported model"** (OPEN, 4 comments, 👍 7)
   Worked for months, broke on 2026-09-04 (v2.1.260). Regression in model routing affecting a documented alias.

10. **[#93068](https://github.com/anthropics/claude-code/issues/93068) — 5-hour reset limits hit after minutes of use** (OPEN, 1 comment)
    Representative of a same-day cluster with [#93100](https://github.com/anthropics/claude-code/issues/93100) and [#93243](https://github.com/anthropics/claude-code/issues/93243) ("monthly" spend limit that is actually daily). Low engine engagement so far, but high emotional intensity from paying users.

*Also notable:* [#93231](https://github.com/anthropics/claude-code/issues/93231) — VS Code window close leaves the git worktree lock naming a dead PID, and no later session reaps it.

---

## 4. Key PR Progress

> Only **3 PRs** were updated in the last 24h — a quiet PR window relative to issue volume.

1. **[#93244](https://github.com/anthropics/claude-code/pull/93244) — mods: API renames and telemetry fixes** (OPEN, poteat)
   Follows the plugin API naming pass (`isFocused`, `tool`) in the diff module. Tightens telemetry: rows emitted sequentially, every analytics switch read per row, and **third-party providers send nothing**. Directly relevant to anyone running the mods/hooks preview.

2. **[#89404](https://github.com/anthropics/claude-code/pull/89404) — validate-agent.sh: don't abort at first warning, stop false-flagging valid agents** (OPEN, bcherny)
   Fixes [#83803](https://github.com/anthropics/claude-code/issues/83803). Three `set -euo pipefail` interactions were causing the plugin-dev skill's validator to fail on plugin-dev's own agent files — `((warning_count++))` returning non-zero aborts the script under `set -e`. Improves plugin/agent authoring DX.

3. **[#93215](https://github.com/anthropics/claude-code/pull/93215) — Add mods: sec-default, diff and telemetry** (CLOSED, poteat)
   The three built-in hooks-module plugins published as source: `sec-default` (an org's default outermost plugin), `diff` (`/diff`), and `telemetry` (`$.telemetry`). Gated behind function hooks being enabled. Closed same-day, superseded by #93244's follow-up work.

---

## 5. Feature Request Trends

Distilled from all 50 issues updated in the last 24h:

- **IDE/editor ergonomics and observability** — chat panel font size ([#34196](https://github.com/anthropics/claude-code/issues/34196)), and exposing a session's **context window + cost to local tools** when no status line is present (VS Code extension / SDK, [#92853](https://github.com/anthropics/claude-code/issues/92853)).
- **Reducing permission and confirmation friction** — configurable suppression of noisy warnings ([#27957](https://github.com/anthropics/claude-code/issues/27957)); site permissions ignored by the built-in Desktop browser ([#91495](https://github.com/anthropics/claude-code/issues/91495)).
- **Cross-device / remote session control** — start a *new* remote session from mobile with a device picker ([#91815](https://github.com/anthropics/claude-code/issues/91815)), and list/reopen a routine's session after the notification is gone ([#76841](https://github.com/anthropics/claude-code/issues/76841)).
- **Desktop app configurability** — simultaneous spellchecker languages ([#88502](https://github.com/anthropics/claude-code/issues/88502)).
- **Privacy-preserving feedback paths** — send feedback without attaching session history ([#89874](https://github.com/anthropics/claude-code/issues/89874)).

---

## 6. Developer Pain Points

1. **Windows Cowork / Desktop regression cluster (highest urgency).** KB5124008 breaks Plan9 mounts ([#92984](https://github.com/anthropics/claude-code/issues/92984)); sandbox stops mounting after Desktop 1.49585.0.0 ([#92977](https://github.com/anthropics/claude-code/issues/92977)); sessions hang after the first message ([#92921](https://github.com/anthropics/claude-code/issues/92921)); VM runtime download leaves a `.partial` and never verifies, surviving clean reinstall ([#93238](https://github.com/anthropics/claude-code/issues/93238)). Also [#93246](https://github.com/anthropics/claude-code/issues/93246) — browser pane can't complete HTTP Basic Auth.

2. **Credential and OAuth races.** `claudeAiOauth` blanked in Keychain by concurrent Desktop sessions racing single-use refresh tokens ([#88583](https://github.com/anthropics/claude-code/issues/88583)); the same class of bug in remote MCP OAuth against IdPs with single-use rotation ([#91641](https://github.com/anthropics/claude-code/issues/91641)). A recurring architectural vulnerability, not isolated incidents.

3. **Quota and cost transparency.** Users report 5-hour windows exhausted in minutes and "monthly" limits behaving daily ([#93068](https://github.com/anthropics/claude-code/issues/93068), [#93100](https://github.com/anthropics/claude-code/issues/93100), [#93243](https://github.com/anthropics/claude-code/issues/93243)). Reinforced by silent cost surprises: subagents defaulting to a different model than the session's ([#80902](https://github.com/anthropics/claude-code/issues/80902)) and the `code-review` skill ignoring `--level low` and running the full high-effort pipeline ([#92436](https://github.com/anthropics/claude-code/issues/92436)). **v2.1.267's `maxEffortLevel` lands squarely on this theme.**

4. **Permission-prompt fatigue.** Routine commands triggering quoted-character confirmations ([#27957](https://github.com/anthropics/claude-code/issues/27957)) and Desktop site-permission settings being ignored by the built-in browser ([#91495](https://github.com/anthropics/claude-code/issues/91495)).

5. **Plugin/agent authoring fragility.** Four shipped plugin agents fail YAML frontmatter parsing and load as placeholders or not at all ([#91871](https://github.com/anthropics/claude-code/issues/91871)); validator scripts false-flag valid agents ([#83803](https://github.com/anthropics/claude-code/issues/83803), fixed by [#89404](https://github.com/anthropics/claude-code/pull/89404)).

6. **Session lifecycle and state leakage.** Git worktree locks held by dead PIDs after VS Code window closes ([#93231](https://github.com/anthropics/claude-code/issues/93231)); background-session git rules with no precedence clause blocking merges the repo's own `CLAUDE.md` requires ([#87996](https://github.com/anthropics/claude-code/issues/87996)).

7. **Access/entitlement dead ends.** Pro subscription blocked with "organization

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-09-10

Source: [github.com/openai/codex](https://github.com/openai/codex)

---

## 1. Today's Highlights

Codex cut **rust-v0.154.0**, bringing **GPT-6-Astra** into the model picker and Amazon Bedrock catalogs plus experimental **worktree support** (`--worktree` / `/worktree`) for isolated checkouts and forked sessions. Meanwhile, the community's attention is concentrated on two fronts: a rising wave of **session/rollout durability bugs** on desktop (compaction destroying transcripts, frozen history after resume) and persistent **"Selected model is at capacity"** errors now hitting GPT-6-Astra users. Windows remains the single largest source of open bug reports, especially around Computer Use and app launch/runtime staging.

---

## 2. Releases

**rust-v0.154.0** (stable) — [release notes](https://github.com/openai/codex/releases)
- **GPT-6-Astra** is now selectable in the model picker and available in Amazon Bedrock catalogs (#42879, #42619).
- **Experimental worktree support**: create isolated checkouts for new or forked sessions via `--worktree` or `/worktree`, with browsing and resuming of existing worktrees (#42652, #43069, #43120).

**Alpha channel** — `0.154.0-alpha.6.1`, `0.154.0-alpha.10.2`, `0.154.0-alpha.11` shipped with no detailed notes, indicating the usual rapid alpha cadence ahead of the next stable cut. Alpha users should expect churn in the worktree and model-picker surfaces.

---

## 3. Hot Issues

1. **[#25178](https://github.com/openai/codex/issues/25178)** — *Windows Computer Use screenshot fails (`SetIsBorderRequired` 0x80004002, Win10 22H2)* — 54 comments, 👍23. The single most-discussed issue in the window; accessibility/interaction works but any screenshot request (`get_window_state`) fails before capture, making Computer Use effectively read-only.
2. **[#25271](https://github.com/openai/codex/issues/25271)** — *Computer Use cannot determine Chrome URL on Windows* — 35 comments, 👍9. Chrome tab/URL resolution fails even on `chrome://newtab/`, blocking browser-driven workflows on Windows.
3. **[#21653](https://github.com/openai/codex/issues/21653)** — *Support multi-line status line (TUI)* — 20 comments, **👍83 (top-voted item)**. Long status lines are truncated with no line-break support; strong sustained demand for TUI customization.
4. **[#44363](https://github.com/openai/codex/issues/44363)** — *Context compaction rewrites the stored rollout in place and permanently destroys the transcript* — New as of today, 👍0 but high severity. Reported on Desktop `26.903.61454` (macOS); potential irreversible conversation data loss.
5. **[#43142](https://github.com/openai/codex/issues/43142)** — *Windows: resume reuses two rollout ordinals after trailing `token_count` records, freezing desktop history* — 16 comments. Durable JSONL is intact but the paginated history projection stops advancing, so users see stale conversation state.
6. **[#43375](https://github.com/openai/codex/issues/43375)** — *Multiple GPT-5 / GPT-6 models return "Selected model is at capacity"* — 15 comments, 👍5. Corroborated same-day by **[#44382](https://github.com/openai/codex/issues/44382)** (CLI v0.154.0, Pro 20x, `gpt-6-astra ultra fast`), suggesting capacity is not model-specific.
7. **[#44386](https://github.com/openai/codex/issues/44386)** — *Desktop replays ~150k cached input per tool call and rapidly drains Plus usage* — New today; a cost/quota-correctness issue tied to tool-call context replay on Desktop `26.903.61454`.
8. **[#39897](https://github.com/openai/codex/issues/39897)** — *Deleted ChatGPT conversation remains in sidebar, cannot be removed (macOS)* — 20 comments, 👍4; see also **[#41399](https://github.com/openai/codex/issues/41399)** (👍14) and **[#41661](https://github.com/openai/codex/issues/41661)**. Server-side deletion does not propagate to the desktop sidebar.
9. **[#42501](https://github.com/openai/codex/issues/42501)** — *Windows app fails to launch UI when `cua_node` staging cannot copy `node_repl.exe`* — 14 comments. Processes start responsive but `MainWindowHandle` stays `0`; a packaging/install regression breaking app startup entirely.
10. **[#29079](https://github.com/openai/codex/issues/29079)** — *Windows Desktop leaves Node/MCP helper processes alive until memory pressure makes the PC unresponsive* — 9 comments, 👍4. Long-running resource-leak report implicating subagent/MCP/Node REPL lifecycles.

*Also worth watching:* **[#44378](https://github.com/openai/codex/issues/44378)** (duplicate `mcp__*` namespace hard-fails a thread), **[#41133](https://github.com/openai/codex/issues/41133)** (MCP shutdown can lose a rotated refresh token), **[#44384](https://github.com/openai/codex/issues/44384)** (Remote Control WebSocket 503 on Windows).

---

## 4. Key PR Progress

All items below merged/closed in the last 24h (mostly via `copyberry[bot]`).

1. **[#44350](https://github.com/openai/codex/pull/44350)** — *Add thread attachment operations with coordinated deletion.* Typed `ThreadStore` ops for idempotent attachment creation and paginated listing, preventing queued requests from referencing deleted threads.
2. **[#44349](https://github.com/openai/codex/pull/44349)** — *Distinguish forked sessions in session-start hooks.* Adds a `fork` session-start kind, so startup hooks stop re-firing for forked threads and inherited-history resumes correctly report `resume`.
3. **[#44346](https://github.com/openai/codex/pull/44346)** — *Support native verification in MCP tool continuations.* Routes MCP `2026-07-28` tool inputs through existing elicitation handling (RMCP's union excludes custom methods).
4. **[#44341](https://github.com/openai/codex/pull/44341)** — *Bind remote-control sessions to their authentication owner.* Prevents relay state and queued ops from leaking across account switches while preserving live connections on same-identity token refresh — relevant to the Remote Control failures above.
5. **[#44352](https://github.com/openai/codex/pull/44352)** — *Remove path-bearing fields from Guardian review analytics.* Replaces full permission profiles with network-only metadata and drops the `execve` `program` field; a privacy hardening change.
6. **[#44336](https://github.com/openai/codex/pull/44336)** — *Add bounded tool-result metadata to executed tool calls.* Size-limited, redacted `tool_result_metadata` snapshots with protection against deserialization from untrusted input.
7. **[#44332](https://github.com/openai/codex/pull/44332)** — *Persist disabled plugin IDs in thread settings.* `disabled_plugin_ids` now survives snapshots, turn contexts, and resume.
8. **[#44331](https://github.com/openai/codex/pull/44331)** — *Expose voice conversations in experimental features.* `realtime_conversation` is flagged experimental, disabled by default, surfaced as "Voice conversations" in `/experimental`.
9. **[#44327](https://github.com/openai/codex/pull/44327)** — *Prevent filesystem-root read denies in the Windows sandbox.* Validates effective `:root` read access before elevated setup; the elevated sandbox cannot safely deny root reads.
10. **[#44320](https://github.com/openai/codex/pull/44320)** — *Block goals after three empty automatic continuation turns.* Stops non-productive continuation loops by marking the goal `blocked`.

*Additional:* **[#44360](https://github.com/openai/codex/pull/44360)** (Escape returns focus to the composer), **[#44344](https://github.com/openai/codex/pull/44344)** (open tasks with Right-arrow from agents overview), **[#44359](https://github.com/openai/codex/pull/44359)** (report OAuth failures in MCP status snapshots), **[#44318](https://github.com/openai/codex/pull/44318)** (independent MCP protocol opt-in for hosted Codex Apps).

---

## 5. Feature Request Trends

- **TUI/UI customization**: multi-line status lines ([#21653](https://github.com/openai/codex/issues/21653), 👍83) is the clearest unmet ask; overlay/footer polish continues in PRs.
- **Image generation control**: expose the effective image model and a model selector for built-in `image_gen` ([#43965](https://github.com/openai/codex/issues/43965), 👍6); related failure reports in [#33379](https://github.com/openai/codex/issues/33379).
- **Cost/limit transparency**: restore a 5-hour limit or allow explicit Ultra budgets ([#34822](https://github.com/openai/codex/issues/34822)); users want to reason about consumption before a run.
- **Session portability & isolation**: worktree support landed and is being extended (fork/browse/resume), alongside requests for durable, non-destructive history.
- **Remote/connectivity parity**: Remote Control enrollment and relay reliability on Windows ([#44384](https://github.com/openai/codex/issues/44384)).
- **Expanded model access**: Astra on Linux reliably ([#42868](https://github.com/openai/codex/issues/42868)) and non-OpenAI/custom model providers ([#44378](https://github.com/openai/codex/issues/44378)).

---

## 6. Developer Pain Points

1. **Windows is the dominant failure surface.** Computer Use screenshots/URLs ([#25178](https://github.com/openai/codex/issues/25178), [#25271](https://github.com/openai/codex/issues/25271)), app start failure ([#42501](https://github.com/openai/codex/issues/42501)), process/memory leaks ([#29079](https://github.com/openai/codex/issues/29079)), Chrome control via `nodeRepl.fetch` ([#44135](https://github.com/openai/codex/issues/44383)), Remote Control 503s ([#44384](https://github.com/openai/codex/issues/44384)), and reasoning-effort resets ([#42435](https://github.com/openai/codex/issues/42435)).
2. **Session state durability is fragile.** Compaction rewrites rollouts in place and can destroy transcripts ([#44363](https://github.com/openai/codex/issues/44363), [#42311](https://github.com/openai/codex/issues/42311)); resume can freeze history via rollout-ordinal reuse ([#43142](https://github.com/openai/codex/issues/43142)); migrated threads show empty history ([#44033](https://github.com/openai/codex/issues/44033)).
3. **Capacity errors are blocking paid tiers.** "Selected model is at capacity" recurs across GPT-5/GPT-6 lines, including Ultra Fast on Pro 20x ([#43375](https://github.com/openai/codex/issues/43375), [#44382](https://github.com/openai/codex/issues/44382)).
4. **Quota/token accounting surprises.** Cached-input replay per tool call burning Plus usage ([#44386](https://github.com/openai/codex/issues/44386)) compounds existing frustration over opaque limits.
5. **MCP/plugin lifecycle correctness.** Lost rotated refresh tokens on shutdown ([#41133](https://github.com/openai/codex/issues/41133)), duplicate `mcp__*` namespaces hard-failing threads ([#44378](https://github.com/openai/codex/issues/44378)), and stale OAuth status reporting (addressed in [#44359](https://github.com/openai/codex/pull/44359)).
6. **Over-aggressive safety filters.** False-positive `content_filter`/safety-check interruptions on legitimate work, including remote compaction of literary text ([#43969](https://github.com/openai/codex/issues/43969)) and a JPEG XL validation probe ([#44380](https://github.com/openai/codex/issues/44380)).
7. **Desktop/cloud sync inconsistency.** Server-deleted conversations persist in desktop Recents/sidebar with

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*