# AI CLI 工具社区动态日报 2026-06-19

> 生成时间: 2026-06-19 03:55 UTC | 覆盖工具: 2 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

好的，作为专注 AI 开发工具生态的资深技术分析师，我将基于您提供的两份日报，为您生成一份横跨 Claude Code 与 OpenAI Codex 的横向对比分析报告。

---

### AI CLI 工具生态横向对比报告 (2026-06-19)

#### 1. 生态全景

当前 AI CLI 工具正从“新奇体验”阶段快速迈入“生产环境依赖”阶段。社区反馈的焦点已从“能否生成代码”转向“能否稳定、安全、可控地融入现有开发工作流”。两大主流工具——Claude Code 与 OpenAI Codex——均处于高频迭代期，但稳定性和用户体验的“地基”仍不牢固，尤其在跨平台兼容性、服务端限流策略及配置管理方面存在显著痛点。企业级特性（如团队管理、成本控制）和第三方集成（MCP/插件生态）成为新的价值角力点。

#### 2. 各工具活跃度对比

| 维度 | Claude Code | OpenAI Codex |
| :--- | :--- | :--- |
| **版本发布** | 1 个 (v2.1.183) | 4 个 (v0.141.0正式版 + v0.142.0三个alpha) |
| **社区热点 Issues** | 10 个 (高热度: 速率限制、多账户) | 10 个 (高热度: 手机验证、macOS性能) |
| **重要 PR 进展** | 3 个 | 10 个 |
| **关键结论** | 发布节奏相对稳健，社区问题聚焦于**服务稳定性**和**安全控制**。 | 迭代速度更快（alpha版本密集），社区问题呈现**多平台、多场景**的分散性，PR贡献活跃，生态建设投入大。 |

#### 3. 共同关注的功能方向

社区对以下方向表现出跨工具的共性诉求：

