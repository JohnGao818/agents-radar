# OpenClaw 生态日报 2026-06-20

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-20 02:56 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-06-20

---

## 1. 今日速览

过去 24 小时内，OpenClaw 项目保持了极高的活跃度：共处理 500 条 Issue 更新（其中新开/活跃 452 条，关闭 48 条）和 500 条 PR 更新（待合并 457 条，合并/关闭 43 条），并发布了 v2026.6.9-beta.1 预览版。社区对 Telegram 体验、会话隔离、内存泄漏等关键问题的讨论热烈，多个 P0/P1 级 Bug 持续引发维护者关注；同时，大量涉及 SDK 类型对齐、Ollama / Telegram 客户端修复的小型 PR 正在快速提交，项目整体处于高强度的迭代周期，健康度良好但稳定性风险尚存。

---

## 2. 版本发布

**v2026.6.9-beta.1**  
发布日期：2026‑06‑20（截至日报生成时间）  
- **Highlights**：Telegram 交付增强 — 现在支持富 HTML、保留 rich markdown 和 sticker 路径；更忠实地渲染进度草稿和命令输出；确保 mentions 和 spooled handlers 在正确的交付路径上。  
- **涉及 PR 集合**：#93286, #93164, #93124, #93364, #9313（含多通道适配）。  
- **破坏性变更 / 迁移注意**：Release 说明中未明确列出 breaking changes，但 Telegram 用户需注意“留存 sticker 路径”可能改变原有机器人行为；建议升级前备份 `openclaw.json` 并验证 Telegram 渠道配置。  
- **发布链接**：[v2026.6.9-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.6.9-beta.1)

---

## 3. 项目进展（今日合并/关闭的重要 PR）

