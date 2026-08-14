# OpenClaw 生态日报 2026-08-14

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-08-14 01:29 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目日报 — 2026-08-14

## 今日速览

过去 24 小时项目活跃度极高：共产生 **500 条 Issue 更新**（新开/活跃 338，关闭 162）与 **500 条 PR 更新**（待合并 386，合并/关闭 114），无新版本发布。社区讨论热度集中在**消息投递可靠性**与**子代理/session 状态一致性**相关的核心缺陷上，其中 #121058 单日评论达 92 条，为近期最热议题。整体来看，项目处于**高速迭代阶段**，但稳定性问题积压明显——大量 P1 级 Bug 长期未修复，且多数带有 `clawsweeper:no-new-fix-pr` 标签，提示维护者带宽或优先级分配存在瓶颈。

---

## 版本发布

过去 24 小时无新版本发布。

---

## 项目进展

过去 24 小时共有 **114 个 PR 被合并/关闭**，在以下方向有可见推进：

### 1. 渠道稳定性修复（微信、iMessage、LINE）
- **[PR #82540](https://github.com/openclaw/openclaw/pull/82540)** `fix(wechat): preserve existing accounts across hot reload` — 修复微信渠道热重载时账户丢失问题，避免已有 live 账户被意外清除。该 PR 规模为 XL，标注了兼容性/消息投递/可用性三类 merge-risk，仍处于 `needs proof` 状态。
- **[PR #123159](https://github.com/openclaw/openclaw/pull/123159)** `fix(imessage): honor bound routes before agent selection` — 修复多智能体配置下 iMessage 用户收到 `AGENT_SELECTION_REQUIRED` 的错误提示，即使运行时已存在权威的会话绑定。维护者发起，规模 M。
- **[PR #110058](https://github.com/openclaw/openclaw/pull/110058)** `fix(line): migrate pre-drain spool rows to the canonical queue contract on upgrade` — 修复 LINE 渠道升级回归：预 drain 构建已确认入队的消息在升级后被 dead-letter 而非投递。规模 XL，等待维护者审阅。

### 2. 核心稳定性（session 状态、备份、更新）
- **[PR #123192](https://github.com/openclaw/openclaw/pull/123192)** `fix(gateway): sessions stuck showing a phantom active run until restart` — 修复 Control UI 中会话永久显示"运行中"的虚假状态，实际 turn 早已结束，该卡死状态直到网关重启才消失。维护者 `steipete` 提交，规模 S。
- **[PR #116677](https://github.com/openclaw/openclaw/pull/116677)** `fix(backup): reclaim archive temps left by an interrupted backup` — 修复 `backup create` 被硬杀（SIGKILL/OOM/重启）后遗留临时目录的问题，对应 Issue #95582。状态为 waiting on author。
- **[PR #123197](https://github.com/openclaw/openclaw/pull/123197)** `fix(update): skip unrelated enclosing git roots` — 修复更新器在 nvm 等版本管理器目录下无法正确发现 OpenClaw 包根目录的问题。

### 3. 安全与边界加固
- **[PR #110716](https://github.com/openclaw/openclaw/pull/110716)** `fix(openshell): bound sandbox readFile with size cap` — 为 openshell 沙箱的 `readFile` 增加大小上限，防止沙箱进程请求读取多 GB 文件导致 OOM。
- **[PR #123194](https://github.com/openclaw/openclaw/pull/123194)** `fix(mcp): cap HTTP/SSE response bodies before SDK parse` — 在 MCP SDK 解析前对 HTTP/SSE 响应体设置上限，避免超大 JSON 在 Gateway 事件循环上分配数十 MB 内存导致心跳停滞。

### 4. 模型兼容性
- **[PR #113462](https://github.com/openclaw/openclaw/pull/113462)** `fix(moonshot): type anyOf branches so Kimi accepts MCP tool schemas` — 修复 Kimi 模型因 Moonshot 严格 JSON Schema 校验（要求 `anyOf` 每个分支声明 `type`）而拒绝 MCP 工具调用的问题。

### 5. Tool 调用可靠性
- **[PR #122513](https://github.com/openclaw/openclaw/pull/122513)** `fix(tool-call-repair): stop re-parsing the whole response per candidate delta` — 修复长输出场景下 tool-call-repair 反复解析整个响应导致 agent 卡顿数秒的问题。

---

## 社区热点

### 🔥 最热 Issue：#121058 — 静默回复失败持续复发（92 评论）
**[Issue #121058](https://github.com/openclaw/openclaw/issues/121058)** — `Silent reply failures still recurring after #116277 closed — no queued reply payload`（作者: sloptop-the-terrible）

- **背景**：#116277 已被关闭，但静默回复失败（监控 cron 持续记录到新发生，包括报告当天）。用户强烈表达了对问题未真正解决的质疑。
- **分析**：这是目前社区最集中的痛点——**回复静默丢失**，且用户已对 "closed but not fixed" 的模式表达了明显的不信任感。该 Issue 虽然评论高达 92 条，但 👍 数为 0，反映大量讨论可能夹杂了抱怨与复现信息而非实际赞同。本项目日报建议维护者优先核实其状态，避免 issue 关闭后问题仍在生产环境复现。

### 高讨论量：内存信任标签（48 评论）与工具调用文本泄漏（48 评论）
- **[Issue #7707](https://github.com/openclaw/openclaw/issues/7707)** — `Feature Request: Memory Trust Tagging by Source`（作者: LumenLantern，2026-02-03 创建）
  提出按来源（用户命令/网页抓取/第三方技能）标记记忆条目的信任级别，防止记忆投毒攻击。该 issue 已存在半年以上，带有 `needs-product-decision`、`needs-security-review` 等多个标签，仍无 fix PR。
- **[Issue #25592](https://github.com/openclaw/openclaw/issues/25592)** — `Text between tool calls leaks to messaging channels`（作者: doomclaw，P1）
  工具调用之间的内部处理文本（错误处理、进度叙述）被错误路由到 Slack/iMessage 等活跃消息渠道，造成 UX 污染。该问题影响面广，已关联 PR。

### 反向信号：用户对修复信心的流失
多个高热度 issue（如 #121058、#121605）中出现了 "closed but not fixed" 的质疑模式。用户对 `clawsweeper:no-new-fix-pr` 标签泛滥的不满正在积累，建议维护者重新审视 issue 关闭流程的严谨性。

---

## Bug 与稳定性

过去 24 小时共有 **162 个 Issue 被关闭**，但大量 P1 级 Bug 仍处于开放状态。以下按严重程度排列：

### 🔴 严重（P1，影响消息投递/数据安全）

| Issue | 问题描述 | 状态 | Fix PR |
|-------|---------|------|--------|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | 工具调用间的中间文本泄漏到 IM 渠道（P1, diamond lobster） | 开放，需产品决策 | 有链接 PR |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | 子代理完成静默丢失——无重试、无通知、超时无自动重启（P1, silver shellfish） | 开放 5 个月 | 无 |
| [#121953](https://github.com/openclaw/openclaw/issues/121953) | Cron agent 在 DeepSeek 上停摆：`[cron:...]` 前缀导致请求被边缘节点降优先级（P1） | 开放 3 天 | 有链接 PR |
| [#43367](https://github.com/openclaw/openclaw/issues/43367) | 多智能体编排不稳定：并发 add/config 覆盖、session-lock 失败、子工作分离（P1） | 开放 5 个月 | 无 |
| [#67777](https://github.com/openclaw/openclaw/issues/67777) | 子代理完成投递在超时/排空/孤儿清理时可能丢失（P1） | 开放，更新于今日 | 无 |
| [#92433](https://github.com/openclaw/openclaw/issues/92433) | 子代理完成被 steering 到已结束的运行时静默丢弃（P1） | 开放 | 无 |
| [#91363](https://github.com/openclaw/openclaw/issues/91363) | Isolated cron 持续报 "LLM request failed"，模型请求从未到达 provider（P1, 👍 6） | 开放 | 无 |
| [#41165](https://github.com/openclaw/openclaw/issues/41165) | Telegram DM 仍可落入 main session，污染 heartbeat 主会话（P1, diamond lobster） | 开放 5 个月 | 有链接 PR |
| [#89278](https://github.com/openclaw/openclaw/issues/89278) | Codex OAuth 刷新成功但 cron/heartbeat 触发 10s 超时（P1, platinum hermit） | 开放 | 无 |
| [#97983](https://github.com/openclaw/openclaw/issues/97983) | iOS/WebChat 消息进入 transcript 但不触发/投递助手回复（P1, diamond lobster, 👍 2） | 开放 | 无 |

### 🟠 中等（P2，影响体验/长期稳定性）

- [#43747](https://github.com/openclaw/openclaw/issues/43747) — 内存管理混乱：3 人使用同一工具却出现完全不同的 memory 行为（chunking/embedding vs raw 存储）（P2, platinum hermit）
- [#114612](https://github.com/openclaw/openclaw/issues/114612) — memory-core 的 SQLite 无保留策略，`memory_index_chunks` 等表无限增长将填满磁盘（P2, diamond lobster）
- [#97616](https://github.com/openclaw/openclaw/issues/97616) — 子进程泄漏导致 zombie 积累与运行时退化（P2 但标记 regression）
- [#95553](https://github.com/openclaw/openclaw/issues/95553) — preflight 压缩被硬编码 ~60s 上限，忽略 `compaction.timeoutSeconds`（P1）
- [#78493](https://github.com/openclaw/openclaw/issues/78493) — `sudo openclaw update` 导致文件所有权混合，doctor 随后覆盖配置（P1, diamond lobster, stable）

### 🟢 已有关闭或接近修复

- [#121605](https://github.com/openclaw/openclaw/issues/121605)（CLOSED）— Claude-CLI 回退后回复不投递（P1, diamond lobster），已关闭
- [#91456](https://github.com/openclaw/openclaw/issues/91456)（CLOSED）— Telegram DM 通道在发送超时后持续 guarded
- [#105342](https://github.com/openclaw/openclaw/issues/105342)（CLOSED）— exec 输出渲染为图片而非文本

---

## 功能请求与路线图信号

### 高优先级、可能纳入下版本

1. **[Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707)**（P2, 安全相关） — 按来源标记记忆条目信任级别。该 issue 已存活半年，带 `needs-product-decision` + `needs-security-review`。鉴于 AI 安全日益受重视，此功能符合大趋势，但缺乏维护者响应。
2. **[TTL/Expiry for Delivery Queue Messages](https://github.com/openclaw/openclaw/issues/16555)**（P1, 消息可靠性）— 为投递队列消息增加过期时间，防止网关重启后积压消息洪泛渠道。与当前大量消息投递问题直接相关，可能被纳入消息可靠性改进批次。
3. **[Pace-Aware Rate Limiting](https://github.com/openclaw/openclaw/issues/45771)**（P2）— 内置感知消耗速率的限流机制，防止自主循环烧穿 Anthropic 限额。针对 cron/subagent 场景，有实际需求支撑。
4. **[YAML 配置文件支持](https://github.com/openclaw/openclaw/issues/45758)**（P3, 👍 2）— 在 JSON5 之外支持 YAML 格式，降低 DevOps 用户的配置门槛。典型 DX 改进，成本可控。

### 平台扩展信号

5. **[Chat-first Android surface](https://github.com/openclaw/openclaw/issues/46058)**（P3）— 社区成员在询问维护者是否愿意接收一个安卓聊天优先客户端的 focused upstream。目前无明确回应，是潜在的生态扩展机会。
6. **[Self-hosted STT/TTS in webchat](https://github.com/openclaw/openclaw/issues/45508)**（P2, 👍 2）— 将 webchat 的语音输入/朗读路由到自托管网关 TTS/STT，而非浏览器 Web Speech API。

### 值得注意

- **[Durable natural-language rule learning](https://github.com/openclaw/openclaw/issues/41366)**（P3）— 持久化自然语言规则学习 + 多提及回复语义。
- **[Session resetPrompt](https://github.com/openclaw/openclaw/issues/45501)**（P2）— 可配置的 session 启动消息，有实际社区需求但非主线。

---

## 用户反馈摘要

### 用户痛点 top 3

1. **"关闭了但没修好"（#121058）** — 用户监控显示 #116277 关闭后问题仍在持续出现。这不是孤例：`closed but not fixed` 的模式在多条高热度 issue（#121605、#91456）中均有出现。这正在侵蚀社区对项目 issue 管理流程的信任。

2. **多智能体编排不可用** — [#43367](https://github.com/openclaw/openclaw/issues/43367) 用户报告 `openclaw agents add` 并发调用会覆盖配置；[#47975](https://github.com/openclaw/openclaw/issues/47975) 报告子代理会话完成后面主会话无响应，需手动重启。多代理在生产环境中的可靠性远未达标。

3. **内存管理一团糟** — [#43747](https://github.com/openclaw/openclaw/issues/43747) 中三位同事使用相同工具却出现完全不同的 memory 行为（有的 chunking+embedding，有的 raw 存储，还有的存到不同位置）。用户原话："Me and my colleague (3 people) are using openclaw. I never see any of our memory is managed in same way." 这反映了功能分支/配置默认值不一致的问题。

### 使用场景亮点

- **Telegram forum bot**（#44925）和 **Discord + WhatsApp**（#54488）是高频生产场景。
- **Browser automation 真实环境测试**（#44431，已关闭）中，用户跨 9+ 邮箱服务商做自动化注册，为浏览器工具提出了 7 条具体改进建议，包括 CSS 选择器支持、快照→Ref 工作流精简等。这说明浏览器自动化是真实且重要的使用场景。
- **Android 独立 fork 生态**（#46058）：有开发者基于 openclaw 构建 Android 聊天优先客户端，表明社区对移动端入口有自发

---

## 横向生态对比

> 说明：本次输入中仅 OpenClaw 有完整日报，Hermes Agent 摘要生成失败，无法获取当日数据。因此本报告以 OpenClaw 为实证主体，对 Hermes 仅作背景性标注，不作虚构量化对比。

## 1. 生态全景

个人 AI 助手与自主智能体开源生态仍处于高速迭代期，但“功能推进速度”与“生产可用性”之间的落差已成为核心矛盾。以 OpenClaw 为样本，单日 500 条 Issue/PR 更新、114 个 PR 被合并/关闭，说明社区供给能力很强；与此同时，消息投递静默失败、子代理状态丢失、多智能体编排不稳定等 P1 问题长期积压，用户开始出现“closed but not fixed”的信任流失。生态整体正从“演示可跑”转向“生产可扛”，多渠道、定时任务、多智能体协作等真实场景正在倒逼可靠性基础设施补齐。安全与记忆可信度也开始被作为产品级需求提出，而非单纯功能增强。

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release | 健康度评估 |
|---|---|---|---|---|
| OpenClaw | 500 条（新开/活跃 338，关闭 162） | 500 条（待合并 386，合并/关闭 114） | 无 | 高速迭代但稳定性承压：P1 积压、热帖质疑“关闭未修复”，维护者带宽存在瓶颈 |
| Hermes Agent | 数据缺失（摘要生成失败） | 数据缺失 | 未知 | 无法评估 |

## 3. OpenClaw 在生态中的定位

OpenClaw 是当前个人 AI 助手开源生态中的“核心参照项目”，其定位更接近 **AI 助手网关/运行时**，而非纯 agent 框架。

- **优势**：渠道覆盖广，包括微信、iMessage、LINE、Telegram、Discord、WhatsApp、WebChat 等；具备 gateway、session、backup、update、MCP 工具链等完整基础设施。
- **技术路线差异**：以“渠道接入 + 消息路由 + 子代理编排 + 工具调用可靠性”为骨架，强调多端一致性和生产环境可用性。
- **社区规模**：单日 500 条 Issue/PR 更新、热帖 92 条评论，说明反馈量和用户基数都很大；已出现 Android 独立 fork，显示生态开始外溢。
- **横向对比限制**：Hermes 当日数据缺失，无法量化比较。从项目归属看，Hermes 偏向研究型 agent 能力，OpenClaw 更偏向个人助理基础设施，二者赛道重叠但侧重点可能不同。

## 4. 共同关注的技术方向

由于只有 OpenClaw 完整数据，无法可靠识别多项目共性。以下为 OpenClaw 社区内部高频涌现的技术主题，可作为后续跨项目对比的候选维度：

- **消息投递可靠性**：静默回复丢失、队列无 payload、TTL/过期机制、dead-letter 问题。
- **子代理与 session 状态一致性**：子代理完成静默丢失、session 卡死显示“运行中”、完成后主会话无响应。
- **内存机制的可信与可控**：按来源标记信任级别、SQLite 无限增长、多用户 memory 行为不一致。
- **安全边界加固**：沙箱 readFile 大小上限、MCP HTTP/SSE 响应体上限、OAuth 超时问题。
- **模型生态适配成本**：Kimi/Moonshot schema 校验、DeepSeek cron 前缀降优先级、Claude-CLI 回退投递失败。
- **移动与语音入口**：Android 聊天优先客户端、自托管 STT/TTS。

涉及项目：当前仅确认 OpenClaw；Hermes 是否同样受这些问题困扰，需要补充数据。

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
|---|---|---|
| 功能侧重 | 多渠道个人 AI 助手网关，消息投递、session、子代理、MCP 工具链 | 未知（本次无数据） |
| 目标用户 | 自托管用户、IM 机器人运维者、多智能体团队 | 未知 |
| 技术架构 | gateway 路由 + 渠道适配 + cron/subagent + tool-call repair | 未知 |
| 社区模式 | Issue/PR 驱动，社区 fork 生态已出现 | 未知 |
| 背景判断 | 个人助理基础设施，强调真实场景落地 | Nous Research 旗下，可能更偏向 agent 能力研究与前沿模型集成 |

结论：OpenClaw 的差异化在于 **“渠道密度 + 生产级消息可靠性”**；Hermes 的差异化暂无法从当日数据判断。

## 6. 社区热度与成熟度

- **OpenClaw：快速迭代期，但质量巩固不足。**
  - 热度：极高。单日 500 条 Issue/PR 更新，114 个 PR 被合并/关闭。
  - 成熟度：功能迭代速度大于稳定性修复速度。大量 P1 级消息/子代理 Bug 开放超过 3-5 个月，且带有 `clawsweeper:no-new-fix-pr` 标签。
  - 用户信任风险：多个高热度 issue 出现“关闭了但没修好”的质疑，说明 issue 关闭流程与实际修复效果之间存在脱节。

- **Hermes Agent：无法分层。**
  - 因摘要生成失败，无法判断处于快速迭代还是质量巩固阶段。

## 7. 值得关注的趋势信号

1. **可靠性已成为社区第一诉求**  
   #121058 静默回复失败单日 92 条评论，#25592 文本泄漏到 IM 渠道，说明用户最痛的不是“功能不够”，而是“消息不可靠”。  
   *对开发者：优先建立投递确认、重试、幂等、可观测性，再叠加新功能。*

2. **多

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ 摘要生成失败。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*