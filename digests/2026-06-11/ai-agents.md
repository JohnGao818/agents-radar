# OpenClaw 生态日报 2026-06-11

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-11 03:33 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 OpenClaw GitHub 数据，我为您生成了 2026 年 6 月 11 日的项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-06-11

### 1. 今日速览

OpenClaw 项目在过去 24 小时内展现出极高的社区活跃度，Issue 和 PR 更新量均达到 500 条，说明项目正处于密集的开发与反馈迭代期。安全加固与会话/消息状态稳定性是今日更新的核心主题，新发布的 `v2026.6.6-beta.1` 版本进一步收紧了安全边界。然而，大量的待办事项（469 个活跃 Issue，396 个待合并 PR）也反映出维护者面临严重的审查与合并压力。值得注意的是，多个被评为最高优先级的 “钻石龙虾” Bug 持续积压，对项目稳定性构成潜在风险。

### 2. 版本发布

- **v2026.6.6-beta.1**: [查看发布详情](https://github.com/openclaw/openclaw/releases/tag/v2026.6.6-beta.1)
  - **更新重点**：此版本是一次重大的安全加固迭代，显著收紧了多个组件的安全边界，包括：
    - 转录（transcripts）、沙箱绑定（sandbox binds）和主机环境继承（host environment inheritance）。
    - MCP stdio、Codex HTTP 访问和原生搜索策略（native search policy）。
    - 针对已删除代理的 ACP 旁路（deleted-agent ACP bypasses）、环回工具（loopback tools）等。
  - **破坏性变更**：未明确列出，但安全边界的收紧可能导致部分依赖旧行为的自定义配置或插件出现问题。
  - **迁移注意事项**：用户在升级后应检查其配置文件，特别是与沙箱、外部服务和工具权限相关的部分，确保一切正常工作。强烈建议在升级前查阅完整的发布说明。

### 3. 项目进展

过去 24 小时内，共有 104 个 PR 被合并或关闭，表明项目进展稳健。以下是一些关键的进展点：

- **会话状态修复**：
  - PR #90128 `fix(sessions): preserve user /model override across daily/idle session rollover` [已关闭]：修复了用户在会话每日/空闲重置时，手动指定的 `/model` 覆盖被静默丢失的问题，确保了用户偏好的持久化。
  - PR #84938 `fix: forward reasoning_content from OpenAI-compatible providers` [已关闭]：修复了网关丢弃 MiMo v2.5 等兼容 OpenAI API 提供商返回的 `reasoning_content` 字段的问题，使推理过程内容得以正确传递。
- **平台集成与兼容性**：
  - PR #77359 [已关闭]：修复了在多 Discord 机器人账号设置中，非默认账号斜杠命令无法注册的 Bug，提升了多账号部署的可靠性。
  - PR #92072 `fix(gateway): treat google-gemini-cli Gemini models as image-capable` [新提交]：修复了谷歌 Gemini CLI 模型在网关被错误地视为不支持图片输入的问题，解除了部分 Gemini 模型的限制。
- **工具与功能加固**：
  - PR #92005 `fix(browser): add force parameter to click action` [新提交]：为浏览器工具的 `click` 动作新增 `force` 参数，以绕过 React/Vue 等现代前端框架严格的元素可操作性检查，提升了自动化测试的健壮性。

### 4. 社区热点

今日讨论最为集中的议题反映了用户对 **数据隐私、会话一致性和系统可靠性** 的深切关注。

- **#25592: Text between tool calls leaks to messaging channels** [评论: 31] [活跃中](https://github.com/openclaw/openclaw/issues/25592)
  - **诉求分析**：这是今日最热门的问题，用户强烈要求将代理的内部处理文本（如错误处理、处理中确认）与对外通信严格隔离。这不仅是用户体验问题，更关乎敏感内部状态泄露的**安全风险**。该 Issue 状态为“P1, 安全影响”，表明其高优先级。
- **#44925: [Bug]: Subagent completion silently lost** [评论: 19] [活跃中](https://github.com/openclaw/openclaw/issues/44925)
  - **诉求分析**：用户对一个“P1, 钻石龙虾”级 Bug 表达了强烈不满。子任务在多种情况下（如超时、完成通知失败）会静默失败，且毫无通知或自动恢复机制。这破坏了用户对多代理编排功能的**信任**和**可靠性预期**，是影响项目核心价值的关键问题。
- **#88838: Track core session/transcript SQLite migration via accessor seam** [评论: 19] [活跃中](https://github.com/openclaw/openclaw/issues/88838)
  - **诉求分析**：此 Issue 由项目成员提出，讨论如何安全地将核心会话/转录运行时状态迁移到 SQLite。高评论数表明社区对**架构演进**和**数据可靠性**的浓厚兴趣。用户希望避免大规模重写，以“小步快跑”的方式推进，确保系统稳定。

### 5. Bug 与稳定性

过去 24 小时内报告了大量 Bug，以下按严重程度排列：

- **P0/关键**:
  - **#88838**: Track core session/transcript SQLite migration via accessor seam
- **P1/高**:
  - **#25592**: Text between tool calls leaks to messaging channels (安全/消息丢失)
  - **#44925**: Subagent completion silently lost (会话状态/消息丢失) - *已有相关PR在讨论*
  - **#32296**: Agent replies to previous message instead of current message (会话状态/消息丢失)
  - **#29387**: Bootstrap files in agentDir are silently ignored (会话状态/安全)
  - **#31583**: `exec` tool does not inherit `skills.entries.*.env` environment variables (安全/回归) - *已有PR #47523 尝试修复*
  - **#43661**: Session hangs indefinitely when compaction times out (会话状态/消息丢失/崩溃循环)
  - **#83184**: Heartbeat-driven agent replies leave pendingFinalDelivery stuck (会话状态/消息丢失)
  - **#38327**: "Cannot convert undefined or null to object" error with Google Vertex (回归/崩溃循环) - *已有关联PR*
- **P2/中**:
  - **#32473**: control ui requires device identity (安全/回归)
  - **#41744**: Feishu: read image tool result loses media (消息丢失)
  - **#40001**: Write tool lacks append mode (数据丢失)
  - **#40540**: `openclaw update` command fails with EBUSY error on Windows (行为Bug/回归)
  - **#45314**: Early abort response templates are not populated (行为Bug)
- **回归问题**:
  - **#31583, #32473, #38439, #43747, #41201, #38327**: 多个回归问题表明近期发布可能引入了未经充分测试的破坏性变更，需要加强回归测试流程。

### 6. 功能请求与路线图信号

社区提出的功能请求指向了 **安全、可控性、集成深度和用户体验** 四个方向。

- **安全与可控性**：
  - **#39604**: [Add tools.web.fetch.allowPrivateNetwork](https://github.com/openclaw/openclaw/issues/39604) (👍9): 用户希望可以灵活开启对私有网络的访问，而非一刀切地禁止。
  - **#39979**: [Path-scoped RWX permissions](https://github.com/openclaw/openclaw/issues/39979): 提出更精细的文件执行权限模型，显示社区对细粒度权限控制的需求。
- **性能与成本**：
  - **#42475**: [Per-agent cost budget enforcement](https://github.com/openclaw/openclaw/issues/42475): 提出按代理设置成本预算，是运营大型部署的常见需求。
  - **#22438**: [Tiered bootstrap file loading](https://github.com/openclaw/openclaw/issues/22438): 针对大工作区优化令牌消耗，表明用户对降低成本和提高效率的迫切期望。
- **功能扩展**：
  - **#18160**: [Direct Exec Mode for Cron Jobs](https://github.com/openclaw/openclaw/issues/18160) (👍10): 希望 Cron 任务能直接执行命令，绕过LLM，以提高效率和可靠性。
  - **#43260**: [Support model field in SKILL.md](https://github.com/openclaw/openclaw/issues/43260): 要求在 Skill 级别指定模型，实现计算资源的精细调度。
  - **PR #78441**: `feat(subagents): forward toolsAllow from sessions_spawn` [待合并]: 该 PR 正在推进子代理工具权限的继承，与#39979 路径权限请求逻辑一致，很可能会被纳入下一版本。

### 7. 用户反馈摘要

从 Issue 评论中提炼出的真实用户反馈：

- **痛点**:
  - **“静默失败”**：用户对子任务 (`#44925`) 和会话上下文 (`#32296`) 出现问题但毫无通知感到非常沮丧，这直接破坏了信任。
  - **“配置无效”**：无论是 Agent 目录下的 bootstrap 文件被忽略 (`#29387`)，还是没有为私有网络访问提供配置 (`#39604`)，都让用户感到系统的灵活性不足。
  - **“回归噩梦”**：多个回归 Bug（如 `#31583`, `#32473`）让用户在升级后工作流中断，打击了用户更新和信赖新版本的积极性。
  - **“调试困难”**：在 Discord (`#44905`) 或 Slack 中看到内部工具调用痕迹，以及浏览器工具无法点击现代 UI 元素 (`PR #92005`)，都增加了用户的理解和调试成本。
- **使用场景**:
  - **多机器人部署**：`#77359` 的修复说明项目被广泛应用于复杂的、多账号的 Discord 和 Slack 场景。
  - **国际化环境**：`#85888` 中关于 MiniMax (中国) API 的问题，以及 `#41744` 的飞书集成问题，表明项目在海外市场和国际团队中也有广泛应用。
- **满意点**:
  - 用户对 OpenClaw 强大的**插件与扩展能力**（如 `PR #82534` 的内存-wiki 页面分组）、**高级功能**（如会话子代理、浏览器自动化）表示认可，尽管这些功能还存在不稳定因素。

### 8. 待处理积压

以下 Issue 和 PR 长期处于开放或停滞状态，对项目健康度构成潜在威胁，建议维护者优先关注：

- **关键问题**:
  - **#25592**: `Text between tool calls leaks` (已开放 108 天): 这是一个 P1 级的安全/UX 问题，社区热度极高，需要尽快给出产品决策。 [链接](https://github.com/openclaw/openclaw/issues/25592)
  - **#29387**: `Bootstrap files in agentDir are silently ignored` (已开放 104 天): P1 级，且是社区普遍遇到的基础配置问题。 [链接](https://github.com/openclaw/openclaw/issues/29387)
  - **#32296**: `Agent replies to previous message` (已开放 101 天): 影响核心会话体验的 P1 级 Bug。 [链接](https://github.com/openclaw/openclaw/issues/32296)
- **长期未响应的功能请求**:
  - **#18160**: `Direct Exec Mode for Cron Jobs` (👍10, 已开放 116 天): 社区反馈强烈，但似乎缺乏产品侧决策。 [链接](https://github.com/openclaw/openclaw/issues/18160)
  - **#22358**: `Post-subagent completion extension hook` (已开放 111 天): 有明确的用例，但对项目的贡献有限，可能需要更多社区力量推动。 [链接](https://github.com/openclaw/openclaw/issues/22358)
- **停滞的 PR**:
  - **#47277**: `feat: add user-specific memory isolation` (已开放 88 天): 一个对多用户场景非常重要的功能，但状态仍为“等待证明”。 [链接](https://github.com/openclaw/openclaw/pull/47277)
  - **#47523**: `Agents: tighten tool name trust` (已开放 88 天): 一个重要的安全加固 PR，处于“等待维护者审查”状态。 [链接](https://github.com/openclaw/openclaw/pull/47523)

---

## 横向生态对比

好的，作为资深技术分析师，基于您提供的OpenClaw和Hermes Agent两份详尽的日报，我为您生成了以下面向技术决策者和开发者的横向对比分析报告。

---

### **AI智能体与个人AI助手开源生态横向对比分析报告（2026-06-11）**

#### **1. 生态全景**

今日，个人AI助手/自主智能体开源生态呈现 **“分裂式繁荣”** 的态势。一方面，以OpenClaw为代表的全能型平台正在经历 **大规模、高密度的功能迭代与安全加固**，但巨大的社区需求与维护者审查能力之间的矛盾日益尖锐。另一方面，以Hermes Agent为代表的项目则展现出对 **特定场景深度优化**（如Docker、Mac、Telegram）和 **基础架构稳定性** 的追求。两个项目共同反映出社区的核心关切已从“能否实现功能”转向 **“功能是否可靠、安全且跨平台一致”**。数据隐私、会话状态一致性以及故障透明化成为所有开发者无法回避的共同挑战。

---

#### **2. 各项目活跃度对比（2026-06-11）**

| 指标 | **OpenClaw** | **Hermes Agent** | **解读** |
| :--- | :--- | :--- | :--- |
| **今日Issue/PR总更新量** | 500+ | 100 | OpenClaw社区规模与迭代速度远超Hermes Agent |
| **今日新增/待处理Issue** | 469个活跃Issue；多个P0/P1级Bug | 未明确总数，但有多个新报告P1级Bug | 两项目均面临显著的质量控制压力 |
| **今日新增/待合并PR** | 396个待合并PR | 50个左右待合并PR | OpenClaw的PR积压问题极为严重，审查效率或成瓶颈 |
| **近期版本发布** | ✅ **有** （v2026.6.6-beta.1，重磅安全更新） | ❌ **无** | OpenClaw处于快速发布周期，Hermes Agent处于功能深耕阶段 |
| **核心Bug趋势** | **安全/消息丢失** 问题井喷，多个“钻石龙虾”级Bug积压 | **平台兼容性崩溃**（Mac、Docker）与**核心会话异常**并存 | OpenClaw的复杂度引发了更多的边缘情况；Hermes Agent在平台化拓展中遇到稳定性挑战 |
| **社区健康度评估** | ⚠️ **高风险高回报**：核心功能强大，但积压问题严重，可能影响新用户信心 | ⚠️ **稳健但有瓶颈**：社区活跃度虽低但仍聚焦，维护者合并效率是制约因素 |

---

#### **3. OpenClaw在生态中的定位**

*   **技术路线优势**：OpenClaw是**全能型平台**的代表，追求“单项目覆盖一切”。其核心优势在于：
    1.  **高集成密度**：浏览器工具、子代理编队、复杂沙箱、多平台网关（Discord, Slack, Feishu）等深度集成。
    2.  **业务级可定制性**：`SKILL.md`, `bootstrap` 文件、路径权限等，提供了强大的工作流与权限控制能力。
    3.  **快速的功能前移**：社区提出的功能（如路径级权限#39979）能迅速转化为PR，创新活跃。
*   **与同类对比**：
    *   **相比Hermes Agent**：OpenClaw功能更全面、架构更复杂、社区规模更大，但同时也更不稳定，对用户的技术能力要求更高。
    *   **相比其他未提及项目（假设）**：OpenClaw更像“智能体领域的Kubernetes”，强大而复杂。而Hermes Agent则更接近“智能体领域的Homebrew”，提供针对特定平台（Mac, Discord, Telegram）的更顺滑体验。
*   **社区规模**：从数据看，OpenClaw的日更新量是Hermes Agent的5倍，表明其开发者社区规模、用户基础及问题反馈量远超后者，是当前该细分领域的**绝对核心参照项目**。

---

#### **4. 共同关注的技术方向**

*   **会话状态一致性与可靠性**（**OpenClaw & Hermes Agent**）：
    *   **OpenClaw**: Issue #44925 (子代理静默失败), #32296 (回复旧消息)。
    *   **Hermes Agent**: Issue #24187 (SessionDB跳过消息轮次)。
    *   **诉求**：社区普遍要求 **“消息不丢、顺序不乱、错误不静默”**，这是智能体成为可靠生产工具的基础。
*   **数据隐私与安全边界**（**OpenClaw & Hermes Agent**）：
    *   **OpenClaw**: Issue #25592 (工具调用文本泄露), 安全加固版本的发布。
    *   **Hermes Agent**: 多个安全修复PR（SSRF、签名比较、隔离开采）。
    *   **诉求**：用户不再满足于“能用”，而是要求“安全地用”。对敏感信息泄露、越权访问、内部状态暴露等风险零容忍。
*   **平台兼容性与原生集成**（**OpenClaw & Hermes Agent**）：
    *   **OpenClaw**: Issue #77359 (多Discord账号), #41744 (飞书图片丢失), PR #92072 (Gemini图片支持)。
    *   **Hermes Agent**: Issue #24187 (macOS launchd崩溃), Issue #23402 (Docker权限), PR #43949 (Telegram回调配置)。
    *   **诉求**：跨平台体验的**一致性和无痛部署**是硬需求，特别是对使用Docker、MacOS以及国际化平台（飞书、微信、Telegram）的用户。

---

#### **5. 差异化定位分析**

| 维度 | **OpenClaw** | **Hermes Agent** |
| :--- | :--- | :--- |
| **功能侧重** | **广度与深度并重**：强调全栈能力，从底层安全到上层业务编排，追求“无所不能”。 | **深度与精良**：聚焦核心平台体验的打磨，如对话交互、平台集成（Mac, Telegram, 微信）的稳定性。 |
| **目标用户** | **高级开发者/技术专家**：能容忍复杂性，追求极致控制和深度定制的“电力用户”。 | **中高级开发者/爱好者**：寻求开箱即用与高度自定义的平衡，更关注特定平台的体验和部署便捷性。 |
| **技术架构** | **微服务/高度模块化**：沙箱、网关、转录、ACP等组件分工明确，但接口复杂，导致集成异常频发。 | **单体/核心优化**：代码库更集中，问题易于定位，但架构扩展性可能不如OpenClaw。 |
| **社区贡献模式** | **蜂群式贡献**：大量外部PR涌入，一方面推动快速迭代，另一方面造成审查积压和质量波动。 | **精英式贡献**：以维护者团队为主导，外部贡献需更高质量，合并门槛较高，迭代节奏可控但可能较慢。 |

---

#### **6. 社区热度与成熟度**

*   **第一梯队（快速迭代、高度活跃）**：
    *   **OpenClaw**：正处于 **“功能爆发与问题井喷并存”** 的高速成长期。社区贡献如火山爆发，但维护者成为瓶颈。项目功能强大但不稳定，适合敢为人先、喜欢折腾的技术先驱。
    *   **特征**：日更新500+，PR积压严重，版本发布频繁，P0/P1 Bug频现。

*   **第二梯队（质量巩固、平台深化）**：
    *   **Hermes Agent**：已度过功能狂飙期，进入 **“平台兼容性与核心稳定性加固”** 阶段。社区讨论更聚焦于特定痛点（Mac崩溃、会话丢失， 无障碍），而非颠覆性新功能。
    *   **特征**：日更新100，合并率低但针对性很强，Bug类型更偏向于平台特有问题，表现出对特定用户群的深度关怀（如无障碍改进）。

---

#### **7. 值得关注的趋势信号**

1.  **“安全即功能”已成为基线**：从OpenClaw的专门加固版本到Hermes Agent的多项安全修复PR，说明 **安全性不再是“加分项”，而是用户选择项目的“底线”**。开发者应建立“安全左移”的发布流程。
2.  **“静默失败”是用户最大的信任杀手**：两个项目的核心Bug都指向同一个关键词。AI智能体作为“智能代理”，其行为的不透明度直接摧毁用户信任。**所有失败必须有明确的故障信号和自动恢复机制**，这是提升产品口碑的捷径。
3.  **“细粒度控制”与“低级配置”不可兼得**：OpenClaw试图提供极致的细颗粒度控制（如路径权限、子代理权限），但其复杂度导致配置项被“忽略”或“失效”（如bootstrap文件被忽略）。这警示我们，**核心配置的“确定性”和“可观察性”比灵活性更重要**。开发者需在强大与简单之间找到平衡点。
4.  **“跨平台无缝体验”是高价值未来战场**：用户对在Mac、Docker、Windows以及飞书、Telegram、Discord之间无缝切换、会话同步的呼声日益高涨（Hermes Agent的桌面端与Gateway不互通、OpenClaw的多账号问题）。**提供统一的、上下文无关的用户体验，是下一阶段竞争的制胜点**。
5.  **国际化与无障碍化是隐藏的蓝海**：Hermes Agent中对葡萄牙语支持 (Issue #40239) 和针对全盲用户的无障碍改进 (Issue #26689) 的提出，表明该领域的用户群体正在向非英语母语者及有特殊需求的人群扩展。这为AI助手开发者提供了差异化竞争的新思路。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 GitHub 数据，我已为您生成了 2026-06-11 的 Hermes Agent 项目动态日报。

---

### Hermes Agent 项目动态日报 — 2026-06-11

---

#### **1. 今日速览**

今日项目社区提交与讨论异常活跃，**共计 100 条 Issue 和 PR 更新**，显示出极高社区参与度。但值得注意的是，**合并/关闭率（仅 3/50）较低**，表明维护团队可能面临较大的审查与合并压力，或正集中精力处理关键功能重构。**新增了多个 P1 (严重) 级别的 Bug**，涉及 Cron 任务、桌面应用崩溃和会话状态损坏，需重点关注。安全方面，社区提出了多项关于 SSRF、加密时间比较和隔离开采的修复 PR，项目安全态势正在积极改善。

---

#### **2. 版本发布**

今日无新版本发布。

---

#### **3. 项目进展**

今日合并/关闭的 3 个 PR 表明项目在文档和特定功能修复上有所推进：

- **文档完善**：PR [#43602](https://github.com/NousResearch/hermes-agent/pull/43602) 已合并，澄清了 Baoyu 图像生成工作流的边界，避免用户期望混淆。这虽不是核心代码变更，但对提升用户体验至关重要。
- **内存模块修复**：PR [#43948](https://github.com/NousResearch/hermes-agent/pull/43948) 已合并，修复了 `MemoryProvider.on_turn_start` 方法未正确传递实时模型名称的问题，确保了内存系统能根据当前模型做出正确决策。
- **功能澄清**：Issue [#43601](https://github.com/NousResearch/hermes-agent/Issue/43601) 作为功能请求被关闭，项目已明确 Baoyu 技能不应替代手动 SVG/HTML 渲染，避免了社区的重复讨论。

**关键推进中的 PR**: 尽管大部分 PR 仍待合并，但其中一些高阶 PR 显示出项目正迈向更宏大和安全的架构。例如，[PR #43039](https://github.com/NousResearch/hermes-agent/pull/43039) 的“Action Runtime”重构旨在统一和执行路径，标志着对核心稳定性的深度投入。同时，多项安全修复 PR（如 #43937, #43940, #43942）的提出，表明社区正积极响应近期安全审计中的发现。

---

#### **4. 社区热点**

今日讨论最热烈的 Issue 反映了用户对**核心功能可用性**和**无障碍体验**的深度关切：

- **Issue [#23402](https://github.com/NousResearch/hermes-agent/Issue/23402): Docker 权限问题 (15条评论, 3个👍)**
  - **分析**: 该问题虽创建较早，但今日仍活跃。用户 `mmartial` 在使用 Docker 部署时，因 `HERMES_UID` 环境变量导致 Dashboard 的 Chat 功能出现权限错误，影响了 Unraid 等 NAS 平台的集成体验。这表明 **Docker 部署的灵活性和稳定性**是社区用户的持续痛点。

- **Issue [#26689](https://github.com/NousResearch/hermes-agent/Issue/26689): 无障碍改进 (9条评论)**
  - **分析**: 此 Issue 由一名全盲的 macOS 用户提出，详细描述了当前 TUI 界面在 “VoiceOver” 屏幕阅读器下的糟糕体验。这表明 **Hermes Agent 的用户群体正在扩展，对无障碍环境的呼声日益增高**，尤其是在开发者社区中。尽管优先级为 P3，但其社会价值和用户呼声不容忽视。

---

#### **5. Bug 与稳定性**

今日报告了多个高优先级 Bug，对项目稳定性构成直接挑战：

- **[P1] Issue [#43899](https://github.com/NousResearch/hermes-agent/Issue/43899): Cron 任务因缺少模型参数而失败**
  - **描述**: Cron 任务在未显式设置 `model` 字段时，即使 `config.yaml` 中已有默认模型配置，仍会返回 HTTP 400 错误。
  - **状态**: 已有对应修复 PR [#43952](https://github.com/NousResearch/hermes-agent/pull/43952) 提交，旨在早期拦截并给出明确错误提示，预计将很快得到解决。

- **[P1] Issue [#24187](https://github.com/NousResearch/hermes-agent/Issue/24187): SessionDB 消息跳过当前轮次**
  - **描述**: 当模型修复 (`_repair_message_sequence`) 缩短对话历史后，会话数据库会错误地跳过当前轮次的消息，导致对话状态丢失。
  - **状态**: 此 Bug 追踪已久，今日仍有新评论，说明问题复杂且尚未彻底解决。

- **[P1] Issue [#43842](https://github.com/NousResearch/hermes-agent/Issue/43842): macOS 上 Gateway 自更新会导致 Launchctl 服务卸载**
  - **描述**: 从 Gateway 内部触发更新会导致其自身的 `launchctl plist` 被 `bootout`，从而“杀死”自己且无法重启。
  - **状态**: 新报告，暂无修复 PR。这对 macOS 用户的自动化运维体验影响严重。

- **[P2] Issue [#43946](https://github.com/NousResearch/hermes-agent/Issue/43946): 非 Claude 基岩模型调用失败**
  - **描述**: 所有非 Claude 的 AWS Bedrock 模型（如 Kimi， DeepSeek， Amazon Nova）在通过 Hermes 调用时会因负载格式错误而全部失败。
  - **状态**: 今日新报告，暂无修复 PR，会严重影响依赖 Bedrock 多种模型的用户。

- **[P2] Issue [#43475](https://github.com/NousResearch/hermes-agent/Issue/43475): `/restart` 命令破坏 macOS launchd 管理的 Gateway**
  - **描述**: 与 #43842 类似，`/restart` 命令会导致 launchd 管理的 Gateway 进程退出并无法被自动重启。
  - **状态**: 昨日报告，暂无修复 PR。

- **[Bug] Issue [#43953](https://github.com/NousResearch/hermes-agent/Issue/43953): 桌面版多Profile会话崩溃**
  - **描述**: 用户报告在桌面应用中同时运行多个 Profile 会话会导致应用崩溃并回退到设置模式。这是一个严重的新发布功能问题。
  - **状态**: 今日新报告，暂无修复 PR。

---

#### **6. 功能请求与路线图信号**

今日提出的功能请求揭示了用户对 **跨平台一致性**、**国际化** 和 **更丰富的平台集成** 的渴求：

- **可能被纳入下一版本**：
  - **[Feature] Issue [#40239](https://github.com/NousResearch/hermes-agent/Issue/40239)**: 请求为桌面应用添加葡萄牙语 (pt-BR) 支持。鉴于项目后端已有相关 i18n 文件 (如 `locales/pt.yaml`)，此功能纳入下一个桌面版本的可能性较高。
  - **[Feature] PR [#43949](https://github.com/NousResearch/hermes-agent/pull/43949)**: 为 Telegram 平台添加可配置的“callback→text”路由，允许用户自定义内联键盘的回调行为。这表明项目正在积极提升 Telegram 平台的用户体验。

- **潜在路线图信号**：
  - **[Feature] Issue [#43008](https://github.com/NousResearch/hermes-agent/Issue/43008)**: 请求在会话因空闲而过期时，为用户和代理提供清晰的“会话重置”通知。这指向了**会话生命周期管理**的优化方向。
  - **[Feature] Issue [#43928](https://github.com/NousResearch/hermes-agent/Issue/43928)**: 请求桌面应用与 Gateway 之间进行跨界面会话同步。这表明用户对 **多设备无缝切换** 有强烈需求，可能是未来版本的重要方向。

---

#### **7. 用户反馈摘要**

从今日 Issues 中可提炼出以下真实用户痛点：

- **Docker 部署复杂性**: 用户 `mmartial` 在尝试将 Docker 模板更新至新指南时遇到 `HERMES_UID` 权限问题，直接导致 Dashboard 功能不可用。这表明部署文档虽已更新，但实际执行中仍有兼容性差异。
- **跨平台体验割裂**: 用户 `madui1seo-bit` 明确指出，运行桌面端和 Telegram Gateway 时，它们是“完全孤立的实例”，各自维护独立的会话数据库。这带来了糟糕的“设备切换”体验，无法实现聊天记录的连续性。
- **安全焦虑**: 多个安全相关的 Issue（如 #43666, #43837）和 PR 被提出，表明社区中有一批高度关注安全性的用户，并且他们在积极地通过代码审计来为项目贡献力量。今日提出的 PR #43937（修复微信签名比较）和 #43938（修复 SSRF）都直接回应了这些关切。
- **macOS 用户的不满**: `ahmadalzaro1` 提出的关于 macOS 下 `/restart` 命令破坏 launchd 管理的 Gateway 的问题，以及 `seiyeolo` 提出的自更新导致服务卸载的问题，都揭示了项目在 **macOS 原生服务集成**方面存在显著的缺陷。

---

#### **8. 待处理积压**

以下是一些值得维护团队关注的重要积压项：

- **[P2] Issue [#17198](https://github.com/NousResearch/hermes-agent/Issue/17198): Gateway 重启致微信Token冲突 (4月29日)**
  - **分析**: 这是一个长期未解决的竞态条件问题，影响了 WeCom/WeChat 平台的使用稳定性。虽评论不多，但作为影响一个关键平台的问题，过期已久。
- **[P1] Issue [#24187](https://github.com/NousResearch/hermes-agent/Issue/24187): SessionDB 消息跳过当前轮次 (5月12日)**
  - **分析**: 此核心Bug累积已久，直接影响对话系统的可靠性。今日仍有新讨论，说明用户持续受此问题困扰，亟需更彻底的修复方案。
- **[P2] PR [#18506](https://github.com/NousResearch/hermes-agent/pull/18506): Matrix 网关功能增强 (5月1日)**
  - **分析**: 这是一个旨在增加 Matrix 平台原生工具和交互控制的重要PR，挂在“草稿”状态一个多月，。如果 Matrix 平台是项目的长期目标，此 PR 应尽快审查和推进。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*