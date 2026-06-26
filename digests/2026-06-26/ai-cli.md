# AI CLI 工具社区动态日报 2026-06-26

> 生成时间: 2026-06-26 02:56 UTC | 覆盖工具: 2 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI CLI 工具横向对比分析报告（2026-06-26）

## 1. 生态全景

当前 AI CLI 工具正从“尝鲜可用”向“生产级可靠”过渡，但均暴露出**成本控制不透明**和**模型质量波动**两大核心痛点。Claude Code 与 OpenAI Codex 均处于高频迭代期，前者着力加强安全与权限体系，后者围绕 MCP（模型上下文协议）构建生态粘性。社区对**计费可视化**、**平台兼容性**（尤其 Windows ARM64）及**工具调用稳定性**的诉求高度一致，反映出开发者对工具 ROI 和可预测性的要求日益严苛。整体呈现“功能快速丰富，但质量打磨滞后”的态势。

## 2. 各工具活跃度对比

| 维度 | Claude Code | OpenAI Codex |
|------|-------------|--------------|
| **当日 Release** | v2.1.193（stable） | rust-v0.142.2（stable）<br>4 个 v0.143.0-alpha<br>codex-zsh-v0.1.0 |
| **热点 Issue 数** | 10 条（社区热议） | 10 条（社区热议） |
| **重要 PR 进展** | 1 条（#63686 延长 stale 超时） | 10 条（#30144、#30164 等） |
| **仓库总待处理 Issue** | ~50 条（当日提及） | 未给出总数，但热点问题评论量更大 |
| **单一 Issue 最高热度** | 380 👍（多账户切换 #36151） | 303 👍（Rate-limit 飙升 #28879） |

*注：数据仅基于日报摘要，并非全量 GitHub API 统计，但可反映当日社区聚焦度。*

## 3. 共同关注的功能方向

| 功能方向 | Claude Code 具体诉求 | OpenAI Codex 具体诉求 |
|----------|----------------------|----------------------|
| **费用/配额透明度** | 模型静默升级导致意外高额费用（#71481，6 天 $500+） | Rate-limit 消耗飙升 10~20 倍（#28879），5h 配额 41 分钟耗尽（#30002） |
| **模型质量稳定性** | Opus 4.7/4.8 推理倒退（#71446），工具调用格式混淆（#49747） | 自动压缩致模型“失忆”（#5957），“模型容量不足”报错（#30008） |
| **Windows 平台稳定性** | ARM64 Cowork 启动失败（#50674） | 多行粘贴只保留首行（#2137），沙盒弹窗堵塞工作流（#29200、#29782） |
| **MCP/工具生态** | 用户中断钩子（#9516），Slack 插件认证失败（#18009） | MCP OAuth 令牌不刷新（#17265），资源更新通知（#30087） |
| **日志与资源管理** | 内存泄漏 “每小时增 348MB”（#71493） | SQLite 日志年化写入 ~640 TB（#28224），后台轮询浪费 Token（#13733） |

可见，**费用失控**和**模型行为退化**是两工具社区最焦虑的共性问题，直接影响用户留存。

## 4. 差异化定位分析

| 维度 | Claude Code | OpenAI Codex |
|------|-------------|--------------|
| **核心卖点** | 安全精细控制（命令分类、权限审计），长上下文（1M），模型定制 | MCP 生态开放，多模型支持（gpt-5.5、gpt-5-codex-high），跨平台插件 |
| **目标用户** | 注重安全合规的团队开发者，重度长上下文调用者 | 追求集成扩展性的个人/企业开发者，偏好插件化工作流 |
| **技术路线** | 聚焦 TUI + VSCode 扩展，权限分层（bwrap 沙盒），自研模型 Opus | 全栈 Rust 重写，MCP 作为中心枢纽，支持 zsh/Windows/远程执行 |
| **迭代速度** | 稳定版更新节奏较慢（每日 1 个 release），但社区 PR 贡献少 | 激进发布 alpha 版，PR 数量多，功能实验性强（如 Apps 虚拟 MCP） |
| **平台支持短板** | ARM64 Windows、Linux TUI 滚动/复制粘贴缺陷 | Windows 沙盒弹窗、多行粘贴、旧账号验证锁定 |

