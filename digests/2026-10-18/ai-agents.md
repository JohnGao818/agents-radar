# OpenClaw 生态日报 2026-10-18

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-10-18 02:48 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

⚠️ 摘要生成失败。

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 · 2026-10-18

> 数据窗口：过去 24 小时｜Issues 更新 50 条（新开/活跃 47，关闭 3）｜PR 更新 50 条（待合并 49，合并/关闭 1）｜新版本 0 个

---

## 1. 今日速览

1. **活跃度极高，但吞吐严重不对称**：Issues 侧 47 进 3 出（关闭率 6%），PR 侧 49 进 1 出（关闭率 2%），零发版。项目处于典型的"高强度稳定化、低合并吞吐"状态，**评审带宽而非开发带宽**是当前第一瓶颈。
2. **全部工作围绕 10/14 合入的统一网关 `#106742` 的善后展开**：追踪 issue [#134889](https://github.com/NousResearch/hermes-agent/issues/134889) 单日新增 175 条评论，已成为事实上的"作战室"，并已拆分为至少 9 个编号修复分包。
3. **修复确有收敛**：今日 3 个关闭项中，[#139160](https://github.com/NousResearch/hermes-agent/issues/139160)（网关修复包 2，"全部行已修复"）与 [#140337](https://github.com/NousResearch/hermes-agent/issues/140337)（包 9，17 项发现）双双收口，P0 级 TLS 崩溃 [#137255](https://github.com/NousResearch/hermes-agent/issues/137255) 也已关闭。
4. **但回归面仍在扩大**：今日新增 P0 网关所有权重启循环 [#135392](https://github.com/NousResearch/hermes-agent/issues/135392)、Nous 缓存命中率崩塌 [#140758](https://github.com/NousResearch/hermes-agent/issues/140758)、Telegram 消息编辑崩溃 [#140845](https://github.com/NousResearch/hermes-agent/issues/140845)，均指向统一网关的边角语义。
5. **贡献通道出现阻塞信号**：[#131859](https://github.com/NousResearch/hermes-agent/issues/131859)（44 条评论、`blocked`）与 [#135782](https://github.com/NousResearch/hermes-agent/issues/135782)（受 per-author open-PR 上限限制）共同说明，外部贡献者"提不了 PR"，这正在人为压低合并侧数据。

**健康度评估**：功能推进 ✅ 正常 ｜ 稳定性 ⚠️ 承压（P0/P2 回归持续产出）｜ 评审吞吐 🔴 告警（49:1 的待合并比）｜ 社区参与 ✅ 旺盛（但 duplicate PR 增多）。

---

## 2. 版本发布

过去 24 小时 **0 个新版本**，无 Release 记录。考虑到统一网关的善后分包仍在滚动关闭（包 1 尚未收口），预计下一个补丁版本仍会以"网关稳定性"为主题，短期内不建议期待新特性版本。

---

## 3. 项目进展

### 今日关闭/合并的重要项

| 编号 | 类型 | 内容 | 意义 |
|---|---|---|---|
| [#139160](https://github.com/NousResearch/hermes-agent/issues/139160) | Issue（CLOSED） |

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*