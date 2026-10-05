# AI CLI Tools Community Digest 2026-10-05

> Generated: 2026-10-05 03:48 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool AI CLI Comparison Report — 2026-10-05

**Data caveat:** OpenAI Codex digest generation failed, so no verifiable Codex issue/PR/release data is available. Claude Code is the only complete dataset today; Codex entries are marked as unavailable rather than inferred.

## 1. Ecosystem Overview

The AI CLI ecosystem on 2026-10-05 shows a hardening phase rather than a launch phase: Claude Code shipped no release, but 50 issues were updated and 5 PRs advanced. The dominant community concerns are reliability, governance, and orchestration correctness—advisor/API failures, silent quota fallbacks, incomplete hook payloads, plugin permission gaps, and state persistence bugs. This suggests these tools are being used in longer, production-like agent workflows where trust, auditability, and fine-grained control matter more than raw feature velocity. The Codex digest failure is itself a monitoring gap: cross-tool trend claims cannot be fully validated from today’s data. Treat Claude Code’s signals as strong leading indicators, not as confirmed ecosystem-wide patterns.

## 2. Activity Comparison

| Tool | Issues Count / Activity | PR Count / Activity | Release Status | Notes |
|---|---:|---:|---|---|
| **Claude Code** | 50 issues updated in last 24h | 5 PRs updated in last 24h | None in last 24h | Highest-engagement issue: #69238, 67 comments, 112 👍. Strong demand for plugin/skill granularity: #14920, 95 👍. |
| **OpenAI Codex** | Data unavailable | Data unavailable | Data unavailable | Digest summary generation failed; no verifiable counts or release status. |

## 3. Shared Feature Directions

> Cross-tool overlap cannot be confirmed today because OpenAI Codex data is missing. The following are Claude Code’s clearest requirement clusters and are candidates for shared cross-tool direction, not verified multi-tool overlap.

