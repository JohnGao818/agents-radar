# OpenClaw 生态日报 2026-06-04

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-04 03:31 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 OpenClaw 项目 GitHub 数据，为您整理出以下 2026-06-04 项目动态日报。

---

# OpenClaw 项目日报 | 2026-06-04

## 1. 今日速览

**整体活跃度：🔥 极高**

过去24小时内，OpenClaw 项目保持了极高的社区活跃度和开发迭代速度。伴随着 3 个新版本的发布，Issues 和 PR 的更新均达到了 500 条的峰值，表明社区在功能改进与稳定性修复上投入了大量精力。最新主要版本 `v2026.6.1` 聚焦于提升 Agent 运行时在复杂场景下的恢复能力以及消息渠道的稳定性。然而，大量待合并的 PR（401 条）和持续涌现的回归性 Bug 也表明了项目目前正处于一个功能密集迭代与暴露稳定性的阵痛期。

## 2. 版本发布

项目今日发布了 3 个新版本，标志着进入 6 月的新迭代周期。

- **[v2026.6.2-beta.1]**
  - **主要内容**：重点改进了插件和技能的安装策略，采用新的“操作者安装策略”（operator install policy）替代了旧的“危险代码扫描”路径。这使得通过 ClawHub、CLI 等方式进行安装的流程更清晰，也优化了诊断(doctor)工具和故障排查体验。这是一个涉及安全性和用户体验的重要改进。
  - **链接**: [Release v2026.6.2-beta.1](openclaw/openclaw/releases/tag/v2026.6.2-beta.1)

- **[v2026.6.1]**
  - **主要内容**：主要版本发布。重点提升了 Agent 和 CLI 运行时在工具调用中断、会话过期、压缩转换交接以及媒体重试等场景下的恢复能力。同时，加强了 Telegram、WhatsApp、iMessage 等渠道的消息投递稳定性。
  - **链接**: [Release v2026.6.1](openclaw/openclaw/releases/tag/v2026.6.1)

- **[v2026.6.1-beta.3]**
  - **主要内容**：与 `v2026.6.1` 版本亮点一致，作为候选版本先行发布。
  - **链接**: [Release v2026.6.1-beta.3](openclaw/openclaw/releases/tag/v2026.6.1-beta.3)

**迁移注意事项**：建议用户在升级至 2026.6.x 系列时，关注 `v2026.6.2-beta.1` 中关于插件安装策略的变更。老旧的“危险代码扫描”路径已被弃用，确保您的自动化部署流程与新策略兼容。

## 3. 项目进展

今日虽然有大量 PR 处于待合并状态，但仍有一些关键修复被合并关闭，推动了项目稳定性的提升。

