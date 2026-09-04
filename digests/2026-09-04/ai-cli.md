# AI CLI 工具社区动态日报 2026-09-04

> 生成时间: 2026-09-04 02:40 UTC | 覆盖工具: 2 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI CLI 工具横向对比分析报告（2026-09-04）

> 本报告基于 anthropics/claude-code 与 openai/codex 两大 GitHub 仓库的公开社区动态数据，聚焦 2026-09-04 当日及近期活跃议题，覆盖范围限摘要中出现的样本，并非全量统计。

---

## 1. 生态全景

当前 AI CLI 工具已进入高频迭代与社区深度参与的阶段：Claude Code 与 OpenAI Codex 均在一日内发布新版本或补丁，功能更新节奏以「日」为单位。社区讨论重心正从「能否完成任务」转向「工程化质量」——窗口管理、会话存储膨胀、跨平台兼容性、检查点回滚、插件扩展等系统性问题成为热门议题。同时，两者都表现出对底层基础设施的探索，例如 Codex 引入 worktrees、Claude Code 社区提出 Function Hooks，标志着 AI CLI 朝着可编程、可插拔、可回滚的「开发环境核心」演进。整体来看，工具的功能边界仍在快速扩张，但稳定性与数据治理的短板也开始制约重度用户的信任度。

---

## 2. 各工具活跃度对比

> 注：数据来自每日社区动态摘要中的「精选」样本，非全量 Issues/PRs 统计。Issue 点赞/评论为摘要中标注的原值。

| 维度 | Claude Code | OpenAI Codex |
|---|---|---|
| **最新 Release** | v2.1.260（/diff 面板、/cost 诊断增强） | rust-v0.153.2（Fast tier 描述修复）；另有 v0.153.1、0.154.0-alpha.1/2/3 |
| **Release 数量（当日）** | 1 个版本 | 1 个稳定版 + 1 个功能版 + 3 个 alpha 预发布 |
| **精选 Issues（Top 10）** | 10 条 | 10 条 |
| **精选 Issues 总点赞** | 约 426 👍（含 #85891 167👍、#12346 131👍） | 约 300 👍（含 #11626 211👍、#2379 32👍） |
| **精选 Issues 总评论** | 约 289 条（#85891 76条、#91870 59条等） | 约 197 条（#11626 40条、#41290 30条等） |
| **PR 动态（当日）** | 摘要未提供 | 10 条（含已合入 #42632、#42605） |
| **最热 Issue 特征** | 桌面窗口置顶缺陷（167👍 + 76💬） | 原生 /rewind 功能请求（211👍 + 40💬） |
| **主要问题类型** | 桌面端体验、功能提案、记忆一致性、安装失败 | 存储膨胀、Windows/WSL 兼容、TUI 体验、会话恢复 |

**小结**：两者社区活跃度接近，但讨论热点分化——Claude Code 最受关注的是 Windows 桌面的软件缺陷与功能提案；Codex 最受关注的是存储规模失控与检查点回滚需求。

---

## 3. 共同关注的功能方向

### 3.1 Windows / WSL 桌面端体验
- **Claude Code**：`#85891` / `#88093` 投诉 Claude Desktop 窗口在 Windows 11 上始终置顶且无法关闭，共获 200+ 赞同 — 属于「基础窗口行为」长期未修复。
- **OpenAI Codex**：`#41290` / `#41463` / `#41539` / `#41822` 等约 29 条活跃 Issue 与 Windows 相关，集中在 WSL 路径解析失败、项目创建删除失败、更新后启动过慢等。
- **共性诉求**：Windows 桌面端的稳定性与原生体验已成为两大工具共同短板，直接影响开发者日常使用接受度。

### 3.2 会话 / 状态数据治理
- **Claude Code**：`#81833` 反映 git-worktree 会话中 Auto-memory 加载不一致，影响多分支记忆可靠性；`#71603` 移动端草稿状态静默丢失。
- **OpenAI Codex**：问题更严重——`#24948` 日志膨胀到 700MB–2GB；`#34268` fork 导致单会话 110GiB 存储增长；`#34337` 更指出 CLI/Desktop 共享存储可达 TiB 级。
- **共性诉求**：会话状态的生命周期管理（记录、索引、快照、回收）尚未形成稳健方案，是规模化使用的核心风险。

