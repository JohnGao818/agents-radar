# OpenClaw 生态日报 2026-06-22

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-22 03:50 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 OpenClaw 项目 GitHub 数据，生成一份结构清晰、数据驱动的项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-06-22

### 1. 今日速览

今日 OpenClaw 项目极其活跃，社区反馈与开发活动均处于高峰。24小时内处理了超过 500 条 Issue 和 500 个 PR，但 Issue 关闭率仅为 5%，PR 合并/关闭率约为 22%，处理速度远跟不上新问题的产生速度。新版本 `v2026.6.10-beta.1` 已发布，聚焦于 Agent 状态与会话管理的可靠性修复。然而，积压了大量 P1 级别的 Bug（尤其是消息丢失、会话状态损坏和回归问题），表明项目当前处于快速迭代与稳定性修复并行的关键阶段。整体活跃度评级：**极高**（但伴随稳定性风险）。

### 2. 版本发布

- **发布版本:** `v2026.6.10-beta.1`
- **链接:** [查看发布详情](https://github.com/openclaw/openclaw/releases/tag/v2026.6.10-beta.1)
- **核心更新 (Highlights):**
    - **更可靠的 Agent 转换与会话状态 (More reliable agent turns and session state):** 本次 Beta 版本重点解决了多个会话状态相关问题，包括：
        - 保留待处理的子代理（subagent）完成公告。
        - 确保聊天记录转录（transcript）内容不为空。
        - 维护媒体索引对齐。
        - 重新启动休眠的后续任务。
        - 一致地解决压缩（compaction）模型别名。
- **破坏性变更与迁移注意事项：**
    - **无明确破坏性变更说明**，但用户需注意，Beta 版本可能包含不稳定的特性。从 Issue `#95495` 的反馈看，跨版本升级（如从 `2026.6.8` 到 `2026.6.9`）曾发生过 `memory store` 存储路径静默变更导致数据重载的问题。建议用户在升级此 Beta 版本前，**务必备份 `~/.openclaw/memory/` 目录**，并关注 `openclaw doctor` 命令的健康检查结果。

### 3. 项目进展

今日项目在处理长期积压的 PR 和修复关键 Bug 方面有一定推进，主要涉及自动化、平台兼容性和稳定性。

- **基础设施与自动化：**
    - **PR #68936 (已合并):** [添加 PR 审查自动修复流水线 + Windows 守护进程](https://github.com/openclaw/openclaw/pull/68936)。这是一个大型特性，显著提升了开发效率和 Windows 平台的用户体验。
    - **PR #95649 (已开启):** [修复 CI：捆绑测试分片并调整 runner 配置](https://github.com/openclaw/openclaw/pull/95649)。旨在优化持续集成效率，减少构建时间。
- **平台兼容性：**
    - **PR #95640 (已关闭):** [整合 iOS 通知权限 UX](https://github.com/openclaw/openclaw/pull/95640)。改善 iOS 应用的推送通知体验。
- **稳定性与 Bug 修复：**
    - **PR #91097 (已合并):** [修复测试：为溢出压缩 harness 添加缺失的 `reasoning` 字段](https://github.com/openclaw/openclaw/pull/91097)。修复了测试文件中的一个类型错误，避免潜在的测试失败。
    - **PR #94260 (已合并):** [修复(cron): 允许 cron 任务返回空回复](https://github.com/openclaw/openclaw/pull/94260)。解决了静默告警监控等场景下，cron 任务因返回空回复而失败的问题。
    - **PR #94803 (已合并):** [修复(agents): 提高默认实时工具结果字符上限](https://github.com/openclaw/openclaw/pull/94803)。将 `DEFAULT_MAX_LIVE_TOOL_RESULT_CHARS` 从 16k 提升到 32k，解决了如截图等工具返回大量文本时被截断的问题。
- **新功能雏形：**
    - **PR #95603 (已开启):** [特性(config): 在环境变量替换中强制转换 JSON 数组/对象](https://github.com/openclaw/openclaw/pull/95603)。允许用户通过环境变量更灵活地配置复杂数据结构的配置项。

**项目进展小结：** 项目在自动化、平台适配和修复边缘 case 方面有所进展，但相比涌入的大量新 Bug 和需求，修复速度仍显不足。

### 4. 社区热点

今日社区讨论异常激烈，多个高优先级 Bug 引发了开发者广泛关注和热烈讨论。

- **🔥 #86519 (评论: 10):** **[[Bug]: Agent 在 Telegram 上重复回复相同消息](https://github.com/openclaw/openclaw/issues/86519)**
    - **诉求：** 用户强烈抱怨自 `2026.5.20` 更新后，Agent 在 Telegram 上出现 2-10 次的重复回复，尽管 `5.22` 版本有所缓解但未根治。这直接影响了核心聊天体验，社区情绪较为负面。
- **🔥 #90354 (评论: 8):** **[[Feature]: 为编译前内存刷新添加有界/验证的追加语义](https://github.com/openclaw/openclaw/issues/90354)**
    - **诉求：** 尽管是功能请求，但本质上是为了解决模型在内存刷新时可能填入过大或噪音数据的稳定性问题，社区对提高内存操作的安全性和可预测性诉求强烈。
- **🔥 #92043 (评论: 8):** **[[Bug]: 180s 压缩超时问题](https://github.com/openclaw/openclaw/issues/92043)**
    - **诉求：** 用户指出新的 180s 超时设置对于历史长、模型慢的会话来说过于严格，导致压缩任务必然失败，形成一个“慢但可恢复”到“完全失败”的恶性循环。
- **👍 #91363 (获得4个👍的反应):** **[[Bug]: 独立 cron 任务持续 LLM 请求失败](https://github.com/openclaw/openclaw/issues/91363)**
    - **诉求：** 独立 cron 任务几乎无法使用的情况引发了大量用户的共鸣。此问题阻塞了所有依赖自动 cron 任务的自动化场景。

**分析：** 社区热点集中于**会话状态损坏、消息丢失、以及核心功能（Telegram、Cron）的回归性 Bug**。用户对近期更新带来的稳定性下降表达了强烈不满。

### 5. Bug 与稳定性

今日报告的 Bug 数量庞大且严重，主要集中在会话状态、数据丢失和跨平台兼容性问题。

**极高严重性 (P1, 影响数据/会话完整性)**
- **#95623 (新报告):** `tool_use.id` 清理器在跨提供商故障恢复时漏处理 OpenAI 复合 ID，导致后续调用 Anthropic 时出现 400 错误，完全阻塞会话。
- **#95495 (新报告):** `2026.6.9` 版本升级导致内存向量存储路径静默迁移，触发 1499 个文件完全重嵌入，升级无任何警告，相当于数据损坏。
- **#92460:** 独立 cron 任务完成公告会丢失 `delivery.channel` 设置，导致消息无法送达。
- **#92076:** 当请求者会话不活跃时，子代理完成结果可能无法传递到用户。

**高严重性 (P1/P2, 功能崩溃或严重恶化)**
- **#93375 (新报告):** Telegram 轮询在短暂网络超时后进入静默崩溃循环，健康监控无法恢复。**（已有修复 PR #95643 在讨论）**
- **#91804 (新报告):** `2026.6.5` 版本出现内部推理内容泄漏给用户的严重隐私回归。
- **#91363:** 独立 cron 任务一致性地因“LLM 请求失败”而失败，导致自动化功能不可用。
- **#91009:** Codex 的 `PreToolUse` 钩子会生成 CPU 密集型进程，导致网关 RPC 停滞。
- **#90325:** Matrix 频道分发在 `v2026.6.1` 版本中崩溃（`TypeError: Cannot read properties of undefined (reading 'run')`），导致 Matrix 用户完全无法使用。

**分析：** 多个 P1 级 Bug 直接导致项目核心功能（聊天、自动化、跨模型调用）不可用，项目当前的稳定性面临严峻挑战。许多 Bug 被标记为“回归”，暗示近期代码变更引入了大量新问题。

### 6. 功能请求与路线图信号

尽管 Bug 修复是当务之急，社区仍提出了多项重要的未来功能需求。

- **强信号（已有相关 PR 或普遍需求）：**
    - **#90916: 话题会话家族 (Topic-session families):** 允许一个 Agent 拥有多个独立上下文的聊天“话题”，共享持久化记忆。已有相关的 PR (#90239, #90259) 在推进，是改善复杂对话体验的关键方向，**可能被纳入下一版本**。
    - **#90354: 编译前内存刷新限额 (Bounded memory flush):** 防止模型在自动刷新到记忆文件时写入过多或错误数据。这属于安全性增强，呼声很高。
- **远期信号（处于提议阶段）：**
    - **#92369: 改进独立 cron 中的子代理编排 (Subagent orchestration in cron):** 用户希望能在 cron 任务的隔离会话中可靠地创建、等待并聚合多个子代理的结果，以构建复杂工作流。这需要架构层面的改进。
    - **#43564: ACP 会话技能上下文注入 (ACP Session Skill Context):** 允许用户定义的技能被注入到 ACP (Codex/Pi/OpenCode/Gemini) 等外部 Agent 的环境中，增强其能力。

**路线图预测：** 短期路线图将毫无疑问地**聚焦于修复上述 P1 级 Bug**，特别是会话状态、消息递送和 Telegram/Matrix 等渠道的稳定性。长期来看，话题会话家族和内存操作安全性将是社区期待的下一阶段重点。

### 7. 用户反馈摘要

从今日的 Issue 评论中可以提炼出以下用户痛点：

- **“升级焦虑”**: 用户对频繁升级感到不安，因为许多新版本引入了比其修复问题更严重的回归。Issue #95495 的用户在未获任何警告的情况下丢失了价值的工作内存，这严重打击了用户对更新的信任。
- **“渠道体验割裂”**: Telegram、Matrix、Cron、Feishu 等渠道均报告了特有的严重 Bug，表明项目在多平台的一致性测试上存在缺陷。许多用户被迫回滚旧版本以求稳定。
- **“自动化受阻”**: Cron 任务的普遍失效是今日的一个重大负面反馈。依赖自动化（如告警、日报、定时任务）的用户群体感到被抛弃，这是对项目生态的重大打击。
- **“配置复杂性”**: Issue #91223 中，用户发现启用 `active-memory` 插件会让提示缓存命中率从 99.9% 暴跌至 22%，这种非预期的副作用让用户对高级配置功能感到困惑和挫败。

### 8. 待处理积压

以下为长期未解决但对项目健康度至关重要的问题，需维护者重点关注。

- **🚨 #67915 (创建于 2026-04-17):** [Local assistant attachments shown as "Unavailable"](https://github.com/openclaw/openclaw/issues/67915)
    - **状态：** 已标记为 `stale`，虽有 `linked-pr-open`，但超过两个月无人跟进。
    - **影响：** 这是一个让本地媒体文件预览功能失效的老问题，严重影响了用户体验。持续搁置可能导致相关功能彻底被弃用。
- **⚠️ #86612 (创建于 2026-05-25):** [Docker gateway container restart loop](https://github.com/openclaw/openclaw/issues/86612)
    - **状态：** 严重性 P1，但无修复 PR。涉及 Windows + Docker 的特定路径。
    - **影响：** 阻塞了部分 Windows 用户的 Docker 部署方式，且涉及沙盒环境 (`SANDBOX=1`)，可能还关乎安全问题。
- **⚠️ #88087 (创建于 2026-05-29):** [Poor UX for long-running background tasks](https://github.com/openclaw/openclaw/issues/88087)
    - **状态：** 评论数不多但反映了用户的流失（用户表示“I'm tearing it down”）。
    - **影响：** 这是一个综合性的反馈，涉及后台任务性能差、Cron 静默失败等问题。直接影响项目的口碑和用户留存。

**建议：** 维护团队应优先处理 `#67915` 和 `#86612`，即使不立即修复，也应给出明确的说明或启用策略，避免问题持续发酵导致用户流失。

---

## 横向生态对比

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 OpenClaw 和 Hermes Agent 两份动态日报，生成一份横向对比分析报告。

---

## AI 智能体与个人 AI 助手开源生态横向对比分析报告 (2026-06-22)

### 1. 生态全景

2026年6月22日，个人 AI 助手/自主智能体开源生态展现出“冰火两重天”的态势。一方面，社区参与度与功能迭代热情空前高涨，Telegram 多机器人支持、看板集成、话题会话等高级需求层出不穷，表明用户群体正从个人实验向复杂业务场景演进。另一方面，两大头部项目均面临严重的稳定性挑战：**快速迭代带来的回归性 Bug 与核心功能损坏（如消息丢失、会话状态损坏）已成为普遍痛点**，用户对“升级焦虑”和“PR 积压”的不满情绪显著。生态整体处于 **“高活跃度、高创新速度，但低稳定性”** 的关键转型期，项目的长期健康度取决于能否在功能扩展与质量巩固之间找到平衡。

### 2. 各项目活跃度对比

| 指标 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **24h 新 Issue 数** | 500+ (极高) | 50 (高) |
| **24h 新 PR 数** | 500+ (极高) | 50 (高) |
| **Issue 关闭率 (24h)** | 5% (极低) | 26% (中等) |
| **PR 合并/关闭率 (24h)** | 约22% (低) | 12% (极低) |
| **版本发布 (近日)** | `v2026.6.10-beta.1` | 无 |
| **核心关注点** | 会话状态损坏、消息丢失、渠道兼容性 | Provider 迁移阵痛、Telegram 多机器人、桌面端完善 |
| **健康度评估** | **极高活跃，但稳定性风险高**，修复速度远跟不上问题产生速度 | **高活跃，但 PR 积压严重**，关键修复难以落地，社区有挫败感 |

### 3. OpenClaw 在生态中的定位

- **优势**：OpenClaw 是当前生态中**社区规模最大、数据量级最高**的项目（Issue/PR 量级是 Hermes Agent 的10倍）。其核心聚焦于 **Agent 状态与会话管理的底层可靠性**，如 `v2026.6.10-beta.1` 对子代理转换、聊天记录转录、内存索引对齐的修复，体现了其在**核心框架鲁棒性**上的技术深度。
- **技术路线差异**：相比 Hermes Agent，OpenClaw 更侧重于**通用框架的稳定性**，其修复工作大量集中在会话基础架构（Compaction、Memory Store、Cron 任务）上。而 Hermes Agent 则更强调**渠道适配与功能扩展**（如 Telegram 多机器人、看板集成）。
- **社区规模对比**：OpenClaw 社区规模显著更大，但负面情绪也更集中。用户对“升级引入新 Bug”的抱怨是 Hermes Agent 的数倍，表明其**快速迭代策略在维护用户信任上面临更大压力**。

### 4. 共同关注的技术方向

两大项目在以下方向上涌现了高度相似的需求，表明这是行业共同挑战：

- **会话状态管理与持久化 (OpenClaw & Hermes Agent)**：
    - **具体诉求**：OpenClaw 在 #95495 中报告了升级时向量存储路径静默迁移导致数据损坏；Hermes Agent 在 #50576 修复了 FTS 写入损坏导致对话丢失的问题。双方都在解决会话数据的**完整性、可恢复性和升级兼容性**。
- **Agent 编排与任务分发 (OpenClaw & Hermes Agent)**：
    - **具体诉求**：OpenClaw 在 #92460 修复了独立 cron 任务消息丢失；Hermes Agent 在 #50575 修复了 cron 会话标题崩溃。两大社区都反馈了**后台任务（Cron）的可靠性不足**，以及**子代理结果传递的稳定性**（OpenClaw #92076，Hermes Agent #50530）。
- **跨平台体验一致性 (OpenClaw & Hermes Agent)**：
    - **具体诉求**：OpenClaw 在 Telegram (#86519) 和 Matrix (#90325) 上均报告了破坏性 Bug；Hermes Agent 则重点解决 Telegram 多机器人和桌面端兼容性。**确保 Agent 在不同渠道（IM、桌面、Web）上行为一致，是用户的核心诉求**。

### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **功能侧重** | **核心框架与状态管理**。更注重 Agent 生命周期的可靠性、会话上下文的管理、记忆的持久化。 | **渠道整合与高级用户体验**。更注重 Gateway 的多平台适配（Telegram、桌面），以及桌面端的高级功能（Kanban、系统托盘）。 |
| **目标用户** | **开发者与高级用户**。需要搭建稳定、自定义程度高的 Agent 系统的用户。对底层机制有理解能力，能承受一定的不稳定性。 | **更广泛的用户群体**，包括 Power User 和轻度业务用户。对桌面端体验和即时通讯机器人有更高要求。 |
| **技术架构差异** | **更“重”的底座**。似乎采用了更复杂的会话压缩（Compaction）和内存管理（Memory Store），架构的复杂性也是其 Bug 来源。 | **更“轻”的核心，重渠道**。核心框架相对简单，但围绕 Gateway 和 Provider 的抽象层非常丰富，形成了以适配器（Adapter）为主的架构。 |
| **关键 Bug 类型** | **数据损坏、会话状态崩溃、核心功能（如 Cron）静默失败**。多为 P1 级、影响数据完整性的问题。 | **Provider 兼容性崩溃、功能缺失或体验不佳（如 Intel Mac 支持）、配置繁琐**。多为 P2 级、功能受损问题。 |

### 6. 社区热度与成熟度

- **快速迭代与震荡阶段 (高风险高回报)**：
    - **OpenClaw**：社区体量最大，功能迭代最快，但**稳定性风险最高**。项目正处于严重的“成长阵痛”期，大量回归性 Bug 威胁着用户信赖。用户情绪复杂，既有对新功能的期待，也有对“升级焦虑”的强烈不满。**建议关注此类项目的用户做好严格的备份和回滚策略。**
- **功能扩展与整合期 (中度风险)**：
    - **Hermes Agent**：社区活跃，功能迭代同样迅速，但主要风险在于 **PR 积压导致修复延迟** 和 **Provider 依赖的脆弱性**（如 Google Gemini CLI 下线）。用户情绪相对乐观，但对合并速度和关键兼容性问题感到不满。**建议关注此类项目的用户可参与社区讨论，推动 PR 合并，并留意 Provider 变更公告。**

### 7. 值得关注的趋势信号

- **信号一：Provider 生态依赖性风险加剧**。Hermes Agent 的 `google-gemini-cli` 服务下线和 OpenClaw 未报告的 Provider 问题，共同敲响了警钟。**依赖单一商业 API 或CLI 的 Agent 项目，其黑盒变更可能瞬间破坏整个用户基础**。未来，更健壮的 Provider 抽象层、多 Provider 自动故障转移、以及对本地化模型的更好支持，将成为项目的核心竞争力。
- **信号二：会话状态管理成为“必争之地”**。两大项目均将大量精力投入会话数据的完整性、序列化和升级兼容性。**“如何让 Agent 记住并延续一次长时间、多轮、多代理的对话”**，已不再是锦上添花的功能，而是决定用户是否信任 Agent 作为“数字身份”的基础。这暗示着**底层存储技术（如向量数据库、日志结构合并树）的优化将成为下一阶段的技术焦点**。
- **信号三：“多 Agent 协作”与“后台任务编排”需求攀升**。OpenClaw 的 #92369 (子代理编排) 和 Hermes Agent 的 #10452 (多 Telegram 机器人)，都指向一个趋势：用户不再满足于单个 Agent 的简单问答，而是希望构建**能独立运行、相互协作、并自动化执行复杂工作流的 Agent 网络**。这为事件驱动架构、任务调度引擎和上下文共享协议等相关技术提供了巨大的发展空间。
- **信号四：平台兼容性仍是“拦路虎”**。从 OpenClaw 的 Windows 守护进程到 Hermes Agent 的 Intel Mac 支持，**跨平台体验的割裂**是头部项目共同的痛点。这不仅仅是简单的打包问题，更关乎底层系统 API 差异、沙箱兼容性和性能优化。对于开发者而言，选择支持平台更广、或对目标平台有深度优化的项目，能显著降低部署和运维成本。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，以下是基于您提供的 GitHub 数据为 Hermes Agent 项目生成的 2026-06-22 项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-06-22

## 今日速览

项目今日活跃度极高，单日 Issue 与 PR 更新均达到 50 条，显示社区参与度与维护工作均十分密集。然而，PR 合并/关闭率（6/50）低于 Issue 关闭率（13/50），**合并积压问题依然显著**，可能导致部分修复和新功能无法及时触达用户。最突出的社区焦点集中在 **Google Gemini CLI 服务下线后的迁移阵痛**（Antigravity）、**Telegram 多机器人支持** 以及 **桌面端功能完善** 上。虽然有大范围 Bug 被提交和修复，但项目整体功能迭代势头强劲。

## 版本发布

无新版本发布。

## 项目进展

过去24小时内，虽然合并的 PR 数量（6条）远低于待合并的数量（44条），但合并的 PR 质量较高，解决了多个关键问题。

- **安全与稳定性**
  - [#50568 fix(email): make pairing opt-in, ignore unknown senders by default](https://github.com/NousResearch/hermes-agent/pull/50568): 修复了一个重要的安全问题，默认情况下邮件网关将忽略未知发件人，防止配对码被滥用。
  - [#50576 fix(gateway): detect FTS write corruption in DB health probe](https://github.com/NousResearch/hermes-agent/pull/50576): 修复了 FTS5 写入路径损坏导致对话记录丢失的严重 Bug，增强了数据库健康检查的健壮性。
  - [#50575 fix(cron): robust session title generation](https://github.com/NousResearch/hermes-agent/pull/50575): 一次性修复了三个与 cron 会话标题相关的 Bug（包括重复标题导致的崩溃）。

- **平台兼容性与配置**
  - [#50563 fix(gateway): accept any inbound file type across all messaging platforms](https://github.com/NousResearch/hermes-agent/pull/50563): 解除了对上传文件类型的限制，提升了跨平台（Telegram/Discord/Slack）的文件接收能力。
  - [#50574 fix(config): accept space-separated key in `config set`](https://github.com/NousResearch/hermes-agent/pull/50574): 修复了配置命令 `config set` 不接受空格分隔键的问题，提升了 CLI 易用性。

- **AI Provider 路由**
  - [#50578 fix(bedrock): route non-Claude Bedrock models off the Anthropic SDK](https://github.com/NousResearch/hermes-agent/pull/50578): 修复了 Bedrock 上非 Claude 模型错误地通过 Anthropic SDK 路由导致的崩溃问题。

这些合并表明项目正积极修复安全漏洞、提升核心库（如 SQLite）健壮性，并优化用户体验。项目在稳定性和易用性方面有实质性的前进。

## 社区热点

今日讨论最热烈的 Issue 主要集中在三大方向：

1.  **Google Gemini CLI 迁移阵痛 (服务中断)**
    多条高活跃度 Issue 紧密相关：
    - [#29294 [CLOSED] google-gemini-cli provider: Gemini CLI / Code Assist sunsets](https://github.com/NousResearch/hermes-agent/issues/29294): 在 Gemini CLI 服务下线后关闭，**获得 8 个 👍**，表明大量用户关注此变更。
    - [#49701 [CLOSED] [Bug]: google-gemini-cli provider completely broken after Code Assist sunset](https://github.com/NousResearch/hermes-agent/issues/49701): 明确指出 Google Gemini CLI 提供商完全失效。
    - [#50530 [OPEN] [Bug]: google-antigravity 遗留 P2 集成问题汇总](https://github.com/NousResearch/hermes-agent/issues/50530): 由用户`kzeokytjvwhnrtl13otf-bit` 在服务下线当日（6月22日）报告，汇总了迁移到 Antigravity 后的三个严重 P2 Bug（子代理崩溃、并发掉线、400错误）。

    **分析**: 尽管核心整合的 PR (#50454) 已合并，但“从旧服务迁移”的震荡远未结束。社区正承受着新旧 Provider 切换带来的阵痛，用户对新 Provider `google-antigravity` 的稳定性和成熟度有非常急迫的诉求。

2.  **Telegram 多机器人支持**
    - [#10452 [OPEN] Support multi Telegram bots for gateway routing and send_message](https://github.com/NousResearch/hermes-agent/issues/10452): 获得了 **7 条评论和 4 个 👍**，是今日最活跃的 feature 请求。
    - [#18652 [OPEN] Fix Telegram multi-bot dispatch edge cases](https://github.com/NousResearch/hermes-agent/pull/18652): 对应的修复 PR 也已跟进。

    **分析**: 用户 `yimwoo` 提出了一个典型的 B 端或高级用户需求：管理多个 Telegram Bot。这表明社区正从个人实验向更复杂的业务场景演进，对 gateway 的功能要求更高。

3.  **桌面端功能与体验**
    - [#41222 [OPEN] Feature Request: Integrate Kanban Board into Desktop App](https://github.com/NousResearch/hermes-agent/issues/41222): 获得 **6 个 👍**，并有对应 PR #41756 在推进。
    - [#37505 [OPEN] Hermes Desktop macOS DMG is arm64-only and fails on Intel Macs](https://github.com/NousResearch/hermes-agent/issues/37505): **6 条评论**，讨论如何解决 Intel Mac 用户的兼容性问题。

    **分析**: 桌面端是社区关注的核心。用户既希望增加高级功能（如看板集成），也面临基础的平台兼容性（Intel Mac）问题。这反映了桌面端从 Power User 工具向更广泛用户群体过渡的“成长的烦恼”。

## Bug 与稳定性

今日报告的 Bug 数量较多，按严重程度排列如下：

- **P1 - 关键安全**
  - [#14073 [CLOSED] Security: browser orphan reaper trusts /tmp PID files and can SIGTERM arbitrary same-user processes](https://github.com/NousResearch/hermes-agent/issues/14073): 浏览器孤儿进程清理器存在安全风险，可能误杀同一用户下的其他进程。

- **P2 - 高优先级 (功能受损)**
  - [#50530 [OPEN] google-antigravity 遗留 P2 集成问题汇总](https://github.com/NousResearch/hermes-agent/issues/50530): 新 Provider 存在子代理崩溃、频繁重新认证、会话无法恢复等严重问题。
  - [#49701 [CLOSED] google-gemini-cli provider completely broken ...](https://github.com/NousResearch/hermes-agent/issues/49701): 旧 Provider 完全失效。
  - [#49983 [OPEN] OpenRouter free models fail with HTTP 404](https://github.com/NousResearch/hermes-agent/issues/49983): 免费模型在 OpenRouter 上无法使用。
  - [#49008 [OPEN] openai-codex image gen plugin ... HTTP 400](https://github.com/NousResearch/hermes-agent/issues/49008): Image Generation 插件调用失败。
  - [#50292 [OPEN] non-Claude models routed through Anthropic SDK](https://github.com/NousResearch/hermes-agent/issues/50292): Bedrock 路由错误，**已有 Fix PR #50578 待合并**。
  - [#50438 [OPEN] TUI sessions don't record cwd](https://github.com/NousResearch/hermes-agent/issues/50438): TUI 会话不记录当前工作目录，导致桌面端分组错误。

- **P3 - 中等优先级 (体验问题)**
  - [#37505 [OPEN] Hermes Desktop macOS DMG is arm64-only ...](https://github.com/NousResearch/hermes-agent/issues/37505): Intel Mac 无法运行。
  - [#37917 [OPEN] Desktop (Windows): Ctrl +/- zoom does nothing](https://github.com/NousResearch/hermes-agent/issues/379017): Windows 桌面端缩放快捷键无效。
  - [#50553 [CLOSED] Switching configurations does not take effect](https://github.com/NousResearch/hermes-agent/issues/50553): 配置切换不生效，**已有 Fix PR #50574 待合并**。
  - [#50537 [OPEN] duplicate auto-generated session titles cause unhandled ValueError](https://github.com/NousResearch/hermes-agent/issues/50537): 自动生成的重复标题导致报错，**已有 Fix PR #50575 待合并**。
  - [#42033 [OPEN] langfuse not receiving trace from hermes](https://github.com/NousResearch/hermes-agent/issues/42033): Langfuse 追踪失败。

**总结**：项目面临新旧 Provider 切换的阵痛期，新集成 `google-antigravity` 的稳定性是当前最大的风险点。尽管多数 Bug 已有相应修复 PR，但这些 PR 仍处于“待合并”状态，是社区反馈的核心痛点。

## 功能请求与路线图信号

- **高频需求**:
  - **[Telegram 多机器人] (#10452)**: 满足更复杂的运营场景，已有对应 PR #18652，**很可能被纳入下一个小版本**。
  - **[Kanban Board 集成] (#41222)**: 将看板功能集成至桌面端，解决用户工作流割裂的痛点，已有 PR #41756 在推进。
  - **[Minimize to System Tray] (#50167**): 请求桌面端关闭窗口时最小化到系统托盘，而不是退出，对于后台任务非常实用，属于成熟的用户体验改进。

- **战略讨论**:
  - **[#41180 [Strategy] Desktop app risks shifting Hermes from power-user harness to watered-down GUI](https://github.com/NousResearch/hermes-agent/issues/41180)**: 这是一个非常值得关注的策略性讨论。核心议题是“桌面端化”是否会让 Hermes 偏离其作为 Power User 工具的本质。这预示着项目在追求更广泛用户群和维护核心用户价值之间需要谨慎平衡。

- **Provider 生态演变**: 大量围绕 `google-gemini-cli` 的 Issue 和转为 `google-antigravity` 的请求，**是路线图的明确信号**：项目必须完成并从这次依赖迁移中吸取教训，建立更健壮的 Provider 抽象层，降低对单一商业服务的依赖风险。

## 用户反馈摘要

从今日 Issue 讨论中可以提炼出以下用户反馈：

- **满意度**:
  - 社区对能快速开启新 Provider（如 Antigravity）的 PR 表示认可，#50454 的合并被视为解决问题的第一步。

- **痛点与不满意**:
  - **“迁移之痛”强烈**：用户对 Google Gemini CLI 的突然失效反应激烈，特别是对新 Provider `google-antigravity` 的稳定性感到失望，质疑“为何能在有这么多 Bug 的情况下直接推送”。
  - **桌面端卡在“中间态”**：用户感觉桌面端功能既不够强大（缺少看板、系统托盘等功能），也不够完善（Intel Mac 无法使用、Win 快捷键无效、布局问题）。这种“两边不靠”的状态让部分用户感到沮丧。
  - **“PR 积压”情绪**：虽然开发者修复迅速，但 PR 合并效率低下，导致修复无法落地。用户 `kzeokytjvwhnrtl13otf-bit` 在 Issue #49701 中直接抱怨 **“PR 超过30天未合并”**，反映出社区对维护者合并速度的不满。
  - **配置和路由混乱**：用户对 `config` 命令不能接受空格键、模型路由错误等低级 Bug 感到困惑，认为这些问题不应出现在相对成熟的版本中。

## 待处理积压

以下为长期未响应或积压情况较为严重的重要 Issue/PR，建议维护团队重点关注：

1.  **高关注度的 Provider 中断**
    - [#49701 / #49705 (CLOSED as duplicate)]: `google-gemini-cli` 彻底失效问题。虽然被关闭为重复，但**实际用户影响依然存在**，需要确保新的 Antigravity Provider 能稳定覆盖所有旧用户功能。

2.  **长期待审的关键修复 PR**
    - [#18652 [OPEN] Fix Telegram multi-bot dispatch edge cases](https://github.com/NousResearch/hermes-agent/pull/18652): 等待合并已超两周，对应的功能请求 (#10452) 热度极高，应优先处理。
    - [#10455 [OPEN] feat(gateway): add multi-account telegram routing](https://github.com/NousResearch/hermes-agent/pull/10455): 与 #18652 高度相关，均为实现“Telegram 多机器人”关键功能的 PR。

3.  **桌面端兼容性 “Show Stopper”**
    - [#37505 [OPEN] Hermes Desktop macOS DMG is arm64-only...](https://github.com/NousResearch/hermes-agent/issues/37505): 此 Issue 已开放 20 天，**但对于 Intel Mac 用户是绝对的阻塞问题**，严重损害了桌面端的用户口碑。

4.  **策略性决策等待**
    - [#41180 [OPEN] [Strategy] Desktop app risks shifting Hermes from power-user harness to watered-down GUI](https://github.com/NousResearch/hermes-agent/issues/41180): 虽然不是一个需要“修复”的 Bug，但它是一个决定项目未来的关键讨论。维护者需要更多地参与并给出明确的路线图指引，以避免社区产生对项目方向的困惑。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*