# AI CLI 工具社区动态日报 2026-10-21

> 生成时间: 2026-10-21 03:06 UTC | 覆盖工具: 2 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI CLI 工具横向对比分析报告  
**数据日期：2026-10-21｜对比对象：Claude Code、OpenAI Codex**  
> 注：以下数据基于给定日报摘要口径；Codex 的 PR 摘要仅展示前 6 条细节，表格以“摘要覆盖/列出”标注，避免将精选条数等同于全量。

---

## 1. 生态全景

当前 AI CLI 工具已从“代码补全/问答入口”演进为**代理运行时与开发工作流平台**，竞争焦点从模型能力转向权限、成本、会话状态与企业集成。两家社区都在高频迭代，但问题类型高度集中：**静默失败、权限不可解释、跨平台不一致、配额与上下文计量**。  
Claude Code 以正式版节奏推进桌面端、沙箱与组织策略，OpenAI Codex 则以 Rust/app-server/MCP 基础设施和 alpha 高频迭代为主。整体看，AI CLI 的“可用性”已不是主要矛盾，**可观测、可治理、可预期**正在成为下一阶段的分水岭。

---

## 2. 各工具活跃度对比

| 工具 | Release 情况 | Issues 摘要口径 | PR 摘要口径 | 今日社区主信号 |
|---|---|---|---|---|
| **Claude Code** | **v2.1.305 正式版 1 个**；新增 `sandbox.allowNestedUserNamespaces`、无人值守重试限流复查参数 | 日报覆盖 **50 条更新 Issue** 并归纳；列出 Top10 + 4 条扫读。最高声量 #87647：19 评论 / **105 👍** | 过去 24h **仅 3 条 PR 更新**，均为 OPEN 且全部列出 | 桌面端回归、Issue 自动关闭治理、沙箱安全取舍、Bedrock 自定义 CA 回归 |
| **OpenAI Codex** | **0.164.0-alpha.8 / alpha.7 两个 alpha**，均无 changelog | 覆盖 **50 条中的 30 条**；精选 10 个主条目（含容量错误 5 条、安全误报 3 条子项）+ 3 条补充。最高赞 #52483：**16 👍** | 覆盖 **50 条中的 20 条**；精选 10 条，摘要展示前 6 条；`copyberry[bot]` 当日批量 CLOSED 约 20 个变更 | 跨端“模型容量不足”爆发、Windows 权限/队列状态缺陷、MCP OAuth 与企业授权、Rust 内存/克隆优化 |

**简要结论：**  
- **Claude Code**：正式版发布稳定，但 PR 活跃度低，社区讨论更集中在产品回归与治理信任。  
- **OpenAI Codex**：PR 吞吐显著更高，处于基础设施快速硬化期；但 alpha 无 changelog、严重缺陷集中在 Windows 与容量路由层。

---

## 3. 共同关注的功能方向

多个工具社区同时指向以下方向：

1. **权限/安全策略的可解释性与可恢复性**
   - **Claude Code**：#103895 Auto mode 分类器无解释拦截 Terraform Cloud apply；#103101 要求分类器拒绝时弹出人工授权；v2.1.305 的嵌套 user namespace 明确以削弱文件保护换兼容性；PR #99540 将组织策略覆盖到个人插件。
   - **OpenAI Codex**：#40125 Full Access 子线程被静默降级为 managed approval；#49453 浏览器显式放行仍被历史拒绝记录阻断；#47001/#42728/#55699 安全审查误报且拒绝状态会“传染”到后续请求。
   - **共同诉求**：拒绝要说明原因、提供人工兜底和撤销入口；组织策略应可审计、可继承。

2. **成本、配额与上下文计量治理**
   - **Claude Code**：#76272 周限额重置时间可控，34 👍；#99560 模型重复同类错误导致 token 超耗。
   - **OpenAI Codex**：#53309 reasoning 重复计数导致过早 auto-compaction；#38495 长命令静默降级为轮询，单任务烧掉 3460 万 tokens；#52483 “More details”消失影响 token/耗时可观测性；跨端容量错误集中爆发。
   - **共同诉求**：从“能不能用”转向“可预期地用”，需要成本熔断、用量透明和配额路由可解释。

