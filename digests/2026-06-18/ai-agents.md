# OpenClaw 生态日报 2026-06-18

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-18 03:33 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，现根据您提供的 OpenClaw 项目（github.com/openclaw/openclaw）2026-06-18 的数据，生成如下项目动态日报。

---

### **OpenClaw 项目日报 | 2026-06-18**

**数据周期：** 2026-06-17 - 2026-06-18

---

#### **1. 今日速览**

今日 OpenClaw 项目保持极高的社区活跃度，24小时内产生近千条 Issue 和 PR 更新。项目维护压力较大，**Bug 修复和安全相关议题是讨论焦点**。尽管有大量新议题涌入，但 PR 合并率仅为 18%（90/500），显示**代码审查和合并流程可能成为当前瓶颈**。值得关注的是，社区正在围绕“文本泄漏”、“会话状态管理”和“安全隔离”等核心稳定性问题展开激烈讨论，其中多个议题被标记为最高优先级（P0/P1）并持续获得高关注度。

- **项目健康度评估：** 🟢 **活跃，但存在性能与安全瓶颈风险**。社区贡献热情高涨，但严重 Bug 的修复周期和 PR 的合并效率是当前需要关注的关键指标。

---

#### **2. 版本发布**

无新版本发布。

---

#### **3. 项目进展**

今日无重大合并或关闭的关键 PR 被明确标注。在展示的 30 条最活跃 PR 中，大部分仍处于开放状态（`OPEN`），仅有 **6 条**被关闭（`CLOSED`），表明项目核心推进速度放缓。这些已关闭的 PR 多为小型修复，显示了项目仍在进行持续的细小改进：

