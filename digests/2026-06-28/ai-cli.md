# AI CLI 工具社区动态日报 2026-06-28

> 生成时间: 2026-06-28 03:25 UTC | 覆盖工具: 2 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

好的，作为专注于 AI 开发工具生态的资深技术分析师，根据您提供的两份详尽的社区动态日报，我为您整理了一份横向对比分析报告。

---

### **AI CLI 工具生态横向分析报告 (2026-06-28)**

**核心洞察：** AI CLI 工具正从“功能炫技”迈向“工程化稳定”阶段。当前社区的核心矛盾点在于：**AI 能力的快速迭代与工具稳定性的滞后**。用户不再满足于“能用”，而是要求“可靠”、“可控”和“透明”。无论是 Claude Code 的模型兼容性 Bug，还是 OpenAI Codex 的配额异常，都指向了同一问题——当 AI 模型能力和计费逻辑发生变更时，下游工具常常缺乏足够的韧性来平滑适应。

---

#### **1. 生态全景**

当前 AI CLI 工具生态呈现出 **“双雄并立，痛点趋同”** 的态势。一方面，两大主流工具均在积极扩展功能边界，如 Cowork 模式和 MCP 协议，但重度用户已开始遭遇 **稳定性瓶颈**——模型升级带来的破坏性变更、资源泄漏、计费模型不透明等问题，正在成为影响开发者粘性的关键挑战。整体而言，市场正从“抢占开发者心智”转向“稳固开发者信任”，工具链的健壮性和可观测性成为新的竞争焦点。

---

#### **2. 各工具活跃度对比**

| 工具/指标 | 今日热点 Issues (精选) | 重要 PR 进展 | 版本发布 | 社区热议程度 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 10个，聚焦 **Opus 4.7 Bug**、**Cowork 增强**、**Windows 兼容** | 1个 (内部脚本修复) | **无** 发布 | 讨论深度高，聚焦特定模型和架构问题 |
| **OpenAI Codex** | 10个，聚焦 **配额/计费异常**、**日志性能**、**跨平台支持** | 10+个，涵盖 MCP OAuth 重构、可观测性、企业策略 | **3个** Rust 预发布版 | 热度极高，讨论集中于服务端引发的付费用户痛点 |

**小结：** OpenAI Codex 今日的社区活跃度（按 Issues 和 PR 数量计）显著高于 Claude Code，且其社区问题多直接由服务端策略/计费变更引发，波及范围更广。Claude Code 的问题则更多集中在特定平台或模型功能的软件缺陷上。

---

#### **3. 共同关注的功能方向**

两大工具社区不约而同地将焦点放在了以下几个方面：

| 共同方向 | 具体表现 (Claude Code) | 具体表现 (OpenAI Codex) | 社区核心诉求 |
| :--- | :--- | :--- | :--- |
| **跨平台与桌面体验** | Windows ARM64 (Cowork 失效)，VSCode 扩展通知缺失 | 强烈要求 Linux 桌面应用，macOS/Windows 稳定性问题突出 | 用户希望在所有主流平台上获得一致、稳定的体验，而非“二等公民”。 |
| **权限与安全机制** | 终端可点击确认的误触问题，自动安全分类器导致工作流阻塞 | 强烈要求 `**.codexignore**` 等敏感文件排除机制 | 用户希望在“便捷性”和“安全性”之间拥有更多控制权，而非被动接受。 |
| **日志与资源管理** | MCP 服务器指令被静默截断 | SQLite 日志写放大 (SSD寿命)，MCP 进程/FD 泄漏 | 开发者开始重视工具的 **“副作用”** ，如对系统资源 (SSD、文件描述符) 的影响，要求工具更“绿色”和可控。 |

---

#### **4. 差异化定位分析**

| 维度 | Claude Code | OpenAI Codex |
| :--- | :--- | :--- |
| **功能侧重** | **深度 IDE 集成** (VSCode)、**协作模式** (Cowork)、**推理过程可视化** (思考摘要) | **企业级安全与管控** (Marketplace 策略)、**平台可观测性** (遥测日志)、**标准化协议** (MCP OAuth)、**配额透明** |
| **目标用户** | 个人开发者、AI 研究者、**Windows 用户** (当前关注重点) | **企业团队** (付费墙、企业策略)、**Linux 重度用户** (桌面应用)、**MCP 高级用户** (配置与稳定性) |
| **技术路线** | **模型能力驱动**：强调模型自身能力 (Opus 4.7 思考) 带来差异化体验，工具需要紧密适配模型变更。 | **平台工程化驱动**：通过 PR (如 MCP OAuth 重构、可观测性改进) 解决规模化、企业级部署面临的工程问题。 |
| **当前最大挑战** | **模型升级的向下兼容性**：模型格式变更直接破坏工具核心功能，暴露了工具链对新模型缺乏缓冲。 | **服务端稳定性与计费模型**：服务端策略、计费逻辑的变更直接引发用户强烈不满，用户对配额缺乏透明度和可控性是最大痛点。 |

