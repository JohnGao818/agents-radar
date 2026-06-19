# OpenClaw 生态日报 2026-06-19

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-19 03:55 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为OpenClaw项目的AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的2026-06-19 GitHub数据，生成以下项目动态日报。

---

# OpenClaw 项目动态日报 — 2026-06-19

## 今日速览

OpenClaw项目今日社区活跃度极高，24小时内收到500条Issue与500条PR更新，但合并率较低（约11.6%），表明维护与审查流程面临巨大压力。项目当前严重缺乏新版本发布，而大量高优先级（P1）的Session状态与消息丢失问题持续积压。社区讨论焦点集中在Session隔离失败、模型回复截断以及多平台消息传递一致性等核心稳定性议题上。尽管面临挑战，针对Telegram、Codex及Embedded Sessions的修复PR正在增加，显示项目正积极应对已知问题。

## 版本发布

今日无新版本发布。

## 项目进展

今日有58个PR被合并或关闭，涉及多项关键修复与改进：

- **核心稳定性修复**：
    - **PR #94453** (已合并): **重要** 修复了cron任务默认`runMode`为`"force"`的安全问题。现已改为`"due"`，防止计划任务在非预定时间被意外执行，增强了安全性与调度行为的可预测性。
    - **PR #94478** (已合并): 修复了`openclaw doctor`命令对遗留Codex路由持久化的问题，确保升级后的配置能正确迁移，提升了升级流程的健壮性。
    - **PR #89203** (已合并): 重构了插件SDK的Session兼容性，通过`seam`模式路由，为后续的存储层变更提供了更清晰的抽象和兼容层。

- **日常优化与清理**：
    - **PR #84794** (已合并): 清理了孤立cron会话，确保在多种终端路径下（如`none`模式、运行错误）也能自动删除已完成的cron运行会话，防止资源泄漏。
    - **PR #93814** (已合并): 修复了导出旧版本（v1）会话时产生空Transcript的bug，确保`openclaw export-trajectory`命令在导出所有历史会话时数据完整。
    - **PR #94687** (已合并): 改进了Gateway健康检查与探测命令，使其能正确接受并使用`--port`参数，提升了运维便利性。

## 社区热点

今日热点议题凸显了用户对**消息传递可靠性**与**Session行为一致性**的强烈关注：

