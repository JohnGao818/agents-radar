# OpenClaw 生态日报 2026-07-24

> Issues: 312 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-07-24 02:16 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，这是为您生成的 OpenClaw 项目动态日报。

---

# OpenClaw 项目动态日报 — 2026-07-24

## 今日速览

今日 OpenClaw 项目保持高度活跃，24小时内共有 **312** 条 Issue 更新和 **500** 条 PR 更新，反映出强大的社区参与度和维护团队响应速度。尽管今日无新版本发布，但维护者在代码合并与问题修复上投入了大量精力。项目健康度良好，但需注意有多个标记为 **P0/P1** 的严重回归问题（如 #108435 更新后无法启动）及涉及**静默消息丢失**的关键 Bug（如 #44925）正在积压处理中，可能对用户体验产生重大影响。

## 版本发布

- **今日无新版本发布。**

## 项目进展

今日共有 **95** 个 Issues 和 **186** 个 PRs 被关闭/合并。主要进展集中在以下几个方向：

1.  **核心稳定性修复：** 重点关注了会话管理与任务编排的可靠性。
    - [#113190 [已合并] fix(agents): strip trailing assistant messages after sessions_yield artifact removal](https://github.com/openclaw/openclaw/pull/113190): 修复了子任务 (subagent) 完成后，由于会话末尾残留的助手角色消息而导致的自动发布流程永久死锁问题，这对多代理协作的稳定性至关重要。
    - [#113188 [已合并] fix(agents): preserve prompt prefix caching during A2A handoffs](https://github.com/openclaw/openclaw/pull/113188): 通过优化智能体间 (A2A) 对话上下文注入方式，恢复了提示前缀缓存 (prompt prefix caching) 功能，能显著降低推理成本和延迟。

2.  **渠道与平台适配：** 跨平台兼容性得到增强。
    - [#113199 [已合并] feat(matrix): render spoilers, underline, and native tables](https://github.com/openclaw/openclaw/pull/113199): Matrix 渠道现支持原生渲染剧透、下划线和表格，提升了特定渠道的信息展示能力。
    - [#113173 [已合并] feat(sessions): suggestion queue + typing indicator](https://github.com/openclaw/openclaw/pull/113173): 引入“建议队列”和“输入指示器”，为非直接参与者提供了安全贡献内容的机制，并改善了多用户会话的协作体验。
    - [#113178 [已合并] fix(whatsapp): restore reactions in current conversations](https://github.com/openclaw/openclaw/pull/113178): 修复了 WhatsApp 渠道上的表情反应功能。

3.  **工具与开发者体验 (DX) 改善：**
    - [#112784 [开放] feat(localization): prove catalog authoring and refresh loop](https://github.com/openclaw/openclaw/pull/112784): 提出并实现了本地化 (i18n) 的目录编写和刷新循环方案，为国际化贡献者提供了更好的工作流。
    - [#113200 [开放] fix(doctor): honor configured plugin load paths](https://github.com/openclaw/openclaw/pull/113200): `openclaw doctor` 命令现在能正确识别通过自定义路径加载的插件，使健康检查更准确。

## 社区热点

今日讨论热度最高的几个议题反映了用户在生产环境中遭遇的重大挑战：

1.  **子任务静默丢失（Issue #44925，22条评论）：**
    - [Bug: Subagent completion silently lost — no retry, no notification, no auto-restart on timeout](https://github.com/openclaw/openclaw/issues/44925)
    - **诉求：** 用户报告在多代理任务编排中存在多种静默失败模式。子任务或告知完成失败，或超时后无任何自动重试、通知或重启机制，导致工作流中断且用户不知情。此问题影响广泛，被标记为 **P1 (高优先级)** 和 **“钻石龙虾 (diamond lobster)”** 评级，是当前社区最担忧的稳定性问题。

2.  **会话初始化冲突（Issue #102020，15条评论）：**
    - [Bug: Second message in a session fails with “reply session initialization conflicted”](https://github.com/openclaw/openclaw/issues/102020)
    - **诉求：** 用户在跨渠道（Signal、Telegram）的新会话中，发送第二条消息后遇到“回复会话初始化冲突”错误。该问题表现为位置依赖性，严重影响了正常交互流程，引发广泛关注。

3.  **Anthropic 思维块签名失效（Issue #94228，14条评论）：**
    - [Native Anthropic path: replaying historical `thinking` blocks bricks long tool-use threads](https://github.com/openclaw/openclaw/issues/94228)
    - **诉求：** 长时间运行的工具使用会话在使用原生 Anthropic API 时会永久卡死。当重放历史 `thinking` 块时，API 返回 `Invalid signature` 错误，导致整个线程无法继续。这直接阻碍了依赖此高级功能的长周期任务。

## Bug 与稳定性

以下列出了今日最严重的 Bug 和回归问题，按严重程度排列：

- **[P0] 更新后网关无法启动（#108435，10条评论）：**
    - [Bug: update to openclaw 2026.7.1: gateway fails to start w/ error](https://github.com/openclaw/openclaw/issues/108435)
    - **描述：** 更新到 `2026.7.1` 版本后，网关在 systemd、Ollama 和手动启动方式下均失败。**尚未有对应的修复 PR**。

- **[P0] 数据库迁移引发渠道错误（#90378，8条评论）：**
    - [Bug: Upgrading from 5.28 → 6.1: cron store migrated ... causing channel errors](https://github.com/openclaw/openclaw/issues/90378)
    - **描述：** 从 `5.28` 升级到 `6.1` 时，cron 存储从 JSON 静默迁移到 SQLite，导致新创建的 job 因 `delivery.mode=announce` 默认值不兼容而报错。

- **[P1] 全渠道陷入静默状态（#101814，4条评论）：**
    - [Bug: All channels enter broken state after 2026.6.11 update](https://github.com/openclaw/openclaw/issues/101814)
    - **描述：** 更新到 `2026.6.11` 后，所有渠道周期性进入每个会话仅允许一次对话后便永久静默的状态，必须重启网关才能恢复。

- **[P1] 编译超时无进度复用（#92043，13条评论）：**
    - [Bug: 180s compaction timeout ... legitimately-long compaction fails identically every turn](https://github.com/openclaw/openclaw/issues/92043)
    - **描述：** 180 秒的上下文压缩超时机制设计存在缺陷，它在整个管道上使用单一墙钟计时。对于需要长时间处理的安装环境（如处理长历史、使用慢速模型），每次压缩都会在相同位置超时而导致循环失败。

- **[P1] Telegram DM 回复降级（#111519，6条评论）：**
    - [Bug: Telegram DM replies fall back after stale DM-scope cleanup](https://github.com/openclaw/openclaw/issues/111519)
    - **描述：** `2026.7.2-beta.3` 版本的回归问题，Telegram 私人消息的回复可能丢失所有权，导致需要通过 `conversations.send` 降级投递。

## 功能请求与路线图信号

今日的热门功能请求揭示了用户对系统自动化、安全性和管理能力的更高期望。

- **统一自动化概念（#110950，9条评论）：**
    - [Feature: Everything is a cron — unify heartbeat, watchers, and scheduled automation](https://github.com/openclaw/openclaw/issues/110950)
    - **信号：** 此请求建议将“心跳 (heartbeat)”、“监视器 (watchers)”和“定时任务 (scheduled automation)”统一为 `cron` 任务这一个原语。这有可能简化系统架构，但也会带来突破性变更。**已关闭**，表明维护团队可能已有其他计划或正在评估。

- **技能权限清单标准（#12219，6条评论）：**
    - [Feature: Skill Permission Manifest Standard (skill.yaml)](https://github.com/openclaw/openclaw/issues/12219)
    - **信号：** 用户强烈要求为技能 (Skill) 实现权限声明标准，以避免近期发生的凭据窃取等安全事件。这是一项重要的安全特性，很可能被纳入后续版本。

- **全局 `--dry-run` 模式（#41418，5条评论）：**
    - [Feature: Add global --dry-run mode to prevent all tool calls from executing](https://github.com/openclaw/openclaw/issues/41418)
    - **信号：** 用户希望添加一个 `--dry-run` 参数，预览 Agent 将要执行的工具调用而不实际运行。这有助于调试和审计，是一个需求量很高的开发者体验特性。

- **会话 TTL/最大生命周期（#45390，5条评论）：**
    - [Feature request: Session TTL / max lifetime for automatic rotation](https://github.com/openclaw/openclaw/issues/45390)
    - **信号：** 用户观察到会话积累上下文物体会无限增长，最终导致超时。请求为会话增加最大生命周期配置以自动轮换，这是一个实用的运维功能。

## 用户反馈摘要

从今日的 Issue 评论中，我们可以提炼出以下真实的用户之声：

- **“静默失败”是最令人沮丧的体验：** 用户对 `#44925` 中子任务完成后无任何反馈或重试机制的情况表达了强烈不满。一位用户评论道：“我无法知道我的工作流在哪里中断了，这完全破坏了自动化流程的信任。”
- **升级风险是主要顾虑：** 多位用户报告因升级导致服务不可用（如 `#108435`）或体验降级（如 `#111519`）。一位用户在 `#98672` 中抱怨：“一夜之间会话全部失效，没有任何改动，升级是唯一的变量。”
- **对上下文膨胀的焦虑：** 用户 `#67419` 指出每次对话都会重新注入约 20-30% 的引导文件 (bootstrap files) 导致令牌浪费，这引发了关于效率和成本的讨论，用户希望能对上下文注入有更精细的控制。
- **对安全性的公开关切：** 在 `#12219` 的讨论中，用户引用了一些因技能权限过大而导致的安全事故，显示出社区对第三方技能安全性的高度警惕，并呼吁官方尽快出台标准。

## 待处理积压

以下是几个长期未关闭或未得到充分响应的关键 Issue，需引起维护者注意：

- **[P1] `#42820`：Feishu 消息发送因投票模式受阻**
    - [message tool: ... poll schema/guard prevents file send](https://github.com/openclaw/openclaw/issues/42820)
    - **状态：** 自 3月11日提出，标记为“需要维护者评审”和“需要产品决策”，已长期未取得进展。

- **[P1] `#43374`：多Agent并发时所有LLM API调用同时超时**
    - [All LLM API calls time out simultaneously ... (multi-agent concurrency issue)](https://github.com/openclaw/openclaw/issues/43374)
    - **状态：** 这是一个可能导致服务完全不可用的严重问题，自 3月11日提出，同样卡在“需要维护者评审”阶段。

- **[P2] `#67419`：引导文件反复注入导致上下文膨胀**
    - [Session context bloat: bootstrap files re-injected every turn](https://github.com/openclaw/openclaw/issues/67419)
    - **状态：** 用户持续反馈，此问题直接影响使用成本和 AI 推理质量，但自 4月15日提出后仍在等待产品决策。

---

## 横向生态对比

好的，作为专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我将基于您提供的两份项目动态摘要，为您生成一份专业的横向对比分析报告。

---

### AI 智能体与个人 AI 助手开源生态横向对比分析报告 (2026-07-24)

#### 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于 **“快速扩张后的质量巩固期”**。社区参与度极高，表现为海量的 Issues 和 PRs 涌入，直接反映了用户对系统稳定性、可观测性和安全性的迫切需求。`OpenClaw` 生态庞大，用户基数广，正面临 **“成长的阵痛”**，多个严重回归问题和“静默失败”Bug 成为核心痛点。相比之下，`Hermes Agent` 虽规模较小，但迭代速度迅猛，在桌面端体验、SSH 集成和第三方模型兼容性上快速演进。一个显著趋势是：**开发者不再满足于“能用”，而是强烈追求“可靠、可控、可审计”的生产级系统**。

#### 2. 各项目活跃度对比

| 维度 | **OpenClaw** | **Hermes Agent** |
| :--- | :--- | :--- |
| **Issues 更新 (24h)** | 312 条 | 50 条 |
| **PRs 更新 (24h)** | 500 条 | 50 条 |
| **今日版本发布** | 无 | 无 |
| **严重 Bug (P0/P1)** | **4个** (网关无法启动、DB迁移致渠道错误、全渠道静默、编译超时无进展) | **2个** (OAuth 401重试循环、反节流永久禁用压缩) |
| **修复 PR 覆盖率** | 部分 Bug 已有合并/开放的修复 PR | 少量 Bug 有相关但未完全解决的 PR |
| **健康度评估** | **高活跃，但高波动**。社区反馈极其活跃，但存在大量影响核心功能的稳定性问题，需要维护团队优先解决重大回归。 | **高活跃，健康度可控**。Bug 聚焦于前端与特定集成，核心推理逻辑相对稳定，但修复合入速度略慢于问题反馈速度。 |

#### 3. OpenClaw 在生态中的定位

`OpenClaw` 是当前该赛道中**社区体量最大、功能最全面**的标杆性项目，被广泛视为 AI 智能体领域的“Linux 内核”。

- **核心优势**: 强大的**多代理编排 (A2A)** 与**多渠道适配**能力（Matrix、WhatsApp、Telegram、Signal），使其成为构建复杂、跨平台自动化工作流的首选基座。
- **技术路线差异**: 更强调**企业级任务编排与可靠性**。相比 `Hermes Agent` 的轻量化、桌面优先，`OpenClaw` 正致力于解决会话管理、子任务编排、上下文压缩等深层次系统问题。
- **社区规模**: 从 312/500 的 Issue/PR 数量即可看出，其社区规模远超 `Hermes Agent`。大规模社区带来了更多贡献，也意味着更大体量的 Bug 和更复杂的维护挑战。

#### 4. 共同关注的技术方向

两个项目社区共同涌现出对以下方向的强烈需求，反映了用户的核心诉求：

- **智能体工作流的可观测性与可靠性（涉及 OpenClaw、Hermes）**:
  - **最大痛点**: **“静默失败” (Silent Failure)**。`OpenClaw` Issue #44925 和 `Hermes` 社区反馈均提及子任务或工作流中断后无任何通知、重试机制，导致用户完全不知情。这表明，**AI 智能体系统的“信任”远比其“智能”更为紧迫**。
  - **诉求**: 统一的重试、超时、告警机制；全局 `--dry-run` 模式（`OpenClaw` #41418）；MoA 进度提示（`Hermes` #59546）。

- **会话管理与上下文膨胀控制（涉及 OpenClaw、Hermes）**:
  - **共同痛点**: 长会话导致上下文无限制膨胀，令牌浪费（`OpenClaw` #67419），并引发压缩超时循环（`OpenClaw` #92043）。`Hermes` 的 OAuth 401 循环（#70401）本质上也是长连接会话状态管理失效。
  - **诉求**: 会话 TTL/最大生命周期（`OpenClaw` #45390）；精细化的上下文裁剪与注入控制；用户侧可配置的压缩与重置策略。

- **安全与权限管理（涉及 OpenClaw、Hermes）**:
  - **共同信号**: 用户对第三方技能/插件的安全性高度警惕。`OpenClaw` 呼吁“技能权限清单标准”（#12219），`Hermes` 则通过 PR #70467 框架化 MCP 工具描述来阻止提示词注入。
  - **诉求**: 为 AI 智能体的能力（技能、工具、模型访问）建立标准化的权限声明与沙箱执行模型，是走向生态安全和可扩展的必然要求。

- **开发者体验 (DX) 和部署便利性（涉及 OpenClaw、Hermes）**:
  - **共同信号**: 用户对升级风险（`OpenClaw` #108435, #90378）、错误诊断（`OpenClaw` #113200，`Hermes` #70471）和本地化（`OpenClaw` #112784，`Hermes` 中文社区问题）的关注度提升。这表明，随着项目普及，**降低维护成本和提升新手友好度成为关键**。

#### 5. 差异化定位分析

| 维度 | **OpenClaw** | **Hermes Agent** |
| :--- | :--- | :--- |
| **功能侧重** | **系统级编排与多渠道融合**。专注于多代理协作、任务调度、会话管理与渠道适配，是构建复杂业务流的“骨架”。 | **个人桌面体验与工具集成**。专注于桌面端UI/UX、SSH远程、本地语音输入（STT）、MoA（集成多种模型）等，是提升个人效率的“肌肉”。 |
| **目标用户** | **DevOps / SRE / 高阶开发者**，需要构建可靠的生产级 AI 工作流与 Bot 生态系统。 | **个人开发者、知识工作者**，追求即时的、多模态、定制化的单用户 AI 助手体验。 |
| **技术架构** | **事件驱动、微服务化**。强调子任务（Subagent）、通信（A2A）、插件加载路径、数据库迁移等后端架构的健壮性。 | **模块化但更偏向单体（桌面应用式）**。关注前端状态同步、WebSocket 连接、进程间通信（CLI vs. Desktop）、OAuth 凭证管理等应用层问题。 |
| **挑战方向** | 解决因复杂性带来的**稳定性和可观测性**问题。 | 解决因快速迭代带来的**UI/UX 一致性和特定场景（如SSH、代理）的兼容性**问题。 |

#### 6. 社区热度与成熟度

- **第一梯队（快速迭代与质量巩固并存）**: **OpenClaw**
  - **特征**: 海量 Issue/PR，社区活跃度极高。项目已进入**生产级成熟度的爬坡期**，用户反馈和贡献质量高，但伴随大量回归问题和深层次 Bug。
  - **状态**: 处于 **“大规模社区协同测试与修复”** 阶段。虽然成熟度在快速提升，但短期内使用体验可能因 Bug 而波动。

- **第二梯队（快速迭代，功能涌现）**: **Hermes Agent**
  - **特征**: 社区增速快，新功能请求（自动备份、会话导航、Cursor 接入）和高频 Bug 并存。开发者响应积极，但修复合入速度略慢于反馈。
  - **状态**: 处于 **“核心功能稳定，周边功能与体验快速打磨”** 阶段。对于追求最新特性、对桌面体验要求高的用户来说吸引力强，但风险在于边缘场景的稳定性。

#### 7. 值得关注的趋势信号

1.  **“可观测性”成为首要需求**: 社区对“静默失败”的零容忍态度表明，AI 智能体系统必须从“黑盒智能”转向“可审计的任务引擎”。未来，**内置的、标准化的工作流追踪、日志、监控和告警体系**将成为项目竞争的核心分水岭。

2.  **安全权限声明的标准化是生态繁荣的前提**: `OpenClaw` 的 #12219 和 `Hermes` 的防注入措施，预示着一个**“权限声明清单” (类似 Android 或 macOS 的应用权限)** 的行业共识正在形成。AI 智能体的指令必须受到细粒度权限约束，否则第三方技能生态将成为安全黑洞。

3.  **上下文压缩与成本控制的“精算化”**: 从`OpenClaw`的超时循环到上下文膨胀焦虑，反映出用户对 AI 推理成本的极度敏感。项目需要在**上下文压缩策略、会话生命周期管理、令牌计费可视化**方面提供更精细的控制能力。

4.  **“个人化”与“平台化”割裂加速**: `OpenClaw` 和 `Hermes` 的差异化定位日益清晰。未来生态可能形成两类主流项目：一类是**个人效率助手**（如 Hermes），轻便、集成度高、体验顺滑；另一类是**自主智能体平台**（如 OpenClaw），强大、可编排、基础设施即代码。开发者需根据自身需求选择合适的“物种”。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报

**日期**: 2026-07-24  
**数据来源**: [NousResearch/hermes-agent GitHub](https://github.com/NousResearch/hermes-agent)  
**分析时段**: 2026-07-23 ~ 2026-07-24 (UTC)

---

## 1. 今日速览

过去 24 小时项目活跃度极高：**50 条 Issues 更新**（新开/活跃 39，关闭 11）与 **50 条 PR 更新**（待合并 45，已合并/关闭 5）并行涌入，社区反馈与开发贡献同步快速增长。无新版本发布。问题集中在**桌面端 UI/会话管理异常**、**Telegram 网关稳定性**、**SSH 远程模式兼容性**以及 **OAuth 认证循环**等核心领域；同时涌现多个高赞功能需求（如自动备份、消息导航侧边栏）。虽然合并节奏略有放缓（仅 5 个 PR 入库），但大量 P1/P2 级 Bug 已提交相应修复 PR，项目健康度总体可控但需加速关键 Bug 的合入。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 PR 与 Issues 主要完成了以下修复与功能：

### 已合并/关闭的 Pull Request
| PR | 描述 | 要点 |
|----|------|------|
| [#70471](https://github.com/NousResearch/hermes-agent/pull/70471) **CLOSED** | `fix(tests): prevent auth_gate.py from leaking state to subsequent test files` | 修复测试框架中认证状态泄漏导致的跨文件污染，提升 CI 稳定性 |

### 已关闭的 Issues（部分重要）
| Issue | 描述 | 影响 |
|-------|------|------|
| [#69512](https://github.com/NousResearch/hermes-agent/issues/69512) **CLOSED** | `fix(anthropic): sanitize empty/whitespace-only text blocks to prevent permanent HTTP 400 after compression` | 修复 Anthropic 压缩后空白文本块导致 API 400 的回归问题 |
| [#59707](https://github.com/NousResearch/hermes-agent/issues/59707) **CLOSED** | `feat(moa): Add enable/disable toggle for individual reference models` | MoA 参考模型开关，满足用户临时排除需求 |
| [#61452](https://github.com/NousResearch/hermes-agent/issues/61452) **CLOSED** | `[Bug]: Reference models fabricate tool execution in text output, misleading aggregator` | 修复 MoA 模型虚构工具执行输出的误导问题（标记为重复） |
| [#59959](https://github.com/NousResearch/hermes-agent/issues/59959) **CLOSED** | `[Feature]: Add optional privacy filter for MoA reference outputs` | 新增 MoA 参考输出的可选隐私/脱敏过滤器 |
| [#59546](https://github.com/NousResearch/hermes-agent/issues/59546) **CLOSED** | `[Feature]: MOA 建议加上进度提示` | 为 TUI/桌面端增加 MoA 进度提示 |

**项目整体向前迈进**：核心 Anthropic 提供器稳定性增强，MoA 功能链更加可控，测试基础得以巩固。

---

## 4. 社区热点

以下 Issues 讨论最活跃、反馈最集中：

### 🔥 Issue #66875 — “最新会话切换失败”  
**评论数**: 8 | **👍**: 0 ([链接](https://github.com/NousResearch/hermes-agent/issues/66875))  
**痛点**: 在桌面端从插件/制品标签页返回时，点击最新会话不响应，必须手动新建会话。背后反映**前端状态同步**的 bug——会话列表刷新逻辑仅在非最新项上生效。用户普遍期待“点哪去哪”的即时性。

### 🔥 Issue #69314 — “Telegram 网关代理 CLOSE_WAIT 死锁”  
**评论数**: 7 | **👍**: 0 ([链接](https://github.com/NousResearch/hermes-agent/issues/69314))  
**痛点**: Docker 部署下 Telegram 网关通过 HTTP 代理时，出现数百个 CLOSE_WAIT 套接字导致永久性卡死，必须完全重启。用户强调**代理健康但网关内部状态腐烂**，属于长期顽疾。

### 🔥 Issue #12238 — “内置自动备份与版本控制”  
**评论数**: 6 | **👍**: 19 ([链接](https://github.com/NousResearch/hermes-agent/issues/12238))  
**最受欢迎的新功能请求**。用户希望保护代理数据（记忆、技能、对话历史）不丢失，并支持版本追踪。背后反映**对 Agent 数据持久化与可回溯性的强烈需求**，尤其适用于长期运行的定制化 Agent。

### 🔥 Issue #49978 — “PageUp 破坏页面布局”  
**评论数**: 6 | **👍**: 2 ([链接](https://github.com/NousResearch/hermes-agent/issues/49978))  
**痛点**: 桌面端当输入框聚焦时按 PageUp，左侧侧边栏被挤出、内容移位、底部留白。该 Bug 影响日常滚动浏览，且**重启方能恢复**，用户重复触发率高。

---

## 5. Bug 与稳定性

今日报告的严重 Bug 按优先级排列：

| 优先级 | Issue | 标题 | 是否有修复 PR |
|--------|-------|------|--------------|
| **P1** | [#70401](https://github.com/NousResearch/hermes-agent/issues/70401) | OAuth 凭证池进入不可中断的 401 重试循环 | ❌ 无 |
| **P1** | [#14694](https://github.com/NousResearch/hermes-agent/issues/14694) | 反节流保护永久禁用自动压缩，无法恢复 | ❌ 无（4月创建至今未修复） |
| **P2** | [#69551](https://github.com/NousResearch/hermes-agent/issues/69551) | 桌面 SSH 远程模式在非默认配置下完全损坏 | ❌ 无 |
| **P2** | [#69930](https://github.com/NousResearch/hermes-agent/issues/69930) | 桌面端 WebSocket 30-45 秒循环重连，UI 冻结 | ❌ 无（[PR #70465](https://github.com/NousResearch/hermes-agent/pull/70465) 相关但未完全解决） |
| **P2** | [#69825](https://github.com/NousResearch/hermes-agent/issues/69825) | `serve` 命令永不注册 Shell 钩子 | ❌ 无 |
| **P2** | [#69925](https://github.com/NousResearch/hermes-agent/issues/69925) | 桌面端与 CLI 同时运行时进入启动循环 | ❌ 无 |
| **P2** | [#70424](https://github.com/NousResearch/hermes-agent/issues/70424) | 从 Kanban/Artifacts 点击会话无法返回聊天 | ❌ 无（与 #66875 相关） |
| **P3** | [#66875](https://github.com/NousResearch/hermes-agent/issues/66875) | 最新会话切换无反应 | ❌ 无 |
| **P3** | [#69314](https://github.com/NousResearch/hermes-agent/issues/69314) | Telegram 网关 CLOSE_WAIT 死锁 | ❌ 无 |
| **P3** | [#60693](https://github.com/NousResearch/hermes-agent/issues/60693) | 界面缩放 110% 间歇性重置为 100% | ❌ 无 |
| **P3** | [#52235](https://github.com/NousResearch/hermes-agent/issues/52235) | Windows 端 PageDown 导致显示异常（中文用户报告） | ❌ 无 |

**已有关联修复 PR 的关键 Bug**：

- [#70465](https://github.com/NousResearch/hermes-agent/pull/70465) — `fix(acp): recover stale OAuth on long-lived ACP sessions`，解决长连接 ACP 会话中 OAuth 令牌过期导致的 403 错误。
- [#70474](https://github.com/NousResearch/hermes-agent/pull/70474) — `fix(plugins): block updates while gateway runs`，防止运行时更新 Git 插件导致回调崩溃。
- [#70467](https://github.com/NousResearch/hermes-agent/pull/70467) — `fix(mcp): frame MCP tool descriptions as untrusted to block prompt injection`，安全增强。
- [#70468](https://github.com/NousResearch/hermes-agent/pull/70468) — `fix(kanban): board default_workdir inheritance for CLI/tool-created tasks`，对齐文档承诺。

---

## 6. 功能请求与路线图信号

### 高呼声新功能（暂无对应 PR）
| Issue | 标题 | 预期关注 |
|-------|------|---------|
| [#12238](https://github.com/NousResearch/hermes-agent/issues/12238) | 内置自动备份与版本控制（👍 19） | 很可能纳入下个里程碑，保护 Agent 学习状态 |
| [#69532](https://github.com/NousResearch/hermes-agent/issues/69532) | 当前会话消息导航侧边栏（类似 DeepSeek） | 用户强烈要求长会话快速定位 |
| [#70140](https://github.com/NousResearch/hermes-agent/issues/70140) | 可选 Cursor Models 账单路径 via 独立 SDK 插件 | 赋能付费用户直通 Cursor 模型池 |
| [#52669](https://github.com/NousResearch/hermes-agent/issues/52669) | 系统提示硬编码 `~/.hermes` 路径，不尊重 `HERMES_HOME` | 影响非标准安装用户 |

### 已有相关 PR 可能被合入的功能
| PR | 描述 | 对应 Issue |
|----|------|-----------|
| [#70466](https://github.com/NousResearch/hermes-agent/pull/70466) | `feat(api): expose Codex account usage` | 提供用量查询 API |
| [#70472](https://github.com/NousResearch/hermes-agent/pull/70472) | `feat(desktop): add local STT provider setup` | 桌面端本地语音输入 |
| [#65982](https://github.com/NousResearch/hermes-agent/pull/65982) | `feat(providers): claude-agent-sdk provider` | 官方 Claude Agent SDK 作为一等公民（fail-closed） |
| [#70428](https://github.com/NousResearch/hermes-agent/pull/70428) | `fix(skills): move dogfood skill into the software-development category` | 技能分类优化 |
| [#70456](https://github.com/NousResearch/hermes-agent/pull/70456) | `refactor(skills): move yuanbao to optional-skills` | 平台专属技能下沉，减小默认安装体积 |

**路线图信号**：项目正加速向**企业级安全（OAuth 修复、MCP 防注入）、前端易用性（会话导航、技能分类）、多模态（本地 STT）以及第三方模型集成（Claude SDK、Cursor 支持）**方向演进。

---

## 7. 用户反馈摘要

从 Issues 评论中提炼的真实用户痛点：

> “点击最新会话什么都不做——这破坏了我每天的工作流。必须点倒数第二个才能切换回去，这显然是个 bug。”  
> —— [pdhande on #66875](https://github.com/NousResearch/hermes-agent/issues/66875)

> “Telegram 网关在 Docker 下用代理就卡死了，CLOSE_WAIT 堆积了几百个。我什么都没动，它自己就废了，只能整个容器重启。”  
> —— [ashanzzz on #69314](https://github.com/NousResearch/hermes-agent/issues/69314)

> “我花了几周训练我的 Agent 记忆和技能，结果一次文件系统事故全丢了。为什么不能像 Git 那样自动备份？”  
> —— [salem221094 on #12238](https://github.com/NousResearch/hermes-agent/issues/12238)

> “你们桌面端 PageUp 会搞乱布局，侧边栏直接消失。我用的是 Windows，重启才能恢复，很烦人。”  
> —— [Murphy-Tong on #49978](https://github.com/NousResearch/hermes-agent/issues/49978)

> “MoA 看不到进度，就是个黑盒。我能从日志里扒拉，但我只想在 TUI 界面看到‘2/3 参考模型完成’。”  
> —— [MYSTERY2019 on #59546](https://github.com/NousResearch/hermes-agent/issues/59546)（已关闭但反映需求）

> “SSH 远程模式在配置非默认 profile 就完全坏了——token 校验路径居然硬编码 `~/.hermes`，而不是遵循当前 profile 的 HERMES_HOME。”  
> —— [MrB0req on #69551](https://github.com/Nous

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*