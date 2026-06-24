# OpenClaw 生态日报 2026-06-24

> Issues: 190 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-24 02:51 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，这是为您生成的 OpenClaw 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-06-24

## 今日速览

项目昨日保持高活跃度，共产生 190 条 Issue 更新和 500 条 PR 更新，显示社区交流和开发工作仍在密集进行。但值得注意的是，合并或关闭的 PR 仅占 PR 总数的 8%（40条），大量 PR 积压在待合并状态，合并效率有待提升。同时，P1 级别的严重 Bug 报告依然较多，主要集中在会话状态、消息丢失和数据一致性问题，表明项目正处于关键的稳定性打磨期。没有新版本发布，团队重心更偏向修复而非新功能。

## 版本发布

N/A（过去 24 小时内无新版本发布）

## 项目进展

- **长期 PR 推进至待审查状态**：数个重要的、修复核心会话机制的 PR 已准备好供维护者审查，标志着相关修复进入最后阶段。
    - [PR #88968](https://github.com/openclaw/openclaw/pull/88968) - `fix: prevent memory flush failure from aborting user reply (#85645)`。这是一个 P1 关键修复，防止内存刷新失败时错误地终止用户的正常回复，避免会话中断。
    - [PR #83988](https://github.com/openclaw/openclaw/pull/83988) - `fix(tts): defer text settlement for final-mode TTS to eliminate churn (#83511)`。修复 Telegram 频道在最终模式（`final mode`）TTS 下的文本“刷屏”问题，提升用户体验。
    - [PR #89045](https://github.com/openclaw/openclaw/pull/89045) - `fix: recover terminal session status on visible inbound turns`。修复群聊会话卡死在 `failed` 状态后静默丢弃所有消息的问题。
- **关键端口检测修复已合并**：[PR #94949](https://github.com/openclaw/openclaw/pull/94949) `fix(ports): route isPortBusy through checkPortInUse to catch IPv4-only occupants` 已被合并。此修复优化了端口占用检测逻辑，解决了可能因仅检测 IPv6 绑定而导致误判的问题，提高了系统启动的可靠性。
- **新功能/改进**：多个与“托管市场”（hosted marketplace）相关的 PR 被提交，如 `Add marketplace feed entries command` ([PR #96158](https://github.com/openclaw/openclaw/pull/96158)) 和 `Add marketplace feed refresh command` ([PR #96155](https://github.com/openclaw/openclaw/pull/96155))，显示项目正在积极构建插件市场基础设施。

## 社区热点

1.  **核心会话 SQLite 迁移** ([Issue #88838](https://github.com/openclaw/openclaw/issues/88838)): 评论数 35，为昨日最高。讨论焦点集中在通过“访问器接缝”（accessor seam）迁移核心会话/转录进程的当前状态、遇到的技术挑战及后续步骤。这是项目重构架构的关键一环，社区深度参与讨论，体现了对项目底层稳定性的高度关注。

2.  **iMessage 源回复延迟** ([Issue #96148](https://github.com/openclaw/openclaw/issues/96148)): 评论数 17。社区用户 `omarshahine` 提出了一个关于 iMessage 响应延迟的深入调查，并附带了已尝试的修复 PR 和相关证据。该 Issue 迅速成为热点，反映出用户对跨平台消息响应的实时性有较高期望，且此问题可能具有一定的复杂性和普遍性。

3.  **Anthropic “思考”签名问题** ([Issue #92201](https://github.com/openclaw/openclaw/issues/92201)): 评论数 14。用户报告了在嵌入式运行器中，实时流式传输的 Anthropic “思考”块的签名在回放时偶尔无效，导致错误恢复机制失效。该问题触及了与特定提供商（Anthropic）集成的核心数据序列化/反序列化稳定性，社区正在积极寻求可复现的复现步骤。

**分析**：社区今日的关注点高度集中。一是围绕**数据持久化和基础设施重构**（Issue #88838），这表明社区开发者对技术架构演进有深度参与意愿；二是围绕**消息传递的实时性、稳定性和跨平台一致性**（Issue #96148, #92201），这直接关系到用户的核心体验，是项目能否在复杂场景下可靠运行的关键。

## Bug 与稳定性

- **严重 (P1)**:
    - **Anthropic “思考”签名问题** ([Issue #92201](https://github.com/openclaw/openclaw/issues/92201)): 恢复包装器因错误信息泛化而无法触发。**无关联 Fix PR**。
    - **紧凑超时问题** ([Issue #92043](https://github.com/openclaw/openclaw/issues/92043)): 180秒紧凑超时为全局墙钟，导致合法长任务每次失败。**无关联 Fix PR**。
    - **子代理完成投递失败** ([Issue #92076](https://github.com/openclaw/openclaw/issues/92076)): 当请求者会话不活跃且转录锁定时，子代理结果无法投递。**无关联 Fix PR**。
    - **自动更新导致陈旧模块** ([Issue #85844](https://github.com/openclaw/openclaw/issues/85844)): 运行中的网关使用旧有哈希包导入。**无关联 Fix PR**。
    - **卡住会话恢复误杀长任务** ([Issue #88870](https://github.com/openclaw/openclaw/issues/88870)): 恢复机制错误地终止了仍在工作的长时运行代理。**有关联开放 PR** ([PR #96260](https://github.com/openclaw/openclaw/pull/96260))。
    - **.jsonl.lock 文件未释放** ([Issue #95833](https://github.com/openclaw/openclaw/issues/95833)): 子代理中止后未释放锁文件，永久性破坏会话。**无关联 Fix PR**。

- **中等 (P2)**:
    - **DeepSeek V4 Flash 不完整响应** ([Issue #88657](https://github.com/openclaw/openclaw/issues/88657)): 5.27/28版本中出现不完整会话。**无关联 Fix PR**。
    - **exec 命令无法访问私有LAN** ([Issue #94032](https://github.com/openclaw/openclaw/issues/94032)): `exec` 命令在 Mac mini 上无法访问私有局域网主机。**无关联 Fix PR**。
    - **Ollama 远程提供商流式传输问题** ([Issue #94251](https://github.com/openclaw/openclaw/issues/94251)): 聊天会话中流式传输卡在 `model_call:started`。**无关联 Fix PR**。
    - **历史 thinking 块破坏工具使用会话** ([Issue #94228](https://github.com/openclaw/openclaw/issues/94228)): 重放历史 thinking 块导致原生 Anthropic 路径出现 400 错误。**无关联 Fix PR**。
    - **DeepSeek 缓存命中率暴跌** ([Issue #94518](https://github.com/openclaw/openclaw/issues/94518)): 6.x 升级后缓存命中率低于 10%。**有关联开放 PR**。

- **近期修复 (已关闭/合并)**:
    - Cron 调度器污染全局状态 ([Issue #90991](https://github.com/openclaw/openclaw/issues/90991)) - 已关闭。
    - Windows 上 ACPX 运行时 EINVAL 错误 ([Issue #93465](https://github.com/openclaw/openclaw/issues/93465)) - 已关闭。
    - NVIDIA Build 提供商流式传输中断 ([Issue #95760](https://github.com/openclaw/openclaw/issues/95760)) - 已关闭。

## 功能请求与路线图信号

- **持久化和易用性**：多个功能请求指向改善会话管理和数据持久化。
    - [Issue #42840](https://github.com/openclaw/openclaw/issues/42840) - 要求在控制 UI 支持 MathJax **LaTeX 渲染**。虽然已提交两周，但获得 7 个 👍，需求明确。
    - [Issue #49931](https://github.com/openclaw/openclaw/issues/49931) - 要求为 `exec` 工具提供**可配置的 Shell**，解决 Windows 上 PowerShell 的痛点。
    - [Issue #93422](https://github.com/openclaw/openclaw/issues/93422) - 要求为 WebChat 添加 `/label` 命令来**命名会话**，方便管理多个会话。获得 2 个 👍，且有关联开放 PR，有望在下一版本或小版本更新中实现。

- **平台与集成**：增强与其他平台和服务的集成能力。
    - [Issue #88032](https://github.com/openclaw/openclaw/issues/88032) - 要求将 Telegram 的引用/回复上下文作为**一等持久化合约**，而不仅仅是运行时补丁。
    - [Issue #91945](https://github.com/openclaw/openclaw/issues/91945) - 要求将 Cloudflare AI Gateway 升级到较新的 REST API。
    - [Issue #96156](https://github.com/openclaw/openclaw/issues/96156) - 允许**MCP 服务器作为紧凑提供商**，这代表了一个强大的扩展方向。

- **安全与管理**：
    - [Issue #71712](https://github.com/openclaw/openclaw/issues/71712) - 提议建立**面向代理的调度 API**，并带有不可伪造的起源证明。
    - [Issue #93068](https://github.com/openclaw/openclaw/issues/93068) - 要求支持**全局 SSRF 策略配置**，统一管理私网/特殊用途 IP 范围的访问。

## 用户反馈摘要

- **关于 iMessage 延迟**：用户 `omarshahine` 在 [Issue #96148](https://github.com/openclaw/openclaw/issues/96148) 中提供了详尽的调查，包括已尝试的修复 PR，但问题依旧。这说明 iMessage 源的延迟问题根深蒂固，可能需要更深层次的架构调整，用户反馈非常专业且具有建设性。
- **关于 Anthropic 签名问题**：用户 `CarlCapital` 在 [Issue #92201](https://github.com/openclaw/openclaw/issues/92201) 中清晰地描述了问题现象和影响，指出“错误文本泛化”导致自动恢复机制失效。这是一个典型的“软件防御性编程失败”案例，用户希望系统能提供更精确的错误分类，而不是将所有错误模糊处理，从而让恢复逻辑能正确触发。
- **关于配置迁移问题**：用户 `cattyclaw-bot` 在 [Issue #95136](https://github.com/openclaw/openclaw/issues/95136) 中指出，当模型提供商 ID 被移除或重命名（如 `openai-codex` -> `openai`）时，OAuth 配置会被静默孤立，导致用户凭据失效且无任何警告。这反映了用户对**平滑升级和配置兼容性**的强烈需求。

## 待处理积压

以下为长期未响应或缺少关键信息（如 `needs-maintainer-review`，`needs-info`）的重要问题，提醒维护者关注：

- **安全**：[Issue #73910](https://github.com/openclaw/openclaw/issues/73910) P1: BUG: OpenClaw管理的Codex ACP使用隔离的CODEX_HOME且无auth桥接。需要维护者审查。
- **Bug**：[Issue #46548](https://github.com/openclaw/openclaw/issues/46548) P2: 工具错误信息未显示失败原因。需要产品决策。
- **功能请求**：[Issue #42840](https://github.com/openclaw/openclaw/issues/42840) P2: 添加MathJax支持。需要产品决策和维护者审查。
- **Bug**：[Issue #49931](https://github.com/openclaw/openclaw/issues/49931) P2: 可配置的Shell。需要维护者审查和安全审查。
- **Bug**：[Issue #72021](https://github.com/openclaw/openclaw/issues/72021) P2: 短期记忆提升中，signalCount混淆了日/会话信号。需要产品决策和维护者审查。
- **Bug**：[Issue #38520](https://github.com/openclaw/openclaw/issues/38520) P2: 紧凑前代理通知。需要产品决策和安全审查。
- **Bug**：[Issue #68780](https://github.com/openclaw/openclaw/issues/68780) P3: 插件允许列表为空的警告对新用户不友好。需要产品决策和安全审查。

---

## 横向生态对比

好的，作为资深技术分析师，我为您梳理了2026-06-24的个人AI助手与自主智能体开源生态全景，并聚焦于OpenClaw与Hermes Agent两个核心项目进行横向对比。

---

### 1. 生态全景

当前，个人AI助手与自主智能体开源生态正处在**从“功能可用”向“生产可靠”过渡的深水区**。一方面，以OpenClaw和Hermes Agent为代表的项目在基础能力（如多模态、工具调用、平台集成）上已趋于完善，社区热情高涨；另一方面，**会话状态管理、数据一致性、Token成本优化及跨平台稳定性**成为阻碍项目大规模落地的共性“拦路虎”。社区讨论的焦点正从“如何实现某个炫酷功能”转向“如何让系统在复杂场景下稳定、高效、低成本运行”，这表明生态正在走向成熟，实用主义和工程化思维正在主导技术演进。

### 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PR 更新数 | 合并/关闭率 | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 190 | 500 | 8% (PR) | 无 | **质量巩固期**：高活跃，但社区热情与合并效率不匹配，P1 Bug积压严重，需加快修复节奏。 |
| **Hermes Agent** | 50 | 50 | 12% (PR) | 无 | **密集开发期**：活跃度均衡，社区焦点清晰（Token优化、多代理编排），合并速度略优于OpenClaw，但同样存在关键Bug和长期未合入的PR。 |

### 3. OpenClaw 在生态中的定位

**优势：**
*   **社区规模与成熟度领先**：从Issue和PR数量上看，OpenClaw的社区活跃度是Hermes Agent的3-4倍，已形成庞大的贡献者和用户基础，生态影响力更大。
*   **基础设施深度扎实**：项目正在进行的核心会话SQLite迁移（Issue #88838）及长期维护的架构重构，显示了其支撑复杂生产环境的决心和技术深度，这是许多同类项目尚未涉足的领域。
*   **稳定性问题暴露充分**：大量P1 Bug的公开报告（会话中断、锁文件问题、数据不一致），虽然短期内看起来是劣势，但侧面反映了该项目已被部署在真实、严苛的环境中，问题暴露更全面，修复后也将更具鲁棒性。

**劣势：**
*   **PR合并效率是最大瓶颈**：8%的合并率远低于健康的开源项目，大量待审查的PR（尤其是核心修复）会导致社区贡献者热情受挫，并延迟关键问题的解决。这可能与过于复杂/严格的审查流程或维护者资源不足有关。
*   **创新速度相对保守**：当前聚焦于修复和打磨，而无重大新版本发布，相比Hermes Agent在探索“通用ACP客户端”等前瞻性特性上，显得较为保守。

### 4. 共同关注的技术方向

两个项目虽路径不同，但在以下领域形成了高度共识的技术挑战：

1.  **核心会话/状态管理的可靠性与一致性** (OpenClaw, Hermes Agent)
    *   **具体诉求**：OpenClaw的SQLite迁移、卡死会话恢复、`.jsonl.lock`文件释放问题，与Hermes Agent的密码脱敏导致工具调用失败、会话恢复机制误杀长任务等问题，本质均是数据持久化、状态转移和一致性保障的挑战。
    *   **影响**：这是项目从“玩具”走向“工具”必须跨过的门槛，直接影响用户对助手“记忆”和“任务连续性”的信心。

2.  **Token开销优化与成本控制** (Hermes Agent, OpenClaw潜在需求)
    *   **具体诉求**：Hermes Agent社区对**懒加载工具模式**的强烈呼吁（Issue #6839, #4379），将Token浪费的问题数据化（73%是固定开销），公开向整个生态发出了一个明确的信号：AI助手的商业化或深度使用，必须解决“每句话都要把所有功能定义塞进上下文”的低效问题。
    *   **分析**：OpenClaw虽未直接热论此话题，但作为同样支持海量工具集的项目，Token开销问题同样是其大规模部署的隐形障碍。

3.  **跨平台消息与桌面端的稳定性** (OpenClaw, Hermes Agent)
    *   **具体诉求**：OpenClaw的iMessage回复延迟、Telegram TTS刷屏问题，与Hermes Agent的Telegram无限消息循环、Windows控制台无响应、桌面版WebSocket容错问题，共同指向了在多种消息平台和操作系统上提供一致、稳定体验的工程挑战。

4.  **多代理/多实体编排的架构探索** (Hermes Agent, OpenClaw)
    *   **具体诉求**：Hermes Agent社区积极讨论**通用ACP客户端**（Issue #5257）以编排不同智能体。OpenClaw通过“托管市场”和新平台路由能力（PR #51635），为不同Agent Profile分配不同平台，体现了类似的趋势。
    *   **趋势**：未来AI助手不再是孤岛，而是一个可以调度、协调其他AI实体的“元调度器”。

### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **功能侧重** | **平台型、全功能聚合器**。集成广泛的消息/模型提供商，强调在复杂网络环境中稳定运行。由插件市场驱动的生态扩展中心。 | **开发型、智能体核心**。更强调智能体推理核心的优化（Token效率、工具Schema设计），以及作为ACP协议中心调度其他编码智能体的能力。 |
| **目标用户** | **高级用户、系统管理员、企业部署者**。需要接入大量服务，对系统稳定性、配置灵活性有极高要求，愿意参与深度技术讨论。 | **AI Agent开发者、效率极客、多代理工作流构建者**。关注Agent核心效率与延迟，倾向于构建自动化、去中心化的AI工作流。 |
| **技术架构** | **重型、集成化、工程导向**。项目中正在进行SQLite迁移、端口检测优化、全局SSRF策略等复杂基础设施改造。 | **模块化、协议驱动、性能导向**。通过ACP协议、懒加载Schema、可配置Shell等设计，追求模块化、高性能和低开销。 |
| **核心挑战** | **稳定压倒一切**。大量P1 Bug和低合并率表明，如何在保持高活跃度、高功能性的同时，确保代码质量和项目航向是其最大挑战。 | **社区增长与功能深度的平衡**。虽然社区热度和创新性强，但在规模上远不及OpenClaw，需要吸引更多开发者构建更强大的工具生态。 |

### 6. 社区热度与成熟度

*   **第一梯队（高活跃，质量巩固期）**：
    *   **OpenClaw**：社区规模最大，讨论最激烈。但低合并率和管理层积压的Bug表明项目可能处于“成长的烦恼”中，正经历从高速开发到质量维稳的阵痛。**适合愿意参与核心架构演进、解决硬核工程问题的贡献者。**
*   **第二梯队（快速迭代，功能探索期）**：
    *   **Hermes Agent**：社区规模较小，但讨论内容前瞻性强，焦点集中。合并效率略高，核心功能（如Token优化、多代理）正在快速演进。**适合对AI Agent核心优化、协议设计有兴趣，且乐于尝试新范式的开发者。**

### 7. 值得关注的趋势信号

1.  **“MoE（混合专家）”思维在工具层萌芽**：
    *   **来源**：Hermes Agent社区对“懒加载工具”的强烈需求。这本质上是将“大模型”领域的MoE思路应用到了Agent的工具层：根据当前任务动态选择注入最相关的工具Schema，而非“一股脑”全塞进去。这将是下一代AI Agent降低延迟、控制成本的**关键架构设计**。

2.  **从“智能体”到“智能体网络”**：
    *   **来源**：Hermes Agent的“通用ACP客户端”（Issue #5257）和OpenClaw的MCP服务器作为提供商（PR #96156）。这表明开发者不再满足于单个智能体的能力，而是追求构建一个由不同AI专家（如Codex、Claude Code、Hermes Agent自身）组成的协作网络。**“编排层”将成为新的竞争高地。**

3.  **数据安全与隐私是永不过时的“技术债”**：
    *   **来源**：两个项目共同面临的问题，如Hermes Agent的密码脱敏导致下游工具调用失败（安全vs.稳态的冲突），OpenClaw的SSRF策略配置。这些问题的解决方案将直接定义Agent的信任边界和安全性，是**从个人玩具走向企业级应用的必要条件**。

**对开发者的建议**：
*   如果你需要一个**功能全面、集成丰富、能够处理复杂生产环境**的个人AI助手，请重点关注**OpenClaw**，但需做好与PR合并周期长、处理偶发性Bug共存的准备。
*   如果你是**Agent效率的偏执狂、或是想构建下一代多Agent协作系统的架构师**，**Hermes Agent**的社区和技术方向更值得你研究、贡献或借鉴，尤其是在Token优化和ACP协议方面。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，这是根据您提供的 Hermes Agent 项目数据生成的 2026-06-24 项目动态日报。

---

# Hermes Agent 项目日报 | 2026-06-24

## 1. 今日速览

过去 24 小时内，Hermes Agent 项目保持高度活跃，共处理了 50 条 Issue 更新和 50 条 PR 更新，但合并/关闭率较低（约 12%），表明项目处于高强度开发与代码审查阶段。社区讨论主要集中在两大核心问题上：通过**懒加载工具模式**解决高昂的 Token 开销，以及推动**通用 ACP 客户端**以实现多智能体编排。同时，多个 P1/P2 级别的 Bug 报告（涉及凭证丢失、Windows 兼容性、Telegram 消息循环等）正在被积极追踪，项目维护者针对部分严重问题已提交修复 PR。整体项目健康度良好，但需加快 PR 审查与合并速度以缓解社区等待焦虑。

## 2. 版本发布

无

## 3. 项目进展 (今日合并/关闭的 PR 与 Issue)

今日项目无明显进展，无任何 Pull Request 被合并，仅少数 Issue 被关闭。这表明项目目前处于功能开发与 Bug 修复的密集提交期，维护者的主要精力集中在代码审查和架构决策上，而非快速合并。

- **关键 Issue 修复确认：**
    - [#51587 【已关闭】Bug：MCP 服务器工具连接成功但未出现在 Agent 工具集中](https://github.com/nousresearch/hermes-agent/issues/51587) (P1)：这是一个影响 MCP 协议集成的严重问题，已被标记为“已关闭”并需要复现。该 Issue 的关闭可能意味着问题已被定位或已提交修复，但尚未合入主分支。

## 4. 社区热点

本周社区讨论的焦点高度集中在两个方向：**降低 Token 开销** 和 **扩展多代理协作能力**。

1.  **[#6839] Feature: Lazy Tool Schema Loading (懒加载工具模式)**  [26 评论, 14 赞]
    [链接](https://github.com/nousresearch/hermes-agent/issues/6839)
    这是近期最受关注的功能请求之一。用户指出，每次 API 调用都注入多达 50+ 个工具的全部 Schema（消耗约 3500-5000 tokens），在需要多轮工具调用的复杂任务中，浪费巨大。社区强烈要求实现“两阶段注入”或“懒加载”机制，仅在代理实际需要调用时才注入目标工具的 Schema。这直接关联到提高推理效率、降低成本。

2.  **[#5257] feat: Generalized ACP client for multi-agent CLI orchestration (通用 ACP 客户端)**  [11 评论, 16 赞]
    [链接](https://github.com/nousresearch/hermes-agent/issues/5257)
    此 Issue 描绘了 Hermes Agent 作为“元调度器”的宏大蓝图。当前 Hermes 仅作为 ACP 服务器供 IDE 集成，或实现了一个针对 Copilot 的专用客户端。社区希望将其推广为通用的 ACP 客户端，使其能编排 Claude Code、GPT-Codex 等任何支持 ACP 的编码代理。这反映了用户对构建灵活、去中心化的多智能体工作流的强烈需求。

3.  **[#4379] Token overhead analysis: 73% of each API call is fixed overhead (Token 开销分析)**  [15 评论]
    [链接](https://github.com/nousresearch/hermes-agent/issues/4379)
    这份基于 v0.6.0 的监控报告，用数据强有力地支撑了 Issue #6839 的论点。报告显示，每次 API 调用中高达 73% 的 Token 是固定开销（约 13.9K Tokens），包括系统提示、工具定义和对话历史。这不仅是成本问题，更影响了本地模型的运行速度。该报告是社区推动性能优化的核心依据。

## 5. Bug 与稳定性 (按严重程度排列)

今日报告的 Bug 主要集中在上层基础设施（凭证安全、网关兼容性）和特定平台（Telegram、Windows）的稳定性上。

- **P1 (严重)**
    - **[#19566] OpenAI-Codex 凭证池在轮换期间会丢失新添加的凭证** | [已报告4天] [Issue](https://github.com/nousresearch/hermes-agent/issues/19566)
        凭证丢失或导致身份验证失败，属于严重安全与稳定性问题。目前尚未有明确关联的 Fix PR。
    - **[#43083] 密码被 `***` 替换后模型读取历史导致工具调用失败** | [已报告15天] [Issue](https://github.com/nousresearch/hermes-agent/issues/43083)
        这是一个重要的安全 Bug 执行正确性 Bug。密码被脱敏后存储，但模型在后续对话中读取历史时因无法看到原始密码，导致需要凭据的第二次工具调用失败。根因在于脱敏逻辑的实现方式。目前已有开发者提交了相关的分析评论，但无公开 Fix PR。
    - **[#48648] Telegram 网关在超长流式回复时陷入无限消息重复循环** | [已报告6天] [Issue](https://github.com/nousresearch/hermes-agent/issues/48648)
        严重影响 Telegram 用户体验，已明确根因为 `gateway` 组件的溢出处理逻辑缺陷。
    - **[#51579] Docker 环境启动 `gateway run` 会覆盖 `.env` 文件** | [已报告1天] [Issue](https://github.com/nousresearch/hermes-agent/issues/51579)
        重大回归问题，每次容器启动都会重写 `.env` 文件，导致 Telegram 配置丢失。严重阻碍了 Hermes Agent 在 Docker 环境下的部署。

- **P2 (重要)**
    - **[#38387] Windows 网关计划任务会留下无响应的空白控制台窗口** | [已报告21天] [Issue](https://github.com/nousresearch/hermes-agent/issues/38387)
        影响 Windows 平台用户体验，网关服务无法作为可靠的系统服务运行。目前有相关 PR ([PR #47569]) 待合并。
    - **[#51636] `terminal.working_dir` 配置项在新建会话时无效** | [今日报告] [Issue](https://github.com/nousresearch/hermes-agent/issues/51636)
        用户配置的终端工作目录被忽略，不符合配置预期。
    - **[#49787] Desktop 应用每次启动都提示重新配置，即使配置有效** | [已报告4天] [Issue](https://github.com/nousresearch/hermes-agent/issues/49787)
        影响桌面版用户体验，macOS 用户反馈强烈。
    - **[#50005] Desktop 在 WebSocket 断开后完全无响应，无离线模式** | [已报告3天] [Issue](https://github.com/nousresearch/hermes-agent/issues/50005)
        桌面端缺乏容错机制，WebSocket 断开即陷入不可用状态。

- **P3 (次要)**
    - **[#35357] Tirith 审批门禁绕过非 Shell 工具 (如 `send_message`, `write_file`)** | [已报告25天] [Issue](https://github.com/nousresearch/hermes-agent/issues/35357)
        安全机制设计缺陷，系统只对终端命令进行安全审批，而 `send_message`、`write_file` 等工具可绕过人类监督，存在安全隐患。

## 6. 功能请求与路线图信号

结合高赞 Issue 和开放 PR，以下功能有较大概率被纳入下一版本规划：

-   **高性能 & 低成本方向：**
    - **懒加载工具 Schema (Lazy Tool Schema)** (Issue #6839, #4379)：是目前社区最迫切的需求。已有相关思路讨论，但尚无具体实现 PR。这是提升性能和降低成本的最具影响力的特性。
-   **多代理编排方向：**
    - **通用 ACP 客户端** (Issue #5257)：该项目因高赞和高讨论度，已成为路线图上的标志性功能。如能实现，将把 Hermes Agent 从“智能体”提升至“智能体平台”。
-   **用户体验 & 平台支持：**
    - **Zulip 集成** (PR #3335)：已开放近三个月，若合并将为团队协作场景提供新选择。
    - **Vertex AI 支持** (PR #8427)：已开放两个半月，是重要企业级模型接入功能。
    - **新平台路由能力** (PR #51635)：实现了 WhatsApp 聊天到不同 Agent Profile 的路由，显示了在统一网关下实现多实体管理的趋势。
    - **终端订阅查看功能** (PR #51639)：优化用户的计费信息交互体验。
    - **对话/会话中添加转账及账单功能** (PR #51634, Issue #51607)：社区对于在会话中切换模型后，账单和 token 统计需要准确追踪的诉求日益强烈，这个功能正在变得重要。
-   **自我演进化：**
    - **角色、技能、脚本的选择决策框架** (PR #41792)：一个“元功能”，帮助开发者和代理自身更好地决定何时使用技能、何时使用脚本、何时使用工具，表明了项目对自身工具生态的深度思考。

## 7. 用户反馈摘要

来自 Issue 评论的真实用户反馈：

-   **关于 Token 浪费：** “每次调用都注入 50+ 个工具的 Schema，消耗 3500-5000 tokens，这太浪费了。对于本地模型，这尤其痛苦。”（源自 Issue #6839）
-   **关于编排能力：** “我们希望 Hermes 能成为我们的‘副驾驶’来调度‘Codex’，但 Hermes 只能做服务器或调度 Copilot。我们需要一个通用的 ACP 客户端来调度任何 ACP 智能体。”（源自 Issue #5257）
-   **关于 MCP 集成体验：** “MCP 服务器连接成功了，工具也启用了，但会话里就是找不到。Hermes 说这些工具‘不存在’。这到底是怎么回事？”（源自 Issue #51587，后已关闭）
-   **关于密码安全功能影响流程：** “密码被 *** 替换，模型看不到密码，于是第二次需要密码的工具调用就失败了。这功能虽然是为了安全，但把我卡住了。”（源自 Issue #43083）
-   **关于安全审查的漏洞：** “我写文件、发消息完全没有审批环节。Tirith 只审查终端命令，这感觉有严重的安全漏洞。”（源自 Issue #35357）
-   **关于桌面版体验：** “每次打开应用都让我重新配置，这是要干嘛？我的配置文件明明都还在。”（源自 Issue #49787）

## 8. 待处理积压

以下为长期待响应的关键 Issue/PR，可能阻碍项目进展，需维护者关注：

1.  **关键安全/稳定性 Bug **
    -   **Issue #19566 (OpenAI-Codex 凭证丢失)**：严重问题已持续近 2 个月，影响大量用户，存在安全风险。**需要尽快确认根因并安排修复。**
    -   **Issue #35357 (Tirith 安全门禁绕过)**：安全设计缺陷，已开放近 1 个月，削弱了系统的安全承诺。

2.  **长期开放的里程碑级 PR**
    -   **PR #3335 (Zulip 集成)**：已开放近 3 个月，且是社区呼声很高的功能，维护者应评估是否将其纳入正式版本。
    -   **PR #8427 (Vertex AI 支持)**：已开放 2 个多月，引入企业级模型接入对项目商业化至关重要。
    -   **PR #22648 (Ollama Cloud 支持)**：已开放近 1.5 个月，涉及重大架构变更（从硬编码转向插件化），维护者应给出明确评审意见。

3.  **文档与学习路径**
    -   **PR #41792 (决定框架)**：虽非核心代码，但为社区贡献者提供了清晰的贡献指引，长期搁置会影响社区贡献质量。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*