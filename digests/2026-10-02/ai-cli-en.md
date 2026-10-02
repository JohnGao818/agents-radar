# AI CLI Tools Community Digest 2026-10-02

> Generated: 2026-10-02 03:49 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

**Scope note:** This comparison covers the two tools with provided 2026-10-02 digests: **Claude Code** and **OpenAI Codex**. Issue/PR counts below are **digest-listed counts**, not full repository totals; Claude Code’s digest is partially truncated.

## 1. Ecosystem Overview
On 2026-10-02, the AI CLI tool landscape is splitting between **deep extensibility** and **operational reliability**. Anthropic is pushing Claude Code toward a plugin/mod platform with **Claude Mods** and a built-in side-agent, while OpenAI Codex is heavily focused on **Windows stability, MCP/sandbox hardening, and cloud/dot orchestration**. Both communities show strong demand for MCP/plugin ecosystems, permission consistency, and reliable agent delegation. The main adoption blocker is no longer model capability alone, but **trust in daily workflows**: crashes, silent message loss, auth/MCP failures, and inconsistent tool access across local, delegated, and cloud sessions.

## 2. Activity Comparison

| Tool | Digest-listed Issues | Digest-listed PRs | Release status today | Top engagement signal |
|---|---:|---:|---|---|
| **Claude Code** | 1 detailed hot issue (#91870) + active bug clusters not itemized: GitHub connector, artifact public sharing, MCP/auth | **5 PRs updated in last 24h** | **v2.1.287 stable**: Claude Mods

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills — Community Highlights

*Data snapshot: 2026-10-02 · Source: `anthropics/skills`*

> **Methodology note:** All 50 sampled PRs report `Comments: undefined` and `👍: 0`, so ranking below uses a composite signal — update recency, cross-referenced Issues, breadth of scope, and whether the Skill touches shared infrastructure (eval harness, packaging, security). Issue comment counts *are* available and are cited directly.

---

## 1. Top Skills Ranking

**1. skill-creator: trigger-eval isolation + Windows/runtime failures** — [PR #1298](https://github.com/anthropics/skills/pull/1298)
*Author: MartinCajiao · OPEN · updated 2026-09-16*
Hardens the trigger-evaluation harness: per-worker command probes racing each other, `select()` on subprocess pipes breaking on Windows, and unrelated tools aborting scans. Runtime failures were being silently reclassified as "non-triggers," which made negative examples pass falsely. This is the direct PR-side counterpart to Issue [#1383](https://github.com/anthropics/skills/issues/1383) and [#556](https://github.com/anthropics/skills/issues/556) — the single most-cited reliability problem in the repo.

**2. mcp-builder: `mcp>=2` streamable HTTP client + custom headers** — [PR #1742](https://github.com/anthropics/skills/pull/1742)
*Author: Kuldeeep18 · OPEN · updated 2026-09-29*
Fixes breakage from the `streamablehttp_client` → `streamable_http_client` rename and moves custom headers to `create_mcp_http_client`. Closes [#1668](https://github.com/anthropics/skills/issues/1668) and pairs with Issue [#1390](https://github.com/anthropics/skills/issues/1390), which reports the MCP evaluation harness scoring 0/N against real servers.

**3. notion-spec-to-implementation + quantitative-resume-auditor** — [PR #1245](https://github.com/anthropics/skills/pull/1245)
*Author: mrdesouzaphd-cmyk · OPEN · updated 2026-09-30 (most recently touched PR)*
Turns product/tech specs into Notion implementation tasks with acceptance criteria and progress tracking. Still under review — the `notion-spec-to-implementation` half of the PR dominates attention.

**4. docx: report LibreOffice timeout as an error + verify output** — [PR #1792](https://github.com/anthropics/skills/pull/1792)
*Author: TINGyu123644 · OPEN · updated 2026-09-25*
`accept_changes.py` now fails loudly on `soffice` timeout and only reports success after confirming no `w:ins`/`w:del`/`w:moveFrom`/`w:moveTo` remain in `word/*.xml`. A correctness fix for a widely used document Skill.

**5. claude-api: mark four retired model IDs as retired** — [PR #1607](https://github.com/anthropics/skills/pull/1607)
*Author: adi-IL · OPEN · updated 2026-09-28*
Closes [#1603](https://github.com/anthropics/skills/issues/1603); corrects `claude-opus-4-1`, `claude-sonnet-4-0`, `claude-opus-4-0`, `claude-3-haiku-20240307`. Notable because `claude-api` is also the subject of Issue [#1487](https://github.com/anthropics/skills/issues/1487) (≈156k tokens injected in one tool call).

**6. skill-creator: standalone execution of `package_skill.py`** — [PR #1681](https://github.com/anthropics/skills/pull/1681)
*Author: Kuldeeep18 · OPEN · updated 2026-09-27*
Fixes `ModuleNotFoundError: No module named 'scripts.quick_validate'` when running the packager directly, plus stale docstrings/CLI paths. Low-risk, high-friction-removal fix for anyone authoring Skills.

**7. proofcore-contract-auditor (Web3 smart-contract notarization)** — [PR #1771](https://github.com/anthropics/skills/pull/1771)
*Author: ProofCore-Protocol · OPEN · updated 2026-09-16*
Static analysis of Solidity/Rust contracts with cryptographic audit proofs anchored to TON via a zero-storage Merkle protocol. The most ambitious *new-domain* Skill in the top set — and the kind of third-party/vendor-flavored submission Issue [#492](https://github.com/anthropics/skills/issues/492) warns about.

**8. testing-patterns (full testing stack)** — [PR #723](https://github.com/anthropics/skills/pull/723)
*Author: 4444J99 · OPEN · updated 2026-09-21*
Testing Trophy model, AAA unit patterns, React Testing Library, and what *not* to test. Representative of the strongest new-Skill demand cluster (test generation), alongside `awt` E2E testing ([PR #822](https://github.com/anthropics/skills/pull/822)).

**Honorable mentions:** `pyxel` retro game dev ([#525](https://github.com/anthropics/skills/pull/525)), `md2video-audio` Markdown→MP4 ([#1703](https://github.com/anthropics/skills/pull/1703)), `document-typography` QC ([#514](https://github.com/anthropics/skills/pull/514)), `scnet-hpc` Slurm workflows ([#1615](https://github.com/anthropics/skills/pull/1615)).

---

## 2. Community Demand Trends

Distilled from the top-15 Issues:

| Direction | Evidence | Signal |
|---|---|---|
| **Security, provenance & trust boundaries** | [#492](https://github.com/anthropics/skills/issues/492) — 43 comments (highest in repo) | Community skills shipping under the `anthropic/` namespace impersonate official ones; demands for signing, namespacing, and a security-analyzer Skill. |
| **Skill distribution & org-scale sharing** | [#228](https://github.com/anthropics/skills/issues/228) — 16 comments, 8 👍 | Users manually Slack `.skill` files today; want a shared library and direct sharing links in Claude.ai. |
| **Evaluation & trigger reliability** | [#556](https://github.com/anthropics/skills/issues/556) (12c, 7👍), [#1383](https://github.com/anthropics/skills/issues/1383), [#1394](https://github.com/anthropics/skills/issues/1394), [#1390](https://github.com/anthropics/skills/issues/1390) | `run_eval.py` reports 0% trigger rate; benchmark layouts silently mismatch; XSS in the eval viewer; MCP evaluation fabricates tool errors. |
| **Context-window economy** | [#1487](https://github.com/anthropics/skills/issues/1487), [#1329](https://github.com/anthropics/skills/issues/1329), [#189](https://github.com/anthropics/skills/issues/189) (9👍), [#202](https://github.com/anthropics/skills/issues/202) | Over-eager token injection, duplicate skills across plugins, and skill-creator's prose-heavy, token-inefficient style. |
| **Agent governance & reasoning quality** | [#412](https://github.com/anthropics/skills/issues/412), [#1385](https://github.com/anthropics/skills/issues/1385) | Proposal-level demand for policy enforcement, audit trails, and pre-task calibration → adversarial review → delivery verification gates. |
| **Skill lifecycle & portability** | [#62](https://github.com/anthropics/skills/issues/62), [#29](https://github.com/anthropics/skills/issues/29), [#1175](https://github.com/anthropics/skills/issues/1175) | Lost skills, Bedrock compatibility, and data-residency concerns for SPO/enterprise document handling. |

---

## 3. High-Potential Pending Skills

All are OPEN, but these show the most recent maintainer/author activity and the smallest surface area to merge:

- [PR #1245](https://github.com/anthropics/skills/pull/1245) — `notion-spec-to-implementation` (+ resume auditor) · updated 2026-09-30
- [PR #1742](https://github.com/anthropics/skills/pull/1742) — mcp-builder `mcp>=2` compatibility · updated 2026-09-29 · closes an existing issue
- [PR #1607](https://github.com/anthropics/skills/pull/1607) — claude-api retired model IDs · updated 2026-09-28 · closes an existing issue
- [PR #1681](https://github.com/anthropics/skills/pull/1681) — skill-creator standalone packaging · updated 2026-09-27
- [PR #1792](https://github.com/anthropics/skills/pull/1792) — docx LibreOffice timeout handling · updated 2026-09-25
- [PR #1734](https://github.com/anthropics/skills/pull/1734) — detect orphaned docx comments · updated 2026-09-25
- [PR #525](https://github.com/anthropics/skills/pull/525) — `pyxel` retro game development · updated 2026-09-22
- [PR #723](https://github.com/anthropics/skills/pull/723) — `testing-patterns` · updated 2026-09-21

**Highest-conviction bets:** #1742 and #1607 (both close open bugs), and #1792/#1681 (narrow, verifiable, low-review-cost fixes to existing first-party Skills).

---

## 4. Skills Ecosystem Insight

**The community's demand has shifted from "what new Skill should exist?" to "can I trust the Skills that already exist?"** — the dominant, cross-cutting pressure is on correctness and trust infrastructure (trigger/eval accuracy, context budget, security provenance, packaging reliability) rather than on new Skill domains.

---

# Claude Code Community Digest — 2026-10-02

## Today’s Highlights
Claude Code **v2.1.287** introduces **Claude Mods**, allowing plugins to modify deeper Claude Code behavior, plus the built-in **“You should know”** mod that runs a side agent to flag missed issues. Community attention is heavily focused on the Mods extensibility thread **#91870** (229 comments, 130 👍), while high-impact bugs around **GitHub connector access**, **artifact public sharing**, and **MCP/auth** remain active. PR activity is light, with only five PRs updated in the last 24h, mostly around diff/dialog behavior and Mods cleanup.

## Releases
- **[v2.1.287](https://github.com/anthropics/claude-code/releases/tag/v2.1.287)** — Adds **Claude Mods**: plugins may now modify deeper behavior. Introduces **“You should know”**, a built-in mod where a side agent watches for things you or Claude might miss. Enable with:  
  `/plugin enable cc-plugin-you-should-know@builtin`  
  *(for first-party sessions; release note truncated in snapshot)*

## Hot Issues
- **[#91870 — Mods: make Claude 10x more extensible](https://github.com/anthropics/claude-code/issues/91870)** — OPEN | 229 comments | 130 👍  
  Central thread for the new Mods/plugin extensibility system. Maintainers have

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-10-02

## 1. Today's Highlights

Windows desktop reliability continues to dominate the tracker: startup hangs, renderer crashes, and missing Computer Use/browser tools in dot-delegated tasks account for most of today's highest-engagement issues. On the release side, `rust-v0.160.0` shipped stable with agent-command-center pagination and Linux fullscreen paste improvements, while the `0.161`/`0.162` alpha trains keep moving with terse, note-free builds. The PR queue shows heavy backend hardening — worktree MCP tools, server-driven permission catalogs, Windows MCP env handling, and a new native gRPC cloud-thread client.

## 2. Releases

- **rust-v0.160.0 (stable)** — Notable features:
  - Keyboard-accessible "Show more" to browse older tasks in the agent command center (#49106)
  - Transcript text selection + middle-click paste in fullscreen on supported local Linux X11 terminals (#49112)
  - Ability to start sessions outside a project using a workspace default
- **rust-v0.162.0-alpha.3 / alpha.2 / alpha.1** — Alpha builds, no detailed notes.
- **rust-v0.161.0-alpha.7 through alpha.13** — Rapid alpha cadence, no detailed notes.
- https://github.com/openai/codex/releases

**Takeaway:** The 0.16x line is iterating quickly in alpha while stable users get incremental TUI/workflow polish. No breaking migrations are flagged in the release notes.

## 3. Hot Issues

1. **[#49458](https://github.com/openai/codex/issues/49458) — [Windows] dot-started local tasks lack Computer Use tools (OPEN, 21 comments, 13 👍)** — Local Codex sessions get Computer Use tools, but dot-originated tasks on the same machine don't. High engagement because it breaks the core "delegate to my PC" workflow.
2. **[#21073](https://github.com/openai/codex/issues/21073) — Auto-resume CLI session when usage limit resets (OPEN, 16 comments, 70 👍)** — The single highest-upvoted item in this batch. Long-running since May; requests using the known reset timestamp to automatically resume mid-task work overnight.
3. **[#49532](https://github.com/openai/codex/issues/49532) — Put the Branch selection BACK in codex app (OPEN, 13 comments, 45 👍)** — A regression complaint about removed branch-selection UI at session start. Strong upvote signal indicates a widely used workflow.
4. **[#48938](https://github.com/openai/codex/issues/48938) — [Windows] Repeated renderer crashes, white-screen reloads, severe input lag (OPEN, 12 comments)** — Reported by a Pro 20x user with significant productivity impact; representative of a broader Windows stability cluster.
5. **[#49488](https://github.com/openai/codex/issues/49488) — [Windows][dot/Work] Computer tasks lack browser/desktop tools; durable MCP startup failures (OPEN, 11 comments)** — Companion to #49458 with additional MCP startup and path errors. Suggests a systemic dot/Windows tool-binding problem rather than a one-off.
6. **[#48377](https://github.com/openai/codex/issues/48377) — [Windows] Endless startup spinner after update (OPEN, 10 comments)** — App never finishes startup; logs show `awaiting-framework` with an undefined bundle version. Blocks all usage when hit.
7. **[#49718](https://github.com/openai/codex/issues/49718) — [Windows] Stuck on logo splash + sandbox setup always fails (OPEN, 9 comments)** — Renderer misses the app-server "connected" state, and the Windows sandbox rejects non-managed permission profiles. Two independent blockers bundled in one report.
8. **[#47041](https://github.com/openai/codex/issues/47041) — GPT-5.6 Sol / GPT-6 Astra reject harmless prompts with `invalid_prompt` (OPEN, 9 comments)** — Model-behavior issue affecting newer models; relevant as teams adopt GPT-6 generation models.
9. **[#49988](https://github.com/openai/codex/issues/49988) — VS Code extension intermittently drops submitted messages (OPEN, 7 comments, 7 👍)** — A silent data-loss class bug: composer clears, message never appears, no response. High 👍-to-comment ratio signals broad impact.
10. **[#50127](https://github.com/openai/codex/issues/50127) — DOT: UNKNOWN task creation, stale disconnect notifications, Luna schema failures (OPEN, 6 comments)** — Fresh report tying together several dot orchestration failure modes; may be the umbrella for the dot/cloud-task issues below.

*Also worth watching:* [#25962](https://github.com/openai/codex/issues/25962) (Computer Use plugins unavailable on Windows, open since June), [#49551](https://github.com/openai/codex/issues/49551) (macOS dots lack `node_repl js`), [#50156](https://github.com/openai/codex/issues/50156) (Windows splash hang on build 26200), and [#49033](https://github.com/openai/codex/issues/49033) (CLI freeze after input).

## 4. Key PR Progress

1. **[#50162](https://github.com/openai/codex/pull/50162) — Bound in-flight file opens in exec-server** — Reserves a semaphore permit *before* polling the file-open future, closing a gap where pending opens escaped the 128-handle per-connection cap. Resource-exhaustion hardening.
2. **[#50148](https://github.com/openai/codex/pull/50148) — Add managed worktree tools to the TUI** — Exposes `create_worktree`, `get_worktree_creation_status`, and `list_worktrees` via MCP for trusted local projects, with embedded and daemon session support. Enables parallel branch workflows.
3. **[#50140](https://github.com/openai/codex/pull/50140) — Use server permission catalog for TUI permission shortcuts** — Shortcuts now respect the connected server's catalog and model-specific auto-review requirements instead of local config. Fixes permission mismatches.
4. **[#50131](https://github.com/openai/codex/pull/50131) — Opt-in JSON diagnostics for TCP tunnels** — Adds `codex tcp-tunnel --diagnostics-json`, emitting versioned NDJSON on stderr with credential/address redaction. Improves remote/network debuggability.
5. **[#50129](https://github.com/openai/codex/pull/50129) — Preserve Windows environment variables for remote MCP servers** — Prevents Unix-default allowlists from filtering out Windows runtime and temp-dir variables when launching stdio MCP servers on a Windows executor.
6. **[#50128](https://github.com/openai/codex/pull/50128) — Expose the model selected for a running turn's next step** — Adds `CodexThread::current_turn_model`, decoupling in-flight model selection from future-turn settings. Useful for UI/telemetry accuracy.
7. **[#50113](https://github.com/openai/codex/pull/50113) — Native gRPC client for cloud thread resume and attach** — New reusable `codex-cloud-client` crate for `ThreadService.Resume` and live `Attach` over HTTP/2. Infrastructure for cloud-thread continuity.
8. **[#50109](https://github.com/openai/codex/pull/50109) — Keep fullscreen prompts bounded and scrollable** — Caps the fullscreen composer at two-thirds height (including padding/hints) and ensures remote image attachments leave an editable prompt row visible.
9. **[#50082](https://github.com/openai/codex/pull/50082) — Dynamic tool inheritance for fresh V2 subagents** — Subagents spawned without forked history now inherit the parent's client-defined dynamic tools (behind `multi_agent_v2_dynamic_tools`). Directly relevant to delegated/browser-tool gaps in issues above.
10. **[#50059](https://github.com/openai/codex/pull/50059) — Fix Linux sandbox startup with multiple denied files** — Bubblewrap closes the fd after each `--ro-bind-data`; the fix opens a separate `/dev/null` descriptor per file mask. Fixes a hard startup failure.

*Also landed:* [#50058](https://github.com/openai/codex/pull/50058) (`windows-sys` 0.61.2 upgrade with `OwnedHandle`), [#50087](https://github.com/openai/codex/pull/50087) (queued agent mail preserved across session eviction), [#50093](https://github.com/openai/codex/pull/50093) (instruction-provider self-delegation recursion fix), [#50066](https://github.com/openai/codex/pull/50066) (bounded Decisions transport for Guardian comparison).

## 5. Feature Request Trends

- **Session resilience & quota automation:** Auto-resume after usage-limit reset (#21073, 70 👍) is the clearest ask — turn the known reset timestamp into automatic continuation.
- **Restoring removed/regressed UI affordances:** Branch selection at session start (#49532, 45 👍), persistent user-defined tab names (#48992), and stable manual conversation titles (#50159) all point to frustration with UI churn and auto-renaming.
- **Multi-client state consistency:** Project/sidebar sync between desktop and ChatGPT web (#50161), and consistent cloud-task visibility across desktop/web/iOS/dot (#50136).
- **Better queued-input handling:** Visibly queue and preserve follow-up prompts while Codex is working in VS Code (#50139).
- **Dot/agent delegation controls:** Explicit main-chat authorization propagating to delegated executors (#50119), plus reliable dot read/create/resume of remote and cloud sessions (#50157, #50015).

## 6. Developer Pain Points

- **Windows desktop instability is the dominant theme.** Repeated renderer crashes and white screens (#48938), infinite startup spinners (#48377), logo-splash hangs (#49718, #50156), and renderer-state resets (#32917) collectively make the Windows app feel unreliable for daily work.
- **Computer Use / browser tooling fails specifically in delegated (dot) tasks.** Multiple reports (#49458, #49488, #49551, #25962, #49521) show manually created chats getting tools that dot-originated tasks on the same machine do not — including MCP startup failures and missing `node_repl js`.
- **Silent message loss erodes trust.** VS Code extension drops submitted messages with no error (#49988), and Mac app returns to the start screen mid-session (#45701).
- **Dot/cloud orchestration surfaces generic `UNKNOWN` errors.** `AppServerBackendRequestError: UNKNOWN` recurs across task creation, resume, and remote session reads (#50015, #49566, #50127, #50157, #50136), making failures hard to triage.
- **Windows sandbox/permission friction.** Non-managed permission profiles are rejected by the Windows sandbox (#49718), blocking sandboxed execution entirely for those users.
- **Model-behavior regressions on new models.** `invalid_prompt` rejections of harmless prompts on GPT-5.6 Sol / GPT-6 Astra (#47041) raise concerns for adopters of the latest models.
- **CLI/TUI edges:** Input freezes after message submission (#49033), archived subagents still listed in `/subagents` (#49085), and fullscreen composer/draft ergonomics (prompt scroll bounding, #50109) remain active polish areas.

*Overall signal:* Maintainers are actively shipping backend and platform hardening (sandbox, MCP env, permissions, worktrees, cloud gRPC), but front-end Windows stability and dot tool-binding gaps are outpacing fixes in community perception. The top-voted enhancement (#21073) has been open since May — a candidate for near-term delivery.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*