# OpenClaw 生态日报 2026-07-04

> Issues: 332 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-07-04 02:32 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，请查收 2026-07-04 的 OpenClaw 项目动态日报。

---

### OpenClaw 项目日报 2026-07-04

**分析师点评：** 今日项目维持极高度活跃状态，社区讨论热烈，大量 Bug 修复和新功能 PR 正在推进。尽管没有新版本发布，但代码库变化显著，尤其是在会话存储重构、新客户端支持和稳定性修复方面。安全性与代理可靠性是社区关注的核心焦点。

---

#### 1. 今日速览

过去 24 小时内，OpenClaw 项目保持了极高的社区活跃度，共产生 **332 条 Issues 更新** 和 **500 条 PR 更新**。尽管当天没有正式版本发布，但开发活动十分密集，大量 Pull Request 处于“待合并”状态（441 条），表明有一系列重要的功能改进和 bug 修复即将落地。社区讨论的热点集中在**消息泄露、代理可靠性（如 Codex 工作器失控）以及安全增强**等关键问题上，反映出用户群体对生产环境稳定性和安全性的高度关注。

#### 2. 版本发布

无新版本发布。

#### 3. 项目进展

虽然当日无新版本，但从已合并/关闭的 PR 和 Issues 中可看出项目在多个关键领域取得实质进展：

- **会话与存储重构：** PR #98236 **“refactor: flip sessions and transcripts to sqlite storage”** 是一项大规模的代码重构，旨在将核心会话和转录数据迁移至 SQLite 存储。这标志着项目在数据持久化和可扩展性方面迈出了重要一步，可能会对现有工作流产生影响。
- **新平台支持：** PR #99767 **“feat(macos): install and run the local Gateway automatically”** 和 PR #98868 **“feat(ios): refresh onboarding setup flow”** 等 PR 表明项目正在积极优化 macOS 和 iOS 客户端的用户体验，简化新用户的入门流程。
- **核心功能修复：** PR #99643 **“fix(opencode-go): expose DeepSeek V4 max thinking levels”** 修复了因元数据暴露不完整导致的功能问题，体现了对模型生态兼容性的持续投入。
- **自动化治理：** PR #99771 和 #99766 等代码库清理工作（如重构测试辅助函数、路径标准化），表明项目在关注新功能的同时，也在持续提升代码质量和可维护性。

#### 4. 社区热点

今日社区讨论焦点集中在几个影响范围广、关注度高的 Issues 上：

- **🥇 消息泄露（Issue #25592）：** 标题为 **“Text between tool calls leaks to messaging channels”**，共获得 **33 条评论**，是今日讨论最激烈的 Issue。用户报告 AI Agent 在处理任务时产生的中间状态文本被错误地发送至消息通道（如 Slack），造成严重的用户体验问题。这揭示了当前 Agent 执行流程与输出管道之间缺乏有效隔离，社区正在寻求解决方案。
- **🥈 工作器安全与稳定性（Issue #99551）：** 标题为 **“[Tracker]: Codex worker runaway hardening sprint”**，这是一个追踪 Issue，旨在集中处理一个 Codex 工作器失控事故暴露出的系统性安全与稳定性问题。共获得 **14 条评论**，社区正在协调多个子问题以彻底解决此隐患。
- **🥉 图片优化与依赖缺失（Issue #73148）：** 标题为 **“Image tool: opaque ‘Failed to optimize image’ when sharp is not installed”**，获得 **14 条评论**。用户反馈在未安装 `sharp` 库的环境下，图片工具的报错信息过于模糊，无法定位问题。该 Issue 反映出对依赖管理和错误提示可操作性的需求。
- **📌 Slack 功能增强（Issue #12602）：** 标题为 **“Slack Block Kit support for agent messages”**，获得 **13 条评论**。用户希望 Agent 能发送格式丰富的 Slack Block Kit 消息，以替代目前的纯文本，这体现了社区对提升 Agent 输出表现力的强烈愿望。

#### 5. Bug 与稳定性

以下是今日报告的、按严重程度排序的关键 Bug 问题，多个问题已被标记为 P1（关键优先级）：

