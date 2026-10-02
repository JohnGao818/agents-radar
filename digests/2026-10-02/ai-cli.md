# AI CLI 工具社区动态日报 2026-10-02

> 生成时间: 2026-10-02 03:49 UTC | 覆盖工具: 2 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

> 数据口径：以下基于你提供的 2026-10-02 摘要；未披露仓库总 Issue/PR 数时，以“摘要中重点/新增条目”统计，避免虚构总量。

## 1. 生态全景

2026-10-02 的 AI CLI 工具生态呈现“代理平台化 + 快速迭代 + 稳定性债务”并行。Claude Code 通过 Claude Mods 把插件能力下沉到更深层行为，Codex 则以 Rust 多端、Worktree、MCP、委派任务推进自动化工作流。双方共同痛点集中在 MCP/权限认证、工具装配一致性、长任务连续性与跨平台稳定性。社区对“可编程代理”期待很高，但对静默失败、能力缺失、桌面崩溃的容忍度极低。整体看，功能竞赛仍在加速，成熟度竞争已转向可靠性与工作流连续性。

## 2. 各工具活跃度对比

| 工具 | Release 

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

⚠️ Skills 摘要生成失败。

---

# Claude Code 社区动态日报（2026-10-02）

## 1. 今日速览
- v2.1.287 发布，正式引入 **Claude Mods** 与内置 mod **“You should know”**，插件可修改更深层行为；相关讨论 Issue #91870 已达 229 评论 / 130 👍。
- 高影响问题持续发酵：GitHub connector 无法访问仓库内容、CLAUDE.md 强制规则被忽略、Artifact 公共分享失败、MCP/Chrome 权限与认证异常。
- 过去 24 小时 PR 更新仅 5 条，主要集中在 diff 面板行为、Mods 回滚与 shell 操作审批修复。

## 2. 版本发布

### v2.1.287
- 新增 **Claude Mods**：插件现在可以修改更深层行为。
- 新增 **You should know**：内置 mod，由 side agent 监视并提示可能被用户或 Claude 遗漏的事项。可通过 `/plugin enable cc-plugin-you-should-know@builtin` 启用（

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-10-02

