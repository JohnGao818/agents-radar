# AI CLI Tools Community Digest 2026-06-15

> Generated: 2026-06-15 03:51 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Development Tools

**Date:** 2026-06-15  
**Sources:** Community digest summaries for Claude Code (Anthropic) and OpenAI Codex (OpenAI)

---

## 1. Ecosystem Overview

Both Claude Code and OpenAI Codex represent the leading edge of AI-assisted CLI development, but each is navigating distinct growing pains. Claude Code’s community is currently reeling from critical regressions in subagent management that can cause unbounded token consumption and system instability, while its user base increasingly demands localized pricing and billing transparency. OpenAI Codex faces a wave of Windows desktop crashes and data-loss bugs, balanced by an aggressive PR pipeline that is shipping improvements to sandboxing, rate-limit visibility, and plugin imports. No new releases were published by either tool in the last 24 hours, but both repositories show sustained development activity with notable differences in community engagement and pain points.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Noteworthy Hot Issues** | 10 | 10 |
| **Key PRs (highlighted in digest)** | 5 | 10 |
| **New Releases (today)** | 0 | 0 |

*Note: The digest for Claude Code included 5 key PRs (3 open, 2 closed). OpenAI Codex listed 10 key PRs (all open, but many are close to merge). Both digests focus on highlights, not full counts.*

---

## 3. Shared Feature Directions

Several requirements emerge across both tool communities, indicating convergence in user expectations:

- **Cost & Rate-Limit Transparency**  
  - *Claude Code:* Users demand India-specific pricing (upvoted 442×) and clear billing for new features like `remote-control`.  
  - *Codex:* The top-voted feature request is renaming threads, but rate-limit visibility (#15281, #28143) is a close second. Both communities want detailed usage data in the CLI.

- **Conversation & Session Management**  
  - *Claude Code:* Request for project-scoped conversation lists (#68495) and local timezone support.  
  - *Codex:* Strong demand for renaming task titles (#12564, 111👍) and frustration over chat history disappearing after updates.

- **Desktop Platform Stability**  
  - *Claude Code:* Windows blank screen bug (#51143) and macOS kernel zone leak (#66020) causing system panics.  
  - *Codex:* Multiple critical Windows crash reports (#27979, #27367) and macOS history loss (#27353). Both tools have unresolved platform-specific blockers.

- **Agent Safety & Resource Controls**  
  - *Claude Code:* Subagent recursion depth limits urgently needed; current `CLAUDE_CODE_FORK_SUBAGENT=0` ignored.  
  - *Codex:* Sandbox inconsistencies (false “Full Access” labels, power-outage breakage) and MCP timeout issues (#23840). Both communities want better guardrails.

- **UI/UX Polish**  
  - *Claude Code:* Copy-paste broken (#66192), window capture request (#68498).  
  - *Codex:* Spellcheck toggle (#25431), terminal resize reflow (now always-on), and auto-resolution timers for input prompts.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|-----------|-------------|--------------|
| **Primary Focus** | Advanced agent workflows (subagents, MCP integrations) with heavy CLI emphasis | Desktop app + CLI; plugin/sandbox ecosystem and rate-limit management |
| **Target Users** | CLI-heavy developers, often running long agent sessions | Developers using both desktop and CLI; strong Windows + WSL user base |
| **Technical Approach** | Subagent spawning for task delegation; suffers from recursion bugs | Managed child environments with MITM CA; extensible via `requirements.toml` and plugin import |
| **Pricing Model** | Subscription with add-ons; community angry about lack of Indian pricing and false rate-limit errors | Plus/Pro tiers; users want detailed usage breakdown and reset credits |
| **Current Pain Points** | Silent data loss (cleanupPeriodDays ignored, file truncation), cost explosion from runaway agents | Windows desktop crashes, history loss after updates, 62+ GB disk bloat on macOS |
| **Community Vocalization** | Highest-voted issue (442👍) – pricing; critical bug reports with high engagement | Highest-voted issue (111👍) – renaming threads; many crash reports with fewer upvotes but high urgency |

**Key Takeaways:**  
- Claude Code is pushing the envelope on autonomous agent capabilities but lacks safety rails, leading to expensive recursion loops.  
- OpenAI Codex is investing heavily in sandbox reliability and rate-limit infrastructure, but desktop stability still lags.

---

## 5. Community Momentum & Maturity

- **Claude Code** has a highly engaged, vocal community that is deeply price-sensitive and willing to upvote and comment extensively. The 442 upvotes on Indo pricing indicate a large underserved demographic. However, the presence of multiple **critical** bugs (infinite recursion, kernel panic, silent file truncation) suggests the codebase may be moving faster than quality assurance can keep up. PR activity is modest (5 key PRs), with several automated “bounty” fixes. Maturity is high in terms of feature scope but low in reliability for certain advanced workflows.

- **OpenAI Codex** shows a higher PR throughput (10 key PRs) with substantial infrastructure improvements (MITM CA, requirements.toml, MCP timeout adjustments). The community is smaller in terms of upvote counts (max 111) but equally frustrated by stability issues, especially on Windows. The digest indicates rapid iteration on missing features (rate-limit reset, async hooks, multi-tool install). Maturity is solid for core functionality but fragile on desktop and sandbox edge cases.

**Conclusion on momentum:**  
OpenAI Codex appears to be iterating faster (more PRs, more infrastructure changes), while Claude Code is dealing with more severe regressions that may slow down feature development. However, Claude Code’s user base is larger and more vocal, which could pressure Anthropic to prioritize fixes.

---

## 6. Trend Signals

From the community feedback across both tools, several industry-wide signals emerge that are valuable for developers and tool vendors:

- **Cost and pricing transparency is non-negotiable.**  
  Users are unwilling to accept opaque billing or lack of localized pricing. The success of competitors offering INR pricing means tool makers must adapt or lose markets.

- **Agent recursion and unbounded resource usage is the new “buffer overflow.”**  
  As agents become more powerful, missing depth limits or infinite loops lead to catastrophic cost and system instability. Safety rails (recursion limits, spend caps) are becoming table stakes.

- **Desktop stability remains a bottleneck for adoption.**  
  Windows crashes and macOS memory leaks are the top blockers for developers who rely on desktop UIs. The CLI is resilient, but the desktop app is where trust is built or broken.

- **Silent data loss destroys user confidence.**  
  Whether through ignored cleanup settings, file truncation, or disappearing chat histories, any data loss without clear warnings erodes trust faster than any other bug.

- **MCP/plugin ecosystems need hardening.**  
  Timeouts, missing binaries, lost credentials, and inconsistent sandbox behavior are hindering the promise of seamless tool integration. Developers expect plug-and-play reliability.

- **Rate-limit management is becoming a core UX feature.**  
  Users want to monitor and control their consumption in real time, not just receive vague error messages. Infrastructure for credit redemption and reset visibility is being built now.

---

*This report is based on community digest summaries for June 15, 2026. It reflects only publicly visible issues and PRs at that time.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
**Data snapshot:** github.com/anthropics/skills · 2026-06-15  

---

## 1. Top Skills Ranking (by discussion activity)

The following open Pull Requests represent the most actively discussed Skill submissions in the community. All remain open and under review.

| Rank | PR | Skill / Purpose | Discussion Highlights |
|------|----|-----------------|----------------------|
| 1 | [#514 – Add document-typography skill](https://github.com/anthropics/skills/pull/514) | Typographic quality control for AI-generated documents – catches orphan words, widow paragraphs, numbering misalignment. | Strong agreement that typography issues affect *every* Claude-generated document. No significant controversy; community wants this merged. |
| 2 | [#486 – Add ODT skill](https://github.com/anthropics/skills/pull/486) | OpenDocument text creation, template filling, and ODT→HTML conversion. | Fills a glaring gap for LibreOffice/ISO-format users. Discussion focuses on parsing correctness and template-variable handling. |
| 3 | [#210 – Improve frontend-design skill](https://github.com/anthropics/skills/pull/210) | Revises the existing frontend-design skill for clarity, actionability, and internal coherence. | Heated debate about making instructions specific enough for a single conversation without becoming overly prescriptive. |
| 4 | [#83 – Add meta-skills: skill-quality-analyzer & skill-security-analyzer](https://github.com/anthropics/skills/pull/83) | Two meta-skills that evaluate other Skills across five quality dimensions and security patterns. | Interest in self-assessment tooling; concerns about circular dependency and maintenance overhead. |
| 5 | [#1140 – Implement agent-creator skill + fix multi-tool evaluation](https://github.com/anthropics/skills/pull/1140) | Meta-skill for generating task-specific agent sets; fixes evaluation.py for parallel tool calls and adds Windows support. | High engagement because it addresses two pain points: agent composition and broken Windows evaluation. |
| 6 | [#361 – Detect unquoted YAML special characters in description fields](https://github.com/anthropics/skills/pull/361) | Pre-parse validation in `quick_validate.py` to catch silent YAML parsing failures. | Duplicates work from [#539](https://github.com/anthropics/skills/pull/539); reviewers asking to consolidate. |
| 7 | [#444 – Add AURELION skill suite (kernel, advisor, agent, memory)](https://github.com/anthropics/skills/pull/444) | Cognitive framework with structured thinking templates and persistent memory for professional knowledge management. | Polarizing – some praise its depth, others call it overly complex for a single skill. Long thread about scope. |
| 8 | [#723 – Add testing-patterns skill](https://github.com/anthropics/skills/pull/723) | Comprehensive testing skill covering philosophy, unit/React/e2e patterns, and what *not* to test. | Broadly welcomed; discussion centers on whether to include mocking libraries by name or keep it framework-agnostic. |

---

## 2. Community Demand Trends (from Issues)

The most vocal community needs fall into three categories:

| Trend | Key Issues | Signal |
|-------|------------|--------|
| **Skill infrastructure reliability** | [#556 – run_eval.py 0% trigger rate](https://github.com/anthropics/skills/issues/556) (12 comments, 7 👍), [#1169 – recall=0% on optimizer](https://github.com/anthropics/skills/issues/1169) (3 comments), [#1061 – Windows compatibility](https://github.com/anthropics/skills/issues/1061) (3 comments) | The evaluation pipeline is broken for most users; fixing it is the #1 blocker for Skill creation. |
| **Collaboration & sharing** | [#228 – Org-wide skill sharing](https://github.com/anthropics/skills/issues/228) (14 comments, 7 👍), [#492 – Security namespace abuse](https://github.com/anthropics/skills/issues/492) (7 comments) | Users want enterprise-grade distribution and trust boundaries. |
| **Skill ecosystem maturity** | [#189 – Duplicate skills from plugins](https://github.com/anthropics/skills/issues/189) (6 comments, 8 👍), [#202 – skill-creator outdated](https://github.com/anthropics/skills/issues/202) (8 comments), [#1220 – Multi-file bundling](https://github.com/anthropics/skills/issues/1220) (2 comments) | As the repository grows, users demand better tooling for creation, validation, and referencing. |

**Most-anticipated new skill directions** (from proposals and wishlist comments):  
- Agent governance / safety patterns (Issue [#412](https://github.com/anthropics/skills/issues/412))  
- MCP-style exposure of Skills as APIs (Issue [#16](https://github.com/anthropics/skills/issues/16))  
- SharePoint Online / enterprise document handling patterns (Issue [#1175](https://github.com/anthropics/skills/issues/1175))

---

## 3. High-Potential Pending Skills (likely to land soon)

These open PRs have active discussion, recent updates, and appear close to merging:

| PR | Skill | Why It May Land Soon |
|----|-------|----------------------|
| [#1298 – fix run_eval.py recall=0%](https://github.com/anthropics/skills/pull/1298) | Critical bugfix – installs eval artifact as a real skill, fixes Windows stream reading and parallel workers. | Addresses #556, the most upvoted open issue; submitted by a first-time contributor with minimal diff. High merge probability. |
| [#1099 – fix run_eval.py crash on Windows (subprocess pipe)](https://github.com/anthropics/skills/pull/1099) | Targeted fix for WinError 10038. | Same root cause as #1298 but narrower; may be superseded or merged separately. |
| [#1050 – fix Windows subprocess + encoding bugs](https://github.com/anthropics/skills/pull/1050) | Two one-line fixes for PATHEXT and cp1252. | Small, well-scoped, and matches repeated community reports. |
| [#539 – warn on unquoted description with YAML special characters](https://github.com/anthropics/skills/pull/539) | Pre-parse validation in quick_validate.py. | Competing with #361; maintainers asked to consolidate. Likely one will be merged. |
| [#541 – fix DOCX tracked change w:id collision](https://github.com/anthropics/skills/pull/541) | Prevents document corruption when bookmarks exist. | Clear root cause, testable fix, and directly affects usability. |

---

## 4. Skills Ecosystem Insight

> **The community’s most concentrated demand is a stable, reliable, and cross-platform evaluation toolchain** — without it, every other Skill contribution is built on a broken foundation, as evidenced by the six-figure sum of issues and PRs dedicated to `run_eval.py`, Windows compatibility, and YAML parsing edge cases.

---

Here is the **Claude Code Community Digest** for **2026-06-15**, based on the latest activity in the `anthropics/claude-code` repository.

---

## Today's Highlights
The community is reeling from a cluster of critical regressions around **subagent management**, where spawned agents recursively launch unbounded child processes, burning through tokens and exhausting system resources (#68430, #68110). A separate, single-issue cause of massive token burn is a **macOS kernel zone leak** (#66020) that can panic the system at ~20GB of memory. Meanwhile, long-standing frustrations around **pricing transparency** (especially for India) and **insufficient billing error handling** (#32544, #59823) continue to draw significant community attention.

## Releases
No new releases were published in the last 24 hours.

## Hot Issues (10 Noteworthy)

1.  **#17432 – India-Specific Pricing Plans (INR) for Claude & Claude Code**
    - **Why it matters:** 442 upvotes and 194 comments make this the single most-requested feature. Users highlight the significant price barrier for Indian developers, especially as competitors (OpenAI, Google) already offer local pricing.
    - **Community reaction:** Overwhelmingly supportive, with users sharing personal use cases and economic arguments. Anthropic has not yet formally responded.

2.  **#53940 – Cowork Edit/Write tools silently truncate files via byte-conservation buffer cap**
    - **Why it matters:** A deterministic bug that silently truncates files at any size. This is a data-loss issue for heavy users of Cowork.

3.  **#41458 – `cleanupPeriodDays: 99999` ignored — 490 sessions silently deleted**
    - **Why it matters:** A clear violation of explicit user configuration. The community is frustrated by the silent data loss, which seems to ignore a safety-limit setting.

4.  **#32544 – Extra Usage charged despite available plan capacity + false rate limit errors**
    - **Why it matters:** A dual bug: users are charged for usage they should already have available under their plan, and they receive incorrect "rate limited" errors. This directly impacts developer trust and costs.

5.  **#51143 – Claude Desktop persistent blank/white screen on Windows**
    - **Why it matters:** A major blocker for Windows users, rendering the Desktop app unusable. Multiple reinstalls and workarounds have failed.

6.  **#63870 – Bash tool calls emitted as raw `<invoke>` text instead of executing**
    - **Why it matters:** A fundamental tool execution regression. The model emits unparsed XML instead of performing actions. This is a critical operational bug.

7.  **#66192 – Copy-paste does not work**
    - **Why it matters:** A basic UI interaction that is broken. This is a high-friction issue for daily use.

8.  **#68430 – Subagent spawning and subagent pattern bugs trigger infinite recursion, infinite token usage**
    - **Why it matters:** A **critical** issue where subagents recursively spawn 50+ levels deep, ignoring the `CLAUDE_CODE_FORK_SUBAGENT=0` setting. This can lead to catastrophic token burn (and cost) with no user recourse.

9.  **#66020 – macOS kernel zone leak (data.kalloc.1024) from Claude Code CLI**
    - **Why it matters:** A system-level memory leak that can cause the kernel to panic at ~20GB. This is an OS-level stability threat for macOS users running agent workloads.

10. **#59823 – Billing implications for `claude remote-control` on June 15th**
    - **Why it matters:** The documentation is unclear about whether using `claude remote-control` consumes API credits from a subscription plan. The ambiguity creates risk for developers scaling headless usage.

## Key PR Progress (5 PRs)

1.  **#43598 – Add upstream issue sync workflow**
    - **Status:** Closed
    - **Summary:** Adds a script/doc to fetch and normalize upstream issues, with robust pagination handling. Infrastructure improvement.

2.  **#68423 – fix(scripts): don't auto-close assigned issues in sweep**
    - **Status:** Open
    - **Summary:** Fixes a script bug where `sweep.ts` would skip assigned issues during the `markStale` stage but then close them in the `closeExpired` stage. Stops the auto-closure of issues that have an active assignee.

3.  **#67699 – [BUG] Claude autonomously ran background scripts calling a paid external**
    - **Status:** Open
    - **Summary:** /bounty $29 fix for an issue where Claude autonomously executed background scripts that called a paid external service. Implementation is automated via NVIDIA AI.

4.  **#67409 – [BUG] Account downgraded due to billing error**
    - **Status:** Open
    - **Summary:** /bounty $200 fix for an account downgrade issue. Also automated via NVIDIA AI.

5.  **#67722 – [BUG] Claude autonomously ran background scripts calling a paid external**
    - **Status:** Closed
    - **Summary:** A separate PR for the same issue class. Reviewed and approved, adds a deduplication workflow.

## Feature Request Trends

- **Pricing & Billing:** The dominant theme. Users want **localized pricing** (INR) and **transparent billing** for new features like `remote-control`. There is also a strong demand for **per-message model selection** in the CLI (#68165) to control costs without switching subscriptions.
- **Subagent & Workflow Control:** Users want to **constrain agent recursion** (e.g., depth limits, `cwd` parameters for task tools). The current "general-purpose" sub-agent is too powerful and lacks safety rails.
- **UI/UX Polish:** Requests for **Appshots-style window capture** (#68498), **project-scoped conversation lists** (#68495), and **local timezone support** (#64988) indicate a maturing tool that needs better integration with developer workflows.
- **Platform Parity:** Windows users continue to report critical bugs (blank screen, file locks), while macOS users struggle with the kernel zone leak. The community wants equal stability across platforms.

## Developer Pain Points

- **Silent Data Loss:** The `cleanupPeriodDays` bug (#41458) and the file truncation bug (#53940) both destroy user work silently, eroding trust.
- **Configuration Overrides:** Settings like `cleanupPeriodDays`, `CLAUDE_CODE_FORK_SUBAGENT`, and model selections in `settings.json` are being ignored by the runtime. This makes configuration feel unreliable.
- **Constant Platform-Specific Bugs:** The kernel zone leak (macOS), blank screen (Windows), and pty exhaustion (macOS) create a cycle of instability that frustrates users on all major platforms.
- **Context Window Bloat from MCP:** Disconnected account-level MCP integrations still inject system-reminder noise into context, wasting tokens (#68462).
- **Inaccurate Billing/Rate Limiting:** False rate limit errors and incorrect usage charges (#32544) create a "death by a thousand cuts" experience for paying users, especially those on subscription plans.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

**OpenAI Codex Community Digest**  
*2026-06-15*

---

## Today's Highlights

A wave of Windows desktop stability issues dominates the conversation, with several users reporting that the latest Codex App update (26.609.4994.0) either fails to open or crashes on launch. Meanwhile, the team is actively shipping improvements to how external agents and plugins are imported, including new progress accounting and telemetry. On the feature front, the community continues to push for better rate-limit visibility and the ability to rename chat threads.

---

## Releases

No new releases in the past 24 hours.

---

## Hot Issues

1. **[#27979 – Windows Codex App 26.609.4994.0 no longer opens after update](https://github.com/openai/codex/issues/27979)**  
   *21 comments, 6 👍*  
   A critical bug affecting Windows users – the desktop app crashes immediately after the June 12 update. No workaround has been confirmed yet. This is the most urgent open issue.

2. **[#25500 – Projects sidebar shows “No chats” for older conversations](https://github.com/openai/codex/issues/25500)**  
   *18 comments, 2 👍*  
   Users lose access to their chat history after updating to 0.135.0-alpha.1. The sidebar incorrectly reports empty projects, making it hard to resume past work.

3. **[#27817 – False positive cybersecurity flag on authorized tax filing](https://github.com/openai/codex/issues/27817)**  
   *16 comments, 0 👍*  
   A legitimate finance task was flagged as a cybersecurity risk, forcing users to rephrase or join a “Trusted Access” program. This highlights over-aggressive safety checks.

4. **[#12564 [CLOSED] – Allow renaming task/thread titles](https://github.com/openai/codex/issues/12564)**  
   *80 comments, 111 👍*  
   The most upvoted item. The community strongly wants to rename conversation titles for easier navigation. Although closed (possibly fixed?), it reflects a long-standing need.

5. **[#15281 – Expose full usage/limits in CLI `/status`](https://github.com/openai/codex/issues/15281)**  
   *6 comments, 15 👍*  
   Users on Plus plans want detailed rate-limit data (reset time, remaining credits) directly in the CLI, rather than vague percentages.

6. **[#27353 – Project chat history disappeared after app update](https://github.com/openai/codex/issues/27353)**  
   *7 comments, 3 👍*  
   Another history-loss bug on macOS. Users report that after the June 9 update, all project chats are missing – no recovery path given.

7. **[#24599 – Reappearing crash loop – Codex UI completely unusable](https://github.com/openai/codex/issues/24599)**  
   *8 comments, 0 👍*  
   A persistent crash on macOS that makes the app unusable. The user cannot even open the About dialog to report the version.

8. **[#27367 – Codex desktop immediately exits on Windows 10 Pro 22H2](https://github.com/openai/codex/issues/27367)**  
   *9 comments, 0 👍*  
   Windows 10 users are locked out after an update, while the CLI continues to work. Suggests a sandbox or Electron initialization issue.

9. **[#28103 – Missing Linux codex binary in MSIX – breaks “Run agent in WSL”](https://github.com/openai/codex/issues/28103)**  
   *5 comments, 9 👍*  
   The Microsoft Store build lacks the Linux CLI binary needed for WSL integration. A regression that blocks WSL users.

10. **[#25431 – Expose spellchecking toggle in Windows App settings](https://github.com/openai/codex/issues/25431)**  
    *5 comments, 14 👍*  
    Users want a simple on/off switch for spellcheck. Currently it is always on and cannot be disabled, which interferes with code input.

---

## Key PR Progress

1. **[#25888 – Prepare managed child MITM CA env](https://github.com/openai/codex/pull/25888)**  
   Part of a large stack to handle MITM certificates in child environments, improving security for agent sandboxing.

2. **[#28008 – Add external agent import result accounting](https://github.com/openai/codex/pull/28008)**  
   Gives clients a stable import ID and detailed completion payloads, enabling reliable tracking of plugin and session imports.

3. **[#28143 – Expose rate-limit reset credits via app-server API](https://github.com/openai/codex/pull/28143)**  
   Adds backend support for reading and redeeming personal rate-limit reset credits, powering the upcoming `/usage` enhancements.

4. **[#28235 – Add request user input auto-resolution timer (TUI)](https://github.com/openai/codex/pull/28235)**  
   Introduces a 60+60 second countdown for user-input prompts in the CLI, with auto-submit if the user doesn’t respond – a UX improvement for non-interactive scripting.

5. **[#27640 – Support multi-tool install requests](https://github.com/openai/codex/pull/27640)**  
   Expands plugin installation to accept multiple tools at once, reducing round trips when restoring a workspace.

6. **[#28154 – Add rate-limit reset redemption to `/usage` TUI](https://github.com/openai/codex/pull/28154)**  
   Gives CLI users the ability to view and redeem earned reset credits directly from the existing usage command.

7. **[#27794 – Remove terminal resize reflow feature flags](https://github.com/openai/codex/pull/27794)**  
   Makes terminal resize reflow always-on, removing deprecated configuration paths. A cleanup PR after stable rollout.

8. **[#28234 – Increase default MCP tool timeout to 300 seconds](https://github.com/openai/codex/pull/28234)**  
   Addresses frequent timeout complaints by raising the default MCP tool-call timeout from 120s to 300s.

9. **[#27452 – Run async hooks and deliver output on accepted requests](https://github.com/openai/codex/pull/27452)**  
   Activates async hook execution, allowing long-running hooks to finish independently and contribute output to later model requests.

10. **[#27666 – Add managed field support to `requirements.toml`](https://github.com/openai/codex/pull/27666)**  
    Extends the requirements system to enforce managed settings (auth, storage, telemetry, etc.) without migrating the old `managed_config.toml`.

---

## Feature Request Trends

- **Rate-limit transparency** – Users repeatedly ask for detailed usage data (remaining credits, reset time, redemption options) in both CLI and desktop interfaces.  
- **Conversation management** – Renaming threads/tasks (#12564) and scrolling long assistant responses in TUI (#23280) are common quality-of-life asks.  
- **Customization controls** – Spellcheck toggle, inheriting shell aliases, and explicit WSL support configuration are top requests.  
- **Plugin and sandbox resilience** – There is growing demand for better error messages and recovery flows when plugin installs or sandbox operations fail.  

---

## Developer Pain Points

- **Windows desktop instability** – Multiple reports of the app failing to open after updates (#27979, #27367, #28245), often with no recovery path.  
- **History/data loss** – Chat and project histories disappearing after updates (#25500, #27353, #24599) is a recurring frustration, especially for users with long-running sessions.  
- **Sandbox inconsistencies** – The sandbox sometimes shows “Full Access” while actually restricting writes (#25590), and power outages can leave sandboxes in a broken state (#28248).  
- **MCP integration fragility** – Timeouts (#23840), OAuth credential loss on restart (#28201), and missing binary in MSIX builds (#28103) hamper the MCP experience.  
- **Disk space bloat** – macOS users report a `code_sign_clone` directory growing to 62+ GB (#27536), with no automated cleanup.  
- **False positive safety flags** – Legitimate finance/tax work flagged as cybersecurity risk (#27817) erodes trust in the safety system.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*