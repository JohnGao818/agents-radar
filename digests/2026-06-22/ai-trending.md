# AI 开源趋势日报 2026-06-22

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-22 03:50 UTC

---

## AI 开源趋势日报（2026-06-22）

---

### 1. 今日速览

- **Agent 技能与工具链** 成为今日最热赛道：`mattpocock/skills`（+1443⭐）和 `mukul975/Anthropic-Cybersecurity-Skills`（+361⭐）将编程与安全领域的结构化技能注入 AI Agent，推动“技能即代码”范式。  
- **Token 优化** 工具 `headroom` 暴涨 2624⭐，显示社区对减少 LLM 调用成本、提升推理效率的需求极为迫切。  
- **AI 视频生成** 迎来开源爆发：`OpenMontage`（+987⭐）和 `palmier-pro`（+1834⭐）分别从智能体工作流和原生编辑器两个方向切入，象征视频生产正式进入 AI 原生时代。  
- **代码智能与记忆系统** 持续升温：`codebase-memory-mcp`（+1032⭐）以毫秒级代码知识图谱刷新 MCP 服务体验；`cognee`（+347⭐）为 Agent 提供持久化记忆层。  

---

### 2. 各维度热门项目

#### 🔧 AI 基础工具（框架 / SDK / 推理引擎 / 开发工具 / CLI）

