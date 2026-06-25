# OpenClaw 生态日报 2026-06-25

> Issues: 432 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-25 02:51 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-06-25

---

## 1. 今日速览

过去 24 小时，OpenClaw 社区保持极高活跃度：累计 432 条 Issue 更新（新开/活跃 368 条，关闭 64 条），500 条 PR 更新（待合并 434 条，合并/关闭 66 条）。项目同时发布了 **v2026.6.10** 和 **v2026.6.11-beta.1** 两个版本，带来 Slack 中继模式、对话快速模式、更可靠的模型路由等多项重要改进。Bug 修复与功能请求仍以 P1/P2 级别为主，安全、会话状态、消息丢失等高频标签持续受到关注。整体看，项目迭代速度快，社区参与度强，但部分长期积压问题（如跨平台桌面应用、MCP 工具注入）仍需维护团队加速决策。

---

## 2. 版本发布

### 2.1 v2026.6.11-beta.1
- **发布日期**：2026-06-11  
- **主要亮点**：
  - **更强大的频道控制**：支持 Slack 中继模式、原生 Mattermost `/oc_queue` 命令以及每个 DM 独立的模型覆盖，使频道操作更容易自动化和调优。（#94707, #95546, #95120）
  - （其余变更因 release notes 截断未完整展示）
- **破坏性变更**：未明确标注，但涉及频道级别配置变化，建议升级后检查各自频道的 `relayMode`、`modelOverride` 等配置项。  
- **迁移注意**：若使用自建 Mattermost，需确保服务端支持 `/oc_queue` 命令；Slack 中继模式需重新评估权限模型。

### 2.2 v2026.6.10
- **发布日期**：2026-06-10  
- **主要亮点**：
  - **对话自动快速模式**：OpenClaw 可在短轮次对话中启用快速模式，并在较长对话中回退到正常模式，带有限界回退与传递行为。（#85104）
  - **更可靠的模型路由**：Zai 模型合成路径得到优化（具体内容因截断未完整展示）。
- **破坏性变更**：无公开破坏性变更。  
- **迁移注意**：自动快速模式默认开启，若希望始终保持正常模式，可在配置中显式设置 `fastMode: false`。

---

## 3. 项目进展

今日共合并/关闭 **66 个 PR**（包括修复与功能合并）。虽然我们无法逐一列举所有已合入的 PR，但从已关闭的 Issue 和活跃 PR 来看，以下重要工作已取得实质推进：

- **Bug 修复推进**：
  - 已关闭 `#95495`（v2026.6.9 内存存储无迁移搬迁导致重新嵌入 1499 文件）—— 该回归问题已在最新版本中修复。
  - 已关闭 `#95554`（v2026.6.9 Telegram 富文本段落换行与表格渲染损坏）—— 该回归问题已修复。
- **活跃 PR 向主线靠拢**：
  - `#77127`（write 工具追加模式）—— 解决 `#40001` 数据丢失问题，现在正在等待维护者最终审查。
  - `#95996`（让 yielded parent runs 保持 deferred 状态直至子 agent 完成）—— 涉及 cron、子 agent 注册、Discord 源消息等多条路径，防止过早完成。
  - `#96642`（Telegram 富文本实体验证失败时回退纯文本）—— 针对 `#96363` 的修复，提升 Telegram 回复可靠性。

整体看，项目在 **稳定性** 与 **频道兼容性** 方面继续向前迈进，多个回归问题得到快速响应。

---

## 4. 社区热点

