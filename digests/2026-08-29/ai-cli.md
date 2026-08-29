# AI CLI 工具社区动态日报 2026-08-29

> 生成时间: 2026-08-29 05:24 UTC | 覆盖工具: 2 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI CLI 工具横向对比分析报告（2026-08-29）


## 1. 生态全景

当前 AI CLI 工具正处于**功能深水区与稳定性攻坚期并行**的阶段。Claude Code 与 OpenAI Codex 均已从单机终端工具向桌面应用、远程协作、跨端会话等方向演进，但两家的迭代重心出现明显分野：Claude Code 侧重工作流可编程性（钩子系统、规则文件），Codex 则在 Windows 桌面端集中爆发稳定性问题。值得注意的是，**Windows 平台已成为两家共同的软肋**——这与 AI CLI 早期以 macOS/Linux 为核心用户群的历史直接相关。与此同时，Token 成本优化与命令可观测性正在从"进阶需求"变为"核心诉求"，反映出用户群体正从尝鲜者过渡到重度日常使用者。

## 2. 各工具活跃度对比

| 维度 | Claude Code | OpenAI Codex |
|------|-------------|--------------|
| 热点 Issues 数 | 11 个（覆盖安全、Windows 稳定性、集成、功能请求等） | 10 个（其中 8 个与 Windows 直接相关） |
| 最热 Issue 评论数 | 164 条（#84352，安全策略与合规） | 86 条（#40752，Windows 启动失败） |
| PR 进展 | 1 个（安全 glob 模式修复） | 10 个（模型目录、MCP 配置、沙箱策略等） |
| Release | **v2.1.251**（正式版，含新钩子事件与远程协作流式传输） | **5 个 Rust crate alpha 版本**（0.151.0-alpha.7.1 ~ alpha.12） |
| 迭代节奏 | 低频但语义化（一次主要版本，新增明确功能） | 高频但碎片化（连发 5 个 alpha，无详细变更日志） |
| 高赞功能请求 | #10018：Web 非默认分支启动（86 👍） | #39903：禁用命令折叠（65 👍） |

**判读**：Claude Code 呈现"集中式"发布节奏，版本含金量高；Codex 采用"碎片式"快速迭代，工程推进密度大但对外沟通不足。两者今日热度接近，但问题属性差异明显——Claude Code 的热议集中于策略一致性，Codex 的热议集中于基础可用性。

## 3. 共同关注的功能方向

| 方向 | Claude Code 表现 | OpenAI Codex 表现 | 共同诉求 |
|------|-----------------|-------------------|---------|
| **模型切换/路由控制** | 新增 `PreModelSwitch`/`PostModelSwitch` 钩子，支持阻止、确认、注解 | PR #41467 模型选择器实时拉取；#41461 支持中途切换模型后的目录描述 | 开发者要求对"何时用哪个模型"拥有编程级控制权，而非仅靠手动选择 |
| **Token 成本与用量透明化** | #80261（用量指示器）、#80732（/usage API 化）、#83092（用法条） | #35050（显式批处理降低加权用量 27–45%）、"AGENTS.md 规则削减 81.6% 输入" | 用量可见性+可编程优化：用户既不满足于"看不见"，也不满足于"只能看" |
| **Windows 稳定性** | 启动失败（HRESULT 0x80070020）、静默更新破坏会话、Remote Control 默认开启争议 | 更新后 GUI 无法显示、spawn EINVAL、DWM 句柄泄漏、WSL 终端竞态 | Windows 已成为两家最大短板，且均存在"更新引入回归"的恶性循环 |
| **远程/跨端协作** | Remote Con 流式传输、Android Remote（#85285 会话同步） | Android Remote 路径信任失败（#40002）、Computer Use Chrome 控制失效 | 跨端会话管理仍处早期，功能已推出但信任验证、平台一致性远未成熟 |
| **命令可观测性** | 终端 UI 增强（消息队列等） | #39903 禁用命令折叠、code mode 宿主请求独立计时 | 重度用户要看到"每条命令到底发生了什么"，而非被折叠/美化 |

## 4. 差异化定位分析

