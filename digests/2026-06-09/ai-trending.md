# AI 开源趋势日报 2026-06-09

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-06-09 02:45 UTC

---

# AI 开源趋势日报 (2026-06-09)

## 今日速览

今日 GitHub 热点高度集中在 **AI Agent 技能化**与**向量/记忆基础设施**两大方向。Trending 榜单中，Agent 技能商店（`last30days-skill`、`pm-skills`）、本地运行 LLM 评估工具（`whichllm`）和开源记忆系统（`MemPalace`）获得爆发性增长；同时，基于 Rust 的向量索引库 `turbovec` 新增超 1700 stars，反映社区对高性能向量引擎的迫切需求。Claude Code 生态持续扩大，相关技能和指南项目（`google/skills`、`claude-howto`）热度不减。总体来看，AI 开源正从通用框架向“可插拔技能 + 持久记忆”的模块化架构演进。

## 各维度热门项目

### 🔧 AI 基础工具
- **[turbovec](https://github.com/RyanCodrai/turbovec)** ⭐0 (+1729 today)  
  Rust 编写、Python 绑定的高性能向量索引库，基于 TurboQuant 量化技术，专为大规模向量检索优化。
- **[whichllm](https://github.com/Andyyyy64/whichllm)** ⭐0 (+143 today)  
  一键评测本地 LLM 性能的工具，按真实基准（而非参数数量）排序，帮助开发者找到最适合硬件的模型。
- **[roboflow/supervision](https://github.com/roboflow/supervision)** ⭐0 (+1288 today)  
  可复用的计算机视觉工具库，提供标注、追踪、可视化等模块，降低 CV 应用开发门槛。
- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐82,262  
  高吞吐、内存高效的 LLM 推理引擎，支持多模型部署与 PagedAttention，已成为生产级推理标准。
- **[ultralytics/ultralytics](https://github.com/ultralytics/ultralytics)** ⭐58,159  
  YOLOv8 及后续系列的统一框架，集训练、推理、部署于一体，是 CV 领域最热门的工具之一。

### 🤖 AI 智能体/工作流
- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** ⭐0 (+3558 today)  
  AI Agent 技能模块，可跨 Reddit、X、YouTube 等平台研究任意主题并合成摘要，是今日新增 stars 最高的项目。
- **[aaif-goose/goose](https://github.com/aaif-goose/goose)** ⭐0 (+699 today)  
  开源可扩展 AI Agent，支持安装、执行、编辑和测试，不限于代码补全，兼容任意 LLM。
- **[CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)** ⭐0 (+378 today)  
  面向 Agent 和生成式 UI 的前端框架，支持 React、Angular、移动端和 Slack，定义 AG-UI 协议。
- **[google/skills](https://github.com/google/skills)** ⭐0 (+461 today)  
  Google 官方发布的 Agent 技能集合，涵盖 Google 产品和技术，标志着大厂推动 Agent 技能标准化。
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐187,545  
  “与你一起成长的 Agent”框架，强调记忆与持续学习，是社区最受关注的 Agent 项目之一。
- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐184,851  
  流行 AI 自主代理框架，支持任务规划、工具调用，持续引领 Agent 思潮。

### 📦 AI 应用
- **[Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach)** ⭐0 (+679 today)  
  CLI 工具，为 AI Agent 提供“看到整个互联网”的能力，零 API 费用即可搜索 Twitter、Reddit、B站等。
- **[santifer/career-ops](https://github.com/santifer/career-ops)** ⭐0 (+308 today)  
  AI 驱动的求职系统，基于 Claude Code，内含 14 种技能模式、Go 仪表盘和 PDF 生成，垂直场景明确。
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐47,083  
  智能聊天、自主 Agent、300+ 助手集成于一身的 AI 生产力工作室，统一访问前沿 LLM。
- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐41,403  
  LLM 驱动的股票分析系统，支持 A/H/美股行情、实时新闻、LLM 决策仪表盘，零成本定时运行。
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐25,319  
  AI 从任意文档生成可编辑 PPT，保留原生图形和动画，支持自定义模板，提升办公效率。
- **[luongnv89/claude-howto](https://github.com/luongnv89/claude-howto)** ⭐0 (+312 today)  
  Claude Code 可视化实战指南，从基础到高级 Agent，附即用模板，是学习 Claude Code 生态的最佳入口。

### 🧠 大模型/训练
- **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)** ⭐72,005  
  统一高效微调框架，支持 100+ 大语言模型和多模态模型（ACL 2024），是微调领域的标杆。
- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,068  
  大模型评估平台，支持 100+ 数据集和多种模型（Llama3、GPT-4、Qwen 等），提供标准化评测。
- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐251  
  可靠、最小化、可扩展的基础模型预训练库，专注于世界模型和基础模型的稳定训练。
- **[tiny-llm](https://github.com/skyzh/tiny-llm)** ⭐4,258  
  面向系统工程师的 LLM 推理课程，在 Apple Silicon 上构建精简版 vLLM + Qwen，兼具教学与实用。

### 🔍 RAG/知识库
- **[MemPalace/mempalace](https://github.com/MemPalace/mempalace)** ⭐0 (+170 today)  
  开源 AI 记忆系统，号称基准测试最佳且免费，为 Agent 提供跨会话的持久记忆。
- **[langgenius/dify](https://github.com/langgenius/dify)** ⭐144,456  
  生产级 Agent 工作流开发平台，支持 RAG、工具调用、可视化编排，社区活跃度极高。
- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐82,235  
  领先开源 RAG 引擎，融合 Agent 能力与高质量上下文层，适用于企业文档问答。
- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐44,687  
  云原生向量数据库，高性能 ANN 搜索，是 RAG 系统中最常用的向量存储之一。
- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** ⭐81,317  
  Agent 跨会话持久上下文系统，自动压缩并注入相关记忆，兼容 Claude Code、Codex 等多种 Agent。
- **[meilisearch/meilisearch](https://github.com/meilisearch/meilisearch)** ⭐58,012  
  闪电般快速的搜索引擎，支持 AI 混合搜索，可轻松集成到 RAG 应用中。

## 趋势信号分析

今日最显著的趋势是 **Agent 技能市场**的兴起。`last30days-skill`（+3558）、`pm-skills`（+164）、`google/skills`（+461）等项目的爆发，表明社区正从构建通用 Agent 框架转向封装可复用的垂直技能——每个技能代理特定任务（如社交媒体研究、项目管理、谷歌产品操作）。这种“乐高式” Agent 生态降低了 AI 落地的门槛，也催生了类似 `Agent-Reach` 的开放网络接口工具。

另一个值得关注的信号是 **向量索引的 Rust 化**。`turbovec` 凭借 Rust 的高性能和 TurboQuant 量化技术，在今日新增 1729 stars，反映出大规模向量检索场景对效率的极致追求。同时，`MemPalace` 和 `claude-mem` 等记忆系统的涌现，说明“Agent 记忆”已成为刚需——不再依赖上下文窗口，而是通过持久化知识图谱或向量存储实现长期记忆。

此外，**本地 LLM 评估工具**（`whichllm`）和 **Claude Code 生态**（`claude-howto`、`google/skills`）持续受到关注。前者帮助用户在硬件限制下找到最优模型，后者依托 Anthropic 平台汇聚官方和社区技能，正形成类似“App Store”的新型分发模式。整体来看，AI 开源正从单一模型/框架竞争进入“基础设施+技能+记忆”的复合生态阶段。

## 社区关注热点

- **Agent 技能化与 Marketplace**：`last30days-skill`、`pm-skills` 等项目的爆发表明，可插拔的 Agent 技能正在成为新范式，开发者应关注技能创建、发布和组合的标准（如 AG-UI 协议）。
- **高性能向量索引库**：`turbovec` 的 Rust + 量化方案值得深入，尤其适合需要超低延迟的实时检索场景（如搜索、RAG）。
- **AI 记忆与上下文管理**：`MemPalace`、`claude-mem` 等项目揭示了跨会话记忆的重要性，未来 Agent 的竞争力将部分取决于记忆系统的鲁棒性和效率。
- **Claude Code 生态扩展**：`google/skills` 和 `claude-howto` 的走红意味着 Anthropic 正加速构建企业级 Agent 技能网络，开发者可提前布局相关技能开发。
- **本地 LLM 效能评估**：`whichllm` 以“一键跑分”解决了选择本地模型的痛点，结合 `vLLM`、`tiny-llm` 等推理工具，本地 AI 部署的实用化门槛进一步降低。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*