总结：Claude Code 走“深安全、强模型”路线，适合对数据主权和推理质量要求高的场景；OpenAI Codex 走“广集成、快迭代”路线，适合需要多工具联动的灵活开发环境。

## 5. 社区热度与成熟度

- **社区活跃度**：OpenAI Codex 明显更高。其热点 Issue 评论数普遍在 30~150 条，PR 单日更新 10 条，且有独立 zsh 插件贡献，说明外部开发者参与度和反馈密度更强。Claude Code 的 PR 仅 1 条，且多为维护性（延长 stale 时间），社区贡献动力偏弱。
- **问题响应效率**：Claude Code 的 Issue 待处理量 ~50 条，但 PR 极少，体现维护团队反应较慢；Codex 虽有大量 Issue，但同日合并 3 个 fix 缓解 SQLite 日志问题（#28224），修复动作更迅捷。
- **成熟度评估**：两者均未达到“生产级稳定”。Claude Code 在模型退化、内存泄漏上问题严重；Codex 在配额计算、Windows 兼容性上漏洞明显。但 Codex 的 alpha 版本发布密度更高，表明其正在快速试错修复，成熟度有望短期提升。

## 6. 值得关注的趋势信号

1. **模型质量成为第一优先级的负反馈**：两工具用户均报告“新版模型比旧版更差”，且伴随意外高额消费。这警示 AI CLI 工具在追求上下文长度和推理速度时，**模型回归测试与成本保障机制**必须前置，否则会快速腐蚀用户信任。

2. **MCP 从概念走向生产瓶颈**：OpenAI Codex 大量 PR 聚焦 MCP 的 OAuth 刷新、路由亲和性、运行时复用——这些基础设施问题的暴露，说明 MCP 已由实验阶段进入实际负载阶段。开发者应关注 MCP 的**认证、日志、资源通知**三项成熟度指标。

3. **Windows 成为第二战场，但 QA 严重滞后**：Claude Code 的 ARM64 兼容性、Codex 的沙盒弹窗与多行粘贴缺陷，反映出两大工具对 Windows 的投入远落后于 macOS/Linux。随着 Snapdragon X 等 ARM Windows 设备普及，**Windows 原生稳定支持**将成关键差异化能力。

4. **费用透明化需求催生新工具链**：用户强烈要求 token 消费明细、配额重置提醒、预算告警。这可能催生第三方计费审计插件或官方提供“费用仪表盘”，建议技术团队在选择工具时将此纳入评估维度。

5. **社区过度依赖“stale bot”表明管理瓶颈**：Claude Code 社区主动提出将 stale 超时从 14 天延长至 90 天（#63686），反映出维护团队人力不足，导致重要 Issue 被误关。对于开源生态，**核心贡献者投入力度**直接决定了工具长期生命力。

---

**结论**：当前 AI CLI 工具正处于“功能爆发期”与“质量临界点”的交叠阶段。开发者若追求稳定可靠，建议优先选择修复活跃度高的分支（如 Codex 的 latest stable）；若需要精细权限管控，可试用 Claude Code 但需监控模型版本和费用消耗。两个工具均需在 **成本可观测性** 和 **模型一致性** 上完成重大改进，才能真正进入开发者日常工具箱。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，作为专注于 Claude Code 生态的技术分析师，我已审阅截至 2026-06-26 的 `anthropics/skills` 仓库数据。以下是社区热点分析报告。

---

### Claude Code Skills 社区热点报告 (数据截止 2026-06-26)

#### 1. 热门 Skills 排行

以下是根据 Pull Request 评论热度及社区关注度筛选出的 6 个关键 Skills：

