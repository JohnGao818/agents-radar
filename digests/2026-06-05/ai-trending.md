# AI 开源趋势日报 2026-06-05

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-05 03:25 UTC

---

## AI 开源趋势日报（2026-06-05）

### 1. 今日速览

- **AI Agent 生态持续爆发**：`hermes-agent`、`ECC` 等 Agent 基础设施项目今日新增 stars 合计超 3600，开发者对 Agent 框架和性能优化的需求极强。
- **Token 压缩成为新热点**：`headroom` 今日新增 3142 stars，以“减少 60-95% token”的口号直击 LLM 成本痛点，显示出社区对推理效率工具的高度渴望。
- **多模态与物理 AI 升温**：NVIDIA 的 `cosmos`（世界模型）和 `PaddleOCR`（OCR+LLM 结构化）持续吸引关注，AI 从纯文本走向图像、视频和机器人领域。
- **RAG 基础设施日趋成熟**：`ragflow`、`milvus`、`qdrant` 等向量数据库和 RAG 引擎 stars 稳定增长，同时新晋项目 `LEANN`（MLsys2026）以 97% 存储节省引起关注。
- **AI 应用“大众化”**：`open-notebook`（开源 NotebookLM）、`Open-LLM-VTuber`（语音交互 Live2D）等面向终端用户的产品快速迭代，降低 AI 使用门槛。

---

### 2. 各维度热门项目

#### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

