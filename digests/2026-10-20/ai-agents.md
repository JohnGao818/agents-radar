# OpenClaw 生态日报 2026-10-20

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-10-20 03:11 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

⚠️ 摘要生成失败。

---

## 横向生态对比

**数据边界**：OpenClaw 今日摘要生成失败，Issues/PR/Release 与健康度均不可得。以下横向对比以 Hermes Agent 为唯一可观测样本；OpenClaw 仅作参照定位，不做定量推断。

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态当前处于“功能迭代与运行可靠性并重”的阶段。可观测样本 Hermes 显示社区输入旺盛但维护吞吐偏低：24 小时内 Issues、PR 各更新 50 条，净积压各约 +48，零发布。讨论焦点正从“能不能做”转向贡献通路、回合级时间感知、跨平台进程治理与工具调用可信度。OpenClaw 数据缺失，使跨项目定量对比和“共同趋势”确认受限。整体生态成熟度正受评审带宽、发版工程和桌面跨平台治理约束。

---

## 2. 各项目活跃度对比

| 项目 | 今日 Issues 更新 | 今日 PR 更新 | Release | 健康度评估 | 数据可信度 |
|---|---:|---:|---:|---|---|
| **OpenClaw** | 不可得（摘要失败） | 不可得 | 不可得 | 不可评估 | 缺失 |
| **Hermes Agent** | 50 条：49 新开/活跃，1 关闭 | 50 条：49 待合并，1 合并/关闭 | 0 | 社区活跃度 **A-**；维护吞吐 **C+**；长尾 PR 积压风险 | 高（基于摘要） |

**Hermes 关键信号**：关闭/合并率仅约 2%，净积压各增加约 48 条；无版本发布，处于修复与评审消化期。最接近交付的 PR 包括 stable 渠道升级修复 #141839、Kanban 跨 profile 环境白名单 #141809、Desktop 附件归属解析 #141810、Chromium 选择 #141817。外部贡献者 `yoyodine-industries` 的 14+ 个 PR 仍待合并，构成成体系但未打通的修复流水线。

---

## 3. OpenClaw 在生态中的定位

- **生态角色**：作为“核心参照”，OpenClaw 更可能承担基准实现与兼容锚点角色；但今日摘要失败，无法验证其活跃度、功能推进和社区规模。
- **优势判断**：无法基于今日数据确认。其潜在优势在于参照地位与生态兼容价值，但需补充 Issues/PR/Release 数据后复核。
- **技术路线差异**：Hermes 可观测到 gateway runtime、stable 渠道、Desktop Electron、Kanban worker、MoA reference、profile 隔离等具体方向；OpenClaw 今日技术路线不可得。
- **社区规模对比**：Hermes 今日 Issues/PR 各 50 条更新，热点 Issue 46 条评论、最高 9 👍；OpenClaw 无可比数据，**不能得出规模结论**。

**结论**：今日无法对 OpenClaw 与 Hermes 做可靠的定量优劣判断；OpenClaw 的定位分析应待数据恢复后补全。

---

## 4. 共同关注的技术方向

今日 OpenClaw 数据缺失，**无法确认“多项目共同涌现”**。以下为 Hermes 单项目高信号方向，建议作为跨项目观察候选：

| 方向 | Hermes 证据 | 涉及项目 | 行业含义 |
|---|---|---|---|
| 回合级实时时间感知 | #10421，24 评论 / 9 👍，`needs-decision` | Hermes；OpenClaw 待验证 | Agent 需稳定感知“现在/今天/星期几”，减少显式工具调用依赖 |
| 外部贡献通路与权限 | #131859，46 评论，`blocked` + `cause/upstream` | Hermes；OpenClaw 待验证 | 贡献者被 API 权限卡住近三周，直接损耗外部贡献意愿 |
| 跨平台进程与生命周期 | #126887 macOS `ps` 换行解析；#135344 `_pid_recycled` 指纹漂移；Kanban worker 误判 | Hermes；OpenClaw 待验证 | 无 `/proc` 平台需要更稳健的进程指纹与生命周期抽象 |
| 结构化工具调用真实性 | #139568：MoA reference 模型伪造 `[called tool]` / `[tool result]` | Hermes；OpenClaw 待验证 | 结构化幻觉会污染混合推理，需要工具调用校验/溯源 |
| 发版与升级通道稳定性 | #141839：stable 渠道被钉在 v0.22.2 | Hermes；OpenClaw 待验证 | 升级路径是用户可感知的可靠性，发版前必须验证 |
| 桌面端附件与浏览器配置 | #141810 附件 owner 解析；#141817 指定 Chromium | Hermes；OpenClaw 待验证 | 多后端、多浏览器环境下桌面体验仍是最佳实践缺口 |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
|---|---|---|
| **功能侧重** | 核心参照/基准实现；具体功能今日不可得 | Agent runtime + 桌面端 + Kanban 工作流 + MoA + 多 profile/浏览器配置 |
| **目标用户** | 生态集成者/核心参照用户（待验证） | 桌面用户、多后端/多 profile 用户、外部贡献者 |
| **技术架构** | 今日不可得 | gateway runtime、stable 渠道、Desktop Electron、Kanban workers、profile scope、MoA reference |
| **当前工程状态** | 不可评估 | 高流入、低吞吐；零发布；PR 长尾积压；平台稳定性热点集中 |

