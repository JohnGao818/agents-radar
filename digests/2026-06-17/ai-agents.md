# OpenClaw 生态日报 2026-06-17

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-17 03:40 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，这是为您生成的 OpenClaw 项目 2026 年 6 月 17 日 动态日报。

---

# OpenClaw 项目日报 — 2026-06-17

## 1. 今日速览

今日项目活跃度极高，过去 24 小时内共产生 1000 条 Issues 和 PR 更新，社区参与度强劲。核心变更集中在渠道稳定性（Telegram/WhatsApp 结构化消息修复）和长期存在的稳定性 Bug（子代理完成丢失、信号守护进程竞态条件）的修复 PR 推进上。v2026.6.8 版本已于近期发布，重点增强了消息传递的健壮性。目前，PR 积压数量仍然较大（409 条待合并），社区修复热情高涨，但合并效率有待观察。

## 2. 版本发布

**版本号:** `v2026.6.8`
**发布日期:** 2026-06-08 附近
**主要亮点：**

- **增强的渠道交付：** 此版本专注于提升 Telegram 和 WhatsApp 两个核心渠道的稳定性和渲染能力。
    - **Telegram：** 现在可以更好地渲染结构化文本，支持表格、列表、可展开的引用块、保留的换行符，以及基于 CLI 的回复。
    - **WhatsApp：** 现在能正确应用配置的 ACP 绑定。
- **破坏性变更：** 无。
- **迁移注意事项：** 更新到此版本后，Telegram 用户应能即刻体验到更丰富的消息展示效果；WhatsApp 用户需确认 ACP 绑定配置是否正确。

## 3. 项目进展

在过去 24 小时内，共有 91 个 PR 被合并或关闭，项目在多条战线上取得进展。

