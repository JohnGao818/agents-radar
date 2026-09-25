# OpenClaw 生态日报 2026-09-25

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-09-25 03:11 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报（2026-09-25）

---

## 1. 今日速览

- **活跃度极高**：过去 24 小时 Issues 更新 500 条（新开/活跃 444、关闭 56），PR 更新 500 条（待合并 393、合并/关闭 107），无新版本发布。项目正处于 2026.9.6 → 2026.9.7 的密集修复窗口期。
- **稳定性是当日主线**：Issues 前 50 条中至少 8 条为 **P0**、18 条为 **P1**，焦点集中在模型目录（model-catalog）重建循环、SQLite 数据库锁/全量拷贝、网关启动耗时随插件数量膨胀等系统级性能问题。
- **回归集中爆发**：多条 2026.9.x 升级路径出现回归（升级回滚、Doctor 迁移被拒、插件激活失败），其中 #157107、#157011、#157234、#153067、#134925 已关闭，显示维护者正在快速收敛 P0 缺陷。
- **PR 积压高企**：393 条待合并 PR 对约 107 条已合并/关闭，合并比约 1:3.7，审查吞吐是当前最大的项目瓶颈。
- **整体健康度评估**：功能面稳定但运维面承压；社区反馈密度极高说明用户基数和使用强度上升，但需警惕 P0 缺陷反复出现对发布信心的侵蚀。

---

## 2. 版本发布