Hermes 的差异化更偏向“可运行的桌面级 Agent 工作台 + 多后端/工作流集成”；OpenClaw 的差异化需待数据恢复后判断。

---

## 6. 社区热度与成熟度

- **Hermes：快速迭代与质量巩固并存，但评审瓶颈明显。** 社区活跃度 A-，维护吞吐 C+；Issues/PR 各 50 条更新、关闭/合并率约 2%、零发布，说明需求与修复输入充足，但合并/关闭能力不足。平台稳定性三连（macOS `ps`、MoA 结构化幻觉、`_pid_recycled`）表明其正处于跨平台质量巩固阶段；stable 渠道升级阻塞则属于发版工程成熟度问题。
- **OpenClaw：不可评估。** 今日无数据，无法判断其处于快速迭代、质量巩固还是维护期。
- **分层判断**：Hermes 属于“活跃迭代 + 质量巩固混合层”，且存在长尾 PR 积压风险；OpenClaw 暂列“数据缺失层”。

---

## 7. 值得关注的趋势信号

1. **贡献者体验成为开源 Agent 基础设施瓶颈。** #131859 高热度且 `blocked` 近三周，说明权限/上游问题会直接阻断外部贡献；项目应建立贡献者 unblock SLA。
2. **Agent 时间感知从“工具调用”转向“运行时上下文”。** #10421 长期悬置但共识高，建议将 turn-level 时间作为默认上下文能力设计。
3. **跨平台进程治理是桌面 Agent 的隐性刚需。** macOS 无 `/proc` 导致 `ps` 解析、PID 指纹漂移、Kanban worker 误判，开发者应抽象跨平台进程指纹与生命周期层。
4. **结构化工具调用需要真实性校验。**

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报
**日期：2026-10-20 ｜ 数据窗口：过去 24 小时 ｜ 数据源：GitHub Issues / PRs / Releases**

---

## 1. 今日速览

