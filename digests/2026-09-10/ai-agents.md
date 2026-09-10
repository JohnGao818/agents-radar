# OpenClaw 生态日报 2026-09-10

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-09-10 02:51 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 · 2026-09-10

---

## 1. 今日速览

OpenClaw 今日维持**极高活跃度**：过去 24 小时内 Issues 与 PR 各更新 500 条，其中 306 条 Issue 新开/活跃、194 条关闭，248 条 PR 待合并、252 条已合并/关闭，合并率约 50%，说明维护带宽基本能跟上提交流入速度。项目今日**未发布新版本**，但围绕 2026.9.x 系列的回归修复与原生端（iOS/macOS/Android）能力建设并行推进。Bug 侧呈现"更新链路 + 会话状态 + 沙箱/凭据边界"三大聚集区，多个 P0/P1 回归在今日获得关闭或进入修复审查。后台服务健康度仍是最大隐忧：僵尸进程泄漏、Gateway 事件循环阻塞、内存索引无界增长等长龄问题持续获得新证据。整体判断：**项目健康度良好但压力显著，更新/迁移可靠性是当前最集中的风险面**。

---

## 2. 版本发布

今日**无新版本发布**（最新 Releases 为空）。社区仍在围绕 `2026.9.1 / 2026.9.2 / 2026.9.3` 的升级问题展开讨论，建议关注后续补丁版本。

---

## 3. 项目进展

今日有 252 条 PR 合并/关闭，以下为**已关闭或高优先级**的关键推进：

**已关闭/合并**
- **#143561 [CLOSED]** `fix(channels): reject unknown accounts before removal` — 修复 `openclaw channels remove` 对未知账号误报成功、误写配置的问题。([链接](https://github.com/openclaw/openclaw/pull/143561))
- **#143626 [CLOSED]** `fix: retain copied engine registries through cleanup` — 避免复制插件上下文引擎在原始注册表退役后意外回退。([链接](https://github.com/openclaw/openclaw/pull/143626))
- **#143579 [CLOSED]** `fix(ui): expand dashboard directly from its side-panel tab` — 修复 Dashboard 侧栏展开后视图顺序错乱。([链接](https://github.com/openclaw/openclaw/pull/143579))

**待合并但已进入"可审查/自动合并"阶段（高确定性）**
- **#142626 [automerge armed]** `fix(imessage): restore feedback after bridge recovery` — iMessage 桥接恢复后重新获得输入指示与已读回执。([链接](https://github.com/openclaw/openclaw/pull/142626))
- **#143633** `fix: retain compaction services through issued work` — 修复取消/超时压缩时过早关闭 MCP/LSP 资源、钩子逃逸工作所有权的问题，直接对应多起会话状态类 Bug。([链接](https://github.com/openclaw/openclaw/pull/143633))
- **#142100** `fix: preserve exact model choices across reloads and fallbacks` — 修复模型在 reload/压缩/降级后静默漂移，替换 #134496。([链接](https://github.com/openclaw/openclaw/pull/142100))
- **#143501** `fix(sandbox): authorize canonical destinations before pinned fs mutations`（P0）— 封堵沙箱写权限绕过策略保护路径（如 `.git`）的越权变更。([链接](https://github.com/openclaw/openclaw/pull/143501))
- **#135838** `fix(workers): stop provisioning after turn authority closes` — 停止在 Gateway 授权失效后继续配置 worker。([链接](https://github.com/openclaw/openclaw/pull/135838))

**方向性推进（大尺寸特性 PR）**
- **#143587 / #143610 / #143615 / #143631** 组成 Draft Stack：Gateway 请求绑定选定 profile → iOS 会话操作 → macOS 会话操作 → iOS 语音动作绑定。原生端"选定会话"能力链路正在成形。([#143587](https://github.com/openclaw/openclaw/pull/143587) · [#143610](https://github.com/openclaw/openclaw/pull/143610) · [#143615](https://github.com/openclaw/openclaw/pull/143615) · [#143631](https://github.com/openclaw/openclaw/pull/143631))
- **#143588** `feat(models): align native sign-in and model runtime choices` — 统一原生登录与模型运行时选择，涉及兼容性与认证风险。([链接](https://github.com/openclaw/openclaw/pull/143588))
- **#140339** `feat(update): retain compatible package rollback and safe recovery admission` — 针对反复出现的"更新卡死/更新后无法启动"，构建可回滚的安全更新通道。([链接](https://github.com/openclaw/openclaw/pull/140339))
- **#132453** `feat(gateway): expose Codex usage per login` — 管理员可按登录账号查看 Codex 配额与余额。([链接](https://github.com/openclaw/openclaw/pull/132453))

**小结**：今日项目在**更新可靠性、压缩资源生命周期、沙箱/授权边界**三条主线上实质前进，原生端会话绑定栈进入评审轨道。

---

## 4. 社区热点

按评论数与反应数排序：

