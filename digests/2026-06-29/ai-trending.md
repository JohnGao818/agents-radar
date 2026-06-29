# AI 开源趋势日报 2026-06-29

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-29 03:31 UTC

---

# AI 开源趋势日报  
**2026-06-29** | 分析师视角

---

## 1. 今日速览

今日 GitHub 上 AI 相关项目热度集中在 **Agent 智能体生态**与**代码智能基础设施**两大方向。`DeusData/codebase-memory-mcp` 以 +2190 stars 的惊人增速成为全天黑马，将代码库索引为持久知识图谱，直接受益于 MCP 协议的快速普及。同时，金融 AI Agent 项目（`xbtlin/ai-berkshire` +1445、`HKUDS/Vibe-Trading` +492）展现出社区对 **AI 驱动决策**的强烈渴求。RAG 领域持续进化，`safishamsi/graphify` 将知识图谱与 RAG 结合，`headroomlabs-ai/headroom` 专注 token 压缩优化。此外，离线语音识别 `altic-dev/FluidVoice` 和文档处理 `opendatalab/MinerU` 等落地应用也获得大量关注。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars | 今日新增 | 说明 |
|------|-------|----------|------|
| [DeusData/codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp) (C) | ❓ | **+2190** | 高性能代码智能 MCP 服务器，将代码库索引为持久知识图谱，支持 158 种语言，亚毫秒查询。今日最热 AI 基础项目。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) (Python) | 84.7k | — | 高吞吐、内存高效的 LLM 推理引擎，已成为生产级部署的标准选择。 |
| [ollama/ollama](https://github.com/ollama/ollama) (Go) | 175.1k | — | 一键运行多种开源大模型（DeepSeek、Qwen、Gemma 等），本地部署趋势的核心推动力。 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) (TypeScript) | 140.9k | — | 面向 AI Agent 的网页搜索与抓取 API，Agent 获取实时数据的关键基础设施。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) (Python) | 101.2k | — | 让 AI Agent 能够操作浏览器，自动化线上任务，今日其衍生项目 `video-use` 也登上 Trending。 |
| [cupy/cupy](https://github.com/cupy/cupy) (Python) | ❓ | +174 | GPU 加速的 NumPy/SciPy 替代品，虽然传统但仍是很多 ML 工作流底层依赖。 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 今日新增 | 说明 |
|------|-------|----------|------|
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) (Python) | 205.1k | — | 社区最瞩目的 “The agent that grows with you”，长期占据 AI Agent 赛道头部。 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) (Python) | 185.2k | — | 经典自主 Agent 项目，持续迭代，至今仍是 Agent 入门的标杆。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) (Python) | 78.6k | — | AI 驱动开发，让 Agent 直接写代码、调试、部署，正快速替代传统开发者工具。 |
| [langgenius/dify](https://github.com/langgenius/dify) (TypeScript) | 146.9k | — | 生产级 Agent 工作流平台，支持 RAG、工具调用、可视化编排，今日 RAG 分类中同样上榜。 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) (TypeScript) | 35.6k | — | 前端 Agent 框架，支持 React/Angular/Mobile，让 UI 层与 Agent 原生交互。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) (TypeScript) | 47.9k | — | AI 生产力工作室，集成智能聊天、自主 Agent、300+ 助手，统一调用前沿 LLM。 |
| [HKUDS/nanobot](https://github.com/HKUDS/nanobot) (Python) | 44.8k | — | 轻量级开源 AI Agent，适用于自定义工具、聊天、工作流，主打简洁易用。 |

### 📦 AI 应用（具体产品、垂直场景解决方案）

| 项目 | Stars | 今日新增 | 说明 |
|------|-------|----------|------|
| [xbtlin/ai-berkshire](https://github.com/xbtlin/ai-berkshire) (Python) | ❓ | **+1445** | AI 时代价值投资研究框架，集成四位投资大师方法论 + 多 Agent 对抗分析，引爆金融 AI 热度。 |
| [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading) (Python) | ❓ | **+492** | 个人交易 Agent，将市场情绪分析与自动交易结合，今日迅速攀升。 |
| [Robbyant/lingbot-map](https://github.com/Robbyant/lingbot-map) (Python) | ❓ | **+372** | 前馈 3D 基础模型，从流数据实时重建场景，在机器人和 AR 领域有广泛应用。 |
| [altic-dev/FluidVoice](https://github.com/altic-dev/FluidVoice) (Swift) | ❓ | **+365** | macOS 离线语音转文字应用，完全本地运行，隐私友好，Mac 用户刚需。 |
| [opendatalab/MinerU](https://github.com/opendatalab/MinerU) (Python) | ❓ | **+380** | 将 PDF/Office 文档转为 LLM 就绪的 Markdown/JSON，Agent 工作流中数据预处理利器。 |
| [browser-use/video-use](https://github.com/browser-use/video-use) (Python) | ❓ | **+196** | 用编码 Agent 编辑视频，拓展了 Agent 在多媒体创作场景的应用边界。 |
| [commaai/openpilot](https://github.com/commaai/openpilot) (Python) | ❓ | +266 | 开源驾驶辅助系统 / 机器人操作系统，社区持续优化，为 300+ 车型提供 AI 升级。 |
| [usestrix/strix](https://github.com/usestrix/strix) (Python) | ❓ | +122 | 开源 AI 黑客工具，自动发现和修复应用漏洞，AI 安全应用新方向。 |

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 今日新增 | 说明 |
|------|-------|----------|------|
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) (Python) | 52.3k | — | 2 小时从零训练 64M 小参数 LLM，降低模型训练门槛，激发大量开发者实验。 |
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) (Python) | 72.7k | — | 统一高效微调 100+ LLM/VLM（ACL 2024），微调领域最流行工具。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) (Python) | 162.0k | — | 模型定义与推理框架，支持文本、视觉、音频、多模态，AI 开发者的标准库。 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) (Python) | 271 | — | 稳定预训练基础模型库，专注于可靠、最小化、可扩展的预训练流程，代表前沿研究。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) (Python) | 7.1k | — | LLM 评估平台，支持 Llama3、Qwen、GLM、Claude 等 100+ 模型，模型比拼的权威擂台。 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 今日新增 | 说明 |
|------|-------|----------|------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) (Go) | 83.8k | — | 领先的开源 RAG 引擎，融合 Agent 能力，为 LLM 构建优质上下文层。 |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) (JavaScript) | 62.2k | — | 本地优先的 Agent 体验，一切工作围绕“拥有数据主权”展开，RAG 入门首选。 |
| [safishamsi/graphify](https://github.com/safishamsi/graphify) (Python) | 73.8k | — | 将代码、SQL、文档等任意文件夹转为可查询知识图谱，与 Claude Code 等无缝集成。 |
| [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) (Python) | 53.2k | — | 压缩工具输出、日志、RAG 块，减少 60-95% token 而不损失答案质量，最务实的 token 节省方案。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) (Python) | 59.6k | — | AI Agent 的通用内存层，跨 Session 记忆，让 Agent 具备长期记忆能力。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) (Go) | 45.0k | — | 高性能云原生向量数据库，ANN 搜索领域的事实标准。 |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) (Python) | 84.2k | — | 100+ 语言的 OCR 工具，将图像/PDF 转为结构化数据，是 RAG 管线中重要的“眼睛”。 |