- **回话状态与崩溃风险（P1）：**
    - **Issue #92043（[链接](openclaw/openclaw Issue #92043)）：** 180秒的压缩超时设定为一个全局的物理时钟，导致真正需要长时间压缩的任务（如长历史记录）每次都会失败。已有 11 条评论讨论。
    - **Issue #98416（[链接](openclaw/openclaw Issue #98416)）：** 发布的 v2026.6.11 版本缺少了重入保护功能，导致回复会话初始化发生冲突。被举报者标记为“严重”，已有 11 条评论，**是发布版本的回归问题**。
    - **Issue #78562（[链接](openclaw/openclaw Issue #78562)）：** 工具循环导致上下文溢出，即使在成功压缩后，下一次循环仍可能立即触发溢出，导致陷入连续自动压缩的死循环。

- **消息丢失与传递问题（P1）：**
    - **Issue #85714（[链接](openclaw/openclaw Issue #85714)）：** 当 Agent 因 LLM 输出格式问题而忘记调用配置好的传递工具时，最终响应将丢失，无任何后备机制。反映了 Agent 指令遵循的可靠性问题。
    - **Issue #86215（[链接](openclaw/openclaw Issue #86215)）：** Codex OAuth 令牌刷新失败可能导致 Agent 被卡死数小时，且缺乏清晰的告警。影响了系统的基本可用性。
    - **Issue #92241（[链接](openclaw/openclaw Issue #92241)）：** 网关在版本更新或回滚后，持有旧的模块导入路径，导致新消息被静默丢弃(ERR_MODULE_NOT_FOUND)。**是一个严重的运维与稳定性问题**。

- **权限与认证问题（P1/P2）：**
    - **Issue #38327（[链接](openclaw/openclaw Issue #38327)）：** 使用 `google-vertex/gemini-3.1-pro-preview` 模型时出现 `TypeError: Cannot convert undefined or null to object`。**这是一个已确认的回归问题**。
    - **Issue #10659（[链接](openclaw/openclaw Issue #10659)）：** 用户请求“屏蔽密钥”系统，以防 Agent 能够直接读取和使用原始 API 密钥，从而避免泄露。这是一个根植于安全设计的根本性需求。

#### 6. 功能请求与路线图信号

社区需求集中在安全、权限和 Agent 能力增强上，以下是可能与下一版本相关的重点请求：

- **安全与权限：**
    - **Issue #10659（[链接](openclaw/openclaw Issue #10659)）：** “Masked Secrets” 系统。考虑到大量 P1 安全 Issue 的关联性，此功能极有可能被纳入近期路线图。
    - **Issue #12678（[链接](openclaw/openclaw Issue #12678)）：** 基于能力的工具/技能权限模型。
    - **Issue #12219（[链接](openclaw/openclaw Issue #12219)）：** `skill.yaml` 权限声明清单标准。此功能与 #12678 结合，是构建安全技能市场的基石。
- **Agent 交互与可靠性：**
    - **Issue #12602（[链接](openclaw/openclaw Issue #12602)）：** Slack Block Kit 支持。常与 “Feature” 标签一起出现，有望在下一迭代中实现。
    - **Issue #14785（[链接](openclaw/openclaw Issue #14785)）：** 减少工具模式（schema）的 Token 开销。这是一个影响所有用户的性能优化请求。
- **数据生命周期管理：**
    - **Issue #13616（[链接](openclaw/openclaw Issue #13616)）：** 备份/恢复实用工具。随着存储向 SQLite 迁移，提供一个标准的备份方案将是顺理成章的需求。
- **多智能体协作：**
    - **Issue #35203（[链接](openclaw/openclaw Issue #35203)）：** 增强多 Agent 协作，包含能力画像、共享黑板和分层记忆。

#### 7. 用户反馈摘要

从今日 Issues 和 PR 评论中，可以提炼出以下用户真实反馈：