今日项目维持**高流入、低吞吐**的运行状态：Issues 更新 50 条（49 条新开/活跃、1 条关闭），PR 更新 50 条（49 条待合并、仅 1 条合并/关闭），净积压各增加约 48 条，关闭/合并率仅 2%。**零版本发布**，说明当前处于修复与评审消化期而非交付期。社区讨论高度集中于两处：一是外部贡献者被 API 权限错误卡住近三周（[#131859](https://github.com/NousResearch/hermes-agent/issues/131859)，46 条评论），二是"回合级实时时间感知"这一高共鸣功能请求（[#10421](https://github.com/NousResearch/hermes-agent/issues/10421)，24 条评论 / 9 👍，为今日唯一显著点赞聚集）。缺陷侧呈现明显的**平台聚集性**：macOS 进程指纹与 ps 解析、Kanban worker 生命周期误判、桌面端 Electron CPU 失控构成三大稳定性热点。整体健康度评估：**社区活跃度良好（A-），维护吞吐与评审带宽偏紧（C+），存在长尾 PR 积压风险**。

---

## 2. 版本发布

今日无新版本发布（0 个），Latest Releases 为空。值得注意的信号是 PR [#141839](https://github.com/NousResearch/hermes-agent/pull/141839) 正在处理"网关运行时上的 stable 渠道安装被钉在 v0.22.2"的问题，涉及 #140729、#139099，并打捞 #140215、#140778 —— 表明 **v0.22.2 的升级路径存在用户可感知的阻塞**，但修复尚未落地，下一次发版前需重点验证。

---

## 3. 项目进展

今日仅 1 条 PR 合并/关闭，且未出现在按评论数展示的 Top 20 样本中，具体内容无法从本次数据确认；因此**今日没有可归因的显性功能推进**。从待合并队列看，最接近交付的实质工作有：

| PR | 内容 | 推进意义 |
|---|---|---|
| [#141839](https://github.com/NousResearch/hermes-agent/pull/141839) | stable 渠道不再被"降级"逻辑拒绝，`hermes update --check` 与 Desktop/Dashboard 停止推送 v0.22.2 | 直接解除升级路径卡死，属发版前必合并项 |
| [#141809](https://github.com/NousResearch/hermes-agent/pull/141809) | Kanban 跨 profile worker 启动改为白名单环境变量，`_worker_profile_scope` 去除 `bind_home=False` | 修复跨 profile 凭据/环境污染，安全面收益明确 |
| [#141810](https://github.com/NousResearch/hermes-agent/pull/141810) | Desktop 会话附件按 transcript owner 解析，贯穿下载/预览/编辑/缓存 | 修复多后端场景下"File not found"，桌面端可用性 |
| [#141817](https://github.com/NousResearch/hermes-agent/pull/141817) | `use_real_profile` 可选择具体 Chromium 浏览器而非 OS 默认 | 解决 Firefox/Zen 为默认浏览器用户的硬失败 |
| [#138820](https://github.com/NousResearch/hermes-agent/pull/138820) | Desktop Capabilities 目录（Skills/Plugins/Connectors/Tools）卡片化重设计 | 信息架构与主题一致性改进，体验层推进 |

**结构性观察**：贡献者 `yoyodine-industries` 自 9 月 16–21 日起提交的 14+ 个 PR（含 bot-delivery 4 层系列 [#115003](https://github.com/NousResearch/hermes-agent/pull/115003)、[#115009](https://github.com/NousResearch/hermes-agent/pull/115009)、[#115010](https://github.com/NousResearch/hermes-agent/pull/115010)、[#115013](https://github.com/NousResearch/hermes-agent/pull/115013)、[#115771](https://github.com/NousResearch/hermes-agent/pull/115771) 与 Kanban 系列 [#118281](https://github.com/NousResearch/hermes-agent/pull/118281)、[#118290](https://github.com/NousResearch/hermes-agent/pull/118290)、[#118421](https://github.com/NousResearch/hermes-agent/pull/118421)、[#118500](https://github.com/NousResearch/hermes-agent/pull/118500)、[#118546](https://github.com/NousResearch/hermes-agent/pull/118546)）全部仍在待合并状态，且多数带有 `sweeper:risk-*` 标记。这是一条**成体系但未被打通的修复流水线**，其停滞本身就构成项目最大的"未推进量"。

---

## 4. 社区热点

**① [#131859](https://github.com/NousResearch/hermes-agent/issues/131859) — 46 条评论，今日讨论绝对中心**
`type/bug, area/auth, P3, blocked, cause/upstream`。某外部贡献者账号无法通过 API 对上游仓库创建 PR（`CreatePullRequest` 权限错误），Issue 创建与 fork PR 仍正常，错误可稳定复现两次。自 2026-10-03 创建、至今未解，标签已标 `blocked` + `cause/upstream`。**诉求本质**：不是产品功能问题，而是**贡献通路被阻断**——对一个高速迭代的开源项目，这类问题会直接损耗外部贡献意愿，46 条评论的高热度说明多方在反复确认/复现，但缺乏有权限方的最终裁决。

**② [#10421](https://github.com/NousResearch/hermes-agent/issues/10421) — 24 条评论，9 👍（今日最高反应）**
`type/feature, comp/agent, P2, needs-decision, area/sessions`。Hermes 仅有 session 级时间（`Conversation started: ...`），缺少可靠的 **turn 级实时时间上下文**，Agent 对"现在/今天/星期几"无稳定感知，必须显式调用工具。这是**长期悬置（4 月创建）且共识度最高**的路线图议题，`needs-decision` 标签表明卡在设计取舍而非可行性。

**③ 平台稳定性三连（各 6 条评论）**
- [#126887](https://github.com/NousResearch/hermes-agent/issues/126887)：macOS 上 `ps` 将 launcher 多行脚本的换行输出为 `\012`，导致 `hermes dashboard --status` 漏报后端进程。
- [#139568](https://github.com/NousResearch/hermes-agent/issues/139568)：MoA reference 模型无视系统提示，稳定伪造 `[called tool: ...]` / `[tool result: ...]` 块——**结构化幻觉**，会污染混合推理结果。
- [#135344](https://github.com/NousResearch/hermes-agent/issues/135344)：`_pid_recycled` 对组合指纹做精确字符串比较，macOS 无 `/proc` 时 start-time 漂移，活

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*