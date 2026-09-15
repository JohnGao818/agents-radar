# AI CLI 工具社区动态日报 2026-09-15

> 生成时间: 2026-09-15 03:09 UTC | 覆盖工具: 2 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI CLI 工具社区动态横向对比分析报告  
**样本：Claude Code vs OpenAI Codex · 2026-09-15**

> 说明：本轮摘要未披露两个仓库的 Issue/PR 总数，以下“数据”均基于摘要中可见的热点条目与发布记录统计。

---

## 1. 生态全景

当前 AI CLI 工具正从“能用”进入“可扩展、可治理、可生产化”阶段。Claude Code 与 OpenAI Codex 的社区焦点已不只是模型能力，而是 hooks/插件体系、成本控制、Windows 稳定性、MCP 集成与自动化可靠性。Claude Code 的社区讨论更聚焦插件化路线与成本治理，官方已对 function hooks 给出交付预期；Codex 则处于 0.155.0 alpha 高频迭代期，底层工程重构密集，但 Windows 桌面稳定性与第三方 provider 兼容性问题集中暴露。整体看，Agent 平台的竞争点正在从“谁更强”转向“谁更可管、更可靠、更容易接入”。

---

## 2. 各工具活跃度对比

| 工具 | 今日 Issues 情况（摘要可见） | PR 更新 | Release 情况 |
|---|---|---|---|
| **Claude Code** | Top 10 热点 + 3 条补充关注；最高 #91870：174 评论 / 105 👍；#92984：113 评论 / 58 👍 | **3 条**：1 个 Mods diff 已关闭、1 个沙箱文档待合并、1 个 pylint CI 已关闭 | **2 个稳定版本**：v2.1.272 仅修复；v2.1.271 支持 Remote 会话 fast mode、全屏 `/config` 鼠标操作 |
| **OpenAI Codex** | 10+ 条热点；最高 #44781：31 评论 / 37 👍；#43410：29 评论 / 17 👍；schema 兼容问题形成系列 | 摘要称“集中落地一批底层 PR”：daemon 与 CLI 解耦、附件 API、Windows 沙箱、Unix socket 权限等，未给具体数量 | **4 个预发布 tag**：`rust-v0.155.0-alpha.2.4` 至 `alpha.6`，无变更说明；稳定版仍为 0.153.4 / 0.154.0 |

**结论**：Claude Code 讨论深度与社区互动更强，单 Issue 声量显著更高；Codex 发布节奏更快，但 alpha 说明缺失，社区问题更多集中在稳定版集成与平台故障。

---

## 3. 共同关注的功能方向

| 方向 | Claude Code | OpenAI Codex | 共同诉求 |
|---|---|---|---|
| **Hooks / 插件扩展与安全边界** | #91870 Mods/function hooks 主导讨论；#92533 hooks 破坏 worktree 隔离；#94424 需要用量事件 | #27833 `PreToolUse` deny 对 `apply_patch` 不生效，安全策略形同虚设 | 可扩展，但 hook 决策必须强制执行；事件模型需覆盖用量、权限、隔离 |
| **Windows 平台稳定性** | KB5124008 导致 Plan9 挂载失败；本地 MCP、Bash 转义、IME 候选窗遮挡 | app-server 队列消息错误、浏览器控制 API-key 不可用、WMI 轮询延迟、`cua_node` EPERM 死循环占 59 GB | 系统更新兼容、认证路径全覆盖、无死循环重试、资源不泄漏 |
| **成本 / 用量 / 容量治理** | Opus 5 xhigh 档 token 涨 2–7 倍；请求运行时熔断、分源归因、per-call effort | 模型频繁报 `Selected model is at capacity`；自动化注入缺 `call_id` 永久破坏会话 | 硬止损、分源账单、容量退避、按调用调整推理算力 |
| **MCP / 第三方工具集成** | 本地 MCP 就绪检测、沙箱网络批准作用域不清 | MCP server 启动失败；严格 provider 拒绝 `oneOf` schema、空 schema 工具 | 兼容性、schema 严格合规、认证与沙箱语义清晰 |
| **会话 / 自动化可靠性** | 自归档静默无效、跨设备续接无提示、长会话 400 不可恢复 | queued follow-up 竞态、Automations 缺 `call_id` 导致永久 400 | 状态一致性、幂等、自愈或降级路径 |
| **沙箱 / 权限 / 隔离** | seccomp 间歇失败、worktree 隔离与 hooks 耦合、权限模式指示符 | PreToolUse deny 失效、Windows 沙箱注册机制 | 安全策略必须生效，作用域和失败行为要明确 |