- **对 Agent 可控性的高要求：** 用户频繁要求更精细的控制能力，如“在 Agent 无法访问原始密钥的情况下使用 API 密钥”（Issue #10659）、“给不同 Agent 设置不同的插件配置”（Issue #55401）、“限制子 Agent 的访问工具”（Issue #15032）。
- **对“隐形”错误的困扰：** 多个 Bug 报告都描述了错误发生但用户难以察觉或根本不知情的情况，如“消息静默丢失”（Issue #92241）、“Agent 卡死无告警”（Issue #86215）、“压缩超时重复失败无明确提示”（Issue #92043）。这表明用户对系统透明度和可观测性有极高的期望。
- **对新手友好度的关注：** 用户反馈 onboarding 流程未提及重要功能（如 Memory 配置，Issue #16670），以及 UI 过于密集、难以导航（Issue #75947），表明社区在功能强大的同时，也开始重视新用户的入门体验。
- **对性能的敏感：** Issue #80131 详细分析了网关首次响应时间（TTFT）的瓶颈，具体指出认证和工具打包占据了大量时间，显示出高级用户愿意深入分析和提供优化建议。

#### 8. 待处理积压

以下为长期存在、但未得到充分关注或解决方案的 Issue，建议维护者审核：

- **Issue #6615（[链接](openclaw/openclaw Issue #6615)）：** “为执行审批添加拒绝列表（denylist）”。**创建于 2 月 1 日**，获得了 7 个 👍，属于社区呼声很高的安全功能，但长期未被采纳。
- **Issue #12678（[链接](openclaw/openclaw Issue #12678)）：** “基于能力的工具/技能权限模型”。**创建于 2 月 9 日**，同样是一个关于权限系统的重大功能请求。
- **Issue #35203（[链接](openclaw/openclaw Issue #35203)）：** “多 Agent 协作增强 RFC”。**创建于 3 月 5 日**，是一个涉及面很广的架构设计方案，需要维护者团队给出初步反馈或计划。
- **PR #75469（[链接](openclaw/openclaw PR #75469)）：** “修复：相同会话的推断承诺可能因心跳任务而无限期饥饿”。**创建于 5 月 1 日**，至今仍标有“📣 needs proof”（需要证明），是一个等待了 2 个多月有待验证或推进的 PR。

---

## 横向生态对比

好的，作为专注 AI 智能体与个人 AI 助手开源生态的资深技术分析师，以下基于您提供的两份动态摘要，为您生成一份横向对比分析报告。

---

### AI 智能体开源生态横向对比分析报告 (2026-07-04)

#### 1. 生态全景

当下个人 AI 助手开源生态正经历从“功能可用”向“生产可靠”的关键跃迁。社区开发者不再满足于简单的对话或工具调用，而是聚焦于**代理的自主行为安全**、**多平台集成稳定性**及**数据生命周期管理**。这种从“能做什么”到“能否安全、稳定地持续做”的转变，标志着生态进入成熟前夜的阵痛期。同时，针对不同形态（桌面端、消息网关、协作平台）的插件化和平台化趋势，成为两大核心项目共同的技术演进方向。

#### 2. 各项目活跃度对比

| 指标 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **今日 Issues 更新数** | 332 条 | 50 条 |
| **今日 PR 更新数** | 500 条 | 50 条 |
| **今日 Release** | 无新版本 | 无新版本 |
| **待合并 PR 数** | 441 条 | 43 条 |
| **社区关注焦点** | 消息泄露（#25592）、Codex 工作器失控（#99551） | OAuth 认证不统一（#12058）、部署体验（#12188） |
| **健康度评估** | **极高度活跃，但存在安全与回归风险**。社区规模大、反馈密集，但高优先级 Bug（如消息丢失、会话崩溃）和长时间积压的需求（如权限模型）并存。 | **中度活跃，迭代稳健**。社区更聚焦于特定平台（Telegram、桌面端）的体验优化和安全性加固。虽然 Bug 密度不低，但修复与功能并进，整体可控。 |

#### 3. OpenClaw 在生态中的定位

OpenClaw 在此生态中扮演着 **“全能型基础设施先行者”** 的角色，定位类似于 AI 智能体领域的 `Kubernetes`。

- **优势**：社区规模与项目复杂度均远超 Hermes Agent。极强的迭代速度与功能广度，覆盖了从底层存储（SQLite重构）到上层应用（Slack Block Kit）的各个环节。
- **技术路线差异**：更倾向于**重架构、重平台**的路线。例如通过大规模重构会话存储（PR #98236）来夯实可扩展性基础。相比之下，Hermes 则更像**轻量化、插件化的个人助手**。
- **社区规模对比**：从今日的 Issue/PR 数量（332/500 vs 50/50）可直观看出，OpenClaw 的社区开发者数量、用户活跃度和问题反馈量级是 Hermes Agent 的 **6~10 倍**。其面临的挑战也更具系统性和复杂性（如全局死循环、运维静默失败问题）。

