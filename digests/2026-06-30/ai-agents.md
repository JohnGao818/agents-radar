# OpenClaw 生态日报 2026-06-30

> Issues: 376 | PRs: 500 | 覆盖项目: 2 个 | 生成时间: 2026-06-30 02:55 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目日报 | 2026-06-30

---

## 1. 今日速览

过去 24 小时项目社区保持高度活跃：共产生 **376 条 Issue 更新**（新开/活跃 317 条，关闭 59 条）以及 **500 条 PR 更新**（待合并 444 条，已合并/关闭 56 条）。值得注意的是，有多个 P1 级 Bug 在昨日获得关键进展，同时一个涉及 `telegram` 多冒号目标解析的修复 PR 已进入维护者审查阶段。整体来看，项目正处于 **高并发修复与功能迭代并存** 的阶段，回归问题和性能瓶颈仍是社区关注焦点。

---

## 2. 版本发布

过去 24 小时无新版本发布。

---

## 3. 项目进展

### 3.1 合并/关闭的 PR（部分）
- **#97913 相关修复** – `Fix Codex dynamic tools returning raw payloads`（#97916）解决了 Codex 动态工具调用时 `Cannot read properties of undefined (reading 'reduce')` 的错误。作者 `100yenadmin` 已提交修复，目前状态为 `needs proof`。
- **#97877 的 fix PR** – `fix(agents): allow empty-error-retry when replayMetadata is absent`（#97966）针对会话中因 `hadPotentialSideEffects` 导致重试阻塞的问题提交了 PR，将空错误重试逻辑的触发条件放宽至 `replayMetadata` 缺失时也允许重试。
- **#78852 性能优化 PR** – `perf(agents): reuse media tool availability during tool prep` 已在 `ready for maintainer look` 阶段，该 PR 通过复用媒体工具可用性扫描结果减少重复注册开销，有望降低多模态场景下的工具准备延迟。
- **#78741 UI 修复 PR** – `fix(ui): reset routed sessions to main on restore` 解决了 Web UI 重载后可能重新打开陈旧的历史会话问题，已标记为 `ready for maintainer look`。
- **#97729 网关修复** – `fix(gateway): check node commands before exec-approvals invoke` 阻止了当节点未声明 `system.execApprovals` 时抛出的原始 TypeError，同样进入 maintainer 审查。

### 3.2 其他活跃 PR
- 多个长期 PR 获得维护者关注：`fix(signal): complete bidirectional quote-reply support`（#36630）、`fix(telegram): prevent silent misparse of multi-colon delivery targets`（#97823）、`pipeline: normalized provider→channel stream grammar`（#93342）等均于昨日被更新或添加了标签。

**总结：** 项目昨日在 **工具调用稳定性、会话状态恢复、代理节点兼容性** 方面取得实质推进，同时有 3 个针对 `telegram` 和 `matrix` 的通道层修复进入审查阶段。

---

## 4. 社区热点

