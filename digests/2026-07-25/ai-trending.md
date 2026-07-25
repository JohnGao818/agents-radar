# AI 开源趋势日报 2026-07-25

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-25 02:13 UTC

---

# AI 开源趋势日报 · 2026-07-25

## 📌 今日速览

- **AI 网关爆发**：`OmniRoute` 单日新增 1841 stars，成为免费聚合 500+ 模型的“瑞士军刀”，暗示开发者对多模型调用效率的迫切需求。
- **Agent 生态持续扩张**：`hermes-agent`（220k stars）与 `Career-Ops`（61k）等 AI Agent 项目占据主题榜单前列，Agent 化工具正在渗透求职、金融、编程等垂直场景。
- **本地化与隐私优先**：`harper`（语法检查）与 `ego-lite`（Agent 专用浏览器）均强调离线运行或零成本，反映社区对数据控制权的重视。
- **小模型训练实践升温**：`dive-into-llms` 教程与 `Kronos` 金融基础模型同日登榜，显示从零训练或微调小参数 LLM 的学习需求激增。

## 🔧 各维度热门项目

### 1. 🔧 AI 基础工具（框架/推理/网关/CLI）

- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐176,814  
  本地运行 K2.6、DeepSeek、GLM 等模型的轻量推理引擎，当前最流行的本地大模型入口。

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐87,093  
  高性能 LLM 推理与服务引擎，支持 PagedAttention，是生产级部署的首选。

- **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** ⭐142,541  
  代理工程平台，统一 LLM 调用、工具链与 Agent 编排，生态最成熟的框架之一。

