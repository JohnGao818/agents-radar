# AI CLI 工具社区动态日报 2026-09-25

> 生成时间: 2026-09-25 03:11 UTC | 覆盖工具: 2 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI CLI 工具社区动态横向对比分析报告（2026-09-25）

> **数据口径说明**：本次仅 OpenAI Codex 摘要完整；Claude Code 摘要生成失败，Issues/PR/Release 均不可得。因此严格意义上的“横向对比”受限，以下为 **Codex 深度画像 + 跨工具比对清单**，并将 Claude Code 标记为数据缺口。

---

## 1. 生态全景

从可获得数据看，AI CLI 工具正从“模型能力接入”进入“多端一致性、沙箱安全、成本可观测、交互效率”的深水区。Codex 0.157.0 将 GPT-6 Sol/Luna 与 Amazon Bedrock 带入稳定版，显示模型开放与商业化并行加速。但 Windows 桌面端模型选择器缺失、长期冻结卡顿等问题，暴露出跨客户端发布不同步和平台质量债。社区热点高度集中在 Windows 稳定性、沙箱权限、TUI/桌面操作路径与配额透明。一天内推进多个 alpha 版本，说明主线迭代极快，但普通用户应谨慎追新。

---

## 2. 各工具活跃度对比

| 工具 | 今日 Issues | 今日 PR | Release 情况 | 数据完整度 |
|---|---|---|---|---|
| **OpenAI Codex** | 摘要提及 **≥14 个**；Top1 #20214 有 **112 评论 / 87 👍** | 摘要列出 **≥8 个**，多为 `copyberry[bot]` 提交并 CLOSED；PR 表末尾被截断 | **0.157.0 稳定版**；`0.158.0-alpha.7~12` 等 **7 个 alpha 构建** | 部分完整 |
| **Claude Code** | N/A | N/A | N/A | **摘要生成失败，无法评估** |

**Codex 关键数据点**：  
- 最热 Issue #20214：Windows 11 下 App 频繁冻结，112 评论、87 赞，4 月持续至今未关闭。  
- 高赞需求 #3141：Linux 沙箱允许 GPU 访问，39 评论、62 赞。  
- #18396：TUI 隐藏工具调用输出，17 评论、40 赞，典型“沉默多数”需求。  
- #47511：桌面端 Git Commit/Push 按钮回归，28 赞。  
- #47972：今日新提，Windows 桌面端模型选择器缺失 GPT-6 Sol/Luna/Astra。

---

## 3. 共同关注的功能方向

由于 Claude Code 数据缺失，无法确认跨工具共同方向。以下为 **Codex 社区集中诉求**，可作为后续跨工具比对清单：

| 方向 | Codex 具体诉求 | 代表 Issue/PR |
|---|---|---|
| **Windows 稳定性与窗口管理** | 冻结卡顿、多屏最大化溢出、沙箱 helper 失败、内存泄漏

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

⚠️ Skills 摘要生成失败。

---

⚠️ 摘要生成失败。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-09-25

## 今日速览

今天最重磅的消息是 **Codex CLI 稳定版 0.157.0 正式发布，引入 GPT-6 Sol / Luna 两款新模型并支持 Amazon Bedrock**，同时开启了全屏 transcript 默认模式。但新模型的端侧落地并不均衡——Windows 桌面端用户立即反馈模型选择器中看不到新模型（#47972）。社区热度最高的问题依然是 **Windows 11 上的 App 卡顿/冻结**（#20214，累计 112 条评论、87 个赞），Windows 平台的稳定性已成为当前最大的体验缺口。

---

## 版本发布

### rust-v0.157.0（稳定版）

- **新模型支持**：新增 GPT-6 Sol 与 Luna，包含 Amazon Bedrock 接入支持，并为旧模型提供迁移提示（#47332、#47347）。
- **TUI 体验**：全屏 transcript 默认启用，新增 `Shift+点击` 扩展文本选择（#47178、#47414）。
- **后台服务**：为符合条件的场景启用自动后台服务器启动。

🔗 https://github.com/openai/codex/releases

### v0.158.0-alpha 系列（7 个 alpha 版本）

过去 24 小时内连续推送 `0.158.0-alpha.7` 至 `0.158.0-alpha.12`，另有 `0.157.0-alpha.11.1`。**仅一天内推进 6 个 alpha 版本**，反映出当前主线迭代节奏非常快，建议普通用户继续停留在 0.157.0 稳定版。

---

## 社区热点 Issues

### 1. #20214 — Windows 11 下 Codex App 频繁冻结卡顿 ⭐ 社区最热
用户报告在 Ryzen 5 5600 / 32GB 内存的 Windows 11 Pro 上，即使系统资源充足，App 仍频繁冻结与卡顿。**112 条评论、87 个 👍**，是当前评论数与点赞数双料第一的 Issue，且从 4 月持续更新至昨天仍未关闭，说明问题长期未被根治。
🔗 https://github.com/openai/codex/issues/20214

### 2. #3141 — 允许沙箱内访问 GPU
Linux 沙箱阻断了 NVIDIA GPU 访问（`nvidia-smi` 不可用），直接影响本地 AI/ML 工作流。**39 条评论、62 个 👍**，是得票最高的功能类需求之一，用户呼吁沙箱提供可选的 GPU 透传能力。
🔗 https://github.com/openai/codex/issues/3141

