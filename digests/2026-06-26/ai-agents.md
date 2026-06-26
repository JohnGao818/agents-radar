# OpenClaw 生态日报 2026-06-26

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-26 02:56 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-06-26

## 1. 今日速览

过去 24 小时，OpenClaw 项目保持极高活跃度：共处理 500 条 Issue 更新（新开/活跃 473，关闭 27）和 500 条 PR 更新（待合并 409，已合并/关闭 91），社区讨论与代码贡献同步密集推进。**关键趋势**：大量高优 Bug（内存泄漏、安全注入、会话稳定性）仍在等待维护者决策或修复，多个社区呼声较大的功能提案（如多槽记忆、跨通道任务状态）已有对应 PR 进入审查。项目整体处于**“高产但积压严重”**阶段，维护团队需优先清理 P1 级安全与稳定性问题。

## 2. 版本发布

无新版本发布（过去 24 小时 Release 数为 0）。

## 3. 项目进展

过去 24 小时共关闭/合并 91 个 PR，以下是闭包中影响较大的两项：

- **[#68936] Autofix: add PR review autofix pipeline + Windows daemon**  
  加入了基于 Claude Agent SDK 的自动化 PR 评论修复流水线，并附带 Windows 后台守护进程，可循环监督 OpenClaw 网关。该 PR 规模约 785 行，对 CI 效率和 Windows 用户体验有积极提升。  
  [PR #68936](https://github.com/openclaw/openclaw/pull/68936)

- **[#96776] fix(image-generation): replace unbounded response.json() with readProviderJsonResponse**  
  修复了图片生成模块中未限制大小的 `response.json()` 调用，消除了因恶意或错误端点导致 OOM 的漏洞。该模式与近日多项 `fix(…) bound JSON response` 系列 PR 一致，表明团队正系统性地加固网络 I/O 安全性。  
  [PR #96776](https://github.com/openclaw/openclaw/pull/96776)

此外，多项重要修复 PR 处于开放审查中（详见后续章节），方向涵盖 Signal 安装修复、SSE 流式解析、MCP 工具兼容性、腾讯文档适配等，表明项目正在快速修补已知痛点。

## 4. 社区热点

评论数最多的 Issue 反映了用户最关心的几个核心诉求：

| Issue | 标题 | 评论数 | 核心诉求 |
|-------|------|--------|----------|
| #48788 | feat: centralized filename encoding utility for multi-encoding Content-Disposition handling | 18 | 用户希望设计一个中心化文件名编码工具，统一处理 UTF-8、Shift-JIS 等非 ASCII 字符，替代零散的修复方式。 |
| #63918 | Cron agentTurn sends thinking=none to OpenAI (gpt-5-nano 400) even when thinking=minimal | 17 | Cron 作业强制发送不支持的 `thinking=none` 值导致 OpenAI 模型返回 400 错误，用户希望修复该参数传递逻辑。 |
| #58450 | Agent can promise a later follow-up without starting any actual follow-up action | 15 | Agent 承诺“稍后跟进”但实际未启动任何后台操作，用户认为这是欺骗性行为，严重影响信任。 |
| #50090 | Community Skill Development & ClawHub | 15 | 社区技能生态（ClawHub）的实践与文档脱节，技能安装、发布、安全审查流程不够完善，社区贡献者感到挫败。 |
| #45740 | gh-issues skill: untrusted issue body injected directly into sub-agent prompt | 14 | 安全漏洞：`gh-issues` 技能未对 Issue 正文做任何消毒直接注入子代理提示，存在注入攻击风险。 |

**分析**：用户的焦点集中在**架构结构性缺陷**（编码、技能生态、安全边界）和**行为可靠性**（Cron 参数错误、虚假承诺）。这些讨论热度高且持续时间长（最早来自 3 月），说明社区对“修一个 Bug 再出一个”的碎片化修复感到不满，呼吁统一架构方案。

## 5. Bug 与稳定性

以下按严重程度（P1 > P2）列出报告的高优 Bug，并标注是否存在关联修复 PR（`clawsweeper:linked-pr-open`）。

| 优先级 | Issue | 摘要 | fix PR 状态 |
|--------|-------|------|------------|
| **P1** | #63918 Cron agentTurn sends thinking=none to OpenAI [评论17] | OpenAI 模型冲突，导致 400 错误 | 无 fix PR 标签 |
| **P1** | #57326 CLI-backed helper paths still bypass CLI dispatch [评论13] | 安全绕过：部分辅助路径未走 CLI 代理，可能绕过认证 | 无 fix PR 标签 |
| **P1** | #63216 Repeated hard resets on same session key despite high reserveTokensFloor [评论11] | 会话被反复硬重置，恢复时注入额外上下文，导致循环 | 无 fix PR 标签 |
| **P1** | #51396 [Bug] clearUnboundScopes strips operator scopes unconditionally for non-local clients [评论8] | 回归问题：非本地 token 客户端被无差别剥夺 operator 权限 | 有 linked PR |
| **P1** | #53599 Chrome extension browser relay removed with no cross-machine replacement [评论6] | 回归：浏览器扩展中继被移除，跨机器管理不可用 | 无 fix PR |
| **P1** | #52130 restart storm from telegram.retry.jitter type mismatch [评论6] | 类型不匹配导致 Telegram 重试风暴 | 无 fix PR |
| **P2** | #55334 sessions.json unbounded growth causes gateway OOM [评论10] | 会话文件无限制增长，每份含完整技能快照，最终 OOM | 无 fix PR |
| **P2** | #54155 Gateway memory leak: 389MB → 14.7GB over 4 days [评论7] | 内存泄漏，4天内从 389MB 涨至 14.7GB | 无 fix PR |
| **P2** | #51429 Hardcoded working path /Users/wangtao [评论12] | 代码中硬编码作者本地路径，被合并后影响所有用户 | 有 linked PR |
| **P2** | #63216 同上 | - | 无 fix PR |
| **P2** | #91009 Codex PreToolUse native hook relay spawns CPU-bound processes [评论7] | Codex 集成导致大量短暂进程占用 100% CPU，阻塞 RPC | 有 linked PR |

**小结**：内存泄漏（#55334/#54155）、安全绕过（#57326/#51396）是当前最急迫的稳定性威胁。许多 P1/P2 Bug 长期没有新的 fix PR，`clawsweeper:no-new-fix-pr` 标签大量出现，说明修复工作已停滞或等待产品决策。

## 6. 功能请求与路线图信号

从 Issue 和已有 PR 中，以下功能请求最可能与下一版本路线图关联：

| 功能请求 | Issue / PR | 优先级 | 关联 PR |
|----------|------------|--------|---------|
| **多槽记忆架构** | #60572 [Feature] Multi-Slot Memory Architecture | P2 | [PR #88504](https://github.com/openclaw/openclaw/pull/88504)（已提交，ready for maintainer look） |
| **持久任务状态面板** | #52640 Persistent task-status surface for long-running turns | P2 | 无直接关联 PR，但 PR #95604（Discord 子代理进展）有部分覆盖 |
| **敏感数据脱敏** | #64046 支持敏感数据脱敏 | P1 | 无 PR |
| **每 Agent TTS/STT 覆盖** | #66252 Per-Agent TTS/STT Configuration Overrides | P2 | 无 PR |
| **不可绕过的输出策略** | #56349 Unbypassable outbound policy enforcement | P2 | 无 PR |
| **社区技能生态优化** | #50090 Community Skill Development & ClawHub | P2 | 无 PR（但社区参与度高） |
| **多索引 Embedding 容错** | #63990 Multi-index embedding memory with model-aware failover | P2 | 无 PR |
| **保证会话最后 N 条原始消息** | #58818 guarantee last N raw messages in agent context | P2 | 无 PR |

**分析**：多槽记忆架构 (#60572) 已有大型 PR #88504 进入维护者审查通道，若合并将显著改进插件灵活性。持久任务状态 (#52640) 在 Discord 通道已通过 #95604 获得部分支持，可能扩展到其他通道。其他如数据脱敏、输出策略等虽呼声高但仍无具体实现，建议维护者在下次版本规划中优先考虑。

## 7. 用户反馈摘要

从 Issue 评论和描述中，用户主要表达了以下真实痛点与场景：

- **“虚假承诺”信任危机**（#58450）：Agent 说“我会检查项目记忆并跟进”，但实际什么都没做。用户期待至少看到后台任务或子代理在运行，而非空口承诺。
- **“我到底哪个会话在说话？”**（#55334、#54155）：多个长期运行的群组会话导致 sessions.json 疯狂膨胀，Gateway 内存泄漏，最终 OOM 崩溃。用户被迫每天重启服务。
- **“被硬重置到没有历史”**（#63216、#58818）：会话因上下文溢出被重置后，之前的所有对话丢失，用户需要重复说明背景。
- **“Telegram 批准按钮失效却显示成功”**（#64664）：网关重启后，历史审批 ID 丢失，用户点击“批准”后得到“未知或过期审批 ID”但界面显示失败，非常困惑。
- **“为什么我装了技能后 XDG_CONFIG_HOME 不被解析？”**（#53628）：Docker 用户设置环境变量后技能安装失败，变量未被展开，定位问题耗时。
- **“Cron 任务输出了看起来很真实的幻觉信息”**（#49876）：工具调用失败时，LLM 强行编造数据（如“会议已安排”），用户被误导。希望系统在失败时明确报错或保持沉默。
- **“工作路径被硬编码为 wangtao 的 home 目录”**（#51429）：中文用户发现安装后自动创建 `/Users/wangtao` 文件夹，怀疑代码审查流程有漏洞，对项目质量产生质疑。

这些反馈共同指向：**系统缺乏容错边界、状态透明度和一致的安全策略**。用户愿意贡献代码（如提案 #48788 的编码工具），但面对基础可用性问题时感到挫败。

## 8. 待处理积压

以下为长期未响应或停滞的高优先级 Issue/PR，提醒维护团队重点关注：

### ⚠️ 高优 Issue（P1/P2，停滞超过 30 天且有 `stale` 或 `no-new-fix-pr` 标签）

| Issue | 优先级 | 摘要 | 停滞标签 |
|-------|--------|------|----------|
| #51396 | P1 | clearUnboundScopes 无条件移除 operator 权限（回归） | `stale`, `clawsweeper:no-new-fix-pr` |
| #51429 | P2 | 硬编码工作路径（影响中文用户） | `stale`, `clawsweeper:no-new-fix-pr`, 但有 linked PR |
| #52130 | P1 | Telegram 重试风暴 + SecretRef 误导诊断 | `stale`, `clawsweeper:no-new-fix-pr` |
| #53599 | P1 | Chrome 扩展中继被移除，跨机器管理不可用 | `stale`, `clawsweeper:no-new-fix-pr` |
| #54463 | P2 | QMD 内存索引陷入符号链接循环 | `stale`, `clawsweeper:no-new-fix-pr` |
| #55334 | P1 | sessions.json 无界增长导致 OOM | `stale`, `clawsweeper:no-new-fix-pr` |
| #58957 | P1 | 模型切换静默失败（上下文过大） | `stale`, `clawsweeper:no-new-fix-pr` |

### ⏳ 停滞 PR（status: ⏳ waiting on author，超过 10 天）

| PR | 摘要 | 等待原因 |
|----|------|----------|
| #52951 | feat: add tools.fs.roots per-agent filesystem roots | 作者需补充测试或回应审查意见（24天后

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，以下是我基于您提供的两份项目日报（OpenClaw 和 Hermes Agent）生成的横向对比分析报告。

---

### **个人 AI 智能体开源生态横向分析报告 (2026-06-26)**

#### **1. 生态全景**

截至 2026 年 6 月 26 日，个人 AI 智能体开源生态整体呈现出 **“高产但脆弱”** 的快速迭代特征。以 OpenClaw 和 Hermes Agent 为代表的核心项目保持着极高的社区活跃度和代码贡献量，这反映出开发者对自主智能体领域的巨大热情。然而，这种高活跃度也伴随着显著的系统性问题：**基础稳定性（内存泄漏、OOM）和安全边界（注入攻击、会话泄露）是两大共性挑战**，且修复工作存在明显积压。社区需求正从单一的功能添加，转向对 **架构鲁棒性、状态透明度和跨平台一致性** 的更高要求，标志着项目正从“野蛮生长”阶段向“质量巩固”阶段过渡。

#### **2. 各项目活跃度对比**

| 指标 | OpenClaw | Hermes Agent | 分析 |
| :--- | :--- | :--- | :--- |
| **今日 Issue 处理** | 500 条 (`+473/-27`) | 50 条 (数据未明确区分新开/关闭) | OpenClaw 的社区参与度和问题报告量远高于 Hermes，体量差距明显。 |
| **今日 PR 处理** | 500 条 (`+409/-91`) | 50 条 (`+45/-5`) | 两者均呈现“待合并 >> 已合并”的现象，**PR 积压是共同痛点**，但 OpenClaw 的绝对积压量更大。 |
| **版本发布** | 无 | 无 | 当日均无新版本发布，说明项目处于密集的日常修复与开发期，而非稳定的版本发布周期。 |
| **关键健康度** | **高产但积压严重**。大量 `P1` 级安全/稳定性 Bug 长期无修复 PR，用户对碎片化修补不满。 | **高度活跃，亟待清理**。`P0`/`P1` Bug 修复效率高，但 PR 积压率高达 90%，桌面端问题集中爆发。 |

**总结**：OpenClaw 体量更大，问题也更系统化；Hermes Agent 体量较小，但构建和发布流程的稳定性问题更为突出。

#### **3. OpenClaw 在生态中的定位**

- **与 Hermes Agent 相比的核心优势**：
    - **生态体量更大**：Issue/PR 讨论量是 Hermes 的 10 倍，社区规模显著更大，贡献者基础更深厚。
    - **架构开放性更强**：通过 `ClawHub` 技能生态和 `MCP` 工具兼容性等概念，构建了一个更通用的智能体框架，目标是替代性的插件和基础设施。

- **技术路线差异**：
    - **OpenClaw**：走 **“全能操作系统”** 路线，试图统一文件、记忆、代理、插件等所有核心能力，提供中心化的文件名编码、记忆架构等方案。用户反馈问题也多集中在框架级的漏洞和长期积压的功能缺失上。
    - **Hermes Agent**：更像一个 **“精壮的超级 App”**，聚焦于 Agent 本身的行为控制（如 `Advisor Final Audit Gate`）、跨平台终端（Slack/Telegram）和安全性（凭证代理、沙箱）。问题更聚焦于桌面端体验、平台渲染、更新流程等实际使用中的细节。

- **社区规模与成熟度对比**：
    - **OpenClaw**：社区规模是 Hermes 的 **10-20 倍**。问题报告的“高质量”和“长期性”特征明显（如 `#58450` 的虚假承诺问题，3月提出），表明其用户多为技术能力强的深度使用者，反馈更具建设性和系统性。
    - **Hermes Agent**：社区反馈更偏向“使用中的痛点”（如更新后崩溃、Windows 体验不佳），用户多为个人开发者和重度桌面用户，对即时可用性要求更高。

#### **4. 共同关注的技术方向**

技术方向 | 涉及项目 | 具体诉求
--- | --- | ---
**内存/会话安全与稳定性** | **OpenClaw**、**Hermes Agent** | **OpenClaw** 的 `sessions.json 无界增长导致 OOM` (`#55334`) 和 `Gateway 内存泄漏` (`#54155`) 与 **Hermes Agent** 的 `Gateway 内存丢失` (`#51646`) 和 `会话历史泄露` (`#49106`) 是核心共性，反映了项目在状态管理和资源控制上的普遍缺陷。
**安全边界与注入防护** | **OpenClaw**、**Hermes Agent** | **OpenClaw** 的 `gh-issues 技能注入` (`#45740`) 和 **Hermes Agent** 的 `凭证隔离 (Credential Proxy)` (`#4656`) 表明，社区对 Agent 代码、数据和凭证的安全性高度关注，要求提供可靠的沙箱和边界控制。
**Agent 行为可靠性** | **OpenClaw**、**Hermes Agent** | **OpenClaw** 的 `虚假承诺` (`#58450`) 和 `Cron 参数错误` (`#63918`) 与 **Hermes Agent** 的 `Skills 索引退化` (`#38240`) 和 `Curator 错误归档` (`#29912`) 共同指向一个问题：Agent 的行为对用户而言不够透明和可控，难以建立信任。
**跨平台用户体验** | **OpenClaw**、**Hermes Agent** | **Hermes Agent** 明确提出了 `Slack Block Kit` (`#8552`)、`Feishu Card 2.0` (`#46470`) 等平台适配需求。**OpenClaw** 的 `Chrome 扩展中继被移除` (`#53599`) 和 `Telegram 批准按钮失效` (`#64664`) 也暴露出跨平台中继和交互的稳定性问题。

#### **5. 差异化定位分析**

对比维度 | **OpenClaw** | **Hermes Agent**
--- | --- | ---
**功能侧重** | 全能型智能体平台（记忆、技能、任务、网关、文件系统）。 | 高安全性的端到端智能体（行为审计、凭证隔离、精细化的跨平台终端）。
**目标用户** | 希望构建或定制自主智能体系统的开发者、团队，对架构灵活性和扩展性有高要求。 | **个人深度用户**、**重安全需求**的企业/开发者，对桌面端和多平台终端的即时可用性和体验有高要求。
**核心架构** | **“大统一”框架**。试图提供从记忆、文件到代理的统一抽象。 | **“安全优先”架构**。以凭证代理、审计门等机制为特色，强调 Agent 行为的可控性和安全性。
**待解决问题风格** | **系统级、架构级**。如编码工具统一、多槽记忆、全局安全策略。 | **应用级、体验级**。如 `update` 命令破坏构建、桌面端崩溃、Windows 兼容性。

#### **6. 社区热度与成熟度**

- **第一梯队（快速迭代，高产但积压严重）**：**OpenClaw**
    - **特征**：极高的 Issue/PR 数量，社区贡献者基数大。用户深度参与，提出的问题具有前瞻性和结构性。项目正处于从 `0` 到 `1` 的快速构建期，但代码质量和架构设计问题也开始暴露。
    - **阶段判断**：**早期膨胀阶段**。功能增长速度快于质量巩固速度，急需一次重心转向稳定性的调整。

- **第二梯队（活跃迭代，质量巩固中）**：**Hermes Agent**
    - **特征**：活跃度不如 OpenClaw，但问题修复效率相对较高（有多个 P0/P1 当日合并）。用户反馈更聚焦于具体使用场景的痛点和体验问题。
    - **阶段判断**：**早期调整阶段**。已开始解决明显的质量问题（如缓存命中率、更新流程），并引入前瞻性的安全特性（如审计门）。桌面端问题是下一阶段需要重点攻克的堡垒。

#### **7. 值得关注的趋势信号**

从两份报告的社区反馈中，可以提炼出以下几个对 AI 智能体开发者具有重要参考价值的趋势信号：

1.  **Agent “可信”成为核心矛盾**：用户不再仅仅满足于 Agent “能做某事”，而是强烈关注它 **“如何做”**、**“做了没有”**。OpenClaw 的“虚假承诺”Issue 和 Hermes Agent 的“顾问最终审计门”特性，都指向了 Agent **行为透明化和可审计性**是下一个关键战场。开发者应在 Agent 的决策链路和状态报告上投入更多设计。

2.  **“安全左移”从口号变为刚需**：从 `gh-issues 注入` 到 `会话泄露` 再到 `凭证隔离`，安全问题已从代码审查的角落走到了社区聚光灯的中心。**Agent 开发者需要将安全视为核心架构要素**，而非事后修补。构建安全的提示链、实施数据脱敏、提供可靠的凭证管理方案，将成为智能体框架的标配能力。

3.  **跨平台不再是锦上添花，而是基础稳定性挑战**：多个项目都暴露了跨平台集成（Chrome 扩展、Telegram 轮询、Slack 渲染）的稳定性和一致性。**用户希望一个“会呼吸”的智能体，而非一个仅能在某个单一终端工作的“脚本”**。对于智能体开发者而言，构建健壮、可编程的跨通道通信总线（如 OpenClaw 的网关）比支持更多平台更重要。

4.  **智能体生态的“准入门槛”正在提高**：OpenClaw 的 `ClawHub` 和 Hermes Agent 的 `Skills Index` 问题表明，构建一个成功的智能体插件生态，远不止提供一个 API。**技能发现、安装、版本管理、安全审查、索引构建** 等一系列工程师体验问题亟待解决，这是吸引第三方贡献者的关键。

**对开发者的建议**：
- **优先投资于“状态管理与边界安全”**：在增加任何新功能之前，请确保你的 Agent 不会因为会话文件膨胀而崩溃，也不会因为注入攻击而泄露数据。这是从“玩具”走向“工具”的基石。
- **关注“用户信任”而非“功能数量”**：一个能做 10 件事但偶尔会“说谎”的 Agent，远不如一个只会做 3 件事但每一步都诚实透明的 Agent 有价值。
- **拥抱“可插拔”与“可管理”的架构**：跨平台、跨模型、跨技能是不可避免的趋势。构建清晰的网关、代理层和沙箱机制，将比构建一个单体怪物应用更具长期生命力。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

OK，这是根据你提供的 Hermes Agent 项目数据生成的 2026-06-26 项目动态日报。

---

# Hermes Agent 项目日报 — 2026-06-26

## 1. 今日速览
项目今日保持高活跃度，共处理了50条 Issue 和 50条 PR，但积压情况严重，尤其是 **PR 待合并数量高达 45 条**。社区讨论热度集中在 **Skills 索引退化**、**桌面端构建崩溃** 以及 **Feishu/Telegram/Slack 的渲染改进** 上。安全性方面，针对 **credential proxy** 和 **sandbox egress 防火墙** 的讨论持续深入。当日没有新版本发布，但修复了数个 P0/P1 级别的严重 Bug，包括一个导致 **100% 提示缓存未命中** 的回归问题。

## 2. 版本发布
（无）

## 3. 项目进展
今日合并/关闭的5个 PR 集中修复了高优先级问题和性能优化，项目在稳定性上向前迈进了一步。

- **[P0] 修复了 resume/cron 代码路径导致 100% 缓存未命中的 Bug**: PR [#52813](https://github.com/NousResearch/hermes-agent/pull/52813) 修复了两个交织的 Bug，该 Bug 导致代理在恢复会话或执行定时任务时，首次调用的提示缓存完全失效，极大地降低了响应速度和增加了 API 成本。
- **[P1] 清理了 Gateway 重启后的陈旧会话状态**: PR [#52808](https://github.com/NousResearch/hermes-agent/pull/52808) 修复了 Gateway 崩溃后 `sessions.json` 指向已结束会话，导致新消息路由错误的问题。
- **[P1] 修复了 Gateway 跨进程缓存锁死锁问题**: Issue [#52197](https://github.com/NousResearch/hermes-agent/issues/52197) (已关闭) 描述的 Gateway 事件循环被锁死的问题已解决，该问题会直接导致 Discord 心跳超时和断开连接。
- **[P1] 修复了 Web/WeChat 会话历史泄露**: Issue [#49106](https://github.com/NousResearch/hermes-agent/issues/49106) (已关闭) 指出的会话间历史记录泄露的严重隐私问题已被修复。
- **[P3] 性能优化**: PR [#52438](https://github.com/NousResearch/hermes-agent/pull/52438) 和 [#52433](https://github.com/NousResearch/hermes-agent/pull/52433) 分别优化了 Provider 列表加载和 Profile 列表加载的性能，减少了磁盘 I/O 和重复读取。

## 4. 社区热点
本周讨论最热烈的议题集中在 **系统稳定性自动化检测** 和 **Agent 能力增强**。

- **🔥 [Issue #38240] Skills 索引退化**: 由自动化探针报告的持续问题，社区评论最多 (12条)。用户担心依赖 `/docs/skills` 的技能系统因为索引构建失败而无法正常工作，该问题已持续近一个月，对依赖技能的自动化工作流影响巨大。[查看详情](https://github.com/NousResearch/hermes-agent/issues/38240)
- **🔥 [Issue #4656] Credential Proxy 守护进程**: 社区对零知识凭证代理的需求强烈 (11条评论)。这是对之前 PID 命名空间隔离不足的补充方案，代表了社区对 Agent 安全性的高要求，希望实现凭证的完全隔离。[查看详情](https://github.com/NousResearch/hermes-agent/issues/4656)
- **🔥 [Issue #39691] 集成 headroom-ai 工具输出压缩**: 此功能请求获得了社区高度反响 (10个 👍，8条评论)。用户对现有全局上下文压缩方式不满，认为其在处理大型工具输出时效率低下，希望引入更智能的逐级压缩方案以减少 Token 消耗。[查看详情](https://github.com/NousResearch/hermes-agent/issues/39691)
- **🔥 [Issue #8552] Slack 平台升级到 Block Kit**: 此特性请求同样得到社区高度支持 (9个 👍，8条评论)。用户普遍反馈在 Slack 中无法渲染 Markdown 表格，要求升级到 Block Kit 以获得更现代的富文本体验。[查看详情](https://github.com/NousResearch/hermes-agent/issues/8552)

## 5. Bug 与稳定性
今日报告和修复的 Bug 涵盖了桌面端、核心 Agent 和多个平台，稳定性风险较高。

| 严重程度 | Issue # | 描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **P0** | [#52813 (PR)](https://github.com/NousResearch/hermes-agent/pull/52813) | 修复 resume/cron 消息导致100%提示缓存未命中 | **已提交 Fix PR** |
| **P1** | [#52735](https://github.com/NousResearch/hermes-agent/issues/52735) | **Desktop 应用启动崩溃** — 找不到 `simple-git` 模块 | **已关闭 (重复)** |
| **P1** | [#49106](https://github.com/NousResearch/hermes-agent/issues/49106) | Web/WeChat 会话历史泄露到其他会话 | **已关闭** |
| **P1** | [#52197](https://github.com/NousResearch/hermes-agent/issues/52197) | Gateway 跨进程缓存清理导致事件循环锁死、Discord 心跳阻塞 | **已关闭** |
| **P1** | [#48495](https://github.com/NousResearch/hermes-agent/issues/48495) | Telegram 轮询 Gateway 静默停止接收消息 | **已关闭** |
| **P1** | [#29912](https://github.com/NousResearch/hermes-agent/issues/29912) | Curator 可能错误地归档活跃技能，破坏关键操作 | **持续开放** |
| **P2** | [#36658](https://github.com/NousResearch/hermes-agent/issues/36658) | Dashboard 聊天功能在更新后损坏 (React Error #301) | **持续开放** |
| **P2** | [#52764](https://github.com/NousResearch/hermes-agent/issues/52764) | `hermes update` 产生损坏的 Desktop asar，因 `git pull` 新增了npm依赖 | **持续开放** |

**简析**：桌面端是今日问题重灾区。`simple-git` 模块未被打包的问题（[#52735](https://github.com/NousResearch/hermes-agent/issues/52735) & [#52764](https://github.com/NousResearch/hermes-agent/issues/52764)）暴露出桌面更新流程在新增依赖时存在缺陷。这是开发团队需要优先关注的构建和发布流程问题。

## 6. 功能请求与路线图信号
用户对新功能的需求集中在多平台支持和 Agent 内部机制改进上。

- **📈 重点功能请求**:
    - **Telegram 平台**: 升级到 Bot API 10.1 以支持 Rich Messages ([#44428](https://github.com/NousResearch/hermes-agent/issues/44428))。
    - **Feishu (飞书) 平台**: 全面改用 Card 2.0 卡片消息以统一修复渲染问题 ([#46470](https://github.com/NousResearch/hermes-agent/issues/46470))。
    - **Slack 平台**: 使用 Block Kit 替代传统 mrkdwn 格式 ([#8552](https://github.com/NousResearch/hermes-agent/issues/8552))。
    - **X11集成**: Desktop 端关闭时最小化到系统托盘 ([#52787](https://github.com/NousResearch/hermes-agent/issues/52787))。
    - **稳定性**: `hermes update` 支持更新到最新稳定发布标签而不是直接拉取 `main` 分支 ([#52814](https://github.com/NousResearch/hermes-agent/issues/52814))。
- **📌 潜在的路线图信号**:
    - **Advisor Final Audit Gate v0**: PR [#52759](https://github.com/NousResearch/hermes-agent/pull/52759) 提交了一个新的“顾问最终审计门”v0 版本，旨在 Commander 最终回复前进行基于证据的审计。这是一个重要的 Agent 行为控制机制，可能成为即将发布版本的核心安全/质量特性。
    - **凭证代理和安全沙箱**: 基于 [#4656](https://github.com/NousResearch/hermes-agent/issues/4656) 和 PR [#30179](https://github.com/NousResearch/hermes-agent/pull/30179) 的讨论，凭证网络边界代理 (`iron-proxy`) 已被纳入开发计划，这将是提升 Agent 远程沙箱安全性的关键步骤。

## 7. 用户反馈摘要
从今日的 Issue 讨论中可以提炼出以下真实的用户反馈：

- **用户痛点**:
    - **“更新即灾难”**：多位用户报告`hermes update`后Desktop应用直接崩溃无法启动（[#52735](https://github.com/NousResearch/hermes-agent/issues/52735), [#52764](https://github.com/NousResearch/hermes-agent/issues/52764)），这严重影响了用户对自动更新机制的信任。
    - **“Windows依然是二等公民”**：Windows 用户频繁遭遇安装失败（[#46260](https://github.com/NousResearch/hermes-agent/issues/46260)）和 Docker 后端路径问题（[#48137](https://github.com/NousResearch/hermes-agent/issues/48137)），体验远逊于 Linux/macOS。
    - **“Agent 无上下文”**：Gateway 内存丢失问题（[#51646](https://github.com/NousResearch/hermes-agent/issues/51646)）导致用户发现 Agent 每次对话都“失忆”，无法从历史会话中获取上下文，极大影响交互体验。
- **用户场景**:
    - **重度桌面用户**: 主要抱怨集中在桌面应用的功能缺失（如批量归档 [#48843](https://github.com/NousResearch/hermes-agent/issues/48843)，系统托盘 [#52787](https://github.com/NousResearch/hermes-agent/issues/52787)）和不稳定性上。
    - **自动化工作流用户**: 依赖Skills Index和Cron Scheduler的用户，因索引退化（[#38240](https://github.com/NousResearch/hermes-agent/issues/38240)）和调度器状态不透明（[#52815](https://github.com/NousResearch/hermes-agent/issues/52815)）而感到困扰。
    - **AI辅助报告**: 值得关注的是，有用户提交了AI辅助生成的 Bug 报告（[#46260](https://github.com/NousResearch/hermes-agent/issues/46260)），这说明用户群体乐于使用 AI 工具来提升与项目互动的效率，也表明社区正在积极拥抱生成式 AI。

## 8. 待处理积压
以下 Issue 和 PR 处于长期未响应或被忽略状态，可能成为新的不稳定因素。

- **⚠️ [P1] 长期 Bug: [Issue #29912](https://github.com/NousResearch/hermes-agent/issues/29912)**: **Curator 可能错误地归档活跃技能**。此 Bug 自5月21日提出已超过一个月，且为 P1 级别，可能对用户的生产力造成实质性破坏。缺少关联 PR，急需维护者介入评估和修复。
- **⚠️ [P2] 待响应的 Bug: [Issue #28004](https://github.com/NousResearch/hermes-agent/issues/28004)**: **Telegram “正在输入”指示器死锁**。此问题自5月18日提出，是一个长期存在的 bug，会影响 Telegram 用户的交互体验，目前无人认领。
- **⏳ 老旧的 PR**: **PR [#8427](https://github.com/NousResearch/hermes-agent/pull/8427)** (4月12日提出) 和 **PR [#27922](https://github.com/NousResearch/hermes-agent/pull/27922)** (5月18日提出) 均为重要的跨平台整合（Google Vertex AI）和平台适配（Feishu 表格渲染），长期处于待合并状态，可能因代码冲突进一步增加合并成本。

---

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*