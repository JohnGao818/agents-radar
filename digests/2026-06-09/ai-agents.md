# OpenClaw 生态日报 2026-06-09

> Issues: 500 | PRs: 472 | 覆盖项目: 2 个 | 生成时间: 2026-06-09 02:45 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)

---

## OpenClaw 项目深度报告

# OpenClaw 项目日报 — 2026-06-09

## 1. 今日速览

- 过去24小时内，项目保持极高活跃度：**500条Issues更新**（新开/活跃436，关闭64）和**472条PR更新**（待合并331，已合并/关闭141），开发与社区讨论双线并行。
- 发布两个小版本 **v2026.6.5-beta.3** 与 **v2026.6.5-beta.5**，重点修复了QQBot的 `thinking` 内容泄漏、MCP工具结果类型强制转换等关键问题。
- 多起高影响Bug（如ChatGPT Responses传输失败、会话上下文混淆、Discord泄漏内部工具调用）仍在审理中，但已有对应PR在推进修复，整体趋向稳定。
- 社区功能请求集中在中英文编码统一、技能市场生态、多会话架构等方向，项目路线图信号清晰。

## 2. 版本发布

### v2026.6.5-beta.5（最新）
- **下载**：[GitHub Release](https://github.com/openclaw/openclaw/releases/tag/v2026.6.5-beta.5)
- **亮点**：
  - **QQBot 内容净化**：自动剥离模型推理的 `<thinking>` 脚手架，防止原始思维链泄漏到频道回复中（#89913, #90132, 感谢 @openperf）。
  - **MCP 工具结果类型强制**：对 `resource_link`、`resource`、`audio`、畸形图片等类型进行自动转换，提升跨MCP协议的兼容性。
  - 其他底层改进与稳定性修复。

### v2026.6.5-beta.3（同日较早发布）
- 同样包含QQBot `<thinking>` 剥离和MCP类型强制，但后续beta.5在此基础上追加了额外修复。建议直接升级至beta.5。

**迁移注意**：两个beta版本的发布间距极短，无破坏性变更，推荐所有用户更新至beta.5。

## 3. 项目进展

以下为今日合并/关闭的重要PR（从数据中按CLOSED状态提取）：

| PR # | 标题 | 标签 | 说明 |
|------|------|------|------|
| #91526 | refactor(sqlite): drop unused async Kysely driver from node:sqlite dialect | maintainer, size:M | 清理未使用的异步Kysely驱动，减少维护负担 |
| #90856 | fix(agents): preserve ImageContent.data from transcript redaction | agents, P1 | 修复用户图片块在会话转录后被错误编辑导致后续请求失败的问题 |
| #91529 | Fix transcript image redaction | agents, maintainer, P1 | 进一步修复图片编辑逻辑，恢复已损坏的会话图片 |
| #91536 | fix(config): use Start-Process -FilePath for Windows config opener | gateway, size:XS | 修复Windows上“打开配置”动作因PowerShell参数错误而失败的问题 |
| #88929 | [Bug] Feishu streaming card: abnormal typewriter effect... | closed | 飞书流式卡片打字机效果异常及内容截断问题已修复 |
| #65156 | Memory vector search broken in v4.11 — sqlite-vec ABI mismatch | closed | 内存向量搜索因SQLite ABI不匹配而失效的问题已修复 |
| #44292 | Add an autofix or generator for missing config field labels | closed | 添加了缺失配置字段标签的自动修复生成器 |
| #44297 | Surface Slack external arg-menu fallback as a visible health signal | closed | Slack外部参数菜单降级现在会作为健康信号可见 |
| #48300 | Bug: memory_search hybrid mode not returning FTS matches | closed | 混合搜索模式下全文搜索匹配未返回的问题已修复 |
| #87326 | Telegram streaming: intermediate text blocks between tool calls are silently lost | closed | Telegram流式消息中工具调用间的中间文本丢失问题已修复 |

此外，多个高讨论度的Bug（如#90083、#32296、#48003）均有对应OPEN状态的PR在审查中，项目整体修复效率较高。

## 4. 社区热点

以下为今日评论数最高、社区关注度最集中的Issues：

1. **#48788** — 「feat: centralized filename encoding utility for multi-encoding Content-Disposition handling」  
   评论18条，0赞  
   需求：针对飞书、Discord等多渠道的附件文件名编码（UTF-8、Shift-JIS、GB18030等）提出统一中央编码工具，解决当前PR#48578仅修复UTF-8的问题。  
   [链接](https://github.com/openclaw/openclaw/issues/48788)

2. **#32473** — 「[Bug]: control ui requires device identity (use HTTPS or localhost secure context)」  
   评论17条，4👍  
   多用户报告在VPS/Docker上使用Brave密钥后报错“control ui requires device identity”，要求HTTPS或localhost安全上下文。影响auth-provider，但尚未有紧急修复PR。  
   [链接](https://github.com/openclaw/openclaw/issues/32473)

3. **#90083** — 「[Bug]: 2026.6.1 OpenAI ChatGPT Responses transport fails with invalid_provider_content_type for gpt-5.4/gpt-5.5」  
   评论15条，3👍  
   升级后使用gpt-5.4/5.5模型传输失败，错误码`invalid_provider_content_type`。影响P1，涉及OpenAI新模型兼容性。  
   [链接](https://github.com/openclaw/openclaw/issues/90083)

4. **#50090** — 「Community Skill Development & ClawHub」  
   评论15条，2👍  
   社区技能市场ClawHub的生态构建讨论，涉及技能开发、发布、安装流程的改进，但当前实际体验距离承诺有较大差距。  
   [链接](https://github.com/openclaw/openclaw/issues/50090)

5. **#32296** — 「[Bug]: Agent replies to previous message instead of current message (session context confusion)」  
   评论14条，1👍  
   经典会话上下文混乱Bug，代理回复错位，P1且影响消息丢失。虽有统计但持续未解决。  
   [链接](https://github.com/openclaw/openclaw/issues/32296)

**诉求分析**：社区最迫切的需求集中在三个方向——**多编码文件名处理**（国际化场景）、**新版OpenAI模型的适配**（紧跟模型发布）、**会话层稳定性**（基础体验问题）。

## 5. Bug 与稳定性

按严重程度排列（P1影响关键功能，P2影响使用体验），括号内标注是否有对应修复PR。

| 严重性 | Issue # | 摘要 | 状态 |
|--------|---------|------|------|
| P1 | #90083 | OpenAI ChatGPT gpt-5.x传输失败 `invalid_provider_content_type` | 无已知修复PR |
| P1 | #32296 | 代理回复错位（会话上下文混淆） | 无新修复PR |
| P1 | #48003 | Steer模式无法在回合中间注入消息 | 无新修复PR（linked PR #48003提及） |
| P1 | #43367 | 多代理编排不稳定（并发添加覆盖、会话锁失效） | 无新修复PR，需产品决策 |
| P1 | #49876 | Cron会话在工具失败时产生幻觉输出 | 无新修复PR |
| P1 | #51363 | Docker沙箱容器名冲突（同一主机多实例） | 无新修复PR |
| P1 | #51396 | clearUnboundScopes无条件剥离非本机Token客户端的操作员作用域 | 无新修复PR |
| P1 | #47975 | 子代理会话持久化导致主会话无响应 | 无新修复PR |
| P2 | #48788 | 多编码Content-Disposition中央工具（功能请求，非Bug） | 无新修复PR |
| P2 | #51429 | 工作路径hardcode为`/Users/wangtao` | 无新修复PR |
| P2 | #41744 | 飞书读取图片工具结果在最终载荷中丢失媒体 | linked PR #41744 |
| P2 | #44993 | Heartbeat/Cron时间戳过时（不刷新） | linked PR #44993 |
| P2 | #85888 | Cron任务在凌晨时段（05:00-07:30 CST）MiniMax 503失败 | 无新修复PR |
| P2 | #45765 | OPENCLAW_HOME设置后产生嵌套目录 | 无新修复PR |
| P2 | #50442 | backup create超时后遗留大.tmp文件耗尽磁盘 | 无新修复PR |

**趋势**：P1 Bug数量仍然较多（至少8个），且多数缺乏修复PR；P2 Bug中部分有linked PR但进展缓慢。需重点关注#90083和#32296对用户基本体验的影响。

## 6. 功能请求与路线图信号

今日出现的高质量功能请求及与已有PR的关联：

- **#50090** (Community Skill Development & ClawHub) — 技能市场生态，已有PR #78441（toolsAllow转发）为子代理能力授权奠定基础。
- **#48788** (centralized filename encoding) — 多编码文件名处理，已有PR #48578解决UTF-8场景，但离统一架构尚远。
- **#42475** (per-agent cost budget) — 按代理成本预算，网关级控制，尚无实现。
- **#43260** (per-skill model routing) — 技能级模型路由，允许不同技能使用不同模型，无对应PR。
- **#50199** (skill priority configuration) — 技能优先级配置，减少技能选择冲突。
- **#45608** (pre-reset agentic memory flush) — 在`/new`和每日重置前执行内存刷新，已有类似机制用于压缩前。
- **#50739** (system event priority/bypass-queue) — 在会话队列拥堵时注入系统事件，提升告警可靠性。
- **#48874** (multi-session architecture: shared LLM + isolated sessions + public knowledge base) — 多会话架构RFC，属于长期演进。

**路线图信号**：社区对**技能生态**（#50090, #50199, #43260）和**成本控制**（#42475）呼声高，而PR #78441、#85104（fast talks auto mode）等正在为更智能的会话调度做铺垫。预计下一版本将优先解决文件名编码和MCP兼容性。

## 7. 用户反馈摘要

从今日活跃Issues的评论中提取真实痛点：

- **文件名编码混乱** (#48788)：用户在飞书等渠道收到中文文件名为乱码，PR#48578仅修复了UTF-8，但其他编码（如Shift-JIS）仍然出错，需要全局方案。
- **控制UI长期打开后卡死** (#45698)：用户报告在2026.3.12版本后，Dashboard逐渐变慢直至不可用，不限于Channels页面，怀疑是前端内存泄漏。
- **内存管理状态不一致** (#43747)：三位同事使用相同版本却出现截然不同的内存行为（有写入SQLite、有存储在文件、有完全不存储），定位为回归Bug。
- **Token用量显示为0** (#44845)：使用火山引擎编码计划时，会话上下文显示0/200k，原因是OpenClaw期望的字段与火山返回字段不一致。
- **文档与发布版本不同步** (#48920)：心跳配置中的`IsolatedSessions`字段在文档中出现但实际版本2026.3.13中没有，导致用户按文档配置失败。
- **工作路径硬编码** (#51429)：用户安装后自动生成了`/Users/wangtao`目录，疑似开发者个人路径被意外合并发布，影响非macOS用户。
- **Windows上打开配置失败** (#91536已修复)：因`Start-Process`参数错误导致无法通过Dashboard打开配置文件，今日已通过PR修复。

**满意度**：用户对项目更新频率和社区响应基本满意，但对基础稳定性（如会话混淆、内存泄漏）和国际化支持仍有强烈改进诉求。

## 8. 待处理积压

以下为长时间未更新（创建超过2周）且仍为OPEN状态的重要Issue，建议维护者优先关注：

| Issue # | 创建时间 | 摘要 | 标签 | 最后更新 |
|---------|----------|------|------|----------|
| #32473 | 2026-03-03 | Control UI要求HTTPS安全上下文 | P2, impact:auth-provider | 2026-06-08 |
| #50090 | 2026-03-19 | 社区技能开发与ClawHub | P2, impact:ecosystem | 2026-06-08 |
| #45740 | 2026-03-14 | gh-issues技能直接将issue body注入子代理提示 | impact:security, P2 | 2026-06-08 |
| #44905 | 2026-03-13 | Discord泄漏内部工具调用痕迹 | P1, impact:security, message-loss | 2026-06-08 |
| #43367 | 2026-03-11 | 多代理编排不稳定 | P1, impact:session-state | 2026-06-08

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我将基于您提供的两份详尽的社区动态摘要，为您呈现一份专业的横向对比分析报告。

***

### AI 智能体与个人 AI 助手开源生态横向对比分析报告 (2026-06-09)

**报告日期:** 2026-06-09
**分析师:** AI 智能体与个人 AI 助手领域资深技术分析师

#### 1. 生态全景

当前，个人 AI 助手与自主智能体开源生态正经历着 **“高热度、高矛盾、快速迭代”** 的成长期。一方面，社区贡献和开发者关注度达到顶峰，项目在功能扩展（如技能市场、多平台集成）和前沿模型适配（如 OpenAI GPT-5x）上竞赛式推进。另一方面，**基础稳定性**（会话、内存、成本统计）与**安全性**（密钥泄漏、工具调用暴露）问题成为普适性痛点，暴露出生态在追求功能广度时，核心工程的成熟度仍有待巩固。国际化（多编码文件名）和容器化部署（Docker）的易用性问题是阻碍项目走向大众化的主要瓶颈。

#### 2. 各项目活跃度对比

| 项目 | 活跃度状态 | Issues 更新 | PR 更新 | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | **极高**，功能与修复并行 | 500条 | 472条 | 2个小版本 (beta.3, beta.5) | **高活跃，中等稳定性**：修复效率高，但P1级Bug积压多，影响核心体验。 |
| **Hermes Agent** | **高**，进入快速修整期 | 50条 | 50条 | 0 | **高活跃，快速响应**：对P1 Bug响应迅速，部分已有PR跟进；但部分特性（如Dashboard粘贴）长期未修复。 |

**分析总结：**
- **规模差异：** OpenClaw 的社区活跃度（Issues/PR数）远超 Hermes Agent，显示出其更庞大的用户基础和开发者社区。
- **开发节奏：** OpenClaw 采用“小步快跑”的版本发布策略，快速修补关键问题。Hermes Agent 则在无发布的情况下，密集提交修复和增强PR，处于“集中攻关”状态。
- **健康度共性：** 两个项目都存在明显的 **“稳定性赤字”** —— 功能迭代快于基础质量的巩固，P1级 Bug 数量较多，是当前生态的普遍特征。

#### 3. OpenClaw 在生态中的定位

- **生态定位：** **综合性、平台化的个人AI助手框架**。OpenClaw 在功能广度、平台集成（QQ、Discord、飞书、Telegram等）和社区生态（技能市场ClawHub设计）上投入巨大，致力于成为 AI 智能体的“操作系统”级底座。
- **优势：** 极高的社区活跃度（500 Issues/472 PR）带来了快速的Bug修复和功能验证。在**多平台适配**和**社区生态构建**（如技能市场、编码统一工具）上已领先一步。
- **技术路线差异：** 相比可能更注重特定场景或技术深度的项目（如 Hermes Agent 在桌面端和多Profile的探索），OpenClaw 的技术路线更像“功能合集”，追求“大而全”。
- **社区规模：** 从数据看，OpenClaw 的社区规模、讨论密度和问题多样性远超 Hermes Agent，表明其拥有更广泛的用户基础和第三方开发者生态。

#### 4. 共同关注的技术方向

| 技术方向 | 具体诉求 | 涉及项目 |
| :--- | :--- | :--- |
| **会话稳定性与上下文管理** | 代理回复错位、会话混淆、多代理编排不稳定。 | **OpenClaw, Hermes Agent** |
| **模型适配与兼容性** | 紧跟 OpenAI 等模型的更新，修复因模型版本升级导致的功能失效（如 `invalid_provider_content_type`）。 | **OpenClaw, Hermes Agent** |
| **成本统计与预算控制** | 成本统计不准确、遗忘定价；社区呼唤 per-agent/per-skill 的成本预算功能。 | **OpenClaw, Hermes Agent** |
| **安全与隐私加固** | 密钥泄露（如 Matrix）、工具调用信息泄露（如 Discord/ QQBot 思维链泄漏）、注入攻击。 | **OpenClaw, Hermes Agent** |
| **多语言与国际化** | 文件名多编码支持（UTF-8, Shift-JIS等），尤其在飞书等非纯英文平台的附件处理。 | **OpenClaw, Hermes Agent** |
| **桌面端体验优化** | 粘贴功能、UI状态不一致、文件路径错误、多会话管理等。 | **OpenClaw, Hermes Agent** |

**核心洞察：** **会话、成本、安全** 是当前两个项目共通的三大核心痛点。这反映出，在追求智能体“能力”的同时，软件工程的“基本功”——数据一致性、资源可观测性和信息安全——已成为制约用户体验和生态健康度的最大短板。

#### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent |
| :--- | :--- | :--- |
| **功能侧重** | **平台生态**：聚焦于多平台集成（聊天、社交）、技能市场、MCP协议兼容等生态系统建设。 | **桌面与开发者工具**：更关注桌面端（Dashboard/终端）、远程开发、多Profile隔离、成本监控等深度用户场景。 |
| **目标用户** | **通用型用户与社区开发者**：希望快速拥有一个多功能、多平台的个人助手，并参与生态建设的用户。 | **高级用户与开发者**：对桌面控制、远程工作流、深度自定义和成本管控有更高要求的开发者和极客。 |
| **技术架构** | **平台解耦型**：通过MCP等协议，旨在实现模型、平台、工具的解耦，追求横向扩展。 | **深度集成型**：与系统（macOS/Windows）、桌面和应用（如Dashboard Terminal）深度集成，强调本地化和控制力。 |
| **社区治理** | **大众社区**：问题反馈、功能请求量大，覆盖面广，体现了更“草根”的社区文化。 | **核心驱动型**：社区讨论更聚焦于技术细节（如文件路径、锁冲突），开发者对话更倾向专业深度。 |

**结论：** **OpenClaw 追求广度（More Features, More Platforms），而 Hermes Agent 追求深度（Better Experience, Deeper Integration）。** 前者像一个“百货商店”，后者像一个“精品专营店”。

#### 6. 社区热度与成熟度

- **快速迭代阶段 (OpenClaw & Hermes Agent)：** 两个项目均处于**高活跃的快速迭代期**。功能请求和Bug报告密集，开发人员响应迅速，PR合并频率高。这表明项目仍有大量“未完成”的工作，从0到1的功能创新和从1到100的稳定性修复同时进行。
- **质量巩固阶段 (未观测到)：** 尚无项目进入以稳定性和性能优化为主的“质量巩固期”。P1级Bug的长期存在（如OpenClaw的#32296会话混淆，Hermes Agent的#21549 macOS死循环）说明，稳定性尚未成为首要优先级。
- **成熟度差异：** 从数据量级看，**OpenClaw 的社区规模和问题多样性远超 Hermes Agent**，这既是其社区活力的体现，也意味着其需要解决的“组织”和“优先级排序”的复杂度更高。Hermes Agent 的社区更聚焦，对核心技术问题（如macOS、成本）的讨论更深入。

#### 7. 值得关注的趋势信号

1.  **模型适配将成为常态性挑战**：随着模型发布节奏加快，API兼容性问题（如OpenClaw #90083）会频繁出现。具备**模型无关**或**协议层抽象**能力的框架将获得优势。
2.  **数据安全与隐私成为核心刚需**：工具调用泄漏、密钥泄漏等安全问题已从“注意事项”升级为“P1 Bug”。所有项目都必须将安全作为基础架构的一部分来重新设计。
3.  **多模态内容的传输与展示是痛点**：图片在会话中丢失、工具返回的`resource`类型不兼容等问题频发，说明智能体对多模态输入/输出的处理能力仍是明显短板。
4.  **“开发者体验”成为新的竞争焦点**：环境配置错误（如硬编码路径）、文档与版本脱节、插件安装失败等问题，是用户流失的主要原因。提供更好的开箱即用体验、诊断工具和文档同步，将成为项目差异化竞争的关键。
5.  **成本透明化与可预测性是用户刚需**：无论是个人用户还是企业，都需要清晰的成本统计和预算控制能力。这将成为智能体平台走向商业化应用不可或缺的一环。

**对 AI 智能体开发者的参考价值：**
- **技术选型时，不要只看功能数量，更要看其“稳定性修复”的效率和“安全响应”的及时性。**
- **优先解决“会话一致性”和“数据完整性”问题，这是所有智能体应用的基础。**
- **关注国际化和多编码处理，是项目能否走向全球市场的前提。**
- **可以考虑开发更便捷的部署工具和诊断脚本，良好的开发者体验是留住用户最直接的方式。**

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 (2026-06-09)

## 1. 今日速览

过去 24 小时内，Hermes Agent 项目保持了极高的社区活跃度：**50 条 Issue 更新**（46 条新开/活跃，4 条关闭）与 **50 条 PR 更新**（46 条待合并，4 条已合并/关闭）。虽然本日无版本发布，但大量针对 Bug 修复、安全增强和功能扩展的 PR 被密集提交，尤其是 **P1 级别的关键错误**（如 `launchd` 双进程死循环、`delegate_task` 上下文污染、macOS 26 网关启动失败）引发了核心贡献者的快速响应。社区讨论集中在 **Dashboard 粘贴功能、Matrix 网关恢复密钥泄露、桌面 UI 状态不一致**等影响日常使用的痛点。项目整体处于高活跃度、高响应状态的“快速修整期”。

## 2. 版本发布

本日无新版本发布。

## 3. 项目进展

本日共有 **4 个 PR 被合并/关闭**（数据源未列出具体 PR），同时 **46 个开放 PR** 正在积极 Review 或自测。以下为今日值得关注的开放 PR 中已推进的功能或修复：

- **系统集成与稳定性**  
  - `#42555`：为 systemd 添加 `ExecStop` 写入 planned-stop marker，避免网关在 `systemctl stop` 时被误判为崩溃。  
  - `#42553`：`kanban_db` 增加迁移安全守卫和单 worker 加锁保护，防止并发模式下的 column 冲突。  
  - `#42552`：修复 cron 任务对 MCP 的惰性初始化，避免远程 MCP 认证失败拖慢搜索类任务。

- **安全与隐私**  
  - `#42514`（Matrix 网关）：恢复密钥由日志明文输出改为写入受限权限文件，修复安全风险。  
  - `#40948`：修复本地 STT 命令模板注入漏洞，同时保持 shell 模板兼容性。

- **功能增强**  
  - `#42521`：桌面端新增可缩放、可换肤的终端侧边栏。  
  - `#42551`：核心工具搜索可配置延迟发现（`tool_search_deferred_core`），优化多工具平台的首次搜索体验。  
  - `#42550`：`web_extract` 链路增加级联后端，提升网页抓取可靠性。  
  - `#42541`：支持从仓库子目录安装插件，减少单插件仓库的维护负担。  
  - `#42542`：添加 `computer-use-linux` 到可选 MCP 目录。

- **性能与成本**  
  - `#42554`：修复成本统计严重低估问题（网关丢失 Telegram 会话 token 字段、定价别名错误等）。  
  - `#42543`：为 Firecrawl 搜索/提取加入超时上限并并行化，防止桌面端卡死 14 分钟。

> 以上 PR 均处于开放状态，但已通过自检说明，预期在未来 1-2 天内陆续合并。

## 4. 社区热点

本日评论数最多的 Issue 集中在 **Web Dashboard 与桌面端交互体验** 上：

| Issue | 标题 | 类型 | 评论数 | 链接 |
|------|------|------|--------|------|
| #27997 | Declarative Skill Protection Policy | Feature | 7 | [链接](https://github.com/NousResearch/hermes-agent/issues/27997) |
| #24860 | Dashboard Chat: Ctrl+V paste broken, image paste not supported | Bug | 6 | [链接](https://github.com/NousResearch/hermes-agent/issues/24860) |
| #34457 | s6-log lock collision in multi-container gateway | Bug | 6 | [链接](https://github.com/NousResearch/hermes-agent/issues/34457) |
| #30399 | Cannot use Matrix gateway from Docker image | Bug | 6 | [链接](https://github.com/NousResearch/hermes-agent/issues/30399) |

**分析与诉求：**
- **#24860**（Dashboard 粘贴失效）是用户日常高频操作断点，影响面广，已获 6 个 👍 反应社区高度共鸣。  
- **#34457 与 #30399** 分别反映 Docker 部署下的 s6-log 死锁和 Matrix 依赖缺失，表明 **容器化部署成熟度仍是短板**，用户期望开箱即用的 Docker 镜像。  
- **#27997** 讨论的技能保护策略分散在 6 个文件中且执行不一致，社区呼吁中心化声明的设计，可能影响后续安全模块的重构方向。

## 5. Bug 与稳定性

本日报告的 Bug 按严重程度排列如下（部分已有对应的修复 PR）：

| 严重度 | Issue | 标题 | 是否已有 Fix PR |
|--------|-------|------|----------------|
| **P1** | #21549 | `launchd` 双进程触发无限重启死循环（macOS） | 未直接对应，但 #42555 覆盖 systemd 场景 |
| **P1** | #42449 | `delegate_task` 通过共享单例污染父级 context_length | 无 |
| **P1** | #42524 | macOS 26: `launchctl` exit 5 回退到 detached 进程 | 无 |
| **P2** | #24860 | Dashboard 粘贴失败（Ctrl+V 无效、图片不支持） | 无 |
| **P2** | #34457 | 多容器共享卷 s6-log 死锁 | 无 |
| **P2** | #30399 | Matrix 网关 Docker 镜像缺 mautrix 依赖 | 无 |
| **P2** | #42405 | Memory 容量满时 `replace` 零匹配导致静默挂起 | 无 |
| **P2** | #42120 | 手动停止按钮导致不完整对话内容丢失 | 无 |
| **P2** | #42376 | macOS 26.5.1 上 plist 中 `LimitLoadToSessionType` 导致 `launchctl bootstrap` 失败 | 无 |
| **P3** | #42431 | 桌面端“文件”面板在远程模式下路径始终 ENOENT | 无 |
| **P3** | #42409 | Artifacts 面板时间戳显示为 1970 年（epoch 秒被当作毫秒） | 无 |
| **P3** | #42401 | 切换页面时未发送的 prompt 被丢弃 | 无 |

值得注意的是，**成本统计严重低估**（#42477）对应的修复 PR #42554 已于今日提交，**Matrix 恢复密钥泄露**（#42505）也已有 PR #42514 进行修复。但多个 P1 级 macOS 相关 Bug 尚未有 PR，需关注后续进展。

## 6. 功能请求与路线图信号

本日新提交的 Feature 请求和已有 PR 反映以下路线图信号：

- **安全与治理**  
  - #27997：声明式技能保护策略（P3），虽然级别不高但讨论热烈，可能进入下一个次版本。  
  - #42505（PR #42514）：Matrix 密钥安全存储，已进入实现阶段，预计随小版本包含。

- **多平台与多 Profile**  
  - #38357：桌面端侧边栏显示所有 Profile 的 Session（P3）。  
  - #42506：新增 usememos 作为官方 memory provider（P3）。  
  - #38641 与 #16675：WeCom（企业微信）适配器增加流式回复与已读回执。

- **开发者体验**  
  - #41933：Windows 核心工具自动安装与诊断脚本（P3），社区贡献了一个完整的 skill 包（`windows-env-diagnosis-skill.zip`）。  
  - #41988：为自定义本地模型提供默认采样参数配置（P3）。  
  - #42541（PR）：支持 Git 仓库子目录插件安装，降低插件分发门槛。

- **UI/UX 优化**  
  - #42521（PR）：可缩放终端侧边栏，提升桌面端多任务体验。  
  - #12020：提供开关关闭 `hermes.tool.progress` 事件输出，以便兼容 OpenAI 接口（2 条评论，提出于 4 月但仍有更新）。  
  - #42479：桌面端停止按钮后 UI 状态未清除。

结合已有 PR 来看，**矩阵安全加固、插件子目录安装、成本定价修复**极有可能是下一小版本的核心内容；而**声明式技能策略、多 profile session 浏览**等较复杂的 feature 可能排期较后。

## 7. 用户反馈摘要

从本日 Issue 评论中提炼的真实用户反馈：

| 用户痛点 / 场景 | 出处 | 关键词 |
|----------------|------|--------|
| “Dashboard 中 Ctrl+V 无效，无法粘贴代码，图片也不支持” | #24860 | 日常效率中断 |
| “Docker 运行 Matrix 网关抛出 `ModuleNotFoundError: No module named 'mautrix'`” | #30399 | 开箱即用期望 |
| “桌面端远程模式，文件面板默认显示远程 cwd 但实际读取本地，总是 ENOENT” | #42431 | 远程开发体验差 |
| “通过删除按钮删除 Discord 产生的 session，刷新后又出现” | #42422 | 数据持久化不一致 |
| “NVIDIA NIM 响应闪烁后消失，终端正常但桌面无内容” | #41898 | 前端渲染 bug |
| “Language 观测插件 spans 创建但无 token 计数和成本” | #42306 | 可观测性缺失 |
| “内存插件 mnemosyne 安装后不被识别” | #40101 | 插件发现机制问题 |
| “Cron view 不显示 script/no_agent 任务，运行历史为空” | #42433 | 功能完整性缺失 |
| “手动停止生成，已生成的内容消失” | #42120 | 数据丢失 |
| “提示语在切换页面时被丢弃” | #42401 | 用户体验落差 |

总体来看，用户对 **桌面端、容器化部署、远程模式、成本监控** 的稳定性与易用性提出了较高期望，当前版本在这些领域尚有多项未解决的回归问题。

## 8. 待处理积压

以下为重点且长期未得到回应的 Issues（创建超过 30 天且无 assignee 或尚未标记为 planned）：

| Issue | 标题 | 创建日期 | 最后更新 | 链接 |
|-------|------|----------|----------|------|
| #12020 | 如何关闭 `hermes.tool.progress` 事件输出 | 2026-04-18 | 2026-06-09 | [链接](https://github.com/NousResearch/hermes-agent/issues/12020) |
| #16675 | Wecom 优化：接收消息后立即回复确认 | 2026-04-27 | 2026-06-09 | [链接](https://github.com/NousResearch/hermes-agent/issues/16675) |
| #21549 | `launchd` 双进程无限重启死循环（P1，macOS） | 2026-05-07 | 2026-06-09 | [链接](https://github.com/NousResearch/hermes-agent/issues/21549) |

- **#12020** 自 4 月提出至今无官方回应，但社区持续有 +1 和讨论，建议维护者考虑在 API 配置中添加开关。  
- **#16675** 涉及 WeCom 企业用户的基础生存状态响应，虽为 P3 但已搁置两个月。  
- **#21549** 为 P1 级 macOS 致命 bug，虽然今日有 PR #42555 改善 systemd 场景，但 `launchd` 侧仍需专门修复。

请核心维护者重点关注上述积压，尤其是 P1 级别的 macOS 启动问题。

---

**报表生成日期：** 2026-06-09  
**数据来源：** Hermes Agent GitHub 仓库（NousResearch/hermes-agent）  
**分析师：** AI 智能体与个人 AI 助手领域开源项目分析师

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*