| 维度 | Claude Code | OpenAI Codex |
|------|-------------|--------------|
| **核心产品思路** | **Agentic Workflow 平台**：以钩子（hooks）为中枢，构建可编程的 agent 生命周期；通过 `.claude/rules/`、安全策略文件实现精细化治理 | **本地执行引擎**：强调 Code Mode 本地工具宿主、沙箱策略、MCP 按工具输出限制，偏向"可控的自动化操作层" |
| **安全/合规路线** | 强合规导向：对接 Cyber Verification Program（CVP）、cyber safeguard 防护层，但因误报频发引发信任危机 | 工程化沙箱路线：权限快照、策略投影惰性化、连续失败自动阻止 goals，安全逻辑与运行机制深度耦合 |
| **目标用户** | 重视规则治理、合规审计的企业/团队用户；利用共享规则文件实现组织级 agent 行为统一 | 追求终端控制力与资源效率的开发者；关注 token 消耗、命令可审计性的 CLI 重度用户 |
| **技术栈倾向** | TypeScript/Node 生态（会话恢复、缓存成本估算、Remote Con 流式传输），Web 运行时拓展至 .NET 9/10 | Rust 核心（5 个 Rust crate 同日发版），强调性能与可嵌入性；TUI/Desktop 分层 |
| **社区反馈与产品决策的互动** | 新钩子事件直接回应开发者对模型路由的诉求；但高赞请求 #10018/#11627 已关闭，社区需求采纳度存疑 | PR 密集合入模型目录、MCP 输出限制等精细控制项，工程响应迅速；但 Windows 故障迟迟未根治，用户已开始自行 workaround |

## 5. 社区热度与成熟度

**Claude Code**：社区热度集中于**个别的深度讨论**——#84352 收获 164 条评论，远超其他 Issue，说明"安全策略一致性"是用户的情绪爆发点。Issue 类型涵盖钩子、规则、符号链接、worktree 等高级特性，用户整体技术水准较高，反馈的专业性较强（如 `**` glob 匹配失败对安全规则的影响分析）。整体呈现**成熟工具特征**：问题不再局限于"能不能用"，而是"是否符合文档承诺、策略是否自洽"。

**OpenAI Codex**：社区热度**分布均匀但议题窄化**——前 10 个热点 Issue 中 8 个涉及 Windows，且集中在 GUI 启动、WSL 集成、DWM 句柄泄漏等技术性故障。这种"一边倒"的问题结构说明 Codex 桌面端仍处于**基础设施补课阶段**。不过其 PR 推进速度（24 小时内 10 个合入/更新）反映出工程团队在核心架构上相当活跃，产品处于**快速迭代但对外沟通滞后**的状态——5 个 alpha 版本无 release notes 即是例证。

> **成熟度结论**：Claude Code 在产品功能深度上领先半步，Codex 在工程迭代速度上显著领先；但从社区反馈质量看，Claude Code 用户已进入"精细化治理"阶段，Codex 用户仍被困在"基本可用性"层面。

## 6. 值得关注的趋势信号

**① Windows 支持已成为 AI CLI 的兵家必争之地**
- 数据：Claude Code 3 条 Windows 专项 Issue（含 0x80070020 启动失败、静默更新破坏会话）；Codex 前 30 个 Issue 中约 2/3 涉及 Windows。
- 信号：AI CLI 的目标用户正从 macOS 开发者扩展到企业 Windows 环境。**当前最大的市场机会，恰恰是解决 Windows 稳定性这个"不性感但决定生死"的问题。**

**② 安全策略的"过度防护"正在反噬信任**
- 数据：Claude Code #84352（CVP 批准组织仍被拦截）164 条评论为今日两工具最高；#90501 授权工作被误判为"毒消息"。Codex #40611 安全增强导致登录死循环。
- 信号：安全功能若缺乏一致性与透明判定依据，对用户信任的损害远大于安全问题本身。**安全与效率的平衡将从"口号"进入"配置粒度"的比拼。**

**③ 模型切换正在成为可编程基础设施，而非手动选择**
- 数据：Claude Code v2.1.251 新增 Pre/PostModelSwitch 钩子；Codex PR #41461/#41457 将模型目录描述贯穿异步消息与多智能体指令。
- 信号：AI CLI 正在从"单模型工具"演进为"多模型路由平台"。**开发者的核心能力将从"选对模型"变为"编排模型切换策略"**——谁能提供最灵活的模型路由控制，谁就掌握下一代 AI 开发工具的平台位。

