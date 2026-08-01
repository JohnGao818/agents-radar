# OpenClaw 生态日报 2026-08-01

> Issues: 500 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-08-01 02:26 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-01

## 1. 今日速览

过去24小时内，OpenClaw 项目持续保持高度活跃：Issues 更新达 500 条（新开/活跃 465 条，关闭 35 条），PR 更新同样为 500 条（待合并 362 条，已合并/关闭 138 条）。尽管今日无新版本发布，但社区讨论热度集中于 **内存泄漏、会话状态一致性与安全边界** 等核心稳定性问题，尤其是 #91588（Gateway 内存泄漏导致 OOM 崩溃）已升至 P0 级，且有多个高优先级（P1）PR 正在推进中，显示维护团队正处于密集修复阶段。总体上项目处于 **高速迭代与质量巩固并行** 状态。

---

## 2. 版本发布

今日无新版本发布（最新 Releases 为空）。

---

## 3. 项目进展

今日虽无新版本发布，但从 PR 活跃度和 Issue 关闭情况来看，多个关键修复已进入合并/审核通道，项目在以下方向取得实质推进：

- **会话状态修复**：#117148（[PR](https://github.com/openclaw/openclaw/pull/117148)）修复了休眠父代理在子任务完成后无法使用工具的问题；#117074（[PR](https://github.com/openclaw/openclaw/pull/117074)）解决 cron-heavy 代理积累不可见会话存储垃圾的问题。
- **安全边界加固**：#116304（[PR](https://github.com/openclaw/openclaw/pull/116304)）增强了对 `child_process` 调用经由别名/计算成员绕过的检测；#110582（[PR](https://github.com/openclaw/openclaw/pull/110582)）为浏览器 WebSocket 客户端增加预握手来源验证，降低跨源攻击面。
- **进程生命周期管理**：#117151（[PR](https://github.com/openclaw/openclaw/pull/117151)）修复取消/超时操作仅终止直接 PID 而遗留孙进程的问题，避免僵尸进程堆积。
- **核心推理链路加固**：#116012（[PR](https://github.com/openclaw/openclaw/pull/116012)）全面强化 Codex 流式推理的取消与错误处理机制。
- **重大架构调整**：#116300（[PR](https://github.com/openclaw/openclaw/pull/116300)）将腾讯云供应商从内置插件外部化为独立包，减少主构建体积与依赖耦合。

综上，项目在 **会话可靠性、安全防护、进程管理和架构优化** 四个维度同步推进，138 个 PR 的合并/关闭也表明代码落地效率较高。

---

## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 主题 | 分析 |
|------|----------|--------|------|------|
| 1 | [#75](https://github.com/openclaw/openclaw/issues/75) Linux/Windows Clawdbot Apps | 116 | 桌面应用支持 | 社区对 Linux/Windows 桌面客户端的呼声极高，discord 生态中用户对 macOS/iOS 之外平台覆盖的诉求强烈，讨论热度远超其他议题。 |
| 2 | [#91588](https://github.com/openclaw/openclaw/issues/91588) Gateway 内存泄漏（P0） | 23 | 内存与稳定性 | 用户报告 RSS 从 350MB 涨至 15.5GB 并触发 OOM，是最严重的稳定性事件，获得 P0 评级，引发广泛关注。 |
| 3 | [#7707](https://github.com/openclaw/openclaw/issues/7707) 记忆信任标记（Memory Trust Tagging） | 23 | 安全与记忆 | 社区关注记忆投毒攻击防御，希望通过来源信任分级防止恶意指令注入，反映用户对 AI 安全性的深层关切。 |
| 4 | [#116201](https://github.com/openclaw/openclaw/issues/116201) 实时语音状态无界积累（P1） | 16 | 资源管理 | 实时语音会话在慢速/突发场景下保留过多状态，涉及系统资源边界问题。 |

**需求分析**：讨论热度最高的三个议题分别指向 **跨平台覆盖、内存稳定性、安全体系**。其中 #75 是一个长达 7 个月仍未解决的特性请求，但评论数持续增长，说明用户对桌面应用的期待未减；#91588 与 #7707 则反映了当前 AI 助手类项目在 **生产环境可靠性** 与 **安全可信** 两大核心诉求上的用户焦虑。

---

## 5. Bug 与稳定性

### 🔴 P0 级

- **[#91588](https://github.com/openclaw/openclaw/issues/91588) [OPEN] Gateway 内存泄漏导致反复 OOM 崩溃** — RSS 从 350MB 涨至 15.5GB，2-3 天即触发 OOM，`launchd-handoff` 反复重启循环。**暂无明确 fix PR**，属于当前最高优先级问题。

### 🟠 P1 级（高影响）

- **[#116201](https://github.com/openclaw/openclaw/issues/116201) [OPEN] 实时语音会话保留无界 provider/consult 状态** — 相关修复 PR [#117162](https://github.com/openclaw/openclaw/pull/117162) 已提交（优化长回复时的音频帧队列处理）。
- **[#86519](https://github.com/openclaw/openclaw/issues/86519) [OPEN] Telegram 上代理重复回复 2-10 次（5.20 更新回归）** — 升级到 5.22 后缓解但未完全修复，影响消息质量。
- **[#115908](https://github.com/openclaw/openclaw/issues/115908) [OPEN] 会话转录投影在持续写入下活锁，阻塞主线程** — 可能导致所有通道停顿数十秒。暂无对应 fix PR。
- **[#113306](https://github.com/openclaw/openclaw/issues/113306) [OPEN] SQLite 快照恢复缺少端到端崩溃与身份保证** — 数据完整性风险。
- **[#116418](https://github.com/openclaw/openclaw/issues/116418) [OPEN] Ollama 提供方在 2026.7.1 中从未被选为主模型** — 模型路由逻辑回归，影响本地模型用户。
- **[#87109](https://github.com/openclaw/openclaw/issues/87109) [OPEN] macOS 上空闲时 Gateway 堆内存增长至 1073MB+** — 与 #91588 同源的内存问题，cron 任务在内存压力下静默失败。
- **[#45494](https://github.com/openclaw/openclaw/issues/45494) [OPEN] Cron 任务在 LLM API 持续故障时静默超时** — 应快速失败而非耗尽全部超时窗口。

### 🟡 P2 级（值得关注）

- **[#51429](https://github.com/openclaw/openclaw/issues/51429) [OPEN] 代码中 hardcode 了贡献者的工作路径** — 用户投诉安装后创建了 `/Users/wangtao` 目录，反映出代码审核流程存在疏漏。
- **[#97616](https://github.com/openclaw/openclaw/issues/97616) [OPEN] hook/tool 子进程泄漏导致僵尸进程累积** — 相关修复 PR [#117151](https://github.com/openclaw/openclaw/pull/117151) 已提交。
- **[#77930](https://github.com/openclaw/openclaw/issues/77930) [OPEN] Discord 通道在 2026.5.4 中未加载（回归）** — 已有 [#linked-pr-open](https://github.com/openclaw/openclaw/pull?q=is%3Apr+head+77930) 标记。
- **[#114137](https://github.com/openclaw/openclaw/issues/114137) [OPEN] 可见通道间歇性无回复负载分发，消息丢失** — 影响多通道可靠性。

### ✅ 今日关闭的 Bug

- **[#116391](https://github.com/openclaw/openclaw/issues/116391)** WebChat 会话历史跨天消失 — **已关闭**。
- **[#116409](https://github.com/openclaw/openclaw/issues/116409)** 所有入站消息重复写入转录（双写问题）— **已关闭**。
- **[#116868](https://github.com/openclaw/openclaw/issues/116868)** SQLite 会话回退到冻结的旧 JSONL 并复活已完成任务 — **已关闭**。

---

## 6. 功能请求与路线图信号

### 高潜力被纳入下一版本

| 功能请求 | 相关 Issue | 已有进展 | 预判 |
|----------|-----------|----------|------|
| **内存信任标记（Memory Trust Tagging）** | [#7707](https://github.com/openclaw/openclaw/issues/7707) | 社区讨论多，涉及安全 | 安全类功能，可能进入安全加固批量开发 |
| **掩蔽密钥（Masked Secrets）** | [#10659](https://github.com/openclaw/openclaw/issues/10659) | 4个 👍，安全影响明确 | 与 #7707 同属安全主题，大概率纳入 |
| **会话记忆预重置清理** | [#45608](https://github.com/openclaw/openclaw/issues/45608) | 4个 👍 | 涉及现有 compaction 机制扩展，实现成本低，可能快速纳入 |
| **主题会话族（Topic-session families）** | [#90916](https://github.com/openclaw/openclaw/issues/90916) | 2个 👍，产品决策中 | 属于较大架构改动，短期纳入可能性较低 |
| **动态模型发现（OpenRouter）** | [#10687](https://github.com/openclaw/openclaw/issues/10687) | 3个 👍，维护者参与讨论 | 模型生态快速演进下，动态发现机制有望进入规划 |

### 从 PR 反推的路线图信号

- **安全扫描升级**：#116304（检测别名绕过）、#106078（端口范围验证）等 PR 表明安全扫描链在持续强化，相关功能可能在近期合入。
- **语音通话体验优化**：#117162 针对长回复音频帧处理优化，配合 #116201 问题的修复，语音功能即将迎来稳定性提升。
- **UI/UX 改进**：#117165（本地 provider 恢复可操作化）、#116683（ClickClack 原生进度显示）等 PR 显示在交互体验细节上的打磨。
- **腾讯供应商外部化**（#116300）：架构层面将第三方服务解耦，后续可能推广至其他云厂商集成。

---

## 7. 用户反馈摘要

### 真实痛点

- **内存泄漏严重影响生产使用** — 用户在 #91588 中详细记录了内存从 350MB 增长至 15.5GB 的完整过程，并通过监控数据佐证，说明该问题在真实生产环境中已持续数日并导致服务中断。
- **Telegram 重复回复体验差** — #86519 用户反馈升级后回复重复 2-10 次，"severity significantly reduced but still annoying"，尽管部分修复已生效，仍持续影响用户体验。
- **代码审核不严引发信任危机** — #51429（hardcode 路径）以中文提交，用户直接质疑"Apparently some wangtao hardcode his working space path into the code and somebody merged his code and published"，这是对项目质量管控的直接批评。
- **配置项缺失导致无效等待** — #14747 指出 lane 等待诊断阈值硬编码为 2 秒，对 60-120 秒的合法 cron 任务造成误报，"warnAfterMs ?? 2e3"这个细节展示了配置灵活性不足。

### 使用场景

- **本地优先用户**：Ollama 主模型路由问题（#116418）表明有相当一批用户尝试用 OpenClaw 配合本地模型运行，他们对推理成本敏感、重视数据隐私。
- **跨平台需求**：#75 的 Linux/Windows 桌面应用请求已积累 80+ 👍，说明用户群已不再局限于 macOS/iOS 生态。
- **重度自动化用户**：多个 cron 相关 Bug（#45494、#87109、#117074）显示自动化任务在真实部署中比重很高，对后台稳定性有刚性需求。

### 满意度信号

- 正面：5 个 👍 的 #10659（掩蔽密钥）和 4 个 👍 的 #45608（会话内存清理）说明用户对项目安全演进方向持认可态度。
- 负面：#51429 的吐槽语气激烈，反映用户对低质量代码合入的态度是"零容忍"。

---

## 8. 待处理积压

### 长期未解决的重大 Issue

| Issue | 创建日期 | 天数 | 状态 | 严重度 | 备注 |
|-------|----------|------|------|--------|------|
| [#75](https://github.com/openclaw/openclaw/issues/75) Linux/Windows Clawdbot Apps | 2026-01-01 | 213 天 | OPEN | 特性 | 评论 116 条、80 👍，但 7 个月无实质进展 |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) Masked Secrets | 2026-02-06 | 177 天 | OPEN | 安全 | 15 条评论、4 👍，涉及安全边界 |
| [#10687](https://github.com/openclaw/openclaw/issues/10687) 动态模型发现 | 2026-02-06 | 177 天 | OPEN | 特性 | 维护者已参与讨论但无代码产出 |
| [#9986](https://github.com/openclaw/openclaw/issues/9986) 上下文超限触发模型回退 | 2026-02-05 | 178 天 | OPEN | 可用性 | 有配置但行为不符合预期 |
| [#46786](https://github.com/openclaw/openclaw/issues/46786) elevated 工具路由回归 | 2026-03-15 | 140 天 | OPEN | 安全 | P1 安全 bug，无 fix PR |
| [#51396](https://github.com/openclaw/openclaw/issues/51396) clearUnboundScopes 误删操作者权限 | 2026-03-21 | 134 天 | OPEN | 安全 | P1 + 安全 + 已有 linked PR |
| [#48238](https://github.com/openclaw/openclaw/issues/48238) 饱和会话的循环感知压缩保护 | 2026-03-16 | 139 天 | OPEN | 稳定性 | 已有改进草案但无 PR |

### 提醒维护者关注

1. **P0 内存泄漏（#91588）** 已经持续 54 天未修复，且是当前最严重的问题。建议优先排查 Gateway 进程中的缓存/订阅未释放问题。
2. **Linux/Windows 桌面应用（#75）** 是社区最长情的呼唤，建议在路线图中给出明确时间表以安抚社区。
3. **多个安全类 P1 问题**（#46786、#51396）已有 PR 但长期未合并（#51396 有 linked-pr-open 标记），促请维护者推进审核流程。
4. **#51429 的 hardcode 事件** 反映代码审查门禁可能存在盲区，建议评估 CI 中增加路径硬编码扫描等自动化检查。

---

## 横向生态对比

# 横向对比分析报告（2026-08-01）

> 说明：本次日报仅覆盖 OpenClaw 与 Hermes Agent 两个项目，以下对比基于二者数据展开。

## 1. 生态全景

个人 AI 助手/自主智能体开源生态仍处于高速演进期。OpenClaw 以单日 500 条 Issue + 500 条 PR 的流量展现出头部项目的规模效应，Hermes Agent 则以较快的 issue-to-PR 响应速度体现社区协作效率。两个项目今日均未发版，工作重心集中在稳定性修复、资源治理和提供方生态适配，而非新功能扩张。本地模型（Ollama/MLX/OpenAI-compatible）兼容性、内存/状态无界增长、跨平台桌面端体验成为共同痛点，说明用户开始将智能体视为“长期运行的生产服务”而非实验脚本。安全与信任机制（记忆防投毒、密钥掩蔽）也开始从边缘议题走向社区核心讨论。

## 2. 各项目活跃度对比

| 指标 | OpenClaw | Hermes Agent |
|------|----------|--------------|
| Issues 更新 | 500（465 活跃 / 35 关闭） | 50（48 活跃 / 2 关闭） |


---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-01

> 数据来源：GitHub Issues/PRs 过去 24 小时更新（50 Issues + 50 PRs）｜数据截止 2026-08-01

---

## 1. 今日速览

过去 24 小时项目保持着**高强度的社区交互**：50 条 Issue 更新 + 50 条 PR 更新，日均新增/活跃讨论量处于近期高位。但值得注意的是**合并吞吐偏低**——47 条 PR 仍在等待合并，仅 3 条被合并/关闭；48 条活跃 Issue 中仅 2 条关闭，积压趋势明显。今日热点集中在**本地推理（MLX/Ollama）误判截断、Windows 更新异常、桌面端回归**三大类问题上。积极的信号是社区响应速度很快：多条同日上报的 Bug 已由贡献者开出修复 PR（如 #75772 → #75794、#75725 → #75779、#75780 → #75792），且一场针对“上帝文件”的模块化重构正在由社区系统性推进。

---

## 2. 版本发布

今日无新版本发布（Releases: 0）。

---

## 3. 项目进展

今日仅 3 条 PR 完成合并/关闭，但两条合并内容质量较高，均属于**长期积压问题的收敛**：

- **[PR #63933（已合并）](https://github.com/NousResearch/hermes-agent/pull/63933) fix(agent): evict old tool-result images on OpenAI-compatible path** — 修复了 browser_vision / vision_analyze 工具结果图片在 chat_completions 线格式上无限累积、每轮重复发送的问题。该问题会导致 token 膨胀，并在 LM Studio、Ollama、vLLM、OpenRouter 等 OpenAI 兼容提供方上触发本地模型 OOM，是本地推理用户长期痛点。
- **[PR #62730（已合并）](https://github.com/NousResearch/hermes-agent/pull/62730) feat(xiaomi): support MiMo native web_search tool (#37844)** — 通过新增 `ProviderProfile.prepare_tools()` 钩子，为小米 MiMo 接入 API 级原生 `web_search` 工具，支持模型自主决策搜索并返回 `url_citation` 来源注解与并发搜索。
- **[Issue #75768（已关闭）](https://github.com/NousResearch/hermes-agent/issues/75768) Telegram 输入指示器卡死（v0.19.0 回归）** — 标注 `sweeper

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*