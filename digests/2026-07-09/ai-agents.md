# OpenClaw 生态日报 2026-07-09

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-07-09 02:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-07-09

---

## 1. 今日速览

过去 24 小时内，OpenClaw 项目保持了极高的社区活跃度：共产生 500 条 Issue 更新（新开/活跃 457 条，关闭 43 条）和 500 条 PR 更新（待合并 407 条，已合并/关闭 93 条）。无新版本发布。**P1 级稳定性和安全性问题**仍然是社区关注的核心，多个“Diamond Lobster”评级的长期 Bug 仍在讨论中。与此同时，大量针对聊天渠道（Telegram、Discord、Feishu、Zalo）的修复 PR 涌入，表明维护团队正集中精力清理消息传输中的“泄漏”和“丢失”问题。总体来看，项目处于**高强度的缺陷修复与功能打磨阶段**，社区参与度极强，但大量高优先级 Issue 积压值得注意。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日关闭/合并的 PR 数量为 93 条，以下为在“最新 Pull Requests”列表中出现且已关闭的几项关键变更，它们代表了项目在关键问题上的实际推进：

- **#102359** (CLOSED) — `fix(openai): stringify replayed tool call arguments`：修复 Ollama 云模型通过 OpenAI-compatible 路由时，重放工具调用参数可能为对象导致拒绝的问题。直接修复 Issue #102200。
- **#98299** (CLOSED) — `feat: add hosted feed envelope verifier`：为托管 feed 信任验证添加签名信封验证器，是系列安全基建的第一步（关联 RFC）。
- **#101296** (CLOSED) — `fix(whatsapp): suppress unhandled rejections from void fire-and-forget calls`：消除 WhatsApp 扩展中四个未捕获的 Promise 拒绝，防止网关进程崩溃。
- **#101668** (CLOSED) — `fix(cron): keep system event queued when main-session heartbeat is disabled`：修复 cron 系统事件在独立会话心跳禁用时被丢失的问题。

这些 PR 集中在**模型兼容性、管道安全性、渠道稳定性**三个方向，项目整体正向收敛并解决早期反馈的可靠性问题。

---

## 4. 社区热点

今日评论数最高的 Issue 集中反映了用户对**信息流安全与会话一致性**的强烈诉求：

- **#25592** (35 条评论) — “Text between tool calls leaks to messaging channels” ([链接](https://github.com/openclaw/openclaw/issues/25592))  
  **诉求**：代理在工具调用之间产生的内部文本（如错误处理、处理确认）被错误地路由到消息通道，造成严重的 UX 问题。用户期望此类内部输出不应出现在最终用户面前。此 Issue 标签包含 `impact:session-state`、`impact:security`、`impact:message-loss`，为 P1 钻石级。
- **#44925** (21 条评论) — “[Bug]: Subagent completion silently lost — no retry, no notification, no auto-restart on timeout” ([链接](https://github.com/openclaw/openclaw/issues/44925))  
  **诉求**：子代理任务在超时或完成通知失败时静默丢失结果，无任何重试或通知机制。用户强调这是“silent data loss”，严重破坏了对多代理编排的信任。
- **#48003** (15 条评论) — “Steer mode does not inject messages mid-turn for main sessions” ([链接](https://github.com/openclaw/openclaw/issues/48003))  
  **诉求**：`messages.queue.mode: "steer"` 无法在正在进行的回合中注入用户消息，消息要等到当前回合完成才被处理，破坏了实时干预体验。该 Issue 带有 3 个 👍 和多个 `impact` 标签。
- **#85333** (15 条评论) — “[Bug]: openclaw doctor --fix 4-5x slower … session snapshot path traversal bottleneck” ([链接](https://github.com/openclaw/openclaw/issues/85333))  
  **诉求**：性能回归，版本 2026.5.20 比前版本慢 4-5 倍，根因是会话快照遍历的路径实现导致 IO 开销剧增，用户在生产环境实测数据充分。

