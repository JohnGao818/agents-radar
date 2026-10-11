# OpenClaw 生态日报 2026-10-11

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-10-11 03:41 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

⚠️ 摘要生成失败。

---

## 横向生态对比

# 2026-10-11 个人 AI 助手 / 自主智能体开源生态横向对比报告

> **数据完整性声明**：OpenClaw 今日摘要生成失败，缺失 Issues、PR、Release、贡献者等量化数据。以下报告以 **Hermes Agent** 为唯一完整样本；OpenClaw 仅作“核心参照”的定性占位，不参与数值排名，避免虚构推断。

---

## 1. 生态全景

在可观测范围内，个人 AI 助手/自主智能体开源生态正进入 **“长会话可靠性 + 多 surface 一致性”** 的工程深水区。  
Hermes Agent 单日 50 条 Issue 更新、50 条 PR 更新，但 PR 合并率不足 6%，显示需求与讨论旺盛，维护带宽成为明显瓶颈。  
上下文压缩、推理回放、跨平台会话记忆、静默失败是当前最集中的问题簇。  
社区信任正受到两类问题侵蚀：**“看起来正常但实际没做事”的静默失败**，以及 **Agent 工具自描述与实际 schema 不一致**。  
OpenClaw 数据缺失，今日无法形成完整生态横截面。

---

## 2. 各项目活跃度对比

| 项目 | 今日 Issue 更新 | 今日 PR 更新 | Release | 合并/关闭情况 | 健康度评估 |
|---|---:|---:|---:|---|---|
| **OpenClaw** | 摘要失败，不可得 | 不可得 | 不可得 | 不可得 | **不可评估** |
| **Hermes Agent** | 50 条

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 · 2026-10-11

---

## 1. 今日速览

今日项目维持**高强度社区活动但低吞吐**的状态：24 小时内 50 条 Issue 更新（42 新开/活跃、仅 8 关闭）、50 条 PR 更新（47 待合并、仅 3 合并/关闭），合并率不足 6%，待审队列持续膨胀。**上下文压缩（compression）与 Desktop 渲染重复**构成本日两大问题簇，前者同时引发数据损坏、错误阈值、工具参数污染三类故障，后者已出现至少三个独立复现报告（#129993 / #129731 / #136335），高度指向同一根因。零版本发布，且多名长期贡献者（如 33hodl）的修复 PR 已积压逾 7 周未合入，维护侧带宽是当前最明显的瓶颈。整体健康度评级：**功能迭代活跃，合并管道受阻（黄色预警）**。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日合并/关闭量偏低，主要进展体现在**关闭确认类**与**关键修复落地的信号**：

