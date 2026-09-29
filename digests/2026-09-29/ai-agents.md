# OpenClaw 生态日报 2026-09-29

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-09-29 03:57 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 · 2026-09-29

> 数据来源：github.com/openclaw/openclaw ｜ 统计窗口：过去 24 小时

---

## 一、今日速览

1. **活跃度极高，但集中在下游修复层面**：24 小时内 Issues 更新 500 条（新开/活跃 382、关闭 118），PR 更新 500 条（待合并 334、已合并/关闭 166），属于典型的"发布后修复窗口"状态。
2. **主线焦点是 2026.9.6 → 2026.9.7 的紧急修复**：`prepared-model-catalog.worker.js` 内存泄漏、Gateway 启动/崩溃循环、`openclaw update` 卡死三条主线占据了绝大多数 P0 讨论；社区自发维护了 2026.9.7 Fixes Tracker（#157531）。
3. **稳定版仍在"止血"**：今日发布的是 `v2026.8.33`（gateway-only extended-stable/LTS 线，只带关键安全与可靠性修复），而当前最新版为 2026.9.6——说明维护者在 LTS 与前沿版之间做双轨兜底。
4. **维护者动作明确**：大量 `deslop`（去重/收敛重构）PR、`qa-lab` 断言修复、以及 `docs: draft v2026.9.7 release notes`（#160933）说明项目正从"新功能"转向"债务清理 + 发布收敛"。
5. **健康度判断：中短期承压，长期可控**。崩溃/内存/更新三大类问题均有明确 owner 与可复现路径，但 P0 未修复项数量偏多，且部分问题（如 #40001）已挂起近 7 个月，存在结构性欠账。

---

## 二、版本发布

### v2026.8.33 — gateway-only `extended-stable`（≈LTS）

- **发布定位**：LTS 通道的补丁版本，基线与 2026 年 8 月底的 OpenClaw 一致。
- **更新内容**：
  - 关键安全更新
  - 可靠性与性能修复
  - 新增模型支持等特性回移
- **破坏性变更**：无。属于保守型回移，面向不愿跟进 2026.9.x 前沿线的生产网关。
- **迁移注意事项**：
  - 该版本**仅覆盖 gateway 组件**，不包含 9.x 线的 UI / agent 运行时新特性；从 9.x 降级回 8.x 会丢失新模型支持与部分会话状态 schema 变更能力，需谨慎评估。
  - 官方明确指出**当前最新版为 2026.9.6**，8.33 是"稳态兜底"而非推荐升级目标。

> 结合今日数据看：8.33 的发布更像是对 9.x 线连续崩溃/内存/更新问题的**风险隔离动作**，为受影响的 632-agent 级舰队和自托管用户提供退路。

---

## 三、项目进展（已合并 / 已关闭）

今日共有 **166 条 PR 合并或关闭**、**118 条 Issue 关闭**。以下为信号最强的几项：

