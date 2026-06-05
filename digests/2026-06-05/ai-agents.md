# OpenClaw 生态日报 2026-06-05

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-05 03:25 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据 OpenClaw (github.com/openclaw/openclaw) 2026-06-05 的 GitHub 动态数据生成的日报。

---

## OpenClaw 项目动态日报 | 2026-06-05

### 1. 今日速览

今日项目活跃度极高，24 小时内涌现了 500 条 Issue 与 500 条 PR 的更新，但无新版本发布。社区焦点集中在解决近期版本（2026.5.22 - 2026.6.1）引入的多个严重回归和稳定性问题上，例如 OpenAI ChatGPT Responses 传输失败、Matrix 线程回复失效以及 Session 上下文数据膨胀。尽管修复活动频繁，但近 400 个待合并的 PR 表明项目正面临严重的代码审查瓶颈，这可能延缓关键修复的落地，值得关注。

### 3. 项目进展 (重要 PR 与 Issue 动态)

今日项目在关键问题的修复上取得了实际进展，以下为已合并或关闭的重要变更：

- **修复 Mattermost 斜杠命令 503 错误**：PR [#90389](https://github.com/openclaw/openclaw/pull/90389) 修复了自 v2026.4.15 以来，Mattermost 斜杠命令返回永久性 503 “未初始化”错误的回归问题。该 PR 通过将插件状态锚定在 `globalThis` 上，解决了 JIT 加载导致的路由注册失败问题。 (关联 Issue: #68113)
- **修复 OpenAI ChatGPT Responses SSE 流处理**：PR [#90399](https://github.com/openclaw/openclaw/pull/90399) 修复了在特定情况下，ChatGPT-OAuth 成功返回有效 SSE 数据包但缺少 `content-type` 头，导致被误报为 `invalid_provider_content_type` 并拒绝服务的问题。(关联 Issue: #90382)
- **关闭 Codex-vs-Pi 运行时一致性 QA 框架跟踪**：Issue [#80171](https://github.com/openclaw/openclaw/issues/80171) 已关闭。该 Issue 跟踪了将 Codex 作为默认运行时背后的整合工作，其关闭标志着这一重大技术栈迁移的深度验证阶段取得阶段性成果。
- **修复模型 Fallback 机制回归**：Issue [#88039](https://github.com/openclaw/openclaw/issues/88039) 已关闭。该 Issue 报告了通过 `/model` 命令选择的Session模型被错误地包含在 Fallback 列表中的问题。此修复确保了故障切换逻辑的正确性。
- **关闭 Feishu 消息分发崩溃问题**：Issue [#88234](https://github.com/openclaw/openclaw/issues/88234) 已关闭，其报告的因 `TypeError` 导致飞书消息分发失败的 Bug 已被修复。

### 4. 社区热点

今日社区讨论热度最高的议题集中在版本升级后的兼容性问题和核心功能的可靠性上：

- **[Bug]: 2026.6.1 OpenAI ChatGPT Responses transport fails with invalid_provider_content_type for gpt-5.4/gpt-5.5** [#90083](https://github.com/openclaw/openclaw/issues/90083)
    - **热度**：3 个 👍，11 条评论。
    - **诉求**：升级至最新稳定版后，调用 OpenAI 高级模型（gpt-5.4/5.5）失败，影响核心推理能力。该问题已获得快速响应和修复 (PR #90399)，但用户仍需等待合并发布。
- **[Bug]: Repeated hard resets on same session key despite high reserveTokensFloor** [#63216](https://github.com/openclaw/openclaw/issues/63216)
    - **热度**：3 个 👍，11 条评论。
    - **诉求**：即使配置了极高的 Token 预留量，特定群组会话仍反复触发硬重置，严重破坏了对话连续性。用户对其中的 `retry loop re-injects bootstrap context` 机制表达了困惑和不满。
- **Cron state silently wiped during SQLite migration on upgrade to 2026.6.1** [#90072](https://github.com/openclaw/openclaw/issues/90072)
    - **热度**：3 个 👍，5 条评论。
    - **诉求**：从 v2026.5.28 升级到 v2026.6.1 时，SQLite 迁移过程静默清除了 44/45 个定时任务。这种“静默删除”行为引发了用户对数据安全和迁移可靠性的严重担忧，认为应至少提供备份或警告机制。

### 5. Bug 与稳定性

今日报告了多个优先级为 P1 的严重 Bug，主要围绕连接丢失、核心功能回归和会话状态损坏：

- **[P1] OpenAI ChatGPT Responses 传输失败** (Issue [#90083](https://github.com/openclaw/openclaw/issues/90083)): 核心 AI 接口在 v2026.6.1 上对新模型失效。已有修复 PR #90399。
- **[P1] Matrix 线程回复回归 + `/status` 沉默** (Issue [#87307](https://github.com/openclaw/openclaw/issues/87307)): v2026.5.22 版本后，Matrix 频道中 Bot 回复无法正确线程化，且 `/status` 等命令无响应。
- **[P1] 活跃内存断路器过于激进，生效后注入垃圾 Prompt** (Issue [#90082](https://github.com/openclaw/openclaw/issues/90082)): v2026.6.1 中，`active-memory` 插件的熔断机制在打开后，会向主会话注入无意义的“请重试”字符串，污染会话并导致模型理解混乱。
- **[P1] Session 模型路由漂移** (Issue [#90036](https://github.com/openclaw/openclaw/issues/90036)): 在原生 Codex 运行时时，配置的模型路由（如 `openai/gpt-5.5`）会被自动切换到内部 `openai-codex/gpt-5.5` 路径，引发兼容性问题。
- **[P1] Feishu 流式卡片打字机效果异常及内容截断** (Issue [#88929](https://github.com/openclaw/openclaw/issues/88929)): 飞书频道启用流式卡片渲染时，出现逐字输出和最终内容只剩一个字符的 UI Bug。

### 6. 功能请求与路线图信号

今日有一项新的功能请求及多个已存在的特色功能请求，显示出社区对**安全合规**和**模型能力扩充**的强烈需求：

- **[Feature] 敏感数据脱敏** (Issue [#64046](https://github.com/openclaw/openclaw/issues/64046)): 用户提议对配置文件（`openclaw.json`）、日志界面和 UI 中的 API Key、Token 等敏感信息进行脱敏处理。该请求被标记为 P1，且涉及安全域，很可能在下一轮安全审查中被优先考虑。
- **[RFC] 控制 UI 插件贡献槽** (Issue [#71736](https://github.com/openclaw/openclaw/issues/71736)): 一个设计讨论（RFC），旨在为插件提供标准化的 UI 插槽（如聊天模式、审批卡片、输入守卫等），以增强 Plan 模式等核心功能的扩展性。这反映了平台化的规划方向。
- **[Feature] 支持 Anthropic advisor 工具** (Issue [#63930](https://github.com/openclaw/openclaw/issues/63930)): 该功能请求已存在数月，要求支持 Anthropic 的 beta 版“顾问工具”，该功能允许 Claude 在推理过程中咨询另一个模型实例，以增强复杂任务处理能力。若被纳入路线图，将是重要的能力扩展。

### 7. 用户反馈摘要

从今日的 Issue 讨论中，可以提炼出以下真实用户痛点和场景：

- **升级恐惧症**：多位用户反馈，从 v2026.5.20/5.28 升级到 `2026.5.22` 或 `2026.6.1` 等“稳定版”后，遇到了**静默数据丢失**（如 Cron 任务）和**核心功能回归**（如 Matrix 回复、SSH 连接）。这表明近期版本的测试和向后兼容性验证有待加强。
- **对话上下文敏感性问题**：用户抱怨 Telegram 的 **JSON 元数据前缀** (Issue #72704) 和 **系统事件（心跳）打断用户回复** (Issue #64810) 严重影响了模型对意图的理解和对话的自然流畅度。这揭示了“平台适配”过程中，数据清洗和上下文管理需要更精细的打磨。
- **“黑盒”问题反馈**：对于 `active-memory` 断路器等内部机制，当它们触发时，用户看到的是“请重试”这样的**无用提示**，而不是清晰的状态说明 (Issue #90082)。用户期望能获得更多透明度，以了解代理内部发生了什么，而不是看到一个“黑盒”错误。

### 8. 待处理积压

以下为长期未得到充分响应或处理停滞的重要 Issue/PR，提醒维护者关注：

- **[P2] memory_search hybrid mode not returning FTS matches** (Issue [#48300](https://github.com/openclaw/openclaw/issues/48300)): 创建于 3 月，详细报告了混合搜索模式下全文搜索（FTS）结果缺失的 Bug。至今已有多条评论和复现步骤，但停留在 `no-new-fix-pr` 状态。
- **[P2] Doctor warns about NVM node instead of Homebrew/system node, but cannot be fixed** (Issue [#60612](https://github.com/openclaw/openclaw/issues/60612)): 一个困扰 macOS 用户的环境治理问题，openclaw doctor 会给出无法被用户修复的警告，原因是程序自身会覆盖启动配置文件。涉及用户信任和工具易用性。
- **[P2, stale] Control UI plugin contribution slots** (Issue [#71736](https://github.com/openclaw/openclaw/issues/71736)): 一个重要的设计提案（RFC），关注平台未来架构的扩展性。目前处于待维护者审阅和产品决策的状态，持续的搁置可能阻碍相关生态建设。
- **[P1, 有 PR] Codex OAuth refresh failures can wedge an agent** (Issue [#86215](https://github.com/openclaw/openclaw/issues/86215)): 这是一个影响用户使用体验的严重问题，当 OAuth Token 过期后，代理会卡住数小时而无法恢复。虽然已有相关的修复 PR #84265，但该 PR 已停滞多日，标记为 `waiting on author`，需跟进。

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，以下是根据您提供的两份项目动态日报（OpenClaw & Hermes Agent）生成的横向对比分析报告。

---

### AI 智能体与个人 AI 助手开源生态横向分析报告 | 2026-06-05

#### 1. 生态全景

今日，AI 智能体与个人 AI 助手开源生态呈现出 **“高活跃度、强阵痛期、分层发展”** 的总体态势。核心项目如 OpenClaw 和 Hermes Agent 均处于高频迭代阶段，但社区反馈的焦点已从“功能探索”转向“稳定性和可靠性”。具体表现为：**版本升级带来的回归问题**（数据静默丢失、核心功能失效）成为用户最主要的痛点，而 **多用户场景下的权限管理** 则成为最强烈的功能需求。这表明该生态正从早期采用者的“尝鲜”阶段，步入早期大众用户的“可用与可控”阶段，稳定性与平台化能力成为当前竞争的关键。

#### 2. 各项目活跃度对比

| 项目名称 | 今日 Issue 数 | 今日 PR 数 | 版本发布 | 代码审查效率（参考） | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | ~500（更新） | ~500（更新） | 无 | **瓶颈**（近 400 个待合并 PR） | **高活跃，但存在开发效能瓶颈和稳定性风险** |
| **Hermes Agent** | ~100（更新） | ~100（更新） | 无 | **较高**（关闭 12 Issues，合并/关闭 6 PRs） | **快速迭代，社区响应迅速，但桌面端存在较严重的入口问题** |

**分析**:
- **OpenClaw** 的开发规模是 Hermes Agent 的约 5 倍，但其庞大的 PR 积压量 (`~400`) 表明代码审查与合并流程存在严重瓶颈，这可能延缓严重 Bug 的修复速度，并引发“升级恐惧症”等社区负面情绪。
- **Hermes Agent** 的体量虽小，但维护效率更高，社区功能请求能迅速转化为 PR（如 `#39492` 到 `#39531`），表明其协作流程更流畅，对社区反馈的响应更敏捷。

#### 3. OpenClaw 在生态中的定位

- **核心参照与标准制定者**：项目描述明确其为“核心参照”，其技术路线（如推进 Codex 运行时）和功能集合（如 Mattermost 集成、ChatGPT-OAuth）对其他项目有标杆和引领意义。
- **优势**：
    - **功能广度与深度**：全面覆盖 OpenAI、Matrix、Mattermost、Feishu 等多种平台与协议，功能复杂度高，是追求“全功能”智能体的首选。
    - **生态整合深度**：与 OpenAI 等模型提供商的深度耦合，以及对自身插件的精细化控制，显示出其技术栈的深厚积累。
- **技术路线差异**：OpenClaw 更侧重于 **统一运行时（Codex）和平台兼容性**，追求一套系统支撑多种使用场景。其 Bug 报告中大量关于“回归”和“迁移”的问题，正是其技术栈高度集成、版本迭代复杂化的直接后果。
- **社区规模对比**：OpenClaw 的社区讨论规模（24小时500条）远超 Hermes Agent（100条），表明其开发者社区和用户基础更为庞大，但同时也意味着问题反馈和噪音更多，维护压力更大。

#### 4. 共同关注的技术方向

两个项目今日的动态强烈指向以下共同的技术方向：

| 共同趋势 | 涉及项目 | 具体诉求 |
| :--- | :--- | :--- |
| **权限管理与多用户支持** | **Hermes Agent** (`#527`)、**OpenClaw** (敏感的 `openclaw.json` 脱敏 RFC `#64046`) | 从“个人”工具走向“团队/企业”协作环境下，**细粒度的角色权限控制**和**敏感信息隔离**成为刚性需求。 |
| **内存/上下文管理** | **OpenClaw** (`#63216` Session膨胀、`#90082` 活跃内存熔断)、**Hermes Agent** (`#39492` 禁用内存工具) | 用户开始关注智能体的长对话能力与资源消耗的平衡，要求更**透明、可控的内存与上下文管理机制**，甚至允许用户按需启用/禁用。 |
| **平台扩展与适配** | **OpenClaw** (修复 Feishu/Matrix)、**Hermes Agent** (接入 OneBot QQ) | 打通更多即时通讯平台是共性趋势，但适配难度（如 Feishu 流式渲染、Matrix 线程化）和由此引入的 Bug 也显著增加。 |
| **安全与合规** | **OpenClaw** (`#64046` 数据脱敏)、**Hermes Agent** (`#9560` 路径遍历漏洞修复、`#39467` aiohttp 更新) | 安全不再是“可选项”，而是基本盘。两个项目都在处理从API密钥泄露到底层依赖的漏洞，反映出生态对**数据安全和系统健壮性**的重视。 |
| **模型能力扩展** | **OpenClaw** (`#63930` Anthropic顾问工具)、**Hermes Agent** (`#39507` 模型配置文件) | 用户不再满足于单一模型，而是探索**多模型协作**（顾问工具）、**快速模型路由切换**（配置文件）等更高级的用法，以应对复杂任务。 |

#### 5. 差异化定位分析

| 维度 | **OpenClaw** | **Hermes Agent** |
| :--- | :--- | :--- |
| **功能侧重** | **平台化、全功能、可编程**。追求一个 Agent 覆盖所有场景，支持复杂的插件生态和运行时。 | **多用户、桌面优先、敏捷扩展**。强调 Gateway 组件作为协作中心，注重桌面端体验和社区平台（如 QQ）的快速接入。 |
| **目标用户** | **重度开发者、系统管理员、追求终极自动化的技术团队**。需要处理复杂的集成、迁移和性能调优。 | **个人开发者、小团队、新兴平台用户（如QQ）**。更看重易用性、功能快速落地和对社区的响应速度。 |
| **技术架构** | **大一统架构**。所有功能深度集成，代码量巨大，导致版本升级风险高。 | **组件化、网关分离**。核心组件（Gateway, Desktop）相对独立，便于快速修复和功能迭代，但也带来了桌面端等子系统的稳定性问题。 |

#### 6. 社区热度与成熟度

- **快速迭代与功能探索阶段**：**Hermes Agent** 处于此阶段。虽然 Bug 多（尤其是桌面端），但功能请求（权限、MCP）和社区 PR 转化迅速，项目整体向上趋势明显，充满了“开疆拓土”的活力。
- **质量巩固与稳定性攻坚阶段**：**OpenClaw** 处于此阶段。其社区活动主体不再是新功能，而是对 **“回归Bug”** 和 **“平台迁移问题”** 的修复和抱怨。这标志着项目已进入成熟期，庞大的用户基数暴露了更复杂的可靠性挑战，维护者的重心必须从“加法”转向“提质”。

#### 7. 值得关注的趋势信号

1.  **“升级恐惧症”成为开发者普遍痛点**：OpenClaw 用户对版本升级导致的数据丢失（Cron 任务、Session 重置）和功能回归（Matrix 回复）表现出强烈不满。这警示所有智能体项目：**必须建立严格的 CI/CD 测试和版本升级指南**，否则将快速消耗社区信任。
2.  **从“工具”到“平台”的演进刚需**：细粒度权限管理在两个项目中同时涌现，且呼声极高，这是 AI 智能体从单用户“玩具”走向多用户“平台”的明确信号。开发者应考虑在初期架构中预留多租户和角色能力。
3.  **对“黑盒”系统的抗议**：OpenClaw 用户对 `active-memory` 断路器给出“请重试”等无用错误信息感到不满。**可解释性是提升用户信任的关键**。智能体需要向用户清晰报告其内部状态和决策路径，而非隐藏在一个“黑盒”中。
4.  **桌面端入口的重要性与脆弱性**：Hermes Agent 的大量桌面端 Bug 报告表明，桌面应用作为个人 AI 助手最直接的入口，其稳定性和用户体验直接决定了产品的成败。一个容易崩溃或启动失败的桌面应用会扼杀任何技术优势。
5.  **社区响应速度是核心竞争力**：Hermes Agent 在数小时内将一个 Issue 转化为 PR 的能力，迅速解决了用户痛点，缓解了负面情绪。在生态竞争初期，**敏捷的社区治理和高效的协作流程** 是吸引和留住开发者的重要法宝。

**对 AI 智能体开发者的参考价值**:
- 在规划新功能时，优先考虑**权限系统**和**上下文管理的可配置性**。
- 投入足够的资源建设 **自动化测试和回滚机制**，以应对版本升级带来的恐惧。
- 将**错误信息和诊断能力**作为一等公民对待，让用户了解 Agent 的决策过程。
- 如果开发桌面端应用，必须将其稳定性放在首位，并准备好应对网络中断、休眠恢复等复杂场景。
- 培养一个 **快速响应社区需求** 的维护团队文化，将大大增加项目成功的概率。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的《Hermes Agent》GitHub 数据，我为您生成了 2026-06-05 的项目动态日报。

---

### **Hermes Agent 项目动态日报 | 2026-06-05**

#### **1. 今日速览**

今日 Hermes Agent 项目社区活跃度极高，共计产生 100 条 Issues 和 PRs 的更新，显示出强大的社区驱动力。项目在 **权限管理** 和 **内存工具控制** 等关键功能上获得了用户强烈关注，但同时 **桌面端应用的稳定性和启动问题**（特别是 v0.15.x 版本）成为焦点，大量 Bug 报告涌入。尽管没有新版本发布，但核心团队通过关闭 12 个 Issues 和合并/关闭 6 个 PRs 维持了较高的维护效率，项目整体处于 **高活跃度、高问题反馈、快速迭代** 的状态。

#### **2. 版本发布**

无新版本发布。

---

#### **3. 项目进展**

今日合并/关闭的 PR 主要集中在基础设施修复和安全加固上，体现了项目在快速迭代中对稳定性的重视。

- **修复安装问题**：PR [#39518](https://github.com/NousResearch/hermes-agent/pull/39518) 已关闭并合并，修复了破损的 `rebuild venv` 逻辑，解决了部分用户（特别是 Mac 用户）的安装失败问题。
- **安全依赖更新**：PR [#39467](https://github.com/NousResearch/hermes-agent/pull/39467) 将 `aiohttp` 依赖从 `3.13.3` 更新至 `3.14.0`，以解决一个严重级别高达 9.1 的安全公告。此举增强了后端网络通信层的安全性。
- **会话安全加固**：针对 Gateway 组件的 PR [#9560](https://github.com/NousResearch/hermes-agent/pull/9560) 关闭，修复了 `session.py` 中的高危路径遍历漏洞 (CWE-22)，强化了网关会话管理。相关修复还包括对 `--replace` 命令的配置文件一致性检查 (PR [#30196](https://github.com/NousResearch/hermes-agent/pull/30196)) 和 `auth remove` 命令的资源清理逻辑 (PR [#24395](https://github.com/NousResearch/hermes-agent/pull/24395))。
- **平台功能拆分与准备**：由社区贡献的 `feat(onebot): add shared OneBot client` PR [#38037](https://github.com/NousResearch/hermes-agent/pull/38037) 和 `feat(qq): add OneBot voice send tool` PR [#38088](https://github.com/NousResearch/hermes-agent/pull/38088) 仍在开放中。前者作为基础性拆分 PR，为支持 QQ 等新平台铺平了道路，显示出项目的平台扩展仍在稳步推进。

---

#### **4. 社区热点**

- **#527 [Feature]: Gateway Permission Tiers**：这是一个热度极高的长期 Issue（已存在 3 个月，今天仍有新评论）。用户对 **细粒度的角色权限控制**（如 Owner/Admin/User/Guest）的需求非常强烈，当前“非黑即白”的授权模式正在成为多用户部署的瓶颈。这反映了项目从个人工具向团队/企业级协作平台演进的强烈用户呼声。
  [链接](https://github.com/NousResearch/hermes-agent/issues/527)

- **#39492 & #39531：内存工具开关与社区快速响应**：用户 `MyQiongbao` 提出需要一个配置项来禁用内置的 `memory` 工具，以在多用户网关场景中避免会话干扰。该需求在数小时内就得到了社区回应，并迅速转化为 PR [#39531](https://github.com/NousResearch/hermes-agent/pull/39531)。这展现了一个 **响应迅速、协作高效** 的社区生态。
  [链接](https://github.com/NousResearch/hermes-agent/issues/39492)

- **#39365 & #39505：桌面端应用的稳定性之痛**：关于桌面端的 Bug 报告成为了今日的另一个焦点。`mroberts1` 抱怨令人困惑的错误提示（`OpenRouter API key missing` 实为网关认证失败），而 `Pauliehedron` 则遇到了应用首次启动时的无限循环崩溃。这些问题直接影响了最终用户的首次使用体验，是当前最突出的痛点之一。
  [链接](https://github.com/NousResearch/hermes-agent/issues/39365) | [链接](https://github.com/NousResearch/hermes-agent/issues/39505)

---

#### **5. Bug 与稳定性**

今日报告的 Bug 数量众多，主要集中在桌面应用 (v0.15.x) 和 CLI 的稳定性上。

- **严重**
    - **桌面应用无限启动循环**：`#39505` 报告了 Electron 应用因 `uvicorn` 子包安装不完整导致的后端崩溃和无限重启。已有修复 PR [#39530](https://github.com/NousResearch/hermes-agent/pull/39530)。
    - **桌面应用崩溃/白屏**：`#39525` 报告了关盖休眠或切换网络后应用失败。`#39484` 报告了 Mac 版首次安装后白屏。
- **高**
    - **桌面应用启动参数错误**：`#39503` 指出 v0.15.1 版本存在 `--tui` 参数冲突，导致应用无法启动。
    - **误导性错误信息**：`#39365` 指出当网关认证失败时，错误提示错误地指向了 OpenRouter API Key，极具迷惑性。
    - **`/stop` 命令清理不彻底**：`#39489` 指出该命令仅杀死后台进程，而未清理 Docker 沙箱环境，可能导致资源泄露。
    - **CLI 会话恢复报错**：`#39469` 报告了 `rich` 库的 MarkupError，导致无法正常恢复旧的 CLI 会话。
- **中**
    - **子会话丢失**：`#39471` 指出某些分支会话会从列表中“消失”，但并未删除，属于可见性 Bug。
    - **CLI 因 MCP 重启冻结**：`#39418` 指出 `/reload-mcp` 命令会导致终端完全无响应。
    - **Mac 上 CJK 输入错误**：`#39457` 报告了在 macOS 上输入中日韩文字时，未确认的预编辑文本会被丢弃。

---

#### **6. 功能请求与路线图信号**

许多功能请求与今日的 Bug 和热点紧密相关，显示了社区对以下方向的强烈期待：

- **更精细的权限管理**：`#527` 提出的角色权限控制是 **最大规模的功能呼声**，很可能被纳入中长期路线图。
- **模块化与可配置性**：
    - `#39492` 提出禁用内置内存工具，凸显了用户对核心功能模块进行插拔式管理的需求。对应的 PR `#39531` 表明这一功能将很快被采纳。
    - `#39523` 提出初始化 `HOME` 桥接目录，以解决沙箱环境子进程无法找到 Keychain/SSH/Git 等资源的问题。这涉及高级用户对沙箱环境的精细化控制需求。
- **新平台接入**：一系列关于 OneBot (QQ) 协议的 PR 正在推进（`#38037`, `#38088`, `#32140`），表明项目正在积极扩展对 **中文/亚太地区即时通讯平台** 的支持。
- **用户界面优化**：
    - `#39509` 提出展示 OpenClaw 无法处理的实例，意在推动 Agent 自动创建 `skill.md` 功能的边界。
    - `#39507` (Draft) 提出的“模型配置文件”概念，旨在不切换整体 Profile 的情况下快速切换模型路由，适合高级用户和测试场景。
    - `#39468` 提出的“系统托盘”功能，表明用户希望桌面端应用能像常驻后台服务一样运行。

---

#### **7. 用户反馈摘要**

从今日的 Issues 中可以提炼出以下真实用户反馈：

- **痛点：桌面端入门门槛高**。大量有关安装崩溃、启动失败、更新后无法使用的反馈。用户 `ramk18`、`Pauliehedron`、`vantang` 都遇到了不同形式的启动问题，表明 v0.15.1 桌面版的打包和首次引导流程存在严重缺陷。
- **痛点：环境恢复不佳**。用户 `crazylionwsw`（笔记本休眠/换网失败）、`MusePredator`（长对话切换会话后丢失焦点）和 `Yashwant00CR7`（CLI 被冻结）等问题反映了应用在各种复杂使用场景下，对网络变化、状态持久化和恢复的处理脆弱。
- **使用场景：多用户/网关部署**。`MyQiongbao` 和 `teknium1` 的诉求都指向了将 Hermes 用于团队协作的场景，对 **会话隔离、权限控制、角色管理** 有强烈需求。这是项目商业化或专业化的重要信号。
- **满意点：社区响应速度快**。尽管存在诸多 Bug，但用户 `MyQiongbao` 提出的 Feature Request 在几小时内就被转化为 PR 的事实，表明社区和核心团队对有价值的反馈处理非常积极，这有助于提升用户留存和贡献意愿。

---

#### **8. 待处理积压**

- **高安全性 PR 等待合并**：PR [#9560](https://github.com/NousResearch/hermes-agent/pull/9560) 作为修复高危漏洞（CWE-22）的 PR，虽已关闭但未提及合并状态，需关注其是否已合入 `main` 分支。
- **长期开放的 Hot Issue**：Feature Request `#527` (Gateway Permission Tiers) 已开放 3 个月且热度不减，是社区呼声最高的需求。维护者应评估将其纳入近期路线图的可能性，或给出明确的阶段性回应，以避免社区期望过高或流失。
- **长期未合并的 PR**：PR [#31292](https://github.com/NousResearch/hermes-agent/pull/31292) (MCP Registry metadata) 和 PR [#22648](https://github.com/NousResearch/hermes-agent/pull/22648) (Ollama Cloud web provider) 已开放超过 2 周，代表了社区在 MCP 生态和本地模型集成方面的贡献，建议核心团队尽快审阅，避免积压。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*