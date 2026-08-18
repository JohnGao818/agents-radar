# OpenClaw 生态日报 2026-08-18

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-08-18 00:58 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-18

## 今日速览

过去 24 小时项目保持高活跃度：共更新 500 条 Issue（新开/活跃 480 条，关闭 20 条）和 500 条 PR（待合并 368 条，已合并/关闭 132 条），社区反馈与开发推进节奏均强劲。无新版本发布，项目处于密集迭代的稳定期。值得关注的是，P0/P1 高优先级 Bug 占比偏高（约 40 条），多数集中在会话状态一致性、消息丢失、崩溃循环等可靠性核心领域，已有多个对应修复 PR 在途（如 #124303 上下文窗口溯源、#124516 会话存储查找上限）。整体健康度良好，但长期积压问题（最早可追溯至 3 月）仍需维护者加速清理。

---

## 项目进展

今日有 132 条 PR 合并/关闭，其中以下几条对项目健康度有显著推动：

- **[PR #122764]** fix(queue): arbitrate shared capacity across grouped lanes（已合并，P1）  
  修复共享容量在分组队列间的调度问题，将共享槽所有权从完成车道移至容量组调度器，避免优先级反转与饥饿。这直接解决了 #122763，是多代理网关调度可靠性的重要补强。  
  https://github.com/openclaw/openclaw/pull/122764

- **[PR #125332]** feat(ui): preserve composer drafts across restarts（已合并，P2）  
  控制 UI 现在可在浏览器或应用重启后保留未发送的草稿文本与附件，消除了一个高频 UX 痛点（#125330）。  
  https://github.com/openclaw/openclaw/pull/125332

- **[PR #125470]** fix(workboard): avoid false lifecycle warning during gateway startup（已合并，P2）  
  解决了 Workboard 插件在网关启动时误报 `sessions.list unavailable` 的问题，并推迟了首次恢复协调，提升启动期稳定性。  
  https://github.com/openclaw/openclaw/pull/125470

- **[PR #125467]** fix(pr): repeated review checkout recovers partial transitions（已合并，P2）  
  修复维护者重复使用 `scripts/pr` 审查流程时 HEAD 可能跳到 origin/main 且残留暂存变更的问题，改善内部协作流程可靠性。  
  https://github.com/openclaw/openclaw/pull/125467

- **[PR #120900]** feat(ui): review install policy warnings（已合并，安全相关）  
  认证管理员现可在控制 UI 中查看插件安装策略警告并选择继续安装，为安全审查提供了显式确认路径。  
  https://github.com/openclaw/openclaw/pull/120900

- **[PR #116489]** feat(security): require acknowledgement for install policy warnings（已合并，安全相关）  
  外部 `security.installPolicy` 现可返回 `warn` 状态，要求操作者输入精确目标名以确认理解风险后才继续安装，强化供应链安全。  
  https://github.com/openclaw/openclaw/pull/116489

---

## 社区热点

以下 Issue 在过去 24 小时获得最多讨论与关注：

- **[Issue #77598]** Track live dev agent behavior and trajectory（23 评论，👎 1）  
  一个持续观察开发代理行为的笔记式 Issue，记录了 24 小时监控过程中代理的行为轨迹。它体现了社区对代理自主行为透明化的强烈兴趣。  
  https://github.com/openclaw/openclaw/issues/77598

- **[Issue #91009]** Codex PreToolUse native hook relay spawns CPU-bound openclaw-hooks processes（20 评论，👍 2，P1）  
  报告 Codex 集成的 pre_tool_use hook 会派生多个 CPU 占用 100%+ 的短命进程并阻塞网关 RPC。这是集成层性能退化的重要信号，社区关注度高。  
  https://github.com/openclaw/openclaw/issues/91009

- **[Issue #68596]** Configurable streaming watchdog timeout threshold（15 评论，👍 8，P2）  
  当模型进行长思考（如 DeepSeek-R1）时，流式看门狗频繁误报。用户强烈要求可配置超时阈值，是体验类诉求中呼声最高的。  
  https://github.com/openclaw/openclaw/issues/68596

- **[Issue #62505]** Coding Agent never completes anything（15 评论，P1，回归）  
  编码代理在 2026.4.2 之后出现不执行任何操作的问题，影响大量开发者日常使用，是当前最高优先级的回归 Bug 之一。  
  https://github.com/openclaw/openclaw/issues/62505

- **[Issue #38327]** "Cannot convert undefined or null to object" in google-vertex/gemini-3.1-pro-preview（14 评论，👍 3，P1）  
  2026.3.2 版本中 Google Vertex/Gemini 模型集成回归，社区已有多个复现报告，是模型兼容性方面的热点。  
  https://github.com/openclaw/openclaw/issues/38327

- **[Issue #51429]** 硬编码工作路径被合并发布（12 评论，P2）  
  用户发现代码中存在某位开发者的绝对路径 `/Users/wangtao` 被硬编码并合并发布，社区反应强烈，涉及代码审查质量。  
  https://github.com/openclaw/openclaw/issues/51429

**PR 侧热点：**

- **[PR #125483]** fix(upgrade): repair stable state before gateway startup（P1，待合并）  
  修复升级过程中稳定版配置键迁移问题，防止网关启动失败，是目前最受关注的待合并 PR 之一。  
  https://github.com/openclaw/openclaw/pull/125483

- **[PR #125261]** fix(gateway): read only the visible-message tail for session previews（P2，待合并）  
  解决加载长会话预览时冻结主线程和内存膨胀问题，直接关系多会话网关的日常可用性。  
  https://github.com/openclaw/openclaw/pull/125261

---

## Bug 与稳定性

按严重程度排列，今日最值得关注的 Bug：

| 级别 | Issue | 描述 | 是否有 Fix PR |
|------|-------|------|---------------|
| **P0** | [#70903](https://github.com/openclaw/openclaw/issues/70903) | 基于文件的 provider 冷却在账单恢复后仍持续阻塞用户数小时 | 无 |
| **P1** | [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex PreToolUse hook 派生 CPU 密集型进程，堵死网关 RPC | 无 |
| **P1** | [#62505](https://github.com/openclaw/openclaw/issues/62505) | Coding Agent 回归：2026.4.2 之后无法完成任何编码任务 | 无 |
| **P1** | [#38327](https://github.com/openclaw/openclaw/issues/38327) | Google Vertex/Gemini 集成抛出 "Cannot convert undefined or null to object" | 无（label: needs-live-repro） |
| **P1** | [#78493](https://github.com/openclaw/openclaw/issues/78493) | `sudo openclaw update` 造成混合文件所有权，doctor 覆盖配置 | 无 |
| **P1** | [#97616](https://github.com/openclaw/openclaw/issues/97616) | hook/tool 子进程泄漏，僵尸进程累积导致运行时性能退化 | 无 |
| **P1** | [#86215](https://github.com/openclaw/openclaw/issues/86215) | Codex OAuth 刷新失败可令代理卡死数小时，缺少告警 | 无 |
| **P1** | [#53408](https://github.com/openclaw/openclaw/issues/53408) | 长会话后 write/exec 工具参数被静默丢弃 | 无 |
| **P1** | [#50093](https://github.com/openclaw/openclaw/issues/50093) | WhatsApp 重连后错失下线期间消息，无补拉机制 | 无 |
| **P1** | [#67777](https://github.com/openclaw/openclaw/issues/67777) | 子代理完成投递可能因超时/清空/孤儿清理而丢失 | 无 |
| **P1** | [#74586](https://github.com/openclaw/openclaw/issues/74586) | AM 内嵌运行中止 memory_search 调用，错误判定为超时 | 无 |
| **P1** | [#53540](https://github.com/openclaw/openclaw/issues/53540) | 大参数工具调用生成超时，误报 "Network connection lost" | 无 |
| **P1** | [#71689](https://github.com/openclaw/openclaw/issues/71689) | tasks registry 因 SQLite 损坏恢复失败，网关启动失败 | 无 |
| **P1** | [#45224](https://github.com/openclaw/openclaw/issues/45224) | Playwright CDP 断言错误未捕获，崩溃整个网关进程 | 无 |
| **P1** | [#72015](https://github.com/openclaw/openclaw/issues/72015) | active-memory 插件阻塞回复，QMD 启动初始化可压垮多代理网关 | 无 |
| **P2** | [#51429](https://github.com/openclaw/openclaw/issues/51429) | 硬编码 `/Users/wangtao` 路径被合并发布（审查问题） | 无 |
| **P2** | [#77930](https://github.com/openclaw/openclaw

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向对比分析报告

**报告日期**：2026-08-18  
**对标对象**：OpenClaw（github.com/openclaw/openclaw）、Hermes Agent（github.com/nousresearch/hermes-agent）

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于“规模化与产品化并行”的关键转折期。OpenClaw 单日 500 条 Issue 和 500 条 PR 的协作吞吐量，标志着头部项目已形成平台级工程协作密度；Hermes Agent 以周级 patch 版本和持续安全审计推进产品化落地。两个项目不约而同地将资源投向同一战场：会话状态一致性、工具/子进程生命周期、安全边界加固——而非新功能堆叠。社区对代理行为透明化、本地模型兼容性、可配置超时机制的诉求显著升温。整体判断：生态正由“功能扩张期”进入“稳定性治理期”。

---

## 2. 各项目活跃度对比

| 维度 | OpenClaw | Hermes Agent |
|---|---|---|
| **Issues（24h）** | 500 条（新开/活跃 480，关闭 20） | 50 条（新开/活跃 35，关闭 15） |
| **PRs（24h）** | 500 条（待合并 368，合并/关闭 132） | 50 条（待合并 40，合并/关闭 10） |
| **Release** | 无新版本，处于密集迭代稳定期 | v0.20.3（patch，聚合约 125 个 PR） |
| **高优 Bug** | P0×1、P1×15+，集中在会话一致性、消息丢失、崩溃循环等可靠性核心域；已有多个修复 PR 在途（#124303、#124516） | CRITICAL×1（Windows ACL 漏洞 #77462）、P2×5+；MCP 超时注销、.git 目录破坏、密钥丢失等 |
| **健康度评估** | 整体良好；但 P0/P1 占比较高（约 40 条），最早积压可追溯至 3 月，需加速清理 | 功能推进有序，但 CRITICAL 漏洞无修复 PR、Skills 索引故障持续 30 天未恢复，安全性/运维响应待加强 |

**数据解读**：OpenClaw 的 Issue/PR 绝对值是 Hermes 的 10 倍，反映两者处于不同量级的社区生态位。OpenClaw 更像“生态基础设施”，Hermes 则接近“产品化应用”。

---

## 3. OpenClaw 在生态中的定位

- **规模优势**：以单日 500 条 Issue + 500 条 PR 计算，OpenClaw 社区活跃度在本次对比中处于绝对高位（约为 Hermes 的 10 倍），具备大型开源平台特有的高吞吐协作特征。
- **技术路线差异**：OpenClaw 的核心技术命题是**多代理网关调度**——如批量间共享容量仲裁（#122764）、跨分组队列防饥饿、会话存储查找上限、`sessions.list unavailable` 启动期误报修复。这使其更接近“为运行大量代理而设计的服务端基础设施”。Hermes 则更贴近**桌面端个人产品**——UI 面板、插件 SDK、Cron 媒体发送、本地模型对接。
- **可靠性纵深**：OpenClaw 今日合并的 PR 中有 4 条直接针对调度可靠性、启动稳定性、审查流程可靠性；P0/P1 集中在“消息丢失”“状态不一致”“崩溃循环”，说明其正在为大规模生产环境高强度使用筑牢底座。
- **社区规模**：从唯一可对比数据源看，OpenClaw 的协作规模远超 Hermes，但这与其定位为“平台型/框架型”项目有关。若要给出生态位完整结论，需进一步与 LangGraph、CrewAI、AutoGen 等横向对比。

---

## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **代理供应链安全** | OpenClaw、Hermes | 安装策略警告与显式确认（OpenClaw #116489/#120900）；子进程凭据隔离（Hermes #83565）、Windows ACL 漏洞（#77462）、威胁扫描绕过（#84259） |
| **子代理/委派生命周期可靠性** | OpenClaw、Hermes | 子代理完成投递丢失（OpenClaw #67777）；委派预算被失败 API 调用耗尽（Hermes #77305）；委派生命周期与任务结果分离（Hermes #68499） |
| **长会话稳定性与内存控制** | OpenClaw、Hermes | 长会话工具参数静默丢弃（OpenClaw #53408）；会话预览冻结主线程（OpenClaw #125261）；MCP 超时导致整个工具集注销（Hermes #88661）；超时后预取线程不可取消（Hermes #84263） |
| **模型长推理/本地模型适配** | OpenClaw、Hermes | 流式看门狗超时阈值不可配置（OpenClaw #68596，支持 DeepSeek-R1）；Google Vertex/Gemini 回归（OpenClaw #38327）；Qwen 3.8 本地模型失败（Hermes #88762） |
| **工具/子进程生命周期治理** | OpenClaw、Hermes | Codex PreToolUse hook 派生 CPU 密集型进程（OpenClaw #91009）；hook/工具子进程泄漏与僵尸进程累积（OpenClaw #97616）；桌面端孤儿 `hermes serve` 进程残留（Hermes #76245/#80898） |
| **代理行为可观测性** | OpenClaw、Hermes | 实时追踪开发代理行为轨迹（OpenClaw #77598）；Cron 失败日志记录实际原因（Hermes #87965）；Skills 索引新鲜度探针（Hermes #66616） |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
|---|---|---|
| **核心定位** | 多代理网关/自主智能体运行时基础设施 | 桌面端个人 AI 助手/代理产品 |
| **功能

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-18

## 今日速览

过去 24 小时项目保持高度活跃：50 条 Issue 更新（35 条新开/活跃、15 条关闭），50 条 PR 更新（40 条待合并、10 条已合并/关闭），并发布了一个新的 patch 版本 v0.20.3（v2026.8.16.2）。版本发布将过去数周约 125 个 PR 汇总为稳定标签，供 Docker 镜像和托管部署采纳。安全类议题继续占据显著比重，包含 1 个 CRITICAL 级 Windows ACL 漏洞（#77462）和多个安全审计 campaign 类 issue；同时，一个评论数高达 48 条的自动化探针故障（#66616）已持续一个月未恢复，值得注意。

---

## 版本发布

### Hermes Agent v0.20.3 (v2026.8.16.2) — 2026-08-16

本次为 Patch 发布，将自 v0.20.2 以来合并的约 125 个 PR 统一收编为稳定版本，主要面向下游消费者（Docker 镜像、托管部署、全新安装）。

- **更新内容**：聚合了近期所有 bugfix、安全加固、文档更新与功能改进；不包含已知破坏性变更。
- **迁移注意事项**：常规平滑升级路径；未提及环境变量、配置格式或数据存储的破坏性变更。
- **建议**：下游部署方可将此标签作为稳定基线；注意自 v0.20.2 以来若未跟进中间版本，涉及安全修复（如 Windows ACL、MCP 密钥继承等）的累积变更较多，建议查阅 release notes 确认兼容性。

---

## 项目进展

今日有 10 条 PR 已合并/关闭，重点如下：

| PR | 内容 | 状态 |
|---|---|---|
| [#88787](https://github.com/NousResearch/hermes-agent/pull/88787) | 整合 #87965、#87967：cron 媒体发送超时可配置（env → config.yaml → 默认 300s），失败日志记录实际原因，修复"timeout 后日志空原因"问题 | ✅ 已合并 |
| [#88788](https://github.com/NousResearch/hermes-agent/pull/88788) | 桌面端 Bots 面板恢复为 Sessions 区域 Tab（而非堆叠在下方）；Cronjobs 面板仅 Bots 模式下显示 | ✅ 已合并 |
| [#88793](https://github.com/NousResearch/hermes-agent/pull/88793) | `npm run fix` 自动格式化（bot 提交） | ✅ 已合并（CI 自动） |
| [#87965](https://github.com/NousResearch/hermes-agent/pull/87965) | cron 媒体发送失败时日志补充非空失败原因 | ✅ 已合并（被 #88787 收编） |
| [#87967](https://github.com/NousResearch/hermes-agent/pull/87967) | 媒体发送超时通过 `HERMES_CRON_MEDIA_SEND_TIMEOUT` 可配置 | ✅ 已合并（被 #88787 收编） |
| [#88764](https://github.com/NousResearch/hermes-agent/pull/88764) | 桌面端运行时预配（runtime provisioning）改为仅主实例（primary-only），防止后台 profile 触发重复预配 | ⏳ 待合并 |

整体来看，项目在 cron 可靠性、桌面端 UI/UX 修正和 CI 自动化方面持续推进。较长期的 [#68499](https://github.com/NousResearch/hermes-agent/pull/68499)（委派生命周期与任务结果分离）仍然开放，涉及 gateway/TUI/Desktop 多端一致性，属于较大的结构性改动。

---

## 社区热点

| 议题 | 评论数 | 核心诉求 |
|---|---|---|
| [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | 48 | **Skills 索引陈旧/降级**。自动化新鲜度探针失败：索引已 29.8h 未更新（阈值 26h）。Skills Hub 依赖 `.github/workflows/skills-index.yml` 触发的统一索引重建。该 issue 自 7 月 18 日创建至今仍为 OPEN，持续一个月未修复，社区关注度极高 |
| [#77305](https://github.com/NousResearch/hermes-agent/issues/77305) | 5 | **委派预算被失败 API 调用耗尽**。子代理的迭代预算在模型 API 调用前即被消耗，HTTP 429 重试会燃烧预算并导致 fallback 链失效。影响所有依赖委派的复杂任务 |
| [#83565](https://github.com/NousResearch/hermes-agent/issues/83565) | 5 | **子进程凭据继承问题（Campaign EPIC）**：受信任的 Hermes 凭据可能泄漏至不受信任或模型编写的子进程。为 #77027 的唯一追踪 meta-issue，多个 PR/Issue 均绑定于此 |
| [#88706](https://github.com/NousResearch/hermes-agent/issues/88706) | 4 | **安全加固跟进**：继 #88232 关闭一个具体 incident path 后，提出关闭 use-time、provenance、authority 差距的更广泛安全加固需求 |

**分析**：#66616 是当前社区关注的焦点——自动化基础设施故障持续一个月未解决，直接影响依赖 Skills Hub 的用户，同时也暴露了监控告警后人工跟进不足的问题。安全类议题（#83565、#88706）持续活跃，反映社区对安全边界问题的敏感度较高，andrexibiza 作为主要贡献者持续跟进。

---

## Bug 与稳定性

### 严重级别最高

| 严重度 | Issue | 描述 | 修复 PR |
|---|---|---|---|
| 🔴 CRITICAL | [#77462](https://github.com/NousResearch/hermes-agent/issues/77462) | **Windows ACL 漏洞**：`_secure_file` 在 Windows 上是 no-op，`os.chmod` 仅切换只读位，不设置 ACL。实测 SYSTEM/Administrators 可读取 secrets | 未见对应 fix PR |
| 🟠 P2 | [#88661](https://github.com/NousResearch/hermes-agent/issues/88661) | **MCP 工具超时导致整个工具集注销**：超时后连接被 parked，所有工具从会话注销，需重启 gateway 恢复 | [#88802](https://github.com/NousResearch/hermes-agent/pull/88802) 已提交修复根因 |
| 🟠 P2 | [#88762](https://github.com/NousResearch/hermes-agent/issues/88762) | **Qwen 3.8 本地模型失败**：Qwen 3.6 正常但 3.8 不可用，用户反馈已尝试所有常见修复 | 待复现/处理 |
| 🟠 P2 | [#78793](https://github.com/NousResearch/hermes-agent/issues/78793) | **write_file/patch 静默破坏 .git 目录**：文件工具可改写 HEAD/refs/index 等 git 内部状态；#78565 的防护仅覆盖 .git 指针文件 | 待修复 |
| 🟠 P2 | [#77529](https://github.com/NousResearch/hermes-agent/issues/77529) | **MCP 子进程丢失密钥**：Secret Source 刷新失败导致 provenance 元数据丢失，子进程构建环境时遗漏仍存在的密钥 | 待修复 |
| 🟠 P2 | [#48860](https://github.com/NousResearch/hermes-agent/issues/48860) | **OAuth 清理器误替换文档 URL**：`hermes-agent.nousresearch.com` 被替换为已死的 `claude-code.nousresearch.com`（NXDOMAIN），影响用户访问 | 待修复 |

### 其他值得注意

- [#88790](https://github.com/NousResearch/hermes-agent/pull/88790) 修复威胁扫描截断问题（对应 #84259）：输入超过 65,536 字符时只扫描头部，尾部可绕过检测。此为安全审计 campaign 的一部分。
- [#88796](https://github.com/NousResearch/hermes-agent/pull/88796) 修复超时记忆预取线程的问题（对应 #84263）：超时后线程仍持有敏感上下文且不可取消。
- 桌面端遗留问题：多个孤儿 `hermes serve` 进程相关 issue（#76245、#80898）已关闭，但 [#88764](https://github.com/NousResearch/hermes-agent/pull/88764) 仍在审查中。

---

## 功能请求与路线图信号

今日新提交的功能/改进类 PR 较多，部分对应社区需求：

| 功能请求 | 对应 PR | 分析 |
|---|---|---|
| [#84177](https://github.com/NousResearch/hermes-agent/issues/84177) 设计模式：桌面预览/浏览器面板元素选择桥接到 agent 上下文 | 暂无直接对应 PR | 用户希望点击预览中的元素即能生成结构化上下文供 agent 操作。社区有 1 👍，需求较明确，但未见排期信号 |
| [#88658](https://github.com/NousResearch/hermes-agent/issues/88658) 插件命令无法唤回已关闭的 pane | [#88795](https://github.com/NousResearch/hermes-agent/pull/88795) 已在 PR 中暴露 `host.revealPane()` SDK 接口 | 大概率纳入下一版本 |
| Bot 隐藏/显示 | [#88800](https://github.com/NousResearch/hermes-agent/pull/88800) 已实现 right-click 隐藏 + 眼睛图标恢复 | 已实现，待合并 |
| skill 行为验证 | [#88801](https://github.com/NousResearch/hermes-agent/pull/88801) 新增 `skill-behavior-validation` 技能，实现基于模拟回放的自我验证 | 已提交，体现对 skill 质量的关注 |
| macOS 窗口半透明可读性 | [#88744](https://github.com/NousResearch/hermes-agent/pull/88744) 提升透明模式下的文字对比度 | 已提交 PR，设计优化向 |
| 中文 i18n 补全 | [#88797](https://github.com/NousResearch/hermes-agent/pull/88797) 补充 HUD/终端快捷键面板缺失的 6 条中文翻译 | 已提交，社区国际化贡献活跃 |

**信号判断**：桌面端体验优化（插件 SDK、Bot 管理、i18n、窗口效果）是近期 PR 的密集方向，反映出项目在完善桌面端产品化。安全类功能（威胁扫描尾部、预取线程隔离）也在同步加固。

---

## 用户反馈摘要

- **对自动化告警未跟进的不满**：#66616（Skills 索引降级）已持续 30 天，用户多次评论推动修复但仍未解决，说明自动化探针发现的 infra 问题缺乏有效的事件响应流程。
- **本地模型体验差异**：#88762 用户反馈 Qwen 3.8 与 3.6 行为不一致且无法自行修复，体现本地模型兼容性对用户体验的直接伤害。
- **桌面端稳定性痛点**：多个关于桌面端后端进程残留的 issue（#76245、#80898）虽然今日显示已关闭，但说明用户对"退出应用后进程不清理"有较高敏感度，期望做到干净退出。
- **安全感知增强**：#77462 的 CRITICAL 报告由 4 个独立的 red-team agent 验证，用户对安全问题的上报质量和透明度评价积极；但也说明了关键

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*