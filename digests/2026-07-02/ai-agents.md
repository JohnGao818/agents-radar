# OpenClaw 生态日报 2026-07-02

> Issues: 251 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-07-02 02:52 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据 OpenClaw 项目 2026-07-01 数据生成的 2026-07-02 项目动态日报。

---

### OpenClaw 项目动态日报 | 2026-07-02

---

### 1. 今日速览

OpenClaw 项目今日保持极高活跃度，但面临显著的稳定性挑战。过去 24 小时内，社区提交了 500 个 Pull Request，其中大量为修复近期回归问题的补丁，同时有 251 个 Issue 被更新，讨论热度不减。尽管无新版本发布，但项目核心团队正在全力应对 `v2026.6.11` 版本中暴露的多个 P1 级回归问题，如“会话中断”和“工具输出为空”。社区对内存安全、会话状态持久化的讨论持续升温，反映出用户对生产环境稳定性的高期待。整体而言，项目正处于高强度的“修复-验证”冲刺阶段，社区积极性极高，但质量控制是当前首要任务。

### 2. 版本发布

- **无** （过去 24 小时无新版本发布）

### 3. 项目进展

过去 24 小时，社区提交了大量修复性 PR，项目在解决多个关键缺陷和提升系统健壮性方面取得实质性进展。主要进展包括：