---

## 4. 差异化定位分析

**Claude Code：CLI/T

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

⚠️ Skills 摘要生成失败。

---

# Claude Code 社区动态日报 · 2026-09-15

> 数据来源：github.com/anthropics/claude-code
> 说明：过去 24 小时内 PR 侧仅有 3 条更新记录，故 PR 部分按实际数据完整列出，不做凑数。

---

## 一、今日速览

社区讨论继续被 **#91870「Mods — make Claude 10x more extensible」** 主导（174 评论 / 105 👍），官方在该帖中承诺 function hooks 将在"数周内"落地，围绕它的周边需求（用量事件、隔离兼容）已开始成批出现。与此同时，**Windows 平台问题集中爆发**：Cowork 的 Plan9 共享挂载因系统更新 KB5124008 全面失效（113 评论），本地 MCP、Bash 反斜杠转义等多条 Windows 缺陷仍在活跃。**成本治理**成为第二大声量主线，从 Opus 5 的 token 异常放大到运行时消费熔断请求，触及真实账单。

---

## 二、版本发布

**v2.1.272**
- 仅包含 Bug 修复与可靠性改进，无功能变更。

**v2.1.271**
- **Remote 会话支持 fast mode**：云端与自托管 runner 均可用，主机侧 fast-mode 设置或会话内输入 `/fast` 生效（受组织策略限制）。
- **全屏模式 `/config` 面板支持鼠标操作**：滚轮可直接滚动设置项。

> 发布节奏平稳，功能增量集中在 Remote 体验与 TUI 交互，与社区近期对 TUI/终端体验的反馈方向一致。

---

## 三、社区热点 Issues（Top 10）

1. **#91870 [OPEN] Mods — make Claude 10x more extensible** · 174 评论 / 105 👍
   本周绝对焦点。帖内发布 Community Update，官方表示已"以周而非天为单位"承诺交付 function hooks，且承认社区高信号反馈已实质影响设计。这是 Claude Code 插件化路线的方向标。
   https://github.com/anthropics/claude-code/issues/91870

2. **#92984 [OPEN] Cowork (Windows)：KB5124008 后所有 Plan9 共享挂载失败** · 113 评论 / 58 👍
   报错 `Plan9 mount failed: invalid argument`，卸载该 Windows 更新即恢复。已定位到外部系统更新与 Cowork 虚拟化层的冲突，属于硬阻塞级平台问题，企业用户受影响面大。
   https://github.com/anthropics/claude-code/issues/92984

3. **#93596 [OPEN] Opus 5 在 xhigh 档位几乎 100% 触发 thinking，输出 token 涨 2–7 倍** · 3 评论
   自 9-11 01:30 UTC 起复现，模型、effort、设置均未变更。客户端无感知的成本突增，是当前最实际的经济性风险点。
   https://github.com/anthropics/claude-code/issues/93596

4. **#85422 [OPEN] Token-burn 熔断器：带来源归因的运行时消费上限** · 15 评论
   要求对 hooks / plugins / subagents 分源统计并**强制**止损，而不仅是警告。虽然 👍 为 0，但切中"没有任何机制能阻止失控消耗"的结构性空白。
   https://github.com/anthropics/claude-code/issues/85422

5. **#92533 [OPEN] function-hook 的 tool.call 挂到 Bash 即破坏 Agent worktree 隔离** · 1 评论
   启用 `CLAUDE_CODE_ENABLE_FUNCTION_HOOKS=1` 后，带 `isolation: "worktree"` 的子代理**所有** Bash 调用（含 `pwd`、`true`）都被拒："isolation context lost"。属 Mods 生态早期必经的机制冲突，值得提前关注。
   https://github.com/anthropics/claude-code/issues/92533

6. **#94424 [OPEN] Function hooks：需要会话用量 / 速率窗口变更事件** · 9-15 新提
   作者在做 context 填充度、5h/7d 计划窗口倒计时与逐轮成本账本，但只能靠轮询 `$.session.usage()`。反映 hooks 事件模型正在向"可观测性"方向细化。
   https://github.com/anthropics/claude-code/issues/94424