| Issue/PR | 类型 | 评论数 | 核心诉求 |
|----------|------|--------|----------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | Issue (OPEN) | 109 | 请求提供 Linux/Windows 桌面应用，弥补当前仅支持 macOS/iOS/Android 的缺口。5 个月来持续热议，但标签含有 `needs-product-decision`，尚未进入开发。 |
| [#88838](https://github.com/openclaw/openclaw/issues/88838) | Issue (OPEN) | 36 | 追踪核心会话/转录 SQLite 迁移的访问器 seam——从整体架构角度讨论技术实现路径，参与开发者较多。 |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) | Issue (OPEN) | 17 | `SIGUSR1` 重启时 Signal daemon 存在竞态条件，导致孤儿进程和发送失败。用户讨论活跃，已附上复现方法。 |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) | Issue (OPEN) | 17 | 提议分层次引导文件加载以节省 token 消耗，用户场景明确（大工作区、多人共享 agent）。 |
| [#32473](https://github.com/openclaw/openclaw/issues/32473) | Issue (OPEN) | 17 | 控制 UI 要求在非 HTTPS 或非 localhost 环境中进行设备身份认证，被用户视为回归。 |

**分析**：社区最强烈的诉求集中在 **跨平台桌面支持**（#75）—— 这是迄今评论和点赞最多的议题，但长期缺乏产品决策。其次是 **Signal 稳定性**（#22676）和 **上下文窗口优化**（#22438），反映了用户对生产环境可靠性和成本控制的关心。

---

## 5. Bug 与稳定性

按严重程度排列今日报告/活跃的 Bug（P1 最高）：

| 严重级别 | Issue | 摘要 | 是否有 Fix PR |
|----------|-------|------|---------------|
| P1 | [#22676](https://github.com/openclaw/openclaw/issues/22676) | Signal daemon `stop()` 在 SIGUSR1 重启时竞态，导致孤儿进程和发送失败 | 无（标签含 `linked-pr-open` 但未列具体 PR） |
| P1 | [#29387](https://github.com/openclaw/openclaw/issues/29387) | 代理目录下的 bootstrap 文件被静默忽略，仅 workspace 文件生效 | 无 |
| P1 | [#48003](https://github.com/openclaw/openclaw/issues/48003) | `steer` 模式无法在回合中注入消息，只能等回合完成 | 无（标签有 linked-pr-open） |
| P1 | [#40001](https://github.com/openclaw/openclaw/issues/40001) | write 工具缺乏追加模式，孤立 cron 会话覆盖共享文件 | 已有 PR [#77127](https://github.com/openclaw/openclaw/pull/77127) 待合并 |
| P1 | [#39476](https://github.com/openclaw/openclaw/issues/39476) | A2A `sessions_send` 双向调用导致重复消息 | 无 |
| P1 | [#86996](https://github.com/openclaw/openclaw/issues/86996) | 活跃内存 + Codex 路径导致长响应延迟、钩子超时、启动中止、事件循环停滞 | 无 |
| P1 | [#85030](https://github.com/openclaw/openclaw/issues/85030) | MCP 工具未注入到子 agent（`sessions_spawn`）会话，文档中所有配置方式均无效 | 无 |
| P1 | [#86827](https://github.com/openclaw/openclaw/issues/86827) | 群聊会话进入 `failed` 状态后静默丢弃后续消息 | 无（标签有 linked-pr-open） |
| P1 | [#95833](https://github.com/openclaw/openclaw/issues/95833) | 子 agent 中止-结算无法释放 `.jsonl.lock`，永久阻塞会话 | 无 |
| P1 | [#87109](https://github.com/openclaw/openclaw/issues/87109) | macOS 上 Gateway 堆内存增长至 1073MB+，cron 任务静默失败 | 无 |
| P2 | [#57901](https://github.com/openclaw/openclaw/issues/57901) | Safeguard 压缩忽略 `compaction.model` 配置，使用会话模型 | 无 |
| P2 | [#31331](https://github.com/openclaw/openclaw/issues/31331) | Docker 安装 + Sandbox 无法正常绑定 workspace | 无 |
| P2 | [#38327](https://github.com/openclaw/openclaw/issues/38327) | v2026.3.2 中 google-vertex/gemini-3.1-pro-preview 报 `Cannot convert undefined or null to object` | 无 |

**小结**：今日报告了多个 P1 级别的严重 Bug，覆盖 **Signal 竞态、文件写入、会话状态卡死、MCP 集成、内存泄漏** 等关键领域。其中 write 工具追加模式已有关联 PR（#77127）接近合并，其他问题大多尚在等待修复或产品决策。没有出现新的崩溃级安全问题。

---

## 6. 功能请求与路线图信号

| 功能请求 | Issue | 热度 | 可能纳入版本？ |
|----------|-------|------|----------------|
| Linux/Windows 桌面应用 | [#75](https://github.com/openclaw/openclaw/issues/75) | ⭐⭐⭐⭐⭐ | 尚未有开发迹象，但长期呼声最高。 |
| Slack Block Kit 富消息支持 | [#12602](https://github.com/openclaw/openclaw/issues/12602) | ⭐⭐⭐ | 明确需求，但未看到对应 PR。 |
| 分层次引导文件加载（渐进上下文控制） | [#22438](https://github.com/openclaw/openclaw/issues/22438) | ⭐⭐⭐ | 已有详细设计，看板上有多个相关 PR（如智慧上下文优化），可能纳入 v2026.7。 |
| 子 agent 完成后的扩展钩子 | [#22358](https://github.com/openclaw/openclaw/issues/22358) | ⭐⭐ | 增强可观测性，但无明确 PR。 |
| Telegram Business 模式支持 | [#20786](https://github.com/openclaw/openclaw/issues/20786) | ⭐⭐⭐ | 已有贡献者实现（8 评论，6 点赞），可能在下个 beta 中。 |
| 备份/恢复工具 | [#13616](https://github.com/openclaw/openclaw/issues/13616) | ⭐⭐ | 长期需求，但尚无开发力量。 |
| 文件系统沙箱配置 | [#7722](https://github.com/openclaw/openclaw/issues/7722) | ⭐⭐⭐ | 与安全相关，已被多次提及，可能纳入路线图。 |
| 多 agent 协作增强（能力画像+共享黑板+分层记忆+代币治理） | [#35203](https://github.com/openclaw/openclaw/issues/35203) | ⭐⭐ | 属于 RFC 阶段，需要架构讨论。 |

**信号**：**write 工具追加模式**（#77127）已接近合并，预计将在下个稳定版中落地，直接解决 `#40001` 数据丢失问题。**Telegram Business 支持** 和 **Slack Block Kit** 也有活跃开发。长期来看，**跨平台桌面应用**和**多 agent 协作**是社区最期待的两大方向。

---

## 7. 用户反馈摘要

从今日活跃的 Issue 评论中，可以提炼出以下真实用户痛点和使用场景：

- **睡眠代理管理**：用户 `UberKitten` 报告 Signal 中继重启时进程混乱，导致消息发送失败，期望系统能在重置配置时完全清理旧进程。
- **上下文窗口浪费**：用户 `882soft` 抱怨大型工作区下每次对话都加载所有引导文件，浪费 token 预算，希望引入按需加载。
- **数据丢失恐惧**：用户 `altsoulkiller` 反馈多个 cron 会话同时写入同一个记忆文件时互相覆盖，希望 write 工具支持追加或并发安全写入。
- **MCP 集成失效**：用户 `reidperyam` 表示严格按照文档配置 MCP 工具暴露到子 agent，但完全不起作用，感觉文档与实际行为脱节。
- **Telegram 富文本退化**：用户 `Ashowt` 在升级 v2026.6.9 后段落换行和表格渲染损坏，担心升级影响日常使用。
- **内存泄漏焦虑**：用户 `Tanklive` 报告 macOS 上 Gateway 内存持续增长至 1GB+，导致 cron 任务静默失败，重启后暂时缓解但无法根除。
- **权限模型缺失**：多位用户（如 `aaroneden`、`subrih`、`ramtinz`）呼吁增加更细粒度的文件系统/命令执行权限控制，以实现“允许一切但阻止危险命令”的策略。

整体用户情绪：**高度参与但部分问题长期未解决**，对于新版本带来的回归问题（如 #95495、#95554）用户反应迅速，团队也在一天内关闭了这些 Bug，反应速度值得肯定。

---

## 8. 待处理积压

以下 Issue 和 PR 已存在较长时间且缺乏明显进展，建议维护团队优先关注：

| 事项 | 类型 | 创建时间 | 最新更新 | 现状 |
|------|------|----------|----------|------|
| [#75](https://github.com/openclaw/openclaw/issues/75) Linux/Windows 桌面应用 | Issue | 2026-01-01 | 2026-06-25 | 109 评论，80 👍，标签 `needs-product-decision`，近 6 个月无实质开发。 |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) exec-approvals 添加黑名单支持 | Issue | 2026-02-01 | 2026-06-24 | 7 👍，标签 `needs-maintainer-review` 和 `needs-product-decision`。 |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) 文件系统沙箱配置 | Issue | 2026-02-03 | 2026-06-24 | 4 👍，配置项已实现但未被采纳。 |
| [#13616](https://github.com/openclaw/openclaw/issues/13616) 备份/恢复工具 | Issue | 2026-02-10 | 2026-06-24 | 标签 `needs-product-decision`。 |
| [#16670](https://github.com/openclaw/openclaw/issues/16670) 向导应包括记忆配置 | Issue | 2026-02-15 | 2026-06-25 | 对新手体验影响大，但无开发计划。 |
| [#22676

---

## 横向生态对比

好的，作为资深技术分析师，我已根据您提供的两份项目日报，并结合对该领域生态的理解，为您准备了这份横向对比分析报告。

---

### **AI 智能体与个人助手开源生态横向对比分析报告 (2026-06-25)**

#### **1. 生态全景**

当前，个人 AI 助手/自主智能体开源生态正处于**由“可用”向“好用”、“可靠”及“经济”过渡的关键阶段**。社区的核心关注点已从基础功能的实现，转向 **Token 成本优化、稳定性提升、多平台兼容以及跨代理协作**。以 OpenClaw 和 Hermes Agent 为代表的两个项目，分别代表了 **“平台型”** 和 **“能力型”** 两种不同的发展路径，前者强于渠道集成与社区治理，后者则聚焦于核心推理效率与编排能力。两个项目均显示出极高的社区参与度，但也都面临着**长期积压问题**（如桌面端支持）与**新版本引入的回归 Bug** 之间的平衡挑战，这表明生态的成熟度仍在爬坡过程中。

#### **2. 各项目活跃度对比**

| 项目 | 今日 Issues 活跃数 | 今日 PR 活跃数 | 版本发布 (今日) | 项目健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 368 条新增/活跃 | 434 条待合并 | **是** (v2026.6.10, v2026.6.11-beta.1) | **高活跃，快速迭代**。版本迭代极快，对关键回归 Bug 响应迅速，但有大量 P1 级 Bug 待修复及长期积压产品决策。 |
| **Hermes Agent** | (极高) | (极高) | **否** | **高活跃，质量巩固**。虽无新版本，但今日合并/关闭9个PR，专注于修复多个关键 Bug（网关、委托任务），同时社区对性能优化呼声极高。 |

*注：Hermes Agent 日报告未提供具体 Issues/PRs 总数字，但其描述为“活跃度极高”、“Issues与PR池均维持高位运行”。*

#### **3. OpenClaw 在生态中的定位**

*   **核心优势**：**强大的渠道控制和社区治理能力**。OpenClaw 的迭代速度（一天两个版本）和对 Slack 中继、Mattermost 命令等企业级渠道的原生支持，使其在**团队协作和自动化场景**中具有显著优势。其对回归 Bug 的快速关闭（如 #95495, #95554）也体现了高效的工程响应。
*   **技术路线差异**：OpenClaw 更倾向于构建一个 **“通用 AI 操作系统”**，强调将 AI 能力无缝嵌入到各类通讯工具和工作流中。Hermes Agent 则更像一个 **“高能 AI 引擎”**，专注于核心的推理效率、上下文管理和多代理编排。
*   **社区规模对比**：从 Issues/PRs 的绝对数量看，OpenClaw 社区的活跃度更高，且其最热门议题（如跨平台桌面应用 #75）拥有 109 条评论，显示出更大的用户基数和对特定功能更为集中的诉求。Hermes Agent 的社区讨论则更偏向技术深度优化（如 Token 开销），反映了其用户群体技术能力更强。

#### **4. 共同关注的技术方向**

| 共同技术方向 | 涉及项目 | 具体诉求 (Issue/PR 案例) |
| :--- | :--- | :--- |
| **多平台/渠道支持** | OpenClaw, Hermes Agent | - **OpenClaw**: 请求 Linux/Windows 桌面应用 (#75)，Slack Block Kit 富消息支持 (#12602)。<br>- **Hermes Agent**: 请求 Rocket.Chat 支持 (#3725)，Windows 桌面客户端 UTF-8 编码 Bug (#52244)。 |
| **Agent 间协作与编排** | OpenClaw, Hermes Agent | - **OpenClaw**: 多 agent 协作增强 RFC (#35203)，A2A 双向调用导致重复消息 Bug (#39476)。<br>- **Hermes Agent**: 构建通用 ACP 客户端以编排所有 ACP 兼容代理 (#5257)，`delegate_task` 工具修复 (#50636, #48644)。 |
| **上下文/Token 优化** | OpenClaw, Hermes Agent | - **OpenClaw**: 分层次引导文件加载以节省 Token 消耗 (#22438)。<br>- **Hermes Agent**: 延迟工具 Schema 加载 (#6839)，Token 开销分析 (73% 为固定开销) (#4379)。 |
| **内存/文件系统管理** | OpenClaw, Hermes Agent | - **OpenClaw**: 内存泄漏 (macOS Gateway) (#87109)，文件写入并发 (write 工具追加模式) (#40001)。<br>- **Hermes Agent**: 可配置的内存后端 (#6932)，秘密修订系统破坏代码语法 (#33801)。 |

#### **5. 差异化定位分析**

| 维度 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **功能侧重** | **渠道集成与管理** (Slack, Mattermost, Telegram)，工作流自动化。 | **核心推理效率** (Token 优化、模型路由)，多代理 **编排层** (ACP 客户端)。 |
| **目标用户** | **团队用户与社区运营者**。侧重部署、管理、通过 IM 工具与 AI 交互。 | **高级开发者和研究者**。关注成本效益、自定义编排、深入性能调优。 |
| **技术架构** | **平台化**。强调作为一个稳定、可靠的后端服务运行。 | **模块化/组件化**。关注代理本身的能力解耦和外部工具/系统的互操作性。 |
| **迭代风格** | **激进、快速响应**。高频版本发布，快速修复回归 Bug，但可能引入新的不稳定因素。 | **稳健、质量优先**。版本发布节奏较慢，但每个 PR 都旨在解决深层次问题或显著提升性能。 |
| **社区痛点** | **产品决策积压**。大量高热度需求（如桌面端）长期停留于讨论阶段。 | **核心库 Bug 持续**。高并发下的认证、网关稳定性等基础设施问题频发。 |

#### **6. 社区热度与成熟度**

*   **第一梯队 - 快速迭代与规模扩张期**：
    *   **OpenClaw**: 社区活跃度最高，版本发布频率惊人。但项目仍处于**功能完善和稳定性巩固并行的“青春期”**。大量 P1 级 Bug 和长期积压的产品决策是其成熟度提升的主要障碍。

*   **第二梯队 - 质量巩固与深度优化期**：
    *   **Hermes Agent**: 社区热度高，但更聚焦于解决深层问题。项目处于**从“可用”向“高效、可编排”过渡的“青年期”**。Token 优化、多代理编排等高级诉求的涌现，是其开发者社区成熟的标志，但基础设施的稳定性是其必须跨越的鸿沟。

#### **7. 值得关注的趋势信号**

1.  **“Token 经济学” 成为核心优化指标**：两个项目社区均自发地、量化地讨论 Token 浪费问题（Hermes Agent 甚至有人分析了 73% 的 Token 被浪费）。这预示着**未来的 AI Agent 竞争将从“模型能力”转向“成本效率”**。能通过架构创新（如延迟加载、Tool 输出压缩）显著降低 Token 消耗的项目将获得强劲的社区动力。

2.  **从单一 Agent 到 Agent 网格**：OpenClaw 的 A2A 和 Hermes Agent 的通用 ACP 客户端，共同指向了**“代理即服务”**的未来。开发者不再满足于单个 AI 助手的强大，而是希望构建一个**可互相调用、协同工作的 Agent 网络**。这将是下一个杀手级应用的基础架构。

3.  **平台原生体验是破局点**：无论是 OpenClaw 对 Slack/Mattermost 的深度集成，还是 Hermes Agent 对 Telegram 内联按钮的改进请求，都表明**深度融合到用户现有的沟通与工作平台**是获取广泛用户的关键。单纯的 API 或 Web 界面已无法满足需求，原生、富媒体的客户端体验是必然趋势。

4.  **安全性是伴随功能扩展的永恒挑战**：从 OpenClaw 的 MCP 工具注入失效和 Signal 竞态，到 Hermes Agent 的凭证管理和秘密修订系统破坏代码，**安全性、正确性和权限模型**始终是 Agent 大规模部署的暗礁。未来，细致的权限沙箱（如文件系统、命令执行）和稳健的凭证管理将是决定项目能否真正进入企业级场景的核心要素。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 Hermes Agent 项目数据，生成了 2026-06-25 的项目动态日报。

---

### Hermes Agent 项目动态日报 | 2026年06月25日

### 1. 今日速览

今日项目活跃度极高，Issues与PR池均维持高位运行，社区参与热情不减。核心关注点集中在**Token开销优化**（如延迟加载工具 Schema）、**多代理编排**（通用 ACP 客户端）以及**桌面端与网关的质量问题**。尽管无新版本发布，但多个关键 Bug 已被 PR 快速响应，显示出项目在稳定性和可靠性上的持续投入。整体而言，项目正处于功能迭代与问题修复并行的密集开发期。

### 2. 版本发布

*无*

### 3. 项目进展

今日共合并/关闭9个PR，推动多项修复与功能改进，项目稳定性与代码质量均有所提升。

-   **网关稳定性修复**：PR #52263 修复了 Discord 网关在转发 DM 回复时因缺少 `guild_id` 导致发送失败的问题。这是一个潜在的沟通渠道静默失效的严重问题，已得到解决。 [链接](https://github.com/nousresearch/hermes-agent/pull/52263)
-   **代理能力提升**：PR #52272 针对推理模型的“思考超时”问题提供了明确的指导信息，避免了以往误导性的文件写入建议，提升了用户交互体验。 [链接](https://github.com/nousresearch/hermes-agent/pull/52272)
-   **关键 Bug 修复**：
    -   PR #52233 修复了辅助任务在遇到显式提供者的速率限制错误（429）时无法触发备用链的问题，增强了系统弹性。 [链接](https://github.com/nousresearch/hermes-agent/pull/52233)
    -   PR #50636 修复了 `delegate_task` 工具返回 HTTP 404 错误的问题。 [链接](https://github.com/nousresearch/hermes-agent/pull/50636)
    -   PR #50636 修复了 Docker 环境下终端工具的 `cwd` 覆盖参数未进行安全清理的潜在安全漏洞。 [链接](https://github.com/nousresearch/hermes-agent/pull/50636)
-   **代码质量改进**：今日有大量 PR（如 #52269, #52268, #52262, #52258）专注于清理代码中无用的 f-string 前缀，涉及超过 300 处修改，表明项目在持续提升代码规范和可读性。 [链接](https://github.com/nousresearch/hermes-agent/pull/52269)

### 4. 社区热点

今日社区讨论热度集中在 **Token 效率**和**功能扩展**两大方向。

1.  **Token 开销优化 (Token Overhead)**：
    -   **Issue #6839**: 提议实现“延迟工具 Schema 加载”，通过两阶段工具注入来减少 API 调用的 Token 开销。获 28 条评论、14 👍。 [链接](https://github.com/nousresearch/hermes-agent/issues/6839)
    -   **Issue #4379**: 一位用户通过自建仪表盘分析发现，73% 的 API 调用 Token 被固定开销浪费。此问题虽无 👍 但获得 16 条评论，说明社区对 Token 效率的普遍关注。 [链接](https://github.com/nousresearch/hermes-agent/issues/4379)
    -   **社区诉求**：用户强烈希望减少无效 Token 消耗，尤其是在本地模型部署场景下，这直接关系到成本和运行效率。

2.  **多平台与代理间协作 (Multi-Agent & Platform Support)**：
    -   **Issue #3725**: 要求支持 Rocket.Chat 作为消息通道，获 11 条评论和 10 👍，表明社区对更多平台集成的期待。 [链接](https://github.com/nousresearch/hermes-agent/issues/3725)
    -   **Issue #5257**: 提议构建通用 ACP 客户端，使 Hermes 能编排所有 ACP 兼容的编码代理（如 Claude Code）。获 11 条评论和 16 👍，反响极佳。 [链接](https://github.com/nousresearch/hermes-agent/issues/5257)
    -   **社区诉求**：用户希望 Hermes 不仅能作为单一代理使用，更能成为一个编排中心，连接并管理不同的 AI 服务。

### 5. Bug 与稳定性

今日Bug报告数量较多，涉及多个组件和平台。以下是按严重程度排列的重点问题：

-   **P1 级 Bug**：
    -   **Issue #52197**: Discord 网关的跨进程缓存清理机制存在瓶颈，会阻塞 asyncio 事件循环，导致 Discord 心跳包无法发送，引发连接断开。目前已有社区成员讨论。 [链接](https://github.com/nousresearch/hermes-agent/issues/52197)
    -   **Issue #19566**: OpenAI-Codex 凭证池在高并发场景下可能丢弃新增凭证，影响用户认证。状态为 OPEN。 [链接](https://github.com/nousresearch/hermes-agent/issues/19566)

-   **P2 级 Bug (部分已有修复 PR)**：
    -   **Issue #52244**: Hermes Desktop (Hermes One) 在 Windows 上存在 UTF-8 编码问题，导致输出信息被截断和乱码。新报告问题。 [链接](https://github.com/nousresearch/hermes-agent/issues/52244)
    -   **Issue #52160**: 在两次以上上下文压缩后，发送给 Anthropic 的消息历史可能以 `assistant` 角色开头，导致 API 400 错误。新报告问题。
    -   **Issue #52212**: 在不支持 `edit_message` 的平台上，所有工具调用的进度消息被静默丢弃。这是一个与平台兼容性相关的关键问题。 [链接](https://github.com/nousresearch/hermes-agent/issues/52212)
    -   **Issue #52271**: 推理模型（如 Reasoning models）的“思考超时”被误判为 `context_overflow`，触发破坏性的压缩和重置循环。此问题已被 PR #52272 修复。 [链接](https://github.com/nousresearch/hermes-agent/issues/52271)

-   **P3 级 Bug**：
    -   **Issue #52255**: Desktop 远程模式在连接经认证的远程网关时因 WebSocket/API 认证失败而卡在启动恢复界面。 [链接](https://github.com/nousresearch/hermes-agent/issues/52255)
    -   **Issue #33801**: 密钥/秘密的修订系统会破坏代码语法，导致 `write_file` 等工具执行失败，是一个影响开发体验的回归性 Bug。
    -   **Issue #52261**: 本地推理（oMLX/MLX）的内存不足等错误被错误分类为 `context_overflow`，导致系统进行不必要的压缩循环。

### 6. 功能请求与路线图信号

社区提出的新功能需求多与**性能优化**和**架构升级**相关，反映用户对高阶应用场景的需求。

-   **强烈信号**：
    -   **令牌/Tokens 优化**：`延迟工具 Schema 加载`和`工具输出压缩`是当前社区呼声最高的性能优化方向，很可能被优先考虑。
    -   **多代理编排**：通用 ACP 客户端的提出，与已有的 `delegate_task` PR (#48644) 形成呼应，表明项目考虑将“代理即服务”能力作为下一阶段的重点。
    -   **内存系统重构**：`可配置的内存后端`和`重命名 memory.md` 的请求指向了当前固定内存方案的灵活性不足，未来可能引入更模块化的内存管理。

-   **潜在纳入**：
    -   PR #22648 和 #8427 分别请求添加 Ollama Cloud 和 Google Vertex AI 作为新的提供商，这能显著扩大用户基础，有较大概率被合并。
    -   PR #38731 为 Telegram 的 Cron 递送添加了内联按钮，是提升用户体验的实用功能。
    -   PR #19448 提出的“隐身模式”（临时对话）在多会话场景中非常实用。

### 7. 用户反馈摘要

从近期的 Issues 和评论中，可以提炼出以下用户反馈：

-   **痛点**：
    -   **Token 浪费**：用户 `Bichev` 和 `jarviszomine` 均对每次 API 调用的 Token 浪费表示不满，认为这降低了效率并增加了成本。
    -   **OAuth 凭证管理**：多个用户反馈 `openai-codex` 的凭证管理有 Bug，导致丢失或无法使用，影响了核心功能。
    -   **桌面端/Windows 支持**：用户 `SrDee00` 报告了 Windows 客户端的乱码问题，`codehere9` 报告了远程模式认证失败，这表明跨平台兼容性和测试仍需加强。
    -   **学习成本**：有用户认为当前 `smart` 审批模式在逻辑上存在缺陷，导致本应被批准的操作为了安全而无法执行，影响了易用性。

-   **满意点**：
    -   **社区生态**：用户 `410979729` 为项目贡献了独立的 memory 插件，体现了活跃的社区生态。
    -   **创新功能**：用户 `flowforgelab` 和 `easyvibecoding` 分别提出了通用 ACP 和更好的委托机制，显示出用户对项目高级功能的探索和期待。
    -   **多平台支持**：对 `Rocket.Chat` 和 `MCP 服务`的请求表明，用户期望 Hermes 能更深入地融入其现有的工作流程和工具链。

### 8. 待处理积压

以下是一些值得维护者关注的老旧或重要问题：

-   **高票 Issue 长期未解决**：
    -   **#13834** (P2): `openai-codex` 在官方 CLI 正常工作时失败。创建于 04-22，至今仍未关闭，对依赖 Codex 的用户影响较大。 [链接](https://github.com/nousresearch/hermes-agent/issues/13834)
    -   **#4379** (P3): Token 开销分析报告。创建于 04-01，有 16 条评论，但一直未获得官方明确回应。 [链接](https://github.com/nousresearch/hermes-agent/issues/4379)

-   **长期未合并的 PR**：
    -   **#8427** (P3): 添加 Vertex AI 支持的 PR，自 04-12 以来一直在等待合并，期间多次 rebase，可能因架构变动导致推延。建议维护者评估其当前优先级。 [链接](https://github.com/nousresearch/hermes-agent/pull/8427)
    -   **#19448** (P3): 添加“隐身模式”的功能，自 05-04 提交以来，虽有更新但仍未合并。 [链接](https://github.com/nousresearch/hermes-agent/pull/19448)

-   **无人认领的 P2 Bug**：
    -   **#17945** (P2): `delegate_task` 返回 HTTP 404 错误。虽然克隆到了一个 PR，但 Issue 本身仍未关闭，根因是否彻底解决存疑。 [链接](https://github.com/nousresearch/hermes-agent/issues/17945)

---
**报告日期**：2026-06-25
**分析师**：AI Agent 开源项目分析引擎

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*