> 数据来源：[github.com/openai/codex](https://github.com/openai/codex)

---

## 一、今日速览

今日 Codex 仓库发布节奏密集，`rust-v0.162.0-alpha.x` 系列持续迭代，同时 `rust-v0.160.0` 正式版落地了任务中心分页浏览、Linux X11 全屏中键粘贴等体验改进。社区侧最突出的矛盾仍集中在 **Windows 桌面客户端的稳定性**（启动卡死、渲染器崩溃、dot 任务工具缺失）以及 **dot/委派任务与 Computer Use、浏览器工具之间的能力断层**。此外，两条高赞功能诉求——**用量限额重置后自动恢复 CLI 会话**（70👍）和 **恢复 Codex App 的分支选择**（45👍）——持续发酵，反映用户对"无人值守长任务"与"工作流连续性"的强烈期待。

---

## 二、版本发布

过去 24 小时内共 9 个 Release，其中 **`rust-v0.160.0` 为唯一正式版**，其余为 alpha 通道滚动发布。

**rust-v0.160.0 主要更新：**

- **Agent 命令中心支持分页浏览历史任务**：新增键盘可访问的 "Show more" 操作，便于在大量任务中回溯。（#49106）
- **Linux X11 终端全屏模式增强**：支持选中转录文本并用中键粘贴。（#49112）
- **支持在项目外启动会话**：可基于 workspace 默认配置启动，降低跨项目使用的摩擦。

**Alpha 通道：** `rust-v0.162.0-alpha.1 ~ alpha.3`、`rust-v0.161.0-alpha.7 ~ alpha.13`、`rust-v0.161.0-alpha.8/9/12/13` 均为版本号递增的例行发布，Release Note 未附变更说明。alpha 版本号已推进至 0.162，说明 0.161 分支接近收敛。

---

## 三、社区热点 Issues

1. **[#21073](https://github.com/openai/codex/issues/21073) 功能请求：用量限额重置后自动恢复 CLI 会话**（16 评论 / 70👍）
   当 Codex 在任务中途触达用量上限时，错误信息已明确给出重置时间（如 "try again at 6:34 AM"），但用户仍需手动回来续跑，夜间时间被浪费。这是今日**点赞数最高**的 Issue，触及长时异步任务的核心体验，企业/rate-limits 标签也暗示其潜在商业价值。

2. **[#49532](https://github.com/openai/codex/issues/49532) 请求把分支选择（Branch selection）加回 Codex App**（13 评论 / 45👍）
   用户在启动会话时无法再选择 Git 分支，配图直指 UI 缺口。45 个赞表明这是**明显的功能回退（regression）**，而非新增诉求，对多分支工作流的开发者影响直接。

3. **[#49458](https://github.com/openai/codex/issues/49458) [Windows] dot 启动的本地任务缺失 Computer Use 工具**（21 评论 / 13👍）
   普通本地 Codex 会话正常，但经 dot 委派启动的任务无法调用 Computer Use。今日**评论数最多**的 Issue，与下面多条 dot 相关报错共同指向委派链路的能力注入缺陷。

4. **[#48938](https://github.com/openai/codex/issues/48938) [Windows] 更新后渲染器反复崩溃、白屏重载与严重输入延迟**（12 评论）
   发帖者为 20x Codex 计划的 ChatGPT Pro 付费用户，措辞激烈，强调对工作、假期与已付费额度造成的实质损失。付费重度用户的强烈反弹值得官方优先响应。

5. **[#49488](https://github.com/openai/codex/issues/49488) [Windows][dot/Work] Computer 任务缺失浏览器/桌面工具，MCP 启动持久失败**（11 评论 / 5👍）
   与 #49458 同源但更深一层：定位到 MCP 启动失败与后续路径错误。两条 Issue 叠加，说明 Windows 上 dot 任务链路的**工具装配是系统性而非偶发问题**。

6. **[#48377](https://github.com/openai/codex/issues/48377) [Windows] 更新后无尽启动转圈，bundle version 未定义**（10 评论）
   About 对话框因启动不完成而无法访问，属典型的启动阻塞类故障，用户几乎无法自助获取诊断信息。

7. **[#47041](https://github.com/openai/codex/issues/47041) GPT-5.6 Sol 与 GPT-6 Astra 以 invalid_prompt 拒绝无害提示**（9 评论 / 2👍）
   两个新模型在 Codex Desktop 上对无害提示返回 `invalid_prompt`，属**模型行为（model-behavior）层面**的问题，对模型可用性影响广泛，需与模型侧联动排查。

8. **[#49988](https://github.com/openai/codex/issues/49988) VS Code 扩展更新后间歇性丢失已提交消息**（7 评论 / 7👍）
   10 月 1 日更新后，按 Enter 会清空输入框但消息未进入会话，重复发送数次才成功。**消息静默丢失**是编辑器集成中最伤信任的缺陷类型，点赞密度高。

9. **[#49551](https://github.com/openai/codex/issues/49551) [macOS] dot 委派任务缺少 Chrome 工具，手动创建的 Chat 却正常**（7 评论 / 5👍）
   同一台机器上手动 Chat 可用 Chrome，dot 委派任务缺少 `node_repl js` 工具。这条 **macOS 对照实验**更具说服力，证明问题出在委派任务的能力继承，而非平台环境。

10. **[#50127](https://github.com/openai/codex/issues/50127) [DOT] 任务创建返回 UNKNOWN、断开通知过期、任务读取语义模糊、Luna schema 失败**（6 评论，今日新建）
    一份聚合式报告，涵盖任务生命周期状态机的多个薄弱点。今日创建即获得讨论，说明 dot 工作流的可观测性问题正在被系统性地收集。

> 其他值得留意：[#50139](https://github.com/openai/codex/issues/50139)（VS Code 需保留并显式排队工作中的后续提示，4 评论）、[#50156](https://github.com/openai/codex/issues/50156)（Windows 11 build 26200 永久卡在 OpenAI logo，今日新建）、[#45701](https://github.com/openai/codex/issues/45701)（macOS 活跃会话被重置回开始屏）。

---

## 四、重要 PR 进展

> 说明：本批次 PR 多为 `copyberry[bot]` 提交并已 CLOSED，推测为内部变更经公开镜像同步，评论数未公开。

1. **[#50148](https://github.com/openai/codex/pull/50148) 向 TUI 暴露托管 Worktree 工具**
   在启用 worktrees 特性的受信本地项目中，通过 MCP 暴露 `create_worktree`、`get_worktree_creation_status`、`list_worktrees`，兼容嵌入式与本地 daemon 会话。为多分支并行开发铺路。

2. **[#50129](https://github.com/openai/codex/pull/50129) 为远程 MCP 服务器保留 Windows 环境变量**
   修复 Unix 侧启动 Windows 执行器上的 stdio MCP server 时，因 allowlist 基于 Unix 默认值而过滤掉 Windows 运行时与临时目录变量的问题。直接对应前述 Windows MCP 启动失败类 Issue。

3. **[#50128](https://github.com

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*