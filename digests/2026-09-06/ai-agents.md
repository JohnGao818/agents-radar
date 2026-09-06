# OpenClaw 生态日报 2026-09-06

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-09-06 02:39 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

⚠️ 摘要生成失败。

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向对比分析报告（2026-09-06）

> **数据说明**：本次数据源仅 Hermes Agent 提供有效动态；OpenClaw 作为“核心参照”项目，其动态摘要生成失败，因此无法进行完整双项目定量对比。下文中 OpenClaw 相关字段以“数据缺失”标注，仅在可推断处给出结构性判断。

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态当前处于“社区贡献洪峰 vs 维护者审阅瓶颈”阶段：以 Hermes Agent 为例，日 Issue 更新 50 条、PR 更新 50 条，但合并率仅约 6%，尚未形成稳定的合入节奏。用户需求已从“单次对话”转向“离线的常驻智能体”，集中要求 Bot 群聊在桌面端关闭、部署至 VPS/家庭服务器后仍持续工作。同时，长期未解决的基础设施问题（如技能索引过期 7 周）与快速修复的安全问题并存，显示生态活跃度高但质量巩固不足。由于 OpenClaw 本次缺席，跨项目共性只能依靠 Hermes 单项目信号推断，全景完整性受限。

---

## 2. 各项目活跃度对比

| 项目 | Issues 动态 | PR 动态 | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 数据缺失（摘要生成失败） | 数据缺失 | 数据缺失 | 未知，无法评估；本次作为“核心参照”缺席 |
| **Hermes Agent** | 50 条更新：49 条新开/活跃，1 条关闭 | 50 条更新：47 条待合并，3 条合并/关闭；合并率约 6% | 无新版本 | 社区提交活跃但审阅吞吐量低；存在 7 周未解决的基础设施问题及 P1 更新故障，整体呈“高活跃、中低稳定”状态 |

---

## 3. OpenClaw 在生态中的定位

本次报告无法给出 OpenClaw 的优势、技术路线差异或社区规模对比，原因在于其动态摘要生成失败。但可以做出两点结构性判断：

- **定位角色**：OpenClaw 被设定为“核心参照项目”，说明在该生态分析框架中它被视为基准坐标。若后续数据恢复，最值得对比的是它与 Hermes 在“常驻 Agent 架构”和“桌面端/网关分离”上的路线差异。
- **缺席本身值得关注**：核心参照项目失去数据可观测性，可能是数据管道故障，也可能是项目热度或更新节奏异常。在恢复数据前，不应将 OpenClaw 的生态影响力简单等同于 Hermes 或默认其健康。

若必须给出差异化结论：Hermes 来自 NousResearch，其 PR 涉及 OAuth 安全、macOS Keychain、Windows 路径兼容等，带有较强的“研究 + 桌面 + 消息平台集成”色彩；OpenClaw 从仓库名看可能更偏向“通用自动化爪手/工具调用”路线，但缺乏数据支持，无法作实质性对比。

---

## 4. 共同关注的技术方向

由于 OpenClaw 数据缺失，无法确认“多项目共同涌现”。但 Hermes 社区的高频诉求已经足够强烈，很可能代表同类项目共同演进方向：

- **“桌面关闭后继续工作”的常驻 Agent**  
  涉及 Hermes Agent 的 #97681、PR #98307 / #98073。用户要求在笔记本、家庭服务器或 VPS 上部署的 Bot 群聊不依赖桌面端常驻，消息与文件交换可持续进行。

- **网关所有权、Runner 与会话状态隔离**  
  这是 #97681 的架构核心，反映单 Agent 从“本地 GUI 会话”走向“分布式多端服务”的趋势。

- **身份与密钥安全的自动化边界**  
  涉及 Claude Code OAuth 刷新令牌被 Hermes 轮换导致登出的安全问题（#103978 → PR #103988 当日修复）。自动化和密钥管理之间存在高风险交叉区。

- **自动化基础设施自身的可维护性**  
  #66616 技能索引新鲜度探针连续 7 周报警，163 条评论多由机器人重复触发。Agent 项目开始需要“维护 AI 的 AI”，否则机器人噪音会淹没真实用户信号。

- **跨平台桌面端细节兼容**  
  涉及 Windows 路径分隔符（PR #103991）、Rich 文本渲染崩溃（PR #103970）等。终端用户体验往往被非核心但高频的平台 bug 卡住。

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
|---|---|---|
| **功能侧重** | 数据缺失 | 自主智能体 + 桌面端 + Bot 群聊连续性，辅以 CLI、工具调用容错 |
| **目标用户** | 数据缺失 | 有意部署常驻机器人到家庭服务器/VPS，并通过消息平台执行 `/group` 命令的高级开发者 |
| **技术架构特色** | 数据缺失 | 网关与 Runner 地位分离、会话状态隔离、macOS Keychain OAuth 集成、Windows 图像识别路径兼容、非流式 provider 工具调用重试 |
| **社区治理** | 数据缺失 | 社区 PR 驱动，但维护者审阅是明显瓶颈；高价值 PR 长期带 `needs-decision` 标签，重复 PR 被快速关闭 |
| **成熟度信号** | 数据缺失 | 功能推进快但基础设施长期降级；P1 更新 bug 影响真实用户，仍处于“功能先行、质量补课”阶段 |

