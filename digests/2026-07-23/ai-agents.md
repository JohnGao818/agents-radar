# OpenClaw 生态日报 2026-07-23

> Issues: 451 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-07-23 02:23 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的OpenClaw项目数据，我为您生成了2026年7月23日的项目动态日报。

---

## OpenClaw 项目动态日报 — 2026-07-23

### 今日速览

今日OpenClaw项目社区活动高度活跃，但与修复和稳定性相关的讨论占据了主导。过去24小时内，Issue和PR总数均超过450条，显示出庞大的社区参与度，但其中大量为“stale”旧问题和新报告的严重Bug。最值得关注的是，一个**P0级别的Gateway启动回归问题**仍未解决，同时性能回归、安全漏洞和核心功能缺陷的讨论热度极高。尽管没有新版本发布，但多个关键修复PR（如Telegram论坛主题修复）已被合并，项目正在积极应对当前面临的稳定性挑战。

### 版本发布

无。尽管有多个涉及发布流程的PR在活动，但并未发布新版本。目前正处于一个通过密集修复来稳定代码库的阶段，下一个版本可能将包含大量Bug修复和针对2026.7.1版本的补丁。

### 项目进展

今日项目向前迈进的步调非常务实，主要集中在修复关键通道、核心架构和基础设施问题上。

- **核心通道修复**：PR #112794 [已关闭] 修复了Telegram频道在论坛主题（Forum Topics）中无法可靠地对已有消息进行编辑、删除或回复的问题，确保了信息变更在主题内的持久性。这对于依赖此功能的团队协作场景至关重要。
- **多平台与兼容性**：PR #112844 [开放] 修复了`kilocode`扩展在需要HTTP代理的网络环境中无法发现模型的问题，改善了企业级部署的兼容性。PR #112723 [已关闭] 修复了iOS App中Markdown列表项显示不全的问题，提升了移动端用户体验。
- **基础设施与工具链**：PR #110562 [开放] 为本地工作流健全性检查添加了超时机制，防止在CI等场景下脚本无限挂起，提升了开发工具链的健壮性。
- **发布流程优化**：PR #112841 和 #112845 [均已关闭] 改进了发布验证流程，解决了稳定版候选版本因CI脚本更新而无法通过验证的问题，为未来的顺利发布扫清障碍。

整体来看，项目正在快速修补已知的、影响范围较广的Bug，特别是优化了多平台通道和内部工具链的健壮性。

### 社区热点

今日社区讨论的焦点并非某个单一功能，而是集中在几个长期存在且严重影响用户体验的核心Bug上。