| 功能方向 | Claude Code 具体体现 | OpenAI Codex 具体体现 |
| :--- | :--- | :--- |
| **速率限制与API稳定性** | **核心痛点**。Issue #38350 (异常速率限制)、#53915 (API限流错误)，评论数与点赞数极高。 | **核心痛点**。Issue #28879 (Plus计划限流成本飙升)、#28811 (重置机制问题)，直接影响付费用户。 |
| **跨平台稳定性** | **Windows** (UI卡顿 #26302)、**macOS** (渲染问题，多版本反馈)。问题集中在界面与渲染。 | **macOS** (性能问题 #25719，`syspolicyd`高CPU)、**Windows** (沙箱ACL #15777，WSL Agent #16815)。问题更底层，涉及系统资源与进程。 |
| **MCP/插件生态深化** | Issue #69487 (MCP工具无限挂起，无超时机制)，关注工具链的鲁棒性。 | 多个PR聚焦MCP OAuth授权流程 (#29022, #29018)，关注协议标准化与安全性。 |
| **配置管理与隔离** | Issue #20944 (禁用自动IDE选择上下文)，关注成本与误操作控制。 | Issue #14601 (配置污染)，强调将项目级设置从全局配置中分离。 |
| **安全与权限控制** | v2.1.183 重点增强了对危险Git操作的防护，社区反响积极。 | PR #29013 (保护MITM CA私钥)，关注沙箱环境的权限隔离。 |

#### 4. 差异化定位分析

| 维度 | Claude Code | OpenAI Codex |
| :--- | :--- | :--- |
| **功能侧重** | **安全与守成**。强化对用户本地环境的保护（如Git操作防护），关注指令遵循的精确度，社区更希望减少“意外破坏”。 | **开放与集成**。大力投入MCP协议、OAuth流程，构建更复杂的沙箱和运行时环境，目标是成为更底层的开发平台。 |
| **目标用户** | 偏向**个人开发者与独立团队**。反馈中多账户隔离、移动端需求等，体现出对个人工作流与场景隔离的重视。 | 偏向**企业级与高阶用户**。对Git客户端兼容性、WSL集成、Token预算控制、OAuth流程等有明确需求，更关注复杂工作流的串联与安全。 |
| **技术路线** | **稳健迭代**。版本号平滑递增，修复优先（如修复分页逻辑），社区提出的“团队管理回归”是主力版本体验。 | **激进创新**。大量Alpha版本并行，围绕Rust运行时、MCP协议、Noise信道等前沿技术进行基础设施重构，PR数量多、范围广。 |

#### 5. 社区热度与成熟度

- **社区热度（互动深度）**:
    - **Claude Code**: 社区讨论更“集中”，问题多集中于少数几个核心痛点（速率限制、多账户），形成高热度Issue。单条Issue的评论数可达60+，用户互动深度高。
    - **OpenAI Codex**: 社区讨论更“分散”，问题覆盖更广的维度（性能、兼容性、配置、UI），虽然单个Issue热度可能不及Claude，但PR贡献量（10个）远超Claude（3个），表明其社区的技术贡献意愿更强。

- **生态成熟度**:
    - **Claude Code**: 处于“由新变稳”阶段。核心功能成熟，但服务端（限流）和客户端（终端渲染）的稳定性是最大短板，用户更期待“修复bug”而非“添加新功能”。
    - **OpenAI Codex**: 处于“快速生长”阶段。项目结构（Rust运行时）、协议标准（MCP）和平台兼容性仍在剧烈演进，功能回归（如#28978桌面版新建对话失败）频繁，用户需要更高的容错预期。

#### 6. 值得关注的趋势信号

1.  **安全治理成为第一议题**: Claude Code 主动限制危险 Git 操作，OpenAI Codex 保护沙箱内 CA 私钥。这表明 AI 工具的“攻击面”意识已觉醒，安全不再只是网络问题，更是操作层面的“Guardrail”（护栏）。开发者应主动了解并配置这些安全策略。

2.  **服务透明度的信任危机**: 两个工具社区均爆发对“速率限制”和“成本消耗”的强烈不满（Claude Code #38350, #53915；OpenAI Codex #28879）。这警示平台方：**任何非公开、非透明的服务端计费或限流变更，都将严重侵蚀用户信任**。对于开发者，需建立自身的成本监控与用量预警机制。

3.  **跨平台兼容性是“隐形门槛”**: 大量 Bug 集中在 macOS 和 Windows 的特定问题上。对于决策者而言，在选择 AI CLI 工具作为团队标准时，**必须将目标团队的主用操作系统平台的兼容性与稳定性作为关键评估项**。忽视这一点可能导致工具在团队内部推广受阻。

4.  **从“工具”到“平台”的演进加速**: OpenAI Codex 在 MCP 协议、OAuth、CA 证书、沙箱隔离等方面的深度投入，标志着其野心远超“代码助手”，而是成为开发者本地的**智能基础设施**。开发者社区也应提前思考，如何构建兼容 MCP 等开放标准的流水线。

5.  **从“追求能力”到“追求控制”**: 社区对“自动IDE选择上下文 (#20944)”、“Token预算管理 (#28707)”、“更简洁的回复 (#29028)”等需求的涌现，表明开发者已不再满足于 AI 生成代码的能力，而是开始精细化管理 **AI 如何与自己协作**。这将是未来工具差异化竞争的关键。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，作为一名专注于 Claude Code 生态的技术分析师，以下是我基于 `anthropics/skills` 仓库数据（截至 2026-06-19）提供的社区热点报告。

---

### Claude Code Skills 社区热点报告

#### 1. 热门 Skills 排行

根据 PR 评论活跃度、社区反馈及讨论深度，以下为最受关注的 5 个 Skills：

- **文档排版优化 Skill (document-typography)**
  - **功能**: 自动修复 AI 生成文档中的“孤词”、“寡行”和编号错位等排版问题。
  - **社区热点**: 社区普遍认可这是一个高价值“痛点型”技能，能显著提升 AI 生成文档的专业度和可读性。讨论集中在实现细节和覆盖场景的边界。
  - **状态**: **OPEN**
  - **链接**: [PR #514](https://github.com/anthropics/skills/pull/514)

- **ODT 文档处理 Skill (odt)**
  - **功能**: 创建、填充、读取及转换 OpenDocument 格式 (.odt, .ods) 文件。
  - **社区热点**: 响应了企业环境下对开源标准格式（特别是 LibreOffice）的强需求。讨论点在于如何高效处理模板填充及 HTML 转换。
  - **状态**: **OPEN**
  - **链接**: [PR #486](https://github.com/anthropics/skills/pull/486)

- **Skill Creator 工具链修复与功能增强 (Run_eval, subprocess, UTF-8 等)**
  - **功能**: 这是多个 PR 的集合，核心是修复 `skill-creator` 脚本的 `run_eval.py` 在 Windows 平台和特定数据格式下的崩溃和零召回率问题。
  - **社区热点**: 这是近期社区最核心的讨论点之一。大量用户反馈 `run_eval.py` 出现 0% 召回率，导致技能优化流程完全失灵。多个 PR（如 #1298, #1099, #1050, #362）尝试解决子进程调用、编码解析、路径兼容等问题，说明该工具链的稳定性和跨平台兼容性是阻碍社区贡献的主要瓶颈。
  - **状态**: **OPEN**
  - **链接**: [PR #1298](https://github.com/anthropics/skills/pull/1298), [PR #1099](https://github.com/anthropics/skills/pull/1099)

- **SAP 预测分析 Skill (SAP-RPT-1-OSS)**
  - **功能**: 集成 SAP 开源的 Tabular Foundation Model，用于对 SAP 业务数据进行预测性分析。
  - **社区热点**: 代表了社区对垂直领域、企业级 AI 技能的浓厚兴趣。讨论焦点在于如何精简模型调用流程，以及该技能与现有 SAP 生态的融合程度。
  - **状态**: **OPEN**
  - **链接**: [PR #181](https://github.com/anthropics/skills/pull/181)

- **前端设计 Skill 优化 (frontend-design)**
  - **功能**: 重构现有前端设计 Skill，使其指令更清晰、更具可执行性，并确保每一条指导都可在单次对话中完成。
  - **社区热点**: 反映了社区对“技能可操作性”的深度诉求。讨论不再局限于“做什么”，而是关注“如何精准地引导 Claude 做”。这是一个元层面的改进，旨在提升所有相关技能的质量。
  - **状态**: **OPEN**
  - **链接**: [PR #210](https://github.com/anthropics/skills/pull/210)

#### 2. 社区需求趋势

从热门 Issues 中可提炼出三个最集中的需求方向：

- **企业级协作与安全**
  - **组织内技能共享**: [Issue #228](https://github.com/anthropics/skills/issues/228) 获得 14 条评论和 7 个赞，是企业用户最核心的诉求。用户强烈希望能在组织内直接共享和发现技能，而非通过文件传输。
  - **信任与安全边界**: [Issue #492](https://github.com/anthropics/skills/issues/492) 提出了社区技能在官方命名空间下分发的信任边界问题，反映了对安全性的日益关注。

- **AI Agent 治理与基础设施**
  - **Agent 治理模式**: [Issue #412](https://github.com/anthropics/skills/issues/412) 提议增加“Agent-Governance”技能，关注 AI Agent 系统的策略执行、威胁检测和审计，表明社区思考已从“技能制作”延伸到了“技能管理”。
  - **基础工具稳定性**: [Issue #556](https://github.com/anthropics/skills/issues/556) 和 [Issue #1169](https://github.com/anthropics/skills/issues/1169) 连续报告 `run_eval.py` 工具无法正常工作，成为社区开发和优化的主要障碍。这突显了稳定、可靠的基础设施对生态繁荣的重要性。

- **平台标准化与可扩展性**
  - **Skills 作为 MCPs 暴露**: [Issue #16](https://github.com/anthropics/skills/issues/16) 提出将 Skills 的 API 以 MCP 协议暴露，以便于标准化集成。这体现了社区对 Skills 可组合性和标准化接口的长期期望。
  - **多平台支持与应用**: [Issue #29](https://github.com/anthropics/skills/issues/29) 反复出现，用户期望 Skills 能无缝应用于 AWS Bedrock 等云端平台。

#### 3. 高潜力待合并 Skills

以下是一些讨论活跃、价值明显、有望在近期合并的 PR：

- **文档处理全家桶**: **document-typography** [PR #514](https://github.com/anthropics/skills/pull/514)、**odt** [PR #486](https://github.com/anthropics/skills/pull/486) 和针对 PDF/DOCX 的修复 [PR #538](https://github.com/anthropics/skills/pull/538) 及 [PR #541](https://github.com/anthropics/skills/pull/541)。社区对文档质量的反馈非常积极，这些技能被合并的可能性极高。
- **工具链稳定性修复**: 合并多个修复 `skill-creator` 的 PR，例如 **Windows 兼容性修复** [PR #1298](https://github.com/anthropics/skills/pull/1298) 和 **YAML 解析检查** [PR #539](https://github.com/anthropics/skills/pull/539)。只有解决了这些痛点，社区贡献的积极性才能被释放。
- **企业级领域技能**: **SAP 预测分析** [PR #181](https://github.com/anthropics/skills/pull/181) 和 **ServiceNow 平台 Skill** [PR #568](https://github.com/anthropics/skills/pull/568) 代表了社区在垂直领域深耕的尝试，一旦通过审核，将吸引大量企业用户。

#### 4. Skills 生态洞察

**当前社区的核心诉求是“稳定性”与“协作性”的博弈：社区不再满足于创造单个技能，而是渴望建立一套稳定、可共享、可治理的技能生态系统。**

一方面，社区致力于通过修复工具链（如 `run_eval`）和跨平台兼容性（Windows）来构建稳定的“创造”环节；另一方面，强烈呼吁通过组织内共享、MCPs 标准和安全审计来打通“使用”和“管理”环节。这表明 Claude Code Skills 正从“个人开发者的兴趣实验”阶段，快速迈向“企业级平台的工具管理”阶段，而基础设施的稳定和社区治理的完善是下一阶段发展的关键。

---

好的，这是为您生成的 2026年6月19日 Claude Code 社区动态日报。

---

# Claude Code 社区动态日报 ｜ 2026-06-19

## 今日速览

Claude Code 今日发布 v2.1.183，重点加强了自动模式下对危险 Git 操作的安全防护。社区方面，关于“异常速率限制”和“API 请求限流”的讨论热度极高，已成为开发者普遍关注的痛点。此外，多个版本的终端显示渲染问题引起了广泛吐槽，已有用户通过系统回溯定位到具体回归版本。

## 版本发布

### v2.1.183 安全增强更新
- **描述**: 官方发布小版本更新，主要聚焦于 Git 操作安全。
- **内容**:
  - **自动模式安全加固**: 现在，当用户未明确要求丢弃本地工作时，`git reset --hard`、`git checkout -- .`、`git clean -fd` 和 `git stash drop` 等危险命令将被阻止执行。
  - **提交管理保护**: `git commit --amend` 操作现在被限制，只有当本次会话中的 agent 发起了该提交时才能执行，防止意外修改。
- **链接**: [v2.1.183 Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.183)

## 社区热点 Issues

1.  **[#36151] 多账户切换功能需求** - 评论最多的 Issue，用户强烈要求在 Claude 移动应用中实现不共享邮箱的多账户切换。社区呼声极高 (👍 352)，反映出专业用户对隔离工作与个人场景的强烈需求。
    - **链接**: [Issue #36151](https://github.com/anthropics/claude-code/issues/36151)

2.  **[#38350] 异常/膨胀的速率限制与会话使用量** - 核心Bug报告，大量用户反馈（62条评论）遭遇了异常高的速率限制和会话消耗，严重影响使用体验，尤其集中在 macOS 平台。
    - **链接**: [Issue #38350](https://github.com/anthropics/claude-code/issues/38350)

3.  **[#53915] API 服务器限流错误** - 另一个关于速率限制的“高频”Bug，Windows 和 VS Code 用户频繁遇到“Server is temporarily limiting requests”的 API 错误，表明服务端限流策略存在问题。
    - **链接**: [Issue #53915](https://github.com/anthropics/claude-code/issues/53915)

4.  **[#26302] Windows 平台桌面版 UI 严重卡顿** - 一个长期存在的问题，用户报告在 Windows 上更新后出现了严重的 UI 延迟和鼠标卡顿（性能回归），对桌面端体验影响大。
    - **链接**: [Issue #26302](https://github.com/anthropics/claude-code/issues/26302)

5.  **[#68721] 团队管理工具回归** - 在 v2.1.178 版本中，原生的团队管理工具 `TeamCreate` / `TeamDelete` 功能消失（回归），直接影响了企业级用户的工作流。
    - **链接**: [Issue #68721](https://github.com/anthropics/claude-code/issues/68721)

6.  **[#26073] Windows MSIX 配置路径错误** - 一个危险的配置漏洞，Windows MSIX 安装版本的“Edit Config”功能会打开错误的配置文件，导致 MCP 服务器静默失效，使用者可能无感知。
    - **链接**: [Issue #26073](https://github.com/anthropics/claude-code/issues/26073)

7.  **[#20944] 禁用自动 IDE 选择上下文** - 用户希望增加设置以禁用自动的 IDE 选择上下文功能，认为其增加了不必要的成本并可能导致误操作。
    - **链接**: [Issue #20944](https://github.com/anthropics/claude-code/issues/20944)

8.  **[#58429] 辅助功能：语音播报请求** - 社区关注到无障碍需求，请求内置将 Claude 响应语音朗读的功能，适用于视障用户或无手操作的场景。
    - **链接**: [Issue #58429](https://github.com/anthropics/claude-code/issues/58429)

9.  **[#35319] 技能调用追踪与分析** - 企业级用户需求，希望获得技能（Skills）的调用追踪和使用分析能力，以更好地进行成本管理和采纳分析。
    - **链接**: [Issue #35319](https://github.com/anthropics/claude-code/issues/35319)

10. **[#69487] MCP 工具调用无限挂起** - 一个严重的新Bug，指出 MCP 工具调用在客户端没有超时机制，可能导致进程无限期等待，影响工具链的鲁棒性。
    - **链接**: [Issue #69487](https://github.com/anthropics/claude-code/issues/69487)

## 重要 PR 进展

1.  **[#69470] 修复“锁定陈旧议题”工作流** - 修复了长期失败（53天连续失败）的自动化工作流，使用搜索 API 替代了分页 offset。极大改善了仓库维护的健康度。
    - **链接**: [PR #69470](https://github.com/anthropics/claude-code/pull/69470)

2.  **[#68673] 修复脚本分页逻辑** - 也对分页逻辑进行了修复，确保在页面未满时也能正确终止分页，而非等到页面为空，与 #69470 共同优化了自动化脚本的稳定性。
    - **链接**: [PR #68673](https://github.com/anthropics/claude-code/pull/68673)

3.  **[#23972] 修复 hookify 插件的 Python 兼容性** - 一个长期开放的 PR，旨在修复 hookify 插件对 Python 3.8 的兼容性和规则加载问题，体现了社区对兼容性的贡献。
    - **链接**: [PR #23972](https://github.com/anthropics/claude-code/pull/23972)

> **注**: 当前活跃的 PR 数量较少，主要集中在修复脚本和兼容性问题。

## 功能需求趋势

- **多账户/角色隔离**: 社区强烈希望能够在同一设备上无缝切换不同账号，以区分个人和职业使用场景。
- **服务稳定性与成本**: “速率限制”、“API 限流”和“会话计费问题”是压倒性的关注热点，用户对于服务质量和成本的透明度有极高要求。
- **IDE 深度集成**: 除了已有的 VS Code，社区对 **JetBrains** 系列 IDE 的官方集成呼声很高，反映了专业开发者的主流选择。
- **MCP 工具链增强**: 围绕 MCP 工具的使用，用户提出了包括 **客户端超时机制**、**更好的错误反馈** 以及 **配置管理** 在内的多项改进需求。
- **无障碍与可访问性**: 语音播报、键盘导航等无障碍功能开始受到关注，表明用户群体正在扩大。
- **终端渲染稳定性**: 多个 Issue 反馈了终端显示问题（乱码、闪烁、文本选择失效），显示终端体验的稳定性是当前最需要改善的用户体验点之一。

## 开发者关注点

- **速率限制与API错误是最大痛点**: 多个高热度Issue均指向API服务端的限流和错误，开发者日常工作流的连续性受到严重干扰。这需要 Anthropic 尽快查明原因并解决。
- **对“破坏性操作”的安全意识加强**: 新版对 Git 危险命令的限制受到欢迎，但同时也反映了用户对 AI 可能产生的非预期破坏性操作存在普遍担忧。社区的潜在诉求是更强的控制感和可预见性。
- **平台特定Bug频繁**: Windows 的 UI 性能、macOS 的显示渲染、Linux 的团队工具回归，表明跨平台兼容性依然是很大的挑战，新版发布后容易出现特定平台的回归。
- **缓存与成本问题**: 用户对于“新会话永远无法命中缓存”的问题表现出敏锐的观察力（#47098），表明开发者非常在意服务调优的细节和成本控制，希望缓存机制更智能。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，这是为您生成的 2026-06-19 OpenAI Codex 社区动态日报。

---

# OpenAI Codex 社区动态日报 | 2026-06-19

## 今日速览

今日，Codex 发布了两个重要的 Rust 运行时版本：v0.141.0 正式版和 v0.142.0 的多个 alpha 版本。与此同时，社区反馈中，macOS 性能问题（`syspolicyd`/`trustd` 高 CPU）和 Windows 平台的稳定性问题依然是痛点。此外，关于配置隔离和速率限制机制变化的讨论热度不减，开发者社区对基础体验的改进呼声很高。

## 版本发布

### Rust 运行时
- **v0.141.0 (正式版):** 主要更新内容：
    - **安全增强:** 远程执行器现在使用经过认证的、端到端加密的 Noise relay 通道进行通信。 (#26242, #26245)
    - **跨平台兼容性:** 跨平台远程执行现在能够保留执行器本机的工作目录和 Shell 环境，包括跨应用服务器和执行服务器边界的文件系统权限路径。
- **v0.142.0-alpha.1 / alpha.2 / alpha.3:** 发布了三个连续的 alpha 版本，预示着一个新的功能迭代周期即将到来。

## 社区热点 Issues

1.  **[#20161] [已关闭] 手机号验证不工作 | 点赞: 125 | 评论: 201**
    - **原因:** 该 Issue 是社区反馈的绝对热门，问题在于跨设备登录 SSO 时，Codex 会强制要求未绑定手机号的用户进行验证，导致无法正常使用。关闭状态可能意味着已经修复或计划修复。
    - **链接:** [Issue #20161](https://github.com/openai/codex/issues/20161)

2.  **[#25719] [开放] macOS 版 Codex Desktop 触发 `syspolicyd` / `trustd` CPU 和内存持续飙升 | 点赞: 40 | 评论: 33**
    - **原因:** 这是一个严重影响 macOS 用户体验的性能问题，导致系统资源被持续消耗。社区反应强烈，是 macOS 用户的核心痛点。
    - **链接:** [Issue #25719](https://github.com/openai/codex/issues/25719)

3.  **[#15777] [开放] Windows 沙箱安装损坏 `AppData` ACL 权限 | 点赞: 2 | 评论: 26**
    - **原因:** 这是一个长期存在的沙箱安装问题，会导致 Windows 用户 `AppData` 目录的访问控制列表损坏，影响其他应用程序，属于严重的环境破坏性 Bug。
    - **链接:** [Issue #15777](https://github.com/openai/codex/issues/15777)

4.  **[#14601] [开放] 配置污染：将 `projects.xxxx.trusted_level` 从 `config.toml` 中分离 | 点赞: 43 | 评论: 15**
    - **原因:** 社区希望将项目级信任设置在全局配置中分离出来，避免 `config.toml` 被项目污染，提升配置管理的整洁性和版本控制友好性。反映了开发者对良好工程实践的追求。
    - **链接:** [Issue #14601](https://github.com/openai/codex/issues/14601)

5.  **[#28988] [开放] macOS 版 “完全访问” 模式持续请求权限 | 点赞: 6 | 评论: 9**
    - **原因:** 最新桌面版更新后，“完全访问”模式在 macOS 上弹出无休止的权限请求，严重影响正常使用，是一个高频复现的回归 Bug。
    - **链接:** [Issue #28988](https://github.com/openai/codex/issues/28988)

6.  **[#28879] [开放] Plus 计划 `gpt-5.5` 模型速率限制成本飙升 10-20 倍 | 点赞: 4 | 评论: 5**
    - **原因:** 从 6月16日开始，Plus 用户的速率限制消耗急剧增加，导致预算快速耗尽。这直接关系到用户的付费体验，社区对这种非预期的变化表示担忧。
    - **链接:** [Issue #28879](https://github.com/openai/codex/issues/28879)

7.  **[#16815] [开放] Windows 上 WSL Agent 模式错误：路径反序列化失败 | 点赞: 7 | 评论: 9**
    - **原因:** WSL2 是 Windows 开发者的重要使用场景，此 Bug 导致 WSL Agent 模式完全不可用，阻碍了 Windows 下的 Linux 开发。
    - **链接:** [Issue #16815](https://github.com/openai/codex/issues/16815)

8.  **[#28978] [开放] 桌面版新对话失败：缺少 `inputSchema` 字段 | 点赞: 5 | 评论: 3**
    - **原因:** 这是一次桌面版自动更新后的严重回归，导致所有新对话都无法建立，且 CLI 正常，说明 Bug 出在桌面版应用层。对用户影响巨大。
    - **链接:** [Issue #28978](https://github.com/openai/codex/issues/28978)

9.  **[#28241] [开放] Codex turn-diff tree refs 破坏基于 libgit2 的 Git 客户端 | 点赞: 1 | 评论: 7**
    - **原因:** Codex 的 Git 操作与其他主流 Git 客户端（如 GitKraken, Fork）不兼容，破坏了开发者的日常 Git 工作流。
    - **链接:** [Issue #28241](https://github.com/openai/codex/issues/28241)

10. **[#28689] [开放] 更新后线程从侧边栏消失：迁移校验和不匹配 | 点赞: 1 | 评论: 2**
    - **原因:** 应用更新后，用户历史对话数据丢失，这是最令用户担忧的 Bug 类型之一，对用户信任度打击很大。
    - **链接:** [Issue #28689](https://github.com/openai/codex/issues/28689)

## 重要 PR 进展

1.  **[#29006] [开放] 保留模型上下文之外的技能描述**
    - **内容:** 解决了一个问题：加载技能元数据时因描述超过 1024 字符限制而丢弃技能，导致非模型消费者（如 UI）丢失完整信息。此 PR 旨在分离模型上下文和元数据存储。
    - **链接:** [PR #29006](https://github.com/openai/codex/pull/29006)

2.  **[#29035] [开放] 优化文件系统线程列表查询**
    - **内容:** 针对大量子 Agent 项目导致线程列表加载缓慢的问题，通过在读取 `SessionMeta` 前进行过滤，显著提高了交互式线程查询的性能。
    - **链接:** [PR #29035](https://github.com/openai/codex/pull/29035)

3.  **[#28489] [开放] 新增“索引化”网页搜索模式**
    - **内容:** 在 `cached` 和 `live` 之外，新增了 `indexed` 网页搜索模式，为托管搜索提供更细粒度的控制。
    - **链接:** [PR #28489](https://github.com/openai/codex/pull/28489)

4.  **[#28707] [开放] 在 Token 预算耗尽时中止任务**
    - **内容:** 实现了“Token 预算”功能的第三部分，当线程级别的 Token 预算用完后，能够优雅地中止当前任务，并返回明确的错误信息。
    - **链接:** [PR #28707](https://github.com/openai/codex/pull/28707)

5.  **[#29014] [开放] 支持启动时自定义 CA 证书包**
    - **内容:** 修复了当用户通过环境变量 `SSL_CERT_FILE` 指定自定义 CA 时，与 Codex 托管 MITM 代理的证书冲突问题。
    - **链接:** [PR #29014](https://github.com/openai/codex/pull/29014)

6.  **[#29013] [开放] 保护托管 MITM CA 私钥不被沙箱命令访问**
    - **内容:** 增强安全：将用于中间人攻击的 CA 私钥文件权限收紧，防止沙箱内的命令读取，防止权限提升。
    - **链接:** [PR #29013](https://github.com/openai/codex/pull/29013)

7.  **[#29022] [开放] 支持受保护资源的 OAuth 发现**
    - **内容:** 统一了 MCP 插件的 OAuth 授权流程，确保预检和登录都使用最新的 SDK 进行协议发现，避免因实现不一致导致的授权失败。
    - **链接:** [PR #29022](https://github.com/openai/codex/pull/29022)

8.  **[#29028] [开放] 收紧实时交互确认引导**
    - **内容:** 优化了 Codex 的实时前端提示词，鼓励模型给出更加简洁、多样的回复，减少重复的“好的”等确认性开场白。
    - **链接:** [PR #29028](https://github.com/openai/codex/pull/29028)

9.  **[#29011] [已关闭] 添加 `clock.current-time` 工具**
    - **内容:** 新增了一个名为 `clock.current_time` 的工具，允许模型在需要上下文时显式查询当前的日期和时间，提高了时间感知的准确性。
    - **链接:** [PR #29011](https://github.com/openai/codex/issues/29011)

10. **[#29018] [开放] MCP OAuth 刷新令牌保留在 Codex 中**
    - **内容:** 改进了 MCP 协议的 OAuth 刷新流程，确保刷新令牌在 Codex 内部进行管理，避免令牌泄露风险，并实现更可靠的凭证持久化。
    - **链接:** [PR #29018](https://github.com/openai/codex/pull/29018)

## 功能需求趋势

从今日的 Issues 和 PR 中可以提炼出社区最关注的几个功能方向：
- **配置与项目管理:** 社区强烈希望实现配置隔离（如 `#14601`），并支持在不同项目间移动对话（`#24519`），以实现更专业化的项目管理。
- **会话管理增强:** 新增 `/merge` 命令以合并不同会话的工作状态（`#29031`）是一个高频需求，这表明用户在处理复杂任务时，需要跨会话进行上下文整合。
- **跨平台与集成兼容性:** 大量的 Bug 报告集中在 macOS (`syspolicyd` 问题) 和 Windows（沙箱、WSL）的特定问题上，社区核心需求是保证基础功能的稳定性和与操作系统其他工具的兼容性。
- **MCP 协议集成深化:** 大量围绕 MCP 的 PR（`#29022`, `#29018`, `#28676`）表明，Codex 正在大力投入 MCP 协议的实现，以支持更丰富的插件生态和资源发现。

## 开发者关注点

开发者们当前的反馈痛点主要集中在以下几个方面：
- **稳定性是第一位:**
    - **macOS 性能问题 (Issue #25719):** `syspolicyd` / `trustd` 的高 CPU 占用是当前 macOS 用户的头号公敌，严重影响了日常开发。
    - **功能回归频繁:** 新版更新 (`#28988`, `#28978`, `#28689`) 频繁引入破坏性 Bug，导致“完全访问”模式不可用、对话无法创建甚至数据丢失，极大打击了用户对更新的信心。
    - **Windows 兼容性是长期痛点:** 沙箱 ACL 损坏 (`#15777`)、WSL Agent 模式故障 (`#16815`) 以及 Git 兼容性问题 (`#28241`) 反复出现，说明 Windows 平台的稳定性和测试覆盖仍有待加强。
- **付费体验的透明与公正:**
    - **速率限制成本剧增 (Issue #28879):** 开发者对无预警的速率限制消耗增加表示强烈不满，认为这是不透明的计费变更，直接损害了付费用户的权益。
    - **重置机制不一致 (Issue #28811):** 公开的速率限制重置未能按承诺的“存入银行”方式执行，引发了社区对 OpenAI 承诺的信任危机。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*