| 条目 | 类型 | 意义 |
|---|---|---|
| [#56004](https://github.com/NousResearch/hermes-agent/issues/56004) Closed | 推理链路 | 思考模型在 OpenAI 兼容端点回放时丢失自身推理内容（7 👍，14 评论）已关闭，是本日**社区呼声最高的修复落地信号** |
| [#122303](https://github.com/NousResearch/hermes-agent/issues/122303) Closed | 提供商兼容 | Kimi 系模型经 OpenRouter 丢失 `reasoning_content` 连续性问题关闭，与 #56004 同属"推理回放"问题域，显示该方向已被系统性清理 |
| [#122190](https://github.com/NousResearch/hermes-agent/issues/122190) Closed | Desktop/Win | Windows 桌面端 profile 切换后会话被静默 `hidden=1` 问题关闭 |
| [#136340](https://github.com/NousResearch/hermes-agent/issues/136340) Closed (invalid) | 自动续跑 | goal 在 server_error 自动恢复后停留 paused，被判为无效 |

**推进方向判断**：项目正在收敛"多提供商推理连续性"这一长期顽疾（#56004 + #122303 同日关闭），对长会话可靠性是实质性改善。但 PR 侧几乎停滞——#136426（execute_code stdin EOF 修复，teknium1 亲自 salvage #123560）与 #106742（"单一 gateway 拥有所有本地会话"的 P1 架构级 PR）仍处 OPEN，后者若合入将显著改变 CLI/TUI/Desktop/ACP/bots 的会话模型。

**整体前进幅度**：约 0.5 个迭代单位——问题清理有进展，交付管道基本冻结。

---

## 4. 社区热点

**① #131859 — 唯一"被阻塞"的元问题（25 评论，全场最高）**
[Issue #131859](https://github.com/NousResearch/hermes-agent/issues/131859) · `[P2, blocked, area/auth]`
贡献者 kuehnberger 无法通过 API 对该仓库创建 PR，而 issue 创建与 fork PR 仍正常。25 条评论说明这不只是个人问题——**贡献者在为项目做贡献的路上被挡在门外**，且被标记 `blocked`，属于典型的"流程阻塞开发"型问题，优先级应被视为高于其 P2 标签。

**② #124583 / #123345 — 终端工具的"文档与实现不一致"双联**
[#124583](https://github.com/NousResearch/hermes-agent/issues/124583)（17 评论）：background hint 指引用户调用不存在的工具名 `process(action=...)`，实际为 `process_manage`。
[#123345](https://github.com/NousResearch/hermes-agent/issues/123345)：`notify=true` 布尔值被校验器拒绝。
**诉求本质**：Agent 的**自我描述不可信**——提示文本指向不存在的工具、schema 与校验器打架。对以"Agent 自主调用工具"为核心的产品，这类问题的隐性成本极高（Agent 会按提示自我误导）。

**③ #103410 — TUI 热重载崩溃（14 评论，1 👍）**
[Issue #103410](https://github.com/NousResearch/hermes-agent/issues/103410) · LCMEngine 缺少 `_coerce_threshold_tokens_cap`，每次配置变更即告警。与 #136350 的阈值解析错误共享同一压缩配置子系统。

**④ #133856 — 高共鸣认证问题（5 👍，为今日 Issue 最高点赞）**
[Issue #133856](https://github.com/NousResearch/hermes-agent/issues/133856) · `sk-ant-usr-` 前缀的 Anthropic API Key 被误判为 OAuth token，导致**按量付费 Key 被当作 Claude Code 身份使用**——直接影响计费与限额，是今日最需紧急处理的 P1。

**⑤ PR 侧静默积压**
多数高评论数 PR 评论区显示 `undefined`，说明**审核互动极少**，PR 处于"挂着没人看"的状态，与 Issue 侧的热烈讨论形成鲜明反差。

---

## 5. Bug 与稳定性

### 🔴 P1 — 需当日处理

| 问题 | 说明 | Fix PR |
|---|---|---|
| [#133856](https://github.com/NousResearch/hermes-agent/issues/133856) | Anthropic `sk-ant-usr-` Key 被误判为 OAuth，按量付费 Key 走 Claude Code 身份路径，影响计费与配额 | 未见 |

### 🟠 P2 — 数据损坏与静默失败（今日问题最密集区）

| 问题 | 影响 | Fix PR |
|---|---|---|
| [#136349](https://github.com/NousResearch/hermes-agent/issues/136349) | **压缩标记 `⟪HERMES-CONTEXT-COMPRESSION...⟫` 泄漏进 Agent 写入的文件**，造成实质性数据污染 | 未见 |
| [#127260](https://github.com/NousResearch/hermes-agent/issues/127260) | 上下文压缩**在途破坏工具调用参数**（截断 + token 插入 + Windows git-bash BOM 不稳定） | 未见 |
| [#136350](https://github.com/NousResearch/hermes-agent/issues/136350) | `compression.threshold_tokens` 解析为 256000 而非按文档的 null 语义（1M 窗口 + 0.5 ⇒ 应 512k），77 分钟会话触发 **7–8 次压缩**，反复丢失实时上下文 | 未见 |
| [#136412](https://github.com/NousResearch/hermes-agent/issues/136412) | Telegram 网关：per-path 连接预算 ≥ 整发截止时间 + 连接阶段超时被误判为不可重试 ⇒ **静默投递丢失**（日志显示已发送，实际未达） | 未见 |
| [#108967](https://github.com/NousResearch/hermes-agent/issues/108967) | `GET /v1/skills` 恒返 500（`include_editorial` 关键字已被移除但调用方未更新，TypeError 被宽泛 except 吞掉） | 未见 |
| [#94928](https://github.com/NousResearch/hermes-agent/issues/94928) | Desktop/Linux 运行一段时间后 `terminal`/`read_file` 恒返空输出（pipe fd 超过 FD_SETSIZE，stdout/stderr 被丢弃） | 未见 |
| [#54572](https://github.com/NousResearch/hermes-agent/issues/54572) | `patch` 工具 replace 模式在 9 级模糊匹配链下**可能改错区域** | 未见 |
| [#131859](https://github.com/NousResearch/hermes-agent/issues/131859) | 无法通过 API 创建 PR（`blocked`）——阻塞外部贡献 | 未见 |

### 🟡 P3 — 体验与状态一致性

- [#129993](https://github.com/NousResearch/hermes-agent/issues/129993) / [#129731](https://github.com/NousResearch/hermes-agent/issues/129731) / [#136335](https://github.com/NousResearch/hermes-agent/issues/136335)：**Desktop 助手回复重复渲染**（DB 只有一行，UI 渲染两次）。三份独立报告，分别指向流式渲染、stale inflight-turn journal 重折叠等方向，**极可能是同一根因的多面表现，建议合并处理**。
- [#119190](https://github.com/NousResearch/hermes-agent/issues/119190)：图片轮次中注入的记忆/`pre_llm_call` 上下文被显示为用户自己的话。
- [#124010](https://github.com/NousResearch/hermes-agent/issues/124010)：Photon sidecar 僵尸流看门狗每 10 分钟重启健康的安静专线。
- [#120016](https://github.com/NousResearch/hermes-agent/issues/120016)、[#134712](https://github.com/NousResearch/hermes-agent/issues/134712)、[#59764](https://github.com/NousResearch/hermes-agent/issues/59764)：状态/配置漂移类问题。

### ⚫ 平台特定静默失败

- [#136390](https://github.com/NousResearch/hermes-agent/issues/136390)：Windows `pm`/Python 3.14 运行时下计划任务登录自启**报告成功但实际不启动**（`Last Result = 0`），完全静默。
- [#136413](https://github.com/NousResearch/hermes-agent/issues/136413)：OpenCode Go 的 `-free` 后缀模型被误路由到匿名 Zen 端点，401。

> **风险提示**：本日最严重的问题类别是**"静默失败"**——Telegram 投递、Windows 自启、Desktop 空输出、500 被 except 吞掉，四类问题都表现为"看起来正常但实际没做事"，对用户信任的侵蚀远大于显式报错。

---

## 6. 功能请求与路线图信号

| 需求 | Issue | 关联 PR / 落点判断 |
|---|---|---|
| **跨平台会话组 + 会话键重映射**：Discord 与 Telegram 共享同一 agent 记忆 | [#79198](https://github.com/NousResearch/hermes-agent/issues/79198) | 与 [#106742](https://github.com/NousResearch/hermes-agent/pull/106742)（单一 gateway 拥有所有本地会话）**方向同源**，后者是 P1 架构级 PR。该需求落地的技术底座正在成型，**下一版本纳入概率较高** |
| **MEMORY.md / USER.md 写入时预算与准入流水线** | [#135039](https://github.com/NousResearch/hermes-agent/issues/135039) | 标记 `needs-decision`。论述有力（记忆注入每个后续轮次，属持续性成本），但需产品决策。短期偏"讨论项" |
| **会话关闭而不删除**（当前只能 delete 或 archive，无法释放并发槽位） | [#75489](https://github.com/NousResearch/hermes-agent/issues/75489) | 无对应 PR，属清晰、低争议的体验缺口，**具备被顺手纳入的条件** |
| **Desktop 新会话空态开放给插件（贡献式欢迎区）** | [#108533](https://github.com/NousResearch/hermes-agent/issues/108533) | 扩展性诉求，暂无 PR |
| **Codex 原生 Goal 接管（长任务免"继续"）** | PR [#134539](https://github.com/NousResearch/hermes-agent/pull/134539) | 已有实现，opt-in 设计，若审核通过可能进下一版本 |

**路线图推断**：项目正从"多 surface 各自持有会话"向"单一 gateway 统一会话所有权"演进（#106742），#79198 的跨平台记忆诉求会在该底座就位后自然获得支持。记忆治理（#135039）是下一个需要产品层表态的议题。

---

## 7. 用户反馈摘要

**痛点一：长会话不可靠（最高频）**
用户不约而同地描述同一种体验——会话变长后开始"自己坏掉"：#136350 报告 77 分钟内压缩 7–8 次；#127260 描述工具参数在压缩中被污染；#136349 发现压缩标记写进了文件。一位用户（#56004）甚至明确表示"我选择提 Issue 而不是提 PR，因为审核一份陌生人的代码比审核一份报告更费劲"——这既是善意，也暗示**外部代码贡献的门槛感知偏高**，与 #131859 的 `blocked` 状态互相印证。

**痛点二：Agent 的自我描述不可信**
#124583（提示指向不存在工具名）和 #123345（schema 与校验器矛盾）来自同一位用户 Ethan-Vex 在两天内分别提交，说明其正在系统性地测试"Agent 按自身提示操作能否走通"——而答案是走不通。

**痛点三：静默无反馈**
#120016 用户抱怨版本落后计数是 24 小时缓存却在 UI 上伪装成实时，"唯一刷新方式是点那个 pill"；#136390 用户遇到计划任务报成功但不启动；#136412 用户遇到消息日志说已发送但对方收不到。**"我知道出了问题"和"我完全不知道出了问题"之间的差距，是当前最伤用户信任的一环。**

**正面信号**
#56004 与 #122303 同日关闭，说明推理连续性问题（过去数月最影响长会话体验的一类）已进入收尾阶段；provider 层问题被逐个清理，说明多提供商矩阵的成熟度在提升。

---

## 8. 待处理积压

### ⚠️ 长期未合入的高质量修复 PR（贡献者 33hodl，均为 8 月创建，已积压 ~7–8 周）

| PR | 主题 | 创建日 |
|---|---|---|
| [#89008](https://github.com/NousResearch/hermes-agent/pull/89008) | gateway：更新进程无退出码时快速失败（当前会轮询 30 分钟） | 2026-08-18 |
| [#89009](https://github.com/NousResearch/hermes-agent/pull/89009) | gateway：在独立 systemd transient unit 中启动更新器 | 2026-08-18 |
| [#92127](https://github.com/NousResearch/hermes-agent/pull/92127) | checkpoints：从 shadow store 的陈旧 git lock 中恢复 | 2026-08-22 |
| [#92829](https://github.com/NousResearch/hermes-agent/pull/92829) | desktop：打开非活跃 profile 会话后未读点不消失 | 2026-08-23 |
| [#94302](https://github.com/NousResearch/hermes-agent/pull/94302) | file-sync：跳过权限拒绝的文件而非卡死整个同步周期 | 2026-08-24 |

**这是一条完整的"健壮性修复流水线"**：更新器生命周期、checkpoint 锁恢复、file-sync 权限容错、Desktop 状态一致性。每一条都对应真实故障场景，且描述清晰、含复现。**积压 7 周以上的 PR 队列是当前项目健康度最大的隐性负债**——若不及时处理，很可能导致核心贡献者流失。

### 📌 长期未响应的功能性 Issue

- [#75489](https://github.com/NousResearch/hermes-agent/issues/75489)（2026-07-31）会话无法关闭——低争议、低复杂度、长期无人

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*