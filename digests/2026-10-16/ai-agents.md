# OpenClaw 生态日报 2026-10-16

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-10-16 02:55 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 · 2026-10-16

> 数据来源：github.com/openclaw/openclaw · 统计窗口：2026-10-15 ~ 2026-10-16

---

## 1. 今日速览

- **整体活跃度极高**：过去 24 小时 Issues 更新 500 条（新开/活跃 407、关闭 93），PR 更新 500 条（待合并 205、合并/关闭 295），单日合并/关闭率约 59%，符合健康的大型开源项目节奏。
- **稳定性是当前主线**：P0 级问题（SQLite WAL 失控增长、Gateway 内存泄漏、插件捕获阻塞事件循环）仍集中在数据库与 Gateway 生命周期，但今日 4 个版本中有 3 个直接指向「更快、更稳的 Gateway」与「更可靠地完成更新」，说明核心团队正在集中火力收敛这些语义。
- **UI 架构迁移成片推进**：多个由 @steipete 主导的 PR 正系统性把 Control UI 从 Lit 迁移到 Solid，同时消除冗余适配层与渲染抖动，是今日 PR 流最显著的技术方向。
- **跨平台信任边界收尾**：Slack / Discord 的 `user:<id>` 命令所有者识别、更新失败误报等一批「安全边界 + 终端体验」PR 进入待合并状态，指向下一个稳定版的发布候选。
- **长尾积压风险显现**：3~4 月提交的多个 P0/P1 Issue 仍处 `stale` 状态（详见第 8 节），需维护者主动排期。

**健康度评估：🟢 活跃且方向聚焦**。发布节奏、合并吞吐、主线收敛三者同时在线，但「数据库/WAL 系列」问题连续两周霸榜评论数前列，是唯一值得警惕的信号。

---

## 2. 版本发布

今日共发布 4 个版本，覆盖 3 条发布轨道（beta 前瞻、稳定、extended-stable/LTS）。

### v2026.10.10-beta.1（前瞻 beta）
- **核心主题：更快的 Gateway**。聊天轮次、会话列表、启动流程与空闲态 Gateway 显著减少 SQLite 与主线程工作量，更多数据库操作被迁移到 worker 线程。
- **用户价值**：在多代理（agent fleet）与高负载宿主机上保持响应性——直接回应了长期存在的「单次会话阻塞整个 Gateway 事件循环」类反馈（如 #160959、#84983）。
- **关联 PR**：#167965、#168002、#168093 等。
- 链接：https://github.com/openclaw/openclaw/releases

### v2026.10.5-beta.4（beta）
- **核心主题：更新流程更可靠**。修复 macOS 在别名临时目录下更新超时；systemd 用户级安装可回收废弃运行时；pacman 与 FreeBSD 包安装交由各自包管理器处理；快照失败可在更早阶段被识别。
- **迁移注意**：包管理器托管场景（pacman / FreeBSD）行为有变更，升级脚本不应再假设 OpenClaw 自行接管包文件。
- 链接：https://github.com/openclaw/openclaw/releases

### v2026.10.4（稳定）
- **关键修复**：计算机休眠或系统时钟跳变后 Gateway 不再因「所有权心跳过期」而自我重启（#170790）。
- **其他**：Gateway 关闭/重启不再挂起。
- **破坏性变更**：数据中未体现。
- **致谢**：@AnvinaLI、@sgh6688、@waynegault、@RomneyDa。
- 链接：https://github.com/openclaw/openclaw/releases

### v2026.9.33（extended-stable / LTS 等效）
- **定位**：gateway-only 长期支持轨道，基线为 2026 年 9 月末的 OpenClaw，叠加关键安全更新、可靠性与性能修复，以及新模型支持。
- **建议**：生产环境若追求最小变更风险，应优先停留此轨道；功能尝鲜走 beta 轨道。
- 链接：https://github.com/openclaw/openclaw/releases

> ⚠️ 注：数据中的 Release 说明均被截断，以上内容基于可见片段归纳；完整说明请以官方 Release 页面为准。

---

