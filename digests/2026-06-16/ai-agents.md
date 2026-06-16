# OpenClaw 生态日报 2026-06-16

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-16 03:40 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我将根据您提供的 OpenClaw GitHub 数据，为您生成一份今日项目动态日报。

---

# OpenClaw 项目动态日报 — 2026-06-16

## 1. 今日速览

今日 OpenClaw 项目活跃度极高，社区贡献和 Bug 反馈呈井喷状态。过去 24 小时内，项目迎来了 481 条新/活跃的 Issue 和 413 个待合并的 PR，同时发布了 v2026.6.8-beta.2 版本。虽然合并/关闭的 PR 数量（87个）相对较低，但大量的活跃讨论和待处理工作表明社区正处于功能密集开发和问题集中反馈的阶段。**项目健康状况良好，但维护者面临显著的修复合入和决策压力。**

## 2. 版本发布

**v2026.6.8-beta.2**

-   **核心更新：** 此次 beta 版本主要聚焦于消息通道传输层的改进。
-   **Telegram & WhatsApp 通道重大升级：**
    -   **结构丰富性：** 现在可以发送结构化富文本，包括表格、列表、可展开的引用块等，显著提升了机器人回复的可读性和信息密度。
    -   **稳定性增强：** 消息损失的脆弱性问题得到改善。
    -   **破坏性变更与迁移：**
        -   **Telegram 原生草稿迁移：** 旧的原生草稿（native draft）发送机制被弃用并迁移。开发者或用户如果依赖于旧的草稿行为，可能需要进行适配。建议检查自定义的 Telegram 回复逻辑。
        -   **CLI 后端交付：** 引入了“保留原始换行符”（preserved intentional line breaks）的 CLI 后端交付方式，可能影响在 Telegram 中通过 CLI 触发的消息格式。
        -   **富媒体兼容性：** “更安全的富媒体启动”（safer rich-media boot）提示在旧版客户端或自定义 Bot 客户端上可能需要兼容性测试。
