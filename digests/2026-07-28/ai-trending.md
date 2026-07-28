# AI 开源趋势日报 2026-07-28

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-28 02:07 UTC

---

# 🧠 AI 开源趋势日报（2026-07-28）

## 今日速览

今日 GitHub Trending 榜上涌现多个 AI 相关新项目，**AI Agent 技能**（如 `last30days-skill`、`claude-video`）和**大模型应用落地**（金融领域 `Kronos`、代码审查 `open-code-review`）成为焦点。主题搜索中，**RAG 与向量数据库**依旧占据统治地位，`dify`、`open-webui` 等平台持续霸榜，同时**轻量级 Agent 框架**（如 `atomic-agents`、`PocketFlow`）和**多模态交互**（`airi`、`browser-use`）获得社区密集关注。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

- **[langgenius/dify](https://github.com/langgenius/dify)** ⭐150,465｜RAG 与 Agent 构建平台，支持模型编排、多工具集成，社区最流行的 AI 应用底座之一。
- **[tensorflow/tensorflow](https://github.com/tensorflow/tensorflow)** ⭐196,577｜经典 ML 框架，持续更新，适合生产级训练与推理。
- **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐163,047｜模型定义框架，覆盖文本/视觉/多模态，是 LLM 生态的核心工具。
- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐177,033｜本地大模型运行工具，支持 Kimi、DeepSeek、Qwen 等，CLI 友好。
- **[headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom)** ⭐62,800｜面向 Agent 的 token 压缩库，可减少 20%～95% 的输入 token，提升效率。
- **[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)** ⭐8,075（[topic:llm-model]）｜Rust 编写的模块化 LLM 应用框架，适合高性能场景。
- **[samchon/nestia](https://github.com/samchon/nestia)** ⭐2,172（[topic:llm-model]）｜NestJS 辅助库，支持 AI Chatbot 快速开发。

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐185,718｜最知名的自主 Agent 项目，推动 AI 自动化任务执行。
- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** ⭐107,035｜让 AI Agent 直接操作浏览器的开源工具，Web 自动化杀手级项目。
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐221,446｜可成长的 Agent 框架，支持技能学习与自我进化。
- **[alibaba/open-code-review](https://github.com/alibaba/open-code-review)** ⭐0 (+979 today)｜阿里巴巴开源的代码审查 Agent，结合确定性规则与 LLM，精准行级评论。
- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** ⭐0 (+240 today)｜AI Agent 技能：跨平台（Reddit、X、YouTube等）搜索并综合输出摘要。
- **[CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)** ⭐36,321｜前端 Agent 框架，支持 React/Angular/Mobile 等，即插即用。
- **[Eigenwise/atomic-agents](https://github.com/Eigenwise/atomic-agents)** ⭐6,093（[topic:llm-model]）｜“原子级”Agent 构建库，强调模块化与可组合性。

### 📦 AI 应用（具体产品、垂直场景解决方案）

- **[moeru-ai/airi](https://github.com/moeru-ai/airi)** ⭐0 (+572 today)｜自托管的 Grok 风格 AI 伴侣，支持实时语音聊天、Minecraft/Factorio 游戏操控。
- **[pbakaus/impeccable](https://github.com/pbakaus/impeccable)** ⭐0 (+847 today)｜AI 辅助设计语言，让 Agent 生成更精美的 UI。
- **[bradautomates/claude-video](https://github.com/bradautomates/claude-video)** ⭐0 (+434 today)｜让 Claude 具备视频理解能力：下载、提取帧、转录后交由 LLM 分析。
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐49,053｜AI 生产力工作室，集成智能聊天、自主 Agent 与 300+ 助手。
- **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** ⭐99,576｜AI 一键生成短视频，关键词/主题驱动，自动化工作流。
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐41,435｜AI 将文档/主题转化为原生 PPT，支持图表、动画和语音旁白。
- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐59,262｜LLM 驱动的多市场股票分析系统，含行情、新闻、决策看板。

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

- **[shiyu-coder/Kronos](https://github.com/shiyu-coder/Kronos)** ⭐0 (+441 today)｜金融领域基础模型，专注市场语言理解，今日 Trending 热榜新项目。
- **[jingyaogong/minimind](https://github.com/jingyaogong/minimind)** ⭐53,906｜从零训练 64M 参数 LLM，仅需 2 小时，教育级项目。
- **[rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)** ⭐99,984｜从零实现 ChatGPT 风格 LLM，PyTorch 手把手教程。
- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,240｜LLM 评估平台，支持 100+ 数据集和主流模型。
- **[Picovoice/picollm](https://github.com/Picovoice/picollm)** ⭐316｜设备端 LLM 推理引擎，基于 X-Bit 量化，适合边缘场景。

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

- **[open-webui/open-webui](https://github.com/open-webui/open-webui)** ⭐146,984｜用户友好的 RAG 界面，支持 Ollama、OpenAI 等后端。
- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐86,174｜领先的开源 RAG 引擎，融合 Agent 能力，构建 LLM 上下文层。
- **[Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm)** ⭐63,983｜本地优先的 RAG 平台，支持多种LLM，强调数据所有权。
- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐45,391｜高性能云原生向量数据库，专为大规模 ANN 搜索设计。
- **[qdrant/qdrant](https://github.com/qdrant/qdrant)** ⭐33,613｜高可用向量搜索引擎，支持云端和自部署。
- **[NirDiamant/RAG_Techniques](https://github.com/NirDiamant/RAG_Techniques)** ⭐28,842｜RAG 技术教程集合，涵盖多种高级检索增强方法。
- **[lancedb/lancedb](https://github.com/lancedb/lancedb)** ⭐11,008｜嵌入式多模态检索库，轻量级 RAG 基础设施。

---

## 趋势信号分析

**1. “Agent + 工具调用”成为今日最热方向。**  
Trending 榜单中 `open-code-review`（+979 stars）、`last30days-skill`（+240）、`claude-video`（+434）均属于 Agent 结合具体工具的垂直案例。社区不再满足于纯对话，而是希望 Agent 能执行代码审查、视频分析、社交媒体调研等复杂任务。

**2. 金融 AI 首次登榜，专业化模型受追捧。**  
`Kronos` 作为专注金融市场的 Foundation Model 今日新增 441 stars，表明开源社区开始向垂直行业渗透。类似 `daily_stock_analysis`（59k stars）也印证了 **AI+金融** 正从实验走向实用。

**3. 轻量级 RAG 与向量数据库持续爆发。**  
`ragflow`（86k）、`anything-llm`（64k）等 RAG 平台 star 数持续增长，同时 `lancedb`、`orama` 等嵌入式/浏览器端向量数据库出现（`orama` <2kb），预示 **RAG 基础设施正在从“重型平台”向“轻量组件”分化**。

**4. 多模态交互（语音+视频+游戏）是新浪潮。**  
`airi` 支持实时语音聊天与游戏操作，`claude-video` 赋予 LLM 视频理解能力，`browser-use` 让 Agent 操作网页，这些项目反映下一波 AI 应用将是 **多模态、高交互、可编程** 的。

---

## 社区关注热点

- **💰 金融领域大模型与实践**：`Kronos` 和 `daily_stock_analysis` 双双获得高关注，提示开发者可以围绕 **行业数据 + 微调** 构建差异化应用。
- **🔧 代码审查 Agent（open-code-review）**：阿里开源的混合架构（规则+LLM）可落地于生产环境，对 DevOps 团队极具参考价值。
- **🖥️ 自托管 AI 伙伴（airi）**：强调隐私与定制化，符合“Owned AI”趋势，适合想要个性化 AI 助手的用户。
- **📽️ 视频理解技能（claude-video）**：简单但实用的 CLI 工具，为 Claude 等模型扩展视频能力，推动 Agent 从文本迈向多模态。
- **🗜️ Token 压缩（headroom）**：针对 Agent 的高 token 开销，提供即插即用的压缩方案，有望成为 Agent 应用的标配组件。

---

*报告生成时间：2026-07-28 | 数据来源：GitHub Trending & Topic Search API*

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*