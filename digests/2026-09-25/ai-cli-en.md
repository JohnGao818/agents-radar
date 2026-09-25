# AI CLI Tools Community Digest 2026-09-25

> Generated: 2026-09-25 03:11 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool AI CLI Digest Comparison — 2026-09-25

**Data caveat:** Only **Claude Code** has a usable digest today. The **OpenAI Codex** digest failed summary generation, so quantitative cross-tool comparison is not possible. The report below treats Claude Code as the observed baseline and marks Codex as unavailable rather than inferring missing data.

## 1. Ecosystem Overview

The AI CLI tooling landscape is in a high-cadence patch phase: releases are shipping frequently, but operational reliability—especially desktop/cloud bridges, auto-update behavior, and session continuity—is the gating factor for adoption. Claude Code’s community is dominated by device-bridge/Cowork failures, compaction-related memory loss, cost predictability, and permission-model coherence. Feature requests are converging on secretless credential handling, durable context, and inspectable trust surfaces. Because Codex data is missing, today’s digest shows a one-sided ecosystem snapshot: strong Claude Code activity, but no verified Codex momentum or comparison.

## 2. Activity Comparison

| Tool | Issues count | PR count | Release status | Notes |
|---|---:|---:|---|---|
| **Claude Code** | 14 highlighted (10 hot + 4 also notable); total not reported | 8 updated: 1 open, 7 closed | **v2.1.282 shipped**; Linux TUI regression #96931 | Top thread #45937 has 42 comments, 👍16. Dominant theme: desktop/Cowork bridge failures across Windows/macOS. |
| **OpenAI Codex** | N/A — summary failed | N/A — summary failed | N/A — summary failed | No usable issue/PR/release data today. |

## 3. Shared Feature Directions

No cross-tool overlap can be confirmed today because Codex data is missing. Within Claude Code, the following requirements appear repeatedly and are strong candidates for ecosystem-wide trends:

- **Credential isolation for agentic dev/QA** — broker-based login where the model triggers auth but never sees secrets: #88165, #96949.
- **Context and memory durability** — instruction files not reloaded after compaction, prose loss/mis-rendering across compaction boundaries: #96422, #96950, #96947.
- **Cost predictability** — visible token spend, hidden cache invalidation, `totalTokensReminder` cache floor: #96565, #90018.
- **Trust and permission coherence** — desktop/CLI trust deadlock, `autoMode.allow` overridden by classifier, Auto-mode banner in Manual: #96928, #96943, #96954.
- **Remote/MCP session continuity** — OAuth refresh tokens for MCP, remote session index durability: #95113, #63025.

**Tools affected:** Claude Code is confirmed for all five. Codex is unverified.

## 4. Differentiation Analysis

**Claude Code** differentiates around a broad integrated surface: CLI + desktop/Cowork + cloud sessions + team workspaces + SSH remote + MCP. Its technical approach includes mod/plugin layers (`diff`, `telemetry`, `agents-md`), telemetry hooks, startup/config visibility, and settings such as `maxProseWidth`. Target users span individual developers through paid Team workspaces, with growing emphasis on remote and multi-server MCP workflows.

**OpenAI Codex** cannot be positioned today because the digest failed. There is no data on feature focus, target users, or technical approach.

## 5. Community Momentum & Maturity

**Claude Code** shows high momentum but visible reliability strain:

- Daily release cadence: v2.1.282 shipped.
- Multiple independent bridge issues filed within ~24 hours: #96911, #96918, #96919, #96887, plus long-running #45937.
- High-engagement issue: #45937 at 42 comments.
- PR traffic is low: 8 updated, 7 closed, 1 open, all but one from a single contributor, suggesting maintainer/plugin-driven rather than broad community PR flow.
- Maturity gap: auto-update regressions (#96931, #94687) and opaque bridge failures survive reboot, re-login, device removal, and app update.

**OpenAI Codex** cannot be ranked on momentum or maturity from this snapshot.

## 6. Trend Signals

1. **Auto-update is a reliability risk.** Binary replacement breaks TCC grants on macOS and introduces Linux TUI input freezes. Projects need canary releases, rollback paths, and session-safe updates.
2. **Cloud/device bridges need self-service diagnostics.** WebSocket handshakes open but never authenticate, leaving users with no recovery path. Health endpoints, bridge state visibility, and clear auth diagnostics are needed.
3. **Context durability is a trust issue.** Compaction can silently drop instructions or memory files. Compaction-aware rehydration and user-visible reload signals are becoming table stakes.
4. **Cost observability is a feature, not a billing detail.** Cache floors and hidden token growth drive demand for attributable per-session spend.
5. **Permission models must be coherent and inspectable.** Agentic auto-mode cannot silently override explicit allowlists or create desktop/CLI trust deadlocks.
6. **Credential brokering is emerging as a core primitive.** The model should trigger authenticated workflows without ever seeing credentials.
7. **Remote/MCP continuity is maturing.** OAuth refresh tokens and durable remote session indexes are needed as SSH-remote and multi-server MCP usage grows.

**Bottom line for technical decision-makers:** Claude Code is iterating quickly and exposing real production pain in bridge reliability, update safety, context durability, and permission coherence. Codex comparison requires a successful digest; today’s actionable signals are Claude Code’s release-window regressions and the ecosystem-wide push toward durable, observable, secret-safe agentic workflows.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills — Community Highlights Report
**Source:** github.com/anthropics/skills | **Data as of:** 2026-09-25

> **Data note:** The PR dataset reports `Comments: undefined` for all 50 PRs, so PR ranking below uses *attention proxies* — update recency, centrality to the repo's core skills, and the presence of long-running back-and-forth (e.g., older PRs still being touched in September). Issue comment counts are available and used directly.

---

## 1. Top Skills Ranking (PRs by attention)

### 1. `skill-creator` — trigger eval isolation + Windows/runtime failure handling
**PR #1298** · OPEN · Author: MartinCajiao · Created 2026-06-10 · **Updated 2026-09-16**
- **Function:** Fixes the meta-skill that generates other Skills. Per-worker command probes compete, `select()` on subprocess pipes breaks on Windows, and unrelated tools abort the scan; runtime failures were being silently scored as "non-triggers," which *passed* negative examples and produced misleading optimization results.
- **Why it matters:** This is the highest-leverage PR in the set — a faulty eval harness corrupts every downstream Skill's quality score.
- **Status:** Open, still active after 3+ months (review friction likely).
- 🔗 https://github.com/anthropics/skills/pull/1298

### 2. `mcp-builder` — MCP v2 import rename + custom HTTP headers
**PR #1742** · OPEN · Author: Kuldeeep18 · Created 2026-09-08 · **Updated 2026-09-19**
- **Function:** In `mcp>=2.0.0`, `streamablehttp_client` → `streamable_http_client`, and custom headers now require `create_mcp_http_client` / `http_client` instead of a direct kwarg. Without this, `skills/mcp-builder/scripts/connections.py` is broken against the current SDK.
- **Highlights:** Closes #1668; a hard compatibility break with a vendor SDK upgrade — a recurring failure class for Skill scripts.
- **Status:** Open, latest-revision active.
- 🔗 https://github.com/anthropics/skills/pull/1742

### 3. `docx` — LibreOffice timeout reported as error + output verification
**PR #1792** · OPEN · Author: TINGyu123644 · Created 2026-09-19 · **Updated 2026-09-25** *(freshest activity in the dataset)*
- **Function:** `accept_changes.py` now surfaces a soffice timeout as an Error instead of false success, and only claims success after verifying the output DOCX no longer contains `w:ins` / `w:del` / `w:moveFrom` / `w:moveTo` in `word/*.xml`.
- **Highlights:** Part of a cluster of correctness fixes to the official document Skills (see also #1790, #1734).
- **Status:** Open, most recently touched PR.
- 🔗 https://github.com/anthropics/skills/pull/1792

### 4. `pyxel` — retro game development and verification
**PR #525** · OPEN · Author: kitao · Created 2026-03-05 · **Updated 2026-09-22**
- **Function:** Creation, debugging, and verification of retro Python games: guided implementation, headless input-driven runs, direct frame inspection, and task-specific state checks, with separate references for Pyxel behavior and release evidence.
- **Highlights:** A six-month-old PR still receiving updates — a strong signal of sustained author investment and reviewer interest in "verifiable" Skills with objective pass/fail evidence.
- **Status:** Open, long-running.
- 🔗 https://github.com/anthropics/skills/pull/525

### 5. `awt` (AI Watch Tester) — AI-powered E2E testing
**PR #822** · OPEN · Author: ksgisang · Created 2026-03-31 · **Updated 2026-09-19**
- **Function:** Gives Claude vision + browser control to run E2E tests with zero-code test generation from a target app.
- **Highlights:** Ties directly to the most-repeated community ask — automated test generation (cf. PR #723 `testing-patterns`).
- **Status:** Open, actively maintained through September.
- 🔗 https://github.com/anthropics/skills/pull/822

### 6. `md2video-audio` — Markdown → narrated MP4
**PR #1703** · OPEN · Author: 70v-Yoyo · Created 2026-09-01 · **Updated 2026-09-15**
- **Function:** Zero-cost Skill compiling Markdown into MP4 videos with human-like voiceover (Marp slides + TTS pipeline).
- **Highlights:** Representative of the new "content-production" wave of Skill submissions (documents → media).
- **Status:** Open, new submission.
- 🔗 https://github.com/anthropics/skills/pull/1703

### 7. `proofcore-contract-auditor` — smart-contract notarization
**PR #1771** · OPEN · Author: ProofCore-Protocol · Created 2026-09-15 · **Updated 2026-09-16**
- **Function:** Agent Skill for Web3 developers performing automated static analysis of Solidity and Rust contracts and anchoring cryptographic audit proofs to the TON Blockchain via a zero-storage Merkle protocol.
- **Highlights:** A vendor-backed Skill proposal — raises the namespace-trust question that dominates Issue #492.
- **Status:** Open, newly filed.
- 🔗 https://github.com/anthropics/skills/pull/1771

### 8. `notion-spec-to-implementation` + `quantitative-resume-auditor`
**PR #1245** · OPEN · Author: mrdesouzaphd-cmyk · Created 2026-06-02 · **Updated 2026-09-24**
- **Function:** Converts product/tech specs into concrete Notion tasks with acceptance criteria and progress tracking; second Skill audits résumés quantitatively.
- **Highlights:** Bundling two unrelated Skills in one PR is a recurring review blocker in this repo.
- **Status:** Open, still iterating.
- 🔗 https://github.com/anthropics/skills/pull/1245

**Also notable:** `document-typography` (#514, orphan/widow/misalignment QC), `blast-radius` (#1776, pre-destructive-write checklist), `skill-quality-analyzer` + `skill-security-analyzer` (#83, meta-skills for marketplace), and Lubrsy706's PDF/DOCX/skill-creator fix series (#538, #539, #541).

---

## 2. Community Demand Trends (from Issues)

| Demand direction | Evidence | What the community wants |
|---|---|---|
| **Skill trust & namespace security** | #492 (43 comments, 2👍) | Community Skills shipped under `anthropic/` impersonate official ones; users grant elevated permissions by mistake. Demand for signed/publisher-scoped namespaces. |
| **Evaluation & trigger reliability** | #556 (12 comments, 7👍), #1390 (4 comments) | `run_eval.py` shows a **0% trigger rate** across all queries; `mcp-builder/evaluation.py` scores 0/N against every real MCP server due to `TextContent` not being JSON-serializable. Tooling that *measures* Skills is the weakest link. |
| **Context-window / token efficiency** | #1487, #202, #1329 | The `claude-api` Skill injects ~156k tokens in a single tool call, exhausting context; skill-creator reads like docs rather than operational instructions; a symbolic "compact-memory" notation is proposed. Token cost is now a first-class Skill quality metric. |
| **Enterprise sharing & governance** | #228 (16 comments, 8👍), #189 (6 comments, 9👍), #412, #1175, #1385 | Org-wide Skill libraries and share links instead of Slack + manual upload; `document-skills` and `example-skills` currently install identical content, causing duplicates. Also: access-control logic inside SKILL.md, agent governance patterns, and a three-gate reasoning quality pipeline. |
| **Platform portability & interoperability** | #29, #16 | Running Skills on AWS Bedrock; exposing Skills as MCPs with typed APIs (`generateAlgorithmArt({ prompt })`). |
| **Build/toolchain robustness** | #1362, #62 | `web-artifacts-builder` fails on pnpm ≥10.1 (ignored builds) with stale assets and non-inlined fonts; users report skills silently disappearing. |

**Emerging new-Skill directions:** E2E/agentic test generation, destructive-operation safety checklists, spec→task→implementation automation, document typography/formatting QC, media generation (video/audio) from Markdown, and meta-skills that audit other Skills.

---

## 3. High-Potential Pending Skills (open, actively updated)

| PR | Skill | Last update | Why it may land soon |
|---|---|---|---|
| [#1792](https://github.com/anthropics/skills/pull/1792) | docx timeout/verification fix | 2026-09-25 | Small, surgical, verifiable; part of a coherent fix cluster (#1790) by the same author. |
| [#1245](https://github.com/anthropics/skills/pull/1245) | notion-spec-to-implementation | 2026-09-24 | Highest-utility workflow automation; needs de-bundling from the résumé Skill. |
| [#525](https://github.com/anthropics/skills/pull/525) | pyxel | 2026-09-22 | Six months of sustained author iteration; strong "verifiable Skill" narrative. |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns | 2026-09-21 | Matches the #1 requested capability (test generation); pure-knowledge Skill, low integration risk. |
| [#1742](https://github.com/anthropics/skills/pull/1742) | mcp-builder MCP v2 fix | 2026-09-19 | Restores a *broken official* Skill — high review priority. |
| [#822](https://github.com/anthropics/skills/pull/822) | awt (E2E testing) | 2026-09-19 | External open-source tool with browser/vision capability; may need dependency review. |
| [#1776](https://github.com/anthropics/skills/pull/1776) | blast-radius | 2026-09-18 | Novel safety niche (bulk/destructive writes); small and self-contained. |
| [#1298](https://github.com/anthropics/skills/pull/1298) | skill-creator eval fixes | 2026-09-16 | Fixes the evaluation foundation; most impactful but also most complex. |

---

## 4. Skills Ecosystem Insight

**The community's demand is concentrated less on *more* Skills and more on *trustworthy* Skills — reliable triggering/evaluation, honest success reporting, namespace authenticity, and token-cheap context — with new-Skill proposals clustering around test generation, destructive-write safety, and spec-to-implementation automation.**

---

# Claude Code Community Digest — 2026-09-25

## 1. Today's Highlights

- **v2.1.282 shipped** with a new `maxProseWidth` setting for wide terminals and new telemetry-visibility notices in startup, `/status`, and `claude doctor`.
- **Desktop/Cowork device-bridge connectivity is the dominant story today**: multiple independent reports on Windows (#96911, #96918) and macOS (#96919, #96887) describe WebSocket handshakes never being acknowledged, leaving linked computers "offline" and cloud sessions unable to start.
- **A fresh 2.1.282 regression is already circulating**: Linux TUI users report the input box silently stops accepting keystrokes within 0–90 seconds (#96931), while the long-running top issue #45937 (42 comments) remains the highest-engagement thread.

---

## 2. Releases

### v2.1.282
- Added a **`maxProseWidth`** setting that caps Claude's prose width in wide terminals while **tables and code blocks keep full width** — a targeted fix for readability on ultrawide/large monitors.
- Added a **startup notice**, plus entries in `/status` and `claude doctor`, listing **telemetry variables in a project's settings files that were ignored** — improving discoverability of silently-ignored config.
- ⚠️ Regression watch: #96931 reports the input box stops accepting keystrokes in 2.1.282 (2.1.281 unaffected).

---

## 3. Hot Issues

1. **[#45937](https://github.com/anthropics/claude-code/issues/45937) — Dispatch main conversation permanently "offline" while Cowork tasks work** (42 comments, 👍16)
   The highest-traffic open issue. Individual Cowork tasks succeed but the main Dispatch thread shows "This desktop appears offline" even when prompted from the desktop itself — pointing at a thread-level routing/registration bug rather than a general connectivity failure.

2. **[#96911](https://github.com/anthropics/claude-code/issues/96911) — Windows device bridge handshake never acknowledged (~18 min), survives reboot + update** (10 comments)
   WebSocket to `wss://bridge.claudeusercontent.com` opens and sends a connect frame, but no `authenticated` reply arrives; every attempt ends in handshake timeout before self-recovery. Reboot and app update did not help — consistent with a server-side bridge state issue.

3. **[#96918](https://github.com/anthropics/claude-code/issues/96918) — Windows: linked computer stuck "Asleep or app closed"; cloud sessions/tasks fail** (7 comments)
   Same symptom class as #96911 but with a permanent failure mode: cloud sessions and scheduled tasks fail with "not connected to the bridge" through reboot, re-login, device removal, and app update.

4. **[#96919](https://github.com/anthropics/claude-code/issues/96919) — macOS Cowork bridge handshake regression after Desktop 2.9939.2**
   Filed within hours of #96887, this confirms the regression is not Windows-only. Since 2026-09-24 20:14 ET the Mac device bridge fails on every attempt — a clear temporal correlation with the 2.9939.2 rollout.

5. **[#96887](https://github.com/anthropics/claude-code/issues/96887) — macOS Cowork: "Couldn't link this session to a computer" — Secure Enclave sign fails with OSStatus -25308**
   Includes a repro. `td-v2` attestation mint unavailable, blocking **every cloud Cowork session on a Team workspace** — the most severe consequence of the bridge regression, since it affects paid team workflows.

6. **[#96931](https://github.com/anthropics/claude-code/issues/96931) — Linux TUI: input box stops accepting keystrokes in 2.1.282** (has repro)
   Session goes unresponsive to keyboard input mid-typing, no redraw, Ctrl-C inert, process still alive. Directly tied to today's release and the top reason to hold off upgrading on Linux.

7. **[#63025](https://github.com/anthropics/claude-code/issues/63025) — SSH Remote: `projects` field in remote `~/.claude.json` nulled after desktop restart** (👍5)
   Marked `data-loss`. Transcript `.jsonl` files survive, but the UI shows "No messages yet" for every session — a silent index corruption that looks like lost history to users.

8. **[#90018](https://github.com/anthropics/claude-code/issues/90018) — `totalTokensReminder` causes repeatable prompt-cache floor in tool loops** (has repro)
   Disabling the reminder restores incremental cache hits. A concrete, reproducible cost regression in long agentic tool loops — exactly the workload Claude Code is optimized for.

9. **[#92178](https://github.com/anthropics/claude-code/issues/92178) — Auto mode steers the model away from Read/Edit/Write toward Bash; TodoWrite unavailable** (👍8)
   Under `defaultMode: auto`, tool selection degrades and TodoWrite disappears. High agreement suggests this is a broad workflow-quality regression, not a niche config issue.

10. **[#96422](https://github.com/anthropics/claude-code/issues/96422) — Custom instructions silently lost across context compaction**
    Project instruction/memory files are not re-loaded after a lossy summarization boundary, so the model silently stops honoring rules with no user signal — a correctness and trust problem for `CLAUDE.md`-heavy projects.

*Also notable:* [#95113](https://github.com/anthropics/claude-code/issues/95113) MCP OAuth credentials persisted with `expiresAt: 0` and no `refreshToken`, forcing re-auth every session; [#94687](https://github.com/anthropics/claude-code/issues/94687) macOS voice dictation dies after the auto-updater replaces `claude.exe` (TCC denies the new PID); [#96943](https://github.com/anthropics/claude-code/issues/96943) auto-mode classifier inconsistently blocks deploys explicitly allowed in `autoMode.allow`; [#96928](https://github.com/anthropics/claude-code/issues/96928) desktop/CLI trust deadlock for worktrees of trusted repos.

---

## 4. Key PR Progress

PR traffic remains low (**8 total updated**, all but one closed, all authored by a single contributor working on the `diff`, `telemetry`, and `agents-md` mods/plugins).

1. **[#96953](https://github.com/anthropics/claude-code/pull/96953) — diff: focus hook answers to either name the engine stamps** *(OPEN)*
   The `ui.focus` matcher hard-coded `Names.PLUGIN_NAME` (`'diff'`), but builds registering the mod as `cc-plugin-diff` stamp elements under that name. Makes the hook tolerant of both identifiers.

2. **[#96487](https://github.com/anthropics/claude-code/pull/96487) — telemetry: rows carry engine version, base version, and build time** *(CLOSED)*
   Rows from external builds previously arrived without version data. Now reads `$.session.version()` → `{ version, base?, builtAt? }` (available from 2.1.281), alongside other environment probes.

3. **[#96917](https://github.com/anthropics/claude-code/pull/96917) — telemetry: `log` and `mark` moved into gated event hooks** *(CLOSED)*
   Replaces the two methods of the `engine.create`-injected noun with `telemetry.log` / `telemetry.mark` hooks that validate the entry, queue the row, and return `{ value }`.

4. **[#96930](https://github.com/anthropics/claude-code/pull/96930) — telemetry/agents-md: test plugins hook and call the collector stream by name** *(CLOSED, tests only)*
   Test-only change: mock plugins now name the single stream they may touch (`on('telemetry.log', { to: 'collector' })`), tightening the contract tests around plugin isolation.

5. **[#96364](https://github.com/anthropics/claude-code/pull/96364) — agents-md: auto-paginated Read of a nested `AGENTS.md` no longer counts as delivering it** *(CLOSED)*
   Fixes a real correctness gap: a whole-file Read exceeding the token cap is paginated by the tool, so the model only saw page one plus a banner — yet the file was marked as delivered and never re-attached.

6. **[#95423](https://github.com/anthropics/claude-code/pull/95423) — diff: skip refetch after read-only shell commands** *(CLOSED)*
   The mod refetched the diff after every Bash/PowerShell call; it now reads `isReadOnly` and skips commands like `ls`, `git status`, `cat`, and `grep`, matching built-in panel behavior and cutting wasted work.

7. **[#96363](https://github.com/anthropics/claude-code/pull/96363) — diff: pass `--no-color` so forced git colors don't empty the diff body** *(CLOSED)*
   Repos with `color.ui=always` / `color.diff=always` produced ANSI escapes that broke hunk-header matching even though `--shortstat`/`--numstat` counts stayed correct.

8. **[#96570](https://github.com/anthropics/claude-code/pull/96570) — diff: `command.run` hook names its command by a literal the engine's scan reads** *(CLOSED)*
   The engine scans hook modules for literal command names to decide which slash commands typed at startup must wait for a module to load. The mod's named-constant matcher defeated that scan; now uses a literal.

---

## 5. Feature Request Trends

- **Credential isolation for agentic dev/QA** — Two independent requests ([#88165](https://github.com/anthropics/claude-code/issues/88165) password-manager/secret-locker broker for accessibility; [#96949](https://github.com/anthropics/claude-code/issues/96949) owner-approved test-account sign-in for domains, iOS Simulator, and native apps) ask for the same primitive: a broker where the model triggers a login but **never sees the credential value**.
- **Context and memory durability** — [#96422](https://github.com/anthropics/claude-code/issues/96422) and [#96950](https://github.com/anthropics/claude-code/issues/96950)/[#96947](https://github.com/anthropics/claude-code/issues/96947) all point at compaction fidelity: instruction files not reloaded, assistant prose dropped or mis-rendered across compaction boundaries.
- **Cost predictability** — [#96565](https://github.com/anthropics/claude-code/issues/96565) and [#90018](https://github.com/anthropics/claude-code/issues/90018) target usage growth and hidden cache invalidation; users want visible, attributable token spend.
- **Trust and permission model coherence** — [#96928](https://github.com/anthropics/claude-code/issues/96928) (desktop vs CLI "trusted" disagreement), [#96943](https://github.com/anthropics/claude-code/issues/96943) (classifier overriding explicit `autoMode.allow`), and [#96954](https://github.com/anthropics/claude-code/issues/96954) (Auto-mode banner shown while in Manual) ask for one consistent, inspectable permission surface.
- **Remote/MCP session continuity** — [#95113](https://github.com/anthropics/claude-code/issues/95113) (OAuth refresh tokens for MCP) and [#63025](https://github.com/anthropics/claude-code/issues/63025) (remote session index durability) reflect growing SSH-remote and multi-server MCP usage.

---

## 6. Developer Pain Points

1. **Device bridge / Cowork reliability is the top friction.** Four separate threads filed within ~24 hours (#45937, #96911, #96918, #96919, #96887) across both platforms. The failure mode is opaque — WebSocket opens, handshake never completes — and survives reboot, re-login, device removal, and app update, so users have no self-service recovery.
2. **Auto-update regressions are landing directly in the release window.** #96931 (Linux TUI input freeze in 2.1.282) and #94687 (macOS dictation killed when the updater replaces the binary, breaking TCC grants) both show that auto-update changes binary identity or session state in ways that break running sessions.
3. **Sil

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

⚠️ Summary generation failed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*