### 3.3 检查点与撤销/回滚能力
- **Claude Code**：v2.1.260 新增 `/diff`，让用户实时查看 Claude 改动，但仍是「观察」层面，未覆盖「回滚」。
- **OpenAI Codex**：`#11626` 请求 `/rewind` 同时恢复对话与代码，211👍 居全榜第一；TUI 输入撤销/重做（`#2379`）也持续被要求。
- **共性诉求**：开发者希望不仅「看见 AI 改了什么」，更希望「能一键回到之前状态」，回滚能力正被视为 AI 编程工具的基本安全网。

### 3.4 模型与后端路由的可配置性
- **Claude Code**：`#38698` 提议为子代理配置独立模型供应商（如主代理用 Anthropic API，子代理用本地 Ollama）。
- **OpenAI Codex**：多 PR 支持 GPT-6-Astra 通过 API 配置并加入 Amazon Bedrock 目录，且 worktrees 功能扩展执行隔离环境。
- **共性诉求**：用户希望突破单一模型/后端的锁定，让不同任务（主对话、子代理、批量执行）可用不同模型或本地推理，以平衡成本、隐私和控制力。

---

## 4. 差异化定位分析

| 维度 | Claude Code | OpenAI Codex |
|---|---|---|
| **功能侧重** | 强调与编辑流程的深度交互（`/diff`、cost 诊断）、插件化能力升级（Function Hooks 提案） | 重在执行隔离（worktrees）、模型目录升级（GPT-6-Astra 接入）、TUI 渲染健壮性 |
| **核心用户画像** | 插件开发者、Hook 研究者、多平台桌面重度用户、企业 GitLab 客户 | CLI 高级用户、本地模型开发者、Windows/WSL 环境开发者、长会话/大数据量任务执行者 |
| **技术路线** | 试图通过`/`命令加 UI 面板解决「可观察性」；社区提出基于 `next` 链的 Hook 架构，强调安全副作用追踪 | 优先解决「存储与状态」的架构级问题，通过 Rust 重写、DAG/增量存储讨论、worktrees 隔离进行根本改进 |
| **版本发布风格** | 小功能增强+补丁，版本号稳定，如 v2.1.260 | 高频补丁+多个 alpha 并行，如 rust-v0.153.2 + 0.154.0-alpha.1/2/3，开发节奏更激进 |
| **社区生态成熟度** | 已有大量围绕高端功能提案的深度讨论（如 Function Hooks、GitLab 集成），但 Windows 基础缺陷分散了部分精力 | 社区更多投入「数据爆炸」的排障与案例分析，对架构演进路径（DAG 存储等）已有清晰声音 |

**总结**：Claude Code 侧重「交互层创新」与「开放扩展」；OpenAI Codex 侧重「执行引擎的工程化与规模化」——前者更像一个「AI 驱动 IDE」的壳，后者更像一个「agent 沙箱容器」。

---

## 5. 社区热度与成熟度

- **Claude Code**：单日精选 Issue 总点赞 426👍、评论约 289 条，最热问题集中在「Windows 窗口置顶」这一类**使用体验缺陷**。说明其社区已有一大群把工具用作日常生产力的用户，对细节体验非常敏感；同时也说明核心开发者可能需要加强桌面端质量管理。成熟度：作为传统 Claude Code 产品，插件与 GitLab 集成等「扩展类」需求长期未落地，显示官方生态开放节奏偏保守。
- **OpenAI Codex**：单日精选 Issue 总点赞约 300👍、评论约 197 条，其中 `#11626` 功能请求点赞 211，远超其他问题，表明社区对「检查点回滚」有极高统一期待。存储膨胀类 issue 从几百 MB 到 TiB 级，反映工具在高负载长期使用中暴露出架构性问题，用户仍在积极给开发团队「上课」。成熟度：处于快速迭代但尚未稳定的阶段；多 alpha 版本 + 多 PR 并行，说明开发团队响应速度较快，但后端存储架构需要谨慎重构。