| PR | 简述 | 状态 |
|----|------|------|
| [#94656](https://github.com/openclaw/openclaw/pull/94656) | **fix(agents): add direct text delivery fallback for subagent completion** — 为子代理完成增加纯文本兜底发送路径，解决活跃请求者唤醒失败和 `SessionWriteLock` 错误时的消息丢失问题。 | CLOSED（已合并） |
| [#95139](https://github.com/openclaw/openclaw/pull/95139) | **fix(ollama): show full thinking levels for live-discovered models in /think menu** — 修复实时发现（通配符模式）的 Ollama 模型在 Telegram `/think` 菜单中只能显示 `default, off` 的问题，现在可以完整列出思维级别。 | CLOSED（已合并） |
| [#95157](https://github.com/openclaw/openclaw/pull/95157) | **fix(infra): use sw_vers productVersion for macOS release on Darwin 25+** — 在 macOS 26 及更高版本上正确报告系统版本，避免将 `Darwin 25` 错误映射为 macOS 15。 | CLOSED（已合并） |
| [#93794](https://github.com/openclaw/openclaw/issues/93794)（Issue） | **[Bug]: Messages on v2026.6.8 no longer supported on telegram web** — 该回归问题今日由 PR #95183 修复并关闭（见下一条）。 | CLOSED（附有修复 PR） |

此外，超过 40 个小型修复 PR（SDK 类型对齐、Telegram 流进度占位符、权限响应更新等）在今天进入合并/关闭状态，项目向前推进了约 43 个变更点。

---

## 4. 社区热点

### 讨论最活跃的 Issue

| Issue | 标题 | 评论数 | 👍 | 诉求分析 |
|-------|------|--------|----|---------|
| [#88838](https://github.com/openclaw/openclaw/issues/88838) | Track core session/transcript SQLite migration via accessor seam | 31 | 1 | 核心会话/转录迁移策略讨论：社区关注如何通过 branch‑by‑abstraction 逐步替换，避免一次性高风险重写。 |
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | Critical: Gateway Memory Leak — RSS grows from 350MB to 15.5GB | 13 | 1 | **P0 级别**内存泄漏导致 OOM 崩溃，用户强烈期待紧急修复。讨论重点在泄漏根因定位和临时缓解措施。 |
| [#85333](https://github.com/openclaw/openclaw/issues/85333) | `openclaw doctor --fix` 4-5x slower on 2026.5.20 vs 2026.5.19 | 13 | 1 | 性能回归影响日常诊断，开发者要求纳入性能监控。 |
| [#85103](https://github.com/openclaw/openclaw/issues/85103) | Model fallback chain not triggered on provider-wide quota exhaustion | 10 | 1 | 模型降级链在配额耗尽时不触发，影响生产环境可靠性。 |
| [#63829](https://github.com/openclaw/openclaw/issues/63829) | Per-agent memory-wiki vault configuration | 10 | **9** | 多智能体场景下强烈需求的功能——为每个 agent 提供独立知识 Wiki 隔离。高赞表明社区关注度极高。 |

### 最受关注（高赞）的 Issue

- **[#93794](https://github.com/openclaw/openclaw/issues/93794)**（已关闭，👍 8）：Telegram Web 消息不支持的回归，用户升级后立即遇到，当天即被修复（PR #95183），体现项目对渠道兼容性的快速响应。
- **[#91363](https://github.com/openclaw/openclaw/issues/91363)**（👍 4）：孤立 cron 任务持续失败，用户需求是可靠的后台任务执行机制。

---

## 5. Bug 与稳定性

按严重程度排列（部分 Bug 已有关联修复 PR 标注 `clawsweeper:linked-pr-open`）：

| 优先级 | Issue | 标题 | 影响 | 修复进展 |
|--------|-------|------|------|----------|
| **P0** | [#91588](https://github.com/openclaw/openclaw/issues/91588) | Gateway 内存泄漏，RSS 从 350MB 增长至 15.5GB 后 OOM | 进程崩溃、服务中断 | 尚未标记 fix PR（仅 `clawsweeper:source-repro`） |
| **P0** | [#84882](https://github.com/openclaw/openclaw/issues/84882) | memory-core Dreaming 静默删除日常记忆文件 | 数据丢失 | 关联 PR 打开，但状态 `needs-info` |
| **P1** | [#85030](https://github.com/openclaw/openclaw/issues/85030) | MCP 工具未注入子代理会话 | 功能缺失 | 标记 `linked-pr-open`，有修复进行中 |
| **P1** | [#84903](https://github.com/openclaw/openclaw/issues/84903) | 单个代理会话阻塞导致整个 Gateway 事件循环停滞（隔离失败） | 全部会话受影响 | 无 fix PR |
| **P1** | [#92043](https://github.com/openclaw/openclaw/issues/92043) | 180s 压缩超时导致合法长压缩失败 | 会话无法压缩 | 标记 `linked-pr-open` |
| **P1** | [#92460](https://github.com/openclaw/openclaw/issues/92460) | 孤立 cron 完成播报丢弃 `delivery.channel` | 消息投递失败 | 无 fix PR（`needs-live-repro`） |
| **P1** | [#90325](https://github.com/openclaw/openclaw/issues/90325) | Matrix 渠道分发断裂 — `Cannot read properties of undefined` | 渠道不可用 | 无 fix PR（`needs-live-repro`） |
| **P1** | [#93807](https://github.com/openclaw/openclaw/issues/93807) | web_fetch 忽略 `NO_PROXY` 环境变量 | 安全风险（请求经代理流出） | 标记 `linked-pr-open` |
| **P1** | [#94032](https://github.com/openclaw/openclaw/issues/94032) | `exec` 在 macOS 上无法访问私有 LAN 主机 | 工具执行受限 | 无 fix PR |
| **P1（回归）** | [#93794](https://github.com/openclaw/openclaw/issues/93794) | Telegram Web v2026.6.8 消息不支持 | 渠道可用性 | **今日已修复**（PR #95183） |

**稳定性评估**：P0 级内存泄漏是当前最大威胁，尚无修复 PR；多个 P1 隔离失败和投递丢失问题持续存在。但 Telegram Web 回归问题的快速修复显示了维护团队对渠道问题的敏感度。

---

## 6. 功能请求与路线图信号

以下功能请求在社区中呼声较高，且部分已有关联 PR，有可能被纳入下一里程碑：

| Issue | 标题 | 优先级 | 关联 PR | 判断 |
|-------|------|--------|---------|------|
| [#63829](https://github.com/openclaw/openclaw/issues/63829) | Per-agent memory-wiki vault configuration | P1, 👍9 | 无 | 高赞需求，多智能体隔离是核心路线，预计会进入设计阶段。 |
| [#90916](https://github.com/openclaw/openclaw/issues/90916) | Topic-session families for one assistant across multiple named context lanes | P2 | 无 | 会话管理革新，需要架构改动，可能性较低但社区讨论活跃。 |
| [#53638](https://github.com/openclaw/openclaw/issues/53638) | Per-channel / per-group / per-DM model override | P2 | 无（有 `linked-pr-open`? 实际未标记） | 长期开放（3月创建），用户期待配置灵活性。 |
| [#46656](https://github.com/openclaw/openclaw/issues/46656) | Webchat / Control UI inline button support | P2 | 无 | 跨渠道 UI 局限，Telegram 已支持但 WebChat 缺失。 |
| [#90354](https://github.com/openclaw/openclaw/issues/90354) | Add bounded/validated append semantics for pre-compaction memory flush | P2 | 无 | 内存写入安全增强，与稳定性相关，可能性高。 |
| [#91455](https://github.com/openclaw/openclaw/issues/91455) | Documentation update for Kubernetes | P3 | 有（PR #91455? 未提供 PR 链接） | 改进部署文档，社区贡献可能。 |

**路线图信号**：维护者近期大量精力投入在 **Telegram 交付改进**（v2026.6.9-beta.1）和 **SDK 类型安全**（多个 `fix(sdk):` PR）上，预计 6 月后续版本将继续围绕消息投递可靠性、会话隔离、类型系统对齐展开。

---

## 7. 用户反馈摘要

从 Issues 评论中提炼的关键反馈：

- **Telegram Web 兼容性失望**（#93794）：”升级到 v2026.6.8 后 Telegram Web 完全无法使用，必须降级” —— 该问题已修复，但用户对破坏性回归感到不满。
- **内存泄漏影响生产服务**（#91588）：”Gateway 运行 2 天就 OOM 重启，导致业务中断，需要紧急 patch”。
- **MCP 工具注入失败影响 AI 编排**（#85030）：”我们依赖 `sessions_spawn` 的子代理流程完全瘫痪，所有 MCP 工具均未注入，这是 beta 级别的 blocker”。
- **压缩超时导致死循环**（#92043）：”合法的长压缩（180s 不够）会被标记失败，然后下一次还是失败，永远无法压缩，会话最终超时”。
- **性能回归困惑**（#85333）：”`doctor --fix` 从 55s 变成 229s，4-5 倍差异，我不得不回滚版本”。
- **Positive 反馈**：Telegram 交付增强（v2026.6.9-beta.1）获初步正面评价，用户期待正式版本；多个快速修复 PR（如 #95139 关于 Ollama /think 菜单）获得感谢评论。

---

## 8. 待处理积压（长期未响应的重要 Issue / PR）

| 项目 | 创建日期 | 优先级 | 状态 | 备注 |
|------|---------|--------|------|------|
| [#63829](https://github.com/openclaw/openclaw/issues/63829) | 2026-04-09 | P1 | OPEN（`clawsweeper:no-new-fix-pr`） | 功能需求，已开放 2 个多月，无 fix PR 安排。 |
| [#53638](https://github.com/openclaw/openclaw/issues/53638) | 2026-03-24 | P2 | OPEN（`linked-pr-open` 但长期无实际合并） | 每通道模型覆盖，3 月至今未进展。 |
| [#46656](https://github.com/openclaw/openclaw/issues/46656) | 2026-03-14 | P2 | OPEN（`clawsweeper:no-new-fix-pr`） | WebChat 内联按钮，等待产品决策。 |
| [#84903](https://github.com/openclaw/openclaw/issues/84903) | 2026-05-21 | **P1** | OPEN（无 `linked-pr-open`） | 单个会话阻塞整个事件循环的重要 Bug，尚无修复方向。 |
| [#85333](https://github.com/openclaw/openclaw/issues/85333) | 2026-05-22 | **P1** | OPEN（`clawsweeper:needs-live-repro`） | 性能回归，需要现场复现才能推进。 |

**提醒维护者关注**：P0 内存泄漏（#91588）和 P1 事件循环隔离失败（#84903）对生产环境威胁最大，建议优先分配资源。同时，高赞功能请求（#63829）和长期积压（#53638）也需给出路线图沟通，避免社区失望。

---

**数据参考**：以上分析基于 2026-06-20 过去 24 小时内 GitHub 公开数据（Issues 500 条, PRs 500 条, 1 个 Release）。完整列表见：[OpenClaw Issues](https://github.com/openclaw/openclaw/issues) / [OpenClaw Pull Requests](https://github.com/openclaw/openclaw/pulls)。

---

## 横向生态对比

好的，作为您的资深技术分析师，我已将 **OpenClaw** 和 **Hermes Agent** 两个项目的详细动态进行横向对比与生态定位分析。以下为报告正文。

---

# AI 智能体与个人助手开源生态横向对比分析报告（2026-06-20）

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态呈现出 **“双轨加速，细分深化”** 的态势。一方面，以 OpenClaw 为代表的**工具链/交付平台**项目，正聚焦于消息渠道兼容性、会话隔离和内存稳定性等工程化问题，其核心矛盾在于如何在大规模生产环境中可靠运行。另一方面，以 Hermes Agent 为代表的**自主智能体框架**项目，正通过引入去中心化多 Agent 通信协议（A2A）、看板视图等特性，从单机工具向“Agent 网络协作平台”演进，其核心矛盾在于协议标准化和复杂功能的稳定性。两个项目均处于高强度的迭代周期，社区反馈密集，反映出用户对“可用性”和“先进性”的双重强烈需求。

## 2. 各项目活跃度对比

| 指标 | OpenClaw | Hermes Agent | 生态对比分析 |
|------|----------|--------------|--------------|
| **24h Issues 更新** | 500 条（新开/活跃 452，关闭 48） | 50 条（新报告+Bug 为主） | OpenClaw 的 Issue 流量是 Hermes 的 10 倍，部分原因为机器人自动标记与大量轻度需求统计，但整体反映 OpenClaw 用户基数或社区参与度极高。 |
| **24h PR 更新** | 500 条（待合并 457，合并/关闭 43） | 50 条（合并/关闭 8 个重要 PR + 大量小型 fix） | OpenClaw 的 PR 数量同样远超 Hermes，但待合并比例极高（91%），暗示可能存在 code review 瓶颈或大量机器人 PR。Hermes 的合并效率更高（16% 合并/关闭率）。 |
| **版本发布** | **v2026.6.9-beta.1**（Telegram 交付增强） | **v0.17.0 (The Reach)**（A2A 协议，Zulip 支持，看板视图） | Hermes 的版本更新更宏大（~800 PR，245 贡献者），OpenClaw 为小版本增量更新。两者均选择在 6 月中旬发布重大版本，显示夏季迭代高峰。 |
| **健康度评估** | **良好但稳定性风险高**。P0 内存泄漏未修复，多个 P1 会话/投递问题持续存在。快速修复 Telegram Web 回归，体现应对能力。 | **高活跃但存在重大功能回归**。Context 压缩导致回答重复（P1）等核心 Bug 影响对话质量，且插件系统 Bug 积压。 | 两个项目都处于“功能迭代快 vs 稳定性承压”的典型阶段。OpenClaw 更偏向工程稳定性焦虑，Hermes 更偏向功能完备性焦虑。 |

## 3. OpenClaw 在生态中的定位

- **生态角色**：OpenClaw 定位为 **AI 智能体交付与编排平台**，强调多通道（Telegram、Matrix、Ollama 等）的统一部署与消息路由。它更接近“AI 后端服务” + “渠道网关”组合，而非独立的 Agent 框架。
- **差异化优势**：
  - **渠道兼容性领先**：Telegram 的富文本、Sticker、进度草稿等特性的支持深度是 Hermes Agent 所不及的。Hermes 目前主要聚焦在 CLI/TUI 和 Web 端，未专门优化 Telegram 体验。
  - **会话隔离机制**：虽然存在单个会话阻塞整个 Gateway 的 Bug（#84903），但设计上已主动追求会话隔离，而 Hermes 尚未在框架层区分会话粒度的资源隔离。
  - **SQLite 迁移策略**：社区正通过 accessor seam 逐步推进核心存储结构重构（#88838），体现了对数据层长期可持续性的重视。
- **社区规模**：OpenClaw 的 Issue/PR 流量是 Hermes 的 10 倍，可能表明其社区更大，或 Issue 统计口径包含更多自动标签/机器人行为。但两者活跃度均属于一线开源项目。
- **技术路线差异**：OpenClaw 采用 **轻量化、配置驱动** 的设计，更符合运维人员和生产力用户；Hermes 采用 **插件化、可扩展** 的架构，更吸引开发者和极客。

## 4. 共同关注的技术方向

两个项目不约而同地在以下方向出现相似需求或 Bug，反映了行业共性痛点：

| 共同关注方向 | 涉及项目 | 具体诉求 / Bug 表现 |
|-------------|---------|-------------------|
| **模型兼容性与 Provider 规范** | OpenClaw, Hermes Agent | OpenClaw 存在 Ollama 模型 /think 菜单显示不完整；Hermes 存在 Gemma 4 兼容性未修复、向严格 API 发送内部字段导致 400 错误。核心诉求：**统一/健壮的模型 API 适配层**。 |
| **上下文管理与压缩可靠性** | OpenClaw, Hermes Agent | OpenClaw 有压缩超时（180s 不够）导致死循环；Hermes 有 Context 压缩导致回答重复。核心诉求：**可配置的、无副作用的上下文压缩/裁剪机制**。 |
| **子代理/任务委托稳定性** | OpenClaw, Hermes Agent | OpenClaw 有子代理完成时 `SessionWriteLock` 错误导致消息丢失；Hermes 有 `delegate_task` 模型覆盖参数被忽略。核心诉求：**可靠的子任务管理与状态同步**。 |
| **桌面端/CLI 体验增强** | OpenClaw (Telegram 已有), Hermes Agent (桌面版看板) | 两者都在增强非纯对话界面的交互，如 OpenClaw 改进 Telegram 富文本，Hermes 增加看板视图。核心诉求：**从聊天框向工作台演进**。 |

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
|------|----------|--------------|
| **功能侧重** | 消息渠道网关 + 会话管理 + 模型降级链 | 自主智能体任务编排 + 多 Agent 通信 + 桌面/CLI 生产力工具 |
| **目标用户** | 运维人员、企业部署者、需要多平台接入的团队 | 开发者、AI 爱好者、需要深度自定义 Agent 行为的用户 |
| **技术架构** | 单体 Gateway 进程 + 插件式渠道适配器；会话隔离通过进程内内存管理 | 高度模块化、插件体系完整；支持分布式运行（A2A 协议刚引入） |
| **社区参与形态** | 以 Bug 报告和小型 PR 为主，贡献者更倾向于修复已有功能 | 以大型功能 PR 和新特性提议为主，社区贡献者更倾向于扩展边界 |
| **当前迭代重心** | 修复 P0/P1 稳定性 Bug，改善 Telegram/Matrix 体验 | 实现去中心化 Agent 网络（A2A），构建项目/工作区管理（Projects） |
| **成熟度信号** | 已有正式/稳定版本的定期发布（v2026.6.x），版本号语义化 | 版本号与日期挂钩（v2026.6.19），仍处于早期快速迭代，存在破坏性变更 |

## 6. 社区热度与成熟度

- **快速迭代阶段**：**Hermes Agent** 处于明显的功能快速迭代阶段。v0.17.0 包含大量新特性，社区对新功能（A2A、桌面版看板）的讨论热烈，同时伴随大量回归 Bug 和兼容性问题。这通常是产品早期高增长的特征。
- **质量巩固阶段**：**OpenClaw** 虽也有大量新 Issue，但社区焦点集中在 **修复现有 Bug、稳定渠道、性能监控** 上。v2026.6.9-beta.1 是增量更新，没有引入颠覆性特性。同时，长期积压的高赞功能请求（如 per-agent wiki）尚未实现，说明项目更倾向于先打磨基础再扩展。
- **健康维度**：两个项目都面临“修复速度跟不上 Bug 发现速度”的挑战。OpenClaw 的 P0 内存泄漏（#91588）数周未修复；Hermes 的 Context 压缩 Bug 虽有关联 PR，但尚未合并。维护者精力分散问题值得关注。

## 7. 值得关注的趋势信号

1. **“去中心化 Agent 网络”成为新热点**：Hermes Agent 的 A2A 协议（PR #49037 的 Projects 功能）表明，行业正在从“一个 Agent 运行多个任务”向“多个 Agent 协作完成任务”演进。这对开发者而言，意味着需要开始规划跨 Agent 的身份认证、任务委托、结果聚合等中间件。
2. **“始终在线”语音唤醒是下一个入口**：Hermes 社区请求桌面版“Hey Hermes”语音唤醒（#49383），与 OpenClaw 的 Telegram 进度草稿优化共同指向 **AI 助手从被动响应到主动触达** 的转变。未来项目的竞争力可能取决于其在“低延迟、低资源、强感知”方面的表现。
3. **模型 API 严格性挑战日益突出**：Hermes 因向 OpenAI 兼容 API 泄漏内部字段而引发 400 错误，揭示出随着模型提供商对 API 参数校验越来越严格，AI 框架的消息序列化标准必须兼容性增强。开发者应关注 **OpenAI SDK 或 LLaMA.cpp 的官方消息格式演化**，避免自行封装。
4. **插件/扩展系统成为项目分水岭**：Hermes 的插件管理 Bug（#23802）持续一个月未修复，OpenClaw 未公开插件生态。当前阶段，插件系统是否成熟直接影响用户粘性。Hermes 若能在 v0.18.0 前修复插件入口点过滤问题，将确立其在可扩展性上的领先地位；否则，用户可能转向更成熟的替代方案。

---

*报告生成时间：2026-06-20 23:00 UTC*  
*数据来源：GitHub Issues / PRs / Release 公开信息*

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 Hermes Agent 数据，生成 2026 年 6 月 20 日的项目动态日报。

---

### Hermes Agent 项目日报 (2026-06-20)

**数据快照日期:** 2026-06-20
**数据覆盖时段:** 2026-06-19 至 2026-06-20
**分析师:** AI Agent 分析师

---

#### 1. 今日速览

昨日 Hermes Agent 项目保持极高活跃度，发布了里程碑式的 **v0.17.0 “The Reach Release”**，该版本包含海量代码变更和社区贡献，并引入了全新的 **Agent-to-Agent 消息协议**。与此同时，社区反馈与 Bug 报告也同步激增，24 小时内产生了 **50 条 Issue** 和 **50 条 PR**，其中 **10 个关键 Bug 已被修复或合并**。项目整体呈现出“大版本迭代”与“紧密社区反馈循环”共存的健康态势，项目正从单一桌面工具向去中心化多 Agent 协作网络快速演进。

#### 2. 版本发布

- **Hermes Agent v0.17.0 (v2026.6.19)**
  - **更新内容**: 代号 **“The Reach”**。这是自 v0.16.0 桌面版以来最大规模的更新，包含约 1475 次 Commits、800 个合并 PR 和 245 位社区贡献者。
  - **亮点功能**: 引入了 **Agent-to-Agent (A2A) Messaging 协议**，使运行在不同设备或云端的 Hermes Agent 可以相互发现、通信和委托任务，是迈向去中心化 Agent 网络的第一步。
  - **关键变更**:
    - **平台适配**: 增加了对 **Zulip** 核心平台的原生支持。
    - **性能与成本优化**: 为背景自我改进和任务委托引入了 **模型路由** 和 **上下文摘要** 机制，以降低昂贵模型的使用成本。
    - **可视化**: 桌面应用新增 **看板（Kanban）视图**，可直观展示任务和工作流状态。
  - **破坏性变更与迁移指南**: (根据发布说明推断)
    - **插件系统变更**: 可能对第三方插件加载机制有调整，建议所有插件开发者检查 `PluginManager` 接口兼容性。
    - **配置字段调整**: `model.vision` 等配置项的行为可能发生变化。建议用户在更新后，通过 `hermes config diff` 或检查 `config.yaml` 来确认配置是否生效。
    - **数据库迁移**: 看板功能可能引入新的 SQLite 数据库。系统会自动迁移，但建议用户备份 `~/.hermes/` 目录。

#### 3. 项目进展

昨日共有 **8 个重要的 PR 被合并或关闭**，标志着项目在多个关键路径上取得进展：

- **Agent 稳定性**:
  - **PR #49375**: **修复** 了 Bedrock 委托任务时，子 Agent 使用错误模式导致失败的 `P1` 级别 Bug。
  - **PR #43970**: **修复** 了 `Path.expanduser()` 在处理 `~user` 格式时可能崩溃的 Bug，提升了路径处理的鲁棒性。
  - **PR #40498**: **合并** 了一个新特性，为 `image_gen` 工具集增加了可选的 `image_edit`（图片编辑）工具。
- **桌面/CLI 体验**:
  - **PR #49260**: **关闭** 了 Signal 平台直播适配器在定时任务中静默发送失败的 Bug。问题已定位并修复。
  - **PR #43476**: **关闭** 了桌面版 `/goal` 指令被吞没（无反馈）的 P3 级别 Bug。
- **凭证与安全**:
  - **PR #49380**: **提交** 了修复方案，确保切换自定义 Provider 时，会清除 `config.yaml` 中的旧凭证（如 `api_key`），防止信息泄露或配置冲突。
- **长期推进的特性**:
  - **PR #49037**: **提交** 了“一级项目（Projects）”特性的核心代码，旨在将分散的 Session 组织成结构化的项目、仓库和分支树，这是对工作区管理模式的重大重构。

这些进展表明，项目在维护近期推出的大版本稳定性方面投入了大量精力，同时也在稳步推进对未来架构的长期规划。

#### 4. 社区热点

昨日社区讨论热度最高的话题集中在 **LLM 兼容性** 和 **API 严格性** 上：

- **#45924: hermes + gemma 4 12b 不兼容** 🗣️ **(5条评论，1个👍)**
  - **链接**: [NousResearch/hermes-agent Issue #45924](https://github.com/NousResearch/hermes-agent/issue/45924)
  - **背景**: 用户报告在 Ollama 上使用 Gemma 4 12B 模型时，Hermes 在简单对话中就会报错。该问题与已关闭的 #39281 高度相似，社区用户 #49297 主动创建新 Issue 提醒维护者：“不确定维护者是否看到了已关闭的 Issue”，体现了用户对**关键模型兼容性问题**的强烈关注。核心Bug 似乎是 `finish_reason='length'` 导致回复截断。

- **#47868 / #48523: 严格 API 兼容性导致 400 错误** 🗣️ **(各3+条评论)**
  - **链接**: [NousResearch/hermes-agent Issue #47868](https://github.com/NousResearch/hermes-agent/issue/47868), [NousResearch/hermes-agent Issue #48523](https://github.com/NousResearch/hermes-agent/issue/48523)
  - **背景**: 社区集中报告了一个模式：Hermes 在向 OpenAI 兼容 API 发送请求时，会泄漏内部元数据字段（如 `timestamp`、`message_id`），导致某些要求严格的模型提供商（如 Fireworks、`glm-5.2`）返回 400 错误。这不是单一 Bug，而是暴露了**消息序列化机制在兼容性标准上的缺陷**，是当前社区反馈的焦点之一。

**分析**: 社区当前最活跃的痛点已从“能不能用”转向“是否兼容标准”。随着 Hermes 支持越来越多 Provider，与各类严格 API 的详细兼容性成为了一个核心挑战。

#### 5. Bug 与稳定性

昨日报告的 Bug 主要集中在 Agent 核心逻辑和特定平台适配，其中 **Context 压缩导致的回答重复** 问题严重性最高。

- **P1 (严重)**:
  - **#49307**: **Context 压缩导致回答重复+丢失新指令** 🤖 **（已存在 Fix PR #49381）**
    - **链接**: [NousResearch/hermes-agent Issue #49307](https://github.com/NousResearch/hermes-agent/issue/49307), [PR #49381](https://github.com/NousResearch/hermes-agent/pull/49381)
    - **描述**: 核心 Bug。Agent 的上下文压缩机制将历史任务错误地标记为“未完成”，导致模型在压缩后重新回答旧问题，甚至覆盖用户的最新指令，严重影响对话连贯性。
  - **#49361**: **Session 索引只追踪 WhatsApp，CLI 会话不可见** 📉
    - **链接**: [NousResearch/hermes-agent Issue #49361](https://github.com/NousResearch/hermes-agent/issue/49361)
    - **描述**: `sessions.json` 索引只记录 WhatsApp 的会话，所有 CLI/TUI 的会话数据在磁盘上但**无法通过命令列表或自动恢复**，导致用户需手动从文件系统恢复，严重损害 CLI 用户的使用体验。

- **P2 (较高)**:
  - **#49297**: **修复后 Gemma 4 在 v0.17.0 中问题仍然存在** 🐛
    - **链接**: [NousResearch/hermes-agent Issue #49297](https://github.com/NousResearch/hermes-agent/issue/49297)
    - **描述**: 用户确认已关闭的 #39281 和 PR #41694 的修复在 v0.17.0 中无效，说明 **Gemma 4 兼容性问题尚未被彻底解决**。
  - **#49332**: **`delegate_task` 模型覆盖参数被忽略** 🔧
    - **链接**: [NousResearch/hermes-agent Issue #49332](https://github.com/NousResearch/hermes-agent/issue/49332)
    - **描述**: `delegate_task` 工具的 `model` 参数完全无效，所有子任务都会使用默认模型，导致用户无法为特定任务分配更高效或更便宜的模型，且可能产生意外的 API 费用。
  - **#49375 (CLOSED)**: **Bedrock 委托任务路径错误** 🔧
    - **链接**: [NousResearch/hermes-agent PR #49375](https://github.com/NousResearch/hermes-agent/pull/49375)
    - **描述**: 该 Bug 已被合并的 PR 修复。

#### 6. 功能请求与路线图信号

用户提出的新功能请求呈现出 **“超越基础对话，追求深度集成与智能控制”** 的趋势，并已出现对应的 PR 线索：

- **【桌面版插件生态】**
  - **#49363**: 要求桌面版支持加载**仪表板插件**，实现与 Web 版相同的运行时扩展能力（如自定义标签页、Shell 插槽）。这表明用户对 **Hermes 作为一个可扩展的桌面平台** 充满期待。
  - **#49383**: 请求为桌面版增加 **“Hey Hermes” 语音唤醒词**。这是一个强烈的信号，表明用户希望将 Hermes 从一个主动交谈的工具转变为**始终在线的“副驾驶”**。

- **【深度平台集成】**
  - **#49229**: 请求添加 **Zulip 平台适配器**。有趣的是，该请求被标记为 `duplicate`，指出它已被核心 PR #3335 取代，暗示 **Zulip 将成为 v0.18.0 或更高版本的标配**。这是提升项目在企业协同领域吸引力的重要信号。
  - **#49279**: 请求为 OpenCodeGo 配置增加对 **GLM-5.x 推理模型** 的支持。这表明开发者社区正积极地为 Hermes 适配最新的模型能力。

**路线图信号**: 从 #49037 (Projects 功能) 和 #49383 (语音唤醒) 可以看出，Hermes 的未来方向是成为一个**具有强组织能力、可扩展且始终可用的智能工作平台**，而不仅仅是简单的 AI 对话壳。

#### 7. 用户反馈摘要

从评论中提炼的用户真实声音：

- **“切换到国内模型，为什么还要我提供 API Key？”**
  - 用户 `zzj1965186613` 在 #49345 中描述，点击“启动网关”按钮无作用。同时 `tspine` 在 #48991 中反馈，当主模型使用自定义 Provider 时，`auxiliary.vision` 设为 `auto` 无法继承 `base_url` 和 `api_key`。这暴露出 **Custom Provider 的配置继承链存在缺陷**，导致用户在使用国内或自建模型时体验割裂。

- **“我需要一份官方的便携/隔离部署指南。”**
  - 用户 `forhonor16309` 在 #46199 中询问 Windows 上 **最小化系统侵入** 的部署方式。这表明存在大量安全敏感型用户（如企业部署），他们希望 Hermes 能更“干净”地运行，不与系统 PATH 过度纠缠。

#### 8. 待处理积压

以下 Issue 和 PR 已存在较长时间，但因其重要性或复杂性，仍待维护者关注或社区进一步讨论：

- **#23802: `hermes plugins enable/list` 过滤掉入口点发现的插件** (更新于 2026-05-11)
  - **链接**: [NousResearch/hermes-agent Issue #23802](https://github.com/NousResearch/hermes-agent/issue/23802)
  - **摘要**: 一个持续了一个多月的 **插件管理 Bug**。CLI 命令会过滤掉通过 `entry_points` 发现的插件，导致通过 `pip install` 安装的第三方插件无法在 CLI 中管理。这是**对接插件生态系统的直接障碍**，亟需解决。

- **#25106: CLI `--global` 模型开关不持久化 `model.base_url` 和 `model.api_mode`** (更新于 2026-05-13)
  - **链接**: [NousResearch/hermes-agent Issue #25106](https://github.com/NousResearch/hermes-agent/issue/25106)
  - **摘要**: 一个被忽视的配置持久化问题。当用户通过 CLI 热切换模型时，自定义 Provider 的 `base_url` 和 `api_mode` 未能正确保存，导致下次启动时可能无法正常连接。该问题与昨日新提交的 PR #49360 和 #49380 高度相关，暗示修复正在进行中，但原 Issue 仍需被引用和关闭。

- **#29433: `Path.expanduser()` 在处理非路径 `~` 字符时引发崩溃** (更新于 2026-05-20)
  - **链接**: [NousResearch/hermes-agent PR #29433](https://github.com/NousResearch/hermes-agent/pull/29433)
  - **摘要**: 这个 PR 旨在修复一个在工具调用路径中，因模型输出包含“~500-700 agencies”这种非路径文本而导致整个调用失败的问题。该 PR 已存在一个月，虽昨日有更新，但仍处于 **OPEN** 状态，需要维护者进行 code review 和合并。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*