7. **#93782 [OPEN] 2.1.269 回归：VS Code 集成终端（WSL2）听写工具粘贴失效** · 7 评论
   剪贴板 + 模拟 Ctrl+V 的输入不再进入 prompt，2.1.268 正常。回归窗口明确、复现路径清晰，是典型的版本回退类修复优先项。
   https://github.com/anthropics/claude-code/issues/93782

8. **#86928 [OPEN] 沙箱 Bash 间歇失败：`unshare(CLONE_NEWUSER): Invalid argument`** · 16 评论
   `sandbox.enabled: true` 下约 **1/10** 的 Bash 调用直接失败，同命令重试可过。间歇性导致难以稳定复现，但已标记 reproduced。
   https://github.com/anthropics/claude-code/issues/86928

9. **#77298 [OPEN] 为 Agent (Task) 工具增加 per-call effort 参数** · 4 评论 / 13 👍
   目前 model 可逐调用覆盖，effort 却必须预先写死 agent 定义文件。与成本治理主线叠加，是"按需投放推理算力"的关键缺口。
   https://github.com/anthropics/claude-code/issues/77298

10. **#44933 [OPEN] Cowork：设置默认项目文件夹，会话启动时自动加载** · 9 评论 / 20 👍
    4 月提出、至今持续活跃的长期高赞需求，反映桌面端多项目工作流的日常摩擦。
    https://github.com/anthropics/claude-code/issues/44933

**值得补充关注**：#90004（条件 `paths:` skills 在 auto 模式下永远无法激活——触发只挂在 Read/Edit/Write，而 bashFirst 又叫模型别用它们）、#94418（计划任务调用 `archive_session("self")` 静默无效）、#85021（权限模式指示符用 U+23F5，常见等宽字体缺字形渲染成豆腐块，同类问题半年来第 5 次被提）。

---

## 四、重要 PR 进展

> 过去 24 小时仅 3 条 PR 更新，以下为全部内容。

1. **#94184 [CLOSED] `mods/diff`：固定表头 + 仅正文滚动** · 作者 poteat
   使 docked 面板与内置 `/diff` 逐帧对齐：表头、base 行与 8 行文件列表保持固定，滚轮以 3 行/格滚动 hunks；指针悬停溢出列表时按文件滚动；`ctrl/opt+↑↓` 与 `ctrl+x b` 可从 prompt 直接生效。与 #91870 的 Mods 提案同源，展示社区自建扩展已达内置体验水准。
   https://github.com/anthropics/claude-code/pull/94184

2. **#71627 [OPEN] docs(sandbox)：补充说明"提示期批准的 host 为会话级"** · 作者 mahirhir
   在 `examples/settings/README.md` 的 Tips 增加一条：经 prompt 批准的网络域名仅当前会话有效，恢复会话后需重新批准。6 月提交至今仍未合并，但恰好回应了大量沙箱网络困惑。
   https://github.com/anthropics/claude-code/pull/71627

3. **#83890 [CLOSED] 新增 pylint.yml** · 作者 KrypticKode007
   仓库 CI 静态检查配置，已关闭。
   https://github.com/anthropics/claude-code/pull/83890

---

## 五、功能需求趋势

1. **可扩展性 / 插件化（最强主线）**：Mods、function hooks、插件作用域设计占据最高声量与最高赞。官方已给出交付时间承诺，社区正在从"要不要 hooks"转向"hooks 应有哪些事件"。
2. **成本与用量治理**：运行时消费熔断、per-source 归因、用量变更事件、per-call effort、异常 token 放大排查——正在从零散诉求汇聚成一条产品线。
3. **Windows 平台健壮性**：系统更新兼容（Plan9）、本地 MCP 就绪检测、Bash 反斜杠吞噬、IME 候选窗遮挡、MSIX 打包限制等，是当前缺陷密度最高的平台。
4. **IDE 集成打磨**：VS Code 扩展的会话删除、diff 双开、`initialPermissionMode` 在更新后静默失效、终端粘贴回归。
5. **会话生命周期与跨设备续接**：自归档失效、跨设备续接在源机器执行且无提示、恢复会话连接卡死。
6. **沙箱与隔离**：seccomp 间歇失败、hooks 与 worktree 隔离的耦合冲突、后台任务被内存压力回收器批量误杀。
7. **终端渲染与可访问性**：字形兼容（U+23F5 → U+25B6）、鼠标支持、全屏面板交互。