- **`#94372` - fix(cli): 修复 CLI `status` 命令上下文窗口显示问题**：解决了某些模型在 `openclaw status` 中始终显示 "X/200k" 的 UI Bug。 [链接](https://github.com/openclaw/openclaw/pull/94372)
- **`#94377` - fix(outbound): 支持外部渠道插件**：修复了外部安装的渠道插件（如微信）在投递消息时被拒绝的问题，增强了可扩展性。 [链接](https://github.com/openclaw/openclaw/pull/94377)
- **`#94382` - fix(agents): 并行化 MCP 服务器连接**：将 MCP 服务器的连接过程从串行改为并行，显著降低了多 MCP 服务器场景下的启动延迟。 [链接](https://github.com/openclaw/openclaw/pull/94382)
- **`#68936` - Autofix: 新增 PR 审查自动修复流水线**：这是一个大型 PR，旨在通过 AI 自动处理 PR 审查意见，提升开发效率。 [链接](https://github.com/openclaw/openclaw/pull/68936)

**总结：** 项目处于小修小补的阶段，重点在于修复细小的 Bug 和提升工具链效率，但尚未有重大功能合入。

---

#### **4. 社区热点**

今日社区讨论热度集中于几个长期存在的复杂问题，社区用户的诉求清晰指向**稳定性、安全性和可用性**。

1.  **【最热】文本泄漏问题 (`#25592`）**：该问题以 32 条评论位列热度榜首，并被标记为 P1 优先级和`impact:security`。核心问题是 Agent 在模型调用（Tool Call）之间产生的处理过程文本会被错误地发送到最终的消息渠道（如 Slack）。社区强烈要求将内部处理输出与给用户的最终回复严格隔离，这是一个严重的 **UX 和安全问题**。 [链接](https://github.com/openclaw/openclaw/issues/25592)

2.  **【最受欢迎】Android APK 预编译请求 (`#9443`）**：获得 25 条评论和 2 个 👍，社区用户明确表达了希望获得预编译 Android APK 的需求。这表明移动端的使用场景是用户非常关心的方向，而当前的构建流程对非技术用户存在门槛。 [链接](https://github.com/openclaw/openclaw/issues/9443)

3.  **【核心关注】会话/SQLite 迁移 (`#88838`）**：该 P0 优先级 Issue 获得 30 条评论，社区正围绕如何平滑、低风险地将核心会话状态迁移到 SQLite 数据库展开深入讨论。项目采取了“分支式抽象”（branch-by-abstraction）策略，避免一次性大规模重写，这反映了社区对稳定性的高度共识。 [链接](https://github.com/openclaw/openclaw/issues/88838)

---

#### **5. Bug 与稳定性**

今日报告的 Bug 主要集中在消息传递、安全隔离和会话状态损坏等关键领域。以下为按严重程度排列的要点：

- **P0 - 严重**
    - **`#88838`：核心会话/SQLite 迁移跟踪**。虽然这是特性请求，但其“高风险的运行时状态重构”本质使其成为影响稳定性的头号议题。 [链接](https://github.com/openclaw/openclaw/issues/88838)

- **P1 - 高危**
    - **`#25592`：文本泄漏到消息渠道** (安全+消息丢失)。**尚无对应 Fix PR**。 [链接](https://github.com/openclaw/openclaw/issues/25592)
    - **`#22676`：Signal 守护进程重启时的竞态条件** (消息丢失+崩溃循环)。**已有关联 PR (`clawsweeper:linked-pr-open`）**。 [链接](https://github.com/openclaw/openclaw/issues/22676)
    - **`#29387`：引导文件被静默忽略** (会话状态)。影响 Agent 初始化配置，严重性高。**尚无对应 Fix PR**。 [链接](https://github.com/openclaw/openclaw/issues/29387)
    - **`#31583`：`exec` 工具不继承技能环境变量** (回归Bug，安全)。导致技能组无法安全使用配置的密钥。**已有关联 PR**。 [链接](https://github.com/openclaw/openclaw/issues/31583)
    - **`#38327`：Google Vertex AI 模型调用失败** (回归Bug，崩溃循环)。**尚无对应 Fix PR**。 [链接](https://github.com/openclaw/openclaw/issues/38327)

---

#### **6. 功能请求与路线图信号**

从今日的议题来看，OpenClaw 的社区正在推动项目向**更安全、更可控、更企业级**的方向发展。

- **高优先级安全增强：**
    - **`#10659`：屏蔽密钥（Masked Secrets）**：允许 Agent 使用 API 密钥但无法直接查看，防御提示注入攻击。这是构建可信自动化系统的关键需求。 [链接](https://github.com/openclaw/openclaw/issues/10659)
    - **`#6731`：安全/不安全 `ClawdBot` 模式**：提议类似 Rust 的安全模式概念，限制 Agent 的底层系统访问权限。 [链接](https://github.com/openclaw/openclaw/issues/6731)

- **用户体验与控制提升：**
    - **`#22438`：分级引导文件加载**：通过分级别加载 bootstrap 文件来优化 Token 消耗，提升大工作空间下的性能。 [链接](https://github.com/openclaw/openclaw/issues/22438)
    - **`#27445`：子Agent完成通知定向路由**：允许子Agent的完成通知以用户消息形式返回给主Agent，以便主Agent进行更复杂的多步编排，提升流程控制力。 [链接](https://github.com/openclaw/openclaw/issues/27445)

- **路线图信号**：`#88838`（会话迁移）和 `#25592`（文本泄漏修复）等高热度议题，很可能被项目维护者列为下一版本的优先目标。同时，社区提交的 PR `#94383`（技能市场审批持久化）和 `#94355`（内存搜索回退）预示着新功能的落地。

---

#### **7. 用户反馈摘要**

- **痛点与不满：**
    - **“我的 Agent 失忆了”**：多个议题（如 `#29387` 引导文件，`#43747` 内存管理混乱）反映了用户在 Agent 状态持久化和一致性方面遇到严重问题，导致 Agent 行为不可预测。
    - **“升级后东西坏了”**：`#38327`（Vertex AI 模型失败）和 `#31583`（`exec` 工具环境变量丢失）是典型的回归 Bug，用户对版本升级可能引入的新问题表示担忧。
    - **“部署太难了”**：`#9443`（请求预编译 APK）和 `#32473`（Control UI HTTPS 要求）暴露了项目在易用性和 Ops 友好性方面的短板，对非开发者用户构成障碍。

- **使用场景与满意点：**
    - **复杂工作流依赖**：`#13583`（强制调用工具挂钩）和 `#27445`（子Agent路由）等特性请求显示，用户正将 OpenClaw 用于金融、安全等高风险、高要求的自动化场景，并迫切需要更精细的控制。
    - **对“记忆”功能的渴望**：尽管存在痛点，`#40418`（会话记忆自动保存）和 `#7707`（记忆信任标签）等请求表明，用户认可“内存”是项目的核心价值，并希望其更强大、更安全。

---

#### **8. 待处理积压**

以下为关键且长期未获响应的议题或 PR，可能阻碍项目健康发展，需维护团队重点关注。

1.  **阻塞/代码冻结风险：**
    - **`#88838` (P0, SQLite迁移)**：作为项目重构的基础，此议题的推进将影响所有下游开发，进展缓慢将成为整个项目的代码冻结风险点。 [链接](https://github.com/openclaw/openclaw/issues/88838)

2.  **高优先级 Bug 等待关注/Review：**
    - **`#25592` (P1, 文本泄漏)**：严重的安全和 UX 问题，评论数最多，但尚无维护者分配或制定明确的修复计划。 [链接](https://github.com/openclaw/openclaw/issues/25592)
    - **`#29387` (P1, 引导文件无效)**：基础功能无法正常工作，影响所有使用自定义 Agent 的同学。长期未解决。 [链接](https://github.com/openclaw/openclaw/issues/29387)
    - **`#32473` (P2, 回归Bug, Control UI HTTPS)**：作为官方 UI 的阻塞性问题，影响范围广，需要尽快给出解决方案（文档或修复）。 [链接](https://github.com/openclaw/openclaw/issues/32473)

3.  **功能请求的路线图失联：**
    - **`#9443` (Android APK)**：热度极高，但未收到官方任何关于是否支持、何时支持的回应。 [链接](https://github.com/openclaw/openclaw/issues/9443)

---

## 横向生态对比

# AI智能体与个人AI助手开源生态横向对比分析报告

**报告日期：2026-06-18**  
**分析范围：OpenClaw (github.com/openclaw/openclaw) 与 Hermes Agent (github.com/nousresearch/hermes-agent)**

---

## 1. 生态全景

当前个人AI助手/自主智能体开源生态整体呈现“功能创新与稳定性加固并行”的活跃态势。头部项目社区参与度极高，但代码审查与合并效率成为普遍瓶颈。核心痛点集中在三大方向：**会话状态持久化与一致性**（Agent“失忆”问题频发）、**安全隔离**（内部处理文本泄漏至用户渠道、密钥暴露风险）、**跨平台与分布式部署体验**（移动端预编译、桌面端纯客户端需求强烈）。同时，Agent间互操作（A2A协议）正从概念走向社区原型实现，预示着生态由单体Agent向多Agent协作范式演进的趋势。

---

## 2. 各项目活跃度对比

| 项目名称 | 24h Issues 活跃数 | 24h PR 活跃数 | 最新 Release | 健康度评估 |
|---------|-------------------|---------------|--------------|------------|
| **OpenClaw** | ~500（新开/活跃占比高） | ~500（合并率18%，即90/500） | 无 | 🟡 活跃但面临性能与安全瓶颈风险；PR合并流程成为瓶颈 |
| **Hermes Agent** | 50（新开/活跃92%，即46条） | 50（待合并94%，即47条） | 无 | 🟢 高活跃度，功能创新强劲；但合并节奏放缓，需关注响应效率 |

**说明：**  
- OpenClaw 的“近千条Issue和PR更新”中，PR数量约500，合并率仅18%，表明大量贡献等待审查。  
- Hermes Agent 虽然绝对数量较低，但Issue和PR几乎全部处于活跃/待合并状态，社区密度极高。

---

## 3. OpenClaw 在生态中的定位

**优势：**  
- **社区规模更大**：24h活动量是Hermes的10倍，表明更广泛的用户基础和贡献者生态。  
- **专注核心稳定性**：当前重点推进“会话/SQLite迁移”（P0议题 #88838），采用“分支式抽象”策略避免大规模重构风险，体现了对运行时一致性的高度承诺。  
- **企业级安全设计**：已出现“屏蔽密钥”（#10659）和“安全/不安全ClawdBot模式”（#6731）等明确的安全增强路线图，适合金融、合规类场景。

**技术路线差异：**  
- OpenClaw 偏向“收敛式”演进：通过小步快修（PR多为小型bug修复）和分支抽象来稳定核心，而非快速叠加新功能。  
- 社区反馈更集中在对现有功能的打磨（如文本泄漏、引导文件被忽略），而非全新功能请求。

**社区规模对比：**  
| 维度 | OpenClaw | Hermes Agent |
|------|----------|--------------|
| 24h Issue/PR总量 | ~1000 | 100 |
| 最高热度Issue评论数 | 32（#25592） | 22（#514） |
| 严重级别Bug（P0/P1） | 7+ | 2 |
| 功能请求数（高赞） | 4+ | 4+ |

OpenClaw 在问题发现和社区反馈的广度上明显领先，但响应效率和合并速度落后于 Hermes Agent（后者已有多个高价值PR等待合并）。

---

## 4. 共同关注的技术方向

以下需求在两个项目中均有明确体现，构成当前行业共性挑战：

| 技术方向 | 涉及的Projects | 具体诉求 |
|----------|---------------|----------|
| **Agent间互操作/通信** | OpenClaw, Hermes Agent | OpenClaw #27445（子Agent通知定向路由）；Hermes #514（A2A协议支持） |
| **安全隔离与密钥保护** | OpenClaw, Hermes Agent | OpenClaw #25592（文本泄漏）、#10659（屏蔽密钥）、#6731（安全模式）；Hermes #48181（内存工具集绕过） |
| **跨平台部署体验** | OpenClaw, Hermes Agent | OpenClaw #9443（Android APK预编译）；Hermes #38602（桌面端纯客户端）、#48186（WSL剪贴板） |
| **会话状态持久化** | OpenClaw, (Hermes间接) | OpenClaw #88838（SQLite迁移）、#29387（引导文件被忽略）；Hermes #13072（CLI智能排队与中断恢复涉及状态保持） |

**行业趋势信号：** 用户不再满足于单机对话，而是要求Agent具备跨设备、跨实例的状态记忆和协作能力，且安全机制必须从“外部防火墙”深入到“内部数据流控制”。

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
|------|----------|--------------|
| **功能侧重** | 会话记忆与安全隔离（核心）、企业级自动化（金融/安全场景引用） | Agent间通信（A2A）、桌面端体验、多元AI提供商集成（Z.AI GLM等） |
| **目标用户** | 开发者/集成商、企业运维团队、需精细控制Agent行为的专业用户 | 个人开发者、爱好者、多Agent协作研究、追求前沿功能的早期采用者 |
| **技术架构关键差异** | 分支式抽象（brownfield重构）、强调会话状态强一致性（SQLite迁移） | 插件生态丰富（OTLP/LUMEN）、并行MCP服务器启动（已有PR）、前端Electron+看板视图 |
| **代码合并策略** | 保守（合并率18%），大量PR等待审查 | 快速（待合并PR占94%但绝对数量少），创新功能能较快进入主分支 |
| **版本成熟度** | 偏“稳定期但未稳固”，严重bug堆积（P0/P1多个无修复PR） | 偏“快速迭代期”，虽有回归bug但修复PR跟进及时（OAuth已有关联PR） |

**关键洞察：**  
- 若需搭建可靠的生产级Agent服务，OpenClaw 的“会话迁移”和“文本泄漏修复”是必须跨越的门槛；而 Hermes Agent 更适合原型验证和对Agent间协作有强需求的研究团队。  
- Hermes Agent 在桌面端体验和跨平台细节上已领先（WSL、macOS、Windows均有PR修复），而 OpenClaw 的移动端支持仍停留在呼声阶段（#9443无官方回复）。

---

## 6. 社区热度与成熟度分层

| 阶段 | 项目 | 依据 |
|------|------|------|
| **快速迭代创新期** | **Hermes Agent** | 大量新功能PR（OTLP插件、LUMEN协议、Z.AI GLM提供商）、A2A协议引发高热度讨论、桌面端纯客户端诉求明确且已有初步设计。 |
| **质量巩固阵痛期** | **OpenClaw** | P0/P1严重bug占比高（7+），且多个无修复PR；用户反馈“升级后东西坏了”现象突出；PR合并率仅18%，维护者应对能力承压。 |
| **共同特征** | 两者均处于“高活跃度”状态，但OpenClaw更接近“修复驱动的轻度停滞”，Hermes Agent更接近“功能驱动的轻度混乱”。 |

**建议：**  
- 开发者若追求稳定，应关注OpenClaw的`#88838`和`#25592`修复进度；若追求创新体验，可优先尝试Hermes Agent的新已合入功能（如并行MCP连接、A2A原型）。

---

## 7. 值得关注的趋势信号

1. **Agent间互操作性成为共识**  
   - Hermes Agent 的 `#514`（A2A协议）获18个👍，OpenClaw 的 `#27445`（子Agent路由）也指向类似需求。这表明行业正从“单一Agent能力提升”转向“多Agent协同工作流”，MCP、A2A等标准将加速落地。

2. **安全从“配置项”升级为“架构原则”**  
   - OpenClaw 提出的“安全/不安全模式”（#6731）和“屏蔽密钥”（#10659），以及Hermes Agent对内存工具绕过（#48181）的担忧，说明社区意识到内建安全（secure by design）比后期补丁更可靠。

3. **移动端与桌面端“客户端化”趋势**  
   - 两个项目均收到强诉求（OpenClaw #9443 Android APK，Hermes #38602 桌面纯客户端），反映用户希望Agent像普通IM客户端一样轻量启动，而非每次都需要自举运行时。

4. **回归测试与构建稳定性成为隐忧**  
   - OpenClaw 用户抱怨“升级后东西坏了”，Hermes Agent 出现Electron缓存失效导致构建失败（#47917）、视觉回链静默崩溃（#27555）。高质量CI/CD管道和回归测试套件将成为项目成熟度的关键分水岭。

5. **生态分化：企业级 vs. 研究级**  
   - OpenClaw 的议题更偏向运维、合规、安全（如Control UI HTTPS要求 #32473），Hermes Agent 则关注协议开放性和模型提供商多样性。开发者应根据自身业务场景（生产部署vs.科研实验）选择不同路线的主导项目。

---

**总结：**  
当前AI智能体开源生态正处于从“单机实验”向“分布式生产”过渡的关键节点。OpenClaw 和 Hermes Agent 代表了两种典型的演进路径——前者以稳健为核心，后者以创新为驱动。建议技术决策者持续跟踪两项目的**会话迁移**（OpenClaw #88838）和**A2A协议实现**（Hermes #514）进展，这两者将直接影响下一阶段Agent系统架构的选型。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，现根据 Hermes Agent (github.com/nousresearch/hermes-agent) 的 GitHub 数据，为您呈上 2026 年 6 月 18 日的项目动态日报。

---

# Hermes Agent 项目动态日报 — 2026-06-18

## 1. 今日速览

项目今日保持极高的社区活跃度，Issues 和 PRs 总量均达到 50 条，其中新开/活跃的 Issues 占比 92%，待合并的 PRs 占比 94%，表明社区在积极反馈问题和提交代码，但项目核心维护团队的合并/响应速度可能面临压力。社区讨论焦点集中在 **Agent间通信协议 (A2A)** 和 **桌面端安装与体验** 两大方向，并报告了多个 **P1/P2 级别的严重 Bug**（如 OAuth 认证失败、视觉回链静默崩溃）。整体而言，项目正处于功能创新与稳定性加固并行的关键时期。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

过去 24 小时内，仅有 3 个 PR 被合并或关闭，项目整体合并节奏放缓。以下为值得关注的已关闭 PR:

-   **PR #43051 [CLOSED]**: `fix(approval): honor glob command allowlist entries` (作者: helix4u) — 修复了命令行权限控制 (命令白名单) 中 glob 模式匹配失败的问题，提升了安全机制的可靠性。
    [链接](https://github.com/NousResearch/hermes-agent/pull/43051)

虽然合并数量不多，但以下**待合并的 PR** 显示了项目在多个维度上的显著进展，一旦合并将带来重要功能更新：

-   **功能增强**: 新增 OTLP 可观测性插件 (`#48184`)、LUMEN 二进制协议传输支持 (`#47740`)、Linux 端计算机使用后端 (`#48180`)、Z.AI GLM 编程计划提供商 (`#47140`)。
-   **平台适配**: 修复了 WSL 下剪贴板粘贴 (`#48186`)、macOS 浏览器检测 (`#48185`)、Windows 下 Node 路径处理 (`#42698`) 等问题，改善了多平台用户体验。

## 4. 社区热点

今日社区讨论热度最高的三个议题：

1.  **A2A (Agent-to-Agent) 协议支持 (`#514`)**: 以 **22 条评论** 和 **18 个 👍** 成为绝对热点。该议题讨论集成 Google 提出的 A2A 开放标准，旨在解决 Agent 间的发现、通信与互操作性问题。社区对这一功能表现出极高的期望，认为它是 Hermes Agent 生态走向开放和互联的关键。
    [链接](https://github.com/NousResearch/hermes-agent/issues/514)

2.  **桌面端仅客户端安装 (`#38602`)**: 获得 **6 条评论** 和 **18 个 👍**，诉求强烈。用户希望 Hermes Desktop 能作为一个纯客户端连接远程服务，而非每次启动都需自举运行 Agent 运行时。这反映了在多设备、分布式部署场景下的真实需求。
    [链接](https://github.com/NousResearch/hermes-agent/issues/38602)

3.  **CLI 智能排队与中断恢复模式 (`#13072`)**: 获得 **5 条评论**，讨论了当前 CLI 模式下，新消息会打断正在进行的 Agent 任务的问题，提出了构建任务队列和断点恢复的功能需求，对提升 CLI 用户体验至关重要。
    [链接](https://github.com/NousResearch/hermes-agent/issues/13072)

## 5. Bug 与稳定性

今日报告的 Bug 中，**P1 级别** 的严重问题需优先关注：

-   **P1 - [Bug]: OAuth Pro/Max/Team 认证被拒 (`#48176`)**: 使用 Claude Pro/Max/Team 的 OAuth 凭证时，请求被 API 以 `HTTP 400` 拒绝。此问题会直接阻断高级用户的使用。**已有对应修复 PR (#48177)**。
    [链接](https://github.com/NousResearch/hermes-agent/issues/48176)

-   **P1 - [Bug]: 视觉回链 (`vision fallback_chain`) 静默崩溃 (`#27555`)**: `_resolve_single_provider()` 函数因参数名不匹配 (`base_url` vs `explicit_base_url`) 引发 `TypeError` 并被静默吞掉，导致整个视觉回退链路失效。这是一个隐蔽且影响严重的回归问题。
    [链接](https://github.com/NousResearch/hermes-agent/issues/27555)

**P2 级别** 的问题也较为集中：

-   **P2 - 安全问题: 禁用内存工具集可被绕过 (`#48181`)**: 报告称，即便在配置中禁用了 `memory` 工具集，外部的内存提供商工具仍可能在后期被注入，绕过安全策略。
    [链接](https://github.com/NousResearch/hermes-agent/issues/48181)

-   **P2 - [Bug]: 桌面端 Electron 构建缓存失效 (`#47917`)**: 在拉取最新代码后，桌面端构建失败，原因是 Electron 二进制缓存被意外清除。这是一个影响 Windows 开发者构建体验的回归问题。
    [链接](https://github.com/NousResearch/hermes-agent/issues/47917)

-   **P2 - [Bug]: XML 工具调用语法导致幻觉 (`#47967`)**: 当模型从外部文件读取包含 XML 标签的内容时，会生成错误的工具调用，污染对话上下文。
    [链接](https://github.com/NousResearch/hermes-agent/issues/47967)

-   **P2 - [Bug]: 安装器在 "desktop" 阶段失败 (`#46260`)**: Hermes 安装器在 Windows 10 上运行到 `npm install` 步骤时退出，导致安装中断。
    [链接](https://github.com/NousResearch/hermes-agent/issues/46260)

## 6. 功能请求与路线图信号

除社区热点的 **A2A 协议 (`#514`)** 和 **桌面纯客户端 (`#38602`)** 外，以下功能请求也值得关注：

-   **功能: CLI 使用量查询 (`#21814`)**: 用户希望新增 `hermes usage` CLI 命令和对应的 Agent 工具，以便实时查看 Token、API 配额等使用信息，这有助于用户管理成本和监控用量。
    [链接](https://github.com/NousResearch/hermes-agent/issues/21814)

-   **功能: 分渠道 Discord 系统提示 (`#48175`)**: 用户希望能为不同的 Discord 频道配置独立的人格和系统提示，这展示了在企业级或高级社区运维场景下的定制化需求。
    [链接](https://github.com/NousResearch/hermes-agent/issues/48175)

-   **功能: 桌面端看板视图 (`#48159`)**: 用户希望在 Hermes Desktop 中集成与 Web UI 一致的看板视图，以统一在桌面客户端的工作流。
    [链接](https://github.com/NousResearch/hermes-agent/issues/48159)

结合已有 PR `feat(providers): add Z.AI GLM Coding Plan provider (#47140)` 来看，项目可能正积极扩展大型语言模型支持，尤其是与国内厂商的合作。这为未来的路线图提供了线索。

## 7. 用户反馈摘要

从今日的 Issues 评论中，我们可以提炼出以下用户声音：

-   **对 A2A 协议的期待**: 用户 `teknium1` 在 `#514` 中将 A2A 描述为“与 MCP 互补的游戏规则改变者”，认为它将使 Hermes Agent 能够发现并协作于其他 Agent，构建更强大的多智能体系统。
-   **对桌面端体验的痛点**: 用户 `diegohb` 在 `#38602` 中表示“每次启动都自举运行时是不必要的”，希望“像普通的聊天客户端一样工作”，这反映了用户对轻量、快速启动体验的渴望。
-   **对视觉功能静默失败的懊恼**: 用户 `saved-j` 在 `#27555` 中指出了“一个不知何故被遗漏了的 Bug”，感叹“因为一个简单的关键词错配，整个视觉回退链被无声破坏了”。
-   **对不稳定构建的挫败感**: 用户 `wordgao` 在 `#47917` 中报告了“修复后再次失败”，并指出“Electron 缓存被更新过程删除了”，显示在解决桌面端构建稳定性方面存在反复。

## 8. 待处理积压

以下为长期未得到有效响应或合并的 Issue/PR，提醒维护者关注：

-   **Issue #20203**: `[Feature]: Add configuration support for OpenAI Responses API text verbosity` 自 5 月 5 日提出，仅有 2 条评论，但获得了 2 个 👍。该需求相对明确，实现起来可能不复杂，建议评估并考虑纳入规划。
    [链接](https://github.com/NousResearch/hermes-agent/issues/20203)

-   **Issue #8359**: `Docs/specs appear out of sync with ACP, pricing, Honcho, and container CLI` 自 4 月 12 日提出，至今仍在 OPEN 状态且仅有一条评论。文档与代码不同步会严重影响新用户上手和开发者贡献，建议列为需要清理的文档债务。
    [链接](https://github.com/NousResearch/hermes-agent/issues/8359)

-   **PR #27208**: `feat(gateway): fire agent_loop_stopped plugin hook on interrupt` 自 5 月 17 日提出，已有近一个月。该 PR 为网关添加了一个重要的插件钩子，关系到插件生态的健康度，建议尽快评审。
    [链接](https://github.com/NousResearch/hermes-agent/pull/27208)

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*