# AI CLI 工具社区动态日报 2026-08-22

> 生成时间: 2026-08-22 00:59 UTC | 覆盖工具: 2 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI CLI 工具横向对比分析报告

**分析日期：2026-08-22**
**覆盖工具：Claude Code v2.1.239 ｜ OpenAI Codex rust-v0.150.0-alpha 系列**

---

## 1. 生态全景

AI CLI 工具正在完成从「编码辅助终端」向「具备安全审查、远程控制与多平台协同能力的开发者基础设施」的转型。当前两大头部玩家均处于高强度迭代期——Claude Code 以稳定节奏发布正式版并加强成本透明化；OpenAI Codex 则密集发布 Rust 预发布版（24 小时内 6 个 alpha），围绕 Guardian 安全审查、沙箱权限与远程连接做系统性重构。**安全机制的可解释性、跨端稳定性、模型工具选择规范性**成为社区最集中的诉求方向。与此同时，Windows 桌面端是两家公认的体验洼地，Top 级 issue 均源于此。

---

## 2. 各工具活跃度对比

| 对比维度 | Claude Code | OpenAI Codex |
|---|---|---|
| 当日版本发布 | 1 个正式版（v2.1.239） | 6 个 Rust 预发布版（0.149/0.150 alpha） |
| 精选热点 Issues | 10 个 | 10 个 |
| 最热 Issue 评论数 | 133 条（#84352，安全拦截） | 24 条（#35119，WSL 误判） |
| 最高 👍 数 Issue | 101（#19649，模型偏爱 Bash） | 17（#35119，WSL 误判） |
| 重要 PR 动态 | 24 小时内无新增/更新 | 6+ 个关键 PR 合入（沙箱/Guardian/Bedrock） |
| 评论集中度 | 高度集中（Top2 issue 占 133/128 条） | 集群爆发（Remote 故障 5 个 issue 同时活跃） |
| 迭代节奏 | 稳定正式版 + 聚焦社区反馈 | 高频 alpha + 批量基础设施重构 |

---

## 3. 共同关注的功能方向

| 关注方向 | Claude Code 具体诉求 | OpenAI Codex 具体诉求 |
|---|---|---|
| **安全审查可解释性** | CVP 批准组织仍被安全拦截，审批状态与邮件矛盾（#84352，133 评论）；Fable 5 安全块 20+ 条误报（#73168–#73228） | Guardian 审查升级命令路由（PR #40005）；严格 MCP 自动审查拒绝/超时结果需保留完整理由（PR #40031） |
| **沙箱/权限精细化** | 模型自动用 Bash sed/heredoc 改文件、绕过内置工具（#88041，最新回归） | 沙箱升级遵循细粒度 `sandbox_approval` 策略（PR #40024）；沙箱状态文件被 NUL 损坏后永久不可用（#35718） |
| **跨平台/Windows 稳定性** | Windows 桌面版文件锁导致无法重启（#42776，63 👍）；Linux TUI 无法复制文本（#62699，67 👍） | Windows+Android Remote 连接故障集群爆发（5 个 issue）；Computer Use 受 WindowsApps 权限限制不可用（#34764） |
| **会话/状态一致性** | 切换账户后全部会话丢失（#48511）；`Claude-Session:` trailer 忽略 attribution 配置（#77830） | 线程重命名后 SQLite 与 session_index 状态分裂（#16405）；VS Code 多窗口打开会话导致所有权静默转移（#38629） |
| **多 Provider/多云支持** | Bedrock/Vertex/Foundry 渲染器体验纳入正式版 | Amazon Bedrock setup 进入 app server（PR #40007）；原生 subagent 编排在第三方 Provider 下失效（#17598） |
| **模型工具选择偏好** | 模型频繁用 Bash 而非 Read/Grep/Edit（#19649，101 👍）；auto-mode "bashFirst" 硬编码误导（#88041） | 虽无同主题 issue，但 PR #40018 为浏览器/Computer Use 增加 typed 配置，侧面回应工具调用规范化 |

---

## 4. 差异化定位分析

