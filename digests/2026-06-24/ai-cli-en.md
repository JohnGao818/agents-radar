# AI CLI Tools Community Digest 2026-06-24

> Generated: 2026-06-24 02:51 UTC | Tools covered: 2

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

## Cross-Tool Comparison Report: Claude Code vs. OpenAI Codex (2026-06-24)

### 1. Ecosystem Overview
The AI CLI tool ecosystem continues to mature with both Claude Code and OpenAI Codex investing heavily in security, credential management, and execution reliability. Claude Code has shipped a security‑focused release while grappling with platform fragmentation and token‑waste bugs; OpenAI Codex is undergoing an internal Rust‑based executor rewrite and has delivered a major fix for excessive disk writes. Both communities are prioritising enterprise‑grade features (e.g., credential brokering, sandbox controls) and struggling with model availability and cross‑platform consistency. The divergence in release cadence and community contribution patterns suggests a widening gap in governance models: Anhtropic’s team‑driven approach vs. OpenAI’s rapid alpha iteration with increasing community–enterprise PR engagement.

### 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex |
|--------|-------------|--------------|
| **Open Issues (hot)** | 10 (notable/trending) | 10 (top impact) |
| **Pull Requests (active)** | 1 (single PR updated) | 10 (key PRs, all with activity) |
| **Latest Release** | v2.1.187 (stable) | rust‑v0.143.0‑alpha.12 (alpha) |
| **Release Cadence** | ~1 stable release/day | Multiple alpha releases/day |
| **Community Engagement (issues)** | High (upvoted issues: 51👍, 38👍) | Moderate–High (333👍 for #28224, now closed) |
| **Bug Fix Velocity** | Moderate (critical iOS crash unpatched, Android regression unresolved) | High (massive SQLite log fix shipped in v0.142.0; several PRs merged in 24h) |

- Claude Code has higher community visibility on platform complaints (Android, iOS), but low PR throughput suggests a closed‑source, team‑centric model.
- OpenAI Codex shows intensive open‑source PR activity, with 10 non‑trivial PRs receiving updates in the same period, reflecting a more permissive contribution process.

### 3. Shared Feature Directions

Both communities are converging on the same pain points and feature requests:

- **Security & Credential Management** – Claude Code ships `sandbox.credentials`; Codex has experimental credential broker (PR #28034, #29752). Direct overlap: sandboxed execution with secret isolation.
- **Token/Cost Efficiency** – Claude Code’s auto‑compaction cost bug (#70459) and deep‑research token waste (#65500) mirror Codex’s SQLite log churn (#28224) and false rate‑limiting (#28515). Both communities demand **budget‑aware execution** and **cache reuse**.
- **Model Availability & Reliability** – Claude Code’s Advisor throttling (#69238) and Codex’s `gpt‑5.5` 404 (#26892) show that **server‑side capacity** and **model metadata consistency** are cross‑tool pain points.
- **Cross‑Platform Stability** – Android/Termux breakage on Claude Code (#50270) and macOS `syspolicyd` exhaustion on Codex (#25243, #16767) highlight **native binary portability** as a shared blocker.
- **Accessibility & Internationalisation** – Claude Code’s screen‑reader request (#70425) and unified i18n meta‑issue (#70490) have no Codex analogue yet, but represent a growing industry requirement.

### 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex |
|-----------|-------------|--------------|
| **Primary Focus** | Security sandboxing, research‑grade workflows (deep‑research, skills) | Execution rewrite (Rust), enterprise credential brokering, marketplace controls |
| **Target User** | Independent developers, teams running automated research agents | Enterprise teams, managed‑network environments, Windows/macOS desktop users |
| **Technical Approach** | Single binary (glibc), token‑heavy compaction, Advisor system | Rust‑based rewrite, SQLite‑backed feedback, managed‑network proxy, credential broker |
| **Release Model** | Stable daily releases, community PRs rarely merged | Multiple alpha releases, high community PR acceptance |
| **Platform Support** | Linux, macOS, iOS (Remote Control); Android broken since glibc switch | macOS, Windows, Linux; focus on macOS Gatekeeper issues |
| **Unique Features** | Mermaid diagram requests (#14375), FleetView agent pinning, web4 governance plugin | Marketplace source admission policies, credential broker, `Ultra reasoning` gated feature |
| **Community Vulnerabilities** | iOS crashes (Swift KeyPath), Android breakage, analytics blackout | Windows auto‑update problems, mojibake path handling, `syspolicyd` resource leaks |

- **Security posture**: Codex’s credential broker lives inside a managed‑network proxy; Claude Code’s `sandbox.credentials` is a simpler guard. Codex goes further with network egress attribution (PR #29697).
- **Enterprise readiness**: Codex leads with marketplace source requirements (PR #29690) and session auth for ChatGPT‑hosted MCP (PR #29733) – direct enterprise onboarding features. Claude Code lacks equivalent enterprise plugin controls.
- **Performance & resource usage**: Codex actively fixing disk write issues (85% reduction); Claude Code battling token waste in compaction and subagent loops – both need cost‑optimisation, but Claude Code’s impact is more directly on API spend.

### 5. Community Momentum & Maturity

- **Claude Code** – Strong vocal community (high upvote counts) but low PR activity signals **limited contribution model**. Users are engaged but frustrated (Android breakage, iOS crashes). The team appears to prioritise internal bug fixes over community patches. Momentum is moderate; the tool is maturing in enterprise security but losing trust on platform fragmentation.
- **OpenAI Codex** – Higher PR throughput (10 active PRs vs. 1) and rapid alpha release cadence indicate **faster iteration**. The closure of the major SQLite log issue (#28224, 333👍) shows responsiveness. However, lingering issues (macOS performance, Windows update breakage) and the unresolved `gpt‑5.5` 404 dilute confidence. Maturity is mixed: core engine being rewritten, while peripheral platform issues remain.
- **Overall**: Codex appears more active and open to community contributions; Claude Code is more stable but less agile in fixing platform regressions.

### 6. Trend Signals

1. **Token‑Aware Development** – Both communities explicitly cost‑optimise: compaction bugs, cache reuse, logging reduction. Developers are treating token spend as a first‑class resource metric.
2. **Security‑First Execution** – Sandboxes, credential isolation, and proxy‑owned credential brokers are no longer optional – they are table stakes for enterprise adoption.
3. **Multi‑Platform Fragmentation** – Android, Windows, and even macOS are causing disproportionate pain. The industry must invest in **portable runtimes** (WASM, musl) or accept significant platform exclusion.
4. **Enterprise Plugin Governance** – Codex’s marketplace source requirements and credential broker reflect an impending need for enterprise IT to control plugin supply chains. Expect similar moves from Claude Code.
5. **Web Automation Barriers** – Both tools face sandbox conflicts with browser automation (Claude Code #11791, #43255; Codex Cloudflare challenge #29197). The next wave of AI CLI tools will need first‑class proxy‑aware web automation.
6. **Accessibility & Inclusion** – While only Claude Code has a dedicated accessibility issue, the low engagement suggests this remains an untapped market gap that early adopters could exploit.
7. **Internationalisation** – Multi‑language support is a recurring request across Claude Code (meta‑issue #70490). Codex has no equivalent yet, but the demand is clear for global developer ecosystems.

**Recommendation for technical decision‑makers**:  
- If your team runs in a managed network and needs strict credential governance, **OpenAI Codex** offers more mature building blocks (credential broker, marketplace policies).  
- If you rely on automated research agents and need robust sandboxing of secrets, **Claude Code**’s `sandbox.credentials` and Advisor system are more immediately applicable – but prepare for platform lock‑in and token budget management.  
- For cross‑platform deployment, neither tool satisfies; supplementary workflows (e.g., Dockerised environments) may be necessary until native binaries converge.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-06-24 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following PRs attracted the most community attention (by comment volume and discussion depth) during this period:

**#1298 — fix(skill-creator): run_eval.py reports 0% recall across all queries**  
*Author: MartinCajiao | Status: OPEN*  
This critical fix addresses a systemic bug where `run_eval.py` reports `recall=0%` for every skill description tested (#556, 10+ independent reproductions). The description-optimization loop has been optimizing against noise. The PR patches three root causes: failing to install the eval artifact as a real skill, broken Windows stream reading, and faulty trigger detection with parallel workers. The high comment count reflects that this bug has been blocking skill development for weeks.  
🔗 [PR #1298](https://github.com/anthropics/skills/pull/1298)

**#514 — Add document-typography skill**  
*Author: PGTBoos | Status: OPEN*  
Proposes a skill for typographic quality control in AI-generated documents: orphan word wrap, widow paragraphs, and numbering misalignment. The discussion highlights that these issues affect every Claude-generated document and that users rarely request fixes directly. Community interest centers on defining the right boundary between automated formatting and user intent.  
🔗 [PR #514](https://github.com/anthropics/skills/pull/514)

**#538 — fix(pdf): correct case-sensitive file references in SKILL.md**  
*Author: Lubrsy706 | Status: OPEN*  
Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where `REFERENCE.md` and `FORMS.md` are referenced in uppercase while actual files are lowercase. This breaks on filesystems like HFS+ and APFS. A small but essential reliability fix.  
🔗 [PR #538](https://github.com/anthropics/skills/pull/538)

**#486 — Add ODT skill (OpenDocument text creation and template filling)**  
*Author: GitHubNewbie0 | Status: OPEN*  
Proposes comprehensive ODT/ODS support including document creation, template filling, and ODT-to-HTML conversion. Triggers on any mention of OpenDocument or LibreOffice. Discussion focused on balancing skill scope with the inherent complexity of the format.  
🔗 [PR #486](https://github.com/anthropics/skills/pull/486)

**#210 — Improve frontend-design skill clarity and actionability**  
*Author: justinwetch | Status: OPEN*  
A revision of the existing frontend-design skill to ensure every instruction is executable within a single conversation. The community debate centers around whether skill descriptions should be written for human clarity or machine determinism.  
🔗 [PR #210](https://github.com/anthropics/skills/pull/210)

**#83 — Add skill-quality-analyzer and skill-security-analyzer**  
*Author: eovidiu | Status: OPEN*  
Adds two meta-skills for evaluating other skills across five quality dimensions (structure, security, documentation) and seven security risk categories. Discussion highlighted the meta-nature of these skills—they analyze skills using the skill system itself.  
🔗 [PR #83](https://github.com/anthropics/skills/pull/83)

**#541 — fix(docx): prevent tracked change w:id collision with existing bookmarks**  
*Author: Lubrsy706 | Status: OPEN*  
Fixes document corruption when the DOCX skill adds tracked changes to documents with existing bookmarks. Root cause: OOXML's shared `w:id` namespace across bookmarks, tracked changes, and comments. Hardcoded low IDs (1, 2, 3) in examples conflicted with real document content.  
🔗 [PR #541](https://github.com/anthropics/skills/pull/541)

**#539 — fix(skill-creator): warn on unquoted YAML special characters in descriptions**  
*Author: Lubrsy706 | Status: OPEN*  
Adds pre-parse validation to detect unquoted `description` fields containing `:`, which causes silent YAML parsing failures where descriptions are truncated or split into multiple keys. Related to a broader community concern about YAML fragility in skill definitions.  
🔗 [PR #539](https://github.com/anthropics/skills/pull/539)

---

## 2. Community Demand Trends

From the most-discussed issues, four clear demand clusters emerge:

| Demand Cluster | Key Issues | Signal Strength |
|---|---|---|
| **Skill sharing & team collaboration** | #228 ("Enable org-wide skill sharing"), #189 ("Duplicate skills from overlapping plugins") | **Highest** (14 + 6 comments, 7 + 9 👍) |
| **Skill-creator reliability & Windows compatibility** | #556 ("0% trigger rate in run_eval"), #1169 ("recall=0% on every iteration"), #1061 ("Windows subprocess, encoding bugs") | **Highest** (12 + 3 + 3 comments, 7 + 1 + 1 👍) |
| **Security & trust boundaries** | #492 ("Community skills under anthropic/ namespace"), #1175 ("SharePoint security concerns") | **Moderate** (9 + 4 comments, 2 + 0 👍) |
| **Platform expansion** | #29 ("Usage with Bedrock"), #16 ("Expose Skills as MCPs") | **Moderate** (4 + 4 comments) |

**Key takeaway:** The community's highest-priority demand is *operational reliability* of the skill development toolchain (especially on Windows) and *organizational sharing* of skills. Security trust boundaries and platform portability to MCPs and Bedrock are emerging as medium-term priorities.

---

## 3. High-Potential Pending Skills

The following open PRs have active discussions and appear likely to merge soon:

**#1323 — fix(skill-creator): run_eval trigger detection misses real skill name**  
*Author: Polluelo978 | Status: OPEN*  
A second independent fix for the 0% recall problem, addressing a different root cause: the trigger detection algorithm looking for the wrong skill name. This suggests the community is converging on a complete fix for #556.  
🔗 [PR #1323](https://github.com/anthropics/skills/pull/1323)

**#1099 — skill-creator: fix run_eval.py crash on Windows subprocess pipe**  
*Author: joshuawowk | Status: OPEN*  
[WinError 10038] flood on Windows where every query is recorded as "not triggered." A companion fix to #1050 and #1061.  
🔗 [PR #1099](https://github.com/anthropics/skills/pull/1099)

**#1050 — skill-creator: fix Windows subprocess + encoding bugs**  
*Author: gstreet-ops | Status: OPEN*  
Two one-line fixes for `PATHEXT` resolution and cp1252 encoding on Windows 11.  
🔗 [PR #1050](https://github.com/anthropics/skills/pull/1050)

**#361 — Detect unquoted YAML special characters in description fields**  
*Author: Mr-Neutr0n | Status: OPEN*  
Broader validation than #539, covering `: # { } [ ]` in both `description` and `compatibility` fields.  
🔗 [PR #361](https://github.com/anthropics/skills/pull/361)

**#509 — docs: add CONTRIBUTING.md**  
*Author: narenkatakam | Status: OPEN*  
Addresses the repo's 25% community health score. Adds contribution guidelines including skill structure, testing, and documentation standards.  
🔗 [PR #509](https://github.com/anthropics/skills/pull/509)

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is for **reliable skill development tooling** (especially fixing the `run_eval.py` 0%-recall bug on Windows, which is blocking all description optimization) and for **document format expansion** (typography, ODT, DOCX corruption fixes), rather than for entirely new skill categories—the ecosystem needs to become stable and accessible before the next wave of skills can flourish.

---

# Claude Code Community Digest — 2026-06-24

## Today’s Highlights
Claude Code shipped **v2.1.187** with two security-centric features: a `sandbox.credentials` setting to block sandboxed commands from accessing secrets, and org-configured model restrictions that now propagate into the model picker, `--model`/`/model`, and `ANTHROPIC_MODEL`. On the bug front, a fresh wave of **iOS Remote Control crashes** (issues #70165, #70262, #70382) is generating significant noise, while a deep-dive report on **auto-compaction cost bugs** (#70459) highlights compounding inefficiencies that can waste millions of tokens.

---

## Releases
**v2.1.187** — *24 hours ago*

- **`sandbox.credentials` setting** – Prevents sandboxed commands from reading credential files and secret environment variables.
- **Org-configured model restrictions** – Enforced via the model picker GUI, `--model`/`/model` CLI commands, and `ANTHROPIC_MODEL` environment variable. Restricted models are clearly flagged.

➡ [Full release notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.187)

---

## Hot Issues (10 Noteworthy)

1. **#50270 – v2.1.113+ breaks on Termux/Android (glibc requirement, no JS fallback)**  
   *[Open, 59 comments, 51 👍]* The switch from a JavaScript entry point to a native glibc binary makes Claude Code completely unusable on Android’s Termux. High community outcry — users demand a fallback or a musl-based binary.  
   🔗 [Issue #50270](https://github.com/anthropics/claude-code/issues/50270)

2. **#69238 – “No response from API” error when Advisor triggers**  
   *[Open, 19 comments, 33 👍]* Sonnet users (base model) hit retry loops with “No response from API” when the Advisor feature kicks in. Network checks are fine; appears to be a server‑side capacity or throttling issue specific to the Opus 4.8 advisor.  
   🔗 [Issue #69238](https://github.com/anthropics/claude-code/issues/69238)

3. **#14375 – Mermaid rendering support (diagrams/charts)**  
   *[Open, 9 comments, 38 👍]* One of the most‑upvoted features: native Mermaid diagram rendering inside the TUI. Currently requires copying output to a third‑party renderer.  
   🔗 [Issue #14375](https://github.com/anthropics/claude-code/issues/14375)

4. **#65500 – deep‑research workflow burns millions of tokens on schema‑bound subagent failure**  
   *[Open, 5 comments, 2 👍]* A single subagent failing to emit `StructuredOutput` aborts the entire run — after consuming ~3.5M tokens across three attempts with zero usable output. A costly architectural gap in the new skill system.  
   🔗 [Issue #65500](https://github.com/anthropics/claude-code/issues/65500)

5. **#70165 – iOS app hard‑crashes opening a Remote Control session**  
   *[Open, 9 comments, 2 👍]* Main‑thread stack overflow in Swift KeyPath metadata. Several duplicates (#70262, #70359, #70288) confirm a widespread regression on iOS 26.5 and 27 Beta 2.  
   🔗 [Issue #70165](https://github.com/anthropics/claude-code/issues/70165)

6. **#11791 – Browser automation tools incompatible with web sandbox proxy**  
   *[Open, 8 comments, 14 👍]* Playwright / Puppeteer cannot run inside the sandbox because the proxy doesn’t support HTTPS CONNECT tunneling. Users want either a documented workaround or a sandbox mode that allows it.  
   🔗 [Issue #11791](https://github.com/anthropics/claude-code/issues/11791)

7. **#43255 – Chrome MCP tools: “Navigation to this domain is not allowed” on all domains**  
   *[Open, 16 comments, 8 👍]* The Chrome MCP integration (v1.0.66) blocks every domain, making web automation useless. No workaround known — users suspect a broken allowlist.  
   🔗 [Issue #43255](https://github.com/anthropics/claude-code/issues/43255)

8. **#64503 – Claude Code Analytics not updated since May 12**  
   *[Open, 4 comments, 6 👍]* The web analytics dashboard has been frozen for six weeks. Users rely on it for cost tracking and session metrics; silence from the team is frustrating.  
   🔗 [Issue #64503](https://github.com/anthropics/claude-code/issues/64503)

9. **#70459 – Auto‑compaction: two compounding cost bugs (stale precompute + repeated cache creation)**  
   *[Open, 2 comments, 2 👍]* A detailed report showing that `/compact` uses stale precomputed summaries (keeping ~200K tokens verbatim), and the prefix is then *re‑created* instead of *cache‑read*, doubling cost. Runner‑up for “most expensive bug of the week”.  
   🔗 [Issue #70459](https://github.com/anthropics/claude-code/issues/70459)

10. **#70425 – Make Claude Code usable out‑of‑the‑box for blind/screen‑reader users**  
    *[Open, 2 comments, 0 👍]* A blind accessibility architect details missing audio cues, poor heading discipline, and non‑humanized announcements. Low community engagement but high impact for inclusion.  
    🔗 [Issue #70425](https://github.com/anthropics/claude-code/issues/70425)

---

## Key PR Progress

Only **one pull request** saw updates in the last 24 hours:

- **#20448 – Add web4‑governance plugin for AI governance with R6 workflow**  
  *[Open, no comments]* Adds a “web4” governance plugin featuring T3 trust tensors, entity witnessing, and R6 audit trails. The repository owner has not yet engaged.  
  🔗 [PR #20448](https://github.com/anthropics/claude-code/pull/20448)

*PR activity remains very low — the team appears focused on bug fixes and the v2.1.187 release rather than merging community contributions.*

---

## Feature Request Trends

- **Internationalization / i18n** — Multiple requests (Spanish #65963, Portuguese #66637, Japanese #65963 dupes) now unified in a new meta‑issue (#70490) proposing locale JSON files similar to the Desktop app approach. High cross‑language demand.  
- **Mermaid diagram rendering** (#14375) continues to be the single most‑upvoted feature; users want inline flowcharts, sequence diagrams, and architecture visuals in the TUI.  
- **Accessibility improvements** (#70425) — screen‑reader‑first cues, audio notifications, and stricter heading semantics for power‑users who rely on VoiceOver/JAWS.  
- **Hook callback control‑plane** (#65179) — a server with per‑invocation UUIDs enabling hooks to trigger session operations (e.g., compaction) instead of being read‑only observers.  
- **Auto‑pin new background agents** (#70488) — in the FleetView (`claude agents`), users want newly created agents pinned by default to avoid manual `Ctrl+T` after every spawn.

---

## Developer Pain Points

- **Android/Termux breakage** (#50270) — the glibc binary switch effectively kills Claude Code for an entire platform. No fallback offered, leaving Android developers stuck on v2.1.112.  
- **iOS Remote Control crashes** — at least 5 distinct issues (#70165, #70262, #70359, #70288, #70382) all report instant crashes on session open. The Swift KeyPath stack overflow suggests a regression in the latest iOS app build.  
- **Token‑wasting bugs** — deep‑research subagent failures (#65500) and auto‑compaction inefficiencies (#70459) are burning users’ budgets with no usable output. Community frustration is palpable, especially for teams with tight API quotas.  
- **Web sandbox limitations** — browser automation tools (#11791) and Chrome MCP (#43255) are blocked by security proxies that lack CONNECT tunneling support, crippling common testing workflows.  
- **Analytics blackout** (#64503) — six weeks without cost/usage data undermines trust and makes capacity planning impossible.  
- **False‑positive safety filters** (#70458) — benign prompts (e.g., “don’t read this folder”) are erroneously flagged as policy violations, disrupting flow and eroding confidence in the guardrail system.  
- **Image/file rendering in desktop apps** — multiple reports (#69279, #69780, #65677, #67869) of file‑attachment chips being non‑clickable or showing empty previews on both macOS and Windows desktop clients. The inconsistency across platforms suggests a deeper UI component issue.  

---

*Generated 2026-06-24 from `git@github.com:anthropics/claude-code` data.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-06-24

## Today's Highlights
A flurry of Rust‑based alpha releases (`v0.143.0‑alpha.x`) signals a major internal rewrite of the Codex executor. The week’s biggest win is the closure of issue #28224 – the infamous SQLite feedback log that could write ~640 TB/year – thanks to three merged PRs. Meanwhile, the `gpt‑5.5` model 404 error continues to affect users across CLI and Desktop, with 84 comments and no fix yet.

## Releases
- **Multiple `rust‑v0.143.0‑alpha` releases** (alpha.3 through alpha.12) – no detailed changelog provided; likely iterative updates to the Rust‑based Codex executor.

## Hot Issues (Top 10 by Impact)
1. **`gpt‑5.5` model 404 in both Desktop and CLI**  
   [#26892](https://github.com/openai/codex/issues/26892) (CLOSED, 84 comments, 28 👍) – Model metadata shows `gpt‑5.5` as available, but actual requests fail with 404. Duplicate reports (#26910) confirm widespread breakage since June 7. Still unresolved despite closure.

2. **SQLite feedback logs write ~640 TB/year**  
   [#28224](https://github.com/openai/codex/issues/28224) (CLOSED, 72 comments, 333 👍) – Massive disk write endurance issue. Three PRs (merged in `v0.142.0`) cut 85% of logs. *Community reaction: highly upvoted, relief that fix shipped.*

3. **macOS relaunch loop exhausts `syspolicyd` file descriptors**  
   [#25243](https://github.com/openai/codex/issues/25243) (OPEN, 46 comments, 3 👍) – `Codex.app` relaunches repeatedly, blocking other apps. Multiple duplicates (#28071, #27662) indicate a systemic Gatekeeper issue on macOS.

4. **`syspolicyd`/`trustd` CPU spikes on macOS**  
   [#16767](https://github.com/openai/codex/issues/16767) (OPEN, 19 comments, 26 👍) – Persistent high CPU from trust evaluation after launching Codex Desktop.

5. **Codex WebSearch blocked by Cloudflare challenge (403)**  
   [#29197](https://github.com/openai/codex/issues/29197) (OPEN, 11 comments) – On Windows, search requests return a Cloudflare managed‑challenge page. Blocks key tool‑call functionality.

6. **SQLite log churn remains after `rust‑v0.142.0`**  
   [#29532](https://github.com/openai/codex/issues/29532) (OPEN, 10 comments, 7 👍) – Partial fix: `responses_websocket` logging reduced, but `TRACE target=log` still churns in `logs_2.sqlite`.

7. **“Model is at capacity. Please try a different model.”**  
   [#28515](https://github.com/openai/codex/issues/28515) (OPEN, 7 comments, 3 👍) – Rate‑limit false positives for Pro users on `gpt‑5.5 xhigh`. Suggests backend capacity mismanagement.

8. **`config.toml` MCP paths stale after Windows auto‑update**  
   [#26011](https://github.com/openai/codex/issues/26011) (OPEN, 6 comments) – MCP startup fails with “os error 3” because old bin directories are retained. Affects `node_repl` and other MCP servers.

9. **Windows: mojibake Chinese user path creates endless runtime staging dirs**  
   [#28258](https://github.com/openai/codex/issues/28258) (CLOSED, 6 comments) – `C:\Users\<ChineseUser>` leads to repeated creation of `.staging` directories under garbage paths, filling disk.

10. **Crash regression of a previously fixed bug**  
    [#15752](https://github.com/openai/codex/issues/15752) (OPEN, 6 comments, 1 👍) – Silent crash during task execution reappeared after update (regression of #11016). Frustrating for users relying on task completion.

## Key PR Progress (Top 10)
1. **[#29765](https://github.com/openai/codex/pull/29765) – Ignore local curated plugins when remote catalog is active**  
   Suppresses `openai‑curated` plugins in favor of remote marketplace. Preserves `openai‑api‑curated` and non‑Codex‑backend auth.

2. **[#29697](https://github.com/openai/codex/pull/29697) – Attribute network requests to the exact exec on Linux**  
   Fixes managed‑network proxy attribution: each concurrent exec now gets its own connection tracking instead of sharing the same proxy ingress.

3. **[#29690](https://github.com/openai/codex/pull/29690) – Add marketplace source requirements**  
   Enterprise‑friendly TOML table for declaring allowed marketplace sources. Uses config precedence without custom merging logic.

4. **[#29752](https://github.com/openai/codex/pull/29752) – Integrate experimental credential broker**  
   First Codex integration layer for the proxy‑owned credential broker (#28034). Brokered values survive shell snapshots, dummy values removed on exit from managed network.

5. **[#28034](https://github.com/openai/codex/pull/28034) – Experimental local credential broker**  
   Proxy‑side slice: moves injectable credentials behind the managed‑network proxy, preventing child processes from exfiltrating real values.

6. **[#29733](https://github.com/openai/codex/pull/29733) – Allow ChatGPT‑hosted MCP servers to use session auth**  
   Decouples session authentication from Codex Apps–specific server names, enabling other ChatGPT‑hosted MCP endpoints to opt in.

7. **[#29762](https://github.com/openai/codex/pull/29762) – Reuse compacted history replacement for new context windows**  
   Fixes missing `item_ids` when creating a fresh context window by sharing the central compacted‑history path.

8. **[#29758](https://github.com/openai/codex/pull/29758) – Fix token‑budget compaction baselines**  
   Resolves P2 review comments: pre‑turn compaction now captures step context from the correct model, preventing stale baselines after budget‑driven resets.

9. **[#29709](https://github.com/openai/codex/pull/29709) – Add gated Ultra reasoning effort**  
   Ultra reasoning (max backend effort) is discoverable only when both the model catalog and `multi_agent_mode` feature are active. No new backend token required.

10. **[#29711](https://github.com/openai/codex/pull/29711) – Let image generation extension hosts control output persistence**  
    Extensions can now return images without writing them to disk or providing a local path to the model.

## Feature Request Trends
- **UI/UX improvements**: Users want a close button for “steers” (#16015, 5 👍), a `Cmd+Enter` submission shortcut (#16111, 4 👍), and the ability to disable the `@` chat search feature (#29231, 2 👍).
- **Git workflow customization**: Configurable `base_branch` in `environment.toml` for non‑`main` workflows (#15768, 7 👍).
- **Enterprise management**: Marketplace source admission policies (PR #29690, #29753) and credential brokering (PR #28034) reflect growing demand for controlled plugin ecosystems and secure credential handling.

## Developer Pain Points
- **macOS performance**: Multiple open issues (e.g., #25243, #16767, #28071, #27662) describe `syspolicyd` resource exhaustion, high CPU spikes, and relaunch loops – affecting the entire system, not just Codex.
- **Model availability**: `gpt‑5.5` 404 errors (#26892, #26910) have been unresolved for weeks, blocking users from the latest model despite it being listed.
- **Excessive disk writes**: SQLite logging remains a pain even after the 85% reduction (#28224, #29532). Users on macOS still observe high churn in `logs_2.sqlite`.
- **Windows‑specific breakage**: Stale MCP paths after auto‑update (#26011), mojibake user‑directory runtime folders (#28258), and bundled plugins breaking after every Microsoft Store update (#26792) erode trust in automatic updates.
- **False rate‑limiting**: Both “model at capacity” (#28515) and “You’re out of Codex messages” (#24445) erroneously appear despite remaining quota, disrupting long coding sessions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*