**④ Token 成本优化已从"技巧分享"进入"产品功能"阶段**
- 数据：Codex #35050 以数据证明串行化导致 27–45% 的加权用量浪费；AGENTS.md 配置可降低 81.6% 累计输入。Claude Code 三条 Issue 指向用量可视化。
- 信号：用户已经意识到**通过配置和工具机制优化成本的空间，可能大于等待模型降价**。可观测性 + 批处理 + 智能上下文管理，将成为 AI CLI 的标配能力。

**⑤ "远程控制"从附加功能走向核心场景，但安全边界尚未厘清**
- 数据：Claude Code 新增前台子代理工具调用流式传输至 Remote Con；Codex Android Remote 因路径大小写无法验证 Windows 项目（#40002）。
- 信号：跨端会话已从小众尝鲜变为真实需求，但路径信任、权限模型、默认开启与否（#88094 的隐私担忧）等基础问题仍未解决。**早期布局者将定义这个赛道的体验标准。**


---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据截止**：2026-08-29 | **数据源**：github.com/anthropics/skills

---

## 一、热门 Skills 排行（按社区关注度 Top 8）

### 1. skill-creator 评估管线修复 — PR #1298
- **功能**：修复 `run_eval.py` 对所有 skill 描述恒定报告 `recall=0%` 的严重缺陷（关联 Issue #556，10+ 独立复现），并顺带修复 Windows 流读取、触发器检测与并行 worker 问题。
- **社区关注点**：评估结果失真意味着描述优化循环一直在"对噪声做优化"，属于基础设施级 bug，直接影响所有 skill 作者。
- **状态**：OPEN（2026-06-10 创建）｜[链接](https://github.com/anthropics/skills/pull/1298)

### 2. document-typography 文档排版技能 — PR #514
- **功能**：防止 AI 生成文档中的孤字换行（1–6 个词溢出到下一行）、寡行段落（标题孤立于页底）和编号错位等排版问题。
- **社区关注点**：针对的是"每个 Claude 生成的文档都会遇到"的普适痛点，属于高质量、低门槛的实用型技能。
- **状态**：OPEN（2026-03-04 创建）｜[链接](https://github.com/anthropics/skills/pull/514)

### 3. scnet-hpc 高性能计算集群技能 — PR #1615
- **功能**：通过 profile 化 SSH 与 Slurm 工作流操作 SCNet HPC 集群，覆盖分区、内存、模块与加速器配置、作业生成与集群发现。
- **社区关注点**：科研/超算场景的垂直需求，社区对专业领域技能的关注度上升。
- **状态**：OPEN（2026-08-20 创建，近期活跃）｜[链接](https://github.com/anthropics/skills/pull/1615)

### 4. pdf 技能大小写引用修复 — PR #538
- **功能**：修正 `skills/pdf/SKILL.md` 中 8 处文件引用大小写不匹配（`REFERENCE.md` → `reference.md` 等），解决大小写敏感文件系统上的加载失败。
- **社区关注点**：官方技能自身的跨平台健壮性问题，社区对"官方仓库也会犯低级错误"反馈强烈。
- **状态**：OPEN（2026-03-06 创建，持续有讨论）｜[链接](https://github.com/anthropics/skills/pull/538)

### 5. ODT 文档技能 — PR #486
- **功能**：新增 OpenDocument 技能，支持 `.odt`/`.ods` 的创建、模板填充、读取及 ODT→HTML 转换，覆盖 LibreOffice 与 ISO 标准格式场景。
- **社区关注点**：文档技能矩阵从 docx/pdf 向开源办公格式延伸，企业用户呼声较高。
- **状态**：OPEN（2026-03-01 创建）｜[链接](https://github.com/anthropics/skills/pull/486)

### 6. frontend-design 技能优化 — PR #210
- **功能**：系统性修订 frontend-design 技能，提升每条指令的可执行性（"在单次对话中可被 Claude 实际遵循"），增强内部一致性与行为引导精度。
- **社区关注点**：社区开始审视现有技能的"可操作性"而非"信息量"，是对官方技能质量的直接反馈。
- **状态**：OPEN（2026-01-05 创建）｜[链接](https://github.com/anthropics/skills/pull/210)

### 7. skill-quality-analyzer + skill-security-analyzer — PR #83
- **功能**：新增两个元技能——质量分析器（结构/文档/示例/资源五维评估）与安全分析器，面向技能的自我审查。
- **社区关注点**：与 Issue #492（社区技能伪装官方命名空间）形成呼应，社区对技能安全审计的需求正在显性化。
- **状态**：OPEN（2025-11-06 创建）｜[链接](https://github.com/anthropics/skills/pull/83)

### 8. Hivemind 零成本多智能体编排 — PR #1628
- **功能**：让 Claude Code 将机械性工作委派给运行免费模型的 headless opencode worker，自身只保留规划、审查与合并角色。
- **社区关注点**："昂贵模型的上下文才是稀缺资源，而非其智能"——多智能体成本优化的新思路，近期热度高。
- **状态**：OPEN（2026-08-21 创建，活跃讨论中）｜[链接](https://github.com/anthropics/skills/pull/1628

---

# Claude Code 社区动态日报（2026-08-29）

## 今日速览

今日发布 **v2.1.251**，引入模型切换生命周期钩子，并将前台子代理的工具调用实时推流到 Remote Con。社区讨论热度集中在 **Windows 平台稳定性**（启动失败、静默更新破坏会话）以及 **cyber safeguard 误报**阻碍合法工作流两大问题上。

---

## 版本发布

### v2.1.251
- **新增钩子事件**：`PreModelSwitch` 与 `PostModelSwitch`，可对模型切换进行阻止、确认或注解
- **SessionStart 增强**：恢复会话时现在会传递 session 过期状态（staleness）及预估重新缓存成本
- **远程协作改进**：前台子代理的工具调用与结果现在支持实时流式传输至 Remote Con

---

## 社区热点 Issues

### ① 安全策略与合规
- **[#84352](https://github.com/anthropics/claude-code/issues/84352)：已获 CVP 批准的 Claude.ai 组织仍被 cyber safeguard 阻止**（164 评论 / 25 👍）
  - 组织已获得 Cyber Verification Program 批准，却在 Claude Code 中持续收到安全拦截；验证门户显示“审核中”，与此前批准邮件矛盾。**社区反响最热烈**，涉及安全策略一致性问题。

- **[#90501](https://github.com/anthropics/claude-code/issues/90501)：实时安全防护误将订单队列验证标记为“毒消息”**（1 评论 / 今日创建）
  - Opus 4.8 误报导致授权工作被 session-halted，属于过高安全过滤的又一实例。

### ② Windows 平台稳定性
- **[#53247](https://github.com/anthropics/claude-code/issues/53247)：Claude Desktop 在 Windows 上启动失败——崩溃后遗留孤立 Silo/Job Object，仅注销/重启可恢复**（30 评论 / 19 👍）
  - HRESULT 0x80070020，影响范围大，重启成本高。

- **[#89680](https://github.com/anthropics/claude-code/issues/89680)：Windows 静默更新遗留孤儿进程，新版无法启动直至重启**（5 评论 / 今日更新）
  - 旧版 AppX 容器被孤儿子进程占用，新版本持续报 0x80070020，是 #53247 的同类或相关根因。

- **[#90172](https://github.com/anthropics/claude-code/issues/90172)：桌面应用静默重启破坏运行中会话（报告 8 项相互关联的缺陷）**（1 评论 / 2 👍）
  - 隐藏重启机制导致会话突断、Remote Control 显示 “computer unreachable”，用户建议按单个缺陷拆分呈报。

### ③ 集成与连接器
- **[#61682](https://github.com/anthropics/claude-code/issues/61682)：GitHub connector 显示“Connected”但 Cowork 中无工具暴露**（27 评论 / 24 👍）
  - Windows 11 环境下 MCP 集成失效，连接状态与实际功能不一致，影响第三方工具链使用。

### ④ 功能请求
- **[#10018](https://github.com/anthropics/claude-code/issues/10018)：Claude Code Web 支持从非默认分支启动会话**（59 评论 / 86 👍 / 已关闭）
  - 社区高赞请求，今日关闭，建议关注是否被官方采纳或被其他方案替代。

- **[#11627](https://github.com/anthropics/claude-code/issues/11627)：Web 运行时支持 .NET 9/10 SDK**（15 评论 / 75 👍 / 已关闭）
  - 后台对数较高的框架支持需求，反映 Web 运行环境对多语言生态的诉求。

### ⑤ 核心行为 Bug
- **[#88405](https://github.com/anthropics/claude-code/issues/88405)：`.claude/rules/` 中的符号链接文件未自动加载，与文档相悖**（7 评论 / 4 👍）
  - 官方文档明确承诺“Symlinks are resolved and loaded normally”，实际不生效——对共享规则工作流影响直接。

- **[#90405](https://github.com/anthropics/claude-code/issues/90405)：git worktree 会话中模型对 cwd 外文件发出相对链接**（2 评论 / 今日创建）
  - 完整 worktree 下可能静默指向其他提交处的过期副本，调试定位成本高。

### ⑥ 隐私与默认行为
- **[#88094](https://github.com/anthropics/claude-code/issues/88094)：Windows 上 Remote Control 被默认开启**（6 评论 / 8 👍）
  - 用户对默认启用远程控制功能表达隐私担忧，建议明确 opt-in 流程。

---

## 重要 PR 进展

过去 24 小时内仅有 1 个 PR 更新：

- **[#87079](https://github.com/anthropics/claude-code/pull/87079)：修复 security-guidance 中 `**` glob 模式无法匹配零深度路径**（更新于 2026-08-28）
  - 当前 `_glob_match` 委托给 `fnmatch`，其中裸 `*` 已能跨 `/` 匹配，导致 `**/*.ts` 需要字面 `/`，从而在 `security-patterns.json` 规则中静默排除顶层文件。**由于是安全规则，这一失败模式会让防护在无提示的情况下失效，修复价值很高。**

---

## 功能需求趋势

从当日 Issue 与 Release 提炼社区关注方向：

1. **模型切换的精细控制** —— 新增 PreModelSwitch/PostModelSwitch 钩子回应了开发者对模型路由可编程控制的需求
2. **Windows 桌面端稳定性** —— 多条 Issue 集中在启动失败、MSIX 安装错误、静默更新破坏会话，是当前最大痛点
3. **用量可见性与可编程访问** —— [#80261](https://github.com/anthropics/claude-code/issues/80261)（主界面用量指示器）、[#80732](https://github.com/anthropics/claude-code/issues/80732)（`/usage` 数据 API 化）、[#83092](https://github.com/anthropics/claude-code/issues/83092)（用法条）共同指向“用量透明化”
4. **远程控制与桌面联动** —— Remote Control 默认开启、iOS/桌面会话同步（[#85285](https://github.com/anthropics/claude-code/issues/85285)）等问题说明跨端会话管理仍在成长期
5. **终端 UI 增强** —— 消息队列（[#348

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-29

## 今日速览

今日社区焦点集中在 Windows 桌面应用的一系列稳定性问题上：多个 Issue 报告应用更新后出现 GUI 无法显示、本地工具宿主握手失败、浏览器控制失效等严重故障，其中 #40752 以 86 条评论成为社区最热话题。与此同时，官方密集推送了 5 个 rust crate 的 alpha 版本，并合入了一批围绕模型目录、上下文管理与 MCP 配置的内部工程优化 PR。

## 版本发布

过去 24 小时内，`openai/codex` 发布了 5 个 Rust crate 版本，均属于 `0.151.0-alpha` 系列：

- [`rust-v0.151.0-alpha.12`](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.12)
- [`rust-v0.151.0-alpha.11`](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.11)
- [`rust-v0.151.0-alpha.10`](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.10)
- [`rust-v0.151.0-alpha.9`](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.9)
- [`rust-v0.151.0-alpha.7.1`](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.7.1)

Release 说明暂未提供详细变更日志，建议关注对应 tag 的 commit 历史。

## 社区热点 Issues

1. **[#40752] Windows 桌面应用更新后无法启动（"Unable to locate Codex CLI" & spawn EINVAL）** — 86 条评论 · 51 👍  
   目前社区最热 Issue。Windows 11 用户在更新至 26.820.60940 后，应用启动即失败，报 `spawn EINVAL` 错误，疑似与 `.cmd` wrapper 处理有关。大量用户确认复现，影响面较广。  
   https://github.com/openai/codex/issues/40752

2. **[#39903] 增加选项：禁用 "Ran N commands" 折叠，始终显示已执行命令** — 44 条评论 · 65 👍  
   开发者希望在 TUI 中保留完整的命令执行记录，而不是自动折叠。该需求获得高赞，反映出核心用户对 CLI 可观测性和审计能力的重视。  
   https://github.com/openai/codex/issues/39903

3. **[#41049] code-mode host 在握手阶段退出，5.6 模型工作异常** — 36 条评论  
   Windows 用户报告本地命令执行通道在初始化握手阶段异常退出，导致无法自动读取目录，属于近期 Windows 工具宿主稳定性问题的又一实例。  
   https://github.com/openai/codex/issues/41049

4. **[#35050] GPT-5.6 常串行化独立的 Code Mode 调用；显式批处理降低加权用量 27–45%** — 29 条评论 · 40 👍  
   用户用数据证明模型在 Code Mode 下倾向于串行执行独立工具调用，建议引入显式批处理机制。这是关于 token 消耗优化的重要实证反馈。  
   https://github.com/openai/codex/issues/35050

5. **[#25271] Computer Use 在 Windows 上无法获取 Chrome URL，甚至 `chrome://newtab/` 也不行** — 26 条评论 · 8 👍  
   Computer Use 的 Chrome 浏览器控制功能在 Windows 上长期存在问题，URL 检测持续失败，已跨多个版本未解决。  
   https://github.com/openai/codex/issues/25271

6. **[#37104] [Windows][WSL] 集成终端在 PTY/WSL 启动前静默失败，底部和侧边面板无法打开** — 23 条评论 · 9 👍  
   Desktop 在 Windows + WSL 环境下的集成终端存在启动竞态问题，错误被静默吞掉，用户无法获得任何提示。  
   https://github.com/openai/codex/issues/37104

7. **[#33192] [Windows 10] DWM Composition 句柄在工具调用任务后持续累积** — 15 条评论 · 10 👍  
   用户通过控制实验证明 Codex 的 terminal 工具调用会导致 DWM 句柄泄漏，单次 5 调用即增加 22 个句柄且不释放，指向渲染子系统的资源管理缺陷。  
   https://github.com/openai/codex/issues/33192

8. **[#41059] [Windows 26.820.9563.0] 外部 Codex CLI workaround 后桌面仍保持无头状态** — 15 条评论  
   即使用户通过外部 CLI 绕过故障，Desktop 应用本身仍无法显示 GUI，说明问题存在于应用层而非 CLI 依赖。  
   https://github.com/openai/codex/issues/41059

9. **[#40611] 启用 Advanced Account Security 后 Codex 应用陷入登录-登出死循环** — 12 条评论  
   macOS 用户在启用高级账户安全（以保留 Daybreak Blue 访问权限）后，应用持续登出，完全不可用，属于认证流程的严重回归。  
   https://github.com/openai/codex/issues/40611

10. **[#40002] Android Remote 因大小写敏感的路径查找，无法验证受信任的 Windows 项目** — 11 条评论 · 8 👍  
    用户在 Android 端发起 Codex Remote 会话时，Windows 项目的路径因大小写不匹配导致信任验证失败，跨端协作场景受阻。  
    https://github.com/openai/codex/issues/40002

## 重要 PR 进展

1. **[#41467] 从 app server 刷新 TUI 模型选择器**  
   模型选择器不再依赖启动时的缓存目录，而是在每次打开时异步拉取当前账户可用模型列表，同时保留缓存选项作为回退。  
   https://github.com/openai/codex/pull/41467

2. **[#41464] 更新会话元数据时保留权限快照**  
   修复了更新客户端名称/版本时意外触发文件系统路径解析、导致既有权限快照被改动的问题，将旧式沙箱策略投影延迟到确实需要重新绑定工作目录时。  
   https://github.com/openai/codex/pull/41464

3. **[#41461] 异步用户消息描述改为从模型目录获取**  
   使 `send_user_message_async` 使用当前 step 模型的目录描述，包括中途切换模型后的场景，并提供内建描述作为回退。  
   https://github.com/openai/codex/pull/41461

4. **[#41457] 主动多智能体指令改为从模型目录获取**  
   为模型元数据增加可选的 `proactive` 多智能体模式消息，`Ultra` 推理在未配置通用模式提示时使用目录中的主动消息。  
   https://github.com/openai/codex/pull/41457

5. **[#41454] 连续执行宿主失败后阻止 goals**  
   跟踪每个 activity goal 的 exec 失败次数，连续 3 次失败后标记 goal 为 blocked，任一工具成功后重置计数。可有效避免反复失败的重试循环。  
   https://github.com/openai/codex/pull/41454

6. **[#41452] 上报 code mode 宿主请求耗时**  
   code mode 的 execute/wait/terminate 请求现在独立计时，wall time 不再包含客户端响应延迟和空闲时间，提升可观测性。  
   https://github.com/openai/codex/pull/41452

7. **[#41448] 澄清 Default 协作模式下的问题处理逻辑**  
   允许在可选问题能实质性地改善工作质量时调用 `request_user_input`，当工具未返回答案时继续按最佳判断工作；权限请求与升级仍走原有流程。  
   https://github.com/openai/codex/pull/41448

8. **[#41447] 支持 `openai/elicitation` 表单请求**  
   新增对 `openai/elicitation/create` 请求的处理，当客户端声明 object 类型的 `form` 能力时即广告该支持，不再从旧的 `openai/form` 能力推断。  
   https://github.com/openai/codex/pull/41447

9. **[#41421] 支持按工具的 MCP 输出限制**  
   为 MCP server 的 `tools` 配置增加 `output_token_limit` 字段，在插件策略与用户策略重叠时取最严格值，审批策略保持独立。  
   https://github.com/openai/codex/pull/41421

10. **[#41413] 优化历史条目查找**  
    对大 thread-history 回合中的条目进行惰性索引，使延迟更新可复用其位置信息；反向搜索映射改为线性扫描 Unicode 字节范围，并保留首次出现语义。  
    https://github.com/openai/codex/pull/41413

## 功能需求趋势

从 Issue 热度与讨论中可提炼出以下方向：

- **Windows 稳定性与修复优先级最高**：前 30 个 Issue 中约 2/3 涉及 Windows，涵盖 GUI 启动失败、WSL 集成、DWM 句柄泄漏、沙箱 EPERM 等，Windows 已成为 Codex 桌面端最突出的稳定性短板。
- **WSL（Windows Subsystem for Linux）支持成熟化**：多个 Issue 关注 WSL 环境下集成终端、Agent 环境切换、项目创建/删除的可靠性，用户对 WSL 作为一等公民的期望持续上升。
- **浏览器控制 / Computer Use 的完善**：Windows 上 Chrome URL 检测失败、native host 过期误报、点击即崩溃等高频问题，表明浏览器自动化功能仍处于早期阶段。
- **Token 成本与上下文效率优化**：既有 #35050（串行调用浪费 token），又有新 Issue #41450 报告“一条 AGENTS.md 规则可削减 81.6% 累计输入”，社区正在积极探索通过配置而非等待模型升级来降本。
- **CLI/TUI 可定制性**：#39903 关于禁用命令折叠的高赞需求，说明重度 CLI 用户希望获得对输出展示的细粒度控制。
- **认证与账户流程**：Advanced Account Security 引发的登录死循环暴露了认证链路中的回归风险，安全增强与稳定性之间的平衡值得关注。

## 开发者关注点

- **Windows 桌面应用故障密集爆发**：从 v26.820 系列开始，多个版本（.60940、.7780、.9563、.80927、.10647）均被报告存在 GUI 不显示、宿主进程握手失败、后台进程启动但无窗口等问题，用户已开始自行通过命令行 flag（如 `--disable-direct-composition`）或外部 CLI workaround 来绕过故障。
- **本地工具宿主（tool host）稳定性**：“code-mode host exited during handshake” 成为 Windows Issue 中的高频错误，直接影响 Code Mode 的目录读取和命令执行，是当前最影响日常使用的缺陷之一。
- **浏览器控制不可用**：Chrome native host 相关的问题反复出现——“out of date”误报、插件卸载失败、只读 sidebar、URL 检测失败——开发者期望恢复对浏览器的可靠读写控制。
- **资源泄漏与性能退化**：DWM Composition 句柄累积、token 串行化导致的加权用量上升，正在引起用户对长会话场景下资源开销的系统性关注。
- **认账流程的回归**：安全功能（Advanced Account Security）与现有会话管理的冲突，导致付费用户完全无法使用应用，这类账号级问题对用户信任的损害尤其严重。

---

*本日报基于 github.com/openai/codex 截至 2026-08-29 的公开数据自动生成，仅供参考。*

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*