---

## 6. 社区热度与成熟度

因 OpenClaw 信息缺失，只能对 Hermes Agent 作分层判断：

- **活跃度分层**：Hermes Agent 处于 **“高提交活跃、低合并完成”的快速迭代阶段**。每日 50 条 Issue

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 (2026-09-06)

## 1. 今日速览

过去 24 小时项目保持高活跃度：50 条 Issue 更新（49 条新开/活跃，1 条关闭）与 50 条 PR 更新（47 条待合并，3 条已合并/关闭）。社区贡献大量修复 PR，涵盖桌面端、Claude Code OAuth 安全、群聊机器人持续性等方向，但合并率仅约 6%，维护者审阅吞吐量是当前瓶颈。无新版本发布；#66616 技能索引自动探针问题已持续近两个月仍未解决，是当前最突出的稳定性隐患。此外多名用户反复报告 `hermes update` 造成的 root 文件权限与更新中断问题，累积情绪明显。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日确认关闭 3 条 PR（含重复 PR #103990，内容为 free-response 频道 opt-in 自动线程的重复提交）。值得注意的新提交与进展包括以下内容。

**安全修复：**
- [PR #103988 fix(auth): stop Hermes from logging Claude Code out](https://github.com/NousResearch/hermes-agent/pull/103988) — 停止 Hermes 轮换来自 macOS Keychain 的 Claude Code OAuth 刷新令牌，解决 9/6 新报告的安全问题（#103978）。当天报告、当天即有 fix PR，响应速度快。

**桌面端修复：**
- [PR #103992 fix(desktop): honor hidden live worktree lanes (#103985)](https://github.com/NousResearch/hermes-agent/pull/103992) — 修复用户“从侧边栏隐藏”的 worktree lane 被实时扫描重新加回的问题。
- [PR #103991 fix(gateway): use forward slashes in Windows vision_analyze image hint](https://github.com/NousResearch/hermes-agent/pull/103991) — 修复 Windows 桌面端图像路由到 `vision_analyze` 时的路径分隔符错误。

**CLI 稳定性：**
- [PR #103970 fix(cli): escape Rich markup in resumed session title (#103602)](https://github.com/NousResearch/hermes-agent/pull/103970) — 会话标题含 `/plan` 等 Rich 标记时导致 CLI 崩溃的问题。
- [PR #103983 fix(agent): retry incomplete tool calls before any batch executes](https://github.com/NousResearch/hermes-agent/pull/103983) — 非流式 provider 返回不完整工具参数时自动重试，并拒绝语法无效的本地 `execute_code` 源码，防止部分副作用产生。

**群聊Bot 主线功能：**
- [PR #98307 feat(bot-mode): complete Group Chat continuity, control, and files](https://github.com/NousResearch/hermes-agent/pull/98307) 与 [PR #98073 feat(bot-mode): control Group Chats from messaging](https://github.com/NousResearch/hermes-agent/pull/98073) 持续更新。这是 #97681 的核心落地，目标是让 Bot 群聊在 Desktop 关闭后仍可持续交换消息与文件，并允许授权用户通过现有消息平台执行 `/group` 命令。两个大 PR 仍带 `needs-decision` 标签待审。

整体来看，项目向前推进主要靠社区 PR 驱动，修复覆盖面广，但维护者合并速度跟不上提交速度。

## 4. 社区热点

- [Issue #66616 [skills-index-watchdog] Skills index is stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616) — **163 条评论**，为今日评论数最高。这是 nousbot-eng 的自动化新鲜度探针在反复报告 `/docs/skills` 依赖的索引文件已过期（当前 29.8h 旧，限制 26h）。高评论数主要由机器人重复探测驱动，但问题持续超过 7 周未被解决。反馈核心是：核心基础设施（技能索引重建工作流）长期降级，可能反映维护者对自动化健康的关注不足。

- [Issue #97681 Bot Group Chats should keep working after Desktop closes](https://github.com/NousResearch/hermes-agent/issues/97681) — **23 条评论**，是真实的社区功能主线。用户希望在笔记本、家庭服务器或 VPS 上部署的 Bot 群聊不依赖 Desktop 常驻。评论中最核心的诉求是网关所有权架构、同网关 runner 与会话状态隔离已经到 main，需要完成最后的桌面端连接工作。对应 PR #98307 / #98073 仍在等待决策。

- [Issue #26058 auto_thread disabled for free_response_channels breaks legitimate use case](https://github.com/NousResearch/hermes-agent/issues/26058) — **10 条评论，5 个 👍**，P1，报告至今近 4 个月。核心矛盾：`free_response_channels` 中的频道会完全跳过 auto_thread 创建，导致享受“免打扰播报”的频道无法使用线程模式。尽管收到 5 个赞且带 P1 标签，团队未给出明确修复方向；9/6 提交的 PR #103990 也因重复被直接关闭。

## 5. Bug 与稳定性

**P1 高影响：**

- [Issue #98022 hermes update 修复引入的 catch-up fleet restart 在每次运行时重复触发（已有临时规避 #95294 fix，但陈旧 interrupted receipt 导致无限重启）](https://github.com/NousResearch/hermes-agent/issues/98022) — 影响真实用户更新。`update_receipts/latest.json` 中如果有一次中断的陈旧 receipt，后续每次更新都会误以为

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*