| 排名 | 条目 | 状态 | 评论 | 👍 | 核心诉求 |
|---|---|---|---|---|---|
| 1 | [#135111](https://github.com/openclaw/openclaw/issues/135111) 工具调用 JSON 参数畸形（claude-sonnet-5, v2026.8.1） | CLOSED | 26 | 0 | 升级后间歇性失败，非特定文件/工具，属 P1 回归 |
| 2 | [#97616](https://github.com/openclaw/openclaw/issues/97616) hook/tool 子进程未回收，僵尸堆积 | OPEN | 15 | 1 | 长时间运行后运行时性能退化 |
| 3 | [#119720](https://github.com/openclaw/openclaw/issues/119720) 同步持久化阻塞 Gateway 事件循环 | OPEN | 15 | 0 | 规模化场景下事件循环被 transcript 维护阻塞 |
| 4 | [#137927](https://github.com/openclaw/openclaw/issues/137927) 内部上下文块泄漏进 Telegram 可见文本 | CLOSED | 14 | 0 | 安全/会话状态，内部指令暴露给用户 |
| 5 | [#53628](https://github.com/openclaw/openclaw/issues/53628) 安装 skill 时 `${XDG_CONFIG_HOME}` 未解析 | OPEN | 14 | 1 | Docker 场景配置变量失效 |
| 6 | [#43367](https://github.com/openclaw/openclaw/issues/43367) 多智能体编排不稳定（并发覆盖 session-lock 失败） | OPEN | 14 | 1 | 并行 agent 生产可用性 |

**分析**：社区注意力高度集中在**"升级后回归"**与**"规模化运行退化"**两类问题上。#135111 的 26 条评论显示出对 provider 层 JSON 参数校验的高度关注；#97616 与 #119720 是同一主题的两个切面——**长驻进程的资源与调度健康度**，且都由资深用户提供了现场证据，具备较高修复价值。#137927 虽已关闭，但其"内部脚手架外泄到用户可见渠道"的模式与今日新开的 [#143278](https://github.com/openclaw/openclaw/issues/143278)（Heartbeat 内部输出泄漏到 Telegram）构成同一类风险，值得系统性排查。

---

## 5. Bug 与稳定性

### P0 / 发布阻断
| 条目 | 状态 | 说明 | Fix PR |
|---|---|---|---|
| [#137813](https://github.com/openclaw/openclaw/issues/137813) Windows Gateway 在 2026.9.1 后完全不启动（`--task-supervisor` 静默退出 0） | **CLOSED** | 计划任务方式安装的 Windows 用户被完全阻断 | 已关闭，需核对发布说明 |
| [#115642](https://github.com/openclaw/openclaw/issues/115642) 订阅制认证下计费冷却远超故障时长（~5h），无手动重置 | OPEN | 影响所有订阅用户，需探测式恢复 | ❌ 无 fix PR，标记 needs-product-decision |
| [#142585](https://github.com/openclaw/openclaw/issues/142585) 2026.9.3 Doctor 拒绝合法旧版工作区迁移/证明导入 | OPEN | 2026.7.1-2 → 2026.9.3 升级阻断 | ❌ 无，标记 needs-info |
| [#141617](https://github.com/openclaw/openclaw/issues/141617) 2026.9.2 npm 更新永久卡在 requested/running | **CLOSED** | 与 #139714 同源 | 已关闭 |
| [#143501](https://github.com/openclaw/openclaw/pull/143501) 沙箱越权写入策略保护路径 | PR OPEN | P0 安全边界 | ✅ PR 审查中 |

### P1
- [#97616](https://github.com/openclaw/openclaw/issues/97616) 僵尸进程堆积 / 运行时退化 — **无 fix PR**，`impact:crash-loop`
- [#119720](https://github.com/openclaw/openclaw/issues/119720) 同步持久化阻塞事件循环 — **无 fix PR**，需产品决策
- [#132762](https://github.com/openclaw/openclaw/issues/132762) overflow 重试以 toolResult 收尾、无最终交付 — ✅ 标记 `fix-shape-clear` + `queueable-fix`
- [#127148](https://github.com/openclaw/openclaw/issues/127148) Codex `sessions.compact` 二次获取 app-server 触发活跃写冲突 — **无 fix PR**
- [#139274](https://github.com/openclaw/openclaw/issues/139274) 原生 `/codex bind

---

## 横向生态对比

# 个人 AI 助手 / 自主智能体开源生态横向分析  
**数据日期：2026-09-10**  
**数据边界说明：OpenClaw 数据完整；Hermes Agent 本期摘要生成失败，无有效 Issues/PR/Release 字段。因此严格意义上的多项目横向对比受限，以下以 OpenClaw 为有效锚点，Hermes 仅标注“数据缺失/不可评估”。**

---

## 1. 生态全景

个人 AI 助手与自主智能体开源生态仍处于**高活跃、快速迭代与生产化补课并行**的阶段。  
OpenClaw 单日 Issues 与 PR 各更新 500 条，PR 合并/关闭 252 条、合并率约 50%，显示头部项目社区规模大、维护带宽接近饱和。  
社区焦点正从“功能可用”转向“升级可靠、长期运行稳定、权限边界安全”。  
原生端、多

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

⚠️ 摘要生成失败。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*