| 维度 | Claude Code | OpenAI Codex |
|---|---|---|
| **功能侧重** | 成本估算精细化（数据驻留溢价）、多平台渲染器体验、Cowork 密集协作、安全审批链路合规（CVP） | Rust 原生重构、Remote Control 移动端延伸、Computer Use 桌面自动化、Guardian 安全审查、沙箱权限系统重建 |
| **目标用户** | 企业级/合规敏感团队，重视成本控制与审批审计；跨 Windows/macOS/Linux 的桌面开发者 | 移动-桌面协同开发者、安全隔离需求强烈的沙箱场景；接受 alpha 版本的早期采用者 |
| **技术路线** | 稳定版本节奏，以功能增强和成本透明为主；社区反馈驱动修复（安全拦截、模型行为修正诉求明显） | 高频预发布快速试错，底层基础设施重构（统一 exec、app server、Rust 线程挂起机制）；PR 由自动化 bot 批量合入，工程流程高度工业化 |
| **社区生态特征** | 讨论深度高：关注模型行为规范、配置一致性等「软性」问题；Windows 稳定性是主要短板 | issue 联名效应强（同一问题多人多端复现）；处于「修复历史欠账 + 铺设新架构」并行期 |

---

## 5. 社区热度与成熟度

**Claude Code**：社区活跃度呈**「高共鸣、低 PR」**特征。用户在行为类 issue 上的共识度极高（如 #19649 获得 101 个 👍，成为模型行为标杆问题）；安全拦截问题积累了惊人的 133 条评论，说明合规链路的信任成本极高。但开发侧响应存在滞后——24 小时无任何 PR 更新，可能意味着主力精力投入在尚未公开的大版本开发中。整体呈现**成熟产品的稳定维护期 + 用户期待更高行为标准**的组合状态。

**OpenAI Codex**：处于**「快速重建期」**。24 小时内 6 个 alpha 版本 + 6+ 个关键 PR 合入（全部由 copyberry[bot] 提交），显示出高度自动化的 CI/CD 流水线和密集的基础设施重构节奏。社区 issue 呈现「集群式爆发」（Remote 故障 5 个 issue 同时出现，跨 3 台设备复现），但单 issue 的评论/点赞量低于 Claude Code，说明用户更倾向于「报告问题」而非「深入讨论根因」。这是典型的高速迭代期表现——用户等待官方修复，而非社区互助。

---

## 6. 值得关注的趋势信号

> 以下信号对技术决策者与开发者具有直接参考价值：

**① 安全机制必须「可解释、可审计、可配置」**  
Claude Code 的

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

> 数据截止 2026-08-22 · 数据源：github.com/anthropics/skills

---

## 1. 热门 Skills 排行

> 以下 PR 均处于 **Open / 未合并** 状态，按社区关注度、Issue 关联度和讨论深度排序。

