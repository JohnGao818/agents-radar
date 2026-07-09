# AI 开源趋势日报 2026-07-09

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-09 02:35 UTC

---

# AI 开源趋势日报（2026-07-09）

## 今日速览

今日 GitHub Trending 榜单中 AI 相关项目占比高达 12/15，显示出 AI 生态在 **智能体（Agent）基础设施**和**本地化部署**方向集中爆发。TencentCloud 连推两个面向 AI 代理的底层组件（长期记忆库与安全沙箱），代表云厂商正加速开放 AI 中间件。开源 LLM 工程框架继续领跑，`langchain` 与 `AutoGPT` 等老牌项目保持超 14 万 Star，而 `system_prompts_leaks` 以近千万级别总 Star（注：实际约5.4万）成为今日最受关注的“反向工程”项目，折射出社区对模型行为可解释性的强烈需求。同时，轻量级向量数据库 `zvec`、嵌入式检索库 `lancedb` 持续迭代，RAG 基础设施进入“小而快”的竞争阶段。

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars | 说明 |
|------|-------|------|
| [ollama/ollama](https://github.com/ollama/ollama) | 175,760 | 本地 LLM 运行的首选工具，今已支持 Kimi、GLM 等新模型 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 85,741 | 高性能 LLM 推理引擎，PagedAttention 内核持续优化 |
| [TencentCloud/TencentDB-Agent-Memory](https://github.com/TencentCloud/TencentDB-Agent-Memory) | 今日+318 | 腾讯云开源的 4 层渐进式智能体本地长期记忆库，零外部 API |
| [TencentCloud/CubeSandbox](https://github.com/TencentCloud/CubeSandbox) | 今日+564 | 即时并发、安全轻量的智能体沙箱，适合多代理隔离运行 |
| [wonderwhy-er/DesktopCommanderMCP](https://github.com/wonderwhy-er/DesktopCommanderMCP) | 今日+28 | 为 Claude 提供终端控制、文件系统搜索与差异编辑的 MCP 服务器 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | 147,893 | 大规模网页抓取与交互 API，是 LLM 获取实时数据的关键管道 |
| [asgeirtj/system_prompts_leaks](https://github.com/asgeirtj/system_prompts_leaks) | 今日+1218 / 54,283 | 提取了 Anthropic、OpenAI、Google、xAI 等数十个模型的最新系统提示词，持续更新 |

### 🤖 AI 智能体/工作流（Agent 框架、多智能体、自动化）

| 项目 | Stars | 说明 |
|------|-------|------|
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 141,325 | 智能体工程平台，今日依然是 RAG + Agent 开发的标准起点 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 185,435 | 通用自主智能体愿景，持续集成新工具链 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 211,640 | “与您一同成长的智能体”，支持记忆、工具调用与自我进化 |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | 今日+1297 | 生产级编码技能集合，让 AI 编码代理掌握 Git、测试、部署等工程实践 |
| [obra/superpowers](https://github.com/obra/superpowers) | 今日+1116 | 智能体技能框架+软件开发方法论，强调“让 Agent 学会工程规范” |
| [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill) | 今日+352 | 能研究 Reddit、X、YouTube 等 6 个平台并生成综合摘要的智能体技能 |
| [esengine/DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix) | 26,447 | 基于 DeepSeek 的终端原生编码代理，强调 prefix-cache 稳定性 |

### 📦 AI 应用（具体产品、垂直场景解决方案）

| 项目 | Stars | 说明 |
|------|-------|------|
| [iOfficeAI/OfficeCLI](https://github.com/iOfficeAI/OfficeCLI) | 今日+1717 | 首个专为 AI 代理设计的 Office 办公套件 CLI，无需 Office 安装，可读写自动化 Word/Excel/PPT |
| [bradautomates/claude-video](https://github.com/bradautomates/claude-video) | 今日+951 | 让 Claude 能“看”视频：下载、抽帧、转录后交给 LLM 分析 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 91,892 | 多智能体金融交易框架，LLM 驱动的量化策略 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 48,323 | AI 生产力工作室，集成智能聊天、自主代理与 300+ 助手 |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | 55,932 | LLM 驱动的多市场股票智能分析系统，支持定时运行与推送 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 37,787 | 从文档自动生成可编辑 PowerPoint，保留原生动画、图表和演讲备注 |

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 说明 |
|------|-------|------|
| [huggingface/transformers](https://github.com/huggingface/transformers) | 162,392 | 最流行的模型定义与训练框架，支持文本、视觉、多模态 |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 101,603 | 动态神经网络框架，GPU 加速深度学习基础 |
| [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow) | 196,121 | 老牌机器学习框架，仍广泛用于生产部署 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,174 | 支持 100+ 数据集和主流模型的 LLM 评测平台 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | 281 | 可靠且可扩展的基础模型/世界模型预训练库，强调最小化依赖 |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | 315 | 设备端 LLM 推理，采用 X-Bit 量化，适合边缘场景 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 说明 |
|------|-------|------|
| [run-llama/llama_index](https://github.com/run-llama/llama_index) | 50,741 | 领先的文档代理 & OCR 平台，RAG 应用标配 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 45,139 | 云原生高性能向量数据库，支持大规模 ANN 搜索 |
| [weaviate/weaviate](https://github.com/weaviate/weaviate) | 16,543 | 同时存储对象和向量的开源向量数据库，支持结构化过滤 |
| [alibaba/zvec](https://github.com/alibaba/zvec) | 今日+395 / 14,445 | 轻量级进程内向量数据库，闪电般速度，适合嵌入式场景 |
| [lancedb/lancedb](https://github.com/lancedb/lancedb) | 10,831 | 开发者友好的 OSS 嵌入式检索库，支持多模态 AI |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 60,429 | AI 智能体的通用记忆层，支持长期记忆跨会话 |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | 27,371 | 自托管知识图谱引擎，为智能体提供持久长期记忆 |

## 趋势信号分析

**智能体工程化是今日最强劲的爆发方向。** `agent-skills`（+1297 stars）和 `superpowers`（+1116）均在强调“让 AI Agent 掌握工程技能”，不再是简单的提示词链，而是模块化、规范化的技能单元（如 Git 操作、测试编排）。这与 `OfficeCLI`（+1717）和 `claude-video`（+951）等应用层项目形成了完整链条——先让 Agent 会写代码，再让 Agent 会操作办公软件和多媒体。

**云厂商开始将 AI 中间件开源。** 腾讯云连续贡献 `TencentDB-Agent-Memory` 和 `CubeSandbox`，分别解决 Agent 的持久记忆和运行安全隔离两大痛点，预示着云原生 AI 基础设施正在从黑盒走向开放。

**“反向工程”成为社区新热点。** `system_prompts_leaks`（+1218）以几乎零行代码的方式捕获了各大模型最新系统提示，获得大量关注。这反映出开发者对模型行为透明度的渴求，也可能催生更多针对提示词安全与审计的开源工具。

**RAG 基础设施进一步分化。** `zvec`（阿里巴巴开源）主打“极轻量、进程内向量数据库”，与 `lancedb`、`oramasearch` 等形成对传统重型向量数据库（Milvus/Weaviate）的补充，适用于边缘设备或轻量级应用。

## 社区关注热点

- **`addyosmani/agent-skills`**：由知名工程专家 Addy Osmani 发起，将“生产级工程技能”编码为 AI 代理可复用的 Skills，可能重新定义 AI 辅助开发的范式。
- **`iOfficeAI/OfficeCLI`** + **`iOfficeAI/AionUi`**：一个专为 Agent 设计的 Office CLI，配套开源 UI，标志着 AI 代理开始接管日常办公流程，具有极高实用价值。
- **`asgeirtj/system_prompts_leaks`**：持续更新各类模型的系统提示词，对开发者理解模型行为边界、设计更鲁棒的 Agent 具有直接参考意义。
- **`tencentcloud/CubeSandbox`**：轻量沙箱用于隔离 Agent 执行环境，解决多代理协同中的安全与并发问题，可能成为未来 Agent 运行时标配。
- **`alibaba/zvec`**：今日新增 395 stars，轻量级进程内向量数据库正在挑战传统方案，特别适合需要低延迟、低资源消耗的 RAG 场景。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*