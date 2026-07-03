# AI 开源趋势日报 2026-07-03

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-03 02:35 UTC

---

# AI 开源趋势日报（2026-07-03）

## 今日速览

- **智能体生态持续爆发**：今日 Trending 榜单中超 70% 为 AI 智能体/代理相关项目，其中 `agency-agents` 单日涨星 3032，`strix` 安全测试工具涨 2137，社区对「可执行多步骤任务」的代理框架热情高涨。
- **Token 优化成为新热点**：`caveman` 用原始人语言风格减少 65% Token 消耗，`headroom` 将 RAG 块压缩 60-95%，两项工具分别从 prompt 和上下文层面降本，反映开发者对推理成本的敏感。
- **Agent Skill（技能）体系标准化加速**：`agentskills`、`obra/superpowers`、`affaan-m/ECC` 等专注 Agent 技能规范、性能优化和多平台兼容，显示 Agent 生态正从单一工具向可组合、可复用的技能市场演进。
- **RAG 基础设施持续升温**：主题搜索中 `dify`、`RAGFlow`、`anything-llm` 等累计星数超 10 万的巨型项目保持活跃，`headroom` 等新锐压缩工具单日破千，RAG 成本优化已成为刚需。
- **视频与金融等垂直场景 Agent 涌现**：`browser-use/video-use` 实现视频编辑代码化，`HKUDS/Vibe-Trading` 打造个人交易 Agent，AI 正快速渗透创意和金融领域。

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 101,250 (ml) / 67,250+ | +65 | 业界标准深度学习框架，GPU 加速张量运算与动态神经网络 |
| [langflow-ai/langflow](https://github.com/langflow-ai/langflow) | 47,000+ (trending) | +117 | 可视化 AI 代理和工作流构建平台，降低 Agent 开发门槛 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 140,781 | - | Agent 工程化平台，提供链式调用、工具集成等基础设施 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 85,201 | - | 高吞吐、低内存的 LLM 推理引擎，核心生产部署组件 |
| [ChromeDevTools/chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp) | 0+（新项目） | +104 | 为编码 Agent 提供 Chrome DevTools 的 MCP 协议接口，让 Agent 直接操控浏览器 |
| [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc) | 0+（新项目） | +352 | OpenAI 官方出品，让 Claude Code 调用 Codex 进行代码审查或任务委派，跨 Agent 协作标杆 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 185,289 | - | 经典自主 Agent 框架，持续迭代支持多模型与工具链 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 79,191 | - | AI 驱动的软件开发 Agent，自动编写代码、调试、部署 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 102,251 | - | 让 AI Agent 自动操作浏览器的开源方案，网页任务自动化利器 |
| [bytedance/deer-flow](https://github.com/bytedance/deer-flow) | 75,939 | - | 字节出品长周期超级 Agent，集成沙箱、记忆、技能、子 Agent，可处理小时级复杂任务 |
| [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents) | 0+（新项目） | +3032 | 一站式 AI 代理机构：包含前端、社区运营、创意等专用 Agent，模块化可组合 |
| [usestrix/strix](https://github.com/usestrix/strix) | 0+（新项目） | +2137 | 开源 AI 渗透测试 Agent，自动发现并修复应用漏洞，安全场景 Agent 标杆 |
| [agentskills/agentskills](https://github.com/agentskills/agentskills) | 0+（新项目） | +86 | Agent Skill 标准化规范，推动技能市场互操作性 |

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 48,079 | - | AI 生产力工作室：智能聊天、自主代理、300+助手，统一接入前沿 LLM |
| [santifer/career-ops](https://github.com/santifer/career-ops) | 57,911 | +372 | AI 驱动求职系统：14 种技能模式、Go 仪表盘、PDF 生成，面向求职自动化 |
| [browser-use/video-use](https://github.com/browser-use/video-use) | 0+（新项目） | +554 | 用代码 Agent 编辑视频，将视频处理工作流交给 AI 自动执行 |
| [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading) | 0+（新项目） | +939 | 个人交易 Agent，结合市场情绪与数据驱动决策，零代码部署 |
| [usestrix/strix](https://github.com/usestrix/strix) | 0+（新项目） | +2137 | （同上）AI 渗透测试安全应用 |

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | 52,481 | - | 从零训练 64M 参数 LLM 仅需 2 小时，适合学习训练全流程 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,146 | - | 开源 LLM 评测平台，支持 100+ 数据集和多模型评估 |
| [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) | 81,150 (主题搜索) | +926 今日 | 原始人语言风格提示词技能，减少 65% Token 消耗，适用于 Claude Code |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | 313 | - | 设备端 LLM 推理库，X-Bit 量化，适合边缘部署 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [langgenius/dify](https://github.com/langgenius/dify) | 147,457 | - | 生产级 RAG Agent 工作流平台，可视化编排知识库与工具 |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 143,904 | - | 用户友好的 AI 前端，支持 Ollama、OpenAI 等，内置 RAG |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 84,172 | - | 领先开源 RAG 引擎，融合 Agent 能力，为 LLM 提供上下文层 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 45,050 | - | 云原生高性能向量数据库，ANN 搜索工业标准 |
| [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) | 55,867 | - | 压缩工具输出、日志、RAG 块，减少 60-95% Token，不影响答案质量 |
| [Weaviate/weaviate](https://github.com/weaviate/weaviate) | 16,486 | - | 开源向量数据库，支持对象+向量混合搜索与云原生扩展 |
| [neo4j/neo4j?] 未收录） | - | - | 本期未在热榜，但知识图谱相关（如 `cognee` 26k+）值得关注 |

## 趋势信号分析

1. **Agent 技能标准化与降本双主线**：`caveman` 和 `headroom` 分别从 prompt 设计和上下文压缩切入，解决 Agent 调用 LLM 的核心成本问题。同时 `agentskills`、`obra/superpowers` 等推动技能可复用、可组合，预示 Agent 生态将进入“技能市场”阶段。

2. **新锐项目“单日破千”现象集中**：`agency-agents`（+3032）、`strix`（+2137）、`Vibe-Trading`（+939）等均于今日首次进入 Trending，且均为“面向任务的专用 Agent”，而非通用框架。说明社区对能立刻解决具体问题（安全、求职、交易、视频编辑）的 Agent 应用兴趣陡增。

3. **MCP 协议加速渗透**：`ChromeDevTools/chrome-devtools-mcp` 由 Google 官方推出，`openai/codex-plugin-cc` 实现跨 Agent 调用，MCP（Model Context Protocol）作为 Agent 工具接口标准正被大厂和社区采纳，可能成为 AI 交互的下层协议。

4. **与近期行业事件关联**：OpenAI 发布 Codex 插件与 Claude Code 互通，Google 开源 Chrome DevTools MCP，表明头部 AI 公司正在推动 Agent 工具链开放化。此外，`browser-use` 生态继续延伸出 video-use，反映出“Agent 操控浏览器”逐渐成为基础能力。

## 社区关注热点

- **⭐ `agency-agents`（+3032）**：当前涨势最猛的 Agent 聚合项目，提供开箱即用的多角色 Agent 团队，适合快速搭建自动化工作流。
- **🔍 `headroom`（55k+）**：RAG 成本压缩利器，与 `caveman` 的 token 优化形成互补，两者结合可将 LLM 调用费用降低 80%+。
- **📹 `browser-use/video-use`（+554）**：视频编辑 Agent 首次登榜，表明 AI 正从文本/代码向多媒体创作扩展，值得关注后续生态。
- **🛡️ `usestrix/strix`（+2137）**：安全领域稀缺的开源 AI 渗透工具，填补 Agent 在 DevSecOps 中的空白，企业级应用潜力大。
- **🔧 `ChromeDevTools/chrome-devtools-mcp`（+104）**：Google 官方发布，为 Agent 提供浏览器调试能力，将成为前端测试和爬虫 Agent 的关键基础设施。

---

*数据来源：GitHub Trending（2026-07-03）& GitHub Search API（7 天活跃 AI 主题项目），已去重。部分项目未标注 total stars 的为当日新上架仓库。*

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*