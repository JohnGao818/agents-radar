# AI 开源趋势日报 2026-07-04

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-04 02:32 UTC

---

# AI 开源趋势日报 | 2026-07-04

---

## 1. 今日速览

- **AI 安全工具爆发**：开源渗透测试智能体 `strix` 单日新增 2,800+ stars，社区对应用安全自动化需求强烈。
- **智能体技能生态趋热**：`superpowers`、`agency-agents`、`agentskills` 三个技能框架/规范项目合计新增近 3,000 stars，标志着 Agent 从单体工具向模块化技能组合演进。
- **Token 效率成刚需**：`caveman` 以“用更少 token 说话”的幽默方式实现 65% 压缩，单日新增 2,800+ stars，低成本推理需求持续升温。
- **Claude Code 生态扩展**：`codex-plugin-cc` 和 `chrome-devtools-mcp` 分别让 Claude Code 获得跨工具协同与浏览器调试能力，开发者对 Agent 集成平台关注度上升。
- **记忆与 RAG 持续演进**：`claude-mem` 突破 85k stars，`cognee`、`mem0` 等项目推动跨会话持久记忆成为 Agent 标配。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 101k+ | +293 | 全球最流行的深度学习框架，今日因 GPU 加速更新获关注。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 85.3k | - | 高吞吐、内存高效的 LLM 推理引擎，生产级部署首选。 |
| [ollama/ollama](https://github.com/ollama/ollama) | 175k | - | 一键运行本地大模型（支持 Kimi、GLM、DeepSeek 等），个人推理入口。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | 162k | - | 多模态模型库，社区新模型持续接入。 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | 7.8k | - | Rust 生态中构建模块化 LLM 应用的框架，语言性能优势渐显。 |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | 313 | - | 设备端 LLM 推理引擎（X-Bit 量化），适合边缘部署。 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [usestrix/strix](https://github.com/usestrix/strix) | 0+2.8k | +2,803 | 开源 AI 渗透测试工具，自动发现并修复漏洞，应用安全自动化新范式。 |
| [obra/superpowers](https://github.com/obra/superpowers) | 0+1.2k | +1,209 | Agentic 技能框架与软件开发方法论，推动 Agent 能力模块化。 |
| [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents) | 0+1.2k | +1,208 | 集众智能体于一身（前端、Reddit、创意等），一站式 AI 代理团队。 |
| [agentskills/agentskills](https://github.com/agentskills/agentskills) | 0+406 | +406 | Agent 技能规范与文档，为标准化 Agent 技能提供参考实现。 |
| [anthropics/claude-code](https://github.com/anthropics/claude-code) | 0+221 | +221 | 终端 Agent 编程工具，理解代码库并自动完成 Git 工作流。 |
| [ogulcancelik/herdr](https://github.com/ogulcancelik/herdr) | 0+478 | +478 | 终端 Agent 多路复用器，同时管理多个 Agent 会话。 |
| [TencentCloud/CubeSandbox](https://github.com/TencentCloud/CubeSandbox) | 0+60 | +60 | 即时、并发、轻量级 AI Agent 沙箱，保障 Agent 安全隔离。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 208.7k | - | 持续进化的通用 Agent，社区最活跃的 Agent 项目之一。 |

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) | 83k / 0+2.8k | +2,863 | Claude Code 技能：用原始语言减少 65% token，低成本推理利器。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 48.1k | - | AI 生产力工作室，集成 300+ 助手与自主 Agent，统一前端入口。 |
| [ChromeDevTools/chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp) | 0+405 | +405 | 为编码 Agent 提供 Chrome 调试能力，Agent 浏览器自动化新工具。 |
| [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc) | 0+634 | +634 | 从 Claude Code 调用 OpenAI Codex 进行代码审查，跨模型协作示例。 |
| [santifer/career-ops](https://github.com/santifer/career-ops) | 58.4k | - | AI 驱动的求职系统，14 种技能模式，批量生成简历与申请。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 36.4k | - | 从文档自动生成可编辑 PPT，包含原生动画与语音旁白。 |

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | 52.5k | - | 从零训练 64M 小模型，2 小时即可复现，降低 LLM 入门门槛。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7.2k | - | 支持 100+ 数据集的 LLM 评测平台，模型选型必备。 |
| [testtimescaling/testtimescaling.github.io](https://github.com/testtimescaling/testtimescaling.github.io) | 107 | - | 对 LLM test-time scaling 的全面调研，指导推理时延长思考。 |
| [Eigenwise/atomic-agents](https://github.com/Eigenwise/atomic-agents) | 6.0k | - | 以原子化方式构建 Agent，强调可组合性与可测试性。 |
| [harvard-edge/cs249r_book](https://github.com/harvard-edge/cs249r_book) | 0+793 | +793 | 哈佛《机器学习系统》课程教材电子版，系统设计思维资源。 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 84.2k | - | 领先的开源 RAG 引擎，融合 Agent 能力，构建高质量上下文层。 |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 77.2k | - | 将代码文件、SQL 模式、文档等转化为可查询知识图谱，Agent 知识库利器。 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 85.7k | - | 跨会话持久上下文，自动压缩并注入相关记忆，Agent 记忆标准方案。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 45.1k | - | 高性能云原生向量数据库，支撑大规模语义搜索。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 32.9k | - | 高可扩展向量搜索引擎，适合实时 AI 检索场景。 |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | 12.6k | - | 97% 存储压缩的个人设备 RAG，兼顾隐私与效率。 |

---

## 3. 趋势信号分析

从今日热榜可提炼出三个核心趋势：

- **Agent 技能生态爆发**：`superpowers`、`agency-agents`、`agentskills` 三个项目同时登榜，且总新增超 2,800 stars，表明社区正从单个 Agent 工具转向标准化技能市场。这类似于 iOS App Store 的早期阶段——Agent 能力的可插拔、可组合成为下一波竞争焦点。
- **Token 效率成 Agent 实用化关键**：`caveman` 用荒诞方式直击痛点——大模型 token 成本仍是 Agent 规模化瓶颈。结合 `headroom`（压缩工具输出）、`claude-mem`（记忆去冗余）等项目，一个“Token 降本”技术栈正在形成。
- **安全与调试基础设施起步**：`strix`（渗透测试）、`CubeSandbox`（沙箱隔离）、`chrome-devtools-mcp`（调试）表明，企业级 Agent 部署需要配套安全、隔离、可观测性工具。这与近期企业大量采用 Claude Code 等 Agent 编码助手的事件直接相关——生产力提升后，安全与治理短板立即凸显。

另外，`openai/codex-plugin-cc` 代表跨模型协作趋势（Claude + Codex），反映了开发者希望在不同 Agent 系统间自由组合能力。

---

## 4. 社区关注热点

- **🔐 `usestrix/strix`**：AI 安全测试自动化，单日 2.8k stars，适合关注应用安全与 AI 合规的团队研究。
- **🛠 `obra/superpowers` + `agency-agents`**：Agent 技能框架的两种不同思路，前者重方法论，后者重开箱即用，值得对比学习。
- **🧠 `caveman`**：Token 优化极简方案，启发 Agent 设计中的成本意识，可以快速集成到 Claude Code 工作流。
- **📚 `harvard-edge/cs249r_book`**：系统学习 ML 系统设计的最佳教材之一，适合想深入 Agent 底层架构的开发者。
- **🔗 `claude-mem`**：跨 Agent 记忆方案已获 85k stars，持久上下文是 Agent 从“工具”走向“副手”的关键，建议参与或集成。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*