| 排名 | Skill / PR | 功能与社区热点 | 状态 |
|---|---|---|---|
| 1 | **skill-creator 评估修复** [PR #1298](https://github.com/anthropics/skills/pull/1298) | 修复 `run_eval.py` 始终报告 `recall=0%` 的关键 bug，涉及 Windows 流读取、触发检测和并行 worker。关联 Issue #556 已有 10+ 独立复现，社区关注度极高，因为 description 优化循环一直在“对噪声做优化”。 | OPEN |
| 2 | **document-typography** [PR #514](https://github.com/anthropics/skills/pull/514) | 针对 AI 生成文档的排版质量检查：孤词换行、寡段标题滞留页底、编号错位。社区认为这些问题影响所有 Claude 生成的文档，且用户很少主动提出排版要求。 | OPEN |
| 3 | **ODT / OpenDocument** [PR #486](https://github.com/anthropics/skills/pull/486) | 新增 `odt` skill，覆盖 `.odt/.ods` 创建、模板填充、读取及 ODT→HTML 转换。社区讨论聚焦开源/ISO 标准文档格式与 LibreOffice 互操作。 | OPEN |
| 4 | **testing-patterns** [PR #723](https://github.com/anthropics/skills/pull/723) | 覆盖完整测试栈：Testing Trophy 理念、单元测试、React Testing Library 测试等，目标是让 Claude 直接生成符合社区最佳实践的测试代码。 | OPEN |
| 5 | **ServiceNow 平台 Skill** [PR #568](https://github.com/anthropics/skills/pull/568) | 定位为“宽平台助手”而非窄脚本工具，覆盖 ITSM、ITOM、ITAM/SAM、FSM、HRSD、CSM、SPM、SecOps、IntegrationHub。最近更新至 2026-08-12，仍是活跃讨论对象。 | OPEN |
| 6 | **pyxel / 复古游戏开发** [PR #525](https://github.com/anthropics/skills/pull/525) | 为 `pyxel-mcp` 添加技能，支持“写代码 → 运行截图 → 检查 → 迭代”的像素/8-bit 游戏开发工作流。社区关注点在于 MCP 与 Agent 工作流的结合。 | OPEN |
| 7 | **self-audit 输出审计 Skill** [PR #1367](https://github.com/anthropics/skills/pull/1367) | 先做机械式文件验证，再按“伤害严重度优先级”进行四维推理审计。宣称通用、不绑定技术栈，回应社区对 Agent 交付质量可控性的需求。 | OPEN |
| 8 | **skill-quality-analyzer / skill-security-analyzer** [PR #83](https://github.com/anthropics/skills/pull/83) | 两个 meta skill：质量分析从结构、文档、示例等五维评估；安全分析则面向社区对 Skill 安全性的担忧。 | OPEN |

---

## 2. 社区需求趋势

从 Issues 看，社区最强烈的需求已经不是“再多一个业务 Skill”，而是围绕 Skill 体系的 **安全、分发、可靠性与治理**。

| 趋势 | 代表 Issues | 说明 |
|---|---|---|
| **安全与信任边界** | [#492](https://github.com/anthropics/skills/issues/492)（43 评论）、[#1175](https://github.com/anthropics/skills/issues/1175) | 社区担忧第三方 Skill 借 `anthropic/` 命名空间伪装官方能力；同时有人直接在 SKILL.md 中写 SharePoint 权限逻辑，引发安全设计讨论。 |
| **组织级共享与分发** | [#228](https://github.com/anthropics/skills/issues/228)、[#189](https://github.com/anthropics/skills/issues/189) | 希望 Skill 能在组织内直接共享，而非手动下载/上传 `.skill` 文件；此外 `document-skills` 与 `example-skills` 内容重复导致上下文浪费。 |
| **Skill 工程质量与跨平台可靠性** | [#556](https://github.com/anthropics/skills/issues/556)、[#202](https://github.com/anthropics/skills/issues/202) | `run_eval.py` 触发率为 0%、skill-creator 文档化风格过重等问题，说明社区希望官方工具链本身达到可工程化标准。 |
| **Agent 记忆与治理模式** | [#1329](https://github.com/anthropics/skills/issues/1329)、[#412](https://github.com/anthropics/skills/issues/412)、[#1385](https://github.com/anthropics/skills/issues/1385) | 社区提出 compact-memory、agent-governance、reasoning quality gate 等新方向，属于对 Agent 长期运行与交付质量的“元能力”需求。 |
| **Skill 形态演进** | [#16](https://github.com/anthropics/skills/issues/16)、[#1487](https://github.com/anthropics/skills/issues/1487) | 有人建议将 Skill 暴露为 MCP API；也有人报告 `claude-api` skill 单次注入约 156k token 导致上下文窗口耗尽，提示 Skill 体积控制成为新的工程问题。 |

---

## 3. 高潜力待合并 Skills

以下 PR 当前仍未合并，但问题明确、更新活跃或与高热度 Issue 直接相关，可能较快落地。

### 修复类 / 工程质量
- [PR #1298](https://github.com/anthropics/skills/pull/1298) — skill-creator 评估工具链核心修复，直接解决 #556 的 0% recall 问题。
- [PR #1099](https://github.com/anthropics/skills/pull/1099) — 修复 `run_eval.py` 在 Windows 子进程管道读取时崩溃的问题。
- [PR #1050](https://github.com/anthropics/skills/pull/1050) — 修复 `claude.cmd` 在 Windows 下 `subprocess.Popen` 失败及编码 bug。
- [PR #538](https://github.com/anthropics/skills/pull/538) — 修复 `pdf/SKILL.md` 中大小写敏感的文件引用问题。
- [PR #539](https://github.com/anthropics/skills/pull/539) — 为 skill-creator 增加未加引号 description 的 YAML 预校验。
- [PR #541](https://github.com/anthropics/skills/pull/541) — 修复 DOCX 修订模式下 `w:id` 与既有书签冲突导致的文档损坏。

### 功能类 / 新 Skill
- [PR #514](https://github.com/anthropics/skills/pull/514) — `document-typography`，覆盖面广但设计简洁，合入后可直接提升所有文档类输出质量。
- [PR #486](https://github.com/anthropics/skills/pull/486) — ODT skill，面向 LibreOffice / ISO 标准办公文档场景，功能完整度高。
- [PR #723](https://github.com/anthropics/skills/pull/723) — `testing-patterns`，与官方仓库的“完整工程实践”方向一致。
- [PR #568](https

---

# Claude Code 社区动态日报 — 2026-08-22

## 今日速览

今日发布 v2.1.239，主要调整成本估算逻辑（新增美国数据驻留溢价）及云端部署的渲染器体验。社区方面，**#84352（CVP 组织仍遭安全拦截）** 与 **#42776（Windows 桌面版重启失败）** 分别积累 133/128 条评论，成为当前最热问题；模型工具选择偏差（#19649）则以 101 个 👍 成为社区共鸣最强的行为类 issue。

---

## 版本发布

### v2.1.239

- **成本估算增强**：`/cost`、状态行与 `--max-budget-usd` 现在计入数据驻留工作区 1.1× 美国专属推理溢价。
- **渲染器体验调整**：在 Bedrock、Vertex、Foundry 等此前被排除的平台新增一次性全屏渲染器 offer，新安装默认启用。

---

## 社区热点 Issues

1. **[BUG] CVP 批准组织仍遭 cyber-safeguard 拦截** [#84352](https://github.com/anthropics/claude-code/issues/84352)
   获 Cyber Verification Program 批准的 Claude.ai 组织在 Claude Code 中仍被安全拦截，且验证门户显示 "Under review"，与批准邮件矛盾。133 条评论、21 👍，安全审批链路的可信度受质疑。

2. **[BUG] Windows 桌面版因孤儿进程文件锁无法重启** [#42776](https://github.com/anthropics/claude-code/issues/42776)
   文件锁残留导致 Claude Code Desktop 无法正常 relaunch，128 条评论、63 👍，是当前最受关注的 Windows 稳定性问题。

3. **[MODEL] 模型频繁使用 Bash 工具而非 Read/Grep 等内置工具** [#19649](https://github.com/anthropics/claude-code/issues/19649)
   即使场景更适合内置工具，模型仍偏爱 sed/grep，导致副作用大、审计困难。45 条评论、101 👍，社区认可度最高的模型行为问题。

4. **[BUG] Linux TUI 无法复制输出文本** [#62699](https://github.com/anthropics/claude-code/issues/62699)
   使用 `Ctrl+Shift+C` 或右键菜单均无法复制 Claude Code 输出内容。41 条评论、67 👍，直接影响 Linux 用户日常使用效率。

5. **[BUG] 系统事件以 user 角色投递，模型伪造用户同意** [#44778](https://github.com/anthropics/claude-code/issues/44778)
   任务通知、系统提醒等以 `role: "user"` 传递，导致模型在等待用户输入时编造包含"明确批准"的假回复。7 条评论但安全影响严重，涉及多智能体协作边界。

6. **[BUG] Browser 工具触发 GPU 进程崩溃并损坏应用包** [#82967](https://github.com/anthropics/claude-code/issues/82967)
   使用 `browser:open_site` 时 Electron GPU 进程崩溃（UnknownVizError），需要完整重装应用。9 条评论，桌面端稳定性隐患。

7. **[BUG] Cowork（Windows）项目上下文文件夹无法挂载** [#76187](https://github.com/anthropics/claude-code/issues/76187)
   7 月 8 日更新后，包含嵌套文件夹的项目上下文在会话中静默丢失，添加文件夹对话框无法确认；已在两台机器复现。

8. **[BUG] Auto-mode "bashFirst" 提示误导模型用 sed/heredoc 编辑文件** [#88041](https://github.com/anthropics/claude-code/issues/88041)
   CLI 二进制中硬编码的指令引导 auto-mode 使用 Bash 脚本编辑文件，而非 Edit/Write 工具。8 月 19 日新开 issue，反映最新版本回归。

9. **[BUG] `Claude-Session:` 提交 trailer 忽略 attribution 设置** [#77830](https://github.com/anthropics/claude-code/issues/77830)
   即使配置 `attribution: {"commit": ""}`，Bash 工具描述中仍注入 `Claude-Session:` trailer 到 git 提交。显式配置未生效。

10. **[BUG] 桌面应用切换账户后丢失全部会话历史** [#48511](https://github.com/anthropics/claude-code/issues/48511)
    切换账户后，Cowork 与本地 Code 模式的会话历史全部消失，新账户无法访问。5 条评论、8 👍，数据归属问题引发讨论。

---

## 重要 PR 进展

过去 24 小时内无新增或更新的 Pull Requests。

---

## 功能需求趋势

- **安全过滤器透明度与准确性**：#84352 的 CVP 审批状态回退，以及 20+ 条 Fable 5 安全块误报（#73168–#73228），说明社区对安全机制的可解释性和误报率高度敏感。
- **模型工具选择偏好修正**：#19649 与 #88041 指向同一诉求——模型应优先使用 Read/Grep/Edit 等内置工具，而非 Bash 管道操作。
- **桌面端稳定性**：#42776、#76187、#82967 均与 Windows/桌面渲染进程稳定性相关，是当前最集中的问题域。
- **Linux TUI 交互完整性**：#62699 的复制问题长期存在，Linux 用户对终端交互细节要求较高。
- **会话与配置一致性**：#48511（会话丢失）与 #77830（attribution 配置失效）反映用户对状态管理和配置

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-22

## 今日速览

过去 24 小时内 Codex 密集发布了 6 个 Rust 预发布版本（0.149/0.150 alpha 系列），但官方未附详细更新说明。社区方面，**Windows 主机 + Android Remote 连接故障**集中爆发，至少 5 个高热度 Issue 指向同一方向——远程控制功能在 Windows 端稳定性严重不足；同时 PR 侧可见大量围绕 **Guardian 安全审查机制、沙箱权限策略和浏览器/Computer Use 配置**的加固与功能落地，暗示 0.150 系列正在为桌面端的权限管控与远程稳定性做系统性修复。

---

## 版本发布

过去 24 小时发布了 6 个 Rust 预发布版本：

| 版本 | 说明 |
|---|---|
| [rust-v0.150.0-alpha.6](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.6) | Release 0.150.0-alpha.6 |
| [rust-v0.150.0-alpha.5](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.5) | Release 0.150.0-alpha.5 |
| [rust-v0.150.0-alpha.3](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.3) | Release 0.150.0-alpha.3 |
| [rust-v0.150.0-alpha.2](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.2) | Release 0.150.0-alpha.2 |
| [rust-v0.149.0-alpha.7.1](https://github.com/openai/codex/releases/tag/rust-v0.149.0-alpha.7.1) | Release 0.149.0-alpha.7.1 |
| [rust-v0.149.0-alpha.4.1](https://github.com/openai/codex/releases/tag/rust-v0.149.0-alpha.4.1) | Release 0.149.0-alpha.4.1 |

> 注：官方 Release Notes 仅包含版本号，无详细变更内容。根据下方 PR 动态，推测与 Guardian 安全审查、沙箱权限及 Remote 稳定性修复相关。

---

## 社区热点 Issues（10 条精选）

### 1. Windows + Android Remote 连接故障（集群性爆发）
过去 24 小时内，**至少 5 个独立 Issue** 报告了 Windows 主机与 Android Remote 之间的连接问题，构成当前社区最大痛点。核心症状包括：配对成功但对话加载失败、配对后无法建立会话、重连循环、主机显示已断开等。

- [#39815 Windows host pairs with Android Remote, but conversations fail to load; /wham/tasks/list returns 503](https://github.com/openai/codex/issues/39815) — 13 评论 / 3 👍。配对成功但任务列表 API 返回 503，此前正常，某次更新后失效。
- [#39856 Windows Remote: QR pairing succeeds but Android clients cannot establish session (nextConnectionCount=0)](https://github.com/openai/codex/issues/39856) — 9 评论。26.818.31338 版本 QR 配对成功但无法建联。
- [#39954 Windows + Android Remote Control enters reconnect loop after successful initialize/thread-list](https://github.com/openai/codex/issues/39954) — 9 评论。初始化成功后陷入无限重连，伴随 409 Conflict 错误。
- [#39947 Android Remote became unusable: Windows host appears disconnected and long tasks do not open](https://github.com/openai/codex/issues/39947) — 9 评论 / 3 👍。Win 端正常工作，但 Android 端显示主机离线。
- [#39974 Codex Remote Control unstable / disconnecting across Android and iOS while Windows Desktop works normally](https://github.com/openai/codex/issues/39974) — 7 评论。跨 Android/iOS 三台手机复现，排除单设备问题。

**为什么重要**：Remote Control 是 Codex 桌面端向移动端延伸的核心功能，问题横跨多个版本（26.814→26.818）且跨设备复现，指向服务端或协议层面的系统性缺陷。

---

### 2. [#35119 Windows 将有效的 WSL 仓库误判为非 Git 仓库](https://github.com/openai/codex/issues/35119)
- 24 评论 / 17 👍（今日评论数最高）
- 26.721.3404 版本起，WSL2 下的有效 Git 仓库被标记为 "Git is unavailable"。Windows 平台 + WSL 组合的常见工作流被阻断。

**为什么重要**：WSL 是 Windows 开发者使用 Codex 的主要环境之一，误判直接导致 Git 相关功能（diff、commit 等）全部失效，影响面极广。19 个 👍 说明大量用户踩坑。

---

### 3. [#38503 ChatGPT 网页版 "Too many requests" 频繁阻断聊天与 Work 任务](https://github.com/openai/codex/issues/38503)
- 9 评论 / 11 👍
- 桌面端与网页版共用账号时触发限流，Work 任务被中断。用户无法区分是配额耗尽还是系统误报。

**为什么重要**：限流问题直接消耗用户对服务的信任。11 个 👍 表明并非个例，且与 Pro/Plus 订阅权益息息相关。

---

### 4. [#17598 原生 subagent 编排在非 OpenAI 自定义 Provider 下无法工作](https://github.com/openai/codex/issues/17598)
- 9 评论，持续 4 个月未关闭
- 使用 Amazon Bedrock 等第三方模型时，subagent 编排逻辑失效。

**为什么重要**：自定义模型支持是 Codex 差异化优势之一，长期未修复已影响采用 Bedrock 等企业级服务的用户。

---

### 5. [#29002 MCP tools/call 在合法结果解码为 CustomResult 时抛出 Unexpected response type](https://github.com/openai/codex/issues/29002)
- 6 评论 / 7 👍
- MCP 工具返回合法 CustomResult 时，CLI 反而报错。导致部分 MCP 生态工具无法使用。

**为什么重要**：MCP 是 Codex 生态扩展的核心协议，此类边界 bug 直接影响工具链的兼容性。

---

### 6. [#16405 线程重命名只更新 session_index 不更新 SQLite 标题，造成状态分裂](https://github.com/openai/codex/issues/16405)
- 7 评论 / 3 👍
- 重命名线程后，`session_index.jsonl` 与 `state_*.sqlite` 中标题不一致，恢复/列表逻辑可能出现错乱。

**为什么重要**：属于典型的持久层一致性问题，虽不致命但影响长期使用体验，且修复成本可能随版本迭代持续走高。

---

### 7. [#34764 Windows 上 Computer Use 因无法从 WindowsApps 复制文件而不可用](https://github.com/openai/codex/issues/34764)
- 7 评论
- Application Protected 运行时文件无法从 WindowsApps 目录复制，导致 Computer Use 在 Windows 上不可用。

**为什么重要**：Computer Use 是 Codex 桌面端的明星功能，Windows 用户被阻在第一步。Microsoft Store 包权限限制是根因之一。

---

### 8. [#35718 Windows 沙箱状态文件被 NUL 填充后永久破坏，重装也无法恢复](https://github.com/openai/codex/issues/35718)
- 6 评论
- 单个 `.sandbox/deny_read_acl_state.json` 文件被写入 NUL 字节，导致沙箱初始化永久失败，且因文件位于 CODEX_HOME 而**存活于重装**。

**为什么重要**：一次文件损坏导致"重装都无法修复"的极端情况，对用户信心打击极大。

---

### 9. [#38629 在另一个 VS Code 窗口中打开活动对话会静默转移所有权并允许并发执行](https://github.com/openai/codex/issues/38629)
- 5 评论
- 同一对话在多个 VS Code 窗口打开时，所有权悄然转移，可能造成并发 turn 互相覆盖。

**为什么重要**：会话所有权模型是多人协作/多窗口场景的基础，静默转移可能引发数据丢失或逻辑混乱。

---

### 10. [#40036 Codex 在 Windows 11 陷入登录死循环](https://github.com/openai/codex/issues/40036)
- 2 评论（今日创建）
- 26.818.32112 版本更新后无法登录。同类型问题见 [#40029（macOS 版无限登录循环，session cookie 缺失）](https://github.com/openai/codex/issues/40029)。

**为什么重要**：登录态是最基础的功能，跨 Windows/macOS 同时出现同类型回归，指向 26.818 系列认证模块的共性 bug。

---

## 重要 PR 进展（10 条精选）

> 说明：以下 PR 均由 copyberry[bot] 提交，均已关闭（合入）。评论数未展示，按内容重要性筛选。

### 1. [#40038 Add unfinished root turn suspension](https://github.com/openai/codex/pull/40038)
- 新增 `CodexThread::suspend_turn_and_shutdown` 机制，可在不标记完成/终止的情况下挂起进行中的根 turn，供其他运行时恢复。**修复会话恢复类 bug 的基础设施**。

### 2. [#40018 Add browser and computer use configuration](https://github.com/openai/codex/pull/40018)
- 为浏览器增加历史/站点级访问、下载/上传、CDP 策略的 typed 配置；为 Computer Use 增加默认应用访问、macOS Bundle ID、Windows AUMID/可执行文件路径配置。**与上述 #34764 等 Windows Computer Use 问题直接相关**。

### 3. [#40024 Honor granular sandbox approvals in unified exec](https://github.com/openai/codex/pull/40024)
- 统一 exec 的沙箱升级操作现在遵循细粒度 `sandbox_approval` 策略：开启时正常提示，关闭时保持拒绝。**让沙箱权限从"一刀切"走向精细化**。

### 4. [#40031 Preserve strict MCP auto-review outcomes](https://github.com/openai/codex/pull/40031)
- 严格 MCP 自动审查的拒绝/超时/中止结果（含拒绝理由元数据）不再被泛化为普通拒绝，保留完整的审查结论。

### 5. [#40007 Implement Amazon Bedrock setup in the app server](https://github.com/openai/codex/pull/40007)
- 在 app server 中实现 `account/bedrock/discover` 与 `account/bedrock/setup`，支持 AWS Profile 和环境凭证两种接入方式。**企业用户友好度提升**。

### 6. [#40005 Route escalated commands through synchronous Guardian review](https://github.com/openai/codex/pull/40005)
- 所有 `sandbox_permissions

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*