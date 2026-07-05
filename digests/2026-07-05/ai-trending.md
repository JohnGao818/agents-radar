# AI 开源趋势日报 2026-07-05

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-05 02:42 UTC

---

# AI 开源趋势日报（2026-07-05）

## 今日速览

今日 GitHub 涌现出一波 **AI Agent 技能（Skills）生态** 的爆发式增长，`mattpocock/skills`、`alirezarezvani/claude-skills` 等项目热度飙升，标志着“技能即代码”的潮流正从少数开发者扩散到整个社区。同时，**Token 高效化** 成为新焦点：`caveman` 通过“原始人语言”压缩 65% 的 tokens，`headroomlabs-ai/headroom` 提供通用压缩库，直击 LLM 成本痛点。此外，**MCP 协议（Model Context Protocol）** 继续扩展边界，`ChromeDevTools/chrome-devtools-mcp` 和 `CoplayDev/unity-mcp` 将 AI 助手与浏览器 DevTools、Unity 编辑器深度打通。本地化 AI 应用同样火热，`Zackriya-Solutions/meetily` 主打 100% 本地会议助手，`open-webui` 星数已破 144k。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

- **`huggingface/transformers`** ⭐162,238  
  模型定义与训练/推理的统一框架，今日社区更新支持最新开源模型（如 Kimi-K2.6、MiniMax 等）。  
  https://github.com/huggingface/transformers

- **`vllm-project/vllm`** ⭐85,379  
  高吞吐、内存高效的 LLM 推理引擎，开源部署的首选。  
  https://github.com/vllm-project/vllm

- **`ChromeDevTools/chrome-devtools-mcp`** ⭐304 (today)  
  Chrome DevTools 通过 MCP 协议向 AI Agent 暴露控制能力，让 LLM 可以像人类一样操作浏览器调试面板。今日首次登榜。  
  https://github.com/ChromeDevTools/chrome-devtools-mcp

- **`ogulcancelik/herdr`** ⭐707 (today)  
  终端中的 Agent 多路复用器，支持同时管理多个 AI Agent 实例，简化本地编排。  
  https://github.com/ogulcancelik/herdr

- **`CoplayDev/unity-mcp`** ⭐69 (today)  
  Unity MCP 桥接器，让 LLM 直接控制 Unity 编辑器（管理资源、修改场景、自动生成脚本），游戏开发自动化新方式。  
  https://github.com/CoplayDev/unity-mcp

- **`crynta/terax-ai`** ⭐62 (today)  
  轻量级（7MB）终端优先的 AI 原生开发工作台，集成 Agent 能力，面向极简主义者。  
  https://github.com/crynta/terax-ai

---

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

- **`Significant-Gravitas/AutoGPT`** ⭐185,353  
  老牌自主 Agent 框架，持续更新，今日社区新增“技能市场”集成。  
  https://github.com/Significant-Gravitas/AutoGPT

- **`langgenius/dify`** ⭐147,681  
  生产级 Agentic Workflow 平台，支持可视化编排 Agent、RAG 和工具调用。  
  https://github.com/langgenius/dify

- **`langchain-ai/langchain`** ⭐140,928  
  Agent 工程平台，提供统一的 Agent、工具、记忆抽象，今日大量新 skill 集成。  
  https://github.com/langchain-ai/langchain

- **`browser-use/browser-use`** ⭐102,741  
  让 AI Agent 像人类一样操控网页，今日新增对动态元素的兼容性优化。  
  https://github.com/browser-use/browser-use

- **`OpenHands/OpenHands`** ⭐79,433  
  AI 驱动的软件开发 Agent，支持多轮协作和代码生成。  
  https://github.com/OpenHands/OpenHands

- **`alibaba/page-agent`** ⭐742 (today)  
  阿里巴巴开源的 JavaScript 网页 GUI Agent，自然语言控制 Web 界面，与 browser-use 形成差异化（更轻量）。  
  https://github.com/alibaba/page-agent

