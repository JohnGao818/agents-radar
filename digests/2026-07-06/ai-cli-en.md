# AI CLI Tools Community Digest 2026-07-06

> Generated: 2026-07-06 02:47 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem – 2026-07-06

## 1. Ecosystem Overview

The AI CLI tools landscape continues to show high community engagement mixed with growing stability concerns. Both Claude Code and OpenAI Codex are navigating post-release regression waves, with users reporting critical bugs (freezes, model downgrades, process leaks) that directly impact daily workflows. Feature demands are converging on platform parity (Linux desktop, Markdown export) and operational transparency (rate-limit metering, permission clarity). While the communities are active and vocal, the pace of code fixes appears uneven – Claude Code shows unusually low PR activity today despite multiple regressions, while OpenAI Codex has a steady flow of targeted pull requests. Overall, the ecosystem is maturing but still grappling with the complexity of multi-agent, multi-model, and cross-platform deployments.

## 2. Activity Comparison

| Metric                | Claude Code                            | OpenAI Codex                         |
|-----------------------|----------------------------------------|--------------------------------------|
| **Hot Issues listed** | 10 noteworthy issues (361👍 top, 125 comments) | 10 top issues (690👍 top, 143 comments) |
| **Pull Requests**     | 2 updated (1 minor doc fix, 1 spam closed) | 10 open/updated (significant fixes)   |
| **Release Status**    | Latest stable v2.1.201; no new release today | Latest CLI v0.141.0; no new version today |
| **Regression Reports**| 3+ v2.1.201 regressions (VS Code load, message desync, zombie agents) | SIGTRAP on Intel macOS, Windows git loop, rate-limit drain |
| **Community Priority**| Safety classifier false-positives, multi-agent coordination, permission model bugs | Linux desktop app, mobile remote control, model quality degradation |

## 3. Shared Feature Directions

Both communities are demanding capabilities that span beyond a single tool:

- **Markdown export / clipboard preservation** – Claude Code users want Markdown clipboard support on macOS ([#74628]); OpenAI Codex users request export chat as Markdown ([#17241]). Both indicate a need to extract conversation content in a portable, structured format.
- **Process naming and lifecycle transparency** – Claude Code requests human-readable daemon process names ([#74641]); OpenAI Codex users report MCP server orphan processes consuming >9 GB RSS ([#30408]). Better observability of background processes is a shared concern.
- **Rate-limit and usage metering** – Claude Code sees billing surprises from silent model downgrades; OpenAI Codex has “model at capacity” errors and usage draining 5–10× too fast ([#30939]). Both communities want clear, real-time consumption data.
- **Model quality assurance** – Claude Code faces false-positive safety classifiers downgrading models mid-task; OpenAI Codex reports GPT-5.5 reasoning-token clustering that degrades complex tasks ([#30364]). Both suffer from unwanted behavior changes without user consent.

## 4. Differentiation Analysis

Claude Code differentiates through **multi-agent orchestration** and **permission granularity**. Its community actively debates subagent model pinning, background team termination, and `--permission-mode dontAsk` contradictions – reflecting a focus on headless/CI workflows and autonomous agent teams. Safety classifiers are a prominent pain point, indicating a more aggressive guardrail system.

OpenAI Codex differentiates through **platform expansion** (Linux desktop, mobile remote control) and **enterprise integration**. Its top issues are about app availability and authentication (Business access-tokens, extension-managed auth). The community also shows strong interest in **AI-assisted skill creation** (e.g., “pet creation”) and **MCP server ecosystem** – hints of a more extensible, plugin-oriented architecture.

Technically, Claude Code’s regressions cluster around session state (AskUserQuestion freeze, turn/message desync) and background processes (zombie agents). OpenAI Codex’s regressions are more platform-specific (Intel macOS SIGTRAP, Windows git loops) and rate-limit infrastructure.

## 5. Community Momentum & Maturity

- **OpenAI Codex** has higher raw engagement on its top feature request (690👍 for Linux desktop) and maintains a steady PR pipeline (10 open/updated today). The community is vocal about platform gaps but also has rapid fix cycles (e.g., PR #31192 addressing SIGTRAP). This suggests a more mature, process-driven development cadence – though still struggling with Windows and enterprise auth.
- **Claude Code** shows a more volatile pattern: massive engagement on a critical regression (#73125, 361👍) with 125 comments, yet virtually no code changes in flight (2 trivial PRs). The “v2.1.201 regression wave” with three distinct bugs reported the same day indicates a rushed release. Community energy is high, but the response appears to be in triage mode rather than active iteration.
- Both tools have equally active user bases, but Claude Code’s current momentum is tilted toward firefighting, while OpenAI Codex is steadily addressing known issues while pushing new features (MongoDB thread store, MCP auth).

## 6. Trend Signals

Several industry-relevant signals emerge from today’s feedback:

1. **Safety systems are hurting trust** – False-positive classifiers in Claude Code and model-downgrade events without user visibility (both tools) risk undermining developer confidence. Expect more demand for opt-out override controls and audit trails.
2. **Rate-limit transparency is non-negotiable** – Both communities are frustrated by opaque billing and capacity errors. Tools that provide real-time credit/reset dashboards (OpenAI Codex PR #30395 is a step) will gain trust.
3. **Platform parity is a growth bottleneck** – Linux and Windows users are increasingly vocal about app quality. Ignoring these platforms risks losing a significant segment of developers to competitors with native support.
4. **Multi-agent/team coordination remains immature** – Claude Code’s message desync, model pin loss, and zombie processes show that concurrent agent management is still fragile. Expect this to be a frontier for differentiation.
5. **Model degradation concerns are rising** – Both communities report “silent downgrades” or reasoning quality drops. Developers want model versions pinned and behavior changes explicitly communicated – not left to opaque safety or routing logic.
6. **MCP server ecosystem needs lifecycle management** – Orphaned processes (OpenAI Codex) and “starting MCP servers” hangs (PR #31189) highlight the need for robust server startup/shutdown protocols.

**Bottom line for developers**: If you depend on multi-agent autonomy, Claude Code offers richer tooling but carries higher instability risk today. If you need broad platform support and enterprise auth, OpenAI Codex is more actively patching its gaps. Both require careful monitoring of model behavior and rate limits – and both communities are pushing for transparency and reliability over raw feature velocity.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data snapshot: 2026-07-06 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following pull requests have drawn the most community discussion and represent the most significant Skills additions or bug fixes under review.

### 1. Fix: Skill-creator eval pipeline producing 0% recall
**PR #1298** — *Open* — by MartinCajiao  
This is the most critical operational fix in the queue. `run_eval.py` (and downstream `run_loop.py` and `improve_description.py`) has been reporting `recall=0%` for every skill description, meaning the description-optimization loop optimizes against noise. The PR addresses four root causes: installs the eval artifact as a real skill (so `claude -p` can trigger it), fixes Windows stream reading, repairs trigger detection logic, and parallelizes workers. The issue (#556) has 10+ independent reproductions, making this the community's highest-priority infrastructure fix.  
🔗 https://github.com/anthropics/skills/pull/1298

### 2. Add document-typography skill
**PR #514** — *Open* — by PGTBoos  
A quality-of-life skill preventing orphan word wrap (1–6 words on a new line), widow paragraphs (headers stranded at page bottom), and numbering misalignment in AI-generated documents. The author argues these "affect every document Claude generates" and users rarely request fixes proactively. The skill has broad applicability across any document-generation workflow.  
🔗 https://github.com/anthropics/skills/pull/514

### 3. Add ODT skill — OpenDocument text creation and template filling
**PR #486** — *Open* — by GitHubNewbie0  
Adds comprehensive OpenDocument Format support (.odt, .ods), including creation, template filling, and ODT-to-HTML conversion. Targeted at users working with LibreOffice or ISO-standard document formats. The skill covers the full round-trip from reading to writing, making it a strong complement to the existing DOCX and PDF skills.  
🔗 https://github.com/anthropics/skills/pull/486

### 4. Add self-audit skill — mechanical verification + reasoning quality gate
**PR #1367** — *Open* — by YuhaoLin2005  
A universal quality-assurance skill that audits AI output before delivery. Step 0 performs mechanical file verification (confirming every claimed output exists), followed by a four-dimension reasoning audit in damage-severity priority order. The author claims it works with any project, tech stack, or model. This represents a new category: meta-quality skills for output validation.  
🔗 https://github.com/anthropics/skills/pull/1367

### 5. Fix: PDF case-sensitive file references
**PR #538** — *Open* — by Lubrsy706  
Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where uppercase file references (`REFERENCE.md`, `FORMS.md`) point to lowercase files (`reference.md`, `forms.md`). This breaks on case-sensitive filesystems (Linux, macOS). Though a simple fix, it highlights a recurring quality gap in the Skills collection.  
🔗 https://github.com/anthropics/skills/pull/538

### 6. Add testing-patterns skill
**PR #723** — *Open* — by 4444J99  
A comprehensive testing skill covering the full stack: testing philosophy (Testing Trophy model), unit testing (AAA pattern, pure functions, edge cases), React component testing (Testing Library), and decisions on what to test versus what NOT to test. Fills a notable gap—the repository previously lacked a dedicated testing skill.  
🔗 https://github.com/anthropics/skills/pull/723

### 7. Add sensory skill — native macOS automation via AppleScript
**PR #806** — *Open* — by AdelElo13  
Teaches Claude to use `osascript` (AppleScript) for native macOS automation, replacing screenshot-based computer use. Features a two-tier permission system: Tier 1 works out of the box (direct app scripting), Tier 2 requires Accessibility permissions (System Events UI control). This represents a platform-specific automation direction that could expand to Windows and Linux analogues.  
🔗 https://github.com/anthropics/skills/pull/806

### 8. Fix: DOCX tracked change `w:id` collision with existing bookmarks
**PR #541** — *Open* — by Lubrsy706  
Fixes document corruption when the DOCX skill adds tracked changes to documents with existing bookmarks. Root cause: OOXML uses a shared `w:id` namespace across bookmarks, tracked changes, comments, and move ranges. The SKILL.md examples used hardcoded low IDs that collide with real document IDs. A systematic fix for a subtle OOXML interoperability bug.  
🔗 https://github.com/anthropics/skills/pull/541

---

## 2. Community Demand Trends

Analysis of the most-discussed Issues reveals five distinct demand directions:

**🔒 Security & Trust Boundaries** — Issue #492 is the most-commented issue (34 comments) and the highest-grossing concern. Community members discovered that community-made skills are distributed under the `anthropic/` namespace, enabling trust boundary abuse where users may grant elevated permissions to skills they believe are official. This has sparked a broader conversation about skill signing, provenance, and permission scoping.

**🏢 Enterprise & Organizational Features** — Issue #228 (14 comments, 7 👍) calls for org-wide skill sharing in Claude.ai. Currently users must download `.skill` files, send via Slack/Teams, and have colleagues manually upload them. The demand for a shared skill library or direct sharing links is growing, especially as teams adopt Claude Code more broadly.

**🛠️ Skill-Creator Reliability** — Issue #556 (12 comments, 7 👍) documenting the 0% trigger rate bug in `run_eval.py` has the most cross-references in PRs. Four separate PRs (#362, #361, #1099, #1050, #1298, #1323) attempt to fix various facets of the same problem. The community clearly wants a working optimization loop, not new features.

**📋 Duplicate Skill Management** — Issue #189 (6 comments, 9 👍) reports that `document-skills` and `example-skills` plugins install identical content, causing duplicate skills in Claude Code's context window. The high 👍 count relative to comments suggests widespread silent agreement—users want deduplication, not just documentation fixes.

**🪟 Windows Compatibility** — Issue #1061 (3 comments, 1 👍) and related PRs (#1099, #1050, #362) document that `skill-creator` scripts are unusable on Windows due to `PATHEXT` handling, `cp1252` encoding, and `select` on pipes. A small but vocal Windows-using segment is blocked from using the optimization tooling entirely.

---

## 3. High-Potential Pending Skills

These open PRs have active discussion and appear close to landing:

- **Windows subprocess + encoding fixes** — PR #1099 (joshuawowk) and PR #1050 (gstreet-ops) both fix the Windows `PATHEXT` issue where `subprocess.Popen(["claude", ...])` fails because the CLI ships as `claude.cmd`. At least one of these is likely to merge soon given the combined pressure from multiple reporters.  
  🔗 https://github.com/anthropics/skills/pull/1099  
  🔗 https://github.com/anthropics/skills/pull/1050

- **UTF-8 multi-byte character handling** — PR #362 (Mr-Neutr0n) replaces character-based length checks with UTF-8 byte-length validation to prevent Rust panics when the CLI processes multi-byte characters. Paired with PR #361 that detects unquoted YAML special characters. These are blocking issues for non-English skill descriptions.  
  🔗 https://github.com/anthropics/skills/pull/362  
  🔗 https://github.com/anthropics/skills/pull/361

- **Trigger detection fix for skill-creator** — PR #1323 (Polluelo978) fixes `run_single_query` failing to detect that a skill triggered, causing the optimization loop to report recall=0%. Directly addresses the core bug in #556, complementing the broader fix in #1298.  
  🔗 https://github.com/anthropics/skills/pull/1323

- **Color-expert skill** — PR #1302 (meodai) adds a self-contained color-expertise skill covering naming systems (ISCC-NBS, Munsell, XKCD, RAL, Ridgway 1912), color spaces with a "what to use when" table, and practical guidance. Low controversy, high utility—likely to merge cleanly.  
  🔗 https://github.com/anthropics/skills/pull/1302

- **CONTRIBUTING.md** — PR #509 (narenkatakam) adds the single most impactful community health file, addressing the repo's 25% community health metrics score. Low technical risk, high community value.  
  🔗 https://github.com/anthropics/skills/pull/509

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *reliable tooling infrastructure* (fixing the skill-creator evaluation pipeline and cross-platform compatibility) and *trust governance* (namespace security, deduplication, and organizational sharing), rather than for new skill categories.**


---

# Claude Code Community Digest — 2026-07-06

## Today’s Highlights
The community is sounding alarm over a critical regression (Issue #73125) where `AskUserQuestion` freezes for 60 seconds and then proceeds without an answer—125 comments and 361 upvotes make it the clearest fire of the day. Meanwhile, a wave of false-positive safety classifiers (Issues #74610, #74615, #74644) is silently downgrading models or halting legitimate security work, sparking backlash. Multiple post-update regressions in v2.1.201, including VS Code extension load failures and turn/message desync with background agents, suggest a rough release.

---

## Releases
No new versions were published in the last 24 hours. The latest stable remains **v2.1.201**.

---

## Hot Issues (10 Noteworthy)

1. **[#73125 — AskUserQuestion: "No response after 60s — continued without an answer"](https://github.com/anthropics/claude-code/issues/73125)**  
   *125 comments · 361 👍 | [CLOSED]*  
   A session-halting bug where Claude silently skips user prompts after 60 seconds. Affects Bedrock API, Linux, VS Code. Massive community engagement suggests it’s a top-priority fix.

2. **[#71542 — GitHub connector links repos but cannot access content (account-wide regression)](https://github.com/anthropics/claude-code/issues/71542)**  
   *27 comments · 18 👍 | [OPEN]*  
   A recent regression renders the GitHub integration useless—public and private repos alike are unreachable. No workaround known.

3. **[#30873 — Chrome extension side panel closes when switching/opening tabs in Microsoft Edge on macOS](https://github.com/anthropics/claude-code/issues/30873)**  
   *24 comments · 32 👍 | [OPEN]*  
   Long-standing bug (since March 2026) disrupting multi-tab workflows on macOS. High upvotes indicate many users hit this daily.

4. **[#71547 — AskUserQuestion dialog auto-submits on mouse click without confirmation](https://github.com/anthropics/claude-code/issues/71547)**  
   *8 comments · 12 👍 | [OPEN]*  
   Accidental submission of critical prompts (e.g., destructive commands) because a single click bypasses Enter/confirm. Usability risk.

5. **[#74636 — Spoofed "file was modified… don't tell the user" system-reminder appears after Claude's own Write/Edit tool calls](https://github.com/anthropics/claude-code/issues/74636)**  
   *1 comment · 0 👍 | [OPEN]*  
   A bizarre false system reminder appears mid-session, potentially covering up actual file modifications. Raised today, low traction but high suspicion.

6. **[#74643 — VS Code extension 2.1.201 fails to load: `PendingMigrationError: navigator is now a global in nodejs`](https://github.com/anthropics/claude-code/issues/74643)**  
   *0 comments | [OPEN]*  
   Fresh regression in the latest extension—Zod migration incompatibility on current VS Code. Blocks all VS Code usage on WSL.

7. **[#74637 — v2.1.201: turn/message desync with background agents — assistant turn starts before queued message delivered](https://github.com/anthropics/claude-code/issues/74637)**  
   *0 comments | [OPEN]*  
   Another v2.1.201 regression: queued user messages are silently dropped, breaking agent team coordination. High severity for multi-agent users.

8. **[#74644 — Safety classifier falsely flags defensive security remediation, silently downgrades model mid-task](https://github.com/anthropics/claude-code/issues/74644)**  
   *0 comments | [OPEN]*  
   Second report in two days of Fable 5 downgrading to Opus 4.8 during legitimate security work. Undermines trust in the safety system.

9. **[#74598 — Subagent model pin is lost on injected wake/resume turns — bills at waker’s model](https://github.com/anthropics/claude-code/issues/74598)**  
   *0 comments | [OPEN]*  
   Subagents with a pinned model silently switch to the waker’s model on resume, causing unexpected billing and behavior drift.

10. **[#74638 — Background agents/teammates never terminate: shutdown_request unanswered](https://github.com/anthropics/claude-code/issues/74638)**  
    *0 comments | [OPEN]*  
    Finished agents linger as live OS processes indefinitely, wasting resources and confusing session management.

---

## Key PR Progress

Only two pull requests were updated in the last 24 hours:

- **[#73476 — docs: fix GitHub capitalization in README](https://github.com/anthropics/claude-code/pull/73476)**  
  Minor typo fix (`Github` → `GitHub`). No functional change. Still open.

- **[#66854 — "toekn" (closed)](https://github.com/anthropics/claude-code/pull/66854)**  
  Appears to be a spam PR (typo title, no description). Closed without merge.

**Observation:** PR activity is unusually low. No code fixes or features are in flight, despite multiple critical regressions reported today. This may indicate a focus on internal stabilization or a pending hotfix release.

---

## Feature Request Trends

Based on recent issues and upvotes, the community is pushing for:

- **Byte-exact data channels for Workflow scripts** ([#67684](https://github.com/anthropics/claude-code/issues/67684)) – Need to pass arbitrary payloads without corruption in the sandboxed Workflow tool.
- **Session group reordering/pinning** ([#70104](https://github.com/anthropics/claude-code/issues/70104)) – Users want manual control over sidebar session grouping in the desktop app.
- **Permission prompt retraction in channel plugins** ([#74645](https://github.com/anthropics/claude-code/issues/74645)) – Stale DM buttons should be dismissed when permission is resolved elsewhere.
- **Background daemon process naming** ([#74641](https://github.com/anthropics/claude-code/issues/74641)) – Raw version strings as process names make process monitoring difficult; request human-readable labels.
- **Markdown clipboard support on macOS** ([#74628](https://github.com/anthropics/claude-code/issues/74628)) – Copy as Markdown currently loses formatting; users want pasteboard flavors preserved.

---

## Developer Pain Points

Recurring themes from high-traffic and today’s issues:

1. **False-positive safety classifiers** – Multiple reports of legitimate defensive security work (Wazuh deployment, SIEM hardening) being blocked or model-downgraded ([#74610](https://github.com/anthropics/claude-code/issues/74610), [#74615](https://github.com/anthropics/claude-code/issues/74615), [#74644](https://github.com/anthropics/claude-code/issues/74644)). Developers feel incorrectly flagged and left without recourse.

2. **v2.1.201 regression wave** – At least three distinct regressions reported on the same day: VS Code load failure ([#74643](https://github.com/anthropics/claude-code/issues/74643)), turn/message desync ([#74637](https://github.com/anthropics/claude-code/issues/74637)), and background agent zombie processes ([#74638](https://github.com/anthropics/claude-code/issues/74638)). This suggests the release was rushed.

3. **Unintentional model switching** – Several users report Fable 5 silently dropping to Opus 4.8 mid-session without explanation ([#74640](https://github.com/anthropics/claude-code/issues/74640), [#74644](https://github.com/anthropics/claude-code/issues/74644)), often linked to safety classifiers. Loss of capability and billing surprises.

4. **UTF-8 surrogates error** – Two separate issues ([#64777](https://github.com/anthropics/claude-code/issues/64777), [#68737](https://github.com/anthropics/claude-code/issues/68737)) with identical error: `str is not valid UTF-8: surrogates not allowed`. Mid-conversation crash on Windows and macOS. No fix yet.

5. **Permission mode contradictions** – `--permission-mode dontAsk` denies Write/Edit even when `--allowedTools` explicitly grants them ([#74567](https://github.com/anthropics/claude-code/issues/74567)). Confuses headless/CI users.

6. **Stale session indicators** – The “working” indicator stays lit after completion ([#74646](https://github.com/anthropics/claude-code/issues/74646)), requiring app restart to clear. Indicative of state management leaks.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# 🧠 **OpenAI Codex Community Digest – 2026-07-06**

## 🔦 Today's Highlights

The community’s loudest demand remains a **native Linux desktop app** (Issue #11023, 143 comments, 690 👍). A **GPT-5.5 reasoning-token clustering pattern** (Issue #30364) has been flagged by users, correlating with degraded complex-task performance. On the engineering side, multiple PRs landed to fix **TUI crashes (SIGTRAP)** on Intel macOS, improve **autocomplete logic**, and reduce **MCP process leaks**.

---

## 🔥 Hot Issues (Top 10 by Community Activity)

1. **[Issue #11023 – Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)**  
   [Enhancement] 143 comments · 690 👍  
   Users are desperate for a Linux app after battery/performance issues on Mac. The high reaction count makes it the community’s #1 feature request.

2. **[Issue #30364 – GPT-5.5 reasoning-token clustering at 516/1034/1552](https://github.com/openai/codex/issues/30364)**  
   [Bug, Model-behavior] 105 comments · 192 👍  
   A data-driven report shows disproportionate token counts at fixed boundaries, suggesting a model-side artifact that harms complex reasoning. Heavy discussion on possible quantization or batch-size side effects.

3. **[Issue #8648 – Agent replies to earlier messages instead of latest](https://github.com/openai/codex/issues/8648)**  
   [Bug, Context] 83 comments · 55 👍  
   Persistent conversational context mishandling – the agent often responds to an older user message in long threads, breaking workflow.

4. **[Issue #9224 – Codex Remote Control (CLOSED)](https://github.com/openai/codex/issues/9224)**  
   [Enhancement] 57 comments · 405 👍  
   Closed as “released” or “duplicate”? Users still want mobile-to-desktop remote control of the CLI via ChatGPT app. High votes indicate strong demand.

5. **[Issue #29000 – Codex CLI 0.141.0 crashes with SIGTRAP on Intel macOS](https://github.com/openai/codex/issues/29000)**  
   [Bug, CLI] 24 comments · 16 👍  
   Multiple users confirm a “trace trap” crash on Intel Macs. Related to keyboard/TUI exit handling. Several PRs this week directly address this.

6. **[Issue #28507 – “Selected model is at capacity”](https://github.com/openai/codex/issues/28507)**  
   [Bug, Rate-limits] 23 comments · 13 👍  
   Pro subscribers hitting model unavailability even with 5x plan. Frustration about opaque capacity logic and forced model switching.

7. **[Issue #25246 – Business access-tokens broken (401)](https://github.com/openai/codex/issues/25246)**  
   [Bug, Auth] 17 comments · 9 👍  
   Enterprise token management page returns 401. Blocks CI/CD and scripted usage for Business customers.

8. **[Issue #18460 – Persistent “Unable to transcribe audio”](https://github.com/openai/codex/issues/18460)**  
   [Bug, App] 14 comments · 16 👍  
   Voice dictation on Codex Desktop frequently fails. No clear pattern across platforms, but users rely on it for rapid input.

9. **[Issue #29492 – Windows Codex desktop creates empty .git folder, spawns git repetitively](https://github.com/openai/codex/issues/29492)**  
   [Bug, Windows] 12 comments · 8 👍  
   When project is not under Git, the app creates a bogus `.git` directory and triggers infinite git processes, slowing the system.

10. **[Issue #30939 – Usage limits draining 5–10x too fast](https://github.com/openai/codex/issues/30939)**  
    [Bug, Rate-limits] 4 comments (but high recency) · 0 👍 yet  
    New report from today: one message consumes 46% of the 5-hour window. Suggests a server-side billing bug that may be widespread.

---

## 🚀 Key PR Progress (Top 10)

1. **PR #31188 – Preserve managed exec policy after rules parse errors**  
   [Open] Fixes fallback bug where custom `.rules` parse failure cleared the entire policy, ignoring managed sandbox requirements.

2. **PR #31201 – Reduce repeated plugin discovery work during tool assembly**  
   [Open] Caches plugin metadata for 30 seconds and reuses unchanged catalog files, improving tool assembly latency.

3. **PR #30982 – Allow extension-managed Apps authentication**  
   [Open] Trusted host extensions can now provide OAuth/auth for the built-in Codex Apps MCP server, enabling third-party auth flows.

4. **PR #31192 – Flush queued terminal input before exit**  
   [Open] Prevents leftover CSI-u key-release bytes from leaking to the parent shell after shutdown, fixing SIGTRAP on Intel macOS.

5. **PR #31191 – Handle completion separators and popup dismissal**  
   [Open] Fixes redundant spaces inserted on autocomplete acceptance and prevents popup dismissal from wrong token.

6. **PR #30463 – Fix autocomplete targeting between mentions**  
   [Open] Correctly selects the unbound skill mention when cursor sits between `$unbound` and `$bound`, improving TUI snippet insertion.

7. **PR #31189 – Fix cancelled review leaving MCP startup busy**  
   [Open] Stops the TUI from remaining in “Starting MCP servers” state after cancelling an inline review, unblocking subsequent `/review` commands.

8. **PR #31176 – Retry goals after model capacity errors**  
   [Open] Automatically retries active goals when a turn fails due to “model at capacity” – retries consume no user tokens.

9. **PR #30395 – Expose rate-limit reset credit details**  
   [Open] Adds v2 endpoint for available credits and expiry times, enabling a redemption UI without private backend access.

10. **PR #31175 – Add MongoDB thread store and session migration**  
    [Open] Experimental MongoDB backend for thread storage, plus a `migrate-to-mongo` CLI command with progress and rollback support.

---

## 📋 Feature Request Trends

The most demanded features are consistently **platform/accessibility expansions**:  
- **Linux desktop app** (Issue #11023) – by far the highest engagement.  
- **Remote control/CLI from mobile** (Issue #9224) – voted second-highest.  
- **Export chat as Markdown** from the Desktop App (Issue #17241).  
- **Built-in pet creation** (Issue #30507) – a niche ask but reflects interest in playful skill integration.

No new feature requests appear in today’s top issues beyond these well-established themes.

---

## 🛠️ Developer Pain Points

Recurring frustrations cluster around **reliability and infrastructure**:  
- **Rate-limit bugs**: usage draining 5–10x too fast (Issue #30939), “model at capacity” errors (Issue #28507), and credits not being applied after purchase (Issue #19830).  
- **Crash-on-Intel-macOS** (Issues #29000, #30927) – SIGTRAP on CLI startup, partially addressed by PR #31192.  
- **Windows-specific regressions** – empty `.git` folder with runaway git processes (Issue #29492), automation threads not starting (Issue #19011), severe temperature spikes (Issue #30055).  
- **MCP server process leaks** (Issue #30408) – orphaned processes consuming >9 GB RSS over time.  
- **Business/enterprise auth tokens broken** (Issue #25246) blocks CI integrations.  
- **GPT-5.5 quality complaints** (Issue #28885) – subjective but numerous reports of “stupidity” after recent model updates.

The community expects OpenAI to focus on **stability, platform parity, and transparent rate metering** in the coming weeks.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*