#### 4. 共同关注的技术方向

尽管项目定位不同，但双方社区反馈揭示了三项共同的核心技术诉求：

1.  **安全与凭证隔离**：这是最突出的共同痛点。
    - **涉及项目**：OpenClaw、Hermes Agent。
    - **具体诉求**：用户强烈要求强凭证隔离机制。OpenClaw 用户提出“屏蔽密钥”系统（#10659），Hermes Agent 则暴露了终端快照将 `.env` 明文写入磁盘（#48441）以及多 Profile 绕过令牌隔离（#54675）的问题。核心诉求是 **“让 Agent 使用我的 API 密钥，但无法读取它”**。
2.  **网关/平台集成的稳定性与权限细化**。
    - **涉及项目**：OpenClaw、Hermes Agent。
    - **具体诉求**：两者都支持多种平台。OpenClaw 社区要求完善 Slack Block Kit 支持（#12602），Hermes Agent 则面临 Telegram 与 CLI 认证不一致（#12058）及 WhatsApp 群组细粒度权限控制（#7269）问题。这表明**平台网关的体验一致性**和**灵活的权限控制**是用户为 Agent 接入更多商业场景的基础要求。
3.  **可观测性与错误透明化**。
    - **涉及项目**：OpenClaw、Hermes Agent。
    - **具体诉求**：用户对“隐形错误”深恶痛绝。OpenClaw 的“消息被静默丢弃”（#92241）和“压缩超时重复失败”（#92043），以及 Hermes Agent 的“桌面端 WebSocket 被 busy-poll 阻塞”（#57903）、“工具静默忽略”（#57967， #57928），都指向同一个需求：**当 Agent 出错或降级运行时，必须给用户清晰、可操作的反馈，而不是静默失败**。

#### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **功能侧重** | **生产级工作流与协作平台**。强调多Agent协作、复杂任务编排、后台自动化治理。 | **个人效率与轻量级接入**。更侧重个人日常任务管理（成就系统、Kanban）、易用的消息网关（Telegram、Desktop）和快速部署。 |
| **目标用户** | 开发者、DevOps 团队、企业级用户。对系统稳定性和安全合规有极高要求。 | 独立开发者、技术爱好者和个人用户。更看重上手速度和单点功能的实用性。 |
| **技术架构** | **厚重、组件化**。有大型重构（如存储迁移、自动化治理），模块间依赖性强，修改影响面广。 | **轻量、插件式**。以 Profile、Gateway 插件、MCP 集成等模块化方式扩展，灵活性高，耦合度低。 |
| **社区成熟度** | **高阶但混乱**。社区体量庞大，讨论深入，但信息噪音大，高质量 Issue 和长期积压并存。 | **专注且有序**。社区规模小，讨论集中，但项目在特定功能（如成就系统、Telegram集成）上迭代迅速。 |

#### 6. 社区热度与成熟度

- **第一梯队：快速迭代与功能扩张期（OpenClaw）**
  - **特征**：活动量巨大，每天数百条 Issue/PR；大量新功能（新客户端、存储重构）与 Bug 修复并行；安全类和回归类问题频发。
  - **评估**：处于**功能狂欢与质量阵痛并存**阶段。社区动力十足，但维护者面临巨大的治理挑战，长期积压问题（如权限模型，PR #75469）可能损害用户信任。

- **第二梯队：质量巩固与体验优化期（Hermes Agent）**
  - **特征**：活动量稳定，修复与功能并重；关注点从“能不能用”转向“容不容易用”（Docker 部署、配置暴露、UI 偏好）；开始出现系统性的安全修复（如防止 `.env` 泄漏）。
  - **评估**：已度过野蛮生长，正进入**精细化打磨**阶段。项目状态更为健康，社区期待的是稳定、优雅的体验而非颠覆性功能。

#### 7. 值得关注的趋势信号

1.  **安全左移成为刚需**：“屏蔽密钥”、“能力权限模型”、“Denylist”等议题在两个社区同时涌现，表明开发者已从被动防御转向主动设计。**对于 AI 智能体开发者而言，将安全策略（如凭证隔离、操作审计、权限预检）内置到 Agent 核心架构中，将是项目能否走向大规模部署的关键分水岭。**

