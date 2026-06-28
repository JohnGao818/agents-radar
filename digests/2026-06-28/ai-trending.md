# AI 开源趋势日报 2026-06-28

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-28 03:25 UTC

---

# AI 开源趋势日报（2026-06-28）

## 1. 今日速览

- **AI 编码代理（Coding Agent）生态爆发**：Trending 榜单中，基于 Claude Code / Codex 的 Agent 工具占据半壁江山，gstack、opencode、ai-website-cloner-template 等单日增长均超 500 stars，社区正在快速构建“AI 开发者工具链”。
- **多 Agent 协作与记忆技术成焦点**：topoteretes/cognee 今日新增 780 stars，其“AI 记忆平台”概念将知识图谱与 Agent 持久化上下文结合；ai-berkshire 则通过多 Agent 对抗分析实现价值投资研究，标志着 Agent 协作从简单任务走向复杂决策。
- **生成式 AI 应用走向实用化**：ppt-master 用 AI 生成可编辑 PowerPoint（含动画、声述），Open-Generative-AI 提供 200+ 模型的免过滤视频/图像生成平台，显示出 AI 内容生产工具的快速成熟。
- **自动驾驶开源项目保持热度**：commaai/openpilot 今日 +322 stars，作为机器人操作系统持续迭代，其“300+ 车型支持”的社区价值依然强劲。

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、开发工具）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [ollama/ollama](https://github.com/ollama/ollama) | 175,008 | 本地运行 LLM 的首选工具，现已支持 Kimi-K2.6、GLM-5.1 等最新模型，社区生态极强。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | 161,977 | 🤗 模型定义框架，支持文本、视觉、音频等多模态模型推理与训练，是 AI 应用的底层基石。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 140,349 | Agent 工程平台，提供组件化的 LLM 应用构建能力，是 RAG、Agent 开发的事实标准。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 84,593 | 高性能 LLM 推理引擎，高吞吐、低内存，支撑大量线上 AI 服务。 |
| [Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec) | 177 today | 规范驱动开发（SDD）工具，为 AI 编码助手提供结构化规范，提升 AI 生成代码的一致性。 |
| [google-labs-code/design.md](https://github.com/google-labs-code/design.md) | 1,541 today | 视觉标识格式规范，让编码 Agent 持久理解设计系统，是 AI 与 UI 协作的新范式。 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 185,185 | 自主 AI Agent 先驱，实现任务规划、工具调用与自我迭代，是 Agent 领域的里程碑。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 78,519 | AI 驱动的软件开发代理，能自动编码、调试、部署，代表“AI 程序员”方向。 |
| [anomalyco/opencode](https://github.com/anomalyco/opencode) | 392 today | 开源编码 Agent，与 Claude Code 类似但完全开源，社区可直接修改与扩展。 |
| [garrytan/gstack](https://github.com/garrytan/gstack) | 674 today | Garry Tan 定制的 Claude Code 工具集，集成 CEO、设计师、工程经理等角色，让 AI 模拟团队协作。 |
| [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading) | 92 today | 个人交易 Agent，结合市场数据与 LLM 推理，提供自动化投资建议。 |
| [xbtlin/ai-berkshire](https://github.com/xbtlin/ai-berkshire) | 685 today | 基于四位投资大师方法论的多 Agent 对抗分析框架，用于价值投资研究。 |
| [luongnv89/claude-howto](https://github.com/luongnv89/claude-howto) | 141 today | Claude Code 视觉指南，从基础到高级 Agent 的粘贴即用模板，降低 Agent 入门门槛。 |

### 📦 AI 应用（具体产品与垂直场景）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 589 today (总33,174) | AI 根据文档生成真实可编辑的 PowerPoint，含原生形状、动画、声音解说，可适配自定义模板。 |
| [Anil-matcha/Open-Generative-AI](https://github.com/Anil-matcha/Open-Generative-AI) | 255 today | 无内容过滤的 AI 图像/视频生成平台，集成 Flux、Midjourney、Sora 等 200+ 模型，MIT 开源。 |
| [JCodesMore/ai-website-cloner-template](https://github.com/JCodesMore/ai-website-cloner-template) | 750 today | 一条命令通过 AI 编码代理克隆整个网站，快速实现网站复制与模板化。 |
| [commaai/openpilot](https://github.com/commaai/openpilot) | 322 today | 机器人操作系统，为 300+ 车型提供辅助驾驶升级，是自动驾驶领域最大开源项目。 |

### 🧠 大模型/训练（模型权重、训练框架、微调）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 101,067 | 动态神经网络框架，GPU 加速，是深度学习训练和研究的首选平台。 |
| [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow) | 195,964 | 端到端机器学习框架，全平台部署支持，工业级应用广泛。 |
| [ultralytics/ultralytics](https://github.com/ultralytics/ultralytics) | 58,887 | YOLO 对象检测系列，实时计算机视觉，适合快速部署。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,126 | 大模型评估平台，支持 Llama、GPT-4、Claude 等 100+ 数据集，是模型能力标尺。 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | 269 | 可复现的基础模型预训练库，关注稳定性和可扩展性，适合研究团队。 |
| [zjunlp/LightThinker](https://github.com/zjunlp/LightThinker) | 164 | EMNLP 2025 论文实现，通过逐步压缩减少链式推理开销，提升 LLM 推理效率。 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 83,749 | 领先的开源 RAG 引擎，融合 Agent 能力与上下文层，适合企业级知识问答。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,983 | 高性能云原生向量数据库，支持大规模近似最近邻搜索，是 RAG 基础设施。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 32,704 | 高可用向量数据库与搜索引擎，专为下一代 AI 应用设计，支持云服务。 |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | 780 today (总24,064) | 开源 AI 记忆平台，基于知识图谱为 Agent 提供持久化上下文，跨会话记忆关键组件。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 59,601 | 通用 AI Agent 记忆层，可压缩、存储、检索对话历史，适配多种 Agent 框架。 |
| [weaviate/weaviate](https://github.com/weaviate/weaviate) | 16,449 | 云原生向量数据库，支持混合搜索与结构化过滤，适合智能体知识管理。 |
| [VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex) | 33,474 | 无向量化的推理型 RAG，直接对文档索引进行推理，减少向量存储消耗。 |

## 3. 趋势信号分析

**AI 编码代理（Coding Agent）成为社区爆发中心**：Trending 榜单中，与 Claude Code / Codex 生态直接相关的项目（gstack、opencode、ai-website-cloner-template、claude-howto）合计今日新增超过 2,000 stars，而 Google 的 `design.md` 规范以 +1,541 次日增居首，表明开发者正急切地为 Agent 化开发建立标准化工具链。这一趋势与近期 Anthropic 发布的 Claude Code 深度集成（如 `gstack` 整合 CEO/工程经理角色）高度关联，社区开始探索“AI 模拟团队协作”的落地形态。

**多 Agent 协作与记忆机制加速演进**：`cognee`（+780）和 `ai-berkshire`（+685）代表了两个方向——前者关注 Agent 跨会话记忆（知识图谱 + RAG），后者关注多 Agent 对抗分析（四位大师方法论协作）。结合主题搜索中 `hermes-agent`（204k stars）和 `mem0`（59.6k stars），可以判断：Agent 的持久化记忆与多智能体协同正从实验走向工程化。

**生成式 AI 应用从“演示”转向“生产力”**：`ppt-master` 以 +589 日增验证了“AI 生成可编辑文档”的市场需求；`Open-Generative-AI`（+255）则提供 200+ 模型的免过滤视频/图像生成，显示出社区对“无限制创作”平台的渴望。这类项目与近期 Sora、Veo 等视频模型的开放形成呼应，开源生态正在快速补充商业工具的空白。

**自动驾驶与机器人系统持续吸引关注**：`openpilot` 稳定增长（+322），其“300+ 车型支持”的社区贡献模式，与近期特斯拉 FSD 开源讨论、以及 L4 级自动驾驶法规进展相关，说明机器人操作系统仍是长线热点。

## 4. 社区关注热点

- **`anomalyco/opencode`**（今日 +392）— 完全开源的编码 Agent，可直接替代 Claude Code 进行本地开发，值得想脱离封闭生态的团队深入研究。
- **`garrytan/gstack`**（今日 +674）— 23 个定制工具模拟 CEO、设计师、QA 等角色，展示了 AI Agent 如何嵌入真实工作流，是“AI 团队”的先行案例。
- **`topoteretes/cognee`**（今日 +780）— 开源 AI 记忆平台，知识图谱引擎为 Agent 提供长期记忆，是构建持久化智能体的关键基础设施。
- **`google-labs-code/design.md`**（今日 +1,541）— 谷歌实验室推出的设计格式规范，让 AI Agent 理解视觉系统，可能成为未来人机协作 UI 开发的标准。
- **`Anil-matcha/Open-Generative-AI`**（今日 +255）— 集合 200+ 模型的免过滤生成平台，MIT 许可证，适合需要大规模生成创意内容的开发者，但需注意内容合规风险。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*