### 4.1 最活跃 Issue（评论数 top 3）
| Issue | 评论数 | 标签 | 主题 |
|-------|--------|------|------|
| [#86538](https://github.com/openclaw/openclaw/issues/86538) | 18 | P1, diamond lobster | Session JSONL 写锁超时阻塞子代理交付通道 |
| [#80319](https://github.com/openclaw/openclaw/issues/80319) | 17 | P2, platinum hermit | QA 默认工具套件混淆 Codex 原生工具与 OpenClaw 动态工具集 |
| [#74586](https://github.com/openclaw/openclaw/issues/74586) | 11 | P1, platinum hermit | 主动记忆插件中的 `memory_search` 工具调用被异常中止并误判为超时 |

### 4.2 高反响 Issue（👍 数 top 3）
- **#79077**（👍8） – 支持 Telegram 2026-05-07 新特性（访客机器人与机器人间通信），社区期待度高但尚未有明确实现路径。
- **#94518**（👍8） – DeepSeek 缓存命中率在 6.x 升级后暴跌至 <10%，原因是边界感知缓存破坏了前缀匹配，大量用户利益受损。
- **#91363**（👍5） – 隔离 cron 任务持续报 `"LLM request failed"`，模型请求根本未到达提供商，影响多用户生产环境。

**分析：** 社区当前最迫切的需求集中在 **高可靠会话管理**（写锁、超时）、**提供商缓存效率**（DeepSeek）、以及 **通道特性对齐**（Telegram 新 API）。`#79077` 虽然热度高但并非 Bug，属于功能请求；而 `#94518` 和 `#91363` 属于直接影响可用性的 P1 级 Bug。

---

## 5. Bug 与稳定性

### 5.1 P1 级严重 Bug（需优先处理）

| Issue | 领域 | 影响 | 是否有 Fix PR |
|-------|------|------|--------------|
| [#86538](https://github.com/openclaw/openclaw/issues/86538) | Session 写锁 | 子代理交付通道被阻塞，导致消息丢失 | 无（linked PR open） |
| [#74586](https://github.com/openclaw/openclaw/issues/74586) | 主动记忆插件 | 工具调用被异常中止，误报超时 | 无 |
| [#80520](https://github.com/openclaw/openclaw/issues/80520) | Telegram 通道 | 消息静默丢失，无日志记录 | 无 |
| [#91363](https://github.com/openclaw/openclaw/issues/91363) | 隔离 cron | LLM 请求失败，模型调用完全未发出 | 无 |
| [#94518](https://github.com/openclaw/openclaw/issues/94518) | DeepSeek 缓存 | 缓存命中率 <10%，成本激增 | 无 |
| [#97877](https://github.com/openclaw/openclaw/issues/97877) | 错误重试逻辑 | `hadPotentialSideEffects` 导致瞬态 5xx 失败无法重试 | **有** → [#97966](https://github.com/openclaw/openclaw/pull/97966) |
| [#95121](https://github.com/openclaw/openclaw/issues/95121) | Codex OAuth | 微小响应竟花 28 秒，性能回归 | 无 |
| [#83532](https://github.com/openclaw/openclaw/issues/83532) | Web UI | 响应延迟，需手动刷新 | 无 |

### 5.2 P2 级回归/行为异常

| Issue | 描述 | 影响 |
|-------|------|------|
| [#82662](https://github.com/openclaw/openclaw/issues/82662) | 隔离 cron `agentTurn` 在 runner 启动前超时，尚未调用 LLM | 崩溃循环 |
| [#80040](https://github.com/openclaw/openclaw/issues/80040) | OAuth 失效级联故障：空占位符回复、重复工具执行、上下文丢失 | 消息丢失 + 安全 |
| [#77642](https://github.com/openclaw/openclaw/issues/77642) | 5.3 回归：重复答案与“缺失工具结果”合成错误 | 消息丢失 |
| [#96857](https://github.com/openclaw/openclaw/issues/96857) | 正常的工具文本输出被替换为 `(see attached image)` 占位符 | 工具结果不可用 |

**趋势：** 昨日社区新报告了 **#97877** 关于错误重试被阻塞的问题，并迅速获得修复 PR；**#96857** 则提示工具文本退化问题可能涉及核心渲染层。此外，多个 `isolated cron` 相关故障（#91363、#82662、#95500）表明 `embedded-run` 启动阶段存在系统性瓶颈。

---

## 6. 功能请求与路线图信号

### 6.1 高优先级功能请求
- **Telegram 访客机器人/机器人间通信**（[#79077](https://github.com/openclaw/openclaw/issues/79077)） – P2, 8 👍，尚无相关联 PR，但被标记 `needs-product-decision`。
- **技能作者定义安装脚本**（[#80213](https://github.com/openclaw/openclaw/issues/80213)） – P2, 4 👍，提出了 `setup.script` 钩子，已有 fix-shape-clear 标签。
- **插件 SDK 稳定暴露**（[#81913](https://github.com/openclaw/openclaw/issues/81913)） – P2, 1 👍，意图减少第三方插件对内部模块的依赖。

### 6.2 可能与下一版本相关的 PR
- **通道级流语法归一化**（[#93342](https://github.com/openclaw/openclaw/pull/93342)） – XL 级 PR，涉及几乎全部通道和提供商，旨在将不同格式统一为单一事件语法。虽然尚未合并，但作者持续更新，有潜力成为 2026.7.x 的核心变更。
- **Hugging Face 文生图支持**（[#94064](https://github.com/openclaw/openclaw/pull/94064)） – 已在 mock-only-proof 阶段，若被采纳将扩展 OpenClaw 的多模态能力。

**路线图信号：** 暂无官方路线图更新，但基于社区热度，`Telegram 新特性`、`DeepSeek 缓存修复`、`Session 写锁优化` 是最可能被纳入下一版本的议题。

---

## 7. 用户反馈摘要

从 Issues 评论中提取的关键用户声音：

### 7.1 普遍痛点
- **“隔离 cron 任务无法使用”** – 多位用户（#91363、#82662、#95500）报告隔离模式下的 cron 作业几乎不可用，即使设置 `timeoutSeconds` 也无济于事，严重影响自动化工作流。
- **“升级后性能变差”** – 用户 `crash2kx` 在 #95121 中抱怨“微小 gpt-5.5 回复在升级后延迟从<5秒变为28秒”，另一位用户 `tpattersonbuilders-code` 则报告 CLI 命令冷启动达到 14 秒回归。
- **“DeepSeek 缓存失效导致成本飙升”** – #94518 的用户 `xiep-dot` 表示缓存命中率从之前 >60% 降至 <10%，直接影响 API 费用。
- **“Telegram 消息静默丢失”** – 用户 `kyle20026` 在 #80520 中详细描述了多次消息“发送成功但无日志、无回复”的体验，操作了 4 次都未收到回应。

### 7.2 积极反馈
- **无障碍用户对线性持久工作区模式的认可** – 盲人用户 `xiaopinpin-music` 在 #82450 中写道：“OpenClaw 是我用过的最强大的 AI 工作界面之一”，并请求增加线性模式以配合屏幕阅读器。
- **对快速修复的感激** – 尽管未明确表达，但 `#97966` 在 #97877 报告后几小时内就提交了 PR，这种响应速度值得肯定。

### 7.3 使用场景多样性
- 用户利用 OpenClaw 完成视频推广、浏览器自动化、社交媒体发布、博客写作、音乐市场研究、AI 辅助工作区管理等。
- 企业用户侧重 Telegram 多代理、隔离 cron 定时任务和 OAuth 集成。

---

## 8. 待处理积压

以下为长期未响应或处于停滞状态的重要议题，提醒维护者关注：

| 议题 | 标签 | 最后更新 | 为何重要 |
|------|------|----------|----------|
| [#80176](https://github.com/openclaw/openclaw/issues/80176) JSONL 会话回放工具 | P3, diamond lobster | 2026-06-29 | 属于 Codex×Pi 对等性第五阶段，依赖阶段一尚未合并，可能影响整个测试框架 |
| [#80286](https://github.com/openclaw/openclaw/issues/80286) CLI `sessions --json` 缺少子代理元数据 | P2, diamond lobster | 2026-06-29 | 涉及可观测性，社区有明确需求，但处于 `needs-product-decision` |
| [#81061](https://github.com/openclaw/openclaw/issues/81061) 预路由拦截钩子 | P2, diamond lobster | 2026-06-29 | 挂钩系统缺失关键 Hook，但被标记 `stale`，无进展 |
| [#82515](https://github.com/openclaw/openclaw/issues/82515) 媒体理解静默路由至未声明视觉模型的模型 | 已关闭 | N/A | 虽已关闭，但修复尚未合并至稳定版 |
| [#16896](https://github.com/openclaw/openclaw/issues/16896) Web 聊天中右键回复 | P3, diamond lobster | 2026-06-29 | 简单但有效的小功能，已关闭但理由不明，可能被优先级后置 |
| [#12581](https://github.com/openclaw/openclaw/pull/12581) 会话修剪生命周期事件 Hook | P2 | 2026-06-30 更新 | 老旧 PR（2月），作者未响应，但若合并可提供可观测性能力 |

**建议：** 维护者应考虑对 `#81061`、`#80286` 等产品决策类 issue 给出明确方向，避免长期积压。此外，针对多个 `isolated cron` 故障（#91363、#82662）建议成立专项调查，因其影响用户自动化工作流的核心能力。

---

*生成时间：2026-06-30 基于 OpenClaw GitHub 数据（github.com/openclaw/openclaw）*

---

## 横向生态对比

好的，这是基于 OpenClaw 和 Hermes Agent 两个项目 2026-06-30 社区动态生成的横向对比分析报告。

---

## 个人 AI 智能体开源生态横向对比分析报告

**报告日期：** 2026-06-30  
**分析对象：** OpenClaw、Hermes Agent  
**分析师：** 资深技术分析师

---

### 1. 生态全景

当前个人 AI 智能体/自主智能体开源生态正经历 **“高活跃度与高脆弱性并存”** 的快速分化阶段。社区贡献者热情高涨（两家项目日均有超过 50 条 Issue/PR 产生），但核心维护团队的响应合并效率明显滞后于社区反馈，导致 **Bug 积压与安全风险持续累积**。同时，用户需求正从“单次对话”向“持久化服务”演进，对会话连续性、跨平台稳定性和缓存效率提出了更高要求。OpenClaw 在通道层和工具调用稳定性上占据领先地位，而 Hermes Agent 则在桌面/TUI 体验与平台兼容性上发力，两者共同推动了智能体从“可用”向“可靠”的跨越。

---

### 2. 各项目活跃度对比

| 指标 | OpenClaw | Hermes Agent | 分析 |
|------|----------|---------------|------|
| **新开/活跃 Issue** | 317 | 50 | OpenClaw 体量约为 Hermes 的 6.3 倍，生态规模更大 |
| **总 Issue 更新量** | 376 | 50（推测） | OpenClaw 社区讨论密度极高 |
| **总 PR 更新量** | 500 | 50 | OpenClaw PR 活跃度是 Hermes 的 10 倍 |
| **合并/关闭 PR 数** | 56 | 4 | 合并率：OpenClaw 11.2% vs Hermes 8% |
| **待合并 PR 数** | 444 | 46 | 两者均存在严重 PR 积压，Hermes 积压比更突出 |
| **版本发布** | 0 | 0 | 均无新版本发布，处于密集修复迭代期 |
| **P1/P2 Bug 总数** | 10+ (明确列出 8 个 P1) | 8+ (明确列出 4 个 P1/P2) | OpenClaw 严重 Bug 绝对数更多，但修复 PR 比例稍高 |
| **健康度评估** | **中等偏高**：合并效率尚可，社区修复积极，但 444 条待合并 PR 构成短期瓶颈。 | **偏低**：合并率极低，核心功能（TUI、平台兼容）Bug 长期未修复，安全 PR 等待审查。 | OpenClaw 更健康，Hermes 急需提升合并效率以避免社区贡献流失。 |

---

### 3. OpenClaw 在生态中的定位

- **优势**：OpenClaw 是目前生态中 **最完整的智能体核心框架**，覆盖了通道层（Telegram/Matrix）、工具调用（Codex 动态工具）、会话管理、缓存与性能优化等全链路。其社区规模（每日 300+ Issue/500+ PR）远超 Hermes Agent，拥有更丰富的第三方插件和技能生态（如主动记忆插件、隔离 cron）。
- **技术路线差异**：OpenClaw 强调 **统一的流语法归一化**（如 PR #93342）和 **跨通道行为一致性**，致力于将不同提供商差异抽象为单一事件语法。Hermes Agent 则更注重 **桌面/TUI 原生体验**（嵌入式浏览器、持久的“超级代理”循环）和 **安全边界强化**（敏感路径检查、API Key 消毒）。
- **社区规模对比**：无论从 Issue/PR 数量还是用户反馈广度（多个企业用户提及 Telegram 多代理、OAuth 集成），OpenClaw 的生态成熟度与影响力均显著高于 Hermes Agent。

---

### 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|----------|----------|
| **高可靠会话管理** | OpenClaw、Hermes Agent | OpenClaw 面临 Session 写锁超时阻塞子代理（#86538）；Hermes Agent 存在会话删除后磁盘残留（#55088）和跨平台会话连续性断裂（#54981）。 |
| **提供商缓存效率** | OpenClaw（DeepSeek #94518）、Hermes（自定义 Provider 推理参数静默丢失 #55276） | 用户对模型调用成本与参数有效性高度敏感，缓存命中率暴跌或推理参数失效导致严重体验下降。 |
| **工具调用稳定性** | OpenClaw（#97877 错误重试阻塞、#96857 工具文本替换为占位符）、Hermes（#55202 会话 ID 获取不稳定） | 两者均存在动态工具/子进程工具调用异常，影响 Agent 自主执行可靠性。 |
| **平台兼容性** | OpenClaw（Telegram 消息静默丢失 #80520）、Hermes（Windows 终端冻结 #32207、符号链接安全绕过 #55367） | 跨平台一致性与安全性是用户核心诉求，尤其 Linux/Windows/macOS 之间的差异导致功能失效。 |
| **错误重试与故障恢复** | OpenClaw（#97877 瞬态 5xx 无法重试）、Hermes（TUI 管道 EOF 崩溃 #27282） | 两者都有因不合理的重试逻辑或管道设计导致的瞬态失败无法恢复的问题。 |

---

### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
|------|----------|---------------|
| **功能侧重** | 通道层抽象、工具调用全链路、缓存优化（DeepSeek）、插件 SDK 生态 | 桌面/TUI 体验、浏览器嵌入式 Agent、安全边界强化（ACL、敏感路径）、平台兼容性（Windows） |
| **目标用户** | 中大型部署（企业级多代理、Telegram 频道运营）、技能开发者 | 个人开发者/研究者、桌面重度用户、追求低延迟交互的 CLI 爱好者 |
| **技术架构关键差异** | 基于 **Pi 对等模型** 的代码库组织，强调通道层与工具层的接口标准化（如 PR #93342 流语法归一化） | 使用 **Gateway 进程模型**，通过 `embedded-run` 实现隔离 cron，依赖 `ACP`（Auto-Connect Protocol）进行跨平台会话管理 |
| **社区协作模式** | 合并效率相对较高（11.2%），维护者积极参与代码审查（如快速响应 #97877 修复） | 合并效率极低（8%），大量高价值安全/修复 PR 长期等待关注，社区贡献者需自行推动 merge |

---

### 6. 社区热度与成熟度

- **快速迭代阶段：OpenClaw**  
  项目处于 **高并发修复与功能迭代并存** 的阶段。社区讨论广泛覆盖性能回归（如 CLI 冷启动 14 秒）、通道新特性（Telegram 2026 新 API）、缓存机制重构等。虽然积压 PR 数量多，但维护者仍保持每日审查和合并节奏，项目整体向 **质量巩固阶段** 过渡。

- **质量巩固阶段早期：Hermes Agent**  
  Hermes 正处于从“功能扩展”向“稳定性加固”转型的 **痛苦期**。社区贡献了大量的安全、兼容性修复 PR，但核心维护团队的审查能力明显不足，导致 Bug 长期未解决（如 TUI 崩溃 #27282 已达数月）。若不能迅速提升合并效率，项目可能逐步失去社区信任。

---

### 7. 值得关注的趋势信号

1. **“持久化 Agent” 成为下一代应用范式**  
   Hermes Agent 中 `#21172`（First-class Loop Contract）与 OpenClaw 隔离 cron 故障频发形成鲜明对比：用户希望 Agent 从“单次对话”进化为“持久的后台服务”，需要声明式的预算、停止、刷新抽象。这对开发者意味着需要重新设计任务调度与状态持久化架构。

2. **缓存策略从“命中率”转向“边界感知”**  
   OpenClaw 的 DeepSeek 缓存崩盘（#94518）揭示了边界感知缓存的脆弱性。用户对成本高度敏感，任何缓存退化都会立即引发社区反弹。未来智能体框架需要提供可观测的缓存命中报告，并允许用户选择缓存模式。

3. **安全边界自动化审查成为刚需**  
   Hermes Agent 连续出现符号链接绕过敏感路径检查（#55367）、API Key 被误解释为命令（#55373）、凭证池读取过时环境变量（#20591）。这表明随着 Agent 权限提升（如 ACP/自动审批），安全扫描、输入消毒和路径解析必须成为 CI/CD 检查标准。

4. **跨平台一致性是用户体验分水岭**  
   两个项目在 Windows/macOS/Linux 上均出现特有 Bug（Hermes 终端冻结、OpenClaw 消息静默丢失），且用户反馈强烈。对于 AI 智能体开发者，未来若以桌面为主要入口，必须将 Windows/WSL 列为第一等公民进行测试。

---

*注：本报告仅基于 2026-06-30 当天的公开社区数据生成，不构成投资或项目选择建议。*

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，以下是为您生成的 **Hermes Agent 项目日报**，基于 2026-06-30 的 GitHub 数据生成。

---

## Hermes Agent 项目日报

**日期:** 2026-06-30
**分析师:** AI 智能体与开源项目分析师

---

### 1. 今日速览

今日项目活动量极高，**社区活跃度达到峰值**。24小时内产生了 **50条 Issue** 和 **50条 PR**，讨论非常热烈，表明用户参与度和贡献意愿都很强。然而，**版本发布为 0**，且 PR 合并率极低（仅 4/50），**积压问题严重**。大量 P1/P2 级别的 Bug 报告（尤其是围绕 TUI、Gateway 会话状态和 Windows 平台兼容性）被密集提交，而安全边界相关的修复 PR 正在积极讨论中。项目社区热情高涨，但维护者的响应和合并效率面临巨大挑战，整体呈现出“高活跃、低处理”的健康度风险信号。

### 2. 版本发布

今日无新版本发布。

### 3. 项目进展

尽管合并数量不多，但今日合并/关闭的 PR 及活跃的 PR 代表了关键进展：

- **安全修复 PR 密集提报：** 社区贡献者针对安全边界问题提交了多个 PR。
    - `#55373` **[PR]** `fix(security): reject command-shaped API key inputs`：旨在防止用户误粘贴CLI命令作为API Key，提升了凭证管理的安全性。
    - `#55368` **[PR]** `Resolve symlinks in the ACP auto-approve sensitive-path guard`：针对 `#55367` 的安全问题提供了修复方案，解决了符号链接绕过敏感路径检查的问题。
    - `#55370` **[PR]** `Keep leading-zero union values as strings`：修复了工具参数中前导零被错误转换为整数的问题，避免了数据丢失。
- **核心功能 Bug 修复：** 针对 Agent 和 Gateway 的核心问题有修复 PR 提交。
    - `#55361` **[PR]** `fix(agent): preserve verify-on-stop attempted final answer`：修复了“验证即停止”功能下，最终答案被错误替换的问题，改善了用户体验一致性。
    - `#55365` **[PR]** `fix(gateway): normalize table fallback headings`：修复了在 Telegram 等平台上表格渲染时，Markdown 标记嵌套导致的显示错误。
- **平台兼容性改进：**
    - `#55339` **[PR]** `fix: add explicit UTF-8 encoding to all subprocess text=True calls`：此大规模修复（涉及146个文件）旨在解决 Windows 平台上因默认编码（GBK）与 UTF-8 不兼容导致的崩溃问题，是提升项目跨平台稳定性的重要一步。
- **其他合并/关闭项：**
    - Issue `#53632` **[Closed]** 关于 Telegram 上 cron 任务表格显示异常的 Bug 已关闭，问题已获解决。

**结论：** 社区贡献者正积极填补维护空缺，特别是在安全性和平台兼容性方面。然而，这些修复 PR 大多仍处于 OPEN 状态，审批和合并速度是当前项目进展的瓶颈。

### 4. 社区热点

- **Issue `#27282` [Bug]** `[--tui] gateway exits mid-turn with stdin EOF`: 该 Issue 以 **10条评论** 成为今日最热门讨论。核心问题是 macOS 上 TUI 模式下的核心崩溃问题，用户指出现象非常严重且非个例。
    - **诉求分析：** 社区对 TUI（文本用户界面）的稳定性容忍度低。该问题直接导致会话中断，严重影响使用基本功能。用户期望开发团队对 TUI 模式的管道通信机制 (stdin/command pipe) 进行彻底审查和修复。
- **Issue `#21172` [Feature]** `[Feature]: First-class Loop Contract`: 以 **6条评论** 位列第二，讨论了“持久化代理循环”的构想。
    - **诉求分析：** 核心贡献者或资深用户（引用了 Claude Code 负责人的观点）正在推动一个更高级别的抽象：将 cron 驱动的循环任务（如持续的代码审查、市场监控）视为“一等公民”，需要声明式的预算、停止、刷新和作用域控制。这表明社区正在思考 Agent 从“单次任务”向“持久化服务”演进。

### 5. Bug 与稳定性

今日报告的 Bug 主要集中在**会话状态丢失**、**平台兼容性**和**安全绕过**等方面。按严重程度排列如下：

- **P1 - 严重：**
    - `#27282` **[Bug]** `[--tui] gateway exits mid-turn`: **macOS 核心崩溃**，会话被强制中断。已有活跃讨论，但尚无Fix PR。 (已在上文分析)
    - `#20591` **[Bug]** `credential pool reads stale os.environ`: **安全凭证污染风险**。`_get_env_prefer_dotenv()` 函数逻辑与文档不符，可能导致使用旧环境变量而非用户手动配置的 `.env` 文件。已有讨论，但无Fix PR。
- **P2 - 高：**
    - `#55367` **[Security]** `ACP auto-approve sensitive-path guard ignores symlinks`: **严重安全绕过**。符号链接可绕过自动审批的敏感路径检查。已有关联的 Fix PR `#55368`，但尚在待合并状态。
    - `#32207` **[Bug]** `/clear command freezes the terminal (Windows/WSL)`: **终端阻塞**，影响 Windows 用户核心体验。
    - `#55276` **[Bug]** `reasoning_effort silently dropped for custom providers`: **功能静默失效**。用户设置的高级推理参数（如 `thinking_budget`）对于部分 Provider 配置无效，且无任何提示，误导性强。
    - `#55088` **[Bug]** `HTTP session delete leaves files on disk`: **资源泄漏**。通过 Dashboard 或 API 删除会话后，相关磁盘文件未被清理。
    - `#55202` **[Bug]** `HERMES_SESSION_KEY... unreliable in gateway/Desktop mode`: **工具功能受限**。子进程工具无法可靠获取当前会话 ID，导致跨工具协作功能可能失效。
- **P3 - 中：**
    - `#37527` **[Bug]** `Desktop chat mouse-wheel scroll-up snaps back`: **GUI 用户体验差**。在长线程中滚动会跳回底部。
    - `#55038` **[Docs]** `bundled skill says cron has 3-minute interrupt, code uses 600s timeout`: **文档与代码不符**，可能误导用户。

### 6. 功能请求与路线图信号

- **潜在纳入下一版本的功能：**
    - **嵌入式 Agent 浏览器 (PR `#55364`)**: 一项重大的新功能 PR，允许 Agent 在桌面应用中“观察”和“控制”浏览器，并提供元素检查器和设计模式。如果被合并，将**显著增强 Agent 的网页自动化能力**。该 PR 今日刚提交，但代表了清晰的路线图方向。
    - **Per-depth Subagent Model Routing (Issue `#55039`)**: 用户希望为不同深度的委派任务使用不同性价比的模型，以优化成本和效率。这是一个高级的代理拓扑管理功能。
    - **`compress_context` 命令 (Issue `#31684`)**: 用户长期诉求的上下文压缩功能，旨在解决长对话中的 token 消耗问题。
- **持续关注的信号：**
    - **Persistence & Continuity (Issue `#54981`, `#32626`)**: 跨平台（Desktop/CLI/Telegram）的会话连续性（`#54981`）和 SSH 隧道连接的持久化（`#32626`）是用户体验提升的关键方向。
    - **Configurable Temperature (Issue `#17565`)**: 社区通过长时间（自4月）的投票和评论，持续呼吁开放 `temperature` 参数配置，以解决模型幻觉问题。
    - **Protected Skills (Issue `#25083`)**: 防止核心技能被 Agent 自身意外修改的需求越来越强烈，是安全治理的重要一环。

### 7. 用户反馈摘要

- **痛点与不满：**
    - **“使用 `/clear` 命令后终端冻结，我必须重启终端。”** —— `ostarev` (#32207)，点出 Windows WSL 环境的严重可用性问题。
    - **“表格总是错乱，不管我怎么告诉代理都不行。”** —— `lrnd1` (#53632)，Telegram 平台上对 cron 任务输出格式的持续抱怨。
    - **“无法在 Desktop 和 Telegram 之间继续同一个会话。”** —— `Gavin-ZCX` (#54981)，会话锁定在单一入口点是明显的体验割裂。
- **使用场景与期望：**
    - **“我的工作流已经从单次会话转向数十个持久化的‘超级代理’。”** —— `zhengsx` (#21172)，高级用户正将 Hermes 用于运行后台，需要更健壮的循环管理和控制。
    - **“我需要 `reasoning_effort` 能真正生效，不然高级模型等于白用。”** —— `aider4ryder` (#55276)，用户愿意为高级推理（如深度思考）付费，但功能失效会导致资源浪费和信任下降。
    - **“能否为一个项目设置它自己的 skill auto-update，就像全局 skill 一样？”** —— `Hayston1001` (#55001)，用户希望将 Agent 管理能力下沉到项目级。

### 8. 待处理积压

- **关键 Bug 等待关注：**
    - `#20591` **[P1, Bug]** `credential pool reads stale os.environ`：该问题自 5 月 6 日上报，持续近两个月未修复，存在安全风险。请开发者优先审查。
    - `#13489` **[P3, Bug]** `ACP sessions with provider="custom" fail to resolve correct credential`：自 4 月 21 日上报的老问题，影响使用自定义 Provider 的 ACP 用户。
- **等待合并的 PR（影响范围大）：**
    - `#55339` 、 `#55373` 、 `#55368` 、 `#55370` ：这些 PR 均涉及**安全、平台兼容性和核心功能修复**，应尽早进行 Code Review 并合并，以回馈社区贡献，稳定项目状态。
    - `#21774` **[P3, PR]** `fix: harden Google Workspace OAuth setup`：自 5 月 8 日创建的 PR，长期未合并，拖慢了 Google 工作区集成功能的完善。
    - `#17480` **[P2, PR]** `fix(auth): resolve Codex usage credentials`：影响 `/usage` 命令的 OAuth 凭证解析，自 4 月底以来一直等待合并。

**每日总结：** 今日的 Hermes Agent 社区呈现出典型的“开源繁荣与尴尬”并存的状态：用户和贡献者热情高涨，大量高价值的新功能和修复被提出，但核心维护团队的响应速度明显跟不上社区节奏，低合并率和高积压正在成为项目的瓶颈。建议项目维护者优先整合社区力量，加快对安全及核心稳定性修复 PR 的审批流程，并明确路线图，引导社区贡献走向。

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*