这些热点反映出社区对**透明性、可靠性、实时性**的高度关注，尤其是多代理编排和跨渠道消息行为。

---

## 5. Bug 与稳定性

以下按严重程度排列今日讨论中最关键的 Bug，并标注是否已有 fix PR。注意：部分 Issue 虽未在今日 PR 列表中出现关联修复，但可能已有进展。

| 严重等级 | Issue | 问题描述 | 关联 Fix PR |
|----------|-------|---------|------------|
| **P0** | [#43661](https://github.com/openclaw/openclaw/issues/43661) | Session 缩容超时导致无限挂起、重复消息发送 | 未发现直接关联 PR |
| **P0** | [#48920](https://github.com/openclaw/openclaw/issues/48920) | 在线文档与发布版本不一致（Live Docs ahead of release） | 未发现直接关联 PR |
| **P1** | [#25592](https://github.com/openclaw/openclaw/issues/25592) | 工具调用间文本泄漏到消息通道 | 未发现直接关联 PR |
| **P1** | [#44925](https://github.com/openclaw/openclaw/issues/44925) | 子代理完成静默丢失 | 未发现直接关联 PR |
| **P1** | [#48003](https://github.com/openclaw/openclaw/issues/48003) | Steer 模式无法在回合中注入消息 | 未发现直接关联 PR |
| **P1** | [#43367](https://github.com/openclaw/openclaw/issues/43367) | 多代理编排不稳定：并发配置覆盖、会话锁失败、子工作脱离 | 未发现直接关联 PR |
| **P1** | [#94228](https://github.com/openclaw/openclaw/issues/94228) | Anthropic 原生路径 replay thinking block 时 400 错误导致持久不可用 | 未发现直接关联 PR |
| **P1** | [#43996](https://github.com/openclaw/openclaw/issues/43996) | 沙盒容器因 `no-new-privileges` 立即退出 | 未发现直接关联 PR |
| **P1** | [#47910](https://github.com/openclaw/openclaw/issues/47910) | 提供者无法按失败类型分类回退，认证错误浪费延迟 | 未发现直接关联 PR |
| **P1** | [#99912](https://github.com/openclaw/openclaw/issues/99912) | Agent 心跳路由到错误 Agent 的会话 | 未发现直接关联 PR |

另有大量 **P2** 级 Bug 集中在渠道适配器（Discord 泄漏内部工具追踪 #44905，Feishu 图片丢失 #41744，Telegram 路由问题 #41165）和性能回退（#85333 已列在社区热点）。值得注意的是，今日有多个 PR 明确修复了 OpenAI/Ollama 兼容性（#102359）、WhatsApp 未捕获异常（#101296）、cron 事件丢失（#101668）等具体问题，说明维护团队正在逐项消化高优先级的稳定性缺陷。

---

## 6. 功能请求与路线图信号

今日讨论中涌现了多项功能请求，结合已有 PR 趋势，以下几条最有可能被纳入近期开发规划：

- **#39604** (13 条评论) — `[Feature]: Add tools.web.fetch.allowPrivateNetwork to allow private network access` ([链接](https://github.com/openclaw/openclaw/issues/39604))  
  用户强烈希望增加 `allowPrivateNetwork` 配置项以便访问内网资源。11 个 👍 和 `linked-pr-open` 标签表明已有相关 PR 在讨论。
- **#42475** (12 条评论) — `[Feature]: Per-agent cost budget enforcement at the gateway level` ([链接](https://github.com/openclaw/openclaw/issues/42475))  
  运营者需要每个 Agent 的每日/每月成本上限，防止意外花费。P2 钻石，`needs-product-decision` 表明团队正在权衡。
- **#43454** (7 条评论) — `Feature Request: Gateway lifecycle hooks` ([链接](https://github.com/openclaw/openclaw/issues/43454))  
  开发者希望在工作区层面挂钩子代理完成、工具调用阈值、回合完成等事件，以替代当前的提示工程和轮询方案。
- **#42840** (8 条评论) — `Feature Request: Add MathJax/LaTeX Support to Control UI` ([链接](https://github.com/openclaw/openclaw/issues/42840))  
  9 个 👍，社区对科学计算的展示有刚性需求。
- **#45758** (7 条评论) — `Feature Request: Support YAML as config file format` ([链接](https://github.com/openclaw/openclaw/issues/45758))  
  用户希望替代 JSON5，以提升可读性和与 DevOps 工具链的兼容性。

此外，`#45608`（预热冲内存刷新）、`#40001`（write 工具追加模式）、`#39406`（抑制瞬态工具错误警告）等改进也获得较高共鸣。从 PR 列表看，今天上线了 `feat(exec): memoize duplicate auto-review verdicts` (#102362) 和 `feat(subagents): native announceTarget` (#101248，进行中) 等功能性改进，说明团队在稳定性的同时也在推进用户呼声较高的特性。

---

## 7. 用户反馈摘要

从 Issue 评论和摘要中提炼的真实用户痛点：

- **消息泄漏成最大困扰**：多位用户报告工具调用间的内部文本（如 `NO_REPLY`、`to=functions.memory_search`）被直接发送到 Discord/Telegram 通道，造成信息混乱和安全隐患（#25592、#44905）。
- **子代理静默失败影响生产力**：用户 `IIIyban` 描述 “Subagent task orchestration has multiple failure modes where results are silently lost”，认为这是“silent data loss”并影响了对 OpenClaw 的信任（#44925）。
- **性能回退显著**：生产用户实测 `openclaw doctor --fix` 从 55 秒飙升至 229 秒以上，IO 瓶颈让日常维护变得痛苦（#85333）。
- **记忆管理行为不一致**：用户 `AM-young-fun` 抱怨同一团队 3 人的记忆系统行为完全不同（有的用 SQLite，有的用文件存储），无法协同工作（#43747）。
- **多代理编排脆弱**：用户 `waliddafif` 尝试并行编码时遇到配置覆盖、会话锁死、子工作无法清理等问题，认为“multi-agent runs unreliable in practice”（#43367）。
- **聊天渠道适配缺陷**：Feishu 图片丢失（#41744）、Telegram DM 路由错误（#41165）、Discord 链接参数丢失（#102162 相关）等，反映出渠道适配的成熟度仍有差距。

积极反馈方面：用户对 `sessions_send` 反向调用导致重复消息（#39476）的详细分析得到认可；“J-Lens observable skill” PR（#102361）可能带来新的可观测能力，社区贡献活跃。

---

## 8. 待处理积压

以下为长期未获得维护者响应或进展迟缓的高价值 Issue/PR，提醒关注：

- **#41744** (P1，标记 `stale`) — Feishu 图片工具结果在最终负载中丢失，自 2026-03-10 开启，至今无相关 fix PR。([链接](https://github.com/openclaw/openclaw/issues/41744))
- **#45314** (P2，标记 `stale`) — 早期中止响应模板变量未填充，自 2026-03-13 开启，无进展。([链接](https://github.com/openclaw/openclaw/issues/45314))
- **#45765** (P2，标记 `stale`) — `OPENCLAW_HOME` 环境变量导致嵌套目录，自 2026-03-14 开启，虽已有 `linked-pr-open` 但 PR 状态不明。([链接](https://github.com/openclaw/openclaw/issues/45765))
- **#44098** (PR，自 2026-03-12 开启) — 沙盒容器默认 pidsLimit 防止 fork bomb，但长期未合并，当前标记 `stale` 且 `needs-real-behavior-proof`。([链接](https://github.com/openclaw/openclaw/pull/44098))
- **#89028** (PR，自 2026-06-01 开启) — `web_fetch` 提取完整 HTML 内容，已等待一个多月且有足够证明，仍处于 `ready for maintainer look` 但未合入。([链接](https://github.com/openclaw/openclaw/pull/89028))
- **#96230** (PR，自 2026-06-24 开启，P1) — 会话重复重启恢复修复，视频证明充分，但挂起在 `ready for maintainer look`，需要维护者干预。([链接](https://github.com/openclaw/openclaw/pull/96230))

这些积压项涉及渠道、安全、性能和核心会话管理，需要优先安排评审与合并，以降低社区不满情绪。

---

**总结**：OpenClaw 项目正处于快速迭代期，今日 1000+ 次的更新表明社区极度活跃。但 P1 级稳定性 Bug 基数较大，功能请求堆积，维护团队需平衡新功能开发与关键缺陷的修复速度。持续关注“消息泄漏”与“子代理可靠性”将成为提升用户满意度的关键。

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我根据您提供的两份详细日报，为您生成以下横向对比分析报告。

---

### **AI 智能体与个人 AI 助手开源生态横向对比分析报告**

**报告日期：** 2026-07-09
**分析对象：** OpenClaw、Hermes Agent
**分析师：** 资深技术分析师

#### **1. 生态全景**

当前个人 AI 助手（PAA）与自主智能体开源生态正处于 **由“功能可用”向“生产可靠”跨越的关键阶段**。社区活动极度活跃，但重心从炫技式功能开发转向了对 **消息一致性、会话状态管理、多代理编排可靠性以及安全边界** 的“补课”。主要玩家在高强度迭代中暴露出相似的架构痛点：工具调用与消息管道之间的“泄漏”问题成为公敌，子代理的“静默失败”严重侵蚀用户信任，而跨平台（桌面、CLI、消息应用）会话管理的碎片化则凸显了基础设施的不足。整体而言，市场热情高涨，但技术成熟度仍有显著提升空间。

#### **2. 各项目活跃度对比**

| 项目 | Issue 更新总数 | (新开/活跃) | (已关闭) | PR 总数 | (待合并) | (已合并/关闭) | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 457 | 43 | 500 | 407 | 93 | 无 | **高活跃，高压力 (待办积压严重)** |
| **Hermes Agent** | 50 | 47 | 3 | 50 | 49 | 1 | v0.18.2 | **活跃但PR效率低 (大量待合并)** |

**分析：**
- **OpenClaw** 的社区体量是 Hermes Agent 的 **10倍**，反映出其作为生态核心参照的地位。然而，其极高的 Issue 和 PR 待办积压量（约80%）表明项目处于 **高负荷冲刺** 状态，维护团队的消化能力面临挑战。
- **Hermes Agent** 活动量适中，但 PR 合并率极低（仅2%），这表明其维护可能更保守，或社区贡献的 PR 质量、与路线图契合度有待提升。
- 两个项目都表现出“高产出、低合并”的特征，是开源社区普遍现象，但在稳定性关键期，可能拖慢缺陷修复速度。

#### **3. OpenClaw 在生态中的定位**

- **行业参照与标杆**：OpenClaw 凭借其庞大的社区、丰富的 PR 和 Issue 讨论，已成为事实上的生态参照系。其 P1/P0 级 Bug 直接定义了整个行业当前面临的核心技术挑战。
- **技术路线的“集大成者”**：相比 Hermes Agent 侧重桌面体验，OpenClaw 更强调 **多模态渠道（Telegram, Discord, Feishu, Zalo）、多模型提供商兼容（Ollama, Anthropic）以及复杂的多代理编排**。其技术栈更全面，但也因此面临更复杂的集成问题。
- **优势与挑战并存**：OpenClaw 的优势在于 **生态领导力和功能广度**，但代价是 **稳定性风险更高、核心 Bug 解决周期更长**。报告显示其多个 P1 bug 长时间无 fix PR，而规模更小的 Hermes Agent 在类似问题上反应可能更快。
- **社区规模对比**：从 Issue/PR 数量（500 vs 50）来看，OpenClaw 社区规模约为 Hermes Agent 的 **8-10倍**，这验证了其作为“旗舰项目”的地位。

#### **4. 共同关注的技术方向**

| 共同技术方向 | 涉及项目 | 具体诉求 (Issue 示例) | 行业意义 |
| :--- | :--- | :--- | :--- |
| **消息泄漏与信息流控制** | OpenClaw, Hermes Agent | #25592 (OpenClaw): 工具调用间文本泄漏；#44905 (OpenClaw): Discord 泄漏内部追踪 | 这是 PAA 从“玩具”走向“产品”的**第一大障碍**，关系到用户信任和信息安全。 |
| **子代理/多代理编排可靠性** | OpenClaw, Hermes Agent | #44925 (OpenClaw): 子代理静默丢失；#43367 (OpenClaw): 多代理不稳定 | 自主智能体的核心价值在于复杂任务分解，但 **编排的“黑盒化”和“不可预测性”** 是当前最大的体验杀手。 |
| **会话状态一致性与可见性** | OpenClaw, Hermes Agent | #59224 (Hermes): CLI 隐藏桌面会话；#48003 (OpenClaw): Steer 模式回合中失效 | 用户期望在多端无缝切换，但 **会话状态管理、同步和中断处理** 的架构设计尚未成熟。 |
| **工具调用与上下文管理** | OpenClaw, Hermes Agent | #5254 (Hermes): 工具调用重复；#39691 (Hermes): 工具输出压缩 | 随着 Agent 链路变长，**工具调用的准确性、重复性以及上下文窗口管理** 成为性能瓶颈。 |

#### **5. 差异化定位分析**

| 维度 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **功能侧重** | **企业级多Agent协同与渠道集成**。强调复杂的编排能力、多消息网关、安全策略。 | **桌面端个人工作流助手**。侧重桌面应用体验、CLI 交互、与本地开发环境（LM-Studio）的集成。 |
| **目标用户** | 开发者、DevOps 团队、企业运营者。需要构建可扩展、多触点、多模型的后台服务。 | 个人开发者、技术创作者、桌面用户。强调开箱即用的桌面体验和轻量级部署。 |
| **技术架构** | **模块化、服务导向**。抽象出网关、会话引擎、模型路由、安全签名等独立服务。 | **事件驱动、单进程为主**。核心逻辑与桌面应用绑定，依赖插件和适配器扩展。 |
| **核心挑战应对** | **所有问题都要解决**：从模型兼容性到渠道稳定，再到性能回退，复杂度最高。 | **聚焦用户体验**：重点解决桌面端显示、中文支持、附件管理等直接面向用户感知的问题。 |

#### **6. 社区热度与成熟度**

- **分层清晰**：
    - **第一梯队 (快速迭代，需关注稳定性)**：**OpenClaw**。社区极度活跃，但高频迭代也伴随着大量高优 Bug。项目处于“边飞边修发动机”的阶段。其成熟度更多体现在**架构设计的“野心”** 而非**生产稳定性**。
    - **第二梯队 (稳定增长，功能打磨)**：**Hermes Agent**。活动量适中，版本发布节奏可控。项目处于“为发动机改装滤清器”的阶段，更注重用户体验的细节打磨。其成熟度更多体现在**桌面应用的“完成度”** 上。

#### **7. 值得关注的趋势信号**

1.  **“消息分控”成为刚需**：OpenClaw 和 Hermes Agent 都涌现了关于“工具调用间文本泄漏”的强烈批评。这预示着，**Agent 内部操作逻辑与面向用户的对话流必须解耦**，“消息过滤与审计”将成为任何生产级 PAA 的核心能力。

2.  **本地模型兼容仍是痛点**：Hermes Agent 中 LM-Studio 工具调用重复的问题持续三个月未解决，说明**本地推理模型的 API 行为与主流闭源模型存在显著差异**。这将是推动 Agent 框架兼容本地模型的关键挑战，也为针对特定硬件/NPU 优化的 Agent 适配器创造了机会。

3.  **显示偏好开始“卷”**：两个项目都出现了大量关于**代码块格式、思考面板行为、中文/数学公式渲染**的讨论。这表明当基础功能可用后，**开发者/用户对 Agent 输出质量和可读性的要求正在快速提升**，AI UI/UX 成为新的竞争点。

4.  **“成本/资源管控”前置**：OpenClaw 的 #42475（Per-agent 成本预算）和 Hermes Agent 的 #39691（工具输出压缩）表明，随着 Agent 使用规模扩大，**运营者开始将 Token 消耗和 API 成本视为核心 TCO（总拥有成本）指标**。架构设计中的成本治理功能将越来越重要。

**对开发者的启示**：在构建个人 AI 智能体时，应当优先投资于 **1) 清晰的消息路由与过滤层**，防止内部信息外泄；**2) 健壮的会话状态管理**，支持中断和恢复；以及 **3) 可观测的 Agent 推理过程**，避免“静默失败”。这些是比“增加一个炫酷工具”更基础、更关键的工程决策。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-07-09

---

## 1. 今日速览

过去 24 小时项目保持高度活跃：共产生 **50 条 Issue 更新**（新开/活跃 47，已关闭 3）和 **50 条 PR 更新**（待合并 49，已合并/关闭 1），并发布了一个同日的紧急补丁版本 **v0.18.2**。社区讨论集中在桌面应用体验（会话可见性、中文显示、文件上传）、网关适配器兼容性以及工具调用重复等稳定性问题上。整体看，项目健康度良好，但大量待合并 PR 需维护团队关注进度。

---

## 2. 版本发布

### Hermes Agent v0.18.2 (v2026.7.7.2) — 2026-07-07

- **更新内容**：针对 v0.18.1 的同日补丁，修复了 WhatsApp Baileys 依赖锁定问题，确保 tagged-release Docker 构建正常工作。
- **具体变更**：`fix(whatsapp): unpin Baileys from git commit, use published 7.0.0-rc13`
- **破坏性变更**：无。
- **迁移注意事项**：无需手动操作；使用 Docker 的用户可直接拉取新镜像。

---

## 3. 项目进展

### 已合并/关闭的 PR（共 1 条）

- **[#61087] Desktop app does not stop gateway on quit (macOS)** [已关闭]  
  该 Bug Issue 已关闭，合并了相关修复。用户关闭 macOS 桌面应用时，后台网关不再继续运行。  
  https://github.com/NousResearch/hermes-agent/issues/61087

### 重要待合并 PR 状态推进

- **[#58023] fix: keep shell fences rendered as code blocks** — 修复桌面端将 shell 代码块降级为普通文本的问题，经过多轮 review 后状态更新为已获得 approve。  
  https://github.com/NousResearch/hermes-agent/pull/58023

- **[#60741] fix: add explicit UTF-8 encoding to subprocess text=True calls** — 针对 Windows 平台的中文编码问题提交修复，补充了 #55339 未覆盖的调用点。  
  https://github.com/NousResearch/hermes-agent/pull/60741

- **[#39754] fix(plugins): update hindsight embedded dependency** — 长达一个月未合并的依赖修复 PR，今日获得更新（新增 review comment），建议维护者尽快合并。  
  https://github.com/NousResearch/hermes-agent/pull/39754

---

## 4. 社区热点

### 评论数/反应最高的 Issues

| Issue | 评论 | 👍 | 核心诉求 |
|-------|------|----|----------|
| [#39691] feat(compression): integrate headroom-ai for tool output compression | 9 | 12 | 提出在工具输出层面进行压缩，而非仅对话级压缩，提升长会话效率。获得大量点赞，说明社区对上下文窗口优化高度关注。 |
| [#59224] Bug: Classic CLI /resume listing hides Desktop sessions | 8 | 0 | 用户发现 CLI 模式的 `/resume` 列表仅显示 `source="cli"` 的会话，隐藏了桌面端和 WebUI 创建的会话，影响多端衔接。 |
| [#39534] v0.15.1 Desktop Windows cutted off chinese prompt | 7 | 0 | 中文输入截断问题（升级后出现），用户提供了详细截图和复现步骤，多位用户跟帖确认。 |
| [#5254] Tool calls repeating when using LM-Studio | 4 | 0 | 老 Issue 今日仍有新评论：工具调用被切分并重复执行，影响 LM-Studio 等本地推理用户。 |

链接：
- https://github.com/NousResearch/hermes-agent/issues/39691
- https://github.com/NousResearch/hermes-agent/issues/59224
- https://github.com/NousResearch/hermes-agent/issues/39534
- https://github.com/NousResearch/hermes-agent/issues/5254

### 分析

社区当前最关注的是 **会话管理可见性** 和 **中文/非ASCII文本支持**。前者反映了多端协同使用的增长（CLI + Desktop + WebUI），后者则与国际化用户（尤其东亚）的日常体验直接相关。此外，对上下文压缩的优化提议（#39691）获得高赞，表明高级用户对 Token 经济性有较高期待。

---

## 5. Bug 与稳定性

### 今日新报 Bug（按严重程度排列）

| 严重度 | Issue | 标题 | 已有 Fix PR？ | 备注 |
|--------|-------|------|---------------|------|
| **P2** | [#61220] | Session expiry finalization doesn't set end_reason — stale recovery reopens expired sessions | ❌ | 会话过期后未正确标记结束原因，导致历史会话被误恢复，可能引发状态混乱。 |
| **P2** | [#61207] | /plan doesn't write a plan file anymore | ❌ | `/plan` 命令不再生成 `plan.md` 文件，功能退化。需确认是否为回归。 |
| **P2** | [#61195] | credential pool overrides explicit delegation.base_url | ❌ | 委托配置中的 `base_url` 被凭据池覆盖，导致子代理路由错误。（已有修复 PR #61258） |
| **P2** | [#61211] | WeCom file upload fails due to percent-encoded filename exceeding MAX_PATH | ❌ | Windows 下中文文件名经百分号编码后路径超长，导致文件无法缓存。已有对应修复 PR #61253。 |
| **P2** | [#61087] | Desktop app does not stop gateway on quit (macOS) | ✨**已关闭** | 已在 v0.18.2 中修复。 |
| **P3** | [#61191] | Desktop Composer persists stale attachments across conversations | ❌ | 附件缓存未随会话切换清空，可能展示其他会话的文件。 |
| **P3** | [#61048] | Kanban worker ignores fallback_providers | ❌ | Kanban 工作器未调用主 agent 的回退逻辑，导致异常时无模型可用。 |

### 值得关注的已关闭 Bug

- **[#28260] custom_providers with self-signed HTTPS fail** — 今日关闭，验证后确认已通过配置修复。
- **[#60715] Nous inference API completely unreachable** — 用户报告全网超时，后续确认是环境 DNS 问题，非项目 Bug。

---

## 6. 功能请求与路线图信号

### 高价值功能请求（结合已有 PR 分析）

| Issue | 标题 | 用户诉求 | 对应 PR 或路线图信号 |
|-------|------|----------|----------------------|
| [#61246] | Minimize to system tray on close | Windows 用户希望关闭窗口时最小化到托盘而非退出 | 无现有 PR，但需求简单（托盘图标），可能被低优先级接受。 |
| [#53617] | Keep reasoning panel expanded instead of auto-collapsing | 使用思考模型时，期望推理面板保持展开以查看完整过程 | 无直接 PR，但类似 #61257 的 PR 添加了工具调用默认展开选项，显示团队正在优化显示偏好。 |
| [#50718] | Session visibility: unread markers, needs-input cues, OS badges | 多会话场景下缺少未读标记和需输入提示，导致用户遗漏消息 | 无合并 PR，但类似 #60994 的命令中心安全中继工作包涉及会话状态，部分需求可能被覆盖。 |
| [#18241] | TUI: show thinking blocks and tool calls in chronological order | 推理模型交替思考与工具调用时，TUI 按类型分组丢失时序信息 | 无直接 PR，但 #61257 显示团队开始接受显示偏好类功能，该需求获 4 赞，有一定呼声。 |

### 可能纳入下一版本的功能迹象

- **桌面端显示偏好优化**：今日提交的 PR [#61257]（展开工具调用）和 PR [#61240]（Memoize 消息分组）表明团队正在积极改善桌面 UI 灵活性和性能。
- **iMessage 网关**：PR [#61250] 新增 Blooio 作为 iMessage 网关平台，若合并将扩展第三方消息渠道。
- **Agent Client Protocol 支持**：Issue [#569] 获得 9 赞，要求支持 ACP 协议以在 Zed/Neovim 等编辑器中集成。维护者在评论中表示“已在路线图规划中”，预计未来版本会落地。

---

## 7. 用户反馈摘要

从今日活跃 Issues 的评论中提炼出以下真实痛点：

- **“Tool calls are fragmented into dozens of separate calls”**（#5254）  
  用户 @micuentadecasa 在使用 LM-Studio + Gemma 4 时遇到工具调用被切分成数十个片段，与 Codex 的已知 bug 类似，严重阻碍本地模型使用。
- **“我输入的中文被截断了”**（#39534）  
  用户 @LiJT 在升级 v0.15.1 后，Windows 桌面版 chat 窗口对中文输入出现截断，反馈“太奇怪了”，并附上截图。多位中文用户跟帖确认。
- **“Desktop composer persists stale file attachments across conversations”**（#61191）  
  用户 @corvofiox 发现桌面端 composer 附件区会永久缓存之前的文件引用，换会话后仍显示，导致误会。
- **“/plan doesn't write a plan file anymore”**（#61207）  
  用户 @fafato1 报告 `/plan` 命令功能退化，猜测是近期重构引起，影响规划技能的正常使用。

### 正面反馈
- 中文用户 @1580812240 在 WeCom 上传文件报错后，提交了修复 PR #61253，表达对 Quick Fix 的期待。
- @Razultull 在 #50718 中详细描述了会话可见性的三个子问题，获得了维护者的认可回应“we should address these in 0.19”。

---

## 8. 待处理积压

以下为长期未响应或停留时间过长的关键 Issue/PR，建议项目维护者优先关注：

### Issues

| Issue | 创建时间 | 最后更新 | 类型 | 备注 |
|-------|----------|----------|------|------|
| [#5254] Tool calls repeating when using LM-Studio | 2026-04-05 | 2026-07-09 | Bug P2 | 已有 3 个月，用户持续反馈，影响本地模型类用户，需定位。 |
| [#569] ACP Server Mode | 2026-03-07 | 2026-07-08 | Feature | 高赞（9👍），虽已回应“在路线图”，但未有关联 PR，社区期待具体进展。 |
| [#18241] TUI chronological order for thinking blocks & tool calls | 2026-05-01 | 2026-07-09 | Feature P3 | 4👍，评论 2，暂无行动，可考虑纳入 0.19 看板。 |

### Pull Requests

| PR | 创建时间 | 最后更新 | 类型 | 备注 |
|----|----------|----------|------|------|
| [#39754] fix(plugins): update hindsight embedded dependency | 2026-06-05 | 2026-07-09 | Bug P3 | 1 个月未合并，依赖问题影响可选功能“Hindsight”嵌入模式。 |
| [#58023] fix: keep shell fences rendered as code blocks | 2026-07-04 | 2026-07-09 | Bug P3 | 已获 Approve，等待合并。 |
| [#53118] fix(desktop): stage esbuild binary when ignore-scripts=true | 2026-06-26 | 2026-07-09 | Bug P2 | 影响在 `ignore-scripts` 环境下构建桌面版，对 CI 和部分用户构成障碍。 |

---

**日报生成时间**：2026-07-09  
**数据来源**：Hermes Agent GitHub 仓库 (NousResearch/hermes-agent)  
**分析师**：AI 智能体与开源项目分析系统

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*