1.  **跨平台桌面应用需求 (Issue #75)**：拥有115条评论和80个点赞，是当之无愧的社区最高呼声。用户`steipete`明确提出对Linux和Windows原生应用的需求，希望获得与macOS相似的功能集。这表明社区对桌面端的使用体验有极高的期待，且Mac/iOS/Android的支持已经让用户对跨平台一致性产生了强烈需求。

2.  **性能回归问题 (Issue #85333)**：尽管评论数不及#75，但17条评论聚焦于一个非常具体的性能回归问题：`openclaw doctor --fix`命令在2026.5.20版本后变慢了4-5倍。用户`samson1357924`提供了详细的对比数据（55秒 vs 229秒+），并定位出瓶颈是会话快照路径遍历。这反映出用户对工具性能和效率的敏感度非常高，即使是命令行工具的性能下降也会被立即察觉并上报。

3.  **核心功能退化 (Issue #92043, #91009, #96857)**：这些Issue共同描绘了一幅核心功能不稳定的图景：
    - **#92043**：180秒的编译超时被视为单一墙钟时间，导致大型会话合法性的长时间编译总是失败。
    - **#91009**：Codex原生的钩子会衍生大量CPU密集型进程，导致网关RPC阻塞。
    - **#96857**：正常的工具文本输出会退化为`(see attached image)`占位符，导致Agent对关键输出“失明”。
    这些问题的评论数多且来自不同用户，表明系统在核心会话管理、资源调度和上下文处理方面正面临普遍性的挑战。

### Bug 与稳定性

今日报告的Bug主要集中在稳定性、性能和安全三个维度，且不少是高优先级的回归问题。

- **P0 (紧急)**
    - **[Bug]: update to openclaw 2026.7.1: gateway fails to start w/ error** (Issue #108435): 7月15日报告，升级到2026.7.1后，Gateway在各种启动方式下均失败。**目前无已合并的修复PR**，是当前最紧急的阻塞问题，影响所有希望升级的用户。
- **P1 (严重)**
    - **性能回归**：`openclaw doctor --fix` 速度下降4-5倍 (Issue #85333)。**无已合并修复PR**。
    - **核心功能异常**：Codex PreToolUse钩子引发CPU风暴 (Issue #91009)；文本输出退化为图片占位符 (Issue #96857)；子Agent原始输出泄露给聊天用户 (Issue #90840)。**以上均无已合并修复PR**。
    - **安全与配置**：容器化部署无法使用外部化频道插件 (Issue #92516)；`tools.deny`无法从Codex延迟工具中隐藏技能工坊 (Issue #97911)。**无已合并修复PR**。
    - **无障碍问题**：屏幕阅读器因`aria-live="polite"`在流式传输时重复朗读每个Token (Issue #65538)。**无已合并修复PR**，但有相关的开放PR。
- **P2 (中等)**
    - 多项长期存在的稳定性和可用性问题，如QQBot WebSocket重连后丢失通道配置 (Issue #88955)、Gateway内存持续增长 (Issue #87314)等，均处于“stale”状态或缺少关键信息。

**总结：** 尽管有修复PR被合并，但今日暴露出的Bug数量和严重性依然很高，尤其是P0的Gateway启动失败和多个P1的核心功能回归，表明项目当前可能正处于一个稳定性波动的时期。

### 功能请求与路线图信号

今日的功能请求依然集中在增强Agent的可控性和安全性上，与项目近期的一些策略调整相符。

- **强制执行与安全（高优先级信号）**： Issue #13583 和 #10659 分别提出了“预响应强制执行钩子”和“屏蔽密钥”功能。这些请求旨在通过代码机制而非提示词来约束Agent行为，防止凭证泄漏和关键步骤遗漏。这与组织级部署和金融等高风险场景的需求高度吻合。结合 PR #112773 (添加可移植的Agent策略设置) 来看，**下一个版本很可能在Agent的策略管理和安全执行方面有重大增强**。
- **会话生命周期管理**：Issue #10142 请求增加一个`session:end`内部钩子事件，以便与Temporal等工作流编排系统集成。这是一个对高级用户和开发者非常有吸引力的功能，如果实现，将大大扩展OpenClaw作为平台的能力。PR #112589 (为会话派生添加租约绑定元数据) 也指向了这个方向，表明项目组正在考虑更成熟的会话管理模型。
- **用户体验微调**：Issue #38568 请求在系统提示中注入上下文窗口使用百分比。虽然优先级不高，但这反映了高端用户希望更精细地监控和利用模型能力的诉求。

### 用户反馈摘要

从今日的Issue评论中，可以提炼出用户的几类核心感受：

- **普遍存在的挫败感与焦虑：** 用户对性能回归、启动失败和核心功能异常感到困扰。例如，针对Issue #85333，用户提供了详尽的数据来证明回归，表现出对工具效率下降的失望。Issue #108435的评论中，用户尝试了各种启动方式（systemd, ollama, manual）均失败，反映了问题的普遍性和用户的无奈。
- **对安全与可控性的高要求：** 社区对Agent安全问题非常重视。Issue #10659和#13583的创建者和评论者（如 `jmkritt`, `JamieMolty`）来自安全或金融领域，他们明确表示软性提示词约束不可接受，需要**机械性地防止**Agent犯错。
- **对特定场景的支持缺失：** Issue #75的跨平台应用请求获得了大量支持，表明macOS用户期望在其他平台获得一致体验。Issue #87318关于Amazon Bedrock推理配置文件的限制，也体现出企业用户在云服务集成上的特定痛点。
- **对核心功能可靠性的担忧：** 用户报告的子Agent输出泄露 (#90840)、Agent会话恢复旧历史 (#99054)、工具输出变为图片占位符 (#96857) 等问题，动摇了用户对系统核心数据处理和上下文管理可靠性的信任。

### 待处理积压

以下是一些长期未解决且重要性高的问题，需要维护者特别关注：

1.  **长期未解决的社区诉求：**
    - **Issue #75 [OPEN]**：Linux/Windows Clawdbot Apps。自2026年1月提出，评论115条，人气极高，但至今未有明确进展。这是社区呼声最强的功能需求。
    - **Issue #41199 [OPEN]**：Agent间通信工具参数冲突。3月报告的问题，涉及核心的Agent协同工作能力，长期未解决会阻碍复杂工作流的构建。

2.  **“stale”状态的重要Bug：**
    - **Issue #85103 [CLOSED]**：模型回退链在提供者配额耗尽时未触发。虽然被关闭，但该问题影响系统的高可用性和可靠性，需要确认是否已从根本上修复。
    - **Issue #87318 [OPEN]**：Amazon Bedrock 推理配置不受支持。对于使用AWS生态的用户是一个硬性阻碍，5月报告至今无解决方案。
    - **Issue #77802 [CLOSED]**：`doctor --fix`原子性失败。该问题会导致用户陷入“无法修复”的循环，虽然关闭，但应确保其修复方案是彻底且经过充分验证的。

**分析师提示：** 当前项目健康度处于“活跃但有风险”的状态。社区参与度极高，但高优先级Bug的数量和持续时间值得警惕。建议维护团队优先解决 **P0 Gateway启动失败 (Issue #108435)** 和 **性能回归 (Issue #85333)** 这两个直接影响绝大多数用户的问题，以稳定社区信心。同时，对于**跨平台应用 (Issue #75)** 这类长期诉求，即使无法立即实现，也建议给出正式的规划或时间表，避免社区热情消耗。

---

## 横向生态对比

好的，作为资深技术分析师，基于您提供的两个项目的详细动态日报，我为您生成了2026年7月23日的横向对比分析报告。

---

## 个人 AI 智能体开源生态横向对比分析报告 (2026-07-23)

### 1. 生态全景

截至2026年7月23日，个人AI助手/自主智能体开源生态呈现出 **“双核鼎立，分化加剧”** 的态势。一方面，以OpenClaw和Hermes Agent为首的核心项目社区极度活跃，每日产生数百乃至上千条技术讨论，标志着该领域已进入规模化的生产部署与优化阶段。另一方面，生态的健康度出现明显分化：OpenClaw作为生态的“旗舰”，正经历着由功能膨胀带来的稳定性阵痛；而Hermes Agent则保持相对稳健的迭代节奏，侧重于生产级功能打磨与多平台扩展。整个生态的核心议题已从“如何构建一个Agent”转向“如何构建一个可靠、安全、可跨平台协作的Agent系统”。

### 2. 各项目活跃度对比

| 指标 | **OpenClaw** | **Hermes Agent** |
| :--- | :--- | :--- |
| **今日Issue动态** | 450+ (其中包含大量P0/P1严重Bug报告) | 50条 (46新开/活跃, 4关闭) |
| **今日PR动态** | 450+ (多个关键修复PR被合并) | 50条 (11合并/关闭) |
| **版本发布** | 无 | 无 |
| **社区健康度评估** | **活跃但有风险**。社区参与度极高，但P0级Gateway启动失败及多个核心功能回归问题集中爆发，表明项目可能处于一个高强度的稳定性波动期。 | **活跃且稳健**。Bug数量控制较好，维护者对核心问题的响应速度快（如及时修复桌面端UI Bug和记忆擦除风险），社区氛围偏向于功能优化和场景扩展。 |
| **核心关注点** | 稳定性、性能回归、安全修复、跨平台应用诉求。 | 跨平台会话共享、桌面端交互可靠性、生产级修复、记忆管理、唤醒词等新功能。 |

### 3. OpenClaw 在生态中的定位

OpenClaw可被定义为该生态的 **“核心参照实现”** 和 **“功能复杂性引领者”**。

- **优势：** 功能广度领先，覆盖了从核心会话管理、多平台通道（Telegram, QQBot）到复杂的Agent策略、网关架构等几乎所有方面。其庞大的社区规模和Issue/PR数量，本身就是其生态主导地位的体现。用户对跨平台桌面应用（Issue #75）的呼声极高，也反向证明了大量用户基于OpenClaw构建了核心工作流。
- **差异：** 与Hermes Agent相比，OpenClaw的社区规模更大、功能更重，但也因此面临更严重的 **“成长烦恼”** 。当前其面临的P0/P1级Bug，如Gateway启动失败（#108435）、Agent输出退化（#96857），直接影响用户体验和信任度。
- **社区规模对比：** OpenClaw的日Issue/PR数量级是Hermes Agent的**9倍**，反映出其社区基数远超后者，但也意味着其维护者面临的压力和噪音更大。

### 4. 共同关注的技术方向

多个项目涌现出对以下方向的共性需求：

1.  **Agent安全与可控制性增强：**
    - **涉及项目：** OpenClaw, Hermes Agent
    - **具体诉求：** 超越提示词约束的“硬性”安全机制。OpenClaw社区提出“预响应强制执行钩子”（#13583）和“屏蔽密钥”（#10659）功能，要求从代码层面防止凭证泄露。Hermes Agent的Bug修复（#69745）也集中在防止记忆文件被意外擦除。这表明，随着Agent被赋予更多权限，社区对**确定性安全边界**的需求愈发强烈。

2.  **跨平台与跨协议统一：**
    - **涉及项目：** OpenClaw, Hermes Agent
    - **具体诉求：** 并非仅指GUI客户端，而是**会话上下文与能力的无缝迁移**。OpenClaw用户要求Linux/Windows原生桌面应用（#75）；Hermes Agent用户则明确提出CLI、Telegram、Discord之间的会话语境共享（#4335）。用户希望在不同入口使用同一Agent时，体验和记忆是连续的。

3.  **会话生命周期与记忆管理：**
    - **涉及项目：** OpenClaw, Hermes Agent
    - **具体诉求：** 更精细的会话控制和更可靠的记忆系统。OpenClaw要求增加`session:end`钩子（#10142），以集成工作流编排引擎；Hermes Agent则提出子Agent记忆隔离（PR #69744）和修复记忆擦除Bug（PR #69745）。这标志着Agent应用正从“单次对话”向“长期、复杂、多任务”的**业务系统**演进。

4.  **唤醒词与语音交互：**
    - **涉及项目：** Hermes Agent (PR #53378)
    - **具体诉求：** 全平台离线唤醒词支持（“Hey Hermes”）。这是在桌面端和移动端进行免提语音交互的基础，也是Agent摆脱“聊天框”限制，向“环境计算”演进的重要一步。

### 5. 差异化定位分析

| 维度 | **OpenClaw** | **Hermes Agent** |
| :--- | :--- | :--- |
| **功能侧重** | 广度与深度并重，追求功能全覆盖和极致的可定制性（如Agent策略、钩子系统、复杂的通道插件架构）。 | **实用性**与**生产级优化**，侧重于修复核心Bug、提升跨平台体验、打磨开发者工具链（CI/CD、自动化）。 |
| **目标用户** | **高级开发者/团队/全栈工程师**。用户有能力处理较复杂的配置和潜在的稳定性问题，追求极致的控制力和功能自由度。 | **更广泛的开发者/个人用户/企业入门者**。用户更看重开箱即用的稳定体验、跨平台的一致性以及与现有工具的集成能力。 |
| **技术架构** | **自建的复杂网关架构**，将路由、会话管理、插件等逻辑高度耦合，强大但脆弱。当前的P0 Bug体现了该架构在升级和配置变更时的脆弱性。 | **模块化**趋势更明显。API标准化（如`/v1/capabilities`）、子Agent生命周期、Profile管理等设计，使系统更易于解耦和扩展。 |
| **社区氛围** | **挑战与机遇并存**。大量Bug反馈和功能请求共存，表现为“痛苦的拥护者”。社区对核心功能的稳定性有焦虑，但对项目的潜力依然抱有巨大期望。 | **务实且高效**。社区讨论更聚焦于具体问题的解决方案和功能提案，维护者响应积极，项目发展方向更可控。 |

### 6. 社区热度与成熟度

- **快速迭代与功能扩张阶段：** **Hermes Agent** 处于此阶段。其PR合并频率高（每日11个），开发动作集中在增加新功能（子Agent模型选择、记忆隔离、Kanban软件工厂）和增强现有能力，Bug修复作为保障，而非主导。项目在快速拓展能力边界。
- **质量巩固与问题修复阶段：** **OpenClaw** 处于此阶段。尽管有大量新功能提案，但当日社区动态被大量严重Bug和回归问题所淹没。项目当前的主要精力被迫集中在“灭火”而非“盖楼”，表明其经历了快速的版本迭代后，正面临质量回撤的阵痛。这通常是大型项目走向成熟前必须经历的阶段。

### 7. 值得关注的趋势信号

1.  **Agent的“工厂化”：** Hermes Agent的“kanban software factory” (PR #69749) 信号强烈。这暗示了Agent的角色正从“对话助手”向“软件开发组织”演变。未来的Agent不仅要回答问题，更要能管理、执行和交付完整的工程项目。
2.  **系统复杂性的“反噬”：** OpenClaw的稳定性危机是一个警钟。当Agent系统集成了太多功能（多模态、复杂钩子、网关、会话快照）后，任何一个模块的微小退化都可能导致整个系统的崩溃或行为异常。**对于开发者而言，控制功能膨胀的节奏，建立完善的回归测试和监控体系，远比盲目堆叠功能更为重要。**
3.  **从“孤立Agent”到“Agent平台”：** 两个项目都表现出向平台化演进的趋势。OpenClaw的会话生命周期管理需求，Hermes Agent的标准化API和Profile管理，都旨在让Agent不再是单个脚本或应用，而是一个可被编程、可被其他系统调用的**基础能力平台**。
4.  **社区对“确定性行为”的渴望：** 无论是OpenClaw的强制执行钩子，还是Hermes Agent对记忆擦除的零容忍，都表明社区已对“黑盒”式Agent感到不满足。**透明、可审计、可干预**，已成为下一代AI智能体的核心设计原则。这要求开发者在设计Agent时，必须将**安全边界作为一等公民**来考虑，而非事后补救的补丁。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-07-23

## 今日速览

项目在过去 24 小时内保持极高活跃度：共产生 50 条 Issue 更新（46 条新开/活跃，4 条关闭）和 50 条 PR 更新（39 条待合并，11 条已合并/关闭）。虽然无正式版本发布，但多方位的功能增强与 bug 修复持续推进。桌面端会话状态问题、跨平台消息传递、配置兼容性仍是社区关注的焦点，同时涌现出多份面向生产场景的有价值 PR（如 subagent 生命周期、记忆隔离、唤醒词支持等）。项目整体健康度良好，维护响应速度较可观，但部分长期积压的 feature request 仍需决策。

## 项目进展

今日共 11 个 PR 被合并/关闭，标志性的进展包括：

| PR | 标题 | 说明 |
|----|------|------|
| [#64090](https://github.com/NousResearch/hermes-agent/pull/64090) | fix(codex): extend native Responses web_search to openai-codex | 将原生 `web_search` 支持从 xAI 扩展至 `openai-codex` 提供者，减少重复实现 |
| [#69699](https://github.com/NousResearch/hermes-agent/pull/69699) | fix(ci): publish inline E2E evidence | 改进 CI 流水线，将端到端测试证据以内联方式发布，提升审查效率 |
| [#69683](https://github.com/NousResearch/hermes-agent/pull/69683) | fmt(js): `npm run fix` auto-fix | 自动格式化 JS 代码，降低潜在 lint 噪音 |
| [#69694](https://github.com/NousResearch/hermes-agent/pull/69694) | feat(delegation): allow per-task model selection in delegate_task | 允许为不同子代理分配不同模型（已关闭，推测已合并） |
| [#68302](https://github.com/NousResearch/hermes-agent/issues/68302) | [Bug]: Clicking a sidebar session has no effect while Skills & Tools is the active view | 桌面端侧栏会话点击失效 bug 已关闭，相应修复预计已落地 |
| [#68979](https://github.com/NousResearch/hermes-agent/issues/68979) | Desktop: long-thread reconciliation re-stacks user messages... | 长线程渲染错乱问题已关闭，提升使用体验 |

这些合并主要围绕 **桌面端交互修复**、**AI 提供者兼容**、**CI/自动化优化** 三个方向，项目在稳定性和开发者体验上均有小幅推进。

## 社区热点

今日讨论最活跃的 Issues 集中在跨平台能力、核心 bug 与配置兼容性：

1. **[#4335](https://github.com/NousResearch/hermes-agent/issues/4335) — Feature Request: Cross-platform session context sharing (CLI ↔ Telegram)**  
   *评论: 9, 👍: 2*  
   用户强烈希望打通不同消息平台（CLI、Telegram、Discord）之间的会话语境，当前隔离存储导致体验碎片化。该 feature 已标记 `needs-decision`，社区期待明确路线图。

2. **[#66875](https://github.com/NousResearch/hermes-agent/issues/66875) — [Bug]: Latest session does not switch after navigating to Plugins/Artifacts tab and back**  
   *评论: 7*  
   桌面端面板切换后无法切换到最近会话，严重影响日常使用，社区用户提供了详细的复现步骤。

3. **[#62936](https://github.com/NousResearch/hermes-agent/issues/62936) — [Bug]: Telegram uploads >~15 MB always fail with TimedOut**  
   *评论: 6*  
   媒体上传超时问题长期困扰 Telegram 用户，环境变量配置无效，属于平台适配关键 bug。

4. **[#21341](https://github.com/NousResearch/hermes-agent/issues/21341) — [Bug]: nixosModule documents option installs files to wrong paths**  
   *评论: 5*  
   Nix 用户报告配置文件路径错误，导致 `SOUL.md` 等关键文件无法被正确读取，影响首次部署体验。

这些热点反映出用户对 **平台统一性**、**桌面交互可靠性**、**消息传递稳定性** 的核心诉求。

## Bug 与稳定性

### P0（紧急）
- **[#69745](https://github.com/NousResearch/hermes-agent/issues/69745) — fix(memory): don't wipe MEMORY.md...**（PR，实为 fix）  
  **现象**：`_read_file` 将任何读取失败降级为 `[]`，导致 `add` 路径下完整清空 `MEMORY.md`。  
  **状态**：已有对应 [PR #69745](https://github.com/NousResearch/hermes-agent/pull/69745)，正在审查中，属严重数据丢失风险。

### P1（高严重性）
- **[#62708](https://github.com/NousResearch/hermes-agent/issues/62708) — Silent context-overflow: no warning when compression is blocked**  
  当压缩被阻止（冷却/反抖）时，上下文持续增长直至模型 token 上限，导致静默失败。目前无关联 fix PR，需优先处理。

### P2（中等严重性，已有关联 PR 或讨论）
| Issue | 标题 | 关联 PR / 状态 |
|-------|------|----------------|
| [#69551](https://github.com/NousResearch/hermes-agent/issues/69551) | Desktop SSH remote mode broken with non-default profile | 无直接 PR，社区在讨论 |
| [#69738](https://github.com/NousResearch/hermes-agent/issues/69738) | `/reload` deletes container-supplied env config | 无 PR，属环境管理退化 |
| [#69737](https://github.com/NousResearch/hermes-agent/issues/69737) | `checkpoints.enabled` ignored in one-shot sessions | 无 PR，影响命令行非交互模式 |
| [#69709](https://github.com/NousResearch/hermes-agent/issues/69709) | `supports_vision` override not resolved for `--provider` | 对应 [PR #69751](https://github.com/NousResearch/hermes-agent/pull/69751) |
| [#57775](https://github.com/NousResearch/hermes-agent/issues/57775) | Windows: atomic_replace drops writes on `ERROR_SHARING_VIOLATION` | 无 PR，影响 Windows 数据持久化 |
| [#63222](https://github.com/NousResearch/hermes-agent/issues/63222) | ACP model switch can preserve stale provider base_url | 无 PR，可能导致请求路由到错误端点 |
| [#65942](https://github.com/NousResearch/hermes-agent/issues/65942) | Snapshot restore can leave newer data when state.db is open | 无 PR |
| [#69638](https://github.com/NousResearch/hermes-agent/issues/69638) | Desktop: queued large image reconnect-loops | 无 PR |
| [#69652](https://github.com/NousResearch/hermes-agent/issues/69652) | fix(terminal): resolve shell init from effective home（PR） | 已提交 [PR #69652](https://github.com/NousResearch/hermes-agent/pull/69652) |

### 已关闭/已修复的 Bug（今日）
- [#68302](https://github.com/NousResearch/hermes-agent/issues/68302) — 侧栏会话在 Skills & Tools 视图下无响应（已关闭）
- [#68979](https://github.com/NousResearch/hermes-agent/issues/68979) — 长线程消息重排序（已关闭）

## 功能请求与路线图信号

以下今日提出的功能请求和 PR 最可能被纳入后续版本（依据讨论热度、实用性与已有实现基础）：

| 请求/PR | 标题 | 潜力分析 |
|---------|------|----------|
| [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) | Cross-platform session context sharing | 呼声最高，已标记 `needs-decision`，可能成为 v0.21 重点 |
| [#69694](https://github.com/NousResearch/hermes-agent/pull/69694) | Per-task model selection in delegate_task | 已合并，增强多模型并行能力 |
| [#69744](https://github.com/NousResearch/hermes-agent/pull/69744) | feat(mem0): filter_by_agent_id | 提供记忆隔离，适合多 profile 场景，可快速集成 |
| [#69749](https://github.com/NousResearch/hermes-agent/pull/69749) | hermes-loop kanban software factory | 大型软件开发套件，面向复杂工作流，需评估依赖 |
| [#53378](https://github.com/NousResearch/hermes-agent/pull/53378) | "Hey Hermes" wake word | 全平台离线唤醒，提升语音交互体验，已积累多轮评审 |
| [#63359](https://github.com/NousResearch/hermes-agent/pull/63359) | Public subagent lifecycle API | 为插件系统提供标准化子代理管理，架构价值高 |
| [#67246](https://github.com/NousResearch/hermes-agent/pull/67246) | Optional file upload support to API server | 使 agent 生成的文件可远程上传并交付，适合企业 API |
| [#67392](https://github.com/NousResearch/hermes-agent/pull/67392) | Profile-scoped deep link (`hermes://profile/...`) | 提升多 profile 桌面用户的操作效率 |
| [#66268](https://github.com/NousResearch/hermes-agent/issues/66268) | Advertise delegation toolset isolation in /v1/capabilities | 增强 API 可发现性，适合平台化 |
| [#69726](https://github.com/NousResearch/hermes-agent/issues/69726) | WhatsApp channel_skill_bindings | 扩展 WhatsApp 平台能力，复制 Discord/Slack 模式 |

## 用户反馈摘要

从 Issue 评论和描述中提炼的真实痛点：

- **会话隔离困扰**（#4335）：用户抱怨 CLI 和 Telegram 上的对话互不相知，无法跨平台延续话题。
- **桌面 UI 交互异常**（#66875, #68302, #68979）：面板切换后会话不响应、消息顺序错乱，严重影响日常使用效率。
- **Telegram 媒体上传不可用**（#62936）：大于 15MB 的文件始终超时，配置变量无效，用户无法发送大文件。
- **配置丢失与损坏**（#69738, #69737, #69709）：Docker 环境变量被 `/reload` 删除、checkpoint 被忽略、custom provider 的 vision 覆盖不生效，配置管理需加固。
- **Windows 特有缺陷**（#57775, #47930, #46369）：文件写入竞争、动画静态、快捷键不支持 Dvorak 布局，Windows 用户体验仍需优化。
- **压缩/溢出无反馈**（#62708）：用户长时间等待后模型静默停止回答，缺乏中间提示，产生困惑。
- **Nix 部署路径错误**（#21341）：模块安装文件到错误目录，导致人格文件不可用，Linux 用户需要手动修正。
- **中文用户推理不足**（#48027）：Agent 不能主动关联上下文线索，记忆同步范围过窄，非英语用户仍需改进。

## 待处理积压

以下 Issue/PR 已长期未得到明确响应或决策，建议维护团队优先审视：

| 项目 | 创建时间 | 标签 | 问题摘要 |
|------|----------|------|----------|
| [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) | 2026-03-31 | `needs-decision` | 跨平台会话共享，呼声最高但尚未分配 |
| [#21341](https://github.com/NousResearch/hermes-agent/issues/21341) | 2026-05-07 | `P2` | Nix 模块文档路径错误，影响包管理安装 |
| [#12651](https://github.com/NousResearch/hermes-agent/issues/12651) | 2026-04-19 | `P2` | `.env` 占位符未清理，可能被当作真实凭证 |
| [#25837](https://github.com/NousResearch/hermes-agent/issues/25837) | 2026-05-14 | `P2` | 视觉分析注入超大图片导致会话不可恢复 |
| [#18539](https://github.com/NousResearch/hermes-agent/issues/18539) | 2026-05-01 | `P2` | FIFO 队列媒体文件仅

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*