---

#### **5. 社区热度与成熟度**

*   **OpenAI Codex：** 社区**极度活跃**，但问题的性质暴露出其处于 **“快速扩张后的阵痛期”** 。高赞 Issues (如 650 👍) 说明它有庞大的用户基础，但严重的服务端问题 (配额、计费) 和数据残留问题 (日志) 正在消耗用户信任。其快速迭代的预发布版本 (一天内3个) 也显示出其在尝试快速响应，但可能缺乏足够的测试。

*   **Claude Code：** 社区 **讨论质量高，但规模相对较小**。问题更聚焦于软件工程细节 (如特定架构 Bug、GUI 交互)。没有新版本发布说明其迭代周期相对稳定，但也可能意味着对紧急 Bug 的响应速度需要加强。其最大的挑战在于如何优雅地拥抱上游模型能力的快速变化，而非自身代码的 Bug。

**结论：** 从成熟度看，Claude Code 的体验更“稳定”，但对来自模型层的变化更敏感；OpenAI Codex 功能更“庞大”，但服务端和工程层面的“慢性病”更多。

---

#### **6. 值得关注的趋势信号**

1.  **“模型更新”已成为最大的破坏性因素：** Claude Code 的 Opus 4.7 和 OpenAI Codex 的 GPT-5.5 都引发了严重的兼容性问题。这意味着，**未来的 AI CLI 工具必须具备“模型版本适配层”**，能够平滑处理模型 API 返回格式、计算逻辑的变化，而不影响用户体验。

2.  **“配额与计费透明度”是付费用户的生命线：** OpenAI Codex 的配额异常问题 (单次请求消耗 10-20 倍) 是一个强烈的警示。**工具必须提供实时、细粒度的成本/消耗监控界面**，让用户在“失控”前就能感知到问题，这是留住付费用户的底线。

3.  **“平台资源管理”成为隐性基础设施：** 从 SQLite 日志写放大到 MCP 进程泄漏，开发者对工具的“副作用”容忍度正在降低。这要求工具设计者从 **“系统资源消耗”** 的角度进行代码审查和优化，避免成为开发环境的“资源蛀虫”。

4.  **“用户体验差异化”从“炫技”转向“控制”：** 用户不再满足于 AI 能做什么，而更关心“我能否控制它做什么、何时做、不做”。`**/.codexignore**`、Cowork 手动压缩开关、禁用终端点击确认等诉求，都反映了 **“用户控制权”** 已成为 AI 工具的新的核心竞争力。

**对开发者的参考价值：**

*   **关注工具的责任边界：** 选择 AI CLI 工具时，不仅要看它有多强，更要看它对系统资源 (SDD, FDs)、网络、身份认证 (OAuth) 的管理是否可靠。
*   **警惕模型依赖陷阱：** 过于紧密地绑定某个前沿模型 (如 Opus 4.7) 可能带来兼容性风险。评估工具是否具备灵活的模型切换或适配能力。
*   **优先选择有“可观测性”的工具：** 选择提供详细日志、遥测、配额/成本明细的工具，这将极大提升排错和成本控制能力。
*   **审视工具的“平台惯性”：** 大量跨平台兼容问题表明，一些工具可能优先适配 Mac/Linux。如果你的主力开发环境是 Windows 或需要 Linux 桌面应用，务必实测确认。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（截至 2026-06-28）

---

## 1. 热门 Skills 排行（Top 7 PR）

以下 PR 因社区关注度高、讨论热烈或影响范围广而入选。

---