**总体**：两个社区都高度活跃，但 `Claude Code` 的用户更关注「桌面端体验与功能可扩展性」，而 `OpenAI Codex` 的用户更关注「数据与执行机制的可靠性」。从 issue 点赞比例看，Codex 的社区需求更集中（少数大票型 issue），Claude Code 的需求更分散（多个高赞议题并存）。

---

## 6. 值得关注的趋势信号

1. **存储膨胀成为规模化死穴**  
   Codex 多个 Issue 指出会话日志、fork 历史、归档文件可增长至数十 GB 乃至 TiB 级，根本不是文本压缩能解决的。这预示着：所有 AI CLI 工具未来都需要引入 **增量/DAG 存储**，而非每次 fork 全量复制父历史。开发者若在工具上构建长期自动化任务，应提前规划会话数据清理/归档策略。

2. **Windows/WSL 是工具渗透的第二战场**  
   两大工具均在 Windows 上出现批量缺陷，Codex 甚至出现 50 条活跃 issue 中 29 条与 Windows 相关。说明 AI CLI 早期用户多为 macOS/Linux，但随着工具走向大众，Windows 支持质量将直接决定市场覆盖度。对开发者的启发：若要为团队选择 AI CLI，需在 Windows 环境小范围验证路径处理、文件系统事件、终端交互等基础环节。

3. **「可回滚」比「可生成」更重要**  
   Codex 的 `/rewind` 请求长期位居榜首，Claude Code 的 `/diff` 也是满足「实时可见」的第一步。AI 编写代码出错不可避免，**可靠的生产力必须包含「撤销与状态恢复」**——这不是锦上添花，而是信任底座。

4. **从「单体 agent」走向「插件与可编程」**  
   Claude Code 社区提出的 Function Hooks、子代理独立模型路由，以及 Codex 的 worktrees、GPT-6-Astra 多后端接入，共同指向一个趋势：AI CLI 将从「固定对话工具」演化为「可编程代理基础设施」。不同任务可挂载不同模型、不同沙箱、不同策略。开发者如果要在自己的工作流中深度嵌入 AI，应优先选择开放 Hook / API / Worktree 机制的工具。

5. **文档与目录驱动需求需同步测试**  
   Codex 的 GPT-6-Astra 改动显示模型接入非常快，但存在「描述文本错误」「仅影响显示，不影响实际请求」等问题，说明**模型目录与实际行为之间存在验证盲区**。类似地，Claude Code 的 `/cost` 新增 cache miss 诊断，也说明「计费/成本透明度」是用户非常敏感的层面。对开发者而言，理解模型分层、cache 机制，以及关注工具自身的诊断能力，能更准确地控制 AI 使用成本。

---

**一句话总结**：2026 年的 AI CLI 竞赛已从「谁能更快写代码」转向「谁能让 AI 代码编写过程更可控、更可回滚、更可扩展」，而 Windows 支持、存储架构、插件生态将在未来 6~12 个月决定工具的护城河。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

⚠️ Skills 摘要生成失败。

---

# Claude Code 社区动态日报（2026-09-04）