| Direction | Tool(s) with evidence | Specific needs |
|---|---|---|
| **Granular plugin/skill control** | Claude Code (#14920, 95 👍) | Disable individual skills such as `commit-push-pr` or `clean_gone` without dropping the entire plugin. |
| **Per-task model/effort selection** | Claude Code (#95190) | Background `spawn_task` operations should carry model/effort settings instead of inheriting the orchestrator’s configuration. |
| **Hook/orchestration ergonomics** | Claude Code (#91910, #99366, #40572) | Global Hookify rules, surfacing non-blocking `PreToolUse` failures to agents, and complete agent context in compaction/stop payloads. |
| **Mobile/headless and team context** | Claude Code (#99525, #99495) | VPS/headless dispatch without an always-on desktop; group-level instructions and shared session context in sidebar groups. |
| **Safety and governance controls** | Claude Code (#99540, #99552, #99553) | Org-level tool ceilings over user-installed plugins; security guidance that covers `NotebookEdit` and parses nested calls correctly. |

**Codex note:** No Codex requirements are available from today’s digest, so no requirement can yet be labeled as shared across both communities.

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|---|---|---|
| **Visible feature focus** | Granular plugins/skills, hooks, advisor/model routing, MCP/connector hygiene, org policy, desktop/TUI parity. | Data unavailable. |
| **Target users** | Developers and teams building plugin-orchestrated,

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills — Community Highlights Report
**Source:** github.com/anthropics/skills · **Snapshot:** 2026-10-05

> **Data caveat:** In this snapshot, PR-level comment counts are recorded as `undefined`, so PRs cannot be ranked by raw comment volume. Ranking below uses available attention signals: recency of update activity, linkage to high-traffic Issues, and breadth of Skill surface area. Issue comment counts are complete and are used directly in Section 2.

---

## 1. Top Skills Ranking

The eight PRs drawing the most sustained community attention (top-of-funnel by update cadence + downstream Issue traffic):

| # | Skill / PR | What it does | Discussion highlight | Status |
|---|---|---|---|---|
| 1 | **claude-api — retire model IDs** [#1607](https://github.com/anthropics/skills/pull/1607) | Syncs `skills/claude-api/shared/models.md` with reality: moves `claude-opus-4-1`, `claude-sonnet-4-0`, `claude-opus-4-0`, `claude-3-haiku-20240307` out of "Legacy (active)" | Most recently touched PR in the set (2026-10-04); fixes #1603. Part of a cluster of claude-api maintenance PRs | OPEN |
| 2 | **claude-api — fix dead doc URLs** [#1730](https://github.com/anthropics/skills/pull/1730) | Replaces 3 hard-404 URLs in `academy-guide` and `tool-use-concepts.md` with verified-200 canonical URLs | Same-day activity as #1607 → claude-api is the current maintenance hotspot | OPEN |
| 3 | **skill-creator — trigger eval isolation / Windows + runtime failures** [#1298](https://github.com/anthropics/skills/pull/1298) | Fixes false trigger misses: competing per-worker probes, `select()` on subprocess pipes failing on Windows, runtime failures silently scored as non-triggers | Directly addresses the failure class reported in Issues #556 and #1383; longest-lived active fix (Jun → Sep) | OPEN |
| 4 | **mcp-builder — mcp>=2 HTTP client migration** [#1742](https://github.com/anthropics/skills/pull/1742) | Adapts to `streamable_http_client` rename and `create_mcp_http_client` / `http_client` header config in `mcp>=2.0.0` | Fixes #1668; complements the eval-harness breakage in Issue #1390 | OPEN |
| 5 | **docx — LibreOffice timeout handling** [#1792](https://github.com/anthropics/skills/pull/1792) | `accept_changes.py` now errors on `soffice` timeout instead of reporting success, and verifies revision marks are gone before claiming success | Example of the broader "silent-success" bug class the community keeps flagging | OPEN |
| 6 | **proofcore-contract-auditor** [#1771](https://github.com/anthropics/skills/pull/1771) | Static analysis of Solidity/Rust contracts with cryptographic audit proofs anchored to TON Blockchain via Merkle protocol | Representative of the Web3/vertical-domain contribution wave | OPEN |
| 7 | **notion-spec-to-implementation + quantitative-resume-auditor** [#1245](https://github.com/anthropics/skills/pull/1245) | Turns product specs into Notion tasks with acceptance criteria; second skill audits resumes quantitatively | One PR, two skills — the multi-skill submission pattern that reviewers flag as harder to merge | OPEN |
| 8 | **md2video-audio** [#1703](https://github.com/anthropics/skills/pull/1703) | Compiles Markdown → Marp slides → MP4 with TTS voiceover, zero-cost | Media-generation Skill direction, adjacent to the frontend-design/typography cluster | OPEN |

**Also notable:** `document-typography` [#514](https://github.com/anthropics/skills/pull/514) (orphan/widow control, numbering alignment), `pyxel` [#525](https://github.com/anthropics/skills/pull/525) (retro game dev, open since March), and `skill-quality-analyzer` / `skill-security-analyzer` [#83](https://github.com/anthropics/skills/pull/83) — a meta-Skill proposal that anticipated today's quality/security debate.

---

## 2. Community Demand Trends (from Issues)

Distilled from the top-comment Issues, four demand clusters dominate:

**A. Trust, security & namespace integrity — the #1 concern by volume**
- [#492](https://github.com/anthropics/skills/issues/492) — *Security: community skills distributed under `anthropic/` namespace enable trust boundary abuse* — **43 comments**, 2 👍. Community skills impersonating official Anthropic skills; users grant elevated permissions to non-official code.
- [#1394](https://github.com/anthropics/skills/issues/1394) — skill-creator `eval-viewer` `escapeHtml` not attribute-safe (display-path XSS).
- [#1175](https://github.com/anthropics/skills/issues/1175) — access-control logic embedded in `SKILL.md` for SharePoint workflows (closed, but framed the concern).

**B. Evaluation & trigger reliability — "does my skill actually fire?"**
- [#556](https://github.com/anthropics/skills/issues/556) — `run_eval.py` produces **0% trigger rate across all queries** — 12 comments, 7 👍.
- [#1383](https://github.com/anthropics/skills/issues/1383) — six reproducible skill-creator defects: silent benchmark failures, inverted delta, broken Windows trigger evals, skill shadowing.
- [#1390](https://github.com/anthropics/skills/issues/1390) — `mcp-builder` evaluation.py scores 0/N against every real MCP server.
- [#202](https://github.com/anthropics/skills/issues/202) — skill-creator reads as developer documentation, not an operational skill (closed).

**C. Context-window economics**
- [#1487](https://github.com/anthropics/skills/issues/1487) — `claude-api` eagerly injects **~156k tokens** in a single tool call, exhausting the window.
- [#189](https://github.com/anthropics/skills/issues/189) — `document-skills` and `example-skills` install identical content → duplicate skills in context — 6 comments, **9 👍** (highest-approval issue in the set).

**D. Distribution, collaboration & platform reach**
- [#228](https://github.com/anthropics/skills/issues/228) — org-wide skill sharing in Claude.ai instead of manual `.skill` file hand-offs — 16 comments, 8 👍.
- [#29](https://github.com/anthropics/skills/issues/29) — AWS Bedrock compatibility (unresolved).
- [#1329](https://github.com/anthropics/skills/issues/1329) — `compact-memory`: symbolic notation for compact agent state.

**Emerging proposal directions:** agent governance/safety patterns ([#412](https://github.com/anthropics/skills/issues/412)), reasoning quality gates ([#1385](https://github.com/anthropics/skills/issues/1385) — pre-task calibration → adversarial review → delivery verification), and persistent-memory compaction ([#1329](https://github.com/anthropics/skills/issues/1329)).

---

## 3. High-Potential Pending Skills

Open PRs with recent update activity — most likely to land or attract maintainer attention next:

| PR | Skill | Why it's a candidate | Last updated |
|---|---|---|---|
| [#1607](https://github.com/anthropics/skills/pull/1607) | claude-api model retirement | Small, factual, fixes a filed Issue; claude-api is the active maintenance area | 2026-10-04 |
| [#1730](https://github.com/anthropics/skills/pull/1730) | claude-api dead URL fixes | Verified-200 URLs, minimal diff, same subsystem | 2026-10-04 |
| [#1245](https://github.com/anthropics/skills/pull/1245) | notion-spec-to-implementation + quantitative-resume-auditor | Two complete skills; long-running since June | 2026-09-30 |
| [#1742](https://github.com/anthropics/skills/pull/1742) | mcp-builder mcp>=2 support | Fixes a filed Issue (#1668); breakage is blocking real usage | 2026-09-29 |
| [#1681](https://github.com/anthropics/skills/pull/1681) | skill-creator direct execution / docstring paths | `ModuleNotFoundError` on standalone `package_skill.py` — concrete, reproducible | 2026-09-27 |
| [#1792](https://github.com/anthropics/skills/pull/1792) | docx timeout-as-error | Correctness fix in a core bundled skill | 2026-09-25 |
| [#1734](https://github.com/anthropics/skills/pull/1734) | Detect orphaned docx comments | docx-category fix; summary body is empty (may need maintainer clarification) | 2026-09-25 |
| [#525](https://github.com/anthropics/skills/pull/525) | pyxel retro game dev | Open since March, still being rebased — a persistent community favorite | 2026-09-22 |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns | Full testing-stack skill (Testing Trophy, AAA, React Testing Library) — matches demand for test-generation/QA Skills | 2026-09-21 |

**Pattern:** the highest-probability landings are *small, Issue-linked maintenance fixes to bundled skills* (`claude-api`, `docx`, `mcp-builder`, `skill-creator`) rather than large net-new domain Skills — the latter stall for months (#525, #822, #210).

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand has shifted from "more Skills" to "trustworthy Skills": members are overwhelmingly asking for verified provenance/namespace integrity, reliable trigger and evaluation behavior, and context-window economy — i.e., making existing Skills safe, correct, and cheap to run rather than adding new ones.**

---

*Note: all linked items were OPEN as of the 2026-10-05 snapshot except Issues #202, #412, and #1175 (CLOSED).*

---

# Claude Code Community Digest — 2026-10-05

## 1. Today's Highlights

No new releases shipped in the last 24 hours, but issue activity remains high (50 issues updated), dominated by a long-running Advisor/API failure on macOS (#69238, 112 👍) and its sibling model-context bug (#67609). The community's clearest signal today is demand for finer-grained control: disabling individual plugin skills (#14920, 95 👍) and per-task model/effort selection (#95190) both advanced. Newly filed reports also point at CLI tool regressions in 2.1.289 (#99556) and security-guidance plugin hook gaps (#99552, #99553).

## 2. Releases

None in the last 24 hours.

## 3. Hot Issues

1. **[#69238](https://github.com/anthropics/claude-code/issues/69238)** — *[BUG] No response from API error when Advisor is triggered* (67 comments, 112 👍). The highest-engagement issue in the queue: Opus 4.8 advisor calls on a Sonnet base return "No response from API · Retrying" with no actionable error. Sustained comment volume over four months suggests neither a fix nor a workaround has landed.
2. **[#67609](https://github.com/anthropics/claude-code/issues/67609)** — *Advisor tool returns "unavailable" on claude-fable-5 above ~100K tokens* (27 comments, 45 👍). A reproducible threshold bug that effectively disables the advisor for long sessions — likely the same failure surface as #69238, and the most technically specific of the advisor reports.
3. **[#14920](https://github.com/anthropics/claude-code/issues/14920)** — *Feature Request: Disable individual plugin skills* (19 comments, 95 👍). Users want to opt out of specific skills (e.g. `commit-push-pr`, `clean_gone`) without dropping the whole plugin. Highest 👍 count of any open enhancement.
4. **[#92007](https://github.com/anthropics/claude-code/issues/92007)** — *`/model opusplan` fails with "Unsupported model"* (9 comments, 13 👍). A Windows regression that broke a configuration working "for months until today" — the classic silent model-availability change that erodes trust in `/model` routing.
5. **[#91910](https://github.com/anthropics/claude-code/issues/91910)** — *Hook payload gaps for subagent compaction* (8 comments). `PreCompact`/`PostCompact`/`SessionStart(compact)` fire without agent fields, and `SubagentStop` fires for internal summarizer calls with a never-created `agent_transcript_path`. Matters to anyone building hook-based orchestration or cost accounting.
6. **[#95815](https://github.com/anthropics/claude-code/issues/95815)** — *WebSearch session cap fails silently* (2 comments). Over-budget calls return non-error results, so agents silently fall back to model memory and contaminate long research runs. A correctness bug disguised as a quota feature.
7. **[#98345](https://github.com/anthropics/claude-code/issues/98345)** — *Auto mode dropped on first turn* (1 comment, 1 👍). `defaultMode: "auto"` doesn't apply until turn two, forcing a re-send from the desktop app. Permission-state inconsistency at session start.
8. **[#97504](https://github.com/anthropics/claude-code/issues/97504)** — *User-directed messages emitted as hidden thinking blocks* (3 comments, 7 👍). Intermittent and tied to replies containing tool calls — content silently never reaches the user.
9. **[#99513](https://github.com/anthropics/claude-code/issues/99513)** — *Stale `claudeAiMcpEverConnected` cache injects disconnected MCP tools* (1 comment). A stale flag in `~/.claude.json` pushes full tool definitions for 16 disconnected claude.ai connectors into every session — context bloat plus a correctness risk.
10. **[#99541](https://github.com/anthropics/claude-code/issues/99541)** — *Desktop sidebar session-to-group assignments lost after Windows reboot* (data-loss). Groups survive, sessions don't. Filed today with a repro.

*Also worth watching:* [#99552](https://github.com/anthropics/claude-code/issues/99552) and [#99553](https://github.com/anthropics/claude-code/issues/99553) — two same-day reports from the same author showing the `security-guidance` plugin's PostToolUse reminders never fire for `NotebookEdit`, and that YAML/torch/`np.load` rules stop at the first `)` (false positives on `SafeLoader`/`weights_only=True`, missed `allow_pickle=True`). Safety tooling that fails open deserves fast triage.

## 4. Key PR Progress

Only 5 PRs were updated in the last 24h, so all are covered:

1. **[#99540](https://github.com/anthropics/claude-code/pull/99540)** — *sec-default: organization tool ceiling holds over user-installed plugins.* The policy mod now enforces org-level approval/deny rules over plugins an individual installs, with `.catch` on every deciding hook. Closes a real governance gap in plugin permissions.
2. **[#40572](https://github.com/anthropics/claude-code/pull/40572)** — *Global Hookify rules from `~/.claude/`.* Adds cross-project rule loading alongside `.claude/`, addressing a recurring request for user-level hook configuration.
3. **[#87077](https://github.com/anthropics/claude-code/pull/87077)** — *Fix invalid YAML frontmatter in pr-review-toolkit agents.* Unquoted scalars containing `key: value` dialogue lines were parsed as nested mappings, causing agents to load with empty `name`/`description`/`model`. A quiet but high-impact fix.
4. **[#20448](https://github.com/anthropics/claude-code/pull/20448)** — *Add web4-governance plugin (T3 trust tensors, R6 audit trails).* Community-contributed governance plugin; still open since January.
5. **[#1](https://github.com/anthropics/claude-code/pull/1)** — *Create SECURITY.md* (CLOSED). Repository housekeeping, updated after a long dormancy.

## 5. Feature Request Trends

- **Granular plugin/skill control** — Disable individual skills rather than whole plugins (#14920); plugins consistently are all-or-nothing today.
- **Per-task model & effort selection** — `spawn_task` chips carry no model/effort picker, so every background task inherits the orchestrator's settings (#95190).
- **Better hook ergonomics** — Global Hookify rules (#40572), surfacing non-blocking `PreToolUse` failures to the agent (#99366), and complete agent context in compaction/stop payloads (#91910).
- **TUI/agent-view customization** — Independently hide mode indicator and hint text (#93803); let the agent declare a semantic work phase (Brainstorming/Implementing/Shipping) on a session (#99551).
- **Mobile/headless workflows** — Dispatch support for VPS/headless servers without an always-on desktop (#99525).
- **Shared session context in sidebar groups** — Group-level instructions and group awareness for claude.ai/code (#99495).

## 6. Developer Pain Points

- **Advisor/model availability is unreliable and opaque.** #69238 and #67609 together account for the two loudest threads: advisor calls fail with network-flavored errors, or go `unavailable` past a token threshold on specific models. Silent `/model` support changes (#92007) compound the frustration.
- **Silent failures over loud errors.** WebSearch cap overruns return non-errors (#95815); non-blocking hook failures never reach the agent and truncate stderr (#99366). Agents proceed on bad assumptions, which is worse than a hard stop.
- **Hook payloads are incomplete or semantically wrong.** Compaction hooks omit agent fields; `SubagentStop` fires for internal summarizer calls (#91910) — orchestration built on hooks can't trust the signal.
- **State and permissions don't persist correctly.** Auto mode lost on turn one (#98345), sidebar grouping lost across reboot (#99541), desktop updates killing running sessions (#90867), remote-control sessions never re-dispatched after unarchive (#98310).
- **Stale caches and cross-surface parity.** Disconnected MCP connectors still injected into sessions (#99513); mods render differently in the desktop app than the terminal (#99535, #99265).
- **Safety tooling that fails open.** The `security-guidance` plugin's pattern rules miss `NotebookEdit` entirely and mis-parse nested calls (#99552, #99553) — false confidence in a security feature is a distinct class of pain.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

⚠️ Summary generation failed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*