- **[affaan-m/ECC](https://github.com/affaan-m/ECC)** ⭐207,398 (今日 +1,750)  
  Agent harness 性能优化系统，集成技能、记忆、安全与科研流程，支持 Claude Code、Codex、Cursor 等主流 Agent 框架。

- **[github/copilot-sdk](https://github.com/github/copilot-sdk)** ⭐? (今日 +38)  
  GitHub 官方 Copilot Agent 多平台 SDK，使开发者能轻松将 Copilot 集成到自有应用中。

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐81,960  
  高吞吐、低内存的 LLM 推理引擎，是部署大模型的事实标准之一。

- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐173,202  
  一键运行本地 LLM（支持 Kimi、DeepSeek、Gemma 等），是 AI 本地化部署最流行的工具。

- **[chopratejas/headroom](https://github.com/chopratejas/headroom)** ⭐0 (今日 +3,142)  
  在数据到达 LLM 之前压缩 token 数量 60–95%，支持库、代理和 MCP 服务器，直接降低推理成本。

- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** ⭐128,768  
  大规模网页搜索、抓取与交互 API，为 AI Agent 提供实时网络数据源。

- **[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)** ⭐7,529  
  Rust 语言下的模块化 LLM 应用框架，适合对性能敏感的后端集成。

---

#### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐181,212 (今日 +1,913)  
  “与你一同成长的 Agent”，强调持续学习和自适应性，今日新增 stars 极高。

- **[langgenius/dify](https://github.com/langgenius/dify)** ⭐143,914  
  生产级 Agentic 工作流开发平台，支持拖拽式编排和多种 LLM 后端。

- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐184,768  
  最早出圈的自主 Agent 项目，提供通用任务自动化能力。

- **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)** ⭐75,865  
  AI 驱动的软件工程助手，可自主编写、调试代码。

- **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)** ⭐82,973  
  多智能体 LLM 金融交易框架，将 Agent 技术应用于量化投资。

- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** ⭐97,225  
  让 Agent 能自动操作浏览器，完成 Web 端复杂任务。

- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** ⭐0 (今日 +199)  
  AI Agent 技能：跨 Reddit、X、YouTube 等平台研究任意主题并合成摘要。

---

#### 📦 AI 应用（具体应用产品、垂直场景解决方案）

- **[PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)** ⭐79,981 (今日 +141)  
  将 PDF/图片转为结构化数据，支持 100+ 语言，是连接文档与 LLM 的关键桥梁。

- **[NVIDIA/cosmos](https://github.com/NVIDIA/cosmos)** ⭐? (今日 +133)  
  NVIDIA 开源世界模型平台，用于机器人、自动驾驶、智能基础设施的物理 AI 开发。

- **[lfnovo/open-notebook](https://github.com/lfnovo/open-notebook)** ⭐0 (今日 +212)  
  开源版 NotebookLM，提供更灵活的知识笔记与 AI 协同体验。

- **[Open-LLM-VTuber/Open-LLM-VTuber](https://github.com/Open-LLM-VTuber/Open-LLM-VTuber)** ⭐0 (今日 +581)  
  本地运行的 LLM 语音交互 + Live2D 虚拟形象，支持语音打断，适合娱乐和陪伴场景。

- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐46,884  
  AI 生产力工作室，集成智能对话、自主 Agent 和 300+ 内置助手，统一管理多家大模型。

- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐40,806  
  LLM 驱动的 A/H/美股智能分析系统，零成本定时运行，适合个人投资者。

- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐24,421  
  AI 根据文档自动生成可编辑 PowerPoint，支持原生形状、动画和语音旁白。

---

#### 🧠 大模型/训练（模型权重、训练框架、微调工具）

- **[tensorflow/tensorflow](https://github.com/tensorflow/tensorflow)** ⭐195,415  
  经典 ML 框架，虽被 PyTorch 超越，但在生产部署中仍有大量用户。

- **[pytorch/pytorch](https://github.com/pytorch/pytorch)** ⭐100,389  
  深度学习第一框架，支撑绝大多数开源大模型的训练与推理。

- **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐161,293  
  模型定义与调用的标准接口，覆盖文本、视觉、多模态。

- **[jingyaogong/minimind](https://github.com/jingyaogong/minimind)** ⭐51,145  
  2 小时从零训练 64M 参数的迷你 LLM，适合教学和快速实验。

- **[rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)** ⭐96,667  
  手把手从零实现 ChatGPT 类 LLM 的教程，代码与理论并重。

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,061  
  综合性 LLM 评测平台，支持 100+ 数据集和主流模型。

- **[shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code)** ⭐64,739  
  从零到一构建类 Claude Code 的 Agent 框架，教学与实战结合。

---

#### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐81,939  
  领先的开源 RAG 引擎，融合 Agent 能力，为 LLM 提供优质上下文。

- **[open-webui/open-webui](https://github.com/open-webui/open-webui)** ⭐140,079  
  用户友好的 AI 界面，支持 Ollama、OpenAI 等多种后端，内置 Chat 与 RAG 功能。

- **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** ⭐138,533  
  Agent 工程平台，提供全套 RAG 与工具调用组件。

- **[run-llama/llama_index](https://github.com/run-llama/llama_index)** ⭐49,924  
  文档 Agent 与 OCR 平台，专注复杂文档的检索与结构化。

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐44,633  
  高性能云原生向量数据库，支撑大规模相似性搜索。

- **[qdrant/qdrant](https://github.com/qdrant/qdrant)** ⭐31,809  
  高可扩展向量搜索引擎，为 AI 应用提供实时检索能力。

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐57,735  
  AI Agent 的通用记忆层，让 Agent 拥有长期记忆与上下文。

- **[StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN)** ⭐11,868  
  MLsys2026 最佳论文：在个人设备上实现 97% 存储节省的 RAG，兼顾速度与隐私。

---

### 3. 趋势信号分析

1. **推理优化成为社区“刚需”**：`headroom` 今日新增 3142 stars，直接反映开发者对 LLM 推理成本的高度敏感。随着大模型进入产品化阶段，Token 压缩、缓存、剪枝等优化工具正迎来爆发式关注。

2. **Agent 基础设施从框架走向性能调优**：`ECC` 以“Agent harness 性能优化系统”定位，今日新增 1750 stars。社区不再满足于“能跑 Agent”，而是追求更快的执行、更低的内存占用和更强的记忆能力。`mem0`、`thedotmack/claude-mem` 等项目也印证了这一方向。

3. **世界模型与物理 AI 首次进入前列**：NVIDIA 的 `cosmos` 虽然今日新增仅 133，但其主题搜索总量已积累到较高水平。伴随机器人、自动驾驶行业对物理世界模拟的迫切需求，世界模型可能成为下一波 AI 开源热点。

4. **RAG 技术栈日趋分化**：一方面 `ragflow`、`milvus` 等成熟项目继续壮大；另一方面新项目如 `LEANN`（存储压缩）和 `PageIndex`（无向量推理）通过差异化方案切入，显示 RAG 正从“通用方案”向“特定场景优化”演进。

5. **AI 应用“娱乐化”与“生产化”双线并行**：`Open-LLM-VTuber` 和 `open-notebook` 分别代表娱乐陪伴与知识管理两个极端，说明 AI 开源生态已覆盖从休闲到工作的全场景。

---

### 4. 社区关注热点

- **🔥 `headroom`（Token 压缩）**：直接降低 API 调用成本，适合所有使用 LLM 的项目，今日新增 stars 为全榜第一，值得立即尝鲜。
- **🔥 `ECC`（Agent 性能调优）**：对于使用 Claude Code、Codex 等工具的高频开发者而言，这款优化系统能显著提升开发效率。
- **📊 `thedotmack/claude-mem`（跨会话记忆）**：主题搜索 stars 高达 80,695，解决 Agent 记忆碎片化问题，是当前 Agent 应用落地的关键组件。
- **🧠 `LEANN`（极致存储节省 RAG）**：MLsys 2026 论文成果，97% 存储节省意味着可在移动端运行完整 RAG，对边缘 AI 有革命性影响。
- **🎙️ `Open-LLM-VTuber`（语音交互虚拟角色）**：本地运行的 Live2D + LLM 语音交互，代表了 AI 在娱乐和社交领域的开源探索，今日新增 581 stars，热度攀升快。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*