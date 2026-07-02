# AI 开源趋势日报 2026-07-02

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-02 02:52 UTC

---

# 《AI 开源趋势日报》2026-07-02

## 📰 今日速览

今日 AI 开源领域呈现 **Agent 生态爆发**与 **垂直场景落地**的双重趋势：Trending 榜单中涌现多个高星 Agent 项目，从全功能 Agency 到渗透测试、交易决策、多模态编排等细分方向均有突破；同时，**AI 安全与隐私**相关工具（如渗透测试、沙箱）获得社区强烈关注；大模型基础设施方面，PDF 线性化工具（olmocr）和神经输入法（karukan）等小众创新也崭露头角。此外，OmniRoute 聚合 231+ 提供商的服务网关成为开发者降低 LLM 调用成本的热门选择。

---

## 🔧 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐175,253 | 一键运行本地大模型，支持 Kimi、GLM、DeepSeek 等最新模型，是本地推理的首选工具。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐85,070 | 高吞吐、低延迟的 LLM 推理引擎，适合生产级部署。 |
| [allenai/olmocr](https://github.com/allenai/olmocr) | ⭐0 (+334 today) | 将 PDF 线性化为 LLM 可直接处理的文本格式，为训练数据集准备提供标准化工具。 |
| [togatoga/karukan](https://github.com/togatoga/karukan) | ⭐0 (+42 today) | 基于神经网络的日语输入法引擎（假名-汉字转换），展现端侧小模型创新。 |
| [TencentCloud/CubeSandbox](https://github.com/TencentCloud/CubeSandbox) | ⭐0 (+79 today) | 为 AI Agent 设计的即时、并发、安全轻量级沙箱，解决 Agent 执行环境隔离问题。 |
| [diegosouzapw/OmniRoute](https://github.com/diegosouzapw/OmniRoute) | ⭐0 (+1010 today) | 统一 AI 网关，一个端点接入 231+ 提供商（含 50+ 免费），支持智能回退和超强 token 压缩。 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents) | ⭐0 (+2114 today) | 全功能 AI Agency，内置前端专家、Reddit 运营、幽默注入等多样化 Agent，今日新增星数最高。 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐185,243 | 经典通用 Agent 框架，持续迭代，目标让 AI 人人可用。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | ⭐140,679 | Agent 工程化平台，提供工具调用、记忆、多 Agent 编排等完整能力。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | ⭐102,028 | 让 AI Agent 像人一样操作浏览器，自动化在线任务。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | ⭐79,044 | AI 驱动的软件开发助手，可自主编码、调试、部署。 |
| [ogulcancelik/herdr](https://github.com/ogulcancelik/herdr) | ⭐0 (+609 today) | 终端中的 Agent 多路复用器，支持同时管理多个 Agent 会话。 |
| [0xNyk/council-of-high-intelligence](https://github.com/0xNyk/council-of-high-intelligence) | ⭐0 (+161 today) | 18 个 AI 人格（亚里士多德、费曼等）进行多轮结构化 deliberation，跨 LLM 提供商。 |

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [usestrix/strix](https://github.com/usestrix/strix) | ⭐0 (+1211 today) | 开源 AI 渗透测试工具，自动发现并修复应用漏洞。 |
| [Unclecheng-li/VulnClaw](https://github.com/Unclecheng-li/VulnClaw) | ⭐0 (+132 today) | 基于 AI Agent + MCP 工具链的渗透全流程自动化，自然语言输入到报告生成。 |
| [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading) | ⭐0 (+694 today) | 个人交易 Agent，结合市场数据与 LLM 分析，辅助投资决策。 |
| [altic-dev/FluidVoice](https://github.com/altic-dev/FluidVoice) | ⭐0 (+572 today) | macOS 最快的本地听写应用，含自训练 AI 增强模型，对标 Wispr Flow。 |
| [browser-use/video-use](https://github.com/browser-use/video-use) | ⭐0 (+693 today) | 让编码 Agent 直接编辑视频，拓展 AI 在多媒体领域的自动化能力。 |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | ⭐143,739 | 用户友好的 AI 聊天界面，支持 Ollama、OpenAI 等多后端。 |

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | ⭐72,883 | 统一高效的 100+ LLM/VLM 微调框架（ACL 2024），支持 LoRA、QLoRA 等。 |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | ⭐52,445 | 2 小时从零训练 64M 参数小模型，适合入门学习和快速实验。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,142 | 全面的大模型评测平台，支持主流模型和 100+ 数据集。 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | ⭐7,805 | Rust 语言的模块化 LLM 应用构建框架，注重性能和安全性。 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐84,077 | 领先的开源 RAG 引擎，融合 Agent 能力，提供高质量上下文层。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐45,040 | 高性能云原生向量数据库，支撑大规模相似性搜索。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐59,874 | 通用 AI Agent 记忆层，实现跨会话持久化记忆。 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐85,396 | 为 Claude Code、Codex 等 Agent 提供持久上下文压缩与注入，解决会话记忆问题。 |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | ⭐62,416 | 本地优先的 Agent 体验，支持文档、网站、数据库等多元知识源。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | ⭐32,870 | 高性能向量搜索引擎，专为下一代 AI 设计。 |

---

## 📈 趋势信号分析

1. **Agent 生态呈现“分工专业化”爆发**：今日 Trending 中 agency-agents 以 2114 星高居榜首，展示了预置多种角色（前端、内容、市场等）的完整 Agent 平台正获得社区认可。同时 herdr（终端多路复用）、council-of-high-intelligence（多智能体 deliberation）等细分工具表明开发者正在从单一 Agent 向多 Agent 协作演进。

2. **AI 安全与渗透测试成为新兴热点**：strix（+1211星）和 VulnClaw（+132星）均聚焦 AI 辅助安全测试，反映了 LLM 能力的“攻防两面性”——开发者既利用 AI 发现漏洞，也需防范 AI 带来的新风险。CubeSandbox 的沙箱方案则提供了运行 Agent 的安全隔离环境。

3. **“便宜 + 多模型”网关模式走红**：OmniRoute（+1010星）以单端点聚合 231+ 提供商、支持 50+ 免费模型，并声称节省 15-95% token，直击当前 LLM 调用成本痛点，或将成为开发者接入多模型的标准层。

4. **小模型与端侧推理回暖**：karukan（神经输入法）、FluidVoice（本地听写）以及 minimind（2小时训练）等项目，显示出社区对高效、轻量、易部署的模型和应用的兴趣回升，这与近期边缘 AI 和隐私保护趋势相呼应。

5. **垂直场景 AI 应用快速落地**：Vibe-Trading（交易）、video-use（视频编辑）、AiToEarn（赚钱）等项目表明，开发者正将 AI Agent 直接嵌入金融、创意、副业等实际场景，从“玩具”走向“工具”。

---

## 🔭 社区关注热点

- **⚡ agency-agents**：全功能 AI Agency 概念，预置 9 种专业 Agent 角色，今日新增星数最高（+2114），值得研究其 Agent 分工与协作设计。
- **🛡️ strix vs VulnClaw**：两个 AI 渗透测试项目同日上榜，表明 AI 安全工具正成为刚需，可对比其技术路线（strix 更专注扫描，VulnClaw 强调全流程 Agent 编排）。
- **🌐 OmniRoute**：聚合 231+ 提供商且支持免费模型，对中小开发者降低 LLM 使用门槛意义重大，关注其 token 压缩和多模型回退机制。
- **🧠 claude-mem**：为多种 Agent 提供持久记忆的压缩注入方案（85K+ stars），解决了 Agent 长期运行的上下文丢失问题，是 RAG 与 Agent 结合的关键组件。
- **🎥 browser-use/video-use**：将浏览器自动化经验迁移到视频编辑，展示 Agent 从“文本操作”向“多模态内容处理”的拓展趋势。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*