# AI CLI Tools Community Digest 2026-09-17

> Generated: 2026-09-17 03:09 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report — AI CLI Tools, 2026-09-17

**Data quality note:** Only the OpenAI Codex digest was usable. Claude Code’s summary generation failed. No digests for other major AI CLI tools were supplied. The Codex digest appears truncated mid-release list, and it does not provide numeric issue or PR counts. Quantitative cross-tool comparison is therefore limited; the report is primarily qualitative and signal-based.

## 1. Ecosystem Overview
The AI CLI landscape remains release-train driven, with Codex publishing multiple alpha tags in 24 hours and no detailed changelogs. Community friction is concentrated on reliability and platform parity: capacity/rate-limit failures despite available quota, Windows Desktop follow-up send regressions, and app-server queued follow-up errors. Feature work is moving toward agent orchestration and integration plumbing: TUI/Code Mode, context and attachment accounting, subagent settings, MCP interaction routing, and Windows sandbox setup. Claude Code produced no usable signal today, preventing a true two-sided comparison. Overall, differentiation is shifting from basic CLI access to production-grade reliability, transparent quota behavior, cross-platform consistency, and MCP/agent extensibility.

## 2. Activity Comparison

| Tool | Issues count | PR count | Release status |
|---|---:|---:|---|
| **OpenAI Codex** | Not reported. Dominant issue themes: capacity/rate-limit failures despite available quota; Windows Desktop follow-up send regressions; app-server queued follow-up errors. | Not reported. PR focus areas: TUI/Code Mode polish; context and attachment accounting; subagent settings; MCP interaction routing; Windows sandbox setup. | Alpha-heavy. Published `rust-v0.155.0-alpha.15`, multiple `0.155.0-alpha.*` tags, and `rusty-v8-v152.2.0` in the last 24h. Release notes contain only version strings. |
| **Claude Code** | N/A — summary generation failed. | N/A — summary generation failed. | N/A — summary generation failed. |

**Interpretation:** Codex shows clear release and PR activity, but without numeric counts it cannot be benchmarked quantitatively against Claude Code. Claude Code has no measurable activity in this dataset.

## 3. Shared Feature Directions
No cross-tool shared feature direction can be confirmed from the supplied data because only one tool produced a usable digest. Codex-only requirement signals are:

- **Quota and capacity reliability** — rate-limit failures despite available quota.
- **Windows Desktop parity** — follow-up send regressions.
- **App-server queue correctness** — queued follow-up errors.
- **TUI/Code Mode UX** — continued polish.
- **Context and attachment accounting** — resource visibility and budgeting.
- **Subagent configuration** — agent orchestration controls.
- **MCP interaction routing** — tool/permission

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills — Community Highlights Report
**Source:** github.com/anthropics/skills · **Data snapshot:** 2026-09-17

> **Data caveat:** PR comment counts are returned as `undefined` in the dataset, so "most-discussed" is inferred from proxy signals — linked-issue traffic (the highest-comment issue a PR fixes), recency of activity, cross-referencing, and whether the PR touches *core tooling* (`skill-creator`, `mcp-builder`, `claude-api`, `office`) rather than a single skill. All PRs listed are **OPEN**; the repo shows no merged items in this window.

---

## 1. Top Skills Ranking