1.  **文档排版质量控制 (document-typography)**
    *   **功能**: 防止 AI 生成文档中的孤词、孤行和编号错位等排版问题。
    *   **社区热点**: 这是一个非常实用且被广泛共鸣的需求。用户普遍认为这些问题影响了文档的专业度，但很少主动要求修复，该 Skill 填补了这一空白。评论讨论了如何平衡排版规则与内容生成效率。
    *   **状态**: [OPEN PR #514](https://github.com/anthropics/skills/pull/514)

2.  **ODT 文档处理 (odt)**
    *   **功能**: 支持创建、填充、读取 LibreOffice/OpenDocument 格式 (.odt, .ods) 文件，并可将 ODT 转换为 HTML。
    *   **社区热点**: 社区对非 Microsoft 办公格式的支持需求强烈，特别是在开源和标准化工作流中。讨论焦点集中在模板填充的准确性和转换后 HTML 的保真度。
    *   **状态**: [OPEN PR #486](https://github.com/anthropics/skills/pull/486)

3.  **前端设计优化 (frontend-design)**
    *   **功能**: 修订并优化了前端设计技能，使指令更清晰、可操作，确保 Claude 能在一个会话内执行具体的设计指导。
    *   **社区热点**: 社区关注点在于如何让通用设计指导（如“提高可读性”）转化为 Claude 可执行的、具体的、原子化的步骤，以提升设计输出的稳定性和质量。
    *   **状态**: [OPEN PR #210](https://github.com/anthropics/skills/pull/210)

4.  **元技能分析器 (skill-quality-analyzer / skill-security-analyzer)**
    *   **功能**: 提供了用于评估其他 Skills 质量的工具，从结构、文档、安全性等多个维度进行分析。
    *   **社区热点**: 这是一个“元”技能，其出现标志着社区开始关注 Skills 本身的成熟度和安全性。讨论围绕如何建立统一的 Skill 质量标准，以及如何防范恶意或设计不良的 Skill 带来的风险。
    *   **状态**: [OPEN PR #83](https://github.com/anthropics/skills/pull/83)

5.  **测试模式 (testing-patterns)**
    *   **功能**: 一个全面的测试技能，覆盖单元测试 (AAA 模式)、React 组件测试、测试哲学（如 Trophy 模型）以及“不测试什么”的指导。
    *   **社区热点**: 社区对系统化、有理论指导的测试实践有很高期待。讨论涉及如何将该 Skill 与现有项目中的特定测试框架（如 Jest, Cypress）结合，并减少误判。
    *   **状态**: [OPEN PR #723](https://github.com/anthropics/skills/pull/723)

6.  **应用部署 (AppDeploy)**
    *   **功能**: 使 Claude 能直接通过 [AppDeploy](https://appdeploy.ai/) 服务部署和管理全栈 Web 应用，包括生命周期管理。
    *   **社区热点**: 体现了社区对“从代码到部署”端到端自动化工作流的强烈兴趣。讨论重点在于部署的安全性、环境配置的复杂性，以及与现有 CI/CD 管线的集成方式。
    *   **状态**: [OPEN PR #360](https://github.com/anthropics/skills/pull/360)

#### 2. 社区需求趋势

从活跃的 Issues 中可以提炼出社区最核心的四大需求方向：

1.  **安全性与信任边界 (Security & Trust)**: (Issue #492) 社区最高关注的议题之一。用户强烈担忧非官方 Skill 被托管在 `anthropic/` 命名空间下，可能导致权限滥用。**核心诉求是建立官方的 Skill 审核、签名和信任机制**。
2.  **组织级 Skill 共享与协作 (Organizational Sharing)**: (Issue #228) 当前的 Skill 分享流程（下载文件 -> 手动上传）效率低下。社区迫切需要**官方的组织级 Skill 库或分享链接机制**，以提升团队协作效率。
3.  **开发与评估工具的稳定性 (Tooling Stability)**: (Issues #556, #1169, #1061) Skill 创建流程中的 `run_eval.py` 脚本存在严重 bug（如 0% 召回率），且对 Windows 系统兼容性差。这**严重阻碍了社区贡献者的 Skill 开发与迭代流程**，是当前最大的“生产力杀手”。
4.  **特定领域能力的深化 (Domain Deepening)**: 用户不再满足于通用技能，而是希望 Skills 能解决更专业的问题，这与高潜力 PR 列表高度相关：
    *   **代理治理 (Agent Governance)**: (Issue #412) 提出为 AI Agent 系统建立安全模式、政策执行和审计追踪。
    *   **文档处理优化 (Document Optimization)**: (Issues #1175, #16) 关注处理 SharePoint 等复杂来源文档时的上下文窗口和安全性，同时探索将 Skills 作为 MCP 服务暴露的可能性。

#### 3. 高潜力待合并 Skills

以下 PR 社区讨论活跃，功能价值高，一旦修复关键技术问题或通过审核，有望近期落地：

1.  **[#514 document-typography](https://github.com/anthropics/skills/pull/514)**: 直击 AI 文档质量的痛点，需求清晰且普遍，落地可能性极高。
2.  **[#83 skill-quality-analyzer](https://github.com/anthropics/skills/pull/83)**: 是构建健康 Skill 生态的基础设施，与社区对安全和质量的核心关切 (Issue #492) 直接相关。
3.  **[#723 testing-patterns](https://github.com/anthropics/skills/pull/723)**: 填补了开发流程中的关键一环，对于希望在项目中系统引入测试的开发者极具吸引力。
4.  **[#486 odt](https://github.com/anthropics/skills/pull/486)**: 满足了对开源办公格式处理的明确需求，丰富了 Claude 在企业级文档生态中的能力。
5.  **[#360 AppDeploy](https://github.com/anthropics/skills/pull/360)**: 代表了“全栈开发 + 一键部署”的理想工作流，与未来 AI Agent 自动化趋势契合。
6.  **[#538 fix(pdf)](https://github.com/anthropics/skills/pull/538)**: 一个简单但至关重要的 bug 修复，确保 Skill 在大小写敏感文件系统上正常工作，是保证生态健壮性的“缝补”型高价值 PR。

#### 4. Skills 生态洞察

**一句话总结**: 当前 Skills 社区的核心矛盾，已从“创造新技能”的阶段，**转变为对官方更可靠的开发工具链（特别是 `run_eval` 的稳定性）、更安全的发布与共享机制，以及更专业的垂直领域能力的迫切渴求**。社区开发者正被工具本身的 bug（如 Windows 兼容性、评估脚本失灵）所困，同时期望官方在治理层面（命名空间、质量审核）给予清晰指导，以建立信任并激发下一波高质量 Skills 的创新浪潮。

---

好的，作为一名专注于AI开发工具的技术分析师，我已根据您提供的GitHub数据，为您生成了2026年6月26日的Claude Code社区动态日报。

---

## Claude Code 社区动态日报 | 2026-06-26

### **今日速览**

- **新功能发布**：`v2.1.193` 版本上线，主要改进了Shell命令的自动模式分类逻辑，并增强了权限机制的用户反馈。
- **社区热议的“模型降级”与“费用激增”问题**：多个高赞Issue指出Opus 4.7/4.8模型疑似出现性能倒退，且存在静默升级导致用户产生意外高额费用的严重问题，成为社区关注焦点。
- **Issue管理流程优化**：社区提交了PR，计划将Issue的“stale”和“autoclose”超时时间从14天延长至90天，以应对堆积如山的待处理问题（共50条）。

### **版本发布**

**v2.1.193** ([更新日志](https://github.com/anthropics/claude-code/releases/tag/v2.1.193))

本次更新侧重于增强安全性和用户控制，主要变化包括：

- **增强命令分类**：新增 `autoMode.classifyAllShell` 设置，可将所有Bash/PowerShell命令（而不仅仅是任意代码执行模式）路由到自动模式分类器，提供更精细的权限控制。
- **提升透明度**：自动模式的拒绝原因现在会显示在对话记录、拒绝通知和 `/permissions` 命令的最近拒绝列表中，便于用户理解决策过程。

### **社区热点 Issues**

1.  **#36151 | [Feature] Claude移动端多账户切换** [110评论 | 380👍]
    这是目前社区呼声最高的功能请求，用户希望在不共享邮箱的情况下，在Claude移动App中方便地切换不同账户。这反映出C端用户对多身份管理功能的强烈需求。
    [查看详情](https://github.com/anthropics/claude-code/issues/36151)

2.  **#3412 | [Enhancement] 允许在提交前查看和编辑“粘贴文本”内容** [76评论 | 269👍]
    在使用听写软件或快速粘贴时，内容会以折叠块形式呈现，导致用户无法在发送给AI前修改。此提议旨在增加编辑环节，提升交互可控性。
    [查看详情](https://github.com/anthropics/claude-code/issues/3412)

3.  **#61415 | [Bug] macOS桌面端“绕过权限”模式无法启用** [63评论 | 24👍]
    一个影响很多用户的bug，用户在macOS上尝试切换至“Bypass Permissions”模式时，设置会自动恢复为“Accept Edits”，导致权限配置失效。
    [查看详情](https://github.com/anthropics/claude-code/issues/61415)

4.  **#61869 | [Bug] Opus 1M上下文模型提示需要“usage credits”** [61评论 | 16👍]
    用户已选择Opus Plan模型，但仍被要求启用“usage credits”才能使用1M上下文窗口。此为Linux平台上的高频问题，影响用户对模型能力的正常使用。
    [查看详情](https://github.com/anthropics/claude-code/issues/61869)

5.  **#63896 | [Bug] 压缩会话时API错误要求启用“usage credits”** [41评论 | 25👍]
    另一个关于“usage credits”的错误，在Windows平台上的会话压缩（compaction）过程中出现，表明相关功能的身份验证或计费逻辑存在问题。
    [查看详情](https://github.com/anthropics/claude-code/issues/63896)

6.  **#49747 | [Bug] Opus 4.7在长上下文中混淆XML和JSON工具调用格式** [30评论 | 32👍]
    一个技术性较强的Bug，指出Opus 4.7在处理较长任务时，会错误地在JSON格式的工具调用中混入传统的XML格式，导致工具执行失败。
    [查看详情](https://github.com/anthropics/claude-code/issues/49747)

7.  **#50674 | [Bug] Cowork功能在ARM64 (Snapdragon X) Windows设备上启动失败** [28评论 | 0👍]
    尽管通过了准备性检查，但Cowork（协同工作）功能在ARM架构的Windows设备上依然无法使用。这触及了对新兴硬件平台兼容性的担忧。
    [查看详情](https://github.com/anthropics/claude-code/issues/50674)

8.  **#29017 | [Bug] VSCode扩展丢失对话历史** [25评论 | 18👍]
    用户在使用VSCode扩展时，对话历史记录会意外丢失。这是开发者日常工作流的核心痛点，影响使用体验和效率。
    [查看详情](https://github.com/anthropics/claude-code/issues/29017)

9.  **#9516 | [Feature] 用户中断钩子 (User Interrupt Hook)** [23评论 | 43👍]
    社区希望引入一个钩子机制，允许在Claude Code执行任务被用户中断（如Ctrl+C）时，执行自定义逻辑（如保存中间状态、发送通知等）。
    [查看详情](https://github.com/anthropics/claude-code/issues/9516)

10. **#18009 | [Bug] Slack插件认证失败** [19评论 | 49👍]
    一个高赞的热门Bug，Slack插件因无法进行动态客户端注册而认证失败，表明第三方集成的稳定性仍有待加强。
    [查看详情](https://github.com/anthropics/claude-code/issues/18009)

### **重要 PR 进展**

**#63686 | 将Stale和Autoclose超时从14天延长至90天** ([查看详情](https://github.com/anthropics/claude-code/pull/63686))

这是过去24小时内唯一被更新的PR，但意义重大。面对多达50个待处理Issue，社区贡献者 `caseyWebb` 提议将Issue被标记为“stale”和自动关闭的等待时间从原来的14天大幅延长至90天。此举旨在给维护团队和社区更充足的时间来解决问题，减少因时间不足而误关重要Issue的风险。

*(注：数据源仅提供了一条PR更新，其余9个条目无法从提供的数据中提取。)*

### **功能需求趋势**

从所有Issue中提炼出社区最关注的几个功能方向：

- **IDE集成与体验**：VSCode扩展的稳定性（如#29017丢失历史）是首要关注点。同时，用户希望在TUI和IDE中获得更精细的控制权，例如编辑粘贴内容（#3412）。
- **性能与模型质量**：用户对Opus系列模型的质量非常敏感。多个Issue（#49747, #68780, #71446）反映了对模型性能倒退、推理能力下降和成本控制的担忧，这是当前最核心的痛点。
- **用户体验与工作流**：多账户切换（#36151）、用户中断钩子（#9516）等功能需求，表明社区希望Claude Code能更好地融入个人和团队的工作流，提升操作灵活性和自主性。
- **安全与权限控制**：新版本虽已增强命令分类，但社区仍在追求更细粒度的权限控制，如Linux bwrap沙箱中对Unix Sockets的精细配置（#44180）。
- **多平台与跨端支持**：从macOS到Windows (包括ARM架构)，从本地到远程，社区对跨平台、跨设备（Remote Control, Cowork）的稳定性和一致性提出了更高要求。

### **开发者关注点**

总结开发者反馈中的主要痛点和高频需求：

1.  **模型降级与费用激增**：这是目前最尖锐的问题。用户反馈Opus 4.7/4.8模型“感觉像旧版Sonnet”（#71446）、“推理能力严重下降”（#68780）。更严重的是，存在静默升级模型导致用户（如#71481的作者）在6天内产生超过500美元意外费用的案例，强烈要求官方增加模型切换的明确通知和确认机制。
2.  **工具调用与格式错误**：Claude Code重度依赖工具调用。开发者对模型在长上下文中混淆工具调用格式（#49747）、返回“malformed”错误（#63687）以及输出虚假的XML标签（#68354）等问题感到非常困扰。
3.  **认证与权限问题**：包括桌面端权限模式无法切换（#61415）、Slack插件认证失败（#18009）、多会话间auth token失效（#54179）等，这些问题严重影响了工具的可用性和工作连续性。
4.  **平台兼容性问题**：特别是在Windows的ARM64（Snapdragon X）设备上Cowork功能失败（#50674），以及Linux（Amazon Linux）环境下TUI的滚动条和复制粘贴功能失效（#71491），表明平台适配仍有短板。
5.  **资源消耗与性能**：存在内存泄漏导致性能极速下降（#71493，“每小时增长348MB”），以及VS Code扩展不警告地恢复超大session快速消耗用量（#71478）等问题，开发者对资源管理的透明度和效率提出了质疑。
6.  **桌面端GUI SSH稳定性**：当通过macOS桌面端GUI SSH功能打开多个远程会话时，所有会话会因token失效而挂起（#54179），这对于需要多任务操作的开发者来说是一个严重的效率障碍。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-06-26）

## 今日速览
- **版本发布**：`rust-v0.142.2` 正式发布，新增 MCP 工具默认搜索和 macOS 系统代理支持；同时密集推送了 4 个 `v0.143.0-alpha` 版本。
- **社区焦点**：Rate-limit 异常（#28879）持续发酵，`gpt-5.5` 下配额消耗飙升 10~20 倍，单条 issue 已获 303 个 👍 和 152 条评论；另一个超高关注度的 SQLite 日志写入量问题（#28224）在 3 个 PR 合并后已缓解 85%，社区建议关闭。
- **Windows 沙盒漏洞**：多个 issue 报告 `apply_patch` 触发 `codex-windows-sandbox-setup.exe` 错误弹窗，成为新的高频痛点。

---

## 版本发布

### rust-v0.142.2（latest stable）
- **新功能**：MCP 工具在支持时默认启用**工具搜索**，提升工具发现能力，同时保持与旧模型和旧提供商的兼容性。（[#29486](https://github.com/openai/codex/pull/29486)）
- **新功能**：macOS 认证客户端可**尊重系统代理、PAC 和 WPAD 设置**（需启用 `respect_system_proxy`）。（[#26709](https://github.com/openai/codex/pull/26709)）

### rust-v0.143.0-alpha 系列
- 连续发布 `0.143.0-alpha.16`、`0.143.0-alpha.21`、`0.143.0-alpha.22`、`0.143.0-alpha.25`（共 4 个 alpha），多为内部实验性功能迭代，未公开详细变更日志。

### codex-zsh-v0.1.0
- 首个独立 zsh 插件版本，提供 Codex CLI 在 zsh 下的深度集成。

---

## 社区热点 Issues（Top 10）

### 1. [#28879 - rate-limit 成本飙升 10~20 倍](https://github.com/openai/codex/issues/28879)
- **重要性**：影响面极广，「Plus 计划」用户使用 `gpt-5.5` 时，每 token 消耗的 limit 比例增加 10~20 倍，原本 5 小时预算在 2~3 次 prompt 内耗尽。
- **社区反应**：303 👍、152 条评论，用户纷纷晒出自己的 `token_count` / `rate_limits` 日志，确认服务器端限制了异常增长。

### 2. [#28224 - SQLite 反馈日志年写入 ~640 TB](https://github.com/openai/codex/issues/28224)
- **重要性**：极端 SSD 磨损风险，社区报告 `~/.codex/logs_2.sqlite` 每秒大量写入，模拟年化 640 TB。
- **更新**：作者发帖称 3 个相关 PR 已合并至 `0.142.0`，避免 85% 日志，建议关闭 issue（385 👍、86 条评论）。

### 3. [#25749 - 账号验证绑定失效的旧电话号码](https://github.com/openai/codex/issues/25749)
- **重要性**：用户可通过 Google OAuth 正常登录 ChatGPT，但 Codex 要求验证一个**已无法使用的旧手机号**，且无任何恢复路径。
- **社区反应**：64 条评论，用户呼吁 OpenAI 提供替换电话或跳过的机制。

### 4. [#2137 - Windows 多行粘贴只保留首行](https://github.com/openai/codex/issues/2137)
- **重要性**：持续近一年未修复的老问题，用户粘贴多行文本时自动提交仅保留第一行，严重影响 Windows 用户日常使用。
- **社区反应**：34 条评论，已被标记为 `windows-os` 缺陷。

### 5. [#5957 - 自动压缩导致模型“失忆”](https://github.com/openai/codex/issues/5957)
- **重要性**：Enterprise 用户反馈在 `gpt-5-codex-high` 下，自动上下文压缩使模型忘记正在进行中的任务和已编辑文件，导致工作流中断。
- **社区反应**：31 条评论，用户期待更智能的压缩策略或手动选择压缩时机。

### 6. [#13733 - 后台进程轮询浪费 Token](https://github.com/openai/codex/issues/13733)
- **重要性**：`cargo build` 等后台进程运行时，每次轮询都携带完整历史进行 API 调用，消耗大量 token。
- **社区反应**：30 条评论，用户建议仅发送增量 token 或使用专用状态查询接口。

### 7. [#4867 - 允许含二进制文件的 PR](https://github.com/openai/codex/issues/4867)
- **重要性**：Codex Web 创建 PR 时自动拒绝包含二进制文件的提交，导致 40 分钟工作成果被阻塞。
- **社区反应**：46 👍，27 条评论，社区希望至少提供可配置选项。

### 8. [#30002 - 5h 配额重置后 41 分钟耗尽](https://github.com/openai/codex/issues/30002)
- **重要性**：Pro 用户报告：5h 限额重置后，实际只用了 ~1.35M token 就再次触发 `usage_limit_reached`，而正常情况需要 ~156M token 才耗尽。
- **社区反应**：24 条评论，服务器端配额统计疑似逻辑错误。

### 9. [#30008 - “模型容量不足”持续报错](https://github.com/openai/codex/issues/30008)
- **重要性**：多个用户同时在 App 和 CLI 中收到“Selected model is at capacity”错误，即使切换到不同模型仍无效。
- **社区反应**：22 条评论，疑似后端容量调度出现问题。

### 10. [#17265 - MCP OAuth 令牌不自动刷新](https://github.com/openai/codex/issues/17265)
- **重要性**：Codex 持久化 `refresh_token` 但从不使用，导致过期后所有 MCP 工具调用失败。影响路由 MCP 服务的稳定性。
- **社区反应**：39 👍，19 条评论，开发者要求 OpenAI 实现自动刷新流程。

---

## 重要 PR 进展（Top 10）

### 1. [#30144 - 修复终端 rollout 持久性缺口](https://github.com/openai/codex/pull/30144)
- **内容**：修复 `TurnComplete` / `TurnAborted` 事件在有序远程写入场景下可能丢失的问题，确保会话结束时终端事件可靠存储。

### 2. [#30164 - 新线程模型默认值作用域感知](https://github.com/openai/codex/pull/30164)
- **内容**：支持在一个配置包中加载多个稳定产品作用域的模型默认值，允许 App 根据“工作”或“编码”场景自动选择默认设置，无需重载。

### 3. [#30148 - 复用 MCP 运行时不因无贡献环境而重建](https://github.com/openai/codex/pull/30148)
- **内容**：优化 MCP 运行时复用逻辑，避免当某个 selected 环境没有提供任何 MCP 服务器或连接器时触发不必要的新建流程，提升性能。

### 4. [#30087 - app-server 转发 MCP 资源更新](https://github.com/openai/codex/pull/30087)
- **内容**：将 MCP `notifications/resources/updated` 回调接入核心事件流，并通过 app-server 公开类型化通知，让客户端实时感知资源变更。

### 5. [#30156 - 远程文件系统 walk 不可用时回退](https://github.com/openai/codex/pull/30156)
- **内容**：当执行器（exec-server）不支持优化的 `fs/walk` RPC 时，自动回退到传统方法，防止因为 `method not found` 导致技能发现中断。

### 6. [#30000 - 原型：Codex Apps 作为虚拟 HTTP MCP 服务器](https://github.com/openai/codex/pull/30000)
- **内容**：新增 `codex-apps` crate，将共享的应用上游快照封装为本地流式 HTTP MCP 端点，使 Codex 可以像普通 MCP 服务一样与 Apps 交互。

### 7. [#28582 - 插件预览流量路由到插件服务](https://github.com/openai/codex/pull/28582)
- **内容**：新增 `features.plugin_service_preview` 开关，通过正常配置路径将预览流量引导至插件服务，为员工测试提供隔离通道。

### 8. [#29516 - 持久化 Cloudflare 亲和性 Cookie 用于 MCP HTTP](https://github.com/openai/codex/pull/29516)
- **内容**：处理托管插件服务的 Streamable HTTP MCP 流量时，持久化 `__cflb` cookie，确保请求始终路由到正确的 Cloudflare 节点，避免会话漂移。

### 9. [#30154 - 保留被驱逐 V2 代理的最终状态](https://github.com/openai/codex/pull/30154)
- **内容**：V2 代理在 LRU 驱逐后，状态查询不应返回 NotFound，而是保留在 AgentMetadata 中的最终状态（completed/errored），提升用户界面一致性。

### 10. [#30149 - 可配置生成图像目录](https://github.com/openai/codex/pull/30149)
- **内容**：新增 `generated_images_dir` 配置项，允许用户自定义 AI 生成图像的存放路径，不再强制写入 `$CODEX_HOME/generated_images`。

---

## 功能需求趋势

从当天所有 Issues 中可以提炼出社区最关注的三个功能方向：

1. **配额与计费可观测性**  
   - 用户强烈要求提供更透明的 token 消费明细、配额重置时间、以及实时预算监控，以便排查异常消耗（如 #28879、#30002、#30034）。

2. **Windows 平台稳定性**  
   - 多行粘贴（#2137）、沙盒弹窗（#29200、#29782、#30009）、内存泄漏（#30050）、应用闪退（#27828）等 Windows 专属缺陷频繁出现，说明 Windows 端的 QA 急需补强。

3. **MCP 生态完善**  
   - OAuth 令牌自动刷新（#17265、#27165）、运行时复用优化（#30148）、资源更新通知（#30087）、路由亲和性（#29516）是当前 MCP 集成的主要改进方向，社区期望 MCP 在可靠性和效率上达到生产级水平。

---

## 开发者关注点

- **Rate-limiter 机制不透明**：多个用户反馈“5h 配额”在服务器端存在双标准计费，实际消耗远高于预期，且官方至今未给出明确解释或临时修复。
- **日志写入量过高**：即使 `rust-v0.142.0` 合并了部分 fix，仍有用户报告 SQLite 日志持续大量写入（#29532），SSD 寿命和磁盘空间仍受影响。
- **Windows 沙盒缺陷**：`apply_patch` 必定触发 `codex-windows-sandbox-setup.exe` 错误弹窗，严重阻塞正常工作流，且有 COM+ 注册表错误（#29782），社区期待紧急热修复。
- **旧账号恢复无门**：绑定已失效手机号却无法绕过验证（#25749），导致部分用户完全无法使用 Codex，呼吁 OpenAI 提供多因子验证的替代方案。
- **模型容量提示模糊**：当出现“Selected model is at capacity”时，用户无法手动切换或等待自动恢复，只能猜测后端问题（#30008）。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*