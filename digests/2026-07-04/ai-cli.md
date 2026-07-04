# AI CLI 工具社区动态日报 2026-07-04

> 生成时间: 2026-07-04 02:32 UTC | 覆盖工具: 2 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

好的，作为一名专注于 AI 开发工具生态的资深技术分析师，我已仔细审阅了您提供的两份社区动态日报。以下是基于这两份报告的横向对比分析报告。

---

### AI CLI 工具横向对比分析报告 (2026-07-04)

**报告摘要**：当前 AI CLI 工具生态正处于从“功能可用”向“生产可靠”过渡的关键阶段。社区反馈的核心矛盾已从“能做什么”转向“如何安全、可预测、跨平台地稳定工作”。两大标杆工具——Claude Code 与 OpenAI Codex——在同一日表现出高度相似的用户痛点（安全性、模型行为可预测性、平台兼容性），但采取了差异化的迭代路径：Anthropic 侧重于调整权限模型和用户交互流程，而 OpenAI 则密集加固底层 Git 操作安全。整体生态快速迭代，但“安全”与“稳定”已成为决定用户留存的关键胜负手。

---

### 1. 生态全景

当前 AI CLI 工具生态已从早期的概念验证阶段，全面进入 **“生产环境压力测试”** 阶段。社区反馈不再是零散的“怎么做”问题，而是系统性地要求工具具备企业级安全隔离、跨平台一致性和可预测的模型行为。两大主流工具 Claude Code 和 OpenAI Codex 在 7 月 4 日的动态不约而同地指向了 **“信任与可控”** 的核心诉求：前者因自动超时机制引发大规模抗议，后者因内部路由协议不透明导致模型兼容性故障。这表明，开发者不再接受“黑盒”行为，对工具的控制权（如超时配置、权限模式）和可见性（如模型行为、安全策略）提出更高要求。同时，Git 安全加固成为突发的共同技术焦点，揭示了 AI 代理操作本地代码仓库时面临的真实攻击面。

### 2. 各工具活跃度对比

