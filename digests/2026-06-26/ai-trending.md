# AI 开源趋势日报 2026-06-26

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-26 02:56 UTC

---

# AI 开源趋势日报 — 2026-06-26

## 一、今日速览

今日 GitHub Trending 榜单中，AI Agent 相关项目占据绝对主导，特别是“Agentic Video Production”（OpenMontage，单日 +3434 stars）和“AI 价值投资框架”（ai-berkshire，+309 stars）等垂直场景 Agent 获得爆发式关注。同时，以 **Design.md**、**gstack** 和 **Claude Code Best Practice** 为代表的“Agent 开发规范与最佳实践”工具正在形成新的生态。在基础设施层面，AWS 官方发布的 **Agent Toolkit** 与阿里巴巴的 **Page Agent** 分别从云服务和浏览器自动化切入，进一步扩展了智能体的能力边界。此外，文档处理工具 **MinerU**（+644 stars）在 RAG 链路中持续升温，表明“文档→LLM 可用格式”的转换需求依然旺盛。

---

## 二、各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

1. **[google-labs-code/design.md](https://github.com/google-labs-code/design.md)**  
   ⭐ 0 / +1475 today  
   *核心说明*：为编码智能体提供视觉身份的格式化规范，让 AI 能够持久、结构性地理解设计系统。今日新增星数极高，标志着“Agent UI 标准化”方向正式登榜。

2. **[aws/agent-toolkit-for-aws](https://github.com/aws/agent-toolkit-for-aws)**  
   ⭐ 0 / +47 today  
   *核心说明*：AWS 官方推出的 MCP 服务器、技能与插件集成，帮助 AI 智能体在 AWS 云上构建应用。云原生 Agent 工具链的标杆。

3. **[garrytan/gstack](https://github.com/garrytan/gstack)**  
   ⭐ 0 / +767 today  
   *核心说明*：封装了 Garry Tan（Y Combinator CEO）的 Claude Code 配置方案，包含 23 个工具角色（CEO、设计师、工程经理等），是 Agent 开发工作流的模板化工具。

4. **[shanraisshan/claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice)**  
   ⭐ 0 / +287 today  
   *核心说明*：从“Vibe Coding”到“Agentic Engineering”的实践指南，帮助开发者系统化使用 Claude Code，是 Agent 工程方法论的快速入门。

5. **[ollama/ollama](https://github.com/ollama/ollama)**  
   ⭐ 174,912  
   *核心说明*：最流行的本地模型运行工具，已支持 Kimi、GLM、DeepSeek、Qwen 等，是开发者本地推理的首选。

6. **[vllm-project/vllm](https://github.com/vllm-project/vllm)**  
   ⭐ 84,338  
   *核心说明*：高性能 LLM 推理与服务引擎，对生产级 Agent 部署至关重要，社区持续迭代。

---

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

1. **[calesthio/OpenMontage](https://github.com/calesthio/OpenMontage)**  
   ⭐ 0 / +3434 today  
   *核心说明*：全球首个开源 Agent 视频制作系统，内置 12 条流水线、52 个工具和 500+ 智能体技能，可将 AI 编码助手变身完整视频工作室。今日 Trending 榜首。

2. **[xbtlin/ai-berkshire](https://github.com/xbtlin/ai-berkshire)**  
   ⭐ 0 / +309 today  
   *核心说明*：基于 Claude Code 的价值投资研究框架，融合巴菲特、芒格等四大师方法论，采用多 Agent 对抗式分析。金融垂直场景 Agent 的典型代表。

3. **[alibaba/page-agent](https://github.com/alibaba/page-agent)**  
   ⭐ 0 / +163 today  
   *核心说明*：JavaScript 页面内 GUI 智能体，通过自然语言控制网页界面，为浏览器自动化 Agent 提供了全新思路。

4. **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)**  
   ⭐ 203,139  
   *核心说明*：与用户共同成长的 Agent 框架，强调自主进化能力，是当前关注度最高的 Agent 项目之一。

5. **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)**  
   ⭐ 78,358  
   *核心说明*：AI 驱动的软件开发智能体，可自主完成编程任务，已成为 Agent 开发领域的参考实现。

6. **[bytedance/deer-flow](https://github.com/bytedance/deer-flow)**  
   ⭐ 74,739  
   *核心说明*：字节跳动开源的长时程 SuperAgent 框架，支持研究、编程、创作等复杂任务，Agent 协作架构的先进实践。

---

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

1. **[mukul975/Anthropic-Cybersecurity-Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)**  
   ⭐ 0 / +571 today  
   *核心说明*：817 个结构化网络安全技能，映射到 MITRE ATT&CK、NIST CSF 等 6 个框架，可与 Claude Code、Cursor 等 20+ 平台集成，是 Agent 安全技能的标准化库。

2. **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)**  
   ⭐ 88,565  
   *核心说明*：多智能体 LLM 金融交易框架，将 Agent 引入量化金融，今日仍保持极高热度。

3. **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)**  
   ⭐ 47,801  
   *核心说明*：AI 生产力工作室，集成智能聊天、自主 Agent 和 300+ 助手，统一访问前沿大模型，是面向终端的全能 AI 工具。

4. **[zhayujie/CowAgent](https://github.com/zhayujie/CowAgent)**  
   ⭐ 45,609  
   *核心说明*：开源超级 AI 助手与 Agent 框架，支持任务规划、工具调用、记忆进化，轻量易用，一命令行安装。

5. **[ScrapeGraphAI/Scrapegraph-ai](https://github.com/ScrapeGraphAI/Scrapegraph-ai)**  
   ⭐ 27,660  
   *核心说明*：基于 AI 的爬虫工具，将自然语言指令转换为网页数据提取，是应用层 Agent 的典型案例。

---

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

1. **[open-compass/opencompass](https://github.com/open-compass/opencompass)**  
   ⭐ 7,121  
   *核心说明*：LLM 评估平台，支持 100+ 数据集和主流模型，是模型选型与质量验证的重要工具。

2. **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)**  
   ⭐ 267  
   *核心说明*：可靠、可扩展的基础模型预训练库，聚焦稳定训练和世界模型构建，适合研究型开发者。

3. **[zjunlp/LightThinker](https://github.com/zjunlp/LightThinker)**  
   ⭐ 164  
   *核心说明*：EMNLP 2025 论文，提出“逐步压缩思维”的方法，旨在减少推理过程中的 Token 消耗，是 LLM 效率优化的前沿方向。

4. **[huggingface/transformers](https://github.com/huggingface/transformers)**  
   ⭐ 161,925  
   *核心说明*：模型定义与训练的标准框架，始终是社区最活跃的 AI 项目之一。

---

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

1. **[opendatalab/MinerU](https://github.com/opendatalab/MinerU)**  
   ⭐ 0 / +644 today  
   *核心说明*：将 PDF、Office 文档等复杂文档转换为 LLM 可用的 Markdown/JSON，是 RAG 流水线中文档预处理的利器，今日新增显著。

2. **[langgenius/dify](https://github.com/langgenius/dify)**  
   ⭐ 146,589  
   *核心说明*：生产级 Agent 工作流平台，内置 RAG、工具调用等功能，是 RAG 生态的综合性标杆。

3. **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)**  
   ⭐ 83,641  
   *核心说明*：领先的开源 RAG 引擎，融合 Agent 能力，构建 LLM 的上层上下文层，对企业级应用尤为关键。

4. **[mem0ai/mem0](https://github.com/mem0ai/mem0)**  
   ⭐ 59,465  
   *核心说明*：AI Agent 的通用记忆层，为跨 Session 持久化提供核心能力，与 RAG 互补。

5. **[milvus-io/milvus](https://github.com/milvus-io/milvus)**  
   ⭐ 44,960  
   *核心说明*：高性能云原生向量数据库，大规模向量检索的标准选择，RAG 的后端基石。

6. **[safishamsi/graphify](https://github.com/safishamsi/graphify)**  
   ⭐ 72,141  
   *核心说明*：将代码、文档、图片等任意文件夹转化为可查询的知识图谱，支持多种 Agent 平台，是知识管理的新范式。

---

## 三、趋势信号分析

**1. Agent 开发规范与工具链爆发**  
今日 Trending 中出现了大量围绕 **Claude Code** 生态的辅助工具：`gstack`（配置模板）、`claude-code-best-practice`（最佳实践）、`design.md`（设计规范）以及 `Anthropic-Cybersecurity-Skills`（技能库）。这表明社区已从“如何使用 Agent”进入“如何体系化地构建 Agent”阶段，类似于早期 Docker 的“标准化封装”浪潮。

**2. 垂直场景 Agent 获得加速度**  
`OpenMontage`（视频制作）和 `ai-berkshire`（价值投资）分别以 +3434 和 +309 的日新增闯入视野，表明 Agent 正在从通用编程辅助向媒体、金融等专业领域渗透。这种“Agent + 领域知识”的组合往往能快速吸引特定社群，形成病毒式传播。

**3. “文档→LLM”管道持续优化**  
`MinerU` 的持续高热（+644 stars）和主题搜索中 `PaddleOCR`、`MinerU` 的庞大基数说明，非结构化文档的清洗与结构化仍然是 RAG 落地的最大瓶颈，相关工具需求旺盛。同时 `graphify`、`mem0` 等知识图谱/记忆层项目也在快速迭代，RAG 正从“检索”走向“推理+记忆”。

**4. 云厂商与社区竞合**  
AWS 推出 `agent-toolkit-for-aws`，阿里推出 `page-agent`，标志着大型云厂商开始主动拥抱 Agent 生态，通过提供标准化接口（MCP、GUI Agent）争夺开发者入口。这与近期各云厂商宣布支持 Claude Code、Copilot 的动向一致。

---

## 四、社区关注热点

- **Claude Code 生态工具**：`gstack`、`claude-code-best-practice`、`design.md` 等项目正在快速积累人气。如果你在使用 Claude Code，这些工具能大幅提升开发效率和组织性，值得第一时间试用。
- **OpenMontage（视频 Agent）**：首次登榜即斩获 3400+ stars，其“AI 编码助手→视频工作室”的概念极具创新性，是多模态 Agent 领域的重要参考。
- **Anthropic-Cybersecurity-Skills**：819 个结构化安全技能的仓库，不仅定义了 Agent 安全能力的标准，还为其他垂直领域（如医疗、法律）的技能库编写提供了可复用的模式。
- **MinerU（文档转 LLM 格式）**：文档预处理一直是 RAG 的痛点，MinerU 今日新增 644 stars，其性能与易用性已被社区验证，适合任何需要将 PDF/Office 接入 LLM 的团队。
- **alibaba/page-agent**：用自然语言控制网页界面的 JavaScript Agent，为浏览器自动化、无头测试等场景提供了新思路，与 `browser-use`（100k+ stars）形成竞合，值得关注。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*