1.  **[Bug]: Session write-lock timeouts block subagent delivery lanes (Issue #86538)**
    - **评论/反应热度**: 评论数 11 👍 1
    - **链接**: [Issue #86538](https://github.com/openclaw/openclaw/issues/86538)
    - **分析**: 该问题直击系统核心，指出Session级别的写锁超时会阻塞所有类型的代理（main, cron, subagent）的消息发送通道。这一问题被标记为P1和最高严重级别，反映了用户对系统在高并发下可靠性的担忧。

2.  **[Bug]: Agent repeats identical replies 2-10x on Telegram after 5.20 update (Issue #86519)**
    - **评论/反应热度**: 评论数 9 👍 1
    - **链接**: [Issue #86519](https://github.com/openclaw/openclaw/issues/86519)
    - **分析**: 这是一个明确的回归问题，在5.20版本更新后出现。用户报告Telegram上同一回复重复发送2-10次，虽然5.22版本有所缓解但未完全修复。社区对此高度关注，因为它严重影响了Telegram用户的日常使用体验。

3.  **[Bug]: Control UI Raw mode permanently disabled since 2026.3.31 (Issue #59330)**
    - **评论/反应热度**: 评论数 9 👍 14
    - **链接**: [Issue #59330](https://github.com/openclaw/openclaw/issues/59330)
    - **分析**: 该问题获得当日最高点赞数(14)，表明这是一个广泛影响高级用户的长期问题。自3月底以来，控制UI的Raw模式被永久禁用，迫使大量使用高级配置的用户只能使用有局限性的Form模式。社区的强烈反应体现了对高级自定义配置能力的依赖性。

4.  **Codex app-server: long agent replies silently truncated at ~1000-1100 chars (Issue #84516)**
    - **评论/反应热度**: 评论数 11 👍 2
    - **链接**: [Issue #84516](https://github.com/openclaw/openclaw/issues/84516)
    - **分析**: 此问题关注Codex模型回复被静默截断的异常行为，且模型状态显示未中断。这是一个隐蔽性极强的Bug，可能导致用户对模型能力产生错误认知，影响基于Codex的深度交互应用。

## Bug 与稳定性

今日报告的Bug中，**Session状态**和**消息丢失/重复**是两大核心主题。按严重程度排列如下：

**P0 (最高优先级)**
- **`[Bug]: memory-core Dreaming ... silently deletes daily memory files` (Issue #84882)** - 主要内存文件被静默删除。已有修复PR (#89203) 在今日被合并，状态已关闭，风险解除。

**P1 (高优先级)**
- **`Telegram isolated ingress spool ... blocked by stale .processing claim` (Issue #84674)** - 孤立入口假脱机停滞，导致Telegram消息完全阻塞。
- **`Model fallback chain not triggered ... EmbeddedAttemptSessionTakeoverError` (Issue #85103)** - 模型降级链失效，当主模型配额耗尽时系统无法自动切换到备用模型。
- **`Agent repeats identical replies 2-10x on Telegram after 5.20 update` (Issue #86519)** - Telegram消息重复。社区用户反馈强烈，修复优先级高。
- **`A single stalled agent session blocks the entire Gateway event loop` (Issue #84903)** - Session隔离失败，单个会话阻塞可导致整个Gateway事件循环瘫痪，是架构性缺陷。
- **`MCP tools not injected into subagent sessions` (Issue #85030)** - 子代理无法使用MCP工具，限制了多代理协作场景的功能。
- **`Gateway loops with SIGTERM every ~90s after upgrade ... WSL2` (Issue #84610)** - WSL2环境下的严重升级回归问题，导致Gateway频繁重启，服务不可用。
- **`Event loop saturation during startup` (Issue #84771)** - 启动过程中事件循环持续饱和，影响快速重启和故障恢复。

**P2 (中优先级)**
- **`Anthropic 1h cache invalidates conversation prefix every turn` (Issue #86063)** - 导致昂贵的AI推理成本浪费，无谓消耗令牌。无直接Fix PR链接。
- **`MissingAgentHarnessError race: non-atomic harness registry clear+restore` (Issue #86342)** - 罕见的竞态条件导致代理Harness丢失，造成请求失败。无直接Fix PR链接。

**Bug动态总结**：尽管当日合并了数个关键修复（如#84882的数据丢失和#94453的调度安全），但仍有大量P1级别的Session与消息传递问题处于开放状态，项目在核心稳定性上仍承压。特别是#86519 (Telegram重复回复) 和 #84903 (Gateway阻塞) 值得优先关注。

## 功能请求与路线图信号

- **`[Feature]: Filesystem Sandboxing Config` (Issue #7722)** - 用户强烈呼吁的文件系统沙箱功能，至今无明确进展。**链接**: [Issue #7722](https://github.com/openclaw/openclaw/issues/7722)
- **`[Feature]: Expose stable plugin SDK surface for installed skill workflows` (Issue #81913)** - 社区需要稳定的插件SDK，以便对已安装Skill进行深度操作。**链接**: [Issue #81913](https://github.com/openclaw/openclaw/issues/81913)
- **`Hook: before_route_inbound_message` (Issue #81061)** - 用户提出需要前置路由Hook以实现高级消息拦截和桥接。**链接**: [Issue #81061](https://github.com/openclaw/openclaw/issues/81061)
- **`Rename 'cron' subsystem to disambiguate from system cron` (Issue #86237)** - 社区提议重命名内部调度器以避免与系统cron冲突，表明该设计缺陷已对用户造成实际困扰。**链接**: [Issue #86237](https://github.com/openclaw/openclaw/issues/86237)
- **`Add core snapshot CLI` (PR #94717) & `Add core snapshot provider proof` (PR #94694)** - 两个新提交的PR，核心主题是添加“快照”功能以提供安全的数据库备份与恢复能力。这表明项目路线图可能正在考虑引入数据持久性与可迁移性的基础设施。

## 用户反馈摘要

从今日的Issue评论中可提炼出以下关键用户痛点：

- **核心稳定性是最大痛点**: 多个带高赞的高热度Bug（如#86519, #84903）表明，用户对于系统稳定性、消息不丢失、Session不阻塞等基本可靠性诉求极为强烈。一些用户可能因此考虑降级或暂停使用。
- **高级用户对控制力不满**: `Control UI Raw mode` 被长期禁用（Issue #59330）引发了大量高级用户的负面反馈，他们需要绕过有局限性的Form模式进行更精细的配置。
- **升级风险高**: 多个问题表明，从5.6到5.22的几个版本升级都引入了新的回归问题（如#86519, #84610, #85027）。用户对升级的信任度可能下降，倾向于停留在旧版本。
- **功能期望与实际不符**: 用户对`sessionKey`实现多轮对话文档与实际行为不符（Issue #11665）、`filesystem sandboxing`未实现（Issue #7722）等情况感到失望。

## 待处理积压

- **长期高赞Bug**: **`Control UI Raw mode permanently disabled` (Issue #59330, 自2026-03-25起，14个👍)**。该问题积压近3个月，是社区最渴望解决的用户体验问题之一。
- **长期未响应的重要功能请求**: **`Filesystem Sandboxing Config` (Issue #7722, 自2026-02-03起，4个👍)** 和 **`Expose stable plugin SDK surface` (Issue #81913, 自2026-05-14起)**。这些功能请求反映了用户对安全性和可扩展性的长期需求，但尚未得到维护者的明确反馈或纳入开发计划。
- **高冲突风险PR等待维护**: **`fix(agents): gate owned-write publish on pre-append fingerprint` (PR #86584)**，该PR修复严重的会话劫持问题，但标记为“等待作者”，可能阻碍了关键修复的合并。**链接**: [PR #86584](https://github.com/openclaw/openclaw/pull/86584)
- **Telegram重复回复问题跟踪**: **`Agent repeats identical replies 2-10x on Telegram after 5.20 update` (Issue #86519)**，这是一个影响面广的回归问题，目前仍在开放状态且只有缓解（Mitigation）而无彻底修复，急需维护者介入。**链接**: [Issue #86519](https://github.com/openclaw/openclaw/issues/86519)

---

## 横向生态对比

好的，以下是根据您提供的 OpenClaw 和 Hermes Agent 项目动态日报，生成的横向对比分析报告。

---

# AI 智能体与个人 AI 助手开源生态横向对比分析报告 (2026-06-19)

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于 **“功能扩张期”向“生产高可用期”过渡** 的关键阶段。社区活跃度极高，但核心稳定性问题（消息丢失、Session 隔离失效、升级回归）成为普遍痛点，迫使项目在快速迭代的同时承受巨大维护压力。另一方面，高阶用户已开始探索复杂 Agent 编排模式（如 Doer/Reviewer 双角色），并强烈呼吁跨平台原生支持、标准化的工具集成接口（MCP）以及长期项目记忆原语，表明生态正从“能跑起来”转向“能可靠地跑好复杂任务”。

## 2. 各项目活跃度对比

| 指标 | OpenClaw | Hermes Agent |
|------|----------|--------------|
| **今日 Issues 数** | 500 条（新增/更新） | 50 条（新增/更新） |
| **今日 PR 数** | 500 条（新增/更新） | 50 条（新增/更新） |
| **今日合并/关闭 PR 数** | 58 个 | 2 个 |
| **今日版本发布** | 无 | 无 |
| **PR 合并率** | 约 11.6%（500 个 PR 中 58 个合并） | 4%（50 个 PR 中 2 个合并） |
| **健康度评估** | **承压**：大量 P1 级 Session/消息 Bug 积压，审查流程拥挤，合并率低 | **活跃但可控**：虽存在 P1 严重问题，但贡献集中，关键修复推进快 |
| **社区规模信号** | 当日 Issue/PR 量级约为 Hermes 的 10 倍，社区体量明显更大 | 体量小但贡献质量高，社区互动紧密 |

## 3. OpenClaw 在生态中的定位

- **优势**：社区规模远超同类（当日活跃量为 Hermes 的 10 倍），拥有更丰富的插件与工具生态。其核心引擎在 Session 隔离、写锁管理、Gateway 事件循环等方面设计较深厚，适合对稳定性和并发要求高的部署场景。
- **技术路线差异**：OpenClaw 更注重**底层状态机与调度健壮性**（cron 任务默认 runMode 修复、Session 写锁超时治理、事件循环饱和度监控），架构偏重而复杂。Hermes Agent 则更关注**用户体验与灵活编排**（Profile 配置、TUI 集成、Doer/Reviewer 模式探索、对推理模型 `reasoning_content` 的兜底）。
- **社区规模对比**：OpenClaw 社区用户基数大，但维护效率受限于 PR 合并瓶颈；Hermes Agent 社区较小但活跃度高，贡献者共识较强。两者均面临升级回归问题，但 Hermes Agent 在跨平台（Windows、macOS）上更主动响应。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|----------|----------|
| **消息传递可靠性** | OpenClaw (Issue #86538, #86519, #84674) <br> Hermes (Issue #48519, #48689) | Session 写锁超时导致消息阻塞、Telegram 重复回复、数据丢失（sessions.json vs state.db 不一致） |
| **模型兼容性** | OpenClaw (Issue #84516 模型回复静默截断) <br> Hermes (PR #48795 空 content 降级、Issue #47868 timestamp 泄漏) | 对非标准模型回复（如 `reasoning_content`）或严格 API schema 提供商的适配能力 |
| **跨平台体验** | OpenClaw (暂无明确 Windows 原生支持 Issue) <br> Hermes (Issue #48716 Windows 受阻、Issue #48721 macOS 升级失败) | Windows 用户入门被拒、macOS launchd 重启机制不兼容、系统 Python 环境保护 |
| **升级回归风险** | OpenClaw (Issue #86519 5.20 回归、#84610 WSL2 升级后循环重启) <br> Hermes (Issue #48519 子配置数据丢失回归、#48721 升级 PEP 668 失败) | 新版本引入的功能回退，影响用户升级意愿 |
| **工具/插件集成** | OpenClaw (Issue #85030 子代理 MCP 工具缺失) <br> Hermes (Issue #41625 TUI 下 MCP 不可用、PR #27738 飞书 SDK 依赖更新) | MCP 协议在前端/子代理中的全面覆盖，以及第三方服务（飞书、Slack、WhatsApp）集成 |
| **高级配置/控制力** | OpenClaw (Issue #59330 Raw 模式被永久禁用) <br> Hermes (Issue #47058 Dashboard 配置热重载) | 用户希望绕过限制性 UI 进行深度自定义，并减少运维操作 |

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
|------|----------|--------------|
| **功能侧重** | **核心引擎稳定性**：cron 调度、Gateway 事件循环、Session 写锁、消息逐级路由、文件系统沙箱（待实现） | **用户编排与体验**：Profile 配置管理、TUI 模式、Doer/Reviewer 并行协作、WhatsApp 群发、Dashboard 热重载 |
| **目标用户** | 运维人员、对高并发与状态一致性有严格要求的部署者 | 开发者、个人高级用户、倾向快速实验与多平台使用的终端用户 |
| **技术架构关键差异** | 复杂的事件循环与 Session 隔离机制，存在写锁超时链式阻塞风险；社区体量大，但 PR 合并瓶颈高 | 灵活的 Profile/插件体系，更轻量的事件处理；社区体量小，但贡献响应速度相对更快 |
| **对跨平台的支持优先级** | 以 Linux 为主，Telegram/Codex 修复多，Windows 原生支持未显式提出 | 明确将 Windows 原生支持列为 P3 功能请求，macOS 启动死锁已有关联 PR 修复，对移动端（Termux）也有社区贡献 |
| **生态整合模式** | 依赖外部插件 SDK（如 seam 模式路由），自身提供大量 CLI/诊断工具 | 更强调 MCP 工具协议与外部提供商适配，主动兼容非标准模型回复 |

## 6. 社区热度与成熟度

- **快速迭代阶段（功能扩张为主）**：**OpenClaw** 社区规模大、Issue/PR 爆发式增长，但合并率低、大量 P1 Bug 积压，暗示其处于“先加功能后治稳定性”的快速迭代期，成熟度尚需提升。
- **质量巩固阶段（稳定性与体验并行）**：**Hermes Agent** 虽然也有 P1 问题，但社区贡献更聚焦（如合入关键 SQLite 泄漏修复、解死锁 PR），且对跨平台、用户反馈响应更快，表现出更强的高可用导向。其社区互动更深度（如高阶用户分享 Doer/Reviewer 实践），成熟度略优于 OpenClaw。
- **总体判断**：两者均未达到成熟稳定期，但 Hermes Agent 在可控性上稍胜一筹，而 OpenClaw 在生态规模上具有显著优势。

## 7. 值得关注的趋势信号

1. **Agent 间协作模式成刚需**：Hermes Agent 社区用户成功实践 Doer/Reviewer 双角色编排（#34592），并请求项目原生支持。这表明用户不再满足于单 Agent 问答，而是追求“多智能体分工协作”的生产级能力。**开发者应关注 Agent 编排原语与共享记忆基础设施**。

2. **跨平台原生支持不可回避**：Hermes Agent 的 Windows 集成请求（#48716）获得社区强烈共鸣，OpenClaw 虽未明确提及，但其 WSL2 升级回归（#84610）也反映跨平台环境的不稳定性。**生态正向“Linux 优先”转向“多平台一等公民”**，缺乏跨平台 CI/CD 的项目将失去大量用户。

3. **模型推理链的透明化与兼容性**：Hermes Agent 对 `reasoning_content` 的兜底处理（PR #48795）和 OpenClaw 对回复截断的报告（#84516）共同指向一个趋势：**Agent 框架需要显式支持“推理过程”与“最终答案”的分离**，以适应 DeepSeek、MiniCPM 等推理模型，并防止信息静默丢失。

4. **“真理源”原语（Truth Source）的探索**：Hermes Agent 社区提出“Mission / Project source-of-truth primitive”（#48011），旨在为长期多步骤任务提供全局一致的项目上下文。这与 OpenClaw 社区对 `sessionKey` 文档与实际行为不符（#11665）的抱怨同源——**现有记忆/会话模型难以支撑战略性任务**，需要更高层级的项目级上下文原语。

5. **升级安全性成用户信任基石**：两个项目均出现升级后严重回归（OpenClaw 的 Telegram 重复回复、Hermes 的数据丢失），导致用户考虑降级。**维护者需建立“升级防火墙”**：在发布前进行更广范围的预发布测试，并提供一键回滚或补丁隔离机制，否则将侵蚀社区信任。

---

**结论**：当前 AI 智能体开源生态正经历“阵痛式增长”，社区规模与稳定性之间的张力日益凸显。OpenClaw 和 Hermes Agent 分别代表了“重型调度”与“灵活编排”两条路线，但共同面对的核心挑战是：**如何在不牺牲功能拓展速度的前提下，构建可靠的生产级基础设施**。对于技术决策者，建议优先关注项目的升级回溯机制、跨平台覆盖度以及多 Agent 协作原语的成熟度，而非单纯的功能数量。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 Hermes Agent 开源项目分析师，根据您提供的 GitHub 数据，我为您生成了 2026 年 6 月 19 日的项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-06-19

## 1. 今日速览

今日项目活跃度极高，共处理了 50 个 Issue 和 50 个 PR，显示出社区强烈的参与度和维护团队的快速响应能力。贡献集中在 Bug 修复（尤其是 4 个 P1 等级严重问题）、跨平台体验优化（Windows 原生支持、macOS 稳定性）以及与外部系统适配（Slack、飞书）。虽然今日无新版本发布，但大量高质量 PR 的提交预示着即将到来的功能增强和稳定性提升。项目整体状态健康，正从功能扩展阶段向生产环境高可用阶段过渡。

## 2. 版本发布

无

## 3. 项目进展

今日共有 2 个 PR 被合并/关闭，以及大量高质量 PR 被提交，标志着项目在关键领域取得了显著进展。

**重要合并/关闭项：**
- **#41386 [P1]**: 修复了 CLI/Desktop 在 SQLite 状态库不可用时仍能运行，导致会话数据丢失的问题。这是一个关键的稳定性修复，确保了数据持久性。
- **#37369 [P1]**: 修复了 Telegram 网关因 `response_store.db` 未正确关闭 SQLite 连接导致文件描述符泄漏的问题，该问题在运行约 2 天后会达到系统限制。此修复对于长时间运行的服务至关重要。

**关键推进项（今日提交的高价值 PR）：**
- **#48453 [P1]**: 解决了网关自重启时的死锁问题。当从 Terminal 工具调用中执行 `hermes gateway restart` 时，CLI 会同步等待网关进程退出，而网关又在处理该请求，导致死锁。该 PR 通过避免同步等待解决了这一高影响问题。
- **#48795 [P2]**: 修复了当模型（如 MiniCPM5, DeepSeek-R1）返回空`content`但包含`reasoning_content`时，Agent 无响应的核心问题。现在 Agent 会优雅地降级使用`reasoning_content`，极大提升了与推理模型的兼容性。
- **#48794 [P2]**: 在长度续写的消息路径中添加了守卫逻辑，防止生成空的 assistant 消息，避免了与严格遵循 OpenAI API schema 的提供商（Provider）的兼容性问题。

## 4. 社区热点

今日社区讨论活跃，多个 Issue 获得了 5 条以上评论，反映了用户的核心关切。

- **#34592 [Feature] [经验分享] Doer/Reviewer 双角色并行编排 + Hindsight 共享记忆实践**
    尽管是 5 月底提出的 Issue，但今日仍有更新。用户 `crayfish-ai` 分享了其基于 Hermes Agent 搭建的生产级 **Doer/Reviewer 双角色并行编排系统** 的实践。这个架构展示了如何通过 Agent 分工（执行者与审查者）和共享记忆来提升复杂任务（文献检索、代码审查）的质量和效率。这代表了社区中高阶用户对 Agent 编排模式的探索需求，希望 Hermes 能原生支持这种复杂的协作模式。
    [链接](https://github.com/NousResearch/hermes-agent/issues/34592)

- **#41625 [Bug] MCP 工具在 TUI 模式下不被 Agent 暴露**
    用户 `xinfengz194-cpu` 报告了一个影响用户体验的关键问题：MCP 服务器成功连接并注册工具，但 TUI 模式的 Agent 无法调用它们。这直接阻碍了依赖于 MCP 协议扩展能力的用户，表明 TUI 前端与底层工具注册系统之间存在集成断层。
    [链接](https://github.com/NousResearch/hermes-agent/issues/41625)

- **#47477 [Feature] WhatsApp 群发技能**
    用户 `bookra123456` 提供了一个包含完整步骤、修复方案和测试用例的一站式指南，旨在让 Hermes 通过 Termux 在 Android 上发送 WhatsApp 群发消息。这展示了社区用户对移动端和社交平台集成功能的强烈需求，并愿意贡献完整的解决方案。
    [链接](https://github.com/NousResearch/hermes-agent/issues/47477)

## 5. Bug 与稳定性

今日 Bug 报告数量较多，涵盖多个组件，其中不乏 P1 严重等级问题。以下按严重程度排列：

**P1 (严重)**
- **#48746**: [macOS 服务重启卡死] Hermes gateway 在 macOS 上使用 exit code 75 自重启，但 launchd 的 KeepAlive 配置未处理此退出码，导致服务被终止。已有关联 PR #48453 旨在解决 gateway 重启死锁问题。
    [Issue链接](https://github.com/NousResearch/hermes-agent/issues/48746) | [PR #48453](https://github.com/NousResearch/hermes-agent/pull/48453)
- **#48519**: [数据丢失] 当网关在子配置文件下运行时，会话会记录到 `sessions.json` 但 `state.db` 为空，导致完全数据丢失。这是一个回归问题，与 #40344、#46144 相关。
    [链接](https://github.com/NousResearch/hermes-agent/issues/48519)
- **#48721**: [更新失败] `hermes update` 在 macOS 系统 Python 上运行失败，由于 PEP 668 保护机制，uv 包管理器会错误地使用 `--system` 标志。这是一个影响系统 Python 用户的严重问题。
    [链接](https://github.com/NousResearch/hermes-agent/issues/48721)

**P2 (中等)**
- **#47868**: [API 兼容性] Agent 向聊天补全 API 的 payload 中泄漏了 `timestamp` 元数据，被严格的 OpenAI 兼容提供商拒绝。这是影响模型兼容性的常见问题。
    [链接](https://github.com/NousResearch/hermes-agent/issues/47868)
- **#48649**: [Cron 不感知 Profile] Cron 任务不遵循 Profile 设置，技能和存储都使用全局路径，导致在不同 Profile 下行为异常。
    [链接](https://github.com/NousResearch/hermes-agent/issues/48649)
- **#48689**: [诊断误报] `hermes doctor` 报告过时的 `ui-tui` npm 漏洞和 `gemini` API Key 错误的假阳性，影响了诊断工具的可信度。
    [链接](https://github.com/NousResearch/hermes-agent/issues/48689)

## 6. 功能请求与路线图信号

社区功能需求呈现出一致的方向：**提升 Agent 生产化能力、跨平台兼容性和可配置性**。

- **强力候选进入下一版本：**
    - **#48011 [P3]**: 用户 `tymrtn` 提出需要一个“任务/项目”的“真理源”原语。目前 Hermes 的记忆/技能/目标是碎片化的，缺少一个在战略性任务中 Agent 必须遵循的全局性项目上下文。此功能若实现，将极大提升 Agent 在长期、多步骤项目中的一致性。已有类似构思的 PR #48809 开始支持外部上下文文件。
        [Issue链接](https://github.com/NousResearch/hermes-agent/issues/48011) | [PR #48809](https://github.com/NousResearch/hermes-agent/pull/48809)
    - **#41190 [P3]**: 需要一个统一的插件路由挂钩，以便在每个对话轮次中覆盖 `provider` 和 `model`。这能解决目前路由逻辑分散在配置、启发式和失败恢复路径中的问题。
        [链接](https://github.com/NousResearch/hermes-agent/issues/41190)
- **用户迫切需求：**
    - **#48716 [P3]**: Windows 原生集成包。`bootstrap.py` 明确拒绝 Windows 环境，导致大量 Windows 用户被排斥，需要原生一键安装方案。这表明项目需要从“Linux 优先”向“多平台优先”转变。
        [链接](https://github.com/NousResearch/hermes-agent/issues/48716)
    - **#43784 [P3]**: 可共享的 Profile 模板。目前创建个性化 Agent Profile 需要从零开始配置，社区希望有模板功能以便于分享和复用。
        [链接](https://github.com/NousResearch/hermes-agent/issues/43784)
    - **#47058 [P3]**: Dashboard 配置热重载。修改 `config.yaml` 后需重启 Dashboard，社区希望提供轮询监听实现热重载，减少运维操作。
        [链接](https://github.com/NousResearch/hermes-agent/issues/47058)

## 7. 用户反馈摘要

- **痛点聚焦：**
    1.  **Windows 用户受阻**: #48716 的作者`markwang2658`明确提出，作为 Windows 用户，其入门体验被 `bootstrap.py` 对 Windows 的拒绝而切断。这是影响用户增长的最直接障碍。
    2.  **MCP 集成体验不佳**: #41625 的用户`xinfengz194-cpu`配备了完整的 MCP 工具，但在 TUI 模式下无法使用，表明功能覆盖不完整，影响了基于 MCP 生态的用户体验。
    3.  **非标准 API 提供商兼容性差**: #47868 和 #48795 反映了 Hermes Agent 对严格遵循行业标准（OpenAI API）或非标准回复（如`reasoning_content`）的模型兼容性存在短板，这会限制用户对模型的选择范围。
    4.  **配置与状态可见性不足**: #48731 (`/model`切换混乱)、#41517 (Dashboard 显示 Profile 与执行 Profile 不一致)、#48649 (Cron 不感知 Profile) 等 Issue 都指向了配置和运行状态的信息不对称，导致用户调试困难。

- **满意与亮点：**
    - 高阶用户`crayfish-ai`在 #34592 中分享的 Doer/Reviewer 实践表明，对于愿意投入时间和技术的用户，Hermes Agent 的框架足够灵活，可以构建出强大的、接近生产级别的 Agent 编排系统。
    - 用户`bookra123456`为 WhatsApp 集成贡献了详尽的单文件指南 (#47477)，显示出社区有强烈的贡献意愿，并乐于主动填补功能空白。

## 8. 待处理积压

以下为长期未响应或近期内部署的重要 Issue/PR，需要维护者关注：

- **长期开放式 PR**：
    - **#27738 [P3]**: “chore: update lark-oapi to 1.6.8”。该 PR 于 5 月 18 日提出，用于更新飞书 SDK 依赖，至今已超过一个月未合并。建议跟进合并。
        [链接](https://github.com/NousResearch/hermes-agent/pull/27738)
    - **#23243 [P3]**: “feat: TUI 16-language i18n framework”。这个雄心勃勃的国际化 PR 自 5 月 10 日提出，等待合并或反馈。若项目计划支持多语言，这是一个重要的基础设施。
        [链接](https://github.com/NousResearch/hermes-agent/pull/23243)

- **被遗忘或反复出现的 Bug (P2)**：
    - **#34569 (历史数据)**: “Persistent /goal is lost after context compression”。这个问题从 5 月底存在至今，是一个影响使用 `/goal` 进行长期规划的用户的核心问题。类似的上下文压缩/轮转问题还有 #33618 和 #18586。建议集中精力解决此系列问题。
        [链接](https://github.com/NousResearch/hermes-agent/issues/34569)
    - **#30594 [P2]**: “`hermes update` lazy-backend refresh fails with PEP 668”。此问题自 5 月 22 日提出，虽然已有部分修复 (#2648)，但在特定场景下仍未完全解决，今日新提的 #48721 与此问题同源，表明修复方案仍需完善。
        [链接](https://github.com/NousResearch/hermes-agent/issues/30594)

- **近期重要反馈，需确认路线图**：
    - **#48716 [P3]**: Windows 原生支持。这是一个重大的社区呼声，团队是否将其纳入下一个版本的路线图，需要公开回应。
        [链接](https://github.com/NousResearch/hermes-agent/issues/48716)
    - **#48011 [P3]**: “Mission / Project source-of-truth primitive”。此功能若实现，将代表 Agent 框架的重大进步，其优先级值得在项目路线图中明确。
        [链接](https://github.com/NousResearch/hermes-agent/issues/48011)

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*