- **`mattpocock/skills`** ⭐973 (today)  
  知名工程师的技能集，直接从 `.claude` 目录导出，定义了“真实工程师”使用的 Prompt 与工具链，今日暴涨。  
  https://github.com/mattpocock/skills

- **`alirezarezvani/claude-skills`** ⭐136 (today)  
  收录 337 个 Claude Code 技能，覆盖工程、营销、产品、合规等 8 种角色，是当前最大的技能市场合集。  
  https://github.com/alirezarezvani/claude-skills

---

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

- **`usestrix/strix`** ⭐1,904 (today)  
  开源 AI 渗透测试工具，自动化发现并修复应用漏洞，今日热度最高之一。  
  https://github.com/usestrix/strix

- **`Zackriya-Solutions/meetily`** ⭐718 (today)  
  完全本地的 AI 会议助手，基于 Rust 实现 4 倍速 Whisper 转录 + 说话人分离 + Ollama 总结，无云依赖。  
  https://github.com/Zackriya-Solutions/meetily

- **`open-webui/open-webui`** ⭐144,217  
  用户友好的 AI 对话前端，支持 Ollama 和 OpenAI API，自托管首选。  
  https://github.com/open-webui/open-webui

- **`CherryHQ/cherry-studio`** ⭐48,160  
  AI 生产力工作室，集成智能聊天、自主 Agent、300+ 助手，统一前端调用前沿 LLM。  
  https://github.com/CherryHQ/cherry-studio

- **`zhayujie/CowAgent`** ⭐45,791  
  开源超级 AI 助手 & Agent Harness，支持多模型、多通道、记忆与工具，一条命令安装。  
  https://github.com/zhayujie/CowAgent

- **`HKUDS/nanobot`** ⭐45,010  
  轻量级 AI Agent，专注于工具调用和聊天工作流自动化。  
  https://github.com/HKUDS/nanobot

---

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

- **`ollama/ollama`** ⭐175,473  
  本地模型运行平台，今日新增支持 Kimi-K2.6、GLM-5.1、gpt-oss 等最新模型。  
  https://github.com/ollama/ollama

- **`pytorch/pytorch`** ⭐101,494  
  深度学习框架，今日社区关注新版本中对训练 Agent 的优化支持。  
  https://github.com/pytorch/pytorch

- **`tensorflow/tensorflow`** ⭐196,041  
  经典机器学习框架，持续更新以适配边缘推理。  
  https://github.com/tensorflow/tensorflow

- **`ultralytics/ultralytics`** ⭐59,112  
  YOLO 系列最新版（YOLO26/11），目标检测与跟踪的工业标准。  
  https://github.com/ultralytics/ultralytics

- **`NousResearch/hermes-agent`** ⭐209,244  
  “与你一起成长的 Agent”——集成了自主训练与持续学习能力，今日星数再创新高。  
  https://github.com/NousResearch/hermes-agent

- **`open-compass/opencompass`** ⭐7,154  
  LLM 评估平台，支持 100+ 数据集，今日新增对最新模型的评测基准。  
  https://github.com/open-compass/opencompass

---

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

- **`infiniflow/ragflow`** ⭐84,283  
  领先的开源 RAG 引擎，融合 Agent 能力与高精度检索，企业级部署首选。  
  https://github.com/infiniflow/ragflow

- **`run-llama/llama_index`** ⭐50,645  
  LlamaIndex 文档 Agent 与 OCR 平台，今日支持更多文件格式和知识图谱注入。  
  https://github.com/run-llama/llama_index

- **`milvus-io/milvus`** ⭐45,072  
  高性能云原生向量数据库，支持十亿级向量 ANN 搜索。  
  https://github.com/milvus-io/milvus

- **`Mintplex-Labs/anything-llm`** ⭐62,584  
  本地优先的 All-in-One 智能体体验，集成 RAG、记忆与工具调用。  
  https://github.com/Mintplex-Labs/anything-llm