| 项目 | 状态 | 意义 |
|---|---|---|
| [#159514](https://github.com/openclaw/openclaw/issues/159514) 【P0】2026.9.6 catalog worker 每次请求重建 discovery registry（≈8 MB 不可回收模块/请求，1.5–2.5 GB/h） | **CLOSED** | 与 #157842 同源的内存泄漏主线，关闭意味着该分支已有落地修复，是今日最重要的止血进展。 |
| [#145072](https://github.com/openclaw/openclaw/issues/145072) 【P0】macOS npm update 在 "global install swap" 失败（launcher 指纹含 symlink mode；shim 备份未 chmod） | **CLOSED**（`clawsweeper:queueable-fix`、`fix-shape-clear`） | 直接解除 macOS 用户无法升级的死锁，属于 release-blocker 级修复。 |
| [#156425](https://github.com/openclaw/openclaw/issues/156425) 【P1】Anthropic 路由下 durable context-engine turn 永不提交，cache-TTL 标记成为终端锚点 | **CLOSED** | 解决长会话在 Anthropic 路由上的"静默断记"问题。 |
| [#90945](https://github.com/openclaw/openclaw/issues/90945) 【P1】`channel_ingress_events` 陈旧 claim 永不回收 → Telegram DM 死锁 | **CLOSED** | 跨度近 4 个月的通道级死锁问题收口。 |
| [#113323](https://github.com/openclaw/openclaw/issues/113323) 【P1】本地推理模型 reasoning-token 流式期间 LLM idle timeout 中断 run | **CLOSED** | 改善本地模型（自托管场景）可用性。 |
| [#64036](https://github.com/openclaw/openclaw/issues/64036) 【P2】`chunkTextByBreakResolver` 末块尾随空白 | **CLOSED** | 文本分块正确性修正。 |
| [#122403](https://github.com/openclaw/openclaw/issues/122403) 【P2】Control UI 模型选择器显示本地/云端来源 | **CLOSED** | 但需注意：以 `stale` 标签关闭，**并非功能落地**，更可能是策略性关闭。 |

**PR 侧推进方向**（多为待合并，反映下一版内容）：
- **发布工程**：[#160933](https://github.com/openclaw/openclaw/pull/160933) v2026.9.7 release notes 草案已起草（涉及 2,669 个 PR、482 个直接提交、326 位贡献者）；[#160695](https://github.com/openclaw/openclaw/pull/160695) 冻结候选版本自带 harness 校验。
- **去债重构（deslop 系列，steipete 主导）**：[#159752](https://github.com/openclaw/openclaw/pull/159752)（Gateway server/worker 环境）、[#160917](https://github.com/openclaw/openclaw/pull/160917)、[#160938](https://github.com/openclaw/openclaw/pull/160938)（delivery 路由与准备层）、[#159527](https://github.com/openclaw/openclaw/pull/159527)（auto-reply 第四轮）、[#160858](https://github.com/openclaw/openclaw/pull/160858)（cron 保留清理移出 Gateway 主线程）。
- **正确性修复**：[#160620](https://github.com/openclaw/openclaw/pull/160620) cron 将节点策略拒绝视为失败（此前会误报成功）、[#160675](https://github.com/openclaw/openclaw/pull/160675) 防止前台节点完成重复投递、[#160696](https://github.com/openclaw/openclaw/pull/160696) 阻断受限会话越根读取回复媒体（P0 安全边界）、[#160888](https://github.com/openclaw/openclaw/pull/160888) 停止把 `pass:` 之后的普通文本误判为密钥。

**整体推进度评估**：今日项目向前迈进的**主要不是功能，而是稳定性与发布基础设施**。9.7 的 release notes 草案出现，意味着 9.6 的问题集群已被系统性收敛为一个可发布的修复批次。

---

## 四、社区热点

按评论数排序，今日讨论最集中的是：

1. **[#153257](https://github.com/openclaw/openclaw/issues/153257)（39 条评论）— "OpenClaw 2026.9.5 把稳定环境变成 8 小时失败恢复"**
   - 标签齐备：`bug:crash`、`P0`、`impact:crash-loop`、`🦐 gold shrimp`、`clawsweeper:manual-only`。
   - **诉求**：用户对"稳定版"的信任被打破。核心情绪不是"有 bug"，而是**升级路径本身不可回退**——出现问题时缺少安全降级手段。

2. **[#149538](https://github.com/openclaw/openclaw/issues/149538)（22 条评论）— `main` 到达 ready 但永不服务，/health 全超时，事件循环饥饿（632-agent 舰队）**
   - **诉求**：大规模部署场景下的可用性。RSS 持续攀升至 OOM，且与 #148529 的启动耗时问题是两个独立缺陷，说明**集群用户同时暴露在多条故障曲线上**。

3. **[#102175](https://github.com/openclaw/openclaw/issues/102175)（21 条评论，`🦞 diamond lobster`）— 嵌入式 prompt cache 跨 room-event / policy / Responses 边界失效**
   - 标签含 `needs-product-decision`、`needs-security-review`。
   - **诉求**：长生命周期会话的**成本与延迟**。工具清单在 44+ 轮之间变化导致 prompt cache 无法复用，直接影响 token 账单。

4. **[#97616](https://github.com/openclaw/openclaw/issues/97616)（16 条评论）— hook/tool 子进程未回收，僵尸进程累积导致运行时退化**
   - **诉求**：长跑网关的资源卫生。与今日的 catalog worker 泄漏形成"内存 + 进程"双重资源泄漏图景。

5. **[#157531](https://github.com/openclaw/openclaw/issues/157531)（15 条评论）— 2026.9.7 Fixes Tracker**
   - 社区/维护者共建的发布追踪清单，当前 prepared PR 已含 18/21 个已确立的 P1 候选。**这是今日最具"路线图信号"价值的条目**。

6. **[#40001](https://github.com/openclaw/openclaw/issues/40001)（16 条评论，`🦞 diamond lobster`，P0）— write 工具缺少 append 模式，隔离 cron 会话覆写共享文件**
   - 创建于 2026-03-08，至今开放。**诉求**：cron/多会话并发下的数据安全，属"设计缺陷"而非"实现 bug"。

> **共性分析**：热点榜单高度集中在 **"稳定性 + 资源泄漏 + 会话状态一致性"** 三类，说明 OpenClaw 已从"功能能否跑通"阶段进入"能否长期稳定承载生产负载"阶段。用户的核心焦虑是 **升级安全性与可回退性**。

---

## 五、Bug 与稳定性

### 🔴 P0 / release-blocker（无现成 fix PR）

| Issue | 摘要 | fix PR |
|---|---|---|
| [#153257](https://github.com/openclaw/openclaw/issues/153257) | 2026.9.5 导致稳定环境崩溃，8 小时恢复 | ❌ `no-new-fix-pr` / `manual-only` |
| [#149538](https://github.com/openclaw/openclaw/issues/149538) | Gateway ready 后不服务，事件循环饥饿 + OOM（632-agent 舰队） | ❌ `no-new-fix-pr` |
| [#40001](https://github.com/openclaw/openclaw/issues/40001) | write 工具无 append 模式，cron 会话静默覆写共享文件 | ❌ 需产品决策 |
| [#157160](https://github.com/openclaw/openclaw/issues/157160) | 插件 doctor 后会话状态导致 Gateway 崩溃循环 | ❌ `recovery-stuck` |
| [#155859](https://github.com/openclaw/openclaw/issues/155859) | 启动墙钟时间随启用插件数线性增长（discord/codex/weixin 主导 120s 发布预算） | ❌ |
| [#156571](https://github.com/openclaw/openclaw/issues/156571) | 2026.9.5 model-catalog worker 泄漏临时源码捕获（1–3 GB/min，打满磁盘） | ❌ |
| [#154114](https://github.com/openclaw/openclaw/issues/154114) | `openclaw update` 候选演练失败："No usable, authenticated, tool-capable inference route" | ❌ |
| [#158936](https://github.com/openclaw/openclaw/issues/158936) | macOS 应用就绪看门狗对慢启动网关发 SIGTERM → 重启循环 | ⚠️ `fix-shape-clear` / `queueable-fix`，**可排队修复** |
| [#156917](https://github.com/openclaw/openclaw/issues/156917) | state-lifecycle 租约无心跳/强制接管，一个挂起客户端阻塞启动 31 分钟 | ❌ `manual-only` |
| [#156424](https://github.com/openclaw/openclaw/issues/156424) | 共享状态 `audit_events` 索引损坏但进程/端口仍存活 | ❌ |
| [#160521](https://github.com/openclaw/openclaw/issues/160521) | 状态 DB 读准入封存 → "Worker environment inventory has closed" → reconcileActive 未处理拒绝 | ❌ `needs-live-repro` |
| [#159612](https://github.com/openclaw/openclaw/issues/159612) | 子代理完成结算无限

---

## 横向生态对比

# 横向对比分析报告 · 2026-09-29  
> 数据说明：OpenClaw 数据完整；Hermes Agent 摘要生成失败，以下横向对比将以 OpenClaw 为主，Hermes 相关结论标注为“数据缺失/无法评估”，不进行无依据推断。

---

## 1. 生态全景

当前样本显示，个人 AI 助手/自主智能体开源生态已进入“生产化深水区”：核心项目 OpenClaw 活跃度极高，但 24 小时 Issues/PR 各更新 500 条，集中处理 2026.9.6 → 2026.9.7 的崩溃、内存泄漏、更新卡死与 Gateway 循环故障。  
社区关注点正从“功能能否跑通”转向“能否长期稳定承载生产负载”，具体表现为升级安全性、可回退性、资源卫生、多会话状态一致性成为高频议题。  
维护者通过 LTS/gateway-only 补丁、2026.9.7 Fixes Tracker、release notes 草案和 deslop 重构进行风险隔离与债务收敛。  
Hermes Agent 因摘要失败暂无可用数据，无法形成双项目完整对比；生态判断目前以 OpenClaw 为唯一高置信样本。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release 情况 | 健康度/阶段 |
|---|---:|---:|---|---|
| **OpenClaw** | 500 条：新开/活跃 382，关闭 118 | 500 条：待合并 334，已合并/关闭 166 | `v2026.8.33` gateway-only extended-stable/LTS；最新版为 2026.9.6；2026.9.7 release notes 草案已起草 | **高活跃 + 发布后修复窗口**。中短期承压，长期可控；P0 较多，但多数有 owner/复现路径；存在 #40001 等结构性欠账 |
| **Hermes Agent** | 摘要生成失败，未提供 | 摘要生成失败，未提供 | 未提供 | **无法评估**。数据缺失，无法判断活跃度、发布节奏与稳定性 |

**结论**：OpenClaw 处于“高活跃、高负载、质量止血”象限；Hermes 当前无有效信号，横向活跃度对比不成立。

---

## 3. OpenClaw 在生态中的定位

**核心参照，偏生产级自托管网关/智能体运行时。**  
OpenClaw 今日数据体现出的社区规模信号很强：2026.9.7 release notes 草案涉及约 2,669 个 PR、482 个直接提交、326 位贡献者；24 小时内 Issues/PR 各 500 条更新。这说明它不是早期小规模项目，而是已有较大贡献者基数与生产用户负载。

**优势**：
- 多通道、Gateway、模型目录、插件体系、Control UI、自托管部署等能力面较宽。
- 采用 LTS/前沿双轨：`v2026.8.33` 作为 gateway-only extended-stable 兜底，2026.9.6 为最新前沿版。
- 社区具备发布工程能力：Fixes Tracker、release notes 草案、qa-lab 断言、deslop 债务清理。

**技术路线差异**：
- 更强调长跑 Gateway、worker 进程、catalog worker、durable context-engine、channel ingress、state-lifecycle 等运行时基础设施。
- 当前主线不是堆功能，而是修复内存泄漏、崩溃循环、更新卡死、会话状态一致性。
- 从需求看，OpenClaw 用户中包含 632-agent 级舰队、自托管生产环境、macOS 升级用户和 cron/多会话自动化场景，定位明显偏向“生产运行时”，而非轻量单机助手。

**与 Hermes 的对比**：因 Hermes 摘要失败，无法进行数据化社区规模、技术路线与生态位对比。若 Hermes 同样定位个人 AI 助手，OpenClaw 的故障面更偏服务端长跑、多租户与大规模舰队。

---

## 4. 共同关注的技术方向

> 当前仅 OpenClaw 有可核验数据，因此以下不是“多项目已验证共同需求”，而是 OpenClaw 社区高度集中、建议跨项目重点核验的方向。Hermes 需补充数据后才能确认是否共同涌现。

| 技术方向 | 具体诉求/证据 | 涉及项目 |
|---|---|---|
| **升级安全与可回退性** | #153257 稳定环境升级后 8 小时失败恢复；#154114 `openclaw update` 候选演练失败；macOS npm update 死锁；LTS 8.33 作为风险隔离 | OpenClaw |
| **资源泄漏治理** | catalog worker 约 8 MB/请求、1.5–2.5 GB/h 内存泄漏；临时源码捕获 1–3 GB/min 打满磁盘；hook/tool 子进程僵尸累积 | OpenClaw |
| **大规模舰队可用性** | 632-agent 舰队出现 main ready 但不服务、/health 全超时、事件循环饥饿、OOM；启动墙钟随插件数线性增长 | OpenClaw |
| **会话状态一致性** | durable context-engine turn 永不提交；`channel_ingress_events` 陈旧 claim 导致 Telegram DM 死锁；state-lifecycle 租约无心跳阻塞启动 | OpenClaw |
| **并发写入与数据安全** | write 工具缺少 append 模式，隔离 cron 会话覆写共享文件；前台节点完成重复投递 | OpenClaw |
| **Prompt Cache 与成本延迟** | 嵌入式 prompt cache 跨 room-event/policy/Responses 边界

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ 摘要生成失败。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*