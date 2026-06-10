# AI 开源趋势日报 2026-06-10

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-10 02:58 UTC

---

# AI 开源趋势日报 2026-06-10

---

## 1. 今日速览

今日 GitHub Trending 中 **AI Agent 技能与工具包** 成为绝对主角，多个以“skill”命名的项目单日增长超千星，折射出社区对 **可组合、可复用的 Agent 能力模块** 的强烈需求。向量索引与本地 LLM 选型工具也迎来波峰，Turbovec 凭借 Rust 实现的高性能向量索引亮相即获 1800+ star。与此同时，主题搜索榜中 `hermes-agent`、`AutoGPT` 等老牌 Agent 框架持续领跑，而 **RAG 与记忆层** 方向（如 `mem0ai`、`thedotmack/claude-mem`）的密集出现标志着“让 Agent 记住你”正在成为基建级需求。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

- **[RyanCodrai/turbovec](https://github.com/RyanCodrai/turbovec)**  
  ⭐ 0（+1801 today）  
  基于 TurboQuant 量化算法的向量索引库，Rust 核心 + Python 绑定，主打高性能与低内存占用，为本地 RAG 提供轻量级索引方案。

- **[Andyyyy64/whichllm](https://github.com/Andyyyy64/whichllm)**  
  ⭐ 0（+633 today）  
  一键运行并评测评测本地 LLM 实际性能，基于实时基准而非参数数量排序，解决“哪款模型能在我的设备上跑快”的痛点。

- **[roboflow/supervision](https://github.com/roboflow/supervision)**  
  ⭐ 0（+733 today）  
  可复用的计算机视觉工具集，封装标注、跟踪、过滤等常用管线，降低 CV 项目落地门槛。

- **[opencv/opencv](https://github.com/opencv/opencv)**  
  ⭐ 0（+102 today）  
  经典开源计算机视觉库，持续更新以适配 AI 工作流，今日仍获社区关注。

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)**  
  ⭐ 82,365  
  高吞吐、低显存的 LLM 推理引擎，支持 PagedAttention 和连续批处理，是部署大模型的标配。

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)**  
  ⭐ 0（+3191 today）  
  AI Agent 技能——聚合 Reddit、X、YouTube、HN 等信息源，自动生成接地气的综合摘要，展示“技能化” Agent 的高效。

- **[aaif-goose/goose](https://github.com/aaif-goose/goose)**  
  ⭐ 0（+489 today）  
  开源可扩展 AI Agent，超越代码补全，支持安装、执行、编辑和测试，对接任意 LLM，强调“全能型”执行能力。

- **[adddyosmani/agent-skills](https://github.com/adddyosmani/agent-skills)**  
  ⭐ 0（+443 today）  
  生产级工程技能集合，专为 AI 编码 Agent 设计，涵盖代码审查、测试生成、部署脚本等，推动 Agent 技能标准化。

- **[phuryn/pm-skills](https://github.com/phuryn/pm-skills)**  
  ⭐ 0（+806 today）  
  PM 技能市场：100+ 个 Agent 技能（发现、策略、执行、增长），将产品管理流程分解为可复用的 Agent 命令。

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)**  
  ⭐ 188,947  
  与用户共同成长的 Agent 框架，注重长期记忆与自适应能力，是社区中最受关注的 Agent 底座之一。

- **[bytedance/deer-flow](https://github.com/bytedance/deer-flow)**  
  ⭐ 70,837  
  字节跳动开源的长时间跨度 SuperAgent，整合沙箱、记忆、工具、子 Agent 和消息网关，可处理分钟至小时级任务。

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

- **[santifer/career-ops](https://github.com/santifer/career-ops)**  
  ⭐ 51,794（+1110 today）  
  基于 Claude Code 的 AI 求职系统，集成 14 种技能模式、Go 仪表盘、PDF 生成，将求职全流程自动化。

- **[maziyarpanahi/openmed](https://github.com/maziyarpanahi/openmed)**  
  ⭐ 0（+191 today）  
  开源医疗 AI 方案，覆盖诊断辅助、病历分析等场景，推动 AI 在垂直行业的落地。

- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)**  
  ⭐ 47,138  
  AI 生产力工作室，集智能对话、自主 Agent、300+ 助理于一体，统一访问前沿 LLM。

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)**  
  ⭐ 82,333  
  领先的开源 RAG 引擎，融合 Agent 能力与 RAG，为企业提供 LLM 上下层，适合快速搭建知识问答系统。

- **[FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise)**  
  ⭐ 53,440  
  可视化 AI Agent 构建工具，拖拽式搭建 LLM 工作流，降低 Agent 开发门槛。

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

- **[ollama/ollama](https://github.com/ollama/ollama)**  
  ⭐ 173,720  
  本地运行大模型的标杆工具，支持 Kimi、DeepSeek、Qwen 等主流模型，一键启动。

- **[huggingface/transformers](https://github.com/huggingface/transformers)**  
  ⭐ 161,461  
  SOTA 模型库与训练框架，支撑文本、视觉、多模态的推理与训练，是 AI 生态的基石。

- **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)**  
  ⭐ 72,036  
  统一高效微调 100+ LLM 与 VLM 的工具，支持 LoRA、QLoRA、全参微调等，被 ACL 2024 收录。

- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)**  
  ⭐ 4,264  
  面向系统工程师的 LLM 推理服务课程，从头构建类 vLLM 引擎，具有极高教学价值。

- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)**  
  ⭐ 251（今日新增？）  
  可靠、可扩展的预训练库，聚焦基础模型与世界模型，适合研究者快速启动训练。

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)**  
  ⭐ 44,706  
  高性能云原生向量数据库，支持大规模 ANN 搜索，是 RAG 系统首选后端之一。

- **[qdrant/qdrant](https://github.com/qdrant/qdrant)**  
  ⭐ 31,984  
  下一代向量搜索引擎，支持过滤、高可用、云原生产品，适合生产级 RAG。

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)**  
  ⭐ 58,210  
  Agent 的通用记忆层，提供持久化上下文与长期记忆，让 Agent 跨会话保持连贯。

- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)**  
  ⭐ 81,499  
  跨会话上下文注入工具，捕获 Agent 行为后用 AI 压缩并注入回未来对话，支持 Claude Code、OpenClaude 等。

- **[safishamsi/graphify](https://github.com/safishamsi/graphify)**  
  ⭐ 64,305  
  将代码、SQL、文档等文件夹转化为可查询知识图谱，打通代码库与知识库的边界。

---

## 3. 趋势信号分析

今日社区爆发性关注的焦点集中在 **“Agent 技能”** 与 **“本地化工具”** 两个方向。`last30days-skill`、`agent-skills`、`pm-skills` 等以“skill”命名的项目单日合计获得近 5000 星，反映出开发者不再满足于单一的 Agent 框架，而是渴望可组合、可复用的能力模块——这标志着 **Agent 开发生态正从“造轮子”进入“搭积木”阶段**。同时，`turbovec` 和 `whichllm` 的崛起表明：当本地 LLM 普及后，**高性能轻量级索引** 和 **硬件感知的模型选型工具** 成为新的基础设施短板，社区正在快速填补。值得注意的是，`system-prompts-and-models-of-ai-tools` 这样的“元资源”项目也获得关注，暗示 **Agent 行为的透明化与可审计性** 正成为值得重视的新方向。与近期 OpenAI 插件生态、Claude Code 普及等事件相呼应，**“技能化 Agent + 记忆层 + 本地推理”** 的技术栈今日已经清晰浮现。

---

## 4. 社区关注热点

- **`mvanhorn/last30days-skill`（+3191 today）**  
  作为“技能”类项目的领头羊，它展示了 Agent 如何快速聚合多源信息并生成可读摘要，**“信息合成”是 Agent 最直接的价值出口**，值得所有 Agent 开发者参考其设计模式。

- **`RyanCodrai/turbovec`（+1801 today）**  
  Rust 编写的向量索引首次亮相即引爆社区，其 TurboQuant 算法可能成为边缘设备上 RAG 的加速方案，**关注其与 LanceDB、Chroma 等老牌向量库的性能对比**。

- **`santifer/career-ops`（+1110 today）**  
  将 Agent 能力完全耦合到具体求职场景，15 种技能模式 + 仪表盘 + PDF 生成，**垂直领域 Agent 应用是商业化最容易落地的方向**。

- **`thedotmack/claude-mem`（81,499 stars）**  
  跨会话记忆方案近期热度飙升，标志着 **“记忆”正从实验特性变成 Agent 标配**，与 mem0 等一起推动 Agent 学习能力进化。

- **`aaif-goose/goose`（+489 today）**  
  开源、可扩展、非代码限制的通用 Agent，**其“执行一切任务”的设计思路可能成为下一代个人 AI 助手的雏形**，与 Codex、Claude Code 形成竞争。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*