2.  **从“单智能体”走向“多智能体协作”面临架构挑战**。OpenClaw 的“多Agent协作RFC”（#35203）虽然是少数，但结合其社区对“子Agent工具限制”的需求（#15032），表明多智能体协作架构已经进入实践探索阶段。开发者需要关注**共享状态管理（黑板模式）**、**通信协议标准化**和**协作安全边界**的设计。

3.  **可观测性需求从“工具”上升为“功能”**。用户不再满足于看日志，而是要求 Agent 自身能报告其状态和错误。Hermes Agent 的成就系统导出（PR #58012）和 OpenClaw 对“隐形错误”的批判，共同指向一个趋势：**未来的 AI 智能体应具备自我报告和健康度自检能力**，这是构建用户信任的基石。

4.  **部署体验的“最后一公里”成为新焦点**。两个项目均有大量关于 Docker 配置、环境变量、UI 导航的反馈。随着技术成熟，**如何让非专家用户也能轻松部署和管理自己的智能体**，将成为项目获得更广泛社区采用的关键瓶颈。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-07-04

## 1. 今日速览

过去 24 小时内，项目保持高度活跃：共产生 50 条 Issue 更新（47 条新开/活跃，3 条关闭）和 50 条 PR 更新（43 条待合并，7 条已合并/关闭），社区讨论热烈，安全与平台集成类问题仍是关注焦点。尽管没有新版本发布，但多个高优先级 Bug 已收到修复 PR，项目整体健康度良好，但长时间未响应的积压 Issue 仍需维护者关注。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 共 7 条，其中较重要的有以下三条：