- **基础设施与自动化：** `#68936 Autofix: add PR review autofix pipeline + Windows daemon` 被合并，引入了基于 Claude Agent SDK 的自动化 PR 审查修复流水线和 Windows 后台守护进程，这有望提高代码审查和迭代效率。
- **UI 与功能增强：** `#93301 fix(skill-workshop): add Global/Selected-agent scope toggle to Control UI` 被合并，解决了多代理场景下 Skill Workshop 面板显示空白的问题，提升了多代理管理体验。
- **关键 Bug 修复：**
    - `#93821 fix(qmd): strip mcporter daemon startup logs from stdout before JSON.parse` 合并，修复了内存搜索组件 `mcporter` 启动时日志干扰导致的崩溃问题 (#59808)。
    - `#93822 fix(slack): forward identity (username/icon) to chat.update for edited messages` 合并，修复了 Slack 上编辑后的消息会丢失自定义名称和头像的问题 (#58737)。
    - `#93890 feat(telegram): export sender isBot field to agent context` 合并，使 Agent 现在能区分 Telegram 消息是由真人用户还是其他 Bot 发送的。

## 4. 社区热点

今日讨论热度最高的议题反映了社区对平台扩展性和数据完整性的关注。

- **#75 Linux/Windows Clawdbot Apps** (评论 109 | 点赞 79)：这是一个长期存在的功能请求，要求为 Linux 和 Windows 提供与 macOS 同等功能的桌面客户端。高评论数和点赞数表明社区对此有强烈的跨平台需求。
    - 链接: `https://github.com/openclaw/openclaw/issues/75`

- **#44925 Subagent completion silently lost** (评论 19): 关于子代理任务在多种故障模式下（超时、驱逐、静默失败）的结果丢失问题，是社区对 Agent 编排可靠性的核心担忧，引发了深入的技术讨论。
    - 链接: `https://github.com/openclaw/openclaw/issues/44925`

- **#22676 Signal daemon stop() race condition** (评论 17): 关于信号守护进程在重启时的竞态条件导致进程孤儿和发送失败。这个问题源于并发编程的复杂性，社区关注度高。
    - 链接: `https://github.com/openclaw/openclaw/issues/22676`

## 5. Bug 与稳定性

过去 24 小时内的 Bug 报告主要集中在会话状态丢失、消息丢失和回归问题上，稳定性隐患依然存在。

- **严重 (P1/Platinum/Diamond)：**
    - **#44925 [Bug]: Subagent completion silently lost** (P1, Platinum) — 子代理任务结果在超时、驱逐等场景下静默丢失。已有关联 PR，需关注合并进度。
        - 链接: `https://github.com/openclaw/openclaw/issues/44925`
    - **#22676 Signal daemon restart race condition** (P1, Diamond) — 信号守护进程重启导致进程孤儿和发送失败。已有关联 PR。
        - 链接: `https://github.com/openclaw/openclaw/issues/22676`
    - **#62505 [Bug]: Coding Agent never completes anything** (P1, Diamond) — 编码 Agent 在 2026.4.2 之后出现回归，完全无法完成任务。这是一个严重的可用性 Bug，影响了核心功能。
        - 链接: `https://github.com/openclaw/openclaw/issues/62505`
    - **#73148 Image tool: Failed to optimize image when sharp is not installed** (P1, 新报告) — 缺少可选依赖 `sharp` 时，图片工具会抛出晦涩难懂的通用错误信息，影响用户排查问题。
        - 链接: `https://github.com/openclaw/openclaw/issues/73148`
- **中等 (P2)：**
    - **#58450 Agent can promise a later follow-up without starting any actual follow-up action** (P2, Diamond) — Agent 可能会“口嗨”承诺后续操作，但实际上并未执行，破坏用户信任。此问题尚未有关联的修复 PR。
        - 链接: `https://github.com/openclaw/openclaw/issues/58450`
    - **#78308 [Feature]: Channel-mediated approval for MCP tool calls** (P2, Diamond) — 虽然标记为 Feature，但本质上是对潜在安全风险的修复，要求 MCP 工具调用也纳入审批流程。
        - 链接: `https://github.com/openclaw/openclaw/issues/78308`

## 6. 功能请求与路线图信号

社区提出的新功能需求显示出对 Agent 能力精细化控制和安全边界扩展的期望。

- **提案 1: 上下文感知的持续工作 (PR #85651):** 名为 `context-pressure-aware continuation` 的大型 PR 被提交。它允许 Agent 在上下文窗口压力过大时，主动请求继续工作、委托或压缩上下文。这代表 Agent 自治能力的重大升级，若被合并，将深刻改变长会话处理范式。
    - 链接: `https://github.com/openclaw/openclaw/pull/85651`

- **提案 2: 私有网络访问控制 (Issue #39604):** 提出增加 `tools.web.fetch.allowPrivateNetwork` 配置项，以允许 `web_fetch` 工具访问内部网络。这是对工具安全边界的细化。
    - 链接: `https://github.com/openclaw/openclaw/issues/39604`

- **提案 3: 每 Agent 的 Wiki 配置 (Issue #63829):** 要求为每个 Agent 创建独立的 `memory-wiki` 隔离知识库。这直接回应了社区对多 Agent 环境下数据隔离的强烈需求，可能成为未来版本的重点特性。
    - 链接: `https://github.com/openclaw/openclaw/issues/63829`

## 7. 用户反馈摘要

从今日的 Issue 评论和描述中，可以提炼出以下真实的用户声音：

- **痛点：消息丢失与上下文混乱。** 多个 Issue（#44925、#32296、#62505）描述了 Agent 回复错乱、执行结果丢失或无法完成任务的场景。用户明确指出“这次真的让我很痛苦”（#62505），影响日常工作流。这反映了 Agent 编排的可靠性仍是当前最大的用户痛点。
- **痛点：配置误解与环境不友好。** 用户反馈配置项（如 `compaction.model`）被忽略 (#57901)，以及对缺少可选依赖的错误提示不够友好（#73148）。这些细节问题增加了用户的配置和排错成本。
- **诉求：更精细的控制。** 用户希望获得更多控制权，例如可配置流式传输看门狗超时（#68596），以及允许 Agent 访问内部网络（#39604），这表明用户正在尝试将 Agent 部署到更复杂的生产环境中。

## 8. 待处理积压

以下为长期未关闭但影响重大的项，建议维护团队关注和排期。

- **重要 Issue:**
    - **#75 Linux/Windows Clawdbot Apps**: 自创建以来已有近 6 个月，社区需求明确（109条评论，79个赞）。暂无明确修复 PR，是跨平台生态的关键缺口。
    - **#45765 HOME路径嵌套Bugs**: 中国用户反馈的关于环境变量 `OPENCLAW_HOME` 设置导致目录嵌套的 Bug，已存在 3 个月，影响特定用户场景。
- **长期待合并 PR:**
    - **#69822 feat(session-message-events) socket.drain**: 一个大型特性 PR，旨在更可靠地通知下游系统会话已失效。自 4 月提出，等待作者响应超一个月，但因其涉及渠道、UI 等多个模块且风险较高，需仔细评估。
    - **#89569 feat(channels): add pre-auth access requests and grouped DM allowlists**: 针对 Telegram 和 WhatsApp 的访问控制增强，功能完善且有视频演示，但也已等待作者响应两周以上。这些 PR 的长期停滞可能打击社区贡献者的积极性。

---

## 横向生态对比

好的，以下是根据您提供的 OpenClaw 和 Hermes Agent 两份日报生成的横向对比分析报告，聚焦技术决策者和开发者关心的核心维度。

---

# 个人 AI 助手开源生态横向对比分析报告（2026-06-17）

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态处于 **高活跃、高痛点并存** 的快速演进期。两个明星项目（OpenClaw、Hermes Agent）日均产生超 1000 条 Issue/PR 更新，社区对 **多渠道消息交付、Agent 编排可靠性、企业级多租户能力** 的需求集中爆发。然而，项目均面临合并瓶颈（OpenClaw 积压 409 PRs，Hermes 合并率不足 10%），大量严重 Bug（如子代理结果丢失、工具调用损坏）尚未闭合，表明生态在功能扩张期尚未完成质量巩固。

## 2. 各项目活跃度对比

| 指标 | OpenClaw | Hermes Agent |
|------|----------|--------------|
| **过去 24h 更新总量** | ~1000 条（Issue + PR） | ~100 条（各 50） |
| **合并/关闭 PR 数** | 91 | 4 |
| **合并/关闭 Issue 数** | 未单独统计，含在 PR 中 | 5 |
| **最近 Release** | v2026.6.8（2026-06-08） | 无 |
| **PR 积压** | 409 条待合并 | 未公布，但合并效率极低 (4/50) |
| **严重 Bug (P1) 数** | 4 个（子代理丢失、信号守护进程竞态、编码 Agent 不可用、图片工具错误） | 1 个（工具调用损坏，开放中） |
| **健康度评估** | **中高**: 高活跃度 + 版本迭代快，但合并瓶颈大、Bug 治理滞后 | **低**: 社区热但审查卡顿，核心工具链存在开放 P1 Bug，功能推进缓慢 |

**关键洞察**：OpenClaw 合并能力明显更强（91 vs 4），但积压规模也更大；Hermes 的合并效率严重不足，可能因维护者带宽或审查流程过严。

## 3. OpenClaw 在生态中的定位

- **优势**：
  - **渠道交付深度**：Telegram/WhatsApp 结构化消息修复（表格、引用块、ACP 绑定）已落地，Hermes 仍受 Markdown 转义困扰。
  - **版本迭代节奏**：近 10 天发布 v2026.6.8，Hermes 近期无正式版本。
  - **自治能力探索**：提交了 `context-pressure-aware continuation` 大型 PR，超前于 Hermes 的实时语音方案。
- **与 Hermes 的差异**：
  - **技术路线**：OpenClaw 偏向 **多通道 Agent 框架**（Signal 守护进程、Agent 上下文路由），Hermes 侧重 **多模型平台 + 扩展技能生态**（Codex 后端、graphify 等 4 个新技能）。
  - **社区规模**：单一 Issue #75（桌面客户端）获 79 赞、109 评论；Hermes 最高热题 #34352 仅 6 评论。OpenClaw 声量显著更大。
- **核心短板**：子代理结果丢失（#44925）和编码 Agent 彻底不可用（#62505）是可用性红线，需优先解决。

## 4. 共同关注的技术方向

以下需求在两个项目中同时涌现，代表了社区共识：

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|----------|----------|
| **多租户 / 数据隔离** | OpenClaw、Hermes | 每 Agent 独立 Wiki（OpenClaw #63829）；多租户记忆隔离（Hermes #34352） |
| **渠道消息格式化一致性** | OpenClaw、Hermes | Telegram Markdown / 结构化内容（OpenClaw v2026.6.8；Hermes #6388） |
| **Agent 编排可靠性** | OpenClaw、Hermes | 子代理结果丢失（OpenClaw #44925）；工具调用管道损坏（Hermes #6841） |
| **Agent 自治能力升级** | OpenClaw、Hermes | 上下文感知持续工作（OpenClaw PR #85651）；实时语音交互（Hermes PR #47330） |
| **认证与配置简化** | OpenClaw、Hermes | 依赖缺失错误提示友好（OpenClaw #73148）；Qwen CLI 认证兼容（Hermes #46771） |

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
|------|----------|--------------|
| **功能侧重** | 多渠道消息交付 + 会话稳定性（Telegram/WhatsApp/Slack 修复为主） | 多模型集成 + 技能生态（GPT-5.5、Qwen、graphify 等插件） |
| **目标用户** | 团队/企业部署 AI 助手（需要跨平台 bot） | 开发者 / 研究者（灵活切换模型、扩展技能） |
| **技术架构** | 独立守护进程（Signal daemon）+ 子 Agent 调度（agent/skill-workshop） | Gateway 插件架构（Mattermost/Daily）+ Codex OAuth 后端 |
| **迭代优先级** | 先稳住渠道可靠性，再扩展自治能力 | 先增强模型兼容与技能丰富度，再处理平台 Bug |
| **当前核心瓶颈** | 合并效率与严重 Bug 治理（409 PRs 积压，1 个 Diamond Bug） | 审查延迟与工具链稳定性（工具调用损坏开放中） |

## 6. 社区热度与成熟度

- **高热度 + 快速迭代阶段**：**OpenClaw** 属于此列。日均 1000 条更新、近期版本发布、大量新功能 PR（上下文持续工作、Windows 守护进程），表明项目仍在大量堆积功能。但 P1/Diamond Bug 未闭合，质量巩固滞后。
- **中低热度 + 审查瓶颈阶段**：**Hermes Agent**。日均 100 条更新，但合并率仅 8%，大量功能 PR（实时语音、Mattermost 增强）等待合并。社区有活跃的功能提案，但维护者响应慢，可能造成贡献者流失。
- **共同特征**：两个项目均未达到稳定期，用户反馈“配置痛苦”“稳定性第一”的频率很高，说明用户体验一致是短板。

## 7. 值得关注的趋势信号

1. **Agent 自治从“响应”转向“主动管理”**：OpenClaw 的上下文感知持续工作（PR #85651）和 Hermes 的实时语音交互（PR #47330），预示 Agent 未来将主动决定何时继续/委托/压缩上下文，而非等待用户输入。这对长会话、高复杂度任务的架构设计有重要参考价值。

2. **企业级多租户需求爆发**：两个项目同时出现多租户/数据隔离诉求（OpenClaw #63829，Hermes #34352），说明单个 Agent 工具正向多方共享平台演进。开发者需提前考虑资源隔离、权限分层、记忆分区。

3. **平台一致性成本被低估**：Telegram 的 Markdown 转义、Signal 审批流断裂、Feishu 卡片解析失败……多平台带来的“平台特有 Bug”正在成为项目管理的主要负担。后续项目应设计统一的中间消息抽象层，减少重复适配。

4. **配置体验是留存门槛**：用户普遍抱怨“配置即折磨”——依赖缺失错误晦涩、认证自动发现失效、MCP 静默失败。这对开源项目造成的隐性流失可能比功能缺失更严重。建议优先投入交互式配置向导和错误兜底提示。

**对开发者建议**：
- 若追求快速部署多通道助手：OpenClaw 更成熟，但需监控其严重 Bug 修复进度；
- 若需要灵活模型切换和技能生态：Hermes 更合适，但需容忍较低发展节奏和偶尔的工具中断；
- 两个项目均处于质量爬坡期，生产环境部署需谨慎规划容灾和回退方案。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为一名 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 Hermes Agent GitHub 数据，为您生成一份客观、专业的项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-06-17

## 1. 今日速览

项目在过去24小时内保持了极高的活跃度，共产生50条Issue更新和50条PR更新。然而，与高并发的提交和讨论形成对比的是，代码合并速度相对缓慢，仅关闭了4个PR和5个Issue，这暗示着项目可能正面临严重的审查瓶颈。社区讨论的焦点集中在**多租户架构、平台兼容性（Telegram、macOS）、配置发现与认证**等方向，反映了项目在从单用户工具向企业级、多平台协作平台演进过程中遇到的真实挑战。

## 2. 版本发布

无

## 3. 项目进展

今日项目推进有限，仅有1个Pull Request被合并/关闭，另有关闭的Issue若干。主要进展体现在对边缘场景的修复和文档/配置的清理。

- **PR #28981 [CLOSED]**: 修复了 `.stash` 目录被错误扫描为技能（Skill）文件的问题。该PR通过在 `skill_utils.py` 和 `skill_commands.py` 中添加排除逻辑，避免了技能同步工具产生的临时工作数据干扰核心功能。这是一个针对开发者体验的微小但重要的修复。
  - 链接: [NousResearch/hermes-agent PR #28981](https://github.com/NousResearch/hermes-agent/pull/28981)

- **Issue #26599 [CLOSED]**: 修复了 `gpt-5.5` 等模型通过 Codex 后端调用时，因传递 `extra_headers` 字段而返回 HTTP 400 的错误。此Bug影响所有使用Codex OAuth路由的模型，修复后恢复了核心模型的可用性。
  - 链接: [NousResearch/hermes-agent Issue #26599](https://github.com/NousResearch/hermes-agent/issues/26599)

- **Issue #46789 [CLOSED]**: 修复了macOS桌面应用进程执行时发生段错误（exit code -11）的严重问题。受影响工具包括 `terminal`、`execute_code` 等，使得桌面端在macOS上基本不可用。此关闭表明该问题已被定位并修复。
  - 链接: [NousResearch/hermes-agent Issue #46789](https://github.com/NousResearch/hermes-agent/issues/46789)

## 4. 社区热点

今日社区讨论最热烈的问题反映了用户对 **多代理、多租户架构** 和 **跨平台兼容性** 的强烈需求。

- **讨论焦点: 多租户与长期会话管理**
  - **Issue #34352**: 该问题引发了关于“多租户Hermes”的哲学和技术讨论。作者提出，由于记忆操作绕过了Hook系统，导致租户隔离在核心代码层面难以实现。作者分享了自己在生产环境运行多租户代理的实践和修复方案，引发了社区对其他多用户、多上下文场景的讨论。这代表了项目从个人助手向平台化演进的关键技术诉求。
    - 链接: [NousResearch/hermes-agent Issue #34352](https://github.com/NousResearch/hermes-agent/issues/34352)

- **痛点焦点: 平台消息格式处理**
  - **Issue #6388**: 报告了Telegram消息中，MarkdownV2转义规则破坏了项目符号列表的显示。用户希望看到渲染后的列表，却看到了被转义的 `\-` 符号。这个问题虽不致命但非常影响用户体验，评论数高达6条，说明该Bug影响了大量使用Telegram bot的用户。
    - 链接: [NousResearch/hermes-agent Issue #6388](https://github.com/NousResearch/hermes-agent/issues/6388)

## 5. Bug 与稳定性

今日报告的Bug中，**工具调用损坏（P1）** 和 **认证/配置问题** 是核心风险点，已有多项提交进行针对性修复。

- **P1 严重: 工具调用管道损坏**
  - **Issue #6841**: 报告了一个间歇性发生的严重问题：工具名称和JSON参数在被传递到验证器前发生损坏，导致工具调用普遍失败。该问题影响所有工具，且症状多样，包括工具名重复、参数格式错误等。当前仍为 **OPEN** 状态，需紧急关注。
    - 链接: [NousResearch/hermes-agent Issue #6841](https://github.com/NousResearch/hermes-agent/issues/6841)

- **P2 重大: 认证与配置兼容性**
  - **Issue #46771**: Hermes与最新版Qwen CLI v0.18.1的认证不兼容，导致 `qwen-oauth` 集成失效。 **无对应fix PR**。
    - 链接: [NousResearch/hermes-agent Issue #46771](https://github.com/NousResearch/hermes-agent/issues/46771)
  - **Issue #47361**: 因18个 `HermesOverlay` 条目缺少 `extra_env_vars`，导致凭证检测发生偏移，影响大量API Key认证的Provider。 **无对应fix PR**。
    - 链接: [NousResearch/hermes-agent Issue #47361](https://github.com/NousResearch/hermes-agent/issues/47361)
  - **Issue #46856**: OpenRouter返回的 `Provider returned error` 未正确分类为限流错误，导致回退机制在每个回合都会重置，无法启用正确的降级策略。 **无对应fix PR**。
    - 链接: [NousResearch/hermes-agent Issue #46856](https://github.com/NousResearch/hermes-agent/issues/46856)

- **P2 重大: 平台特定功能缺陷**
  - **Issue #46947**: 邮件平台网关中，发送新邮件时Subject被硬编码为“Re: Hermes Agent”，无法自定义，严重限制了邮件作为自动化报告通道的可用性。
    - 链接: [NousResearch/hermes-agent Issue #46947](https://github.com/NousResearch/hermes-agent/issues/46947)
  - **Issue #46866**: Signal平台网关中，用户对危险命令的批准/拒绝响应被错误路由为普通消息，导致审批流程完全失效。 **无对应fix PR**。
    - 链接: [NousResearch/hermes-agent Issue #46866](https://github.com/NousResearch/hermes-agent/issues/46866)

## 6. 功能请求与路线图信号

今日涌现了多个重要的功能请求，展示了用户对 **专业化、平台化** 和 **低代码配置** 的迫切需求。

- **新技能与多模态**: PR #47576 一次提交了 `graphify`（知识图谱）、`ui-ux-pro-max`、`impl-validator` 和 `suede-promo` 四个可选技能，表明社区正在围绕核心Agent构建丰富的应用生态。
- **实时语音交互**: PR #47330 提出了一个深入集成的实时语音对话平台方案（基于 Daily + Deepgram + Cartesia），以Gateway插件形式运行在Agent会话进程中，而非外部编排器。这表明项目正在向更自然、更实时的交互模式探索。
- **基础架构与配置**: Issue #34352 关于多租户的讨论、PR #47600 关于在运行时footer中显示Provider/Model信息的建议，以及PR #47598 关于为每个用户配置自动配置git凭证的功能，都指向了项目从单机工具向企业级、多用户服务演进的方向。
- **Mattermost平台支持**: PR #47593 为Mattermost适配器添加了频道发现、原始ID定位、消息删除和反应等高级功能，补齐了与Slack/Discord等参考实现的功能差距。

## 7. 用户反馈摘要

从今日的Issues评论中，可以提炼出以下真实用户痛点：

- **“配置即折磨”**: 多位用户反馈配置过程不透明、易出错。例如MCP服务器的静默失败（#31246），自定义模型的自动发现缺失（#10011），以及Qwen CLI认证的兼容性问题（#46771）。用户期望更智能的“自动发现”和更清晰的错误反馈。
- **“平台化带来了平台特有的麻烦”**: 随着支持平台增多，平台特有的Bug开始凸显。Telegram的Markdown渲染问题（#6388, #47048）、Signal的审批流断裂（#46866）、Feishu中卡片消息解析失效（#47596）都是典型例子。用户对“平台一致性”的期望与实现之间存在差距。
- **“稳定性是第一要务”**: macOS桌面端的段错误（#46789）让桌面用户无法使用；GPT-5.5模型的调用失败（#26599）影响核心功能；工具调用偶尔损坏（#6841）动摇了用户对Agent可靠性的信心。用户明确表示，在添加新功能之前，优先保证核心功能的稳定。

## 8.

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*