# OpenClaw 生态日报 2026-10-07

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-10-07 04:02 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

⚠️ 摘要生成失败。

---

## 横向生态对比

# 横向对比分析报告 | 2026-10-07

> **数据口径说明**：本次输入仅含 OpenClaw 与 Hermes Agent 两项，其中 OpenClaw 摘要生成失败，无法获得 Issues、PR、Release 等量化数据。因此，以下横向对比以 Hermes Agent 为唯一可量化样本；OpenClaw 仅作生态位占位与待验证项。跨项目“共同趋势”只能视为候选信号，需 OpenClaw 数据补全后确认。

---

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正处于“协作层扩张 + 稳定性补课”并行阶段。以 Hermes Agent 为可观测样本，社区焦点集中在跨网关 Bots 协作、插件加载可靠性、更新路径回归与远程桌面/SSH 稳定性。项目保持高 Issue/PR 活跃度，但 PR 合流率仅 10%，显示创新速度明显快于维护吞吐。OpenClaw 作为核心参照今日数据缺失，横向全景不完整，但也提示生态观测与摘要管道本身需要更高健壮性。整体看，生态仍处快速迭代期，质量巩固与发布可信度是当前瓶颈。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release | 关键信号 | 健康度评估 |
|---|---:|---:|---|---|---|
| OpenClaw | 摘要失败，N/A | N/A | N/A | 无可用动态 | 不可评估，数据缺口 |
| Hermes Agent | 50 条：43 新开/活跃，7 关闭 | 50 条：45 待合并，5 合并/关闭 | 无 | #97681 40 评论；插件静默失败；2 个 P1 关闭 | 高活跃、低合流；稳定性与更新机制风险突出 |

Hermes 今日 PR 合流率约 **10%**，Issue 关闭率约 **14%**。虽然关闭了 Windows 网关死锁、SSH 重连泄漏等 P1 问题，但 45 条 PR 待合并说明维护积压明显，项目处于“功能推进快、合流能力紧”的状态。

---

## 3. OpenClaw 在生态中的定位

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报
**日期：2026-10-07**

---

## 1. 今日速览

过去24小时，Hermes Agent 社区保持高活跃：Issues 更新 50 条（新开/活跃 43，已关闭 7），PR 更新 50 条（待合并 45，已合并/关闭 5），无新版本发布。讨论焦点集中在 **Bots 跨网关协作**（#97681，40 条评论）、**插件加载稳定性**（#123926、#134107/#134115）以及 **更新路径回归**（#133992、#113294）。虽然今日关闭了多个 P1 级问题（Windows 网关死锁、SSH 重连泄漏），但 PR 合并率仅 10%，积压明显，项目整体处于“高活跃、低合流”状态，稳定性与更新机制仍是当前主要风险点。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并/关闭的重要 PR 与 Issue：

- **PR #98307 [CLOSED]** `chore(groups): compose Group Chat layers in a permanent integration draft`  
  为 #97681（Bots 跨网关协作）提供集成测试草稿，推进 Group Chat 多智能体协作基础设施。  
  🔗 https://github.com/NousResearch/hermes-agent/pull/98307

- **PR #134126 [CLOSED]** `fix(plugins): register solstice in the stripped PM runtime without httpx`  
  修复 solstice 插件在精简 PM 运行时因缺失 `httpx` 而加载失败的问题。  
  🔗 https://github.com/NousResearch/hermes-agent/pull/134126

- **Issue #133249 [CLOSED, P1]** Windows 创建 profile 死锁多路复用网关（watchdog exit 75）。  
  🔗 https://github.com/NousResearch/hermes-agent/issues/133249

- **Issue #132034 [CLOSED, P1]** Desktop SSH 重连风暴泄漏 detached serve 后端，导致远程 OOM。  
  🔗 https://github.com/NousResearch/hermes-agent/issues/132034

- **Issue #85029 [CLOSED]** macOS Desktop 卡在 CONNECTING，404 读取 dashboard token。  
  🔗 https://github.com/NousResearch/hermes-agent/issues/85029

- **Issue #88994 [CLOSED]** SSH 远程 profile 在本地 profile 名 ≠ remoteProfile 时损坏（回归）。  
  🔗 https://github.com/NousResearch/hermes-agent/issues/88994

- **Issue #49769 [CLOSED]** 可恢复 402（“只能负担 N tokens”）被误判为终端计费并丢弃请求。  
  🔗 https://github.com/NousResearch/hermes-agent/issues/49769

**整体推进评估**：Group Chat 协作层向前迈出一步；solstice 插件问题有多个修复尝试，但尚未全部落地；今日关闭了 2 个 P1 稳定性问题，对 Windows 网关和 SSH 远程桌面场景有积极意义。然而，PR 合并/关闭仅 5 条，大量修复仍待审。

---

## 4. 社区热点

今日讨论最活跃的 Issues/PRs：

- **Issue #97681 [OPEN]** `Let Bots collaborate across gateways`  
  评论 40，👍 4。诉求：让个人智能体跨机器、跨所有者协作，同时不牺牲控制权。这是当前路线图中最核心的议题，已有 PR #98307 集成草稿和 #99960 修复跨网关重复执行。  
  🔗 https://github.com/NousResearch/hermes-agent/issues/97681

- **Issue #123926 [OPEN]** `[Bug]: Plugins silently dropped at boot — _evict_modules iterates sys.modules live`  
  评论 18。插件在启动时随机子集静默失败，仅 `errors.log` 中一条 WARNING，平台集成不可用。反映插件生命周期管理存在严重缺陷。  
  🔗 https://github.com/NousResearch/hermes-agent/issues/123926

- **Issue #31375 [OPEN]** `Feature: Per-tool enable/disable in config (below toolset granularity)`  
  评论 6，👍 3。用户希望工具配置能细化到单个工具，而非整个 toolset（如 `web_search` 与 `web_extract` 分开）。长期需求，社区有共鸣。  
  🔗 https://github.com/NousResearch/hermes-agent/issues/31375

- **PR #134235 / #133957 / #134000 / #133785 / #134237 [OPEN]**  
  多个 PR 集中修复 sol

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*