- **关键修复与安全加固：**
    - **修复了多个潜在的内存溢出风险：** 多个 PR 针对不同插件（Google Meet, Feishu, Codex 等）中未限制 JSON 响应读取大小的问题进行了修复，通过引入字节上限（如 16 MiB）来防止恶意或超大响应导致进程 OOM。[PR #98355](https://github.com/openclaw/openclaw/pull/98355), [PR #98341](https://github.com/openclaw/openclaw/pull/98341), [PR #98047](https://github.com/openclaw/openclaw/pull/98047)
    - **提升了 CLI 工具的健壮性：** 修复了 CLI 中 `config-set-input` 和 `exec-approvals-cli` 两个命令在处理超大型文件时可能导致内存耗尽的问题，增加了读取大小限制。[PR #98664](https://github.com/openclaw/openclaw/pull/98664), [PR #98676](https://github.com/openclaw/openclaw/pull/98676)
    - **修复了 OpenAI Responses API 在特定超时场景下的处理错误：** 解决了 `fix(openai-transport): 120-second timeout` 问题，该问题导致 API 成功完成但流式传输仍在循环，造成用户体验延迟。[Issue #98244](https://github.com/openclaw/openclaw/issues/98244)

- **核心功能与稳定性推进：**
    - **iMessage 代理交互优化：** 一个包含三个缺陷修复的 PR 正在审查中，旨在解决 iMessage 代理在处理投票时回复不当、重复发言及评论误判的体验问题。[PR #98781](https://github.com/openclaw/openclaw/pull/98781)
    - **Google Meet 插件修复：** 修复了 Fal 集成中 `grok-imagine` 和 `nano-banana-2-lite` 等模型参考图像调用路由错误的问题。[PR #98688](https://github.com/openclaw/openclaw/pull/98688)
    - **LLM 工具结果重放修复：** 一个旨在修复共享状态重放边界（由 #97742 引入）的 PR 已提交，以保留非数组格式的工具结果文本，提升模型回复的准确性。[PR #98826](https://github.com/openclaw/openclaw/pull/98826)

- **新功能/特性开发：**
    - **Signal 目标别名功能：** 一个新特性 PR 为 Signal 通道添加了目标别名功能，允许用户为复杂的手机号或群组 ID 配置易记的友好名称，简化目标寻址。[PR #95738](https://github.com/openclaw/openclaw/pull/95738)
    - **管理性事件储存库：** 一个大型 PR 引入了“持久化例程注册表”功能，旨在为 Cron 任务、心跳等重复性操作提供官方的创建、监控和暂停接口。[PR #98727](https://github.com/openclaw/openclaw/pull/98727)

### 4. 社区热点

今日社区讨论聚焦于 `v2026.6.11` 版本带来的系列严重回归问题，以及围绕内存管理和会话安全性的长期功能讨论。

- **最热 Issue: [Bug] v2026.6.11 published dist missing reentrancy guard** (#98416)
    - **链接：** [Issue #98416](https://github.com/openclaw/openclaw/issues/98416)
    - **“点赞”：** 5 👍
    - **分析：** 该问题直指发布流程中的严重失误——`v2026.6.11` 发布的构建产物缺失了关键的 `reentrancy guard`（重入保护），导致自动回复功能无法正常初始化。5个“点赞”表明大量用户受到影响，引发了社区对版本发布质量的强烈关注。

- **最具影响力的功能讨论：Feature Request: Memory Trust Tagging by Source** (#7707)
    - **链接：** [Issue #7707](https://github.com/openclaw/openclaw/issues/7707)
    - **分析：** 尽管该 Issue 已存在数月，但13条评论表明社区对其持续高度关注。其核心诉求是建立基于来源的“内存信任标记”，以防御来自不可信内容（如网页、第三方集成）的记忆投毒攻击。这反映了高级用户对 Agent 安全性和数据治理的深度需求。

- **其他高活跃度 Issue：**
    - **[Bug] “Cannot convert undefined or null to object” with google-vertex/gemini...** (#38327): 一个已持续数月的 P1 回归问题，在 `v2026.3.2` 版本后出现，导致嵌入代理完全失效。10条评论，3个点赞，是影响面最广的长期 Bug 之一。[链接](https://github.com/openclaw/openclaw/issues/38327)
    - **[Bug] Sessions breaking constantly** (#98672): 用户在毫无预警的情况下从稳定状态转为频繁会话中断，总结了大量 `v2026.6.11` 版本升级后的用户挫败感。[链接](https://github.com/openclaw/openclaw/issues/98672)

### 5. Bug 与稳定性

过去 24 小时是 Bug 报告的高峰期，特别是 `v2026.6.11` 版本相关的回归问题占据了主导地位，项目稳定性面临严峻考验。

| 严重程度 | Issue/PR 链接 | 摘要 | 修复状态 |
| :--- | :--- | :--- | :--- |
| **P1 回归** | [Issue #98416](https://github.com/openclaw/openclaw/issues/98416) | `v2026.6.11` 发布产物缺失重入保护，导致自动回复初始化冲突。 | **无直接 Fix PR** |
| **P1 回归** | [Issue #98528](https://github.com/openclaw/openclaw/issues/98528) | `v2026.6.11` 回归：工具输出（exec, web_fetch等）在每次对话的第一次调用后返回空结果。 | **无直接 Fix PR** |
| **P1 回归** | [Issue #98672](https://github.com/openclaw/openclaw/issues/98672) | `v2026.6.11` 升级后，会话频繁中断，模型回复中断。 | **无直接 Fix PR** |
| **P1** | [Issue #97983](https://github.com/openclaw/openclaw/issues/97983) | iOS/WebChat 消息成功后无法可靠触发助手回复。 | **无直接 Fix PR** |
| **P1** | [Issue #98740](https://github.com/openclaw/openclaw/issues/98740) | `Mattermost` 插件在 `v2026.6.11` 外部化后，原生斜杠指令返回 `401`。 | **有 Fix PR #98819** |
| **P2** | [Issue #90414](https://github.com/openclaw/openclaw/issues/90414) | 内存搜索功能持久性返回“索引元数据丢失”错误。 | **无直接 Fix PR** |
| **P2** | [Issue #98601](https://github.com/openclaw/openclaw/issues/98601) | Docker E2E 测试因 Docker 拒绝默认资源限制而失败。 | **无直接 Fix PR** |

**总结：** 稳定性是当前最突出的问题。`v2026.6.11` 版本引入了至少三个 P1 级别的回归问题，直接导致核心功能（代理回复、工具执行）失效。项目需优先对这些回归问题进行根源分析、修复并发布补丁。此外，多个长期存在的 P1 问题（如 #38327, #92201）仍未解决，构成了项目的技术债务。

### 6. 功能请求与路线图信号

从社区 Issue 和 PR 中，可以识别出以下潜在的下一个版本方向：

- **安全与信任：** 除了长期讨论的 `Memory Trust Tagging by Source (#7707)`，社区还提出了 `Audit log for agent memory changes (#20935)` 的要求，显示用户对 Agent 的透明度和数据完整性提出了更高要求。`Skill-creator bypasses skill_workshop proposal workflow (#96054)` 的 Issue 也表明安全策略的执行同样被社区关注。
- **会话状态管理：** 多个功能请求集中在会话的持久化和上下文切换上。`Pre-reset agentic memory flush (#45608)` 和 `Automated Session Memory Preservation (#40418)` 旨在解决 `/new` 重置后上下文丢失的痛点。`Topic-session families (#90916)` 则提出了更高级的“上下文多通道”概念，这可能是未来实现更复杂多任务 Agent 的基础。
- **性能与成本控制：** `Add rate limiting and throttling (#13615)` 的提议反映了社区对成本控制和 API 资源保护的重视，这与 `per-request auth and tool bundling dominate gateway TTFT (#80131)` 的性能分析是同一个方向上的诉求。
- **自动化与运维：** 新建的 `Durable routines registry (PR #98727)` 功能如果被接纳，将显著提升 OpenClaw 作为自动化平台的运维能力，使其从单次任务执行器迈向可管理的任务调度系统。

### 7. 用户反馈摘要

从社区反馈中可以提炼出以下关键用户声音：

- **主流使用场景：**
    - **自动化工作流：** 许多用户利用 OpenClaw 构建复杂的自动化工作流，例如“跨9家邮件供应商的浏览器自动化”([Issue #44431](https://github.com/openclaw/openclaw/issues/44431))，表明其在 RPA 领域有广泛应用。
    - **多平台集成：** 用户活跃部署在 Discord、Telegram、Slack、Feishu、WhatsApp 等多个平台，对平台间一致性和稳定性有极高要求。

- **主要痛点与不满意：**
    - **版本升级风险导致信任危机：** `v2026.6.11` 版本暴露的严重回归问题（如 #98416, #98528）严重打击了用户对“无痛升级”的信任。用户 @AaronFaby 在 Issue #98672 中描述的“早上起来突然坏了”的现象极具代表性，凸显了版本质量控制的紧迫性。
    - **稳定性不足：** 除了回归问题，长期存在的会话中断、消息丢失、代理回复失败等 P1 问题（如 #92201, #38327）令用户日常工作受阻，反馈日益增加。
    - **特定平台集成问题：** 微信（#

---

## 横向生态对比

# AI 智能体与个人助手开源生态横向对比分析报告

**报告日期：2026-07-02**  
**数据来源：OpenClaw、Hermes Agent 项目社区动态**

---

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正呈现出 **“双速演进”** 态势：一方面，头部项目保持极高迭代频率，单日数百 PR 的贡献量表明社区参与度已进入工业化阶段；另一方面，版本质量与稳定性成为普遍瓶颈——OpenClaw 在 `v2026.6.11` 中爆发多个 P1 级回归，Hermes Agent 虽发布 v0.18.0 大版本但亦残留 iMessage sidecar 死循环等长期问题。社区需求正从“功能堆叠”转向“安全可信与自动化闭环”，**内存信任标记（Memory Trust Tagging）、真实自主性（True Autonomy）、持久化状态管理**成为跨项目共识方向。整体来看，生态正从“能做什么”向“能否稳定可靠地做”过渡，质量控制与安全基础设施建设显得尤为迫切。

---

## 2. 各项目活跃度对比

| 指标 | **OpenClaw** | **Hermes Agent** |
|------|-------------|------------------|
| 过去24h Pull Request 数 | **500**（大量修复性PR） | **50**（含合并/关闭） |
| 过去24h Issue 更新数 | **251** | **50** |
| 版本发布 | **无**（v2026.6.11存在严重回归） | **v0.18.0 (v2026.7.1)** — 大版本“Judgment” |
| 累计贡献者 | 未明确（社区规模庞大） | **370+** 社区贡献者（自v0.17.0以来） |
| 代码变更量 | 未单独统计（日均数十万行？） | ~25万行插入、4.1万行删除（自v0.17.0） |
| 健康度评估 | ⚠️ **高风险**：版本回归导致核心功能失效，需紧急修复冲刺 | 🟢 **中高风险**：虽有P0安全漏洞已修复，但多个P2长期Bug待解 |

**解读**：OpenClaw 的绝对活跃度（500 PRs / 251 Issues）远超 Hermes Agent，但健康度更差——大量 PR 是修复自身回归问题，而 Hermes Agent 在发布新版本的同时保持了更稳定的节奏。

---

## 3. OpenClaw 在生态中的定位

### 与 Hermes Agent 相比

| 维度 | **OpenClaw** | **Hermes Agent** |
|------|-------------|------------------|
| **核心路线** | 通用 Agent 框架，强调多平台集成（Google Meet、Feishu、iMessage 等）与插件生态 | 聚焦自主决策（Judgment）与“真实自主性”（True Autonomy），MoA 延迟优化、Cron 背景任务注入 |
| **优势** | 平台覆盖广度极高（Discord/Telegram/微信等），社区 PR 数量级领先，具备“跨9家邮件供应商浏览器自动化”等复杂 RPA 用例 | 安全响应速度快（P0漏洞当日修复），版本节奏清晰（里程碑命名），社区贡献者协作流程规范（998 PRs / 370+ 贡献者） |
| **技术路线差异** | 强调“外部化插件”与“重入保护”等工程级特性，更偏向**集成编排** | 强调“判断力”与“自主性”，内置 Cron 任务注入、Advisor 模型路由，更偏向**决策智能体** |
| **社区规模** | 每日500 PRs，Issue 讨论热度高（单个Issue获5👍即被视为“最热”），用户群体偏**重度自部署者** | 每日50 PRs，社区讨论更聚焦（如 True Autonomy 获11👍），用户群体偏**技术尝鲜与自动化爱好者** |

### 生态整体定位

OpenClaw 是目前个人 AI 助手领域**社区参与度最密集**的项目之一，类似“Kubernetes 级别的编排框架”，但当前版本质量控制暴露短板。Hermes Agent 则更接近“LangChain + 自主决策”的结合体，在小而精的社区中快速迭代新范式。

---

## 4. 共同关注的技术方向

两个项目均出现了以下跨项目需求（注：需求虽源于特定项目，但反映了生态整体趋势）：

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|---------|----------|
| **内存安全与信任** | OpenClaw (#7707)、Hermes Agent（隐含） | 防止来自不可信源（如网页、第三方集成）的记忆投毒攻击，要求“基于来源的信任标记” |
| **真实自主性（True Autonomy）** | OpenClaw（Cron任务注入、持久化例程注册表 #98727）、Hermes Agent (#5712) | 希望Agent能自动将后台任务结果注入实时会话，形成无需人工干预的闭环工作流 |
| **会话状态持久化** | OpenClaw (#45608 / #40418)、Hermes Agent（iMessage sidecar 状态保持） | 解决 `/new` 重置后上下文丢失、Sidecar 崩溃后自动恢复状态 |
| **跨平台一致性** | OpenClaw（多平台回归问题）、Hermes Agent（Telegram / iMessage / Docker） | 各适配器在行为、错误处理、日志输出上应保持统一标准 |
| **成本控制与速率限制** | OpenClaw (#13615)、Hermes Agent (#13983 Token消耗过高) | 用户对默认 Token 消耗和 API 速率限制提出质疑，需要可配置的节流与计量功能 |

---

## 5. 差异化定位分析

| 维度 | **OpenClaw** | **Hermes Agent** |
|------|-------------|------------------|
| **功能侧重** | 插件生态与多平台集成（10+ 通讯平台）、任务编排（浏览器自动化、工具链组合） | 自主决策机制（Cron注入、MoA优化）、安全沙盒、技能（Skill）系统（如加密货币数据） |
| **目标用户** | 高级用户、系统管理员、希望构建“个人数字员工”的开发者 | 技术爱好者和早期采用者，追求“AI Agent 自主工作”的实验者 |
| **技术架构关键差异** | 采用“外部化插件”模型，每个插件独立风险管理（如 JSON 响应大小限制）；**重入保护**是核心防御机制 | 内置“Sidecar”进程模型（如 iMessage 适配器），通过 **Shell 语法解析** 实现危险命令检测；**MoA 参考限制**降低延迟 |
| **版本发布策略** | 频率较高但质量控制不稳（v2026.6.11发布缺失关键组件） | 里程碑式发布（v0.17.0 → v0.18.0 间隔约一个月），有破坏性变更说明和迁移指南 |
| **运维复杂度** | 高：需配置多平台令牌、插件权限、内存搜索等 | 中：提供 CLI 与 TUI，但 Sidecar 稳定性和桌面应用兼容性仍有问题 |

---

## 6. 社区热度与成熟度

### 活跃度分层

- **第一梯队（极高活跃，但处于“质量巩固”阶段）**  
  **OpenClaw**：每日500 PRs、251 Issues，社区贡献狂热的背后是版本回归带来的大量修复工作。健康度评分较低，属于“快速迭代导致技术债务累积”的典型。
  
- **第二梯队（高活跃，处于“快速迭代+逐步稳定”阶段）**  
  **Hermes Agent**：每日50 PRs，发布大版本同时修复P0漏洞，社区贡献流程成熟（998 PRs / 370+贡献者）。健康度中等，但长期Bug（iMessage死循环、Token消耗）仍待解决。

### 成熟度标志

- **OpenClaw**：已具备企业级生态雏形（多平台、插件市场、内存搜索），但缺少稳定的 LTS 版本。
- **Hermes Agent**：版本命名体系清晰（v0.x.x），提供迁移指南和破坏性变更说明，更接近“产品化”阶段。

---

## 7. 值得关注的趋势信号

1. **“可靠性优先”取代“功能优先”**  
   OpenClaw 的 v2026.6.11 回归危机与 Hermes Agent 的 P0 安全漏洞修复表明，用户已对“早上起来突然坏了”零容忍。**开发者应优先建立自动化回归测试、重放保护、发布流水线质量门禁**。

2. **自主性（Autonomy）进入实战验证期**  
   True Autonomy（Cron 结果注入实时会话、持久化例程注册表）是同时被两个项目社区强烈呼吁的特性。这表明通用智能体的下一个关键突破点在于**无缝衔接任务调度与对话上下文**，而非简单的工具调用。

3. **记忆安全成为新战场**  
   内存信任标记（来源级标签）、审计日志等需求涌现，指向Agent 记忆系统的**可解释性与抗污染**。未来 Agent 框架需内置“记忆加密+签名验证”能力，以防通过第三方集成投毒。

4. **Token 成本意识觉醒**  
   默认 Token 消耗过高（Hermes Agent #13983 中一次性消耗16K+）引发广泛讨论，**可配置的提示词压缩、请求节流、模型路由**将成为基础功能需求。

5. **跨平台适配器标准化压力增大**  
   iMessage、微信、Telegram 等平台的稳定性问题反复出现，社区开始要求**统一适配器规范**（包括错误码、重试策略、日志格式），这可能会催生“平台适配层”的开源标准。

---

**总结**：个人 AI 助手开源生态正处于从“功能探索”到“工程化落地”的关键转折点。开发者若想基于这些项目构建产品，应优先关注 **版本兼容性、记忆安全机制和长期维护能力**，而非单纯追求功能密度。OpenClaw 适合需要多平台快速集成的场景，Hermes Agent 更适合追求自主决策实验的场景。两个项目都在各自方向上面临“从狂热到成熟”的阵痛，这也是开源社区成长的必然阶段。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-07-02

## 1. 今日速览

- 项目整体活跃度极高：过去24小时内累计产生**50条 Issue 更新、50个 PR 更新**，同时发布了 **v0.18.0 (v2026.7.1) 大版本**，标志着项目进入“判断力（Judgment）”里程碑。
- 社区贡献踊跃：新版本自 v0.17.0 以来已合并 **998 个 PR**，关闭 **949 个 Issues**，涉及 **370+ 社区贡献者**，代码变更量约 **25 万行插入、4.1 万行删除**。
- 安全与稳定性是今日关注焦点：出现 **P0 级安全漏洞（#36846）** 已被修复关闭，另有 **多个 P2 级 Bug** 报告，主要集中在 Sidecar 通讯、Token 消耗、平台兼容性等方面。
- 功能需求旺盛：**True Autonomy（真实自主性）**、**任务感知模型路由** 等高级特性获得社区强烈关注，反映出用户对 Agent 自主决策和精细化控制的需求持续增长。
- 项目健康度：在快速迭代的同时保持了对 Bug 的快速响应（接近半数 Issue 已有关联 PR 修复），但部分长期积压的 PR 仍需维护者关注。

## 2. 版本发布

### v0.18.0 (v2026.7.1) — The Judgment Release

- **发布标签**：`v2026.7.1`
- **变动规模**：自 v0.17.0 以来 ~1,720 commits · 998 merged PRs · 2,215 files changed · ~251,000 insertions · ~41,000 deletions · 949 issues closed · 370+ community contributors
- **核心主题**：**“Judgment”（判断力）**——本次发布重点强化了 Agent 的自主决策能力，包括 Cron 背景任务与实时会话的融合、MoA（Mixture-of-Agents）的延迟优化、安全沙盒改进等。
- **主要亮点（从 PR/Issue 推断）**：
  - **True Autonomy 基础**：Cron 任务结果可自动注入实时聊天会话（Feature #5712 虽未关闭，但相关 PR 已合入基础能力）。
  - **MoA 性能优化**：`reference_max_tokens` 参数可缩减 Advisor 输出，减少单轮延迟约 44%（PR #56756）。
  - **安全升级**：危险命令黑名单改为不可绕过的 Shell 解析（修复 #36846）。
  - **环境与工具链**：Docker 镜像修复 Exa 搜索不可用 (#49445)，新增 `ssl_ca_cert` 字段支持自签名证书。
- **破坏性变更 / 迁移注意事项**：
  - `custom_providers` 中新增 `ssl_ca_cert` 字段，若之前依赖全局 `verify=False` 绕过，需更新配置。
  - 危险命令匹配规则变更（从字符串匹配改为 Shell 语法解析），部分自定义 deny 规则可能需要调整。
  - Cron 任务投递行为调整（`direct_messages_topic_id` 处理逻辑变更），影响 Telegram 私聊群组用户。
- **推荐操作**：用户执行 `hermes update` 更新至 v0.18.0，并检查配置文件中 `dangerous_command_denylist` 和 `custom_providers` 设置。

## 3. 项目进展

今日合并/关闭了 **15 个 PR**，主要推进方向如下：

### 关键合并 PR

| PR | 标题 | 类型 | 影响组件 | 说明 |
|----|------|------|----------|------|
| #56743 | `fix(gateway): transcribe voice messages during pending clarify` | Bug修复 | Gateway / Telegram | 修复 `clarify` 等待用户回复时语音消息被静默丢弃的问题 |
| #56754 | `feat(skills): add surf crypto data skill` | 新功能 | Skills | 新增可选技能 `surf`，提供 83+ 只读加密货币数据命令 |
| #45285 | `fix(mcp): rotate and filter stderr logs` | 优化 | MCP | 对 stdio MCP 子进程 stderr 进行旋转和过滤，减少日志噪声 |
| #22369 | `fix(tui): prevent transcript tail cutoff` | Bug修复 | TUI | 修复流式输出停止后会话窗口底部被截断的问题 |
| #30651 | `feat(agent): add provider fallback telemetry helper` | 新功能 | Agent / Telemetry | 新增 provider 故障切换的 JSONL 事件记录，便于运维排查 |
| #56752 | `fix(tui): check prebuilt bundle before requiring ui-tui/ workspace` | Bug修复 | CLI / TUI | 修复 `hermes --tui` 在无 workspace 时直接报错的问题 |
| #56751 | `fix(auth): use SameSite=None for PKCE cookie over HTTPS` | Bug修复 | Auth / Dashboard | 修复跨域 OAuth 登录时 PKCE cookie 丢失问题 |
| #56723 | `fix(update): detect profile dashboard processes in stale-dashboard sweep` | Bug修复 | CLI | 修复 `hermes update` 后无法正确关闭非默认 profile 的 Dashboard 进程 |
| #43876 | `fix(cron): require exact silent marker for delivery suppression` | Bug修复 | Cron | 强化 `[SILENT]` 标记必须完全匹配，防止误拦截 |

**总体进展**：项目在 Agent 核心逻辑（语音、日志、安全）、平台适配（Telegram、MCP）、开发者体验（TUI、CLI）等多个维度均有实质性修复和功能增强。v0.18.0 发布后，更多社区贡献正在快速进入 `main` 分支。

## 4. 社区热点

今日讨论热度最高的 Issues/PRs 反映出用户对 **自主性、稳定性、跨平台体验** 的强烈关注。

| 排名 | Issue/PR | 标题 | 评论数 | 👍 数 | 核心诉求 |
|------|----------|------|--------|-------|----------|
| 1 | [#5712](https://github.com/NousResearch/hermes-agent/issues/5712) | [Feature]: True Autonomy - Automatically Inject Cron Results into Live Gateway Chat Sessions | 11 | 11 | 用户希望 Cron 任务的结果能够自动推送到实时聊天会话中，实现真正无干预的自主工作流。背景：Cron 在隔离会话中运行，但结果需要手动查询或仅通过文件传递，无法融入对话上下文。 |
| 2 | [#49858](https://github.com/NousResearch/hermes-agent/issues/49858) | Photon iMessage: sidecar death causes silent reconnect death spiral (no respawn) | 8 | 0 | iMessage 适配器在 sidecar 崩溃后进入静默重连死循环，用户必须手动重启 Gateway。该问题影响重要通讯通道的可靠性。 |
| 3 | [#13983](https://github.com/NousResearch/hermes-agent/issues/13983) | [Bug]: 16K Tokens consumption by default | 6 | 1 | 用户反映默认配置下发送“who u?”这样简单问题时消耗 16K+ tokens，质疑过多。社区观点分化（有人认为是 prompt 模板问题，有人认为是模型解析开销）。 |
| 4 | [#55658](https://github.com/NousResearch/hermes-agent/issues/55658) | [Bug] It cannot be started after updating | 4 | 0 | 更新后桌面应用无法启动（附截图），可能是配置文件或依赖问题，社区尚无明确重现步骤。 |
| 5 | [#49445](https://github.com/NousResearch/hermes-agent/issues/49445) | search.exa completely non-functional in official Docker image | 4 | 0 | Docker 镜像中 Exa 搜索后端失效，影响 web_search 和 web_extract 工具。该问题已在 v0.18.0 中修复（见 Releases）。 |

**分析**：第 1 位的 #5712 表明高级用户已不满足于简单的自动化，而是追求 Agent 能够无缝衔接环境内外部事件，形成闭环工作流。该 Feature 获得了 11 个 👍，社区参与度很高。第 2 位的 #49858 则凸显了稳定性的核心需求，尤其是对支持商业级通信渠道（iMessage）来说，Sidecar 的自动重启机制至关重要。

## 5. Bug 与稳定性

以下按严重程度排列今日报告的 Bug，同时标注是否已有修复 PR 合并或关闭。

### P0（严重安全漏洞）
- **[已关闭/已修复]** [#36846](https://github.com/NousResearch/hermes-agent/issues/36846) — **危险命令黑名单可绕过 → 静默 RCE**  
  漏洞描述：`DANGEROUS_PATTERNS`/`HARDLINE_PATTERNS` 使用字符串匹配，可被反斜杠/引号绕过。  
  修复：PR #56751 及系列提交已将匹配改为 Shell 语法解析。**用户强烈建议立即升级 v0.18.0。**

### P2（高影响 Bug）
1. **[#49858](https://github.com/NousResearch/hermes-agent/issues/49858) — Photon iMessage sidecar 死亡导致静默重连死循环**  
   状态：OPEN（无合并 PR）  
   影响：iMessage 通道永久性不可用，需手动重启 Gateway。建议优先处理。
2. **[#13983](https://github.com/NousResearch/hermes-agent/issues/13983) — 默认 Token 消耗过高（16K+）**  
   状态：OPEN（尚无 PR）  
   影响：所有用户默认配置下均会浪费大量 Tokens，增加成本与延迟。
3. **[#55658](https://github.com/NousResearch/hermes-agent/issues/55658) — 更新后桌面应用无法启动**  
   状态：OPEN（需要更多信息）  
   影响：Windows 用户可能卡在更新流程。
4. **[#56533](https://github.com/NousResearch/hermes-agent/issues/56533) — `/journey` 命令泄露原始 ANSI 转义码**  
   状态：CLOSED（已由 @louquillio 提交修复）  
   影响：TUI/Desktop 聊天气泡显示乱码。
5. **[#56717](https://github.com/NousResearch/hermes-agent/issues/56717) — 非默认 profile 保留过期运行时导致 ImportError**  
   状态：OPEN（已有 PR #56723 合并修复？实际上 PR #56723 是针对 Dashboard 进程，而本 Issue 是运行时 ImportError，可能尚未完全解决）  
   建议：确认 PR #56723 是否覆盖或关闭本 Issue。
6. **[#56704](https://github.com/NousResearch/hermes-agent/issues/56704) — `computer_use` capture 在 Linux/WSL 崩溃（int(None)）**  
   状态：OPEN（尚无 PR）  
   影响：Linux 桌面环境无法使用计算机控制工具。
7. **[#56732](https://github.com/NousResearch/hermes-agent/issues/56732) — `hermes-api-server` / `hermes-acp` 丢失整个 terminal 工具集**  
   状态：OPEN（标记为 duplicate，需确认是否被其他 PR 修复）
8. **[#56727](https://github.com/NousResearch/hermes-agent/issues/56727) — Kimi /coding endpoint thinking 被错误阻止**  
   状态：OPEN（无需紧急，但影响 Kimi 模型用户的推理能力）
9. **[#55265](

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*