> 技术分析师精选 · 数据来自 [anthropics/claude-code](https://github.com/anthropics/claude-code) GitHub 仓库
> 数据统计截至 2026-09-04，覆盖过去 24 小时 Releases / Issues / PRs 动态。

---

## 一、今日速览

- **发布 v2.1.260**，带来期待已久的 `/diff` 全屏差异面板，并改进 `/cost` 对 prompt-cache miss 的原因诊断。
- **Windows 桌面端"窗口置顶"缺陷持续发酵**：两个关联 Issue 合计获 200+ 赞同、93 条评论，成为当下社区讨论度最高的软件缺陷。
- **两个高赞方向性提案浮出水面**：`#91870` 提出 Function Hooks 以重构插件能力模型，`#12346` 再次催更 GitLab 官方集成——社区对深层次扩展基础设施的需求越发强烈。

---

## 二、版本发布

### v2.1.260
- 新增 `/diff`：在全屏模式下，会话旁边打开差异面板，实时展示 Claude 编辑时产生的未提交更改；可按键也可通过 `/diff` 切换。
- 完善 `/cost` 诊断信息：现在会给出 prompt-cache 未命中的可能原因，例如工具定义或系统提示变更、空闲超过 TTL 等。

> 发布说明很短，属于小功能增强版本。`/diff` 直接回应了开发者"希望实时看到 Claude 改动"的高频反馈。

---

## 三、社区热点 Issues（精选 10 条）

### 1. Claude Desktop (Windows 11)：主窗口始终置顶，无设置项可关闭
- **Issue #85891** · 💬 76 条评论 · 👍 167 · 2026-08-11 创建，09-04 更新
- Windows 11 上 Claude Desktop 窗口始终显示在其他应用之上，切换焦点也无法遮盖，且应用内没有任何开关能禁用该置顶行为。这是 #66516 的 Windows 对应报告。
- 社区反应：讨论度极高，多个用户给出 registry hack 和第三方窗口管理工具的临时方案，更多人期待官方修复。
- 链接：https://github.com/anthropics/claude-code/issues/85891

### 2. Function Hooks——让插件能力 10 倍提升
- **Issue #91870** · 💬 59 条评论 · 👍 32 · 2026-09-03 创建，09-04 更新
- 作者提出"Function Hooks"设计，允许深入修改 Claude Code 行为，通过带参数化 `$` 对象的副作用追踪来保证安全性，同时借鉴 Express/Koa 的注册顺序 `next` 链式模型，确保组件能够优雅组合。
- 社区反应：插件和 Hook 开发者高度关注，围绕安全边界和兼容性展开了深入讨论。
- 链接：https://github.com/anthropics/claude-code/issues/91870

### 3. 【功能请求】添加 GitLab 集成（仓库连接、MR、移动端访问）
- **Issue #12346** · 💬 51 条评论 · 👍 131 · 2025-11-25 创建，09-04 更新
- 用户希望 Claude Code 原生支持 GitLab 仓库连接与合并请求操作，目前 GitHub 之外的 Git 托管平台支持明显缺失。
- 社区反应：该请求已存活近一年仍处于 Open，131 个 👍 说明企业自建 GitLab 的用户群体庞大且呼声长期不减。
- 链接：https://github.com/anthropics/claude-code/issues/12346

### 4. Claude Desktop Windows 安装器失败（AddPackage 0x80073CF6）
- **Issue #49917** · 💬 37 条评论 · 👍 8 · 2026-04-17 创建，09-04 更新
- 首次安装看似成功，但实际留下不一致状态；后续重装触发 Windows 包管理器错误 `HRESULT 0x80073CF6`，普通卸载流程难以修复。
- 社区反应：大量用户报告了相似环境（Windows 11 + MSIX 部署），评论中互相分享 PowerShell 清理脚本，属于影响上手体验的阻塞级缺陷。
- 链接：https://github.com/anthropics/claude-code/issues/49917

### 5. Claude Desktop (Windows) 窗口始终覆盖其他应用
- **Issue #88093** · 💬 17 条评论 · 👍 37 · 2026-08-20 创建，09-04 更新
- 与 #85891 相同问题的第二次独立上报，包含更加具体的环境复现信息。
- 社区反应：这是对 #85891 的有力佐证——问题并非个例，已形成多源反馈。
- 链接：https://github.com/anthropics/claude-code/issues/88093

### 6. git-worktree 会话中 Auto-memory 加载不一致
- **Issue #81833** · 💬 12 条评论 · 👍 0 · 2026-07-28 创建，09-04 更新
- 在 `<repo>/.claude/worktrees/<name>` 中启动的会话，有时能加载项目完整的 `MEMORY.md` 索引，有时则完全没有任何记忆内容——同一仓库、同一天内复现。
- 社区反应：虽然点赞数不高，但评论中多位重度用户确认遇到，影响多分支并行开发工作流的记忆可靠性。
- 链接：https://github.com/anthropics/claude-code/issues/81833

### 7. 功能提案：为子代理配置独立的模型供应商路由（如本地 Ollama）
- **Issue #38698** · 💬 12 条评论 · 👍 43 · 2026-03-25 创建，09-04 更新
- 目前 `ANTHROPIC_BASE_URL` 和模型供应商配置属于会话级作用域，子代理无法单独路由到其他推理后端；`model` 参数只能指定 `sonnet/opus/haiku` 且都指向同一供应商。
- 社区反应：43 👍 背后是本地模型开发者群体的痛点，希望主代理用 Anthropic API、子代理跑本地 Ollama 或自建网关。
- 链接：https://github.com/anthropics/claude-code/issues/38698

### 8. 移动端（Pixel 8 Pro）：代理忙时输入的文字在后台时被静默丢弃
- **Issue #71603** · 💬 11 条评论 · 👍 8 · 2026-06-26 创建，09-04 更新
- 用户在 Claude Code 移动端/Web 界面中正在输入，而代理仍在忙碌执行。此时切到后台再返回，未确认的草稿消失且不可找回。
- 社区反应：与 #63975（iOS 滑动退出丢输入）一起，构成跨平台移动端输入状态管理不佳的证据链。
- 链接：https://

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-09-04）

## 1. 今日速览

今日 Codex 发布了 0.153.2 补丁版本，修复了 GPT-6-Astra Fast tier 的速度描述文本错误；同时完成了 GPT-6-Astra 模型目录向 Rust 0.153 系列的后向移植，使其可通过 API 配置但不改变默认模型。社区方面，Windows/WSL 环境下的项目创建失败、会话日志无限膨胀等存储与稳定性问题仍是用户反馈的核心焦点。

## 2. 版本发布

### rust-v0.153.2
- **Bug 修复**：更正 GPT-6-Astra Fast tier 描述为“2x speed, increased usage”而非“1.5x”，仅影响显示文本，不影响实际请求处理。（[#42632](https://github.com/openai/codex/pull/42632)）
- Changelog: https://github.com/openai/codex/compare/rust-v0.153.1...rust-v0.153.2

### rust-v0.153.1
- **新功能**：支持通过 API 配置 GPT-6-Astra，无需更改默认模型或将其显示在模型选择器中。（[#42605](https://github.com/openai/codex/pull/42605)）
- Changelog: https://github.com/openai/codex/compare/rust-v0.153.0...rust-v0.153.1

### alpha 预发布版本
- 0.154.0-alpha.1 / alpha.2 / alpha.3：连续三次 alpha 迭代，无明显公开发行说明。

## 3. 社区热点 Issues（Top 10）

### [#11626](https://github.com/openai/codex/issues/11626) — CLI 原生 /rewind 检查点恢复功能（211👍 / 40💬）
创建于 2026-02-12 并持续活跃。用户希望 `/rewind` 能从同一检查点同时恢复对话上下文与 Codex 应用的工作区代码编辑。当前 Esc rewind 只能回滚对话，代码改动无法一并还原。该 issue 长期位于社区功能需求榜首，表明工作区安全回滚是 CLI 重度用户最迫切的需求。

### [#24948](https://github.com/openai/codex/issues/24948) — Codex 会话日志膨胀至 700MB–2GB（4👍 / 31💬）
Codex CLI 0.118.0（Pro、gpt-5.5、macOS arm64）会话日志因反复的 compaction history 与原始工具输出累积而膨胀至 700MB-2GB。大量用户在评论中确认复现，是存储增长类问题中最具代表性的公开讨论之一。

### [#41290](https://github.com/openai/codex/issues/41290) — Windows + WSL 切换后项目创建/删除失败（21👍 / 30💬）
Codex 桌面版（26.825.31414）在将 Agent Environment 切换为 WSL 后创建和删除项目失败。Windows 用户在多个版本上确认该 bug 持续存在，此 issue 也是 29 个 Windows 相关活跃 issue 中被讨论最多的入口。

### [#41463](https://github.com/openai/codex/issues/41463) — Windows + WSL 路径反序列化导致无法创建项目（12👍 / 23💬）
**AbsolutePathBuf 缺少基础路径**导致 Codex Desktop（Windows + WSL2）无法创建项目。与 #41290 相关联但根因不同，开发者正追踪此路径处理缺陷，是 Windows/WSL 生态问题中的关键子issue。

### [#25779](https://github.com/openai/codex/issues/25779) — Codex Desktop 会话状态无界增长导致冻结（meta-bug，8👍 / 17💬）
会话/轮次状态无界增长造成应用冻结、上下文膨胀、丢失活动轮次控制。该文件被标记为 meta-bug，汇总了多个 Desktop 会话状态子问题。

### [#39897](https://github.com/openai/codex/issues/39897) — macOS 已删除会话残留于侧栏且无法移除（4👍 / 15💬）
ChatGPT Desktop (Codex) 中删除会话后条目仍残留在侧边栏“Recent”列表中，即使重启也无法消失。macOS 用户在多版本中反馈同样的“ghost conversation”问题（参见另一重复 issue #41987），疑似会话索引与存储层之间的同步缺陷。

### [#34268](https://github.com/openai/codex/issues/34268) — Multi-agent V2 全历史 fork 导致超 100GiB 存储增长（6👍 / 13💬）
长会话中每次 fork 都重复父级 compaction 快照与内联图像，导致 Multi-agent V2 会话存储呈乘性增长（单会话达 110GiB），属于 #24948 与 #41806 的高阶形态。

### [#2379](https://github.com/openai/codex/issues/2379) — TUI 输入框支持撤销/重做（32👍 / 11💬）
请求 Cmd-Z / Shift-Cmd-Z 撤销/重做提示词输入。虽为 2025-08 就提出的旧 issue，但 2026-09-04 仍在持续更新，充分显示 TUI 用户对基础编辑体验的诉求长期未被满足。

### [#34337](https://github.com/openai/codex/issues/34337) — CLI/Desktop 共享 rollout 存储可悄然膨胀至 TiB 级（2👍 / 10💬）
CLI 与 Desktop 共用 rollout/session 存储，常规长跑任务即可使卷宗从几十GiB扩展至数百GiB乃至TiB规模。评论指出现有 zstd 压缩值并非根因，存储结构本身需要重构。

### [#41822](https://github.com/openai/codex/issues/41822) — Windows 更新后 CPU 运行时执行 4,680 次加密复制重试（0👍 / 7💬）
每次 Store 更新后首次启动需要执行 4,680 次注定失败的加密复制重试，导致约 8 分钟的“headless”等待。是 Windows Desktop 更新时间过长系列问题的一部分（见 #41539）。

## 4. 重要 PR 进展（Top 10）

### [#42632](https://github.com/openai/codex/pull/42632) — 修复 GPT-6-Astra Fast tier 描述（已合入 0.153.2）
人工提交（非 bot），修正 bundled 目录中的速度描述为“2x speed, increased usage”，用于 0.153.2 补丁版本。

### [#42652](https://github.com/openai/codex/pull/42652) — 为 `codex exec` 增加 managed worktrees
为 `codex exec` 新增实验性的 worktrees 功能与共享 `--worktree` 标志。每个启用的会话在独立的 Git worktree 中运行，可大幅提升并行任务与 fork 实验的隔离性。

### [#42605](https://github.com/openai/codex/pull/42605) — GPT-6-Astra 模型目录 backport 至 0.153（已合入 0.153.1）
将 hidden/API-only 的 GPT-6-Astra 模型定义（含 prompts、policies、`unified_exec` shell 类型）回移发布线，不改变默认模型，不进入模型选择器。

### [#42650](https://github.com/openai/codex/pull/42650) — 在 TUI 中将助手文件引用渲染为本地链接
将 `codex-file-citation` 指令转为本地文件链接，同时保留路径中 Markdown 特殊字符、Unicode、Windows 分隔符与位置后缀。增强 TUI 中对文件引用的可点击性。

### [#42641](https://github.com/openai/codex/pull/42641) — 修复全屏覆盖层退出后的 TUI 内联恢复
离开 alternate-screen overlay 后使恢复的 inline viewport 无效化，避免残留脏单元格及历史对话被滚出视野。针对全屏查看器与内联模式切换的渲染 bug。

### [#42640](https://github.com/openai/codex/pull/42640) — 加固 TUI 对助手标记语言的解析
新增共享解析器来统一处理带引号/不带引号属性、嵌入花括号、转义引号及畸形输入；解析器统一用于 Git action receipts 与代码注释提取。

### [#42639](https://github.com/openai/codex/pull/42639) — 保存模型默认值被覆盖时发出警告
当配置写入成功但被更高优先级配置层覆盖时，TUI 会给出警告——解决“保存成功但实际不生效”的误导性问题，影响模型、 reasoning-effort 与 service-tier 默认值。

### [#42619](https://github.com/openai/codex/pull/42619) — GPT-6-Astra 加入 Amazon Bedrock 目录
添加 `openai.gpt-6-astra` 至 Amazon Bedrock 模型目录，包括全球与 US 跨区域变体。延续 Codex 对多后端模型分发的支持扩展。

### [#42607](https://github.com/openai/codex/pull/42607) — GPT-6-Astra 加入 bundled 模型目录
新增隐藏的 `gpt-6-astra` 模型定义（含推理级别、工具能力、上下文限制、Agent 指令与审查策略），并调整既有模型优先级。

### [#42631](https://github.com/openai/codex/pull/42631) — Voice 宿主初始化 bundled GStreamer 运行时
为 voice helper 增加 `initializeRuntime` 协议交换，对话前先加载并验证打包的 GStreamer 原生运行时是否可安全初始化。

## 5. 功能需求趋势

综合活跃 Issues，社区当前最关注以下功能方向：

- **检查点/回滚机制**（#11626）：原生 `/rewind` 恢复对话+代码的呼声居高不下，212👍 为全 Issue 列表最高
- **TUI 编辑器体验**（#2379 撤销/重做、#41242 浅色主题、#42650 本地文件链接）：基础编辑器能力与视觉一致性持续被诟病
- **存储/会话数据治理**（#24948、#25779、#34268、#34337、#41806）：“会话膨胀”已从偶发变成系统性隐忧——compaction 复制、fork 重复、归档不清理三大根因被反复提及
- **Windows/WSL 原生支持**（#41290、#41463、#41539、#41822）：路径解析、进程退出、文件操作在 WSL 环境的多处断裂成为 Windows 用户的首要痛点
- **GPT-6-Astra 模型接入**（#42607、#42605、#42619）：新模型以“hidden / API-only”方式进入目录，未来可能支持跨 Bedrock 多区域部署
- **TUI 输出健壮性**（#42640、#42641）：用共享解析器统一处理所有助手标记可减少边缘输入导致的渲染崩溃

## 6. 开发者关注点

- **存储增长是最突出痛点**：多个独立 issue（#24948、#34268、#34337、#41806、#22593）指向同一深层问题的不同面——rollout JSONL 中反复嵌入 `replacement_history`、session fork 全量复制父历史、归档永不清理。#41806 给出量化案例：单月膨胀 28.6GB，总计 42GB。开发者期望的修复路径之一是 **delta/DAG 存储**（#22593），避免全量历史复制。
- **会话与索引不一致**：#39897 / #41987（macOS 幽灵会话）、#38972（后台 turn 状态误报）、#42483（中断后的恢复/分叉挂起）表明 Desktop 与 CLI 在会话生命周期管理上仍存在竞态与索引同步的缺陷。
- **Windows + WSL 是新重灾区**：当前 50 条活跃 Issue 中约 **29 条与 Windows 直接相关**，且 #41290 / #41463 / #41539 / #41822 多个 issue 集中在同一天（8/28–8/31）提交，说明近期 Windows 版本的改动引入了批量回归。
- **执行层信任与安全检查**：#32597（个人仓库被误判为安全风险）与 #42602（deprecate detached review delivery）说明沙箱与审查策略正在变得更为严格，但误报与弃用路径需要更平稳迁移。
- **新模型需更低接入成本**：GPT-6-Astra 的目录配置变更（#42638、#42605、#42607）全部由人工或 bot 在 48 小时内密集合入，社区新模型支持节奏快，但部分改动仍停留在文本与目录层面——真正的行为差异（#42632 中描述与实际的差异）需要更完善的测试验证机制防止文本承诺先行。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*