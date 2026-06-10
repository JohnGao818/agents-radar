# OpenClaw 生态日报 2026-06-10

> Issues: 443 | PRs: 483 | 覆盖项目: 2 个 | 生成时间: 2026-06-10 02:58 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，现根据您提供的 OpenClaw (github.com/openclaw/openclaw) 数据，为您呈上 2026年6月10日的项目动态日报。

---

### **OpenClaw 项目日报：2026-06-10**

#### **1. 今日速览**

OpenClaw 项目今日呈现 **极高的社区活跃度**，24小时内产生超过 440 条 Issue 和 480 条 PR 更新，显示出开发者和用户群体的深度参与。项目发布了两个新版本，重点关注了消息通道的安全性与兼容性。然而，社区热点和 Bug 报告高度集中在 **会话状态混乱、消息丢失/泄露** 以及 **多通道兼容性问题** 上，表明这些是当前最亟待解决的稳定性短板。开发团队通过大量的修复 PR (如 #91801, #91810) 快速响应，项目整体保持着高强度的迭代推进态势。

#### **2. 版本发布**

项目今日发布了两个新版本，内容基本相同，以下为详细说明：

- **最新版本**: `openclaw 2026.6.5` 与候选版 `openclaw 2026.6.5-beta.6`
- **主要更新亮点**:
    1.  **QQBot 消息净化**: 修复了 QQ 机器人消息通道中，模型内部思考过程 (`<thinking>`) 被泄露到群聊回复中的安全问题。现在，这些封装内容在原生发送前会被自动剥离。 (相关 Issue: #89913, #90132)
    2.  **MCP 工具结果处理增强**: 增强了 MCP (Model Context Protocol) 工具结果的兼容性处理，会对 `resource_link`、`resource`、`audio` 以及格式错误的图片等结果进行强制性格式统一，提升数据处理的鲁棒性。
- **破坏性变更**: 无明确说明。
- **迁移注意事项**: 建议所有使用 QQBot 通道的用户升级，以修复消息泄露的安全隐患。使用 MCP 工具的开发者应关注其返回结果格式的变化。

---

#### **3. 项目进展**

过去24小时内，有不少关键 PR 被合并或关闭，推动了项目核心功能的完善：

- **会话稳定性和恢复**:
    - PR #91801: 修复了当嵌入式回复运行异常中止并清空后，诊断会话仍显示有排队的“卡住”状态问题，提升了会话恢复的准确性。
    - PR #91590: 修复了 Codex 会话的上下文引擎压缩所有权问题，确保在特定场景下不会发生压缩冲突。
- **用户体验与 UI/UX**:
    - PR #91810: 修复了 WebChat 在处理“延迟思考”模式时，无法正确重载完整历史记录并展示思考过程的问题。
    - PR #91557: 大幅改进了 iPad 和 iPhone 的控制界面，引入了侧边栏导航、专属页面等功能，显著提升了移动端的操作体验。
- **通道兼容性加固**:
    - PR #91783: 对 iMessage 的发送通道进行了加固，引入了 `sendTransport` 配置选项，解决特定场景下消息发送失败的问题。
    - PR #91811: 修复了单次运行的定时任务因心跳机制被禁用而无法正常触发的问题，确保任务能被正确执行。

---

#### **4. 社区热点**

今日社区讨论焦点集中在几个长期存在的会话与消息处理问题上：

- **#25592 `[OPEN] Text between tool calls leaks to messaging channels`** (评论: 29)
    - **链接**: [Issue #25592](https://github.com/openclaw/openclaw/issues/25592)
    - **分析**: 这是社区讨论最热烈的问题。用户反映，当 Agent 在调用工具的间隙产生文本（如错误处理、中间思考）时，这些本不应出现的内部处理信息会被直接发送到聊天通道，造成严重的文本泄露和糟糕的 UI 体验。该 Issue 被标记为 **P1 优先级** 和 **安全影响**，是当前社区最为关切的痛点之一。

- **#90083 `[CLOSED] [Bug]: OpenAI ChatGPT Responses transport fails`** (评论: 16)
    - **链接**: [Issue #90083](https://github.com/openclaw/openclaw/issues/90083)
    - **分析**: 一个短时间内被解决（CLOSED）的高热度问题，涉及升级后 gpt-5.4/5.5 模型推理失败。用户报告了 `invalid_provider_content_type` 错误。该 Issue 的快速关闭表明团队对重大兼容性问题有快速的应急响应机制。

- **#32296 `[OPEN] [Bug]: Agent replies to previous message instead of current message`** (评论: 15)
    - **链接**: [Issue #32296](https://github.com/openclaw/openclaw/issues/32296)
    - **分析**: 这是一个非常关键的“会话状态混乱”问题。用户表达了对 Agent “答非所问”的强烈不满。该问题导致对话错位，严重影响了基础的用户交互体验。它被标记为 **P1 优先级**，是开发团队必须攻克的难关。

---

#### **5. Bug 与稳定性**

今日报告的 Bug 主要集中在会话状态、消息传递和模型兼容性上，按严重程度排列如下：

- **P1 (Critical)**
    - **[Bug]: Agent replies to previous message instead of current message (session context confusion) (#32296)**: 会话上下文混乱，代理回复错误信息。**无关联修复 PR**。
    - **[Bug]: [Regression] Codex app-server turn-completion stall returns (#88312)**: 回归性 Bug，导致 Codex 服务器端无法完成交互轮次。**无关联修复 PR**。
    - **[Bug]: Discord run fails with EmbeddedAttemptSessionTakeoverError (#86508)**: Discord 通道运行失败，报会话文件被接管的错误。**无关联修复 PR**。
    - **[Bug]: Active Memory + Codex app-server path causes long response latency (#86996)**: 结合特定插件和模型后导致响应延迟、钩子超时等问题。**无关联修复 PR**。

- **P2 (Major)**
    - **[Bug]: Spurious "Something went wrong" failures in large Telegram direct sessions (#87299)**: 在大型 Telegram 直接会话中出现无故故障。
    - **[Bug]: gateway heap grows unbounded over time, gets killed by cgroup OOM (#89315)**: 长时间运行后，Gateway 进程内存泄漏并因 OOM 被系统杀死。
    - **其他**: 包括 XDG_CONFIG_HOME 变量未处理 (#53628)、Feishu 卡片消息渲染回归 (#53486)、备份超时导致磁盘写满 (#50442) 等。

---

#### **6. 功能请求与路线图信号**

以下用户提出的功能请求反映了社区对 Agent 可控性和易用性的更高期待：

- **#52640: Feature request: Persistent task-status surface**：用户希望在长时间运行的频道对话中，除了当前的花样更新外，能有一个**持久的、权威的任务状态视图**，以清晰地了解后台仍在进行的工作。
- **#42840: Feature Request: Add MathJax/LaTeX Support to Control UI**：用户希望 OpenClaw 的控制界面能原生支持数学公式/LaTeX 的渲染，以期更高效地交流和展示科学内容。该请求获得 6 个 👍，反映了对专业领域支持的需求。
- **#53638: Feature: per-channel / per-group / per-DM model override**：用户希望能在配置中**为不同频道、群组或私聊设定不同的模型**，以实现更灵活的模型管理与成本控制。

**路线图信号**：今日提交的 PR `#91807` 为 `image generate` 命令新增了 `--file` 支持（针对 Issue #91734），表明团队正在逐步补齐 CLI 工具的功能；PR `#91438` 为语音通话功能增加了 Microsoft Teams 提供商，显示了项目在扩展企业级通道上的持续投入。

---

#### **7. 用户反馈摘要**

从 Issues 评论中提炼的用户真实反馈：

- **痛点**:
    - “答非所问”是头号痛点，用户 (`survivor998`) 明确描述了“Agent 回复的是上一条消息”的场景，认为这造成了“对话错位”。
    - “内部逻辑泄露”令用户困扰，`doomclaw` 指出 Agent 在工具调用间的文本泄露到聊天频道是“严重的 UI 问题”。
    - “一键多言”或“无限循环”降低了 Agent 的可用性。用户 `51Google` 描述了 Agent 因工具调用失败而陷入无限重试循环并疯狂刷屏的情况。
- **使用场景**:
    - 用户 (`iravikiran`) 尝试在 RISC-V64 架构上运行 OpenClaw 受阻，反映了社区对跨平台支持的需求。
    - 用户 (`JakeBiggs`, `fionn77`) 报告了在 Windows 系统和启用特定插件 (Active Memory) 时遇到的性能瓶颈和死锁问题，展示了不同环境下的兼容性挑战。
- **满意点**:
    - 从 Issue #90083 的快速关闭可以看出，用户对项目团队处理关键兼容性问题的速度和效率感到认可 (获 3 个 👍)。

---

#### **8. 待处理积压**

以下 Issue 和 PR 因长时间未取得进展或处于等待状态，需引起维护者关注：

- **长期未响应的重要 Issue**:
    - **[OPEN] #54253**: [Bug]: OpenClaw returns "run Error : LLM Request Failed" on RISC-V64 System. (创建于 2026-03-25，已有 13 条评论，P2 优先级)
    - **[OPEN] #31331**: [Bug]: Docker Install + Sandbox can't workspaceAccess at all. (创建于 2026-03-02，已有 9 条评论，P1 优先级，安全影响)
- **长期待审核的 PR**:
    - **[OPEN] #55851**: feat: include provider/model/profile/trigger context in overloaded and rate limit error messages. (创建于 2026-03-27，状态为 `⏳ waiting on author`)
    - **[OPEN] #79982**: feat(tools): introduce group:core for all built-in core tools. (创建于 2026-05-09，状态为 `⏳ waiting on author`)

---

## 横向生态对比

好的，作为AI智能体与个人AI助手开源生态的资深技术分析师，现基于您提供的OpenClaw与Hermes Agent两份项目日报，为您呈上2026年6月10日的横向对比分析报告。

---

## AI智能体与个人AI助手开源生态横向对比分析报告 (2026-06-10)

### 1. 生态全景

当前，个人AI助手与自主智能体开源生态呈现 **“繁荣但焦虑”** 的态势。一方面，以OpenClaw和Hermes Agent为代表的头部项目社区贡献极度活跃，开发者正以前所未有的速度向项目中注入新功能、新技能（Skills）和第三方集成。另一方面，这种高速增长带来了显著的质量与稳定性挑战。近期的社区焦点已从“实现功能”转向 **“治理复杂性”** ：如何解决会话状态混乱、多平台消息泄露、跨平台体验割裂、以及核心任务流中断等“软件工程硬骨头”。这表明该生态正从“原型探索期”过渡到“可用性巩固期”与“规模化部署期”的交汇点。

### 2. 各项目活跃度对比

| 指标维度 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **今日Issues (新增/总数)** | 440+ (极高) | 50 (高) |
| **今日PRs (新增/总数)** | 480+ (极高) | 50 (高) |
| **今日版本发布** | ✅ `2026.6.5` & `2026.6.5-beta.6` | ❌ 无 |
| **核心PR合并率** | 较高 (多数重要PR在当日闭合) | **极低 (6%, 3/50)** |
| **社区焦点集中度** | **“会话/消息通道混乱”** (P1级) | **“桌面端/TUI体验”** (平台特定) |
| **健康度评估** | **高活跃，但稳定性承压** | **高活跃，但审查瓶颈严重** |

**分析**：OpenClaw在社区规模、合并效率与发布节奏上均远超Hermes Agent，处于生态领导者地位。但其P1级Bug的频发和社区热议，也暴露了大项目在快速迭代中的稳定性管理难点。Hermes Agent则面临典型的“社区增长而维护未跟上”的困境，大量高质量的PR（如新技能、平台优化）等待合并，可能削弱贡献者热情。

### 3. OpenClaw 在生态中的定位

- **核心优势**：**全平台、全模态的“通用智能体中间件”**。其技术路线侧重于构建一个统一的、有状态的会话核心，并以强大的消息通道抽象层接入QQ、iMessage、Discord、Telegram等近20个平台。其UI（WebChat，Control UI）拥有深度的“思考过程展示”和CLI工具，适合开发者和重度用户进行精细控制。
- **技术路线差异**：与Hermes Agent相比，OpenClaw更强调 **“统一会话状态管理”**和 **“跨通道消息格式标准化”** （如剥离思维链、标准化MCP结果）。这在带来强大能力的同时，也引入了会话混乱、消息泄露等复杂的分布式系统问题。
- **社区规模对比**：OpenClaw的日活跃度（单日440+ Issues）是Hermes Agent（50 Issues）的8-10倍。这表明其用户基础与开发者网络非常庞大，是生态的绝对中心。Hermes Agent更像是一个专注于特定开发者群体（特别是桌面用户和技能开发者）的精品项目。

### 4. 共同关注的技术方向

以下需求在两个项目社区中均有体现，揭示了行业共同痛点：

1.  **会话状态一致性与可靠性**（OpenClaw `#32296`， Hermes Agent `#43216`）：
    - **具体诉求**：Agent回复错位、会话卡死、任务状态混乱、操作步骤烦琐。这是当前智能体规模化应用的最大拦路虎。
    - **涉及项目**: 两者均有此类P1级Bug报告，说明这是整个生态的普遍问题。

2.  **模型调用失败处理与优雅降级**（OpenClaw `#90083`, Hermes Agent `#43211`）：
    - **具体诉求**：模型升级后接口不兼容、流式响应超时后无法触发fallback、重试策略僵化。社区需要更智能、可配置的错误处理与容错机制。
    - **涉及项目**: 两者均报告了因模型兼容性或调用失败导致的任务中断，是“可靠性”问题的另一侧影。

3.  **跨平台门户（Portal）集成的深度与稳定性**（OpenClaw QQBot/iMessage/Feishu Bugs, Hermes Agent Telegram Matrix Desktop）：
    - **具体诉求**：消息泄露、特定平台（如QQ、Telegram）的卡片/UI渲染回归、iOS/Android移动端体验提升、企业级平台（Teams, Feishu）支持。
    - **涉及项目**: 两者都在积极扩展和修复其消息通道，但稳定性和兼容性仍是主要挑战。

### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **功能侧重** | **统一的、有状态的对话引擎** + **广泛的通道连接**。强于会话管理和多平台接入。 | **“个人电脑上的智能体操作系统”**。强于桌面GUI体验、TUI网关、技能生态、Kanban工作流管理。 |
| **目标用户** | 社区运营者、企业开发者、多平台部署者。追求统一入口和规模化。 | **个人开发者、技术爱好者、桌面用户**。追求控制权、自定义工作流和精致的个人使用体验。 |
| **技术架构关键差异** | 强会话状态与事件驱动架构，强调状态持久化与恢复。 | 更倾向于 **“桌面原生”** 架构，与操作系统文件系统、进程管理深度集成，强调本地模型友好性和实时响应。 |
| **社区生态特征** | **大而全的“平台生态”**。贡献集中在核心框架、通道适配和稳定性修复。 | **小而美的“工具体现”**。社区贡献大量聚焦于新技能、新插件和平台集成，但核心框架审查门槛高。 |

### 6. 社区热度与成熟度

- **快速迭代阶段**：**OpenClaw**。其版本发布频繁、功能迭代迅速（今日发布两个版本），但伴随大量Bug修复和回归测试，处于“在高速路上边跑边修车”的阶段。
- **质量巩固/拓展阶段**：**Hermes Agent**。其核心功能（如Kanban、Desktop）相对成熟，但社区大量新功能的PR积压表明，项目正努力在核心稳定的基础上，吸收社区贡献以快速拓展技能和平台生态。审查瓶颈是其主要矛盾。

### 7. 值得关注的趋势信号

1.  **“会话状态”是当前最大的技术债**：OpenClaw `#32296`和Hermes Agent `#43216`共同指向 **“Agent不知当下”** 这一核心问题。这表明简单的上下文窗口已无法满足复杂多轮任务。未来，**显式的状态机、任务队列、以及可中断/恢复的工作流**将被视为Agent的必备特性。

2.  **“企业级/严肃使用”需求涌现**：OpenClaw新增Microsoft Teams支持、Feishu (飞书)的Bug修复，以及Hermes Agent用户提出的 **“持久任务状态视图”** (`#52640`) 和 **“命令描述重写/本地化”** (`#13107`)，都标志着智能体正从“个人玩具”走向“企业生产力工具”。

3.  **用户开始要求“更精细的控制权”**：从OpenClaw的 **“按频道分配不同模型”** (`#53638`)、Hermes Agent的 **“逐个工具启用/禁用”** (`#31375`)，到双方社区共有的 **“更灵活的权限/审批策略”** 呼声，用户已不满足于全自动，而是希望像配置操作系统一样精细化地管理Agent的行为边界。

4.  **本地模型与自托管生态持续壮大**：Hermes Agent社区的Ollama静默模式、对RISC-V架构的尝试、以及OpenClaw社区对Termux/PRoot环境的支持呼声，都表明 **“离线优先”和“隐私优先”** 的用户群体在增长，这对项目架构提出了跨平台和运行时效率的更高要求。

**对AI智能体开发者的参考价值**：
- **近期投入重点**：应优先解决 **会话状态管理** 和 **多平台消息处理的可靠性**，这是用户体验的基石。
- **中期规划方向**：设计灵活的 **模型/Provider路由策略** 和 **细粒度的权限/命令控制系统**，以匹配企业级和专业用户的需求。
- **长期生态布局**：关注 **本地模型（Ollama）** 和 **非x86架构** 的兼容性，并建立高效的社区贡献审核与合并机制，避免因审查瓶颈导致社区热情冷却。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的Hermes Agent项目数据，为您生成一份结构清晰、数据驱动的项目动态日报。

---

### Hermes Agent 项目动态日报 | 2026年6月10日

**分析师点评：** 今日项目社区异常活跃，Issue与PR提交数均达到50条，但合并率极低（3/50），表明维护者审查能力与社区贡献速度之间存在显著差距。社区焦点分散在体验优化、UI/UX错误、平台功能请求（尤其是Telegram与Desktop）及大量新技能（Skills）的批量提交上。虽然未发布新版本，但多个P2级别的Bug修复PR与功能增强PR正在积极迭代中。

---

### 1. 今日速览

- **社区高度活跃但审查瓶颈明显**：过去24小时内，社区提交了50个Issue与50个PR，但仅有2个Issue和3个PR被处理（关闭或合并），合并率仅为6%。这表明项目正经历“贡献洪峰”，维护团队响应压力巨大。
- **桌面端(Desktop)与TUI是问题高发区**：大量Bug报告集中在Desktop应用（会话刷新、文件浏览器、内存崩溃）和TUI网关上（令牌计数器不显示、用户消息被裁剪），用户体验问题亟待修复。
- **新技能(Skills)批量涌入**：多位贡献者提交了共计15个新技能的PR（如Linear、Spotify、1Password、AgentMail等），显示社区正积极丰富Hermes Agent的能力生态。
- **核心稳定性与基础设施问题浮现**：报告了如macOS桌面崩溃、Kanban看板意外复活归档看板、流式响应过期失效后不触发fallback等影响核心稳定性的P2级Bug。
- **功能请求聚焦细节与本地化**：社区提出的Feature Request趋向于精细化控制，如支持命令描述重写、逐个工具启用/禁用、Telegram菜单配置、本地提供者(Local Provider)配置优化等。

### 3. 项目进展（今日合并/关闭的重要PR）

尽管总量不多，但今日被合并/关闭的3个PR中，有一个关键的P1安全修复，显示了项目组对关键问题的快速响应。

- **`#43223` [P1] fix(cron): don't strict-scan script-injected output in no-skills jobs**
  - **状态**: 已关闭 (Merged)
  - **意义**: 修复了一个潜在的安全问题。在无技能（no-skills）模式的Cron任务中，脚本注入的输出数据可能被“严格扫描”模式误判，导致误封或报错。此PR修复了该问题，提升了Cron作业的稳定性和安全性。
  - **链接**: `NousResearch/hermes-agent PR #43223`

- **`#40377` [P3] fix(update): support Termux/PRoot environments**
  - **状态**: 开放中但被标记为重要修复
  - **推进方向**: 尽管未合并，该PR为在Termux/PRoot（如Android终端）等非标准环境下运行`hermes update`提供了必要支持（如自动设置`UV_LINK_MODE=copy`）。这拓宽了Hermes Agent的运行场景。
  - **链接**: `NousResearch/hermes-agent PR #40377`

### 4. 社区热点（今日讨论最活跃的Issues）

以下议题因触及用户广泛痛点或涉及社区共同关注的功能，获得了最多评论。

1. **[#13107] Feature: support command description override via config.yaml** (4 评论)
   - **诉求分析**: 用户希望能在`config.yaml`中重写命令的描述，以便在使用Telegram或Discord等平台时，为不同语言/场景的用户展示本地化或自定义的命令提示。这是对多语言支持和自定义性的直接需求。
   - **链接**: `NousResearch/hermes-agent Issue #13107`

2. **[#29331] feat: add Volcengine as built-in provider** (3 评论)
   - **诉求分析**: 用户请求将字节跳动的火山引擎（Volcengine）作为内置模型提供商。火山引擎已有官方集成文档，社区希望免除手动配置的麻烦。此需求呼应了中国区开发者对国内主流云服务商原生支持的需求。
   - **链接**: `NousResearch/hermes-agent Issue #29331`

3. **[#42086] fix(vision): support gemini-2.5 and gemini-2.0 in _supports_media_in_tool_results** (3 评论)
   - **诉求分析**: 一个看似微小的Bug，但反映了社区对前沿模型（Gemini 2.0/2.5）的快速跟进需求。现有代码硬编码了模型名称，导致新模型无法使用视觉工具结果，限制了新模型的能力发挥。
   - **链接**: `NousResearch/hermes-agent Issue #42086`

### 5. Bug 与稳定性

今日报告了多个影响体验和稳定性的Bug，按严重程度排列如下：

| 严重程度 | Issue # | 标题 (摘要) | 是否有Fix PR | 链接 |
| :--- | :--- | :--- | :--- | :--- |
| **P1** | `#43242` | Desktop app crash on macOS 26.5.1: Fatal process out of memory | **否** | [Issue Link](NousResearch/hermes-agent Issue #43242) |
| **P2** | `#43211` | Stale stream errors silently retry on same provider instead of triggering runtime fallback | **否** | [Issue Link](NousResearch/hermes-agent Issue #43211) |
| **P2** | `#43196` | Dashboard wedges (SIGKILL required) when hosted as a persistent service | **否** | [Issue Link](NousResearch/hermes-agent Issue #43196) |
| **P3** | `#42962` | Desktop active session does not refresh after same session is updated from Telegram | **是** (PR #43050) | [Issue Link](NousResearch/hermes-agent Issue #42962) |
| **P3** | `#43042` | Desktop file browser ENOENT: session.info CWD overwrite ignores local filesystem | **否** | [Issue Link](NousResearch/hermes-agent Issue #43042) |

**重点关注问题分析：**
- **macOS桌面内存崩溃 (#43242)**：这是一个严重的问题，直接导致应用无法启动，影响所有macOS 26.5.1用户。目前尚无已知的Fix PR。
- **流式响应Fallback失效 (#43211)**：当模型流式响应超时后，系统在一段时间内仍会重试同一失败的provider，而非按预期触发运行时fallback。这是一个影响系统可靠性的设计缺陷。

### 6. 功能请求与路线图信号

结合用户的新功能请求与已有的PR，可以初步判断项目的未来演进方向。

- **精细化配置与控制**：`#13107` (命令描述重写)、`#31375` (逐工具启用/禁用) 和 `#43052` (本地provider环境变量) 表明用户越来越希望获得更细粒度的配置能力。
- **平台集成深化**：`#43162` (Telegram菜单可配置) 和 `#7507` (Matrix引用回复配置) 的PR表明社区正积极完善对主流消息平台的适配。
- **插件与机器学习管道增强**：`#43241` (transform_api_request 钩子) 和 `#36765` (上下文选择/路由作为First-Class引擎) 的提出，预示着社区希望将数据流控制权更多地交给开发者，并推动更智能的上下文管理方案。考虑到已有相关PR，`transform_api_request` 钩子功能很有可能被纳入下一个版本。
- **本地模型与自托管友好性**：`#43028` (Ollama静默模式) 和 `#43052` (本地provider overlay) 的需求，反映出本地模型用户群体的声音正在变大，要求更好的使用体验和配置便捷性。

### 7. 用户反馈摘要

从今日的Issue评论中，可以提炼出用户使用Hermes Agent时的真实场景与痛点：

- **痛点：远程与桌面体验割裂**
  - Telegram用户在桌面查看网关会话时，令牌消耗统计显示为`0/1.0M` (`#42989`)，会话状态不同步 (`#42962`)。用户抱怨Desktop在远程场景下更像一个“只读的文本回放器”，缺乏实时数据同步。
  - 《“底部上下文占用统计始终显示为 `0/1.0M-0%` ... Desktop的会话查看器没有从gateway拉取usage stats的接口”》——`#42989`

- **痛点：权限控制过于严格且不灵活**
  - 即使在YOLO模式下，用户仍需为`execute_code`工具授权 (`#42921`)，全局命令允许列表不支持Shell Glob模式 (`#43051`)。用户抱怨这破坏了自动化工作流。
  - 《“Even when running in YOLO mode... The `execute_code` tool still triggers an approval prompt...”》——`#42921`

- **痛点：Kanban流程体验不佳**
  - Kanban看板在被询问后“阻塞”时，用户需要8步以上才能回复并“解封”任务 (`#43216`)。这表明当前看板流程在处理人机交互时效率低下。
  - 《“When a kanban worker blocks and asks a question, the current dashboard flow requires 8+ steps...”》——`#43216`

- **满意点：模型与工具的扩展能力**
  - 多个为Gemini 2.x模型修复Bug的Issue (`#42086`)、请求Volcengine集成的Issue (`#29331`) 以及大量新技能的PR (`#43166`)，表明用户对Hermes Agent的可扩展性持积极态度，并乐于在社区中贡献，以支持更多样的AI模型和应用场景。

### 8. 待处理积压

以下为长时间未更新但有代表性或对项目健康度重要的旧Issue，提醒维护团队关注。

1. **[`#7507`] [P2] feat(matrix): add configurable reply quoting for group chats** (2 评论, 创建于 2026-04-11)
   - **状态**: 搁置近2个月，已标记为P2。
   - **影响**: 对于Matrix用户这是一个重要的可用性问题，悬而未决可能影响该平台用户的留存。
   - **链接**: `NousResearch/hermes-agent Issue #7507`

2. **[`#20307`] [P3] [Feature]: Add plugin hook for ephemeral API-message transformation (transform_api_message)** (1 评论, 创建于 2026-05-05)
   - **状态**: 创建已超过一个月，虽然有深入讨论，但无实质进展。今日有功能相似的 `transform_api_request` PR (`#43241`) 提交，可能会推动此需求的解决。
   - **影响**: 此功能对插件生态的构建至关重要，能极大扩展灵活性。
   - **链接**: `NousResearch/hermes-agent Issue #20307`

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*