### #1 fix(skill-creator): run_eval.py always reports 0% recall  
**状态：OPEN**  
**功能：** 修复 `run_eval.py`、`run_loop.py`、`improve_description.py` 始终报告 `recall=0%` 的严重 bug，同时解决 Windows 下子进程读取、触发检测、并行工作等问题。  
**社区讨论热点：** 该问题被多次独立复现（#556），导致技能描述优化循环完全失效——所有描述评分均为 0%，优化相当于“对噪声做优化”。PR 本身涉及多平台兼容性，是当前整个 skill-creator 工具链最关键的一环。  
**链接：** [PR #1298](https://github.com/anthropics/skills/pull/1298)

---

### #2 Add document-typography skill  
**状态：OPEN**  
**功能：** 新增文档排版技能，自动修正 AI 生成文档中的常见排版问题：孤词（orphan word wrap）、孤段（widow paragraphs）、编号错位等。  
**社区讨论热点：** 用户普遍反映 Claude 生成的文档在最终排版上存在体验下降问题，该技能直接解决“所有文档都会遇到”的通病，被视作提升输出质量的关键补丁。  
**链接：** [PR #514](https://github.com/anthropics/skills/pull/514)

---

### #3 fix(pdf): correct case-sensitive file references in SKILL.md  
**状态：OPEN**  
**功能：** 修复 PDF 技能中 8 处大小写引用不一致（如 `REFERENCE.md` → `reference.md`），使其在大小写敏感文件系统（如 Linux）上正常工作。  
**社区讨论热点：** 虽为修复类 PR，但暴露了跨平台测试覆盖不足的问题。社区对 PDF 技能本身的稳定需求较高，该 PR 被持续关注。  
**链接：** [PR #538](https://github.com/anthropics/skills/pull/538)

---

### #4 Add ODT skill — OpenDocument text creation and template filling  
**状态：OPEN**  
**功能：** 支持创建、填充、读取及转换 ODF 格式（.odt, .ods），对标 LibreOffice / OpenDocument 标准，提供 ISO 标准文档格式处理能力。  
**社区讨论热点：** 企业用户对开源文档格式支持需求强烈，该技能填补了仅支持 DOCX 的空白，讨论集中在模板填充和 HTML 转换的稳定性。  
**链接：** [PR #486](https://github.com/anthropics/skills/pull/486)

---

### #5 Improve frontend-design skill clarity and actionability  
**状态：OPEN**  
**功能：** 重构前端设计技能，使其指令更清晰、可执行，确保每条指导 Claude 能在单次对话中执行，并减少歧义。  
**社区讨论热点：** 原始技能存在“教育风格过重”问题（类似 Issue #202 对 skill-creator 的批评），社区期望所有技能都是“可操作的指令”，而非文档。该 PR 被视为改进模板。  
**链接：** [PR #210](https://github.com/anthropics/skills/pull/210)

---

### #6 Add skill-quality-analyzer and skill-security-analyzer to marketplace  
**状态：OPEN**  
**功能：** 两个元技能：质量分析器从结构/文档/性能/可维护性/安全性五个维度评估技能；安全分析器专门检测安全风险。  
**社区讨论热点：** 社区对技能质量参差不齐和安全隐患（如 Issue #492）的担忧上升，元技能提供标准化评估工具，被视作自治理机制。讨论焦点是评分权重和误报率。  
**链接：** [PR #83](https://github.com/anthropics/skills/pull/83)

---

### #7 fix(docx): prevent tracked change w:id collision with existing bookmarks  
**状态：OPEN**  
**功能：** 修复 DOCX 技能在已有书签的文档中添加修订时，因 `w:id` 冲突导致文档损坏的问题。  
**社区讨论热点：** 该 Bug 直接影响企业协同场景（如合同、报告），社区高度关注此类“隐蔽数据破坏”问题。PR 分析根因透彻（OOXML ID 空间共享），被多次引用。  
**链接：** [PR #541](https://github.com/anthropics/skills/pull/541)

---

## 2. 社区需求趋势（从 Issues 提炼）

| 需求方向 | 代表 Issue | 核心诉求 |
|---------|-----------|----------|
| **安全与信任** | #492（23 评论，👍2） | 社区技能未与官方技能区分，易造成信任边界滥用，需命名空间隔离或签名机制 |
| **组织级共享与协作** | #228（14 评论，👍7） | 技能无法在 org 内直接分享，需共享库或链接，减少手动 Slack/Teams 传递 |
| **技能创作工具可靠性** | #556（12 评论，👍7）、#1169、#1061 | `run_eval.py` 持续报 0% 召回率，Windows 平台完全不可用，工具链亟待稳定 |
| **持久记忆与上下文** | #1329（6 评论）、#154（PR） | 长对话需要紧凑符号化记忆系统，避免上下文被冗余笔记占满 |
| **Agent 治理与安全模式** | #412（6 评论） | 希望有预设的治理模式（策略执行、威胁检测、信任评分、审计），类似企业级 Agent 管控 |
| **文档格式扩展** | 隐含在 ODT PR 及 #1175（SPO） | 对 OpenDocument、SharePoint、模板填充等企业格式需求上升 |
| **元技能与质量治理** | #83（PR）、#202（Issue） | 需要自动评估技能质量、安全性的工具，以及明确的创作规范（避免“文档式”技能） |

**亮点需求：**  
- **Agent 记忆** 和 **Agent 治理** 是近期两大新兴方向，代表了社区从“单一指令”向“持久化、自主化”演进的深层需求。  
- **安全/信任** 议题关注度急剧上升（#492 评论数最高），可能促使 Anthropic 在官方层面规范技能分发。  

---

## 3. 高潜力待合并 Skills（评论活跃但尚未合并的 PR）

以下 PR 社区关注度高、问题明确，合并前景较大：

| PR | 描述 | 为什么高潜力 |
|----|------|------------|
| #1298 fix(skill-creator): run_eval.py always reports 0% recall | 解决 skill-creator 核心工具链瘫痪问题，已被多个 issue 复现，作者积极迭代（6 月还在更新） | **直接影响所有技能创作者**，官方应优先合并 |
| #514 Add document-typography skill | 解决所有 AI 文档的排版通病，需求广泛，代码逻辑独立 | 用户体验提升明显，无破坏性 |
| #486 Add ODT skill | 填补重要格式空白，企业用户呼声高，且已有完整实现（模板、解析） | 与 DOCX 形成互补，扩展适用场景 |
| #723 feat: add testing-patterns skill | 系统性测试技能（Trophy 模型、单元测试、React 测试等），覆盖测试栈 | 开发者刚需，内容详实，直接改善输出质量 |
| #154 Add shodh-memory skill: persistent context | 持久记忆系统，支持跨对话上下文保持，符合 Agent 长期运行趋势 | 创新性强，Issue #1329 也在呼吁同类技能 |
| #83 skill-quality-analyzer and security-analyzer | 元技能，为社区提供技能质量与安全评估能力，呼应 #492 | 生态治理基础设施，长期价值高 |

> 注意：全部为 OPEN 状态，尚无 merged 或 closed 指示。建议关注 #1298 和 #514 的最新动态。

---

## 4. Skills 生态洞察

> **当前社区最集中的诉求：修复与完善 skill-creator 工具链（尤其是 `run_eval.py` 的 0% 召回率 bug），使其能在 Windows 和 Linux 上稳定工作，同时拓展实用技能（文档排版、ODT、测试模式、持久记忆），并建立安全信任机制。**  

一句话概括：**“让创作工具可靠，让技能库实用，让生态安全可信”。**

---

好的，这是为您生成的 2026-06-28 Claude Code 社区动态日报。

---

# Claude Code 社区动态日报 | 2026-06-28

## 今日速览

今日社区最集中的反馈围绕 **Opus 4.7 模型思考摘要（Thinking Summaries）在 VSCode 扩展中无法渲染** 的持续性 Bug，相关议题已累积超百条评论。此外，关于 **Cowork 模式** 的功能增强、**Windows 原生通知** 以及 **MCP 插件兼容性** 的讨论热度上升。项目无新版本发布，但社区对提升开发体验的呼声愈发强烈。

## 版本发布

**（无）** 过去 24 小时内无新版本发布。

## 社区热点 Issues

挑选了 10 个最值得关注的 Issue，覆盖当前社区最关心的问题。

1.  **[BUG] Opus 4.7 思考摘要未在 VSCode 扩展中渲染**
    -   **编号**: [#49322](https://github.com/anthropics/claude-code/issues/49322)
    -   **重要性**: **社区头号热点**。大量用户报告在 VSCode 扩展中无法看到 Opus 4.7 模型的思考摘要，严重影响模型推理过程的可见性。该问题与多个 Issue 重复，并获得超过 75 个 👍，开发者正在集中追踪。
    -   **社区反应**: 47 条评论，用户提供了详细的复现步骤与环境信息，确认问题与 `showThinkingSummaries` 配置项未生效有关（见 [#49268](https://github.com/anthropics/claude-code/issues/49268)）。

2.  **[BUG] Opus 4.7 思考摘要缺失 —— 核心问题定位**
    -   **编号**: [#49268](https://github.com/anthropics/claude-code/issues/49268)
    -   **重要性**: 作为 [#49322](https://github.com/anthropics/claude-code/issues/49322) 的根因分析，该 Issue 明确指出是因为新模型 Opus 4.7 更改了 API 返回的 `display` 字段，而 Claude Code 的工具链未适配新格式。
    -   **社区反应**: 75 个 👍 和 46 条评论，这是当前社区里认可度最高的技术分析帖之一。

3.  **[BUG] Snapdragon X Plus (ARM64) 上 Cowork VM 无法启动**
    -   **编号**: [#39636](https://github.com/anthropics/claude-code/issues/39636)
    -   **重要性**: 影响 Windows ARM64 架构用户的关键 Bug，Cowork 模式核心功能完全不可用，连接始终超时。
    -   **社区反应**: 32 条评论，但 👍 数不高，可能受影响用户群体较小，但问题性质严重。

4.  **[Feature Request] 添加禁用终端可点击确认提示的选项**
    -   **编号**: [#70622](https://github.com/anthropics/claude-code/issues/70622)
    -   **重要性**: 反映 UI/UX 设计上的争议。新的可点击“是/否”权限提示虽然新颖，但**误触**成为主要痛点，用户防不胜防。
    -   **社区反应**: 24 个 👍，社区呼声较高，希望回归传统键盘交互或提供开关选项。

5.  **[Feature] 为 VSCode 扩展添加原生系统通知**
    -   **编号**: [#57230](https://github.com/anthropics/claude-code/issues/57230)
    -   **重要性**: 提升 IDE 内异步工作流体验的关键需求。当前只能通过状态栏颜色变化提示，用户希望能像常规 IDE 功能一样收到 Toast 通知。
    -   **社区反应**: 14 个 👍，代表了扩展用户对**非侵入式任务状态提示**的强烈需求。

6.  **[Feature] Cowork 模式：为用户提供手动压缩（/compact）功能**
    -   **编号**: [#65114](https://github.com/anthropics/claude-code/issues/65114)
    -   **重要性**: Cowork 功能的体验优化。用户抱怨自动压缩时机不可控，希望能手动触发上下文压缩以避免关键信息丢失。
    -   **社区反应**: 5 条评论，讨论集中在自动与手动控制的权衡上。

7.  **[BUG] 多 MCP 服务器配置时，服务器指令被静默截断**
    -   **编号**: [#43474](https://github.com/anthropics/claude-code/issues/43474)
    -   **重要性**: 这是一个隐蔽的 Bug，影响使用多个 MCP 服务器的高级用户。指令被截断会导致模型无法正确理解工具用法，造成逻辑错误。
    -   **社区反应**: 3 条评论，虽热度不高但问题质量高，有明确的复现步骤。

8.  **[BUG] 安全分类器故障阻止所有 Bash/工具调用**
    -   **编号**: [#69950](https://github.com/anthropics/claude-code/issues/69950)
    -   **重要性**: **影响所有用户的阻塞性错误**。当安全后端不可用时，自动模式下的所有 Bash 命令和 MCP 工具调用都会被拒绝，完全阻断开发流程。
    -   **社区反应**: 2 条评论，应为近期新问题，但潜在影响巨大，需要运营团队紧急关注。

9.  **[Enhancement] 插件 hooks.json 文件使用顶级 `description` 键导致 Codex 钩子加载失败**
    -   **编号**: [#71943](https://github.com/anthropics/claude-code/issues/71943)
    -   **重要性**: 反映了 **跨平台兼容性** 问题。Claude Code 宽松的 JSON 解析器允许了非标准字段，导致与 OpenAI Codex 等严格解析器的兼容失败。
    -   **社区反应**: 1 条刚刚提交的 Issue，但指出了项目维护和规范性问题。

10. **[Feature] 跨 Claude 产品线（Code, Cowork, claude.ai）功能不一致**
    -   **编号**: [#71941](https://github.com/anthropics/claude-code/issues/71941)
    -   **重要性**: 代表了高级用户对**统一体验**的诉求。用户期望在不同界面上获得一致的能力和反馈机制，而非体验碎片化。
    -   **社区反应**: 新提交的 Issue，讨论刚刚开始，但代表了未来的体验演进方向。

## 重要 PR 进展

1.  **[Merged] 修复 `edit-issue-labels.sh` 脚本在无参数调用时的静默失败**
    -   **编号**: [#68787](https://github.com/anthropics/claude-code/pull/68787)
    -   **内容**: 修复了一个开发脚本 Bug。当未提供标签参数时，脚本会静默退出，现在会输出明确的错误信息。
    -   **重要性**: 提升项目自动化流程（CI）的健壮性与可调试性，属于内部工程改进。

## 功能需求趋势

从今日的 Issues 中可以提炼出社区关注的几个主要方向：

1.  **IDE 深度集成与状态提示**：
    -   **核心诉求**：VSCode 扩展需要更强大的通知机制（系统 Toast、任务完成/等待状态），不再满足于仅靠状态栏或图标颜色来提示。相关要求基于 [#57230](https://github.com/anthropics/claude-code/issues/57230)、[#65241](https://github.com/anthropics/claude-code/issues/65241)。

2.  **Cowork 功能完善**：
    -   **核心诉求**：用户希望拥有更多对 Cowork 会话的控制权，例如手动触发上下文压缩（/compact）和更稳定的 VM 启动。相关要求基于 [#65114](https://github.com/anthropics/claude-code/issues/65114)、[#71803](https://github.com/anthropics/claude-code/issues/71803)。

3.  **Windows 平台体验优化**：
    -   **核心诉求**：Windows 用户希望获得与 Mac/Linux 同等的原生通知体验（Windows Toast），并解决 ARM64 等特殊硬件的兼容性问题。相关要求基于 [#67220](https://github.com/anthropics/claude-code/issues/67220)、[#39636](https://github.com/anthropics/claude-code/issues/39636)。

## 开发者关注点

1.  **Opus 4.7 模型兼容性**：模型升级（尤其是 Opus 4.7）带来的破坏性更改是当前最核心的痛点，包括“思考摘要”不显示、安全分类器错误、以及模型无法正确输出等问题。这提示模型更新时应充分考虑下游工具的兼容性。
2.  **权限与安全机制的交互体验**：无论是可点击确认的误触问题（[#70622](https://github.com/anthropics/claude-code/issues/70622)），还是自动安全分类器故障导致的流程阻塞（[#69950](https://github.com/anthropics/claude-code/issues/69950)），都说明现有的权限和安全模型在便捷性与安全性之间尚未取得良好平衡。
3.  **Git 交互的稳定性**：在 Git 工作树操作时残留的 `.git/index.lock` 文件（[#57102](https://github.com/anthropics/claude-code/issues/57102)）虽然小众，但会影响特定工作流，体现了在边缘情况下的健壮性需要加强。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 | 2026-06-28

---

## 今日速览

今日 Codex 社区出现多起严重的 **rate-limit 与配额异常**，多位 Plus/Pro 用户反馈预算在 2-3 次请求内瞬间耗尽，疑似服务端计费逻辑变更；同时 **SQLite 日志写放大**问题虽经修复但仍有多平台残留，多个 macOS/Windows 进程泄漏与僵尸进程报告持续发酵。功能方面，社区对 **Linux 桌面应用**、**`.codexignore` 文件排除**等呼声依旧高涨，MCP OAuth 恢复机制则迎来大规模 PR 重构。

---

## 版本发布

今日无主要版本发布，但有以下 **3 个 Rust 预发布版本**（alpha）上线，均未附带详细更新日志：

- **[rust-v0.143.0-alpha.29](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.29)**
- **[rust-v0.143.0-alpha.28](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.28)**
- **[rust-v0.143.0-alpha.27](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.27)**

> 推测为持续迭代的内部实验版本，未公开具体变更内容。

---

## 社区热点 Issues

### 1. #28879 – Plus 用户 rate-limit 成本飙升 10–20 倍  
**状态**：OPEN | **评论**：186 | **👍**：334  
**链接**：https://github.com/openai/codex/issues/28879  
**摘要**：自 6月16日起，Plus 用户在 `gpt-5.5` 上每次 token 消耗的配额比例暴增，原本可用 20+ 次请求现在仅 2-3 次就耗尽 5 小时预算。日志显示 `limit-% consumed per token` 上升 10–20 倍。  
**影响**：广泛影响 Plus 方案用户体验，社区质疑计费模型变更，官方尚未正面回应。

### 2. #11023 – 强烈要求 Linux 桌面应用  
**状态**：OPEN | **评论**：130 | **👍**：650  
**链接**：https://github.com/openai/codex/issues/11023  
**摘要**：用户因 macOS 版功耗问题无法使用，希望官方提供 Linux 原生桌面应用或修复现有性能问题。  
**影响**：持续近 5 个月，650 👍 表明这是社区最强烈的功能需求之一。

### 3. #28224 – SQLite 反馈日志每年写入 ~640 TB  
**状态**：已关闭（因 PR 修复，避免 85% 日志） | **评论**：93 | **👍**：400  
**链接**：https://github.com/openai/codex/issues/28224  
**摘要**：日志以 TRACE 级别高频繁写入 `logs_2.sqlite`，消耗 SSD 寿命。作者感谢 @jif-oai 合并 3 个 PR 后减少 85% 写量，但仍有关注残留问题。  
**社区反应**：大量用户反馈该问题严重影响日常使用，虽已部分修复但仍有其他平台残留（见 #29532、#30405）。

### 4. #2847 – 请求添加 `.codexignore` / 敏感文件排除机制  
**状态**：OPEN | **评论**：79 | **👍**：414  
**链接**：https://github.com/openai/codex/issues/2847  
**摘要**：希望支持仓库级/全局忽略路径机制，防止 agent 读取或发送敏感文件（如 `node_modules/` 保留为可搜索但不可发送）。  
**社区反应**：414 👍 表明该需求非常普遍，类似 `.gitignore` 的模式被广泛认可。

### 5. #30224 – GPT-5.5 在 Codex Desktop 报“模型不支持”错误  
**状态**：OPEN | **评论**：52 | **👍**：18  
**链接**：https://github.com/openai/codex/issues/30224  
**摘要**：当使用 `X-OpenAI-Internal-Codex-Responses-Lite` 请求头时，GPT-5.5 返回“This model is not supported”。  
**影响**：用户无法在桌面端使用最新模型，需降级到 5.4，影响开发效率。

### 6. #29955 – 100 积分瞬间耗尽，5 小时配额重置为 0%  
**状态**：OPEN | **评论**：29 | **👍**：7  
**链接**：https://github.com/openai/codex/issues/29955  
**摘要**：Pro*5 用户反馈一次消息即耗尽 100 积分，5 小时上限归零。  
**影响**：与 #28879 类似，进一步印证配额计费异常。

### 7. #29532 – macOS 上 SQLite TRACE 日志在 v0.142.0 后仍有残留  
**状态**：OPEN | **评论**：22 | **👍**：7  
**链接**：https://github.com/openai/codex/issues/29532  
**摘要**：尽管 #29432 降低了 `codex_api::endpoint::responses_websocket` 日志频率，但 #29457 似乎未生效，macOS 上仍持续写入 `logs_2.sqlite`。  
**影响**：提示日志修复不完整，Windows 也有类似报告（#30405）。

### 8. #25744 – macOS 上 MCP/Computer Use 辅助进程泄漏，导致 HID 延迟  
**状态**：OPEN | **评论**：8 | **👍**：3  
**链接**：https://github.com/openai/codex/issues/25744  
**摘要**：长时间运行的 Codex 会话累积未回收子进程，造成 WindowServer/TCC 卡顿、HID 输入延迟。  
**影响**：影响 macOS 用户的日常编辑体验，且难以复现，但症状严重。

### 9. #26984 – MCP stdio 服务器泄漏管道 fd 和孤儿进程，导致 EMFILE  
**状态**：OPEN | **评论**：7 | **👍**：1  
**链接**：https://github.com/openai/codex/issues/26984  
**摘要**：Codex CLI 在使用 MCP stdio 时，持续泄漏文件描述符和子进程，最终触发“Too many open files”。  
**影响**：长期运行 MCP 工作流时系统稳定性严重下降。

### 10. #30359 – Codex Desktop 反复崩溃，报 SIGKILL  
**状态**：OPEN | **评论**：4 | **👍**：0  
**链接**：https://github.com/openai/codex/issues/30359  
**摘要**：6月27日，桌面应用更新后频繁崩溃，错误信息为 bundled process exited with `(code=null, signal=SIGKILL)`。  
**影响**：直接导致用户无法启动，紧急程度高。

---

## 重要 PR 进展

### 1. #30395 – 显示使用限制重置到期详情  
**状态**：OPEN | **作者**：jayp-oai  
**链接**：https://github.com/openai/codex/pull/30395  
**内容**：在 `account/rateLimits/read` 中增加重置积分过期日期展示，允许客户端直接显示到期时间，无需调用私有后端。直接回应 #29618 等社区诉求。

### 2. #30334 – 结构化工具和推理计时事件的遥测日志  
**状态**：OPEN | **作者**：bolinfest  
**链接**：https://github.com/openai/codex/pull/30334  
**内容**：在 JSON 日志中区分调度/队列时间与处理时间，帮助下游诊断工具延迟。属于可观测性改进。

### 3. #30269 – 禁用 Rendezvous WebSocket 的 Nagle 算法  
**状态**：OPEN | **作者**：richardopenai  
**链接**：https://github.com/openai/codex/pull/30269  
**内容**：通过 `disable_nagle=true` 降低 exec-server 通信延迟，无需功能开关和 rollout 变更。

### 4. #30294 + #30296 + #30295 + #30293 + #30292 – **MCP OAuth 恢复栈重构**  
**状态**：OPEN | **作者**：stevenlee-oai  
**内容**：一系列 PR（共 5 个）串行合并，共同目标：将 MCP OAuth 刷新、登录/登出、凭证存储等操作序列化，防止并发竞争；同时将恢复逻辑路由通过 Codex 自身处理，改善 OAuth 过期后自动恢复的可靠性。  
**链接**：  
- https://github.com/openai/codex/pull/30294  
- https://github.com/openai/codex/pull/30296  
- https://github.com/openai/codex/pull/30295  
- https://github.com/openai/codex/pull/30293  
- https://github.com/openai/codex/pull/30292  

### 5. #30327 – 稳定合成调用输出 ID  
**状态**：CLOSED | **作者**：bolinfest  
**链接**：https://github.com/openai/codex/pull/30327  
**内容**：为 `ContextManager::for_prompt` 中合成的 "aborted" 输出分配稳定 ID，避免重试和回放时对话身份不一致。

### 6. #29691 – 在运行时强制市场源策略（Enterprise）  
**状态**：CLOSED | **作者**：xl-openai  
**链接**：https://github.com/openai/codex/pull/29691  
**内容**：通过企业源策略过滤已安装的插件，使其无效；并在列表/发现/CLI 报告中强制准入检查。面向企业级安全管控。

### 7. #30291 – 暴露环境信息 RPC  
**状态**：CLOSED | **作者**：maxj-oai  
**链接**：https://github.com/openai/codex/pull/30291  
**内容**：允许 app-server 客户端发现执行环境的 shell 和工作目录，支持跨操作系统环境选择。

### 8. #30091 – 已废弃的 MCP OAuth 恢复（旧栈）  
**状态**：CLOSED | **作者**：stevenlee-oai  
**链接**：https://github.com/openai/codex/pull/30091  
**内容**：被新栈（#30292 系列）取代，已标记为 superseded。说明开发者正在集中重构 MCP OAuth 逻辑。

### 9. #29020 – 在刷新前重新读取持久化 OAuth 凭证  
**状态**：CLOSED | **作者**：stevenlee-oai  
**链接**：https://github.com/openai/codex/pull/29020  
**内容**：确保 MCP OAuth 刷新时使用最新的存储凭证，修复潜在竞争条件。被新栈取代。

### 10. #30384 – 增加 currentTime/read 超时从 5s 到 10s  
**状态**：CLOSED | **作者**：rka-oai  
**链接**：https://github.com/openai/codex/pull/30384  
**内容**：提升外部时间读取请求的超时容忍度，减少因网络波动导致的失败。

---

## 功能需求趋势

从近期 Issues 中可提炼出社区最关注的 **5 大功能方向**：

1. **Rate-limit 透明度与配额可靠性**  
   #28879、#29955、#29618 等表明用户迫切需要实时可见的配额消耗明细、重置到期时间，并要求解决计费异常。

2. **跨平台桌面应用支持**  
   #11023（Linux）持续高赞，同时 Windows (#21863, #24259, #29408) 和 macOS (#25744, #29532) 存在大量稳定性问题，用户希望官方提供稳定、一致的多平台体验。

3. **文件排除与安全机制**  
   #2847（`.codexignore`）、#24993（`.aiignore` 或 config.toml 排除）等已获得数百赞，用户强烈要求 agent 不自动读取敏感文件（如凭据、私钥）。

4. **MCP 稳定性与 OAuth 恢复**  
   #26984（fd 泄漏）、#27165（OAuth token 不刷新）、#30170（浏览器被意外打开）等表明 MCP 子系统和身份认证是当前最大痛点之一。

5. **日志写放大与 SSD 寿命保护**  
   尽管 #28224 已部分修复，但 #29532、#30405 等仍报告残留问题，社区期望彻底消除 SQLite 高频 TRACE 日志写入。

---

## 开发者关注点

- **配额异常已成为最紧急的付费用户痛点**：多条 issue 指向 6月中旬后 `gpt-5.5` 的 token 消耗计算出现 10–20 倍飙升，Plus/Pro 用户实际可用请求数锐减，影响核心生产力。
- **日志写放大是“次世代”慢性病**：即使部分修复，macOS 和 Windows 上仍持续写入 `logs_2.sqlite`，开发者建议增加日志级别控制或自动清理策略。
- **MCP 资源泄漏影响长期会话**：文件描述符泄漏、僵尸进程、OAuth token 过期未刷新导致 MCP 工具频繁失效，依赖 MCP 的 CI/CD 或自动化工作流不可靠。
- **OAuth 认证与令牌管理混乱**：Desktop 从 Keychain 读取过期 token、CLI 中 `auth.json` 更新丢失等问题，让多人协作环境下的身份管理变得脆弱。
- **模型兼容性碎片化**：GPT-5.5 在部分端点和请求头下报错，用户被迫回退到 5.4，影响新功能体验。
- **桌面应用稳定性亟待提升**：近 24 小时内出现新崩溃报告（#30359），Windows 下 `git.exe` 进程泄漏、macOS 下 `Computer Use` 服务缺失等问题，表明桌面端质量仍需夯实。

--- 
*数据截至 2026-06-28 12:00 UTC，自动生成。*

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*