- **渠道稳定性**：
  - **WhatsApp 频道修复**：PR [#87965](openclaw/openclaw/pull/87965) 修复了在热配置更新时，禁用 WhatsApp 账户不会关闭对应频道的问题，确保了配置的即时生效，防止资源泄露。
  - **Telegram 修复**：PR [#90123](openclaw/openclaw/pull/90123) 修复了自动回复场景下，回复消息状态计数不准确的问题，使投递状态更可靠。

- **平台兼容性**：
  - **macOS 伴侣应用**：PR [#88890](openclaw/openclaw/pull/88890) 修复了 macOS 伴侣应用中“点击通话”功能硬编码低层级思考模式的问题，使得思考层级配置在平台间保持一致，为 macOS 用户提供了更好的体验。

## 4. 社区热点

今日讨论最活跃的议题反映了用户对核心架构稳定性和会话安全性的深切关注。

1. **[#88838] 核心会话/转录 SQLite 迁移** 🔥 17 条评论
   - **诉求**：这是一个关于核心架构变更的重大讨论。社区贡献者 `jalehman` 提议采用“分支抽象模式”(branch-by-abstraction seam)，将核心会话状态的 SQLite 迁移工作拆解为多个小型、可审查的 PR，以避免大规模重写带来的高风险。这反映了社区对核心变更的谨慎态度，以及对架构演进的深度参与。
   - **链接**: [Issue #88838](openclaw/openclaw/issues/88838)

2. **[#65161] 心跳模式严重 Bug** 🔥 14 条评论
   - **诉求**：该问题报告了在隔离模式下系统心跳机制存在多项回归问题，包括心跳节奏停滞、心跳事件报告错误等。社区对此表现出高度关注，因为心跳对于远程运维和系统监控至关重要，直接关系到用户对Agent状态的感知。
   - **链接**: [Issue #65161](openclaw/openclaw/issues/65161)

3. **[#67035] Windows 聊天 UI 回归问题** 🔥 14 条评论
   - **诉求**：用户报告在 Windows 上升级后，Web 聊天界面出现“输入内容被吞”、“流式回复不可见”等严重回归问题。这直接影响了 Windows 用户的核心交互体验，反馈非常强烈，是典型的“交付受阻”类问题。
   - **链接**: [Issue #67035](openclaw/openclaw/issues/67035)

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在**会话状态异常、消息丢失、以及严重的回归问题**上。以下按严重程度排列：

**P1 (严重) 级别 Bug：**

- **[Bug] Codex 应用服务器“完成”停滞回归** 🔥 P1 - [Issue #88312](openclaw/openclaw/issues/88312)
  - 描述：`2026.5.27` 版本开始，Codex 服务器在完成多工具 Agent 轮次时稳定性存在回归问题。这是一个严重阻碍用户使用高级 Agent 功能的回归。
  - Fix PR：尚无。

- **[Bug] 相同会话键上反复硬重置** 🔥 P1 - [Issue #63216](openclaw/openclaw/issues/63216)
  - 描述：即便配置了高容错，特定会话仍会反复发生“上下文溢出”硬重置，造成会话循环中断。
  - Fix PR：尚无。

- **[Bug] Mattermost 斜杠命令返回 503** 🔥 P1 - [Issue #68113](openclaw/openclaw/issues/68113)
  - 描述：在 `v2026.4.15` 中，Mattermost 斜杠命令完全失效，返回“未初始化”错误。
  - Fix PR：尚无。

- **[Bug] 聊天 UI 消息重复** 🔥 P1 - [Issue #88020](openclaw/openclaw/issues/88020)
  - 描述：Anthropic `thinking` 模块签名过期后，会话未能优雅恢复，导致硬失败。
  - Fix PR：尚无。

**P2 (重要) 级别 Bug：**

- 多个与**会话上下文膨胀** (#67419)、**子代理 MCP 工具注入失败** (#85030)、**WebChat 消息渲染失败** (#77136) 相关的Bug，反映了项目在处理复杂会话和跨组件协作时的脆弱性。

**当前已有关联 Fix PR 的 Bug：**

- **[Bug] WebChat 消息重复** - [Issue #71992](openclaw/openclaw/issues/71992) 对应的 Fix PR [#86646](openclaw/openclaw/pull/86646) 已提交，旨在通过在 `chat.status` 最终事件时去重来解决该问题。

## 6. 功能请求与路线图信号

社区对新功能的需求主要集中在**安全性与标准化**上，这可能成为下一版本的重点方向。

- **[Feature] 外部安全与护栏检查的标准接口** 🔥 - [Issue #72741](openclaw/openclaw/issues/72741)
  - 请求：提供一个标准化的接口，允许开发者围绕Agent动作集成外部安全检查和护栏系统。这显示出社区对于在复杂生产环境中部署Agent的安全合规考虑日益增长。

- **[Feature] 配置上传大小限制** - [Issue #71142](openclaw/openclaw/issues/71142)
  - 请求：允许用户配置 Web 界面的文件上传大小限制。这反映了用户上传更大文件（如图像）的直接需求，目前硬编码的 5MB 限制成为了一个痛点。

- **[Feature] 多索引嵌入记忆** - [Issue #63990](openclaw/openclaw/issues/63990)
  - 请求：支持多索引的嵌入记忆，以实现在不同模型/提供商间弹性切换而不破坏向量语义。这是一个更长期、更高级的特性，旨在提升生产环境下的可靠性，可能与项目“记忆优化”路线图一致。

## 7. 用户反馈摘要

从今日的 Issues 讨论中，可以提炼出以下用户痛点和使用体验：

1. **对“回归”的容忍度降低**：用户如 `yair` 在 #88312 中明确指出了“之前能用，现在不行”的回归问题，并有详细对比，显示出社区对版本质量的要求很高，回归 Bug 会严重影响用户信任。

2. **对核心稳定性的焦虑**：评论活跃的 #88838 表明，资深社区成员对核心架构变动（如SQLite迁移）非常敏感，他们更倾向于渐进、可控的演进方式，而非大版本重写。这种对风险意识的高度共识是项目成熟的体现。

3. **跨平台体验不一致的困扰**：`bobopenclawson-bit` 在 #67735 中抱怨 WebChat 不遵守身份链接（identityLinks）规则，导致其行为与 Telegram DM 不一致。这表明用户期望在任何渠道都能获得统一的、符合预期的体验。

4. **对“沉默”错误的困惑**：`ericiperson` 在 #86214 中描述了一个棘手问题：Agent 在请求中间阶段突然停止，但不报错或不显示明显异常，用户难以自行排查。这类“软故障”对用户信心打击很大。

## 8. 待处理积压

以下是一些已长期未更新或等待关键决策的重要 Issue，这些项目可能影响部分用户的核心使用体验，值得维护者优先关注。

- **[Issue #65161] 心跳隔离模式停滞** - 创建于 2026-04-12，P2 级别，已标记为 `stale`。该问题报告了核心系统功能（心跳）的严重问题，但因信息不足或等待决策而停滞，建议发起投票或补充测试场景以推动解决。
- **[Issue #63216] 会话反复硬重置** - 创建于 2026-04-08，P1 级别，同样标记为 `stale`。该项目直接导致会话无法使用，影响面大，但缺少明确的修复路径或产品决策，需要优先干预。
- **[Issue #67419] 会话上下文膨胀** - 创建于 2026-04-15，P2 级别，标记为 `stale`。该问题涉及重要的性能优化，用户反馈浪费了 20-30% 的 Token，但长期缺少维护者审查。
- **[Issue #68691] Sandbox 僵尸进程** - 创建于 2026-04-18，P1 级别。该问题可能导致沙箱资源耗尽，构成隐蔽的稳定性风险，但长期未更新。

---

## 横向生态对比

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将基于您提供的OpenClaw和Hermes Agent项目在2026年6月4日的动态，为您呈现一份横向对比分析报告。

---

# 个人AI智能体开源生态横向分析报告 | 2026-06-04

## 1. 生态全景

当前个人AI智能体与自主Agent开源生态正经历从“功能扩张”到“稳定化与安全合规”的关键转型期。头部项目社区活跃度极高，但共同面临着因快速迭代导致的**回归Bug频发、跨平台体验不一致**以及**核心架构稳定性不足**等阵痛。社区需求已从“能否实现功能”转向“能否在生产环境中可靠、安全地运行”，对**会话管理、资源控制、跨渠道统一体验**的诉求空前强烈。同时，**安全与护栏系统**的需求从上游浮现，标志着生态正为更复杂、更敏感的企业级应用场景做准备。

## 2. 各项目活跃度对比

| 项目 | Issues (Open/New) | PRs (Open/Merged) | New Releases | 社区健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | ~500条（峰值，24h内） | ~500条（峰值，但401条待合并） | 3个（`v2026.6.2-beta.1`, `v2026.6.1`, `v2026.6.1-beta.3`） | **极高活跃，但存在质量隐患**。功能迭代密集，但大量待合并PR和回归性Bug表明项目处于快速扩张后的质量巩固期，维护压力巨大。 |
| **Hermes Agent** | ~50条（24h内） | ~50条（24h内） | 0 | **高度活跃，安全与稳定性优先**。社区响应快，但暴露了P0级别的安全漏洞和关键平台兼容性问题。项目正在处理更为复杂的架构和安全审查，迭代节奏更稳健。 |

**分析结论**：OpenClaw的社区规模（以Issue/PR数衡量）约为Hermes Agent的10倍，呈现出更蓬勃的社区生态。但“量大”并不等同于“质优”，OpenClaw的待办事项积压和回归问题更多，处于 **“野蛮生长”** 阶段；而Hermes Agent社区虽小，但问题聚焦于安全和高阶稳定性，显示出 **“精耕细作”** 的特征。

## 3. OpenClaw在生态中的定位

- **优势**：**社区规模与覆盖度**。OpenClaw凭借极低的参与门槛和强大的插件生态，聚集了远超竞品的社区贡献者，形成了“数据飞轮”效应。其日活、功能迭代速度和新版本发布频率均处于领先地位，是生态中最具“大众影响力”的项目。
- **技术路线差异**：OpenClaw倾向于**更广泛的渠道和插件集成**（如Wecome、Mattermost），而Hermes Agent更聚焦于**“桌面端”和“container-native”体验**。OpenClaw当前通过“操作者安装策略”改革安全性，而Hermes Agent直接暴露并处理P0级漏洞，前者是**优化流程**，后者是**修补核心骨架**。
- **社区规模对比**：OpenClaw（千级Issue/PR）远大于Hermes Agent（百级），但Hermes Agent的贡献者（如`jalehman`等）表现出更深度的架构参与能力，社区**成熟度**更高。OpenClaw的优势在**广度**，Hermes Agent的优势在**深度**。

## 4. 共同关注的技术方向

多个项目不约而同地聚焦于以下技术方向，这构成了当前生态的核心痛点与机遇：

1.  **稳定性与回归控制**：
    -   **OpenClaw**：`#88312` Codex服务器停滞回归、`#67035` Windows UI回归、`#65161` 心跳模式Bug。
    -   **Hermes Agent**：`#37881` Windows更新损坏、`#30230` macOS文件描述符限制。
    -   **核心诉求**：两个项目都报告了“之前能用，升级后失效”的严重回归，且都集中在**Windows平台**。这揭示了跨平台（特别是非Linux系统）稳定性是当前所有Agent项目的通用挑战。

2.  **安全与权限管控**：
    -   **OpenClaw**：`#72741` 请求标准化的外部安全检查/护栏接口。
    -   **Hermes Agent**：`#38643` P0路径遍历漏洞、`#38638` P0网关默认开放、`#38068` Slack审批绕过。
    -   **核心诉求**：社区不再满足于项目内置的基本安全策略，而是要求**可集成、可扩展的外部安全框架**。这暗示了Agent正从玩具走向生产工具。

3.  **智能体会话与记忆管理**：
    -   **OpenClaw**：`#88838` 核心会话SQLite迁移、`#67419` 会话上下文膨胀、`#63216` 会话硬重置。
    -   **Hermes Agent**：`#38552` 工作区自动记忆、`#65161` 心跳模式停滞（反映状态监控失效）。
    -   **核心诉求**：会话的 **“抗衰减”与“可恢复”** 能力是核心痛点。Agent在长期运行或复杂任务后容易出现上下文漂移、Token浪费甚至硬重置，社区渴望更科学的记忆生命周期管理机制。

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **功能侧重** | **多渠道通讯与Agent协作**。强调通过插件连接各类聊天应用，以及Agent之间的工具调用远程协作。 | **桌面端原生体验与安全合规**。聚焦于本地GUI、系统托盘、以及P0级别的安全审计。 |
| **目标用户** | **社区爱好者、个人开发者、集成商**。旨在打造“万能Agent中心”，降低所有场景的部署门槛。 | **高级开发者、安全敏感用户、企业内测团队**。提供更精细的控制和更高的安全基线。 |
| **技术架构** | **插件化 + 标准接口**。依赖“ClawHub”等生态市场，架构设计偏向于功能的热插拔。 | **桌面端 + 容器化**。强调`container-native`，利用Docker隔离性，同时专注于macOS/Windows原生适配。 |
| **关键Bug信号** | **回归问题密集**，说明改动范围大，测试覆盖不足。 | **安全漏洞高优先级**，说明项目更重视核心安全，对非对称风险有更严格的控制流程。 |

## 6. 社区热度与成熟度

-   **第一梯队（高爆发期）**：**OpenClaw**。其活跃度、问题量和发布频率均呈爆发态，是生态中最“热”的项目，但也是Bug和待办最多的项目。社区处于 **“快速试错、功能优先”** 的早期大众阶段。

-   **第二梯队（成熟巩固期）**：**Hermes Agent**。活跃度同样很高，但问题类型更聚焦、更深度（如P0漏洞、macOS极限性能）。社区更小，但贡献者专业度更高，项目处于 **“存量精雕、安全加固”** 的后期成熟阶段。

-   **社区成熟度定性**：两个项目都表现出**对安全性的高度重视**。OpenClaw通过改版安装策略来实践，Hermes Agent则直接处理高危漏洞。这表明在整个生态中，**“安全”已不再是可选项，而是参与竞争的基础门槛**。

## 7. 值得关注的趋势信号

1.  **安全合规成为“新基建”**：无论是OpenClaw的“标准安全接口请求”还是Hermes Agent的“P0路径遍历”，都标志着社区对Agent安全的理解从“用户自身责任”向“框架赋予能力”转变。开发者应关注项目的安全审计工具和策略配置能力，这将是未来Agent能否进入生产环境的第一道门槛。

2.  **跨平台稳定性的“黑暗森林”**：大量的Windows/macOS专属Bug（文件描述符限制、更新损坏、UI回归）揭示了当前Agent项目在非Linux环境上的脆弱。对于想要在桌面端部署Agent的开发者，**应高度关注项目对特定平台的CI测试覆盖度和修复承诺**。

3.  **智能体的“自愈”与“工作记忆”机制**：OpenClaw的核心会话迁移和Hermes的工作区记忆尝试，都指向同一个核心诉求：**Agent需要知道自己“之前做了什么”以及“该怎样恢复正常”**。未来的Agent将不再只是一个“对话机器人”，而是一个具备持久记忆和状态恢复能力的“数字大脑”。

4.  **性能与成本的隐忧**：OpenClaw中“会话上下文膨胀浪费20-30% Token”的Bug，以及Hermes对macOS文件描述符限制的吐槽，都暗示了Agent在长周期运行下的资源管理挑战。**性能优化和成本控制**（特别是Token成本）将成为下一个竞争焦点。

5.  **标准化协议的萌芽**：OpenClaw的“操作者安装策略”和Hermes的“MCP协议集成”，都在试图定义更清晰、更安全的组件交互标准。开发者应留意**MCP、MCP等协议**的采纳情况，这可能成为未来Agent生态间互联互通的基石。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 Hermes Agent 项目数据，生成以下 2026-06-04 的项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-06-04

## 1. 今日速览

本日 Hermes Agent 项目呈现高度活跃状态，社区贡献者参与度极高。过去 24 小时内，项目处理了 50 条 Issue 和 50 条 PR，体现了社区的强劲动能和快速响应能力。**稳定性与安全性成为今日两大焦点**：一方面，社区报告了涉及 P0 级别的路径遍历安全漏洞和多个高优先级 Bug；另一方面，维护者对桌面应用、MCP（Model Context Protocol）集成和 Docker 容器化等问题提交了大量修复 PR。尽管项目当日未发布新版本，但通过密集的 Issue 讨论和 PR 提交，项目正在从 **“功能扩展”** 向 **“稳定化、安全化与平台优化”** 阶段快速迈进。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日合并/关闭了 2 个 PR，虽然数量不多，但体现了项目在代码重构和测试稳定性上的扎实推进。

- **`[PR #38593] refactor(web): unify main-slot model assignment base_url/context handling`** - **已合并**。合并了关于 Web 端主要模型配置（`base_url`/`context`）的处理逻辑。这个重构 PR 将由 `POST /api/model/set` 接口和 profile 写入器两处处理的逻辑统一到一个 helper 中，减少了未来因代码分散而导致的自定义/托管模式 `base_url` 配置不一致的风险。这表明项目团队在关注功能的同时，也在致力于代码质量的提升，为后续扩展打下更稳固的基础。
    - **链接**: [NousResearch/hermes-agent PR #38593](https://github.com/NousResearch/hermes-agent/pull/38593)

- **`[PR #38665] test(docker): make tty-passthrough probe robust to container boot-log noise`** - **已合并**。修复了 Docker 测试中的一个脆弱点。原有的 `test_tty_passthrough_to_container` 测试在容器启动时因日志噪音导致断言失败。该 PR 提升了测试的鲁棒性，确保持续集成 (CI) 环境的稳定，这对于一个依赖容器化部署的项目至关重要。
    - **链接**: [NousResearch/hermes-agent PR #38665](https://github.com/NousResearch/hermes-agent/pull/38665)

## 4. 社区热点

今日社区讨论最热烈的 Issue 和 PR 如下，主要集中在对 **用户体验、系统兼容性和安全性** 的广泛关注上。

- **`[Issue #26689] Accessibility improvements for blind VoiceOver users`** (评论：8)
    - **热点分析**: 这是一个讨论热度极高的（8条评论）无障碍功能需求。来自**盲人用户**的详细反馈，指出 Hermes 强大的后端功能被当前对屏幕阅读器不友好的用户体验（UX）所阻碍。这不仅是社区包容性的体现，也揭示了项目在 **“终端用户界面（TUI）”和桌面端**在可访问性设计上的短板，是提升用户基础和社区声誉的关键诉求。
    - **链接**: [NousResearch/hermes-agent Issue #26689](https://github.com/NousResearch/hermes-agent/issues/26689)

- **`[Issue #30230] Gateway hits macOS fd limit (256): OSError Too many open files`** (评论：3)
    - **热点分析**: 该问题揭示了在 macOS 系统上，当运行多个 Profile 和 MCP 服务器时，Gateway 进程会轻易超过默认的 256 个文件描述符限制，导致服务崩溃。这是一个**特定于平台**的稳定性问题，触及到核心组件的**资源管理**。社区的讨论表明，经验丰富的用户（例如提及 `trade-paper` 配置）已开始触及该限制，该问题对重度用户和高级部署场景构成严重威胁。
    - **链接**: [NousResearch/hermes-agent Issue #30230](https://github.com/NousResearch/hermes-agent/issues/30230)

- **`[Issue #37881] [Bug]: hermes update bricks the install on Windows`** (评论：3，👍: 1)
    - **热点分析**: 这是用户反馈的 **Windows 平台上的“致命”升级问题**，导致安装环境完全损坏。虽然评论数不多，但引起了用户的强烈共鸣（1个赞）。问题暴露了`hermes update`命令在 Windows 上处理 venv 重建时的逻辑缺陷（如“目录已存在”错误），导致核心模块 `hermes_cli` 无法导入。这表明 Windows 平台的兼容性和更新机制仍需重点打磨。
    - **链接**: [NousResearch/hermes-agent Issue #37881](https://github.com/NousResearch/hermes-agent/issues/37881)

- **`[Issue #38643] [Security] Hermes skill_view name traversal discloses files outside the trusted skills directory`** (评论：0)
    - **热点分析**: 尽管评论为零，但作为今日 **P0 级安全问题**，必为社区（尤其是维护者）最高关注。该漏洞指出 `skill_view` 工具可能被利用遍历目录，泄露受保护的 “trusted skills” 目录之外的文件。尽管尚未有公开讨论，其潜在影响巨大，预计维护者会立即响应并发布修复。
    - **链接**: [NousResearch/hermes-agent Issue #38643](https://github.com/NousResearch/hermes-agent/issues/38643)

## 5. Bug 与稳定性

今日报告的 Bug 和稳定性问题范围广泛，从安全漏洞到平台兼容性问题。以下按严重程度排列，并标注是否已有修复 PR。

-   **P0 (Critical)**:
    -   **`[Issue #38643] skill_view 路径遍历漏洞**，可泄露文件。*未标注已有修复 PR。*
        -   链接: [Issue #38643](https://github.com/NousResearch/hermes-agent/issues/38643)
    -   **`[Issue #38638] Gateway own-policy 适配器无白名单时“默认开放”**（CVSS 9.3 Critical）。*未标注已有修复 PR。*
        -   链接: [Issue #38638](https://github.com/NousResearch/hermes-agent/issues/38638)

-   **P1 (High)**:
    -   **`[Issue #37881] Windows 上 `hermes update` 破坏安装**。*未标注已有修复 PR。*
        -   链接: [Issue #37881](https://github.com/NousResearch/hermes-agent/issues/37881)
    -   **`[Issue #38652] OpenRouter/ Nous 提供商 `output cap too large` 错误导致无限重置循环**。*已有修复 PR: [#38667](https://github.com/NousResearch/hermes-agent/pull/38667)*
        -   链接: [Issue #38652](https://github.com/NousResearch/hermes-agent/issues/38652)

-   **P2 (Medium)**:
    -   **`[Issue #30230] macOS Gateway 文件描述符限制导致崩溃**。*未标注已有修复 PR。*
        -   链接: [Issue #30230](https://github.com/NousResearch/hermes-agent/issues/30230)
    -   **`[Issue #38068] Slack 审批/确认按钮忽略授权配置**（CVSS 8.0 High）。*已有修复 PR: [#38069](https://github.com/NousResearch/hermes-agent/pull/38069)*
        -   链接: [Issue #38068](https://github.com/NousResearch/hermes-agent/issues/38068)
    -   **`[Issue #38618] `hermes update` 报告版本滞后但实际已更新**。*未标注已有修复 PR。*
        -   链接: [Issue #38618](https://github.com/NousResearch/hermes-agent/issues/38618)
    -   **`[Issue #38674] 盲目执行 `.py` 文件**，可能导致意外行为。*未标注已有修复 PR。*
        -   链接: [Issue #38674](https://github.com/NousResearch/hermes-agent/issues/38674)
    -   **`[PR #38664] 修复本地 VLM 视觉路由问题**。*解决 computer_use 在本地/自定义视觉模型上的路由bug。*
        -   链接: [PR #38664](https://github.com/NousResearch/hermes-agent/pull/38664)

-   **P3 (Low)**:
    -   **`[Issue #38580] 依赖 `requests==2.33.0` 导致在 Jetson (ARM) 平台崩溃**。*未标注已有修复 PR。*
        -   链接: [Issue #38580](https://github.com/NousResearch/hermes-agent/issues/38580)
    -   **`[Issue #38650] `hermes dump` 报告 MCP 服务器状态错误**。*未标注已有修复 PR。*
        -   链接: [Issue #38650](https://github.com/NousResearch/hermes-agent/issues/38650)
    -   **`[Issue #38651] 桌面端 Slash 命令不显示已安装技能**。*未标注已有修复 PR。*
        -   链接: [Issue #38651](https://github.com/NousResearch/hermes-agent/issues/38651)
    -   **`[Issue #38669] Web UI 聊天滚动条无法滚到底部**。*未标注已有修复 PR。*
        -   链接: [Issue #38669](https://github.com/NousResearch/hermes-agent/issues/38669)

## 6. 功能请求与路线图信号

今日收到的新功能请求主要围绕 **桌面端体验**、**远程连接** 和 **第三方平台集成**。结合已有的 PR，可以观察到项目可能的发展方向。

-   **桌面端增强**：
    -   **系统托盘支持** (`[Issue #38007]`): 要求桌面应用支持后台运行，关闭窗口后不退出。这是提升桌面端用户体验的高频需求。
    -   **开机自启选项** (`[Issue #38640]`): Windows 平台用户的基本需求。
    -   **远程 Profile 切换** (`[Issue #37713]`): 用户期望在桌面端 UI 中直接切换连接的远程 Hermes 后端的 Profile。
    -   **真·远程文件浏览器** (`[Issue #38671]`): 指出当前桌面端远程连接后，文件浏览器并未操作远程文件系统，存在逻辑混淆。这是一个重大的功能缺陷。
    -   **Mermaid 图表渲染** (`[Issue #38654]`): 要求桌面端 Markdown 预览支持 Mermaid 图表。

-   **平台集成提速**：
    -   **企业微信 (WeCom) 流式回复** (`[Issue #38641]` & `[PR #38660]`): 用户要求 WeCom 适配器支持流式消息编辑，这在聊天场景中至关重要。`[PR #38660]` 提出了使用 `aibot_respond_msg` 流协议实现该功能，并被标记为 P3 功能请求，表明项目有意向支持。
    -   **YouPet 企业微信桥接** (`[PR #38678]`): 提出的新概念，将 Hermes 聊天功能与企业级“YouPet Link OS”集成，这在企业级应用部署上是一个非常前沿的信号。

-   **核心功能形态**：
    -   **自动化工作区记忆** (`[Issue #38552]`): 提出 Agent 应能记住每个目录的用途，避免每次对话都从零开始学习文件系统，从而节约 token 并减少错误。这是一个很有前景的智能增强提议，与 #33856 互补。
    -   **桌面客户端独立安装** (`[Issue #38602]`): 希望将桌面端作为纯客户端，连接远程服务，避免在本地引导安装整个 Agent 运行时。这为降低桌面端使用门槛提供了可能。

## 7. 用户反馈摘要

从今日的 Issue 评论和报告中，可以提炼出以下典型用户声音：

-   **“我根本无法升级” (Windows)**: 用户 `everglow01` 在 #37881 中报告 `hermes update` 命令直接损坏了他的安装环境，这暴露了核心更新流程在指定平台上的脆弱性，是可能导致用户流失的严重问题。
-   **“对于视障用户，Hermes 几乎不可用”**: 用户 `xiaopinpin-music` 在 #26689 中的详细描述不仅是简单的 Bug 报告，更是对项目设计包容性的深刻反思，揭示了一个被忽视的关键用户群。
-   **“macOS 上运行几个我就崩了”**: 用户 `BournYSix` 在 #30230 中抱怨 macOS 系统的文件描述符限制导致服务中断，这是高级用户在高负载场景下遇到的资源管理短板。
-   **“为什么我的 Slack 审批按钮会绕过权限？”**: 用户 `coygeek` 高亮报告的安全问题（#38068）显示了用户对操作安全性的深切担忧，即使是简单的审批流程也存在被利用的风险。
-   **“远程模式下的文件浏览器是假的”**: 用户 `andrewkangkr` 在 #38671 中指出了一个严重的功能逻辑错误，这破坏了远程协作的核心体验，让用户感到被误导。

## 8. 待处理积压

今日未发现长期未响应或长时间未更新的待处理关键 Issue/PR。项目的 Issue 处理相当迅速。以下为值得长期关注的开放 PR 和 Issue：

-   **`[PR #38403] feat: add Concentrate AI as a model provider`**: 新的模型提供商集成请求，虽然目前评论数未知，但持续开放表明可能需要进行更深度的技术讨论或合规审查。
-   **`[Issue #26689] Accessibility improvements for blind VoiceOver users`**: 尽管已提出 19 天，但仍然开放。此关乎项目可访问性文化的核心问题需要长期追踪和规划。
-   **多个 Windows 相关 Issue** (#37881, #38407, #38618, #38156 等): 系统性风险信号，提醒维护者需要将 Windows 平台的稳定性和兼容性作为专项进行治理。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*