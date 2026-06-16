# AI 开源趋势日报 2026-06-16

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-16 03:40 UTC

---

# AI 开源趋势日报｜2026-06-16

## 今日速览

- **AI Agent 安全与可观测性成新热点**：NVIDIA 发布 SkillSpector（专攻 Agent 技能安全扫描）、trycua/cua 提供桌面操控型 Agent 沙箱基础设施，两者均以超高热度冲入 Trending 榜单。
- **“零 API 费用”数据采集 Agent 爆发**：Agent-Reach 凭借“一眼看遍全网”的 CLI 能力单日新增 1100+ stars，凸显开发者对低成本、多功能数据源的 Agent 应用需求。
- **金融领域大模型加速落地**：Kronos（金融基础模型）与 TradingAgents（多智能体交易框架）同时登榜，表明量化金融与 LLM 结合进入深水区。
- **AI 编程助手生态持续分化**：CopilotKit、Dify、Flowise 等可视化 Agent 平台热度不减，而 rohitg00/ai-engineering-from-scratch 这类“从零构建”学习项目也获得大量关注，社区正在从“用工具”向“造工具”演进。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|----------------|------------|
| [ollama/ollama](https://github.com/ollama/ollama) | 174,263 | 一键运行本地大模型的 CLI 工具，已支持 Kimi、DeepSeek、Qwen 等主流模型，是个人开发者的首选推理入口。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 82,993 | 高性能 LLM 推理引擎，PagedAttention 优化吞吐量，已成为企业级部署标准。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | 161,618 | 拥抱 Transformers 的模型定义与训练框架，覆盖文本、视觉、多模态，是 AI 研究的基础设施。 |
| [trycua/cua](https://github.com/trycua/cua) | 未显示总量 (+70 today) | 开源计算机使用 Agent 的沙箱 & SDK，支持 macOS/Linux/Windows 桌面操控，用于训练和评估 AI Agent。 |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | 313 | 专为边缘设备设计的量化推理库，实现端侧 LLM 推断。 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | 7,626 | Rust 生态的模块化 LLM 应用框架，强调可组合性与性能。 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|----------------|------------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 184,962 | 最早的自主 Agent 实现，近期更新持续支持工具调用与记忆模块。 |
| [langgenius/dify](https://github.com/langgenius/dify) | 145,376 | 生产级 Agent 工作流开发平台，支持可视化编排与多模型接入。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 99,015 | 让 AI Agent 操控浏览器完成自动化任务，已被广泛集成到各类 Agent 框架。 |
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | 30,558 (+1100 today) | 零 API 费用的全网信息采集 Agent，一条 CLI 即可读取 Twitter、Reddit、Bilibili 等平台。 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | 35,167 | 前端 Agent 集成栈，支持 React、Angular、Mobile 等，提供 AG-UI 协议。 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 86,488 | 多智能体金融交易框架，结合 LLM 实现投资决策自动化。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 194,587 | 开源 Agent 核心，可与 Claude Code、OpenClaw 等交互，支持技能与记忆扩展。 |

### 📦 AI 应用（具体产品、垂直场景解决方案）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|----------------|------------|
| [NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector) | 未显示总量 (+1079 today) | AI Agent 技能安全扫描器，检测恶意模式与漏洞，保障 Agent 安全。 |
| [shiyu-coder/Kronos](https://github.com/shiyu-coder/Kronos) | 未显示总量 (+396 today) | 专为金融市场语言构建的基础模型，可应用于量化分析与预测。 |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | 82,336 | 轻量级 OCR 工具，支持 100+ 语言，将图片/PDF 转化为结构化数据供 LLM 使用。 |
| [ScrapeGraphAI/Scrapegraph-ai](https://github.com/ScrapeGraphAI/Scrapegraph-ai) | 27,246 | 基于 AI 的网页爬虫，自动解析页面结构并提取信息。 |
| [acon96/home-llm](https://github.com/acon96/home-llm) | 1,360 | 用本地 LLM 控制智能家居的 Home Assistant 集成。 |
| [gluonfield/enchanted](https://github.com/gluonfield/enchanted) | 5,964 | iOS/macOS 原生聊天应用，对接 Ollama 提供的本地模型。 |

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|----------------|------------|
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,088 | 综合性 LLM 评测平台，支持 Llama、Qwen、GPT-4 等 100+ 模型。 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4,281 | 面向系统工程师的 LLM 推理服务课程，从零搭建类 vLLM+Qwen 的迷你推理栈。 |
| [zchoi/Awesome-Embodied-Robotics-and-Agent](https://github.com/zchoi/Awesome-Embodied-Robotics-and-Agent) | 1,815 | 具身智能与机器人结合 LLM 的研究资源列表，追踪最新论文。 |
| [llm-jp/awesome-japanese-llm](https://github.com/llm-jp/awesome-japanese-llm) | 1,409 | 日本語 LLM 资源汇总，覆盖模型、数据集、工具。 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|----------------|------------|
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,796 | 云原生向量数据库，专为大规模向量 ANN 搜索设计。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 82,856 | 领先的开源 RAG 引擎，融合 Agent 能力构建上下文层。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 58,652 | AI Agent 的通用记忆层，支持持久化知识图谱。 |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | 11,960 | 在设备端实现 97% 存储压缩的 RAG 方案，强调隐私与效率。 |
| [safishamsi/graphify](https://github.com/safishamsi/graphify) | 67,745 | 将代码、文档、SQL 等转化为可查询知识图谱的 Agent 技能工具。 |

---

## 趋势信号分析

1. **Agent 安全与沙箱化成为基础设施级需求**：NVIDIA SkillSpector 和 trycua/cua 的“双杀”登榜，表明社区正从“如何构建 Agent”转向“如何安全地运行 Agent”。SkillSpector 的 +1079 stars 异常瞩目，预示着企业级 Agent 部署亟需配套的漏洞扫描、权限隔离、行为审计方案。

2. **“零成本数据获取”类 Agent 爆发**：Agent-Reach 单日新增 1100+ stars，其核心卖点是“零 API 费用”。结合近期 Twitter/X 等平台提高 API 定价的背景，这种通过浏览器自动化或公开接口爬取的方式，正在催生一批“开源数据代理”工具，为小型开发者和研究团队提供低成本替代方案。

3. **金融大模型走向细分领域**：Kronos 和 TradingAgents 分别从“基础模型预训练”和“多智能体交易”两个方向切入，显示出 LLM 在量化金融领域的专业化分工。Kronos 更是直接命名为“语言 of Financial Markets”，说明垂直领域预训练大模型（不同于通用 LLM）正获得社区认可。

4. **传统 ML 框架依旧坚挺，但注意力向 Agent 栈转移**：TensorFlow、PyTorch、scikit-learn 等仍占据高 stars，但今日搜索排名靠前的主题几乎全部围绕 ai-agent、llm-model、vector-db 等，反映新项目更偏重应用层与中间件，而非底层训练框架。

---

## 社区关注热点

- 🚨 **NVIDIA SkillSpector** — Agent 安全的第一个专用扫描工具，值得所有 Agent 开发者集成到 CI/CD 中。
- 🌐 **trycua/cua** — 计算机使用 Agent 的“虚拟机 + SDK”标准，可能成为未来 Agent 沙箱的事实标准。
- 🔍 **Agent-Reach** — 零 API 费用与多平台覆盖能力，适合需要构建舆情监控、内容聚合类应用的团队。
- 🏦 **Kronos + TradingAgents** — 金融 AI 是一个高价值赛道，这组项目正在构建从模型到交易链路的完整方案。
- 🧠 **LEANN + graphify** — RAG 领域正在从“检索文档”进化到“知识图谱+压缩存储”，性能和隐私双提升。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*