3. **会话/任务状态机与静默失败**
   - **Claude Code**：#98910 云会话空闲唤醒后恢复到 `/clear` 之前旧对话；#102949 后台 Hook 继承陈旧终端标识；#103894 `/goal` 评估器自相矛盾。
   - **OpenAI Codex**：#49027 已回答 prompt 仍留在队列阻塞后续提交；#50812 超时请求占满 RPC 槽；#51790 `send_message_to_thread` 方法绑定丢失。
   - **共同诉求**：状态要可观测、可恢复；静默降级比直接报错更伤信任。

4. **Windows / WSL / 跨平台一致性**
   - **Claude Code**：#66535 Windows ARM64 / Snapdragon 上 Cowork 沙箱无法就绪；#103896

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据截止**：2026-10-21 ｜ **数据源**：github.com/anthropics/skills

> **数据说明（重要）**：PR 列表的「评论数」字段全部为 `undefined`、👍 均为 0，因此无法据评论量对 PR 做真实排名。本期 PR 排行改用**关联 Issue 热度、更新活跃度、影响面（受影响的 Skill 与用户群）**作为替代指标；Issues 部分则可按评论数严格排序。

---

## 一、热门 Skills 排行（PR）

| 排名 | PR | Skill / 功能 | 讨论热点 | 状态 |
|---|---|---|---|---|
| 1 | [#1742](https://github.com/anthropics/skills/pull/1742) | **mcp-builder**：适配 `mcp>=2.0.0`（`streamable_http_client` 重命名、custom headers 改走 `create_mcp_http_client`） | 随 MCP SDK 主版本升级，`mcp-builder` 的连接脚本整体失效；关联 Issue #1668，属"被生态上游打断"的强制迁移 | OPEN（10-08 更新） |
| 2 | [#1961](https://github.com/anthropics/skills/pull/1961) | **skill-creator**：加固 eval viewer（脚本逃逸、DNS rebinding、跨站 POST、转义） | 评审页渲染的是**模型生成内容**（不可信），本地 HTTP server 成为攻击面；与 Issue #1394 的 XSS 同源 | OPEN（10-11 更新） |
| 3 | [#1298](https://github.com/anthropics/skills/pull/1298) | **skill-creator**：隔离 trigger evals，修复 Windows 与运行时失败 | 触发率评测假阴性、Windows 上 `select()` 失效、运行崩溃被误判为"未触发"，直接污染描述优化结果 | OPEN（09-16 更新） |
| 4 | [#1997](https://github.com/anthropics/skills/pull/1997) | **skill-creator**：正确解析 YAML frontmatter 标量 | 手写解析器 strip 引号/拼接续行，导致评测与描述优化拿到的 metadata 与 `SKILL.md` 不一致（含转义与闭合引号丢失） | OPEN（10-19 更新，最新活跃） |
| 5 | [#1245](https://github.com/anthropics/skills/pull/1245) | **notion-spec-to-implementation** + **quantitative-resume-auditor**（双 Skill 新增） | 把 Notion 规格页拆成带验收标准的可执行任务，是"规格 → 实现"闭环的代表性新增 | OPEN（10-15 更新） |
| 6 | [#1703](https://github.com/anthropics/skills/pull/1703) | **md2video-audio**：Markdown → Marp 幻灯片 → MP4 + 拟人配音 | "零成本"内容生产管线，媒体生成类 Skill 的典型诉求 | OPEN（09-15 更新） |
| 7 | [#1771](https://github.com/anthropics/skills/pull/1771) | **proofcore-contract-auditor**：Solidity/Rust 合约静态分析 + TON 链上审计存证 | Web3 垂直场景；但强绑定提交方自有协议（ProofCore Merkle），存在**商业推广型 PR** 的信任疑虑 | OPEN（09-16 更新） |
| 8 | [#525](https://github.com/anthropics/skills/pull/525) | **pyxel**：Python 复古游戏开发（headless 输入驱动、逐帧检查） | 3 月提交、9 月仍在更新，是"高质量新 Skill 长期搁置"的标本 | OPEN（09-22 更新） |

**结构性观察**：前 20 条热门 PR **无一合并，全部 OPEN**。其中 skill-creator 相关 4 条、文档类（docx/pdf）4 条 —— "修基础设施 + 修既有 Skill"已占总量的四成，超过纯新增。

---

## 二、社区需求趋势（Issues 提炼）

按评论数看，社区诉求高度集中在**三件事**，而非"再加一个 Skill"：

**1）评测与工具链的可信度（最集中，也是最高优先级）**
- [#556](https://github.com/anthropics/skills/issues/556)（13 评论 / 7👍）：`run_eval.py` 的 `claude -p` **从不触发任何 skill**，全查询 0% 触发率 —— 整个 skill 质量度量体系失去基准。
- [#1383](https://github.com/anthropics/skills/issues/1383)：skill-creator 六连 bug（目录布局与 `aggregate_benchmark.py` 不兼容、delta 反向、Windows 触发评测失败）。
- [#1390](https://github.com/anthropics/skills/issues/1390)：mcp-builder `evaluation.py` 对真实 MCP server **全部伪造为工具错误**，静默 0/N。
- [#202](https://github.com/anthropics/skills/issues/202)(CLOSED)：skill-creator 写成了"给人类看的开发文档"，违背 token 效率与操作性原则。

**2）安全与信任边界（评论量第一）**
- [#492](https://github.com/anthropics/skills/issues/492)（**46 评论**，全站最高）：社区 Skill 冒用 `anthropic/` 命名空间，构成信任边界滥用与提权风险。
- [#1394](https://github.com/anthropics/skills/issues/1394)：eval viewer 的 `escapeHtml` 非属性安全 → display-path XSS。

**3）上下文效率与 Skill 体积治理**
- [#1487](https://github.com/anthropics/skills/issues/1487)：`claude-api` 单次调用**注入约 156k tokens**，一次就耗尽上下文窗口。
- [#1329](https://github.com/anthropics/skills/issues/1329)：提议 `compact-memory`，用符号化记法压缩 agent 持久状态。

**4）分发与协作机制**
- [#228](https://github.com/anthropics/skills/issues/228)（8👍，👍最高）：希望 **Claude.ai 组织内直接共享 Skill**，而非下载 .skill 再 Slack 传文件。
- [#189](https://github.com/anthropics/skills/issues/189)（9👍）：`document-skills` 与 `example-skills` 插件内容**完全相同**，导致重复注入上下文。

**5）元能力 / 质量守门类新方向**
- [#1385](https://github.com/anthropics/skills/issues/1385) 推理质量三门

---

# Claude Code 社区动态日报 · 2026-10-21

> 数据来源：[github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)

---

## 1. 今日速览

v2.1.305 发布，新增 Linux 沙箱内嵌 user namespace 的开关和无人值守重试（unattended retry）的限流复查参数；前者在提升 Chromium / rootless podman 兼容性的同时，明确承认会削弱沙箱的文件保护边界。

社区侧，桌面端（Code tab）连续多个回归问题成为讨论中心，围绕 **侧边栏信息架构**与**功能在 macOS / Windows 间的差异**的讨论最集中；同时 #87647“6k+ 带 has repro 标签的 Issue 被自动关闭”以 105 👍 成为治理层面声量最高的议题。

---

## 2. 版本发布

### v2.1.305

- **新增 `sandbox.allowNestedUserNamespaces`**：允许 Linux 沙箱内的命令创建 user namespace，从而支持 Chromium、rootless podman 等依赖用户命名空间的负载。官方说明同时提示：该选项会让这类命令绕过沙箱的文件保护，属于**显式的安全/兼容性取舍**，建议仅在受信工作负载中开启。
- **新增 `CLAUDE_CODE_RETRY_WATCHDOG_USAGE_LIMIT_RECHECK_MS`**：为无人值守重试模式（unattended retry）提供用量限额复查间隔的可配置能力，便于 CI / 长任务场景下控制重试节奏与配额消耗。
- ⚠️ 关联观察：同日 #103680 报告 2.1.304 起 Bedrock 自定义 CA 失效（`UNABLE_TO_GET_ISSUER_CERT`，2.1.303 正常），升级前建议在自定义证书环境中先行验证。

链接：https://github.com/anthropics/claude-code/releases

---

## 3. 社区热点 Issues（Top 10）

**1. #87647 · 6k+ 带 `has repro` 标签的 Issue 自 2026-03 起被自动关闭** — 19 评论 / **105 👍**
本周声量最高的议题，已超出单一 bug 范畴，直指 **Issue 分诊与自动关闭策略的信任问题**。社区高赞说明问题在于维护者与用户对“可复现”流程的预期断裂。链接：https://github.com/anthropics/claude-code/issues/87647

**2. #12676 · [FEATURE] Claude Code 支持视频输入** — 19 评论 / **46 👍**
近一年持续活跃的多模态需求，46 👍 是目前增强类请求中的高位。反映出用户希望 Code 不只处理文本与截图，而能直接消费录屏 / 演示视频。链接：https://github.com/anthropics/claude-code/issues/12676

**3. #102142 · 桌面端 2.37337.1：侧边栏更新后 Code tab 的 Routines 区域被隐藏且每次启动重置** — 18 评论 / 13 👍
功能“消失 + 设置不持久”双重回归，直接影响依赖定时 Routine 的用户。与 #54517（Routine 运行应出现在 Recents / 可置顶）形成同一主题簇。链接：https://github.com/anthropics/claude-code/issues/102142

**4. #66535 · Windows ARM64 / Snapdragon X Plus 上 Cowork 沙箱始终无法就绪** — 16 评论 / 12 👍
ARM64 Windows 平台支持缺口，长期未收敛，对使用新款 Windows on ARM 设备的开发者属于阻断性问题。链接：https://github.com/anthropics/claude-code/issues/66535

**5. #76110 · xfce4-terminal 下 Ctrl+click 打开两个重复标签页** — 19 评论
典型 TUI 链接渲染问题（普通 `echo` 输出不受影响，说明是 Claude Code 自身的链接渲染路径），Linux 终端兼容性关注度持续。链接：https://github.com/anthropics/claude-code/issues/76110

**6. #76272 · 周限额重置时间可控（可配置重置日 / 类似 Codex 的“银行式”按需重置）** — 8 评论 / **34 👍**
成本与配额治理方向的高赞需求，作者明确指出早期同类请求 #11360 未获实质分诊，说明该诉求长期积压。链接：https://github.com/anthropics/claude-code/issues/76272

**7. #103680 · Bedrock：自定义 CA 已加载但未被使用，`UNABLE_TO_GET_ISSUER_CERT`（2.1.303 → 2.1.304 回归）** — 3 评论
企业内网 / 私有 CA 场景的严重回归，直接影响 Bedrock 用户升级意愿，属于需要尽快回归验证的类型。链接：https://github.com/anthropics/claude-code/issues/103680

**8. #90800 · 无头 Linux 上除 `--version` 外所有子命令无限挂起** — 2 评论
native 与 npm 安装均复现，零 stdout 输出。服务器 / CI 场景的阻断性缺陷，复现条件清晰。链接：https://github.com/anthropics/claude-code/issues/90800

**9. #98910 · 云会话在空闲唤醒（VM 重启）后恢复到 `/clear` 之前的旧对话** — 2 评论 / 2 👍
上下文一致性缺陷：`/clear` 语义在云端会话中失效，可能导致模型基于错误历史继续工作，对云端长任务风险较高。链接：https://github.com/anthropics/claude-code/issues/98910

**10. #103895 · Auto mode 分类器拦截用户明确要求的操作（Terraform Cloud apply）且无解释** — 0 评论（新）
与 #103101（分类器拦截时应弹出权限提示而非直接拒绝）构成同一设计议题：**Auto mode 的可解释性与人工兜底**。链接：https://github.com/anthropics/claude-code/issues/103895

**其他值得快速扫读**
- #94710 桌面端会话满意度调查无用户级关闭开关：https://github.com/anthropics/claude-code/issues/94710
- #102949 后台会话 Hook 继承守护进程的陈旧终端标识（`ZELLIJ_PANE_ID` / `TMUX_PANE`）：https://github.com/anthropics/claude-code/issues/102949
- #103896 Windows 桌面端缺失 macOS 上的 git 分支 / PR / 合并状态图标：https://github.com/anthropics/claude-code/issues/103896
- #99560 模型重复同类错误导致 token 超耗：https://github.com/anthropics/claude-code/issues/99560

---

## 4. 重要 PR 进展

> 说明：过去 24 小时内仓库仅有 **3 条** PR 更新（均为 OPEN、无公开评论数），以下全部列出，暂不足 10 条。

**1. #21459 · feat(hookify): 增加 `glob_match` 支持与大小写敏感控制** — @tianrking
为 hookify 规则增加基于 glob（如 `*.py`）的路径匹配，并提供 `case_sensitive` 选项。动机是避免为简单路径匹配编写过度复杂的正则，同时满足需要区分大小写的场景。属长期挂起的工具链增强。链接：https://github.com/anthropics/claude-code/pull/21459

**2. #99141 · diff：尚无可绘制该 pane 的宿主时保留 pane，具备条件后立即显示** — @poteat
修复 `/diff` 在宿主页面尚未 attach 时被丢弃的问题：pane 会被保留，一旦有渲染能力即刻呈现。基于 #99118 叠加（stacked）。改善 TUI / 多宿主场景下的交互一致性。链接：https://github.com/anthropics/claude-code/pull/99141

**3. #99540 · sec-default：组织对工具设定的上限，覆盖用户自行安装的插件** — @poteat
当组织要求某连接器工具必须审批时，policy mod 现在将该上限延伸覆盖到个人安装的插件，且所有判定 hook 均带 `.catch` 兜底。方向是**收紧插件生态的权限逃逸面**，与今日 v2.1.305 的沙箱话题同属安全治理主线。链接：https://github.com/anthropics/claude-code/pull/99540

---

## 5. 功能需求趋势

从 50 条更新 Issue 中可归纳出六条主线：

| 方向 | 代表 Issue | 观察 |
|---|---|---|
| **桌面端 / IDE 侧边栏信息架构** | #102142、#54517、#93058、#98654、#102116、#103896 | 最密集的需求簇：嵌套分组、Routine 可置顶、归档可见性、分支/PR 状态图标。核心诉求是“会话规模变大后如何组织与定位” |
| **多模态输入** | #12676（视频）、#103553（桌面端 push-to-talk 语音） | 视频为长期高赞请求；语音则呈现“终端已有、桌面端缺失”的功能落差 |
| **成本与配额治理** | #76272、#99560 | 从“能不能用”转向“可预期地用”：重置时机可控、重复犯错的 token 追责 |
| **权限 / Auto mode 可解释性** | #103101、#103895 | 分类器拒绝应升级为人工授权提示，且需给出理由，否则形成“静默阻断” |
| **企业网络与证书** | #103680、#68941 | Bedrock + 自定义 CA、Stripe 支付风控，均为企业落地摩擦点 |
| **平台一致性（Windows / ARM64 / 云端）** | #66535、#93522、#102573、#103896、#98910 | Windows 桌面与 ARM64 长期落后于 macOS；云端会话状态机存在语义缺陷 |

---

## 6. 开发者关注点

1. **自动化链路的“静默失败”最受诟病。** Auto mode 分类器无理由拒绝（#103895）、后台 Hook 拿到错误终端标识（#102949）、`/goal` 评估器自相矛盾地返回 `met:false`（#103894）、云会话 `/clear` 被回滚（#98910）—— 共同点是**行为不可观测、原因不可解释**，比直接报错更消耗信任。
2. **回归质量与发布节奏。** 2.1.303 → 2.1.304 的 Bedrock 证书回归、桌面端侧边栏改动引发的连锁回归（Routines 消失、归档入口丢失），使开发者倾向于“先观望再升级”，并希望 changelog 明确标注破坏性变更。
3. **Issue 治理信任危机。** #87647 的 105 👍 表明社区对自动关闭“已可复现”Issue 的做法强烈不满，实质诉求是**可见的分诊承诺**（谁看、多久、如何复开）。
4. **macOS 与 Windows 桌面端的功能差异。** git/PR 状态图标、插件生效情况、Cowork 沙箱可用性在两端不一致，Windows 用户尤其感到被边缘化。
5. **沙箱安全边界的取舍需要更明确指引。** 新增 `allowNestedUserNamespaces` 直接以削弱文件保护为代价换取兼容性，配套的组织级策略默认值（参见 PR #99540）与告警提示将成为实际落地关键。
6. **多模态与语音是下一波体验竞争点。** 终端 `/voice` 的顺滑体验已形成预期，桌面端缺失反而放大了落差（#103553）。

---

*本日报由 GitHub 公开数据自动汇总与人工整理生成，Issue/PR 状态以仓库实时信息为准。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-10-21

> 数据源：[github.com/openai/codex](https://github.com/openai/codex)｜覆盖过去 24 小时 Releases、50 条 Issue 中的 30 条、50 条 PR 中的 20 条

---

## 一、今日速览

今日没有功能性版本发布，只有 0.164.0 的两个连续 alpha 快照（无变更说明），迭代节奏以内部重构为主。社区侧问题集中在两处：**跨平台“Selected model is at capacity”报错**在 Desktop、CLI、Cloud Web 上同时爆发，以及 **Windows 桌面端的权限状态机、会话状态缺陷**（线程被静默降级、浏览器授权被缓存拒绝、队列卡死）。PR 侧由 `copyberry[bot]` 单日批量合并约 20 个 CLOSED 变更，主线是 **MCP 生态（OAuth 协调、企业授权、工具定义复用）与 Rust 侧内存/克隆开销优化**。

---

## 二、版本发布

仅有两个 alpha 版本，release note 均为空（只有版本号本身），推测为 CI 自动发布的构建快照：

- **rust-v0.164.0-alpha.8** — [Release](https://github.com/openai/codex/releases)
- **rust-v0.164.0-alpha.7** — [Release](https://github.com/openai/codex/releases)

📌 解读：同日连发两个 alpha 且无 changelog，说明 0.164 处于高频内部迭代期。值得注意的是，社区报告的严重问题（如 #53309 的 reasoning 重复计数）集中在 `0.162.0-alpha.*` 上，0.164 是否修复尚无公开说明，**升级前建议自行验证上下文计数行为**。

---

## 三、社区热点 Issues（精选 10 条）

### 1. [#40125](https://github.com/openai/codex/issues/40125) Codex Desktop 间歇性将 Full Access worktree 子线程降级为 managed approval mode
`bug / windows-os / sandbox / subagent / app-server`｜27 评论 · 👍5 · 持续 2 个月
`create_thread` 在创建子代理线程时会**静默降低权限等级**。这是权限模型层面的不一致，直接影响无人值守场景下的 subagent 编排：用户在 UI 上看到的是 Full Access，实际执行却受审批拦截。27 条评论、跨两个月仍未关闭，说明问题难以复现且涉及 worktree 与子线程权限传递的架构缺陷。

### 2. [#49453](https://github.com/openai/codex/issues/49453) 显式放行站点后，浏览器访问仍被 chat 级历史拒绝记录阻断
`bug / windows-os / browser`｜27 评论 · 👍3
聊天级别的 denial 记录**优先级高于全局 allow**，导致用户无法通过显式授权恢复访问，且没有可见的撤销入口。与 #51179、#55285 构成同一类问题（origin gate 状态机 + 无重新授权路径），是本季度 Windows 桌面端最集中的权限类缺陷族。

### 3. [#51790](https://github.com/openai/codex/issues/51790) `send_message_to_thread` 报错 `'sendRequest.bind' is not a function`
`bug / tool-calls / app / app-server`｜24 评论 · 👍2
app-server 的 RPC 实现在 macOS 桌面端直接抛 TypeError，导致跨线程消息投递完全不可用。这类"方法绑定丢失"通常来自序列化/透传层的重构回归，是 app-server 作为公共接口层稳定性的直接信号。

### 4. [#22185](https://github.com/openai/codex/issues/22185) Windows + WSL workspace：`unified_exec` 尝试 `CreateProcess /bin/bash` 失败（ENOENT）
`bug / windows-os / tool-calls`｜18 评论 · 👍10（高赞）
典型的混合宿主环境路径解析错误：命令应以 WSL 上下文执行，却被 Windows CreateProcess 接管。**👍10 的高赞说明 WSL 开发流是主流工作方式**，该问题直接阻断 Windows 用户使用 Linux 工具链，价值很高。

### 5. [#53309](https://github.com/openai/codex/issues/53309) 历史 reasoning 在 0.162.0-alpha.17.2 中被重复计数，触发过早 auto-compaction
`bug / rate-limits / context`｜17 评论 · 👍8
上下文用量统计虚高，导致远未达到上限就触发自动压缩，**直接损失有效上下文并影响长任务质量**。这类计量 bug 对 Pro Max 用户尤其敏感，因为压缩后的降质是不可逆的。

### 6. [#38495](https://github.com/openai/codex/issues/38495) code-mode `exec` 将长命令静默降级为全上下文模型轮询，任务完成后烧掉 3460 万 tokens
`bug / exec / rate-limits / tool-calls`｜11 评论 · 👍7
`exec` 超时后被"停放"为编号 cell，且**没有完成通知或定时器**，模型只能反复 `wait` 轮询来获知结果——单任务 34.6M tokens 的成本事故。这是"异步执行 + 模型主动轮询"设计缺陷的教科书案例，也暴露了 CLI 缺少成本熔断机制。

### 7. [#52483](https://github.com/openai/codex/issues/52483) macOS 更新后响应选择菜单中的 "More details" 消失
`bug / app`｜14 评论 · 👍16（全站最高赞）
纯 UI 回退，但 16 个赞说明这个入口使用频率很高。用户无法查看详细的 token/耗时/工具调用信息，属于**可观测性能力的退化**，与 #38495 的成本问题形成呼应。

### 8. [#49027](https://github.com/openai/codex/issues/49027) Windows app：已投递并已回答的 prompt 仍留在队列，阻塞后续提交
`bug / windows-os / app`｜15 评论 · 👍1
队列中的陈旧条目无法自动清理，必须手动删除才能继续对话——**会话状态机没有正确 mark-done**。这类问题会让用户误以为是网络或模型问题。

### 9. 模型容量错误全线爆发：`Selected model is at capacity` 跨平台复现
- [#53569](https://github.com/openai/codex/issues/53569) Desktop / Web / CLI 三端均报错，配额充足（9 评论 · 👍4）
- [#55260](https://github.com/openai/codex/issues/55260) Windows Desktop + CLI v0.161.0 + Cloud Web 全部失败（4 评论）
- [#52894](https://github.com/openai/codex/issues/52894) 同一台 Mac 上 A 账号失败、B 账号正常（4 评论）
- [#55305](https://github.com/openai/codex/issues/55305) ChatGPT 订阅下持续报错，但同一客户端的 API provider 正常（4 评论）
- [#55526](https://github.com/openai/codex/issues/55526) 附带模型质量下降的回归报告（2 评论）

`#52894` 与 `#55305` 的对照实验（同机不同账号、同客户端不同 provider）是**很强的定位线索**——问题更可能出在账号级路由/容量分配层，而非模型真实容量。这是今日社区情绪最集中的议题。

### 10. 安全审查误报开始影响正常开发流
- [#47001](https://github.com/openai/codex/issues/47001) 良性 prompt 被 cybersecurity 风险警告阻断，且警告后的中性追问也继续被拦（8 评论）
- [#42728](https://github.com/openai/codex/issues/42728) 一次不透明的 Computer Use 拒绝扩散为跨工具全面拒绝，并沿 handoff 传递给后继线程（3 评论）
- [#55699](https://github.com/openai/codex/issues/55699) 用户以激烈措辞投诉同类拦截（2 评论）

关键共性是**拒绝状态的"传染性"**：一次触发会污染后续中性请求与后继线程，且缺少解释与恢复入口。这是安全策略与可用性之间最需要拿捏的边界。

> 其他值得留意的： [#55014](https://github.com/openai/codex/issues/55014) Windows 更新后本地项目列表清空、[#50812](https://github.com/openai/codex/issues/50812) 超时请求占满全部 8 个 host RPC 槽导致必须重启、[#55721](https://github.com/openai/codex/issues/55721) PowerShell 调用被拒但无策略来源信息。

---

## 四、重要 PR 进展（精选 10 条）

> 说明：以下 PR 均由 `copyberry[bot]` 于 10-21 提交并当日 CLOSED，属于内部自动化流水线的批量合入，评论数据缺失。方向高度集中于 **MCP 认证体系** 与 **Rust 侧开销削减**。

### MCP 与企业认证（主线）

1. **[#55701](https://github.com/openai/codex/pull/55701) 默认启用 MCP OAuth refresh 协调**
   将 `mcp_oauth_refresh_coordination` 标记为 stable 并默认开启。解决多连接并发刷新 token 时的竞态，是 MCP 走向生产可用的关键开关。

2. **[#55698](https://github.com/openai/codex/pull/55698) 企业 MCP 认证复用 Codex 账号授权**
   优先使用已存企业凭据，否则使用 issuer 匹配的 Codex OAuth grant，并将连接与凭据来源、OAuth client 绑定。减少企业场景下的重复授权与凭据错配。

3. **[#55696](https://github.com/openai/codex/pull/55696) 运行时刷新时保留企业 MCP 授权**
   配置重载需取消过期启动、同时保证运行中线程的可访问性；`thread/revert` 替换 runtime 后仍需能使用企业凭据。属典型的热重载状态一致性问题。

4. **[#55705](https://github.com/openai/codex/pull/55705) 云 skill 缓存状态统一收敛到 catalog 锁下**
   将缓存内容并入 `SkillCatalogState`，与 catalog 代次同锁管理，auth scope 变更时清理缓存。解决鉴权切换后的**脏缓存**风险。

### MCP 工具与调用链

5. **[#55724](https://github.com/openai/codex/pull/55724) 跨 session 共享已准备的 MCP 工具定义**
   把不可变的 MCP 工具元数据与规范化 schema 从 per-handler 缓存中拆出复用，避免同一 catalog 下重复做 schema 归一化并消除重复 spec 内存占用。多 MCP server 用户会感受到启动与内存改善。

6. **[#55710](https://github.com/openai/codex/pull/55710) 从运行时事件解析 MCP backend 身份**
   修复按名字分类 MCP 调用的误判：命名空间/tool 名可能与 backend 身份

</details>

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*