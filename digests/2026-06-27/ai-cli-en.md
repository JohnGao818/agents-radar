# AI CLI Tools Community Digest 2026-06-27

> Generated: 2026-06-27 02:46 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: Claude Code vs OpenAI Codex

**Date:** 2026-06-27  
**Prepared for:** Technical decision-makers and AI developer tool strategists

---

## 1. Ecosystem Overview

The AI CLI tools landscape remains highly dynamic, with both Anthropic’s Claude Code and OpenAI’s Codex releasing updates this week while grappling with significant community feedback on cost, reliability, and cross-platform parity. Claude Code’s community is most vocal about model instability (Opus 4.8 tool-call malformation and disappearing 1M context windows) and billing friction, while Codex users are pressed by a dramatic rate-limit cost spike and resource leaks. Both ecosystems show strong developer engagement but differ in their focus—Claude Code leans deeper into agent orchestration and cowork features, whereas Codex prioritizes rate-limit transparency, plugin ecosystem enforcement, and broad platform support. The overall trend is one of rapid iteration with growing pains around maturity and trust.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Latest Release** | v2.1.195 (stable patch) | rust-v0.142.3 (maintenance) + alpha v0.143.0-alpha.26 |
| **Top Issue Engagement** | #5088 – 177 comments, 58 👍 (account disabled after payment) | #28879 – 175 comments, 326 👍 (rate-limit cost 10–20× jump) |
| **Hot Issues Tracked** | 10 (listed by community impact) | 10 (listed by community impact) |
| **PR Activity (last 24h / tracked)** | 2 PRs (1 trivial, 1 docs) | 10 PRs (multiple code-reviewed, open, and closed) |
| **Release Type** | Single stable release | Maintenance patch + alpha prerelease |

**Key observations:**  
- Both tools have similar comment volume on their top issues, but Codex’s top issue received 5.6× more upvotes, indicating broader consensus on the priority of rate-limit transparency.  
- Codex shows significantly higher PR throughput (10 vs 2), though this may reflect a longer reporting window or a more active development sprint. Claude’s PR count was explicitly for the last 24 hours; Codex’s list was “10 important” without a strict time constraint.  
- Claude shipped a single stable patch; Codex shipped both a maintenance release and an alpha, suggesting a faster iteration pace with higher risk tolerance.

---

## 3. Shared Feature Directions

The following requirements appear across both tool communities, suggesting industry-wide gaps:

- **Cost transparency and billing reliability**  
  - Claude Code: #5088 – account disabled immediately after Max plan payment; #71729 – conversation history lost on restart (indirectly causes data loss).  
  - Codex: #28879 – rate-limit cost jumped 10–20×; #30212 – 5-hour allowance consumed in ~1 hour.  
  *Users cannot trust displayed budgets or payment flows; both tools need clearer billing instrumentation and predictable consumption.*

- **Memory and context management**  
  - Claude: #65585 – auto-compact broken for third-party providers; #36351, #68287 – 1M context window missing.  
  - Codex: #30299 – request for official CLI commands to inspect, prune, and manage `codex_memory` files.  
  *Both communities want explicit control over context window size, compression behavior, and memory lifecycle.*

- **Cross-platform stability**  
  - Claude: #39636 – Cowork broken on ARM64 Snapdragon X; #70684 – SOCKS5 proxy breaks SSH git on macOS.  
  - Codex: #29000 – SIGTRAP crash on Intel macOS; #29070 – terminal read fails on Windows.  
  *Platform-specific bugs remain a major friction point, especially for ARM64 and Windows users.*

- **Resource leak and data loss prevention**  
  - Claude: #71729 – Desktop conversation history silently lost; #69691 – sub-agent sync/async inconsistent.  
  - Codex: #26984 – MCP stdio fd/process leaks; #27536 – code_sign_clone temp directory grows unbounded.  
  *Reliability concerns—lost work, file descriptor exhaustion, orphan processes—are top-of-mind for production usage.*