- **[diegosouzapw/OmniRoute](https://github.com/diegosouzapw/OmniRoute)** ⭐0（+1841 today）  
  免费 MIT AI 网关：一个端点聚合 290+ 提供商、500+ 模型，支持自动回退与压缩，今日爆发式增长。

- **[citrolabs/ego-lite](https://github.com/citrolabs/ego-lite)** ⭐0（+880 today）  
  专为 AI Agent 设计的极速浏览器，共享登录状态给 Codex/Claude Code，零成本零配置。

- **[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)** ⭐8,035  
  Rust 生态的模块化 LLM 应用框架，适合对性能要求苛刻的场景。

### 2. 🤖 AI 智能体/工作流

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐220,047  
  与你共同成长的 Agent 框架，支持记忆、工具调用与多模型，社区最活跃的 Agent 项目之一。

- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐185,682  
  自动 AI 代理开创者，让 LLM 自主分解任务并执行，持续迭代至今。

- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** ⭐106,631  
  让网站“可访问”于 AI 代理，自动化网页交互的核心库，配套 egol-lite 浏览器。

- **[HKUDS/nanobot](https://github.com/HKUDS/nanobot)** ⭐46,200  
  轻量开源 AI Agent，零依赖部署，支持工具、聊天与工作流，适合快速集成。

- **[zhayujie/CowAgent](https://github.com/zhayujie/CowAgent)** ⭐46,111  
  多模态超级 AI 助手，规划任务、调用技能、自我演化，支持多平台（原 chatgpt-on-wechat）。

- **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)** ⭐81,995  
  AI 驱动的软件开发 Agent，可自动编写代码、调试、部署。

### 3. 📦 AI 应用（垂直场景）

- **[koala73/worldmonitor](https://github.com/koala73/worldmonitor)** ⭐0（+2184 today）  
  AI 驱动的全球情报仪表盘，聚合新闻、地缘政治与基础设施跟踪，今日最热（+2184 stars）。

- **[shiyu-coder/Kronos](https://github.com/shiyu-coder/Kronos)** ⭐0（+499 today）  
  金融大语言模型基础版，专为金融市场语言设计，可能开启金融垂直 LLM 新方向。

- **[Automattic/harper](https://github.com/Automattic/harper)** ⭐0（+876 today）  
  Rust 编写、离线隐私优先的语法检查器，对标 Grammarly 但完全本地运行。

- **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** ⭐99,148  
  利用 AI 大模型自动生成高清短视频，内容创作者的效率工具。

- **[OtterMind/Chat2DB](https://github.com/OtterMind/Chat2DB)** ⭐0（+82 today）  
  AI 驱动的数据库 SQL 客户端，支持 MySQL、PG 等，自然语言查数据库。

- **[ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)** ⭐0（+663 today）  
  Claude 工作流技能精选集，降低定制化的门槛。

- **[ruvnet/RuView](https://github.com/ruvnet/RuView)** ⭐0（+1022 today）  
  将 WiFi 信号转化为空间智能与生命体征监测，无需摄像头，隐私安全。

### 4. 🧠 大模型/训练

- **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐162,950  
  🤗 模型定义与训练框架，支持文本、视觉、多模态，行业标准。

- **[jingyaogong/minimind](https://github.com/jingyaogong/minimind)** ⭐53,819  
  2 小时从零训练 64M 参数小模型，入门级 LLM 训练最佳实践。

- **[Lordog/dive-into-llms](https://github.com/Lordog/dive-into-llms)** ⭐0（+328 today）  
  《动手学大模型》中文编程教程，适合系统学习从训练到推理。

- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** ⭐4,406  
  为系统工程师定制的 LLM 推理服务课程，基于 Apple Silicon 搭建 mini vLLM。

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,235  
  全面 LLM 评估平台，覆盖 100+ 数据集，模型选型的权威工具。

### 5. 🔍 RAG/知识库

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐45,371  
  高性能云原生向量数据库，大规模 ANN 搜索与 RAG 基础设施。

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐85,929  
  领先的开源 RAG 引擎，融合 Agent 能力，为 LLM 提供优质上下文层。

- **[run-llama/llama_index](https://github.com/run-llama/llama_index)** ⭐51,073  
  文档代理与 OCR 平台，简化数据注入 RAG 流程。

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐61,635  
  通用 AI Agent 记忆层，持久化跨会话上下文，解决 Agent 无记忆痛点。

- **[NirDiamant/RAG_Techniques](https://github.com/NirDiamant/RAG_Techniques)** ⭐28,798  
  RAG 技术教程集合，覆盖高级检索、重排序、混合搜索等。

- **[Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm)** ⭐63,805  
  本地优先的 Agent 体验平台，内置文档管理、向量存储与多模型支持。

## 📈 趋势信号分析

**1. AI 网关成为新基建**  
`OmniRoute` 单日 1841 stars 表明开发者对“一次接入，多模型随意切换”的需求已从实验走向实用。配合 Claude Code、Codex 等 CLI 工具，这类网关正在成为 AI 编程工作流的“代理器热点”。

**2. Agent 专用基础设施涌现**  
`ego-lite`（Agent 浏览器）、`headroom`（token 压缩）、`mem0`（记忆层）——这些为 Agent 定制的组件相继登榜，标志 Agent 生态从“单一框架”向“分层基础设施”演进。尤其是记忆与上下文压缩，直击成本与连续性痛点。

**3. 垂直领域模型加速落地**  
金融领域的 `Kronos`、求职领域的 `Career-Ops`、智能监控的 `RuView` 均获得高关注。社区不再满足于通用模型，而是用 LLM 改造传统行业的细分场景，且倾向于开源+本地部署。

**4. 小模型训练成为新学习热点**  
`dive-into-llms`（+328 today）与 `minimind`（53k stars）的持续热度，反映开发者渴望从“API 调用者”转向“模型自建者”。随着量化与蒸馏技术成熟，在消费级 GPU 上训练小参数模型已变得可行。

## 🔍 社区关注热点

- **Agent 记忆层**：`mem0`（61k stars）和 `thedotmack/claude-mem`（88k）——让 Agent 记住跨会话内容是实现自主性的关键一步，值得深度研究其压缩与检索机制。
- **多功能 AI 网关**：`OmniRoute` 提供了免费且兼容 290+ 提供商的中转层，适合希望打破模型锁定、降低成本的团队。
- **本地 AI 语法检查**：`harper`（Rust 编写，离线）可能是隐私敏感场景下 Grammarly 的替代品，其技术路线（Rust + 离线 NLP）可迁移到其他语言工具。
- **WiFi 感知 AI**：`RuView` 利用现有信号实现空间感知，无需摄像头，在智能家居与安防领域有巨大想象空间，且完全开源。
- **金融垂直 LLM**：`Kronos` 与 `daily_stock_analysis`（58k）同期活跃，金融量化 + LLM 的结合正在形成新的开源生态，建议关注其数据标注与评估方法。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*