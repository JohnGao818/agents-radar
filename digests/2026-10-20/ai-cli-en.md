# AI CLI Tools Community Digest 2026-10-20

> Generated: 2026-10-20 03:11 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool AI CLI Comparison — 2026-10-20

**Data caveat:** The Claude Code digest is complete. The OpenAI Codex digest failed to generate, so Codex issue counts, PR activity, release status, feature direction, and community momentum cannot be verified. This report therefore provides a **Claude Code baseline plus explicit Codex data gaps**, not a normalized two-tool ranking.

---

## 1. Ecosystem Overview

The AI CLI landscape is shifting from raw model access toward **platform extensibility with enterprise governance** — plugins, hooks, policy ceilings, and human approval gates. Claude Code’s most engaged thread, Mods (#91870, 264 comments, 131 👍), plus `decider: "person"` and org-level tool ceilings (#99540), show extensibility being treated as a governed platform surface. At the same time, operational trust — streaming reliability, quota accounting, session continuity, and desktop/CLI parity — remains a first-order adoption blocker. The missing Codex digest prevents confirming whether these patterns are ecosystem-wide; they are validated for Claude Code and should be treated as hypotheses for Codex.

---

## 2. Activity Comparison

| Tool | Issues count | PR count | Release status | Signal |
|---|---|---|---|---|
| **Claude Code** | 10 hot issues + 4 notable issues reported in digest — **not total tracker count**. Top issue #91870: 264 comments, 131 👍 | **1 PR updated in 24h** (#99540) — not total open PRs | **v2.1.304 shipped** | High issue engagement; quiet PR day; active release cadence |
| **OpenAI Codex** | **Data unavailable** | **Data unavailable** | **Data unavailable** | Digest generation failed; absence of data is **not** evidence of zero activity |

**Comparability note:** Claude Code figures are digest-selected, not full repository totals. Codex cannot be compared without a valid digest.

---

## 3. Shared Feature Directions

**No requirement can be confirmed as shared across multiple tool communities with the supplied data**, because only Claude Code provides evidence. The following are Claude Code signals that should be validated against Codex once data is available:

| Direction | Claude Code evidence | Codex evidence | Cross-tool status |
|---|---|---|---|
| Extensibility + governance | Mods #91870; org policy ceiling over personal plugins #99540; `decider: "person"` | Unavailable | Unconfirmed |
| Streaming reliability / observability | #69336, #70217, #90005, #88900, #97593 | Unavailable | Unconfirmed |
| Cost and quota transparency | #102667 — weekly limit depleting faster | Unavailable | Unconfirmed |
| Session continuity and retrieval | #95231 remote-control sessions hidden from `/resume`; #103630 cross-machine sessions; #99836 folder grouping | Unavailable | Unconfirmed |
| Desktop/IDE parity and turn correctness | #102132 premature turn end; #101323 dictation; #100742 WSL initialization | Unavailable | Unconfirmed |
| Write-path data integrity | #94247 Gmail connector rewriting URLs | Unavailable | Unconfirmed |

---

## 4. Differentiation Analysis

Only Claude Code can be profiled from today’s data.

**Claude Code**
- **Feature focus:** Mods/plugin extensibility, hook composition transparency, enterprise policy enforcement, human-in-the-loop approval, session retrieval, Remote Control multi-device use, and Desktop turn correctness.
- **Target users:** Professional developers, platform teams, and enterprise/security administrators who need org-level policy controls over user-installed extensions.
- **Technical approach:** Policy mods with fail-closed deciding hooks; org ceilings that hold over personal plugins; explicit approval modes; plugin-hook transparency. Weaknesses are visible in streaming diagnosability, quota opacity, and documented-vs-observed hook lifetimes.

**OpenAI Codex**
- **Cannot be assessed.** No valid data on feature focus, target users, technical approach, release cadence, or community priorities.

---

## 5. Community Momentum & Maturity

**Claude Code — high momentum, mixed maturity.**
- Engagement is concentrated: #91870 alone has **264 comments and 131 👍**, far above the next issues at ~22–23 comments. This indicates a dominant roadmap thread rather than diffuse demand.
- Maintainers are posting dated micro-updates on Mods, suggesting active co-development with the community.
- Release cadence is active: **v2.1.304** shipped with enterprise-relevant approval and hook-transparency features.
- PR throughput appears quiet today — only **one PR updated in 24h** — while issue activity is high. This suggests an issue-driven and release-driven cycle, possibly with a PR review bottleneck.
- Maturity is uneven: governance primitives are shipping, but streaming reliability, cost trust, closure policy, and documentation consistency remain friction points.

**OpenAI Codex — unrated.** No activity or maturity signal is available today; it cannot be ranked against Claude Code.

---

## 6. Trend Signals

1. **Extensibility is becoming a governance battleground.** Developers should design plugin hooks with scoped lifetimes, fail-closed defaults, and clear org-over-user

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills — Community Highlights Report
**Source:** `github.com/anthropics/skills` · Data as of 2026‑10‑20

> **Data note:** The pull-request extract reports comment counts as `undefined` for all 50 PRs, so absolute discussion volume cannot be cited. The ranking below follows the repository's comment-sorted order plus observable engagement signals (update recency, linked issues, cross-referenced PRs). No PR in the top 20 is merged — every entry is **OPEN**.

---

## 1. Top Skills Ranking (most-discussed PRs)

**#1 — [#1742](https://github.com/anthropics/skills/pull/1742) `fix(mcp-builder)`: MCP ≥2 streamable HTTP client + custom headers**
Author: Kuldeeep18 · Created 2026‑09‑08 · Updated 2026‑10‑08 · **OPEN**
Repairs `skills/mcp-builder/scripts/connections.py` after `mcp>=2.0.0` renamed `streamablehttp_client` → `streamable_http_client` and moved custom headers to `create_mcp_http_client` / `http_client`. Closes #1668. **Highlights:** the most-watched submission is a *compatibility break* in the MCP builder, i.e. the ecosystem's MCP scaffolding is drifting behind upstream SDK releases. Status: open, actively revised into October.

**#2 — [#1298](https://github.com/anthropics/skills/pull/1298) `fix(skill-creator)`: isolate trigger evals, handle Windows and runtime failures**
Author: MartinCajiao · Created 2026‑06‑10 · Updated 2026‑09‑16 · **OPEN**
Fixes false-miss trigger evaluation: per-worker command probes compete with each other, `select()` on subprocess pipes fails on Windows, unrelated tools abort the scan, and runtime failures are silently scored as non-triggers — incorrectly passing negative examples. **Highlights:** the longest-running skill-creator correctness thread; it overlaps directly with issue #556 and PR #1383's findings.

**#3 — [#1245](https://github.com/anthropics/skills/pull/1245) Add `notion-spec-to-implementation` + `quantitative-resume-auditor`**
Author: mrdesouzaphd-cmyk · Created 2026‑06‑02 · Updated 2026‑10‑15 · **OPEN**
A dual submission: one skill turns Notion product/tech specs into actionable tasks with acceptance criteria and progress tracking; the other audits resumes quantitatively. **Highlights:** the highest-attention *new-Skill* PR, updated as recently as 2026‑10‑15 yet open since early June — a signal of review latency for multi-skill bundles.

**#4 — [#1771](https://github.com/anthropics/skills/pull/1771) `feat(skills)`: `proofcore-contract-auditor` for smart-contract notarization**
Author: ProofCore-Protocol · Created 2026‑09‑15 · Updated 2026‑09‑16 · **OPEN**
Static analysis of Solidity/Rust contracts, with cryptographic audit proofs anchored to the TON Blockchain via a zero-storage Merkle protocol. **Highlights:** a vendor-originated Web3 proposal — the discussion pattern here is about scope fit and external-network dependency for an official skill collection. Status: open, not revised since submission.

**#5 — [#1961](https://github.com/anthropics/skills/pull/1961) `skill-creator`: harden eval viewer (script breakout, DNS rebinding, cross-site POST, escaping)**
Author: Joncik91 · Created 2026‑10‑03 · Updated 2026‑10‑11 · **OPEN**
Closes three gaps in `generate_review.py` + `viewer.html`: script breakout via JSON embedded in page data, DNS rebinding against the localhost feedback server, and cross-site POST plus inconsistent escaping of model-written eval output. **Highlights:** the fastest-rising security PR in the set, and a direct response to issue #1394.

**#6 — [#1734](https://github.com/anthropics/skills/pull/1734) Detect orphaned docx comments**
Author: rohitjain25 · Created 2026‑09‑06 · Updated 2026‑09‑25 · **OPEN**
No body text supplied. **Highlights:** placed high in the comment sort despite an empty description — evidence that docx comment integrity is a felt pain point; the missing description itself is likely blocking review.

**#7 — [#1703](https://github.com/anthropics/skills/pull/1703) Add `md2video-audio` skill**
Author: 70v-Yoyo · Created 2026‑09‑01 · Updated 2026‑09‑15 · **OPEN**
A zero-cost pipeline compiling Markdown into MP4 with realistic voiceover: Marp renders slides, then TTS narrates (`skills/md2video-audio/SKILL.md`). **Highlights:** representative of the "content-repurposing" cluster of proposals (Markdown → slides → video).

**#8 — [#1792](https://github.com/anthropics/skills/pull/1792) `fix(docx)`: report LibreOffice timeout as an error and verify output**
Author: TINGyu123644 · Created 2026‑09‑19 · Updated 2026‑09‑25 · **OPEN**
`accept_changes.py` now returns an error when `soffice` times out instead of reporting success, and only claims success after confirming no `w:ins` / `w:del` / `w:moveFrom` / `w:moveTo` revision marks remain. **Highlights:** a silent-failure class bug — the same theme as #1298 and #1390.

---

## 2. Community Demand Trends (from Issues)

| Direction | Evidence | What the community wants |
|---|---|---|
| **Security & trust boundary of skills** | [#492](https://github.com/anthropics/skills/issues/492) (46 comments, top issue by far) | Community skills circulating under the `anthropic/` namespace impersonate official skills; users grant elevated permissions to packages they believe are first-party. Demand for namespace/naming enforcement and provenance. |
| **Team distribution & sharing** | [#228](https://github.com/anthropics/skills/issues/228) (16 comments, 👍8) | Org-wide skill libraries and shareable links instead of downloading `.skill` files and manually uploading via Settings → Capabilities. |
| **Evaluation & trigger reliability** | [#556](https://github.com/anthropics/skills/issues/556) (12 comments, 👍7), [#1383](https://github.com/anthropics/skills/issues/1383) | `claude -p` never triggers skills (0% trigger rate); benchmarks fail silently. Demand for trustworthy *meta*-tooling before more skills are added. |
| **Context/memory efficiency** | [#1329](https://github.com/anthropics/skills/issues/1329), [#1487](https://github.com/anthropics/skills/issues/1487) | A compact symbolic-notation memory skill, and fixes for `claude-api` eagerly injecting ~156k tokens in one tool call. |
| **Quality gates & governance workflows** | [#1385](https://github.com/anthropics/skills/issues/1385), [#412](https://github.com/anthropics/skills/issues/412) | Pre-task calibration → adversarial review → delivery verification pipelines; policy enforcement, threat detection, trust scoring, audit trails. |
| **Document-processing correctness** | [#2018](https://github.com/anthropics/skills/issues/2018), [#1868](https://github.com/anthropics/skills/issues/1868), [#189](https://github.com/anthropics/skills/issues/189) | docx namespace corruption, off-by-one gradient interpolation, duplicate plugin content in context. Not new features — *reliability* of shipped skills. |

**Reading:** demand has shifted from "more skills" to "make the skill layer safe, shareable, and verifiable." The top four issue threads are all infrastructure (trust, distribution, evaluation, context cost), not skill ideas.

---

## 3. High-Potential Pending Skills

Ranked by recency of activity — these are most likely to move:

- **[#1997](https://github.com/anthropics/skills/pull/1997)** `fix(skill-creator)`: parse YAML frontmatter scalars correctly — updated **2026‑10‑19** (most recent activity in the set). Fixes quote-stripping that corrupts descriptions such as `Use for requests like "review my draft."`, which then skews eval and description optimization.
- **[#1977](https://github.com/anthropics/skills/pull/1977)** `algorithmic-art`: `wrapAround()` now actually wraps (modulo handles negatives, stays in `[0, max)`); fixes #1897 — updated 2026‑10‑18.
- **[#1976](https://github.com/anthropics/skills/pull/1976)** `webapp-testing`: report `textarea`/`select` correctly in `element_discovery.py`; the `'text'` fallback now applies only to `input`; fixes #1891 — updated 2026‑10‑18. (Same author as #1977 — a small, reviewable pair.)
- **[#2040](https://github.com/anthropics/skills/pull/2040)** New `architecture-advisor` skill: pattern selection with written justification; companion to #2039, part of the MIT-licensed "harness" SDD suite — created/updated 2026‑10‑16, newest *new-skill* submission.
- **[#1245](https://github.com/anthropics/skills/pull/1245)** `notion-spec-to-implementation` + `quantitative-resume-auditor` — updated 2026‑10‑15; the highest-visibility unmerged new skill.
- **[#1961](https://github.com/anthropics/skills/pull/1961)** skill-creator eval-viewer hardening — updated 2026‑10‑11; security fixes tend to merge ahead of feature proposals.

*Lower probability:* [#1771](https://github.com/anthropics/skills/pull/1771) (vendor-anchored Web3), [#1734](https://github.com/anthropics/skills/pull/1734) (no description), [#514](https://github.com/anthropics/skills/pull/514) (document-typography, stale since 2026‑03‑13).

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is not new capabilities but reliability and trust in the skill layer itself — top threads cluster on official-namespace spoofing (#492), team distribution (#228), broken trigger evaluation (#556), and silent failures/OOM in shipped skills — with the PR queue dominated by corrective patches rather than new Skills.**

*Caveat: `Comments` was `undefined` across all PR records, so "most-watched" here reflects repository sort order and update recency, not verified comment counts.*

---

# Claude Code Community Digest — 2026-10-20

## 1. Today's Highlights

Release v2.1.304 lands with plugin-hook transparency and a new `decider: "person"` approval mode for mods, both of which signal that the **Mods extensibility work (#91870) is now the dominant roadmap thread** — 264 comments and 131 👍 make it by far the most-engaged issue in the tracker. Meanwhile, the loudest operational signal is **streaming reliability**: multiple independent reports of mid-stream API disconnects now span macOS, Linux, and Windows, with one macOS user logging 291 failures in seven days.

---

## 2. Releases

**v2.1.304**
- Added a transcript line when a plugin that runs first skips one of your mod's hooks, naming the event and the plugin — improves debuggability of hook composition order.
- Added `decider: "person"` to a mod's `tool.check` answer: only the permission dialog or a host's callback can approve the ask, otherwise it is refused. This is enterprise-relevant, granting policy mods a hard human-in-the-loop gate rather than a model-decided approval.

---

## 3. Hot Issues

1. **[#91870] Mods — make Claude 10x more extensible** (264 comments, 131 👍) — The center of gravity for the whole project right now. Maintainers are posting dated micro-updates ("we're live", "shipping in N weeks"), indicating active co-development with the community: https://github.com/anthropics/claude-code/issues/91870
2. **[#69336] Connection closed mid-response, immediately in a new context window** (Linux, 22 comments, 24 👍) — The highest-upvoted reliability bug; repro conditions are tight enough to look like a server-side or SDK-level defect rather than a flaky network: https://github.com/anthropics/claude-code/issues/69336
3. **[#70217] API Error: Connection closed mid-response** (macOS, 23 comments, 16 👍) — Brother issue to the above and explicitly flagged as costing "real time and money." Long-lived since June with no resolution: https://github.com/anthropics/claude-code/issues/70217
4. **[#102132] Desktop Code tab: next-step box can end the turn before the reply is written** (Windows, 16 comments, 22 👍) — A correctness bug in the new `wrap_up` turn tool: the UI renders the ask/actions box and the assistant's message never arrives. High upvote-to-comment ratio suggests broad silent agreement: https://github.com/anthropics/claude-code/issues/102132
5. **[#102157] "Group by → Project" removed from sessions sidebar** (13 comments, 11 👍, closed **invalid**) — A visible regression closed without a restoration path; the "invalid" label on a widely-reproduced UX loss is itself generating friction: https://github.com/anthropics/claude-code/issues/102157
6. **[#90005] "The response stopped arriving" — 33 times in one day, zero on any prior day** (Windows, 7 comments) — Notable for arriving immediately after an auto-update (2.1.227 → 2.1.246) and for the error providing no attribution to diagnose: https://github.com/anthropics/claude-code/issues/90005
7. **[#102667] Possible usage accounting regression: weekly limit depletes much faster** (3 comments, 2 👍) — Claims 5-hour windows now consume far more of the weekly quota for identical usage. Low volume, high blast radius — cost trust is the most expensive thing to lose: https://github.com/anthropics/claude-code/issues/102667
8. **[#94247] Gmail connector rewrites URLs in message bodies into google.com/url redirects** (7 comments, 5 👍, has repro) — Silent data mutation on write. Small scope, but the failure mode (content corruption in outbound mail) is severe: https://github.com/anthropics/claude-code/issues/94247
9. **[#95231] Remote Control sessions hidden from local `/resume` picker** (5 comments, 3 👍) — `claude rc` sessions are persisted locally but filtered out as `entrypoint=sdk-cli`, which breaks the mental model of "local transcript = resumable": https://github.com/anthropics/claude-code/issues/95231
10. **[#102858] Hooks in command/skill frontmatter stop firing after the skill's own turn** (1 comment) — Direct contradiction between documented "rest of the session" behavior and observed behavior; pairs with [#89669](https://github.com/anthropics/claude-code/issues/89669) requesting properly scoped skill hooks: https://github.com/anthropics/claude-code/issues/102858

*Also worth tracking:* [#96942](https://github.com/anthropics/claude-code/issues/96942) Windows update deadlock via single-instance lock; [#96492](https://github.com/anthropics/claude-code/issues/96492) `bashEditDiff` forcing `git status` on every Bash call; [#99489](https://github.com/anthropics/claude-code/issues/99489) iOS effort picker reverting Ultracode → Extra; [#103624](https://github.com/anthropics/claude-code/issues/103624) orchestrator over-prompting for permissions.

---

## 4. Key PR Progress

Only **one** PR was updated in the 24h window, so this section is a single item rather than a top-10 — a quiet PR day, with activity concentrated in Issues.

**[#99540] sec-default: an organization's ceiling on a tool holds over the plugins a person installs** (OPEN, updated 2026-10-19) — Extends policy-mod enforcement so that an org-mandated approval requirement for a connector's tool cannot be escaped by installing a personal plugin. Every deciding hook in the policy mod carries a `.catch`, so a thrown hook fails closed rather than silently granting. This is the governance half of the Mods initiative and pairs directly with the new `decider: "person"` primitive in v2.1.304: https://github.com/anthropics/claude-code/pull/99540

---

## 5. Feature Request Trends

- **Extensibility with governance (dominant):** Mods/plugins (#91870), org-level tool ceilings over user-installed plugins (#99540), and precise hook lifetimes — per-skill scoping rather than "rest of session" (#89669, #102858).
- **Session organization and retrieval:** grouping by actual folder rather than repo (#99836), restoring "Group by → Project" (#102157), and surfacing Remote Control sessions in `/resume` (#95231).
- **Cross-device continuity:** sessions from another machine disappearing from the sidebar (#103630) and iOS/Mac effort-state divergence (#99489) — Remote Control is being used as a multi-device product and the sync semantics lag behind.
- **Conversation control in the IDE:** in-place rewind without forking (#96694); predictable turn boundaries on Desktop (#102132).
- **Desktop input/UX parity:** live dictation transcripts (#101323), WSL skills and Files/Git panels loading before session start (#100742).

---

## 6. Developer Pain Points

1. **Streaming reliability is the top complaint, full stop.** Five separate high-signal issues describe the same class of failure with different triggers: mid-stream connection close ([#70217](https://github.com/anthropics/claude-code/issues/70217), [#69336](https://github.com/anthropics/claude-code/issues/69336)), post-update "response stopped arriving" ([#90005](https://github.com/anthropics/claude-code/issues/90005)), 0.5–2.7 KB stalls hitting the 180s byte-watchdog ([#88900](https://github.com/anthropics/claude-code/issues/88900)), and an EPIPE loop pinning a core at 100% after macOS content-filter changes ([#97593](https://github.com/anthropics/claude-code/issues/97593)). Errors carry no attribution, so users cannot distinguish their network from Anthropic's infrastructure — that diagnosability gap is as damaging as the drops themselves.
2. **Cost and quota opacity.** Fast-depleting weekly limits (#102667) land on top of retry-heavy sessions, so failures are billed twice: in time and in quota.
3. **Desktop app instability and update mechanics.** Update deadlocks (#96942), auto-archiving on PR merge (#91607), unclosable side chats (#103631), and WSL initialization gaps (#100742) make the Desktop surface feel less trustworthy than the CLI.
4. **Permission friction and agent reliability.** #103624 ("orchestrator does nothing, asks constantly") and #103286 (context compression degrading coordinator memory) point at the same underlying concern: long-running multi-agent sessions are still hard to keep coherent and unblocked.
5. **Closure policy eroding trust.** Bugs closed as `invalid` (#102157) or `stale` (#59018, a security-relevant backdoor/noop report) without a visible resolution path — and hooks behaving contrary to documentation (#102858) — push users toward re-filing rather than engaging.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

⚠️ Summary generation failed.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*