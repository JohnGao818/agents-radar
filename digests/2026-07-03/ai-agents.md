# OpenClaw 生态日报 2026-07-03

> Issues: 196 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-07-03 02:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为您生成的 OpenClaw 项目日报。

---

# OpenClaw 项目动态日报 | 2026-07-03

## 今日速览

今日 OpenClaw 项目维持高度活跃状态，共产生 196 条 Issue 更新和 500 条 PR 更新。虽然待合并 PR 数量庞大（425），但项目仍发布了 `v2026.7.1-beta.1` 小版本，引入了对 OpenAI GPT-5.6 模型族的支持。然而，社区讨论焦点主要集中在多个影响消息传递的 P1 级 Bug 上，尤其是“工具间文本泄漏”和“Codex 应用服务器卡死回归”等问题，引发了大量讨论。项目整体处于“新功能开发与稳定性修复并行”的健康但高压状态。

## 版本发布

### v2026.7.1-beta.1: openclaw 2026.7.1-beta.1

-   **发布日期**: 2026-07-03
-   **主要更新**:
    -   **OpenAI GPT-5.6 支持**: OpenClaw 现在可在目录、能力和运行时选择路径中识别和使用 GPT-5.6 模型家族。 (#98333) 感谢贡献者 @steipete-oai。
    -   **外部工具挂载**: 引入了 `openclaw attach` 命令，允许用户在现有 Gateway 会话上启动一个外部工具（harness）。
    -   **破坏性变更**: 发布说明未提及破坏性变更。
    -   **迁移注意事项**: 未提及特殊迁移步骤，建议用户升级前备份配置文件。

## 项目进展

尽管合并/关闭 PR 数量（75）远低于待合并数量，但团队依然取得了一些关键进展，主要集中在安全性、兼容性和核心稳定性上：

-   **安全与边界修复**:
    -   **PR #99024**: 修复了控制界面 CSP 策略，将 `connect-src` 从宽松的 `ws:`/`wss:` 收紧为明确的 WebSocket 端点，降低了数据泄露风险。该 PR 今日已被合并。
    -   **PR #96691**: 修复了浏览器插件 SSRF 运行时的导入路径问题，解决了因路径错误导致的懒加载失败。该 PR 今日已被合并。
-   **兼容性与环境适配**:
    -   **PR #96894**: 新增了对 Cloudflare Sandbox (Cloudchamber) 容器环境的自动检测，提升了在不同云环境下的兼容性。该 PR 今日已被合并。
-   **新功能探索**:
    -   **PR #98791**: 为 Signal 频道添加了状态反应功能，使 Signal 用户能够像在其他频道一样看到消息的“已收到、处理中、完成”等状态提示（需维护者跟进）。

## 社区热点

今日社区讨论高度集中，多个涉及消息丢失和会话状态的 P1 级 Bug 引发热议。

1.  **#25592: [P1] Text between tool calls leaks to messaging channels**
    -   **热度**: 33 条评论
    -   **链接**: [Issue #25592](https://github.com/openclaw/openclaw/issues/25592)
    -   **分析**: 这是今日最受关注的问题。用户和开发者强烈讨论了 Agent 在工具调用间隙生成的内部处理文本（如错误处理、叙述）被错误地路由并显示在最终消息渠道（如 Slack、iMessage）的严重 UX 问题。这被视为影响消息安全性和清晰度的核心缺陷。

2.  **#88312: [P1] [Bug]: [Regression] 2026.5.27: Codex app-server turn-completion stall returns**
    -   **热度**: 19 条评论
    -   **链接**: [Issue #88312](https://github.com/openclaw/openclaw/issues/88312)
    -   **分析**: 用户报告 Codex 应用服务器（ChatGPT Plus 子模块）中一个已修复的“卡死”问题在 2026.5.27 版本中再次回归。该回归严重影响了依赖 Codex 运行时的用户，社区对此表达了强烈不满和担忧，希望团队优先处理。

3.  **#92201: [P1] Embedded runner: freshly streamed thinking signatures intermittently invalid on replay (Anthropic)**
    -   **热度**: 18 条评论
    -   **链接**: [Issue #92201](https://github.com/openclaw/openclaw/issues/92201)
    -   **分析**: 该问题讨论了在 Slack 插件等嵌入式运行器中，Anthropic 模型的新流式思考签名在重放时间歇性无效，导致恢复包装器无法触发的复杂场景。该问题涉及多线程和状态管理，技术难度高，社区在深入探讨根因。

## Bug 与稳定性

今日报告的 Bug 中，消息传递和会话状态的可靠性问题最为突出。

-   **严重**:
    -   **#25592**: 工具间文本泄漏（见社区热点）。无修复 PR。
    -   **#88312**: Codex 应用服务器卡死回归（见社区热点）。无修复 PR。
    -   **#92201**: Anthropic 思考签名重放失败（见社区热点）。无修复 PR。
    -   **#73148**: 图像工具在缺少 `sharp` 模块时给出模糊错误提示。无修复 PR。
    -   **#38327**: Google Vertex/Gemini 模型因 `null` 对象导致崩溃。无修复 PR。
-   **中/高**:
    -   **#87744**: Codex 驱动的 Telegram 会话超时问题。无修复 PR。
    -   **#75593**: 子 Agent 列表在创建后仍为空。无修复 PR。
    -   **#98416**: 发布版 `v2026.6.11` 缺失重入锁，导致回复会话初始化冲突。无修复 PR。
    -   **#72015**: `active-memory` 插件导致多 Agent 网关过载。无修复 PR。
-   **低/稳定性**:
    -   **#97983**: iOS/WebChat 消息发送后不触发回复。
    -   **#99253**: AI 助手虚构用户输入并回应，安全性问题严重。无修复 PR。
    -   **#99168**: 大型工具输出导致后续结果显示异常。该 Bug 已关闭，可能已修复。

**总结**: 今日涌现大量 P1 级 Bug，其中多个与消息传递和 Codex 集成相关，严重影响核心使用体验，社区反馈非常强烈。

## 功能请求与路线图信号

尽管 Bug 较多，社区对新功能的探索并未停止。

-   **PR #89569**: `feat(channels): add pre-auth access requests and grouped DM allowlists`。这是一个大型 PR，为 Telegram 和 WhatsApp 增加了访问请求和 DM 白名单功能，可能成为下一版本中频道安全性的重要增强。
-   **PR #98236**: `refactor: flip sessions and transcripts to sqlite storage`。这是一个非常大的重构 PR，意图将核心的会话和转存存储从 JSON 文件迁移到 SQLite。该 PR 被标记为“不要合并”，属于长期规划中的基础设施改进，表明团队正为未来的性能和可扩展性做准备。
-   **Issue #35203**: `[RFC] Multi-Agent Collaboration Enhancement`。这是一个详细的多 Agent 协作增强提案，涵盖能力分析、共享黑板等高级功能。虽然目前评论不多，但它标志着社区对未来 Agent 主导协作范式的期待。

## 用户反馈摘要

-   **核心痛点**: 用户对回归 Bug 感到沮丧，尤其是那些已经修复过的问题再度出现（如 #88312）。这损害了用户对版本稳定性的信心。
-   **UX 问题**: “工具间文本泄漏”（#25592）是一个明显的 UX 设计缺陷，用户期望 Agent 仅展示最终结果，而非其内部处理过程。
-   **透明度需求**: 用户希望错误提示更加清晰。例如，缺少依赖时（#73148）或配置错误时（#38327），用户需要明确的指引，而非晦涩的通用错误。
-   **功能期待**: 对于涉及未来架构的讨论（如 SQLite 迁移 #98236 和多 Agent 协作 #35203），用户（尤其在评论较少的初期阶段）似乎更多地是在观望和期待，而非直接参与激烈讨论。

## 待处理积压

以下为长期未响应或积压的重要 Issue/PR，提醒维护者关注：

1.  **Issue #32530**: 关于“自动发现外部工作区 Agent 配置”的功能请求，自 2026-03-03 创建以来，标签为 `needs-maintainer-review`，至今已超过 4 个月，无实质性进展。
    -   链接: [Issue #32530](https://github.com/openclaw/openclaw/issues/32530)
2.  **Issue #11623**: 关于“macOS 浮动的 Agent 气泡”功能请求，自 2026-02-08 创建，需维护者决策。
    -   链接: [Issue #11623](https://github.com/openclaw/openclaw/issues/11623)
3.  **PR #90152**: 一个老旧的 PR（2026-06-04 创建），旨在为 Telegram 添加延迟调度测试场景，但已被标记为 `needs proof` 且状态为未合并。急需维护者或贡献者更新证明并推动此 PR。
    -   链接: [PR #90152](https://github.com/openclaw/openclaw/pull/90152)

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，以下是我基于您提供的 OpenClaw 和 Hermes Agent 两份项目日报生成的横向对比分析报告。

---

## AI 智能体开源生态横向对比分析报告 | 2026-07-03

### 1. 生态全景

截至2026年7月3日，个人 AI 助手/自主智能体开源生态整体呈现出 **“新功能快速迭代”与“核心稳定性承压”并存的动态平衡**。头部项目如 OpenClaw 和 Hermes Agent 普遍处于高压开发状态，大量新特性（如多 Agent 协作、新模型支持、平台集成）与回归性 Bug、消息泄漏等稳定性问题激烈碰撞。这表明该领域正处于从“技术验证”向“生产就绪”过渡的关键阶段，社区对**消息传递可靠性、安全边界和跨平台用户体验**的焦虑感显著上升。同时，社区对**基础设施重构（如 SQLite 存储迁移）** 和**未来协作范式（如多 Agent 协同）** 的长期投入信号，也预示着行业正为下一阶段的规模化应用做准备。

### 2. 各项目活跃度对比

| 指标 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **今日 Issues 数** | 196 | 50 |
| **今日 PR 数** | 500 | 50 |
| **今日 Release** | `v2026.7.1-beta.1` (小版本) | 无 |
| **核心 Bug 等级** | 多个 P1 级 Bug，集中在消息泄漏、会话卡死 | 1个 P1 级 Bug (QQBot无限重试)、多个 P2 级 Bug (桌面端体验) |
| **社区呼声最高** | “工具间文本泄漏”（严重影响UX）、“回归Bug”（损害信任） | “Desktop 独立安装”（轻量化部署）、“命令误判为注入”（安全与功能冲突） |
| **健康度评估** | **高压迭代，稳定性承压**。吞吐量巨大，但回归和P1级Bug造成社区信任危机。 | **快节奏质量攻坚**。修复效率高，但桌面端和平台网关问题集中爆发，反映出多平台支持引入的复杂性。 |

### 3. OpenClaw 在生态中的定位

- **平台级 AI 智能体底座**：OpenClaw 的定位更偏向于一个**企业级、多 Agent、网关化的智能体平台**。其核心功能如外部工具挂载、多频道集成（Slack, Telegram, Signal）、会话/转存 SQLite 重构、多 Agent 协作增强等，都指向构建复杂、可扩展的自动化工作流。
- **强项与差异化**：
    - **模型生态广度**：率先支持 OpenAI GPT-5.6 等最新模型族，体现了对前沿模型快速集成的能力。
    - **多 Agent 协作**：社区 RFC（#35203）探讨了能力分析、共享黑板等高级协作模式，这在生态中处于探索前沿。
    - **安全与合规性**：收紧 CSP 策略、修复 SSRF 导入路径等行动，显示出对安全边界的主动管理。
- **社区规模**：从 Issue/PR 数量（196/500）看，OpenClaw 的社区活跃度**显著高于** Hermes Agent (50/50)，用户基础和贡献者生态更庞大，但同时也带来了更多噪音和回归问题。

### 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求/表现 |
| :--- | :--- | :--- |
| **消息传递可靠性** | OpenClaw, Hermes Agent | **OpenClaw (#25592)**：工具内部文本泄漏到用户可见通道。**Hermes Agent (#52914)**：QQBot 网关无限重试循环。共同核心关切：Agent 推理过程与最终用户交互的边界隔离。 |
| **会话状态管理** | OpenClaw, Hermes Agent | **OpenClaw (#88312, #98416)**：Codex 卡死回归、会话初始化冲突。**Hermes Agent (#44456, #46556)**：`/compress` 命令路由错误。痛点在于：状态持久化、重入锁、命令过滤等实现不够健壮。 |
| **平台/网关稳定性** | OpenClaw, Hermes Agent | **OpenClaw (#87744)**：Codex 驱动 Telegram 超时。**Hermes Agent (#52914, #53449)**：QQBot 连接失败、Telegram 消息重复。多平台集成是共性挑战，尤其在非主流平台（QQ、Telegram）上稳定性问题突出。 |

### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **功能侧重** | **多 Agent 协作、企业级工作流、模型前沿集成**。强调“平台”和“网关”属性，支撑复杂的 Agent 间通信与外部工具链。 | **个人桌面体验、轻量化部署、安全与隐私**。强调“客户端”属性，尤其是 Desktop 客户端的易用性和独立运行能力。 |
| **目标用户** | **开发者、技术团队、DevOps 工程师**，用于构建自动化业务流、内部 AI Copilot。 | **个人开发者、AI爱好者、Power User**，作为个人 AI 助手，强调本地运行与隐私保护。 |
| **技术架构** | **Gateway + Runner 架构**。强调通过 Gateway 管理多个外部工具和 Agent 运行时（如 Codex、Sandbox），架构更具分布式和微服务风格。 | **单 Agent + 多平台 Adapter**。核心是一个 Agent 进程，通过插件/Adapter 连接不同平台（QQ、TG、Discord），架构相对集中。 |
| **核心痛点** | 回归 Bug 频发，**“大而全”带来的稳定性代价**。 | 桌面端体验割裂，**“小而美”但在多平台适配中暴露碎片化问题**。 |

### 6. 社区热度与成熟度

- **快速迭代阶段**：
    - **Hermes Agent**：尽管 Bug 不少，但 PR 修复效率高（一天合并18个），且社区对 Desktop 独立安装、新技能（如 `mind`、`unbroker`）的讨论和贡献非常活跃。其特征是**“快速反馈、高频修复”**，社区生态处于快速成长的青春期。
- **质量巩固阶段**：
    - **OpenClaw**：社区规模大，讨论复杂（如 RFC 多Agent协作）。但多个回归 Bug（#88312）和长期未决的 Issue（如 #32530）表明项目正面临 **“规模带来的管理复杂度”**。当前阶段更侧重于**修补核心稳定性**，为更复杂的特性提供坚实基础。其状态是 **“在高压下求稳”**。

### 7. 值得关注的趋势信号

1.  **“生产稳定性” 是当前最大瓶颈**：多个项目共同遭遇回归和消息泄漏问题，这强烈暗示当前 AI 智能体框架在处理**非确定性 Agent 推理输出**与**确定性用户交互规则**之间的鸿沟时，存在架构性缺陷。开发者应重点关注**消息边界隔离**和**状态机健壮性**的设计模式。

2.  **“安全与主权” 成为核心推动力**：OpenClaw 收紧 CSP、Hermes Agent 防御 Prompt 注入、用户要求独立桌面端（无需远端依赖），这些信号表明社区正从 “能跑起来” 向 **“安全、可控、离线”** 转变。**部署形态的轻量化（独立客户端）和权限控制的精细化**将是未来产品的重要卖点。

3.  **“桌面端” 被重新定义为 Agent 主战场**：Hermes Agent 对 Desktop 客户端的集中投入和用户的热烈反馈，暗示**桌面端**可能超越移动端或 Web 端，成为个人 AI 智能体的核心交互载体。开发者应考虑优先优化桌面端（特别是 Profile 管理、命令路由、UI/UX 一致性）的体验。

4.  **“多 Agent 协作” 正从概念走向工程实践**：OpenClaw 的 RFC (#35203) 和 Hermes Agent 的 `unbroker` 技能，都指向了多个 Agent 或工具间的协同。这预示着未来 Agent 将不再“单打独斗”，**构建 Agent 间通信协议（如共享黑板、能力广播）和编排引擎**将是下一阶段的技术高地。

**对开发者的启示**：当前阶段，一个健壮的 AI 智能体项目需要同时解决“前端的用户体验（如消息不泄露）”、“中台的状态管理（如会话不卡死）”和“后端的安全与治理（如权限控制）”。建议开发者优先夯实基础稳定性，再探索高级协作范式。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，这是根据您提供的 Hermes Agent 项目数据生成的 2026-07-03 项目动态日报。

---

## Hermes Agent 项目动态日报 — 2026-07-03

### 今日速览

今日项目活跃度极高，共产生 50 条 Issue 和 50 条 PR 更新，社区贡献踊跃。核心关注点集中在三个方向：一是对桌面客户端（Desktop）的体验优化和 Bug 修复，如配置文件管理、UI 渲染和命令路由问题；二是对多平台网关（QQBot, Telegram, Discord）的稳定性和安全性加固；三是围绕 Agent 核心的会话状态管理、Prompt 注入防御等深层技术问题。大量 PR 已提交并被合并，显示了项目在快速迭代中的高修复效率。

### 版本发布

今日无新版本发布。

### 项目进展

今日有 18 个 PR 被合并或关闭，多项重要功能和 Bug 修复取得进展，项目稳健向前推进。

- **安全加固**：
    - PR [#57475](https://github.com/NousResearch/hermes-agent/pull/57475) 修复了可通过 `sh -c "rm -rf /"` 方式绕过安全审批系统的问题，强化了命令执行的边界检查。
    - PR [#57458](https://github.com/NousResearch/hermes-agent/pull/57458) 修复了对敏感路径的安全检查，通过解析符号链接避免了路径字符串层面的绕过。
- **桌面客户端 (Desktop) 体验修复**：
    - PR [#57471](https://github.com/NousResearch/hermes-agent/pull/57471) 修复了桌面端启动后无法保持已选 Profile 的问题，现在 Profile 可以持久化保存。**（相关 Issue: #57283）**
    - PR [#57455](https://github.com/NousResearch/hermes-agent/pull/57455) 修复了在 macOS (Tahoe) 上桌面窗口控制按钮重叠的问题。
    - PR [#57457](https://github.com/NousResearch/hermes-agent/pull/57457) 隐藏了 Windows 更新程序在后台运行时弹出的控制台窗口，提升了用户体验。
- **平台兼容性**：
    - PR [#57456](https://github.com/NousResearch/hermes-agent/pull/57456) 修复了 macOS 上因用户 ID 解析失败导致的 LaunchAgent 启动问题，提升了 Mac 环境下的稳定性。**（相关 Issue: #57292）**
    - PR [#57470](https://github.com/NousResearch/hermes-agent/pull/57470) 修复了 Windows 网关上 `PYTHONPATH` 环境变量泄露到全局环境的问题，避免了潜在的副作用。
    - PR [#57459](https://github.com/NousResearch/hermes-agent/pull/57459) 修复了与 Python 3.14 的兼容性问题，调整了自定义线程池实现。
    - PR [#57469](https://github.com/NousResearch/hermes-agent/pull/57469) 优化了 TUI 在 monorepo 下的包检查逻辑，避免了不必要的 npm install 操作。
- **会话与指令处理**：
    - PR [#56073](https://github.com/NousResearch/hermes-agent/pull/56073) 实现了针对 Provider 速率限制的自动恢复机制，当 API 配额恢复后，受影响的会话会带延迟自动重试，提升了自动化的可靠性。
    - PR [#57461](https://github.com/NousResearch/hermes-agent/pull/57461) 在 ContextEngine 中添加了 `post_compress()` 钩子，允许第三方插件在上下文压缩后自定义处理逻辑。
    - PR [#57445](https://github.com/NousResearch/hermes-agent/pull/57445) 修复了在仅配置密码认证的 Dashboard 上登录时返回 500 错误的问题。
- **其他**：PR [#57438](https://github.com/NousResearch/hermes-agent/pull/57438) 新增了面向安全的 `unbroker` 技能，旨在自动化数据代理移除流程；PR [#57225](https://github.com/NousResearch/hermes-agent/pull/57225) 在安装路径中明确标记 pip 和 Homebrew 为不被支持的安装方式。

### 社区热点

- **Issue #52914 - QQBot 无限重试循环**: 该 Issue 以 12 条评论成为今日最热。贡献者 **fishlikeX** 报告了 QQBot 网关因 `connect()` 方法缺少 `is_reconnect` 参数而陷入无限循环的严重问题。该问题引发了对 QQ 机器人网关稳定性的广泛讨论，显示了中文用户社区的高度关注。 [查看链接](https://github.com/NousResearch/hermes-agent/issues/52914)
- **Issue #38602 - 桌面客户端独立安装**: 以 37 个 👍 和 8 条评论成为社区最渴望的功能之一。用户 **diegohb** 要求桌面端可以作为纯客户端运行，连接到远程 Hermes Agent，而不需要本地启动完整的 Agent 运行时。这反映了用户对轻量化、灵活部署模式的强烈需求。 [查看链接](https://github.com/NousResearch/hermes-agent/issues/38602)
- **Issue #36934 - `/steer` 命令被误判为 Prompt 注入**: 该问题讨论了在使用 `/steer` 指令时，高安全级别的模型（如 Opus 4.8）会将其误判为 Prompt 注入攻击。这引发了社区关于如何平衡工具功能与安全防御的热议，尤其聚焦于“工具通道”与“注入防御”之间的冲突问题。 [查看链接](https://github.com/NousResearch/hermes-agent/issues/36934)

### Bug 与稳定性

今日报告的 Bug 主要集中在桌面客户端、多平台网关和 Agent 核心功能上。

- **严重 (P1)**:
    - **QQBot 无限重试循环**（Issue #52914）：`QQBot adapter.connect()` 参数缺失，导致无法连接。尚无 Fix PR。
    - **Prompt 注入误报**（Issue #36934）：`/steer` 命令在高安全模型下被误杀。尚无 Fix PR。
- **中等 (P2)**:
    - **Desktop `/compress` 命令失效**（Issue #44456, #46556）：多个用户报告内置命令被错误路由到插件处理。尚无 Fix PR。
    - **Telegram 回复消息重复**（Issue #53449）：因流式传输完成标志位丢失导致消息重复发送。尚无 Fix PR。
    - **Desktop 删除 Profile 失效**（Issue #47368）：UI 上删除后 Profile 仍会重建，是持久化问题。Fix PR #57471 已被合并。
    - **`computer_use` 在 Linux/WSL 上崩溃**（Issue #56704）：因 `list_windows` 返回 `None` 类型的 pid。尚无 Fix PR。
    - **SubAgent Fallback 模型 URL 配置错误**（Issue #24782）：子 Agent 降级时使用了错误的 `base_url`。尚无 Fix PR。
    - **Dashboard 自动重启失败**（Issue #52470）：子进程继承错误的 `_HERMES_GATEWAY=1` 环境变量。尚无 Fix PR。
    - **Discord 频道提及授权失效**（PR #57460, #57463）：已通过新建和已合并的 PR 修复。
- **较低 (P3)**:
    - **Desktop 侧边栏频繁刷新导致高 CPU**（Issue #53049）：用户报告更新后出现此回归问题。尚无 Fix PR。
    - **macOS Tahoe 标题栏重叠**（Issue #57455）：已通过已合并的 PR #57455 修复。

### 功能请求与路线图信号

- **高需求功能**: **Desktop 客户端独立安装** (Issue #38602, 👍37) 是社区的强烈呼声。这表明用户希望 Hermes Agent 能支持更灵活的 C/S 架构。
- **安全与治理**: 用户提出**通用 OAuth Broker 凭证源** (Issue #23944) 以解决多运行时环境下 Token 刷新冲突问题，这指向更复杂的企业级部署场景。
- **新技能与插件**: 社区贡献了多个新技能，如 **`mind` 离线项目记忆技能** (PR #56859) 和 **`unbroker` 数据代理移除技能** (PR #57438)。这些 PR 已被接收，表明项目对新插件持开放态度，并可能在下一个版本中加入。
- **未来版本信号**: **价格覆盖与合同定价** (Issue #9403) 功能尚未实现，这可能是一个尚未定版的高级特性。**高级安全功能** (Issue #3630) 如临时密钥、外部 Vault 集成等，仍处于规划阶段，表明项目在安全能力上还有长远的路线图。

### 用户反馈摘要

- **痛点**: 桌面客户端的体验问题集中爆发。多位用户指出 `/compress` 命令被错误路由、`/model` 切换逻辑混乱。用户 `Pauliehedron` 甚至在 Issue #54473 中直言，Desktop 版本与 CLI/TUI 存在较大体验差距，原因是团队开发重心过度偏向 Desktop 而忽略了非 GUI 的参考实现。
- **使用场景**: 用户 **humble92** 希望通过 Desktop 的“删除 profile”功能彻底移除配置，以管理多个开发或测试环境，但功能的失效导致其流程受阻。
- **满意之处**: 有用户对新增的 GCP `vertex` Provider 和 Service Account JSON 上传功能表示赞赏，认为这是一个非常棒的更新（Issue #56687）。
- **社区温度**: 社区对 Prompt 注入等安全话题的讨论非常深入，并提出了有建设性的解决方案。同时，对 QQBot、Telegram 等非主流平台的关注度也很高，显示了 Hermes Agent 的社区多样性。

### 待处理积压

- **长期未决的 Feature Request**:
    - **Issue #8465 - 更好的 LiteLLM 支持** (创建于 2026-04-12)：用户希望 Hermes Agent 能自动检测 LiteLLM 的上下文大小，避免默认使用 128k 的限制。该问题长期未获得明确答复，可能阻碍了部分使用自定义 Provider 的用户。
    - **Issue #3630 - 高级安全功能** (创建于 2026-03-28)：作为安全管理的第4阶段规划，包含临时密钥、外部 Vault 等特性。该功能依赖前期阶段，但作为规划性 Issue 已存在数月。

- **长期未决的 Bug**:
    - **Issue #23944 - OAuth Token 刷新冲突** (创建于 2026-05-11)：该功能提议虽然用户呼声较高（2个👍），但尚未被纳入开发日程。

以上待处理项建议项目维护者关注，特别是 LiteLLM 支持问题，可能会影响期望使用低成本或定制化 LLM 服务的用户群体。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*