-   **链接：** [v2026.6.8-beta.2 发布页面](https://github.com/openclaw/openclaw/releases/tag/v2026.6.8-beta.2)

## 3. 项目进展

今日虽有大量 PR 提交，但核心进展在于已合并/关闭的 87 个 PR。以下为关键推进：

-   **核心稳定性修复：** PR [#91208](https://github.com/openclaw/openclaw/pull/91208) 已关闭，修复了插件会话扩展注册表不固定，导致 `sessions.pluginPatch` 在代理/子代理加载切换后失效的严重问题。这直接增强了多人会话插件的稳定性。
-   **身份认证与配置：** 有关 Copilot Token 缓存忽略 Profile 轮转的问题 (#43659) 和跨网关会话通信功能 (#43656) 虽仍 Open，但相关代码进入审查阶段，表明项目正在积极推进多代理、多身份认证场景。
-   **工具生态补全：** CLI 工具 `image generate` 新增 `--file` 参数 (PR [#91807](https://github.com/openclaw/openclaw/pull/91807))，实现了与 `image edit` 命令的参数对齐。

## 4. 社区热点

-   **热度最高 Issue：** **#75 - Linux/Windows Clawdbot Apps**
    -   **链接：** [Issue #75](https://github.com/openclaw/openclaw/issues/75)
    -   **分析：** 该 Issue 以 109 条评论和 79 个 👍 遥遥领先。核心诉求是要求 OpenClaw 提供与 macOS 功能相当的 Linux 和 Windows 平台应用。这是社区对**跨平台体验一致性**的强烈呼声，考虑到项目核心是用 Node.js 实现，这是一个巨大的工程但也是拓宽用户基础的关键。
-   **反馈最热烈：** **#25592 - 工具调用间文本泄露至消息通道**
    -   **链接：** [Issue #25592](https://github.com/openclaw/openclaw/issues/25592)
    -   **分析：** 虽然评论数 (32) 不如 #75，但被标记为 `impact:message-loss` 和 `diamond lobster` 高影响力问题。用户反馈代理在处理工具调用（如错误处理、中间处理日志）时生成的文本会错误地发送到用户可见的消息通道（如 Slack），造成非常严重的 UX 污染。这表明社区对**Agent 行为的可预测性和内部状态透明性**有极高的要求。
-   **高期待功能：** **#9443 - 请求预构建 Android APK**
    -   **链接：** [Issue #9443](https://github.com/openclaw/openclaw/issues/9443)
    -   **分析：** 评论数 25，用户明确希望项目提供开箱即用的 Android 伴侣应用 APK 下载。这与 #75 的跨平台呼声一脉相承，验证了用户对**移动端和桌面端便携使用**的巨大需求。

## 5. Bug 与稳定性

今日报告的 Bug 集中在会话管理、消息传递和配置兼容性上，且多个为回归问题。

-   **严重 (P1 & `diamond lobster`)：**
    -   [#25592](https://github.com/openclaw/openclaw/issues/25592) **文本泄露** (无 fix PR)：有`linked-pr-open`标签，表明有关联PR，但尚未彻底解决。
    -   [#22676](https://github.com/openclaw/openclaw/issues/22676) **Signal daemon 重启竞争** (无 fix PR)：导致孤儿进程和发送失败。
    -   [#32296](https://github.com/openclaw/openclaw/issues/32296) **会话上下文混乱** (无 fix PR)：Agent 回复上一条消息，核心会话逻辑错误。
    -   [#40540](https://github.com/openclaw/openclaw/issues/40540) **Windows 更新失败 (EBUSY)** (无 fix PR)：关键维护命令在 Windows 上失效。
-   **中等 (P2 & `diamond lobster`)：**
    -   [#32473](https://github.com/openclaw/openclaw/issues/32473) **Control UI 要求HTTPS** (无 fix PR)：Docker 部署时因非 HTTPS 环境导致 UI 功能不可用，是严重的部署体验 Bug。
    -   [#41201](https://github.com/openclaw/openclaw/issues/41201) **Control UI 头像显示为损坏图片** (无 fix PR)：回归问题，影响 UI 体验。
    -   [#31331](https://github.com/openclaw/openclaw/issues/31331) **Docker 内 Sandbox 工作区挂载问题** (无 fix PR)：Docker-in-Docker 环境下的典型权限和路径问题。
-   **值得注意的回归：**
    -   **#32473**, **#41201**, **#38327** (Google Vertex 模型崩溃), **#38439** (Webchat头像 404) 均被标记为 `regression`，说明近期更新引入了多个向下兼容性问题，需要维护团队重点排查。

## 6. 功能请求与路线图信号

-   **安全与权限 (高优先级)：**
    -   **Masked Secrets** ([#10659](https://github.com/openclaw/openclaw/issues/10659))：防止 Agent 看到原始 API Key，是安全增强的核心诉求。
    -   **Filesystem Sandboxing** ([#7722](https://github.com/openclaw/openclaw/issues/7722)) 和 **Path-scoped RWX** ([#39979](https://github.com/openclaw/openclaw/issues/39979))：用户对精细化文件访问控制的需求强烈。
    -   **Denylist for exec-approvals** ([#6615](https://github.com/openclaw/openclaw/issues/6615))：希望有“放行所有，仅阻止特定危险命令”的灵活策略。
-   **会话与记忆增强：**
    -   **Tiered Bootstrap** ([#22438](https://github.com/openclaw/openclaw/issues/22438))：按需加载配置文件以节省 Token。
    -   **Automated Session Memory Preservation** ([#40418](https://github.com/openclaw/openclaw/issues/40418))：实现 `/new` 后自动保存和总结记忆，是提升用户体验的关键功能。
    -   **Multi-Agent Collaboration Enhancement** ([#35203](https://github.com/openclaw/openclaw/issues/35203))：能力画像、共享黑板等，开启了多Agent协作的进阶玩法。
-   **通道与UI：**
    -   **Slack Block Kit** ([#12602](https://github.com/openclaw/openclaw/issues/12602))：让Agent能发送富交互消息。
    -   **Reasoning stream** ([#42276](https://github.com/openclaw/openclaw/issues/42276))：用户期望能看到 Agent 的“思考过程”，类似 OpenAI 和 Grok。

**路线图信号：** `sandbox: keep workspaceAccess none workspaces writable` ([#37634](https://github.com/openclaw/openclaw/issues/37634)) 获得了 6 个 👍，表明沙箱功能的成熟度是社区关注的重点。同时，`Tools: web_fetch allowPrivateNetwork` ([#39604](https://github.com/openclaw/openclaw/issues/39604)) 获得了9个👍，说明许多用户有在私有网络内进行数据抓取的需求，该功能很可能在下一个版本中被纳入。

## 7. 用户反馈摘要

-   **痛点：**
    -   **配置不生效：** 用户 `tuna-chin` 在 [#29387](https://github.com/openclaw/openclaw/issues/29387) 中报告 per-agent `bootstrap` 文件被忽略，只能使用全局工作区文件。这导致复杂的 Agent 无法“人格化”，是高级用户的挫折点。
    -   **Docker 体验差：** `jiesou` 在 [#31331](https://github.com/openclaw/openclaw/issues/31331) 和 `RafaelLee` 在 [#32473](https://github.com/openclaw/openclaw/issues/32473) 共同反映了 Docker 部署下 Sandbox 和 UI 的痛点，说明官方部署文档和容器镜像急需优化。
    -   **“写”工具缺陷：** `altsoulkiller` 在 [#40001](https://github.com/openclaw/openclaw/issues/40001) 指出 `write` 工具缺乏追加模式，导致定时任务等并发场景下互相覆盖文件，造成数据丢失。
-   **场景反馈：**
    -   **希望开箱即用：** 用户 `AstridQing-AI` 代表 `Lysen` 提交的 [#9443](https://github.com/openclaw/openclaw/issues/9443) 和 `steipete` 的 [#75](https://github.com/openclaw/openclaw/issues/75)，都表达了用户希望项目提供更完善的打包和分发机制，降低使用门槛。
    -   **对高可靠性有期待：** `ZemonVunter` 在 [#41165](https://github.com/openclaw/openclaw/issues/41165) 中反馈，即使有之前的修复，Telegram DM 仍然会错误路由到主会话，表明用户对消息路由的可靠性和隔离性要求很高。

## 8. 待处理积压

-   **长期未响应的平台需求：**
    -   **[#75 - Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)**: 创建于 2026年初，虽最近仍有活跃讨论，但无里程碑或进展，已成为社区最大的“等待区”。该问题很可能需要一次重大的架构决策。
-   **无进展信号的功能请求：**
    -   **[#11665 - Webhook Hook 会话复用](https://github.com/openclaw/openclaw/issues/11665)**: “多轮对话”功能未按文档工作，标记为 `no-new-fix-pr` 和 `needs-product-decision`，表明该任务已停滞。
    -   **[#10687 - 动态模型发现](https://github.com/openclaw/openclaw/issues/10687)**: 创建于2月，对于集成 OpenRouter 这类快速更新模型列表的服务至关重要，但仍停留在规划阶段，需要维护者优先考虑。
    -   **[#41744 - Feishu 图片丢失](https://github.com/openclaw/openclaw/issues/41744)**: 已标记为 `stale`，但这是一个明确的消息丢失 Bug，对于使用飞书的用户社群影响很大，应被激活处理。

---
**分析师总结：** OpenClaw 今日展现了强大的社区活力，但项目处于“高产高反馈”的瓶颈期。大量 PR 和 Issue 的涌入超过了维护者的响应和处理速度，特别是严重 Bug 的修复和长期积压的功能请求。**下一阶段的重点应是：**
1.  **加速合入已完成的 PR**，特别是修复回归问题和增强稳定性的。
2.  **对 P1 级别的 Bug 进行集中分类和攻坚**，尤其是 #32296、#22676 等影响核心会话逻辑的问题。
3.  **对 #75 和 #9443 等热门跨平台需求给出明确的 roadmap 信号**，哪怕只是指出当前不可行的原因或未来的技术选型方向，以避免社区猜疑和不满。

---

## 横向生态对比

好的，作为 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我根据您提供的 OpenClaw 和 Hermes Agent 最新动态，为您生成以下横向对比分析报告。

---

# 个人 AI 智能体开源生态横向对比日报 — 2026-06-16

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于 **“高产与阵痛并存”** 的密集活跃期。以 OpenClaw 和 Hermes Agent 为代表的两个项目均呈现出 **社区贡献井喷、功能快速迭代与回归 Bug 集中爆发** 的典型特征。核心矛盾在于：用户对 **跨平台原生体验、安全沙箱、分布式 Agent 架构** 的需求日益强烈，而项目维护团队在应对海量 PR 和 Issue 时节奏明显滞后。生态整体正从“单 Agent 工具”向“多 Agent 编排 + 安全可控的私有化部署”方向演进，高度活跃的社区为技术突破提供了动力，也带来了稳定性和兼容性挑战。

## 2. 各项目活跃度对比

| 指标 | OpenClaw | Hermes Agent |
|------|----------|--------------|
| **新/活跃 Issues** | 481 条 | 43 条 |
| **待合并 PR** | 413 个 | 45 个 |
| **已合并/关闭 PR** | 87 个 | 5 个 |
| **新版本发布** | v2026.6.8-beta.2 | 无（上一个 v0.16.0） |
| **P1 级严重 Bug 数** | 4 个（均无已合并 Fix PR） | 3 个（1 个有 PR 待合） |
| **社区反馈（热门 Issue 点赞/评论）** | #75 获 79 👍、109 评论 | #18715 获 15 👍、4 评论 |
| **健康度评估** | ⚠️ **高产高压**：社区参与度极高，但积压严重、P1 修复滞后，维护者瓶颈明显 | 🟢 **稳步巩固**：Issue/PR 量级较低，但重点功能（TaskGraph、MoA）有长期推进，P1 修复有对应 PR |

**结论**：OpenClaw 在活跃度（量级）上远超 Hermes Agent，但 High-Volume, Low-Response 的失衡风险也更大；Hermes Agent 体量较小，但核心演进方向清晰，Bug 修复相对有序。

## 3. OpenClaw 在生态中的定位

与同为个人 AI 助手领域的 Hermes Agent 相比，OpenClaw 呈现出以下特征：

- **优势**：
  - **社区规模更大**：今日活跃 Issue/PR 数量是 Hermes Agent 的 10 倍以上，表明其用户/贡献者基数和生态影响力显著更高。
  - **版本迭代更快**：持续发布 Beta 版本（今日 v2026.6.8-beta.2），尤其是在消息通道（Telegram、WhatsApp）富文本支持等端到端体验上快速落地。
  - **跨平台呼声最高**：#75（Linux/Windows App）和 #9443（Android APK）获得社区超高共鸣，说明 OpenClaw 是用户心中“跨平台个人助手”的首选载体。

- **技术路线差异**：
  - OpenClaw 更 **侧重消息通道集成**（Telegram、Slack、飞书等），强调 Agent 与用户的实时交互体验（富文本、结构化回复）。
  - Hermes Agent 更 **侧重模型编排与 Agent 内部架构**（MoA 虚拟模型、DAG TaskGraph、Kanban 工作流、MCP 协议），面向高阶用户和研究场景。

- **社区规模对比**：
  - OpenClaw 属于 **大型社区**（日新增 400+ Issue/PR），适用于希望快速集成、跨平台部署的个人/小团队。
  - Hermes Agent 属于 **中型研究导向社区**，适合对 Agent 内部机制（多智能体协作、模型组合）有探索需求的开发者。

## 4. 共同关注的技术方向

两个项目今日的 Issue/PR 中涌现出多个 **高度重合** 的技术诉求，显示出生态共性趋势：

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|----------|----------|
| **跨平台原生应用** | OpenClaw (#75, #9443)、Hermes Agent (#40187) | 用户强烈要求提供 Linux/Windows 桌面端、Android 移动端的一键安装/编译体验，降低部署门槛。 |
| **远程智能体 + 本地工具执行** | OpenClaw（Sandbox 挂载 #31331）、Hermes Agent (#18715) | 期望一种架构：核心 Agent 运行在远程服务器，但文件操作、Docker 等敏感工具在本地安全执行。 |
| **安全沙箱与权限控制** | OpenClaw（Filesystem Sandboxing #7722, Masked Secrets #10659）、Hermes Agent（每进程 UUID session key #16511） | 防止 Agent 越权访问用户密钥、文件系统，以及跨会话数据泄露。 |
| **多智能体协作基础** | OpenClaw（共享黑板、能力画像 #35203）、Hermes Agent（DAG TaskGraph #12436, Kanban worker） | 多个 Agent 可共享工作区、消息队列，实现任务分派和结果汇总。 |
| **输出长度与格式优化** | OpenClaw（Telegram 富文本 Beta）、Hermes Agent（输出截断 #7237、Rich Text 分段） | 用户期望 Agent 能处理长回复、结构化内容（表格/代码块），并在不同消息通道上优雅呈现。 |
| **中国区本地化支持** | OpenClaw（飞书图片丢失 Bug #41744）、Hermes Agent（minimax-cn-oauth #36286, 网络访问优化 #46839） | 需要适配中国特有消息平台（飞书）、OAuth 提供商及网络环境。 |

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
|------|----------|--------------|
| **功能侧重** | 消息通道集成、统一收件箱、跨平台 Clawdbot 应用、富文本交互 | 模型编排（MoA/Fusion）、Agent 内部工作流（Kanban/DAG）、MCP 协议、研究级多智能体 |
| **目标用户** | 个人用户、小团队，需要“一个 Agent 管理所有聊天渠道”的日常助手 | AI 研究员、高级开发者，探索多模型协作、自定义 Agent 拓扑 |
| **技术架构** | Node.js 核心，插件化会话管理，强调与第三方 IM 的深度对接 | 语言未明确（从 PR 看涉及 Python/JS），强调灵活模型提供者、标准化协议（MCP）、任务图执行 |
| **典型痛点** | 跨平台应用缺失（#75）、Docker 部署下 Sandbox/UI 问题（#31331, #32473） | 输出截断（#7237）、Skill 列表膨胀导致 token 浪费（#22620）、桌面端编译失败（#40187） |
| **社区治理** | 大社区，PR 合入压力大，P1 修复缺少明确责任人 | 小社区，大型 PR（TaskGraph）持续迭代但速度慢，P1 修复有对应 PR 但未合 |

**一句话总结**：OpenClaw 是 **“通往用户端的桥梁”**，Hermes Agent 是 **“架设 Agent 大脑的实验室”**。两者在生态中互补大于竞争。

## 6. 社区热度与成熟度

| 分层 | 项目 | 阶段判断 | 依据 |
|------|------|----------|------|
| **快速迭代阶段** | 🟡 **OpenClaw** | 高产高反馈，但稳定性承压 | 日增 400+ Issue/PR，频繁 Beta 发版，P1 Bug 堆积但社区参与度极高 |
| **质量巩固阶段** | 🟢 **Hermes Agent** | 稳步推进，重点修复回归问题 | v0.16.0 发布后集中修复回归，PR 合入少但方向明确（TaskGraph、MoA、安全 session key） |

**注**：OpenClaw 的健康度虽因积压问题被标记为“高压”，但高社区参与度说明其生态活力和用户粘性很强，适合能够接受一定不稳定性的早期采用者。Hermes Agent 则更适合对稳定性要求较高、愿意等待版本成熟的用户。

## 7. 值得关注的趋势信号

从今日两个项目的社区反馈中，提炼以下 **对 AI 智能体开发者有直接参考价值** 的行业趋势：

1. **分布式 Agent 部署成为刚需**：用户明确要求“远程 Agent + 本地工具”（Hermes #18715, OpenClaw #31331），预示个人 AI 助手将走向 **“中央大脑 + 边缘执行”** 的混合架构。开发者应提前设计 Agent 的远程调用接口和本地沙箱隔离机制。

2. **跨平台原生应用是获取用户心智的关键**：OpenClaw #75（Linux/Windows App）和 #9443（Android APK）的高热度印证了 **“移动端+桌面端”一体化** 是个人助手普及的瓶颈。任何新项目在初期就应考虑 Electron/Tauri 或 Flutter 封装。

3. **Agent 内部状态透明化需求崛起**：用户期望看到 Agent 的“思考过程”（OpenClaw reasoning stream #42276）、工具调用日志不被泄露给终端用户（#25592），以及错误信息直接透传（Hermes #46593）。这意味着开发者需要设计 **可观察性框架**（如 Logs、Traces），同时控制哪些信息对用户可见。

4. **安全沙箱和权限粒度从“可选”变为“必须”**：OpenClaw 的 Masked Secrets、Filesystem Sandboxing、Denylist，以及 Hermes 的每进程 UUID session key，都指向同一方向：**Agent 必须运行在一个可审计、可限制的沙箱内**，且权限策略应支持路径级、操作级（RWX）的细粒度配置。

5. **多 Agent 协作从概念走向代码**：OpenClaw 的共享黑板 (#35203) 和 Hermes 的 DAG TaskGraph (#12436) 都已进入 PR 阶段，说明 **任务编排、能力注册、结果聚合** 等基础组件正在标准化。开发者在构建 Agent 时，应预留“协作接口”（如共享内存、事件总线、协议定义）。

6. **长文本处理仍是 Agent 最普遍的 UX 痛点**：Hermes #7237 即便已关闭仍持续收获评论，表明 **输出截断** 严重影响多轮对话、代码生成、文章撰写等场景。建议开发者实现 **智能分页/续写/摘要** 机制，而非简单依赖模型 max_tokens。

---

**分析师结语**：OpenClaw 和 Hermes Agent 今日动态折射出个人 AI 助手生态的两个面：**广阔的市场需求**（跨平台、易用性）和 **深层的技术挑战**（安全、编排、稳定性）。对于技术决策者，建议关注 OpenClaw 的跨平台进展和 Hermes 的多 Agent 编排成果，并准备在项目初期就将 **分布式架构、安全沙箱、可观察性** 三大核心能力纳入技术栈，以应对下一波用户期望的升级。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目日报  
**日期**: 2026-06-16  
**数据来源**: GitHub (NousResearch/hermes-agent) · 过去 24 小时统计  

---

## 1. 今日速览

过去 24 小时社区高度活跃：共产生 **50 条 Issue 更新**（新开/活跃 43 条，关闭 7 条）和 **50 条 PR 更新**（待合并 45 条，已合并/关闭 5 条）。无新版本发布。项目正处于 **v0.16.0 发布后的密集维护期**，大量回归问题、配置兼容性 bug 以及功能优化请求集中涌现，同时旧版遗留的架构性问题（如 Kanban 协议、MCP 配置可见性、会话隔离等）仍在持续修复中。社区贡献者参与度较高，约半数 PR 来自外部开发者。

---

## 2. 版本发布

**无新版本发布。** 上一个正式版为 v0.16.0（2026-06-05），今日多条 Issue 涉及该版本的回归问题。

---

## 3. 项目进展

今日合并/关闭的 PR 数量较少，以下为已确认完成的重要变更：

| PR | 描述 | 状态 | 关联 Issue |
|----|------|------|------------|
| [#46958](https://github.com/NousResearch/hermes-agent/pull/46958) | 在容器化环境中隐藏桌面版 dashboard 的更新控制按钮，避免误操作 | **已合并** | — |

此外，仍有 **45 个 PR 处于开放待合并状态**，其中值得关注的长期推进包括：
- [#12436](https://github.com/NousResearch/hermes-agent/pull/12436) (4月19日): DAG TaskGraph + 多智能体编排基础设施，已持续获得 commits 更新。
- [#46081](https://github.com/NousResearch/hermes-agent/pull/46081) (6月14日): 将 MoA (Mixture of Agents) 暴露为可选虚拟模型提供者，简化配置。
- [#46094](https://github.com/NousResearch/hermes-agent/pull/46094) (6月14日): 为 OpenRouter/Nous Fusion 预设添加可配置模型别名。
- [#36286](https://github.com/NousResearch/hermes-agent/pull/36286) (6月1日): 新增 `minimax-cn-oauth` 中国区 OAuth 提供者。
- [#16511](https://github.com/NousResearch/hermes-agent/pull/16511) (4月27日): 使用每进程 UUID 作为默认 session key 以防止跨会话状态泄露（P1 安全修复）。

整体来看，项目在**多智能体编排、MoA 虚拟模型、中国区兼容性**等方向上有实质进展，但许多大型 PR 仍需进一步 review 与测试。

---

## 4. 社区热点

今日讨论最活跃的 Issue 与 PR 如下：

| 编号 | 标题 | 评论数 | 核心诉求 |
|------|------|--------|----------|
| [#7237](https://github.com/NousResearch/hermes-agent/issues/7237) (已关闭) | Error: Response truncated due to output length limit | 50 👍6 | 长文本生成时被输出长度限制截断，影响 CLI/Telegram/Discord/Slack 等多种场景。该 Issue 已关闭，但高评论表明这是社区长期痛点。 |
| [#40187](https://github.com/NousResearch/hermes-agent/issues/40187) (开放) | `hermes update` / `hermes desktop` 在 macOS 上编译桌面应用失败 | 8 | Electron Builder 在最终编译阶段报错，影响 macOS 用户安装体验。 |
| [#22620](https://github.com/NousResearch/hermes-agent/issues/22620) (开放) | Skill 列表膨胀导致上下文窗口膨胀——需矢量路由或懒加载 | 5 | 大量 skill 列表占用上下文 token，社区期待智能路由机制。 |
| [#27178](https://github.com/NousResearch/hermes-agent/issues/27178) (开放) | Kanban worker 在代理以文本回复结束时报告 `protocol_violation` | 4 | Kanban 流程中缺少 fallback 机制，导致协议违规误报。 |
| [#18715](https://github.com/NousResearch/hermes-agent/issues/18715) (开放) | 支持远程 Hermes Agent 搭配本地工具执行 | 4 👍15 | 用户希望分布式部署：远程 agent 处理模型交互，本地执行工具。获 15 个赞，社区期望值高。 |

**分析**: 社区核心关注点集中在 **输出长度限制**、**编译兼容性**、**Skill 管理** 和 **异构部署** 上。`#7237` 虽已关闭但评论活跃说明用户对长文本场景的稳定性仍有顾虑；`#18715` 点赞数最高，反映分布式 agent 架构需求强烈。

---

## 5. Bug 与稳定性

按严重程度（P1 > P2 > P3）排列今日报告的 Bug，标注是否已有修复 PR：

| 严重等级 | Issue | 描述 | 已有 Fix PR |
|----------|-------|------|-------------|
| 🔴 **P1** | [#46675](https://github.com/NousResearch/hermes-agent/issues/46675) | Claude Max OAuth 请求因工具名 `mcp_` 下划线前缀被拒（HTTP 400） | 未开放 |
| 🔴 **P1** | [#40691](https://github.com/NousResearch/hermes-agent/issues/40691) | Telegram Gateway 在轮询冲突恢复后冻结，停止处理消息 | 未开放 |
| 🔴 **P1** | [#47002](https://github.com/NousResearch/hermes-agent/issues/47002) | v0.16.0 回归：SessionDB 在缺少 trigram tokenizer 的 SQLite 上崩溃 | 未开放 |
| 🟠 **P2** | [#46303](https://github.com/NousResearch/hermes-agent/issues/46303) | 并发会话内存/工作树交叉污染 | 未开放 |
| 🟠 **P2** | [#42682](https://github.com/NousResearch/hermes-agent/issues/42682) | 插件 curator 归档技能被错误标记为用户修改，阻挡更新 | 未开放 |
| 🟠 **P2** | [#29325](https://github.com/NousResearch/hermes-agent/issues/29325) | Telegram 轮询冲突导致 409 循环 | 未开放 |
| 🟠 **P2** | [#46917](https://github.com/NousResearch/hermes-agent/issues/46917) | Beings 无法响应空白（强制输出占位符文本） | 未开放 |
| 🟠 **P2** | [#46934](https://github.com/NousResearch/hermes-agent/issues/46934) | 僵尸会话 `resume_pending` 在网关重启后导致上下文泄漏 | 未开放 |
| 🟠 **P2** | [#46941](https://github.com/NousResearch/hermes-agent/issues/46941) | 飞书等消息平台终端命令被截断为单行 | 未开放 |
| 🟠 **P2** | [#46897](https://github.com/NousResearch/hermes-agent/issues/46897) | 后台审查误报“Skill created”，未验证技能是否真正可加载 | 未开放 |
| 🟠 **P2** | [#46979](https://github.com/NousResearch/hermes-agent/issues/46979) | v0.16.0 回归：桌面版 Run History 为空 | 未开放 |
| 🟠 **P2** | [#46961](https://github.com/NousResearch/hermes-agent/issues/46961) | 桌面底部栏模型切换无视觉反馈 | 未开放 |
| 🟢 **P3** | [#31246](https://github.com/NousResearch/hermes-agent/issues/31246) | MCP 服务器配置失败静默无提示（日志级别仅 DEBUG） | 未开放 |
| 🟢 **P3** | [#38855](https://github.com/NousResearch/hermes-agent/issues/38855) | 桌面工作目录设置对已记忆的工作区无效 | 未开放 |
| 🟢 **P3** | [#40480](https://github.com/NousResearch/hermes-agent/issues/40480) | 自定义提供者模型未在桌面下拉框显示 | 未开放 |
| 🟢 **P3** | [#46975](https://github.com/NousResearch/hermes-agent/issues/46975) | 桌面版累积僵尸后台进程（80+ 个） | 未开放 |

**今日已有修复 PR 的 Bug**:
- [#47007](https://github.com/NousResearch/hermes-agent/pull/47007) (P1) — Windows 上强制 SQLite 使用 DELETE 模式避免 WAL 损坏（未合并）。
- [#47012](https://github.com/NousResearch/hermes-agent/pull/47012) (P3) — 自定义端点 live catalog 未正确使用 base_url。
- [#47010](https://github.com/NousResearch/hermes-agent/pull/47010) (P2) — 桌面版允许对自定义端点手动输入模型名。
- [#47008](https://github.com/NousResearch/hermes-agent/pull/47008) (P2) — 将 `cdn.discordapp.com` 加入受信任的私有 IP 主机列表，修复 12 个测试失败。
- [#47013](https://github.com/NousResearch/hermes-agent/pull/47013) — Windows MCP 子进程弹窗问题（`CREATE_NO_WINDOW` 修复）。
- [#46985](https://github.com/NousResearch/hermes-agent/pull/46985) — Kanban worker 真实错误替代通用“protocol violation”。
- [#47005](https://github.com/NousResearch/hermes-agent/pull/47005) — Kanban diagnostics 区分已过时故障与活跃阻塞。

**总结**: 今日高优先级（P1）Bug 集中在 **OAuth 兼容性**、**Telegram 稳定性** 和 **SQLite 版本兼容性** 上，均为 v0.16.0 引入或暴露的回归问题。内核级 P1 修复 PR（SQLite WAL, session key 安全等）已提交待合。

---

## 6. 功能请求与路线图信号

以下用户提出的新功能需求较为突出，结合已有 PR 预测可能纳入下一版本：

| 需求 | 相关 Issue/PR | 社区热度 | 预测优先级 |
|------|---------------|----------|------------|
| **Skill 矢量路由/懒加载** | [#22620](https://github.com/NousResearch/hermes-agent/issues/22620) | 评论 5 | 中，长期痛点 |
| **远程 Agent + 本地工具执行** | [#18715](https://github.com/NousResearch/hermes-agent/issues/18715) | 👍15 | **高**，社区强烈需求，涉及架构变化 |
| **桌面字体大小设置** | [#46097](https://github.com/NousResearch/hermes-agent/issues/46097) | 👍2 | 低，但已有基础 UI 调整 |
| **中国用户网络访问优化** | [#46839](https://github.com/NousResearch/hermes-agent/issues/46839) | 评论 1 | 中，反映特定区域用户体验 |
| **自定义端点 onboarding 支持非 /v1/models 路径** | [#47006](https://github.com/NousResearch/hermes-agent/issues/47006) + PR[#47010](https://github.com/NousResearch/hermes-agent/pull/47010) | 新开 | **高**，已有 PR 待合 |
| **Beings 静默模式** | [#46917](https://github.com/NousResearch/hermes-agent/issues/46917) | P2 Bug 但本质是功能缺失 | 中，影响自定义 role 场景 |
| **Discord 消息静默通知模式** | PR[#47004](https://github.com/NousResearch/hermes-agent/pull/47004) | 新 PR | **高**，直接解决工具调用通知轰炸 |
| **MoA / Fusion 预设作为虚拟模型** | PR[#46081](https://github.com/NousResearch/hermes-agent/pull/46081), [#46094](https://github.com/NousResearch/hermes-agent/pull/46094) | 待合并 | **高**，完善模型选择体系 |
| **桌面 composer 模型选择器 & 每模型预设** | PR[#46959](https://github.com/NousResearch/hermes-agent/pull/46959) | 待合并 | **高**，UI 体验提升 |

**路线图信号**: 项目正在稳步推进 **多智能体编排（TaskGraph）**、**MoA/Fusion 虚拟化** 和 **中国区 OAuth 支持**，同时用户对 **分布式部署** 和 **Skill 效率** 的呼声最高，可能成为下一阶段重点。

---

## 7. 用户反馈摘要

从今日 Issues 评论中提炼真实用户声音：

1. **“输出长度限制截断是我最大的痛点——在 Telegram 上回复到一半就断了。”**（来自 #7237）  
   该问题虽已关闭，但评论显示用户对长文本场景的稳定性仍不满，期望更智能的续写或分段机制。

2. **“我想把 Hermes Agent 跑在远程服务器上，只让本机执行本地工具（比如文件操作、Docker）。”**（#18715）  
   强调分布式 agent 的实用场景：中央模型、本地安全执行。

3. **“Skill 列表现在已经 40+ 个，每次对话都要把全部 skill 描述塞进上下文，浪费了大量 token。”**（#22620）  
   用户明确要求基于 vector 的 skill 路由或懒加载，减少 token 开销。

4. **“每次切换桌面模型都没有反馈，我根本不知道切换成功了没有。”**（#46961）  
   对 UI 交互缺失的直接抱怨。

5. **“中国用户安装桌面版简直噩梦——GitHub 被墙，但安装程序不会用代理。”**（#46839）  
   建议在安装脚本中提供代理设置或镜像源。

6. **“Kanban 任务失败后只显示‘protocol violation’，完全不知道真实错误（如 boto3 认证失败）。”**（#46593，已关闭）  
   用户期望 worker 错误信息直接透传。

7. **“Windows 上每次启动 Hermes 都会弹出一堆 cmd 窗口，MCP 服务器太多了

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*