- **PR #58012** `feat(achievements): add export endpoint and agent summary (#18472)` — 已合并。实现了成就系统的导出接口和智能体概要功能，使原本仅存在于 `state.json` 和 Dashboard 的成就数据可被外部工具或智能体自身读取，增强了数据可移植性。
  [https://github.com/NousResearch/hermes-agent/pull/58012](https://github.com/NousResearch/hermes-agent/pull/58012)

- **PR #57999** `feat(telegram): add external callback handlers` — 已合并。为 Telegram 网关添加外部回调处理器支持，允许通过 `prefix-based callback_data` 将按钮回调分发给本地脚本，并保持了原有的回调鉴权逻辑。
  [https://github.com/NousResearch/hermes-agent/pull/57999](https://github.com/NousResearch/hermes-agent/pull/57999)

- **PR #56074** `fix: reset in-memory _openrouter_catalog_cache on /model --refresh` — 已合并。修复了 `/model --refresh` 命令仅清除磁盘缓存而未重置内存缓存的问题，避免用户看到过时的 OpenRouter 模型列表。
  [https://github.com/NousResearch/hermes-agent/pull/56074](https://github.com/NousResearch/hermes-agent/pull/56074)

此外，项目在 MCP、OAuth、Windows 平台兼容性、技能管理等方面均有多个提交处于待合并状态，显示核心维护者正在持续推动功能与稳定性改进。

## 4. 社区热点

今日讨论最活跃的 Issues 集中在以下几个方向：

### 🔥 平台网关 & 认证问题
- **Issue #7269** — [Question] Whatsapp groups and require_mention: true, only reply to allowed users (5 评论)。用户询问在 WhatsApp 群组中 `require_mention` 与 `WHATSAPP_ALLOWED_USERS` 的交互设计，期望能回复群组成员而无需全局放行。
  [https://github.com/NousResearch/hermes-agent/issues/7269](https://github.com/NousResearch/hermes-agent/issues/7269)

- **Issue #12058** — [Bug]: OpenAI Codex OAuth works in CLI, but Telegram gateway replies “No Codex credentials stored” (5 评论)。报告了 CLI 与 Telegram 网关的认证不一致问题，属于网关特定认证漏洞。
  [https://github.com/NousResearch/hermes-agent/issues/12058](https://github.com/NousResearch/hermes-agent/issues/12058)

- **Issue #48534** — Anthropic Max OAuth fails: token exchange 404s because Anthropic now blocks the claude-cli/ User-Agent (3 评论)。因 Anthropic 服务端拦截了默认 User-Agent，导致 OAuth 流程中断。
  [https://github.com/NousResearch/hermes-agent/issues/48534](https://github.com/NousResearch/hermes-agent/issues/48534)

### 🔥 配置文件与部署体验
- **Issue #12188** — [Feature]: Setting `hermes model` config/settings inside Docker compose as env variables (5 评论, 👍2)。用户反馈 Docker 部署文档缺失，无法通过环境变量配置模型，需进入容器执行命令，请求更好的环境变量支持。
  [https://github.com/NousResearch/hermes-agent/issues/12188](https://github.com/NousResearch/hermes-agent/issues/12188)

### 🔥 安全漏洞
- **Issue #48441** — [Security] Terminal session snapshots leak .env secrets to disk in plaintext (5 评论, 👍1)。严重安全漏洞：终端快照机制将环境变量（包括密钥）明文写入磁盘。已被关闭（已修复或标记），但社区高度关注。
  [https://github.com/NousResearch/hermes-agent/issues/48441](https://github.com/NousResearch/hermes-agent/issues/48441)

**诉求分析**：社区强烈期望更灵活的网关权限控制（WhatsApp 群组、多 Profile 路由）、更完善的部署文档与配置暴露方式、以及更严格的凭证隔离与安全存储。

## 5. Bug 与稳定性

按严重程度排列今日报告的 Bug，并标注已有修复 PR 的情况：

| 严重级别 | Issue # | 摘要 | 修复 PR 状态 |
|----------|---------|------|-------------|
| **P1** | #12058 | Codex OAuth 在 Telegram 网关失效 | 暂无对应 PR |
| **P1** | #48534 | Anthropic OAuth 因 User-Agent 被拦截而 404 | 暂无对应 PR |
| **P1** | #58010 | AsyncSessionDB 缺少 await 导致 /resume 崩溃 | 暂无对应 PR（刚创建） |
| **P2** | #54675 | 多 Profile 模式下 bot token 绕过隔离 | 已有 PR #57563 处理 |
| **P2** | #57928 | Telegram 文件附件在斜杠命令下被静默丢弃 | 暂无对应 PR |
| **P2** | #57903 | 桌面端 WebSocket 被 LLM 调用的 busy-poll 阻塞 | 已有草案 PR #57933 |
| **P2** | #56747 | Windows 桌面端终端控制台窗口闪烁 | 暂无对应 PR |
| **P2** | #57905 | `computer_use` 在 Windows 上无法发现窗口 | 暂无对应 PR |
| **P3** | #57967 | `hermes kanban create` 静默丢失任务（SQLite 提交竞争） | 暂无对应 PR |
| **P3** | #57986 | `/journey` 因技能 Frontmatter 非 dict 崩溃 | 暂无对应 PR |
| **P3** | #57955 | terminal 工具绕过 SOUL.md 写保护 | 暂无对应 PR |
| **P3** | #57949 | Langfuse 插件占位 API key 静默失败 | 暂无对应 PR |

**特别关注**：多个安全边界类 Bug (#54675, #57955, #58006) 表明凭证隔离和路径校验仍需加强。P2 级 `AsyncSessionDB` 缺失 await 属于基础代码错误，建议优先修复。

## 6. 功能请求与路线图信号

今日用户提出的新功能需求中，以下几个有较高采纳可能性，部分已有对应 PR 准备中：

- **Issue #40173** — `feat(telegram): channel_profiles` 允许单个 bot 路由不同会话到不同 Profile（👍3，社区高度期待）。已有相关讨论，可能纳入下一版本。
  [https://github.com/NousResearch/hermes-agent/issues/40173](https://github.com/NousResearch/hermes-agent/issues/40173)

- **PR #57734** — `feat(gateway): add Linear Agent platform plugin` 将 Linear 作为一级 Hermes 平台，支持 Agent 在 Linear 上被 @提及并响应。此 PR 处于开放状态，若合入将极大扩展团队协作场景。
  [https://github.com/NousResearch/hermes-agent/pull/57734](https://github.com/NousResearch/hermes-agent/pull/57734)

- **Issue #50668** — Telegram cron 投递自动创建新 DM Topic。对使用 Topic 模式的用户非常实用，属于小粒度增强。
  [https://github.com/NousResearch/hermes-agent/issues/50668](https://github.com/NousResearch/hermes-agent/issues/50668)

- **Issue #46337** — 桌面端 UI 配置自定义本地 STT/TTS 和媒体生成提供商。随着桌面客户端推广，该需求增长迅速。
  [https://github.com/NousResearch/hermes-agent/issues/46337](https://github.com/NousResearch/hermes-agent/issues/46337)

- **PR #58015** — `feat(achievements): add export endpoint and agent summary` 已合并，预示成就系统将成为 Agent 可感知的能力，未来可能衍生更多智能体自我审计功能。

**路线图信号**：从今日 PR 和 Issue 趋势看，项目正朝多 Profile 路由、平台插件化（Linear、Feishu 等）、桌面端增强、以及安全审计/合规可视化方向发展。

## 7. 用户反馈摘要

从 Issues 评论中提炼的典型用户痛点与期望：

- **部署体验**：“Docker 文档相当缺乏……不确定 OpenAI 是指仅 ChatGPT 还是也兼容 vLLM。”（#12188）——用户希望有更清晰的模型配置说明和环境变量支持。
- **WhatsApp 权限**：“我不希望将所有人加入白名单，但希望对群组成员自动回复。”（#7269）——群聊场景下的细粒度权限控制是高频需求。
- **安全暴露**：“终端快照将 .env 中的密码全部明文写入磁盘文件，任何进程都能读取。”（#48441）——用户对敏感信息泄漏极其敏感，虽然已修复但心理阴影仍在。
- **稳定性**：“Cron 触发的会话永远得不到 Composio MCP 工具，但交互式会话却正常。”（#57861）——定时任务与交互任务的行为不一致让用户困惑。
- **桌面端**：“更新后侧边栏的‘Recent Sessions’列表消失了，只剩 Pinned 和 Projects。”（#57968）——用户对 UI 变更缺乏预期感到不满。
- **功能缺失**：“在桌面端设置中无法配置自定义 STT/TTS 提供商。”（#46337）——高级用户希望超越内置限制。

**整体满意度**：社区对新功能（如成就导出、Linear 集成）反响积极，但对安全漏洞、认证不一致、文档不足等问题仍有较多批评。

## 8. 待处理积压

以下长期未响应的 Issue 或 PR 需要维护者重点关注：

- 🟡 **Issue #624** — “Feature: Automatic Session Title Generation” (2026-03-07 创建，4 评论)。已搁置近 4 个月，社区期待该轻量级 LLM 生成的标题功能，可显著改善多会话管理体验。
  [https://github.com/NousResearch/hermes-agent/issues/624](https://github.com/NousResearch/hermes-agent/issues/624)

- 🟡 **Issue #6347** — “Anthropic OAuth refresh path gets Cloudflare 403 and leaves Hermes PKCE creds unrefreshable” (2026-04-09 创建，2 评论)。与 #48534 类似但更底层，仍无修复方案。
  [https://github.com/NousResearch/hermes-agent/issues/6347](https://github.com/NousResearch/hermes-agent/issues/6347)

- 🟡 **Issue #17790** — “Make Discord voice inactivity timeout configurable” (2026-04-30 创建，4 评论)。简单的配置暴露需求，至今未合并。
  [https://github.com/NousResearch/hermes-agent/issues/17790](https://github.com/NousResearch/hermes-agent/issues/17790)

- 🟡 **PR #54588** — “feat: Add configurable attribution string for agent identity” (2026-06-29 创建，待合并)。为 Agent 添加可配置的身份归属，有助于企业用户合规审计，但尚未获审核。
  [https://github.com/NousResearch/hermes-agent/pull/54588](https://github.com/NousResearch/hermes-agent/pull/54588)

- 🔴 **Issue #25106** — “[Bug]: CLI --global model switch does not persist/clear model.base_url and model.api_mode” (2026-05-13 创建，3 评论)。影响用户切换模型的实际体验，虽为 P2 但已开放近 2 个月。
  [https://github.com/NousResearch/hermes-agent/issues/25106](https://github.com/NousResearch/hermes-agent/issues/25106)

建议维护者在处理新 Issue 的同时，对上述积压项逐一评估关闭或排期，以避免社区信任度下降。

---

*本日报基于 Hermes Agent GitHub 仓库 2026-07-04 公开数据生成，数据截止时间 UTC 23:59。*

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*