| # | Skill / PR | What it does | Discussion highlight | Status |
|---|---|---|---|---|
| 1 | [**skill-creator** — isolate trigger evals, Windows & runtime failures, #1298](https://github.com/anthropics/skills/pull/1298) | Fixes false-miss scoring in trigger evaluation: per-worker command probes competing, `select()` on subprocess pipes failing on Windows, unrelated tools aborting scans, and runtime failures mis-scored as non-triggers (which silently "pass" negative examples). | Sits on top of the repo's hottest bug class — Issue [#556](https://github.com/anthropics/skills/issues/556) (12 comments): *"`claude -p` never triggers skills (0% trigger rate across all queries)"*. Latest activity 2026‑09‑16, one day before snapshot. | OPEN |
| 2 | [**skill-creator** — trigger detection reporting 0% recall, #1769](https://github.com/anthropics/skills/pull/1769) | Fixes [#1721](https://github.com/anthropics/skills/issues/1721): trigger evaluation reports `precision=100% recall=0%` for *every* skill regardless of description, and `run_loop` then "optimizes" against fabricated evidence. | Same failure surface as #1298, submitted one day earlier — converging independent diagnoses of the eval harness. High merge probability. | OPEN |
| 3 | [**mcp-builder** — support `mcp>=2` `streamable_http_client` + custom headers, #1742](https://github.com/anthropics/skills/pull/1742) | Fixes [#1668](https://github.com/anthropics/skills/issues/1668): in `mcp>=2.0.0` the client was renamed and headers moved to `create_mcp_http_client`/`http_client`, breaking `scripts/connections.py`. | `mcp-builder` is the most bug-reported skill in the collection (cf. Issue [#1390](https://github.com/anthropics/skills/issues/1390): eval harness fabricates tool errors, scores 0/N). Updated 2026‑09‑17 — the freshest PR in the set. | OPEN |
| 4 | [**skill-quality-analyzer + skill-security-analyzer** (marketplace), #83](https://github.com/anthropics/skills/pull/83) | Two meta-skills: five-dimension quality analysis (structure/docs, examples, resources…) and a security analyzer for Skills. | Maps directly to the single highest-traffic community issue — [#492](https://github.com/anthropics/skills/issues/492), 43 comments: community skills distributed under the `anthropic/` namespace enabling trust-boundary abuse. Long-lived (Nov 2025 → Jan 2026). | OPEN |
| 5 | [**pyxel** — retro game development, #525](https://github.com/anthropics/skills/pull/525) | Guides agents through building, debugging and verifying Pyxel/Python retro games: deterministic headless runs, direct frame inspection, task-specific state checks, plus references for Pyxel behavior and presentation defaults. | Open since 2026‑03‑05 yet still updated 2026‑09‑16 — one of the longest-running actively-iterated submissions, indicating sustained author/reviewer engagement. | OPEN |
| 6 | [**proofcore-contract-auditor**, #1771](https://github.com/anthropics/skills/pull/1771) | Web3 Agent Skill: static analysis of Solidity and Rust contracts, with cryptographic audit proofs anchored to the TON Blockchain via a zero-storage Merkle protocol. | Newest arrival (created 2026‑09‑15, updated 2026‑09‑16) and an unusual vertical — blockchain notarization — which tends to attract cross-ecosystem attention. | OPEN |
| 7 | [**document-typography / ODT / docx fixes** — typography quality control, #514](https://github.com/anthropics/skills/pull/514) · [ODT skill, #486](https://github.com/anthropics/skills/pull/486) · [docx `w:id` collision, #541](https://github.com/anthropics/skills/pull/541) | Prevents orphan word wrap, widow paragraphs and numbering misalignment; adds OpenDocument creation/templating; fixes DOCX corruption from tracked-change ID collisions with bookmarks. | The "document-skills" cluster is the largest coherent body of PR activity, largely driven by repeat contributors (PGTBoos, Lubrsy706, GitHubNewbie0) and by Issue [#189](https://github.com/anthropics/skills/issues/189) (6 comments, 9 👍) on duplicate `document-skills`/`example-skills` content. | OPEN |
| 8 | [**claude-api** — mark four retired model IDs as retired, #1607](https://github.com/anthropics/skills/pull/1607) | Corrects `shared/models.md`: moves `claude-opus-4-1`, `claude-sonnet-4-0`, `claude-opus-4-0`, `claude-3-haiku-20240307` out of "Legacy (still active)" / "Deprecated". | Fixes [#1603](https://github.com/anthropics/skills/issues/1603), and rides alongside Issue [#1487](https://github.com/anthropics/skills/issues/1487) — `claude-api` eagerly injecting ~156k tokens and exhausting the context window in one tool call. | OPEN |

*Other notable active PRs:* [md2video-audio, #1703](https://github.com/anthropics/skills/pull/1703) · [office UTF‑8 redlining diff fix, #1765](https://github.com/anthropics/skills/pull/1765) · [Hivemind multi-agent orchestration, #1628](https://github.com/anthropics/skills/pull/1628) · [Buffer GraphQL skill, #1627](https://github.com/anthropics/skills/pull/1627).

---

## 2. Community Demand Trends (from Issues)

| Trend | Evidence | What the community wants |
|---|---|---|
| **Trust, provenance & security of Skills** | [#492](https://github.com/anthropics/skills/issues/492) — 43 comments (top issue); [#1175](https://github.com/anthropics/skills/issues/1175) on embedding access-control logic in `SKILL.md` | Namespace verification, signing/provenance, permission scoping, and a first-party security analyzer before a skill can claim `anthropic/`. |
| **Evaluation & tooling correctness** | [#556](https://github.com/anthropics/skills/issues/556) — 12 comments, 7 👍; [#1390](https://github.com/anthropics/skills/issues/1390) — mcp-builder eval scores 0/N on real servers | Working, trustworthy trigger/eval harnesses. Two independent PRs (#1298, #1769) target the same 0%-recall bug — the community is effectively debugging Anthropic's own meta-tooling. |
| **Team/organization distribution** | [#228](https://github.com/anthropics/skills/issues/228) — 16 comments, 8 👍; [#189](https://github.com/anthropics/skills/issues/189) — duplicate skills across plugins | Org-wide shared skill libraries, share links, deterministic installs — replacing the current "download the `.skill` file and Slack it" workflow. |
| **Context-window economy** | [#1487](https://github.com/anthropics/skills/issues/1487) — `claude-api` injects ~156k tokens in one call; [#202](https://github.com/anthropics/skills/issues/202) — skill-creator reads like human docs, not operational instructions | Progressive/lazy loading, token budgets per skill, and concise instruction-style authoring as a hard guideline. |
| **Cross-runtime interoperability** | [#29](https://github.com/anthropics/skills/issues/29) — Bedrock; [#16](https://github.com/anthropics/skills/issues/16) — expose Skills as MCPs | Portable skill format usable beyond Claude Code; MCP-style interface contracts so Skills can wrap software APIs. |
| **Agent governance & reasoning quality** | [#412](https://github.com/anthropics/skills/issues/412) — agent-governance (closed); [#1385](https://github.com/anthropics/skills/issues/1385) — three-gate reasoning quality pipeline; [#1329](https://github.com/anthropics/skills/issues/1329) — compact-memory | Safety patterns for autonomous agents, adversarial review gates, and compressed symbolic agent state. |
| **Reliability of skill persistence** | [#62](https://github.com/anthropics/skills/issues/62) — 12 skills silently disappeared | Stable storage/versioning for user-authored skills; less fear of losing work. |

---

## 3. High-Potential Pending Skills (most likely to land)

| PR | Skill | Why it's close |
|---|---|---|
| [#1742](https://github.com/anthropics/skills/pull/1742) | `mcp-builder` `mcp>=2` compatibility | Narrow, version-specific fix with an upstream issue (#1668); updated on the snapshot date. |
| [#1769](https://github.com/anthropics/skills/pull/1769) | `skill-creator` 0%-recall fix | Directly closes a reproducible bug (#1721) that mirrors the high-traffic #556. |
| [#1298](https://github.com/anthropics/skills/pull/1298) | `skill-creator` eval isolation + Windows/runtime failures | Broader companion to #1769; if reviewers pick one, they likely pick the narrower one first. |
| [#1765](https://github.com/anthropics/skills/pull/1765) | Office redlining UTF‑8 decoding | Small, validated across DOCX/PPTX/XLSX validators; fixes #1707 for Windows and non-UTF‑8 locales. |


---

⚠️ Summary generation failed.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-09-17

## Today's Highlights
The Codex Rust release train remains alpha-heavy, with `rust-v0.155.0-alpha.15` plus multiple `0.155.0-alpha.*` tags and `rusty-v8-v152.2.0` published in the last 24h; release notes contain only version strings. Community attention is dominated by capacity/rate-limit failures despite available quota, Windows Desktop follow-up send regressions, and app-server queued follow-up errors. PR activity is focused on TUI/Code Mode polish, context and attachment accounting, subagent settings, MCP interaction routing, and Windows sandbox setup.

## Releases
New prerelease tags in the last 24h. No detailed changelogs were provided.

- [rust-v0.155.0-alpha.15](https://github.com/openai/codex/releases/tag/rust-v0.155.0-alpha.15) — `0.155.0-alpha.15`
- [rust-v0.155.0-alpha.14](https://github.com/openai/codex/releases/tag/rust-v0.155.0-alpha.14) — `0.155.0-alpha.14`
- [rust-v0.155.0-alpha.13](https://github.com/openai/codex/releases/tag/rust-v0.155.0-alpha.13) — `0.155.0-alpha.13`
- [rust-v0.155.0-alpha.12](https://github.com/openai/codex/releases/tag/rust-v0.155.0-alpha.12) — `0.155.0-alpha.12`
- [rust-v0.155.0-alpha.11](https://github.com/openai/codex/releases/tag/rust-v0.155.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*