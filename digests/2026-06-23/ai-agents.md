# OpenClaw 生态日报 2026-06-23

> Issues: 259 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-23 02:50 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是根据您提供的 GitHub 数据生成的 OpenClaw 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026年6月23日

## 今日速览

OpenClaw 项目今日保持极高活跃度，过去24小时内处理了259条 Issue 和500条 PR，社区热度与维护压力并存。新发布的 `v2026.6.10-beta.2` 带来了对话快速模式这一实用新特性，并优化了模型路由。然而，项目中仍积压了大量高优（P0/P1）Bug，其中“Gateway 内存泄漏”等关键问题对生产环境的稳定性构成了严重威胁，社区对此反馈强烈。

## 版本发布

- **v2026.6.10-beta.2** (2026-06-22)
  - **更新内容**：该版本引入了两项重要的改进。
    - **对话快速模式 (Automatic fast mode for talks)**：当进行简短的对话轮次时，OpenClaw 能够自动启用快速模式，以降低延迟；在长时间的运行后则会恢复至正常模式，确保设备有界回退和执行。这是一个对用户体验有显著提升的特性。 (#85104)
    - **更可靠的模型路由 (More reliable model routing)**：此次发布包含了对 **Zai** (此处原文截断，未完整说明) 相关模型路由的优化，旨在提高路由的稳定性和鲁棒性。
  - **破坏性变更**: 公告未明确提及破坏性变更。
  - **迁移注意事项**: 建议用户关注更新后对话流畅度的变化，并留意模型路由行为是否与预期一致。

## 项目进展

虽然 PR 合并/关闭的数量（62条）远低于待合并数量（438条），但部分关键修复和功能推进值得关注：

- **CI/CD 与 QA 流程**：`fix(ci): honor reusable QA evidence failure policy` ([#95928](https://github.com/openclaw/openclaw/pull/95928)) 已被合并，该 PR 增强了持续集成流程的健壮性，使 QA 证据失败处理策略更加明确。
- **安全监控**：一个旨在为 Codex 会话增加持续安全监控的新 PR ([#95911](https://github.com/openclaw/openclaw/pull/95911)) 已被提交，表明项目正在积极探索生产环境下的安全防护能力。
- **媒体理解**：`fix(media-understanding): append actionable install hint when a media provider is missing` ([#95926](https://github.com/openclaw/openclaw/pull/95926)) 被提出，旨在改善当媒体提供方缺失时的用户错误提示，优化安装体验。

总体来看，项目在功能迭代和安全增强上有所推进，但大量 PR 仍处于等待合并或作者反馈的状态，整体吞吐效率有待提升。

## 社区热点

今日社区讨论集中在以下几个关键问题上，反映了用户对**稳定性**和**可用性**的强烈关注：

1.  **Gateway 内存泄漏 (#91588)**：该 Issue 获得了13条评论和1个 👍，是当前热度最高的问题。用户报告 Gateway 进程在正常运行2-3天后，内存占用从350MB暴涨至15.5GB，最终导致操作系统 OOM（内存耗尽）机制将其杀死。这是严重影响生产环境的 P0 级问题。 [查看详情](https://github.com/openclaw/openclaw/issues/91588)

2.  **Codex 应用服务器响应中断回归 (#88312)**：一个回归 Bug 引发了17条评论和4个 👍。用户在升级到 2026.5.27 版本后，Codex 应用服务器在处理多工具代理轮次时，会出现“Codex stopped before confirming the turn was complete”的致命错误。用户对回归问题表示强烈不满。 [查看详情](https://github.com/openclaw/openclaw/issues/88312)

3.  **核心会话/转录 SQLite 迁移 (#88838)**：作为项目核心架构的一部分，此 Issue 积累了34条评论，虽未获得大量 👍，但讨论深度反映了社区对数据一致性和存储稳健性的关注。 [查看详情](https://github.com/openclaw/openclaw/issues/88838)

## Bug 与稳定性

今日报告的 Bug 主要集中在会话状态丢失、消息递送失败和内存/性能问题上。

| 严重等级 | 问题描述 | 链接 | 是否有 Fix PR |
| :--- | :--- | :--- | :--- |
| **P0** | **关键: Gateway 内存泄漏 — RSS 从 350MB 增长至 15.5GB，导致反复 OOM 崩溃** | [#91588](https://github.com/openclaw/openclaw/issues/91588) | 无 |
| **P1** | **孤立 cron 完成宣布器在最终控制器返回时丢弃明确的 delivery.channel** | [#92460](https://github.com/openclaw/openclaw/issues/92460) | 有 (Linked PR Open) |
| **P1** | **增量迁移 (2026.6.9) 静默搬迁内存存储，无迁移/升级警告，导致完全重嵌入** | [#95495](https://github.com/openclaw/openclaw/issues/95495) | 有 (Linked PR Open) |
| **P1** | **子代理解锁失败无法释放 .jsonl.lock，永久阻塞会话** | [#95833](https://github.com/openclaw/openclaw/issues/95833) | 无 |
| **P1** | **非 Anthropic 模型将工具调用输出为纯文本 `[tool: exec]` 而非结构化块** | [#90288](https://github.com/openclaw/openclaw/issues/90288) | 无 |
| **P1** | **执行私有局域网访问失败，但同一用户的 GUI/LaunchAgent 可以访问** | [#94032](https://github.com/openclaw/openclaw/issues/94032) | 有 (Linked PR Open) |

## 功能请求与路线图信号

- **支持 PostgreSQL 替代 SQLite** (`#90370`)：这是一个呼声很高的功能请求（👍: 2），用户希望用 PostgreSQL 作为内部存储来避免资源浪费、利用高级功能并应对高并发。虽然目前没有直接对应的 PR，但此请求代表了社区对更健壮、可扩展存储方案的普遍需求。 [查看详情](https://github.com/openclaw/openclaw/issues/90370)
- **添加 Antigravity CLI 作为 CLI 后端** (`#84527`)：获得9个 👍，是今日最受期待的功能请求。由于 Google 宣布 Gemini CLI 即将停止服务，社区强烈要求 OpenClaw 接入其继任者 Antigravity CLI (`agy`)。已有相关 PR 提出，预计会被优先考虑。 [查看详情](https://github.com/openclaw/openclaw/issues/84527)
- **Telegram 内联查询支持** (`#54794`)：虽然 Issue 已标记为`stale`，但仍获得2个 👍。该功能允许用户在任意聊天中通过 `@botname query` 调用机器人，大幅提升使用便捷性。 [查看详情](https://github.com/openclaw/openclaw/issues/54794)

## 用户反馈摘要

- **痛点（稳定性）**：多位用户报告了导致程序彻底不可用的稳定性问题。例如，Gateway 内存泄漏导致“连续两天导致计算机死机”，孤立 cron 任务“始终失败”且不提供有效错误信息。核心痛点集中在系统在高负载或长时间运行后无法提供可靠服务。
- **痛点（数据与状态）**：`[2026.6.9 静默搬迁内存存储]` 的问题尤显严重，用户反馈“升级后，系统强制重嵌了1499个文件，没有任何警告”。此类破坏性变更未在升级流程中有效沟通，严重影响了用户信任。
- **使用场景**：用户反馈展示了多样化的部署环境，包括通过 OpenRouter 使用 DeepSeek V4、通过 NVIDIA Build 使用 GLM、在 macOS 上运行、以及将 OpenClaw 作为“多 Agent 平台”的需求。这表明项目社区覆盖了从个人开发者到企业级应用的各种场景。

## 待处理积压

- **Issue #8299**: “Config option to suppress sub-agent announce” 是一个自2026年2月就提出的功能请求，至今未合并。该问题涉及子代理完成后的通知行为，是提升用户体验的常见需求。 [查看详情](https://github.com/openclaw/openclaw/issues/8299)
- **PR #69039**: “add option for MCP apps support” 是一个大型（Size: XL）的高价值 PR，早在4月就已提交，但状态仍为等待作者。该功能对于拓展 OpenClaw 的工具生态至关重要，亟需维护者推进。 [查看详情](https://github.com/openclaw/openclaw/pull/69039)
- **PR #68986**: “fix: normalize visible assistant output before delivery”，同样是4月提交的重要修复，旨在解决 Discord 等渠道上泄露内部文本的问题，目前也处于等待作者状态。 [查看详情](https://github.com/openclaw/openclaw/pull/68986)

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我已仔细审阅了您提供的两份日报。基于这些详实的数据，以下是我的横向对比分析报告。

---

# AI 智能体与个人助手开源生态横向分析报告 (2026-06-23)

## 1. 生态全景

当前，AI 智能体与个人助手开源生态已进入 **“高活跃度与生产级阵痛并存”** 的成熟化初期阶段。一方面，以 OpenClaw 为代表的平台型项目社区规模巨大，功能迭代极快，正从“能用”向“好用”冲刺；另一方面，两大主流项目（OpenClaw 与 Hermes Agent）均暴露出**内存泄漏、状态损坏、平台兼容性瓶颈**等生产环境稳定性问题，表明行业正从原型验证转向严肃部署。社区的核心诉求已从“添加炫酷功能”转向“**保障核心服务的可靠性、数据一致性与跨平台无缝体验**”。

## 2. 各项目活跃度对比

| 项目 | 活跃 Issue 数 | 活跃 PR 数 | 发布情况 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 259 | 500 | **今日发布** `v2026.6.10-beta.2` | **警告**。社区规模庞大但健康度堪忧。极高的 PR 积压（438条待合并）与 P0 级内存泄漏等生产 Bug 形成鲜明对比，表明**修复速度远落后于问题爆发速度**，维护者面临严峻挑战。 |
| **Hermes Agent** | 50 | 50 | 无新版本发布 | **关注**。活跃度较 OpenClaw 低一个数量级，但问题聚焦、修复响应更快（今日合并6个PR）。P1 级 Bug 集中在平台兼容性（macOS/Windows）和网络层，整体处于 **“补坑式”巩固期**。 |

> **结论**: OpenClaw 是“高流量、高压力”的生态中心，而 Hermes Agent 是“小而锐、重点突破”的挑战者。两者都面临稳定性瓶颈。

## 3. OpenClaw 在生态中的定位

OpenClaw 当前扮演着 **“旗舰级参照物”** 角色，是整个生态的风向标。

- **核心优势**: **社区规模与功能广度**。每日数百条 Issue/PR 的吞吐量、频繁的版本发布（Beta版）以及如“对话快速模式”等持续创新的特性，使其成为功能最丰富、社区最活跃的选项。
- **技术路线差异**: OpenClaw 尝试构建一个**完整的“平台”**，其架构考虑了多模型路由、可插拔的媒体理解、CI/CD 流程等多种企业级特性。相比之下，Hermes Agent 更侧重于 **“Agent”核心能力**、平台接入（Telegram/Discord）和轻量化。
- **社区规模对比**: OpenClaw 的活跃度（259 Issue / 500 PR）是 Hermes Agent（50 Issue / 50 PR）的 **5-10倍**，代表其生态影响力是压倒性的。但这同时也意味着决策噪音和风险更大，新的开发者可能因信息过载而感到困惑。

## 4. 共同关注的技术方向

尽管规模不同，两个项目社区同时涌现了以下关键诉求，这代表了行业的普遍痛点：

| 共同方向 | 涉及项目 | 具体诉求 |
| :--- | :--- | :--- |
| **严重的稳定性问题** | **OpenClaw** (#91588 Gateway内存泄漏) <br> **Hermes Agent** (#30636 state.db损坏) | 内存泄漏、数据/状态损坏、服务器响应中断，这些都是**生产环境部署的“头号杀手”**。 |
| **平台可用性与兼容性** | **OpenClaw** (#94032 局域网访问失败) <br> **Hermes Agent** (#30230 macOS fd限制, #50765 ACP会话挂起) | 跨平台（macOS/Windows）的稳定运行是基础，但仍在突破中。 |
| **对更健壮存储的需求** | **OpenClaw** (#90370 支持PostgreSQL) <br> **Hermes Agent** (#51088 持久化会话状态) | SQLite在并发、数据恢复方面的局限性已被社区广泛感知，向更专业的存储方案迁移是明确趋势。 |
| **原生AI Provider集成** | **OpenClaw** (未明确提及，但模型路由是核心) <br> **Hermes Agent** (#12639 原生Google/Vertex AI Provider) | 社区对依赖单一第三方路由（如OpenRouter）感到不安，要求直接集成主流模型提供商的原生API，以降低成本、提升可靠性和自主可控。 |
| **UI/UX 定制化** | **OpenClaw** (#8299 抑制子Agent通知) <br> **Hermes Agent** (#37566 字体选择器) | 用户不再满足于基础功能，开始追求个人化和沉浸式的交互体验定制。 |

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **功能侧重** | **多Agent编排与平台能力**。强调对话快速模式、模型路由、媒体理解、CI/CD流程等平台级能力。 | **核心Agent与消息平台集成**。专注于增强Agent本身（如ACP、computer_use）、深度绑定Telegram/Discord等消息平台。 |
| **目标用户** | **高级开发者和企业团队**。需要部署、管理、监控多个Agent，构建复杂工作流的用户。 | **个人开发者和Bot运维者**。注重快速部署、与社区平台（Discord/Telegram）无缝对接的用户。 |
| **技术架构** | **重量级、微服务倾向**。Gateway、Codex应用服务器等组件分离，架构复杂，带来更高的灵活性和更高的运维成本。 | **相对紧凑、模块化**。更强调单体应用的易用性与部署便捷性，但也因此更容易暴露平台底层（如OS级fd限制）问题。 |
| **风险点** | **复杂性带来的稳定性脆弱性**。内存泄漏、响应中断等问题，很大程度源于其复杂架构。 | **平台兼容性的“最后一公里”**。macOS fd限制、Intel Mac支持缺失等问题表明其在特定平台上的打磨不够。 |

## 6. 社区热度与成熟度

- **高活跃度、快速迭代阶段（OpenClaw）**: 项目处于明显的**功能快速发展期**，但其健康状况堪忧。P0/P1级Bug频发且修复缓慢，表明项目正从“功能原型”向“生产级系统”转变，过程痛苦但必要。优点是创新速度快，缺点是**信任成本高**。
- **中等活跃度、质量巩固阶段（Hermes Agent）**: 项目进入了 **“追债还债”的质量巩固期**。大量的工作（50条PR）用于修复回归、平台兼容性和网络问题，而非添加新特性。这表明项目正在从“快速搭建”转向“精细化打磨”，追求稳定而非速度。

## 7. 值得关注的趋势信号

1.  **“稳定性”已成为第一竞争力**：在AI智能体领域，提供稳定、不丢消息、不崩溃的“可靠底座”，其价值正在超越“能完成哪些炫酷任务”。两个项目的P0/P1 Bug 反馈，是给所有开发者的强烈信号。
2.  **从“模型路由”到“基础设施的痛点”转移**：社区关注点正从“调用哪个模型”转向“如何在复杂系统（内存、状态、网络）中稳定地跑完一个工作流”。这意味着，**解决系统级问题（如内存管理、数据一致性）的开发者，将获得巨大优势**。
3.  **“去OpenRouter化”运动兴起**：Hermes Agent 社区对原生API的强烈呼声，预示着一个趋势：企业或个人开发者将开始避免对单一API管理平台的过度依赖，转向**直接、多供应商的模型接入策略**，以规避集中风险。
4.  **外部依赖的脆弱性传导**：OpenClaw 社区对“Antigravity CLI”的强烈需求，源于Google关闭Gemini CLI这一外部事件。这表明，AI智能体生态的上层应用，**高度依赖并受制于底层模型提供商和基础设施服务的策略变化**，生态链的脆弱性值得警惕。

---
**报告总结**：当前个人AI助手开源生态正处于关键的十字路口。OpenClaw 作为领跑者，正承受着规模增长带来的“成长的烦恼”；Hermes Agent 作为追赶者，则专注于解决“最后一公里”的稳定性问题。对于开发者而言，**选择 OpenClaw 意味着拥抱创新与风险，选择 Hermes Agent 则意味着拥抱稳定与局部优秀**。最终，谁能率先跨越“生产级可靠性”的门槛，谁就将真正赢得用户的信任与市场。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报（2026-06-23）

**数据来源**：GitHub (NousResearch/hermes-agent)，统计时段 2026-06-22 至 2026-06-23。

---

## 1. 今日速览

- 过去 24 小时项目活跃度极高：共产生 50 条 Issue 更新（新开/活跃 45 条，关闭 5 条）和 50 条 PR 更新（待合并 44 条，已合并/关闭 6 条）。
- 社区关注点集中在 **Telegram/Discord 平台稳定性**、**macOS 文件描述符限制**、**ACP 会话挂起** 以及 **OpenRouter 替代方案** 等生产环境痛点。
- 没有新版本发布，但 PR 合并/关闭量（6 条）表明维护团队正在积极响应部分回归和配置问题。
- 今日新开 Issue 中 P1 级别严重性 bug 占 3 个（Discord 消息重复分发、ACP 挂起、state.db 损坏），整体健康度需警惕。

---

## 2. 版本发布

**无新版本发布**。上次发布信息缺失，当前主分支处于 v0.17.0 状态（从 Issue 提及确认）。

---

## 3. 项目进展

今日共有 **6 条 PR 被合并或关闭**（根据 PR 更新数据统计），以下为关键合入项：

| PR 编号 | 标题 | 影响组件 | 描述 |
|---------|------|----------|------|
| #50090 | [Windows] bootstrap-installer kills Gateway without respawning (closed) | CLI/Gateway | 修复 Windows 上更新技能后 Telegram 网关被杀死且未重生的问题，已关闭。 |
| #27912 | [Feature]: Add Telegram passive history mode (sweeper:implemented-on-main，已关闭) | Telegram | “被动历史模式”特性已合入主分支，赋予用户选择仅在唤醒词后响应的能力。 |
| #41044 | computer_use tool should support Windows (closed) | vision | 社区讨论后关闭，但未合并具体实现，可能转至后续 PR。 |
| #45323 | Telegram rich tables rewritten by bullets (closed) | Telegram | 修复富表格在 Telegram 中被错误渲染为 bullet 的问题，已合并。 |
| #51033 | list_windows returns 0 despite apps running (closed) | tools | 修复 Linux 下 AT-SPI 窗口检测问题，已关闭。 |

此外，今天有大量 **待合并 PR**（44 条），其中不少为紧急 bug 修复（如 #51153 修复 Discord 重复消息、#51088 持久化会话状态），预计将在未来几天内合入。

---

## 4. 社区热点

### 🔥 最活跃 Issue
- **#12639** (评论 11，👍 10)  
  [Feature]: Support for Native Google / Vertex AI Provider (Bypass OpenRouter 402 Errors & Rate Limits)  
  **诉求**：用户频繁遭遇 OpenRouter 的 402 付费墙和速率限制，强烈要求直接接入 Google Vertex AI 原生 API。  
  **链接**：https://github.com/NousResearch/hermes-agent/issues/12639

### 🔥 高关注度讨论
- **#37505** (评论 7，👍 1)  
  Hermes Desktop macOS DMG 仅 arm64，Intel Mac 无法运行。讨论集中于构建 universal binary 的可能性。  
- **#30230** (评论 4)  
  macOS 文件描述符软限制 256 导致网关崩溃。社区已有临时方案（修改 launchctl），但希望官方自动调整。  
- **#37566** (评论 3，👍 4)  
  字体选择器请求：用户希望自定义桌面端字体，反映 UI 定制化需求。

### 🔥 最活跃 PR（评论数缺失，但标题反映紧迫性）
- **#51153** `fix(discord): prevent duplicate user message processing on auto-thread and reconnects`  
  直接解决 #51057 的 P1 Discord 重复分发问题，是社区高优先级关注点。

---

## 5. Bug 与稳定性

### 严重级别 P1 (紧急，存在生产环境风险)

| Issue | 标题 | 组件 | 是否有 Fix PR |
|-------|------|------|--------------|
| #30636 | state.db corruption from SIGTERM during launchd shutdown under high load | agent/gateway | 无 |
| #31599 | Telegram adapter leaks httpx connections through HTTP proxy → fd limit hit | Telegram | 无 |
| #41289 | /model command blocks Discord event loop for 120-150s | Discord | 无 |
| #51057 | Discord: single user message dispatched twice → 2 agent runs / 2 responses | Discord | **有** (#51153) |
| #50765 | ACP session/prompt hangs after conversation turn on Windows v0.17.0 regression | ACP | 无 |

### 严重级别 P2 (影响用户体验但可规避)

| Issue | 标题 | 组件 | 状态 |
|-------|------|------|------|
| #30230 | macOS fd limit (256) 下网关崩溃 | gateway | 讨论中 |
| #48648 | Telegram 4096字符溢出导致无限嵌套回复循环 | Telegram | 无 PR |
| #50090 | Windows bootstrap-installer 杀网关不重连（已关闭） | CLI/Gateway | **已修复** |
| #50755 | Photon iMessage AuthenticationError 后项目密钥轮换 | plugins | 无 |
| #51089 | Session resume 丢失 tool-loop 或压缩状态 | agent | **有** (#51088) |
| #51141 | write_file 密钥红化误伤有效 Python 代码 | tools/auth | 无 |
| #51136 | Docker 镜像中惰性依赖无法安装 | docker | 无 |

### 其他注意
- **#51155** (P2)：人格设置不生效，持久化到 config.yaml 未按预期工作（新开）。
- **#49289** (P3)：桌面端删除 profile 后图标残留，UI 状态不一致。

---

## 6. 功能请求与路线图信号

### 可能纳入下个版本的功能

| Issue/PR | 标题 | 优先级 | 说明 |
|----------|------|--------|------|
| #12639 | 原生 Google/Vertex AI Provider | 高（👍 10） | 绕过 OpenRouter 的强烈需求，已有社区讨论，但无实现 PR。 |
| #51158 (PR) | session-scoped reasoning effort override | P3 | 为 /reasoning 命令添加临时覆盖，不影响全局配置，源自用户反馈。 |
| #51135 (PR) | 加载项目本地 .mcp.json | P3 | 允许复用项目已有 MCP 配置，提升开发效率。 |
| #42448 | OIDC 登录窗口支持 WebAuthn / Passkey / Touch ID | P3 | 企业用户无密码认证需求，但实现依赖 WebView 能力。 |
| #50885 | 桌面端远程创建/删除 workspace 文件夹按钮 | P3 | 用户希望不用终端直接管理远程工作区。 |
| #51069 | 支持项目 .mcp.json（已 duplicate） | P3 | 与 #51135 重复，已被标记。 |

### 路线图信号
- Telegram 被动模式（#27912）已合并，表明团队重视平台细粒度控制。
- `computer_use` 对 Windows 的支持（#51137 PR）正在推进，cua-driver v0.6.x 已跨平台。
- 社区多次要求 **Docker 镜像惰性依赖安装**（#51136），但尚未解决。

---

## 7. 用户反馈摘要

### 典型痛点
1. **OpenRouter 成本/限制**（#12639）：用户在评论中表示“每天被 402 打断，必须切换到其他 API”，呼吁原生 Google/Vertex 支持。
2. **macOS 稳定性**：用户因 `maxfiles=256` 导致网关崩溃（#30230），不得不编写 launchd plist 调整。Intel Mac 用户无法启动桌面端（#37505）。
3. **Telegram 平台**：流式消息超过 4096 字符导致无限循环（#48648），代理商无法中断；代理连接下连接池泄漏（#31599）。
4. **Windows 支持缺失**：ACP 挂起（#50765）、Docker 挂载问题（#51142）、computer_use 不可用（#41044）是三大障碍。
5. **配置体验**：`bool("false")` 导致 YAML 引号内的布尔值错误（#51147 PR修复），用户困惑。

### 积极反馈案例
- 用户对 `/model` 命令阻塞事件环的修复 PR（#51153）表示期待：“终于不用重启 Bot 了”。
- 社区对 **Telegram 被动模式**（#27912）的合入表示满意，认为可以“安静地监听群聊”。

---

## 8. 待处理积压

### 长期未响应的重要 Issue（超过 3 天无维护者回应）

| Issue | 创建时间 | 标题 | 严重性 | 关键性 |
|-------|----------|------|--------|--------|
| #37505 | 2026-06-02 | macOS DMG 仅 arm64, Intel Mac 无法运行 | P3 | 影响半数 macOS 用户 |
| #30230 | 2026-05-22 | macOS fd limit 256 导致崩溃 | P2 | 高并发场景必现 |
| #30636 | 2026-05-22 | state.db SIGTERM 损坏 | P1 | 可能导致数据丢失 |
| #31599 | 2026-05-24 | Telegram httpx 连接泄漏 → fd 耗尽 | P1 | 连续运行 2 天后崩溃 |
| #41289 | 2026-06-07 | Discord /model 阻塞事件环 120-150s | P1 | 影响 Discord 机器人可用性 |
| #12639 | 2026-04-19 | 原生 Google/Vertex AI Provider 支持 | 功能 | 高赞需求，长期未实现 |

### 提醒
- #31599 (Telegram 连接泄漏) 虽已有部分讨论，但仍无修复 PR，建议优先分配资源。
- #30636 (state.db 损坏) 对数据持久性影响大，可参考 #51088 的持久化改进思路进行系统性修复。
- #12639 作为 4 月即提出的高赞 feature，合理规划进下一里程碑。

---

**总结**：Hermes Agent 今日社区活跃度高，团队正在积极解决多个 P1/P2 生产级 Bug，尤其在 Discord 和 Telegram 平台稳定性方面有所推进。macOS 和 Windows 的兼容性问题仍是主要瓶颈。功能请求向原生 API 支持、MCP 集成和 UI 定制化倾斜。建议维护者重点关注 `state.db` 损坏和 fd 泄漏两个长期悬而未决的数据安全问题。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*