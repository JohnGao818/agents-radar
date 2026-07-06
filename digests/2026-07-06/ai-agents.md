# OpenClaw 生态日报 2026-07-06

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-07-06 02:47 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为AI智能体与个人AI助手领域的开源项目分析师，我将根据您提供的OpenClaw项目数据进行整理和分析，为您呈现2026年7月6日的项目日报。

---

## OpenClaw 项目日报 — 2026年7月6日

### 1. 今日速览

今日OpenClaw项目社区活跃度极高，过去24小时内创建和更新了大量议题（500条）和拉取请求（500条），并发布了新的Beta版本。尽管社区讨论热烈，功能请求和Bug报告层出不穷，但项目维护者也在积极审查并合并了大量PR（328条），显示出旺盛的迭代速度。当前社区关注的核心痛点集中在跨平台支持、AI模型的稳定性与幻觉问题、以及安全与沙箱机制的完善上。

### 2. 版本发布

**新版本：[v2026.7.1-beta.2](https://github.com/openclaw/openclaw/releases/tag/v2026.7.1-beta.2)**

这是针对即将发布的2026年7月稳定版的第二个Beta版本。

- **主要内容：**
    -   **OpenAI GPT-5.6 支持：** OpenClaw现在在目录、能力和运行时选择路径中识别并支持最新的GPT-5.6模型系列。 (PR [#98333](https://github.com/openclaw/openclaw/pull/98333)，感谢 @steipete-oai)
    -   **外部工具挂载 (External harness attachment)：** 新增 `openclaw attach` 命令，允许用户将一个外部执行环境挂载到一个已存在的Gateway会话上。

- **破坏性变更与迁移注意事项：** 未在数据中提及，建议查看完整的Release Notes以确保平稳升级。

### 3. 项目进展

过去24小时内，共有328个PR被合并或关闭，项目迭代速度很快。以下是几项关键进展：

- **改进自动回复上下文质量：** 由@gorkem2020提交的PR [#100366](https://github.com/openclaw/openclaw/pull/100366) 已进入维护者审查阶段。该PR将自动回复功能中“自上次回复以来的聊天历史”从原始JSON格式改为了更易读的逐条消息叙述形式，有望显著提升AI对对话上下文的理解能力。
- **完善Android平台连接稳定性：** 由@ly85206559提交的PR [#100347](https://github.com/openclaw/openclaw/pull/100347) 已就绪，等待维护者审查。该PR为Android客户端增加了网络恢复后自动重连Gateway的能力，减少了节点会话的离线时间。
- **基础架构与开发者体验改进：** 社区提交了多个旨在提升代码健壮性和开发者体验的 PR，例如修复 TranscriptsStore 流读取错误 ([#100524](https://github.com/openclaw/openclaw/pull/100524))、降低插件钩子安装失败时的日志噪音 ([#100554](https://github.com/openclaw/openclaw/pull/100554)) 等。

### 4. 社区热点

过去24小时讨论最为活跃的议题反映了社区对平台扩展性和AI安全的核心关切。

- **跨平台应用支持：** [Issue #75](https://github.com/openclaw/openclaw/issues/75) - “Linux/Windows Clawdbot Apps” 以110条评论高居榜首。用户对官方提供Linux和Windows原生应用的需求非常强烈，期望获得与macOS一致的体验。这是当前项目最受关注的功能请求，已被标记为P2优先级和“寻求帮助”状态。
- **解决AI幻觉和错误响应：** [Issue #92201](https://github.com/openclaw/openclaw/issues/92201) - “Embedded runner: freshly streamed thinking signatures intermittently invalid on replay...” 引起了广泛讨论。此问题深入探讨了在使用Anthropic模型时，由流式处理和签名验证引发的复杂Bug，导致AI回复无法正确重现。这凸显了用户对AI行为一致性和可靠性的高要求。
- **发布与代码质量：** [Issue #98416](https://github.com/openclaw/openclaw/issues/98416) - “[Bug] v2026.6.11 published dist missing reentrancy guard...” 获得16条评论和5个赞。用户报告实际发布的版本缺少了关键的重入锁修复代码，导致回复会话初始化冲突。这反映出用户对版本发布质量的敏感性，以及社区对代码审查流程的高度关注。

### 5. Bug 与稳定性

今日报告了多个重要的Bug和回归问题，部分已经有对应的修复PR。

**P0 (最高优先级)**
- **Android APK发布问题：** [Issue #9443](https://github.com/openclaw/openclaw/issues/9443) 要求提供预编译的Android APK下载。这直接影响到普通用户的使用门槛，被标记为“UX发布阻塞器”。
- **文档超前于发布：** [Issue #48920](https://github.com/openclaw/openclaw/issues/48920) 报告了在线文档中存在但当前稳定版(2026.3.13)中并未实现的功能配置（如`IsolatedSessions`），这会导致用户配置失败并产生困惑。

**P1 (高优先级)**
- **发布缺失关键修复：** [Issue #98416](https://github.com/openclaw/openclaw/issues/98416)，如上文所述，已发布的v2026.6.11版本遗漏了重要的`reentrant`修复。
- **会话状态问题：** [Issue #48003](https://github.com/openclaw/openclaw/issues/48003) 讨论“Steer模式”无法在对话轮次中及时注入消息。另一问题 [Issue #69118](https://github.com/openclaw/openclaw/issues/69118) 报告群组频道中Claude CLI每轮对话都会重置会话。这些问题严重影响用户体验，特别是多用户协作场景。
- **安全问题：** [Issue #51396](https://github.com/openclaw/openclaw/issues/51396) 报告了一个回归Bug，`clearUnboundScopes`会错误地剥离通过Token认证的后端客户端的操作者权限，是一个潜在的安全和功能阻断问题。

**已有修复PR的Bug：**
- **[#96704](https://github.com/openclaw/openclaw/issues/96704) 管理浏览器Cookies不持久化：** 此P1级别的Bug已有关联的讨论，但修复PR尚未明确。
- **[#99021](https://github.com/openclaw/openclaw/issues/99021) Discord附件大于10MB丢失：** 此问题已有修复PR [#99053](https://github.com/openclaw/openclaw/pull/99053)，通过裁剪过大附件来解决HTTP 413错误，目前正在等待维护者审查。

### 6. 功能请求与路线图信号

以下功能需求呼声较高，结合已有PR，可判断项目未来的演进方向。

- **更安全、更可控的AI平台：**
    - **[Issue #7707](https://github.com/openclaw/openclaw/issues/7707) 内存信任标签：** 建议根据信息来源（用户、网络、第三方技能）为记忆内容打上信任标签，以防止记忆投毒攻击。
    - **[Issue #10659](https://github.com/openclaw/openclaw/issues/10659) 屏蔽密钥（Masked Secrets）：** 让Agent能使用API密钥但无法看到其明文，防止泄露。
    - **[Issue #7722](https://github.com/openclaw/openclaw/issues/7722) 文件系统沙箱配置：** 用户希望精确控制Agent可以访问的文件系统路径，这是企业级部署的关键需求。
- **提升平台生态与扩展性：**
    - **[Issue #50090](https://github.com/openclaw/openclaw/issues/50090) 社区技能开发与ClawHub：** 这是构建OpenClaw应用生态的核心，用户期待更成熟的技能发布、共享和安装机制。
    - **[Issue #10687](https://github.com/openclaw/openclaw/issues/10687) 动态模型发现：** 用户希望OpenClaw能动态获取OpenRouter等快速更新的模型提供商列表，而不是依赖静态的本地生成目录。
- **高质量的多智能体协作：**
    - **[Issue #35203](https://github.com/openclaw/openclaw/issues/35203) [RFC] 多智能体协作增强：** 提议通过能力分析、共享黑板、分层内存和Token成本治理来解决当前多Agent协作中信息孤岛和任务委派模糊等问题。
    - **[Issue #60572](https://github.com/openclaw/openclaw/issues/60572) 多槽位内存架构：** 建议将单一内存槽位拆分为多个专用内存槽位（如短期、长期、工作记忆），以支持更复杂的记忆策略。

### 7. 用户反馈摘要

从今日活跃的Issues中，可以提炼出以下用户声音：

- **对跨平台支持的强烈渴望：** “We have apps for macOS, iOS and Android... Linux and Windows are missing.” ([#75](https://github.com/openclaw/openclaw/issues/75)) 这是社区最统一且最迫切的呼声。
- **对AI可靠性的不满与担忧：**
    - “An agent turn can end with a final user-facing message... even though no background action was actually started.” ([#58450](https://github.com/openclaw/openclaw/issues/58450)) 用户对AI“虚假承诺”的行为表示困扰。
    - “Normal tool text outputs can degrade to `(see attached image)` placeholders...” ([#96857](https://github.com/openclaw/openclaw/issues/96857)) 用户反馈普通文本输出被替换为无用图片占位符，使Agent“失明”。
- **对系统稳定性的严格审视：** “Gateway memory leak: 389MB → 14.7GB over 4 days” ([#54155](https://github.com/openclaw/openclaw/issues/54155))。用户报告了严重的内存泄漏问题，表明其对生产环境下的性能和稳定性非常关注。

### 8. 待处理积压

以下议题长期未得到维护者的明确处理或决策回应，可能会影响社区贡献者的积极性。

- **关键功能请求缺乏决策：**
    - **[Issue #7707](https://github.com/openclaw/openclaw/issues/7707) 内存信任标签：** 自2月提出以来，已获得14条讨论，但状态仍为“需要产品决策”。
    - **[Issue #10659](https://github.com/openclaw/openclaw/issues/10659) 屏蔽密钥：** 同样自2月提出，讨论热烈，但仍未进入开发阶段。
    - **[Issue #6615](https://github.com/openclaw/openclaw/issues/6615) 执行审批黑名单：** 这是一项用户基础很大的安全功能，自2月提出，有7个赞，但状态仍是“需要产品决策”。
- **长期未解决的高优先级Bug：**
    - **[Issue #29387](https://github.com/openclaw/openclaw/issues/29387) 引导文件 (Bootstrap files) 被静默忽略：** 这是一个P1级别的Bug，自2月底报告，会阻止用户自定义Agent行为，但至今未修复。
    - **[Issue #51429](https://github.com/openclaw/openclaw/issues/51429) 开发者的工作路径被硬编码：** 这是一个非常能体现维护流程疏忽的问题，一个开发者的个人路径被硬编码并合并发布，导致许多用户工作区被错误创建。虽然有趣，但也反映了潜在的代码审查风险。

---

## 横向生态对比

好的，作为专注于AI智能体与个人AI助手开源生态的资深技术分析师，我将基于您提供的OpenClaw和Hermes Agent项目日报，生成一份横向对比分析报告。

---

## AI智能体与个人AI助手开源生态横向对比分析报告

**报告日期：** 2026-07-06
**分析师：** 资深技术分析师

### 1. 生态全景

当前个人AI助手开源生态正呈现出“高歌猛进”与“痛点丛生”并存的态势。一方面，以OpenClaw为代表的核心项目保持了极高的迭代速度，社区讨论异常活跃，表明市场对自主智能体的需求极为旺盛。另一方面，跨平台支持缺失、AI模型的“幻觉”与稳定性问题、以及安全沙箱机制的薄弱，成为制约用户体验和规模化部署的核心瓶颈。各项目均在加速解决这些共性问题，但技术路线和侧重点开始出现分化。整体来看，生态正处于从“可用”向“好用、安全、可信任”迈进的关键阶段，竞争与创新同时加速。

### 2. 各项目活跃度对比

| 评估维度 | OpenClaw | Hermes Agent | 对比分析 |
| :--- | :--- | :--- | :--- |
| **项目定位** | 全能型AI助手核心框架 | 轻量化Agent框架 |
| **当日Issues (创建/更新)** | 500条 (非常高) | 50条 (高) | **OpenClaw**的社区规模和问题暴露程度远超**Hermes Agent**，是当前生态的绝对热点。 |
| **当日PRs (创建/合并/关闭)** | 500条 / 328条合入 | 50条 / 20条合入 | **OpenClaw**的代码库变动量和合入速度惊人，表明其维护团队投入巨大，迭代极快。**Hermes Agent**虽数据量小，但效率同样可观。 |
| **版本发布** | **有**：新Beta版 (v2026.7.1-beta.2) | **无** | **OpenClaw**发布节奏紧凑，新特性持续集成。**Hermes Agent**当前侧重于稳定性修复。 |
| **社区健康度** | **高活跃、高增长，但伴生质量问题** (发布遗漏、严重Bug) | **高质量、快响应，但需求聚集度不如前者** | **OpenClaw**是“风口上的猪”，用户众多但需求繁杂。**Hermes Agent**是“小而美”的精品，社区讨论更聚焦，维护者响应更精准。 |
| **核心痛点** | 跨平台应用、AI稳定性与幻觉、安全沙箱 | 模型自主路由、反向代理支持、OAuth集成 | 两者痛点有重叠，但**OpenClaw**的“基建”问题更突出，而**Hermes Agent**的“体验”和“集成”问题更典型。 |

### 3. OpenClaw 在生态中的定位

OpenClaw在生态中扮演着 **“激进的前沿探索者”** 和 **“标准化聚合器”** 的双重角色。

- **优势与地位**：从庞大的Issue数和PR数来看，OpenClaw是当前最受关注、迭代最快的个人AI助手项目之一。它已成为社区新想法、新功能（如多智能体协作增强、动态模型发现）的核心试验田。其发布节奏和对最新模型（如GPT-5.6）的支持能力，显示出其强大的技术敏感性和适配能力。
- **技术路线差异**：与Hermes Agent更侧重于“Agent”框架层不同，OpenClaw倾向于提供更全面的系统级解决方案，涵盖从底层运行时到上层应用交互的完整能力。它试图构建一个类似“操作系统”的整合平台。
- **社区规模**：从单日500条Issue的体量推断，OpenClaw的社区贡献者和用户规模可能比Hermes Agent大一个数量级以上，是当前生态中社区活跃度最高的单一项目。
- **潜在风险**：其高速迭代也带来了“版本质量”和“开发流程”风险（如发布遗漏关键修复）。如果质量控制跟不上扩张速度，可能会造成用户信任流失，给Hermes Agent等竞争者留下细分市场的机会。

### 4. 共同关注的技术方向

两大项目在以下方向达成了高度共识，揭示了AI助手行业的共性挑战：

1.  **AI可靠性与可控性**
    - **涉及项目**：OpenClaw、Hermes Agent
    - **具体诉求**：
        - **OpenClaw**：解决“AI幻觉与错误响应”（Issue #92201）、“普通文本输出退化”（Issue #96857）、“虚假承诺”（Issue #58450）。
        - **Hermes Agent**：解决Ollama本地模型“上下文被静默截断”（Issue #43900）、中文用户“长任务截断与继续失败”（Issue #10943）。
    - **趋势解读**：用户对AI稳定输出的容忍度已降至冰点，开发者正通过精细化的上下文管理、流式处理逻辑验证、以及任务分步执行等策略来应对。

2.  **跨平台与设备生态**
    - **涉及项目**：OpenClaw、Hermes Agent
    - **具体诉求**：
        - **OpenClaw**：呼声最高的Linux/Windows原生应用支持（Issue #75，110条评论）。
        - **Hermes Agent**：修复Windows桌面端安装与更新问题（PR #59304、#59313），改善QQ等本地平台重连（PR #59317）。
    - **趋势解读**：PC端（特别是Linux）和移动端（如Android APK）支持是拓展用户基数的必须项。单纯依赖macOS或CLI/TUI无法满足主流办公和创作场景。

3.  **安全、隐私与沙箱机制**
    - **涉及项目**：OpenClaw、Hermes Agent
    - **具体诉求**：
        - **OpenClaw**：要求“内存信任标签”（#7707）防止记忆投毒、“屏蔽密钥”（#10659）防止API Key泄露、“文件系统沙箱配置”（#7722）。
        - **Hermes Agent**：核心讨论围绕Claude订阅OAuth集成（#25267），避免用户“双重付费”，本质是简化安全凭证管理。
    - **趋势解读**：随着Agent权限不断扩大，企业级应用和高级个人用户对数据安全和访问控制的需求已成为核心痛点，安全能力将从“加分项”变为“准入门槛”。

### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | 关键差异解读 |
| :--- | :--- | :--- | :--- |
| **功能侧重** | **全能集成与平台化**：提供多模型支持、记忆管理、技能市场、多智能体协作等完整生态。 | **框架化与灵活性**：专注于Agent核心逻辑、MCP协议接入、Dashboard可视化、以及模型路由等更“软”的能力。 |
| **目标用户** | **高需求专业用户与团队**：需要复杂工作流、多模态处理、或大规模部署的用户。 | **开发者与自托管者**：更关注框架的扩展性、自定义能力、以及与现有系统（如Ollama、Claude）的集成。 |
| **技术架构** | **复杂与全栈**：路由、内存、技能、运行时等组件高度耦合，形成一个功能完备但可能较为“重”的系统。 | **模块化与轻量**：核心Agent框架与UI（Dashboard）、模型后端解耦，更易于定制和二次开发。 |
| **社区主导方向** | **解决“大而全”带来的问题**：如跨平台、分发、质量、安全。 | **解决“精而深”带来的问题**：如特定场景下的稳定性、模型集成细节、开发者体验。 |

### 6. 社区热度与成熟度

- **高活跃、高速迭代层**：**OpenClaw** 处于这一层。其特点是社区需求爆炸式增长，项目以极快的速度响应并推进。风险在于快速迭代可能导致质量下降和流程混乱，正处于“扩张”向“成熟”过渡的挑战期。
- **高质量、低冗余层**：**Hermes Agent** 处于这一层。社区讨论更聚焦，问题和PR的“噪声”更低。项目维护者能更从容地进行精细化修复和功能打磨，呈现出“小而美、稳而精”的健康态势。

### 7. 值得关注的趋势信号

1.  **从“工具化”向“可信AI伙伴”进化**：用户已不满足于Agent执行简单指令，而是要求其行为 **“可解释”**（解决幻觉）、**“可追溯”**（修复输出退化）、**“有记忆”**（防止承诺落空）。这要求Agent系统从单纯的API调用层向上，构建更完善的上下文理解、行为审计和逻辑验证层。

2.  **“安全即功能”**：社区对 **“内存信任标签”**、**“屏蔽密钥”** 和 **“文件系统沙箱”** 的呼声，标志着用户对Agent安全性的认知已超越“网络安全”，进入到“AI安全”的新维度。开发者应将安全机制作为核心功能之一进行设计，而非事后修补。

3.  **“模型自主路由”成为新的效率瓶颈**：Hermes Agent社区对“模型自主路由”的强烈诉求（#16525）表明，用户希望在单一Agent内部，根据任务类型（简单问答 vs. 复杂推理）动态选择性价比最优的模型。这将是下一阶段提升效率和降低成本的关键技术方向。

4.  **“本地模型”与“长文本”的矛盾激化**：Ollama等本地模型因上下文窗口被静默限制而导致任务截断的问题反复出现（Hermes #43900, OpenClaw相关讨论），反映出当前主流框架在适配本地模型的长上下文能力上存在严重滞后，成为阻碍其大规模应用的主要障碍。

**对AI智能体开发者的建议**：
- **优先投资AI可靠性**：将解决“幻觉”和“行为退化”提升到最高优先级，这可能涉及**流式处理逻辑的重构**、**上下文预算的精准管理**以及**输出验证机制**。
- **将安全内化到架构**：在设计记忆系统、工具调用机制时，立即考虑**信任标签、密钥屏蔽和路径沙箱**的设计。
- **拥抱模型路由**：为用户提供**基于任务复杂度的模型自动切换能力**，这将成为AI助手能否从“玩具”变为“生产力工具”的关键分水岭。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 — 2026-07-06

## 今日速览
过去 24 小时项目保持高度活跃：共有 50 条 Issue 更新（其中 13 条已关闭）和 50 条 PR 更新（20 条已合并/关闭），社区讨论集中在模型自主路由（#16525）、Dashboard 反向代理配置（#34390）以及 Claude 订阅集成（#25267）等热点。无新版本发布，但维护团队批量提交了多组“salvage”PR，系统性修复了 gateway/desktop 中的遗留问题，项目整体向稳定性和安全性迈出坚实一步。

---

## 版本发布
无新版本发布。

---

## 项目进展
今日合并/关闭的重要 PR 显示 Hermes 在桌面端安装可靠性、MCP 客户端重连机制、以及跨平台兼容性方面取得关键修复：
- **Windows 桌面安装语法检查**：PR [#59304](https://github.com/NousResearch/hermes-agent/pull/59304)（salvage #59230）为 Windows 新增 `web_server.py` 语法校验，防止因合并冲突或代码错误导致安装成功但后端无法启动。
- **Desktop 断线重连保护**：PR [#59313](https://github.com/NousResearch/hermes-agent/pull/59313) 修复 Windows 更新时渲染进程在退出间隙误唤后端的问题，通过预写 `.hermes-update-in-progress` 标记避免“更新砖机”。
- **MCP 超时与预检修复**：PR [#59311](https://github.com/NousResearch/hermes-agent/pull/59311) 为 catalog install 中的 `subprocess.run` 添加超时参数；PR [#59316](https://github.com/NousResearch/hermes-agent/pull/59316) 优化 MCP 预检逻辑，允许仅通过 POST 提供服务的 Streamable HTTP 服务器（如 Stirling-PDF）通过探测。
- **Gateway 多 profile 环境变量与凭证处理**：PR [#59315](https://github.com/NousResearch/hermes-agent/pull/59315)、[#59320](https://github.com/NousResearch/hermes-agent/pull/59320)、[#59310](https://github.com/NousResearch/hermes-agent/pull/59310) 分别修复了多 profile 下的 token 环境变量读取、配置路径嵌套、以及回复路由问题，确保了 multiplex 模式的正确性。
- **QQ 平台重连崩溃**：PR [#59317](https://github.com/NousResearch/hermes-agent/pull/59317) 修复 `QQAdapter.connect()` 缺少 `is_reconnect` 参数导致 Type Error 的阻断性 Bug。

此外，今日还关闭了多个等待已久的 PR（如 #59230）和积压 Issue，项目 backlog 减少了约 5% 的活跃任务。

---

## 社区热点
今日讨论最活跃的 Issue 及背后的诉求：

1. **[#16525] Expose model_switch as agent-callable tool**  
   - 评论：9 | 👍：5  
   - 用户要求将模型切换能力暴露为 Agent 可调用的工具，让代理能根据任务复杂度自主路由到不同模型，而非仅依靠配置文件或斜杠命令。这是对“自主路由”能力的强烈需求，反映了高级用户希望减少手动干预、提升多模型协作效率的期望。  
   - [链接](https://github.com/NousResearch/hermes-agent/issues/16525)

2. **[#34390] Dashboard: add --allowed-hosts flag**  
   - 评论：9 | 👍：0  
   - 用户反映在反向代理（Tailscale、nginx）后使用 Dashboard 时，host-header 验证导致访问受限，要求增加 `--allowed-hosts` 参数允许自定义域名。直接击中企业用户和自托管者的痛点，是 Dashboard 可用性的关键改进。  
   - [链接](https://github.com/NousResearch/hermes-agent/issues/34390)

3. **[#25267] Claude Agent SDK model provider with subscription OAuth**  
   - 评论：9 | 👍：41（最高赞）  
   - Claude 订阅用户希望无需额外 API Key 即可使用 Hermes，避免“双重付费”。现有 Anthropic 提供商要求 Developer Platform API Key，而用户已付月费。该需求有 41 个 👍，是社区最迫切的功能请求之一，可能影响下一版本的提供商架构设计。  
   - [链接](https://github.com/NousResearch/hermes-agent/issues/25267)

4. **[#43900] Ollama本地模型上下文被静默限制为4096**  
   - 评论：8  
   - 使用 Ollama 本地模型时，实际上下文被限制为默认 4096 token，即使模型支持更大上下文（如 Gemma 4 的 131072）。用户遭遇 `finish_reason=length` 截断，严重影响长对话和代码生成。属于模型集成层面的重要缺陷。  
   - [链接](https://github.com/NousResearch/hermes-agent/issues/43900)

---

## Bug 与稳定性
按严重程度排列，标注是否已有修复 PR：

| 严重度 | Issue # | 描述 | 修复状态 |
|--------|---------|------|----------|
| **P1** | — | 今日无 P1 Issue 新增，但 PR [#59313](https://github.com/NousResearch/hermes-agent/pull/59313) 修复了 Windows 更新时的进程竞态条件（P1 级）。 | 已合入 |
| **P2** | [#58962](https://github.com/NousResearch/hermes-agent/issues/58962) | Session 永久陷入“Stream stale”循环，所有重试均会 stale，无法恢复。影响 OpenAI 兼容提供商。 | 无 fix PR |
| **P2** | [#57129](https://github.com/NousResearch/hermes-agent/issues/57129) (已关) | MCP 客户端在 5 次重连失败后永久放弃服务器，需进程重启。同类问题还见于 #57604、#38488。 | 已关闭（关联修复） |
| **P2** | [#59272](https://github.com/NousResearch/hermes-agent/issues/59272) | QQAdapter.connect() 缺少 `is_reconnect` 导致整个 QQ 平台断线后无法恢复。 | PR [#59317](https://github.com/NousResearch/hermes-agent/pull/59317) 已修复 |
| **P2** | [#42961](https://github.com/NousResearch/hermes-agent/issues/42961) | `terminal.cwd` 配置在本地后端被忽略，始终使用进程工作目录。 | 无 fix PR |
| **P3** | [#59314](https://github.com/NousResearch/hermes-agent/issues/59314) | `resolve_display_context_length()` 忽略 custom_providers 中的 per-model 上下文长度 | 无 fix PR |
| **P3** | [#59262](https://github.com/NousResearch/hermes-agent/issues/59262) | 插件 `transform_terminal_output` 钩子签名不匹配导致每条消息产生警告 | 无 fix PR |
| **P3** | [#59244](https://github.com/NousResearch/hermes-agent/issues/59244) | 后台记忆回顾忽略已配置的记忆提供商，仅写入传统内存。 | 无 fix PR |
| **P3** | [#31987](https://github.com/NousResearch/hermes-agent/issues/31987) | MCP HTTP 传输清理时抛出 `RuntimeError` 导致重连失败循环 | 无 fix PR |
| **P3** | [#59257](https://github.com/NousResearch/hermes-agent/issues/59257) (已关) | Desktop 优先提交导致 CLI/TUI 会话退出摘要丢失。 | 已关闭（已修复） |

---

## 功能请求与路线图信号
以下用户需求获得较多关注或已出现对应 PR，可能被纳入下一版本：

- **Agent 自主路由**（[#16525](https://github.com/NousResearch/hermes-agent/issues/16525)）：社区呼声高，已有初步设计，但暂无 PR。若实现将大幅提升多模型工作流的自动化水平。
- **Claude 订阅 OAuth**（[#25267](https://github.com/NousResearch/hermes-agent/issues/25267)）：41 👍 最高赞，表明大量 Claude 月费用户有强烈需求。若开发，可能需要引入新的 provider 类型。
- **Dashboard 反向代理支持**（[#34390](https://github.com/NousResearch/hermes-agent/issues/34390)）：企业部署刚需，已有用户提议实现方案，预计会在 dashboard 配置中增加 `--allowed-hosts` 参数。
- **自动工作区记忆**（[#38552](https://github.com/NousResearch/hermes-agent/issues/38552)）：Agent 跟踪每个目录用途，减少每次 session 的上下文浪费。此为长期 feature 提案，与 #33856 互补。
- **Desktop 快捷归档**（[#59308](https://github.com/NousResearch/hermes-agent/issues/59308)）：增加存档会话的键盘快捷键，提升频繁操作效率。
- **macOS 菜单栏命令参考**（PR [#59312](https://github.com/NousResearch/hermes-agent/pull/59312)）：桌面端新增斜杠命令快捷参考弹窗，提升新用户上手体验。

---

## 用户反馈摘要
从今日活跃的 Issue 评论中提炼真实用户声音：

- **Ollama 上下文截断问题**（[#43900](https://github.com/NousResearch/hermes-agent/issues/43900)）：用户“jhonymiler”抱怨模型上下文未按 GGUF 元数据设置，导致长对话被截断。这是本地模型用户的常见痛点，社区多次反馈但未修复。
- **Dashboad 反向代理限制**（[#34390](https://github.com/NousResearch/hermes-agent/issues/34390)）：用户“dklangst-sys”描述 Tailscale 场景下无法访问 Dashboard，原因是 host-header 校验。用户希望获得更灵活的配置选项。
- **Claude 双重付费**（[#25267](https://github.com/NousResearch/hermes-agent/issues/25267)）：用户“YongboYu”明确表示“已付订阅费却仍需 API Key 是双重收费”，希望直接复用订阅 credits。此类反馈在 Reddit 和 Discord 上也频繁出现。
- **中文用户输入截断**（[#10943](https://github.com/NousResearch/hermes-agent/issues/10943)）：用户“remychen20-cloud”用中文描述模型在长任务中频繁因 `finish_reason=length` 截断，且继续指令后模型再次截断，无法完成程序编写。反映了输出 token 限制对多步骤任务的严重影响。
- **MCP 永久断连**（[#57129](https://github.com/NousResearch/hermes-agent/issues/57129)）：用户“admsk2”强调仅一次瞬态故障就会导致 MCP 工具永久失效，恢复成本极高（需重启进程）。这是 MCP 生态稳定性的核心挑战。

---

## 待处理积压
以下为长期未响应的重要 Issue 或 PR，建议维护者优先关注：

1. **[#2637] Add quick shell command feature (!cmd)**  
   - 创建时间：2026-03-23  
   - 状态：OPEN | P3  
   - 摘要：添加 `!cmd` 前缀直接执行 shell 命令，绕过 LLM。已有实现但未合并，需评审。  
   - [PR 链接](https://github.com/NousResearch/hermes-agent/pull/2637)

2. **[#18366] fix: make /busy command available on gateway platforms**  
   - 创建时间：2026-05-01  
   - 状态：OPEN | P2  
   - 摘要：`/busy` 命令在 Telegram/Discord 等 Gateway 平台上不可用，但引导中却提示用户可使用。已有一份实现 PR 但长期搁置。  
   - [PR 链接](https://github.com/NousResearch/hermes-agent/pull/18366)

3. **[#10943] 中文输入截断与继续失败**  
   - 创建时间：2026-04-16  
   - 状态：OPEN | 无优先级  
   - 摘要：用户报告长任务中模型持续截断，继续后仍截断，无法完成任务。虽为中文报告，但涉及的核心问题（多步骤工具调用时的 token 限额）值得关注。  
   - [Issue 链接](https://github.com/NousResearch/hermes-agent/issues/10943)

4. **[#41445] hermes prompt-size over-counts tools**  
   - 创建时间：2026-06-07  
   - 状态：已关闭（但修复未合入？）  
   - 注意：该 Issue 已于2026-07-06关闭，但关闭原因未知（可能是 duplicate 或已修复），建议确认对应修复是否已进入主干。  
   - [Issue 链接](https://github.com/NousResearch/hermes-agent/issues/41445)

以上积压项目若不及时处理，可能影响社区信心和贡献者留存。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*