本周期无新版本发布（Release 数量为 0），项目处于 2026.9.6 后的修复阶段。维护者已开设 2026.9.7 修复跟踪台账（[#157531](https://github.com/openclaw/openclaw/issues/157531)），对 1,058 个主线提交进行审计，暗示下一个补丁版本将以稳定性修复为主。

---

## 3. 项目进展

今日已关闭的 P0/重要 Issue（问题侧收敛信号）：

| 编号 | 标题 | 状态 |
|---|---|---|
| [#157107](https://github.com/openclaw/openclaw/issues/157107) | 2026.9.6 prepared-model-catalog worker 每 ~6s 重建插件 generation，agent 永不被放行 | ✅ CLOSED |
| [#157011](https://github.com/openclaw/openclaw/issues/157011) | 2026.9.5→9.6 托管更新总是回滚（RangeError: Maximum call stack size exceeded） | ✅ CLOSED |
| [#157234](https://github.com/openclaw/openclaw/issues/157234) | 更新恢复因 `agent-database-lease-active` 失败 | ✅ CLOSED |
| [#153067](https://github.com/openclaw/openclaw/issues/153067) | 网关稳态下每 ~5s 重拷整个状态 DB（~170MB/次，~5.9TB/天写入） | ✅ CLOSED |
| [#134925](https://github.com/openclaw/openclaw/issues/134925) | ARM64/Pi 上网关主线程每次 agent turn 跑到 ~100% CPU | ✅ CLOSED |

**进展判断**：今日最重要的进展是**模型目录（catalog）相关 P0 的整链收敛**——#157107 与 #155753、#156191、#156571 同属一条故障链，配套 PR [#157300](https://github.com/openclaw/openclaw/pull/157300)（验证 catalog capture 复用）已就绪待审，说明该类问题已从"定位"进入"修复+回归防护"阶段。同时，状态数据库快照风暴（#153067）关闭，意味着网关 IO 放大问题取得实质进展。整体项目在"运维性能与升级可靠性"方向上向前迈进了明显一步，但尚未转化为可供用户直接安装的版本。

---

## 4. 社区热点

**讨论最活跃的 Issues（按评论数）**

1. [#155753（23 评论）](https://github.com/openclaw/openclaw/issues/155753) — **Model-catalog 过期/重建循环烧掉一整个 CPU 核心**。`readFullModelCatalog()` 每次读取都触发 `refreshExpiredCatalog()`，配合 ~60s 的目录 TTL 形成无限重建。该问题关联 #154276/#153422，与今日关闭的 #157107 同源，是本周最受关注的技术议题。
2. [#112423（20 评论）](https://github.com/openclaw/openclaw/issues/112423) — **大型 SQLite 转录清理阻塞网关事件循环**。会话清理期间在网关线程上做全量物化、压缩、持久化 IO 与回读，属于典型的"重活跑在主线程"。自 7 月挂起至今仍未解决，用户呼声持续走高。
3. [#142585（17 评论）](https://github.com/openclaw/openclaw/issues/142585) — **Doctor 拒绝合法旧版工作区迁移（P0 回归）**。从 2026.7.1-2 升级到 9.3 时，Doctor 能识别旧状态却拒绝迁移，属于升级阻断级问题。
4. [#97616（16 评论，1 👍）](https://github.com/openclaw/openclaw/issues/97616) — **hook/tool 子进程未回收，僵尸堆积导致运行时劣化**。长期未修复的回归问题。
5. [#137332（16 评论）](https://github.com/openclaw/openclaw/issues/137332) — **混合 terminal requester-settle 批次在所有权检查后永久重试**。
6. [#98435（14 评论，1 👍）](https://github.com/openclaw/openclaw/issues/98435) — **网关重启后 MCP loopback 传输不自动重连，`recovered=1` 具有误导性**。涉及安全审查，修复路径复杂。
7. [#157531（11 评论）](https://github.com/openclaw/openclaw/issues/157531) — 2026.9.7 修复跟踪台账，维护者主动索引问题全景。

**诉求背后的共性**：社区讨论高度集中于**"长期运行 + 大规模部署下的资源放大"**——CPU 被目录重建吃满、DB 被反复全量拷贝、事件循环被同步 IO 阻塞、子进程泄漏。这不是单点 bug，而是架构层面的"大安装可用性"问题。

---

## 5. Bug 与稳定性

### P0（发布阻断 / 崩溃 / 数据风险）

| 编号 | 问题 | 是否有修复 PR |
|---|---|---|
| [#142585](https://github.com/openclaw/openclaw/issues/142585) | Doctor 拒绝合法旧版工作区与 attestation 迁移（回归） | ❌ 无新修复 PR，待维护者评审 |
| [#152275](https://github.com/openclaw/openclaw/issues/152275) | 插件提交后激活失败，模型目录与回复分发不可用直至重启 | ❌ 待 live repro |
| [#148307](https://github.com/openclaw/openclaw/issues/148307) | 会话回收超过 5s busy timeout，agent DB `database is locked` | ❌ 待补充信息 |
| [#151467](https://github.com/openclaw/openclaw/issues/151467) | 自升级死锁 + 回滚 cron 失败（v6.33→v9.4） | ❌ 待补充信息 |
| [#137177](https://github.com/openclaw/openclaw/issues/137177) | 内置 `@wecom/wecom-openclaw-plugin@2026.7.2` 无法安装 | ❌ 无修复 PR |
| [#115256](https://github.com/openclaw/openclaw/issues/115256) | 桌面 App 令网关反复重启（实测 32s~727s） | ❌ 待 live repro |
| [#152252](https://github.com/openclaw/openclaw/issues/152252) | 配置写入 `meta.migrations.utilityModelSeparation` 致旧版网关启动硬失败（exit 78） | ❌ 无修复 PR |
| [#117742](https://github.com/openclaw/openclaw/issues/117742) | 多文件 `apply_patch` 失败后仍提交了先前的删除操作（数据丢失风险） | ❌ 无修复 PR |
| [#155859](https://github.com/openclaw/openclaw/issues/155859) | 2026.9.5 网关启动墙钟时间随启用插件数线性增长（120s 预算被占满） | ❌ 无修复 PR |
| [#157415](https://github.com/openclaw/openclaw/issues/157415) | `Doctor --fix` 拒绝外部安装 acpx/codex 的会后迁移 | ❌ 需手动复现 |

### P1（功能受损 / 消息丢失 / 会话状态异常）

- [#112423](https://github.com/openclaw/openclaw/issues/112423) 大 SQLite 转录清理阻塞事件循环（20 评论，长期未解）。
- [#97616](https://github.com/openclaw/openclaw/issues/97616) 子进程僵尸堆积致运行时劣化。
- [#137332](https://github.com/openclaw/openclaw/issues/137332) requester-settle 批次永久重试。
- [#98435](https://github.com/openclaw/openclaw/issues/98435) MCP loopback 不自动重连。
- [#118885](https://github.com/openclaw/openclaw/issues/118885) 单次启动重复执行多轮 SQLite 完整性检查。
- [#157067](https://github.com/openclaw/openclaw/issues/157067) Windows 隔离 cron 传递不可 clone 的 environment Proxy —— **已有开放 PR（linked-pr-open）**。
- [#118839](https://github.com/openclaw/openclaw/issues/118839) "restart recovery claim changed before agent adoption" 回归。
- [#145309](https://github.com/openclaw/openclaw/issues/145309) claude-cli 后端忽略 `CLAUDE_CONFIG_DIR` —— **已有开放 PR**。
- [#121661](https://github.com/openclaw/openclaw/issues/121661) CLI 子代理 announce-wake 轮次无工具运行，模型伪造工具调用。
- [#129314](https://github.com/openclaw/openclaw/issues/

---

## 横向生态对比

# 横向对比分析报告：个人 AI 助手 / 自主智能体开源生态（2026-09-25）

> **数据边界说明**：本次输入中仅 OpenClaw 提供完整社区动态；Hermes Agent 摘要生成失败，无 Issues、PR、Release、健康度等可验证数据。因此下文定量分析以 OpenClaw 为核心锚点，Hermes Agent 仅能做“数据缺失”标注，不做推测。真正的多项目横向对比需补齐 Hermes 数据。

---

## 1. 生态全景

个人 AI 助手 / 自主智能体开源生态仍处高速扩张期，功能迭代速度普遍快于生产化治理速度。以 OpenClaw 为样本看，社区反馈已从“功能有没有”转向“长期运行稳不稳、升级可不可靠、资源消耗能不能扛”。当前核心矛盾集中在模型目录缓存、SQLite/状态 DB、网关主线程、插件启动成本与升级迁移链路。插件和工具生态扩大了能力边界，也放大了启动耗时、子进程泄漏和 IO 放大问题。整体判断：生态正在从“可用”进入“大规模长稳部署”的阵痛期，质量巩固与运维性能将成为下一阶段竞争点。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新（24h） | PR 更新（24h） | Release | 关键状态 | 健康度评估 |
|---|---:|---:|---:|---|---|
| **OpenClaw** | 500（新开/活跃 444，关闭 56） | 500（待合并 393，合并/关闭 107） | 0；处于 2026.9.6 → 2026.9.7 修复窗口 | Issues 前 50 中至少 8 条 P0、18 条 P1；合并比约 1:3.7 | 功能面稳定，运维面承压；高活跃、高积压；P0 正在快速收敛 |
| **Hermes Agent** | 摘要生成失败 | 摘要生成失败 | 摘要生成失败 | 无可用数据 | 无法评估 |

**OpenClaw 关键补充**：已关闭多条 P0，包括模型目录重建循环 #157107、托管更新回滚 #157011、状态 DB 每 5 秒全量拷贝 #153067、ARM64/Pi 主线程 100% CPU #134925。维护者已建立 2026.9.7 修复跟踪台账 #157531，审计 1,058 个主线提交，说明项目正从“故障定位”转入“修复+回归防护”。

---

## 3. OpenClaw 在生态中的定位

**优势**
- **社区反馈强度极高**：24h 内 Issues/PR 各更新 500 条，热点 Issue 评论数达 20+，说明用户基数大、部署规模大、使用强度高。
- **问题收敛机制存在**：P0 关闭速度较快，且有修复跟踪台账与配套 PR，如 #157300 验证 catalog capture 复用。
- **功能覆盖完整**：涉及网关、插件、模型目录、SQLite 状态 DB、Doctor 迁移、cron、MCP、CLI/桌面端，属于典型“个人 AI 助手运行时”全栈项目。

**技术路线特征**
OpenClaw 呈现“重网关 + 插件生态 + 本地状态 DB + 模型目录 + 多后端/子进程”的架构画像。其稳定性问题并非单点 bug，而是长期运行下的资源放大：CPU 被目录重建吃满、DB 被反复全量拷贝、事件循环被同步 IO 阻塞、插件数导致启动耗时线性增长。

**社区规模对比**
在可获得数据中，OpenClaw 是唯一具备大规模社区动态样本的项目。Hermes Agent 数据缺失，无法比较社区规模。因此只能判断：OpenClaw 在当前样本中属于高活跃、高压力、进入质量巩固期的核心参照项目。

---

## 4. 共同关注的技术方向

> 受 Hermes Agent 数据缺失影响，以下为 OpenClaw 暴露出的、对生态具普遍参考价值的方向；多项目交叉验证暂不可完成。

| 技术方向 | 涉及项目 | 具体诉求 / 风险 |
|---|---|---|
| 模型目录与缓存生命周期 | OpenClaw | `readFullModelCatalog()` 触发过期重建，形成无限循环，烧掉整个 CPU 核；#155753、#157107 |
| SQLite / 状态 DB IO 放大 | OpenClaw | 每 ~5s 全量拷贝 ~170MB DB，约 5.9TB/天写入；大转录清理阻塞事件循环；#112423、#153067 |
| 网关主线程与启动性能 | OpenClaw | 插件数增加导致启动墙钟时间线性增长，120s 预算被占满；ARM64/Pi 每 turn 跑满 CPU；#155859、#134925 |
| 升级、迁移与回滚可靠性 | OpenClaw | Doctor 拒绝合法旧版迁移、自升级死锁、回滚 cron 失败、旧版网关启动 exit 78；#142585、#151467、#152252 |
| 插件 / 子进程生命周期 | OpenClaw | 子进程僵尸堆积、插件激活失败、内置插件无法安装；#97616、#152275、#137177 |
| MCP 与恢复语义可信度 | OpenClaw | 网关重启后 MCP loopback 不自动重连，`recovered=1` 具误导性；#98435 |

**结论**：当前生态级共性问题不是“模型能力不足”，而是“运行时资源治理不足”。谁先解决长稳、升级和插件启动成本，谁更可能获得生产部署信任。

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
|---|---|---|
| 功能侧重 | 完整个人 AI 助手运行时：网关、插件、模型目录、DB、Doctor、cron、MCP、CLI/桌面 | 数据缺失 |
| 目标用户 | 大规模、长期运行、插件化部署用户；从 Issues 密度可推断部署强度高 | 数据缺失 |
| 技术架构 | 网关 + 插件 + SQLite 状态 DB + 模型目录 + 子进程/多后端 | 数据缺失 |
| 成熟度阶段 | 功能面稳定，处于质量巩固与运维性能修复窗口 | 数据缺失 |
| 主要风险 | 资源放大、升级回归、PR 审查积压 | 无法判断 |

因此，本次无法做真正意义上的“OpenClaw vs Hermes”差异化对比。唯一可确定的是：OpenClaw 已进入大规模部署后的稳定性治理阶段，而 Hermes Agent 的定位、架构和阶段均待补充。

---

## 6. 社区热度与成熟度

**OpenClaw：高活跃 + 质量巩固期**
- 24h Issues 500、PR 500，社区热度极高。
- P0/P1 密集，但已关闭多条关键 P0，说明维护者响应速度尚可。
- 待合并 PR 393，已合并/关闭 107，审查吞吐是最大瓶颈。
- 无新 Release，处于 2026.9.6 后密集修复窗口，成熟度表现为“功能稳定、运维承压”。

**Hermes Agent：无法分层**
- 摘要生成失败，不能判断其处于快速迭代、质量巩固还是早期原型阶段。

**生态分层建议**
在现有数据下，OpenClaw 可归入“高活跃、大规模部署压力、质量巩固期”一档。若补齐 Hermes 数据，可按 Issues/PR 比、P0 密度、Release 节奏、评论集中度进一步划分快速迭代区与质量巩固区。

---

## 7. 值得关注的趋势信号

1. **Agent 运行时的资源放大成为头号稳定性问题**  
   目录 TTL、DB 全量拷贝、主线程同步 IO、子进程泄漏，都会在长期运行中变成 TB 级写入或满核 CPU。开发者需将资源预算纳入核心指标。

2. **升级/迁移/回滚必须作为一等公民测试**  
   Doctor 拒绝迁移、自升级死锁、回滚失败会直接阻断发布信心。建议把跨版本升级路径纳入 CI。

3. **插件生态需要启动隔离与懒加载**  
   插件数导致启动时间线性增长，说明架构上缺少启动预算和依赖隔离。插件沙箱、懒加载、缓存复用会成为刚需。

4. **可观测性语义必须准确**  
   `recovered=1` 误导式状态会影响安全审查和故障判断。恢复、重连、降级状态需要可审计

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ 摘要生成失败。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*