## 3. 项目进展

今日合并/关闭 PR 共 **295 条**，其中可直接追溯到高价值 commits 的方向如下：

| 方向 | 代表 PR | 推进内容 |
|---|---|---|
| **UI 架构迁移（Lit → Solid）** | [#171664](https://github.com/openclaw/openclaw/pull/171664)、[#173629](https://github.com/openclaw/openclaw/pull/173629)、[#173630](https://github.com/openclaw/openclaw/pull/173630)、[#173627](https://github.com/openclaw/openclaw/pull/173627)、[#173337](https://github.com/openclaw/openclaw/pull/173337) | 将表现层契约与 Lit 解耦、聊天输入框直接以 Solid 渲染、移除冗余适配器，减少「双框架并存」的维护成本 |
| **UI 性能与体验打磨** | [#173282](https://github.com/openclaw/openclaw/pull/173282)、[#173681](https://github.com/openclaw/openclaw/pull/173681)、[#173679](https://github.com/openclaw/openclaw/pull/173679)、[#173673](https://github.com/openclaw/openclaw/pull/173673) | 修复侧边栏插画在实时更新中反复重绘（曾观测到 5 秒内 3800+ 次 DOM 变更）、Recent Chats 时间戳换行、Share 按钮错位、插件主题背景可见度 |
| **Gateway / 会话性能** | [#173677](https://github.com/openclaw/openclaw/pull/173677)、[#173674](https://github.com/openclaw/openclaw/pull/173674)、[#173678](https://github.com/openclaw/openclaw/pull/173678) | 信任内部 transcript 帧、跳过冗余深冻结、避免子代理恢复时的重复读取 |
| **数据库引擎抽象** | [#173462](https://github.com/openclaw/openclaw/pull/173462) | Agent 数据库统一通过「选定引擎」打开，为 PostgreSQL 后端铺路——这是 10.x 系列最关键的基础设施变更之一 |
| **状态一致性** | [#173671](https://github.com/openclaw/openclaw/pull/173671)、[#173214](https://github.com/openclaw/openclaw/pull/173214) | 数据库隔离后拒绝缓存读取；`chat.message.get` 返回存储的压缩摘要，让客户端能展示「代理还记得什么」 |
| **更新器健壮性** | [#173593](https://github.com/openclaw/openclaw/pull/173593)、[#173569](https://github.com/openclaw/openclaw/pull/173569) | 通道不可用（`/readyz` 503）时误报更新失败；瞬时 Git 下载错误自动重试一次 |
| **安全边界** | [#172424](https://github.com/openclaw/openclaw/pull/172424)、[#172385](https://github.com/openclaw/openclaw/pull/172385)、[#160364](https://github.com/openclaw/openclaw/pull/160364) | Slack / Discord 正确识别 `user:<id>` 形式的命令所有者；日志脱敏保留非密钥环境变量引用 |
| **跨通道 / 扩展** | [#170534](https://github.com/openclaw/openclaw/pull/170534)、[#173580](https://github.com/openclaw/openclaw/pull/173580)、[#173665](https://github.com/openclaw/openclaw/pull/173665) | 严格遵守精确 `NO_REPLY` 语义、不再伪造结束性回复；Codex 会话交接后 Stop 导致的下一轮停滞；直接运行 `migrate codex` 时能发现插件清单 |

**已关闭的重要 Issue**（标志问题闭环）：
- [#164113](https://github.com/openclaw/openclaw/issues/164113) P0：非特权 LXC 容器内更新因 FICLONE EPERM 失败 —— CLOSED
- [#121617](https://github.com/openclaw/openclaw/issues/121617) P0：压缩后「Already compacted」守卫误判 —— CLOSED
- [#84037](https://github.com/openclaw/openclaw/issues/84037) Codex app-server 稳态 CPU 与辅助进程开销 —— CLOSED
- [#71058](https://github.com/openclaw/openclaw/issues/71058) 单 Gateway 支持多个 Azure/Teams Bot —— CLOSED
- [#77298](https://github.com/openclaw/openclaw/issues/77298) Cron `consecutiveErrors` 被重启中断污染 —— CLOSED

**整体推进幅度：约 60% 的 PR 在本窗口内闭环**，且合并内容高度集中在「性能收敛 + UI 单向迁移 + 更新器健壮性」三条主线，属于典型的稳定版发布前的收口阶段。

---

## 4. 社区热点

按评论数排序的今日焦点：

**① [#143524](https://github.com/openclaw/openclaw/issues/143524) — Agent SQLite WAL 无界增长（128 条评论）** 🔥 全场最高
Windows 单 Gateway 宿主机上，某 agent 的 `openclaw-agent.sqlite-wal` 数天内涨至 **2865 MB**，手动 `wal_checkpoint(TRUNCATE)` 归零后又迅速反弹，最终阻塞 Gateway 启动。标签含 `P0`、`impact:message-loss`、`impact:crash-loop`、`ux-release-blocker`。
> 这是今日唯一评论破百的议题，且已从 9 月 9 日持续到 10 月 16 日仍未闭环。诉求指向 WAL 自动检查点策略在 Windows 上存在系统性缺陷。

**② [#91588](https://github.com/openclaw/openclaw/issues/91588) — Gateway 内存泄漏 350MB → 15.5GB（40 条评论，👍1）**
2~3 天正常使用后 RSS 膨胀至 15.5 GB，触发 launchd-handoff 反复重启。`P0` + `impact:crash-loop` + `maturity:stable`——说明稳定轨道同样受影响。

**③ [#160959](https://github.com/openclaw/openclaw/issues/160959) — 大型外部插件捕获导致 Gateway 阻塞数分钟（25 条评论）**
2026.9.6 引入插件生成捕获后的回归，启动时与模型运行时重新发布时都会阻塞事件循环。`P0`、`diamond lobster` 评分。

**④ [#148707](https://github.com/openclaw/openclaw/issues/148707) — 回复丢失「no active tool authority snapshot」（20 条评论）**
同一会话中第二次运行顶替进行中的轮次时，被打断的轮次回复**完全丢失**（无重试、无部分交付）。`P1`、`impact:message-loss`。

**⑤ [#164294](https://github.com/openclaw/openclaw/issues/164294) — Gateway 状态库 WAL 自动检查点从未完成（18 条评论）**
与 #143524 同源但作用于 `state/openclaw.sqlite`：检查点被进程内 reader 永久钉住，`consecutiveBlocked` 持续累积。

**⑥ [#157989](https://github.com/openclaw/openclaw/issues/157989) — 插件源码捕获造成严重 SSD 磨损（18 条评论）**
每条 CLI 命令重写约 1.1–1.4 GB，每次 Gateway 启动约 6.5 GB（含体积较大的原生二进制）。`P1`、「回归」+「beta 发布阻断」。

**⑦ [#87744](https://github.com/openclaw/openclaw/issues/87744) — Codex 驱动的 Telegram 轮次反复超时（18 条评论，👍4）**
`turn/completed` 永不抵达，

---

## 横向生态对比

# 横向对比分析报告：个人 AI 助手 / 自主智能体开源生态  
**统计窗口：2026-10-15 ~ 2026-10-16**  
样本：OpenClaw、Hermes Agent。部分原始摘要被截断，以下结论限于可见数据。

---

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正从“功能扩张”转向“运行时稳定性、跨平台可靠性与安全边界”竞争。  
Gateway / 会话所有权成为核心架构命题：谁能稳定拥有会话、消息、插件与存储状态，谁就掌握平台入口。  
共同故障面高度集中：SQLite/WAL、Gateway 内存与生命周期、插件授权、更新安装、消息投递。  
成熟项目进入发布收口与 LTS 轨道，架构迁移项目进入 post-merge 债务清算期。  
社区开始出现“用 agent 管理 agent 自身技术债”的自举实践，Hermes 的分包修复是典型信号。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release 情况 | 关键指标 | 健康度评估 |
|---|---:|---:|---|---|---|
| **OpenClaw** | 500 条：新开/活跃 407，关闭 93 | 500 条：待合并 205，合并/关闭 295 | 4 个版本：beta、稳定、extended-stable/LTS | PR 合并/关闭率约 **59%**；Issues 关闭率约 **19%**；P0 集中在 WAL、Gateway 内存泄漏、插件阻塞 | 🟢 活跃且方向聚焦，发布前收口；DB/WAL 是主要风险 |
| **Hermes Agent** | 50 条：新开/活跃 47，关闭 3 | 50 条：待合并 41，合并/关闭 9 | v0.22.2，修复 v0.22.1 错误构建与 Microsoft Store 卡 “Connecting” | PR 合并/关闭率约 **18%**；Issues 关闭率约 **6%**；统一网关 post-merge 追踪 74 评论 | 🟡 高强度修复期，架构收益大但稳定性债务集中释放 |

**结论**：OpenClaw 规模约 10 倍于 Hermes，合并吞吐约 30 倍；Hermes 单位问题讨论强度高，但当前处于“问题沉积快于清理”的阶段。

---

## 3. OpenClaw 在生态中的定位

**优势**
- **规模与吞吐领先**：单日 Issues / PR 更新各 500 条，合并/关闭 295 条 PR，远高于 Hermes 的 9 条。
- **发布工程成熟**：同时维护 beta、稳定、extended-stable/LTS 三条轨道，已有 v2026.9.33 LTS 等效版本。
- **平台化能力强**：覆盖 Control UI、Gateway、插件系统、更新器、Slack/Discord/Teams/Codex 等跨通道。
- **社区讨论深度大**：SQLite WAL 问题 #143524 达 128 条评论，是当日全生态最高热点。

**技术路线差异**
- OpenClaw 正系统性推进 **Control UI 从 Lit 迁移到 Solid**，

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 · 2026-10-16

---

## 1. 今日速览

- **项目处于"大合并后稳定化"的高强度修复期**：统一网关 PR #106742（`feat/unified-gateway-runtime`）于 10 月 14 日合入 `main`，两天来社区围绕其 post-merge 问题产生了大量追踪与修复活动，过去 24 小时 Issues 更新 50 条、PR 更新 50 条，活跃度处于极高水平。
- **Issue 侧以"新开/活跃"为主（47/50）**，关闭仅 3 条，说明问题沉积速度仍快于清理速度；PR 侧待合并 41 条、已合并/关闭 9 条，合并率约 18%，积压明显。
- **核心贡献者 `unsupportedpastels` 主导了网关修复的"分包"工作**：将 #134889 的 post-merge 发现拆成 4 个可并行领取的 issue（#139158–#139162，合计约 62 项发现），并已提交多条对应修复 PR。
- **v0.22.2 发布**，属于对 v0.22.1 错误构建的补救版本，主要解决 Microsoft Store 应用卡在 "Connecting" 的问题，但版本日期显示与 0.22.1 网关会话状态等**已知遗留问题仍未完全收敛**。
- 整体健康度评价：**架构演进收益大，但当前稳定性债务集中释放，建议维护者优先消化 P0/P1 与网关分包清单**。

---

## 2. 版本发布：v0.22.2

**Hermes Agent v0.22.2**（发布日期：2026-10-15）

### 更新内容

- **v0.22.1 是从错误的 commit 构建的**，意外发布了尚未发布的网关（gateway）工作内容。
- **Microsoft Store 应用可能卡在 "Connecting" 状态**——这是 0.22.1 的核心用户可见故障。
- 0.22.2 是 0.22.1 "本应成为的版本"，即回退/修正了错误构建引入的内容。

### 破坏性变更与迁移注意事项

- **已知问题**：在 **0.22.1 网关（gateway）下运行过的会话**存在遗留问题（release notes 原文在此处被截断，未给出完整描述）。建议从 0.22.1 升级的用户**检查既有会话状态**，尤其是会话恢复、消息投递链路。
- 由于 0.22.1 曾被描述为"shipped unreleased gateway work"，从 0.22.1 回退到 0.22.2 的用户需注意**网关侧会话状态与本地状态可能不一致**，与今日多条 gateway/session 相关 Bug（#139002、#139536、#139564）互为印证。

### 补充提示（非本 release 直接内容，但今日高频出现）

- `hermes --version` 与启动横幅中的**发布日期仍冻结为 `2026.9.24`**（`hermes_cli.__release_date__`），导致 0.22.2 显示为 `v0.22.2 (2026.9.24)`，易被用户误读为版本陈旧。相关 Issue #135217 仍处于 OPEN。

---

## 3. 项目进展

今日共 9 条 PR 被合并/关闭，其余 41 条待合并。值得注意的是，**今日未见新的大功能落地 PR**，进展集中于"修复 + 抢救（salvage）+ 分包"。

### 已关闭的 PR

| PR | 内容 | 意义 |
|---|---|---|
| [#138598](https://github.com/NousResearch/hermes-agent/pull/138598) | `fix(desktop)`: 在附件预览前解析 Windows shell 路径（Git Bash 风格 `MEDIA:/c/Users/...`） | 修复 Electron 将 `/c/...` 误走 WSL 回退导致附件被判缺失；改善 Windows 桌面端体验 |
| [#139566](https://github.com/NousResearch/hermes-agent/pull/139566) | `fix(wecom)`: 停止因 stale `req_id` 丢消息，并加入主动重试（salvage #129074） | 抢救了自 2026-10-02 起一直 `CONFLICTING` 的停滞 PR，覆盖两类仍在真实环境中静默丢消息的故障 |

### 今日关闭的 Issues

- [#137646](https://github.com/NousResearch/hermes-agent/issues/137646) `[CLOSED]` `hermes update` 在 release commit 非本地时拒绝 stable 渠道（10 秒 ancestry 探针超时）——安装/更新链路的重要修复闭环。
- [#139514](https://github.com/NousResearch/hermes-agent/issues/139514) `[CLOSED]` `__release_date__` 冻结问题，以 **duplicate** 关闭，与 #135217 归并。
- [#138908](https://github.com/NousResearch/hermes-agent/issues/138908) `[CLOSED]` `groups.log` 违反 wire contract，`RoomActor` 缺失 `profile`/`display_name`/`connection_id`，导致每次调用触发契约校验失败。

### 推进中的关键修复（待合并）

- **网关分包修复**（由 #134889 派生，`unsupportedpastels` 提交，含配图）：
  - [#139577](https://github.com/NousResearch/hermes-agent/pull/139577) 配置与新 MCP server 以"已提交策略代际"形式下发到恢复的会话（package 5 · lane 5）
  - [#139576](https://github.com/NousResearch/hermes-agent/pull/139576) 新建本地会话读取 profile 的当前配置（lane 4）
  - [#139575](https://github.com/NousResearch/hermes-agent/pull/139575) 经典 CLI 插件命令改在网关内执行，disable 能触达运行中的网关（lane 3）
  - [#139570](https://github.com/NousResearch/hermes-agent/pull/139570) 插件 hook 每消息只触发一次，插件注入不越出所属 profile（lane 2）
  - [#139569](https://github.com/NousResearch/hermes-agent/pull/139569) 插件 websocket 统一走一个授权闸门；本地网关上的 Desktop 插件 socket（lane 1，含安全边界标签）
- **P0 修复**：[#139537](https://github.com/NousResearch/hermes-agent/pull/139537) `/reasoning` 会话中途切换时保留 prompt cache（OpenAI Responses / Codex / Claude），为 #129233 的 salvage，并整合了 #114534、#118932。
- **其他**：[#139572](https://github.com/NousResearch/hermes-agent/pull/139572) `hermes doctor` 在网关进程或 A2A 端口宕机时改为失败；[#139579](https://github.com/NousResearch/hermes-agent/pull/139579) 修复 bootstrap-installer 的 `__dirname` 未定义问题。

**整体推进幅度评估**：项目完成了一次统一网关架构的大型迁移（#106742），当前正处于**"收益已落袋、债务待偿还"**阶段。今日净进展主要体现为约 62 项发现的**归类与首批修复落地**，属结构性推进而非功能扩张。

---

## 4. 社区热点

### 🔥 最活跃：统一网关 post-merge 追踪（74 评论）

- [#134889](https://github.com/NousResearch/hermes-agent/issues/134889) `[OPEN]` `Tracking: one gateway owns every local session (#106742) — post-merge fixes`
  作者 `unsupportedpastels`｜创建 2026-10-08｜更新 2026-10-16｜**74 条评论**
  标签覆盖几乎所有核心组件：`comp/agent`、`comp/cli`、`comp/gateway`、`comp/tui`、`comp/acp`、`comp/cron`、`comp/desktop`、`platform/windows`，并带多条 `sweeper:risk-*` 风险标记（session-state、message-delivery、compatibility、platform-windows）。
  **诉求分析**：这是当前项目的"单一事实中心"。PR #106742 于 10 月 14 日合入 `main`（merge commit `eb75627f`），其目标——**让所有面向本地会话的入口面（surface）都由同一个网关统一拥有**——是一次架构级重构。高评论量反映的正是重构后跨组件契约不一致的集中暴露。

### 分包执行（为 #134889 提供的"可领取工作包"）

| Issue | 范围 | 发现数 |
|---|---|---|
| [#139158](https://github.com/NousResearch/hermes-agent/issues/139158) | 经典 CLI（`hermes chat`）作为共享网关客户端：切换/恢复会话 | 16 |
| [#139160](https://github.com/NousResearch/hermes-agent/issues/139160) | 会话创建、模型选择与凭据（`session.create` 拒绝、model/provider 路由） | 17 |
| [#139161](https://github.com/NousResearch/hermes-agent/issues/139161) | Ink TUI 与 Desktop 会话、命令、实时事件（19 项，有 👍） | 19 |
| [#139162](https://github.com/NousResearch/hermes-agent/issues/139162) | 消息机器人、cron 与 Kanban workers 的"非本地查看者"回合 | 10 |

**诉求分析**：维护者显式采用"一个人 + 子智能体即可领取整包"的组织方式，说明项目在**用 Hermes 自身（delegate/sub-agent）来消化自身的技术债**，这本身是一个值得关注的自举实践信号。

### 其他热点

- [#137646](https://github.com/NousResearch/hermes-agent/issues/137646)（8 评论，已关闭）`hermes update` stable 渠道 ancestry 探针超时——**安装/升级可用性**是用户最敏感的触点之一。
- [#28024](https://github.com/NousResearch/hermes-agent/issues/28024)（7 评论）白名单化的 `config_set` 工具，让 agent 能自我配置——社区对**agent 自主性边界**的讨论持续升温。
- [#135217](https://github.com/NousResearch/hermes-agent/issues/135217)（6 评论，👍1）版本横幅显示陈旧日期——典型的"小问题、高频可见"。
- [#139303](https://github.com/NousResearch/hermes-agent/issues/139303)（6 评论）Bot Mode DM 中 `asyncio.run()` 在已有事件循环的同步工具处理器里被调用，消息在拨号前即失败，并被**误判为"ambiguous / do not resend"**——这是一个会造成消息静默丢失的复合故障。
- [#89199](https://github.com/NousResearch/hermes-agent/issues/89199)（6 评论）CLI 对 `~/.hermes/.env` 中确实存在的 `${env:VAR}` 误报警告——长期存在（自 8 月 18 日）的用户困扰。

---

## 5. Bug 与稳定性

按严重程度排列（含是否已有 fix PR）：

### 🔴 P0

- **`/reasoning` 中途切换导致 prompt cache 失效**（OpenAI Responses、Codex、Claude）
  已有修复：[PR #139537](https://github.com/NousResearch/hermes-agent/pull/139537)（salvage #129233，整合 #114534、#118932），标签 `sweeper:risk-caching`、`sweeper:risk-session-state`。
  影响：缓存命中失效直接推高成本与延迟，属体验与成本双重回归。

### 🟠 P1

- **网关统一化后的会话状态与消息投递风险**：[#134889](https://github

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*