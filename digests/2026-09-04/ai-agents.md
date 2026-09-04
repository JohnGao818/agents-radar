# OpenClaw 生态日报 2026-09-04

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-09-04 02:40 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 开源项目动态日报

**日期：** 2026-09-04  
**数据窗口：** 过去 24 小时  

---

## 1. 今日速览

过去 24 小时社区与开发活动热度处于**高位**：共 500 条 Issue 更新（新开/活跃 364，关闭 136），500 条 PR 更新（其中 412 条仍开放待处理，88 条已合并/关闭），并发布 1 个新版本 **v2026.9.1**（首次亮相 2026.9.x 系列，主打 Control UI 与原生应用的 Mermaid 图表渲染）。

**项目健康度评估：** ⚠️ 需重点关注。尽管 PR 合并节奏较好（88 条/日），但存在多个 P0 稳定性问题（SQLite 损坏复发、Windows 升级阻塞、Linux 桌面端崩溃）和 P1 生产环境缺陷迟迟无法关闭（大量 Issue 携带 `clawsweeper:needs-maintainer-review` 标签），说明**合并速度赶不上问题报告速度**。此外，多个长期未关闭的核心 Issue（进程泄漏、存储无界增长）已积压超 2 个月，需要维护者投入精力清理。

---

## 2. 版本发布

### v2026.9.1