- **`Graphify-Labs/graphify`** ⭐77,705  
  AI 编码助手技能：将代码、SQL 模式、文档等转化为可查询的知识图谱，支持多 Agent 共享。  
  https://github.com/Graphify-Labs/graphify

- **`StarTrail-org/LEANN`** ⭐12,635  
  论文级 RAG 方案：97% 存储压缩、100% 私有，设备端运行，新星项目。  
  https://github.com/StarTrail-org/LEANN

- **`VectifyAI/PageIndex`** ⭐33,735  
  无需向量化、基于推理的 RAG 索引方案，降低对 Embedding 的依赖。  
  https://github.com/VectifyAI/PageIndex

---

## 趋势信号分析

1. **Agent Skills 生态迎来爆发式增长**：今日 Trending 榜单中，超过 1/3 的项目与 “Skill” 直接相关（`mattpocock/skills`、`agentskills/agentskills`、`alirezarezvani/claude-skills`、`dotnet/skills`）。社区正在将“Prompt 工程”产品化为可复用、可版本化的“技能文件”，并涌现出 `agent-skills` 规范。这标志着 AI Agent 从“写一次用一次”走向“积累、共享、标准化”的新阶段。

2. **Token 压缩成新战场**：`caveman` 通过“原始人语言”压缩 65% tokens、`headroomlabs-ai/headroom` 提供通用压缩库可减少 60-95% tokens 且不损失答案质量。在 API 成本依然高企的背景下，这类“无感节省”工具正在快速获得社区关注，可能成为 Agent 框架的标准组件。

3. **MCP 协议全面渗透开发工具链**：从 Chrome DevTools 到 Unity 编辑器，MCP 桥接器成为连接 AI 与开发者工具的“最后一公里”。`ChromeDevTools/chrome-devtools-mcp` 和 `CoplayDev/unity-mcp` 今日登榜，意味着 AI Agent 正在突破代码编辑，进入浏览器调试、游戏开发等多元场景。

4. **本地化、隐私优先持续升温**：`meetily`（100% 本地会议助手）、`anything-llm`（本地 Agent 体验）、`ollama` 持续增长，反映用户对数据主权和低延迟的刚性需求。`terax-ai` 以 7MB 终端工作空间挑战传统 IDE，极简主义趋势明显。

5. **AI 安全与渗透测试崛起**：`strix` 以 1904 颗今日 stars 登顶 Trending，首次将 AI 应用于自动化渗透测试，可能催生新的“红队 Agent”品类。

---

## 社区关注热点

- **⚡ Skills 标准化与复用**：`agentskills/agentskills` 试图定义统一规范，结合 `mattpocock/skills` 等实践，开发者应关注这份规范如何影响未来 Agent 的可移植性。  
  https://github.com/agentskills/agentskills

- **🧠 Token 压缩的艺术**：`caveman` 和 `headroom` 代表了两种范式（模式压缩 vs 工具压缩），值得实验以降低日常 Agent 任务的 API 消耗。  
  https://github.com/JuliusBrussee/caveman  
  https://github.com/headroomlabs-ai/headroom

- **🔗 MCP 生态的“万能适配器”**：`ChromeDevTools/chrome-devtools-mcp` 和 `unity-mcp` 展示了 MCP 的扩展性，开发者可参考其模式为自己常用的工具（如 Figma、Postman）编写 MCP 桥接器。

- **🕵️ AI 安全工具进入主流**：`strix` 爆红提示安全领域正在被 Agent 化，建议安全工程师关注此类项目如何自动化漏洞发现与修复的流程。  
  https://github.com/usestrix/strix

- **📦 从“写代码”到“写技能”**：`claude-skills` 集合了 337 个高质量技能，覆盖多个业务角色（营销、合规、C 层顾问等），对于希望快速构建垂直 Agent 的团队极具参考价值。  
  https://github.com/alirezarezvani/claude-skills

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*