---

## 3. 趋势信号分析

- **MCP 协议引爆代码智能基础设施**：`DeusData/codebase-memory-mcp` 以单日 +2190 stars 暴力登顶，验证了 **Model Context Protocol** 将成为 Agent 与代码仓库之间的事实标准。与 `thedotmack/claude-mem` 等上下文管理项目一起，共同构成“Agent 记忆层”的关键拼图。
- **金融 AI Agent 迎来爆发**：`xbtlin/ai-berkshire` 和 `HKUDS/Vibe-Trading` 分别拿下 +1445 和 +492 stars，反映社区对 **AI 辅助投资决策**的极高热情。它们并非简单的“预测股价”，而是结合多 Agent 分析、价值投资方法论，属于 **专业领域 Agent** 的成功案例。
- **RAG 向“智能压缩”演进**：`headroomlabs-ai/headroom` 和 `safishamsi/graphify` 分别从 token 压缩和知识图谱两个角度优化 RAG 效率，不再单纯依赖向量检索，而是转向“推理增强检索”。这一趋势与 LLM 上下文窗口增长但成本仍高并存，实际价值巨大。
- **离线/本地 AI 应用持续升温**：`altic-dev/FluidVoice`（离线语音）、`MinerU`（本地文档处理）、`open-webui` 等代表用户对 **数据主权和低延迟** 的追求，尤其在 macOS/边缘设备上形成新基建。
- **大模型“小而美”**：`minimind` 训练 64M 参数模型仅需 2 小时，说明开发者社区正在从盲目追求大模型转向 **可控、可训练的小模型** 研究，这与 `stable-pretraining` 等预训练库的兴起一致。

---

## 4. 社区关注热点

- 🚀 **`DeusData/codebase-memory-mcp`：代码智能的“MCP 杀手”**  
  今日最大黑马。它将 MCP 协议落地为高性能代码知识图谱，单二进制、零依赖、毫秒级查询。任何使用 Claude Code / Codex 的开发者都应关注，可能改变代码导航与 Agent 协作的方式。

- 🧠 **`NousResearch/hermes-agent`：Agent 框架的持续领跑者**  
  200k+ stars 的背后是社区对其“自生长 Agent”理念的认可。最新版本强化了多模态与工具调用能力，是研究 Agent 架构的最佳起点。

- 💰 **`xbtlin/ai-berkshire`：AI 价值投资的新范式**  
  融合巴菲特、芒格、段永平、李录四位大师方法论，加上多 Agent 对抗分析——这不是简单的量化策略，而是 AI 逻辑推理在金融领域的深度应用。对 Agent 产品化感兴趣者必看。

- 🔍 **`safishamsi/graphify`：让 RAG 理解结构化关系**  
  将任意代码、文档、数据库 Schema 转化为知识图谱，并直接集成到 Claude Code / Codex 中——本质上把 RAG 从“关键词匹配”升级到“关系推理”。适合构建企业级知识库。

- 🌐 **`firecrawl/firecrawl`：Agent 的“眼睛和耳朵”**  
  作为搜索和抓取 API，它是 Agent 获取实时互联网数据的关键中间件。今日其 `browser-use` 生态衍生出的 `video-use` 也证明了该基础设施的扩展性。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*