- **Plugin / MCP ecosystem maturation**  
  - Claude: #71711 – Gmail connector invisible in CLI; #71675 – MCP auth prompts offer no options.  
  - Codex: #26984 – MCP stdio leaks; #29691 – plugin marketplace source enforcement; #30297 – enabling remote plugins by default.  
  *Both platforms are pushing plugin ecosystems but face integration stability, authentication friction, and trust issues.*

- **Background and remote capabilities**  
  - Claude: #71731 – request for remote session without local access; #69691 – sub-agent sync control.  
  - Codex: #29922 – request for a `monitor` tool to wake Codex on background events (logs, CI).  
  *Developers increasingly need asynchronous, CI-friendly workflows that do not require a persistent local terminal.*

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|-----------|-------------|--------------|
| **Primary user persona** | Agent orchestration & cowork users (multiple sub-agents, sandbox, browser extension) | Rate-limit sensitive developers, plugin/skill ecosystem adopters, Windows/Intel Mac users |
| **Model focus** | Opus 4.8 with 1M context; strong emphasis on tool-use reliability | GPT-5.5 and custom models; performance regressions around rate limits |
| **Feature emphasis** | Agent collaboration (cowork, sub-agents), desktop/CLI parity, sandbox networking | Rate-limit management, plugin marketplace enforcement, remote control, memory management |
| **Community pain points** | Billing account lock, model regression (tool_use malformed), context window missing, ARM64 incompatibility | Cost transparency (10–20× increase), resource leaks (fd, temp files), platform-specific crashes |
| **Release strategy** | Conservative stable releases with occasional hotfixes; alpha/experimental appears less publicly | Frequent patch + alpha dual-track; higher PR throughput suggests faster iteration |
| **Tool-surface parity** | Desktop app lags CLI in steering and context window options (multiple issues) | Desktop app has bugs (double-send, no image on clipboard) but fewer parity gaps reported |

**Key differentiators:**  
- Claude Code’s community is more narrowly focused on agent interactions (cowork, sub-agent sync/async, sandbox proxy), while Codex’s concerns center on cost, memory leaks, and platform fragmentation.  
- Codex’s top issue (326 👍) has far greater consensus than Claude’s top issue (58 👍), suggesting a more united user base on priorities.  
- Codex has higher PR activity and an explicit alpha track, indicating a higher risk tolerance for new features; Claude appears to prioritize stability but suffers from regressions (e.g., auto-compact, proxy).  
- Claude’s desktop ↔ CLI parity issues are a recurring theme; Codex’s desktop issues are more about input handling and resource cleanup.

---

## 5. Community Momentum & Maturity