- **Release 链接：** [openclaw/openclaw Releases v2026.9.1](https://github.com/openclaw/openclaw/releases/tag/v2026.9.1)
- **发布亮点（Highlights）：**
  1. **每个聊天中的图表：** Mermaid 代码块现可在 Control UI 以及原生 macOS、iOS、Android 应用中渲染为图表，支持放大预览；移动端渲染失败时可重试。涉及 PR：#134913、#135746、#135470、#135342
  2. **从安装到聊天：** 优化了新用户的上手流程（Release Notes 有更详细描述，但截断不完整）。

- **破坏性变更 / 迁移注意事项：** 从当前数据来看，该版本涉及多个先前开放的 P0/P1 升级问题（如 #136203、#137377 等）所影响的 2026.8.x 用户。若您的环境正在运行 2026.8.1/2026.8.2 并依赖 Doctor 的自动修复或运行的是 Windows 多代理（multi-agent）环境，请确保升级前阅读 Doctor 输出并做好迁移备份。**注意事项：** 前述提到虽然发版了 2026.9.1，但仓库中仍存在大量针对 2026.8.1/2026.8.2 系列的未决升级问题，需确认该版本是否完整包含修复。

---

## 3. 项目进展

今日 88 条 PR 被合并或关闭。虽然列表未明确给出已合入 PR 的具体标题，但从关闭的 Issue（通常伴随修复的 PR）和相关条目来看，项目在以下方面向前推进：

- **Doctor / 迁移工具链修复**——今日关闭了 #137377（Windows 2026.8.2 上 Doctor --fix 因 Gateway 服务身份检查失败）、#134938（doctor --fix 在遗留 exec-approvals 关卡上死锁，阻塞 session-store 和 workspace-setup-state 迁移）以及 #134179（从文件存储版本升级后遗留 exec-approvals 导致 Gateway 无法启动）。这表明团队在重点修复 2026.7.x → 2026.8.x 的升级路径，解决 Doctor 死锁与服务所有权验证等迁移痛点。
- **Codex 应用服务器可靠性**——关闭了 #135970（Managed Codex app-server 因 dist/extensions 缺少 node_modules 而无法启动），这是 Codex 后端工作流中的一个阻断性问题。
- **进程生命周期管理**——关闭了 #125344（memory-core 本地 embedding workers 与 codex app-servers 无空闲 TTL，导致 gateway cgroup 资源耗尽），说明团队正着手处理 worker 进程泄漏问题，并将其与此前报告的 #124573 进行区分处理。

**建议跟进：** 从关闭的 Issue 和已打开的 PR（#137800、#137828、#137822 等）来看，当前开发重点集中于 **worker/skill 文件回收、原生 Codex 父子会话唤醒、以及 session transcript 完整性**。建议关注以下活跃 PR 的动态：

- [#137800 fix(worker): reclaim remote skill files after worker loss](https://github.com/openclaw/openclaw/pull/137800) —— 处理 #137071 中的 worker 丢失后远端 skill 残留问题。
- [#137822 fix(codex): wake yielded parents after native child completion](https://github.com/openclaw/openclaw/pull/137822) —— 修复 Codex 子进程完成后父会话未被唤醒的问题（与 Issue #137710 对应）。
- [#137273 fix(agents): runtime-only turns persist a fabricated user turn](https://github.com/openclaw/openclaw/pull/137273) —— 修复运行时事件被虚假用户记录填充的问题（对应 Issue #124244）。

---

## 4. 社区热点

以下 Issue 在过去 24 小时获得了较多讨论：

- **#125626：** [OpenClaw 2026.8.

---

## 横向生态对比

# AI 个人助手 / 自主智能体开源生态横向分析报告

**日期：** 2026-09-04

> ⚠️ **数据可用性声明：** 本次分析中，OpenClaw 日报提供完整量化数据；Hermes Agent 日报概述被截断，当前仅能确认“过去 24 小时非常活跃、Issues 与 [数据缺失]”这一信息。涉及 **Hermes Agent 的判断均为待验证推测**，建议补采数据后深化对比。

## 1. 生态全景

个人 AI 助手/自主智能体赛道仍处于**极速迭代与工程化爬坡并存**阶段：头部开源项目保持每日数百 Issue/PR 的高吞吐，但 P0/P1 稳定性问题（数据损坏、升级阻塞、进程泄漏）明显增多，说明社区正从“能做 demo”转向“扛得住真实部署”。产品形态上，多端原生应用（macOS/iOS/Android/Web UI）与系统级治理能力（Doctor 迁移工具链、cgroup 资源隔离）正在成为新一代开源助手框架的标配。与此同时，项目维护压力显著上升——合并速度已开始低于问题报告速度，社区治理与质量巩固成为当务之急。整体来看，生态重心正从前沿能力创新，切换到**可靠性、可升级性与跨平台一致性**。

## 2. 各项目活跃度对比

| 项目 | Issues（总数） | 新开/活跃 | 关闭 | PRs（总数） | 开放 | 合并/关闭 | Release | 健康度 |
|---|---|---|---|---|---|---|---|---|
| **OpenClaw** | 500 | 364 | 136 | 500 | 412 | 88 | **v2026.9.1**（新 2026.9.x 系列，首推 Mermaid 图表渲染） | ⚠️ 需重点关注：P0/P1 问题积压，核心 Issue 超 2 个月未关闭 |
| **Hermes Agent** | 数据缺失 | 数据缺失 | 数据缺失 | 数据缺失 | 数据缺失 | 数据缺失 | 未知 | ⚠️ 无法量化评估（可见活跃度较高） |

OpenClaw 单日 500 Issue + 500 PR 的流量，使该仓库处于**顶级开源生态活跃区间**（显著高于 GitHub 绝大多数项目）。但 412 条 PR 仍开放待处理，结合多个 P0 问题复发，体现的是**高热度下的治理瓶颈**。

## 3. OpenClaw 在生态中的定位

- **规模定位：** 单日 88 条 PR 合并/关闭、364 条活跃 Issue，社区规模与迭代速度处于个人 AI 助手开源阵营头部；其健康度问题也正由这种规模反噬而来。
- **技术路线差异：** OpenClaw 并非单纯 Agent 开发框架，而是走**垂直整合的完整个人助手系统**路线——自研 Control UI + 原生桌面/移动客户端 + Doctor 迁移工具链 + Gateway 服务治理，类似“AI 助手中的 Apple 式闭环”。
- **功能重心：** v2026.9.1 引入聊天内 Mermaid 渲染、新手流程优化，说明产品已从 Agent 能力延伸至**会话体验与可视化表达层**。
- **工程痛点暴露：** SQLite 损坏复发、Windows/Linux 跨平台升级阻塞、worker 进程泄漏——表明 OpenClaw 用户已进入大规模真实使用阶段，项目正在为“成规模的生产级个人助手”买单。
- **与 Hermes Agent 同场对比的限制：** Hermes Agent 数据不完整，若其保持相似活跃度，则证明“模型背景实验室做 Agent”与“开发者社区驱动做 Agent”两条路径正在平行发展，但目前无法做量化横向排名。

## 4. 当前阶段共同关注的技术方向

由于 Hermes Agent 今日数据缺失，跨项目“共同”结论仍需验证。从 OpenClaw 社区可提炼出当前 AI 智能体工程化的 **6 个核心方向**，它们很可能也是同类项目正在攻克的共性难题：

1. **数据持久化可靠性** — SQLite 损坏问题复发（Issue 持续暴露），指向嵌入式存储在高频读写下的稳定性短板。
2. **跨平台升级与迁移** — 2026.8.x 系列多个升级阻塞问题，涉及 Windows 服务权限、Doctor 死锁、遗留配置项导致 Gateway 无法启动；迁移工具链本身成为高优先级模块。
3. **进程/worker 生命周期管理** — memory-core embedding workers、codex app-servers 无空闲 TTL 导致 cgroup 资源耗尽，以及 worker 丢失后远端 skill 文件回收（PR #137800）。
4. **子会话与父子 Agent 唤醒机制** — PR #137822 修复 Codex 子进程完成后父会话未被唤醒的问题，多 Agent 嵌套对话生命周期成为实现难点。
5. **会话记录真实性与完整性** — PR #137273 修复运行时事件被“虚假用户记录”污染的问题，涉及 transcript 审计可信度。
6. **端侧渲染与跨端一致性** — Mermaid 在 Web/桌面/移动端渲染与移动端失败重试，表明多端体验统一是产品化关键路径。

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
|---|---|---|
| **功能侧重** | 完整个人助手系统：Control UI、原生移动/桌面端、图表渲染、会话管理 | 数据不足；从背景推测侧重模型原生 Agent 能力（待验证） |
| **目标用户** | 需要开箱即用多端助手的个人用户/开发者；大规模

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-09-04

## 1. 今日速览

过去 24 小时 Hermes Agent 仓库非常活跃：Issues 与

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*