| 指标 | **Claude Code** | **OpenAI Codex** | **其他 (推测)** |
| :--- | :--- | :--- | :--- |
| **当日热点 Issues (Top 10)** | 10 个 (高互动) | 10 个 (高互动) | -- |
| **Top Issue 最高评论数** | 116 (#36151) | 68 (#30224) | -- |
| **Top Issue 最高 👍 数** | 495 (#65697) | 53 (#30364) | -- |
| **当日新/更新 PR 数** | 7 个 | 10+ 个 | -- |
| **当日版本发布** | 2 (v2.1.200, v2.1.201) | 1 (rust-v0.143.0-alpha.35) | -- |
| **核心 Bug 严重性** | **极高** (凭据泄露 #72274) | **高** (模型被拒 #30224, 性能退化 #30364) | -- |
| **迭代策略** | 快速功能/配置响应 (v2.1.200) | 底层安全加固为主 (10+ 安全 PR) | -- |

**分析**：
- **热度与规模**：两者社区活跃度均处于高位，均积累了超百条评论的高热度 Issue。Claude Code 在单个 Issue 的点赞数上（495个）远超 Codex（53个），表明其部分功能需求（如 Linux 桌面版）拥有更强烈的单一用户群体支持。
- **迭代节奏**：Claude Code 发布两个小版本，以快速回应用户反馈（超时行为、权限模式），体现其敏捷迭代能力。OpenAI Codex 则表现出更深度的防御性开发，密集提交安全相关的 PR，表面节奏放缓，实则在进行重要的底层重构。
- **问题严重性**：Claude Code 报告的 **跨会话凭据泄露**（#72274）是这轮所有问题中安全风险最高的，表明其会话隔离或缓存机制可能存在严重缺陷。Codex 的模型兼容性问题虽影响面广，但属功能性阻塞，而非直接的安全事故。

### 3. 共同关注的功能方向

多款工具社区均表现出对以下方向的强烈诉求：

1.  **安全与信任的零容忍**：
    - **Claude Code**: 用户要求细化权限模式（v2.1.200 已部分响应）、可配置超时、紧急修复**凭据泄露**漏洞。
    - **OpenAI Codex**: 开发者团队主动大规模加固 Git 操作安全（阻止恶意 filter、防止配置注入），社区则关注**Responses-Lite 机制不透明**带来的功能阻塞。

2.  **模型行为的可预测性**：
    - **Claude Code**: 用户报告**模型幻觉**（#70315）导致生成虚假对话历史，严重破坏信任。
    - **OpenAI Codex**: 用户发现**推理 token 聚类**（#30364）导致复杂任务性能下降，并质疑**上下文压缩丢失规则**（#25792）破坏任务连续性。

3.  **细粒度的控制权限与可配置性**：
    - **Claude Code**: 对 `AskUserQuestion` 超时、权限模式（`Manual` vs `Auto`）的讨论与配置。
    - **OpenAI Codex**: 需求包括主会话与子 Agent 选用不同模型（#14039）、App 与 Client 实时同步（#31062）。

4.  **跨平台一致性和兼容性**：
    - **Claude Code**: 强烈呼唤 **Linux 桌面版**（#65697），且 `.claude/settings.json` 路径解析错误影响项目配置。
    - **OpenAI Codex**: **Windows 平台**存在大量顽疾（卡顿、sandbox 错误、认证不一致），macOS 与 Windows 的认证行为也不同。

### 4. 差异化定位分析

| 维度 | **Claude Code** | **OpenAI Codex** |
| :--- | :--- | :--- |
| **功能侧重** | **复杂、多步骤的代理工作流**。强调“询问用户”（`AskUserQuestion`）、子Agent管理和多步骤任务执行。 | **深度融入开发环境**。侧重 VS Code 扩展、`apply_patch` 操作、Git 操作底层安全，更像一个“AI 驱动的 IDE 内核”。 |
| **目标用户** | 需要高级助手完成**软件工程全生命周期**任务的开发者，如架构设计、跨模块重构、复杂调试。 | 追求**高效率编码和代码修改**的日常开发者，强调与现有开发流程（VSCode、Git）的无缝集成。 |
| **核心优势** | **Agentic 能力**：其内部 `harness`、子 Agent、`AskUserQuestion` 等机制，使其能处理需要频繁人类确认的复杂任务。 | **安全性与 IDE 生态**: 对 Git 操作的安全加固程度极高，且社区 PR 数量多，显示出更强的社区安全共建能力。 |
| **核心劣势** | **安全与稳定性**：爆出凭据泄露、模型幻觉等信任危机，且子目录设置解析错误等基础问题影响体验。 | **模型与平台**：模型内部路由机制（Responses-Lite）不透明，Windows 平台生态体验远落后 macOS。 |
| **技术路线** | 快速功能迭代 + 基于社区反馈的配置修正。 | 底层安全加固先行，平台兼容性跟进，模型迭代与机制调整相对缓慢。 |

### 5. 社区热度与成熟度

- **Claude Code**: **“成长痛”最明显的工具**。社区极其活跃（高评论、高点赞数），但反馈内容充满了“功能惊喜”后的“信任危机”。大量 Issue 指向产品策略改变（如 AskUserQuestion 超时）带来的巨大争议。这表明其正经历从“新奇工具”向“可靠生产工具”转型的阵痛。其社区更感性，对功能变化反应激烈。
- **OpenAI Codex**: **“稳扎稳打”的平台型工具**。社区同样活跃，但焦点更偏向于“平台差距”（如 Windows 支持）和“模型行为”（如 token 聚类）。其开发者团队（bookholt-oai）表现出高度的“防御性开发”风格，集中解决安全基础问题。这表明 Codex 可能已度过最快速增长期，正处于优化和加固的成熟化阶段。其社区更理性，关注长期稳定性和生态体系。

### 6. 值得关注的趋势信号

1.  **安全成为最高优先级**：无论是 Claude Code 爆出凭据泄露，还是 Codex 团队主动上报大量 Git 安全 PR，都表明在 AI 代理可以自由操作本地文件系统后，**“安全默认”已从可选项变为必选项**。任何权限与控制流程的微小疏忽，都可能引发严重安全事故。

2.  **“手动模式”的回归**：Claude Code 将默认权限模式改为 **Manual**，是对社区“不想被 AI 绕过”诉求的回应。这预示着，在自动化与用户控制权之间，行业可能会阶段性向“用户控制”倾斜。开发者不再迷信全自动，而是要求“我在我在场，且我知情并批准”。

3.  **模型行为的“黑盒”危机**：OpenAI Codex 的 token 聚类问题和 Claude Code 的幻觉问题，共同指向了 **“AI 大脑”的不透明性正在引发信任危机**。开发者不仅需要模型输出结果，更需要理解其推理过程。任何看似随机的性能退化或行为异常，都会削弱对工具的依赖。

4.  **平台“二等公民”的代价**：Claude Code 对 Linux 桌面的呼吁，以及 Codex 在 Windows 上的长期 Bug，表明 **非主力平台（非 macOS）的用户体验正在成为社区分裂和用户流失的导火索**。对于想要服务更广泛开发者的工具，全平台的一致体验将不再是加分项，而是基础要求。

5.  **从“工具”到“伴侣”的转变**：用户不再仅仅用这些工具来生成或修补代码，而是期望它们能**像资深同事一样参与整个开发流程**。这体现在对任务状态持久化、跨会话上下文管理、以及子 Agent 协作等复杂功能的强需求上。工具必须具备“记忆”和“规划”能力，并能处理长时间、多步骤的任务。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（截至2026-07-04）

## 1. 热门 Skills 排行

以下 PR 在社区中获得了较高关注（讨论密集、修复关键问题或填补需求空白），且目前均为 **open** 状态。

### 1.1 `skill-creator` 修复：`run_eval.py` 始终报告 0% 召回率  
**PR #1298** | [链接](https://github.com/anthropics/skills/pull/1298)  
**功能**：修复了技能评估脚本 `run_eval.py` 在多平台（Windows、Mac、Linux）下触发检测失效、并行 worker 死锁等问题，使得描述优化循环能正常工作。  
**社区热点**：该问题被多次复现（#556、#1169、#1323），用户反馈优化循环实际上在优化噪声，导致技能质量无法提升，是 **skill-creator 工具链最核心的 bug**。

### 1.2 `document-typography` — 文档排版质量控制  
**PR #514** | [链接](https://github.com/anthropics/skills/pull/514)  
**功能**：防止 AI 生成文档中的常见排版错误：孤词换行、孤行段落、编号错位等。覆盖所有 Claude 生成的文档。  
**社区热点**：用户普遍认可这是一类“所有人都需要但很少主动提”的问题，讨论集中在如何定义“好排版”的规则边界以及是否需要与 PDF/DOCX 技能联动。

### 1.3 `testing-patterns` — 全面测试模式技能  
**PR #723** | [链接](https://github.com/anthropics/skills/pull/723)  
**功能**：覆盖单元测试（AAA 模式）、React 组件测试（Testing Library）、集成测试、E2E 测试、Mock/Stub 策略、测试 Trophy 模型等。  
**社区热点**：社区对测试自动化的需求强烈，该技能试图在同一 skill 内提供完整测试哲学与实践指导。讨论焦点在于是否过于宽泛、是否应拆分多个小技能。

### 1.4 `self-audit` — 输出自审计技能  
**PR #1367** | [链接](https://github.com/anthropics/skills/pull/1367)  
**功能**：在交付前对 AI 输出进行机械验证（检查所有声明文件是否存在）和四维度推理审计（按损害严重性优先顺序）。适用于任何项目。  
**社区热点**：这是一个相对新颖的方向——让技能自身具备质量门控能力。讨论集中在审计维度的可定制性以及是否会增加 token 消耗。

### 1.5 `ODT` 技能 — OpenDocument 文本创建与模板填充  
**PR #486** | [链接](https://github.com/anthropics/skills/pull/486)  
**功能**：创建、填充、读取、转换 .odt、.ods 文件，支持模板化填充和导出 HTML。  
**社区热点**：这是对现有 PDF/DOCX 技能的有力补充，尤其受 LibreOffice 用户和开源文档流程的开发者关注。讨论点包括 ODF 格式与 Office 格式的互操作性问题。

### 1.6 `color-expert` — 色彩专业知识技能  
**PR #1302** | [链接](https://github.com/anthropics/skills/pull/1302)  
**功能**：涵盖 ISCC-NBS、Munsell、XKCD、RAL、Ridgway 等颜色命名系统，以及 OKLCH、OKLAB、CAM16 等色彩空间的适用场景。  
**社区热点**：该技能填补了设计类技能的空白，讨论集中在色彩术语的准确性和与前端设计技能的关系。

### 1.7 `sensory` — macOS 原生自动化（AppleScript）  
**PR #806** | [链接](https://github.com/anthropics/skills/pull/806)  
**功能**：使用 `osascript` 替代基于截图的 Computer Use，实现 macOS 应用直接操作（两层级权限系统）。  
**社区热点**：社区对“非截图”自动化有强烈需求，但涉及系统权限和安全模型，讨论热度高且持续。部分用户担心 AppleScript 的跨版本兼容性。

### 1.8 `skill-quality-analyzer` & `skill-security-analyzer` — 元技能分析器  
**PR #83** | [链接](https://github.com/anthropics/skills/pull/83)  
**功能**：提供技能质量（结构、文档、示例、资源、可测试性）和安全（权限、注入、敏感信息）的五维度分析。  
**社区热点**：这是少数“关于技能本身的技能”，讨论集中在分析标准是否客观、是否应纳入官方工具链。同时也是 #492 安全问题的直接呼应。

---

## 2. 社区需求趋势

从 Issues 高频讨论中提炼出以下方向：

| 需求方向 | 典型 issue | 描述 |
|---------|------------|------|
| **技能创建工具链稳定性** | #556、#1169、#1061 | `run_eval.py` 在 Windows/Linux/Mac 下均存在触发检测、子进程编码、并行死锁等问题，社区期望官方优先修复 skill-creator 工具。 |
| **安全与信任边界** | #492、#1175 | 社区技能在 `anthropic/` 命名空间下分发导致信任滥用；SharePoint 文档处理中的权限脚本安全问题。 |
| **组织级技能共享** | #228 | 当前只能手动下载/上传 .skill 文件，用户期望企业和团队内直接分享、接口调用。 |
| **新技能类型：代理治理** | #412 | 要求技能涵盖 AI 代理系统的安全模式：策略执行、威胁检测、信任评分、审计追踪。 |
| **新技能类型：紧凑记忆** | #1329 | 长运行代理的符号化上下文压缩，减少 token 消耗。 |
| **平台集成** | #29、#16 | 希望技能能在 AWS Bedrock 中运行，以及以 MCP（Model Context Protocol）接口暴露技能能力。 |
| **重复技能问题** | #189 | `document-skills` 和 `example-skills` 插件安装后包含相同技能，导致上下文膨胀。 |
| **技能可靠性** | #62、#184 | 技能文件消失、`agentskills.io` 页面重定向错误等基础架构问题。 |

---

## 3. 高潜力待合并 Skills

以下 PR 评论活跃、解决实际痛点，且尚未合并，预计未来几周内可能落地：

| PR | 名称 | 状态 | 理由 |
|----|------|------|------|
| [#1298](https://github.com/anthropics/skills/pull/1298) | skill-creator 修复（run_eval 全面修复） | open | 直接影响所有技能开发者，修复后可使优化循环真正工作。 |
| [#1367](https://github.com/anthropics/skills/pull/1367) | self-audit 自审计技能 | open | 独创的质量门控理念，社区反馈积极。 |
| [#1302](https://github.com/anthropics/skills/pull/1302) | color-expert 色彩专家 | open | 填补设计技能空白，结构清晰。 |
| [#514](https://github.com/anthropics/skills/pull/514) | document-typography 排版控制 | open | 跨文档类型通用，受众广。 |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns 测试模式 | open | 测试自动化刚需，内容完整。 |
| [#486](https://github.com/anthropics/skills/pull/486) | ODT 技能 | open | 开源文档生态的重要拼图。 |
| [#806](https://github.com/anthropics/skills/pull/806) | sensory (macOS AppleScript) | open | 非截图自动化的先锋方案。 |
| [#83](https://github.com/anthropics/skills/pull/83) | skill-quality-analyzer & security-analyzer | open | 元技能分析器，有安全议题支撑。 |

---

## 4. Skills 生态洞察

**当前社区最集中的诉求是：优先修复 skill-creator 工具链的跨平台稳定性与触发检测逻辑，同时建立社区技能的安全命名与信任机制，以确保技能生态系统能够可靠、安全地扩展。**

---

# Claude Code 社区动态日报 | 2026-07-04

## 今日速览

昨日（7月3日），Anthropic 连续发布 **v2.1.200** 与 **v2.1.201** 两个版本，核心调整了 `AskUserQuestion` 的超时行为并默认将权限模式改为 **Manual**，回应了社区对“自动跳过用户输入”的强烈不满。与此同时，多个高热度 Bug 仍在发酵——#73125（AskUserQuestion 60 秒超时后自动继续）收获 111 条评论，#70315（模型幻觉重复报告）再次被用户质疑未得到修复。当天还有 7 个新 PR 被提交，主要集中在插件和安全性优化上。

---

## 版本发布

### v2.1.201
- **更改**: Claude Sonnet 5 会话不再使用 mid-conversation system role 来放置 harness reminders（即不再通过系统角色插入提醒）。
- **链接**: https://github.com/anthropics/claude-code/releases/tag/v2.1.201

### v2.1.200
- **更改**:
  1. `AskUserQuestion` 对话框默认不再自动继续；用户可通过 `/config` 配置空闲超时。
  2. 将 CLI、`--help`、VS Code 和 JetBrains 插件的默认权限模式改为 **“Manual”**（原为自动审批）。对应参数：`--permission-mode manual` 与 `"defaultMode": "manual"`。
- **链接**: https://github.com/anthropics/claude-code/releases/tag/v2.1.200

---

## 社区热点 Issues（Top 10）

### 1️⃣ #36151 — [FEATURE] 多账户切换（116 评论，415 👍）
- **摘要**: 要求在 Claude Mobile 应用中支持多账户切换，且无需共享邮箱。
- **为什么重要**: 用户对多环境（个人/工作）支持的需求强烈，415 个赞为社区最高。
- **链接**: https://github.com/anthropics/claude-code/issues/36151

### 2️⃣ #73125 — [BUG] AskUserQuestion 60 秒无响应后自动继续（111 评论，354 👍）
- **摘要**: 更新后 AskUserQuestion 工具等待约 60 秒便自行继续，导致空选择。用户希望恢复之前无限等待的行为或令超时可配置。
- **为什么重要**: 直接关联 v2.1.200 的变更，社区反应激烈，是本次日报最核心的 Bug。
- **链接**: https://github.com/anthropics/claude-code/issues/73125

### 3️⃣ #19673 — [BUG] 使用率 84% 却提示“已达限制”（101 评论，75 👍）
- **摘要**: 会话使用率仅 84%，但频繁出现“You've hit your limit”错误，限额计算逻辑疑似有误。
- **为什么重要**: 长期未修复，影响高频用户的正常使用。
- **链接**: https://github.com/anthropics/claude-code/issues/19673

### 4️⃣ #65697 — [FEATURE] 官方 Linux 桌面版（51 评论，495 👍）
- **摘要**: 请求提供 Ubuntu LTS / Debian 的正式桌面端构建，目前仅 macOS 和 Windows 有桌面版。
- **为什么重要**: 495 个 👍 是社区最高赞 Feature，Linux 用户呼声极高。
- **链接**: https://github.com/anthropics/claude-code/issues/65697

### 5️⃣ #23626 — [FEATURE] diff 比较支持非 main 分支（24 评论，78 👍）
- **摘要**: 在 Claude Code IDE 功能中，当前 diff 比较只能针对 main 分支，希望支持任意分支或工作树。
- **链接**: https://github.com/anthropics/claude-code/issues/23626

### 6️⃣ #70315 — [BUG] 模型幻觉：错误插入假对话历史（12 评论，0 👍，但问题严重）
- **摘要**: assistant 生成假的 user/system 回合，stop_reason=null，导致 Opus 4.8 无法使用。用户声称此前 #64791 已被 bot 错误自动关闭。
- **为什么重要**: 影响核心模型行为，用户投诉“无法使用该模型”。
- **链接**: https://github.com/anthropics/claude-code/issues/70315

### 7️⃣ #73105 — [FEATURE] AskUserQuestion 超时时间可配置（6 评论，27 👍）
- **摘要**: 用户请求将 60 秒超时改为可配置或恢复无限等待，与 #73125 类似但独立提出。
- **链接**: https://github.com/anthropics/claude-code/issues/73105

### 8️⃣ #74060 — [BUG] Web 版 claude.ai/code 初始化后无响应（当天创建，3 评论）
- **摘要**: Cloud web session 初始化完成后永久挂起，任何消息均无响应。
- **为什么重要**: 影响浏览器用户，当天新报，可能为近期部署问题。
- **链接**: https://github.com/anthropics/claude-code/issues/74060

### 9️⃣ #74023 — [BUG] .claude/settings.json 未按 git 根目录解析（3 评论）
- **摘要**: 从子目录启动时，settings.json 按 literal cwd 查找而非 git 根目录，导致项目级设置被忽略。
- **链接**: https://github.com/anthropics/claude-code/issues/74023

### 🔟 #72274 — [BUG] 跨会话凭据泄露：生产数据库被恶意修改（2 评论）
- **摘要**: 用户发现自己会话中出现了另一用户的服务器凭据，导致非授权主机修改了生产数据库，安全风险极高。
- **为什么重要**: 数据表明存在严重的跨会话隔离漏洞，需紧急检查。
- **链接**: https://github.com/anthropics/claude-code/issues/72274

---

## 重要 PR 进展（全部 7 个，当日更新）

由于当日 PR 数量有限，以下列出所有被更新的 PR：

### 1️⃣ #74021 — [OPEN] fix(security-guidance): 允许 findings 字段为 null
- **作者**: sourabharsh
- **摘要**: agentic commit reviewer 的 `FINDINGS_SCHEMA` 要求 findings 为数组，但模型有时返回 null，导致 schema 校验失败浪费一次轮次。本次修复允许 null。
- **链接**: https://github.com/anthropics/claude-code/pull/74021

### 2️⃣ #74010 — [OPEN] enhance(feature-dev): 为 code-architect agent 添加系统设计模式、边界案例和运营上下文
- **作者**: sourabharsh
- **摘要**: 在 `feature-dev` 插件的 code-architect agent 中新增三个步骤，弥补高层系统设计与代码库具体架构之间的鸿沟。
- **链接**: https://github.com/anthropics/claude-code/pull/74010

### 3️⃣ #74009 — [OPEN] fix(plugin-dev): 将 skill-development 和 plugin-settings 描述中的 "wants to" 改为 "asks to"
- **作者**: sourabharsh
- **摘要**: 完成 #13204 的 API 描述一致性修复，此前有两个技能被遗漏。
- **链接**: https://github.com/anthropics/claude-code/pull/74009

### 4️⃣ #74007 — [CLOSED] enhance(feature-dev): 与 #74010 相同但已关闭（重复）
- **链接**: https://github.com/anthropics/claude-code/pull/74007

### 5️⃣ #73999 — [CLOSED] fix(plugin-dev): 与 #74009 相同但已关闭（重复）
- **链接**: https://github.com/anthropics/claude-code/pull/73999

### 6️⃣ #42701 — [CLOSED] fix init-firewall.sh crash from ipset: 处理重复 IP
- **作者**: michaelkonecny
- **摘要**: devcontainer 启动时因 marketplace.visualstudio.com 解析出重复 IP 导致 ipset 报错退出，添加 `-exist` 开关解决。
- **链接**: https://github.com/anthropics/claude-code/pull/42701

### 7️⃣ #66854 — [OPEN] 拼写错误/toekn（无描述）
- **作者**: apaimabong-design
- **摘要**: 无有效描述，疑似测试或误操作。
- **链接**: https://github.com/anthropics/claude-code/pull/66854

---

## 功能需求趋势

根据当日 Issue 和 PR 数据，社区最关注的功能方向如下：

1. **多账户/工作区切换**（#36151）：个人与工作环境分离，无共享邮箱支持。
2. **Linux 桌面版**（#65697）：需求迫切，495 👍 为社区最高。
3. **diff 比较支持任意分支**（#23626）：开发工作流中常见需求。
4. **AskUserQuestion 超时配置**（#73125、#73105）：用户希望能完全控制工具行为，而非被强制自动跳过。
5. **权限模式精细化**（v2.1.200 默认改为 Manual 已部分回应）：但仍需更多自定义策略，如 `--dangerously-skip-permissions` 在 fullscreen 下失效等问题（#72479）。
6. **安全与隔离**（#72274 凭据泄露、#59296 敏感文件过滤、#65122 shell 输出密文脱敏）：安全类需求逐渐增多。
7. **模型行为可预测性**（#70315 幻觉问题、#67051 文本被吞问题）：用户期望助手文本能可靠呈现。

---

## 开发者关注点

高频痛点与反馈梳理：

- **AskUserQuestion 自动继续引发误操作**：v2.1.200 虽已改为默认 Manual，但用户仍希望超时完全可配置或移除。多个高赞 Issue 要求恢复无限等待。
- **会话限制逻辑混乱**：使用率仅 84% 却触发限流（#19673），长年未修复，严重影响工作连续性。
- **模型幻觉问题**（#70315）重复报告被 bot 错误关闭，用户表示无法信任 Opus 4.8，呼吁人工核查。
- **设置文件路径解析错误**（#74023）：从子目录启动时 `.claude/settings.json` 无法加载，导致项目配置丢失。
- **跨会话安全隔离不足**（#72274、#74066）：出现其他用户的凭据或上下文，需紧急评估 session/cache 沙箱机制。
- **REPL 工具缓存导致读取空字符串**（#74069）：`cat()` 对重复文件返回空而非错误，下游脚本可能覆写真实文件。
- **macOS TCC 权限问题**（#74068）：权限弹窗显示版本号而非应用名，每次升级权限重置。
- **桌面端 Ghost 会话残留**（#73675）：Remote Control 面板中已死亡会话无法清除。
- **日程调度器重启后重放任务**（#74055）：重启后重复执行已完成的每日任务，且忽略 `enabled: false`。

整体而言，社区对 **行为可预测性** 和 **安全隔离** 的诉求明显上升，而新版对 AskUserQuestion 的改动虽意图向好，但执行细节仍引发大量反馈。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# 2026-07-04 OpenAI Codex 社区动态日报

## 📡 今日速览

今日社区焦点集中在 **GPT-5.5 模型在特定内部响应接口（Responses-Lite）上的兼容性故障**——多个 issue 报告该模型被拒绝使用，而 GPT-5.4 正常。同时 **Windows 平台稳定性** 与 **上下文压缩丢失 AGENTS 规则** 两大长期问题持续发酵。在开发侧，安全团队密集提交了一组 **Git 操作安全加固 PR**，旨在隔离恶意仓库对 patch、merge、staging 等流程的潜在注入攻击。

## 🚀 版本发布

- **[rust-v0.143.0-alpha.35](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.35)**  
  仅发布标记，无详细变更日志。属于 Rust 组件的小版本 alpha 迭代，预计包含一些底层修复。

## 🔥 社区热点 Issues（Top 10）

1. **#30224 – 模型不支持 X-OpenAI-Internal-Codex-Responses-Lite**  
   [链接](https://github.com/openai/codex/issues/30224) | 评论 68 | 👍 22  
   **重要性**：Plus 用户在 Win11 上使用 Codex 时，GPT-5.5 报错“This model is not supported when using X-OpenAI-Internal-Codex-Responses-Lite”，而 GPT-5.4 正常。该问题已持续多日，影响面广，社区呼吁官方明确该动态开关的适用范围与修复时间表。

2. **#7291 – VSCode 扩展撤销更改失败**  
   [链接](https://github.com/openai/codex/issues/7291) | 评论 47 | 👍 16  
   **重要性**：macOS + VSCode 0.4.46 环境下，Codex 执行更改后无法正确 revert，影响日常开发回滚操作。虽已提出较长时间，仍未被标记为 closed，表明修复存在复杂性。

3. **#30364 – GPT-5.5 推理 token 聚类导致复杂任务性能下降**  
   [链接](https://github.com/openai/codex/issues/30364) | 评论 37 | 👍 53  
   **重要性**：用户发现 gpt-5.5 的 `reasoning_output_tokens` 高度集中在 516/1034/1552 等固定边界，推测与内部 token 管理策略有关，导致复杂推理任务效果退化。该 issue 获最高赞数，反映社区对模型行为透明度的迫切需求。

4. **#20214 – Windows 11 Pro 上 Codex App 频繁卡顿/冻结**  
   [链接](https://github.com/openai/codex/issues/20214) | 评论 27 | 👍 40  
   **重要性**：尽管系统资源充足，App 仍频繁卡顿。该问题已存在两个多月，是 Windows 平台上最受抱怨的性能 bug。

5. **#25792 – 上下文压缩忘记 AGENTS 规则，任务进度回退**  
   [链接](https://github.com/openai/codex/issues/25792) | 评论 12 | 👍 0  
   **重要性**：长任务中 Codex 自动压缩上下文后，子 agent 的进度从 97% 跳到 42%，严重破坏任务连续性。虽点赞数不高，但描述详实，属于影响开发效率的严重逻辑缺陷。

6. **#30595 – macOS CLI 认证异常：同一账号 Windows 可用但 macOS 报错**  
   [链接](https://github.com/openai/codex/issues/30595) | 评论 11 | 👍 0  
   **重要性**：macOS 上的 Codex CLI 将 ChatGPT 认证请求错误路由到 Responses-Lite 导致失败，而 Windows 正常。显示平台间认证策略不一致。

7. **#30406 – GPT-5.5 在 macOS Codex App 上同样因 Responses-Lite 失败**  
   [链接](https://github.com/openai/codex/issues/30406) | 评论 10 | 👍 2  
   **重要性**：与 #30224 类似，但明确发生在 macOS 平台，进一步印证该问题跨平台、跨版本地影响 GPT-5.5。

8. **#30009 – Windows sandbox 下 apply_patch 失败**  
   [链接](https://github.com/openai/codex/issues/30009) | 评论 20 | 👍 4  
   **重要性**：Windows 系统上文件编辑通过 `apply_patch` 时，sandbox 返回环境错误，导致代码修改无法落地。WSL 用户同样受影响。

9. **#26429 – Computer Use 插件在桌面重启后不可用**  
   [链接](https://github.com/openai/codex/issues/26429) | 评论 9 | 👍 3  
   **重要性**：macOS Desktop 上 Computer Use 插件在重启后消失，需要在设置中重新启用。用户抱怨频繁断联影响自动化工作流。

10. **#31033 – 上下文自动压缩 bug 导致消耗重置信令异常**  
    [链接](https://github.com/openai/codex/issues/31033) | 评论 4 | 👍 0  
    **重要性**：最新版（26.623.101652）中上下文压缩逻辑似乎提前触发，消耗重置额度但未正确释放上下文，且无明显告警。新提交的 issue 可能指向近期回归。

## 🛠 重要 PR 进展（Top 10）

1. **#30848 – 在 patch 应用前阻止可执行 Git 过滤器**  
   [链接](https://github.com/openai/codex/pull/30848) | 作者: bookholt-oai  
   **内容**：在 patch apply、preflight、revert 前，禁止仓库选择的 clean/smudge/process 过滤器运行，防止恶意配置通过 Git 操作执行任意命令。

2. **#31072 – 将 patch 应用绑定到受保护的 Git 配置**  
   [链接](https://github.com/openai/codex/pull/31072) | 作者: bookholt-oai  
   **内容**：确保验证后的 Git 配置与执行 patch 的子进程绑定，防止后续代码重新构造命令绕过安全检查。

3. **#31071 – 授权 patch 操作前的 Git include 配置源**  
   [链接](https://github.com/openai/codex/pull/31071) | 作者: bookholt-oai  
   **内容**：递归解析 `include.path` 和 `includeIf` 引入的配置文件，防止仓库通过间接配置注入恶意 alias、filter 等。

4. **#31070 – 授权 patch 操作前的主要配置源**  
   [链接](https://github.com/openai/codex/pull/31070) | 作者: bookholt-oai  
   **内容**：限制 Git 加载初始配置的环境变量路径（如 HOME、XDG、Windows Profile），确保 patch 不使用来自工作树或仓库控制的主要配置文件。

5. **#31069 – 为 patch 操作绑定 Git 配置环境变量**  
   [链接](https://github.com/openai/codex/pull/31069) | 作者: bookholt-oai  
   **内容**：将 `GIT_CONFIG_*` 等环境变量在验证与执行间保持一致，防止子进程读取不同配置源导致验证失效。

6. **#30395 – [app-server] 暴露 rate-limit 重置信用详情**  
   [链接](https://github.com/openai/codex/pull/30395) | 作者: jayp-oai  
   **内容**：在 `account/rateLimits/read` 接口中新增可用信用额度、过期时间等字段，为前端兑换 UI 提供数据支持。

7. **#30488 – [codex-cli] 在兑换选择器中显示重置详情**  
   [链接](https://github.com/openai/codex/pull/30488) | 作者: jayp-oai  
   **内容**：用户打开“兑换使用限制重置”时，列出所有可用信用及其过期时间，提升操作透明度。

8. **#31058 – [core] 重试模型容量错误**  
   [链接](https://github.com/openai/codex/pull/31058) | 作者: steipete-oai  
   **内容**：对 HTTP 503（容量不足）响应增加最多三次重试，间隔 30 秒/2 分钟/5 分钟（带抖动），减少因临时容量满导致的请求失败。

9. **#30896 – 集中 Git helper 启动的仓库授权**  
   [链接](https://github.com/openai/codex/pull/30896) | 作者: bookholt-oai  
   **内容**：创建操作级别的 Git 可执行文件信任策略，避免重复验证开销，并解决 Windows 上多步操作的不一致问题。

10. **#30837 – 通过 Git 推导有效的 patch 路径**  
    [链接](https://github.com/openai/codex/pull/30837) | 作者: bookholt-oai  
    **内容**：不再自行解析 diff 头，而是利用 Git 返回实际影响路径，防止重命名、复制或误导性头部导致后续安全策略失效。

## 📊 功能需求趋势

- **多层模型/子 Agent 配置**（#14039）：社区强烈希望主会话与子 agent 能选用不同模型、提供商或配置 profile，以灵活应对不同任务类型。
- **多 Git 仓库父目录支持**（#26338）：大型项目常包含多个独立仓库，用户期望 Codex App 能识别并管理此类工作区。
- **App 与 Client 实时同步**（#31062）：Pro 用户提出跨设备 session 同步需求，避免在桌面端和 CLI 间切换时丢失上下文。
- **文件查看器增强**（#22095）：建议保留滚动位置，支持 Page Up/Down 翻页，提升大型文件浏览体验。
- **Dock 图标自定义回归**（#28861）：App 图标中“Codex Light”与默认图标无区别，期望恢复可区分的视觉设计。

## 👀 开发者关注点

- **Responses-Lite 机制不透明**：大量 issue 指向 GPT-5.5 被拒绝而 GPT-5.4 正常，内部路由逻辑对用户不可见，开发者建议官方提供模型兼容性文档或客户端侧报错区分。
- **Windows WSL 生态兼容性顽疾**：包含 sandbox 路径映射、Computer Use 不可用、后台弹出 PowerShell 窗口、权限批准循环等问题，Windows 用户体验明显落后 macOS。
- **上下文压缩逻辑的副作用**：自动压缩导致 AGENTS 规则丢失、进度回退、重置额度错误消费，长任务可靠性堪忧。
- **认证与平台一致性**：同一账号 macOS 和 Windows 行为不同（CLI 路由、桌面与浏览器 limit 不同步），需要统一认证与限流策略。
- **子 Agent 管理缺陷**：`close_agent` 可能永久阻塞父线程（#31036），`/agent` 命令列出子 agent 但无法选择切换（#30813），多 agent 场景下的线程与界面交互不成熟。
- **Git 安全基线持续加固**：bookholt-oai 团队连续提交 10+ 个 PR 聚焦 Git 配置注入与路径穿越，表明 Codex 内部已将针对恶意工作树的攻击列为高优先级安全课题。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*