### 3. #29343 — Chrome 插件与 Computer Use 静默拒绝访问特定网站
Pro 订阅用户（€225/月）反馈 Codex 在加载某些网站时会无提示地拒绝操作。**35 条评论**，核心争议在于：是安全策略还是 Bug？用户希望至少有明确的错误提示或策略说明。
🔗 https://github.com/openai/codex/issues/29343

### 4. #25826 — Windows 多显示器下最大化窗口溢出到相邻屏幕
在多显示器环境中，最大化窗口会跨越到相邻显示器，**34 条评论、20 个 👍**。这是典型的 Windows 桌面端窗口管理缺陷，对多屏开发者影响明显。
🔗 https://github.com/openai/codex/issues/25826

### 5. #44696 — Windows 沙箱 helper 在每次 exec_command 时失败
`helper_unknown_error: setup refresh had errors`，导致**连普通文件读取都失败**。沙箱初始化层问题，完全阻断 Windows CLI 可用性，21 条评论跟进。
🔗 https://github.com/openai/codex/issues/44696

### 6. #43237 — GPT-6 Astra 对 `hi` 返回 `invalid_prompt`
用户给出了跨 Linux/macOS、CLI 与最小后端的完整复现路径：新模型对最简单的问候语直接报错。**17 条评论**，属于典型的新模型行为回归，对 GPT-6 系列上线信心造成影响。
🔗 https://github.com/openai/codex/issues/43237

### 7. #18396 — TUI 需要提供隐藏工具调用/输出的选项
用户贴出终端截图，展示每条命令后工具调用输出如何淹没界面。**17 条评论、40 个 👍**，点赞数远超评论数，是典型的“沉默多数”需求——用户不愿争论，只想有个开关。
🔗 https://github.com/openai/codex/issues/18396

### 8. #47511 — 桌面端缺少 Git Commit / Push 按钮（回归）
26.917.51856 版本把可见的提交/推送按钮移入了无标签的省略号菜单。**28 个 👍**，用户认为这破坏了日常开发循环中最常用的操作路径。相关需求 #47897 同步提出。
🔗 https://github.com/openai/codex/issues/47511

### 9. #22486 — 上下文压缩应支持独立配置模型
用户指出上下文压缩（compaction）与交互式编码是两类不同任务，用同一模型既不经济也不最优。**13 个 👍**，反映了高级用户对模型使用成本与质量的精细化诉求。
🔗 https://github.com/openai/codex/issues/22486

### 10. #47972 — Windows 桌面端模型选择器缺失 GPT-6 Sol/Luna/Astra
**今日新提**，与 v0.157.0 发布直接相关：CLI 和移动端 Work 已可用新模型，但 Windows 桌面端模型选择器仍不可见。属于典型的跨客户端发布不同步问题。
🔗 https://github.com/openai/codex/issues/47972

> 其他值得关注：#46690（Windows 渲染进程内存泄漏至 4–7 GB）、#33266（MCP `tools/list_changed` 未使工具缓存失效）、#47637（5 小时额度数分钟内被消耗 98%，疑似计量问题）、#47969（Mac App 账号权限报错）。

---

## 重要 PR 进展

> 注：今日 PR 几乎全部由 `copyberry[bot]` 提交并标记为 CLOSED，显示为内部自动化流水线的合入记录。

| PR | 内容 | 价值 |
|---|---|---|
| [#47974](https://github.com/openai/codex/pull/47974) | 跨可写根保留 Git 目录保护 | **安全**：防止 `.git` 指针被解析到其他可写根后绕过保护，修补 Seatbelt/bubblewrap 权限漏洞 |
| [#47971](https://github.com/openai/codex/pull/47971) | 新增 Pro Max 套餐支持 | **商业化**：认证、账户响应、限流后端识别 `promax`，并调整 Pro 层级显示名 |
| [#47988](https://github.com/openai/codex/pull/47988) | 跨等价绑定复用 MCP handlers | **性能**：工具元数据未变时不再重建 handler，避免工具搜索索引反复重建 |
| [#47984](https://github.com/openai/codex/pull/47984) | 新增多智能体生成延迟与失败指标 | **可观测性**：记录 `codex.multi_agent.spawn.phase.duration_ms`，覆盖驻留预留到总延迟全链路 |
| [#47967](https://github.com/openai/codex/pull/47967) | Flex 容量不足改为独立终态错误 | **错误语义**：识别 `flex_unavailable`，停止无意义重试并明确提示 |
| [#47957](https://github.com/openai/codex/pull/47957) | 将工具调用观测限制在 15 MiB 消息预算内 | **稳定性**：避免 Code Mode 场景下请求超限导致工具调用被截断 |
| [#47956](https://github.com/openai/codex/pull/47956) | 图像编辑请求支持文件引用 | **功能**：`ImageEditRequest` 同时接受 `image_url` 与 `file_id`，修复引用历史图片编辑失败 |
| [#47968](https://github.com/openai/codex/pull/47968) | 处理 Btrfs 设备号不匹配 | **Linux 沙箱修复**：Btrfs

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*