- **[headroom](https://github.com/chopratejas/headroom)** — ⭐44,861（+2,624 today）  
  在 LLM 调用前压缩工具输出、日志、文件与 RAG 块，减少 60-95% token 且不损失答案质量。今日增长最快的项目，反映社区对推理成本控制的高度关注。

- **[codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp)** — ⭐ （+1,032 today）  
  高性能代码智能 MCP 服务器，将代码库索引为持久知识图谱，支持 158 语言、毫秒级查询，单静态二进制零依赖。为 AI 编码助手提供近乎实时的上下文理解。

- **[system_prompts_leaks](https://github.com/asgeirtj/system_prompts_leaks)** — ⭐ （+282 today）  
  持续收集 Anthropic、OpenAI、Google、xAI 等最新模型系统提示词，社区主动逆向工程以提升对 AI 行为的透明度和可调控性。

- **[rig](https://github.com/0xPlaygrounds/rig)** — ⭐7,705  
  Rust 原生的模块化 LLM 应用框架，以类型安全和零开销抽象实现高性能编排，适合对延迟敏感的生产场景。

- **[vllm/vllm](https://github.com/vllm-project/vllm)** — ⭐83,507  
  高吞吐、内存高效的 LLM 推理引擎，支持多种模型与量化方案，是企业部署大模型的首选基础设施。

---

#### 🤖 AI 智能体 / 工作流（Agent 框架 / 自动化 / 多智能体）

- **[bytedance/deer-flow](https://github.com/bytedance/deer-flow)** — ⭐72,693（+442 today）  
  字节跳动开源的长期任务 SuperAgent，集成沙箱、记忆、工具、技能、子代理与消息网关，可处理分钟至小时级复杂任务。今日登榜标志着“长周期自主 Agent”从论文走向工程。

- **[OpenMontage](https://github.com/calesthio/OpenMontage)** — ⭐ （+987 today）  
  世界首个开源 Agentic 视频制作系统，内置 12 条流水线、52 个工具、500+ Agent 技能。将 AI 编程助手直接转变为视频生产工作室，彻底重构视频创作流程。

- **[mukul975/Anthropic-Cybersecurity-Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)** — ⭐ （+361 today）  
  754 个结构化网络安全技能，映射到 MITRE ATT&CK、NIST CSF 等五大框架，兼容 Claude Code、Copilot、Cursor 等 20+ 平台。推动 Agent 技能标准化。

- **[mattpocock/skills](https://github.com/mattpocock/skills)** — ⭐ （+1,443 today）  
  来自 Claude 目录的真实工程师技能集，可直接用于增强 Claude Code、Copilot 等 Agent 的编程能力。社区将其视为“AI 技能市场”的早期范式。

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** — ⭐199,142  
  “与你一起成长的 Agent”，强调持续学习与个性化。虽非今日突增，但凭借超高星标代表社区对自适应 Agent 的期待。

- **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)** — ⭐87,853  
  多智能体金融交易框架，将 LLM 推理与量化策略结合，展示 Agent 在专业金融领域的落地潜力。

---

#### 📦 AI 应用（具体产品 / 垂直场景）

- **[palmier-io/palmier-pro](https://github.com/palmier-io/palmier-pro)** — ⭐ （+1,834 today）  
  为 AI 构建的 macOS 视频编辑器，原生集成智能剪辑、字幕、特效等。今天的新星，标志桌面端 AI 视频编辑进入开源时代。

- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** — ⭐44,779（+568 today）  
  LLM 驱动的多市场股票智能分析系统，整合多源行情、实时新闻与决策看板，支持零成本定时运行。今天新增 568⭐，印证 AI+金融的持续热度。

- **[koala73/worldmonitor](https://github.com/koala73/worldmonitor)** — ⭐ （+163 today）  
  实时全球情报面板，用 AI 聚合新闻、监控地缘政治与基础设施，为分析人员提供统一的态势感知界面。

- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** — ⭐29,986  
  AI 根据文档自动生成可编辑的 PowerPoint，支持原生形状动画、语音旁白，已与主流 LLM 集成。今日虽未在 Trending 前列，但作为应用工具长期受关注。

---

#### 🧠 大模型 / 训练（模型权重 / 训练框架 / 微调）

- **[huggingface/transformers](https://github.com/huggingface/transformers)** — ⭐161,781  
  模型定义与生态总枢纽，支持文本、视觉、音频、多模态模型。今天没有新增高峰，但仍是训练和推理的基石项目。

- **[stable-pretraining](https://github.com/galilai-group/stable-pretraining)** — ⭐266  
  可靠的预训练轻量库，专注于基础模型与世界模型的稳定训练，适合中小团队尝试自研模型。

- **[testtimescaling.github.io](https://github.com/testtimescaling/testtimescaling.github.io)** — ⭐104  
  关于 LLM 测试时扩展（Test-Time Scaling）的调研项目，系统梳理“是什么、怎么做、效果如何”。反映社区对推理阶段计算扩展的关注。

- **[R-D-BioTech-Alaska/Qelm](https://github.com/R-D-BioTech-Alaska/Qelm)** — ⭐27  
  量子增强语言模型（Qelm），探索量子计算与 LLM 的交叉，虽小而新，但代表前沿探索方向。

---

#### 🔍 RAG / 知识库（向量数据库 / 检索增强 / 知识管理）

- **[cognee](https://github.com/topoteretes/cognee)** — ⭐18,715（+347 today）  
  AI Agent 的持久记忆层，基于自托管知识图谱引擎在会话间保持长期记忆。今日新增 347⭐，凸显 Agent 记忆基础设施的迫切需求。

- **[langgenius/dify](https://github.com/langgenius/dify)** — ⭐146,085  
  生产级 Agentic 工作流开发平台，集 RAG、工具调用、Agent 编排于一体，是企业构建 AI 应用的首选开源方案。

- **[open-webui/open-webui](https://github.com/open-webui/open-webui)** — ⭐142,554  
  用户友好的 AI 界面，支持 Ollama、OpenAI 等后端，内置 RAG 功能，让个人和小团队零成本搭建本地知识库。

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** — ⭐83,309  
  先进的 RAG 引擎，将检索增强与 Agent 能力融合，为 LLM 提供优质上下文层。

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** — ⭐59,067  
  通用 AI Agent 记忆层，自动捕获、压缩并注入历史上下文，适用于 Claude Code、OpenCode 等主流 Agent CLI。

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** — ⭐44,878  
  高性能云原生向量数据库，支撑大规模 ANN 搜索，是 RAG 系统的核心存储组件。

---

### 3. 趋势信号分析

**① 爆发性关注：Agent 技能与上下文压缩**  
`headroom`（+2624⭐）和 `mattpocock/skills`（+1443⭐）分别代表两个方向：**减少 token 成本** 和 **复用结构化技能**。前者指向 LLM 推理的经济化，后者指向 Agent 能力的标准化。两者均属于 AI 工程化中的“基础设施级”缺失，社区急迫需要。

**② 新兴方向首次登榜：Agentic 视频制作**  
`OpenMontage` 和 `palmier-pro` 同时登上 Trending，且各自获得近千星标。这表明 **AI 视频生产从“生成”走向“编排”**——不再是简单的 Text-to-Video，而是完整的 Agentic 工作流（调用工具、管理资产、实时编辑）。这与近期多家厂商发布视频生成模型的背景高度吻合（如 Sora 开源、Runway 等），开源社区正在抢占“视频生产操作系统”的生态位。

**③ 代码智能 MCP 服务器爆发**  
`codebase-memory-mcp` 以+1032⭐宣告“代码知识图谱”成为 MCP 协议下的热门场景。结合 `deer-flow` 的长周期 Agent 框架，可见 **AI 编程辅助正从“单次补全”升级为“长期上下文记忆的自主代理”**。这一趋势与 Anthropic 近期发布 Claude Code 以及 MCP 规范的推广直接相关。

**④ 提示工程转向反工程**  
`system_prompts_leaks` 持续收集顶尖模型的系统提示，今日新增 282⭐。这反映出开发者对 AI 行为透明度的高度需求，也预示着**提示工程可能向“提示审计”和“逆向工程”演化**，甚至催生新的安全与合规工具。

---

### 4. 社区关注热点

- 🔥 **`headroom` 引领 Token 压缩领域**：如果能在不影响回答质量的前提下实现 60-95% 的 token 削减，将彻底改变 RAG 和 Agent 调用计费模式。建议所有使用 LLM 的应用团队关注并测试集成。

- 🎬 **`OpenMontage` 与 `palmier-pro` 推动视频 AI 开源化**：视频生成门槛极高，而这两款工具将视频制作流程智能体化与编辑器化，适合想做视频方向应用的开发者尝试。

- 🧰 **`mattpocock/skills` + `mukul975/Anthropic-Cybersecurity-Skills` 开启技能 marketplace 先河**：标准化技能文件（`.claude` 目录等）意味着 Agent 能力可以像 npm 包一样共享，建议关注技能格式的演进。

- 🧠 **`cognee` 与 `mem0` 竞夺 Agent 记忆层标准**：Agent 记忆是长期自主运行的关键瓶颈，这两个项目分别从知识图谱和压缩注入切入，值得比较选型。

- 🛡️ **`system_prompts_leaks` 揭示安全与合规需求**：随着企业部署 AI Agent，知晓底层 prompt 以避免被注入或泄露敏感信息成为刚需，该仓库可作为 prompt 审计的参考基线。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*