---

## 六、开发者关注点

- **回归比新功能更痛**：2.1.269 的粘贴回归、扩展更新后权限模式被重置（#85077），都属于"静默改变既有行为"，比功能缺失更侵蚀信任。
- **长会话脆弱性**：二进制工具输出导致会话陷入永久 `400 unexpected end of data`（#94408，含 fork 也无法恢复），缺乏会话自愈或降级路径。
- **失败静默**：自归档无报错、权限模式变 undefined、跨设备执行无提示——开发者反复强调"宁可报错也不要无声失败"。
- **资源回收策略争议**：Linux 上以 MemFree 而非 MemAvailable/PSI 判定内存压力，导致 39 GB 可用时仍批量杀死后台任务（#78674）。
- **配置语义不清**：沙箱网络批准的作用域（会话级）、条件 skills 的触发机制与 bashFirst 策略相互矛盾（#90004），文档与实现之间存在解释成本。
- **成本可预期性缺口**：没有硬性止损、没有分源账单、effort 不可逐调用调整——在 agent 自主性提高的同时，开发者希望保有"刹车"。

---

*日报生成时间：2026-09-15 ·

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-09-15

数据来源：[github.com/openai/codex](https://github.com/openai/codex)

---

## 一、今日速览

1. 0.155.0 系列 alpha 版本在 24 小时内密集迭代到 `alpha.6`，主线仍在快速推进，但 release 说明极简，无公开变更明细。
2. 社区讨论高度集中在 **Windows 桌面端稳定性**（app-server 队列、浏览器控制、WMI 轮询、cua_node 文件系统异常）与 **自定义 OpenAI 兼容 provider 的 schema 严格性问题**（DeepSeek 相关 Issue 已形成系列）。
3. PR 侧集中落地一批底层工程改造：daemon 包与 CLI 解耦、附件上传/解析 API、Windows 沙箱注册机制、Unix socket 权限修复——多为基础设施级铺垫。

---

## 二、版本发布

过去 24 小时共 4 个 tag，**全部为 `rust-v0.155.0-alpha.*` 预发布版本**，release note 仅包含版本号本身，无可读变更说明：

| 版本 | 链接 |
| --- | --- |
| rust-v0.155.0-alpha.6 | [release](https://github.com/openai/codex/releases) |
| rust-v0.155.0-alpha.5 | [release](https://github.com/openai/codex/releases) |
| rust-v0.155.0-alpha.4 | [release](https://github.com/openai/codex/releases) |
| rust-v0.155.0-alpha.2.4 | [release](https://github.com/openai/codex/releases) |

> 观察：一天内连续 4 个 alpha 且跨 `.2.4` / `.4` / `.5` / `.6` 等非连续编号，说明 0.155.0 正处于高频内部验证阶段。当前用户侧稳定版仍为 0.153.4 / 0.154.0，社区反馈的多数问题均基于这两个稳定版。

---

## 三、社区热点 Issues

### 1. [Windows] 编辑并重发队列消息触发 app-server 错误 — 本日最热
[#44781](https://github.com/openai/codex/issues/44781) · 31 评论 · 👍 37 · OPEN

Codex Desktop Windows 包 `26.903.9818.0`，内嵌 codex-cli 0.153.4。用户编辑一条已排队的 follow-up 消息并重发时，提示 `App-server queued follow-up no longer exists`。**这是今日评论数与点赞数双高的 Issue**，说明 queued follow-up 的消息生命周期管理存在真实竞态，且 37 个 👍 表明影响面不小。

### 2. [Windows] 浏览器控制在 API-key 认证下完全不可用
[#43410](https://github.com/openai/codex/issues/43410) · 29 评论 · 👍 17 · OPEN

Edge 插件与 native host 均连接成功，但首次浏览器操作即报 `unsupported Codex auth method: apikey`。**这是一个认证路径覆盖不全的实现缺口**：ChatGPT 订阅登录可用、API key 登录不可用。issue 已持续一周多仍在更新，属于跨模块（auth + browser + app-server）的硬骨头。

### 3. GPT-6 Astra 在 CLI 上连 `hi` 都被拒绝
[#43237](https://github.com/openai/codex/issues/43237) · 14 评论 · OPEN

Linux/macOS 上用 ChatGPT 订阅登录的 CLI 0.153.4，向 `gpt-6-astra` 发送 `hi` 返回 `invalid_prompt`，作者提供了 CLI 与最小后端复现。**模型侧 prompt 校验与 CLI 请求构造之间的不匹配**，直接影响新模型的可用性，值得官方优先定位。

### 4. macOS CLI 0.154.0 实验能力破坏 Messages / Computer History MCP 启动
[#44458](https://github.com/openai/codex/issues/44458) · 12 评论 · 👍 5 · OPEN

Homebrew 安装的 0.154.0，ChatGPT Pro 20x，两个 MCP server 在启动阶段双双失败。**实验性开关默认打开导致既有 MCP 集成回归**，是典型的"新功能破坏老能力"问题，也提示 MCP 生态对 CLI 版本升级比较敏感。

### 5. [Windows] Powershell/WMI 全量轮询造成全局输入延迟（已关闭）
[#36176](https://github.com/openai/codex/issues/36176) · 13 评论 · 👍 5 · CLOSED

从 26.721 版本一路跟踪到 9 月，作者甚至本地打了 patch 验证原因，最终本日关闭。**这是本周少见的"长期性能问题收敛"信号**，对 Windows 桌面版用户是好消息，也说明进程/系统信息采集策略在重新设计。

### 6. Automations 注入缺失 `call_id` 的函数输出，永久破坏会话
[#44723](https://github.com/openai/codex/issues/44723) · 7 评论 · OPEN

Windows 桌面版 + 自定义 provider（DeepSeek，`wire_api = "responses"`）。heartbeat/cron 自动化触发时注入的 `function_call_output` 缺少 `call_id`，导致该 session 之后**每一轮**都返回 400 missing field call_id。**这是数据/状态一致性问题，一旦触发不可自愈**，对使用自动化的用户杀伤力很大。

### 7. PreToolUse hook 的 deny 对 `apply_patch` 不生效（安全边界失效）
[#27833](https://github.com/openai/codex/issues/27833) · 4 评论 · OPEN

项目级 `.codex/hooks.json` 注册的 `PreToolUse` hook 在 `apply_patch` 上确实被触发，但通过文档规定的两种渠道（exit code 2 + stderr，或 `permissionDecision` JSON）发出的 deny **均未阻止写入**。**hook 被触发但决策被忽略，等于安全策略形同虚设**，属于最高优先级类型的问题。

### 8. `automation_update` / `tool_search` schema 被严格 provider 全面拒绝（系列问题）
[#45585](https://github.com/openai/codex/issues/45585)（今日新增）· [#37786](https://github.com/openai/codex/issues/37786) · [#39848](https://github.com/openai/codex/issues/39848) · 均 OPEN

同一根因的多个报道：`automation_update` 使用根级 `oneOf` 而**缺少顶层 `"type": "object"`**，严格校验函数 schema 的 OpenAI 兼容服务会直接拒绝整个请求；`tool_search` 则暴露空 schema 的延迟工具，一旦被调用该线程后续所有轮次全部失败。OpenAI 自家 Responses 端点容忍这种写法，第三方不容忍。**这是一个"隐式依赖自家服务宽容度"的兼容性债**，已积累成跨 8 月的长尾系列。

### 9. Windows `cua_node` rename_staging EPERM 死循环，占用约 59 GB 并冻结 UI
[#42484](https://github.com/openai/codex/issues/42484) · 5 评论 · OPEN

Windows 11 Pro 25H2，桌面版 26.901.1978.0。文件重定位失败后无限重试，磁盘占用飙升至 ~59 GB 且桌面 UI 卡死。**这是资源泄漏 + 无退避重试的组合故障**，对用户机器有实际破坏性。

### 10. 模型容量错误频发：`Selected model is at capacity`
[#44395](https://github.com/openai/codex/issues/44395) · 9 评论 · [#44531](https://github.com/openai/codex/issues/44531) · 4 评论 · 均 OPEN

ChatGPT Pro (20x) 用户反馈模型频繁报容量

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*