- **Claude Code:** Highly engaged community with many duplicate and overlapping issues (e.g., four separate reports on missing 1M context). The top issue (#5088) has 177 comments but only 58 upvotes, suggesting fragmented attention rather than unified demand. A strong presence of “regression” tagged issues indicates a user base that values stability but is experiencing frequent breakage. The volume of ARM64/cowork blockers and billing lockouts suggests a significant portion of users are in production and feeling pain.

- **OpenAI Codex:** Community momentum is higher in terms of upvote concentration (326 on #28879) and PR activity (10 important PRs). The rate-limit cost spike has unified a broad segment of users. However, the presence of multiple platform-specific issues (Intel Mac, Windows terminal, WSL) indicates a diverse user base that feels underserved. The closed issue #29000 (SIGTRAP) without resolution details suggests transparency could improve.

- **Maturity assessment:** Neither tool is fully mature. Both have regressions, resource leaks, and billing friction. Codex appears to iterate faster (alpha releases, more PRs) but with more unpredictable cost impact. Claude appears more conservative but suffers from regressions that erode trust. Developer decision-makers should evaluate based on their need for stability (Claude may be slightly ahead) vs. feature velocity (Codex leads).

---

## 6. Trend Signals

The following industry trends emerge from cross-tool community feedback:

1. **Cost predictability is the #1 developer concern**  
   Both tools have billing anomalies that undermine trust. Expect increased demand for granular cost logging, real-time budget alerts, and consumption-based pricing transparency.

2. **Cross-platform support is still an aftermarket**  
   ARM64 (Snapdragon X), Intel Mac, and Windows continue to see second-class treatment. As AI tool usage expands beyond macOS, platforms like Windows and ARM64 will become critical differentiators.

3. **Model quality regressions eclipse feature velocity**  
   Users prefer a stable model (Claude Opus 4.7 vs 4.8; Codex GPT-5.5 crashes) over new capabilities. Both communities signal that model reliability must be a release gate.

4. **Memory and context management is the next frontier**  
   Auto-compact, 1M context windows, and explicit memory CLI commands are not luxuries—they are requirements for long-running, production-grade agent workflows.

5. **Plugin/MCP ecosystem needs standardization**  
   Authentication, sandbox integration, and resource leaks are common across both tools. A shared standard (e.g., MCP spec) would benefit the entire industry.

6. **Background and remote workflows are emerging as must-haves**  
   Users want to trigger AI actions from CI/CD, monitor logs, and run cowork sessions without local presence. This will

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report based on the data provided.

---

## Claude Code Skills Community Highlights Report

**Data Snapshot:** 2026-06-27 | **Source:** [github.com/anthropics/skills](https://github.com/anthropics/skills)

---

### 1. Top Skills Ranking

The following pull requests have attracted the most community discussion and represent the most-watched Skills or critical fixes within the repository.

**#1 – [#1298: fix(skill-creator): run_eval.py always reports 0% recall](https://github.com/anthropics/skills/pull/1298)**
- **Functionality:** Fixes the core evaluation script `run_eval.py`, which prints `recall=0%` for every skill description regardless of content. The fix installs the eval artifact as a real skill, corrects Windows stream reading, trigger detection, and parallel workers.
- **Discussion Highlights:** Identified as a blocker for the entire description-optimization loop (`run_loop.py`). The community has produced "10+ independent reproductions" of the bug (see Issue #556). This PR is a comprehensive response to a deeply felt pain point.
- **Status:** Open (Updated 2026-06-23)

**#2 – [#514: Add document-typography skill](https://github.com/anthropics/skills/pull/514)**
- **Functionality:** Prevents typographic defects in AI-generated documents: orphaned word wrap, widowed section headers, and numbering misalignment. Designed to be a universal downstream polish for every document Claude generates.
- **Discussion Highlights:** The highly specific, universally applicable problem it solves has resonated widely. Community feedback focused on the value of "invisible" quality improvements in production output.
- **Status:** Open (Updated 2026-03-13)

**#3 – [#486: Add ODT skill](https://github.com/anthropics/skills/pull/486)**
- **Functionality:** Enables creation, filling, reading, and conversion of OpenDocument Format files (.odt, .ods). Covers LibreOffice document workflows, template filling, and HTML conversion.
- **Discussion Highlights:** Demonstration of strong demand for enterprise and open-source document format support. Conversation centered on LibreOffice interoperability and edge cases in template filling.
- **Status:** Open (Updated 2026-04-14)

**#4 – [#210: Improve frontend-design skill clarity and actionability](https://github.com/anthropics/skills/pull/210)**
- **Functionality:** A structural revision of the existing frontend-design skill, ensuring every instruction is actionable within a single conversation and steering Claude behavior with specific, non-generic guidance.
- **Discussion Highlights:** The debate around "how prescriptive should a Skill be" vs. "how much creative freedom should Claude retain" played out here. A benchmark PR for Skill design philosophy.
- **Status:** Open (Updated 2026-03-07)

**#5 – [#83: Add skill-quality-analyzer and skill-security-analyzer](https://github.com/anthropics/skills/pull/83)**
- **Functionality:** Two meta-skills for evaluating other Skills across quality dimensions (structure, documentation, examples) and security posture (privilege escalation, data exfiltration risks, prompt injection).
- **Discussion Highlights:** The first serious attempt at establishing a quality and security assurance framework inside the ecosystem. Generated significant interest in community standards and governance.
- **Status:** Open (Updated 2026-01-07)

**#6 – [#723: Add testing-patterns skill](https://github.com/anthropics/skills/pull/723)**
- **Functionality:** A comprehensive testing stack covering unit testing (AAA pattern, naming, edge cases), React component testing with Testing Library, integration testing, and E2E patterns. Teaches Claude the "Testing Trophy" model.
- **Discussion Highlights:** Highly praised for its breadth and practical structure. Noted as a skill that could change how Claude approaches test generation across projects.
- **Status:** Open (Updated 2026-04-21)

**#7 – [#360: Added AppDeploy skill](https://github.com/anthropics/skills/pull/360)**
- **Functionality:** Enables Claude to deploy and manage full-stack web applications using the AppDeploy platform, including lifecycle management (status, versions, rollbacks).
- **Discussion Highlights:** Signals growing demand for "Claude as operator" – moving beyond code generation to actual infrastructure management.
- **Status:** Open (Updated 2026-05-04)

---

### 2. Community Demand Trends

The Issues board reveals several concentrated demand vectors:

- **Security & Trust Boundaries:** Issue [#492](https://github.com/anthropics/skills/issues/492) (21 comments, top-voted) exposes a critical vulnerability: community skills distributed under the `anthropic/` namespace can impersonate official skills, enabling trust boundary abuse. This has become the community's most urgent governance conversation. Related concerns surface in [#1175](https://github.com/anthropics/skills/issues/1175) regarding SharePoint access control logic in SKILL.md files.
- **Organizational Sharing & Collaboration:** Issue [#228](https://github.com/anthropics/skills/issues/228) (14 comments) requests org-wide skill sharing without manual file transfer. This points to a need for enterprise-grade distribution mechanisms.
- **Tooling Reliability & Windows Support:** The cluster of Windows compatibility bugs ([#1061](https://github.com/anthropics/skills/issues/1061)) and the broken `run_eval` evaluation loop ([#556](https://github.com/anthropics/skills/issues/556), [#1169](https://github.com/anthropics/skills/issues/1169)) dominate developer experience concerns. The community is demanding a stable, cross-platform development toolchain.
- **New Capabilities in Demand:** Proposals for a compact-memory skill using symbolic notation ([#1329](https://github.com/anthropics/skills/issues/1329)) and an agent-governance safety skill ([#412](https://github.com/anthropics/skills/issues/412)) indicate interest in making Claude retain state more efficiently and operate within safety guardrails.
- **Duplicate Skill Ecosystem:** Issue [#189](https://github.com/anthropics/skills/issues/189) highlights that `document-skills` and `example-skills` plugins contain identical content, causing duplicates. The community is asking for better curation and deduplication in the official collection.

---

### 3. High-Potential Pending Skills

These open PRs have active discussion threads and address critical gaps. They are strong candidates for merging in the near term.

- **[#1298 – run_eval.py 0% recall fix](https://github.com/anthropics/skills/pull/1298)** – The highest-attention PR in the repository. If merged, it would unblock the entire skill-development feedback loop. Multiple reviewers and testers have engaged.
- **[#1323 – run_eval trigger detection fix](https://github.com/anthropics/skills/pull/1323)** – A complementary fix to #1298, addressing a second cause of `recall=0%` (failing to detect real skill names and bailing on non-skill tools). Combined with #1298, these two PRs would resolve the most painful developer experience issue.
- **[#723 – testing-patterns skill](https://github.com/anthropics/skills/pull/723)** – Fully fleshed out, well-structured, addressing a clear gap in the official collection. Poised to land as a major new capability.
- **[#541 – docx tracked change fix](https://github.com/anthropics/skills/pull/541)** – Fixes document corruption from `w:id` collisions. A precise, low-risk fix for a high-impact bug in the existing DOCX skill.
- **[#360 – AppDeploy skill](https://github.com/anthropics/skills/pull/360)** – First-class deployment skill with a working external service integration. Demonstrates path for third-party tool integration in the skills ecosystem.

---

### 4. Skills Ecosystem Insight

The community’s most concentrated demand is for **reliable, well-governed developer tooling**—the highest-attention PRs and issues are overwhelmingly about fixing `run_eval.py` , ensuring cross-platform (especially Windows) compatibility, and establishing security trust boundaries, revealing that the ecosystem's top priority is stabilizing the skill-creation pipeline itself before scaling the number of available skills.

---

# Claude Code Community Digest — 2026-06-27

## Today's Highlights

Anthropic shipped **v2.1.195** with a new env var to disable mouse interactions in fullscreen mode and a breaking fix for hook matcher substring matching. The most heated community topic remains **Issue #5088** (177 comments) — users having their account disabled immediately after paying for the Max 5x plan. Multiple bug reports about **Opus 4.8’s 1M context window missing** from model pickers and **Cowork failing on ARM64 (Snapdragon X)** continue to draw attention.

## Releases

### [v2.1.195](https://github.com/anthropics/claude-code/releases/tag/v2.1.195) (latest)

- Added `CLAUDE_CODE_DISABLE_MOUSE_CLICKS` environment variable to disable mouse click/drag/hover in fullscreen mode while preserving wheel scroll.
- Fixed hook matchers with hyphenated identifiers (e.g., `code-reviewer`, `mcp__brave-search`) — they now use exact matching instead of substring matching.

## Hot Issues (top 10 by community impact)

1. **[#5088](https://github.com/anthropics/claude-code/issues/5088) — Claude Account Disabled After Payment for Max 5x Plan**  
   *177 comments, 58 👍* | *Bug, area:cost, area:auth*  
   User paid for renewal and immediately lost access to both Claude Code and Claude.ai. Widespread frustration; no official resolution yet (oncall labeled). This is the highest-traffic issue currently open.

2. **[#39636](https://github.com/anthropics/claude-code/issues/39636) — Cowork VM guest kernel never boots on Snapdragon X Plus (ARM64)**  
   *31 comments, 9 👍* | *Bug, platform:windows, area:cowork*  
   Connection timeout on every attempt to start a cowork session on ARM64 Windows hardware. Duplicate reports (#50674 with 30 comments) confirm the problem is widespread.

3. **[#36351](https://github.com/anthropics/claude-code/issues/36351) — 1M context window removed from Desktop Code tab model picker after v1.1.7714**  
   *17 comments, 11 👍* | *Bug, platform:windows, area:model, area:desktop*  
   Max plan users report that after updating, only 256k context options appear. Upvoted heavily, suggesting many are affected.

4. **[#63604](https://github.com/anthropics/claude-code/issues/63604) — Opus 4.8 repeatedly emits malformed tool_use blocks, entire response discarded**  
   *11 comments, 14 👍* | *Bug, platform:windows, area:model, api:anthropic*  
   Opus 4.8 responses are thrown away due to malformed tool calls. 4.7 works fine — a regression affecting users who rely on tool use in production.

5. **[#40173](https://github.com/anthropics/claude-code/issues/40173) — Claude-in-Chrome: Server-side domain blocking breaks business automation**  
   *11 comments, 7 👍* | *Enhancement, platform:macos, area:browser-extension, area:chrome*  
   Extension blocks financial sites (Wells Fargo, Schwab) with no override. Users want per-domain whitelisting.

6. **[#65585](https://github.com/anthropics/claude-code/issues/65585) — Auto-compact stopped working for third-party API providers since v2.1.161**  
   *6 comments, 4 👍* | *Bug, has repro, platform:macos, area:core, regression*  
   Auto-compact (context compression) is broken for users with third-party providers. Regression confirmed with reproduction steps.

7. **[#68287](https://github.com/anthropics/claude-code/issues/68287) — Max plan: Opus 4.8 only shows 256k context, 1M option missing in model picker**  
   *6 comments, 1 👍* | *Bug, platform:windows, area:model*  
   Another instance of the 1M context window vanishing. Likely same root cause as #36351 but different platform (Windows).

8. **[#71729](https://github.com/anthropics/claude-code/issues/71729) — Desktop `</> Code` conversation history silently lost on restart**  
   *6 comments, 0 👍* | *Bug, platform:windows, area:desktop*  
   Messages disappear after closing and reopening Claude Desktop. Claude does not detect the gap — a data-loss issue for Desktop users.

9. **[#69691](https://github.com/anthropics/claude-code/issues/69691) — Sub-agent sync-vs-async is session-host-dependent; `run_in_background:false` not reliably honored**  
   *4 comments, 0 👍* | *Bug, area:agents*  
   No documented way to force synchronous sub-agent execution. Behavior differs between sessions, causing unpredictable task orchestration.

10. **[#70684](https://github.com/anthropics/claude-code/issues/70684) — Sandbox SOCKS5 proxy requires authentication that BSD nc cannot negotiate, breaking SSH git**  
    *3 comments, 12 👍* | *Bug, has repro, platform:macos, regression, area:sandbox*  
    High 👍/comment ratio. Sandbox mode injects `GIT_SSH_COMMAND` with a proxy authentication method not supported by macOS’s `nc`, breaking all SSH git operations. Regression from a previous sandbox update.

## Key PR Progress (2 PRs in last 24h)

1. **[#71530](https://github.com/anthropics/claude-code/pull/71530) — Merge pull request #1 from anthropics/main**  
   Trivial merge from main.

2. **[#71627](https://github.com/anthropics/claude-code/pull/71627) — docs(sandbox): note that prompt-approved hosts are session-scoped**  
   Adds a bullet to `examples/settings/README.md` clarifying that `sandbox.network.allowedDomains` entries added via prompt-time approval are lost on restart. Small but useful documentation fix for sandbox users.

## Feature Request Trends

- **Context window flexibility**: Users consistently ask that the 1M context option be restored and made available consistently across platforms and models. Several issues (#36351, #68287, #69109, #69444) all point to this as a top concern.
- **Desktop ↔ CLI parity**: The Desktop app’s Code tab lacks mid-task message injection (“steering”) that CLI has (#71726), and copy-link on file references yields dead URLs (#67490). Users want Desktop to match CLI behavior.
- **Remote control**: A new request (#71731) asks for the ability to enable remote sessions without physical local access — important for users running multiple workspaces away from their machine.
- **Customization in voice/interface**: #71721 requests custom vocabulary for voice dictation (technical acronyms, accent handling). #66117 asks for the ability to disable prompt suggestions entirely.
- **Co-working / Cowork**: Multiple issues (#39636, #50674) highlight desire for functional Cowork on ARM64 Windows hardware, a blocker for users with Snapdragon X machines.

## Developer Pain Points

1. **Opus 4.8 instability**: Malformed tool_use blocks (#63604) and the disappearing 1M context window (#36351, #68287, #69109) erode trust in the latest model.
2. **ARM64 / Snapdragon X incompatibility**: Cowork is completely broken (#39636, #50674). No workaround known.
3. **Account / billing friction**: Payment triggers account lock (#5088) with no clear resolution path; high anxiety for users relying on Claude Code for daily work.
4. **Data loss risks**: Conversation history lost on restart (#71729), sub-agent behavior inconsistent (#69691), and sandbox proxy failures (#70684) — all can lead to lost work.
5. **Auto-compact regression**: Third-party API users lose context compression (#65585), driving up token costs for heavy users.
6. **Plugin & environment portability**: Hardcoded absolute paths in plugins break across Linux/WSL (#31388). VS Code integrated terminal gets “saturated” 503 errors while native Terminal works (#71683) — mysterious environment-specific failures.
7. **MCP connector friction**: Gmail connector doesn’t surface in CLI while Calendar/Drive work (#71711); authentication prompts for MCP servers offer no listed options (#71675).

These pain points suggest the community is eager for a stable, cross-platform experience with reliable model behavior and predictable billing. The volume of reports around Opus 4.8 and the 1M context window is unusually high — expect Anthropic to prioritize fixes there.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-27

## Today’s Highlights
A major **rate-limit cost jump** (Issue #28879) is the top community concern, with 175 comments and 326 upvotes reporting a 10–20× increase in per-token cost eating Plus budgets in 2–3 prompts. Two minor releases landed: a maintenance patch (`rust-v0.142.3`) with no user-facing changes, and an alpha (`rust-v0.143.0-alpha.26`). A **SIGTRAP crash on Intel macOS** (Issue #29000) was also closed after 16 comments.

## Releases
- **rust-v0.142.3** – Maintenance-only patch; no user-facing changes since 0.142.2. [Full Changelog](https://github.com/openai/codex/compare/rust-v0.142.2...rust-v0.142.3)
- **rust-v0.143.0-alpha.26** – Pre-release alpha; no changelog details provided.

## Hot Issues (10 noteworthy)
1. **[#28879 – Rate-limit cost per token jumped ~10-20x since June 16](https://github.com/openai/codex/issues/28879)** – Open, 175 comments, 326 👍. The top-voted issue on the repo. Users on Plus plan report budget draining in 2–3 prompts vs. 20+ previously. Logs show `limit-% consumed per token` increased drastically. Community reaction is strong, with many users sharing similar logs and workarounds.
2. **[#29000 – CLI 0.141.0 crashes with SIGTRAP on Intel macOS](https://github.com/openai/codex/issues/29000)** – Closed, 16 comments, 11 👍. Crash on Darwin x86_64 when using `gpt-5.5`. Likely a CPU architecture bug; closed without resolution details.
3. **[#30224 – "This model is not supported" with X-OpenAI-Internal-Codex-Responses-Lite](https://github.com/openai/codex/issues/30224)** – Open, 12 comments. API returns error when using internal header with custom models on Windows. Community seeks workaround.
4. **[#27536 – code_sign_clone grows unbounded (62 GB+) on macOS](https://github.com/openai/codex/issues/27536)** – Closed, 10 comments. Desktop app (Electron) accumulates huge temp directories across auto-updates. Finally addressed after weeks.
5. **[#18357 – Upgraded to PRO but "You’re out of Codex messages"](https://github.com/openai/codex/issues/18357)** – Open, 9 comments, 5 👍. Persistent issue: PRO subscribers see "out of messages" despite having quota. No resolution yet.
6. **[#26984 – MCP stdio servers leak pipe fds + orphan processes → EMFILE](https://github.com/openai/codex/issues/26984)** – Open, 6 comments. File descriptor leak in CLI, cumulative over long sessions. Affects Pro users on Linux/macOS.
7. **[#19529 – Pressing Enter occasionally sends same message 2-3 times](https://github.com/openai/codex/issues/19529)** – Open, 6 comments. Desktop-only double-send bug, confirmed not hardware. Intermittent and frustrating.
8. **[#30212 – 5-hour allowance consumed in about 1 hour](https://github.com/openai/codex/issues/30212)** – Open, 6 comments, 8 👍. Another rate-limit anomaly: Pro user with 20x allowance sees abnormal depletion. Related to #28879.
9. **[#29632 – Unable to send message on Windows 11](https://github.com/openai/codex/issues/29632)** – Open, 5 comments. Simple messages fail with no clear error; connectivity or sandbox issue.
10. **[#29070 – Codex App could not read terminal on Windows](https://github.com/openai/codex/issues/29070)** – Open, 5 comments. Tool-call fail due to terminal read errors in Windows app.

## Key PR Progress (10 important)
1. **[#30327 – core: persist unmatched call output repairs](https://github.com/openai/codex/pull/30327)** – Code-reviewed. Fixes a gap where `ContextManager::for_prompt` synthesized aborted outputs without permanent storage, breaking conversation identity.
2. **[#30325 – Read faster model from safety buffering events](https://github.com/openai/codex/pull/30325)** – Open. Adds support for `safety_buffering.faster_model` field from Responses WebSocket, enabling faster model selection for third-party traffic.
3. **[#29691 – [plugins] Enforce marketplace source policy at runtime](https://github.com/openai/codex/pull/29691)** – Code-reviewed. Blocks inactive plugins violating enterprise source policy. Filters discovery and reporting.
4. **[#30297 – [codex] Enable remote plugins by default](https://github.com/openai/codex/pull/30297)** – Open. Promotes remote plugin feature to stable; preserves opt-out override.
5. **[#30315 – [codex] Add generated token auth to app-server WebSockets](https://github.com/openai/codex/pull/30315)** – Open. Generates 256-bit connection tokens for WebSockets; adds `--no-token-check` bypass.
6. **[#30269 – gate Rendezvous TCP_NODELAY by signed path](https://github.com/openai/codex/pull/30269)** – Open. Gates TCP_NODELAY on exec-server Rendezvous via signed URL, improving latency for production traffic.
7. **[#30291 – [app-server] expose environment info RPC](https://github.com/openai/codex/pull/30291)** – Open. Adds `environment/info` RPC for named environments, returning shell/cwd metadata.
8. **[#30319 – [codex] Add retired model compaction repro](https://github.com/openai/codex/pull/30319)** – Open. Integration test for model-switch compaction when previous slug is retired; ensures error handling before sampling.
9. **[#30302 – Preserve namespaces on custom tool calls](https://github.com/openai/codex/pull/30302)** – Open. Maintains optional namespace throughout deserialization and replay; adds regression tests.
10. **[#30201 – fix(remote-control): avoid server token refresh retry storms](https://github.com/openai/codex/pull/30201)** – Closed. Prevents cascading refresh failures when `/server/refresh` returns transient 502; keeps valid token in use.

## Feature Request Trends
- **Monitoring & background triggers** – Issue #29922 requests an agent-callable `monitor` tool to wake Codex on background events (logs, files, builds, CI) without polling. Popular across CLI and Desktop surfaces.
- **Provider configuration flexibility** – Issue #28902 asks for configurable `base_url` for the `amazon-bedrock` provider, mirroring existing `openai_base_url` support. Needed for proxy routing.
- **Memory management CLI commands** – Issue #30299 proposes official CLI commands to inspect, prune, delete, and scope accumulated memories. Currently there is no official surface for managing the growing `codex_memory` files (thousands of lines).
- **Window/session state persistence** – Several requests for restoring windows after restart (Issue #27104) and proper archived chat display (Issue #30312).

## Developer Pain Points
- **Rate-limit transparency** – Two high-severity issues (#28879, #30212) show that budget consumption is unpredictable and logs lack clear attribution. Users cannot trust displayed usage.
- **Platform fragmentation bugs** – Multiple issues specific to Intel Mac (SIGTRAP, missing Computer Use service), Windows (terminal read fail, Chrome control broken in WSL), and Linux (EMFILE from MCP leaks). Each platform feels second-class.
- **Resource leaks** – File descriptor leaks (MCP stdio), massive temp disk usage (code_sign_clone), and orphan child processes plague long-running sessions.
- **Unreliable input handling** – Duplicate message send, disabled prompt textarea after several prompts, and “no image on clipboard” errors are common small frustrations.
- **Plugin/skill ecosystem friction** – Missing PyYAML in bundled Python, plugins disappearing after updates, and sandbox config blocking app startup (Windows elevated) show rough edges in skill management.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*