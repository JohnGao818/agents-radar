# AI 开源趋势日报 2026-06-11

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-11 03:33 UTC

---

# AI 开源趋势日报 – 2026-06-11

---

## 1. 今日速览

今日 GitHub AI 开源社区出现明显信号：**Agent Skills（代理技能）** 类项目集体爆发，`last30days-skill` 单日斩获 2535 星，`agent-skills`、`pm-skills`、`superpowers` 等也大幅增长，表明开发者正从“搭建 Agent 框架”转向“复用即用技能模块”。同时，**AI 视频生成**（`MoneyPrinterTurbo` 日增 1389⭐）、**计算机视觉工具**（`supervision` 日增 695⭐）保持热度。新方向方面，`RuView` 将 WiFi 信号转化为空间智能，`openmed` 聚焦开源医疗 AI，显示出 AI 与物联网、医疗的交叉创新。此外，**RAG/知识库**赛道持续稳健，`claude-mem`、`mem0` 等长期记忆项目关注度极高。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具

- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐ 173,809 – 本地运行大量 LLM 的最简方案，已成为社区标配。
- **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** ⭐ 138,997 – 代理工程平台，支持多模型、工具调用和 RAG。
- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐ 82,476 – 高吞吐、低延迟的 LLM 推理引擎，生产部署首选。
- **[roboflow/supervision](https://github.com/roboflow/supervision)** ⭐ 0 (+695 today) – 可复用的计算机视觉工具集，今日新增 star 爆炸式增长。
- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** ⭐ 131,197 – 网页搜索、抓取与交互 API，为 AI 代理提供实时数据源。
- **[open-webui/open-webui](https://github.com/open-webui/open-webui)** ⭐ 141,022 – 用户友好的 AI 前端界面，支持 Ollama 和多种 API。

### 🤖 AI 智能体/工作流

- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** ⭐ 0 (+2,535 today) – **今日最大黑马**：AI 代理技能，自动从 Reddit、X、YouTube 等平台调研话题并生成总结。
- **[addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)** ⭐ 0 (+821 today) – 生产级 AI 编码代理技能，专为代码场景设计。
- **[obra/superpowers](https://github.com/obra/superpowers)** ⭐ 0 (+1,104 today) – 一套代理技能框架 + 软件开发方法论，强调可落地。
- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐ 184,888 – 自主 AI 代理先驱，支持任务规划与工具调用。
- **[langgenius/dify](https://github.com/langgenius/dify)** ⭐ 144,771 – 生产级代理工作流开发平台，可视化和可扩展。
- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** ⭐ 98,179 – 让 AI 代理自动化操作浏览器，赋能 Web 任务。
- **[zhayujie/CowAgent](https://github.com/zhayujie/CowAgent)** ⭐ 45,210 – 开源超级 AI 助手，支持任务规划、工具调用与记忆进化。
- **[google/skills](https://github.com/google/skills)** ⭐ 0 (+211 today) – Google 官方推出的 Agent Skills 包，打通 Google 产品生态。

### 📦 AI 应用

- **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** ⭐ 0 (+1,389 today) – 一键利用 AI 大模型生成高清短视频，持续火爆。
- **[maziyarpanahi/openmed](https://github.com/maziyarpanahi/openmed)** ⭐ 0 (+527 today) – 开源医疗 AI 项目，覆盖诊断、影像、病历分析等场景。
- **[ruvnet/RuView](https://github.com/ruvnet/RuView)** ⭐ 0 (+420 today) – 创新项目：将普通 WiFi 信号转化为实时空间感知与生命体征监测。
- **[safishamsi/graphify](https://github.com/safishamsi/graphify)** ⭐ 65,049 – 将任意代码/文档/图像转化为可查询知识图谱，辅助 AI 编码。
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐ 26,209 – AI 从文档生成可编辑的 PowerPoint，含动画和语音。
- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐ 41,907 – LLM 驱动的多市场股票分析系统，零成本定时运行。

### 🧠 大模型/训练

- **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)** ⭐ 72,056 – 统一高效微调 100+ LLM/VLM 的框架，ACL 2024 论文。
- **[FareedKhan-dev/train-llm-from-scratch](https://github.com/FareedKhan-dev/train-llm-from-scratch)** ⭐ 0 (+247 today) – 从头训练 LLM 的简明指南，从数据下载到生成文本。
- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** ⭐ 4,267 – 面向系统工程师的 LLM 推理服务学习项目，构建迷你 vLLM + Qwen。
- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐ 7,080 – 多模型、多数据集、多维度的大模型评估平台。
- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐ 254 – 可靠、最小化、可扩展的基础模型预训练库。

### 🔍 RAG/知识库

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐ 82,423 – 领先的开源 RAG 引擎，融合代理能力与深度文档理解。
- **[run-llama/llama_index](https://github.com/run-llama/llama_index)** ⭐ 50,069 – 文档代理与 OCR 平台，构建 RAG 应用的核心框架。
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐ 58,293 – AI 代理的通用记忆层，实现跨会话持久记忆。
- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** ⭐ 81,668 – 捕获并压缩代理会话上下文，跨会话注入相关记忆。
- **[StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN)** ⭐ 11,903 – 97% 存储节省的 RAG 方案，支持个人设备完全隐私运行。
- **[Weaviate/weaviate](https://github.com/weaviate/weaviate)** ⭐ 16,307 – 原生云向量数据库，支持混合搜索。
- **[FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise)** ⭐ 53,463 – 可视化构建 AI 代理与 RAG 工作流，零代码友好。

---

## 3. 趋势信号分析

1. **Agent Skills 成为社区爆发点**：`last30days-skill` 单日 2535 星的增量远超其他类别，`agent-skills`、`pm-skills`、`superpowers` 等也紧随其后。这标志着 AI 代理的“技能生态”开始形成——开发者不再仅关注框架，更希望直接插入经过验证的、可组合的功能模块（如信息调研、项目管理、编码辅助）。Google 官方也加入了 `google/skills`，说明大厂正在为代理生态铺设标准 API。

2. **RAG 向“记忆”与“上下文”深化**：`claude-mem`（81k⭐）和 `mem0`（58k⭐）均聚焦跨会话记忆，配合 `graphify` 的知识图谱化，RAG 正在从简单的“检索+生成”升级为具有长时记忆和结构化推理的智能层。`LEANN` 则展示了极致的存储效率（97% 节约），推动 RAG 在边缘设备落地。

3. **非传统 AI 感知领域出现新颖项目**：`RuView` 利用 WiFi 信号实现空间感知与生命体征监测，无需摄像头，将 AI 感知延伸到无光、隐私敏感场景。这类“信号级 AI”可能开辟新的 IoT 应用赛道。

4. **“即用型”训练工具持续受关注**：`train-llm-from-scratch` 简化了全流程，`LlamaFactory` 保持 72k 高星，表明社区对透明化、可定制模型训练的需求依然旺盛。

---

## 4. 社区关注热点

- **Agent Skills 生态**：`mvanhorn/last30days-skill`、`addyosmani/agent-skills`、`obra/superpowers` 等提供了可直接集成到 Claude Code、Codex 等代理中的技能包，建议关注如何利用这些技能快速构建生产级代理。
- **开源医疗 AI**：`openmed` 今日 +527⭐，标志着 AI 在医疗领域的开源渗透加速，可能成为下一个垂直爆发点。
- **非视觉感知 AI**：`ruvnet/RuView` 用 WiFi 信号替代摄像头，对隐私敏感场景和物联网场景有重要启示，值得测试其在实际环境中的表现。
- **长期记忆/上下文管理**：`thedotmack/claude-mem` 和 `mem0ai/mem0` 解决了代理“失忆”痛点，是构建持续运行 Agent 的关键基础设施。
- **低成本从头训练 LLM**：`FareedKhan-dev/train-llm-from-scratch` 给出了端到端流程，适合希望掌握训练细节的开发者及小团队快速验证模型。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*